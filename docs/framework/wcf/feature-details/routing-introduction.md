---
title: "라우팅 소개"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bf6ceb38-6622-433b-9ee7-f79bc93497a1
caps.latest.revision: 
author: wadepickett
ms.author: wpickett
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: e0fe14f096ae0914235ea1d23b874f0aea906d9d
ms.sourcegitcommit: 15316053918995cc1380163a7d7e7edd5c44e6d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2018
---
# <a name="routing-introduction"></a>라우팅 소개
라우팅 서비스는 메시지 내용에 따라 메시지를 라우트할 수 있는 제네릭 플러그형 SOAP 매개자를 제공합니다. 라우팅 서비스를 사용하면 서비스 집계, 서비스 버전 관리, 우선 순위 라우팅 및 멀티캐스트 라우팅과 같은 시나리오를 구현할 수 있도록 하는 복합적인 라우팅 논리를 만들 수 있습니다. 또한 라우팅 서비스는 오류 처리 기능을 제공하므로 기본 대상 끝점으로 메시지를 보내는 중 오류가 발생할 경우 이 기능을 통해 메시지를 보낼 백업 끝점 목록을 설정할 수 있습니다.  
  
 이 항목은 라우팅 서비스를 새로 접하는 사용자를 대상으로 하며 기본적인 구성과 라우팅 서비스의 호스팅에 대해 설명합니다.  
  
## <a name="configuration"></a>구성  
 라우팅 서비스는 클라이언트 응용 프로그램으로부터 메시지를 수신하여 이 메시지를 하나 이상의 대상 끝점으로 라우트하는 하나 이상의 서비스 끝점을 노출하는 WCF 서비스로 구현됩니다. 이 서비스는 서비스에 의해 노출되는 서비스 끝점에 적용되는 <xref:System.ServiceModel.Routing.RoutingBehavior>를 제공합니다. 이 동작은 서비스 작동 방식의 다양한 측면을 구성하는 데 사용됩니다. 에 지정 된 매개 변수는 구성 파일을 사용 하는 경우 구성의 쉽도록는 **RoutingBehavior**합니다. 코드 기반 시나리오에서 이러한 매개 변수는 지정할 수의 일부로 <xref:System.ServiceModel.Routing.RoutingConfiguration> 에 전달 될 수 있는 개체는 **RoutingBehavior**합니다.  
  
 이러한 동작은 시작 시 SOAP 메시지 처리를 수행하는 데 사용되는 <xref:System.ServiceModel.Routing.SoapProcessingBehavior>를 클라이언트 끝점에 추가합니다. 이렇게 하면 라우팅 서비스에서 필요한 다른 끝점에 메시지를 전송할 수 있습니다. **MessageVersion** 보다 메시지 수신 된 끝점과 합니다. **RoutingBehavior** 도 서비스 확장을 등록는 <xref:System.ServiceModel.Routing.RoutingExtension>, 런타임에 라우팅 서비스 구성을 수정 하기 위한 액세스 지점을 제공 합니다.  
  
 **RoutingConfiguration** 클래스 구성과 라우팅 서비스의 구성을 업데이트 하는 일관성 있는 방법을 제공 합니다.  라우팅 서비스에 대 한 설정으로 작동 하 고 구성 하는 데 사용 되는 매개 변수가 포함는 **RoutingBehavior** 서비스가 시작 될 때에 전달 되었습니다는 **RoutingExtension** 라우팅 수정 하려면 런타임 시 구성입니다.  
  
 내용을 기반으로 메시지를 라우트하는 데 사용되는 라우팅 논리는 여러 <xref:System.ServiceModel.Dispatcher.MessageFilter> 개체를 필터 테이블(<xref:System.ServiceModel.Dispatcher.MessageFilterTable%601> 개체)로 그룹화하여 정의합니다. 들어오는 메시지는 각각에 대해 및 필터 테이블에 포함 된 메시지 필터에 대해 평가 **MessageFilter** 대상 끝점으로 전달 된 메시지와 일치 하는 합니다. 사용 하 여 메시지를 라우팅할 사용 해야 하는 필터 테이블을 지정 하는 **RoutingBehavior** 또는 사용 하 여 코드를 통해 구성에는 **RoutingConfiguration** 개체입니다.  
  
### <a name="defining-endpoints"></a>끝점 정의  
 구성의 첫 작업은 사용할 라우팅 논리를 정의하는 것이라고 생각하기 쉽지만 사실 수행해야 할 첫 번째 단계는 메시지를 라우트할 끝점의 셰이프를 결정하는 것입니다. 라우팅 서비스는 메시지를 보내고 받는 데 사용되는 채널의 셰이프를 정의하는 계약을 사용하므로 입력 채널의 셰이프는 출력 채널의 셰이프와 일치해야 합니다.  예를 들어 요청-회신 채널 셰이프를 사용하는 끝점으로 라우트하는 경우 인바운드 끝점에 호환되는 계약을 사용해야 합니다(예: <xref:System.ServiceModel.Routing.IRequestReplyRouter>).  
  
 이는 대상 끝점이 여러 통신 패턴을 가진 계약을 사용하는 경우(예: 단방향과 양방향 작업의 혼합) 이러한 모든 끝점에서 메시지를 수신하고 라우트할 수 있는 하나의 서비스 끝점을 만들 수 없음을 의미합니다. 호환되는 셰이프를 가진 끝점을 확인하고 대상 끝점으로 라우트될 메시지를 수신하는 데 사용될 하나 이상의 서비스 끝점을 정의해야 합니다.  
  
