---
title: '&lt;httpTransport&gt;'
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8b30c065-b32a-4fa3-8eb4-5537a9c6b897
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 50cbf6521870a54f4f87c3eeb12030d5d7f2f6bb
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="lthttptransportgt"></a>&lt;httpTransport&gt;
사용자 지정 바인딩의 SOAP 메시지 전송을 위한 HTTP 전송을 지정합니다.  
  
 \<system.serviceModel>  
\<bindings>  
\<customBinding>  
\<binding>  
\<httpTransport>  
  
## <a name="syntax"></a>구문  
  
```xml  
<httpTransport  
    allowCookies=Boolean"  
    authenticationScheme="Digest/Negotiate/Ntlm/Basic/Anonymous"  
    bypassProxyOnLocal=Boolean"  
    hostnameComparisonMode="StrongWildcard/Exact/WeakWildcard"  
    keepAliveEnabled="Boolean"  
    maxBufferSize="Integer"  
    proxyAddress="Uri"  
    proxyAuthenticationScheme="None/Digest/Negotiate/Ntlm/Basic/Anonymous"  
IntegratedWindowsAuthentication: Specifies Windows authentication"  
    realm="String"  
    transferMode="Buffered/Streamed/StreamedRequest/StreamedResponse"  
        unsafeConnectionNtlmAuthentication="Boolean"  
        useDefaultWebProxy="Boolean" />  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|allowCookies|클라이언트가 쿠키를 수락하고 이를 앞으로의 요청에서 전파할지 여부를 지정하는 부울 값입니다. 기본값은 `false`입니다.<br /><br /> 쿠키를 사용하는 ASMX 웹 서비스와 상호 작용할 때 이 특성을 사용할 수 있습니다. 그러면 서버에서 반환된 쿠키가 해당 서비스에 대한 이후의 모든 클라이언트 요청에 자동으로 복사되도록 할 수 있습니다.|  
|authenticationScheme|HTTP 수신기가 처리하는 클라이언트 요청을 인증하는 데 사용되는 프로토콜을 지정합니다. 유효한 값은 다음과 같습니다.<br /><br /> 다이제스트: 다이제스트 인증을 지정 합니다.<br />-Negotiate: 인증 체계를 결정 하는 클라이언트와 협상 합니다. 클라이언트와 서버 모두 Kerberos를 지원하면 이 인증 체계가 사용되고, 그렇지 않으면 NTLM이 사용됩니다.<br />-Ntlm: NTLM 인증을 지정 합니다.<br />-기본: 기본 인증을 지정 합니다.<br />-Anonymous: 익명 인증을 지정 합니다.<br /><br /> 기본값은 Anonymous입니다. 이 특성은 <xref:System.Net.AuthenticationSchemes> 형식입니다. 이 특성은 한 번만 설정할 수 있습니다.|  
|bypassProxyOnLocal|로컬 주소에 대해 프록시 서버를 사용하지 않을 것인지 여부를 나타내는 부울 값입니다. 기본값은 `false`입니다.<br /><br /> 로컬 주소는 로컬 LAN 또는 인트라넷에 있는 주소입니다.<br /><br /> 서비스 주소가 http://localhost로 시작되는 경우 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)]은 항상 프록시를 무시합니다.<br /><br /> 클라이언트가 동일한 시스템의 서비스와 통신할 때 프록시를 통하게 하려면 localhost 대신 호스트 이름을 사용해야 합니다.|  
|hostnameComparisonMode|URI 구문 분석에 사용되는 HTTP 호스트 이름 비교 모드를 지정합니다. 유효한 값은 다음과 같습니다.<br /><br /> -StrongWildcard: ("+")는 지정한 체계, 포트 및 상대 URI의 컨텍스트에서 모든 호스트 이름을 일치 합니다.<br />비슷한: 와일드 카드<br />-WeakWildcard: ("*") 컨텍스트에서 지정 된 체계, 포트 및 상대 UIR 명시적으로 일치 하지 않는 또는 강력한 와일드 카드 메커니즘을 통해 가능한 모든 호스트 이름과 일치 합니다.<br /><br /> 기본값은 StrongWildcard입니다. 이 특성은 `System.ServiceModel.HostnameComparisonMode` 형식입니다.|  
|keepAliveEnabled|인터넷 리소스에 영구 연결을 할 것인지 여부를 지정하는 부울 값입니다.|  
|maxBufferSize|버퍼의 최대 크기를 지정하는 양의 정수입니다. 기본값은 524288입니다.|  
|proxyAddress|HTTP 프록시의 주소를 지정하는 URI입니다. `useSystemWebProxy`가 `true`일 경우 이 설정은 `null`이어야 합니다. 기본값은 `null`입니다.|  
|proxyAuthenticationScheme|HTTP 프록시가 처리하는 클라이언트 요청을 인증하는 데 사용되는 프로토콜을 지정합니다. 유효한 값은 다음과 같습니다.<br /><br /> -None: 인증이 수행 되지 않습니다.<br />다이제스트: 다이제스트 인증을 지정 합니다.<br />-Negotiate: 인증 체계를 결정 하는 클라이언트와 협상 합니다. 클라이언트와 서버 모두 Kerberos를 지원하면 이 인증 체계가 사용되고, 그렇지 않으면 NTLM이 사용됩니다.<br />-Ntlm: NTLM 인증을 지정 합니다.<br />-기본: 기본 인증을 지정 합니다.<br />-Anonymous: 익명 인증을 지정 합니다.<br />-IntegratedWindowsAuthentication: Windows 인증을 지정합니다.<br /><br /> 기본값은 Anonymous입니다. 이 특성은 <xref:System.Net.AuthenticationSchemes> 형식입니다.|  
|realm|프록시/서버에서 사용할 영역을 지정하는 문자열입니다. 기본값은 빈 문자열입니다.<br /><br /> 서버에서는 보호되는 리소스를 분할할 때 영역을 사용합니다. 각 파티션에는 자체 인증 체계 및/또는 권한 부여 데이터베이스가 있을 수 있습니다. 영역은 기본 및 다이제스트 인증에만 사용됩니다. 클라이언트가 성공적으로 인증되면 이 인증은 지정된 영역의 모든 리소스에 대해 유효합니다. 영역에 대 한 자세한 설명을에서 RFC 2617을 참조 하세요. http://www.ietf.org합니다.|  
|transferMode|메시지가 버퍼링되거나 스트리밍되는지 또는 요청이나 응답인지를 지정합니다. 유효한 값은 다음과 같습니다.<br /><br /> -Buffered: 요청 및 응답 메시지가 버퍼링 됩니다.<br />스트리밍: 요청 및 응답 메시지가 스트리밍됩니다.<br />-StreamedRequest: 요청 메시지는 스트리밍되고 응답 메시지는 버퍼링 됩니다.<br />-StreamedResponse: 요청 메시지는 버퍼링 하 고 응답 메시지는 스트리밍됩니다.<br /><br /> 기본값은 Buffered입니다. 이 특성은 <xref:System.ServiceModel.TransferMode> 형식입니다.|  
|unsafeConnectionNtlmAuthentication|서버에서 안전하지 않은 연결 공유를 사용할 수 있는지 여부를 지정하는 부울 값입니다. 기본값은 `false`입니다. 사용할 경우 각 TCP 연결에서 NTLM 인증이 한 번씩 수행됩니다.|  
|useDefaultWebProxy|사용자별 설정이 아닌 시스템 수준의 프록시 설정을 사용할지 여부를 지정하는 부울 값입니다. 기본값은 `true`입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<binding>](../../../../../docs/framework/misc/binding.md)|사용자 지정 바인딩의 모든 바인딩 기능을 정의합니다.|  
  
## <a name="remarks"></a>설명  
 `httpTransport` 요소는 HTTP 전송 프로토콜을 구현하는 사용자 지정 바인딩을 만들기 위한 시작점입니다. HTTP는 상호 운용성을 위해 사용되는 기본 전송입니다. 이 전송은 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)]에서 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 외의 다른 웹 서비스 스택과의 상호 운용성을 보장하기 위해 지원됩니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.ServiceModel.Configuration.HttpTransportElement>  
 <xref:System.ServiceModel.Channels.HttpTransportBindingElement>  
 <xref:System.ServiceModel.Channels.TransportBindingElement>  
 <xref:System.ServiceModel.Channels.CustomBinding>  
 [전송](../../../../../docs/framework/wcf/feature-details/transports.md)  
 [전송 선택](../../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)  
 [바인딩](../../../../../docs/framework/wcf/bindings.md)  
 [바인딩 확장](../../../../../docs/framework/wcf/extending/extending-bindings.md)  
 [사용자 지정 바인딩](../../../../../docs/framework/wcf/extending/custom-bindings.md)  
 [\<customBinding>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)
