---
title: "작업 성능 카운터"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 333a51e0-f56e-4e1a-b359-5c91ff390568
caps.latest.revision: "7"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: f5724e32c61bb49c3251f4fd9785396e6c97f55f
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/22/2017
---
# <a name="operation-performance-counters"></a>작업 성능 카운터
작업 성능 카운터는 성능 모니터(Perfmon.exe)에서 볼 때 `ServiceModelOperation 4.0.0.0` 성능 개체 아래에 있습니다. 각 작업에는 개별 인스턴스가 있습니다. 즉, 지정된 계약에 10개의 작업이 있는 경우 10개의 작업 카운터 인스턴스가 해당 계약에 연결되어 있습니다. 개체 인스턴스 이름은 다음 패턴으로 지정됩니다.  
  
```  
(ServiceName).(ContractName).(OperationName)@(first endpoint listener address)  
```  
  
 이 카운터를 사용하면 호출이 사용되는 방법과 작업 진행 상태를 측정할 수 있습니다.  
  
> [!CAUTION]
>  성능 카운터 인스턴스의 이름 길이에는 제한이 있습니다. [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 카운터 인스턴스 이름이 최대 길이를 초과하면 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)]는 인스턴스 이름 부분을 해시 값으로 바꿉니다.  
  
## <a name="see-also"></a>참고 항목  
 [성능 카운터](../../../../../docs/framework/wcf/diagnostics/performance-counters/index.md)
