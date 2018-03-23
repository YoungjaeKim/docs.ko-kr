---
title: 샘플 컴파일 명령줄(Visual Basic)
ms.date: 03/13/2018
ms.prod: .net
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- command line [Visual Basic], compilers
- compilation [Visual Basic], command-line
- command-line compilers
- compiling source code [Visual Basic], from command line
- Visual Basic compiler, sample command lines
ms.assetid: 5bfbb487-5f47-4267-969a-39dfb917beeb
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cf20e2916efd2eb10065be22c319e34ddb2bda9a
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/23/2018
---
# <a name="sample-compilation-command-lines-visual-basic"></a>샘플 컴파일 명령줄 (Visual Basic)
Visual Basic 프로그램 내에서 컴파일 하는 대신 [!INCLUDE[vsprvs](~/includes/vsprvs-md.md)], 실행 파일 (.exe) 또는 동적 연결 라이브러리 (.dll) 파일을 생성 하기 위해 명령줄에서 컴파일할 수 있습니다.  
  
 Visual Basic 명령줄 컴파일러 입출력 파일, 어셈블리 및 디버그 및 전처리기 옵션을 제어 하는 옵션 집합을 지원 합니다. 각 옵션은 서로 바꿔 사용할 수 있는 두 가지 형태로 사용할 수 있는: `-option` 및 `/option`합니다. 이 설명서 표시는 `-option` 폼입니다.  
  
 다음 표에서 일부 예제 명령줄 사용자만 수정할 수 있습니다.  
  
|대상|사용|  
|--------|---------|  
|File.vb 컴파일하고 File.exe 만들기|`vbc -reference:Microsoft.VisualBasic.dll File.vb`|  
|File.vb 컴파일하고 File.dll 만들기|`vbc -target:library File.vb`|  
|File.vb 컴파일하고 My.exe 만들기|`vbc -out:My.exe File.vb`|  
|File.vb 컴파일하고 라이브러리와 File.dll 이라는 참조 어셈블리를 만들|`vbc -target:library -ref:.\debug\bin\ref\file.dll File.vb`|
|최적화 된 현재 디렉터리에 있는 모든 Visual Basic 파일에서 컴파일 및 `DEBUG` File2.exe 생성 정의 기호|`vbc -define:DEBUG=1 -optimize -out:File2.exe *.vb`|  
|로고 또는 경고를 표시 하지 않고 File2.dll의 디버그 버전을 생성 하는 현재 디렉터리에 있는 모든 Visual Basic 파일을 컴파일하십시오.|`vbc -target:library -out:File2.dll -nowarn -nologo -debug *.vb`|  
|현재 디렉터리 Something.dll에 있는 모든 Visual Basic 파일을 컴파일하십시오.|`vbc -target:library -out:Something.dll *.vb`|  
  
> [!TIP]
>  연결 된 작업에 대 한 정보를 표시할 수는 Visual Studio IDE를 사용 하 여 프로젝트를 빌드할 때 **vbc** 명령을 출력 창에 해당 컴파일러 옵션을 사용 합니다. 이 정보를 표시 하려면 엽니다는 [옵션 대화 상자, 프로젝트 및 솔루션, 빌드 및 실행](/visualstudio/ide/reference/options-dialog-box-projects-and-solutions-build-and-run)를 설정한는 **MSBuild 프로젝트 빌드 출력의 자세한 정도** 를 **보통** 또는 더 높은 수준의 세부 정보 표시 합니다.   
  
## <a name="see-also"></a>참고 항목  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
 [조건부 컴파일](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)
