---
title: 값 형식과 참조 의미 체계
description: 구조 복사를 안전하게 최소화하는 언어 기능 이해
author: billwagner
ms.author: wiwagn
ms.date: 11/10/2017
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.custom: mvc
ms.openlocfilehash: 778897dc92f8a94178ebbbed7704c0dfe2397729
ms.sourcegitcommit: 935d5267c44f9bce801468ef95f44572f1417e8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="reference-semantics-with-value-types"></a>값 형식과 참조 의미 체계

값 형식을 사용할 경우의 장점은 대개 힙 할당을 할 필요가 없다는 것입니다.
단점은 값 형식이 값으로 복사된다는 점입니다. 이러한 장단점 간에 균형을 잡으려고 하니 많은 양의 데이터에서 작동하는 알고리즘을 최적화하기가 어렵습니다. C# 7.2의 새로운 언어 기능은 값 형식으로 pass-by-reference 의미 체계를 가능하게 하는 메커니즘을 제공합니다. 이러한 기능을 현명하게 사용하여 할당 및 복사 작업을 최소화하세요. 이 문서에서는 이러한 새로운 기능을 살펴봅니다.

이 문서의 샘플 코드 상당수는 C# 7.2에 추가된 기능을 보여 줍니다. 이러한 기능을 사용하려면 C# 7.2 이상을 사용하도록 프로젝트를 구성해야 합니다. Visual Studio를 사용하여 선택할 수 있습니다. 각 프로젝트에 대해 메뉴에서 **프로젝트**를 선택한 다음 **속성**을 선택합니다. **빌드** 탭을 선택하고 **고급**을 클릭합니다. 여기서 언어 버전을 구성합니다. “7.2” 또는 “latest”를 선택합니다.  또는 *csproj* 파일을 편집하고 다음 노드를 추가할 수 있습니다.

```XML
  <PropertyGroup>
    <LangVersion>7.2</LangVersion>
  </PropertyGroup>
```

값에 “7.2” 또는 “latest”를 사용할 수 있습니다.

## <a name="passing-arguments-by-readonly-reference"></a>읽기 전용 참조로 인수 전달

C# 7.2에서는 기존 `ref` 및 `out` 키워드를 보완하기 위해 `in` 키워드를 추가하여 참조로 인수를 전달합니다. `in` 키워드는 인수를 참조로 전달하도록 지정하지만 호출된 메서드는 값을 수정하지 않습니다. 

이 추가는 설계 의도를 표현하기 위한 완벽한 어휘를 제공합니다. 메서드 서명에 다음 한정자 중 어떤 것도 지정하지 않으면 호출된 메서드에 전달될 때 값 형식이 복사됩니다. 이러한 각 한정자는 값 형식이 참조로 전달되도록 지정하여 복사를 방지합니다. 각 한정자는 각기 다른 의도를 표현합니다.

- `out`: 이 메서드는 이 매개 변수로 사용되는 인수의 값을 설정합니다.
- `ref`: 이 메서드는 이 매개 변수로 사용되는 인수의 값을 설정할 수 있습니다.
- `in`: 이 메서드는 이 매개 변수로 사용되는 인수의 값을 수정하지 않습니다.

참조로 인수를 전달하기 위해 `in` 한정자를 추가하고 불필요한 복사를 방지하기 위해 참조로 인수를 전달할 디자인 의도를 선언합니다. 해당 인수로 사용되는 개체를 수정하려는 의도를 갖지 않습니다. 다음 코드는 3D 공간에서 두 점 사이의 거리를 계산하는 메서드의 예를 보여 줍니다. 

