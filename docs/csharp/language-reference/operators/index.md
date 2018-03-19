---
title: "C# 연산자"
ms.date: 03/09/2017
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- cs.operators
helpviewer_keywords:
- boolean operators [C#]
- expressions [C#], operators
- logical operators [C#]
- operators [C#]
- Visual C#, operators
- indirection operators [C#]
- assignment operators [C#]
- shift operators [C#]
- relational operators [C#]
- bitwise operators [C#]
- address operators [C#]
- keywords [C#], operators
- arithmetic operators [C#]
ms.assetid: 0301e31f-22ad-49af-ac3c-d5eae7f0ac43
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 68da402bde670077e0700ce1ac60e7980c6568ad
ms.sourcegitcommit: 1c0b0f082b3f300e54b4d069b317ac724c88ddc3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/16/2018
---
# <a name="c-operators"></a>C# 연산자
C#에서는 많은 연산자를 제공하며, 이러한 연산자는 식에서 수행할 연산(수학, 인덱싱, 함수 호출 등)을 지정하는 기호입니다.  많은 연산자를 [오버로드](../../../csharp/programming-guide/statements-expressions-operators/overloadable-operators.md)하여 사용자 정의 형식에 적용되는 경우의 의미를 변경할 수 있습니다.  
  
 정수 계열 형식에 대한 연산(예: `==`, `!=`, `<`, `>`, `&`, `|`)은 일반적으로 열거형(`enum`에서 허용됩니다.  
  
 이 섹션에서는 우선 순위가 가장 높은 것부터 시작하여 순서대로 C# 연산자를 나열합니다.  각 섹션 내의 연산자는 동일한 우선 순위 수준을 공유합니다.  
  
## <a name="primary-operators"></a>기본 연산자  
 우선 순위가 가장 높은 연산자입니다.  연산자를 클릭하면 예제가 포함된 상세 페이지로 이동할 수 있습니다.  
  
 [x.y](../../../csharp/language-reference/operators/member-access-operator.md) – 멤버 액세스  
  
 [x?.y](../../../csharp/language-reference/operators/null-conditional-operators.md) – null 조건부 멤버 액세스  왼쪽 피연산자가 `null`인 경우 `null`을 반환합니다.  
 
 [x?[y]](../../../csharp/language-reference/operators/null-conditional-operators.md) - null 조건부 인덱스 액세스 왼쪽 피연산자가 `null`인 경우 `null`을 반환합니다.
 
 [f(x)](../../../csharp/language-reference/operators/invocation-operator.md) – 함수 호출  
  
 [a&#91;x&#93;](../../../csharp/language-reference/operators/index-operator.md) – 집계 개체 인덱싱  
   
 [x++](../../../csharp/language-reference/operators/increment-operator.md) – 후위 증가.  x의 값을 반환하고 1 더 큰 x 값(일반적으로 정수 1을 더함)으로 저장소 위치를 업데이트합니다.  
  
 [x--](../../../csharp/language-reference/operators/decrement-operator.md) –  후위 감소.  x의 값을 반환하고 1 더 작은 x 값(일반적으로 정수 1을 뺌)으로 저장소 위치를 업데이트합니다.  
  
 [new](../../../csharp/language-reference/keywords/new-operator.md) – 형식 인스턴스화.  
  
 [typeof](../../../csharp/language-reference/keywords/typeof.md) – 피연산자를 나타내는 System.Type 개체를 반환합니다.  
  
 [checked](../../../csharp/language-reference/keywords/checked.md) – 정수 연산에 오버플로 검사를 사용하도록 설정합니다.  
  
 [unchecked](../../../csharp/language-reference/keywords/unchecked.md) – 정수 연산에 오버플로 검사를 사용하지 않도록 설정합니다.  이것은 기본 컴파일러 동작입니다.  
  
 [default(T)](../../../csharp/programming-guide/statements-expressions-operators/default-value-expressions.md) – T 형식의 기본값을 반환합니다. 참조 형식의 경우 `null`, 숫자 형식의 경우 0, 구조체 형식의 경우 멤버에 입력된 0/`null`을 반환합니다.  
  
 [delegate](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md) – 대리자 인스턴스를 선언하고 반환합니다.  
  
 [sizeof](../../../csharp/language-reference/keywords/sizeof.md) – 형식 피연산자의 크기(바이트)를 반환합니다.  
  
 [->](../../../csharp/language-reference/operators/dereference-operator.md) – 멤버 액세스와 결합된 포인터 역참조입니다.  
  
## <a name="unary-operators"></a>단항 연산자  
 이러한 연산자는 다음 섹션보다 우선 순위가 높고 이전 섹션보다 우선 순위가 낮습니다.  연산자를 클릭하면 예제가 포함된 상세 페이지로 이동할 수 있습니다.  
  
 [+x](../../../csharp/language-reference/operators/addition-operator.md) – x의 값을 반환합니다.  
  
 [-x](../../../csharp/language-reference/operators/subtraction-operator.md) – 숫자 부정  
  
 [\!x](../../../csharp/language-reference/operators/logical-negation-operator.md) – 논리 부정  
  
 [~x](../../../csharp/language-reference/operators/bitwise-complement-operator.md) – 비트 보수  
  
 [++x](../../../csharp/language-reference/operators/increment-operator.md) – 전위 증가  1 더 큰 x 값(일반적으로 정수 1을 더함)으로 저장소 위치를 업데이트한 후 x의 값을 반환합니다.  
  
 [--x](../../../csharp/language-reference/operators/decrement-operator.md) – 전위 감소  1 더 작은 x 값(일반적으로 정수 1을 뺌)으로 저장소 위치를 업데이트한 후 x의 값을 반환합니다.  
  
 [(T)x](../../../csharp/language-reference/operators/invocation-operator.md) – 형식 캐스팅  
  
 [await](../../../csharp/language-reference/keywords/await.md) – `Task`를 대기합니다.  
  
 [&x](../../../csharp/language-reference/operators/and-operator.md) – 주소  
  
 [*x](../../../csharp/language-reference/operators/multiplication-operator.md) – 역참조  
  
## <a name="multiplicative-operators"></a>곱하기 연산자  
 이러한 연산자는 다음 섹션보다 우선 순위가 높고 이전 섹션보다 우선 순위가 낮습니다.  연산자를 클릭하면 예제가 포함된 상세 페이지로 이동할 수 있습니다.  
  
 [x * y](../../../csharp/language-reference/operators/multiplication-operator.md) – 곱하기  
  
 [x / y](../../../csharp/language-reference/operators/division-operator.md) – 나누기  피연산자가 정수인 경우 결과는 0으로 잘린 정수입니다(예: `-7 / 2 is -3`).  
  
 [x % y](../../../csharp/language-reference/operators/modulus-operator.md) – 나머지  피연산자가 정수인 경우 x를 y로 나눈 나머지를 반환합니다.  `q = x / y`이고 `r = x % y`인 경우 `x = q * y + r`입니다.  
  
## <a name="additive-operators"></a>더하기 연산자  
 이러한 연산자는 다음 섹션보다 우선 순위가 높고 이전 섹션보다 우선 순위가 낮습니다.  연산자를 클릭하면 예제가 포함된 상세 페이지로 이동할 수 있습니다.  
  
 [x + y](../../../csharp/language-reference/operators/addition-operator.md) – 더하기  
  
 [x – y](../../../csharp/language-reference/operators/subtraction-operator.md) – 빼기  
  
## <a name="shift-operators"></a>시프트 연산자  
 이러한 연산자는 다음 섹션보다 우선 순위가 높고 이전 섹션보다 우선 순위가 낮습니다.  연산자를 클릭하면 예제가 포함된 상세 페이지로 이동할 수 있습니다.  
  
 [x <\<  y](../../../csharp/language-reference/operators/left-shift-operator.md) – 왼쪽 비트를 시프트하고 오른쪽을 0으로 채웁니다.  
  
 [x >> y](../../../csharp/language-reference/operators/right-shift-operator.md) – 오른쪽 비트를 시프트합니다.  왼쪽 피연산자가 `int` 또는 `long`이면 왼쪽 비트는 부호 비트로 채워집니다.  왼쪽 피연산자가 `uint` 또는 `ulong`이면 왼쪽 비트는 0으로 채워집니다.  
  
## <a name="relational-and-type-testing-operators"></a>관계형 및 형식 테스트 연산자  
 이러한 연산자는 다음 섹션보다 우선 순위가 높고 이전 섹션보다 우선 순위가 낮습니다.  연산자를 클릭하면 예제가 포함된 상세 페이지로 이동할 수 있습니다.  
  
 [x \< y](../../../csharp/language-reference/operators/less-than-operator.md) –보다 작음(x가 y보다 작은 경우 true)  
  
 [x > y](../../../csharp/language-reference/operators/greater-than-operator.md) – 보다 큼(x가 y보다 큰 경우 true)  
  
 [x \<= y](../../../csharp/language-reference/operators/less-than-equal-operator.md) – 크거나 같음  
  
 [x >= y](../../../csharp/language-reference/operators/greater-than-equal-operator.md) – 보다 크거나 같음  
  
 [is](../../../csharp/language-reference/keywords/is.md) – 형식 호환성.  계산된 왼쪽 피연산자를 오른쪽 피연산자에 지정된 형식(정적 형식)으로 캐스팅할 수 있는 경우 true를 반환합니다.  
  
 [as](../../../csharp/language-reference/keywords/as.md) – 형식 변환.  오른쪽 피연산자에 지정된 형식(정적 유형)으로 캐스팅된 왼쪽 피연산자를 반환하지만 `(T)x`가 예외를 throw하는 경우 `as`는 `null`을 반환합니다.  
  
## <a name="equality-operators"></a>같음 연산자  
 이러한 연산자는 다음 섹션보다 우선 순위가 높고 이전 섹션보다 우선 순위가 낮습니다.  연산자를 클릭하면 예제가 포함된 상세 페이지로 이동할 수 있습니다.  
  
 [x == y](../../../csharp/language-reference/operators/equality-comparison-operator.md) – 같음.  기본적으로 `string`이 아닌 참조 형식에 대해 참조 같음(ID 테스트)을 반환합니다.  그러나 형식이 `==`를 오버로드할 수 있으므로 ID를 테스트하려는 경우에는 `object`에서 `ReferenceEquals` 메서드를 사용하는 것이 가장 좋습니다.  
  
 [x != y](../../../csharp/language-reference/operators/not-equal-operator.md) – 같지 않음.  `==`에 대한 설명을 참조하세요.  형식이 `==`를 오버로드하는 경우 `!=`를 오버로드해야 합니다.  
  
## <a name="logical-and-operator"></a>논리적 AND 연산자  
 이 연산자는 다음 섹션보다 우선 순위가 높고 이전 섹션보다 우선 순위가 낮습니다.  연산자를 클릭하면 예제가 포함된 상세 페이지로 이동할 수 있습니다.  
  
 [x & y](../../../csharp/language-reference/operators/and-operator.md) – 논리적 또는 비트 AND.  정수 형식에 사용되고 일반적으로 `enum` 형식이 허용됩니다.  
  
## <a name="logical-xor-operator"></a>논리적 XOR 연산자  
 이 연산자는 다음 섹션보다 우선 순위가 높고 이전 섹션보다 우선 순위가 낮습니다.  연산자를 클릭하면 예제가 포함된 상세 페이지로 이동할 수 있습니다.  
  
 [x ^ y](../../../csharp/language-reference/operators/xor-operator.md) – 논리적 또는 비트 XOR.  일반적으로 정수 형식 및 `enum` 형식에서 사용할 수 있습니다.  
  
## <a name="logical-or-operator"></a>논리적 OR 연산자  
 이 연산자는 다음 섹션보다 우선 순위가 높고 이전 섹션보다 우선 순위가 낮습니다.  연산자를 클릭하면 예제가 포함된 상세 페이지로 이동할 수 있습니다.  
  
 [x &#124; y](../../../csharp/language-reference/operators/or-operator.md) – 논리적 또는 비트 OR.  정수 형식에 사용되고 일반적으로 `enum` 형식이 허용됩니다.  
  
## <a name="conditional-and-operator"></a>조건부 AND 연산자  
 이 연산자는 다음 섹션보다 우선 순위가 높고 이전 섹션보다 우선 순위가 낮습니다.  연산자를 클릭하면 예제가 포함된 상세 페이지로 이동할 수 있습니다.  
  
 [x && y](../../../csharp/language-reference/operators/conditional-and-operator.md) – 논리적 AND.  첫 번째 피연산자가 false이면 C#에서 두 번째 피연산자를 계산하지 않습니다.  
  
## <a name="conditional-or-operator"></a>조건부 OR 연산자  
 이 연산자는 다음 섹션보다 우선 순위가 높고 이전 섹션보다 우선 순위가 낮습니다.  연산자를 클릭하면 예제가 포함된 상세 페이지로 이동할 수 있습니다.  
  
 [x &#124;&#124; y](../../../csharp/language-reference/operators/conditional-or-operator.md) – 논리적 OR.  첫 번째 피연산자가 true이면 C#에서 두 번째 피연산자를 계산하지 않습니다.  
  
## <a name="null-coalescing-operator"></a>Null 병합 연산자  
 이 연산자는 다음 섹션보다 우선 순위가 높고 이전 섹션보다 우선 순위가 낮습니다.  연산자를 클릭하면 예제가 포함된 상세 페이지로 이동할 수 있습니다.  
  
 [x ?? y](../../../csharp/language-reference/operators/null-conditional-operator.md) – `null`이 아닌 경우 `x`를 반환하고, 그렇지 않은 경우 `y`를 반환합니다.  
  
## <a name="conditional-operator"></a>조건 연산자  
 이 연산자는 다음 섹션보다 우선 순위가 높고 이전 섹션보다 우선 순위가 낮습니다.  연산자를 클릭하면 예제가 포함된 상세 페이지로 이동할 수 있습니다.  
  
 [t ? x : y](../../../csharp/language-reference/operators/conditional-operator.md) - 테스트 `t`가 true인 경우 `x`를 계산하여 반환하고, 그렇지 않은 경우 `y`를 계산하여 반환합니다.  
  
## <a name="assignment-and-lambda-operators"></a>할당 및 람다 연산자  
 이러한 연산자는 다음 섹션보다 우선 순위가 높고 이전 섹션보다 우선 순위가 낮습니다.  연산자를 클릭하면 예제가 포함된 상세 페이지로 이동할 수 있습니다.  
  
 [x = y](../../../csharp/language-reference/operators/assignment-operator.md) – 할당  
  
 [x += y](../../../csharp/language-reference/operators/addition-assignment-operator.md) – 증가.  `y`의 값을 `x` 값에 더하고 결과를 `x`에 저장한 다음 새 값을 반환합니다.  `x`가 `event`를 지정하는 경우 `y`는 C#에서 이벤트 처리기로 추가하는 적절한 함수여야 합니다.  
  
 [x -= y](../../../csharp/language-reference/operators/subtraction-assignment-operator.md) – 감소.  `x`의 값에서 `y`의 값을 빼고 결과를 `x`에 저장한 다음 새 값을 반환합니다.  `x`가 `event`를 지정하는 경우 `y`는 C#에서 이벤트 처리기로 제거하는 적절한 함수여야 합니다.  
  
 [x *= y](../../../csharp/language-reference/operators/multiplication-assignment-operator.md) – 곱하기 대입.  `y`의 값을 `x`의 값에 곱하고 결과를 `x`에 저장한 다음 새 값을 반환합니다.  
  
 [x /= y](../../../csharp/language-reference/operators/division-assignment-operator.md) – 나누기 대입.  `x`의 값을 `y`의 값으로 나누고 결과를 `x`에 저장한 다음 새 값을 반환합니다.  
  
 [x %= y](../../../csharp/language-reference/operators/modulus-assignment-operator.md) – 모듈러스 대입.  `x`의 값을 `y`의 값으로 나누고 나머지를 `x`에 저장한 다음 새 값을 반환합니다.  
  
 [x &= y](../../../csharp/language-reference/operators/and-assignment-operator.md) – AND 대입.  `y`의 값을 `x`의 값과 AND하고 결과를 `x`에 저장한 다음 새 값을 반환합니다.  
  
 [x &#124;= y](../../../csharp/language-reference/operators/or-assignment-operator.md) – OR 대입.  `y`의 값을 `x`의 값과 OR하고 결과를 `x`에 저장한 다음 새 값을 반환합니다.  
  
 [x ^= y](../../../csharp/language-reference/operators/xor-assignment-operator.md) – XOR 대입.  `y`의 값을 `x`의 값과 XOR하고 결과를 `x`에 저장한 다음 새 값을 반환합니다.  
  
 [x <<= y](../../../csharp/language-reference/operators/left-shift-assignment-operator.md) – 왼쪽 시프트 대입.  `x`의 값을 왼쪽으로 `y` 위치만큼 시프트하고 결과를 `x`에 저장한 다음 새 값을 반환합니다.  
  
 [x >>= y](../../../csharp/language-reference/operators/right-shift-assignment-operator.md) – 오른쪽 시프트 대입.  `x`의 값을 오른쪽으로 `y` 위치만큼 시프트하고 결과를 `x`에 저장한 다음 새 값을 반환합니다.  
  
 [=>](../../../csharp/language-reference/operators/lambda-operator.md) – 람다 선언.  
  
## <a name="arithmetic-overflow"></a>산술 연산 오버플로  
 산술 연산자([+](../../../csharp/language-reference/operators/addition-operator.md), [-](../../../csharp/language-reference/operators/subtraction-operator.md), [*](../../../csharp/language-reference/operators/multiplication-operator.md), [/](../../../csharp/language-reference/operators/division-operator.md))는 관련된 숫자 형식에 가능한 값의 범위를 벗어나는 결과를 생성할 수 있습니다. 자세한 내용은 특정 연산자에 대한 섹션을 참조해야 하지만 일반적으로 다음과 같습니다.  
  
- 정수 산술 연산 오버플로는 <xref:System.OverflowException>을 throw하거나 결과의 가장 중요한 비트를 삭제합니다. 정수를 0으로 나누면 항상 <xref:System.DivideByZeroException>이 throw됩니다.  

   정수 오버플로가 발생할 경우 수행되는 작업은 실행 컨텍스트에 따라 달라지며, 컨텍스트는 [checked 또는 unchecked](../../../csharp/language-reference/keywords/checked-and-unchecked.md)일 수 있습니다. checked 컨텍스트에서는 <xref:System.OverflowException>이 throw됩니다. unchecked 컨텍스트에서는 결과의 가장 중요한 비트가 무시되고 실행이 계속됩니다. 따라서 C#에서는 오버플로 처리 또는 무시를 선택합니다. 기본적으로 산술 연산은 *unchecked* 컨텍스트에서 발생합니다. 

   산술 연산자 외에도 정수 계열 형식 간 캐스팅(예: [long](../../../csharp/language-reference/keywords/long.md)을 [int](../../../csharp/language-reference/keywords/int.md)로 캐스팅)은 오버플로를 발생시키고 checked 또는 unchecked 실행이 적용될 수 있습니다. 그러나 비트 연산자와 시프트 연산자는 오버플로를 발생시키지 않습니다.  
   
-   부동 소수점 산술 연산 오버플로 또는 0으로 나누기에서 예외를 throw하지 않습니다. 부동 소수점 형식은 IEEE 754를 기반으로 하여 무한대 및 NaN(숫자가 아님)를 나타내려면 프로비전이 필요하기 때문입니다.  
  
-   [10진수<xref:System.OverflowException> 산술 연산 오버플로는 항상 ](../../../csharp/language-reference/keywords/decimal.md)을 throw합니다. 10진수를 0으로 나누면 항상 <xref:System.DivideByZeroException>이 throw됩니다.  
  
  
## <a name="see-also"></a>참고 항목  
 [C# 참조](../../../csharp/language-reference/index.md)  
 [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
 [C#](../../../csharp/index.md) [오버로드할 수 있는 연산자](../../../csharp/programming-guide/statements-expressions-operators/overloadable-operators.md)  
 [C# 키워드](../../../csharp/language-reference/keywords/index.md)
