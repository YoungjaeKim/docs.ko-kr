---
title: 바인딩 및 보안
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
- bindings [WCF], security
- WCF security
- Windows Communication Foundation, security
- bindings [WCF]
ms.assetid: 4de03dd3-968a-4e65-af43-516e903d7f95
caps.latest.revision: ''
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.workload:
- dotnet
ms.openlocfilehash: 9e44db963a696f22f91569eb3d7c2956289a9c76
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="bindings-and-security"></a>바인딩 및 보안
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]에 포함된 시스템 제공 바인딩은 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 응용 프로그램을 신속하게 프로그래밍하기 위한 방법을 제공합니다. 한 가지 예외를 통해 모든 바인딩의 기본 보안 스키마가 활성화됩니다. 이 항목은 보안 요구 사항에 적합한 바인딩을 선택하는 데 도움을 줍니다.  
  
 에 대 한 개요 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 보안 참조 [보안 개요](../../../../docs/framework/wcf/feature-details/security-overview.md)합니다. [!INCLUDE[crabout](../../../../includes/crabout-md.md)] 프로그래밍 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 바인딩을 사용 하 여, 참조 [WCF 보안 프로그래밍](../../../../docs/framework/wcf/feature-details/programming-wcf-security.md)합니다.  
  
 연결에서 보안 된 런타임 동작에 대 한 자세한 내용을 확인할 수 이미 바인딩을 선택 하는 경우 [보안 동작](../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)합니다.  
  
 일부 보안 기능은 시스템 제공 바인딩을 사용하여 프로그래밍할 수 없습니다. 사용자 지정 바인딩을 사용 하 여 더 많은 컨트롤에 대 한 참조 [사용자 지정 바인딩을 사용 하는 보안 기능](../../../../docs/framework/wcf/feature-details/security-capabilities-with-custom-bindings.md)합니다.  
  
## <a name="security-functions-of-bindings"></a>바인딩의 보안 기능  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에는 대부분의 요구 사항을 충족하는 여러 시스템 제공 바인딩이 포함되어 있습니다. 또한 특정 바인딩이 요구 사항을 충족하지 않는 경우, 사용자 지정 바인딩을 만들 수도 있습니다. 시스템 제공 바인딩 목록, 참조 [시스템 제공 바인딩](../../../../docs/framework/wcf/system-provided-bindings.md)합니다. [!INCLUDE[crabout](../../../../includes/crabout-md.md)] 사용자 지정 바인딩을 참조 [사용자 지정 바인딩을](../../../../docs/framework/wcf/extending/custom-bindings.md)합니다.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]의 모든 바인딩에는 두 가지 양식 즉, 구성 파일에서 사용되는 XML 요소 및 API가 있습니다. 예를 들어는 `WSHttpBinding` (API) 해당 하는 도구에는 [ \<wsHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)합니다.  
  
 다음 단원에서는 각 바인딩에 대한 두 가지 양식을 나열하고 해당 보안 기능에 대해 요약하여 설명합니다.  
  
### <a name="basichttp"></a>BasicHttp  
 코드를 사용 하 여는 <xref:System.ServiceModel.BasicHttpBinding> 클래스; 구성에서 사용 된 [ \<basicHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)합니다.  
  
 이 바인딩은 다음을 포함하여 일정 범위의 기존 기술을 사용하도록 디자인되었습니다.  
  
-   ASP.NET 웹 서비스(ASMX), 버전 1  
  
-   WSE(Web Service Enhancement) 응용 프로그램  
  
