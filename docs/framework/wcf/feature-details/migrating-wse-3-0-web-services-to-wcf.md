---
title: WSE 3.0 웹 서비스를 WCF로 마이그레이션
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7bc5fff7-a2b2-4dbc-86cc-ecf73653dcdc
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: a7e7187eb6ed444ba2c28aa301ce4b3b16129030
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="migrating-wse-30-web-services-to-wcf"></a>WSE 3.0 웹 서비스를 WCF로 마이그레이션
WSE 3.0 웹 서비스를 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]로 마이그레이션하면 성능이 향상되고 추가 전송, 추가 보안 시나리오 및 WS-* 사양이 지원됩니다. WSE 3.0에서 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]로 마이그레이션된 웹 서비스는 2배에서 4배까지 성능이 향상됩니다. 지 원하는 전송에 대 한 자세한 내용은 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], 참조 [전송 선택](../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)합니다. 지 원하는 시나리오의 목록은 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], 참조 [일반적인 보안 시나리오](../../../../docs/framework/wcf/feature-details/common-security-scenarios.md)합니다. 지 원하는 사양 목록은 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], 참조 [웹 서비스 프로토콜 상호 운용성 가이드](../../../../docs/framework/wcf/feature-details/web-services-protocols-interoperability-guide.md)합니다.  
  
 다음 단원에서는 WSE 3.0 웹 서비스의 특정 기능을 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]로 마이그레이션하는 방법에 대한 지침을 제공합니다.  
  
## <a name="general"></a>일반  
 WSE 3.0 응용 프로그램과 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 응용 프로그램에서는 유선 수준의 상호 운용을 지원하며 공통된 용어 집합을 사용합니다. 이러한 유선 수준의 상호 운용은 WSE 3.0 응용 프로그램과 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 응용 프로그램에서 모두 지원하는 WS-* 사양 집합을 통해 가능합니다. WSE 3.0 응용 프로그램이나 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 응용 프로그램 개발 시 WSE의 턴키 보안 어설션 이름과 인증 모드 등의 공통되는 용어 집합이 사용되었습니다.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]와 ASP.NET 또는 WSE 3.0 프로그래밍 모델은 비슷한 점이 많지만 서로 다른 프로그래밍 모델입니다. 에 대 한 내용은 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 참조 프로그래밍 모델을 [기본 프로그래밍 수명 주기](../../../../docs/framework/wcf/basic-programming-lifecycle.md)합니다.  
  
> [!NOTE]
>  WSE 웹 서비스를 WCF로 마이그레이션하는 [ServiceModel Metadata 유틸리티 도구 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 도구를 클라이언트를 생성 하기 위해 사용할 수 있습니다. 그러나 이 클라이언트에는 WCF 서비스의 시작 지점으로 사용할 수 있는 인터페이스와 클래스도 포함되어 있습니다. 생성되는 인터페이스에는 <xref:System.ServiceModel.OperationContractAttribute> 속성이 <xref:System.ServiceModel.OperationContractAttribute.ReplyAction%2A>로 설정되어 계약의 멤버에 적용되는 `*` 특성이 있습니다. WSE 클라이언트가이 설정을 사용 하 여 웹 서비스를 호출 하면 다음 예외가 throw 됩니다: **Web.Services3.ResponseProcessingException: WSE910: 응답 메시지를 처리 하는 동안 오류가 발생 하 고 내부에서 오류를 찾을 수 있습니다 예외**합니다. 이를 완화하려면 <xref:System.ServiceModel.OperationContractAttribute.ReplyAction%2A> 특성의 <xref:System.ServiceModel.OperationContractAttribute> 속성을 `null`처럼 `http://Microsoft.WCF.Documentation/ResponseToOCAMethod`이 아닌 값으로 설정합니다.  
  
## <a name="security"></a>보안  
  
### <a name="wse-30-web-services-that-are-secured-using-a-policy-file"></a>정책 파일을 사용하여 WSE 3.0 웹 서비스 보안  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스에서는 구성 파일을 사용하여 서비스를 보안할 수 있으며 그 메커니즘은 WSE 3.0 정책 파일과 비슷합니다. WSE 3.0에서 정책 파일을 사용하여 웹 서비스를 보호할 때 턴키 보안 어설션 또는 사용자 지정 정책 어설션을 사용합니다. 턴키 보안 어셜션은 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 보안 바인딩 요소의 인증 모드에 밀접하게 매핑됩니다. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 인증 모드와 WSE 3.0 턴키 보안 어설션은 같거나 비슷하게 이름이 지정될 뿐만 아니라 같은 자격 증명 형식을 사용하여 메시지를 보안합니다. 예를 들어 WSE 3.0의 `usernameForCertificate` 턴키 보안 어설션은 `UsernameForCertificate`의 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 인증 모드에 매핑됩니다. 다음 코드 예제에서는 WSE 3.0의 `usernameForCertificate` 턴키 보안 어설션을 사용하는 최소 정책이 사용자 지정 바인딩에서 `UsernameForCertificate`의 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 인증 모드에 매핑되는 방식을 보여 줍니다.  
  
 **WSE 3.0**  
  
```xml  
<policies>  
  <policy name="MyPolicy">  
    <usernameForCertificate messageProtectionOrder="SignBeforeEncrypt"  
                            requireDeriveKeys="true"/>  
  </policy>  
</policies>  
```  
  
 **WCF**  
  
```xml  
<customBinding>  
  <binding name="MyBinding">  
    <security authenticationMode="UserNameForCertificate"   
              messageProtectionOrder="SignBeforeEncrypt"  
              requireDerivedKeys="true"/>  
  </binding>  
</customBinding>  
```  
  
 정책 파일에 지정된 WSE 3.0 웹 서비스의 보안 설정을 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]로 마이그레이션하려면 구성 파일에 사용자 지정 바인딩을 만들고 턴키 보안 어설션을 해당 인증 모드로 설정해야 합니다. 또한 WSE 3.0 클라이언트가 서비스와 통신할 때 August 2004 WS-Addressing 사양을 사용하도록 사용자 지정 바인딩을 구성해야 합니다. 마이그레이션된 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스가 WSE 3.0 클라이언트와 통신하지 않아도 되고 보안 패리티만 유지하면 되는 경우에는 사용자 지정 바인딩을 만들지 않고 적합한 보안 설정이 지정된 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 시스템 정의 바인딩을 사용하는 것이 좋습니다.  
  
 다음 표에서는 WSE 3.0 정책 파일과 이에 해당하는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]의 사용자 지정 바인딩 간의 매핑을 보여 줍니다.  
  
