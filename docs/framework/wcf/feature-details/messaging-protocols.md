---
title: "메시징 프로토콜"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5b20bca7-87b3-4c8f-811b-f215b5987104
caps.latest.revision: 
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 75a39fa1d0301a48cec7ad61c968ee3fc82d189c
ms.sourcegitcommit: 15316053918995cc1380163a7d7e7edd5c44e6d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2018
---
# <a name="messaging-protocols"></a>메시징 프로토콜
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 채널 스택에서는 인코딩 및 전송 채널을 통해 내부 메시지 표현을 통신 형식으로 변환한 후 특정 전송을 사용하여 보냅니다. 웹 서비스 상호 운용성을 위해 사용되는 가장 일반적인 전송은 HTTP이고, 웹 서비스에 사용되는 가장 일반적인 인코딩은 XML 기반 SOAP 1.1, SOAP 1.2 및 MTOM(Message Transmission Optimization Mechanism)입니다.  
  
 이 항목에서는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에 사용되는 다음 프로토콜에 대한 <xref:System.ServiceModel.Channels.HttpTransportBindingElement> 구현 정보에 대해 설명합니다.  
  
|사양/문서|링크|  
|-----------------------------|----------|  
|HTTP 1.1|http://www.ietf.org/rfc/rfc2616.txt|  
|SOAP 1.1 HTTP 바인딩|http://www.w3.org/TR/2000/NOTE-SOAP-20000508/섹션 7|  
|SOAP 1.2 HTTP 바인딩|http://www.w3.org/TR/soap12-part2/섹션 7|  
  
 이 항목에서는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 및 <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>에 사용되는 다음 프로토콜에 대한 <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement> 구현 정보에 대해 설명합니다.  
  
|사양/문서|링크|  
|-----------------------------|----------|  
|XML|http://www.w3.org/TR/REC-xml|  
|SOAP 1.1|http://www.w3.org/TR/2000/NOTE-SOAP-20000508/|  
|SOAP 1.2 Core|http://www.w3.org/TR/soap12-part1/|  
|WS-Addressing 2004/08|http://www.w3.org/Submission/2004/SUBM-ws-addressing-20040810/|  
|W3C Web Services Addressing 1.0 - Core|http://www.w3.org/TR/2006/REC-ws-addr-core-20060509|  
|W3C Web Services Addressing 1.0 - SOAP 바인딩|http://www.w3.org/TR/2006/REC-ws-addr-soap-20060509|  
|W3C Web Services Addressing 1.0 - WSDL 바인딩|http://www.w3.org/TR/2006/CR-ws-addr-wsdl-20060529/|  
W3C Web Services Addressing 1.0 - Metadata|http://www.w3.org/TR/ws-addr-metadata/|  
|WSDL SOAP1.1 바인딩|http://www.w3.org/TR/wsdl/|  
|WSDL SOAP1.2 바인딩|http://www.w3.org/Submission/wsdl11soap12/|  
  
 이 항목에서는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에 사용되는 다음 프로토콜에 대한 <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement> 구현 정보에 대해 설명합니다.  
  
|사양/문서|링크|  
|-----------------------------|----------|  
|XOP|http://www.w3.org/TR/xop10/|  
|MTOM + SOAP 1.2 바인딩|http://www.w3.org/TR/soap12-mtom/|  
|MTOM SOAP 1.1 바인딩|http://www.w3.org/Submission/soap11mtom10/|  
|MTOM WS-Policy Assertion|http://www.w3.org/Submission/2006/SUBM-WS-MTOMPolicy-20061101/.|  
  
 다음 XML 네임스페이스 및 관련 접두사는 이 항목 전체에서 사용됩니다.  
  
|접두사|네임스페이스 URI(Uniform Resource Identifier)|  
|------------|---------------------------------------------------|  
|s11|http://schemas.xmlsoap.org/soap/envelope|  
|s12|http://www.w3.org/2003/05/soap-envelope|  
|wsa|http://www.w3.org/2004/08/addressing|  
|wsam|http://www.w3.org/2007/05/addressing/metadata|  
|wsap|http://schemas.xmlsoap.org/ws/2004/09/policy/addressing|  
|wsa10|http://www.w3.org/2005/08/addressing|  
|wsaw10|http://www.w3.org/2006/05/addressing/wsdl|  
|xop|http://www.w3.org/2004/08/xop/include|  
|xmime|http://www.w3.org/2004/06/xmlmime<br /><br /> http://www.w3.org/2005/05/xmlmime|  
dp|http://schemas.microsoft.com/net/2006/06/duplex|  
  
## <a name="soap-11-and-soap-12"></a>SOAP 1.1 및 SOAP 1.2  
  
### <a name="envelope-and-processing-model"></a>봉투 및 처리 모델  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 BP11(Basic Profile 1.1) 및 SSBP10(Basic Profile 1.0)에 따라 SOAP 1.1 봉투 처리를 구현합니다. SOAP 1.2 봉투 처리는 SOAP12-Part1에 따라 구현됩니다.  
  
 이 단원에서는 BP11 및 SOAP12-Part1과 관련하여 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서 제공되는 특정 구현 선택 항목에 대해 설명합니다.  
  
#### <a name="mandatory-header-processing"></a>필수 헤더 처리  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 SOAP 1.1 및 SOAP 1.2 사양에 명시된 `mustUnderstand` 헤더 처리 규칙을 다음과 같이 변형하여 따릅니다.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 채널 스택에 전달되는 메시지는 텍스트 메시지 인코딩, 보안, 신뢰할 수 있는 메시징, 트랜잭션 등과 같은 관련 바인딩 요소로 구성된 개별 채널에 의해 처리됩니다. 각 채널은 연결된 네임스페이스에서 헤더를 인식한 후 인식된 것으로 표시합니다. 메시지가 디스패처에 전달되면 작업 포맷터는 해당 메시지/작업 계약에 필요한 헤더를 읽고 인식된 것으로 표시합니다. 그런 다음 디스패처는 나머지 헤더가 인식되지 않았지만 `mustUnderstand`로 표시되지 않았는지 확인하고 예외를 throw합니다. 받는 사람을 대상으로 하는 `mustUnderstand` 헤더가 포함된 메시지는 받는 사람 응용 프로그램 코드로 처리되지 않습니다.  
  
 이러한 계층화된 처리를 사용하면 SOAP 노드의 응용 프로그램 계층과 인프라 계층을 분리할 수 있습니다.  
  
-   B1111: 인식되지 않은 헤더는 메시지가 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 인프라 채널 스택에서 처리되고 나서 응용 프로그램에서 처리되기 전에 감지됩니다.  
  
     SOAP 1.1과 SOAP 1.2의 `mustUnderstand` 헤더 값은 서로 다릅니다. Basic Profile 1.1에서 SOAP 1.1 메시지의 `mustUnderstand` 값은 0 또는 1이어야 합니다. SOAP 1.2에서는 0, 1, `false` 및 `true`를 값으로 사용할 수 있지만 정식으로 표현된 `xs:boolean` 값(`false`, `true`)을 내보내는 것이 좋습니다.  
  