> [!NOTE]
>  여러 통신 패턴을 지정하는 계약을 사용하는 경우(예: 단방향과 양방향 작업의 혼합) 해결 방법은 라우팅 서비스에서 이중 계약을 사용하는 것입니다(예: <xref:System.ServiceModel.Routing.IDuplexSessionRouter>). 그러나 이는 바인딩이 이중 통신을 수행할 수 있어야 함을 의미하므로 이 방법이 가능하지 않은 경우도 있습니다. 이 방법이 가능하지 않은 시나리오에서는 통신을 여러 끝점으로 팩터링하거나 응용 프로그램을 수정해야 할 수 있습니다.  
  
 라우팅 계약에 대 한 자세한 내용은 참조 [라우팅 계약](../../../../docs/framework/wcf/feature-details/routing-contracts.md)합니다.  
  
 서비스 끝점이 정의 된 후 사용할 수 있습니다는 **RoutingBehavior** 특정 연결할 **RoutingConfiguration** 끝점을 사용 합니다. 구성 파일을 사용 하 여 라우팅 서비스를 구성 하는 경우는 **RoutingBehavior** 이 끝점에서 받은 메시지를 처리 하는 데 사용 하는 라우팅 논리를 포함 하는 필터 테이블을 지정 하는 데 사용 됩니다. 구성 하는 경우 라우팅 서비스에서 프로그래밍 방식으로 사용 하 여 필터 테이블을 지정할 수 있습니다는 **RoutingConfiguration**합니다.  
  
 다음 예제에서는 라우팅 서비스에서 프로그래밍 방식으로, 구성 파일을 통해 사용되는 서비스와 클라이언트 끝점을 정의합니다.  
  
```xml  
    <services>  
      <!--ROUTING SERVICE -->  
      <service behaviorConfiguration="routingData"  
               name="System.ServiceModel.Routing.RoutingService">  
        <host>  
          <baseAddresses>  
            <add baseAddress="http://localhost:8000/routingservice/router"/>  
          </baseAddresses>  
        </host>  
        <!-- Define the service endpoints that are receive messages -->  
        <endpoint address=""  
                  binding="wsHttpBinding"  
                  name="reqReplyEndpoint"  
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />      
      </service>  
    </services>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="routingData">  
          <serviceMetadata httpGetEnabled="True"/>  
          <!-- Add the RoutingBehavior and specify the Routing Table to use -->  
          <routing filterTableName="routingTable1" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    <client>  
    <!-- Define the client endpoint(s) to route messages to -->  
      <endpoint name="CalculatorService"  
                address="http://localhost:8000/servicemodelsamples/service"  
                binding="wsHttpBinding" contract="*" />  
    </client>  
```  
  
```csharp  
//set up some communication defaults  
string clientAddress = "http://localhost:8000/servicemodelsamples/service";  
string routerAddress = "http://localhost:8000/routingservice/router";  
Binding routerBinding = new WSHttpBinding();  
Binding clientBinding = new WSHttpBinding();  
//add the endpoint the router uses to receive messages  
serviceHost.AddServiceEndpoint(  
     typeof(IRequestReplyRouter),   
     routerBinding,   
     routerAddress);  
//create the client endpoint the router routes messages to  
ContractDescription contract = ContractDescription.GetContract(  
     typeof(IRequestReplyRouter));  
ServiceEndpoint client = new ServiceEndpoint(  
     contract,   
     clientBinding,   
     new EndpointAddress(clientAddress));  
//create a new routing configuration object  
RoutingConfiguration rc = new RoutingConfiguration();  
….  
rc.FilterTable.Add(new MatchAllMessageFilter(), endpointList);  
//attach the behavior to the service host  
serviceHost.Description.Behaviors.Add(  
     new RoutingBehavior(rc));  
```  
  
 이 예제에서는 ": //localhost: 8000/라우팅 서비스/라우터" 라우트될 메시지를 수신 하는 데 사용 되는 주소를 가진 단일 끝점을 노출 하도록 라우팅 서비스를 구성 합니다. 메시지는 요청-회신 끝점으로 라우트되므로 서비스 끝점은 <xref:System.ServiceModel.Routing.IRequestReplyRouter> 계약을 사용합니다. 또한이 구성은 ": //localhost: 8000/servicemodelsample/service" 메시지를 라우팅할의 단일 클라이언트 끝점을 정의 합니다. 필터 테이블 (표시 되지 않음) "routingtable1" 메시지를 라우트하는 데 사용 하는 라우팅 논리를 포함 하 고 사용 하 여 서비스 끝점과 연결 된는 **RoutingBehavior** (구성 파일)에 대 한 또는  **RoutingConfiguration** 프로그래밍 방식으로 구성 합니다.  
  
