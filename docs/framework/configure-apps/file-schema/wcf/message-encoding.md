---
title: 메시지 인코딩
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f30ee941-aca9-4c67-82a5-421568496f07
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: b3040a16b6d167c4f066b2ddbd0a542741f88d62
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="message-encoding"></a>메시지 인코딩
인코딩은 유니코드 문자 집합을 바이트 시퀀스로 변환하는 프로세스입니다. 디코딩은 역프로세스입니다. WCF(Windows Communication Foundation)에서는 SOAP 메시지에 대해 텍스트, 이진 및 MTOM(Message Transmission Optimization Mechanism)이라는 세 가지 형식의 인코딩을 제공합니다.  
  
 `binaryMessageEncoding` 구성 섹션은 이진 기반 XML 메시지에 사용되는 문자 인코딩 및 메시지 버전 관리를 지정합니다. 이진 메시지 인코더는 통신 중에 WCF(Windows Communication Foundation) 메시지를 이진 형식으로 인코딩합니다. 이 인코딩은 전송 속도가 매우 빠르지만 WS-* 표준과 호환되지 않습니다.  
  
 `mtomMessageEncoding` 구성 섹션은 MTOM(Message Transmission Optimization Mechanism) 인코딩을 사용하는 메시지에 사용되는 문자 인코딩 및 메시지 버전 관리를 지정합니다. MTOM은 WCF(Windows Communication Foundation) 메시지의 이진 데이터를 효율적으로 전송하는 기술입니다. MTOM 인코더는 효율성과 상호 운용성 간의 균형을 유지하려고 합니다. MTOM 인코딩은 대부분의 XML을 텍스트 형식으로 전송하지만, 큰 이진 데이터 블록의 경우에는 텍스트로 변환하지 않고 있는 그대로 전송하여 최적화합니다.  
  
 `textMessageEncoding` 구성 섹션은 통신 중에 텍스트 기반 메시지를 만드는 데 사용되는 텍스트 인코더를 지정합니다. 이 인코더에서 생성하는 메시지는 WS-* 기반 interop과 호환됩니다. 웹 서비스 또는 웹 서비스 클라이언트는 일반적으로 텍스트 XML을 이해할 수 있습니다. 그러나 큰 이진 데이터 블록을 텍스트 형태로 전송하는 것은 가장 비효율적인 XML 메시지 인코딩 방법입니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.ServiceModel.Channels.CustomBinding>  
 <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>  
 [바인딩](../../../../../docs/framework/wcf/bindings.md)  
 [바인딩 확장](../../../../../docs/framework/wcf/extending/extending-bindings.md)  
 [사용자 지정 바인딩](../../../../../docs/framework/wcf/extending/custom-bindings.md)  
 [\<customBinding>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)  
 [메시지 인코더 선택](../../../../../docs/framework/wcf/feature-details/choosing-a-message-encoder.md)