-   B1112: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 SOAP 1.1과 SOAP 1.2 버전 SOAP 봉투 모두에 대해 `mustUnderstand` 값 0과 1을 내보냅니다. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 `xs:boolean` 헤더에 `mustUnderstand`의 전체 값 공간(0, 1, `false`, `true`)을 사용합니다.  
  
#### <a name="soap-faults"></a>SOAP 오류  
 다음은 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 관련 SOAP 오류 구현 목록입니다.  
  
-   B2121: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] SOAP 1.1 오류 코드는 다음 반환: `s11:mustUnderstand`, `s11:Client`, 및 `s11:Server`합니다.  
  
-   B2122: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 `s12:MustUnderstand`, `s12:Sender` 및 `s12:Receiver`와 같은 SOAP 1.2 오류 코드를 반환합니다.  
  
### <a name="http-binding"></a>HTTP 바인딩  
  
#### <a name="soap-11-http-binding"></a>SOAP 1.1 HTTP 바인딩  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 Basic Profile 1.1 사양 단원 3.4에 따라 SOAP1.1 HTTP 바인딩을 다음과 같이 구현합니다.  
  
-   B2211: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스에서는 HTTP POST 요청의 리디렉션을 구현하지 않습니다.  
  
-   B2212: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 클라이언트는 3.4.8에 따라 HTTP 쿠키를 지원합니다.  
  
#### <a name="soap-12-http-binding"></a>SOAP 1.2 HTTP 바인딩  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 SOAP12Part2(SOAP 1.2-part 2) 사양에 설명된 대로 SOAP 1.2 HTTP 바인딩을 다음과 같이 구현합니다.  
  
 SOAP 1.2에는 `application/soap+xml` 미디어 유형에 대한 선택적 작업 매개 변수가 추가되었습니다. 이 매개 변수는 WS-Addressing을 사용하지 않을 때 SOAP 메시지 본문을 구문 분석할 필요 없이 메시지 디스패치를 최적화하는 데 유용합니다.  
  
-   R2221: `application/soap+xml` 작업 매개 변수(SOAP 1.2 요청에 있는 경우)는 해당 WSDL 바인딩 내 `soapAction` 요소의 `wsoap12:operation` 특성과 일치해야 합니다.  
  
-   R2222: WS-Addressing 2004/08 또는 WS-Addressing 1.0을 사용할 경우 `application/soap+xml` 작업 매개 변수(SOAP 1.2 메시지에 있는 경우)가 `wsa:Action`과 일치해야 합니다.  
  
 WS-Addressing을 사용하지 않고 들어오는 요청에 작업 매개 변수가 없는 경우 메시지 `Action`이 지정되지 않은 것으로 간주됩니다.  
  
## <a name="ws-addressing"></a>WS-Addressing  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 다음과 같은 세 가지 버전의 WS-Addressing을 구현합니다.  
  
-   WS-Addressing 2004/08  
  
-   W3C Web Services Addressing 1.0 Core(ADDR10-CORE) 및 SOAP 바인딩(ADDR10-SOAP)  
  
-   WS-Addressing 1.0 - Metadata  
  
### <a name="endpoint-references"></a>끝점 참조  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서 구현되는 모든 WS-Addressing 버전에서는 끝점 참조를 사용하여 끝점을 설명합니다.  
  
#### <a name="endpoint-references-and-ws-addressing-versions"></a>끝점 참조 및 WS-Addressing 버전  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 WS-Addressing을 사용하는 많은 인프라 프로토콜을 구현하며 특히, `EndpointReference` 요소 및 `W3C.WsAddressing.EndpointReferenceType` 클래스(예: WS-ReliableMessaging, WS-SecureConversation, WS-Trust)를 구현합니다. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 WS-Addressing 버전을 다른 인프라 프로토콜과 함께 사용할 수 있도록 지원합니다. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 끝점은 끝점당 하나의 WS-Addressing 버전을 지원합니다.  
  
 R3111에서 `EndpointReference` 끝점과 교환된 메시지에 사용된 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 요소 또는 형식의 네임스페이스는 이 끝점에서 구현된 WS-Addressing 버전과 일치해야 합니다.  
  
 예를 들어, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 끝점에서 WS-ReliableMessaging을 구현하는 경우 `AcksTo`에서 이러한 끝점에 의해 반환되는 `CreateSequenceResponse` 헤더는 `EncodingBinding` 요소가 이 끝점에 대해 지정하는 WS-Addressing 버전을 사용합니다.  
  
#### <a name="endpoint-references-and-metadata"></a>끝점 참조 및 메타데이터  
 대부분의 시나리오에서는 지정된 끝점에 대해 메타데이터 또는 메타데이터 참조를 전달해야 합니다.  
  
 B3121: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 WS-MetadataExchange(MEX) 사양 단원 6에 명시된 메커니즘을 사용하여 값으로 또는 참조로 끝점 참조에 대한 메타데이터를 포함합니다.  
  
 가정해 볼 수 있는 한 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스에서 토큰 발급자가 발급 한 SAML Security Assertions Markup Language () 토큰을 사용 하 여 인증에 필요한 http://sts.fabrikam123.com합니다. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 끝점에서는 토큰 발급자를 가리키는 중첩 `sp:IssuedToken` 어설션과 함께 `sp:Issuer` 어설션을 사용하여 이 인증 요구 사항을 설명합니다. `sp:Issuer` 어설션에 액세스하는 클라이언트 응용 프로그램은 토큰 발급자 끝점과 통신하는 방법을 알고 있어야 합니다. 클라이언트는 토큰 발급자에 대한 메타데이터를 알고 있어야 합니다. MEX에 정의된 끝점 참조 메타데이터 확장을 사용하여 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 토큰 발급자 메타데이터에 대한 참조를 제공합니다.  
  
```xml  
<sp:IssuedToken>  
  <sp:Issuer>  
    <wsa10:Address>  
      http://sts.fabrikam123.com  
    </wsa10:Address>  
    <wsa10:Metadata>  
      <mex:Metadata>  
        <mex:MetadataSection>  
          <mex:MetadataReference>  
            <wsa10:Address>  
              http://sts.fabrikam123.com/mex  
            </wsa10:Address>  
          </mex:MetadataReference>  
        </mex:MetadataSection>  
      </mex:Metadata>  
    </wsa10:Metadata>  
  </sp:Issuer>  
</sp:IssuedToken>  
```  
  
### <a name="message-addressing-headers"></a>메시지 주소 지정 헤더  
  
#### <a name="message-headers"></a>메시지 헤더  
 두 Ws-addressing 버전에 대해 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 사양에 설명 된 대로 다음 메시지 헤더를 사용 하 여 `wsa:To`, `wsa:ReplyTo`, `wsa:Action`, `wsa:MessageID`, 및 `wsa:RelatesTo`합니다.  
  
 B3211: 모든 WS-Addressing 버전에 대해 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 WS-Addressing 메시지 헤더인 `wsa:FaultTo` 및 `wsa:From`을 사용하지만 이 헤더를 즉시 생성하지는 않습니다.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 응용 프로그램과 상호 작용하는 응용 프로그램은 이러한 메시지 헤더를 추가할 수 있으며 이에 따라 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서 해당 메시지 헤더를 처리합니다.  
  
