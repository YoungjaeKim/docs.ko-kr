---
title: 데이터 서비스 만들기
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework-oob
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- csharp
- vb
ms.assetid: 34d1d971-5e18-4c22-9bf6-d3612e27ea59
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 7d890e4c2041ae4c70a79adfc0ab4141402fcd3f
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="creating-the-data-service"></a>데이터 서비스 만들기
이 작업을 사용 하는 샘플 데이터 서비스 만듭니다 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 노출 하는 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] Northwind 샘플 데이터베이스를 기반으로 하는 피드입니다. 작업에 필요한 기본 단계는 다음과 같습니다.  
  
1.  [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 웹 응용 프로그램을 만듭니다.  
  
2.  [!INCLUDE[adonet_edm](../../../../includes/adonet-edm-md.md)] 도구를 사용하여 데이터 모델을 정의합니다.  
  
3.  웹 응용 프로그램에 데이터 서비스를 추가합니다.  
  
4.  데이터 서비스에 액세스할 수 있도록 설정합니다.  
  
> [!NOTE]
>  이 작업을 완료할 때 만드는 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 웹 응용 프로그램은 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]에서 제공하는 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] Development Server에서 실행됩니다. [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] Development Server는 로컬 컴퓨터에서의 액세스만 지원합니다. 개발 중에 보다 쉽게 데이터 서비스를 테스트하고 관련 문제를 해결하려면 IIS(인터넷 정보 서비스)를 사용하여 데이터 서비스를 호스트하는 응용 프로그램을 실행하는 것이 좋습니다. 자세한 내용은 [방법: IIS에서 실행되는 WCF Data Services 개발](../../../../docs/framework/data/wcf/how-to-develop-a-wcf-data-service-running-on-iis.md)을 참조하십시오.  
  
### <a name="to-create-the-aspnet-web-application"></a>ASP.NET 웹 응용 프로그램을 만들려면  
  
1.  [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)]의 **파일** 메뉴 선택 **새로**, 선택한 후 **프로젝트**합니다.  
  
