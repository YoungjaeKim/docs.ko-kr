---
title: 명령줄에서 빌드(Visual Basic)
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- builds [Visual Basic], command-line
- Visual Basic compiler, about Visual Basic compiler
- command line [Visual Basic], compilers
- command line [Visual Basic], building from
- command line [Visual Basic], builds
- compilers [Visual Basic], invoking from command line
- command-line builds
- compiling source code
- command-line compilers [Visual Basic], Visual Basic
- command line [Visual Basic], Visual Basic
ms.assetid: e61947e9-a42e-4717-a699-5f70a98cdd03
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: c3f71a84feffce46bafd92ff701a0250c059a82e
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="building-from-the-command-line-visual-basic"></a>명령줄에서 빌드(Visual Basic)
A [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] 프로젝트 하나 이상의 별도 소스 파일로 구성 됩니다. 컴파일 이라는 프로세스 동안 이러한 파일 통합할 하나의 패키지로-응용 프로그램으로 실행할 수 있는 단일 실행 파일입니다.  
  
 [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] 내에서 프로그램을 컴파일 하는 대신 명령줄 컴파일러를 제공는 [!INCLUDE[vsprvs](~/includes/vsprvs-md.md)] 통합된 개발 환경 (IDE). 명령줄 컴파일러는 필요 하지 않으면 IDE의 기능 중 일부만 상황 용인지-예를 들어 경우 있습니다 하거나 작성 하는 제한 된 시스템 메모리 또는 저장소 공간이 있는 컴퓨터에 대 한 합니다.  
  
  내에서 소스 파일을 컴파일하는 [!INCLUDE[vsprvs](~/includes/vsprvs-md.md)] IDE, 선택는 **빌드** 명령을 **빌드** 메뉴.  
  
> [!TIP]
>  연결 된 작업에 대 한 정보를 표시할 수는 Visual Studio IDE를 사용 하 여 프로젝트 파일을 빌드할 때 **vbc** 명령 및 출력 창에 해당 스위치입니다. 이 정보를 표시 하려면 엽니다는 [옵션 대화 상자, 프로젝트 및 솔루션, 빌드 및 실행](/visualstudio/ide/reference/options-dialog-box-projects-and-solutions-build-and-run)를 설정한는 **MSBuild 프로젝트 빌드 출력의 자세한 정도** 를 **보통** 또는 더 높은 수준의 세부 정보 표시 합니다. 자세한 내용은 [방법: 빌드 로그 파일 보기, 저장 및 구성](http://msdn.microsoft.com/library/75d38b76-26d6-4f43-bbe7-cbacd7cc81e7)을 참조하세요.  
  
 MSBuild를 사용 하 여 명령 프롬프트에서 프로젝트 (.vbproj) 파일을 컴파일할 수 있습니다. 자세한 내용은 참조 [Command-Line Reference](/visualstudio/msbuild/msbuild-command-line-reference) 및 [연습: MSBuild를 사용 하 여](/visualstudio/msbuild/walkthrough-using-msbuild)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [방법: 명령줄 컴파일러 호출](../../../visual-basic/reference/command-line-compiler/how-to-invoke-the-command-line-compiler.md)  
 MS-DOS 프롬프트 또는 특정 하위 디렉터리에서 명령줄 컴파일러를 호출 하는 방법을 설명 합니다.  
  
 [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)  
 사용자만 수정할 수 있는 샘플 명령줄의 목록을 제공 합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
 컴파일러 옵션을 사전순 또는 용도 따라 구성의 목록을 제공 합니다.  
  
 [조건부 컴파일](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)  
 코드의 특정 섹션을 컴파일하는 방법에 설명 합니다.  
  
 [Visual Studio에서 프로젝트 및 솔루션 빌드 및 정리](/visualstudio/ide/building-and-cleaning-projects-and-solutions-in-visual-studio)  
 다양 한 빌드에 포함 될 것, 프로젝트 속성을 선택 및 올바른 순서로 프로젝트를 빌드하는 기능을 구성 하는 방법에 설명 합니다.
