---
title: -bugreport
ms.date: 03/08/2018
ms.prod: .net
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- -bugreport compiler option [Visual Basic]
- bugreport compiler option [Visual Basic]
- /bugreport compiler option [Visual Basic]
ms.assetid: e4325406-8dbd-4b48-b311-9ee0799e48bb
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 766a4252fd77be95e2641239cba53a4d90e0cb1d
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="-bugreport"></a>-bugreport
버그 보고서를 파일로 작성할 때는 사용할 수 있는 파일을 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
-bugreport:file  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`file`|필수. 버그 보고서를 포함 하는 파일의 이름입니다. 파일 이름을 따옴표로 묶습니다 ("")는 이름에 공백이 포함 하는 경우.|  
  
## <a name="remarks"></a>설명  
 다음 정보에 추가 됩니다 `file`:  
  
-   컴파일할 때 모든 소스 코드 파일의 복사본입니다.  
  
-   컴파일에 사용 된 컴파일러 옵션의 목록.  
  
-   컴파일러, 공용 언어 런타임 및 운영 체제에 대 한 버전 정보입니다.  
  
-   컴파일러 출력입니다(있는 경우).  
  
-   에 대 한 메시지가 표시 되는 문제에 대 한 설명  
  
-   문제를 생각 하는 방법에 대 한 설명을 수정 되어야는 대 한 메시지가 표시 됩니다.  
  
 모든 소스 코드 파일의 복사본에 포함 되어 있으므로 `file`, 가능한 한 짧은 프로그램의 코드 결함을 재현 하는 것이 좋습니다.  
  
> [!IMPORTANT]
>  `-bugreport` 옵션은 잠재적으로 중요 한 정보가 포함 된 파일을 생성 합니다. 현재 시간, 컴파일러 버전 여기에 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 버전, 운영 체제 버전, 사용자 이름, 명령줄 인수는 컴파일러를 실행 하면서 모든 소스 코드 및 참조 된 어셈블리의 모든 이진 형식입니다. 이 옵션의 서버 쪽 컴파일에 대 한 Web.config 파일에서 명령줄 옵션을 지정 하 여 액세스할 수는 [!INCLUDE[vstecasp](~/includes/vstecasp-md.md)] 응용 프로그램입니다. 이 방지 하려면 사용자가 서버에서 컴파일하지을 Machine.config 파일을 수정 합니다.  
  
 이 옵션은 함께 사용할 경우 `-errorreport:prompt`, `-errorreport:queue`, 또는 `-errorreport:send`, 응용 프로그램의 정보는 내부 컴파일러 오류를 발견 한 `file` Microsoft Corporation에 전송 됩니다. 해당 정보 Microsoft 엔지니어가 오류의 원인을 파악 하는 데 도움이 되며의 다음 릴리스에서 향상 하는 데 도움이 될 수 있습니다 [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)]합니다. 기본적으로 Microsoft로 정보가 전송 됩니다. 그러나 컴파일하는 경우 응용 프로그램 사용 하 여 `-errorreport:queue`, 기본적으로 활성화 되어, 응용 프로그램의 오류 보고서를 수집 합니다. 그런 다음 컴퓨터의 관리자가 로그인 할 때 오류 보고 시스템 관리자 로그온 이후 발생 한 모든 오류 보고서를 Microsoft로 전달할 수 있도록 하는 팝업 창을 표시 합니다.  
  
> [!NOTE]
>  `/bugreport` 옵션은 Visual Studio 개발 환경 내에서 사용할 수 없습니다; 가능 하다는 명령줄에서 컴파일할 때만 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 컴파일합니다 `T2.vb` 파일에 모든 버그 보고 정보를 저장 하 고 `Problem.txt`합니다.  
  
```  
vbc -bugreport:problem.txt t2.vb  
```  
  
## <a name="see-also"></a>참고 항목  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
 [-디버그 (Visual Basic)](../../../visual-basic/reference/command-line-compiler/debug.md)  
 [-errorreport](../../../visual-basic/reference/command-line-compiler/errorreport.md)  
 [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)  
 [securityPolicy (ASP.NET 설정 스키마)에 대 한 trustLevel 요소](http://msdn.microsoft.com/library/729ab04c-03da-4ee5-86b1-be9d08a09369)
