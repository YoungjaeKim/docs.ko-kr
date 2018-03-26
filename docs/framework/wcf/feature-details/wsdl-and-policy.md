---
title: WSDL 및 정책
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cea87440-3519-4640-8494-b8a2b0e88c84
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: dd52e36199fc2412abb003d530dd5614cda8049b
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="wsdl-and-policy"></a>WSDL 및 정책
이 항목에서는 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] WSDL 1.1, WS-Policy 및 WS-PolicyAttachment 구현 세부 정보와 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서 소개된 추가 WS-Policy 어설션 및 WSDL 1.1 확장에 대해 다룹니다.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]는 이 문서에 설명된 제약 조건과 확인된 내용을 사용하여 W3C에 제출된 WS-Policy 및 WS-PolicyAttachment 사양을 구현합니다.  
  
 이 문서에서는 다음 표에 있는 접두사와 네임스페이스를 사용합니다.  
  
|접두사|네임스페이스|  
|------------|---------------|  
|wsp(WS-Policy 1.2)|http://schemas.xmlsoap.org/ws/2004/09/policy|  
|wsp(WS-Policy 1.5)|http://www.w3.org/ns/ws-policy|  
|http|http://schemas.microsoft.com/ws/06/2004/policy/http|  
|msmq|http://schemas.microsoft.com/ws/06/2004/mspolicy/msmq|  
|msf|http://schemas.microsoft.com/ws/2006/05/framing/policy|  
|mssp|http://schemas.microsoft.com/ws/2005/07/securitypolicy|  
|msc|http://schemas.microsoft.com/ws/2005/12/wsdl/contract|  
|cdp|http://schemas.microsoft.com/net/2006/06/duplex|  
  
## <a name="wcf-wsdl11-extensions"></a>WCF WSDL1.1 확장명  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]는 다음 WSDL1.1 확장을 사용하여 계약 세션 요구 사항에 대해 설명합니다.  
  
 wsdl:portType/wsdl:operation/@msc:isInitiating  
 xs:boolean은 이 작업이 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 세션을 시작함을 나타냅니다. 기본값은 `false`입니다.  
  
 wsdl:portType/wsdl:operation/@msc:isTerminating  
 xs:boolean은 이 작업이 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 세션을 종료함을 나타냅니다. 기본값은 `false`입니다.  
  
 wsdl:portType/wsdl:operation/@msc:usingSession  
 xs:boolean은 이 계약에 대해 세션을 설정해야 함을 나타냅니다.  
  
### <a name="soap-1x-http-binding-transport-uris"></a>SOAP 1.x HTTP 바인딩 전송 URI  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]는 다음 URI를 사용하여 WSDL 1.1, SOAP 1.1 및 SOAP 1.2 바인딩 확장 요소에 사용할 전송을 나타냅니다.  
  
|전송|URI|  
|---------------|---------|  
|HTTP|http://schemas.xmlsoap.org/soap/http|  
|TCP|http://schemas.microsoft.com/soap/tcp|  
|MSMQ|http://schemas.microsoft.com/soap/msmq|  
|명명된 파이프|http://schemas.microsoft.com/soap/named-pipe|  
  
## <a name="policy-assertions-implemented-by-wcf"></a>WCF에서 구현된 정책 어설션  
 WS-*(웹 서비스 사양)에서 소개되고 이 문서의 다른 단원에서 설명된 정책 어설션 외에도 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]는 다음 정책 어설션을 구현합니다.  
  
|정책 어설션|정책 주체|설명|  
|----------------------|--------------------|-----------------|  
|http:HttpBasicAuthentication|끝점|끝점이 HTTP 기본 인증을 사용합니다.|  
|http:HttpDigestAuthentication|끝점|끝점이 HTTP 다이제스트 인증을 사용합니다.|  
|http:HttpNegotiateAuthentication|끝점|끝점이 HTTP Negotiate 인증을 사용합니다.|  
|http:HttpNtlmAuthentication|끝점|끝점이 HTTP NTLM 인증을 사용합니다.|  
|msf:Streamed|끝점|끝점이 스트리밍된 메시지 프레이밍을 사용합니다. TCP, 명명된 파이프 등의 전송에 제공되는 메시지 프레이밍 프로토콜에 이 어설션이 사용됩니다.|  
|msf:SslTransportSecurity|끝점|끝점이 메시지 프레이밍에 TLS(Transport Layer Security)를 사용합니다.|  
|msf:WindowsTransportSecurity|끝점|끝점이 메시지 프레이밍에 SPNEGO(Security Provider Negotiation)를 사용합니다.|  
|msmq:MsmqBestEffort|끝점|최상의 보증을 제공하는 MSMQ입니다.|  
|msmq:MsmqSession|끝점|세션 보증을 제공하는 MSMQ입니다.|  
|msmq:MsmqVolatile|끝점|일시적인 MSMQ입니다.|  
|msmq:Authenticated|끝점|MSMQ 전송에 인증이 사용됩니다.|  
|msmq:WindowsDomain|끝점|MSMQ에서 Windows 도메인 인증을 사용합니다.|  
|cdp:CompositeDuplex|끝점|끝점이 in 및 out 메시지에 두 개의 별도 통신 전송 연결을 사용합니다.|  
|mssp:RsaToken|중첩|RSA 키 토큰 어설션입니다. 이 요구 사항은 일반적으로 보증 서명에 있는 키 정보의 일부로 직접 serialize된 RSA 키에 의해 만족됩니다.|  
|mssp:SslContextToken|중첩|WS-Trust를 사용한 이진 TLS 핸드셰이크를 사용하여 가져온 SecurityContextToken을 사용하도록 요구합니다. 중첩 어설션에는 sp:RequireDerivedKeys, mssp:MustNotSendCancel, mssp:RequireClientCertificate가 포함됩니다.|  
|mssp:MustNotSendCancel|중첩|취소 바인딩 [WS-Trust, WS-SC]을 사용한 RST(요청 보안 토큰) 요청 메시지 [WS-Trust]가 지정된 SecurityContextToken의 발급자에게 전송되지 않도록 하는 요구 사항을 지정합니다. 이 어설션이 있으면 이러한 요청 메시지를 발급자에게 보내면 안 됩니다. 이 어설션이 없으면 이러한 요청 메시지를 발급자에게 보낼 수 있습니다.|  
|mssp:RequireClientCertificate|중첩|이 선택적 요소는 클라이언트 인증서가 TLSNEGO 프로토콜의 일부로 제공되도록 하는 요구 사항을 지정합니다. 이 어설션이 있으면 클라이언트 인증서를 제공해야 합니다. 이 어설션이 없으면 클라이언트 인증서를 제공하면 안 됩니다. 이 어설션은 mssp:SslContextToken 외부에서 사용하면 안 됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [사용자 지정 WSDL 게시](../../../../docs/framework/wcf/samples/custom-wsdl-publication.md)  
 [방법: 사용자 지정 WSDL 내보내기](../../../../docs/framework/wcf/extending/how-to-export-custom-wsdl.md)  
 [방법: 사용자 지정 WSDL 가져오기](../../../../docs/framework/wcf/extending/how-to-import-custom-wsdl.md)