-   웹 서비스 상호 운용성에 정의 된 대로 basic 프로 파일링 (WS-I) 사양 ([http://go.microsoft.com/fwlink/?LinkId=38955](http://go.microsoft.com/fwlink/?LinkId=38955)).  
  
-   WS-I에 정의된 기본 보안 프로필  
  
 기본적으로 이 바인딩은 보안 처리되어 있지 않습니다. ASMX 서비스와 상호 운용되도록 디자인되었습니다. 보안을 사용하는 경우 바인딩은 기본 인증, 다이제스트 및 통합 Windows 보안과 같이 IIS(인터넷 정보 서비스) 보안 메커니즘과 원활한 상호 운용을 위해 디자인됩니다. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [전송 보안 개요](../../../../docs/framework/wcf/feature-details/transport-security-overview.md)합니다. 이 바인딩은 다음을 지원합니다.  
  
-   HTTPS 전송 보안.  
  
-   HTTP 기본 인증.  
  
-   WS-Security.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.BasicHttpSecurity>, <xref:System.ServiceModel.BasicHttpMessageSecurity>, <xref:System.ServiceModel.BasicHttpMessageCredentialType> 및 <xref:System.ServiceModel.BasicHttpSecurityMode>를 참조하십시오.  
  
### <a name="wshttpbinding"></a>WSHttpBinding  
 코드를 사용 하 여는 <xref:System.ServiceModel.WSHttpBinding> 클래스; 구성에서 사용 된 [ \<wsHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)합니다.  
  
 기본적으로 이 바인딩은 WS-Security 사양을 구현하고 WS-* 사양을 구현하는 서비스와의 상호 운용성을 제공합니다. 다음을 지원합니다.  
  
-   HTTPS 전송 보안.  
  
-   WS-Security.  
  
-   호출자를 인증하기 위한 SOAP 메시지 자격 증명 보안을 사용하여 HTTPS 전송 보호.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.WSHttpSecurity>, <xref:System.ServiceModel.MessageSecurityOverHttp>, <xref:System.ServiceModel.MessageCredentialType>, <xref:System.ServiceModel.SecurityMode>, <xref:System.ServiceModel.HttpTransportSecurity>, <xref:System.ServiceModel.HttpClientCredentialType> 및 <xref:System.ServiceModel.HttpProxyCredentialType>을 참조하십시오.  
  
### <a name="wsdualhttpbinding"></a>WSDualHttpBinding  
 코드를 사용 하 여는 <xref:System.ServiceModel.WSDualHttpBinding> 클래스; 구성에서 사용 된 [ \<wsDualHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md)합니다.  
  
 이 바인딩은 이중 서비스 응용 프로그램을 사용하도록 디자인되었습니다. 이 바인딩은 메시지 기반 전송 보안을 위한 WS-Security 사양을 구현합니다. 전송 보안을 사용할 수 없습니다. 기본적으로 다음 기능을 제공합니다.  
  
-   안정성을 위해 WS-Reliable Messaging을 구현합니다.  
  
-   전송 보안 및 인증을 위해 WS-Security를 구현합니다.  
  
-   메시지 배달을 위해 HTTP를 사용합니다.  
  
-   텍스트/XML 메시지 인코딩을 사용합니다.  
  
 WS-Security(메시지 계층 보안)를 사용하면 바인딩을 통해 다음 매개 변수를 구성할 수 있습니다.  
  
-   암호화 알고리즘을 결정하기 위한 보안 알고리즘 모음.  
  
-   다음에 대한 바인딩 옵션.  
  
    -   클라이언트에서 서비스 자격 증명 사용 가능한 out-of-band를 제공하는 경우.  
  
    -   채널 설정의 일부로 서비스에서 협상된 서비스 자격 증명을 제공하는 경우.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.WSDualHttpSecurity> 및 <xref:System.ServiceModel.WSDualHttpSecurityMode>합니다.  
  
### <a name="nettcpbinding"></a>NetTcpBinding  
 코드를 사용 하 여는 <xref:System.ServiceModel.NetTcpBinding> 클래스; 구성에서 사용 된 [ \<netTcpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md)합니다.  
  
 이 바인딩은 시스템 간 통신을 위해 최적화됩니다. 기본적으로 다음과 같은 특성이 있습니다.  
  
-   전송 계층 보안을 구현합니다.  
  
-   전송 보안 및 인증을 위해 Windows 보안을 사용합니다.  
  
-   전송을 위해 TCP를 사용합니다.  
  
-   이진 메시지 인코딩을 구현합니다.  
  
-   WS-Reliable Messaging을 구현합니다.  
  
 다음과 같은 옵션을 사용할 수 있습니다.  
  
-   메시지 계층 보안(WS-Security 사용).  
  
-   메시지 자격 증명을 통한 전송 보안—TCP를 통한 TLS(전송 계층 보안)에 의해 제공되는 기밀성과 무결성 및 WS-Security에 의해 제공되는 권한에 대한 자격 증명.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.NetTcpSecurity>, <xref:System.ServiceModel.TcpTransportSecurity>, <xref:System.ServiceModel.TcpClientCredentialType>, <xref:System.ServiceModel.MessageSecurityOverTcp> 및 <xref:System.ServiceModel.MessageCredentialType>을 참조하십시오.  
  
### <a name="netnamedpipebinding"></a>NetNamedPipeBinding  
 코드를 사용 하 여는 <xref:System.ServiceModel.NetNamedPipeBinding> 클래스; 구성에서 사용 된 [ \<netNamedPipeBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/netnamedpipebinding.md)합니다.  
  
 이 바인딩은 일반적으로 동일한 시스템에서의 프로세스 간 통신을 위해 최적화됩니다. 기본적으로 이 바인딩에는 다음과 같은 특성이 있습니다.  
  
-   메시지 전송 및 인증을 위해 전송 보안을 사용합니다.  
  
-   메시지 배달을 위해 명명된 파이프를 사용합니다.  
  
-   이진 메시지 인코딩을 구현합니다.  
  
-   암호화 및 메시지 서명.  
  
 다음과 같은 옵션을 사용할 수 있습니다.  
  
-   Windows 보안을 사용하여 인증.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.NetNamedPipeSecurity>, <xref:System.ServiceModel.NetNamedPipeSecurityMode> 및 <xref:System.ServiceModel.NamedPipeTransportSecurity>을 참조하십시오.  
  
### <a name="msmqintegrationbinding"></a>MsmqIntegrationBinding  
 코드를 사용 하 여는 <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> 클래스; 구성에서 사용 된 [ \<msmqIntegrationBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/msmqintegrationbinding.md)합니다.  
  
 이 바인딩은 비[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] MSMQ(Microsoft Message Queuing) 끝점과 상호 운용되는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 클라이언트 및 서비스를 만들기 위해 최적화됩니다.  
  
 기본적으로 이 바인딩은 전송 보안을 사용하고 다음과 같은 보안 특성을 제공합니다.  
  
-   보안을 사용할 수 없습니다(None).  
  
-   MSMQ 전송 보안입니다(Transport).  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.NetMsmqSecurity> 및 <xref:System.ServiceModel.NetMsmqSecurityMode>합니다.  
  
### <a name="netmsmqbinding"></a>NetMsmqBinding  
 코드를 사용 하 여는 <xref:System.ServiceModel.NetMsmqBinding> 클래스; 구성에서 사용 된 [ \<netMsmqBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/netmsmqbinding.md)합니다.  
  
 이 바인딩은 MSMQ 대기 중인 메시지 지원이 필요한 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스를 만들 때 사용합니다.  
  
 기본적으로 이 바인딩은 전송 보안을 사용하고 다음과 같은 보안 특성을 제공합니다.  
  
-   보안을 사용할 수 없습니다(None).  
  
-   MSMQ 전송 보안입니다(Transport).  
  
-   SOAP 기반 메시지 보안입니다(Message).  
  
-   동시 전송 및 메시지 보안입니다(Both).  
  
-   지원되는 클라이언트 자격 증명 형식: None, Windows, UserName, Certificate, IssuedToken  
  
 <xref:System.ServiceModel.MessageCredentialType.Certificate> 자격 증명은 보안 모드를 <xref:System.ServiceModel.NetMsmqSecurityMode.Both> 또는 <xref:System.ServiceModel.NetMsmqSecurityMode.Message> 중 하나로 설정하는 경우에만 지원됩니다.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.MessageSecurityOverMsmq> 및 <xref:System.ServiceModel.MsmqTransportSecurity>합니다.  
  
### <a name="wsfederationhttpbinding"></a>WSFederationHttpBinding  
 코드를 사용 하 여는 <xref:System.ServiceModel.WSFederationHttpBinding> 클래스; 구성에서 사용 된 [ \<wsFederationHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md)합니다.  
  
 기본적으로 이 바인딩은 WS-Security(메시지 계층 보안)를 사용합니다.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [페더레이션](../../../../docs/framework/wcf/feature-details/federation.md), <xref:System.ServiceModel.WSFederationHttpSecurity>, 및 <xref:System.ServiceModel.WSFederationHttpSecurityMode>합니다.  
  
## <a name="custom-bindings"></a>사용자 지정 바인딩  
 시스템 제공 바인딩이 요구 사항을 충족하지 못하는 경우 사용자 지정 보안 바인딩 요소를 사용하여 사용자 지정 바인딩을 만들 수 있습니다. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [사용자 지정 바인딩 사용 하는 보안 기능](../../../../docs/framework/wcf/feature-details/security-capabilities-with-custom-bindings.md)합니다.  
  
## <a name="binding-choices"></a>바인딩 선택  
 다음 표에서는 보안 모드 설정에서 제공하는 기능에 대해 요약하여 설명합니다. 즉, 보안 모드를 `Transport`, `Message` 또는 `TransportWithMessageCredential`로 설정한 경우 사용할 수 있는 기능을 보여 줍니다. 이 표를 사용하면 응용 프로그램에서 필요한 보안 기능을 찾는 데 도움을 줍니다.  
  
|설정|기능|  
|-------------|--------------|  
|전송|서버 인증<br /><br /> 클라이언트 인증<br /><br /> 지점 간 보안<br /><br /> 상호 운용성<br /><br /> 하드웨어 가속<br /><br /> 높은 처리량<br /><br /> 보안 방화벽<br /><br /> 대기 시간이 긴 응용 프로그램<br /><br /> 여러 홉을 통해 다시 암호화|  
|메시지|서버 인증<br /><br /> 클라이언트 인증<br /><br /> 종단 간 보안<br /><br /> 상호 운용성<br /><br /> 다양한 클레임<br /><br /> 페더레이션<br /><br /> 다단계 인증<br /><br /> 사용자 지정 토큰<br /><br /> 공증/타임스탬프 서비스<br /><br /> 대기 시간이 긴 응용 프로그램<br /><br /> 메시지 서명 지속성|  
|TransportWithMessageCredential|서버 인증<br /><br /> 클라이언트 인증<br /><br /> 지점 간 보안<br /><br /> 상호 운용성<br /><br /> 하드웨어 가속<br /><br /> 높은 처리량<br /><br /> 다양한 클라이언트 클레임<br /><br /> 페더레이션<br /><br /> 다단계 인증<br /><br /> 사용자 지정 토큰<br /><br /> 보안 방화벽<br /><br /> 대기 시간이 긴 응용 프로그램<br /><br /> 여러 홉을 통해 다시 암호화|  
  
 다음 표에서는 다양한 모드 설정을 지원하는 바인딩을 보여 줍니다. 표에서 서비스 끝점을 만드는 데 사용할 바인딩을 선택합니다.  
  
|바인딩|Transport 모드 지원|Message 모드 지원|TransportWithMessageCredential 지원|  
|-------------|----------------------------|--------------------------|--------------------------------------------|  
|`BasicHttpBinding`|예|예|예|  
|`WSHttpBinding`|예|예|예|  
|`WSDualHttpBinding`|아니요|예|아니요|  
|`NetTcpBinding`|예|예|예|  
|`NetNamedPipeBinding`|예|아니요|아니요|  
|`NetMsmqBinding`|예|예|아니요|  
|`MsmqIntegrationBinding`|예|아니요|아니요|  
|`wsFederationHttpBinding`|아니요|예|예|  
  
## <a name="transport-credentials-in-bindings"></a>바인딩의 전송 자격 증명  
 다음 표에서는 전송 보안 모드에서 `BasicHttpBinding` 또는 `WSHttpBinding` 사용 시 사용할 수 있는 클라이언트 자격 증명 형식을 보여 줍니다.  
  
|형식|설명|  
|----------|-----------------|  
|없음|클라이언트가 자격 증명을 제공할 필요가 없음을 지정합니다. 익명 클라이언트로 변환됩니다.|  
|기본|기본 인증입니다. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] RFC 2617 – HTTP 인증: 기본 및 다이제스트 인증에 사용할 수 있는 [ http://go.microsoft.com/fwlink/?LinkId=84023 ](http://go.microsoft.com/fwlink/?LinkId=84023)합니다.|  
|Digest|다이제스트 인증입니다. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] RFC 2617 – HTTP 인증: 기본 및 다이제스트 인증에 사용할 수 있는 [ http://go.microsoft.com/fwlink/?LinkId=84023 ](http://go.microsoft.com/fwlink/?LinkId=84023)합니다.|  
|NTLM|NTLM(NT LAN Manager) 인증입니다.|  
|Windows|Windows 인증입니다.|  
|인증서|인증서를 사용하여 수행되는 인증입니다.|  
|IssuedToken|이를 사용하는 서비스의 경우 보안 토큰 서비스 또는 [!INCLUDE[infocard](../../../../includes/infocard-md.md)]에서 발급한 토큰을 사용하여 클라이언트를 인증해야 합니다. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [페더레이션 및 발급 된 토큰](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)합니다.|  
  
### <a name="message-client-credentials-in-bindings"></a>바인딩의 메시지 클라이언트 자격 증명  
 다음 표에서는 메시지 보안 모드에서 바인딩 사용 시 사용할 수 있는 클라이언트 자격 증명 형식을 보여 줍니다.  
  
|형식|설명|  
|----------|-----------------|  
|없음|서비스와 익명 클라이언트가 상호 작용할 수 있습니다.|  
|Windows|Windows 자격 증명의 인증된 컨텍스트에서 SOAP 메시지 교환을 수행할 수 있습니다.|  
|UserName|서비스에서 사용자 이름 자격 증명을 사용하여 클라이언트를 인증하도록 요구할 수 있습니다. 보안 모드를 `TransportWithMessageCredential`로 설정할 경우 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]는 암호 다이제스트를 보내거나 암호를 사용하여 키를 파생하고 메시지 모드 보안에 이러한 키를 사용하는 것을 지원하지 않습니다. 따라서 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 사용자 이름 자격 증명을 사용할 때 전송에 보안을 적용합니다.|  
|인증서|서비스에서 인증서를 사용하여 클라이언트를 인증하도록 요구할 수 있습니다.|  
|IssuedToken|서비스가 보안 토큰 서비스를 사용하여 사용자 지정 토큰을 제공할 수 있습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [보안 개요](../../../../docs/framework/wcf/feature-details/security-overview.md)  
 [서비스 및 클라이언트에 보안 설정](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)  
 [자격 증명 형식 선택](../../../../docs/framework/wcf/feature-details/selecting-a-credential-type.md)  
 [사용자 지정 바인딩을 사용하는 보안 기능](../../../../docs/framework/wcf/feature-details/security-capabilities-with-custom-bindings.md)  
 [보안 동작](../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)  
 [Windows Server App Fabric에 대 한 보안 모델](http://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)
