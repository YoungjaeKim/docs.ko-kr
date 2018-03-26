---
title: 웹 서비스 프로토콜 상호 운용성 가이드
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f2981678-ebdb-433d-899b-467f7df95fb2
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 6b962452b6127d259733418969f1fb7b5036b1e5
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="web-services-protocols-interoperability-guide"></a>웹 서비스 프로토콜 상호 운용성 가이드
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]에서는 다양한 웹 서비스 프로토콜을 구현합니다. 이러한 프로토콜의 대부분에는 구현자가 결정하는 여러 가지 옵션과 확장 지점이 포함되어 있습니다. 이 항목에서는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서 구현하는 웹 서비스 프로토콜의 목록을 제공합니다. 이 단원의 다른 항목에서는 지원되는 각 프로토콜의 구현에 대해 자세히 설명합니다.  
  
## <a name="web-services-protocols-implemented-by-wcf"></a>WCF에서 구현하는 웹 서비스 프로토콜  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]는 채널을 통해 WS(웹 서비스) 인프라 프로토콜을 지원하고 계약 기능을 통해 웹 서비스 응용 프로그램 프로토콜을 지원합니다. 응용 프로그램 프로토콜의 상호 운용은 XSD(XML 스키마 설명 언어) 1.0과 WSDL(웹 서비스 기술 언어) 1.1을 통해 가능합니다.  
  
 인프라 프로토콜 상호 운용성은 WS-* 사양에서 제공됩니다. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 채널은 다양 한 WS-에 대 한 지원을 제공\* 인프라 프로토콜입니다. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 채널은 바인딩 요소를 사용하여 구성됩니다. 다음 표에 WS-의 전체 목록을\* 다양 한 의해 구현 되는 인프라 프로토콜 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 바인딩 요소입니다.  
  
 <xref:System.ServiceModel.Channels.HttpTransportBindingElement>는 다음 표의 사양을 지원합니다.  
  
