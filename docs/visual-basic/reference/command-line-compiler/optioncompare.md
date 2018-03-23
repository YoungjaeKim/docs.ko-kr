---
title: -optioncompare
ms.date: 07/20/2015
ms.prod: .net
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- /optioncompare
- -optioncompare
helpviewer_keywords:
- optioncompare compiler option [Visual Basic]
- -optioncompare compiler option [Visual Basic]
- /optioncompare compiler option [Visual Basic]
ms.assetid: 7237b766-b44d-4cc5-9a3c-885348a7d9e4
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 033be2ce3845ed470d56c2097b89b81d10275046
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="-optioncompare"></a>-optioncompare
문자열 비교 방법을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
-optioncompare:{binary | text}  
```  
  
## <a name="remarks"></a>설명  
 지정할 수 있습니다 `-optioncompare` 두 형식 중 하나로: `-optioncompare:binary` 이진 문자열 비교를 사용 하도록 및 `-optioncompare:text` 텍스트 문자열 비교를 사용 하도록 합니다. 기본적으로 컴파일러는 다음과 같이 사용 됩니다. `-optioncompare:binary`합니다.  
  
 Microsoft Windows에서 현재 코드 페이지는 이진 정렬 순서를 결정합니다. 일반적인 이진 정렬 순서는 다음과 같습니다.  
  
 `A < B < E < Z < a < b < e < z < À < Ê < Ø < à < ê < ø`  
  
 텍스트 기반 문자열 비교는 시스템의 로캘에 따라 결정 하는 대/소문자 구분 텍스트 정렬 순서를 기준으로 합니다. 일반 텍스트 정렬 순서는 다음과 같습니다.  
  
 `(A = a) < (À = à) < (B=b) < (E=e) < (Ê = ê) < (Z=z) < (Ø = ø)`  
  
### <a name="to-set--optioncompare-in-the-visual-studio-ide"></a>-Optioncompare Visual Studio IDE에서 설정 하려면  
  
1.  **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 **속성**을 클릭합니다.   
  
2.  **컴파일** 탭을 클릭합니다.  
  
3.  값을 수정 된 **Option Compare** 상자입니다.  
  
### <a name="to-set--optioncompare-programmatically"></a>-Optioncompare를 프로그래밍 방식으로 설정 하려면  
  
-   참조 [Option Compare 문](../../../visual-basic/language-reference/statements/option-compare-statement.md)합니다.  
  
## <a name="example"></a>예제  
 다음 코드에서는 `ProjFile.vb` 컴파일하고 이진 문자열 비교를 사용 합니다.  
  
```console
vbc -optioncompare:binary projFile.vb  
```  
  
## <a name="see-also"></a>참고 항목  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
 [-optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)  
 [-optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)  
 [-optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md)  
 [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)  
 [Option Compare 문](../../../visual-basic/language-reference/statements/option-compare-statement.md)  
 [옵션 대화 상자, 프로젝트, Visual Basic 기본값](/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