### <a name="routing-logic"></a>라우팅 논리  
 메시지를 라우트하는 데 사용되는 라우팅 논리를 정의하려면 들어오는 메시지에 포함된, 고유한 작업 대상이 될 수 있는 데이터를 확인해야 합니다. 예를 들어 라우트하는 모든 대상 끝점이 동일한 SOAP 작업을 공유하는 경우 메시지 내에 포함된 Action 값은 메시지를 라우트해야 할 특정 끝점을 나타내는 지표로 적절하지 않습니다. 하나의 특정 끝점으로 메시지를 고유하게 라우트해야 하는 경우 메시지가 라우트되는 대상 끝점을 고유하게 식별하는 데이터를 대상으로 필터링해야 합니다.  
  
 라우팅 서비스에는 몇 가지 **MessageFilter** 주소, 작업, 끝점 이름 또는 XPath 쿼리에 같은 메시지 내의 특정 값을 검사 하는 구현 합니다. 이러한 구현 중 어떤 사용자의 요구에 맞지 않을 경우에 사용자 지정을 만들 수 있습니다 **MessageFilter** 구현 합니다. 메시지 필터 및 라우팅 서비스에서 사용 하는 구현 비교 하는 방법에 대 한 자세한 내용은 참조 [메시지 필터](../../../../docs/framework/wcf/feature-details/message-filters.md) 및 [필터 선택](../../../../docs/framework/wcf/feature-details/choosing-a-filter.md)합니다.  
  
 각각에 연결 하는 필터 테이블에 여러 메시지 필터는 함께 구성 된 **MessageFilter** 대상 끝점을 사용 합니다. 또한 필요에 따라 필터 테이블은 전송 오류가 발생할 경우 라우팅 서비스가 메시지 보내기를 시도할 백업 끝점 목록을 지정하는 데 사용될 수도 있습니다.  
  
 기본적으로 필터 테이블 내의 모든 메시지 필터는 동시에 평가되지만 메시지 필터가 특정 순서에 따라 평가되도록 하는 <xref:System.ServiceModel.Routing.Configuration.FilterTableEntryElement.Priority%2A>를 지정할 수 있습니다. 우선 순위가 가장 높은 모든 항목이 가장 먼저 평가되며, 상대적으로 더 높은 우선 순위 수준에서 일치하는 항목이 발견될 경우 이에 비해 우선 순위가 낮은 메시지 필터는 평가되지 않습니다. 필터 테이블에 대 한 자세한 내용은 참조 [메시지 필터](../../../../docs/framework/wcf/feature-details/message-filters.md)합니다.  
  
 다음 예제에서는 모든 메시지에 대해 <xref:System.ServiceModel.Dispatcher.MatchAllMessageFilter>를 반환하는 `true`를 사용합니다. 이 **MessageFilter** 연결 하는 "routingTable1" 필터 테이블에 추가 되는 **MessageFilter** "CalculatorService" 라는 클라이언트 끝점을 사용 합니다. **RoutingBehavior** 다음이 테이블 서비스 끝점에서 처리할 메시지를 라우팅하는 데 사용 해야 함을 지정 합니다.  
  
```xml  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="routingData">  
      <serviceMetadata httpGetEnabled="True"/>  
      <!-- Add the RoutingBehavior and specify the Routing Table to use -->  
      <routing filterTableName="routingTable1" />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
<!--ROUTING SECTION -->  
<routing>  
  <filters>  
    <filter name="MatchAllFilter1" filterType="MatchAll" />  
  </filters>  
  <filterTables>  
    <table name="routingTable1">  
      <filters>  
        <add filterName="MatchAllFilter1" endpointName="CalculatorService" />  
      </filters>  
    </table>  
  </filterTables>  
</routing>  
```  
  
```csharp  
//create a new routing configuration object  
RoutingConfiguration rc = new RoutingConfiguration();  
//create the endpoint list that contains the endpoints to route to  
//in this case we have only one  
List<ServiceEndpoint> endpointList = new List<ServiceEndpoint>();  
endpointList.Add(client);  
//add a MatchAll filter to the Router's filter table  
//map it to the endpoint list defined earlier  
//when a message matches this filter, it is sent to the endpoint contained in the list  
rc.FilterTable.Add(new MatchAllMessageFilter(), endpointList);  
```  
  
> [!NOTE]
>  기본적으로 라우팅 서비스는 메시지의 헤더만 평가합니다. 필터에서 메시지 본문에 액세스하도록 허용하려면 <xref:System.ServiceModel.Routing.RoutingConfiguration.RouteOnHeadersOnly%2A>를 `false`로 설정해야 합니다.  
  
 **Multicast**  
  
 많은 라우팅 서비스 구성에서 하나의 특정 끝점으로만 메시지를 라우트하는 단독 필터 논리를 사용하지만 주어진 메시지를 여러 대상 끝점으로 라우트해야 하는 경우도 있습니다. 메시지를 여러 대상으로 멀티캐스트하려면 다음 조건이 충족되어야 합니다.  
  
