---
title: C# 6의 새로운 기능 - C# 가이드
description: C# 버전 6의 새로운 기능을 알아봅니다.
keywords: .NET, .NET Core
author: BillWagner
ms.date: 09/22/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 4d879f69-f889-4d3f-a781-75194e143400
ms.openlocfilehash: ea54e9a05120134eea8e1bc9d82302a7513b43e7
ms.sourcegitcommit: 935d5267c44f9bce801468ef95f44572f1417e8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="whats-new-in-c-6"></a>C# 6의 새로운 기능

C#의 6.0 릴리스에는 개발자의 생산성을 개선하는 많은 기능이 추가되었습니다. 이 릴리스의 기능은 다음과 같습니다.

* [읽기 전용 Auto 속성](#read-only-auto-properties):
    - 생성자에서만 설정할 수 있는 읽기 전용 auto 속성을 만들 수 있습니다.
* [Auto 속성 이니셜라이저](#auto-property-initializers)
    - Auto 속성의 초기 값을 설정하는 초기화 식을 작성할 수 있습니다.
* [식 본문 함수 멤버](#expression-bodied-function-members):
    - 람다 식을 사용하여 한 줄 메서드를 작성할 수 있습니다.
* [using static](#using-static):
    - 단일 클래스의 모든 메서드를 현재 네임스페이스로 가져올 수 있습니다.
* [Null - 조건 연산자](#null-conditional-operators):
    - Null 조건 연산자를 사용하여 null이 있는지 계속 확인하면서 개체의 멤버에 간결하고 안전하게 액세스할 수 있습니다.
* [문자열 보간](#string-interpolation):
    - 위치 인수 대신 인라인 식을 사용하여 문자열 서식 지정 식을 작성할 수 있습니다.
* [예외 필터](#exception-filters):
    - 예외 속성 또는 기타 프로그램 상태에 따라 식을 catch할 수 있습니다. 
* [nameof 식](#nameof-expressions):
    - 컴파일러를 통해 기호의 문자열 표현을 생성할 수 있습니다.
* [catch 및 finally 블록의 await](#await-in-catch-and-finally-blocks):
    - 이전에 허용되지 않았던 위치에서 `await` 식을 사용할 수 있습니다.
* [인덱스 이니셜라이저](#index-initializers):
    - 시퀀스 컨테이너 및 연관 컨테이너에 대한 초기화 식을 작성할 수 있습니다.
* [컬렉션 이니셜라이저의 확장 메서드](#extension-add-methods-in-collection-initializers):
    - 컬렉션 이니셜라이저는 멤버 메서드 이외에 액세스 가능한 확장 메서드를 사용할 수 있습니다.
* [향상된 오버로드 확인](#improved-overload-resolution):
    - 이전에 모호한 호출을 생성한 일부 구문이 이제 제대로 확인됩니다.

이러한 기능의 전반적인 영향은 더 읽기 쉬운 더 간결한 코드를 작성한다는 것입니다. 많은 일반적인 사례에 대한 더 적은 의례가 구문에 포함됩니다. 더 적은 의례로 디자인 의도를 더 쉽게 파악할 수 있습니다. 이러한 기능을 알고 있으면 생산성이 향상되고 더 읽기 쉬운 코드를 작성하고 언어의 구문보다 핵심 기능에 더 집중하게 됩니다.

이 항목의 나머지 부분에서는 이러한 기능을 각각 자세히 설명합니다.

## <a name="auto-property-enhancements"></a>Auto 속성 향상된 기능 

자동으로 구현된 속성에 대한 구문(대개 “auto 속성"이라고 함) 덕분에 간단한 get 및 set 접근자가 포함된 속성을 매우 쉽게 만들 수 있습니다:

[!code-csharp[ClassicAutoProperty](../../../samples/snippets/csharp/new-in-6/oldcode.cs#ClassicAutoProperty)]

하지만 이 간단한 구문은 auto 속성 사용을 지원할 수 있는 디자인 종류를 제한했습니다. C# 6에서는 더 많은 시나리오에서 사용할 수 있도록 auto 속성 기능이 향상되었습니다. 지원 필드를 직접 자주 선언하고 조작하는 더 자세한 구문을 대신 사용할 필요가 없습니다.

새 구문은 읽기 전용 속성에 대한 시나리오와 auto 속성 뒤에서 변수 저장소를 초기화하는 시나리오를 처리합니다.

### <a name="read-only-auto-properties"></a>읽기 전용 auto 속성

*읽기 전용 auto 속성*은 변경할 수 없는 형식을 만드는 더 간결한 구문을 제공합니다. C#의 이전 버전에서 변경할 수 없는 형식을 사용하는 것과 가장 가까운 방법은 private setter를 선언하는 것이었습니다.

[!code-csharp[ClassicReadOnlyAutoProperty](../../../samples/snippets/csharp/new-in-6/oldcode.cs#ClassicReadOnlyAutoProperty)]
 
이 구문을 사용하면 컴파일러에서는 형식이 실제로 변경할 수 없는지 확인하지 않습니다. `FirstName` 및 `LastName` 속성이 클래스 외부의 코드에서 수정되지 않도록만 적용합니다.

읽기 전용 auto 속성은 실제 읽기 전용 동작을 구현합니다. get 접근자만 사용하여 auto 속성을 선언합니다.

[!code-csharp[ReadOnlyAutoProperty](../../../samples/snippets/csharp/new-in-6/newcode.cs#ReadOnlyAutoProperty)]

`FirstName` 및 `LastName` 속성은 생성자 본문에서만 설정할 수 있습니다.

[!code-csharp[ReadOnlyAutoPropertyConstructor](../../../samples/snippets/csharp/new-in-6/newcode.cs#ReadOnlyAutoPropertyConstructor)]

다른 메서드에서 `LastName`을 설정하려고 하면 `CS0200` 컴파일 오류가 생성됩니다.

```csharp
public class Student
{
    public string LastName { get;  }

    public void ChangeName(string newLastName)
    {
        // Generates CS0200: Property or indexer cannot be assigned to -- it is read only
        LastName = newLastName;
    }
}
```

이 기능은 변경할 수 없는 형식을 만들고 더 간결하고 편리한 auto 속성 구문을 사용하기 위한 실제 언어 지원을 구현합니다.

### <a name="auto-property-initializers"></a>Auto 속성 이니셜라이저

*Auto 속성 이니셜라이저*를 통해 속성 선언의 일부로 auto 속성의 초기 값을 선언할 수 있습니다.  이전 버전에서는 이러한 속성에 setter를 포함해야 하고, 지원 필드에서 사용되는 데이터 저장소를 초기화하려면 해당 setter를 사용해야 합니다. 이름이 포함된 학생 및 학생의 성적 목록에 이 클래스를 사용하는 것이 좋습니다.

[!code-csharp[Construction](../../../samples/snippets/csharp/new-in-6/oldcode.cs#Construction)]
 
이 클래스가 커지면 다른 생성자를 포함할 수 있습니다. 각 생성자는 이 필드를 초기화해야 합니다. 초기화하지 않으면 오류가 발생합니다.

C# 6에서는 auto 속성 선언에서 auto 속성에 사용되는 저장소의 초기 값을 할당할 수 있습니다.

[!code-csharp[Initialization](../../../samples/snippets/csharp/new-in-6/newcode.cs#Initialization)]

`Grades` 멤버는 선언된 위치에서 초기화됩니다. 따라서 더 쉽게 정확히 한 번 초기화를 수행할 수 있습니다. 초기화가 속성 선언의 일부이므로 `Student` 개체에 대한 public 인터페이스를 통해 저장소를 균등하게 할당하기 쉽습니다.

다음과 같이 속성 이니셜라이저는 읽기 전용 속성 및 읽기/쓰기 속성과 함께 사용할 수 있습니다.

[!code-csharp[ReadWriteInitialization](../../../samples/snippets/csharp/new-in-6/newcode.cs#ReadWriteInitialization)]

## <a name="expression-bodied-function-members"></a>식 본문 함수 멤버

여기서 작성하는 많은 멤버의 본문은 식으로 표현될 수 있는 하나의 식으로만 구성됩니다. 대신 식 본문 멤버를 작성하여 해당 구문을 줄일 수 있습니다. 이 내용은 메서드 및 읽기 전용 속성에 적용됩니다. 예를 들어 `ToString()`의 재정의가 좋은 예입니다.

[!code-csharp[ToStringExpressionMember](../../../samples/snippets/csharp/new-in-6/newcode.cs#ToStringExpressionMember)]

읽기 전용 속성에서도 식 본문 멤버를 사용할 수 있습니다.

[!code-csharp[FullNameExpressionMember](../../../samples/snippets/csharp/new-in-6/newcode.cs#FullNameExpressionMember)]

## <a name="using-static"></a>using static

*using static* 향상된 기능을 사용하여 단일 클래스의 정적 메서드를 가져올 수 있습니다. 이전에는 `using` 문으로 네임스페이스의 모든 형식을 가져왔습니다. 

일반적으로 전체 코드에서 클래스의 정적 메서드를 사용합니다. 클래스 이름을 반복해서 입력하면 코드의 의미가 모호해질 수 있습니다. 일반적인 예는 많은 숫자 계산을 수행하는 클래스를 작성하는 경우입니다.
코드는 <xref:System.Math.Sin%2A>, <xref:System.Math.Sqrt%2A>, 및 <xref:System.Math> 클래스의 여러 가지 메서드에 대한 기타 호출로 복잡해집니다. 새 `using static` 구문을 사용하면 이러한 클래스를 훨씬 더 깔끔하게 읽을 수 있습니다. 사용 중인 클래스를 지정합니다.

[!code-csharp[UsingStaticMath](../../../samples/snippets/csharp/new-in-6/newcode.cs#UsingStaticMath)]

이제 <xref:System.Math> 클래스를 한정하지 않고 <xref:System.Math> 클래스에서 정적 메서드를 사용할 수 있습니다. <xref:System.Math> 클래스는 인스턴스 메서드를 포함하지 않으므로 이 기능에 대한 좋은 사용 사례입니다. `using static`을 사용하여 정적 및 인스턴스 메서드가 둘 다 포함된 클래스에 대한 클래스의 정적 메서드를 가져올 수도 있습니다. 가장 유용한 예 중 하나는 <xref:System.String>입니다.

[!code-csharp[UsingStatic](../../../samples/snippets/csharp/new-in-6/newcode.cs#UsingStatic)]

> [!NOTE]
> static using 문에서는 정규화된 클래스 이름 `System.String`을 사용해야 합니다. 대신 `string` 키워드를 사용할 수 없습니다. 

이제 <xref:System.String> 클래스에 정의된 정적 메서드를 해당 클래스의 멤버로 한정하지 않고 해당 메서드를 호출할 수 있습니다.

[!code-csharp[UsingStaticString](../../../samples/snippets/csharp/new-in-6/newcode.cs#UsingStaticString)]

`static using` 기능 및 확장 메서드는 흥미로운 방식으로 상호 작용하고 언어 디자인에는 해당 상호 작용을 구체적으로 처리하는 몇 가지 규칙이 포함됩니다. 목적은 기존 코드베이스에서 주요한 변경이 발생할 가능성을 최소화하는 것입니다.

확장 메서드는 정적 메서드로 호출될 때가 아닌 확장 메서드 호출 구문을 사용하여 호출될 때만 범위 내에 있습니다.
일반적으로 LINQ 쿼리에서 이를 확인할 수 있습니다. <xref:System.Linq.Enumerable>을 가져와 LINQ 패턴을 가져올 수 있습니다.

[!code-csharp[UsingStaticLinq](../../../samples/snippets/csharp/new-in-6/newcode.cs#usingStaticLinq)]

이 작업은 <xref:System.Linq.Enumerable> 클래스의 모든 메서드를 가져옵니다.
그러나 확장 메서드는 확장 메서드로 호출될 때만 범위 내에 있습니다. 정적 메서드 구문을 사용하여 호출될 경우 범위 내에 있지 않습니다.

[!code-csharp[UsingStaticLinqMethod](../../../samples/snippets/csharp/new-in-6/newcode.cs#UsingStaticLinkMethod)]

이 결정은 일반적으로 확장 메서드는 확장 메서드 호출 식을 사용하여 호출되기 때문입니다. 드물지만 확장 메서드가 정적 메서드 호출 구문을 사용하여 호출될 경우에는 모호성이 해결됩니다.
호출의 일부로 클래스 이름을 요구하는 것이 좋습니다.

`static using`의 마지막 한 가지 기능이 있습니다. `static using` 지시문은 모든 중첩 형식도 가져옵니다. 이 기능을 통해 한정 없이 중첩 형식을 참조할 수 있습니다.

## <a name="null-conditional-operators"></a>Null 조건 연산자

Null 값은 코드를 복잡하게 만듭니다. `null`을 역참조하지 않는지 확인하려면 변수의 모든 액세스를 확인해야 합니다. *null 조건 연산자*를 사용하면 이러한 확인이 훨씬 더 쉽고 유연합니다.

멤버 액세스 `.`를 `?.`로 바꾸면 됩니다.

[!code-csharp[NullConditional](../../../samples/snippets/csharp/new-in-6/program.cs#NullConditional)]

이전 예제에서 person 개체가 `null`인 경우 `first` 변수에 `null`이 할당됩니다. null이 아닌 경우 `FirstName` 속성의 값이 할당됩니다. 가장 중요한 점은 `?.`는 `person` 변수가 `null`일 경우 이 코드 줄이 `NullReferenceException`을 생성하지 않음을 의미한다는 것입니다. 대신 이 코드 줄은 단락되고 `null`을 생성합니다.

또한 이 식은 `person` 값에 관계없이 `string`을 반환합니다.
단락의 경우 반환된 `null` 값은 전체 식과 일치하도록 형식화됩니다.

이 구문을 *null 결합* 연산자와 함께 사용하여 속성 중 하나가 `null`일 경우 기본값을 할당합니다.

[!code-csharp[NullCoalescing](../../../samples/snippets/csharp/new-in-6/program.cs#NullCoalescing)]

`?.` 연산자의 오른쪽 피연산자는 속성 또는 필드로 제한되지 않습니다.
메서드를 조건부로 호출하는 데 사용할 수도 있습니다. null 조건 연산자와 함께 멤버 함수를 사용하는 가장 일반적인 경우는 `null`일 수 있는 대리자(또는 이벤트 처리기)를 안전하게 호출하는 것입니다.  이 작업을 수행하려면 `?.` 연산자를 통해 대리자의 `Invoke` 메서드를 호출하여 멤버에 액세스합니다. 예제는  
[대리자 패턴](../delegates-patterns.md#handling-null-delegates) 항목에서 확인할 수 있습니다.

`?.` 연산자 규칙을 적용하면 연산자의 왼쪽이 한 번만 계산됩니다. 이 기능은 중요하고 이벤트 처리기 사용 예제를 비롯한 많은 관용구를 구현합니다. 먼저 이벤트 처리기 사용법을 살펴보겠습니다. C#의 이전 버전에서는 다음과 같이 코드를 작성하는 것이 좋습니다.

```csharp
var handler = this.SomethingHappened;
if (handler != null)
    handler(this, eventArgs);
```

더 간단한 구문보다 이 방법을 사용하는 것이 좋습니다.

```csharp
// Not recommended
if (this.SomethingHappened != null)
    this.SomethingHappened(this, eventArgs);
```

> [!IMPORTANT]
> 이전 예제에서는 경합 상태를 소개합니다. `SomethingHappened` 이벤트는 `null`에 대해 확인될 경우 구독자를 포함할 수 있고 해당 구독자는 이벤트가 발생하기 전에 제거되었을 수 있습니다. 이로 인해 <xref:System.NullReferenceException>이 throw됩니다.

이 두 번째 버전에서 `SomethingHappened` 이벤트 처리기는 테스트될 때 null이 아닐 수 있지만 다른 코드가 처리기를 제거할 경우 이벤트 처리기가 호출될 때 null일 수 있습니다.

컴파일러에서는 `?.` 식의 왼쪽(`this.SomethingHappened`)이 한 번 계산되도록 하는 `?.` 연산자에 대한 코드를 생성하고 결과는 캐시됩니다.

```csharp
// preferred in C# 6:
this.SomethingHappened?.Invoke(this, eventArgs);
```

왼쪽이 한 번만 계산되도록 하면 `?.`의 왼쪽에서 메서드 호출을 비롯한 모든 식을 사용할 수 있습니다. 이 방법에서 의도하지 않은 결과가 발생하더라도 한 번 계산되므로 의도하지 않은 결과도 한 번만 발생합니다. [이벤트](../events-overview.md#language-support-for-events)에 대한 내용에서 예제를 확인할 수 있습니다.

## <a name="string-interpolation"></a>문자열 보간

C# 6에는 형식 문자열 및 다른 문자열 값을 생성하기 위해 계산되는 식에서 문자열을 작성하기 위한 새 구문이 포함됩니다.

기존에는 `string.Format` 같은 메서드에서 위치 매개 변수를 사용해야 했습니다.

[!code-csharp[stringFormat](../../../samples/snippets/csharp/new-in-6/oldcode.cs#stringFormat)]

C# 6에서는 새 [문자열 보간](../language-reference/tokens/interpolated.md) 기능을 통해 서식 문자열에 식을 포함할 수 있습니다. 간단히 문자열 앞에 `$`를 추가하면 됩니다.

[!code-csharp[stringInterpolation](../../../samples/snippets/csharp/new-in-6/newcode.cs#FullNameExpressionMember)]

이 초기 예제에서는 대체 식에 속성 식을 사용했습니다. 임의 식을 사용하도록 이 구문을 확장할 수 있습니다. 예를 들어 보간의 일부로 학생의 성적 점수 평균을 계산할 수 있습니다.

[!code-csharp[stringInterpolationExpression](../../../samples/snippets/csharp/new-in-6/newcode.cs#stringInterpolationExpression)]

이전 예제를 실행하면 `Grades.Average()`에 대한 출력에 원하는 것보다 더 많은 소수 자릿수가 포함됨을 알 수 있습니다. 문자열 보간 구문은 이전 서식 메서드를 통해 제공되는 모든 서식 문자열을 지원합니다. 중괄호 내에 서식 문자열을 추가합니다. 서식 지정할 식 다음에 `:`을 추가합니다.

[!code-csharp[stringInterpolationFormat](../../../samples/snippets/csharp/new-in-6/newcode.cs#stringInterpolationFormat)]

이전 코드 줄은 소수 자릿수가 두 개인 부동 소수점 숫자로 `Grades.Average()` 값의 형식을 지정합니다.

`:`은 항상 서식이 지정되는 식과 서식 문자열 사이의 구분 기호로 해석됩니다. 식에서 `:`을 조건 연산자와 같은 다른 방식으로 사용할 경우 이로 인해 문제가 발생할 수 있습니다.

```csharp
public string GetGradePointPercentages() =>
    $"Name: {LastName}, {FirstName}. G.P.A: {Grades.Any() ? Grades.Average() : double.NaN:F2}";
```

이전 예제에서 `:`은 조건 연산자의 일부가 아닌 서식 문자열의 시작으로 구문 분석됩니다. 이 문제가 발생할 때마다 식을 괄호로 묶어 컴파일러가 식을 의도한 대로 해석하게 할 수 있습니다.

[!code-csharp[stringInterpolationConditional](../../../samples/snippets/csharp/new-in-6/newcode.cs#stringInterpolationConditional)]

중괄호 사이에 배치할 수 있는 식에 대한 제한 사항은 없습니다. 보간된 문자열 내부에서 복잡한 LINQ 쿼리를 실행하여 계산을 수행하고 결과를 표시할 수 있습니다.

[!code-csharp[stringInterpolationLinq](../../../samples/snippets/csharp/new-in-6/newcode.cs#stringInterpolationLinq)]

이 샘플에서 문자열 보간 식을 또 다른 문자열 보간 식 내부에 중첩할 수도 있음을 알 수 있습니다. 이 예제는 프로덕션 코드에서 원하는 것보다 훨씬 더 복잡할 수 있습니다.
오히려 기능의 범위를 잘 보여 줍니다. 모든 C# 식은 보간된 문자열의 중괄호 사이에 배치할 수 있습니다.

### <a name="string-interpolation-and-specific-cultures"></a>문자열 보간 및 특정 문화권

이전 섹션에 나와 있는 모든 예제는 코드가 실행되는 컴퓨터에서 현재 문화권과 언어를 사용하여 문자열의 서식을 지정합니다. 일반적으로 특정 문화권을 사용하여 생성된 문자열의 서식을 지정해야 할 수 있습니다.
이렇게 하려면 문자열 보간에 의해 생성된 개체가 암시적으로 <xref:System.FormattableString>으로 변환될 수 있다는 사실을 참고하세요.

<xref:System.FormattableString> 인스턴스에는 서식 문자열 및 문자열로 변환하기 전에 식을 계산한 결과가 포함됩니다. <xref:System.FormattableString>의 public 메서드를 사용하여 문자열의 서식을 지정할 때 문화권을 지정할 수 있습니다. 예를 들어 다음 예에서는 독일 문화권을 사용하여 문자열을 생성합니다. (',' 문자를 소수 구분 기호로 사용하고 '.' 문자를 천 단위 구분 기호로 사용합니다.)

```csharp
FormattableString str = $"Average grade is {s.Grades.Average()}";
var gradeStr = str.ToString(new System.Globalization.CultureInfo("de-DE"));
```

자세한 내용은 [문자열 보간](../language-reference/tokens/interpolated.md) 토픽을 참조하세요.

## <a name="exception-filters"></a>예외 필터

C# 6의 또 다른 새로운 기능은 *예외 필터*입니다. 예외 필터는 지정된 catch 절을 적용해야 하는 경우를 결정하는 절입니다.
예외 필터에 사용된 식이 `true`로 계산되면 catch 절은 예외에 대한 일반적인 처리를 수행합니다. 식이 `false`로 계산되면 `catch` 절을 건너뜁니다.

한 가지 사용 예는 예외에 대한 정보를 검사하여 `catch` 절이 예외를 처리할 수 있는지 결정하는 것입니다.

[!code-csharp[ExceptionFilter](../../../samples/snippets/csharp/new-in-6/NetworkClient.cs#ExceptionFilter)]

예외 필터에서 생성된 코드는 throw되지만 처리되지 않은 예외에 대한 더 나은 정보를 제공합니다. 예외 필터가 언어에 추가되기 전에 다음과 같이 코드를 만들어야 합니다.

[!code-csharp[ExceptionFilterOld](../../../samples/snippets/csharp/new-in-6/NetworkClient.cs#ExceptionFilterOld)]

이러한 두 개의 예제에서는 예외가 throw된 지점이 서로 다릅니다.
이전 코드에서 `throw` 절이 사용된 경우 크래시 덤프의 스택 추적 분석 또는 검사에서는 catch 절의 `throw` 문에서 예외가 throw되었음을 보여 줍니다. 실제 예외 개체에는 원래 호출 스택이 포함되지만 이 throw 지점과 원래 throw 지점 위치 사이에 있는 호출 스택의 변수에 대한 모든 기타 정보가 손실되었습니다. 

예외 필터를 사용하여 코드를 처리하는 방법과 달리 예외 필터 식은 `false`로 계산됩니다. 따라서 실행이 `catch` 절로 들어가지 않습니다. `catch` 절이 실행되지 않으면 스택 해제가 수행되지 않습니다. 이는 나중에 수행되는 디버깅 활동을 위해 원래 throw 위치가 보존됨을 의미합니다.

예외 형식만 사용하는 대신 예외의 필드 또는 속성을 계산해야 할 때마다 예외 필터를 사용하여 더 많은 디버깅 정보를 보존합니다.

예외 필터를 사용하는 또 다른 권장 패턴은 루틴을 기록하는 데 사용하는 것입니다. 이 방법은 예외 필터가 `false`로 계산될 때 예외 throw 지점을 보존하는 방식을 이용합니다.

로깅 메서드는 인수가 무조건 `false`를 반환하는 예외인 메서드입니다.

[!code-csharp[ExceptionFilterLogging](../../../samples/snippets/csharp/new-in-6/ExceptionFilterHelpers.cs#ExceptionFilterLogging)]

예외를 기록하려고 할 때마다 catch 절을 추가하고 이 메서드를 예외 필터로 사용할 수 있습니다.

[!code-csharp[LogException](../../../samples/snippets/csharp/new-in-6/program.cs#LogException)]

예외는 catch되지 않습니다. `LogException` 메서드는 항상 `false`를 반환하기 때문입니다. 항상 false인 예외 필터는 이 로깅 처리기를 다른 예외 처리기 앞에 배치할 수 있음을 의미합니다.

[!code-csharp[LogExceptionRecovery](../../../samples/snippets/csharp/new-in-6/program.cs#LogExceptionRecovery)]

이전 예제에서는 예외 필터의 매우 중요한 부분을 강조합니다.
예외 필터는 더 일반적인 예외 catch 절이 더 구체적인 절 앞에 나타날 수 있는 시나리오를 구현합니다. 같은 예외 형식이 여러 catch 절에 표시되게 할 수도 있습니다.

[!code-csharp[HandleNotChanged](../../../samples/snippets/csharp/new-in-6/NetworkClient.cs#HandleNotChanged)]

또 다른 권장 패턴을 사용하면 디버거가 연결될 때 catch 절이 예외를 처리할 수 없습니다. 이 방법을 사용하여 디버거를 통해 응용 프로그램을 실행하고 예외가 throw될 때 실행을 중지할 수 있습니다.

코드에서 디버거가 연결되지 않을 때만 복구 코드가 실행되도록 예외 필터를 추가합니다.

[!code-csharp[LogExceptionDebugger](../../../samples/snippets/csharp/new-in-6/program.cs#LogExceptionDebugger)]

코드에 이 예외 코드를 추가한 후 처리되지 않은 모든 예외에서 중단되도록 디버거를 설정합니다. 디버거에서 프로그램을 실행합니다. 그러면 `PerformFailingOperation()`이 `RecoverableException`을 throw할 때마다 디버거가 중단됩니다.
false 반환 예외 필터로 인해 catch 절이 실행되지 않으므로 디버거가 프로그램을 중단합니다.

## <a name="nameof-expressions"></a>`nameof` 식

`nameof` 식은 기호 이름으로 계산됩니다. 변수, 속성 또는 멤버 필드의 이름이 필요할 때마다 도구를 작동하는 것이 좋습니다.

`nameof`의 가장 일반적인 사용 예 중 하나는 예외를 일으킨 기호의 이름을 제공하는 것입니다.

[!code-csharp[nameof](../../../samples/snippets/csharp/new-in-6/NewCode.cs#UsingStaticString)]

또 다른 사용 예는 `INotifyPropertyChanged` 인터페이스를 구현하는 XAML 기반 응용 프로그램에서 사용하는 것입니다.

[!code-csharp[nameofNotify](../../../samples/snippets/csharp/new-in-6/viewmodel.cs#nameofNotify)]

상수 문자열에 비해 `nameof` 연산자 사용의 장점은 도구가 기호를 인식할 수 있다는 것입니다. 리팩터링 도구를 사용하여 기호 이름을 바꿀 경우 `nameof` 식에서 이름을 바꿉니다. 상수 문자열에는 이 장점이 없습니다. 원하는 편집기에서 직접 변수 이름을 바꿔 보세요. 그러면 모든 `nameof` 식도 업데이트됩니다.

인수의 정규화된 이름을 사용하는 경우에도 `nameof` 식은 인수의 정규화되지 않은 이름을 생성합니다(이전 예제에서는 `LastName`).

[!code-csharp[QualifiedNameofNotify](../../../samples/snippets/csharp/new-in-6/viewmodel.cs#QualifiedNameofNotify)]

이 `nameof` 식은 `UXComponents.ViewModel.FirstName`이 아닌 `FirstName`을 생성합니다.

## <a name="await-in-catch-and-finally-blocks"></a>Catch 및 Finally 블록의 Await

C# 5에는 `await` 식을 배치할 수 있는 위치에 대한 여러 제한 사항이 있었습니다.
제한 사항 중 하나가 C# 6에서 제거되었습니다. 이제 `catch` 또는 `finally` 식에서 `await`를 사용할 수 있습니다. 

catch 및 finally 블록에 await 식을 추가하면 식 처리 방식이 복잡하게 보일 수 있습니다. 어떻게 보이는지 설명하는 예제를 추가해 보겠습니다. 비동기 메서드의 finally 절에서 await 식을 사용할 수 있습니다.

C# 6에서는 catch 식에서 대기할 수도 있습니다. 이 방법이 로깅 시나리오에서 가장 일반적을 사용됩니다.

[!code-csharp[AwaitFinally](../../../samples/snippets/csharp/new-in-6/NetworkClient.cs#AwaitFinally)]

`catch` 및 `finally` 절 내부에 `await` 지원을 추가하기 위한 구현 세부 정보에 따라 동작이 동기 코드에 대한 동작과 일치합니다. `catch` 또는 `finally` 절에서 실행되는 코드가 throw되면 실행은 다음 바깥쪽 블록에서 적합한 `catch` 절을 검색합니다. 현재 예외가 있는 경우 해당 예외가 손실됩니다. `catch` 및 `finally` 절에서 대기된 식에서도 같은 작업이 수행됩니다. 적합한 `catch`가 검색되고 현재 예외(있는 경우)가 손실됩니다.  

> [!NOTE]
> 이 동작 때문에 새 예외가 추가되지 않도록 `catch` 및 `finally` 절을 신중하게 작성하는 것이 좋습니다.

## <a name="index-initializers"></a>인덱스 이니셜라이저

*인덱스 이니셜라이저*는 컬렉션 이니셜라이저를 더 일관되게 만드는 두 가지 기능 중 하나입니다. C#의 이전 예제에서는 시퀀스 스타일 컬렉션에서만 *컬렉션 이니셜라이저*를 사용할 수 있습니다.

[!code-csharp[ListInitializer](../../../samples/snippets/csharp/new-in-6/initializers.cs#ListInitializer)]

이제 <xref:System.Collections.Generic.Dictionary%602> 컬렉션 및 비슷한 형식에서도 사용할 수 있습니다.

[!code-csharp[DictionaryInitializer](../../../samples/snippets/csharp/new-in-6/initializers.cs#DictionaryInitializer)]

이 기능은 여러 버전에 대한 시퀀스 컨테이너를 대신한 것과 비슷한 구문을 사용하여 연관 컨테이너를 초기화할 수 있음을 의미합니다.

### <a name="extension-add-methods-in-collection-initializers"></a>컬렉션 이니셜라이저의 확장 `Add` 메서드

컬렉션을 더 쉽게 초기화하도록 하는 또 다른 기능은 `Add` 메서드에 *확장 메서드*를 사용하는 기능입니다. 이 기능은 Visual Basic의 패리티를 위해 추가되었습니다. 

이 기능은 의미상으로 새 항목을 추가하기 위해 다른 이름을 가진 메서드가 포함된 사용자 지정 컬렉션 클래스가 있는 경우 가장 유용합니다.

예를 들어 다음과 같은 학생 컬렉션을 살펴봅니다.

[!code-csharp[Enrollment](../../../samples/snippets/csharp/new-in-6/enrollment.cs#Enrollment)]

`Enroll` 메서드는 학생을 추가합니다. 그러나 `Add` 패턴을 따르지 않습니다.
C#의 이전 버전에서는 `Enrollment` 개체와 함께 컬렉션 이니셜라이저를 사용할 수 없습니다.

[!code-csharp[InitializeEnrollment](../../../samples/snippets/csharp/new-in-6/classList.cs#InitializeEnrollment)]

이제 함께 사용할 수 있지만 `Add`를 `Enroll`에 매핑하는 확장 메서드를 만들 경우로 제한됩니다.

[!code-csharp[ExtensionAdd](../../../samples/snippets/csharp/new-in-6/classList.cs#ExtensionAdd)]

이 기능을 통해 수행하는 작업은 확장 메서드를 만들어 컬렉션에 항목을 추가하는 모든 메서드를 `Add` 메서드에 매핑하는 것입니다. 

[!code-csharp[Enrollment](../../../samples/snippets/csharp/new-in-6/enrollment.cs#Enrollment)]
[!code-csharp[ExtensionAddSample](../../../samples/snippets/csharp/new-in-6/classList.cs#ExtensionAddSample)]

## <a name="improved-overload-resolution"></a>향상된 오버로드 확인

이 마지막 기능은 알지 못하는 기능일 수 있습니다. C# 컴파일러의 이전 버전에서 람다 식을 포함하는 일부 메서드 호출이 모호한 것으로 확인될 수 있는 구문이 있었습니다. 이 메서드를 살펴봅니다.

[!code-csharp[AsyncMethod](../../../samples/snippets/csharp/new-in-6/overloads.cs#AsyncMethod)]

C#의 이전 버전에서는 메서드 그룹 구문을 통한 해당 메서드 호출이 실패합니다.

[!code-csharp[MethodGroup](../../../samples/snippets/csharp/new-in-6/overloads.cs#MethodGroup)]
 
이전 컴파일러에서는 `Task.Run(Action)` 및 `Task.Run(Func<Task>())`를 제대로 구분할 수 없습니다. 이전 버전에서는 람다 식을 인수로 사용해야 했습니다.

[!code-csharp[Lambda](../../../samples/snippets/csharp/new-in-6/overloads.cs#Lambda)]

C# 6 컴파일러에서는 `Task.Run(Func<Task>())`가 더 나은 선택인지 제대로 결정합니다.
