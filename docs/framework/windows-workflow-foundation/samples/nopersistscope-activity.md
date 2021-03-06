---
title: "NoPersistScope 활동"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9a0baeb7-a05c-4fac-b905-252758cb71bb
caps.latest.revision: "10"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: bfc651403988fa7558f79a4c99e42fb776efec4d
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/22/2017
---
# <a name="nopersistscope-activity"></a>NoPersistScope 활동
이 샘플에서는 워크플로 내의 serialize할 수 없고 삭제 가능한 상태를 처리하는 방법을 보여 줍니다. 이때 워크플로에서 serialize 불가능 상태를 지속하려고 시도하지 않는다는 점이 중요하며 삭제 가능한 개체를 워크플로에 사용하고 나면 이를 정리해야 한다는 점도 중요합니다.  
  
## <a name="demonstrates"></a>세부 항목  
 `NoPersistScope` 사용자 지정 활동 및 디자이너  
  
## <a name="using-the-nopersistzone-activity"></a>NoPersistZone 활동 사용  
 샘플 워크플로를 실행하면 `CreateTextWriter`라는 사용자 지정 활동을 통해 <xref:System.IO.TextWriter> 형식의 개체가 만들어지고 이 개체가 워크플로 변수에 저장됩니다. <xref:System.IO.TextWriter>가 <xref:System.IDisposable> 개체인 경우. 샘플이 실행되는 디렉터리의 'out.txt'라는 파일에 텍스트를 쓰도록 구성되어 있는 이 <xref:System.IO.TextWriter>는 <xref:System.Activities.Statements.WriteLine> 활동에 사용되며 사용자가 콘솔에 입력하는 모든 텍스트를 그대로 반복합니다.  
  
 이 echo 논리는 워크플로가 지속되지 않도록 하는 `NoPersistScope` 활동 내에서 실행됩니다. 이 활동의 코드도 이 샘플에 포함되어 있습니다. 에 입력 하면 `unload` 는 콘솔에서 호스트에서 워크플로 인스턴스를 지속 하려고 시도 하지만 워크플로 내에서 유지 되기 때문에이 작업 시간이 초과 `NoPersistScope`합니다. 또한 이 워크플로에서는 `Dispose` 개체 사용을 마쳤을 때 <xref:System.IO.TextWriter>라는 사용자 지정 활동을 사용하여 이 개체를 삭제합니다. `Dispose` 활동은 Try 블록을 실행하는 동안 예외가 발생하더라도 문제 없이 실행되도록 하기 위해 <xref:System.Activities.Statements.TryCatch.Finally%2A> 변수가 선언된 <xref:System.Activities.Statements.TryCatch> 활동의 <xref:System.IO.TextWriter> 블록 내에 배치됩니다.  
  
 에 입력할 수 `exit` 워크플로 인스턴스를 완료 하 고 프로그램을 끝냅니다.  
  
#### <a name="to-run-the-sample"></a>이 샘플을 실행하려면  
  
1.  [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)]에서 NoPersistZone.sln 솔루션을 엽니다.  
  
2.  솔루션을 빌드하려면 CTRL + SHIFT + B 키를 누르거나 선택 **솔루션 빌드** 에서 **빌드** 메뉴.  
  
3.  빌드가 성공한 후 F5 키를 누르거나 선택 **디버깅 시작** 에서 **디버그** 메뉴 또는 CTRL + f 5를 눌러 수도 있고 선택할 **디버깅 하지 않고 시작** 에서 **디버그** 메뉴 디버깅 없이 실행 합니다.  
  
#### <a name="to-cleanup-optional"></a>정리하려면(옵션)  
  
1.  SQL 인스턴스 저장소를 제거하려면 Cleanup.cmd를 실행합니다.  
  
> [!IMPORTANT]
>  컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  이 디렉터리가 없으면 [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4(.NET Framework 4용 WCF(Windows Communication Foundation) 및 WF(Windows Workflow Foundation) 샘플)](http://go.microsoft.com/fwlink/?LinkId=150780) 로 이동하여 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 모두 다운로드하세요. 이 샘플은 다음 디렉터리에 있습니다.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\NoPersistScope`