-   클라이언트 응용 프로그램은 요청에 대한 응답으로 하나의 회신만 수신할 수 있으므로 채널 셰이프가 요청-회신이면 안 됩니다.  
  
-   메시지를 평가할 때 여러 필터에서 `true`를 반환해야 합니다.  
  
 이러한 조건이 충족되면 `true`를 반환하는 모든 필터의 모든 끝점으로 메시지가 라우트됩니다. 다음 예제에서는 메시지의 끝점 주소가 http://localhost:8000/routingservice/router/rounding인 경우 두 끝점으로 모두 메시지가 라우트되는 라우팅 구성을 정의합니다.  
  
```xml  
<!--ROUTING SECTION -->  
<routing>  
  <filters>  
    <filter name="MatchAllFilter1" filterType="MatchAll" />  
    <filter name="RoundingFilter1" filterType="EndpointAddress"  
            filterData="http://localhost:8000/routingservice/router/rounding" />  
  </filters>  
  <filterTables>  
    <table name="routingTable1">  
      <filters>  
        <add filterName="MatchAllFilter1" endpointName="CalculatorService" />  
        <add filterName="RoundingFilter1" endpointName="RoundingCalcService" />  
      </filters>  
    </table>  
  </filterTables>  
</routing>  
```  
  
```csharp  
rc.FilterTable.Add(new MatchAllMessageFilter(), calculatorEndpointList);  
rc.FilterTable.Add(new EndpointAddressMessageFilter(new EndpointAddress(  
    "http://localhost:8000/routingservice/router/rounding")),  
    roundingCalcEndpointList);  
```  
  
### <a name="soap-processing"></a>SOAP 처리  
 서로 다른 프로토콜 간의 메시지 라우팅을 지원 하기 위해는 **RoutingBehavior** 기본적으로 추가 <xref:System.ServiceModel.Routing.SoapProcessingBehavior> 메시지가 라우팅되는 모든 클라이언트 끝점에 있습니다. 이 문제를 자동으로 새 만듭니다 **MessageVersion** 하기 전에 끝점에 메시지 라우팅 효과적으로 호환 되는 **MessageVersion** 를 반환 하기 전에 모든 응답 문서에 대 한 요청 클라이언트 응용 프로그램입니다.  
  
 새을 만드는 데 필요한 단계 **MessageVersion** 아웃 바운드 메시지에는 다음과 같습니다.  
  
 **요청 처리**  
  
-   가져오기는 **MessageVersion** 아웃 바운드 바인딩/채널의 합니다.  
  
-   원본 메시지에 대한 본문 판독기를 가져옵니다.  
  
-   동일한 작업, 본문 판독기 및 새 새 메시지를 만들고 **MessageVersion**합니다.  
  
-   경우 <xref:System.ServiceModel.Channels.MessageVersion.Addressing%2A> ! = **Addressing.None**, To, From, FaultTo 복사 및 RelatesTo 헤더를 새 메시지입니다.  
  
-   모든 메시지 속성을 새 메시지에 복사합니다.  
  
-   응답을 처리할 때 사용할 원본 요청 메시지를 저장합니다.  
  
-   새 요청 메시지를 반환합니다.  
  
 **응답 처리**  
  
-   가져오기는 **MessageVersion** 원본 요청 메시지입니다.  
  
-   수신한 응답 메시지에 대한 본문 판독기를 가져옵니다.  
  
-   새 응답 메시지를 동일한 작업, 본문 판독기 만들기 및 **MessageVersion** 원래 요청 메시지의 합니다.  
  
-   경우 <xref:System.ServiceModel.Channels.MessageVersion.Addressing%2A> ! = **Addressing.None**, To, From, FaultTo 복사 및 RelatesTo 헤더를 새 메시지입니다.  
  
-   메시지 속성을 새 메시지에 복사합니다.  
  
-   새 응답 메시지를 반환합니다.  
  
 하지만 기본적으로는 **SoapProcessingBehavior** 의해 클라이언트 끝점에 자동으로 추가 되는 <xref:System.ServiceModel.Routing.RoutingBehavior> 서비스가 시작할 때 않으면 SOAP 처리를 사용 하 여 모든 클라이언트 끝점에 추가 되는지 여부를 제어할 수는는 <xref:System.ServiceModel.Routing.RoutingConfiguration.SoapProcessingEnabled%2A> 속성입니다. 또한 SOAP 처리에 대한 더 세부적인 제어가 필요한 경우에는 특정 끝점에 동작을 직접 추가하고 끝점 수준에서 이 동작을 사용하거나 사용하지 않도록 설정할 수 있습니다.  
  
> [!NOTE]
>  원본 요청 메시지와 다른 MessageVersion을 요구하는 끝점에 대해 SOAP 처리를 사용하지 않도록 설정할 경우 메시지를 대상 끝점으로 보내기 전에 필요한 SOAP 수정 작업을 수행하기 위한 사용자 지정 메커니즘을 제공해야 합니다.  
  
 다음 예에는 **soapProcessingEnabled** 속성을 사용 하지 않도록는 **SoapProcessingBehavior** 모든 클라이언트 끝점에 자동으로 추가 되지 않도록 합니다.  
  