|WSE 3.0 턴키 보안 어설션|WCF 사용자 지정 바인딩 구성|  
|----------------------------------------|--------------------------------------|  
|\<usernameOverTransportSecurity />|`<customBinding>   <binding name="MyBinding">     <security authenticationMode="UserNameOverTransport" />     <textMessageEncoding messageVersion="Soap12WSAddressingAugust2004" />   </binding> </customBinding>`|  
|\<mutualCertificate10Security />|`<customBinding>   <binding name="MyBinding">     <security messageSecurityVersion="WSSecurity10WSTrustFebruary2005WSSecureConversationFebruary2005WSSecurityPolicy11BasicSecurityProfile10" authenticationMode="MutualCertificate" />     <textMessageEncoding messageVersion="Soap12WSAddressingAugust2004" />   </binding> </customBinding>`|  
|\<usernameForCertificateSecurity />|`<customBinding>   <binding name="MyBinding">     <security authenticationMode="UsernameForCertificate"/>     <textMessageEncoding messageVersion="Soap12WSAddressingAugust2004" />   </binding> </customBinding>`|  
|\<anonymousForCertificateSecurity />|`<customBinding>   <binding name="MyBinding">     <security authenticationMode="AnonymousForCertificate"/>     <textMessageEncoding messageVersion="Soap12WSAddressingAugust2004" />   </binding> </customBinding>`|  
|\<kerberosSecurity />|`<customBinding>   <binding name="MyBinding">     <security authenticationMode="Kerberos"/>     <textMessageEncoding messageVersion="Soap12WSAddressingAugust2004" />   </binding> </customBinding>`|  
|\<mutualCertificate11Security />|`<customBinding>   <binding name="MyBinding">     <security authenticationMode="MutualCertificate"/>     <textMessageEncoding messageVersion="Soap12WSAddressingAugust2004" />   </binding> </customBinding>`|  
  
 Wcf에서 사용자 지정 바인딩 만들기에 대 한 자세한 내용은 참조 [사용자 지정 바인딩을](../../../../docs/framework/wcf/extending/custom-bindings.md)합니다.  
  
