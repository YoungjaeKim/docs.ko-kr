---
title: 어떤&#39;Windows Communication Foundation 4.5의 새로운 s
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- WCF [WCF], what's new
- Windows Communication Foundation [WCF], what's new
ms.assetid: 7e93fe73-af93-46b5-9f63-32f761ee40cf
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 091925dd1f505693df0d1eb770bca604cf038667
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/23/2018
---
# <a name="what39s-new-in-windows-communication-foundation-45"></a>어떤&#39;Windows Communication Foundation 4.5의 새로운 s
이 항목에서는 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)]에 새로 추가된 기능에 대해 설명합니다.  
  
## <a name="wcf-simplification-features"></a>WCF 단순화 기능  
 WCF 4.5 응용 프로그램을 더 쉽게 개발하고 유지할 수 있도록 많은 작업이 이루어졌습니다. [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [WCF 단순화 기능](../../../docs/framework/wcf/wcf-simplification-features.md)합니다.  
  
### <a name="task-based-async-support"></a>작업 기반 비동기 지원  
 기본적으로 서비스 참조를 추가하면 태스크 반환 비동기 서비스 작업 메서드가 생성됩니다. 이는 동기 및 비동기 메서드에 대해 수행됩니다. 따라서 새로운 작업 기반 비동기 프로그래밍 모델을 사용하여 비동기적으로 서비스 작업을 호출할 수 있습니다. 생성된 프록시 메서드를 호출하면 WCF는 비동기 작업을 나타내는 작업 개체를 생성하고 해당 작업를 사용자에게 반환합니다. 작업이 완료 되는 작업을 완료 합니다.  비동기 작업을 구현 하는 경우에 작업 기반 비동기 작업으로 구현할 수 있습니다. 자세한 내용은 참조 하십시오 [동기 및 비동기 작업](../../../docs/framework/wcf/synchronous-and-asynchronous-operations.md)합니다.  
  
### <a name="simplified-generated-configuration-files"></a>단순화되어 생성된 구성 파일  
 Visual Studio에 서비스 참조를 추가하거나 SvcUtil.exe 도구를 사용하면 클라이언트 구성 파일이 생성됩니다. 이전 버전의 WCF에서는 바인딩 속성 값이 기본값인 경우를 포함하여 모든 바인딩 속성 값이 이러한 구성 파일에 포함되었습니다. WCF 4.5에서는 생성된 구성 파일에 기본값이 아닌 값으로 설정된 바인딩 속성만 포함됩니다.  
  
 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [WCF 단순화 기능](../../../docs/framework/wcf/wcf-simplification-features.md)  
  
### <a name="contract-first-development"></a>계약 중심 개발  
 WCF는 이제 계약 중심 개발을 지원합니다. svcutl.exe에는 WSDL 문서에서 서비스 및 데이터 계약을 생성하는 데 사용할 수 있는 /serviceContract 스위치가 있습니다.  
  
### <a name="add-service-reference-from-a-portable-subset-project"></a>이식 가능한 하위 집합 프로젝트의 서비스 참조 추가  
 이식 가능한 하위 집합 프로젝트를 사용하면 복수 .NET 플랫폼(데스크톱, Silverlight, Windows Phone, XBOX)을 지원하면서 .NET 어셈블리 프로그래머가 하나의 소스 트리를 유지하고 시스템을 빌드할 수 있습니다. 이식 가능한 하위 집합 프로젝트는 모든.NET 플랫폼에 사용할 수 있는.NET framework 어셈블리인.NET 이식 가능한 라이브러리만 참조 합니다. 개발자 환경은 다른 WCF 클라이언트 응용 프로그램에 서비스 참조를 추가하는 것과 동일합니다. [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [이식 가능한 하위 집합 프로젝트에서 서비스 참조 추가](../../../docs/framework/wcf/add-service-reference-in-a-portable-subset-project.md)합니다.  
  
### <a name="aspnet-compatibility-mode-default-changed"></a>ASP.NET 호환 모드 기본값 변경  
 WCF는 개발자가 WCF 서비스를 작성할 때 ASP.NET HTTP 파이프라인 기능에 완전하게 액세스할 수 있게 해 주는 ASP.NET 호환 모드를 제공합니다. 이 모드를 사용 하려면 설정 해야 합니다는 `aspNetCompatibilityEnabled` 특성을 true로는 [ \<serviceHostingEnvironment >](../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md) web.config의 섹션입니다. 또한 이 appDomain의 모든 서비스는 `RequirementsMode`의 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute> 속성이 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.Allowed> 또는 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.Required>로 설정되어야 합니다. 기본적으로 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute> 로 설정 되었습니다 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.Allowed>합니다. [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Windows Communication Foundation의 새로운 소식](../../../docs/framework/wcf/whats-new.md) 및 [WCF 서비스 및 ASP.NET](../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md)합니다.  
  
### <a name="new-transport-default-values"></a>새 전송 기본값  
 구성을 단순화하기 위해 여러 전송 속성의 기본값이 변경되었습니다. [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [WCF 단순화 기능](../../../docs/framework/wcf/wcf-simplification-features.md)합니다.  
  
### <a name="xmldictionaryreaderquotas"></a>XmlDictionaryReaderQuotas  
 <xref:System.Xml.XmlDictionaryReaderQuotas>에는 메시지를 만드는 동안 인코더가 사용하는 메모리의 크기를 제한하는 XML 사전 판독기에 대한 구성 가능 할당량 값이 포함됩니다. 이러한 할당량은 구성 가능하지만, 개발자가 이를 명시적으로 설정해야 할 가능성을 줄이기 위해 기본값이 변경되었습니다. [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [WCF 단순화 기능](../../../docs/framework/wcf/wcf-simplification-features.md)합니다.  
  
### <a name="wcf-configuration-validation"></a>WCF 구성 유효성 검사  
 이제 Visual Studio 내에서 빌드 프로세스의 일부로 WCF 구성 파일에 대해 프로젝트 내에 정의된 특성의 유효성이 검사됩니다. 유효성 검사가 실패할 경우 유효성 검사 오류 또는 경고의 목록이 Visual Studio에 표시됩니다.  
  
### <a name="xml-editor-tooltips"></a>XML 편집기 도구 설명  
 WCF 서비스의 기존 및 새 개발자들이 서비스를 구성하는 데 도움이 되도록 이제 Visual Studio XML 편집기에서 서비스 구성 파일에 포함된 모든 구성 요소 및 해당 속성에 대한 도구 설명을 제공합니다.  
  
## <a name="streaming-improvements"></a>스트리밍 향상  
 수신 측이 읽고 있지 않거나 느리게 읽고 있을 때 전송 측이 스레드를 차단하지 않는 진정한 의미의 비동기 스트리밍을 추가 지원하여 확장성을 향상시켰습니다. 클라이언트가 스트리밍된 메시지를 IIS에서 호스팅된 WCF 서비스에 전송할 때 메시지 버퍼링 제한을 제거하였습니다. [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [WCF 단순화 기능](../../../docs/framework/wcf/wcf-simplification-features.md)합니다.  
  
## <a name="simplifying-exposing-an-endpoint-over-https-with-iis"></a>IIS를 사용하여 HTTPS에 끝점 노출 단순화  
 HTTPS에서 끝점 노출을 단순화하기 위해 HTTPS 프로토콜 매핑이 추가되었습니다. HTTPS 끝점을 활성화하려면 웹 사이트에 HTTPS 바인딩 및 SSL 인증서가 구성되어 있는지 확인하고 서비스를 호스팅하는 가상 디렉터리에 HTTPS를 사용하도록 설정하기만 하면 됩니다. 서비스에 메타데이터가 활성화되어 있으면 메타데이터도 HTTPS에 노출됩니다.  
  
## <a name="generating-a-single-wsdl-document"></a>단일 WSDL 문서 생성  
 일부 타사 WSDL 처리 스택은 xsd:import를 통해 다른 문서에 종속된 WSDL 문서를 처리할 수 없습니다.  WCF에서는 이제 모든 WSDL 정보가 단일 문서로 반환되도록 지정할 수 있습니다. 추가 하는 단일 WSDL 문서를 요청 하려면 "? singleWSDL"을 서비스에서 메타 데이터를 요청할 때 URI입니다.  
  
## <a name="websocket-support"></a>WebSocket 지원  
 WebSocket은 TCP와 유사한 성능 특성으로 포트 80 및 443에서 진정한 의미의 양방향 통신을 제공하는 기술입니다. WebSocket 전송에서 통신을 지원하기 위해 <xref:System.ServiceModel.NetHttpBinding>와 <xref:System.ServiceModel.NetHttpsBinding>을 참조하세요. 자세한 내용은 참조: [시스템 제공 바인딩](../../../docs/framework/wcf/system-provided-bindings.md)합니다.  
  
## <a name="new-transport-default-values"></a>새 전송 기본값  
 다음 표에는 변경된 설정과 추가 정보를 찾을 수 있는 위치가 나와 있습니다.  
  
|속성|켜기|새 기본값|추가 정보|  
|--------------|--------|-----------------|------------------------------|  
|channelInitializationTimeout|<xref:System.ServiceModel.NetTcpBinding>|30초|<xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement.ChannelInitializationTimeout%2A>|  
|listenBacklog|<xref:System.ServiceModel.NetTcpBinding>|12 * 프로세서 수|<xref:System.ServiceModel.NetTcpBinding.ListenBacklog%2A>|  
|maxPendingAccepts|ConnectionOrientedTransportBindingElement<br /><br /> SMSvcHost.exe|2 * 전송용 프로세서 수<br /><br /> 4 \* SMSvcHost.exe 용 프로세서 수|<xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement.MaxPendingAccepts%2A> [Net.TCP Port Sharing Service를 구성 합니다.](http://msdn.microsoft.com/library/b6dd81fa-68b7-4e1b-868e-88e5901b7ea0)|  
|maxPendingConnections|ConnectionOrientedTransportBindingElement|12 * 프로세서 수|<xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement.MaxPendingConnections%2A>|  
|receiveTimeout|SMSvcHost.exe|30초|[Net.TCP Port Sharing Service 구성](http://msdn.microsoft.com/library/b6dd81fa-68b7-4e1b-868e-88e5901b7ea0)|  
  
## <a name="xml-editor-tooltips"></a>XML 편집기 도구 설명  
 WCF 서비스의 기존 및 새 개발자들이 서비스를 구성하는 데 도움이 되도록 이제 Visual Studio XML 편집기에서 서비스 구성 파일에 포함된 모든 구성 요소 및 해당 속성에 대한 도구 설명을 제공합니다.  
  
## <a name="configuring-wcf-services-in-code"></a>코드로 WCF 서비스 구성  
 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)]에서는 개발자가 구성 파일 또는 코드를 사용하여 서비스를 구성할 수 있습니다.  구성 파일은 배포 후 서비스를 구성해야 하는 경우에 유용합니다. 구성 파일을 사용할 경우 IT 전문가가 구성 파일을 업데이트하기만 하면 되고 다시 컴파일할 필요가 없습니다. 하지만 구성 파일은 관리하기가 복잡하고 어려울 수 있습니다. 구성 파일 디버깅은 지원되지 않으며 구성 요소는 이름으로 참조되므로 구성 파일을 작성하기가 어렵고 오류가 발생하기 쉽습니다. [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]에서는 서비스를 코드로 구성할 수도 있습니다. 이전 버전 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)](4.0 이하)의 경우 자체 호스팅 시나리오에서 코드로 서비스를 구성하기가 쉬웠으며 <xref:System.ServiceModel.ServiceHost> 클래스를 사용하여 ServiceHost.Open을 호출하기 전에 끝점 및 동작을 구성할 수 있었습니다. 그러나 웹 호스팅 시나리오에서는 <xref:System.ServiceModel.ServiceHost> 클래스에 액세스할 수 없습니다. 웹 호스팅 서비스를 구성하려면 `System.ServiceModel.ServiceHostFactory`를 만들고 필요한 구성을 수행하는 <xref:System.ServiceModel.Activation.ServiceHostFactory>를 만들어야 했습니다. .NET 4.5부터 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]는 자체 호스팅 서비스와 웹 호스팅 서비스를 모두 코드로 구성할 수 있는 더욱 손쉬운 방법을 제공합니다. [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [코드로 WCF 서비스를에서 구성](../../../docs/framework/wcf/configuring-wcf-services-in-code.md)합니다.  
  
## <a name="channelfactory-caching"></a>ChannelFactory 캐싱  
 WCF 클라이언트 응용 프로그램에서는 <xref:System.ServiceModel.ChannelFactory%601> 클래스를 사용하여 WCF 서비스와의 통신 채널을 만듭니다.  <xref:System.ServiceModel.ChannelFactory%601> 인스턴스를 만들 때는 다음 작업이 필요하기 때문에 약간의 오버헤드가 발생합니다.  
  
1.  <xref:System.ServiceModel.Description.ContractDescription> 트리 생성  
  
2.  필요한 모든 CLR 형식 반영  
  
3.  채널 스택 생성  
  
4.  리소스 삭제  
  
 이 오버헤드를 최소화하기 위해 사용자가 WCF 클라이언트 프록시를 사용할 때 WCF가 채널 팩터리를 캐시할 수 있습니다. [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [채널 팩터리 및 캐싱](../../../docs/framework/wcf/feature-details/channel-factory-and-caching.md)합니다.  
  
## <a name="compression-and-the-binary-encoder"></a>압축 및 이진 인코더  
 WCF 4.5부터는 WCF 이진 인코더에서 압축을 추가 지원합니다. 압축 형식은 <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement.CompressionFormat%2A> 속성에서 구성합니다. 클라이언트와 서비스 모두 <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement.CompressionFormat%2A> 속성을 구성해야 합니다. HTTP, HTTPS 및 TCP 프로토콜에 대해 압축이 가능합니다. 클라이언트가 압축을 사용하도록 지정하더라도 서비스에서 이를 지원하지 않으면 프로토콜이 일치하지 않는다는 프로토콜 예외가 throw됩니다. [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [메시지 인코더 선택](../../../docs/framework/wcf/feature-details/choosing-a-message-encoder.md)  
  
## <a name="udp"></a>UDP  
 개발자가 "fire and forget"를 사용 하는 서비스를 작성할 수 있도록 UDP 전송에 대 한 지원이 추가 되었습니다 메시징입니다. 클라이언트는 서비스에 메시지를 보내고 서비스에서 응답을 기대하지 않습니다.  
  
## <a name="multiple-authentication-support"></a>다중 인증 지원  
 HTTP 전송 및 전송 보안을 사용할 경우 단일 WCF 끝점에서 IIS의 지원 방식과 같은 복수 인증 모드 지원이 추가되었습니다. IIS에서는 가상 디렉터리에서 복수 인증 모드를 사용할 수 있습니다. 이 기능을 사용하면 단일 WCF 끝점에서 WCF 서비스가 호스팅되는 가상 디렉터리에 대해 복수 인증 모드를 지원할 수 있습니다.  
  
## <a name="idn-support"></a>IDN 지원  
 IDN(Internationalized Domain Name)을 사용하는 WCF 서비스에 대한 지원이 추가되었습니다. 자세한 내용은 참조 [WCF 및 다국어 도메인 이름](../../../docs/framework/wcf/feature-details/wcf-and-internationalized-domain-names.md)합니다.  
  
## <a name="httpclient"></a>HttpClient  
 <xref:System.Net.Http.HttpClient>라는 새 클래스가 추가되어 HTTP 요청 작업을 더 쉽게 수행할 수 있습니다. 자세한 내용은 참조 하십시오. [소셜 및 HTTP 서비스와 연결 된 앱을 만드는](http://go.microsoft.com/fwlink/?LinkId=231886) 및 [HTTP 클라이언트 샘플](http://code.msdn.microsoft.com/windowsapps/HttpClient-sample-55700664)합니다.  
  
## <a name="configuration-intellisense"></a>구성 Intellisense  
 프로젝트에 정의된 사용자 지정 특성의 경우 이제 구성 파일의 특성 값에서 intellisense를 지원하므로 구성 작업을 쉽고 빠르고 정확하게 수행할 수 있습니다.  
  
## <a name="configuration-tooltips"></a>구성 도구 설명  
 이제 XML 편집기에서 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 요소 및 특성에 도구 설명이 표시되므로 요소 또는 특성의 용도를 더 쉽고 정확하게 식별할 수 있습니다.  
  
## <a name="paste-data-as-classes"></a>데이터를 클래스로 붙여넣기  
 WCF 프로젝트에서는 XML에 정의된 데이터 형식(서비스에 노출된 형식 등)을 코드 페이지에 직접 붙여넣을 수 있습니다. XML 형식은 CLR 형식으로 붙여 넣게 됩니다. 참조 [XML에서 데이터 형식 클래스 생성](../../../docs/framework/wcf/generating-data-type-classes-from-xml.md) 내용을 확인 합니다.  
  
## <a name="webservicehost-and-default-endpoints"></a>WebServiceHost 및 기본 끝점  
 Visual Studio 2010에서는 사용자가 끝점을 명시적으로 지정했는지 여부에 상관 없이 WebServiceHost가 기본 끝점을 자동으로 만들었습니다. Visual Studio 2012에서는 끝점이 명시적으로 추가되지 않은 경우에만 WebServiceHost가 기본 끝점을 만듭니다. 클라이언트에 기본 끝점이 필요한 경우에는 끝점을 명시적으로 추가하고 클라이언트를 이 끝점에 연결할 수 있습니다. 또는 응용 프로그램의 구성 파일에 다음 설정을 추가하여 WCF가 이전 동작으로 되돌아가도록 지정할 수도 있습니다.  
  
```xml  
<appSettings>  
    <add key="wcf:webservicehost:enableautomaticendpointscompatability" value="true"/>  
  </appSettings>  
```  
  
## <a name="ihttpcookiecontainermanager"></a>IHttpCookieContainerManager  
 이 인터페이스는 <xref:System.ServiceModel.Channels.IChannelFactory%601>에 의해 노출되며 클라이언트 측의 쿠키 작업을 훨씬 손쉽게 해 줍니다. 바인딩의 AllowCookies가 true로 설정되어 있으면 다음 코드를 사용하여 쿠키에 액세스할 수 있습니다.  
  
```csharp  
IHttpCookieContainerManager cookieManager = factory.GetProperty<IHttpCookieContainerManager>();   
System.Net.CookieContainer container = cookieManager.CookieContainer;  
```  
  
 그런 다음 <xref:System.Net.CookieContainer>에서 쿠키를 검색하거나 설정할 수 있습니다. AllowCookies가 false로 설정되어 있으면 <xref:System.ServiceModel.OperationContext>를 사용하여 쿠키를 수동으로 검색하고, 또 다른 <xref:System.ServiceModel.OperationContext>나 메시지 검사자를 사용하여 다른 요청에서 이 쿠키를 보낼 수 있습니다. IHttpCookieContainerManager 인터페이스를 사용하면 서비스에 사용자를 인증한 후 해당 서비스에서 반환된 인증 쿠키를 사용하여 다른 서비스에 대해 인증을 수행할 수 있습니다.
