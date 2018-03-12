---
title: "Visual Basic의 튜플"
ms.custom: 
ms.date: 04/23/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- tuples [Visual Basic]
ms.assetid: 3e66cd1b-3432-4e1d-8c37-5ebacae8f53f
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: bf26b7ce58c1e20fbbe5043cbd2acfd5712837fa
ms.sourcegitcommit: d95a91d685565f4d95c8773b558752864a6a3d7e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2018
---
# <a name="tuples-visual-basic"></a>튜플 (Visual Basic)

Visual Basic 2017 부터는 Visual Basic 언어는 기본 제공 하는 튜플 지원 튜플 만들고 튜플 쉽게 요소에 액세스 합니다. 튜플은 특정 수 및 값의 시퀀스를 포함 하는 간단한 데이터 구조입니다. 튜플의 인스턴스화할 때 수 및 각 값 (또는 요소)의 데이터 형식을 정의 합니다. 예를 들어 2-튜플 (또는 쌍)에 두 개의 요소가 있습니다. 첫 번째 수는 `Boolean` 값을 고 두 번째는는 `String`합니다. 튜플 쉽게 단일 개체에 여러 값을 저장할 수 있도록, 때문에 종종 메서드에서 여러 값을 반환 하는 간단한 방법으로 사용 됩니다.

> [!IMPORTANT]
> 튜플 지원 하려면는 <xref:System.ValueTuple> 유형입니다. NuGet 패키지를 추가 해야.NET Framework 4.7 설치 되어 있지 않으면 `System.ValueTuple`은 NuGet 갤러리에서 사용할 수 있습니다. 이 패키지 없이 오류가 발생할 수 있습니다는 컴파일, "미리 정의 된 형식과 비슷한 'ValueTuple(Of,,,)'가 정의 하지 않았거나 가져오지 하지 않습니다."

## <a name="instantiating-and-using-a-tuple"></a>인스턴스화 및 튜플을 사용

쉼표로 구분 된 값 im 괄호를 포함 하 여 튜플을 인스턴스화합니다. 각 값 튜플의 필드가 다음 됩니다. 다음 코드를 세 번 (또는 3-튜플)을 정의 예를 들어 한 `Date` 해당 첫 번째 값으로는 `String` 를 두 번째 및 `Boolean` 세 번째도 합니다.

