---
title: '완화: 풀 차단 기간'
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-bcl
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 92d2de20-79be-4df1-b182-144143a8866a
caps.latest.revision: ''
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 42eaddeb2714a8c294f45d24eb7e6d9cf216fecc
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="mitigation-pool-blocking-period"></a>완화: 풀 차단 기간
Azure SQL 데이터베이스 연결에 대한 연결 풀 차단 기간이 제거되었습니다.  
  
## <a name="additional-description"></a>추가 설명  
 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] 및 이전 버전에서 데이터베이스에 연결할 때 응용 프로그램에 일시적인 연결 오류가 발생할 경우, 연결 풀이 오류를 캐시하고 5초에서 1분 동안 다시 throw하기 때문에 연결 시도는 신속하게 다시 시도될 수 없습니다. 자세한 내용은 [SQL Server 연결 풀링(ADO.NET)](../../../docs/framework/data/adonet/sql-server-connection-pooling.md)을 참조하십시오. 이 동작은 일반적으로 몇 초 내에 복구되는 일시적인 오류가 자주 발생하는 Azure SQL 데이터베이스에 대한 연결 문제가 있습니다. 연결 풀 차단 기능은 데이터베이스를 사용할 수 있어도 광범위한 기간 동안 응용 프로그램 데이터베이스에 연결할 수 없다는 것을 의미합니다. 이 동작은 Azure SQL 데이터베이스에 연결하고 몇 초 안에 렌더링해야 하는 웹 응용 프로그램에 대해 특히 문제가 됩니다.  
  
 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]부터는 알려진 Azure SQL 데이터베이스(*.database.windows.net, \*.database.chinacloudapi.cn, \*.database.usgovcloudapi.net, \*.database.cloudapi.de)에 대한 연결 열기 요청의 경우 연결 열기 오류가 캐시되지 않습니다. 다른 모든 연결 시도의 경우 연결 풀 차단 기간이 계속 적용됩니다.  
  
## <a name="impact"></a>영향  
 이 변경은 Azure SQL 데이터베이스에 대한 연결 열기 시도를 즉시 다시 시도하도록 하여 클라우드 지원 응용 프로그램의 성능을 향상시킵니다.  
  
## <a name="mitigation"></a>완화  
 이 변경으로 인해 문제가 발생하는 앱의 경우 새로운 <xref:System.Data.SqlClient.SqlConnectionStringBuilder.PoolBlockingPeriod%2A> 속성을 설정하여 연결 풀 차단 기간을 구성할 수 있습니다.  속성의 값은 다음의 세 값 중 하나를 사용할 수 있는 <xref:System.Data.SqlClient.PoolBlockingPeriod?displayProperty=nameWithType> 열거형의 멤버입니다.  
  
-   `PoolBlockingPeriod.AlwaysBlock` 
  
-   `PoolBlockingPeriod.Auto`  
  
-   `PoolBlockingPeriod.NeverBlock` 
  
 <xref:System.Data.SqlClient.SqlConnectionStringBuilder.PoolBlockingPeriod%2A> 속성을 `PoolBlockingPeriod.AlwaysBlock`으로 설정하여 이전 동작을 복원할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [런타임 변경 내용](../../../docs/framework/migration-guide/runtime-changes-in-the-net-framework-4-6-2.md)