### <a name="wse-30-web-services-that-are-secured-using-application-code"></a>응용 프로그램 코드를 사용하여 보안된 WSE 3.0 웹 서비스  
 WSE 3.0을 사용하는지 또는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]를 사용하는지에 관계없이 구성 대신 응용 프로그램 코드에서 보안 요구 사항을 지정할 수 있습니다. WSE 3.0에서 보안 요구 사항을 지정하려면 `Policy` 클래스에서 파생되는 클래스를 만든 다음 `Add` 메서드를 호출하여 요구 사항을 추가합니다. 코드에서 보안 요구 사항을 지정 하는 방법에 대 한 자세한 내용은 참조 하십시오. [하는 방법: 정책 파일을 웹 서비스 사용 하지 않는 보안](http://go.microsoft.com/fwlink/?LinkId=73747)합니다. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서 코드에 보안 요구 사항을 지정하려면 <xref:System.ServiceModel.Channels.BindingElementCollection> 클래스의 인스턴스를 만들고 <xref:System.ServiceModel.Channels.SecurityBindingElement>의 인스턴스를 <xref:System.ServiceModel.Channels.BindingElementCollection>에 추가합니다. 보안 어설션 요구 사항은 <xref:System.ServiceModel.Channels.SecurityBindingElement> 클래스의 정적 인증 모드 도우미 메서드를 사용하여 설정됩니다. 사용 하 여 코드에서 보안 요구 사항을 지정 하는 방법에 대 한 자세한 내용은 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], 참조 [하는 방법: SecurityBindingElement를 사용자 지정 바인딩을 사용 하 여 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md) 및 [하는 방법:에 대 한 SecurityBindingElement 만들기는 인증 모드를 지정 된](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)합니다.  
  
### <a name="wse-30-custom-policy-assertion"></a>WSE 3.0 사용자 지정 정책 어설션  
 WSE 3.0에는 SOAP 메시지를 보안하는 사용자 지정 정책 어설션과 SPAO 메시지를 보안하지 않는 사용자 지정 정책 어설션이 있습니다. SOAP 메시지를 보안하는 정책 어설션은 WSE 3.0 `SecurityPolicyAssertion` 클래스에서 파생되며 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서 <xref:System.ServiceModel.Channels.SecurityBindingElement> 클래스와 같은 개념입니다.  
  
 중요한 점은 WSE 3.0 턴키 보안 어설션이 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 인증 모드의 하위 집합이라는 것입니다. WSE 3.0에서 사용자 지정 정책 어설션을 만든 경우에는 이에 해당하는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 어설션 모드가 있을 수 있습니다. 예를 들어 WSE 3.0에서 `UsernameOverTransport` 턴키 보안 어설션에 해당하는 CertificateOverTransport 보안 어설션을 제공하지는 않지만 클라이언트 인증을 위해 X.509 인증서를 사용합니다. 이 시나리오에 대한 고유의 사용자 지정 정책 어설션을 정의한 경우 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서 마이그레이션이 간단해 집니다. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]는 이 시나리오에 대해 인증 모드를 정의하므로 정적 인증 모드 도우미 메서드를 활용하여 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]<xref:System.ServiceModel.Channels.SecurityBindingElement>를 구성할 수 있습니다.  
  
 SOAP 메시지를 보안하는 사용자 지정 정책 어설션에 해당하는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 인증 모드가 없는 경우 <xref:System.ServiceModel.Channels.TransportSecurityBindingElement>, <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 또는 <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 클래스에서 클래스를 파생하고 해당 바인딩 요소를 지정합니다. 자세한 내용은 참조 하십시오. [하는 방법: SecurityBindingElement를 사용자 지정 바인딩을 사용 하 여 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)합니다.  
  
 참조는 SOAP 메시지를 보호 하지 하는 사용자 지정 정책 어설션을 변환할 [필터링](../../../../docs/framework/wcf/feature-details/filtering.md) 및 샘플 [사용자 지정 메시지 인터셉터](../../../../docs/framework/wcf/samples/custom-message-interceptor.md)합니다.  
  
