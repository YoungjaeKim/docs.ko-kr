---
title: WCF 서비스 이름 바꾸기
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 14235a65-b1c5-409d-b6cc-a979acd54bbd
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: f2ab3d780f85131fc7adf24c5f420bd5fe643d9e
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="renaming-a-wcf-service"></a>WCF 서비스 이름 바꾸기
이 항목에서는 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 서비스 이름을 바꾸는 방법을 설명합니다.  
  
## <a name="renaming-a-wcf-service"></a>WCF 서비스 이름 바꾸기  
 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 템플릿에서 서비스 이름을 바꾸려면 다음 단계를 수행합니다.  
  
-   서비스를 구현하는 클래스 이름을 변경합니다.  
  
-   다음 예제에 표시된 대로 서비스의 구성 파일에서 선택한 새 이름으로 서비스 이름을 변경합니다. 구성 파일은 호스팅 모델에 따라 app.config 또는 web.config 파일입니다.  
  
```xml  
<system.servicemodel>  
   <services>  
      <service name="WcfService.NewName">  
      </service>  
   </services>  
</system.servicemodel>  
```  
  
-   서비스가 WebHosted인 경우 *.svc 파일을 사용합니다. svc 파일을 열고 다음 예제에 표시된 대로 서비스 이름을 수정합니다. svc 파일이 없는 경우 이 단계는 자체 호스팅 응용 프로그램에 필요하지 않습니다.  
  
```  
<%@ ServiceHost Service="WcfService.NewName">  
```  
  
## <a name="renaming-a-wcf-service-contract"></a>WCF 서비스 계약 이름 바꾸기  
  
-   서비스 계약 이름을 바꾸려면 다음 단계를 수행합니다.  
  
-   서비스 계약 이름을 변경합니다.  
  
-   다음 예제에 표시된 대로 서비스의 구성 파일에서 선택한 새 이름으로 서비스 계약 이름을 변경합니다. 구성 파일은 호스팅 모델에 따라 app.config 또는 web.config 파일입니다.  
  
```xml  
<system.servicemodel>  
   <services>  
      <service>  
         <endpoint contract="WcfService.NewContractName" />  
      </service>  
   </services>  
</system.servicemodel>  
```
