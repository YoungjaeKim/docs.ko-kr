---
title: 숫자 결과 형식 지정 표(C# 참조)
ms.date: 07/20/2015
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
helpviewer_keywords:
- formatting [C#]
- numeric formatting [C#]
- String.Format method
- Console.Write method
ms.assetid: 120ba537-4448-4c62-8676-7a8fdd98f496
caps.latest.revision: 14
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: d389703c2d82d74760b99059201cb634849aa433
ms.sourcegitcommit: 935d5267c44f9bce801468ef95f44572f1417e8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="formatting-numeric-results-table-c-reference"></a>숫자 결과 형식 지정 표(C# 참조)
<xref:System.String.Format%2A?displayProperty=nameWithType> 메서드를 사용하거나 `String.Format`을 호출하는 <xref:System.Console.Write%2A?displayProperty=nameWithType> 또는 <xref:System.Console.WriteLine%2A?displayProperty=nameWithType> 메서드를 통하거나 [문자열 보간](../tokens/interpolated.md)을 사용하여 숫자 결과의 서식을 지정할 수 있습니다. 형식은 형식 문자열을 사용하여 지정됩니다. 다음 표에는 지원되는 표준 형식 문자열을 보여 줍니다. 형식 문자열은 `Axx` 형식을 사용합니다. 여기서 `A`는 형식 지정자이고 `xx`는 전체 자릿수 지정자입니다. 형식 지정자는 숫자 값에 적용되는 서식 형식을 제어하고, 전체 자릿수 지정자는 서식이 지정된 출력의 유효 자릿수 또는 소수 자릿수를 제어합니다. 전체 자릿수 지정자의 값은 0에서 99 사이입니다.  
  
 표준 및 사용자 지정 서식 문자열에 대한 자세한 내용은 [형식 서식 지정](../../../standard/base-types/formatting-types.md)을 참조하세요.
  
|형식 지정자|설명|예제|출력|  
|----------------------|-----------------|--------------|------------|  
|C 또는 c|통화|Console.Write("{0:C}", 2.5);<br /><br /> Console.Write("{0:C}", -2.5);|$2.50<br /><br /> ($2.50)|  
|D 또는 d|Decimal|Console.Write("{0:D5}", 25);|00025|  
|E 또는 e|지수|Console.Write("{0:E}", 250000);|2.500000E+005|  
|F 또는 f|고정 소수점|Console.Write("{0:F2}", 25);<br /><br /> Console.Write("{0:F0}", 25);|25.00<br /><br /> 25|  
|G 또는 g|일반|Console.Write("{0:G}", 2.5);|2.5|  
|N 또는 n|수|Console.Write("{0:N}", 2500000);|2,500,000.00|  
|X 또는 x|16진수|Console.Write("{0:X}", 250);<br /><br /> Console.Write("{0:X}", 0xffff);|FA<br /><br /> FFFF|  
  
## <a name="see-also"></a>참고 항목  
 [C# 참조](../../../csharp/language-reference/index.md)  
 [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
 [표준 숫자 형식 문자열](../../../standard/base-types/standard-numeric-format-strings.md)  
 [형식 참조 테이블](../../../csharp/language-reference/keywords/reference-tables-for-types.md)  
 [string](../../../csharp/language-reference/keywords/string.md)