#### <a name="reference-parameters-and-properties"></a>참조 매개 변수 및 속성  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 끝점 참조 매개 변수 및 참조 속성을  
  
 해당 사양에 따라 처리합니다.  
  
 B3221: WS-Addressing 2004/08을 사용하도록 구성된 경우 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 끝점은 참조 속성과 참조 매개 변수의 처리를 구분하지 않습니다.  
  
### <a name="message-exchange-patterns"></a>메시지 교환 패턴  
 웹 서비스 작업 호출에 관련 된 메시지의 시퀀스 라고는 *메시지 교환 패턴*합니다. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]는 단방향, 요청-회신 및 이중 메시지 교환 패턴을 지원합니다. 이 단원에서는 사용 중인 메시지 교환 패턴에 따른 메시지 처리에 대한 WS-Addressing 요구 사항에 대해 자세히 설명합니다.  
  
 이 단원에서 요청자는 첫 번째 메시지를 보내고 응답자는 첫 번째 메시지를 받습니다.  
  
#### <a name="one-way-message"></a>단방향 메시지  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 끝점이 지정된 `Action`을 포함하는 메시지를 지원하도록 구성되어 단방향 패턴을 따르는 경우 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 끝점은 다음과 같은 동작 및 요구 사항을 따릅니다. 별도로 지정하지 않는 한 동작과 규칙은 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서 지원되는 두 WS-Addressing 버전 모두에 적용됩니다.  
  
-   R3311: 요청자는 `wsa:To`, `wsa:Action` 및 끝점 참조에 지정된 모든 참조 매개 변수에 대한 헤더를 포함해야 합니다. WS-Addressing 2004/08을 사용하고 [reference properties]이 끝점 참조에 지정된 경우에도 해당 헤더를 메시지에 추가해야 합니다.  
  
-   B3312: 요청자가 `MessageID`, `ReplyTo` 및 `FaultTo` 헤더를 포함할 수 있습니다. 이러한 헤더는 수신자 인프라에서 무시되고 응용 프로그램으로 전달됩니다.  
  
-   R3313: HTTP를 사용하고 HTTP 응답 레그에 전송 중인 메시지가 없을 때 응답자는 HTTP 202 상태 코드와 함께 본문이 빈 HTTP 응답을 보내야 합니다.  
  
     HTTP 전송을 사용 중이고 작업 계약에 메시지가 단방향으로 선언되어 있는 경우에도 인프라 메시지를 보내는 데 HTTP 응답을 사용할 수 있습니다. 예를 들어, 신뢰할 수 있는 메시징을 사용하여 HTTP 응답에서 `SequenceAcknowledgement` 메시지를 보낼 수 있습니다.  
  
-   B3314: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 응답자는 단방향 메시지에 대한 응답으로 오류 메시지를 보내지 않습니다.  
  
#### <a name="request-reply"></a>요청-회신  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 끝점이 지정된 `Action`을 포함하는 메시지가 요청-회신 패턴을 따르도록 구성되어 있는 경우 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 끝점은 다음과 같은 동작 및 요구 사항을 따릅니다. 별도로 지정하지 않는 한 동작과 규칙은 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서 지원되는 두 WS-Addressing 버전 모두에 적용됩니다.  
  
-   R3321: 요청자는 요청에 포함 해야 `wsa:To`, `wsa:Action`, `wsa:MessageID`, 모든 참조 매개 변수 또는 참조 속성 (또는 둘 다) 끝점 참조에 지정 된에 대 한 헤더입니다.  
  
-   R3322: WS-Addressing 2004/08을 사용하는 경우 `ReplyTo`도 요청에 포함해야 합니다.  
  
-   R3323: Ws-addressing 1.0을 사용 하는 경우 및 `ReplyTo` 같음 [address] 속성을 사용 하 여 기본 끝점 참조 요청에 없는 "http://www.w3.org/2005/08/addressing/anonymous" 사용 됩니다.  
  
-   R3324: 요청자 있어야 `wsa:To`, `wsa:Action`, 및 `wsa:RelatesTo` 회신 메시지의 헤더 뿐 아니라 모든 참조 매개 변수 또는 참조 속성 (또는 둘 다)으로 지정 된 헤더는 `ReplyTo` 끝점 참조에는 요청입니다.  
  
### <a name="web-services-addressing-faults"></a>Web Services Addressing 오류  
 R3411: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 WS-Addressing 2004/08에 정의된 다음과 같은 오류를 생성합니다.  
  
|코드|원인|  
|----------|-----------|  
|wsa:DestinationUnreachable|이 채널에 대해 설정된 회신 주소와 다른 `ReplyTo`를 사용하여 메시지가 도착했습니다. 받는 사람 헤더에 지정된 주소에서 수신 대기하는 끝점이 없습니다.|  
|wsa:ActionNotSupported|끝점과 연결된 인프라 채널 또는 디스패처가 `Action` 헤더에 지정된 동작을 인식하지 못합니다.|  
  
 R3412: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 WS-Addressing 1.0에 정의된 다음과 같은 오류를 생성합니다.  
  
|코드|원인|  
|----------|-----------|  
|wsa10:InvalidAddressingHeader|중복 `wsa:To`, `wsa:ReplyTo`, `wsa:From` 또는 `wsa:MessageID`합니다. 중복 `wsa:RelatesTo` 같은 `RelationshipType`합니다.|  
|wsa10:MessageAddressingHeaderRequired|필수 주소 지정 헤더가 없습니다.|  
|wsa10:DestinationUnreachable|이 채널에 대해 설정된 회신 주소와 다른 `ReplyTo`를 사용하여 메시지가 도착했습니다. 받는 사람 헤더에 지정된 주소에서 수신 대기하는 끝점이 없습니다.|  
|wsa10:ActionNotSupported|`Action` 헤더에 지정된 동작이 끝점과 연결된 디스패처 또는 인프라 채널에서 인식되지 않습니다.|  
|wsa10:EndpointUnavailable|RM 채널에서 이 오류를 다시 보냅니다. 이는 끝점에서 `CreateSequence` 메시지의 주소 지정 헤더를 검사하여 시퀀스를 처리하지 않는다는 것을 나타냅니다.|  
  
 위 표의 코드가 SOAP 1.1의 경우 `FaultCode`에 매핑되고 SOAP 1.2의 경우 `SubCode`(Code=Sender)에 매핑됩니다.  
  
### <a name="wsdl-11-binding-and-ws-policy-assertions"></a>WSDL 1.1 바인딩 및 WS-Policy Assertion  
  
#### <a name="indicating-use-of-ws-addressing"></a>WS-Addressing 사용 지정  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 정책 어설션을 사용하여 특정 WS-Addressing 버전에 대한 끝점 지원을 나타냅니다.  
  
 다음 정책 어설션은 끝점 정책 주체가 [WS-PA]이고 끝점에서 보내거나 받은 메시지가 WS-Addressing 2004/08을 사용해야 함을 나타냅니다.  
  
```xml  
<wsap:UsingAddressing />  
```  
  
 이 정책 어설션은 WS-Addressing 2004/08 사양을 보완합니다.  
  
 다음 정책 어설션은 보내거나 받은 메시지가 WS-Addressing 1.0을 사용해야 함을 나타냅니다.  
  
