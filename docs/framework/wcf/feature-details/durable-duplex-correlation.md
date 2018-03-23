---
title: 영속 이중 상관 관계
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8eb0e49a-6d3b-4f7e-a054-0d4febee2ffb
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: ceb5cbedf30c8ec53bc815f9cd52f7bcb8a6e327
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/23/2018
---
# <a name="durable-duplex-correlation"></a>영속 이중 상관 관계
콜백 상관 관계라고도 하는 영속 이중은 워크플로 서비스를 사용하여 초기 호출자에게 콜백을 보내야 하는 경우에 유용합니다. WCF 이중과 달리 콜백은 나중에 언제든지 발생할 수 있으며 동일한 채널이나 채널 수명과 연결되지 않습니다. 따라서 유일한 요구 사항은 호출자에 콜백 메시지를 수신 대기하는 활성 끝점이 있어야 한다는 점입니다. 그러면 장기 실행 대화에서 워크플로 서비스를 사용하여 통신할 수 있습니다. 이 항목에서는 영속 이중 상관 관계에 대해 간략하게 설명합니다.  
  
## <a name="using-durable-duplex-correlation"></a>영속 이중 상관 관계 사용  
 영속 이중 상관 관계를 사용하려면 두 서비스에서 <xref:System.ServiceModel.NetTcpContextBinding> 또는 <xref:System.ServiceModel.WSHttpContextBinding> 같이 양방향 작업을 지원하는 컨텍스트 사용 바인딩을 사용해야 합니다. 호출하는 서비스는 클라이언트 <xref:System.ServiceModel.WSHttpContextBinding.ClientCallbackAddress%2A>에 원하는 바인딩을 사용하여 <xref:System.ServiceModel.Endpoint>를 등록합니다. 수신하는 서비스는 초기 호출에서 이 데이터를 받은 다음 호출하는 서비스로 콜백하는 <xref:System.ServiceModel.Endpoint> 작업에서 자신의 <xref:System.ServiceModel.Activities.Send>에 이 데이터를 사용합니다. 다음 예제에서는 두 개의 서비스가 서로 통신합니다. 첫 번째 서비스는 두 번째 서비스의 메서드를 호출한 다음 응답을 기다립니다. 두 번째 서비스는 콜백 메서드의 이름을 알고 있지만 디자인 타임에는 이 메서드를 구현하는 서비스의 끝점을 알 수 없습니다.  
  
> [!NOTE]
>  영속 이중은 끝점의 <xref:System.ServiceModel.Channels.AddressingVersion>이 <xref:System.ServiceModel.Channels.AddressingVersion.WSAddressing10%2A>을 사용하여 구성된 경우에만 사용할 수 있습니다. 그렇지 않을 경우 아니라면 <xref:System.InvalidOperationException> 다음 메시지와 함께 예외가: "메시지에 AddressingVersion에 대 한 끝점 참조를 사용 하는 콜백 컨텍스트 헤더가 포함 되어 ' Addressing200408 (HYPERLINK"http://schemas.xmlsoap.org/ws/2004/08/addressing" http://schemas.xmlsoap.org/ws/2004/08/addressing)'. 콜백 컨텍스트는 AddressingVersion이 'WSAddressing10'으로 구성되어 있을 경우에만 전송할 수 있습니다."라는 메시지가 표시됩니다.  
  
 다음 예제에서는 <xref:System.ServiceModel.Endpoint>을 사용하여 콜백 <xref:System.ServiceModel.WSHttpContextBinding>를 만드는 워크플로 서비스를 호스팅합니다.  
  
```csharp  
// Host WF Service 1.  
string baseAddress1 = "http://localhost:8080/Service1";  
WorkflowServiceHost host1 = new WorkflowServiceHost(GetWF1(), new Uri(baseAddress1));  
  
// Add the callback endpoint.  
WSHttpContextBinding Binding1 = new WSHttpContextBinding();  
host1.AddServiceEndpoint("ICallbackItemsReady", Binding1, "ItemsReady");  
  
// Add the service endpoint.  
host1.AddServiceEndpoint("IService1", Binding1, baseAddress1);  
  
// Open the first workflow service.  
host1.Open();  
Console.WriteLine("Service1 waiting at: {0}", baseAddress1);  
```  
  
 이 워크플로 서비스를 구현하는 워크플로는 해당 <xref:System.ServiceModel.Activities.Send> 작업을 사용하여 콜백 상관 관계를 초기화하고 <xref:System.ServiceModel.Activities.Receive>와 연결되는 <xref:System.ServiceModel.Activities.Send> 작업의 콜백 끝점을 참조합니다. 다음 예제에서는 `GetWF1` 메서드에서 반환되는 워크플로를 나타냅니다.  
  