### <a name="wse-30-custom-security-token"></a>WSE 3.0 사용자 지정 보안 토큰  
 사용자 지정 토큰을 만드는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 프로그래밍 모델은 WSE 3.0과 다릅니다. WSE에서 사용자 지정 토큰 만들기에 대 한 세부 정보를 참조 하십시오. [사용자 지정 보안 토큰 만들기](http://go.microsoft.com/fwlink/?LinkID=73750)합니다. 사용자 지정 토큰에 대 한 자세한 내용은 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], 참조 [하는 방법: 사용자 지정 토큰 만들기](../../../../docs/framework/wcf/extending/how-to-create-a-custom-token.md)합니다.  
  
### <a name="wse-30-custom-token-manager"></a>WSE 3.0 사용자 지정 토큰 관리자  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서 사용자 지정 토큰 관리자를 만드는 프로그래밍 모델은 WSE 3.0과 다릅니다. 사용자 지정 토큰 관리자 및 사용자 지정 보안 토큰에 필요한 다른 구성 요소를 만드는 방법에 대 한 세부 정보를 참조 하십시오. [하는 방법: 사용자 지정 토큰 만들기](../../../../docs/framework/wcf/extending/how-to-create-a-custom-token.md)합니다.  
  
> [!NOTE]
>  사용자 지정 `UsernameToken` 보안 토큰 관리자를 만든 경우 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 사용자 지정 보안 토큰 관리자를 만드는 것보다 쉽게 인증 논리를 지정하는 메커니즘을 제공합니다. 자세한 내용은 참조 하십시오. [하는 방법: 사용자 지정 사용자 이름 및 암호 유효성 검사기를 사용 하 여](../../../../docs/framework/wcf/feature-details/how-to-use-a-custom-user-name-and-password-validator.md)합니다.  
  
### <a name="wse-30-web-services-that-use-mtom-encoded-soap-messages"></a>MTOM 인코딩된 SOAP 메시지를 사용하는 WSE 3.0 웹 서비스  
 WSE 3 응용 프로그램처럼 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 응용 프로그램에서 구성에 MTOM 메시지 인코딩을 지정할 수 있습니다. 이 설정을 마이그레이션할 추가 [ \<mtomMessageEncoding >](../../../../docs/framework/configure-apps/file-schema/wcf/mtommessageencoding.md) 바인딩에 서비스에 대 한 합니다. 다음 코드 예제에서는 WSE 3.0에서 MTOM 인코딩을 지정하는 방법과 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서 이에 해당하는 서비스를 지정하는 방법을 보여 줍니다.  
  
 **WSE 3.0**  
  
```xml  
<messaging>  
    <mtom clientMode="On"/>  
</messaging>  
```  
  
 **WCF**  
  
```xml  
<customBinding>  
  <binding name="MyBinding">  
    <mtomMessageEncoding/>  
  </binding>  
</customBinding>  
```  
  
## <a name="messaging"></a>메시징  
  
### <a name="wse-30-applications-that-use-the-wse-messaging-api"></a>WSE 메시징 API를 사용하는 WSE 3.0 응용 프로그램  
 WSE 메시징 API를 사용하여 클라이언트와 웹 서비스 간에 전달되는 XML에 직접 액세스할 수 있으면 "POX"(Plain Old XML)를 사용하도록 응용 프로그램을 변환할 수 있습니다. POX에 대 한 자세한 내용은 참조 하십시오. [POX 응용 프로그램과 상호 운용](../../../../docs/framework/wcf/feature-details/interoperability-with-pox-applications.md)합니다. WSE 메시징 API에 대 한 자세한 내용은 참조 하십시오. [Sending and 받는 SOAP 메시지를 사용 하 여 WSE 메시징 API](http://go.microsoft.com/fwlink/?LinkID=73755)합니다.  
  
## <a name="transports"></a>전송  
  
### <a name="tcp"></a>TCP  
 기본적으로 TCP 전송을 사용하여 SOAP 메시지를 보내는 WSE 3.0 클라이언트 및 웹 서비스는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 클라이언트 및 웹 서비스와 상호 운용되지 않습니다. 이러한 비호환성은 성능상의 이유와 TCP 프로토콜에 사용된 프레이밍의 차이로 인한 것입니다. 그러나 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 샘플에는 WSE 3.0과 상호 운용하는 사용자 지정 TCP 세션을 구현하는 방법이 자세히 설명되어 있습니다. 이 샘플에 대 한 세부 정보를 참조 하십시오. [전송: WSE 3.0 TCP 상호 운용성](../../../../docs/framework/wcf/samples/transport-wse-3-0-tcp-interoperability.md)합니다.  
  
 지정 하는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 응용 프로그램에서 TCP 전송을 사용, 사용 하 여는 [ \<netTcpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md)합니다.  
  
### <a name="custom-transport"></a>사용자 지정 전송  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서 WSE 3.0 사용자 지정 전송에 해당하는 것이 채널 확장입니다. 채널 확장을 만드는 방법에 대 한 세부 정보를 참조 하십시오. [채널 계층 확장](../../../../docs/framework/wcf/extending/extending-the-channel-layer.md)합니다.  
  
## <a name="see-also"></a>참고 항목  
 [기본 프로그래밍 수명 주기](../../../../docs/framework/wcf/basic-programming-lifecycle.md)  
 [사용자 지정 바인딩](../../../../docs/framework/wcf/extending/custom-bindings.md)  
 [방법: SecurityBindingElement를 사용하여 사용자 지정 바인딩 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)  
 [방법: 지정된 인증 모드에 대한 SecurityBindingElement 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)