```xml  
<behaviors>  
  <!--default routing service behavior definition-->  
  <serviceBehaviors>  
    <behavior name="routingConfiguration">  
      <routing filterTableName="filterTable1" soapProcessingEnabled="false"/>  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
```csharp  
//create the default RoutingConfiguration  
RoutingConfiguration rc = new RoutingConfiguration();  
rc.SoapProcessingEnabled = false;  
```  
  
### <a name="dynamic-configuration"></a>동적 구성  
 부가적인 클라이언트 끝점을 추가하는 경우 또는 메시지를 라우트하는 데 사용되는 필터를 수정해야 하는 경우 현재 라우팅 서비스를 통해 메시지를 수신하는 끝점에 대한 서비스를 중단시키지 않도록 런타임에 동적으로 구성을 업데이트하는 방법이 필요합니다. 구성 파일이나 호스트 응용 프로그램의 코드를 수정하는 것으로는 부족한 경우가 있습니다. 두 방법에는 모두 응용 프로그램 재활용이 필요하고, 이 경우 현재 전송 중인 메시지가 손실될 가능성, 그리고 서비스가 다시 시작될 때까지 대기하는 동안 작동 중단이 발생할 가능성이 있기 때문입니다.  
  
 수정할 수 있습니다는 **RoutingConfiguration** 프로그래밍 방식으로 합니다. 구성 파일을 사용 하 여 처음 서비스를 구성할 수만 구성을 수정할 수 있습니다는 런타임 시 새 구성 하 여 **RoutingConfigution** 에 대 한 매개 변수로 전달 하는 <xref:System.ServiceModel.Routing.RoutingExtension.ApplyConfiguration%2A> 메서드 에 의해 노출 된 <xref:System.ServiceModel.Routing.RoutingExtension> 서비스 확장 합니다. 현재 전송 중인 메시지가 계속 이전 구성을 호출 후에 수신 된 메시지를 사용 하 여 전달 **ApplyConfiguration** 새 구성을 사용 합니다. 다음 예제에서는 라우팅 서비스의 인스턴스를 만들고 그 후 구성을 수정하는 것을 보여 줍니다.  
  
```csharp  
RoutingConfiguration routingConfig = new RoutingConfiguration();  
routingConfig.RouteOnHeadersOnly = true;  
routingConfig.FilterTable.Add(new MatchAllMessageFilter(), endpointList);  
RoutingBehavior routing = new RoutingBehavior(routingConfig);  
routerHost.Description.Behaviors.Add(routing);  
routerHost.Open();  
// Construct a new RoutingConfiguration  
RoutingConfiguration rc2 = new RoutingConfiguration();  
ServiceEndpoint clientEndpoint = new ServiceEndpoint();  
ServiceEndpoint clientEndpoint2 = new ServiceEndpoint();  
// Add filters to the FilterTable in the new configuration  
rc2.FilterTable.add(new MatchAllMessageFilter(),  
       new List<ServiceEndpoint>() { clientEndpoint });  
rc2.FilterTable.add(new MatchAllMessageFilter(),  
       new List<ServiceEndpoint>() { clientEndpoint2 });  
