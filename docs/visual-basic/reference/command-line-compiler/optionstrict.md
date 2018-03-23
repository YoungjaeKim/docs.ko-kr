---
title: -optionstrict
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- -optionstrict
helpviewer_keywords:
- -optionstrict compiler option [Visual Basic]
- optionstrict compiler option [Visual Basic]
- /optionstrict compiler option [Visual Basic]
ms.assetid: c7b10086-0fa4-49db-b3c8-4ae0db5957da
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 2ff7d13fcb3e224ee76cdb42f3974a4eddb042f5
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="-optionstrict"></a>-optionstrict
암시적 형식 변환을 제한 하는 엄격한 형식 의미 체계를 적용 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
-optionstrict[+ | -]  
-optionstrict[:custom]  
```  
  
## <a name="arguments"></a>인수  
 `+` &#124; `-`  
 선택 사항입니다. `-optionstrict+` 옵션 암시적 형식 변환을 제한 합니다. 이 옵션의 기본값은 `-optionstrict-`합니다. `-optionstrict+` 옵션은 동일 `-optionstrict`합니다. 관대 한 형식 의미 체계를 모두 사용할 수 있습니다.  
  
 `custom`  
 필수. 엄격한 언어 의미 체계를 준수 하지 않을 때 경고를 표시 합니다.  
  
## <a name="remarks"></a>설명  
 때 `-optionstrict+` 가 적용 된 경우 확장 유형 변환만 암시적으로 만들 수 있습니다. 할당 하는 등의 형식 변환에 축소 변환을 암시적는 `Decimal` 형식 개체는 정수 형식 개체를, 오류로 보고 됩니다.  
  
 암시적 축소 형식 변환에 대 한 경고를 생성 하려면 사용 `-optionstrict:custom`합니다. 사용 하 여 `-nowarn:numberlist` 특정 경고를 무시 하 고 `-warnaserror:numberlist` 특정 경고를 오류로 처리 하도록 합니다.  
  
### <a name="to-set--optionstrict-in-the-visual-studio-ide"></a>-Optionstrict Visual Studio IDE에서 설정 하려면  
  
1.  **솔루션 탐색기**에서 프로젝트를 선택합니다. 에 **프로젝트** 메뉴를 클릭 하 여 **속성입니다.**   
  
2.  **컴파일** 탭을 클릭합니다.  
  
3.  값을 수정 된 **Option Strict** 상자입니다.  
  
### <a name="to-set--optionstrict-programmatically"></a>-Optionstrict를 프로그래밍 방식으로 설정 하려면  
  
-   참조 [Option Strict 문](../../../visual-basic/language-reference/statements/option-strict-statement.md)합니다.  
  
## <a name="example"></a>예제  
 다음 코드에서는 `Test.vb` 엄격한 형식 의미 체계를 사용 하 여 합니다.  
  
```console
vbc -optionstrict+ test.vb  
```  
  
## <a name="see-also"></a>참고 항목  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
 [-optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)  
 [-optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)  
 [-optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md)  
 [-nowarn](../../../visual-basic/reference/command-line-compiler/nowarn.md)  
 [-warnaserror (Visual Basic)](../../../visual-basic/reference/command-line-compiler/warnaserror.md)  
 [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)  
 [Option Strict 문](../../../visual-basic/language-reference/statements/option-strict-statement.md)  
 [옵션 대화 상자, 프로젝트, Visual Basic 기본값](/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