2.  에 **새 프로젝트** 대화 상자에서 아래에서 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 또는 [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 선택의 **웹** 템플릿을 선택한 다음 선택 **ASP.NET 웹 응용 프로그램**합니다.  
  
    > [!NOTE]
    >  [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] Web Developer를 사용하는 경우 새 웹 응용 프로그램 대신 새 웹 사이트를 만들어야 합니다.  
  
3.  형식 `NorthwindService` 프로젝트의 이름으로 합니다.  
  
4.  **확인**을 클릭합니다.  
  
5.  (선택 사항) 웹 응용 프로그램의 특정 포트 번호를 지정합니다. 참고: 포트 번호 `12345`가 퀵 스타트의 나머지 부분에서 사용됩니다.  
  
    1.  **솔루션 탐색기**의 이름을 마우스 오른쪽 단추로 클릭는 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 프로젝트 방금 만든 마우스 클릭 **속성**합니다.  
  
    2.  선택은 **웹** 탭의 값을 설정 하 고는 **특정 포트** 입력란을 `12345`합니다.  
  
### <a name="to-define-the-data-model"></a>데이터 모델을 정의하려면  
  
1.  **솔루션 탐색기**의 이름을 마우스 오른쪽 단추로 클릭는 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 프로젝트를 마우스 클릭 **새 항목 추가 합니다.**  
  
2.  에 **새 항목 추가** 대화 상자를 클릭는 **데이터** 템플릿을 선택한 후 **ADO.NET 엔터티 데이터 모델**합니다.  
  
3.  데이터 모델의 이름으로 입력 `Northwind.edmx`합니다.  
  
4.  에 [!INCLUDE[adonet_edm](../../../../includes/adonet-edm-md.md)] 마법사 **데이터베이스에서 생성**, 클릭 하 고 **다음**합니다.  
  
5.  다음 단계 중 하나를 수행 하 여 데이터 모델 데이터베이스에 연결 하 고 클릭 **다음**:  
  
    -   데이터베이스 연결이 이미 구성 되어 있으면 클릭 **새 연결** 고 새 연결을 만듭니다. 자세한 내용은 참조 [하는 방법: SQL Server 데이터베이스에 대 한 연결 만들기](http://go.microsoft.com/fwlink/?LinkId=123631)합니다. 이 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] 인스턴스에는 Northwind 샘플 데이터베이스가 연결되어 있어야 합니다.  
  
         \- 또는 -  
  
    -   Northwind 데이터베이스에 연결할 수 있도록 데이터베이스 연결이 이미 구성되어 있는 경우 연결 목록에서 해당 연결을 선택합니다.  
  
6.  마법사의 마지막 페이지에서 데이터베이스의 모든 테이블에 대한 확인란을 선택하고 뷰 및 저장 프로시저에 대한 확인란의 선택을 취소합니다.  
  
7.  클릭 **마침** 마법사를 닫습니다.  
  
    > [!NOTE]
    >  생성된 이 데이터 모델은 엔터티 형식의 외래 키 속성을 노출합니다. [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 2008을 사용하여 만들어진 데이터 모델에는 이러한 외래 키 속성이 포함되지 않습니다. 이 때문에 이 버전의 Northwind 데이터 서비스에 액세스하기 전에 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 2008을 사용하여 만들어진 Northwind 데이터 서비스에 액세스하기 위해 만들어진 모든 클라이언트 응용 프로그램의 클라이언트 데이터 서비스 클래스를 업데이트해야 합니다.  
  
### <a name="to-create-the-data-service"></a>데이터 서비스를 만들려면  
  
1.  **솔루션 탐색기**의 이름을 마우스 오른쪽 단추로 클릭 하면 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 프로젝트를 마우스 클릭 **새 항목 추가**합니다.  
  
2.  에 **새 항목 추가** 대화 상자에서 **WCF 데이터 서비스**합니다.  
  
3.  서비스의 이름으로 입력 `Northwind`합니다.  
  
     [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)]에서 새 서비스의 XML 태그와 코드 파일이 만들어집니다. 기본적으로 코드 편집기 창이 열립니다. **솔루션 탐색기**, 서비스 이름은, 확장명을 갖습니다. svc.cs 또는. svc.vb 합니다.  
  
4.  데이터 서비스 코드에서 데이터 서비스를 정의하는 클래스 정의의 `/* TODO: put your data source class name here */` 주석을 데이터 모델의 엔터티 컨테이너인 형식(이 경우 `NorthwindEntities`)으로 바꿉니다. 클래스 정의는 다음과 같이 나타납니다.  
  
     [!code-csharp[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria quickstart service/cs/northwind.svc.cs#servicedefinition)]
     [!code-vb[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria quickstart service/vb/northwind.svc.vb#servicedefinition)]  
  
### <a name="to-enable-access-to-data-service-resources"></a>데이터 서비스 리소스에 액세스할 수 있도록 설정하려면  
  
1.  데이터 서비스 코드에서 `InitializeService` 함수의 자리 표시자 코드를 다음 코드로 바꿉니다.  
  
     [!code-csharp[Astoria Quickstart Service#AllReadConfig](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria quickstart service/cs/northwind.svc.cs#allreadconfig)]
     [!code-vb[Astoria Quickstart Service#AllReadConfig](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria quickstart service/vb/northwind.svc.vb#allreadconfig)]  
  
     이렇게 하면 권한 있는 클라이언트가 지정된 엔터티 집합의 리소스에 대한 읽기 및 쓰기 액세스 권한을 가질 수 있습니다.  
  
    > [!NOTE]
    >  [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 응용 프로그램에 액세스할 수 있는 클라이언트는 데이터 서비스에 의해 노출되는 리소스에도 액세스할 수 있습니다. 리소스에 무단으로 액세스할 수 없도록 하려면 프로덕션 데이터 서비스에서 응용 프로그램 자체에도 보안을 설정해야 합니다. 자세한 내용은 [Securing WCF Data Services](../../../../docs/framework/data/wcf/securing-wcf-data-services.md)을 참조하세요.  
  
## <a name="next-steps"></a>다음 단계  
 노출 하는 새 데이터 서비스를 성공적으로 만들었습니다는 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] Northwind 샘플 데이터베이스를 기반으로 하는 피드 액세스에 대 한 사용 권한이 있는 클라이언트에 대 한 피드를 사용 하도록 설정한는 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 웹 응용 프로그램입니다. 데이터 서비스를 시작 합니다 다음으로 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 및가 액세스 하 고는 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 웹 브라우저를 통해 HTTP GET 요청을 제출 하 여 피드:  
  
 [웹 브라우저에서 서비스 액세스](../../../../docs/framework/data/wcf/accessing-the-service-from-a-web-browser-wcf-data-services-quickstart.md)  
  
## <a name="see-also"></a>참고 항목  
 [ADO.NET 엔터티 데이터 모델 도구](http://msdn.microsoft.com/library/91076853-0881-421b-837a-f582f36be527)
