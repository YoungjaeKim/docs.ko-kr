---
title: 텍스트 파일 사용 추적
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 56a82682-73c2-4b91-a206-4d8bb12c561b
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: f1d4b3f319d86dd463dabc8b71be7c76c7fef41f
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/23/2018
---
# <a name="tracking-using-a-text-file"></a>텍스트 파일 사용 추적
이 샘플에서는 사용자 지정 추적 참가자를 만들어 [!INCLUDE[wf](../../../../includes/wf-md.md)]에서 추적을 확장하는 방법을 보여 줍니다. 추적 참가자는 추적 레코드를 내보낼 때 런타임에서 추적 레코드를 받는 .NET Framework 클래스입니다. 시나리오에 필요한 대상에 추적 이벤트를 전송하는 추적 참가자를 만들 수 있습니다. 예를 들어 ETW(Windows용 이벤트 추적) 추적 참가자는 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]의 일부로 제공됩니다. 이 샘플의 추적 참가자는 XML 형식의 레코드를 텍스트 파일에 기록합니다.  
  
## <a name="sample-details"></a>샘플 세부 정보  
 추적 참가자의 유용성과 견고성을 최적화하려면 추적 참가자를 런타임에 올바르게 연결하기 위한 몇 가지 추가 단계를 완료해야 합니다. 다음 표에서는 이 샘플에서 최선의 방법을 따르는 추적 참가자를 만드는 데 사용된 클래스에 대해 설명합니다.  
  
|클래스|설명|  
|-----------|-----------------|  
|`TextFileTrackingExtensionElement`|<xref:System.ServiceModel.Configuration.BehaviorExtensionElement>는 텍스트 파일 추적 참가자를 구성하는 데 사용되는 구성 섹션을 정의하는 데 사용됩니다. 이 클래스를 사용하면 사용자가 표준 .NET Framework 구성 파일을 사용하여 로그 파일의 대상을 지정할 수 있습니다.|  
|`TextFileTrackingBehavior`|[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]의 동작을 통해 사용자는 확장을 런타임에 삽입할 수 있습니다. 이 동작은 서비스가 시작될 때 추적 참가자를 서비스에 추가합니다.|  
|`TextFileTrackingParticipant`|런타임에 추적 참가자를 받아 로그 파일에 XML로 저장하는 추적 참가자입니다.|  
  
## <a name="behavior-extension-elements-configuration"></a>동작 확장 요소 구성  
 .NET Framework 구성 파일을 사용하여 이전에 설명한 동작 확장 요소를 사용하려면 하나의 단계가 더 필요합니다. 확장이 사용될 구성 파일에 다음 구성을 배치해야 합니다.  
  
```xml  
<system.serviceModel>  
    <extensions>  
      <behaviorExtensions>  
        <add name="textFileTracking" type="Microsoft.Samples.TextFileTracking.TextFileTrackingExtensionElement, WFStockPriceApplication, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />  
      </behaviorExtensions>  
    </extensions>  
…  
  </system.serviceModel>  
```  
  
> [!NOTE]
>  동작 확장 요소 구성의 자세한 예제 사용법을 보려면 샘플에 있는 Web.config 파일을 참조하세요.  
  
## <a name="custom-tracking-records"></a>사용자 지정 추적 레코드  
 GetStockPrices.cs 파일에서는 <xref:System.Activities.CodeActivity> 내에서 사용자 지정 추적 레코드를 만드는 방법을 보여 줍니다. 샘플을 실행할 때 이 레코드를 찾습니다.  
  
#### <a name="to-use-this-sample"></a>이 샘플을 사용하려면  
  
1.  [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)]을 사용하여 WFStockPriceApplication.sln 솔루션 파일을 엽니다.  
  
2.  Ctrl+Shift+B를 눌러 솔루션을 빌드합니다.  
  
3.  Ctrl+F5를 눌러 솔루션을 실행합니다.  
  
     브라우저 창이 열리고 응용 프로그램의 디렉터리 목록이 표시됩니다.  
  
4.  브라우저에서 StockPriceService.xamlx를 클릭합니다.  
  
5.  브라우저 표시는 **StockPriceService** 로컬 서비스 wsdl 주소가 포함 된 페이지가 있습니다. 이 주소를 복사합니다.  
  
     로컬 서비스 wsdl 주소의 예로는 http://localhost:53797/StockPriceService.xamlx?wsdl이 있습니다.  
  
6.  [!INCLUDE[fileExplorer](../../../../includes/fileexplorer-md.md)]를 사용하여 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 폴더로 이동합니다. 기본 설치 폴더는 %SystemDrive%\Program Files\Microsoft Visual Studio 10.0입니다. 그런 다음 Common7\IDE\ 하위 폴더를 찾습니다.  
  
7.  WcfTestClient.exe 파일을 두 번 클릭하여 WCF 테스트 클라이언트를 시작합니다.  
  
8.  WCF 테스트 클라이언트에서 선택 **서비스 추가...** **파일** 메뉴.  
  
9. 방금 복사한 URL을 텍스트 상자에 붙여 넣습니다.  
  
10. 클릭 **확인** 는 대화 상자를 닫습니다.  
  
11. WCF 테스트 클라이언트를 사용하여 서비스를 테스트합니다.  
  
    1.  WCF 테스트 클라이언트에서 두 번 클릭 **getstockprice ()** 아래는 **IStockPriceService** 노드.  
  
         **getstockprice ()** 메서드가 매개 변수를 사용 하 고 오른쪽 창에 나타납니다.  
  
    2.  매개 변수 값으로 Contoso를 입력합니다.  
  
    3.  클릭 **호출**합니다.  
  
12. 응용 프로그램 데이터 디렉터리에 있는 로그 파일(%APPDATA%\trackingRecords.log)에서 추적된 이벤트를 참조하세요.  
  
    > [!NOTE]
    >  % APPDATA %는 %SystemDrive%\Users 확인 되는 환경 변수\\< 사용자 이름\>에 \AppData\Roaming [!INCLUDE[wv](../../../../includes/wv-md.md)], [!INCLUDE[lserver](../../../../includes/lserver-md.md)], 또는 Windows Server 2008.  
  
> [!IMPORTANT]
>  컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  이 디렉터리가 없으면 [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4(.NET Framework 4용 WCF(Windows Communication Foundation) 및 WF(Windows Workflow Foundation) 샘플)](http://go.microsoft.com/fwlink/?LinkId=150780) 로 이동하여 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 모두 다운로드하세요. 이 샘플은 다음 디렉터리에 있습니다.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Tracking\TextFileTracking`  
  
## <a name="see-also"></a>참고 항목  
 [AppFabric 모니터링 샘플](http://go.microsoft.com/fwlink/?LinkId=193959)
