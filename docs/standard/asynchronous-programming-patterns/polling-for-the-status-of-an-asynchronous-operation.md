---
title: 비동기 작업의 상태에 대한 폴링
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: ''
ms.suite: ''
ms.technology: dotnet-standard
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- asynchronous programming, status polling
- polling asynchronous operation status
- status information [.NET Framework], asynchronous operations
ms.assetid: b541af31-dacb-4e20-8847-1b1ff7c35363
caps.latest.revision: ''
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 51e2ada4b493e8b1cbe0744c00fc2c25f9a266fb
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="polling-for-the-status-of-an-asynchronous-operation"></a>비동기 작업의 상태에 대한 폴링
비동기 작업의 결과를 기다리는 동안 다른 작업을 수행할 수 있는 응용 프로그램은 작업이 완료될 때까지 차단되면 안 됩니다. 다음 옵션 중 하나를 사용하여 비동기 작업이 완료될 때까지 대기하는 동안 명령을 계속 실행합니다.  
  
-   비동기 작업의 **Begin***OperationName* 메서드에서 반환한 <xref:System.IAsyncResult>의 <xref:System.IAsyncResult.IsCompleted%2A> 속성을 사용하여 해당 작업이 완료되었는지 여부를 확인합니다. 이 방법을 폴링이라고 하고 이 항목에서 이 방법을 설명합니다.  
  
-   <xref:System.AsyncCallback> 대리자를 사용하여 비동기 작업 결과를 별도의 스레드에서 처리합니다. 이 방법을 설명하는 예제는 [AsyncCallback 대리자를 사용하여 비동기 작업 종료](../../../docs/standard/asynchronous-programming-patterns/using-an-asynccallback-delegate-to-end-an-asynchronous-operation.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 다음 코드 예제는 <xref:System.Net.Dns> 클래스에서 비동기 메서드를 사용하여 사용자가 지정한 컴퓨터의 Domain Name System 정보를 검색하는 방법을 보여줍니다. 이 예제에서는 비동기 작업을 시작한 다음, 작업이 완료될 때까지 콘솔에서 마침표(“.”)를 인쇄합니다. 이 방법을 사용할 경우 이러한 인수가 필요하지 않기 때문에 <xref:System.Net.Dns.BeginGetHostByName%2A><xref:System.AsyncCallback> 및 <xref:System.Object> 매개 변수에 대해 **null**(Visual Basic의 **Nothing**)이 전달됩니다.  
  
 [!code-csharp[AsyncDesignPattern#3](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDesignPattern/CS/Async_Poll.cs#3)]
 [!code-vb[AsyncDesignPattern#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDesignPattern/VB/Async_Poll.vb#3)]  
  
## <a name="see-also"></a>참고 항목  
 [EAP(이벤트 기반 비동기 패턴)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)  
 [이벤트 기반 비동기 패턴 개요](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)
