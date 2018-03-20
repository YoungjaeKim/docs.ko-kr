---
title: "람다 식"
description: "인수로 전달할 수 있는 실행 코드 블록인 람다 식 사용 방법을 알아봅니다."
keywords: ".NET, .NET Core, 람다 식, 람다, 대리자"
ms-author: ronpet
author: rpetrusha
ms.date: 11/22/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: b6a0539a-8ce5-4da7-adcf-44be345a2714
ms.openlocfilehash: 6395d873c4a04501d25a2edbb1acc0a163dd3e5c
ms.sourcegitcommit: 83dd5ec003e788ccb3e33f3412a7af39ae347646
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="lambda-expressions"></a>람다 식 #

*람다 식*은 개체로 처리되는 코드 블록(식 또는 문 블록)입니다. 이 식은 인수로 메서드에 전달할 수 있으며 메서드 호출에서 반환될 수도 있습니다. 람다 식은 다음과 같은 경우에 광범위하게 사용됩니다.

- 실행될 코드를 <xref:System.Threading.Tasks.Task.Run(System.Action)>과 같은 비동기 메서드에 전달.

- [LINQ 쿼리 식](linq/index.md) 작성.

- [식 트리](expression-trees-building.md) 만들기.

람다 식은 대리자로 나타내거나 대리자로 컴파일되는 식 트리로 나타낼 수 있는 코드입니다. 람다 식의 특정 대리자 형식은 해당 매개 변수 및 반환 값에 따라 달라집니다. 값을 반환하지 않는 람다 식은 해당 매개 변수의 개수에 따라 특정 `Action` 대리자에 해당하고, 값을 반환하는 람다 식은 해당 매개 변수의 개수에 따라 특정 `Func` 대리자에 해당합니다. 예를 들어 매개 변수는 두 개지만 값을 반환하지 않는 람다 식은 <xref:System.Action%602> 대리자에 해당합니다. 매개 변수가 하나이고 값을 반환하는 람다 식은 <xref:System.Func%602> 대리자에 해당합니다.

람다 식은 [람다 선언 연산자](language-reference/operators/lambda-operator.md) `=>`을 사용하여 람다의 매개 변수 목록을 실행 코드와 구분합니다. 람다 식을 만들려면 람다 연산자 왼쪽에 입력 매개 변수(있는 경우)를 지정하고 다른 쪽에 식이나 문 블록을 삽입합니다. 예를 들어 한 줄 람다 식 `x => x * x`는 이름이 `x`인 매개 변수를 지정하고 `x` 제곱 값을 반환합니다. 다음 예제와 같이 대리자 형식에 이 식을 할당할 수도 있습니다.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/lambda1.cs#1)]

또는 메서드 인수로 직접 전달할 수 있습니다.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/lambda2.cs#2)]

## <a name="expression-lambdas"></a>식 람다 ##

 => 연산자의 오른쪽에 식이 있는 람다 식을 *식 람다*라고 합니다. 식 람다는 [식 트리](expression-trees.md)를 만드는 데 광범위하게 사용됩니다. 식 람다는 식의 결과를 반환하며 기본 형식은 다음과 같습니다.

```csharp
(input parameters) => expression
```

괄호는 람다 식에 입력 매개 변수가 하나뿐인 경우에만 생략할 수 있고 그렇지 않으면 생략할 수 없습니다. 입력 매개 변수가 0개이면 다음과 같이 빈 괄호를 지정합니다.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/expression3.cs#1)]

둘 이상의 입력 매개 변수는 다음과 같이 괄호로 묶고 쉼표로 구분해야 합니다.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/expression3.cs#2)]

일반적으로 컴파일러는 매개 변수 형식을 확인하는 데 형식 유추를 사용합니다. 그러나 컴파일러에서 입력 형식을 유추하기 어렵거나 유추할 수 없는 경우도 있습니다. 이런 경우 다음 예제와 같이 형식을 명시적으로 지정할 수 있습니다.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/expression3.cs#3)]

위의 예제에서 식 람다의 본문은 메서드 호출로 구성될 수 있습니다. 그러나 SQL Server 또는 EF(Entity Framework)와 같이 .NET Framework 외부에서 평가되는 식 트리를 만드는 경우 .NET 구현 컨텍스트 외부에서는 메서드가 의미가 없을 수 있으므로 람다 식에서 메서드 호출을 사용할 수 없도록 방지해야 합니다. 이 경우 메서드 호출을 사용하도록 선택하면 메서드 호출을 철저히 테스트하여 성공적으로 해결할 수 있도록 해야 합니다.