```csharp  
Variable<CorrelationHandle> CallbackHandle = new Variable<CorrelationHandle>();  
  
Receive StartOrder = new Receive  
{  
    CanCreateInstance = true,  
    ServiceContractName = "IService1",  
    OperationName = "StartOrder"  
};  
  
Send GetItems = new Send  
{  
    CorrelationInitializers =   
    {  
        new CallbackCorrelationInitializer  
        {  
            CorrelationHandle = CallbackHandle  
        }  
    },  
    ServiceContractName = "IService2",  
    OperationName = "StartItems",  
    Endpoint = new Endpoint  
    {  
        AddressUri = new Uri("http://localhost:8081/Service2"),  
        Binding = new WSHttpContextBinding  
        {  
            ClientCallbackAddress = new Uri("http://localhost:8080/Service1/ItemsReady")                          
        }  
    }  
};  
  
Receive ItemsReady = new Receive  
{  
    ServiceContractName = "ICallbackItemsReady",  
    OperationName = "ItemsReady",  
    CorrelatesWith = CallbackHandle,  
};  
  
Activity wf = new Sequence  
{  
    Variables =  
    {  
        CallbackHandle  
    },  
    Activities =  
    {  
        StartOrder,  
        new WriteLine  
        {  
            Text = "WF1 - Started"  
        },  
        GetItems,  
        new WriteLine  
        {  
            Text = "WF1 - Request Submitted"  
        },  
        ItemsReady,  
        new WriteLine  
        {  
            Text = "WF1 - Items Received"  
        }  
     }  
};  
```  
  
 두 번째 워크플로 서비스는 시스템 제공 컨텍스트 기반 바인딩을 사용하여 호스팅됩니다.  
  
```csharp  
// Host WF Service 2.  
string baseAddress2 = "http://localhost:8081/Service2";  
WorkflowServiceHost host2 = new WorkflowServiceHost(GetWF2(), new Uri(baseAddress2));  
  
// Add the service endpoint.  
WSHttpContextBinding Binding2 = new WSHttpContextBinding();  
host2.AddServiceEndpoint("IService2", Binding2, baseAddress2);  
  
// Open the second workflow service.  
host2.Open();  
Console.WriteLine("Service2 waiting at: {0}", baseAddress2);  
```  
  
 이 워크플로 서비스를 구현하는 워크플로는 <xref:System.ServiceModel.Activities.Receive> 작업으로 시작합니다. 이 받기 작업은 이 서비스의 콜백 상관 관계를 초기화하고 장기 실행 작업을 시뮬레이션하는 동안 대기한 다음 초기 호출에서 서비스에 전달된 콜백 컨텍스트를 사용하여 첫 번째 서비스로 콜백합니다. 다음 예제에서는 호출에서 `GetWF2`로 반환되는 워크플로를 나타냅니다. <xref:System.ServiceModel.Activities.Send> 작업에는 `http://www.contoso.com`의 자리 표시자 주소가 있으므로 런타임에 사용되는 실제 주소는 제공된 콜백 주소입니다.  
  
```csharp  
Variable<CorrelationHandle> ItemsCallbackHandle = new Variable<CorrelationHandle>();  
  
Receive StartItems = new Receive  
{  
    CorrelationInitializers =   
    {  
        new CallbackCorrelationInitializer  
        {  
            CorrelationHandle = ItemsCallbackHandle  
        }  
    },  
    CanCreateInstance = true,  
    ServiceContractName = "IService2",  
    OperationName = "StartItems"  
};  
  
Send ItemsReady = new Send  
{  
    CorrelatesWith = ItemsCallbackHandle,  
    Endpoint = new Endpoint  
    {  
        // The callback address on the binding is used  
        // instead of this placeholder address.  
        AddressUri = new Uri("http://www.contoso.com"),  
  
        Binding = new WSHttpContextBinding()  
    },  
    OperationName = "ItemsReady",  
    ServiceContractName = "ICallbackItemsReady"  
};  
  
Activity wf = new Sequence  
{  
    Variables =  
    {  
        ItemsCallbackHandle  
    },  
    Activities =  
    {  
        StartItems,  
        new WriteLine  
        {  
            Text = "WF2 - Request Received"  
        },  
        new Delay  
        {  
            Duration = TimeSpan.FromMinutes(90)  
        },  
        new WriteLine  
        {  
            Text = "WF2 - Sending items"  
        },  
        ItemsReady,  
        new WriteLine  
        {  
            Text = "WF2 - Items sent"  
        }  
     }  
};  
```  
  
 첫 번째 워크플로에서 `StartOrder` 메서드가 호출되면 두 워크플로를 통해 실행 흐름을 보여 주는 다음 출력이 표시됩니다.  
  
```Output  
Service1 waiting at: http://localhost:8080/Service1  
Service2 waiting at: http://localhost:8081/Service2  
Press enter to exit.   
WF1 - Started  
WF2 - Request Received  
WF1 - Request Submitted  
WF2 - Sending items  
WF2 - Items sent  
WF1 - Items Received  
```  
  
 이 예제에서는 두 워크플로에서 <xref:System.ServiceModel.Activities.CallbackCorrelationInitializer>를 사용하여 상관 관계를 명시적으로 관리합니다. 이러한 샘플 워크플로에는 하나의 상관 관계만 있으므로 기본 <xref:System.ServiceModel.Activities.CorrelationHandle> 관계만으로 충분할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [영 속 이중 &#91;WF 샘플&#93;](../../../../docs/framework/windows-workflow-foundation/samples/durable-duplex.md)