[!code-csharp[InArgument](../../samples/csharp/reference-semantics/Program.cs#InArgument "Specifying an In argument")]

인수는 각각 세 개의 double을 포함하는 두 개의 구조입니다. double은 8바이트이므로 각 인수는 24바이트입니다. `in` 한정자를 지정하여 컴퓨터 아키텍처에 따라 해당 인수에 4바이트 또는 8바이트 참조를 전달합니다. 크기의 차이는 작지만, 응용 프로그램이 다양한 값을 사용하여 연속 루프에서 이 메서드를 호출하면 빠르게 늘어날 수 있습니다.
 
`in` 한정자는 `out` 및 `ref`를 다른 방식으로도 보완합니다. `in`, `out` 또는 `ref`가 있는 경우에만 다른 메서드의 오버로드를 만들 수 없습니다. 이러한 새 규칙은 항상 `out` 및 `ref` 매개 변수에 대해 정의된 같은 동작을 확장합니다.

`in` 한정자는 메서드, 대리자, 람다, 로컬 함수, 인덱서, 연산자 매개 변수를 사용하는 모든 멤버에 적용될 수 있습니다.

`ref` 및 `out` 인수와 달리 `in` 매개 변수에 대한 인수에 리터럴 값 또는 상수를 사용할 수 있습니다. 또한 `ref` 또는 `out` 매개 변수와 달리 호출 사이트에서 `in` 한정자를 적용할 필요가 없습니다. 다음 코드는 `CalculateDistance` 메서드를 호출하는 두 가지 예를 보여 줍니다. 첫 번째 예에서는 참조로 전달된 두 개의 로컬 변수를 사용합니다. 두 번째 예는 메서드 호출의 일부로 만들어진 임시 변수를 포함합니다. 

[!code-csharp[UseInArgument](../../samples/csharp/reference-semantics/Program.cs#UseInArgument "Specifying an In argument")]

컴파일러가 `in` 인수의 읽기 전용 특성이 강제 적용되도록 하는 여러 가지 방법이 있습니다.  먼저, 호출된 메서드는 `in` 매개 변수에 직접 할당할 수 없습니다. 값이 `struct` 형식일 때 `in` 매개 변수의 모든 필드에 직접 할당할 수 없습니다. 또한 `ref` 또는 `out` 한정자를 사용하여 모든 메서드에 `in` 매개 변수를 전달할 수 없습니다.
이러한 규칙은 필드가 `struct` 형식이고 매개 변수 또한 `struct` 형식인 경우 `in` 매개 변수의 모든 필드에 적용됩니다. 사실 이러한 규칙은 멤버 액세스의 모든 수준에서 형식이 `structs`인 경우 멤버 액세스의 여러 계층에 적용됩니다. 컴파일러는 `in` 인수로 전달된 `struct` 형식과 그 `struct` 멤버가 다른 메서드에 대한 인수로 사용될 경우 읽기 전용 변수가 되도록 합니다.

`in` 매개 변수를 사용하면 복사본 작성 시 발생할 수 있는 잠재적인 성능 비용을 방지할 수 있습니다. 어떤 메서드 호출의 의미 체계도 변경되지 않습니다. 따라서 호출 사이트에서 `in` 한정자를 지정할 필요가 없습니다. 그러나 호출 사이트에서 `in` 한정자를 생략하면 다음과 같은 이유로 인수의 복사본을 만들 수 있음을 컴파일러에 알립니다.

- 암시적 변환은 있지만 인수 유형에서 매개 변수 유형으로의 ID 변환이 아닙니다.
- 인수는 식이지만 알려진 저장소 변수는 없습니다.
- `in`의 유무의 따라 달라지는 오버로드가 있습니다. 이 경우에는 by 값 오버로드가 더 적합합니다.

이러한 규칙은 읽기 전용 참조 인수를 사용하도록 기존 코드를 업데이트할 때 유용합니다. 호출된 메서드 내에서 by 값 매개 변수를 사용하는 모든 인스턴스 메서드를 호출할 수 있습니다. 이러한 경우 `in` 매개 변수의 복사본이 만들어집니다. 컴파일러가 `in` 매개 변수에 대한 임시 변수를 만들 수 있으므로 사용자는 `in` 매개 변수에 대한 기본값을 지정할 수도 있습니다. 다음 코드에서는 원점(포인트 0,0)을 두 번째 점의 기본값으로 지정합니다.

[!code-csharp[InArgumentDefault](../../samples/csharp/reference-semantics/Program.cs#InArgumentDefault "Specifying defaults for an in parameter")]

컴파일러가 읽기 전용 인수를 참조로 전달하도록 하려면 다음 코드에 나와 있는 것처럼 호출 사이트의 인수에 `in` 한정자를 지정합니다. 

[!code-csharp[UseInArgument](../../samples/csharp/reference-semantics/Program.cs#ExplicitInArgument "Specifying an In argument")]

이 동작을 통해 성능 향상이 가능한 대규모 코드 베이스에서 시간이 지남에 따라 `in` 매개 변수를 보다 쉽게 채택할 수 있습니다. 먼저 메서드 서명에 `in` 한정자를 추가합니다. 그런 다음, 호출 사이트에 `in` 한정자를 추가하고 `readonly struct` 형식을 생성하여 컴파일러가 더 많은 위치에서 `in` 매개 변수의 방어 복사본을 만들지 않도록 할 수 있습니다.

`in` 매개 변수 지정은 참조 형식 또는 숫자 값과 함께 사용될 수도 있습니다. 그러나 두 경우 모두의 이점은 있다고 하더라도 아주 적습니다.

## <a name="ref-readonly-returns"></a>`ref readonly` return

참조로 값 형식을 반환하되, 호출자가 해당 값을 수정하지 못하게 할 수도 있습니다. `ref readonly` 한정자를 사용하여 해당 설계 의도를 표현합니다. 이 한정자는 기존 데이터에 대한 참조를 반환하지만, 수정을 허용하지 않음을 판독기에 알립니다. 

컴파일러는 호출자가 참조를 수정할 수 없음을 강제 적용합니다. 값을 직접 할당하려고 하면 컴파일 시간 오류가 발생합니다. 그러나 컴파일러는 멤버 메서드가 구조체의 상태를 수정하는지를 알 수 없습니다.
개체가 수정되지 않도록 컴파일러는 복사본을 만들고 해당 복사본을 사용하여 멤버 참조를 호출합니다. 모든 수정은 해당 방어 복사본에 대한 것입니다. 

`Point3D`를 사용하는 라이브러리에서는 흔히 코드 전체에서 원점을 사용할 가능성이 높습니다. 모든 인스턴스는 스택에 새 개체를 만듭니다. 상수를 만들고 참조로 반환하는 것이 유용할 수 있습니다. 그러나 내부 저장소에 대한 참조를 반환하는 경우 호출자가 참조된 저장소를 수정할 수 없도록 강제 적용하려고 할 수 있습니다. 다음 코드는 원점을 지정하는 `Point3D`에 `readonly ref`를 반환하는 읽기 전용 속성을 정의합니다.

[!code-csharp[OriginReference](../../samples/csharp/reference-semantics/Point3D.cs#OriginReference "Creating a readonly Origin reference")]

ref readonly return의 복사본을 만들기는 쉽습니다. `ref readonly` 한정자로 선언되지 않은 변수에 이를 할당하기만 하면 됩니다. 컴파일러는 지정의 일부로 개체를 복사하는 코드를 생성합니다. 

`ref readonly return`에 변수를 할당하면 `ref readonly` 변수나 읽기 전용 참조의 값 형식 복사본을 지정할 수 있습니다.

[!code-csharp[AssignRefReadonly](../../samples/csharp/reference-semantics/Program.cs#AssignRefReadonly "Assigning a ref readonly")]

이전 코드의 첫 번째 할당에서는 `Origin` 상수의 복사본을 만들고 해당 복사본을 할당합니다. 두 번째 할당에서는 참조를 할당합니다. `readonly` 한정자는 변수 선언의 일부여야 합니다. 참조하는 항목에 대한 참조는 수정할 수 없습니다. 이를 수행하려고 시도하면 컴파일 시간 오류가 발생합니다.

## <a name="readonly-struct-type"></a>`readonly struct` 형식

구조체의 트래픽이 많은 사용에 `ref readonly`를 적용하는 것으로 충분할 수 있습니다.
그렇지 않은 경우에는 변경할 수 없는 구조체를 만들려고 할 수 있습니다. 그런 다음, 항상 읽기 전용 참조로 전달할 수 있습니다. 이 방법을 사용하면 `in` 매개 변수로 사용되는 구조체의 메서드에 액세스할 때 발생하는 방어 복사본이 제거됩니다.

`readonly struct` 형식을 만들어 이렇게 할 수 있습니다. 구조체 선언에 `readonly` 한정자를 추가할 수 있습니다. 컴파일러는 구조체의 모든 인스턴스 멤버가 `readonly`임을 강제 적용합니다. `struct`는 변경할 수 없어야 합니다.

`readonly struct`에 대한 다른 최적화가 있습니다. `readonly struct`가 인수인 모든 위치에 `in` 한정자를 사용할 수 있습니다. 또한 수명이 개체를 반환하는 메서드의 범위 이상으로 연장되는 개체를 반환할 때 `readonly struct`를 `ref return`으로 반환할 수 있습니다.

마지막으로 컴파일러는 `readonly struct`의 멤버를 호출할 때 더 효율적인 코드를 생성합니다. 수신기의 복사본 대신 `this` 참조는 항상 멤버 메서드에 대한 참조로 전달되는 `in` 매개 변수입니다. 이 최적화는 `readonly struct`를 사용할 때 더 많은 복사 작업을 줄여줍니다. `Point3D`는 이 변경에 대한 좋은 후보입니다. 다음 코드는 업데이트된 `ReadonlyPoint3D` 구조를 보여 줍니다.

[!code-csharp[ReadonlyOnlyPoint3D](../../samples/csharp/reference-semantics/Point3D.cs#ReadonlyOnlyPoint3D "Defining an immutable structure")]

## <a name="ref-struct-type"></a>`ref struct` 형식

또 다른 관련 언어 기능은 스택에 할당되어야 하는 값 형식을 선언하는 기능입니다. 즉, 이러한 형식은 다른 클래스의 멤버로 힙에 만들어질 수 없습니다. 이 기능의 기본 동기 부여는 <xref:System.Span%601> 및 관련 구조였습니다. <xref:System.Span%601>는 해당 멤버 중 하나로 관리되는 포인터를 포함하고 나머지로는 범위 길이를 포함할 수 있습니다. C#은 안전하지 않은 컨텍스트 외부에서 관리되는 메모리에 대한 포인터를 지원하지 않으므로 약간 다르게 구현됩니다. 포인터와 길이를 변경하는 모든 쓰기는 원자성이 아닙니다. 즉, <xref:System.Span%601>는 단일 스택 프레임으로 제약되지 않으므로 범위를 벗어나는 오류나 다른 형식 안전성 위반이 발생할 수 있습니다. 또한 GC 힙에 관리되는 포인터를 넣으면 일반적으로 JIT 시간에 충돌합니다.

[`stackalloc`](language-reference/keywords/stackalloc.md)을 사용하여 만들어진 메모리로 작업할 때나 interop API에서 메모리를 사용할 때도 유사한 요구 사항이 있을 수 있습니다. 해당 요구 사항에 대한 사용자 고유의 `ref struct` 형식을 정의할 수 있습니다. 이 문서에서는 편의상 `Span<T>`를 사용하는 예를 살펴봅니다.

`ref struct` 선언에서는 이 형식의 구조체가 스택에 있어야 함을 선언합니다. 언어 규칙은 이러한 형식의 안전한 사용을 보장합니다. `ref struct`로 선언된 다른 형식은 <xref:System.ReadOnlySpan%601>를 포함합니다. 

`ref struct` 형식을 스택에 할당된 변수로 유지하는 목표로 인해 컴파일러가 모든 `ref struct` 형식에 대해 강제 적용하는 여러 규칙이 도입되었습니다.

- `ref struct`를 boxing할 수 없습니다. `ref struct` 형식을 `object`, `dynamic` 형식 또는 인터페이스 유형의 변수에 할당할 수 없습니다.
- `ref struct`를 클래스 또는 일반 구조체의 멤버로 선언할 수 없습니다.
- 비동기 메서드에 `ref struct` 형식인 로컬 변수를 선언할 수 없습니다. `Task`, `Task<T>` 또는 Task와 유사한 형식을 반환하는 동기 메서드에 선언할 수 있습니다.
- 반복기에 `ref struct` 로컬 변수를 선언할 수 없습니다.
- 람다 식 또는 로컬 함수에서 `ref struct` 변수를 캡처할 수 없습니다.

이러한 제한 사항은 실수로 `ref struct`를 관리되는 힙으로 승격할 수 있는 방식으로 이 구조체를 사용하지 않게 해줍니다.

## <a name="readonly-ref-struct-type"></a>`readonly ref struct` 형식

구조체를 `readonly ref`로 선언하면 `ref struct` 및 `readonly struct` 선언의 이점과 제한이 결합됩니다. 

다음 예에서는 `readonly ref struct`의 선언을 보여줍니다.

```csharp
readonly ref struct ReadOnlyRefPoint2D
{
    public int X { get; }
    public int Y { get; }
    
    public ReadOnlyRefPoint2D(int x, int y) => (X, Y) = (x, y);
}
```

## <a name="conclusions"></a>결론

C# 언어에 대한 이러한 향상된 기능은 필요한 성능을 달성하는 데 메모리 할당이 중요할 수 있는, 성능이 중요한 알고리즘을 위해 설계되었습니다. 작성하는 코드에서 이러한 기능을 자주 사용하지 않을 수 있습니다. 그러나 이러한 향상된 기능은 .NET Framework의 많은 위치에 채택되었습니다. 점점 더 많은 API에서 이러한 기능을 사용하므로 사용자의 응용 프로그램 성능이 개선되는 것을 알 수 있습니다.