## <a name="statement-lambdas"></a>문 람다 ##

문 람다는 다음과 같이 중괄호 안에 문을 지정한다는 점을 제외하면 식 람다와 비슷합니다.

```csharp
(input parameters) => { statement; }
```

문 람다의 본문에 지정할 수 있는 문의 개수에는 제한이 없지만 일반적으로 2-3개 정도만 지정합니다.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/statement1.cs#1)]

무명 메서드와 마찬가지로 문 람다는 식 트리를 만드는 데 사용할 수 없습니다.

## <a name="async-lambdas"></a>비동기 람다 ##

[async](language-reference/keywords/async.md) 및 [await](language-reference/keywords/await.md) 키워드를 사용하여 비동기 처리를 통합하는 람다 식과 문을 쉽게 만들 수 있습니다. 예를 들어 예제에서는 비동기적으로 실행되는 `ShowSquares` 메서드를 호출합니다.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/async1.cs#1)]

비동기 메서드를 만들고 사용하는 방법에 대한 자세한 내용은 [Async 및 Await를 사용한 비동기 프로그래밍](programming-guide/concepts/async/index.md)을 참조하세요.

## <a name="lambda-expressions-and-tuples"></a>람다 식 및 튜플 ##

C# 7.0부터 C# 언어에서 튜플을 기본적으로 지원합니다. 람다 식에 인수로 튜플을 제공할 수 있으며 람다 식에서 튜플을 반환할 수도 있습니다. 경우에 따라 C# 컴파일러는 형식 유추를 사용하여 튜플 구성 요소의 형식을 확인할 수 있습니다. 

쉼표로 구분된 해당 구성 요소 목록을 괄호로 묶어 튜플을 정의합니다. 다음 예제에서는 5개 구성 요소가 있는 튜플을 사용하여 숫자 시퀀스를 람다 식에 전달하고 각 값을 두 배로 늘린 후 곱하기의 결과가 포함된, 5개 구성 요소가 있는 튜플을 반환합니다.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/tuples1.cs#1)]

일반적으로 튜플 필드의 이름은 `Item1`, `Item2` 등입니다. 그러나 다음 예제에서처럼 명명된 구성 요소가 있는 튜플을 정의할 수 있습니다.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/tuples2.cs#1)]

C#의 튜플 지원에 대한 자세한 내용은 [C# 튜플 형식](tuples.md)을 참조하세요.

## <a name="lambdas-with-the-standard-query-operators"></a>표준 쿼리 연산자와 람다 식 ##

다른 구현 중에 LINQ to Objects는 형식이 제네릭 대리자의 <xref:System.Func%601> 패밀리 중 하나인 입력 매개 변수를 사용합니다. 이러한 대리자는 형식 매개 변수를 사용하여 입력 매개 변수의 수와 형식 및 대리자의 반환 형식을 정의합니다. `Func` 대리자는 소스 데이터 집합에 있는 각 요소에 적용할 사용자 정의 식을 캡슐화하는 데 매우 유용합니다. 예를 들어 구문이 다음과 같은 <xref:System.Func%601> 대리자를 가정해 보세요.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/query1.cs#1)]

다음과 같은 코드로 대리자를 인스턴스화할 수 있습니다.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/query1.cs#2)]

여기서 `int`는 입력 매개 변수이고 `bool`은 반환 값입니다. 반환 값은 항상 마지막 형식 매개 변수에 지정됩니다. 다음 `Func` 대리자를 호출하면 입력 매개 변수가 5인지 여부를 나타내는 true 또는 false가 반환됩니다.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/query1.cs#3)]

<xref:System.Linq.Queryable> 형식에 정의되어 있는 표준 쿼리 연산자의 경우와 같이 인수 형식이 <xref:System.Linq.Expressions.Expression%601>인 경우에도 람다 식을 사용할 수 있습니다. <xref:System.Linq.Expressions.Expression%601> 인수를 지정하면 람다 식이 식 트리로 컴파일됩니다. 다음 예제에서는 [System.Linq.Enumerable.Count](xref:System.Linq.Enumerable.Count%60%601(System.Collections.Generic.IEnumerable{%60%600})) 표준 쿼리 연산자를 사용합니다.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/query1.cs#4)]