```xml
<wsam:Addressing/>   
```  
  
 다음 정책 어설션은 끝점 정책 주체가 [WS-PA]이고 끝점에서 보내거나 받은 메시지가 WS-Addressing 2004/08을 사용해야 함을 나타냅니다.  
  
```xml  
<wsaw10:UsingAddressing />  
```  
  
 `wsaw10:UsingAddressing` 요소는 [WS-Addressing-WSDL]에서 가져온 것이며 해당 사양 단원 3.1.2에 따라 WS-Policy 컨텍스트에서 사용됩니다.  
  
 주소 지정을 사용해도 WSDL 1.1, SOAP 1.1 및 SOAP 1.2 HTTP 바인딩의 의미 체계가 변경되지 않습니다. 예를 들어, 주소 지정 및 WSDL SOAP 1.x HTTP 바인딩을 사용하는 끝점에 보낸 요청에 대한 회신이 필요한 경우 HTTP 응답을 사용하여 회신을 보내야 합니다.  
  
 http 응답을 통해 전송되는 회신의 경우 WS-AM 어설션은 다음과 같습니다.  
  
```xml  
<wsam:AnonymousResponses/>  
```  
  
 완성된 정책 어설션은 다음과 같을 수 있습니다.  
  
```xml  
<wsam:Addressing>  
    <wsp:Policy>  
        <wsam:AnonymousResponses />   
    </wsp:Policy>  
</wsam:Addressing>  
```  
  
 그러나 요청자와 응답자 간에 설정된 두 개의 독립적인 역방향 HTTP 연결을 활용하는 메시지 교환 패턴이 있습니다(예: 응답자가 보낸 원하지 않은 단방향 메시지).  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 두 기본 전송 채널에서 복합 이중 채널을 설정하는 데 사용할 수 있는 기능을 제공합니다. 복합 이중 채널에서는 입력 메시지에 하나의 채널이 사용되고 출력 메시지에 나머지 하나의 채널이 사용됩니다. HTTP 전송의 경우 복합 이중 채널은 두 개의 역방향 HTTP 연결을 제공합니다. 요청자가 한 연결을 사용하여 메시지를 응답자에게 보내고, 응답자는 다른 연결을 사용하여 메시지를 요청자에게 다시 보냅니다.  
  
 별도의 http 요청을 통해 전송되는 회신의 경우 WS-AM 어설션은 다음과 같습니다.  
  
```xml  
<wsam:NonAnonymousResponses/>  
```  
  
 완성된 정책 어설션은 다음과 같을 수 있습니다.  
  
```xml  
<wsam:Addressing>  
    <wsp:Policy>  
      <wsam:NonAnonymousResponses />   
   </wsp:Policy>  
  </wsam:Addressing>  
```  
  
 WSDL 1.1 SOAP 1.x HTTP 바인딩을 사용하는 끝점에서 끝점 정책 주체가 [WS-PA]인 다음 어설션을 사용하려면 요청자와 응답자 간에 주고 받는 메시지 흐름에 각각 사용할 두 개의 개별적인 역방향 HTTP 연결이 필요합니다.  
  
```xml  
<cdp:CompositeDuplex/>  
```  
  
 앞의 문에 따라 요청 메시지의 `wsa:ReplyTo` 헤더에 대해 다음 요구 사항이 충족되어야 합니다.  
  
-   R3514: 요청 메시지는 끝점에 보낸는 `ReplyTo` 헤더는 `[address]` 속성 같지 않음 "http://www.w3.org/2005/08/addressing/anonymous" 끝점이 WSDL 1.1 SOAP 1.x HTTP 바인딩을 사용 하 고 않은 정책 대안이 있는 경우는 `wsap10:UsingAddressing` 또는 `wsap:UsingAddressing` 와 결합 되어 어설션 `cdp:CompositeDuplex` 연결 합니다.  
  
-   R3515: 요청 메시지는 끝점에 보낸는 `ReplyTo` 헤더는 `[address]` 속성에 "http://www.w3.org/2005/08/addressing/anonymous", 수도 있고 한 `ReplyTo` 끝점이 WSDL 1.1 SOAP 1.x HTTP 바인딩을 사용 하 고 정책 대안이 있는 경우 헤더 와 `wsap10:UsingAddressing` 어설션은 `cdp:CompositeDuplex` 어설션은 연결 합니다.  
  
-   R3516: 요청 메시지는 끝점에 보낸는 `ReplyTo` 헤더는 `[address]` 속성에 "http://www.w3.org/2005/08/addressing/anonymous" 끝점이 WSDL 1.1 SOAP 1.x HTTP 바인딩을 사용 하 고 않은 정책 대안이 있는 `wsap:UsingAddressing` 어설션은 고 없는 `cdp:CompositeDuplex`어설션은 연결 합니다.  
  
 WS-addressing WSDL 사양에서는 세 개의 텍스트 값(required, optional, prohibited)을 가진 `<wsaw:Anonymous/>`wsa:ReplyTo 요소를 추가하여`wsa:ReplyTo` 헤더(단원 3.2)에 대한 요구 사항을 나타냄으로써 비슷한 프로토콜 바인딩을 설명하려고 합니다. 그러나 해당 요소를 어설션으로 사용하여 대안 교차를 지원하려면 도메인별 확장이 필요하므로, 이러한 요소 정의는 WS-Policy 컨텍스트에서 어설션으로 사용할 수 없습니다. 또한 이러한 요소 정의는 통신 중인 끝점 동작과 반대로 `ReplyTo` 헤더 값을 나타내므로 HTTP 전송에만 해당됩니다.  
  
