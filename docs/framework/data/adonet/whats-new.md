---
title: 어떤&#39;ADO.NET의 새로운 s
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-ado
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3bb65d38-cce2-46f5-b979-e5c505e95e10
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload:
- dotnet
ms.openlocfilehash: fb23f329906e21f3d8558139075c5f575f2f13bd
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/23/2018
---
# <a name="what39s-new-in-adonet"></a>어떤&#39;ADO.NET의 새로운 s
다음은 [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)]에서 [!INCLUDE[net_v45](../../../../includes/net-v45-md.md)]의 새로운 기능입니다.  
  
## <a name="sqlclient-data-provider"></a>SqlClient Data Provider  
 다음은 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]에서 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] Data Provider for [!INCLUDE[net_v45](../../../../includes/net-v45-md.md)]의 새로운 기능입니다.  
  
-   ConnectRetryCount 및 ConnectRetryInterval 연결 문자열 키워드(<xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>)를 사용하면 유휴 연결 복원 기능을 제어할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]에서 응용 프로그램으로의 스트리밍 지원은 서버의 데이터가 구조화되지 않는 시나리오를 지원합니다.  참조 [SqlClient 스트리밍 지원](../../../../docs/framework/data/adonet/sqlclient-streaming-support.md) 자세한 정보에 대 한 합니다.  
  
-   비동기 프로그래밍에 대한 지원이 추가되었습니다.  참조 [비동기 프로그래밍](../../../../docs/framework/data/adonet/asynchronous-programming.md) 자세한 정보에 대 한 합니다.  
  
-   이제 연결 실패가 확장 이벤트 로그에 기록됩니다. 자세한 내용은 [ADO.NET의 데이터 추적](../../../../docs/framework/data/adonet/data-tracing.md)을 참조하세요.  
  
-   이제 SqlClient에 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]의 고가용성, 재해 복구 기능, AlwaysOn에 대한 지원이 포함되어 있습니다. 자세한 내용은 참조 [고가용성, 재해 복구에 대 한 SqlClient 지원](../../../../docs/framework/data/adonet/sql/sqlclient-support-for-high-availability-disaster-recovery.md)합니다.  
  
-   <xref:System.Security.SecureString> 인증을 사용할 때 암호를 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]으로 전달할 수 있습니다. 자세한 내용은 <xref:System.Data.SqlClient.SqlCredential>를 참조하세요.  
  
-   `TrustServerCertificate`가 false이고 `Encrypt`가 true인 경우 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] SSL 인증서의 서버 이름 또는 IP 주소는 연결 문자열에 지정된 서버 이름 또는 IP 주소와 정확하게 일치해야 합니다. 그렇지 않으면 연결을 시도할 경우 실패합니다. 자세한 내용은 `Encrypt`의 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> 연결 옵션에 대한 설명을 참조하세요.  
  
     이러한 변경으로 인해 기존 응용 프로그램이 더 이상 연결되지 않는 경우 다음 중 하나를 사용하여 응용 프로그램을 수정하면 됩니다.  
  
    -   CN(일반 이름) 또는 SAN(주체 대체 이름) 필드에 약식 이름을 지정하는 인증서를 발급합니다. 이 방법은 데이터베이스 미러링에 적용됩니다.  
  
    -   정규화된 도메인 이름에 약식 이름을 매핑하는 별칭을 추가합니다.  
  
    -   연결 문자열에서 정규화된 도메인 이름을 사용합니다.  
  
-   SqlClient는 확장된 보호를 지원합니다. 확장 된 보호에 대 한 자세한 내용은 참조 [는 데이터베이스를 사용 하 여 확장 된 보호 엔진에 연결](http://go.microsoft.com/fwlink/?LinkId=219978)합니다.  
  
-   SqlClient는 LocalDB 데이터베이스에 대한 연결을 지원합니다. 자세한 내용은 참조 [LocalDB에 대 한 SqlClient 지원](../../../../docs/framework/data/adonet/sql/sqlclient-support-for-localdb.md)합니다.  
  
-   `Type System Version=SQL Server 2012;`는 `Type System Version` 연결 속성에 전달되는 새로운 값입니다. `Type System Version=Latest;` 값은 더 이상 사용되지 않으며 `Type System Version=SQL Server 2008;`과 동일해졌습니다. 자세한 내용은 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>을 참조하세요.  
  
-   SqlClient에서는 SQL Server 2008에 추가된 기능인 스파스 열에 대한 추가 지원을 제공합니다. 응용 프로그램이 이미 스파스 열을 사용하는 테이블의 데이터에 액세스하는 경우 성능이 향상됩니다. <xref:System.Data.SqlClient.SqlDataReader.GetSchemaTable%2A>의 IsColumnSet 열은 해당 열이 열 집합의 멤버인 스파스 열인지 여부를 나타냅니다. <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A> 열이 스파스 열인지 여부를 나타냅니다 (참조 [SQL Server 스키마 컬렉션](../../../../docs/framework/data/adonet/sql-server-schema-collections.md) 자세한 정보에 대 한). 스파스 열에 대 한 자세한 내용은 참조 [스파스 열 사용](http://go.microsoft.com/fwlink/?LinkId=224244)합니다.  
  
-   공간 데이터 형식이 포함되어 있는 Microsoft.SqlServer.Types.dll 어셈블리가 버전 10.0에서 버전 11.0으로 업그레이드되었습니다. 이 어셈블리를 참조하는 응용 프로그램은 제대로 실행되지 않을 수 있습니다. 자세한 내용은 참조 [데이터베이스 엔진 기능의 주요 변경 내용](http://go.microsoft.com/fwlink/?LinkId=224367)합니다.  
  
## <a name="adonet-entity-framework"></a>ADO.NET Entity Framework  
 [!INCLUDE[net_v45](../../../../includes/net-v45-md.md)]에는 Entity Framework 5.0을 사용할 경우 새로운 시나리오를 사용할 수 있게 하는 API가 추가되었습니다. Entity Framework 5.0에 추가 된 기능과 개선 사항에 대 한 자세한 내용은 다음 항목을 참조 하십시오.: [새로운](http://go.microsoft.com/fwlink/?LinkID=251106) 및 [Entity Framework 릴리스 및 버전 관리](http://go.microsoft.com/fwlink/?LinkId=234899)합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ADO.NET](../../../../docs/framework/data/adonet/index.md)  
 [ADO.NET 개요](../../../../docs/framework/data/adonet/ado-net-overview.md)  
 [SQL Server 및 ADO.NET](../../../../docs/framework/data/adonet/sql/index.md)  
 [WCF Data Services의 새로운 기능](http://msdn.microsoft.com/library/cf22cad5-b8d9-472b-8d7c-b863b64eaae8)  
 [ADO.NET 관리되는 공급자 및 데이터 집합 개발자 센터](http://go.microsoft.com/fwlink/?LinkId=217917)