컴파일러에서 입력 매개 변수의 형식을 유추하거나 사용자가 형식을 명시적으로 지정할 수 있습니다. 이 람다 식은 2로 나누었을 때 나머지가 1인 정수(`n`)의 수를 계산합니다.

다음 예제에서는 숫자 시퀀스에서 조건을 만족하지 않는 첫 번째 숫자가 "9"이기 때문에 `numbers` 배열에서 "9" 앞에 오는 모든 요소가 포함된 시퀀스를 생성합니다.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/query1.cs#5)]

다음 예제에서는 입력 매개 변수를 괄호로 묶어 여러 개 지정합니다. 이 메서드는 값이 배열의 서수 위치보다 작은 숫자가 나타날 때까지 숫자 배열의 모든 요소를 반환합니다.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/query1.cs#6)]

## <a name="type-inference-in-lambda-expressions"></a>람다 식에서의 형식 유추 ##

컴파일러에서는 람다 식 본문, 매개 변수 형식 및 C# 언어 사양에 설명되어 있는 기타 요소를 기준으로 형식을 유추할 수 있기 때문에 대부분의 경우에는 람다 식을 작성할 때 입력 매개 변수의 형식을 지정하지 않아도 됩니다. 대부분의 표준 쿼리 연산자에서 첫 번째 입력 형식은 소스 시퀀스 요소의 형식입니다. `IEnumerable<Customer>`를 쿼리할 경우 입력 변수가 `Customer` 개체로 유추됩니다. 이는 이 개체의 메서드와 속성에 액세스할 수 있음을 의미합니다.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/infer1.cs#1)]

람다 식의 형식 유추에 대한 일반적인 규칙은 다음과 같습니다.

- 람다 식과 대리자 형식에 포함된 매개 변수 수가 같아야 합니다.

- 람다 식의 각 입력 인수는 해당되는 대리자 매개 변수로 암시적으로 변환할 수 있어야 합니다.

- 람다 식의 반환 값(있는 경우)은 대리자의 반환 형식으로 암시적으로 변환될 수 있어야 합니다.

공용 형식 시스템에는 "람다 식"이라는 개념이 기본적으로 포함되어 있지 않기 때문에 람다 식 자체에는 형식이 없습니다. 그러나 람다 식의 "형식"을 비공식적으로 언급해야 할 경우도 있는데 이 경우 형식은 대리자 형식 또는 람다 식이 변환되는 <xref:System.Linq.Expressions.Expression> 형식을 의미합니다.

## <a name="variable-scope-in-lambda-expressions"></a>람다 식의 변수 범위 ##

람다 식은 람다 함수를 정의하는 메서드 범위 내에 있거나 람다 식을 포함하는 형식 범위 내에 있는 *외부 변수*([무명 메서드](programming-guide/statements-expressions-operators/anonymous-methods.md) 참조)를 참조할 수 있습니다. 이러한 방식으로 캡처되는 변수는 변수가 범위를 벗어나 가비지 수집되는 경우에도 람다 식에 사용할 수 있도록 저장됩니다. 외부 변수는 명확하게 할당해야만 람다 식에 사용할 수 있습니다. 다음 예제에서는 이러한 규칙을 보여 줍니다.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/scope.cs#1)]

 람다 식의 변수 범위에는 다음과 같은 규칙이 적용됩니다.

- 캡처된 변수는 해당 변수를 참조하는 대리자가 가비지 수집 대상이 될 때까지 가비지 수집되지 않습니다.

- 람다 식에 사용된 변수는 외부 메서드에 표시되지 않습니다.

- 람다 식은 바깥쪽 메서드에서 `in`, `ref` 또는 `out` 매개 변수를 직접 캡처할 수 없습니다.

- 람다 식의 return 문에 의해서는 바깥쪽 메서드가 반환되지 않습니다.

- 점프문의 대상이 블록 외부에 있는 경우 람다 식에 람다 함수 내에 있는 `goto` 문, `break` 문 또는 `continue` 문을 포함할 수 없습니다. 대상이 블록 내에 있는 경우 람다 함수 블록 외부에 점프문을 사용해도 오류가 발생합니다.

## <a name="see-also"></a>참고 항목 ##

[LINQ(Language-Integrated Query)](../standard/using-linq.md)   
[무명 메서드](programming-guide/statements-expressions-operators/anonymous-methods.md)   
[식 트리](expression-trees.md)
