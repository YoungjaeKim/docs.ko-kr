---
title: -errorreport
ms.date: 03/10/2018
ms.prod: .net
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- -errorreport compiler option [Visual Basic]
- /errorreport compiler option [Visual Basic]
- errorreport compiler option [Visual Basic]
ms.assetid: a7fe83a2-a6d8-460c-8dad-79a8f433f501
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 59dc833299161eac7b119e654c94534f202b1cb7
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="-errorreport"></a>-errorreport
[!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] 컴파일러에서 내부 컴파일러 오류를 보고하는 방식을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
-errorreport:{ prompt | queue | send | none }  
```  
  
## <a name="remarks"></a>설명  
 이 옵션은 보고서에는 편리한 방법을 제공는 [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] 에 내부 컴파일러 오류 (ICE)는 [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] 팀 시작 합니다. 기본적으로 컴파일러 정보가 Microsoft에 보냅니다. 그러나 내부 컴파일러 오류를 발생 수행 하면이 옵션 Microsoft로 오류를 보고할 수 있습니다. 해당 정보 Microsoft 엔지니어가 원인을 파악 하는 데 도움이 되며 다음 릴리스의 향상 하는 데 도움이 될 수 있습니다 [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)]합니다.  
  
 컴퓨터 및 사용자 정책 사용 권한에 사용자의 보고서를 보낼 수 있는 기능에 따라 다릅니다.  
  
 다음 표에서 요약의 효과 `-errorreport` 옵션입니다.  
  
|옵션|동작|  
|---|---|  
|`prompt`|내부 컴파일러 오류가 발생 하는 경우 컴파일러에서 수집한 정확한 데이터를 볼 수 있도록 대화 상자 제공 됩니다. 모든 중요 한 정보가 오류 보고서에 없는 경우를 확인 하 고 Microsoft로 보낼지 여부를 결정 합니다. 보내기,로 컴퓨터 및 사용자 정책 설정에서 허용 하는 경우 컴파일러는 데이터를 Microsoft로 보냅니다.|  
|`queue`|오류 보고서를 큐에 넣습니다. 관리자 권한으로 로그인 하는 경우에 기록 된 마지막 시간 이후 발생 한 모든 오류를 보고할 수 있습니다 (하면 메시지가 표시 되지 것입니다 3 일에 두 번 이상 실패에 대 한 보고서를 보내도록). 이것이 기본 동작 때는 `-errorreport` 옵션을 지정 하지 않습니다.|  
|`send`|내부 컴파일러 오류가 발생 하 고 컴퓨터 및 사용자 정책 설정에서 허용, 컴파일러는 데이터를 Microsoft로 보냅니다.<br /><br /> 옵션 `-errorreport:send` Microsoft로 오류 정보를 자동으로 보내려고 시도 합니다. 이 옵션은 레지스트리에 따라 달라 집니다. 레지스트리에서 적절 한 값을 설정 하는 방법에 대 한 자세한 내용은 참조 [Visual Studio 2008 명령줄 도구에서 자동 오류 보고 설정 하는 방법](http://go.microsoft.com/fwlink/?LinkID=184695)합니다.|  
|`none`|내부 컴파일러 오류가 발생 하는 경우 그를 하지 수집 하거나 Microsoft로 전송 합니다.|  
  
 컴파일러는 일반적으로 일부 소스 코드를 포함 하는 오류 발생 시 스택을 포함 하는 데이터를 보냅니다. 경우 `-errorreport` 와 함께 사용 되는 [-bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md) 옵션을 전체 소스 파일에 보내집니다.  
  
 이 옵션은 함께 사용할 가장는 [/bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md) 더 많은 작업을 Microsoft 엔지니어가 오류를 쉽게 재현할 수 있기 때문에 옵션입니다.  
  
> [!NOTE]
>  `-errorreport` 옵션은 Visual Studio 개발 환경 내에서 사용할 수 없습니다; 명령줄에서 컴파일할 경우에 사용할 수는 있습니다.  
  
## <a name="example"></a>예제  
 다음 코드를 컴파일하려면 시도 `T2.vb`, 한 컴파일러에 내부 컴파일러 오류가 발생 하는 경우 Microsoft로 오류 보고서를 보낼 것인지 묻습니다.  
  
```  
vbc -errorreport:prompt t2.vb  
```  
  
## <a name="see-also"></a>참고 항목  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
 [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)  
 [-bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md)