rc2.RouteOnHeadersOnly = false;  
// Apply the new configuration to the Routing Service hosted in  
routerHost.routerHost.Extensions.Find<RoutingExtension>().ApplyConfiguration(rc2);  
```  
  
> [!NOTE]
>  이 방법으로 라우팅 서비스를 업데이트하는 경우 새 구성을 전달하는 것만 가능합니다. 현재 구성에서 선택한 요소만 수정하거나 현재 구성에 새 항목을 추가하는 것은 불가능합니다. 즉, 기존 구성을 대체하는 새 구성을 만들어 전달해야 합니다.  
  
> [!NOTE]
>  이전 구성을 사용하여 열린 세션은 계속 이전 구성을 사용합니다. 새 구성은 새 세션에서만 사용됩니다.  
  
## <a name="error-handling"></a>오류 처리  
 메시지를 보내려고 시도하는 중에 <xref:System.ServiceModel.CommunicationException>이 발생하는 경우 오류 처리가 수행됩니다. 일반적으로 이러한 예외는 정의된 클라이언트 끝점과 통신을 시도하는 중에 문제가 발생했음을 나타냅니다(예: <xref:System.ServiceModel.EndpointNotFoundException>, <xref:System.ServiceModel.ServerTooBusyException> 또는 <xref:System.ServiceModel.CommunicationObjectFaultedException>). 오류 처리 코드를 catch 및 때 보내기를 재시도 합니다도 <xref:System.TimeoutException> 발생에서 파생 되지 않은 또 다른 일반적인 예외인 **CommunicationException**합니다.  
  
 앞서 언급한 예외 중 하나가 발생하면 라우팅 서비스는 백업 끝점 목록으로 장애 조치됩니다. 모든 백업 끝점이 통신 오류로 인해 실패하거나 끝점에서 대상 서비스 내의 오류를 나타내는 예외를 반환하는 경우 라우팅 서비스는 클라이언트 응용 프로그램에 오류를 반환합니다.  
  
> [!NOTE]
>  오류 처리 기능은 메시지 보내기를 시도할 때와 채널 닫기를 시도할 때 발생하는 예외를 캡처하여 처리합니다. 오류 처리 코드를 검색 하거나;와 통신 하는 응용 프로그램 끝점에서 생성 된 예외 처리 아닙니다. <xref:System.ServiceModel.FaultException> 에 의해 throw으로 라우팅 서비스에서 표시 되는 서비스는 **FaultMessage** 클라이언트로 다시 이동 되 고 있습니다.  
>   
>  라우팅 서비스에서 메시지를 릴레이하려고 할 때 오류가 발생하는 경우 라우팅 서비스가 없을 때 일반적으로 발생하는 <xref:System.ServiceModel.FaultException> 대신 <xref:System.ServiceModel.EndpointNotFoundException>이 클라이언트측에서 발생할 수 있습니다. 따라서 중첩된 예외를 검사하지 않는 한 라우팅 서비스는 예외를 마스킹하고 완전한 투명성을 제공하지 않을 수 있습니다.  
  
### <a name="tracing-exceptions"></a>예외 추적  
 라우팅 서비스는 결과 예외 데이터를 추적 및 메시지 속성으로 예외 정보를 연결 실패 하는 목록에 끝점에 메시지를 보낼 때 **예외**합니다. 이 속성은 예외 데이터를 보존하며 사용자가 메시지 검사자를 통해 프로그래밍 방식으로 액세스하도록 허용합니다.  예외 데이터는 메시지를 보내려고 시도할 때 발생하는 예외 정보에 끝점 이름을 매핑하는 사전에 메시지별로 저장됩니다.  
  
### <a name="backup-endpoints"></a>백업 끝점  
 필터 테이블 내의 각 필터 항목은 기본 끝점으로 보낼 때 전송 오류가 발생하는 경우 사용되는 백업 끝점 목록을 선택적으로 지정할 수 있습니다. 이러한 오류가 발생하는 경우 라우팅 서비스는 백업 끝점 목록의 첫 번째 항목으로 메시지를 전송하려고 시도합니다. 이 시도에서도 전송 오류가 발생하면 백업 목록의 다음 끝점에 대해 전송을 시도합니다. 라우팅 서비스는 메시지가 성공적으로 수신되거나 모든 끝점이 전송 오류를 반환하거나 끝점에서 전송 오류 이외의 오류를 반환할 때까지 목록의 각 끝점으로 계속 메시지를 보냅니다.  
  
 다음 예제에서는 백업 목록을 사용하도록 라우팅 서비스를 구성합니다.  
  
```xml  
<routing>  
  <filters>  
    <!-- Create a MatchAll filter that catches all messages -->  
    <filter name="MatchAllFilter1" filterType="MatchAll" />  
  </filters>  
  <filterTables>  
    <!-- Set up the Routing Service's Message Filter Table -->  
    <filterTable name="filterTable1">  
        <!-- Add an entry that maps the MatchAllMessageFilter to the dead destination -->  
        <!-- If that endpoint is down, tell the Routing Service to try the endpoints -->  
        <!-- Listed in the backupEndpointList -->  
        <add filterName="MatchAllFilter1" endpointName="deadDestination" backupList="backupEndpointList"/>  
    </filterTable>  
  </filterTables>  
  <!-- Create the backup endpoint list -->  
  <backupLists>  
    <!-- Add an endpoint list that contains the backup destinations -->  
    <backupList name="backupEndpointList">  
      <add endpointName="realDestination" />  
      <add endpointName="backupDestination" />  
    </backupList>  
  </backupLists>  
