---
title: "서비스 런타임 동작 지정"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
ms.assetid: 5c5450ea-6af1-4b75-a267-613d0ac54707
caps.latest.revision: "12"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: c2c1534b161f81fa90dce52c825b0417dc8fd35d
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/22/2017
---
# <a name="specifying-service-run-time-behavior"></a>서비스 런타임 동작 지정
서비스 계약을 디자인([Designing Service Contracts](../../../docs/framework/wcf/designing-service-contracts.md)) 서비스 계약을 구현([Implementing Service Contracts](../../../docs/framework/wcf/implementing-service-contracts.md))했으면 서비스 런타임의 작업 동작을 구성할 수 있습니다. 이 항목에서는 시스템 제공 서비스와 작업 동작에 대해 설명하고, 새 동작을 만들기 위해 추가 정보를 찾을 수 있는 위치에 대해 설명합니다. 일부 동작은 특성으로 적용되지만 대부분은 응용 프로그램 구성 파일을 사용하여 적용되거나 프로그래밍 방식으로 적용됩니다. [!INCLUDE[crabout](../../../includes/crabout-md.md)] 는 [Configuring Services](../../../docs/framework/wcf/configuring-services.md)를 참조하세요.  
  
## <a name="overview"></a>개요  
 계약은 해당 형식의 서비스 입력, 출력, 데이터 형식 및 기능을 정의합니다. 서비스 계약을 구현하면 주소에서 바인딩으로 구성된 경우 구현한 계약을 이행하는 클래스가 만들어집니다. 클라이언트에서는 계약, 바인딩 및 주소 정보를 모두 알고 있습니다. 이러한 정보가 없으면 클라이언트는 서비스를 사용할 수 없습니다.  
  
 그러나 스레딩 문제 또는 인스턴스 관리와 같은 특정 작업은 클라이언트에 불분명합니다. 서비스 계약을 구현한 경우에는 *동작*을 사용하여 여러 개의 작업 특징을 구성할 수 있습니다. 동작은 런타임 속성을 설정하거나 사용자 지정 형식을 런타임에 삽입하여 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 런타임을 수정하는 개체입니다. [!INCLUDE[crabout](../../../includes/crabout-md.md)] 는 [Extending ServiceHost and the Service Model Layer](../../../docs/framework/wcf/extending/extending-servicehost-and-the-service-model-layer.md)를 참조하세요.  
  
 <xref:System.ServiceModel.ServiceBehaviorAttribute?displayProperty=nameWithType> 및 <xref:System.ServiceModel.OperationBehaviorAttribute?displayProperty=nameWithType> 특성은 가장 널리 쓰이는 유용한 동작이며, 가장 일반적으로 요청되는 작업 기능을 노출합니다. 이들은 특성이기 때문에 서비스 또는 작업 구현에 적용합니다. <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=nameWithType> 또는 <xref:System.ServiceModel.Description.ServiceDebugBehavior?displayProperty=nameWithType> 등의 다른 동작은 프로그래밍 방식으로 사용될 수 있긴 하지만 일반적으로 응용 프로그램 구성 파일을 사용하여 적용됩니다.  
  
 이 항목에서는 <xref:System.ServiceModel.ServiceBehaviorAttribute> 및 <xref:System.ServiceModel.OperationBehaviorAttribute> 특성에 대해 간략하게 설명하고, 동작이 작동할 수 있는 여러 범위에 대해 설명하고, [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 개발자에게 유용할 수 있는 여러 범위의 다양한 시스템 제공 동작에 대해 짧게 설명합니다.  
  
## <a name="servicebehaviorattribute-and-operationbehaviorattribute"></a>ServiceBehaviorAttribute 및 OperationBehaviorAttribute  
 가장 중요한 동작은 다음을 제어할 때 사용할 수 있는 <xref:System.ServiceModel.ServiceBehaviorAttribute> 및 <xref:System.ServiceModel.OperationBehaviorAttribute> 특성입니다.  
  
-   인스턴스 수명  
  
-   동시성 및 동기화 지원  
  
-   구성 동작  
  
-   트랜잭션 동작  
  
-   Serialization 동작  
  
-   메타데이터 변환  
  
-   세션 수명  
  
-   주소 필터링 및 헤더 처리  
  
-   가장  
  
-   이러한 특성을 사용하려면 서비스 또는 작업 구현에 해당 범주에 적합한 특성을 표시하고 속성을 설정합니다. 예를 들어 다음 코드 예제에서는 이 작업 호출자가 가장을 지원하기 위해 <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A?displayProperty=nameWithType> 속성을 사용하는 작업 구현을 보여 줍니다.  
  
 [!code-csharp[OperationBehaviorAttribute_Impersonation#1](../../../samples/snippets/csharp/VS_Snippets_CFX/operationbehaviorattribute_impersonation/cs/services.cs#1)]
 [!code-vb[OperationBehaviorAttribute_Impersonation#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/operationbehaviorattribute_impersonation/vb/services.vb#1)]  
  
 대부분의 속성에 바인딩의 추가 지원이 필요합니다. 예를 들어 클라이언트의 트랜잭션이 필요한 작업은 이동한 트랜잭션을 지원하는 바인딩을 사용하도록 구성해야 합니다.  
  
### <a name="well-known-singleton-services"></a>잘 알려진 singleton 서비스  
 <xref:System.ServiceModel.ServiceBehaviorAttribute> 및 <xref:System.ServiceModel.OperationBehaviorAttribute> 특성을 사용하여 <xref:System.ServiceModel.InstanceContext> 와 작업을 구현하는 서비스 개체의 특정 수명을 제어할 수 있습니다.  
  
 예를 들어 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=nameWithType> 속성은 <xref:System.ServiceModel.InstanceContext>가 해제되는 빈도를 제어하고, <xref:System.ServiceModel.OperationBehaviorAttribute.ReleaseInstanceMode%2A?displayProperty=nameWithType> 및 <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A?displayProperty=nameWithType> 속성은 서비스 개체가 해제되는 시점을 제어합니다.  
  
 그러나 서비스 개체를 직접 만들고, 해당 개체를 사용하여 서비스 호스트를 만들 수도 있습니다. 이렇게 하려면 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=nameWithType> 속성도 <xref:System.ServiceModel.InstanceContextMode.Single>로 설정해야 하며, 그렇지 않으면 서비스 호스트를 열 때 예외가 throw됩니다.  
  
 <xref:System.ServiceModel.ServiceHost.%23ctor%28System.Object%2CSystem.Uri%5B%5D%29?displayProperty=nameWithType> 생성자를 사용하여 이러한 서비스를 만듭니다. singleton 서비스에서 사용할 특정 개체 인스턴스를 제공하려면 사용자 지정 <xref:System.ServiceModel.Dispatcher.IInstanceContextInitializer?displayProperty=nameWithType>를 구현하는 대신 제공합니다. 예를 들어 매개 변수가 없는 기본 public 생성자를 구현하지 않는 경우와 같이 서비스 구현 형식을 생성하기 어려운 경우 이 오버로드를 사용할 수 있습니다.  
  
 이 생성자에 개체가 제공되면 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 인스턴스 만들기 동작과 관련된 일부 기능이 다르게 작동합니다. 예를 들어 잘 알려진 개체 인스턴스를 제공하는 경우 <xref:System.ServiceModel.InstanceContext.ReleaseServiceInstance%2A?displayProperty=nameWithType> 호출은 아무런 효과가 없습니다. 마찬가지로 다른 인스턴스 해제 메커니즘도 무시됩니다. <xref:System.ServiceModel.ServiceHost> 클래스는 항상 모든 작업에 대해 <xref:System.ServiceModel.OperationBehaviorAttribute.ReleaseInstanceMode%2A?displayProperty=nameWithType> 속성이 <xref:System.ServiceModel.ReleaseInstanceMode.None?displayProperty=nameWithType>으로 설정된 것처럼 동작합니다.  
  
## <a name="other-service-endpoint-contract-and-operation-behaviors"></a>기타 서비스, 끝점, 계약 및 작업 동작  
 <xref:System.ServiceModel.ServiceBehaviorAttribute> 특성과 같은 서비스 동작은 전체 서비스에서 작동합니다. 예를 들어 <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A?displayProperty=nameWithType> 속성을 <xref:System.ServiceModel.ConcurrencyMode.Multiple?displayProperty=nameWithType>로 설정하는 경우 해당 서비스의 각 작업 내에서 스레드 동기화 문제를 직접 처리해야 합니다. 끝점 동작은 끝점에서 작동합니다. 대부분의 시스템 제공 끝점 동작은 클라이언트 기능에 대한 것입니다. 계약 동작은 계약 수준에서 작동하고 작업 동작은 작업 배달을 수정합니다.  
  
 이러한 동작은 대부분 특성에서 구현되므로 <xref:System.ServiceModel.ServiceBehaviorAttribute> 및 <xref:System.ServiceModel.OperationBehaviorAttribute> 특성을 사용할 때 이러한 동작을 사용합니다. 이렇게 하려면 적합한 서비스 클래스 또는 작업 구현에 해당 동작을 적용하면 됩니다. <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 또는 <xref:System.ServiceModel.Description.ServiceDebugBehavior> 개체 등의 다른 동작은 프로그래밍 방식으로 사용될 수 있긴 하지만 일반적으로 응용 프로그램 구성 파일을 사용하여 적용됩니다.  
  
 예를 들어 메타데이터 게시는 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 개체를 사용하여 구성됩니다. 다음 응용 프로그램 구성 파일은 가장 일반적인 사용 방법을 보여 줍니다.  
  
 [!code-csharp[ServiceMetadataBehavior#1](../../../samples/snippets/csharp/VS_Snippets_CFX/servicemetadatabehavior/cs/hostapplication.cs#1)]  
  
 다음 단원에서는 서비스 또는 클라이언트의 런타임 배달을 수정할 때 사용할 수 있는 여러 개의 가장 유용한 시스템 제공 동작에 대해 설명합니다. 참조 항목을 참조하여 각 동작의 사용 방법을 결정합니다.  
  
### <a name="service-behaviors"></a>서비스 동작  
 다음 동작은 서비스에서 작동합니다.  
  
-   <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute>. 해당 서비스를 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 호환 모드로 실행할 수 있는지 여부를 나타내기 위해 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 서비스에 적용됩니다.  
  
-   <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>. 서비스가 클라이언트 클레임에 권한을 부여하는 방식을 제어합니다.  
  
-   <xref:System.ServiceModel.Description.ServiceCredentials>. 이 클래스는 서비스 자격 증명을 구성합니다. 이 클래스를 사용하여 서비스에 대한 자격 증명(예: X.509 인증서)을 지정합니다.  
  
-   <xref:System.ServiceModel.Description.ServiceDebugBehavior>. [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 서비스에 대한 디버깅 및 도움말 정보 기능을 사용합니다.  
  
-   <xref:System.ServiceModel.Description.ServiceMetadataBehavior>. 서비스 메타데이터 및 관련 정보의 게시를 제어합니다.  
  
-   <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>. 보안 이벤트의 감사 동작을 지정합니다.  
  
-   <xref:System.ServiceModel.Description.ServiceThrottlingBehavior>. 서비스 성능을 조정할 수 있는 런타임 처리량 설정을 구성합니다.  
  
### <a name="endpoint-behaviors"></a>끝점 동작  
 다음 동작은 끝점에서 작동합니다. 이러한 동작은 대부분 클라이언트 응용 프로그램에서 사용됩니다.  
  
-   <xref:System.ServiceModel.CallbackBehaviorAttribute>. 이중 클라이언트 응용 프로그램에서 콜백 서비스 구현을 구성합니다.  
  
-   <xref:System.ServiceModel.Description.CallbackDebugBehavior>. [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 콜백 개체에 대해 서비스 디버깅을 사용하도록 설정합니다.  
  
-   <xref:System.ServiceModel.Description.ClientCredentials>. 사용자가 클라이언트와 서비스 자격 증명 및 클라이언트에서 사용할 서비스 자격 증명 인증 설정을 구성할 수 있습니다.  
  
-   <xref:System.ServiceModel.Description.ClientViaBehavior>. 전송 채널을 만들어야 하는 URI(Uniform Resource Identifier)를 지정하기 위해 클라이언트에서 사용합니다.  
  
-   <xref:System.ServiceModel.Description.MustUnderstandBehavior>. [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 처리를 사용하지 않도록 `MustUnderstand` 에 지시합니다.  
  
-   <xref:System.ServiceModel.Description.SynchronousReceiveBehavior>. 런타임에 채널에 대한 동기 수신 프로세스를 사용하도록 지시합니다.  
  
-   <xref:System.ServiceModel.Description.TransactedBatchingBehavior>. 트랜잭션 수신을 지원하는 전송에 대해 받기 작업을 최적화합니다.  
  
### <a name="contract-behaviors"></a>계약 동작  
 <xref:System.ServiceModel.DeliveryRequirementsAttribute>. 바인딩이 서비스 또는 클라이언트 구현에 제공해야 하는 기능 요구 사항을 지정합니다.  
  
### <a name="operation-behaviors"></a>작업 동작  
 다음 작업 동작은 작업에 대한 serialization 및 트랜잭션 제어를 지정합니다.  
  
-   <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>. <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType>의 런타임 동작을 나타냅니다.  
  
-   <xref:System.ServiceModel.Description.XmlSerializerOperationBehavior>. `XmlSerializer` 의 런타임 동작을 제어하고 해당 동작을 작업과 연결합니다.  
  
-   <xref:System.ServiceModel.TransactionFlowAttribute>. 서비스 작업에서 트랜잭션 헤더를 허용하는 수준을 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [서비스 구성](../../../docs/framework/wcf/configuring-services.md)  
 [방법: 서비스 인스턴스 만들기 제어](../../../docs/framework/wcf/feature-details/how-to-control-service-instancing.md)