|사양/문서|링크|  
|-----------------------------|----------|  
|HTTP 1.1|[RFC 2616](http://go.microsoft.com/fwlink/?LinkId=90372)|  
|SOAP 1.1 HTTP 바인딩|[Simple Object Access Protocol (SOAP) 1.1](http://go.microsoft.com/fwlink/?LinkId=90520), 섹션 7|  
|SOAP 1.2 HTTP 바인딩|[SOAP 버전 1.2 2 부: Adjuncts (Second Edition)](http://go.microsoft.com/fwlink/?LinkId=95329), 섹션 7|  
  
 <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> 및 <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>는 다음 표의 사양을 지원합니다.  
  
|사양/문서|링크|  
|-----------------------------|----------|  
|XML|[Extensible Markup Language (XML) 1.0 (Fourth Edition)](http://go.microsoft.com/fwlink/?LinkId=15139)|  
|SOAP 1.1|[Simple Object Access Protocol (SOAP) 1.1](http://go.microsoft.com/fwlink/?LinkId=96687)|  
|SOAP 1.2 Core|[SOAP 버전 1.2 1 부: 메시징 프레임 워크 (Second Edition)](http://go.microsoft.com/fwlink/?LinkId=94664)|  
|WS-Addressing 2004/08|[웹 서비스 주소 지정 (Ws-addressing)](http://go.microsoft.com/fwlink/?LinkId=81239)|  
|W3C Web Services Addressing 1.0 - Core|[웹 서비스 주소 지정 1.0-코어](http://go.microsoft.com/fwlink/?LinkId=96688)|  
|W3C Web Services Addressing 1.0 - SOAP 바인딩|[Web Services Addressing 1.0-SOAP 바인딩](http://go.microsoft.com/fwlink/?LinkId=96689)|  
|W3C Web Services Addressing 1.0 - WSDL 바인딩*|[Web Services Addressing 1.0-WSDL 바인딩](http://go.microsoft.com/fwlink/?LinkId=96690)|  
|W3C Web Services Addressing 1.0 Metadata|[웹 서비스 주소 지정 1.0-메타 데이터](http://www.w3.org/TR/ws-addr-metadata/)|  
|WSDL SOAP1.1 바인딩|[웹 서비스 기술 언어 (WSDL) 1.1](http://go.microsoft.com/fwlink/?LinkId=96160)|  
|WSDL SOAP1.2 바인딩|[SOAP 1.2에 대 한 WSDL 1.1 바인딩 확장명](http://go.microsoft.com/fwlink/?LinkId=96691)|  
  
 <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>는 다음 표의 사양을 지원합니다.  
  
|사양/문서|링크|  
|-----------------------------|----------|  
|XOP|[XML 바이너리 최적화 패키징](http://go.microsoft.com/fwlink/?LinkId=96714)|  
|MTOM + SOAP1.2 바인딩|[SOAP 메시지 전송 최적화 메커니즘](http://go.microsoft.com/fwlink/?LinkId=96713)|  
|MTOM SOAP 1.1 바인딩|[SOAP MTOM 1.0에 대 한 1.1 바인딩](http://go.microsoft.com/fwlink/?LinkId=96712)|  
|MTOM WS-PolicyAssertions|게시될 예정|  
  
 <xref:System.ServiceModel.Channels.SecurityBindingElement>는 다음 표의 사양을 지원합니다.  
  
|사양/문서|링크|  
|-----------------------------|----------|  
|WSS: SOAP Message Security 1.0|[Web Services Security: SOAP 메시지 보안 1.0](http://go.microsoft.com/fwlink/?LinkId=94684)|  
|WSS: Username Token Profile 1.0|[웹 서비스 보안 프로필 1.0](http://go.microsoft.com/fwlink/?LinkId=95334)<br /><br /> 필요한 Password/@Type= 후 (기본값)|  
|WSS: X.509 Token Profile 1.0|[Web Services Security X.509 인증서 토큰 프로필](http://go.microsoft.com/fwlink/?LinkId=95335)|  
|WSS: SAML 1.1 Token Profile 1.0|[Web Services Security: SAML 토큰 프로필](http://go.microsoft.com/fwlink/?LinkId=96693)|  
|WSS: SOAP Message Security 1.1|[Web Services Security: SOAP 메시지 보안 1.1](http://go.microsoft.com/fwlink/?LinkId=91240)|  
|WSS Username Token Profile 1.1|[웹 서비스 보안 UsernameToken Profile 1.1](http://go.microsoft.com/fwlink/?LinkId=95331)<br /><br /> 암호 기반 키 파생을 구현하지 않음<br /><br /> 필요한 Password/@Type= 후 (기본값)|  
|WSS: X509 Token Profile 1.1|[Web Services Security X.509 인증서 토큰 프로필 1.1](http://go.microsoft.com/fwlink/?LinkId=95332)|  
|WSS: Kerberos Token Profile 1.1|[Web Services Security Kerberos 토큰 프로필 1.1](http://go.microsoft.com/fwlink/?LinkId=95333)|  
|WSS: SAML 1.1 Token Profile 1.1|[웹 서비스 보안 SAML 토큰 프로필 1.1](http://go.microsoft.com/fwlink/?LinkId=96694)|  
|WS-Secure Conversation|[웹 서비스 보안 대화 언어](http://go.microsoft.com/fwlink/?LinkId=95317)|  
|WS-Trust 1.4|[웹 서비스 트러스트 언어](http://go.microsoft.com/fwlink/?LinkId=169514)|  
|WS-SecurityPolicy 2005/07|[웹 서비스 보안 대화 언어](http://go.microsoft.com/fwlink/?LinkId=95317)<br /><br /> OASIS WS-SX Technical Committee에 제출된 오류에 따라 수정됨<br /><br /> [ws-sx 메시지](http://go.microsoft.com/fwlink/?LinkId=96700)|  
|WS-ReliableMessaging 1.1|[Reliable Messaging 프로토콜 버전 1.1](../../../../docs/framework/wcf/feature-details/reliable-messaging-protocol-version-1-1.md)|  
  
 <xref:System.ServiceModel.Channels.TransactionFlowBindingElement>는 다음 표의 사양을 지원합니다.  
  
|사양/문서|링크|  
|-----------------------------|----------|  
|WS-Coordination|[웹 서비스 조정](http://go.microsoft.com/fwlink/?LinkId=95324)|  
|WS-AtomicTransaction|[웹 서비스 원자성 트랜잭션](http://go.microsoft.com/fwlink/?LinkId=95323)|  
  
 <xref:System.ServiceModel.Description.MetadataExporter>, <xref:System.ServiceModel.Description.MetadataImporter>, <!--zz <xref:System.ServiceModel.Description.WSDLExporter>, <xref:System.ServiceModel.Description.WSDLImporter>, --> `System.ServiceModel.Description.MetadataImporter`, `System.ServiceModel.Description.WSDLImporter`, 및 <xref:System.ServiceModel.Description.MetadataResolver> 클래스에서는 다음 메타 데이터 사양을 지원 합니다.  
  
-   [XML 스키마 1 부: 구조 제 2 판](http://go.microsoft.com/fwlink/?LinkId=3536)  
  
-   [XML 스키마 2 부: 데이터 형식 제 2 판](http://go.microsoft.com/fwlink/?LinkId=40138)  
  
-   [WSDL 1.1](http://go.microsoft.com/fwlink/?LinkId=96160)  
  
-   [WS-Policy 1.2](http://go.microsoft.com/fwlink/?LinkId=96705)  
  
-   [WS-Policy 1.5](http://go.microsoft.com/fwlink/?LinkId=96706)  
  
-   [Ws-policyattachment 1.2](http://go.microsoft.com/fwlink/?LinkId=96707)  
  
-   [WS-MetadataExchange 1.1](http://go.microsoft.com/fwlink/?LinkId=94868)  
  
-   [Ws-transfer Get 메타 데이터 검색](http://go.microsoft.com/fwlink/?LinkId=96708)  
  
 또한 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 다음과 같은 상호 운용성 프로필이 구현됩니다.  
  
-   [Basic Profile 1.1](http://go.microsoft.com/fwlink/?LinkId=69313)  
  
-   [단순 SOAP 바인딩 1.0](http://go.microsoft.com/fwlink/?LinkId=96710)  
  
-   [기본 보안 프로필 1.0 초안](http://go.microsoft.com/fwlink/?LinkId=96711)  
  
## <a name="see-also"></a>참고 항목  
 [시스템 제공 상호 운용성 바인딩에서 지원하는 웹 서비스 프로토콜](../../../../docs/framework/wcf/feature-details/web-services-protocols-supported-by-system-provided-interoperability-bindings.md)  
 [메시징 프로토콜](../../../../docs/framework/wcf/feature-details/messaging-protocols.md)  
 [데이터 계약 스키마 참조](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)  
 [WSDL 및 정책](../../../../docs/framework/wcf/feature-details/wsdl-and-policy.md)  
 [보안 프로토콜](../../../../docs/framework/wcf/feature-details/security-protocols.md)  
 [Reliable Messaging 프로토콜 버전 1.0](../../../../docs/framework/wcf/feature-details/reliable-messaging-protocol-version-1-0.md)  
 [Reliable Messaging 프로토콜 버전 1.1](../../../../docs/framework/wcf/feature-details/reliable-messaging-protocol-version-1-1.md)  
 [트랜잭션 프로토콜](../../../../docs/framework/wcf/feature-details/transaction-protocols.md)  
 [컨텍스트 교환 프로토콜](../../../../docs/framework/wcf/feature-details/context-exchange-protocol.md)