</routing>  
```  
  
```csharp  
//create the endpoint list that contains the service endpoints we want to route to  
List<ServiceEndpoint> backupList = new List<ServiceEndpoint>();  
//add the endpoints in the order that the Routing Service should contact them  
//first add the endpoint that we know is down  
//clearly, normally you wouldn't know that this endpoint was down by default  
backupList.Add(fakeDestination);  
//then add the real Destination endpoint  
//the Routing Service attempts to send to this endpoint only if it   
//encounters a TimeOutException or CommunicationException when sending  
//to the previous endpoint in the list.  
backupList.Add(realDestination);  
//add the backupDestination endpoint  
//the Routing Service attempts to send to this endpoint only if it  
//encounters a TimeOutException or CommunicationsException when sending  
//to the previous endpoints in the list  
backupList.Add(backupDestination);  
//create the default RoutingConfiguration option              
RoutingConfiguration rc = new RoutingConfiguration();  
//add a MatchAll filter to the Routing Configuration's filter table  
//map it to the list of endpoints defined above  
//when a message matches this filter, it is sent to the endpoints in the list in order  
//if an endpoint is down or does not respond (which the first endpoint won't  
//since the client does not exist), the Routing Service automatically moves the message  
//to the next endpoint in the list and try again.  
rc.FilterTable.Add(new MatchAllMessageFilter(), backupList);  
```  
  
### <a name="supported-error-patterns"></a>지원되는 오류 패턴  
 다음 표에서는 백업 끝점 목록 사용과 호환되는 패턴에 대해 설명하고 특정 패턴에 대한 오류 처리의 세부 정보를 설명하는 참고 사항을 제공합니다.  
  
|패턴|세션|트랜잭션|받기 컨텍스트|백업 목록 지원|참고|  
|-------------|-------------|-----------------|---------------------|---------------------------|-----------|  
|단방향||||예|백업 끝점에 메시지를 다시 보내려고 시도합니다. 이 메시지가 멀티캐스트되는 경우 실패한 채널의 메시지만 백업 대상으로 이동됩니다.|  
|단방향||![확인 표시](../../../../docs/framework/wcf/feature-details/media/checkmark.gif "확인 표시")||아니요|예외가 throw되고 트랜잭션이 롤백됩니다.|  
|단방향|||![확인 표시](../../../../docs/framework/wcf/feature-details/media/checkmark.gif "확인 표시")|예|백업 끝점에 메시지를 다시 보내려고 시도합니다. 메시지가 성공적으로 수신된 후 모든 받기 컨텍스트를 완료합니다. 메시지가 성공적으로 수신된 끝점이 없는 경우 받기 컨텍스트를 완료하지 마세요.<br /><br /> 이 메시지가 멀티캐스트되는 경우 받기 컨텍스트는 메시지가 최소 하나의 끝점(기본 또는 백업)에 성공적으로 수신된 경우에만 완료됩니다. 모든 멀티캐스트 경로의 어떠한 끝점에서도 메시지를 성공적으로 수신하지 못한 경우 받기 컨텍스트를 완료하지 마세요.|  
|단방향||![확인 표시](../../../../docs/framework/wcf/feature-details/media/checkmark.gif "확인 표시")|![확인 표시](../../../../docs/framework/wcf/feature-details/media/checkmark.gif "확인 표시")|예|이전 트랜잭션을 중단하고 새 트랜잭션을 만들고 모든 메시지를 다시 보냅니다. 오류가 발생한 메시지는 백업 대상으로 전송됩니다.<br /><br /> 모든 전송이 성공한 트랜잭션이 만들어진 후 받기 컨텍스트를 완료하고 트랜잭션을 커밋합니다.|  
|단방향|![확인 표시](../../../../docs/framework/wcf/feature-details/media/checkmark.gif "확인 표시")|||예|백업 끝점에 메시지를 다시 보내려고 시도합니다. 멀티캐스트 시나리오에서는 오류가 발생한 세션 또는 세션 닫기가 실패한 세션의 메시지만 백업 대상으로 다시 전송됩니다.|  
|단방향|![확인 표시](../../../../docs/framework/wcf/feature-details/media/checkmark.gif "확인 표시")|![확인 표시](../../../../docs/framework/wcf/feature-details/media/checkmark.gif "확인 표시")||아니요|예외가 throw되고 트랜잭션이 롤백됩니다.|  
|단방향|![확인 표시](../../../../docs/framework/wcf/feature-details/media/checkmark.gif "확인 표시")||![확인 표시](../../../../docs/framework/wcf/feature-details/media/checkmark.gif "확인 표시")|예|백업 끝점에 메시지를 다시 보내려고 시도합니다. 오류 없이 모든 메시지 보내기가 완료된 후 세션은 더 이상 메시지가 없음을 나타내고 라우팅 서비스는 모든 아웃바운드 세션 채널을 성공적으로 닫고 모든 받기 컨텍스트가 완료되며 인바운드 세션 채널이 닫힙니다.|  
|단방향|![확인 표시](../../../../docs/framework/wcf/feature-details/media/checkmark.gif "확인 표시")|![확인 표시](../../../../docs/framework/wcf/feature-details/media/checkmark.gif "확인 표시")|![확인 표시](../../../../docs/framework/wcf/feature-details/media/checkmark.gif "확인 표시")|예|현재 트랜잭션을 중단하고 새 트랜잭션을 만듭니다. 세션의 모든 이전 메시지를 다시 보냅니다. 모든 메시지가 성공적으로 전송된 트랜잭션이 만들어진 후 세션은 더 이상 메시지가 없음을 나타내고 모든 아웃바운드 세션 채널이 닫히고 트랜잭션과 함께 받기 컨텍스트가 모두 완료되고 인바운드 세션 채널이 닫히고 트랜잭션이 커밋됩니다.<br /><br /> 세션이 멀티캐스트되는 경우 오류가 발생하지 않은 메시지는 이전과 같은 대상으로 다시 전송되고 오류가 발생한 메시지는 백업 대상으로 전송됩니다.|  
|양방향||||예|백업 대상으로 보냅니다.  채널이 응답 메시지를 반환한 후 응답을 원래 클라이언트로 반환합니다.|  
|양방향|![확인 표시](../../../../docs/framework/wcf/feature-details/media/checkmark.gif "확인 표시")|||예|채널의 모든 메시지를 백업 대상으로 보냅니다.  채널이 응답 메시지를 반환한 후 응답을 원래 클라이언트로 반환합니다.|  
|양방향||![확인 표시](../../../../docs/framework/wcf/feature-details/media/checkmark.gif "확인 표시")||아니요|예외가 throw되고 트랜잭션이 롤백됩니다.|  
|양방향|![확인 표시](../../../../docs/framework/wcf/feature-details/media/checkmark.gif "확인 표시")|![확인 표시](../../../../docs/framework/wcf/feature-details/media/checkmark.gif "확인 표시")||아니요|예외가 throw되고 트랜잭션이 롤백됩니다.|  
|이중||||아니요|비-세션 이중 통신은 현재 지원되지 않습니다.|  
|이중|![확인 표시](../../../../docs/framework/wcf/feature-details/media/checkmark.gif "확인 표시")|||예|백업 대상으로 보냅니다.|  
  
## <a name="hosting"></a>호스팅  
 라우팅 서비스는 WCF 서비스로 구현되므로 응용 프로그램 내에서 자체 호스트되거나 IIS 또는 WAS에서 호스트되어야 합니다. 자동 시작 및 수명 주기 관리 기능을 사용하려면 호스팅 환경에서 이러한 기능을 제공하는 IIS, WAS 또는 Windows 서비스 응용 프로그램에서 라우팅 서비스를 호스트하는 것이 좋습니다.  
  
 다음 예제에서는 응용 프로그램에서 라우팅 서비스를 호스트하는 방법을 보여 줍니다.  
  
```csharp  
using (ServiceHost serviceHost =  
                new ServiceHost(typeof(RoutingService)))  
