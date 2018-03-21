---
title: "C# 7의 새로운 기능 - C# 가이드"
description: "C# 언어의 새 버전 7에서 제공되는 새로운 기능을 간단히 살펴봅니다."
keywords: "C#, .NET, .NET Core, 최신 기능, 새로운 기능"
author: BillWagner
ms.author: wiwagn
ms.date: 12/21/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: fd41596d-d0c2-4816-b94d-c4d00a5d0243
ms.openlocfilehash: 374ac9917464a7e83566440abab10eda8a9c8683
ms.sourcegitcommit: 32172ca05d5dcce7ef3d327b9c8639c736e0fe2b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2018
---
# <a name="whats-new-in-c-7"></a>C# 7의 새로운 기능

C# 7에서는 C# 언어에 많은 새로운 기능을 추가합니다.
* [`out` 변수](#out-variables)
    - `out` 값을 사용되는 메서드에 대한 인수로 인라인으로 선언할 수 있습니다.
* [튜플](#tuples)
    - 여러 public 필드가 포함된 간단한 명명되지 않은 형식을 만들 수 있습니다. 컴파일러 및 IDE 도구는 이러한 형식의 의미 체계를 이해합니다.
* [삭제](#discards)
    - 삭제는 할당된 값에 신경 쓰지 않을 때 할당에서 사용되는 임시 쓰기 전용 변수입니다. 매개 변수는 `out` 매개 변수를 사용하여 메서드를 호출할 때뿐만 아니라 튜플 및 사용자 정의 형식을 분해할 때 특히 유용합니다.
* [패턴 일치](#pattern-matching)
    - 임의 형식 및 해당 형식의 멤버 값에 따라 분기 논리를 만들 수 있습니다.
* [`ref` local 및 return](#ref-locals-and-returns)
    - 메서드 인수와 지역 변수는 다른 저장소에 대한 참조일 수 있습니다.
* [로컬 함수](#local-functions)
    - 함수를 다른 함수 내부에 중첩하여 범위와 표시 여부를 제한할 수 있습니다.
* [추가 식 본문 멤버](#more-expression-bodied-members)
    - 식을 사용하여 작성할 수 있는 멤버 목록이 증가했습니다.
* [`throw` 식](#throw-expressions)
    - `throw` 문이었기 때문에 이전에 허용되지 않은 코드 구문에서 예외를 throw할 수 있습니다. 
* [일반화된 비동기 반환 형식](#generalized-async-return-types)
    - `async` 한정자를 사용하여 선언된 메서드는 `Task` 및 `Task<T>` 외에 다른 형식을 반환할 수 있습니다.
* [숫자 리터럴 구문 개선 사항](#numeric-literal-syntax-improvements)
    - 새로운 토큰으로 숫자 상수의 가독성이 향상됩니다.

이 항목의 나머지 부분에서는 각 기능을 설명합니다. 각 기능의 배경과 원리를 알아봅니다. 구문을 알아봅니다. 새로운 기능을 사용하여 개발자로서 생산성을 높일 수 있는 몇 가지 샘플 시나리오를 살펴봅니다. 

## <a name="out-variables"></a>`out` 변수

`out` 매개 변수를 지원하는 기존 구문이 이 버전에서 개선되었습니다.  

이전에는 out 변수의 선언과 초기화를 두 개의 다른 문으로 구분해야 했습니다.

[!code-csharp[OutVariableOldStyle](../../../samples/snippets/csharp/new-in-7/program.cs#03_OutVariableOldStyle "classic out variable declaration")]

이제 개별 선언 문을 작성하는 대신 메서드 호출의 인수 목록에서 `out` 변수를 선언할 수 있습니다.

[!code-csharp[OutVariableDeclarations](../../../samples/snippets/csharp/new-in-7/program.cs#01_OutVariableDeclarations "Out variable declarations")]

위에 나와 있는 대로 쉽게 구별할 수 있도록 `out` 변수의 형식을 지정할 수 있습니다. 그러나 이 언어는 암시적 형식 지역 변수를 지원하지 않습니다.

[!code-csharp[OutVarVariableDeclarations](../../../samples/snippets/csharp/new-in-7/program.cs#02_OutVarVariableDeclarations "Implicitly typed Out variable")]

* 코드를 읽기가 더 쉽습니다. 
    - 위의 다른 줄이 아니라 사용하는 위치에서 out 변수를 선언합니다.
* 초기 값을 할당할 필요가 없습니다.
    - 메서드 호출에서 사용되는 위치에 `out` 변수를 선언하면 변수가 선언되기 전에 실수로 사용할 가능성이 없습니다.

이 기능은 `Try` 패턴에 가장 일반적으로 사용됩니다. 이 패턴에서 메서드는 성공 또는 실패를 나타내는 `bool` 및 메서드가 성공할 경우 결과를 제공하는 `out` 변수를 반환합니다.

`out` 변수 선언을 사용할 경우 선언된 변수가 if 문의 외부 범위로 "누수"됩니다. 따라서 이후에도 해당 변수를 사용할 수 있습니다.

```csharp
if (!int.TryParse(input, out int result))
{    
    return null;
}

return result;
```

## <a name="tuples"></a>튜플

> [!NOTE]
> 새 튜플 기능을 사용하려면 <xref:System.ValueTuple> 형식이 필요합니다.
> 형식을 포함하지 않는 플랫폼에서 사용하려면 NuGet 패키지 [`System.ValueTuple`](https://www.nuget.org/packages/System.ValueTuple/)을 추가해야 합니다.
>
> 이는 프레임워크에서 제공되는 형식을 사용하는 다른 언어 기능과 비슷합니다. 예를 들어 `async` 및 `await`는 `INotifyCompletion` 인터페이스를 사용하고 LINQ는 `IEnumerable<T>`을 사용합니다. 그러나 .NET이 점점 더 플랫폼 독립적으로 되면서 배달 메커니즘도 변하고 있습니다. .NET Framework가 언어 컴파일러와 동일한 주기로 제공되지 않을 수도 있습니다. 새로운 언어 기능이 새 형식을 사용하는 경우 해당 형식은 언어 기능이 제공될 때 NuGet 패키지로 제공됩니다. 이러한 새로운 형식이 .NET Standard API에 추가되고 프레임워크의 일부로 제공되면, NuGet 패키지 요구 사항이 제거됩니다.

C#에서는 디자인 의도를 설명하는 데 사용되는 클래스 및 구조체에 대한 다양한 구문을 제공합니다. 하지만 다양한 구문에는 이점이 거의 없는데 추가 작업이 필요한 경우가 있습니다. 일반적으로 두 개 이상의 데이터 요소가 포함된 간단한 구조체가 필요한 메서드를 작성할 수 있습니다. 이러한 시나리오를 지원하기 위해 *튜플*이 C#에 추가되었습니다. 튜플은 데이터 멤버를 나타내는 여러 필드가 포함된 간단한 데이터 구조입니다.
필드는 유효성이 검사되지 않고 자체 메서드를 정의할 수 없습니다.

> [!NOTE]
> 튜플은 C# 7 이전부터 사용할 수 있었지만 비효율적이었고 언어 지원이 없었습니다.
> 즉, 튜플 요소는 `Item1`, `Item2` 등으로만 참조될 수 있었습니다. C# 7은 새롭고 보다 효율적인 튜플 유형을 사용하여 튜플의 필드에 대해 의미론적 이름을 사용할 수 있는 튜플에 대한 언어 지원을 소개합니다.

각 멤버를 값에 할당하여 튜플을 만들 수 있습니다.

[!code-csharp[UnnamedTuple](../../../samples/snippets/csharp/new-in-7/program.cs#04_UnnamedTuple "Unnamed tuple")]

이 할당은 멤버가 `Item1` 및 `Item2`이고 <xref:System.Tuple>과 동일한 방식으로 사용할 수 있는 튜플을 생성합니다. 구문을 변경하여 의미론적 이름을 튜플의 각 멤버에 제공하는 튜플을 만들 수 있습니다.

[!code-csharp[NamedTuple](../../../samples/snippets/csharp/new-in-7/program.cs#05_NamedTuple "Named tuple")]

`namedLetters` 튜플에는 `Alpha` 및 `Beta`라는 필드가 포함됩니다. 이러한 이름은 컴파일 시간에만 존재하며 런타임 시 반영을 통해 튜플을 검사하는 경우 등을 위해 보존되지 않습니다.

튜플 할당에서 할당의 오른쪽에 필드의 이름을 지정할 수도 있습니다.

[!code-csharp[ImplicitNamedTuple](../../../samples/snippets/csharp/new-in-7/program.cs#06_ImplicitNamedTuple "Implicitly named tuple")]

할당의 왼쪽 및 오른쪽에서 모두 필드의 이름을 지정할 수 있습니다.

[!code-csharp[NamedTupleConflict](../../../samples/snippets/csharp/new-in-7/program.cs#07_NamedTupleConflict "Named tuple conflict")]

위 줄에서는 할당의 오른쪽에 있는 이름 `Alpha` 및 `Beta`가 왼쪽에 있는 이름 `First` 및 `Second`와 충돌하기 때문에 무시됨을 알리는 경고 `CS8123`을 생성합니다.

위 예제에서는 튜플을 선언하는 기본 구문을 보여 줍니다. 튜플은 `private` 및 `internal` 메서드의 반환 형식으로 가장 유용합니다. 튜플은 여러 개별 값을 반환하기 위한 해당 메서드에 대한 간단한 구문을 제공합니다. 반환되는 형식을 정의하는 `class` 또는 `struct`를 작성하는 작업을 저장합니다. 새 형식을 만들 필요가 없습니다.

튜플을 만드는 것이 더 효율적이고 더 생산적입니다.
두 개 이상의 값을 전달하는 데이터 구조를 정의하는 것이 더 간단한 구문입니다. 아래 예제 메서드는 정수 시퀀스에서 발견된 최소값 및 최대값을 반환합니다.

[!code-csharp[TupleReturningMethod](../../../samples/snippets/csharp/new-in-7/program.cs#08_TupleReturningMethod "Tuple returning method")]

이 방법으로 튜플을 사용하는 것에는 몇 가지 장점이 있습니다.

* 반환되는 형식을 정의하는 `class` 또는 `struct`를 작성하는 작업을 저장합니다. 
* 새 형식을 만들 필요가 없습니다.
* 언어가 향상되어 <xref:System.Tuple.Create``1(``0)> 메서드를 호출할 필요가 없습니다.

메서드 선언은 반환되는 튜플의 필드 이름을 제공합니다. 메서드를 호출할 경우 반환 값은 필드가 `Max` 및 `Min`인 튜플입니다.

[!code-csharp[CallingTupleMethod](../../../samples/snippets/csharp/new-in-7/program.cs#09_CallingTupleMethod "Calling a tuple returning method")]

메서드에서 반환된 튜플의 멤버를 패키지 해제하려는 경우가 있을 수 있습니다.  이 작업을 수행하려면 튜플에서 각 값에 대한 개별 변수를 선언합니다. 이 작업을 튜플 *분해*라고 합니다.

[!code-csharp[CallingWithDeconstructor](../../../samples/snippets/csharp/new-in-7/program.cs#10_CallingWithDeconstructor "Deconstructing a tuple")]

<!-- Add wildcards here, if they are in C# 7
-->

.NET에 있는 형식에 대한 비슷한 분해를 제공할 수도 있습니다. 이 작업을 수행하려면 `Deconstruct` 메서드를 클래스의 멤버로 작성합니다. 해당 `Deconstruct` 메서드는 추출하려는 각 속성에 대한 `out` 인수 집합을 제공합니다. `X` 및 `Y` 좌표를 추출하는 분해자 메서드를 제공하는 이 `Point` 클래스를 살펴봅니다.

[!code-csharp[PointWithDeconstruction](../../../samples/snippets/csharp/new-in-7/point.cs#11_PointWithDeconstruction "Point with deconstruction method")]
 
`Point`에 튜플을 할당하여 개별 필드를 추출할 수 있습니다.

[!code-csharp[DeconstructPoint](../../../samples/snippets/csharp/new-in-7/program.cs#12_DeconstructPoint "Deconstruct a point")]

`Deconstruct` 메서드에 정의된 아름으로 바인딩되어 있지 않습니다. 할당의 일부로 추출 변수의 이름을 바꿀 수 있습니다.  

[!code-csharp[DeconstructNames](../../../samples/snippets/csharp/new-in-7/program.cs#13_DeconstructNames "Deconstruct with new names")]

[튜플 항목](../tuples.md)에서 튜플에 대해 자세히 알아볼 수 있습니다.

## <a name="discards"></a>버림

종종 튜플을 분해하거나 `out` 매개 변수로 메서드를 호출할 때 값을 신경 쓰지 않고 사용하지 않을 변수를 정의해야 합니다. C#은 *버림*에 대한 지원을 추가하여 이 시나리오를 처리합니다. 무시는 이름이 `_`(밑줄 문자)인 쓰기 전용 변수입니다. 단일 변수에 버리려는 모든 값을 할당할 수 있습니다. 버림은 할당 문과 별도로 분리되는 할당되지 않은 변수와 같습니다. 코드에서 버림을 사용할 수 없습니다.

다음 시나리오에서는 버림이 지원되지 않습니다.

* 튜플이나 사용자 정의 형식을 분해할 때.

* [out](../language-reference/keywords/out-parameter-modifier.md) 매개 변수로 메서드를 호출할 때.

* [is](../language-reference/keywords/is.md) 및 [switch](../language-reference/keywords/switch.md) 문을 사용한 패턴 일치 작업에서.

* 할당 값을 버림으로 명시적으로 지정할 때 독립 실행형 식별자인 경우.

다음 예제는 서로 다른 2년 동안 도시에 대한 데이터를 포함한 6 튜플을 반환하는 `QueryCityDataForYears` 메서드를 정의합니다. 예제의 메서드 호출은 메서드에 의해 반환된 두 개의 채우기 값에만 관련되어 있으므로 튜플을 해체할 때 튜플의 나머지 값을 버림으로 처리합니다.

[!code-csharp[Tuple-discard](../../../samples/snippets/csharp/programming-guide/deconstructing-tuples/discard-tuple1.cs)]

자세한 내용은 [버림](../discards.md)을 참조하세요.
 
## <a name="pattern-matching"></a>패턴 일치

*패턴 일치*는 개체 형식이 아닌 속성에 대한 메서드 디스패치를 구현할 수 있는 기능입니다. 개체 형식에 따른 메서드 디스패치에 이미 익숙할 수 있습니다. 개체 지향 프로그래밍에서 가상 및 재정의 메서드는 개체 형식에 따라 메서드 디스패치를 구현하기 위한 언어 구문을 제공합니다. 기본 및 파생 클래스는 서로 다른 구현을 제공합니다. 패턴 일치 식은 상속 계층 구조를 통해 관련되지 않은 형식 및 데이터 요소에 대한 비슷한 디스패치 패턴을 쉽게 구현할 수 있도록 이 개념을 확장합니다. 

패턴 일치는 `is` 식과 `switch` 식을 지원합니다. 각 식을 통해 개체 및 관련 속성을 검사하여 해당 개체가 검색된 패턴을 충족하는지 확인할 수 있습니다. `when` 키워드를 사용하여 패턴에 대한 추가 규칙을 지정합니다.

### <a name="is-expression"></a>`is` 식

`is` 패턴 식은 친숙한 `is` 연산자를 확장하여 형식을 넘어서서 개체를 쿼리합니다.

먼저 간단한 시나리오를 살펴보겠습니다. 패턴 일치 식을 통해 관련되지 않은 형식을 사용하는 알고리즘을 단순화하는 기능을 이 시나리오에 추가합니다. 먼저 많은 주사위 굴리기의 합계를 계산하는 메서드를 살펴봅니다.

[!code-csharp[SumDieRolls](../../../samples/snippets/csharp/new-in-7/patternmatch.cs#14_SumDieRolls "Sum die rolls")]

여러 개의 주사위를 굴리는 경우 주사위 굴리기의 합계를 빠르게 확인해야 합니다. 입력 시퀀스의 일부는 단일 숫자가 아닌 여러 결과일 수 있습니다.

[!code-csharp[SumDieRollsWithGroups](../../../samples/snippets/csharp/new-in-7/patternmatch.cs#15_SumDieRollsWithGroups "Sum die rolls with groups")]

이 시나리오에서는 `is` 패턴 식이 잘 작동합니다. 형식 검사의 일부로 변수 초기화를 작성합니다. 이렇게 하면 유효성 검사된 런타임 형식의 새 변수가 만들어집니다.

이러한 시나리오를 계속 확장하면 더 많은 `if` 및 `else if` 문을 빌드한다는 것을 알 수 있습니다. 구조가 너무 복잡해지면 `switch` 패턴 식으로 전환할 수 있습니다.

### <a name="switch-statement-updates"></a>`switch` 문 업데이트

*일치 식*에는 이미 C# 언어의 일부인 `switch` 문에 기반을 둔 친숙한 구문이 있습니다. 새 사례를 추가하기 전에 일치 식을 사용하도록 기존 코드를 변환해 보겠습니다. 

[!code-csharp[SumUsingSwitch](../../../samples/snippets/csharp/new-in-7/patternmatch.cs#16_SumUsingSwitch "Sum using switch")]

일치 식에는 `case` 식의 시작 부분에 형식과 변수를 선언하는 `is` 식과 약간 다른 구문이 있습니다.

일치 식은 상수도 지원합니다. 이 방법에서는 간단한 사례를 제외하여 시간을 절약할 수 있습니다.

[!code-csharp[SwitchWithConstants](../../../samples/snippets/csharp/new-in-7/patternmatch.cs#17_SwitchWithConstants "Switch with constants")]

위의 코드는 `0`에 대한 사례를 `int`의 특수 사례로 추가하고 입력이 없는 경우 `null`을 특수 사례로 추가합니다. 이것은 스위치 패턴 식의 한 가지 중요한 새로운 기능을 보여 줍니다. 이제 `case` 식의 순서는 중요하지 않습니다. `0` 사례는 일반적인 `int` 사례 앞에 와야 합니다. 그렇지 않으면 값이 `0`인 경우에도 일치시킬 첫 번째 패턴이 `int` 사례가 됩니다. 일치 식의 순서를 잘못 지정하여 나중 사례가 이미 처리되었다면 컴파일러는 여기에 플래그를 지정하고 오류를 생성합니다.

이런 동일한 동작을 통해 빈 입력 시퀀스에 대한 특수 사례가 가능해집니다.
요소가 포함된 `IEnumerable` 항목에 대한 사례가 일반적인 `IEnumerable` 사례 앞에 나타나야 함을 알 수 있습니다.

이 버전에서는 `default` 사례를 추가했습니다. `default` 사례는 소스에서 나타나는 순서에 관계없이 항상 마지막으로 계산됩니다. 이런 이유로 `default` 사례를 마지막에 배치하는 것이 규칙입니다.

마지막으로 새로운 주사위 스타일에 대한 하나의 마지막 `case`를 추가해 보겠습니다. 일부 게임에서는 백분위수 주사위를 사용하여 더 큰 범위의 숫자를 나타냅니다. 

> [!NOTE]
> 두 개의 10면 백분위수 주사위는 0~99의 모든 숫자를 나타낼 수 있습니다. 하나의 주사위에는 `00`, `10`, `20`, ... `90`이 표시된 면이 있습니다. 다른 주사위에는 `0`, `1`, `2`, ... `9`가 표시된 면이 있습니다. 두 주사위 값을 더하면 0~99의 모든 숫자를 얻을 수 있습니다.

이 유형의 주사위를 컬렉션에 추가하려면 먼저 백분위수 주사위를 나타내는 형식을 정의합니다. `TensDigit` 속성은 `0`, `10`, `20`, 최대 `90` 값을 저장합니다.

[!code-csharp[18_PercentileDice](../../../samples/snippets/csharp/new-in-7/patternmatch.cs#18_PercentileDice "Percentile Die type")]

그런 다음 새 형식에 대한 `case` 일치 식을 추가합니다.

[!code-csharp[SwitchWithNewTypes](../../../samples/snippets/csharp/new-in-7/patternmatch.cs#19_SwitchWithNewTypes "Include Percentile Die type")]

패턴 일치 식에 대한 새로운 구문을 사용하면 분명하고 간결한 구문을 통해 개체 형식에 따른 디스패치 알고리즘 또는 기타 속성을 더 쉽게 만들 수 있습니다. 패턴 일치 식을 사용하면 상속이 관련되지 않은 데이터 형식에서 이러한 구문을 사용할 수 있습니다.

패턴 일치에 대한 자세한 내용은 [C#의 패턴 일치](../pattern-matching.md)에 관련된 항목을 참조하세요.

## <a name="ref-locals-and-returns"></a>Ref local 및 return

이 기능을 통해 다른 곳에 정의된 변수에 대한 참조를 사용 및 반환하는 알고리즘이 가능해집니다. 한 가지 예는 큰 매트릭스를 사용하고 특정 특징을 가진 하나의 위치를 찾는 것입니다. 하나의 메서드가 매트릭스에 있는 하나의 위치에 대한 두 개의 인덱스를 반환합니다.

[!code-csharp[FindReturningIndices](../../../samples/snippets/csharp/new-in-7/MatrixSearch.cs#20_FindReturningIndices "Find returning indices")]

이 코드에는 많은 문제가 있습니다. 무엇보다 이 코드는 튜플을 반환하는 public 메서드입니다. 언어에서는 이 코드를 지원하지만 public API의 경우 사용자 지정 형식(클래스 또는 구조체)이 기본적으로 사용됩니다.

두 번째로, 이 메서드는 매트릭스의 항목으로 인덱스를 반환합니다.
이에 따라 호출자는 해당 인덱스를 사용하여 매트릭을 역참조하고 단일 요소를 수정하는 코드를 작성합니다.

[!code-csharp[UpdateItemFromIndices](../../../samples/snippets/csharp/new-in-7/program.cs#21_UpdateItemFromIndices "Update Item From Indices")]

변경할 매트릭스의 요소에 대한 *참조*를 반환하는 메서드를 작성하는 것이 좋습니다. 이 작업을 수행하려면 안전하지 않은 코드를 사용하고 이전 버전의 `int`로 포인터를 반환해야 합니다.

ref local 기능을 보여 주고 내부 저장소에 대한 참조를 반환하는 메서드를 만드는 방법을 보여 주는 일련의 변경을 살펴보겠습니다.
계속해서 실수로 잘못 사용하는 경우를 방지하는 ref return 및 ref local 기능의 규칙을 알아봅니다.

먼저 튜플 대신 `ref int`를 반환하도록 `Find` 메서드 선언을 수정합니다. 그런 다음 두 개의 인덱스 대신 매트릭스에 저장된 값을 반환하도록 return 문을 수정합니다.

```csharp
// Note that this won't compile. 
// Method declaration indicates ref return,
// but return statement specifies a value return.
public static ref int Find2(int[,] matrix, Func<int, bool> predicate)
{
    for (int i = 0; i < matrix.GetLength(0); i++)
        for (int j = 0; j < matrix.GetLength(1); j++)
            if (predicate(matrix[i, j]))
                return matrix[i, j];
    throw new InvalidOperationException("Not found");
}
```

메서드가 `ref` 변수를 반환하도록 선언할 경우 각 return 문에 `ref` 키워드도 추가해야 합니다. 이는 참조에 의한 반환을 나타내고 나중에 코드를 읽는 개발자가 메서드가 참조에 의해 반환된다는 것을 기억하도록 도와줍니다.

[!code-csharp[FindReturningRef](../../../samples/snippets/csharp/new-in-7/MatrixSearch.cs#22_FindReturningRef "Find returning by reference")]

이제 메서드는 매트릭스의 정수 값에 대한 참조를 반환하므로 메서드가 호출되는 위치를 수정해야 합니다.  `var` 선언은 `valItem`이 이제 튜플이 아닌 `int`임을 의미합니다.

[!code-csharp[AssignRefReturnToValue](../../../samples/snippets/csharp/new-in-7/program.cs#23_AssignRefReturnToValue "Assign ref return to value")]

위 예제의 두 번째 `WriteLine` 문은 `24`가 아닌 `42` 값을 출력합니다. `valItem` 변수는 `ref int`가 아닌 `int`입니다. `var` 키워드를 사용하면 컴파일러가 형식을 지정할 수 있지만 `ref` 한정자가 암시적으로 추가되지 않습니다. 대신, `ref return`이 참조하는 값이 할당의 왼쪽에 있는 변수로 *복사*됩니다. 변수는 `ref` local이 아닙니다.

원하는 결과를 얻으려면 지역 변수 선언에 `ref` 한정자를 추가하여 반환 값이 참조인 경우 변수를 참조로 만들어야 합니다.

[!code-csharp[AssignRefReturn](../../../samples/snippets/csharp/new-in-7/program.cs#24_AssignRefReturn "Assign ref return")]

이제 위 예제의 두 번째 `WriteLine` 문은 매트릭스의 저장소가 수정되었음을 나타내는 `24` 값을 출력합니다. 지역 변수는 `ref` 한정자로 선언되었고 `ref` return을 사용합니다. `ref` 변수는 선언될 때 초기화해야 합니다. 선언과 초기화를 분할할 수 없습니다.

C# 언어에는 `ref` local 및 return을 잘못 사용하는 경우를 방지하는 세 가지 다른 규칙이 있습니다.

* 표준 메서드 반환 값을 `ref` 로컬 변수에 할당할 수 없습니다.
    - 이로 인해 `ref int i = sequence.Count();` 같은 문이 허용되지 않습니다.
* 메서드 실행보다 길게 수명이 연장되지 않는 변수로 `ref`를 반환할 수는 없습니다.
    - 이는 지역 변수 또는 비슷한 범위의 변수에 대한 참조를 반환할 수 없음을 의미합니다.
* `ref` local 및 return은 비동기 메서드와 함께 사용할 수 없습니다.
    - 컴파일러는 비동기 메서드가 반환될 때 참조된 변수가 최종 값으로 설정되었는지 여부를 알 수 없습니다.

ref local 및 ref return을 추가하면 값을 복사하거나 역참조 작업을 여러 번 수행하는 경우를 방지하여 더 효율적인 알고리즘이 가능해집니다. 

## <a name="local-functions"></a>로컬 함수

클래스에 대한 대부분의 디자인에는 한 위치에서만 호출되는 메서드가 포함됩니다. 이러한 추가 private 메서드는 각 메서드를 작고 집중되게 유지합니다. 그러나 이러한 메서드를 사용하면 클래스를 처음 읽을 때 이해하기가 더 어려울 수 있습니다. 이러한 메서드는 단일 호출 위치의 컨텍스트 외부에서 이해되어야 합니다.

해당 디자인의 경우 *로컬 함수*를 사용하여 다른 메서드의 컨텍스트 내부에서 메서드를 선언할 수 있습니다. 이렇게 하면 클래스 판독기는 로컬 메서드가 선언된 컨텍스트에서만 호출됨을 더 쉽게 알 수 있습니다.

로컬 함수의 매우 일반적인 두 가지 사용 사례는 public 반복기 메서드 및 public 비동기 메서드입니다. 두 메서드 형식 모두 프로그래머가 예상한 것보다 늦게 오류를 보고하는 코드를 생성합니다. 반복기 메서드의 경우 모든 예외는 반환된 시퀀스를 열거하는 코드를 호출할 경우에만 관찰됩니다. 비동기 메서드의 경우 모든 예외는 반환된 `Task`가 대기 상태일 경우에만 관찰됩니다.

먼저 반복기 메서드를 살펴보겠습니다.

[!code-csharp[IteratorMethod](../../../samples/snippets/csharp/new-in-7/Iterator.cs#25_IteratorMethod "Iterator method")]

반복기 메서드를 잘못 호출하는 아래 코드를 검사합니다.

[!code-csharp[CallIteratorMethod](../../../samples/snippets/csharp/new-in-7/program.cs#26_CallIteratorMethod "Call iterator method")]

`resultSet`가 만들어질 때가 아니라 `resultSet`가 반복될 때 예외가 throw됩니다.
이 포함된 예제에서 대부분 개발자는 문제를 빠르게 진단할 수 있습니다. 그러나 코드베이스가 커지면 반복기를 만드는 코드가 결과를 열거하는 코드와 가깝지 않은 경우가 많습니다. public 메서드가 모든 인수의 유효성을 검사하고 private 메서드가 열거형을 생성하도록 코드를 리팩터링할 수 있습니다.

[!code-csharp[IteratorMethodRefactored](../../../samples/snippets/csharp/new-in-7/Iterator.cs#27_IteratorMethodRefactored "Iterator method refactored")]

public 메서드가 반복기 메서드가 아니고 private 메서드만 `yield return` 구문을 사용하므로 이 리팩터링된 버전은 즉시 예외를 throw합니다. 그러나 이 리팩터링에서 문제가 발생할 수 있습니다. private 메서드는 public 인터페이스 메서드에서만 호출되어야 합니다. 그렇지 않으면 모든 인수 유효성 검사를 건너뛰기 때문입니다.
클래스 판독기는 전체 클래스를 읽고 `alphabetSubsetImplementation` 메서드에 대한 다른 참조를 검색하여 이 사실을 발견해야 합니다.

public API 메서드 내부에서 `alphabetSubsetImplementation`을 로컬 함수로 선언하여 디자인 의도를 더 분명히 설명할 수 있습니다.

[!code-csharp[22_IteratorMethodLocal](../../../samples/snippets/csharp/new-in-7/Iterator.cs#28_IteratorMethodLocal "Iterator method with local function")]

위 버전을 사용하면 로컬 메서드가 외부 메서드의 컨텍스트에서만 참조됩니다. 로컬 함수에 대한 규칙을 적용하면 개발자가 클래스의 다른 위치에서 로컬 함수를 실수로 호출하고 인수 유효성 검사를 건너뛸 수 없게 됩니다.

`async` 메서드에서 같은 방법을 사용하면 인수 유효성 검사에서 발생하는 예외가 비동기 작업이 시작되기 전에 throw됩니다.

[!code-csharp[TaskExample](../../../samples/snippets/csharp/new-in-7/AsyncWork.cs#29_TaskExample "Task returning method with local function")]

> [!NOTE]
> 로컬 함수가 지원하는 일부 디자인은 *람다 식*을 사용하여 완료할 수 있습니다. 관심 있는 사용자는 [차이점을 자세히 확인](../local-functions-vs-lambdas.md)할 수 있습니다.

## <a name="more-expression-bodied-members"></a>추가 식 본문 멤버

C# 6에서는 멤버 함수의 [식 본문 멤버](csharp-6.md#expression-bodied-function-members) 및 읽기 전용 속성을 추가했습니다. C# 7에서는 식으로 구현될 수 있는 허용 멤버를 확장합니다. C# 7에서는 *속성* 및 *인덱서*에 대한 *생성자*, *종료자* 및 `get`/`set` 접근자를 구현할 수 있습니다. 다음 코드는 각각에 대한 예제를 보여 줍니다.

[!code-csharp[ExpressionBodiedMembers](../../../samples/snippets/csharp/new-in-7/expressionmembers.cs#36_ExpressionBodiedEverything "new expression-bodied members")]

> [!NOTE]
> 이 예제에는 종료자가 필요하지 않지만 구문을 보여 주기 위해 표시됩니다. 관리되지 않는 리소스를 릴리스해야 하는 경우가 아니면 클래스에서 종료자를 구현하면 안 됩니다. 관리되지 않는 리소스를 직접 관리하지 않고 <xref:System.Runtime.InteropServices.SafeHandle> 클래스를 사용하는 것도 고려해야 합니다.

식 본문 멤버의 이러한 새 위치는 C# 언어에 대한 중요한 기준을 나타냅니다. 이러한 기능은 오픈 소스 [Roslyn](https://github.com/dotnet/Roslyn) 프로젝트에 대한 작업을 수행하는 커뮤니티 멤버가 구현했습니다.

## <a name="throw-expressions"></a>Throw 식

C#에서 `throw`는 항상 문이었습니다. `throw`는 식이 아닌 문이므로 이 문을 사용할 수 없는 C# 구문이 있었습니다. 이러한 구문에는 조건식, null 병합 식 및 몇몇 람다 식이 포함되었습니다. 식 본문 멤버가 추가됨에 따라 `throw` 식이 유용할 수 있는 추가 위치도 추가됩니다. 이러한 구문을 작성할 수 있도록 C# 7에서는 *throw 식*을 추가합니다.

구문은 항상 `throw` 문에 사용하던 것과 같습니다. 유일한 차이점은 이제 이러한 구문을 조건식과 같은 새 위치에 배치할 수 있다는 것입니다.

[!code-csharp[Throw_ExpressionExample](../../../samples/snippets/csharp/new-in-7/throwexpressions.cs#37_Throw_ExpressionExample "conditional throw expressions")]

이 기능을 통해 초기화 식에서 throw 식을 사용할 수 있습니다.

[!code-csharp[ThrowInInitialization](../../../samples/snippets/csharp/new-in-7/throwexpressions.cs#38_ThrowInInitialization "conditional throw expressions")]

이전에는 해당 초기화가 생성자 내에 있고 throw 문이 생성자 본문 내에 있어야 했습니다.


[!code-csharp[ThrowInConstructor](../../../samples/snippets/csharp/new-in-7/throwexpressions.cs#39_ThrowInConstructor "throw statements")]

> [!NOTE]
> 이전 구문에서는 둘 다 개체 생성 중에 예외가 throw됩니다. 이러한 경우는 보통 복구하기가 어렵습니다.
> 이런 이유로 생성 중에 예외를 throw하는 디자인은 사용하지 않는 것이 좋습니다.

## <a name="generalized-async-return-types"></a>일반화된 비동기 반환 형식

비동기 메서드에서 `Task` 개체를 반환하면 특정 경로에 성능 병목 현상이 발생할 수 있습니다. `Task`는 참조 형식이므로 이를 사용하는 것은 개체 할당을 의미합니다. `async` 한정자로 선언된 메서드가 캐시된 결과를 반환하거나 동기적으로 완료된 경우 코드의 성능이 중요한 섹션에서 추가 할당에 상당한 시간이 소요될 수 있습니다. 연속 루프에서 이러한 할당이 발생하면 큰 부담이 될 수 있습니다.

새로운 언어 기능은 비동기 메서드가 `Task`, `Task<T>` 및 `void` 외에 다른 형식을 반환할 수 있음을 의미합니다. 반환된 형식은 비동기 패턴을 충족해야 합니다. 즉, `GetAwaiter` 메서드에 액세스할 수 있어야 합니다. 한 가지 구체적인 예로 이 새로운 언어 기능을 사용할 수 있도록 `ValueTask` 형식이 .NET Framework에 추가되었습니다. 

[!code-csharp[UsingValueTask](../../../samples/snippets/csharp/new-in-7/AsyncWork.cs#30_UsingValueTask "Using ValueTask")]

> [!NOTE]
> <xref:System.Threading.Tasks.ValueTask%601> 형식을 사용하려면 NuGet 패키지 [`System.Threading.Tasks.Extensions`](https://www.nuget.org/packages/System.Threading.Tasks.Extensions/)를 추가해야 합니다.

간단한 최적화는 이전에 `Task`가 사용된 위치에서 `ValueTask`를 사용하는 것입니다. 그러나 추가 최적화를 직접 수행하려는 경우 비동기 작업에서 결과를 캐시하고 후속 호출에서 결과를 다시 사용할 수 있습니다. `ValueTask` 구조체에는 기존 비동기 메서드의 반환 값에서 `ValueTask`를 생성할 수 있도록 `Task` 매개 변수가 포함된 생성자가 있습니다.

[!code-csharp[AsyncOptimizedValueTask](../../../samples/snippets/csharp/new-in-7/AsyncWork.cs#31_AsyncOptimizedValueTask "Return async result or cached value")]
 
모든 성능 권장 사항처럼 코드를 대규모로 변경하기 전에 두 가지 버전을 모두 벤치마크해야 합니다.

## <a name="numeric-literal-syntax-improvements"></a>숫자 리터럴 구문 개선 사항

숫자 상수를 잘못 읽으면 코드를 처음 읽을 때 이해하기가 더 어려울 수 있습니다. 이 문제는 일반적으로 해당 숫자가 숫자 값이 아닌 비트 마스크나 다른 기호로 사용될 경우 발생합니다. C# 7에는 의도한 용도에 맞게 가장 읽기 쉬운 방식으로 숫자를 더 쉽게 작성할 수 있는 두 가지 새로운 기능인 *이진 리터럴* 및 *숫자 구분 기호*가 포함됩니다.

비트 마스크를 만들 경우 또는 숫자의 이진 표현이 가장 읽기 쉬운 코드를 만들 때마다 해당 숫자를 이진으로 작성하세요.

[!code-csharp[BinaryConstants](../../../samples/snippets/csharp/new-in-7/Program.cs#32_BinaryConstants "Binary constants")]

상수의 시작 부분에 있는 `0b`는 숫자가 이진 숫자로 작성되었음을 나타냅니다.

이진 숫자는 매우 길어질 수 있으므로 `_`을 숫자 구분 기호로 추가하면 비트 패턴을 더 쉽게 확인할 수 있습니다.

[!code-csharp[ThousandSeparators](../../../samples/snippets/csharp/new-in-7/Program.cs#33_ThousandSeparators "Thousands separators")]

숫자 구분 기호는 상수 내의 어디에나 나타날 수 있습니다. 기본 10개 숫자의 경우 일반적으로 숫자 구분 기호가 천 단위 구분 기호로 사용됩니다.

[!code-csharp[LargeIntegers](../../../samples/snippets/csharp/new-in-7/Program.cs#34_LargeIntegers "Large integer")]

숫자 구분 기호는 `decimal`, `float` 및 `double` 형식에서도 사용할 수 있습니다.

[!code-csharp[OtherConstants](../../../samples/snippets/csharp/new-in-7/Program.cs#35_OtherConstants "non-integral constants")]

함께 사용하면 숫자 상수를 훨씬 더 읽기 쉽게 선언할 수 있습니다.
