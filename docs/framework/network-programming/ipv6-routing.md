---
title: "IPv6 라우팅"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c98731b4-b542-46a2-9947-1cea63c186b2
caps.latest.revision: "4"
author: mcleblanc
ms.author: markl
manager: markl
ms.workload: dotnet
ms.openlocfilehash: c7bfb79c5ab5406793a27f653b7e6a1abf2b2859
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/22/2017
---
# <a name="ipv6-routing"></a>IPv6 라우팅
유연한 라우팅 메커니즘은 IPv6의 장점입니다. IPv4 네트워크 ID가 할당된 방식으로 인해 인터넷 백본에 있는 라우터에서 대규모 라우팅 테이블을 유지해야 합니다. 이러한 라우터는 인터넷의 모든 노드로 방향이 지정되는 패킷을 전달하기 위해 모든 경로를 알고 있어야 합니다. 주소를 집계하는 기능을 통해 IPv6에서는 유연하게 주소를 지정할 수 있고 라우팅 테이블의 크기가 대폭 감소됩니다. 이 새로운 주소 지정 아키텍처에서는 적절하게 메시지를 전달하기 위해 중간 라우터를 통해 네트워크의 로컬 부분만 계속 추적해야 합니다.  
  
## <a name="neighbor-discovery"></a>네트워크 환경 검색  
 네트워크 환경 검색에서 제공하는 일부 기능은 다음과 같습니다.  
  
-   라우터 검색. 이 기능을 통해 로컬 라우터를 식별할 수 있습니다.  
  
-   주소 확인. 이 기능을 사용하면 노드에서 올바른 다음 홉 주의 링크-계층 주소를 확인할 수 있습니다(주소 확인 프로토콜 [ARP] 대체).  
  
-   주소 자동 구성. 이 기능을 사용하면 호스트에서 사이트-로컬 및 글로벌 주소를 자동으로 구성할 수 있습니다.  
  
 네트워크 환경 검색에서는 다음을 포함하는 ICMPv6(Internet Control Message Protocol for IPv6) 메시지를 사용합니다.  
  
-   라우터 알림. 의사(pseudo) 주기적으로 또는 라우터 요청에 대한 응답으로 라우터에서 전송합니다. IPv6 라우터에서는 라우터 알림을 사용하여 가용성, 주소 접두사 및 다른 매개 변수를 알립니다.  
  
-   라우터 요청. 링크의 라우터에서 라우터 알림을 즉시 보내도록 요청하기 위해 호스트에서 전송합니다.  
  
-   네트워크 환경 요청. 주소 확인, 중복 주소 검색 또는 네트워크 환경이 여전히 연결할 수 있는지 확인하기 위해 노드에서 전송합니다.  
  
-   네트워크 환경 알림. 네트워크 환경 요청에 응답하거나 링크 계층 주소 변경을 네트워크 환경에 알리기 위해 노드에서 전송합니다.  
  
-   리디렉션. 전송 노드의 특정 대상으로 더 유용한 다음 홉 주소를 알리기 위해 라우터에서 전송합니다.  
  
## <a name="see-also"></a>참고 항목  
 [인터넷 프로토콜 버전 6](../../../docs/framework/network-programming/internet-protocol-version-6.md)  
 [소켓](../../../docs/framework/network-programming/sockets.md)