```  
  
 IIS 또는 WAS 내에서 라우팅 서비스를 호스트하려면 서비스 파일(.svc)을 만들거나 서비스의 구성 기반 활성화를 사용해야 합니다. 서비스 파일을 사용하는 경우 Service 매개 변수를 사용하여 <xref:System.ServiceModel.Routing.RoutingService>를 지정해야 합니다. 다음 예제에는 IIS 또는 WAS를 사용하여 라우팅 서비스를 호스트하는 데 사용할 수 있는 샘플 서비스 파일이 포함되어 있습니다.  
  
```  
<%@ ServiceHost Language="C#" Debug="true" Service="System.ServiceModel.Routing.RoutingService,   
     System.ServiceModel.Routing, version=4.0.0.0, Culture=neutral,   
     PublicKeyToken=31bf3856ad364e35" %>  
```  
  
## <a name="routing-service-and-impersonation"></a>라우팅 서비스 및 가장  
 WCF 라우팅 서비스는 메시지 보내기 및 받기 모두에 대해 가장을 사용할 수 있습니다. 가장에 대한 일반적인 모든 Windows 제약 조건이 적용됩니다. 자신의 서비스를 작성할 때 가장을 사용하기 위한 서비스 또는 계정 권한을 설정해야 하는 경우 라우팅 서비스에서 가장을 사용하려면 같은 단계를 수행해야 합니다. 자세한 내용은 참조 [위임 및 가장](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)합니다.  
  
 라우팅 서비스에서 가장을 사용하려면 ASP.NET 호환 모드에서 ASP.NET 가장을 사용하거나 가장을 허용하도록 구성된 Windows 자격 증명을 사용해야 합니다. ASP.NET 호환 모드에 대 한 자세한 내용은 참조 [WCF 서비스 및 ASP.NET](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md)합니다.  
  
> [!WARNING]
>  WCF 라우팅 서비스는 기본 인증의 가장을 지원하지 않습니다.  
  
 라우팅 서비스에서 ASP.NET 가장을 사용하려면 서비스 호스팅 환경에서 ASP.NET 호환 모드를 활성화해야 합니다. 라우팅 서비스는 이미 ASP.NET 호환 모드를 허용하는 것으로 표시되었으며 가장이 자동으로 사용됩니다. 가장은 라우팅 서비스에서 유일하게 지원되는 ASP.NET 통합 사용 방식입니다.  
  
 라우팅 서비스에서 Windows 자격 증명 가장을 사용하려면 자격 증명과 서비스 둘 다를 구성해야 합니다. 클라이언트 자격 증명 개체(<xref:System.ServiceModel.Security.WindowsClientCredential>, <xref:System.ServiceModel.ChannelFactory>에서 액세스)는 가장을 허용하기 위해 반드시 설정해야 하는 <xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A> 속성을 정의합니다. 마지막으로, 서비스에서 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior> 동작을 구성해서 `ImpersonateCallerForAllOperations`를 `true`로 설정해야 합니다. 라우팅 서비스는 이 플래그를 사용하여 가장을 사용하는 메시지를 전달하기 위한 클라이언트를 만들지 여부를 결정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [메시지 필터](../../../../docs/framework/wcf/feature-details/message-filters.md)  
 [라우팅 계약](../../../../docs/framework/wcf/feature-details/routing-contracts.md)  
 [필터 선택](../../../../docs/framework/wcf/feature-details/choosing-a-filter.md)