#### <a name="action-definition"></a>동작 정의  
 WS-Addressing 2004/08에서는 `wsa:Action` 요소에 대한 `wsdl:portType/wsdl:operation/[wsdl:input | wsdl:output | wsdl:fault]` 특성을 정의합니다. WS-ADDR10-WSDL(WS-Addressing 1.0 WSDL 바인딩)에서는 비슷한 특성인 `wsaw10:Action`을 정의합니다.  
  
 둘 간에는 WS-ADDR의 단원 3.3.2와 WS-ADDR10-WSDL의 단원 4.4.4에 각각 설명된 기본 동작 패턴의 의미 체계만 차이가 있습니다.  
  
 동일한 `portType` 또는 계약([!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 용어)을 공유하지만 서로 다른 WS-Addressing 버전을 사용하는 두 개의 끝점을 사용하는 것이 바람직합니다. 그러나 동작이 `portType`에 정의되어 있고 `portType`을 구현하는 끝점을 통해 변경되지 않아야 할 경우 두 기본 동작 패턴을 모두 지원할 수 없습니다.  
  
 이 문제를 해결하기 위해 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 단일 버전의 `Action` 특성을 지원합니다.  
  
 B3521: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 WS-ADDR10-WSDL에 정의된 대로 `wsaw10:Action` 요소에서 `wsdl:portType/wsdl:operation/[wsdl:input | wsdl:output | wsdl:fault]` 특성을 사용하여 끝점에 사용되는 WS-Addressing 버전에 상관없이 해당 메시지에 대한 `Action` URI를 결정합니다.  
  
#### <a name="use-endpoint-reference-inside-wsdl-port"></a>WSDL 포트에서 끝점 참조 사용  
 WS-ADDR10-WSDL 단원 4.1에서는 `wsdl:port` 자식 요소를 포함하도록 `<wsa10:EndpointReference…/>` 요소를 확장하여 WS-Addressing 용어로 끝점을 설명합니다. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 WS-Addressing 2004/08에서 이 유틸리티를 확장하여 `<wsa:EndpointReference…/>`를 `wsdl:port`의 자식 요소로 나타낼 수 있게 합니다.  
  
-   R3531: 끝점에 `<wsaw10:UsingAddressing/>` 정책 어설션과 연결된 정책 대안이 있는 경우 해당`wsdl:port` 요소는`<wsa10:EndpointReference …/>` 자식 요소를 포함할 수 있습니다.  
  
-   R3532: 경우는 `wsdl:port` 에 자식 요소가 `<wsa10:EndpointReference …/>`, `wsa10:EndpointReference/wsa10:Address` 자식 요소 값의 값과 일치 해야는 `@address` 형제의 특성 `wsdl:port` / `wsdl:location` 요소입니다.  
  
-   R3533: 끝점에 `<wsap:UsingAddressing/>``wsdl:port` 정책 어설션과 연결된 정책 대안이 있는 경우 해당 `<wsa:EndpointReference …/>` 요소는 자식 요소를 포함할 수 있습니다.  
  
-   R3534: 경우는 `wsdl:port` 에 자식 요소가 `<wsa:EndpointReference …/>`, `wsa:EndpointReference/wsa:Address` 자식 요소 값의 값과 일치 해야는 `@address` 형제의 특성 `wsdl:port` / `wsdl:location` 요소입니다.  
  
### <a name="composition-with-ws-security"></a>WS-Security를 사용하여 구성  
 WS-ADDR 및 WS-ADDR10의 보안 고려 사항 단원에 따르면 모든 주소 지정 메시지 헤더를 메시지 본문과 함께 서명하여 바인딩하는 것이 좋습니다.  
  
 WS-Security가 메시지 무결성 보호를 위해 사용될 경우 WS-Addressing 메시지 헤더뿐 아니라 참조 매개 변수 또는 속성(또는 둘 모두)에서 생성된 헤더를 메시지 본문과 함께 서명해야 합니다.  
  
### <a name="examples"></a>예제  
  
#### <a name="one-way-message"></a>단방향 메시지  
 이 시나리오에서 발신자는 수신자에게 단방향 메시지를 보냅니다. SOAP 1.2, HTTP 1.1 및 W3C WS-Addressing 1.0이 사용됩니다.  
  
 요청 메시지 구조: 메시지 헤더는 `wsa10:To` 및 `wsa10:Action` 요소를 포함합니다. 메시지 본문은 응용 프로그램 네임스페이스의 특정 `<app:Ping>` 요소를 포함합니다.  
  
 HTTP 헤더: POST의 대상이 URI에서 일치 하는 `wsa10:To` 요소입니다.  
  
 Content-Type 헤더에는 SOAP 1.2에 필요한 `application/soap+xml` 값이 있습니다. `charset` 및 `action` 매개 변수가 포함됩니다. Content-Type 헤더의 `action` 매개 변수가 `wsa10:Action` 메시지 헤더의 값과 일치합니다.  
  
```  
POST http://fabrikam123.com/Service HTTP/1.1  
Content-Type: application/soap+xml; charset=utf-8;    
              action="http://fabrikam123.com/Service/OneWay"  
Host: 131.107.72.15  
Content-Length: 1501  
Expect: 100-continue  
Proxy-Connection: Keep-Alive  
<s12:Envelope>  
  <s12:Header>  
    <wsa10:To s12:mustUnderstand="1">  
        http://fabrikam123.com/Service  
    </wsa10:To>  
    <wsa10:Action s12:mustUnderstand="1">  
        http://fabrikam123.com/Service/OneWay   
    </wsa10:Action>  
  </s12:Header>  
  <s12:Body>  
    <Ping xmlns="http://fabrikam123.com/Service/">  
      <Text>Hello World</Text>  
    </Ping>  
  </s12:Body>  
</s12:Envelope>  
```  
  
 수신자는 빈 HTTP 응답 및 상태 202를 사용하여 응답합니다. HTTP 응답의 예를 들면 다음과 같습니다.  
  
```  
HTTP/1.1 202 Accepted  
Date: Fri, 15 Jul 2005 08:56:07 GMT  
Server: Microsoft-IIS/6.0  
MicrosoftOfficeWebServer: 5.0_Pub  
X-Powered-By: ASP.NET  
X-AspNet-Version: 2.0.50215  
Cache-Control: private  
Content-Length: 0  
```  
  
## <a name="soap-message-transmission-optimization-mechanism"></a>SOAP MTOM(Message Transmission Optimization Mechanism)  
 이 단원에서는 HTTP SOAP MTOM에 대한 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 구현 정보에 대해 설명합니다. MTOM 기술은 기존 텍스트/XML 인코딩 또는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 이진 인코딩과 동일한 클래스의 SOAP 메시지 인코딩 메커니즘입니다. MTOM에는 다음과 같은 내용이 포함됩니다.  
  
-   base64 인코딩된 이진 데이터를 개별 이진 부분으로 포함하는 XML 정보 항목을 최적화하는 [XOP]에 설명된 XML 인코딩 및 패키징 메커니즘  
  
-   XOP 패키지의 각 이진 부분 및 XML Infoset을 개별 MIME 부분으로 serialize하는 XOP 패키지의 MIME 캡슐화  
  
-   SOAP 1.x 봉투에 적용되는 MIME XOP 인코딩  
  
-   HTTP 전송 바인딩  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 HTTP를 사용하지 않는 전송에서 MTOM을 사용할 수 있습니다. 그러나 이 항목에서는 HTTP에 중점을 두어 설명합니다.  
  
 MTOM 형식에서는 MTOM 자체와 XOP 및 MIME을 포함한 다양한 사양을 사용합니다. 이 사양의 모듈성으로 인해 형식 및 처리 의미 체계에 대한 정확한 요구 사항을 재구성하기가 다소 어렵습니다. 이 단원에서는 MTOM HTTP 바인딩의 형식 및 처리 요구 사항에 대해 설명합니다.  
  
### <a name="mtom-message-encoding"></a>MTOM 메시지 인코딩  
  
#### <a name="generating-mtom-messages"></a>MTOM 메시지 생성  
 [XOP] 단원 3.1에서는 base64 값을 추상적으로 정의된 XOP 패키지에 포함하는 요소 정보 항목을 사용하여 XML을 인코딩하는 프로세스를 설명합니다.  
  
 다음 단계에서는 MTOM 관련 인코딩 프로세스에 대해 설명합니다.  
  
1.  인코딩할 SOAP 봉투와 요소 정보 항목이 포함 되어 있는지 확인 한 `[namespace name]` 의 "http://www.w3.org/2004/08/xop/include"와 `[local name]` 의 `Include`합니다.  
  
2.  빈 MIME 패키지를 만듭니다.  
  
3.  원본 XML Infoset에서 최적화할 요소 정보 항목을 식별합니다. 항목을 최적화하려면 요소 정보 항목의 `[children]`을 구성하는 문자가 `xs:base64Binary`의 정규 형식(XSD-2, 3.2.16 base64Binary 참조)이고 공백 없는 콘텐츠 앞, 옆 또는 다음에 공백 문자를 포함하지 않아야 합니다.  
  
4.  원본 SOAP 봉투의 복사본인 XOP SOAP 봉투를 만듭니다. 단, 이전 단계에서 식별된 각 요소 정보 항목의 자식을 다음과 같이 구성된 `xop:Include` 요소 정보 항목으로 대체합니다.  
  
    1.  대체된 문자를 base64 인코딩된 데이터로 처리하여 이진 데이터로 변환합니다.  
  
    2.  R3133 및 R3134 요구 사항을 충족하는 고유한 Content-ID 헤더 값을 생성합니다.  
  
    3.  이진 값을 사용하여 Content-Transfer-Encoding MIME 헤더를 생성합니다.  
  
    4.  최적화할 요소 정보 항목(새로 삽입된 `xop:Include` 요소 정보 항목의 [parent])에 `xmime:contentType` 특성 정보 항목이 있는 경우 `xmime:contentType` 특성 값을 사용하여 Content-Type MIME 헤더를 생성합니다.  
  
    5.  base64, 4b의 Content-ID 헤더, 4c의 Content- Transfer-Encoding 헤더, Content-Type 헤더(4d 단계에서 생성된 경우)로 처리된 대체 문자에서 디코딩된 이진 데이터로 형성된 콘텐츠를 사용하여 새 이진 MIME 부분을 생성합니다.  
  
    6.  4b 단계에서 생성된 Content-ID 헤더 값에서 파생된 cid: uri 값을 사용하여 `href` 특성을 `xop:Include` 요소에 추가합니다. 묶는 제거 "\<" 및 ">" 문자를 이스케이프 URL 문자열 및 접두사를 추가 합니다. 나머지 `cid:`합니다. RFC1738 및 RFC2396으로 이스케이프하려면 다음과 같은 최소 문자 집합이 필요합니다. 다른 문자를 이스케이프할 수 있습니다.  
  
        ```  
        Hexadecimal 00-1F , 7F, 20, "<" | ">" | "#" | "%" | <">  
        "{" | "}" | "|" | "\" | "^" | "[" | "]" | "`" | "~" | "^"  
        ```  
  
5.  4단계의 XOP SOAP 봉투를 사용하여 루트 MIME 부분을 만듭니다.  
  
6.  HTTP Content-Type 헤더를 포함하여 HTTP 헤더를 씁니다.  
  
7.  MIME 패키지를 씁니다.  
  
#### <a name="processing-mtom-messages"></a>MTOM 메시지 처리  
 MTOM 메시지 처리 과정은 이전 "MTOM 메시지 생성" 단원에서 설명한 프로세스와 정확히 반대입니다.  
  
1.  루트 MIME 부분에 Content-Type `application/xop+xml`이 있는지 확인합니다.  
  
2.  패키지의 루트 MIME 부분을 구문 분석하여 SOAP 봉투를 XML 문서로 구성합니다. 문자 인코딩은 루트 MIME 부분 Content-Type의 `charset` 매개 변수에 의해 결정됩니다.  
  
3.  `xop:Include` 요소 정보 항목을 [children] 속성의 단독 멤버로 가진 구성된 SOAP 봉투의 각 요소 정보 항목의 경우 다음을 수행합니다.  
  
    1.  `cid:` 접두사를 제거하고 `@href` 요소의 `xop:Include` 특성 값에서 모든 URI 이스케이프 시퀀스(RFC 2396)를 이스케이프 해제합니다. 결과 문자열을 묶습니다 "\<", ">"입니다.  
  
    2.  3a 단계에서 파생된 문자열과 일치하는 Content-ID 헤더 값을 가진 MIME 부분을 찾습니다.  
  
    3.  각 항목의 `xop:Include` 속성에 나타나는 `children` 요소 정보 항목을 3b 단계에서 식별된 MIME 부분의 엔터티 본문의 정규 base64 인코딩(XSD-2, 3.2.16 base64Binary 참조)을 나타내는 문자 정보 항목으로 대체합니다. 즉, `xop:Include` 요소 정보 항목을 패키지 부분에서 재구성된 데이터로 효과적으로 대체합니다.  
  
#### <a name="http-content-type-header"></a>HTTP Content-Type 헤더  
 다음은 MTOM 및 RFC 2387에서 파생되고 MTOM 사양 자체에 명시된 요구 사항에서 파생된 SOAP 1.x MTOM 인코딩된 메시지의 HTTP Content-Type 헤더 형식에 대한 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]를 구현하는 설명입니다.  
  
-   R4131: HTTP Content-Type 헤더에는 multipart/related(대/소문자 구분 안 함) 값 및 해당 매개 변수가 있어야 합니다. 매개 변수 이름은 대/소문자를 구분하지 않습니다. 매개 변수의 순서는 중요하지 않습니다.  
  
-   MIME 메시지에 대한 Content-Type 헤더의 전체 BNF(Backus-Naur Form)는 RFC 2045, 단원 5.1에 나열되어 있습니다.  
  
-   R4132: HTTP Content-Type 헤더에는 큰따옴표로 묶은 `application/xop+xml` 값을 가진 형식 매개 변수가 있어야 합니다.  
  
 큰따옴표 사용 요구 사항이 없으면 RFC 2387 텍스트에서 모든 multipart/related 미디어 형식 매개 변수에 가장 가능성이 높은 포함 되어 등의 문자는 예약 "@" or "/" 큰따옴표가 필요 합니다.  
  
-   R4133: HTTP Content-Type 헤더에는 SOAP 1.x 봉투를 포함하는 MIMI 부분의 Content-ID 헤더 값이 큰따옴표로 묶인 시작 매개 변수가 있어야 합니다. 시작 매개 변수가 생략된 경우 첫 번째 MIME 부분에 SOAP 1.x 봉투가 포함되어야 합니다.  
  
-   R4134: SOAP 1.1 MTOM 인코딩된 메시지의 HTTP Content-Type 헤더는 큰따옴표로 묶인 text/xml 값을 가진 start-info 매개 변수를 포함해야 합니다.  
  
-   R4135: SOAP 1.2 MTOM 인코딩된 메시지의 HTTP Content-Type 헤더는 큰따옴표로 묶인 `application/soap+xml` 값을 가진 start-info 매개 변수를 포함해야 합니다.  
  
-   R4136: SOAP 1.x MTOM 인코딩된 메시지의 HTTP Content-Type 헤더에는 RFC 2046, 단원 5.1.1에 정의된 MIME 경계 BNF와 일치하는 큰따옴표로 묶인 값을 가진 boundary 매개 변수가 있어야 합니다.  
  
    ```  
    boundary := 0*69<bchars> bcharsnospace   
    bchars := bcharsnospace / " "   
    bcharsnospace :=    DIGIT / ALPHA / "'" / "(" / ")" / "+"   
                        / "_" / "," / "-" / "." / "/" / ":" / "=" / "?"  
    ```  
  
     예를 들면 다음과 같습니다.  
  
     올바른 예  
  
    ```  
    Content-Type: multipart/related; type="application/xop+xml";start=" <part0@tempuri.org>";boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1";start-info="text/xml"  
    ```  
  
     올바른 예  
  
    ```  
    Content-Type: Multipart/Related; type="application/xop+xml";start-info="text/xml";boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1"  
    ```  
  
     잘못된 예  
  
    ```  
    Content-Type: Multipart/Related; type=application/xop+xml;start=" <part0@tempuri.org>";start-info="text/xml";boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1"   
    ```  
  
#### <a name="infoset-mime-part"></a>Infoset MIME 부분  
 SOAP 1.x 봉투는 XOP MIME 패키지의 루트 부분으로 캡슐화되며 `infoset` 부분이라고도 합니다.  
  
-   R4141: SOAP 1.x 봉투는 XOP MIME 패키지의 루트 부분으로 캡슐화되어야 하고, `infoset` 부분이라고도 하며, HTTP Content-Type에서 참조되어야 합니다.  
  
-   R4142: SOAP `Infoset` 부분은 `Content-ID`, `Content-Transfer-Encoding` 및 `Content-Type` MIME 헤더를 포함해야 합니다.  
  
 Content-ID 헤더의 형식은 RFC 2045에 다음과 같이 정의되어 있습니다.  
  
```  
"Content-ID" ":" msg-id  
```  
  
 `msg-id`는 RFC 2822(RFC 822보다 우선하며, RFC 2045에서 참조됨)에 다음과 같이 정의되어 있으며  
  
```  
msg-id    =       [CFWS] "<" id-left "@" id-right ">" [CFWS]  
```  
  
 효과적으로 전자 메일 주소 내에 포함 되어 및 "\<" 및 ">"입니다. `[CFWS]` 접두사와 접미사는 설명을 전달하기 위해 RFC 2822에 추가되었지만 상호 운용성을 유지하려면 사용하지 않아야 합니다.  
  
 R4143: Infoset MIME 부분의 Content-ID 헤더 값은 `msg-id` 접두사 및 접미사 부분을 생략한 상태의 RFC 2822의 `[CFWS]` 생성을 따라야 합니다.  
  
 많은 MIME 구현 내에 포함 된 값에 대 한 요구 사항 완화 "\<" 및 ">" 전자 메일 주소를 사용 하 고 `absoluteURI` 묶인 "\<", ">" 전자 메일 주소와 함께 합니다. 이 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 버전에서는 다음과 같은 형식의 Content-ID MIME 헤더 값을 사용합니다.  
  
```  
Content-ID: <http://tempuri.org/0>   
```  
  
 R4144: MTOM 프로세서는 다음과 같은 완화된 `msg-id`와 일치하는 Content-ID 헤더 값을 사용해야 합니다.  
  
```  
msg-id-relaxed =     [CFWS] "<" (absoluteURI | mail-address) ">" [CFWS]  
mail-address   =     id-left "@" id-right  
```  
  
 MIME(RFC 2045)은 MIME 부분의 콘텐츠 인코딩을 전달하기 위해 Content-Transfer-Encoding 헤더를 제공합니다. Content-Transfer-Encoding에 대해 정의된 기본값은 7비트로 대부분의 SOAP 메시지에 적합하지 않으므로 상호 운용성 향상을 위해 Content-Transfer-Encoding 헤더가 필요합니다.  
  
-   R4145: SOAP Infoset 부분은 Content-Transfer-Encoding 헤더를 포함해야 합니다.  
  
-   R4146: SOAP 봉투 문자 인코딩이 UTF-8이면 Content-Transfer-Encoding 헤더 값이 8비트여야 합니다.  
  
-   R4147: SOAP 봉투 문자 인코딩이 UTF-16이면 Content-Transfer-Encoding 헤더 값이 이진이어야 합니다.  
  
-   [XOP] 단원 5에 따르면  
  
-   R4148: SOAP1.1 Infoset 부분은 미디어 형식이 application/xop + xml 콘텐츠 형식 헤더를 포함 해야 하 고 매개 변수가 type = "text/xml" 및 charset  
  
    ```  
    Content-Type: application/xop+xml;  
                  charset=utf-8;type="text/xml"  
    ```  
  
-   R4149: SOAP 1.2 Infoset 부분은 미디어 유형으로 Content-type 헤더를 포함 해야 `application/xop+xml` 고 매개 변수가 type = "`application/soap+xml`" 및 `charset`합니다.  
  
    ```  
    Content-Type: application/xop+xml;  
                  charset=utf-8;type="application/soap+xml"  
    ```  
  
     XOP에서는 `charset`의 `application/xop+xml` 매개 변수를 선택적 요소로 정의하고 있지만, `charset` 미디어 형식의 `text/xml` 매개 변수에 대한 BP 1.1 요구 사항과 마찬가지로 상호 운용성을 위해 필요합니다.  
  
-   R41410: `type` 및 `charset` 매개 변수가 SOAP 1.x Infoset 부분의 Content-Type 헤더에 있어야 합니다.  
  
#### <a name="wcf-endpoint-support-for-mtom"></a>MTOM에 대한 WCF 끝점 지원  
 MTOM의 목적은 SOAP 메시지를 인코딩하여 base64 인코딩된 데이터를 최적화하는 데 있습니다. 다음은 제약 조건 목록입니다.  
  
-   R4151: base64 인코딩된 데이터를 포함하는 모든 요소 정보 항목이 최적화될 수 있습니다.  
  
-   B4152: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 base64 인코딩된 데이터를 포함하고 길이가 1024바이트를 초과하는 요소 정보 항목을 최적화합니다.  
  
 MTOM을 사용하도록 구성된 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 끝점은 항상 MTOM 인코딩된 메시지를 보냅니다. 필수 조건을 충족하는 부분이 없더라도 MTOM 인코딩된 메시지를 보냅니다. 이 메시지는 단일 MIME 부분에서 SOAP 봉투를 포함하는 MIME 패키지로 serialize됩니다.  
  
### <a name="ws-policy-assertion-for-mtom"></a>MTOM WS-Policy Assertion  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 다음과 같은 정책 어설션을 사용하여 끝점의 MTOM 사용을 나타냅니다.  
  
```xml  
<wsoma:OptimizedMimeSerialization ... />  
```  
  
-   R4211: 이전 정책 어설션은 끝점 정책 주체를 포함하고 MTOM을 사용하여 끝점에서 보내거나 받은 모든 메시지를 최적화하도록 지정합니다.  
  
-   B4212: MTOM 최적화를 사용하도록 구성된 경우 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 끝점은 해당 `wsdl:binding`에 연결된 정책에 MTOM 정책 어설션을 추가합니다.  
  
### <a name="composition-with-ws-security"></a>WS-Security를 사용하여 구성  
 MTOM은 `text/xml` 및 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 이진 XML과 비슷한 인코딩 메커니즘입니다. MTOM은 WS-Security 및 기타 WS-* 프로토콜을 사용하여 자연스러운 구성을 제공합니다. WS-Security를 사용하여 보안된 메시지는 MTOM을 사용하여 최적화할 수 있습니다.  
  
### <a name="examples"></a>예제  
  
#### <a name="wcf-soap-11-message-encoded-using-mtom"></a>MTOM을 사용하여 인코딩한 WCF SOAP 1.1 메시지  
  
```  
POST http://131.107.72.15/Mtom/svc/service.svc/Soap11MtomUTF8 HTTP/1.1  
SOAPAction: "http://xmlsoap.org/echoBinaryAsString"  
Content-Type: multipart/related;type="application/xop+xml";  
              start="<http://tempuri.org/0>";start-info="text/xml";  
       boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1"  
Host: 131.107.72.15  
Content-Length: 1501  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1  
Content-ID: <http://tempuri.org/0>  
Content-Transfer-Encoding: 8bit  
Content-Type: application/xop+xml;charset=utf-8;type="text/xml"  
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">  
  <s:Body>  
    <EchoBinaryAsString xmlns="http://xmlsoap.org/Ping">  
      <array>  
        <xop:Include   
         href="cid:http%3A%2F%2Ftempuri.org%2F1%2F632618206521093670"   
         xmlns:xop="http://www.w3.org/2004/08/xop/include"/>  
      </array>  
    </EchoBinaryAsString>  
  </s:Body>  
</s:Envelope>  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1  
Content-ID: <http://tempuri.org/1/632618206521093670>  
Content-Transfer-Encoding: binary  
Content-Type: application/octet-stream  
…Binary Content..  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1  
```  
  
#### <a name="wcf-secure-soap-12-message-encoded-using-mtom"></a>MTOM을 사용하여 인코딩한 WCF Secure SOAP 1.2 메시지  
 이 예제에서 메시지는 WS-Security를 사용하여 보호된 SOAP 1.2 및 MTOM을 사용하여 인코딩됩니다. 인코딩을 위해 식별되는 이진 부분은 `BinarySecurityToken`의 콘텐츠로서, 암호화된 서명 및 암호화된 본문에 해당하는 `CipherValue`의 `EncryptedData`입니다. `CipherValue`의 `EncryptedKey`는 길이가 1024바이트 미만이므로 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서 최적화하도록 식별되지 않습니다.  
  
```  
POST http://131.107.72.15/Mtom/service.svc/Soap12MtomSecureSignEncrypt HTTP/1.1  
Content-Type: multipart/related; type="application/xop+xml";  
              start="<http://tempuri.org/0>";  
            boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3";  
              start-info="application/soap+xml";   
              action="http://xmlsoap.org/echoBinaryAsString"  
Host: 131.107.72.15  
Content-Length: 1941  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3  
Content-ID: <http://tempuri.org/0>  
Content-Transfer-Encoding: 8bit  
Content-Type: application/xop+xml;charset=utf-8;type="application/soap+xml"  
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/" xmlns:u="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">  
  <s:Header>  
    <o:Security s:mustUnderstand="1" xmlns:o="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd">  
      <u:Timestamp u:Id="uuid-4d4ee765-5717-4d53-9ac9-99bddc07df6c-5">  
        <u:Created>2005-09-09T06:57:32.488Z</u:Created>  
        <u:Expires>2005-09-09T07:02:32.488Z</u:Expires>  
      </u:Timestamp>  
      <o:BinarySecurityToken u:Id="uuid-4d4ee765-5717-4d53-9ac9-99bddc07df6c-2" ValueType="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-x509-token-profile-1.0#X509v3" EncodingType="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-soap-message-security-1.0#Base64Binary">  
        <xop:Include href="cid:http%3A%2F%2Ftempuri.org%2F1%2F632618206525089430" xmlns:xop="http://www.w3.org/2004/08/xop/include"/>  
      </o:BinarySecurityToken>  
      <e:EncryptedKey Id="_1" xmlns:e="http://www.w3.org/2001/04/xmlenc#">  
        <e:EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#rsa-oaep-mgf1p"/>  
        <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">  
          <o:SecurityTokenReference>  
            <o:KeyIdentifier ValueType="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-x509-token-profile-1.0#X509SubjectKeyIdentifier">Xeg55vRyK3ZhAEhEf+YT0z986L0=</o:KeyIdentifier>  
          </o:SecurityTokenReference>  
        </KeyInfo>  
        <e:CipherData>          <e:CipherValue>oQfpxwT8/SAGyZQzKE2b4yO6dXuQj7pwJ+5CGL3Rf7C06bQ5ttMoQ9GLJcQYkXTzin+WwHEgs5bj5ml9HKTW9QAU5JJ6lksdymmQvWP5ZtGPBVchO4sofEGoCKmBiZL/DYS/cnbzgnc/3a6NYnc10y2fWGaGLiqa00zijAw7o0Y=</e:CipherValue>  
        </e:CipherData>  
      </e:EncryptedKey>  
      <c:DerivedKeyToken u:Id="_2" xmlns:c="http://schemas.xmlsoap.org/ws/2005/02/sc">  
        <o:SecurityTokenReference>  
          <o:Reference URI="#_1"/>  
        </o:SecurityTokenReference>  
        <c:Nonce>OrEPRX7fISIS4sXYWPMv3g==</c:Nonce>  
      </c:DerivedKeyToken>  
      <e:ReferenceList xmlns:e="http://www.w3.org/2001/04/xmlenc#">  
        <e:DataReference URI="#_3"/>  
        <e:DataReference URI="#_4"/>  
      </e:ReferenceList>  
      <e:EncryptedData Id="_4" Type="http://www.w3.org/2001/04/xmlenc#Element" xmlns:e="http://www.w3.org/2001/04/xmlenc#">  
        <e:EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#aes256-cbc"/>  
        <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">  
          <o:SecurityTokenReference>  
            <o:Reference URI="#_2"/>  
          </o:SecurityTokenReference>  
        </KeyInfo>  
        <e:CipherData>  
          <e:CipherValue>  
            <xop:Include href="cid:http%3A%2F%2Ftempuri.org%2F2%2F632618206525089430" xmlns:xop="http://www.w3.org/2004/08/xop/include"/>  
          </e:CipherValue>  
        </e:CipherData>  
      </e:EncryptedData>  
    </o:Security>  
  </s:Header>  
  <s:Body u:Id="_0">  
    <e:EncryptedData Id="_3" Type="http://www.w3.org/2001/04/xmlenc#Content" xmlns:e="http://www.w3.org/2001/04/xmlenc#">  
      <e:EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#aes256-cbc"/>  
      <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">  
        <o:SecurityTokenReference xmlns:o="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd">  
          <o:Reference URI="#_2"/>  
        </o:SecurityTokenReference>  
      </KeyInfo>  
      <e:CipherData>  
        <e:CipherValue>  
          <xop:Include href="cid:http%3A%2F%2Ftempuri.org%2F3%2F632618206525089430" xmlns:xop="http://www.w3.org/2004/08/xop/include"/>  
        </e:CipherValue>  
      </e:CipherData>  
    </e:EncryptedData>  
  </s:Body>  
</s:Envelope>  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3  
Content-ID: <http://tempuri.org/1/632618206525089430>  
Content-Transfer-Encoding: binary  
Content-Type: application/octet-stream  
...Binary content of BinarySecurityToken - X509 Certificate...  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3  
Content-ID: <http://tempuri.org/2/632618206525089430>  
Content-Transfer-Encoding: binary  
Content-Type: application/octet-stream  
...Binary serialization of the encrypted primary signature...  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3  
Content-ID: <http://tempuri.org/3/632618206525089430>  
Content-Transfer-Encoding: binary  
Content-Type: application/octet-stream  
...Binary serialization of the encrypted Body...  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3--  
```
