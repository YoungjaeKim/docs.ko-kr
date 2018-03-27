---
title: "보간된 문자열(C#)"
ms.date: 10/18/2017
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
ms.assetid: 324f267e-1c61-431a-97ed-852c1530742d
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 03315a2d9a44405ff520a1c333f56311e2657df6
ms.sourcegitcommit: 3a96c706e4dbb4667bf3bf37edac9e1666646f93
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/27/2018
---
# <a name="interpolated-strings-c-reference"></a>보간된 문자열(C# 참조)

문자열을 생성하는 데 사용됩니다.  보간된 문자열은 *보간된 식*이 포함된 템플릿 문자열과 유사합니다.  보간된 문자열은 포함하는 보간된 식을 해당 문자열 표현으로 바꾸는 문자열을 반환합니다. 이 기능은 C# 6 이상 버전에서 사용할 수 있습니다.

보간된 문자열의 인수는 [복합 형식 문자열](../../../standard/base-types/composite-formatting.md#composite-format-string)보다 더 쉽게 이해할 수 있습니다.  예를 들어 보간된 문자열  
  
```csharp  
Console.WriteLine($"Name = {name}, hours = {hours:hh}");
```  
에는 두 개의 보간된 식 '{name}' 및 '{hours:hh}'가 포함되어 있습니다. 동등한 복합 형식 문자열은 다음과 같습니다.

```csharp
Console.WriteLine("Name = {0}, hours = {1:hh}", name, hours); 
```  

보간된 문자열의 구조는 다음과 같습니다.  
  
```  
$"<text> {<interpolated-expression> [,<field-width>] [:<format-string>] } <text> ..."  
```  

여기서 

- *필드 너비*는 필드의 문자 수를 나타내는 부호 있는 정수입니다. 양수이면 필드가 오른쪽에 맞춰지고, 음수이면 왼쪽에 맞춰집니다. 

- *형식 문자열*은 형식을 지정할 개체 형식에 적합한 형식 문자열입니다. 예를 들어 <xref:System.DateTime> 값의 경우 "D" 또는 "d"와 같은 표준 날짜 및 시간 형식 문자열일 수 있습니다.

> [!IMPORTANT]
> 문자열을 시작하는 `$` 및 `"` 사이에 공백이 없어야 합니다. 이렇게 하면 컴파일 시간 오류가 발생합니다.

 문자열 리터럴을 사용할 수 있는 곳이면 어디든지 보간된 문자열을 사용할 수 있습니다.  보간된 문자열을 포함하는 코드가 실행될 때마다 보간된 문자열이 평가됩니다. 이렇게 하면 보간된 문자열의 정의 및 평가를 구분할 수 있습니다.  
  
 보간된 문자열에 중괄호("{" 또는 "}")를 포함하려면 두 개의 중괄호 "{{" 또는 "}}"를 사용합니다.  자세한 내용은 [암시적 변환](#implicit-conversions) 섹션을 참조하세요.  

큰따옴표("), 콜론(:), 쉼표(,) 등 특별한 의미를 가진 다른 문자가 보간된 문자열에 포함된 경우 리터럴 텍스트에 발생하면 이스케이프해야 하거나, 보간된 식에 포함된 언어 요소이면 괄호로 구분된 식에 포함해야 합니다. 다음 예제에서는 따옴표를 이스케이프하여 결과 문자열에 포함하고, 콜론이 형식 문자열의 시작으로 해석되지 않도록 괄호를 사용하여 `(age == 1 ? "" : "s")` 식을 구분합니다.

[!code-csharp[interpolated-strings4](../../../../samples/snippets/csharp/language-reference/keywords/interpolated-strings4.cs#1)]  

약어 보간된 문자열은 `@` 문자가 뒤에 오는 `$` 문자를 사용합니다. 약어 문자열에 대한 자세한 내용은 [문자열](string.md) 항목을 참조하세요. 다음 코드는 약어 보간된 문자열을 사용하는 이전 코드 조각의 수정된 버전입니다.

[!code-csharp[interpolated-strings4](../../../../samples/snippets/csharp/language-reference/keywords/interpolated-strings5.cs#1)]  

약어 문자열은 `\` 이스케이프 시퀀스를 준수하지 않기 때문에 서식 지정 변경 내용이 필요합니다.

> [!IMPORTANT]
> `$` 토큰은 약어 보간된 문자열에서 `@` 토큰 앞에 나타나야 합니다.


## <a name="implicit-conversions"></a>암시적 변환  

보간된 문자열에서 다음과 같은 세 가지 암시적 형식 변환을 수행할 수 있습니다.  

1. 보간된 문자열을 <xref:System.String>으로 변환. 다음 예제에서는 보간된 문자열 식이 해당 문자열 표현으로 바뀐 문자열을 반환합니다. 예:

   [!code-csharp[interpolated-strings1](../../../../samples/snippets/csharp/language-reference/keywords/interpolated-strings1.cs#1)]  

   이는 문자열 해석의 최종 결과입니다. 나타나는 모든 이중 중괄호("{{" 및 "}}")가 단일 중괄호로 변환됩니다. 

2. 보간된 문자열을 <xref:System.IFormattable> 변수로 변환. 이 변수를 사용하면 단일 <xref:System.IFormattable> 인스턴스의 문화권별 콘텐츠로 여러 결과 문자열을 만들 수 있습니다. 이 옵션은 개별 문화권의 올바른 숫자 및 날짜 형식 등을 포함하는 데 유용합니다.  모든 이중 중괄호("{{" 및 "}}")는 <xref:System.Object.ToString> 메서드를 명시적 또는 암시적으로 호출하여 문자열을 형식을 지정할 때까지 이중 중괄호로 유지됩니다.  포함된 보간 식은 모두 {0}, {1} 등으로 변환됩니다.  

   다음 예제에서는 리플렉션을 사용하여 보간된 문자열에서 생성된 <xref:System.IFormattable> 변수의 필드 및 속성 값뿐 아니라 멤버를 표시합니다. 또한 <xref:System.IFormattable> 변수를 <xref:System.Console.WriteLine(System.String)?displayProperty=nameWithType> 메서드에 전달합니다.

   [!code-csharp[interpolated-strings2](../../../../samples/snippets/csharp/language-reference/keywords/interpolated-strings2.cs#1)]  

   보간된 문자열은 리플렉션을 통해서만 검사할 수 있습니다. <xref:System.Console.WriteLine(System.String)> 등의 문자열 형식 지정 메서드에 전달되는 경우 해당 형식 항목이 확인되고 결과 문자열이 반환됩니다. 

3. 보간된 문자열을 복합 형식 문자열을 나타내는 <xref:System.FormattableString> 변수로 변환. 예를 들어 복합 형식 문자열 및 복합 형식 문자열이 결과 문자열로 렌더링되는 방식을 검사하면 쿼리를 빌드하는 경우 삽입 공격으로부터 보호하는 데 도움이 됩니다. <xref:System.FormattableString>에는 <xref:System.Globalization.CultureInfo.InvariantCulture> 및 <xref:System.Globalization.CultureInfo.CurrentCulture>에 대한 결과 문자열을 생성할 수 있도록 하는 <xref:System.FormattableString.ToString> 오버로드도 포함되어 있습니다.  나타나는 모든 이중 중괄호("{{" 및 "}}")는 형식을 지정할 때까지 이중 중괄호로 유지됩니다.  포함된 보간 식은 모두 {0}, {1} 등으로 변환됩니다.  

   [!code-csharp[interpolated-strings3](../../../../samples/snippets/csharp/language-reference/keywords/interpolated-strings3.cs#1)]  

## <a name="language-specification"></a>언어 사양  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.IFormattable?displayProperty=nameWithType>  
 <xref:System.FormattableString?displayProperty=nameWithType>  
 <xref:System.String.Format%2A?displayProperty=nameWithType>  
 [C#의 문자열 보간](../../../csharp/tutorials/string-interpolation.md)  
 [C#에서 보간된 문자열](../../../csharp/quick-starts/interpolated-strings.yml)  
 [C# 참조](../../../csharp/language-reference/index.md)  
 [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)
