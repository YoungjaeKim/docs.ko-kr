---
title: "Option Compare 문 | Microsoft 문서"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Compare
- vb.OptionCompare
dev_langs:
- VB
helpviewer_keywords:
- case sensitivity, Option Compare statement
- Compare keyword
- binary comparison
- strings [Visual Basic], returning from functions
- binary comparison, Option Compare statement
- strings [Visual Basic], comparing
- string comparison [Visual Basic], Option Compare statement
- Text keyword, Option Compare statement
- Binary keyword, Option Compare statement
- string comparison [Visual Basic], sorting data
- Option Compare statement
- text [Visual Basic], comparing
ms.assetid: 54e8eeeb-3b0d-4fb9-acce-fbfbd5975f6e
caps.latest.revision: 37
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 8b1b077a8818315e52ada6b08ff1e1ced9bbd17c
ms.lasthandoff: 03/13/2017

---
# <a name="option-compare-statement"></a>Option Compare 문
문자열 데이터를 비교할 때 사용할 기본 비교 방법을 선언합니다.  
  
## <a name="syntax"></a>구문  
  
```  
Option Compare { Binary | Text }  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`Binary`|선택 사항입니다. 문자의 내부 이진 표현에서 파생된 정렬 순서에 따라 문자열을 비교합니다.<br /><br /> 이 유형의 비교는 문자열에 텍스트로 해석할 수 없는 문자가 포함될 수 있는 경우 특히 유용합니다. 이 경우 대/소문자 미구분 등의 영문자 동일 여부에 따라 비교 결과가 달라지지 않습니다.|  
|`Text`|선택 사항입니다. 시스템의 로캘에 따라 결정되는 대/소문자 미구분 텍스트 정렬 순서에 따라 문자열을 비교합니다.<br /><br /> 문자열에 텍스트 문자만 포함되며 대/소문자 미구분, 밀접하게 관련된 문자 등의 영문자 동일 여부를 고려하여 이러한 문자를 비교하려는 경우에는 이 유형의 비교가 유용합니다. 예를 들어 `A`와 `a`를 같은 문자로 간주하고 `Ä` 및 `ä`가 `B` 및 `b` 앞에 온다고 간주할 수 있습니다.|  
  
## <a name="remarks"></a>설명  
 `Option Compare` 문은 사용하는 경우 파일에서 다른 소스 코드 문 앞에 나와야 합니다.  
  
 `Option Compare` 문은 문자열 비교 방법(`Binary` 또는 `Text`)을 지정합니다.  기본 텍스트 비교 방법은 `Binary`입니다.  
  
 `Binary` 비교에서는 각 문자열 내 각 문자의 숫자 유니코드 값을 비교합니다. `Text` 비교에서는 현재 문화권의 어휘 의미에 따라 각 유니코드 문자를 비교합니다.  
  
 Microsoft windows에서 정렬 순서는 코드 페이지에 의해 결정됩니다. 자세한 내용은 [코드 페이지](https://docs.microsoft.com/cpp/c-runtime-library/code-pages) 참조하세요.  
  
 다음 예제에서는 `Option Compare Binary`를 사용하여 영어/유럽어 코드 페이지(ANSI 1252)의 문자를 정렬합니다. 그러면 일반적인 이진 정렬 순서가 생성됩니다.  
  
 `A < B < E < Z < a < b < e < z < À < Ê < Ø < à < ê < ø`  
  
 
          `Option Compare Text`를 사용하여 같은 코드 페이지의 같은 문자를 정렬하면 다음 텍스트 정렬 순서가 생성됩니다.  
  
 `(A=a) < (À = à) < (B=b) < (E=e) < (Ê = ê) < (Z=z) < (Ø = ø)`  
  
## <a name="when-an-option-compare-statement-is-not-present"></a>Option Compare 문이 없는 경우  
 소스 코드에 없는 경우는 `Option Compare` 문는 **옵션 비교** 에 설정 된 [컴파일 페이지, 프로젝트 디자이너 (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic) 사용 됩니다. 으로 지정한 설정이 명령줄 컴파일러를 사용 하는 경우는 [/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md) 컴파일러 옵션을 사용 합니다.  
  
[!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
#### <a name="to-set-option-compare-in-the-ide"></a>IDE에서 Option Compare를 설정하려면  
  
1.  **솔루션 탐색기**, 프로젝트를 선택 합니다. 에 **프로젝트** 메뉴를 클릭 하 여 **속성**합니다. 자세한 내용은 참조 [NIB: 프로젝트 디자이너를 사용 하 여 프로젝트 속성 관리](http://msdn.microsoft.com/en-us/983f3c18-832f-4666-afec-74b716ff3e0e)합니다.  
  
2.  클릭 하 고 **컴파일** 탭 합니다.  
  
3.  값을 설정 된 **Option Compare** 상자입니다.  
  
 프로젝트를 만들 때는 **Option Compare** 설정에 **컴파일** 로 설정 되는 **Option Compare** 에서 설정는 **옵션** 대화 상자. 이 설정을 변경 하는 **도구** 메뉴를 클릭 하 여 **옵션**합니다. 에 **옵션** 대화 상자에서 **프로젝트 및 솔루션**를 클릭 하 고 **VB 기본값**합니다. 초기 기본 설정은 **VB 기본값** 는 **이진**합니다.  
  
#### <a name="to-set-option-compare-on-the-command-line"></a>명령줄에서 Option Compare를 설정하려면  
  
-   포함은 [/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md) 컴파일러 옵션에는 **vbc** 명령입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `Option Compare` 문을 사용하여 이진 비교를 기본 문자열 비교 방법으로 설정합니다. 이 코드를 사용하려면 `Option Compare Binary` 문의 주석 처리를 제거하여 소스 파일 맨 위에 삽입합니다.  
  
 [!code-vb[VbVbalrStatements #&45;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-compare-statement_1.vb)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 `Option Compare` 문을 사용하여 대/소문자 미구분 텍스트 정렬 순서를 기본 문자열 비교 방법으로 설정합니다. 이 코드를 사용하려면 `Option Compare Text` 문의 주석 처리를 제거하여 소스 파일 맨 위에 삽입합니다.  
  
 [!code-vb[VbVbalrStatements #&46;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-compare-statement_2.vb)]  
  
## <a name="see-also"></a>참고 항목  
 <xref:Microsoft.VisualBasic.Strings.InStr%2A></xref:Microsoft.VisualBasic.Strings.InStr%2A>   
 <xref:Microsoft.VisualBasic.Strings.InStrRev%2A></xref:Microsoft.VisualBasic.Strings.InStrRev%2A>   
 <xref:Microsoft.VisualBasic.Strings.Replace%2A></xref:Microsoft.VisualBasic.Strings.Replace%2A>   
 <xref:Microsoft.VisualBasic.Strings.Split%2A></xref:Microsoft.VisualBasic.Strings.Split%2A>   
 <xref:Microsoft.VisualBasic.Strings.StrComp%2A></xref:Microsoft.VisualBasic.Strings.StrComp%2A>   
 [/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)   
 [비교 연산자](../../../visual-basic/language-reference/operators/comparison-operators.md)   
 [Visual Basic의 비교 연산자](../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [Like 연산자](../../../visual-basic/language-reference/operators/like-operator.md)   
 [문자열 함수](../../../visual-basic/language-reference/functions/string-functions.md)   
 [Option Explicit 문](../../../visual-basic/language-reference/statements/option-explicit-statement.md)   
 [Option Strict 문](../../../visual-basic/language-reference/statements/option-strict-statement.md)