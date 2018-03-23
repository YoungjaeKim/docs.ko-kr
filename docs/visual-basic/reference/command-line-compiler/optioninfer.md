---
title: -optioninfer
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- -optioninfer
helpviewer_keywords:
- -optioninfer compiler option [Visual Basic]
- /optioninfer compiler option [Visual Basic]
- optioninfer compiler option [Visual Basic]
ms.assetid: f6c09db1-0553-464a-abe3-d4510c61d6ed
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: df01fccd7276f0ec759065306ad3614d735f89ef
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="-optioninfer"></a>-optioninfer
변수 선언에서 지역 형식 유추를 사용하도록 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
-optioninfer[+ | -]  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`+` &#124; `-`|선택 사항입니다. 지역 형식 유추를 사용하도록 설정하려면 `-optioninfer+`를 지정하고, 차단하려면 `-optioninfer-`를 지정합니다. 값을 지정하지 않은 `-optioninfer` 옵션은 `-optioninfer+`와 같습니다. `-optioninfer` 스위치가 없을 때의 기본값도 `-optioninfer+`입니다. 기본값은 vbc.rsp 지시 파일에서 설정됩니다.|  
  
> [!NOTE]
>  `-noconfig` 옵션을 사용하여 vbc.rsp에 지정된 값 대신 컴파일러의 내부 기본값을 유지할 수 있습니다. 이 옵션에 대한 컴파일러 기본값은 `-optioninfer-`입니다.  
  
## <a name="remarks"></a>설명  
 소스 코드 파일을 포함 하는 경우는 [Option Infer 문](../../../visual-basic/language-reference/statements/option-infer-statement.md), 문이 재정의 `-optioninfer` 명령줄 컴파일러 설정을 사용 합니다.  
  
### <a name="to-set--optioninfer-in-the-visual-studio-ide"></a>-Optioninfer Visual Studio IDE에서 설정 하려면  
  
1.  프로젝트를 선택 **솔루션 탐색기**합니다. **프로젝트** 메뉴에서 **속성**을 클릭합니다.  
  
2.  에 **컴파일** 탭에서 값을 수정 된 **Option infer** 상자입니다.  
  
## <a name="example"></a>예제  
 다음 코드에서는 지역 형식 유추를 사용하도록 설정한 상태로 `test.vb`를 컴파일합니다.  
  
```console
vbc -optioninfer+ test.vb  
```  
  
## <a name="see-also"></a>참고 항목  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
 [-optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)  
 [-optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)  
 [-optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)  
 [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)  
 [Option Infer 문](../../../visual-basic/language-reference/statements/option-infer-statement.md)  
 [지역 형식 유추](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)  
 [옵션 대화 상자, 프로젝트, Visual Basic 기본값](/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)  
 [프로젝트 디자이너, 컴파일 페이지(Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)  
 [/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)  
 [명령줄에서 빌드](../../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md)
