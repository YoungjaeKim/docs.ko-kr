---
title: "연산자(C# 프로그래밍 가이드)"
ms.date: 07/20/2015
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
helpviewer_keywords:
- operators [C#]
- C# language, operators
- operators [C#], about operators
ms.assetid: 214e7b83-1a41-4f7c-9867-64e9c0bab39f
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 267022b8c6b7f8faf301cae1a62f4dfaa8249f96
ms.sourcegitcommit: 1c0b0f082b3f300e54b4d069b317ac724c88ddc3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/16/2018
---
# <a name="operators-c-programming-guide"></a>연산자(C# 프로그래밍 가이드)
C#에서 *연산자* 는 식 또는 문에서 하나 이상의 *피연산자* 에 적용되는 프로그램 요소입니다. 증가 연산자(`++`)나 `new`같이 피연산자 하나를 사용하는 연산자를 *단항* 연산자라고 합니다. 산술 연산자(`+`,`-`,`*`,`/`) 같이 피연산자 두 개를 사용하는 연산자를 *이항* 연산자라고 합니다. 조건 연산자(`?:`)는 피연산자 세 개를 사용하며 이는 C#에서 유일한 삼진 연산자입니다.  
  
 다음 C# 문에는 단항 연산자 하나와 피연산자 하나가 들어 있습니다. 증가 연산자 `++`는 피연산자 `y`의 값을 수정합니다.  
  
 [!code-csharp[csProgGuideStatements#5](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/operators_1.cs)]  
  
 다음 C# 문에는 이항 연산자가 두 개 있습니다. 각 연산자는 피연산자를 두 개씩 사용합니다. 할당 연산자 `=`에는 정수 변수 `y` 와 식 `2 + 3` 이 피연산자로 사용됩니다. 식 `2 + 3` 자체는 더하기 연산자와 두 개의 피연산자, `2` 및 `3`으로 구성됩니다.  
  
 [!code-csharp[csProgGuideStatements#6](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/operators_2.cs)]  
  
## <a name="operators-evaluation-and-operator-precedence"></a>연산자, 평가, 및 연산자 우선 순위  
 피연산자는 모든 길이의 코드로 구성된 유효한 식이 될 수 있으며 모든 개수의 하위 식으로 구성될 수 있습니다. 여러 연산자를 포함하는 식에서 연산자가 적용되는 순서는 *operator precedence*, *associativity*및 괄호로 결정됩니다.  
  
 각 연산자에는 정의된 우선 순위가 있습니다. 다른 우선 순위 수준을 가진 여러 연산자가 포함된 식에서 연산자의 우선 순위는 연산자가 평가되는 순서를 결정합니다. 예를 들어, 다음 문은 `n1`에 3을 할당합니다.  
  
 `n1 = 11 - 2 * 4;`  
  
 곱셈은 뺄셈보다 우선하기 때문에 곱하기가 가장 먼저 실행됩니다.  
  
 다음 표에서는 연산자를 각각 수행하는 연산의 종류에 따라 범주별로 구분하여 보여 줍니다. 이 범주는 우선 순위에 따라 나열되어 있습니다.  
  
 **기본 연산자**  
  
|식|설명|  
|----------------|-----------------|  
|x[.](../../../csharp/language-reference/operators/member-access-operator.md)y<br /><br /> x?.y|멤버 액세스<br /><br /> 조건부 멤버 액세스|  
|f[(x)](../../../csharp/language-reference/operators/invocation-operator.md)|메서드 및 대리자 호출|  
|a[&#91;x&#93;](../../../csharp/language-reference/operators/index-operator.md)<br /><br /> a?[x]|배열 및 인덱서 액세스<br /><br /> 조건부 배열 및 인덱서 액세스|  
|x[++](../../../csharp/language-reference/operators/increment-operator.md)|후위 증가|  
|x[--](../../../csharp/language-reference/operators/decrement-operator.md)|후위 감소|  
|[new](../../../csharp/language-reference/keywords/new-operator.md) T(...)|개체 및 대리자 생성|  
|`new` T(...){...}|이니셜라이저를 사용한 개체 생성. [개체 이니셜라이저 및 컬렉션 이니셜라이저](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)를 참조하세요.|  
|`new` {...}|익명 개체 이니셜라이저. [무명 형식](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)을 참조하세요.|  
|`new` T[...]|배열 생성. [배열](../../../csharp/programming-guide/arrays/index.md)을 참조하세요.|  
|[typeof](../../../csharp/language-reference/keywords/typeof.md)(T)|T에 대한 System.Type 개체 가져오기|  
|[checked](../../../csharp/language-reference/keywords/checked.md)(x)|checked 컨텍스트에서 식 계산|  
|[unchecked](../../../csharp/language-reference/keywords/unchecked.md)(x)|unchecked 컨텍스트에서 식 계산|  
|[default](../../../csharp/language-reference/keywords/default.md) (T)|T 형식의 기본값 가져오기|  
|[delegate](../../../csharp/language-reference/keywords/delegate.md) {}|익명 함수(무명 메서드)|  
  
 **단항 연산자**  
  
|식|설명|  
|----------------|-----------------|  
|[+](../../../csharp/language-reference/operators/addition-operator.md)x|클레임|  
|[-](../../../csharp/language-reference/operators/subtraction-operator.md)x|부정|  
|[\!](../../../csharp/language-reference/operators/logical-negation-operator.md)x|논리 부정|  
|[~](../../../csharp/language-reference/operators/bitwise-complement-operator.md)x|비트 부정 연산|  
|[++](../../../csharp/language-reference/operators/increment-operator.md)x|전위 증가|  
|[--](../../../csharp/language-reference/operators/decrement-operator.md)x|전위 감소|  
|[(T)](../../../csharp/language-reference/operators/invocation-operator.md)x|x를 T 형식으로 명시적 변환|  
  
 **곱하기 연산자**  
  
|식|설명|  
|----------------|-----------------|  
|[*](../../../csharp/language-reference/operators/multiplication-operator.md)|곱하기|  
|[/](../../../csharp/language-reference/operators/division-operator.md)|나눗셈 기호|  
|[%](../../../csharp/language-reference/operators/modulus-operator.md)|나머지|  
  
 **더하기 연산자**  
  
|식|설명|  
|----------------|-----------------|  
|x [+](../../../csharp/language-reference/operators/addition-operator.md) y|더하기, 문자열 연결, 대리자 결합|  
|x [-](../../../csharp/language-reference/operators/subtraction-operator.md) y|빼기, 대리자 제거|  
  
 **시프트 연산자**  
  
|식|설명|  
|----------------|-----------------|  
|x [<\<](../../../csharp/language-reference/operators/left-shift-operator.md) y|왼쪽 시프트|  
|x [>>](../../../csharp/language-reference/operators/right-shift-operator.md) y|오른쪽 시프트|  
  
 **관계 및 형식 연산자**  
  
|식|설명|  
|----------------|-----------------|  
|x [\<](../../../csharp/language-reference/operators/less-than-operator.md) y|보다 작음|  
|x [>](../../../csharp/language-reference/operators/greater-than-operator.md) y|보다 큼|  
|x [\<=](../../../csharp/language-reference/operators/less-than-equal-operator.md) y|작거나 같음|  
|x [>=](../../../csharp/language-reference/operators/greater-than-equal-operator.md) y|크거나 같음|  
|x [is](../../../csharp/language-reference/keywords/is.md) T|x가 T이면 true를 반환하고, 그렇지 않으면 false를 반환합니다.|  
|x [as](../../../csharp/language-reference/keywords/as.md) T|T로 형식화된 x 또는 null(x를 T로 형식화할 수 없는 경우)을 반환합니다.|  
  
 **같음 연산자**  
  
|식|설명|  
|----------------|-----------------|  
|x [==](../../../csharp/language-reference/operators/equality-comparison-operator.md) y|Equal|  
|x [!=](../../../csharp/language-reference/operators/not-equal-operator.md) y|같지 않음|  
  
 **논리, 조건 및 null 연산자**  
  
|범주|식|설명|  
|--------------|----------------|-----------------|  
|논리적 AND|x [&](../../../csharp/language-reference/operators/and-operator.md) y|정수 비트 AND, 부울 논리곱 AND|  
|논리 XOR|x [^](../../../csharp/language-reference/operators/xor-operator.md) y|정수 비트 XOR, 부울 논리곱 XOR|  
|논리적 OR|x [&#124;](../../../csharp/language-reference/operators/or-operator.md) y|정수 비트 OR, 부울 논리곱 OR|  
|조건부 AND|x [&&](../../../csharp/language-reference/operators/conditional-and-operator.md) y|x가 true인 경우에만 y를 계산합니다.|  
|조건부 OR|x [&#124;&#124;](../../../csharp/language-reference/operators/conditional-or-operator.md) y|x가 false인 경우에만 y를 계산합니다.|  
|Null 결합|x [??](../../../csharp/language-reference/operators/null-conditional-operator.md) y|x가 null인 경우 y로 계산하고, 그렇지 않으면 x로 계산합니다.|  
|조건|x [?](../../../csharp/language-reference/operators/conditional-operator.md) y : z|x가 true이면 y로 계산되고 false이면 z로 계산됩니다.|  
  
 **할당 및 익명 연산자**  
  
|식|설명|  
|----------------|-----------------|  
|[=](../../../csharp/language-reference/operators/assignment-operator.md)|할당|  
|x op= y|복합 할당. 다음 연산자를 지원합니다. [+=](../../../csharp/language-reference/operators/addition-assignment-operator.md), [-=](../../../csharp/language-reference/operators/subtraction-assignment-operator.md), [*=](../../../csharp/language-reference/operators/multiplication-assignment-operator.md), [/=](../../../csharp/language-reference/operators/division-assignment-operator.md), [%=](../../../csharp/language-reference/operators/modulus-assignment-operator.md), [&=](../../../csharp/language-reference/operators/and-assignment-operator.md), [&#124;=](../../../csharp/language-reference/operators/or-assignment-operator.md), [!=](../../../csharp/language-reference/operators/not-equal-operator.md), [<\<=](../../../csharp/language-reference/operators/left-shift-assignment-operator.md), [>>=](../../../csharp/language-reference/operators/right-shift-assignment-operator.md)|  
|(T x) [=>](../../../csharp/language-reference/operators/lambda-operator.md) y|익명 함수(람다 식)|  
  
## <a name="associativity"></a>결합성  
 우선 순위가 동일한 연산자 두 개 이상이 식 하나에 있으면 두 연산자의 결합성에 따라 연산 순서가 결정됩니다. 왼쪽 결합성이 있는 연산자는 왼쪽에서 오른쪽으로 계산됩니다. 예를 들어, `x * y / z` 는 `(x * y) / z`로 계산됩니다. 오른쪽 결합성이 있는 연산자는 오른쪽에서 왼쪽으로 계산됩니다. 예를 들어, 할당 연산자는 오른쪽 결합성이 있는 연산자입니다. 아닌 경우 다음 코드 오류가 발생합니다.  
  
```csharp  
int a, b, c;  
c = 1;  
// The following two lines are equivalent.  
a = b = c;  
a = (b = c);  
  
// The following line, which forces left associativity, causes an error.  
//(a = b) = c;  
```  
  
 또 다른 예로, 3개로 구성된 연산자([?:](../../../csharp/language-reference/operators/conditional-operator.md))는 오른쪽 결합형이고, 대부분의 이항 연산자는 왼쪽 결합형입니다.  
  
 식에서 연산자가 왼쪽 결합성인지, 오른쪽 결합성인지에 따라 각 식의 피연산자가 먼저 평가됩니다. 다음 예제는 연산자와 피연산자의 계산 순서를 보여 줍니다.  
  
|문|계산 순서|  
|---------------|-------------------------|  
|`a = b`|a, b, =|  
|`a = b + c`|a, b, c, +, =|  
|`a = b + c * d`|a, b, c, d, *, +, =|  
|`a = b * c + d`|a, b, c, *, d, +, =|  
|`a = b - c + d`|a, b, c, -, d, +, =|  
|`a += b -= c`|a, b, c, -=, +=|  
  
## <a name="adding-parentheses"></a>괄호 추가  
 괄호를 사용하여 연산자 우선 순위와 연결을 통해 부과된 실행 순서를 변경할 수 있습니다. 예를 들어, `2 + 3 * 2` 는 일반적으로 승제 연산자가 가감 연산자보다 우선하기 때문에 8로 평가됩니다. 그러나 식을 `(2 + 3) * 2`처럼 작성하는 경우 곱셈 전에 덧셈이 계산되고 결과는 10입니다. 다음 예제는 괄호로 묶인 식의 계산 순서를 보여 줍니다. 이전 예제에서와 같이 피연산자는 연산자가 적용되기 전에 평가됩니다.  
  
|문|계산 순서|  
|---------------|-------------------------|  
|`a = (b + c) * d`|a, b, c, +, d, *, =|  
|`a = b - (c + d)`|a, b, c, d, +, -, =|  
|`a = (b + c) * (d - e)`|a, b, c, +, d, e, -, *, =|  
  
## <a name="operator-overloading"></a>연산자 오버로드  
 사용자 지정 클래스 및 구조체에서 연산자의 동작을 변경할 수 있습니다. 이러한 과정을 *연산자 오버로드*라고 합니다. 자세한 내용은 [오버로드할 수 있는 연산자](../../../csharp/programming-guide/statements-expressions-operators/overloadable-operators.md)를 참조하세요.  
  
## <a name="related-sections"></a>관련 단원  
 자세한 내용은 [연산자 키워드](../../../csharp/language-reference/keywords/operator-keywords.md) 및 [C# 연산자](../../../csharp/language-reference/operators/index.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
 [문, 식, 연산자](../../../csharp/programming-guide/statements-expressions-operators/index.md)