[!code-vb[Instantiate](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple1.vb#1)]

기본적으로 문자열의 튜플의 각 필드의 이름이 구성 `Item` 튜플의 필드의 1-시작 위치와 함께 합니다. 이 3-튜플에 대 한는 `Date` 필드는 `Item1`, `String` 필드는 `Item2`, 및 `Boolean` 필드는 `Item3`합니다. 다음 예제에서는 코드의 이전 줄에서 인스턴스화된 튜플의 필드의 값 표시

[!code-vb[Instantiate](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple1.vb#2)]

Visual Basic 튜플의 필드는 읽기 / 쓰기; 튜플을 인스턴스화한 한 후 해당 값을 수정할 수 있습니다. 다음 예제에서는 두 개의 이전 예제에서 만든 튜플의 세 개의 필드를 수정 하 고 결과 표시 합니다.

[!code-vb[Instantiate](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple1.vb#3)]

## <a name="instantiating-and-using-a-named-tuple"></a>인스턴스화 및 명명 된 튜플을 사용

튜플의 필드에 대 한 기본 이름을 사용 하는 대신 인스턴스화할 수 있습니다는 *라는 튜플* 튜플의 요소에 고유한 이름을 지정 하 여 합니다. 튜플의 필드에 할당 된 이름으로 액세스할 수 있습니다 *또는* 기본 이름으로 합니다. 다음 예제에서는 첫 번째 필드 이름을 명시적으로 지정 한다는 점을 제외 하면 앞에서 동일한 3-튜플 인스턴스화합니다 `EventDate`, 두 번째 `Name`, 세 번째 `IsHoliday`합니다. 필드 값을 표시,를 수정 하 고 다시 필드 값이 표시 됩니다.

[!code-vb[Instantiate](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple1.vb#4)]

## <a name="inferred-tuple-element-names"></a>유추 된 튜플 요소 이름

Visual Basic 15.3 부터는 Visual Basic 유추할 수; 여 튜플 요소 이름 명시적으로 할당 필요가 없습니다. 유추 된 튜플 이름은 변수 집합에서 튜플을 초기화 하 고 변수 이름으로 동일 하 게 튜플 요소 이름을 사용 하려는 경우에 유용 합니다. 

다음 예제에서는 한 `stateInfo` 명명 된 요소를 명시적으로 3 개 포함 된 튜플을 `state`, `stateName`, 및 `capital`합니다. 유의 요소 이름 지정 시에, 튜플 초기화 문 지정 명명 된 요소는 동일 하 게 명명 된 변수의 값입니다.

[!code-vb[ExplicitlyNamed](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/named-tuples/program.vb#1)]
 
요소 및 변수의 이름이 동일 하기 때문에 Visual Basic 컴파일러는 다음 예제와 같이 필드의 이름이 추론할 수 있습니다.

[!code-vb[ExplicitlyNamed](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/named-tuples/program.vb#2)]

Visual Basic 프로젝트에서 사용 하는 Visual Basic 컴파일러의 버전을 정의 해야 수감 되어 튜플 요소 이름을 사용 하려면 (\*.vbproj) 파일: 

```xml 
<PropertyGroup> 
  <LangVersion>15.3</LangVersion> 
</PropertyGroup> 
```

버전 번호는 15.3 부터는 Visual Basic 컴파일러의 모든 버전일 수 있습니다. 하드 코딩 특정 컴파일러 버전을 대신 지정할 수도 있습니다 "최신"의 값으로 `LangVersion` 를 시스템에 설치 하는 Visual Basic 컴파일러의 가장 최신 버전을 사용 하 여 컴파일합니다.

Visual Basic 컴파일러에 따라서는 후보 이름에서 튜플 요소 이름을 유추할 수 없습니다 및와 같은 기본 이름으로 사용 하 여 튜플 필드 참조만 수 `Item1`, `Item2`등입니다. 여기에는 다음이 포함됩니다.

- 후보 이름은 튜플 멤버의 이름과 같은 `Item3`, `Rest`, 또는 `ToString`합니다.

- 튜플의 후보 이름이 중복 됩니다.
 
필드 이름 유추가 실패 한 경우 Visual Basic 컴파일러 오류가 발생 하지 않습니다 없거나 이러한 속성이 런타임 시 발생 하는 예외입니다. 대신, 튜플 필드 참조 해야의 미리 정의 된 이름이 같은 `Item1` 및 `Item2`합니다. 
  
## <a name="tuples-versus-structures"></a>구조 및 튜플

Visual Basic 튜플 값 형식이 중 하나의 인스턴스가는 **System.ValueTuple** 제네릭 형식입니다. 예를 들어는 `holiday` 의 인스턴스가 이전 예제에서 정의 된 튜플을 <xref:System.ValueTuple%603> 구조입니다. 데이터에 대 한 간단한 컨테이너 되도록 설계 되었습니다. 튜플의 쉽게 여러 데이터 항목이 있는 개체를 만들 수 있도록 목표, 이후 사용자 정의 구조를 가질 수 있는 기능 중 일부는 없습니다. 여기에는 다음이 포함됩니다.

- 고객 멤버입니다. 사용자 고유의 속성, 메서드 또는 튜플의 대 한 이벤트를 정의할 수 없습니다.

- 유효성 검사 합니다. 필드에 할당 된 데이터를 확인할 수 없습니다.

- 변경 불가능 합니다. Visual Basic 튜플은 변경할 수 있습니다. 반면, 사용자 정의 구조를 제어할 수 있습니다 인지 인스턴스 변경할 수 있는 변경 불가능 합니다.

사용자 지정 멤버, 속성 및 필드 유효성 검사 또는 불변성 중요 한 경우에 Visual Basic을 사용 해야 [구조](../../../language-reference/statements/structure-statement.md) 을 사용자 지정 값 형식을 정의 합니다.

Visual Basic 튜플 멤버의 상속지 않습니다 해당 **ValueTuple** 유형입니다. 해당 필드와 함께 다음 메서드는 다음과 같습니다.

| 멤버 | 설명 |
| ---|---|
| CompareTo | 현재 튜플을 다른 튜플에 동일한 수의 요소를 비교합니다. |
| 같음 | 현재 튜플을 다른 튜플 또는 개체와 같은지 여부를 결정 합니다. |
| GetHashCode | 현재 인스턴스에 대 한 해시 코드를 계산합니다. |
| ToString | 형식은이 튜플의 문자열 표현을 반환 `(Item1, Item2...)`여기서 `Item1` 및 `Item2` 튜플의 필드의 값을 나타냅니다. |

또한는 **ValueTuple** 형식은 구현 <xref:System.Collections.IStructuralComparable> 및 <xref:System.Collections.IStructuralEquatable> 인터페이스는 고객 비교자를 정의할 수 있습니다.

## <a name="assignment-and-tuples"></a>할당 및 튜플

Visual Basic에서는 동일한 필드 수 있는 튜플 형식 사이 할당을 지원 합니다. 다음 중 하나 이면 필드 유형을 변환할 수 있습니다.

- 원본 및 대상 필드는 같은 형식입니다.

- 확대 (또는 암시적) 변환 원본 유형 대상 유형으로 정의 됩니다. 

- `Option Strict` `On`, 축소 (또는 명시적) 변환 원본 유형 대상 유형으로 정의 됩니다. 이 변환은 원본 값이 대상 형식의 범위 밖에 있는 경우 예외를 throw 합니다.

다른 변환은 할당에 고려되지 않습니다. 튜플 형식 간에 허용되는 할당 종류를 살펴보겠습니다.

다음 예제에서 사용되는 이러한 변수를 살펴보세요.

[!code-vb[Assign](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple3.vb#1)]

처음 두 개의 변수 `unnamed` 및 `anonymous`는 필드에 대해 제공 된 의미 체계 이름이 없습니다. 필드 이름 요소가 기본 `Item1` 및 `Item2`합니다. 마지막 두 개의 변수 `named` 및 `differentName` 의미 체계 필드 이름이 있습니다. 이러한 두 튜플의 필드 이름은 서로 다릅니다.

이러한 튜플의 네 필드 (라고도 함 '인자 수가'), 동일한 수 있고 해당 필드의 형식이 동일 합니다. 따라서 다음 할당이 모든 작동합니다.

[!code-vb[Assign](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple3.vb#2)]

튜플 이름은 할당되지 않습니다. 필드 값은 튜플의 필드 순서에 따라 할당됩니다.

마지막으로 할당할 수 있습니다 알는 `named` 에 튜플을 `conversion` 튜플 경우에의 첫 번째 필드로 `named` 은 `Integer`, 및의 첫 번째 필드 `conversion` 는 `Long`합니다. 변환 있기 때문에이 할당 성공는 `Integer` 에 `Long` 확대 변환 합니다.

[!code-vb[Assign](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple3.vb#3)]

필드의 수를 다르게 하 여 튜플은 할당할 수 없습니다.

```vb
' Does not compile.
' VB30311: Value of type '(Integer, Integer, Integer)' cannot be converted
'          to '(Answer As Integer, Message As String)'
var differentShape = (1, 2, 3)
named = differentShape
```

## <a name="tuples-as-method-return-values"></a>메서드 반환 값으로의 튜플

메서드는 단일 값만 반환할 수 있습니다. 대부분의 경우 하지만 원하는 여러 값을 반환 하는 메서드 호출 합니다. 여러 가지 방법을 사용 하 여이 제한을 해결할 수 있습니다.

- 사용자 지정 클래스 또는 구조체 속성을 가진 만들거나 필드 메서드에 의해 반환 되는 값을 나타냅니다. 따라서는 중량 솔루션입니다. 유일한 목적인 메서드 호출에서 값을 검색 하는 사용자 지정 형식을 정의 하는 필요 합니다.

- 단일 값은 메서드에서 돌아오기 있고 메서드에 대 한 참조를 전달 하 여 나머지 값을 반환 합니다. 변수 및 참조로 전달 하는 변수의 값을 덮어쓰는 위험을 인스턴스화하는 오버 헤드 포함 됩니다.

- 여러 개의 반환 값을 검색 하는 간단한 솔루션을 제공 하는 튜플을 사용할 수 있습니다.

예를 들어는 **TryParse** .NET 리턴으로 메서드는 `Boolean` 구문 분석 작업이 성공 했는지 여부를 나타내는 값입니다. 구문 분석 작업의 결과 메서드에 참조로 전달 되는 변수에 반환 됩니다. 에 대 한 호출 일반적으로와 같은 구문 분석 방법을 <xref:System.Int32.TryParse%2A?displayProperty=nameWithType> 은 다음과 같습니다.

[!code-vb[Return](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple-returns.vb#1)]

문자열을 반환할 수 튜플을 구문 분석 작업에서 호출을 래핑할 하는 경우는 <xref:System.Int32.TryParse%2A?displayProperty=nameWithType> 고유한 메서드에서 메서드. 다음 예에서 `NumericLibrary.ParseInteger` 호출은 <xref:System.Int32.TryParse%2A?displayProperty=nameWithType> 메서드 및 두 개의 요소가 있는 명명 된 튜플을 반환 합니다. 

[!code-vb[Return](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple-returns.vb#2)]

다음과 같은 코드를 사용 하 여 메서드를 호출할 수 있습니다.

[!code-vb[Return](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple-returns.vb#3)]

## <a name="visual-basic-tuples-and-tuples-in-the-net-framework"></a>Visual Basic 튜플 및.NET Framework의 튜플

Visual Basic 튜플은 중 하나의 인스턴스는 **System.ValueTuple** 제네릭 형식.NET Framework 4.7에 도입 되었습니다. .NET Framework 제네릭 집합이 포함 되어 **System.Tuple** 클래스입니다. 그러나 Visual Basic 튜플에서와 다 이러한 클래스와 **System.ValueTuple** 다양 한 방법으로의 제네릭 형식:

- 요소는 **튜플** 클래스는 명명 된 속성 `Item1`, `Item2`등입니다. Visual Basic 튜플에 및 **ValueTuple** 형식, 튜플 요소는 필드입니다.

- 요소에 의미 있는 이름을 할당할 수 없습니다는 **튜플** 인스턴스 또는 **ValueTuple** 인스턴스. Visual Basic을 사용 하는 필드의 의미를 전달 하는 이름을 지정할 수 있습니다.

- 속성은 **튜플** 인스턴스는 읽기 전용; 튜플을 변경할 수 없습니다. Visual Basic 튜플에 및 **ValueTuple** 형식, 튜플 필드는 읽기 / 쓰기; 튜플에 변경할 수 있습니다.

- 제네릭 **튜플** 형식은 참조 형식입니다. 이 사용 하 여 **튜플** 개체 할당 의미를 입력 합니다. 실행 부하 과다 경로에서는 이로 인해 응용 프로그램 성능이 크게 영향을 받을 수 있습니다. Visual Basic 튜플 및 **ValueTuple** 유형은 값 형식입니다.

확장 메서드는 <xref:System.TupleExtensions> 클래스 쉽게 튜플 Visual Basic 및.NET 사이 변환할 **튜플** 개체입니다. **ToTuple** 메서드는.NET Visual Basic 튜플 변환 **튜플** 개체 및 **ToValueTuple** 메서드 변환.NET **튜플** Visual Basic 튜플 개체입니다.

다음 예제는 튜플을 만듭니다을 하는.NET 변환 **튜플** 개체 및 Visual Basic 튜플에 다시 변환 합니다. 그런 다음 원래 같은지 확인에 있는이 튜플을 비교 합니다.

[!code-vb[Convert](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple2.vb#1)]

## <a name="see-also"></a>참고 항목

[Visual Basic 언어 참조](index.md)  
