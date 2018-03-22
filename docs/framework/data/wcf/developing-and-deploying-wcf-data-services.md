---
title: WCF Data Services 개발 및 배포
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework-oob
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- WCF Data Services, developing
- WCF Data Services, deploying
- deploying [WCF Data Services
- developing applications [WCF Data Services]
ms.assetid: 6557c0e3-5aea-4f6e-bc14-77ad317a168b
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 8abe23aebefadc68268aa1dada8474336b1f87e7
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="developing-and-deploying-wcf-data-services"></a>WCF Data Services 개발 및 배포
이 항목에서는 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]의 개발 및 배포에 대한 정보를 제공합니다. 에 대 한 자세한 기본 정보에 대 한 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)], 참조 [시작](../../../../docs/framework/data/wcf/getting-started-with-wcf-data-services.md) 및 [개요](../../../../docs/framework/data/wcf/wcf-data-services-overview.md)합니다.  
  
## <a name="developing-wcf-data-services"></a>WCF Data Services 개발  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 를 사용하여 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)]을 지원하는 데이터 서비스를 만들 때는 개발 과정에서 다음과 같은 기본 작업을 수행해야 합니다.  
  
1.  **데이터 모델 정의**  
  
     [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 에서는 관계형 데이터베이스부터 런타임에 바인딩된 데이터 형식에 이르기까지 다양한 데이터 원본의 데이터를 기반으로 데이터 모델을 정의할 수 있도록 다양한 데이터 서비스 공급자를 지원합니다. 자세한 내용은 참조 [데이터 서비스 공급자](../../../../docs/framework/data/wcf/data-services-providers-wcf-data-services.md)합니다.  
  
2.  **데이터 서비스 만들기**  
  
     가장 기본적인 데이터 서비스는 <xref:System.Data.Services.DataService%601> 클래스에서 상속하는 클래스를 엔터티 컨테이너의 네임스페이스로 정규화된 이름인 `T` 형식으로 노출합니다. 자세한 내용은 [Defining WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)의 개발 및 배포에 대한 정보를 제공합니다.  
  
3.  **데이터 서비스 구성**  
  
     기본적으로 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 는 엔터티 컨테이너에 의해 노출되는 리소스에 액세스할 수 없도록 설정되어 있습니다. <xref:System.Data.Services.DataServiceConfiguration> 인터페이스를 사용하면 리소스 및 서비스 작업에 대한 액세스를 구성하고 지원되는 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]버전을 지정할 수 있으며 일괄 처리 동작 또는 단일 응답 피드에 반환될 수 있는 최대 엔터티 수와 같은 서비스 전반적인 기타 동작을 정의할 수 있습니다. 자세한 내용은 참조 [데이터 서비스 구성](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md)합니다.  
  
 이 항목에서는 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)]를 사용하여 데이터 서비스의 개발 및 배포를 주로 다룹니다. 데이터를 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 피드로 노출할 수 있도록 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 에서 제공하는 유연성에 대한 자세한 내용은 [Defining WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)의 개발 및 배포에 대한 정보를 제공합니다.  
  
### <a name="choosing-a-development-web-server"></a>개발 웹 서버 선택  
 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 를 사용하여 WCF Data Services를 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 응용 프로그램 또는 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)]웹 사이트로 개발하는 경우 개발하는 중에 데이터 서비스를 실행할 웹 서버를 선택할 수 있습니다. 다음 웹 서버는 로컬 컴퓨터에서 데이터 서비스를 쉽게 테스트하고 디버깅할 수 있도록 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 와 통합됩니다.  
  
1.  **로컬 IIS 서버**  
  
     IIS(인터넷 정보 서비스)에서 실행되는 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 응용 프로그램 또는 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 웹 사이트인 데이터 서비스를 만들 때 로컬 컴퓨터에서 IIS를 사용하여 데이터 서비스를 개발하고 테스트하는 것이 좋습니다. IIS에서 데이터 서비스를 실행하면 디버깅하는 동안 HTTP 요청을 쉽게 추적할 수 있습니다. 또한 IIS에서 데이터 서비스에 필요한 파일, 데이터베이스 및 기타 리소스에 액세스하는 데 필요한 권한을 미리 결정할 수도 있습니다. IIS에서 데이터 서비스를 실행하려면 IIS 및 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 를 올바르게 설치하고 구성했는지 확인하고 파일 시스템 및 데이터베이스에 있는 IIS 계정에 액세스 권한을 부여해야 합니다. 자세한 내용은 [방법: IIS에서 실행되는 WCF Data Services 개발](../../../../docs/framework/data/wcf/how-to-develop-a-wcf-data-service-running-on-iis.md)을 참조하십시오.  
  
    > [!NOTE]
    >  관리자 권한으로 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 를 실행해야만 개발 환경을 사용하여 로컬 IIS 서버를 구성할 수 있습니다.  
  
2.  **Visual Studio 개발 서버**  
  
     [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 에는 기본 제공 웹 서버인 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 개발 서버가 포함되어 있으며 이 서버는 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 프로젝트의 기본 웹 서버입니다. 이 웹 서버는 개발 중에 로컬 컴퓨터에서 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 프로젝트를 실행하도록 디자인되었습니다. [WCF Data Services 퀵 스타트](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md) 에서는 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 개발 서버에서 실행되는 데이터 서비스를 만드는 방법을 보여 줍니다.  
  
     [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 개발 서버를 사용하여 데이터 서비스를 개발할 때 다음과 같은 제한 사항을 알고 있어야 합니다.  
  
    -   이 서버는 로컬 컴퓨터에서만 액세스할 수 있습니다.  
  
    -   이 서버는 HTTP 메시지의 기본 포트인 특정 포트(포트 80 제외)와 `localhost` 에서 수신 대기합니다. 자세한 내용은 [Visual Studio의 ASP.NET 웹 프로젝트에 대한 웹 서버](http://msdn.microsoft.com/library/31d4f588-df59-4b7e-b9ea-e1f2dd204328)를 참조하세요.  
  
    -   이 서버는 현재 사용자 계정의 컨텍스트에서 데이터 서비스를 실행합니다. 예를 들어, 관리자 수준의 사용자로 실행 중인 경우 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 개발 서버에서 실행되는 데이터 서비스는 관리자 수준의 권한을 가집니다. 따라서 데이터 서비스가 IIS 서버에 배포된 리소스 중 액세스 권한이 없는 리소스에도 액세스할 수 있습니다.  
  
    -   이 서버에는 인증과 같은 IIS의 추가 기능이 포함되어 있지 않습니다.  
  
    -   이 서버는 데이터 서비스에서 큰 이진 데이터에 액세스할 때 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 클라이언트가 기본적으로 보내는 청크된 HTTP 스트림을 처리할 수 없습니다. 자세한 내용은 참조 [스트리밍 공급자](../../../../docs/framework/data/wcf/streaming-provider-wcf-data-services.md)합니다.  
  
    -   URL의 마침표 문자(`.`)가 키 값에서 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 에 의해 지원되는 경우에도 이 서버에서 이 문자 처리와 관련된 문제가 발생합니다.  
  
    > [!TIP]
    >  개발 중에 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 개발 서버를 사용하여 데이터 서비스를 테스트할 수 있지만 IIS를 실행하는 웹 서버에 데이터 서비스를 배포한 후 다시 데이터 서비스를 테스트해야 합니다.  
  
3.  **Microsoft Azure 개발 환경**  
  
     [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 용 Microsoft Azure Tools에는 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)]에서 Microsoft Azure 서비스를 개발하는 데 사용할 수 있는 통합된 도구 집합이 포함되어 있습니다. 이 도구를 사용하면 Microsoft Azure에 배포할 수 있는 데이터 서비스를 개발하고, 배포하기 전에 로컬 컴퓨터에서 데이터 서비스를 테스트할 수 있습니다. [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 를 사용할 때 이 도구를 통해 Microsoft Azure 플랫폼에서 실행되는 데이터 서비스를 개발할 수 있습니다. [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] Microsoft 다운로드 센터 [에서](http://go.microsoft.com/fwlink/?LinkID=201848)용 Windows Azure 도구를 다운로드할 수 있습니다. Windows Azure에서 실행되는 데이터 서비스 개발[!INCLUDE[crabout](../../../../includes/crabout-md.md)] 은 [Windows Azure에서 OData 서비스 배포](http://go.microsoft.com/fwlink/?LinkId=201847)게시물을 참조하십시오.  
  
### <a name="development-tips"></a>개발 팁  
 데이터 서비스를 개발할 때 다음 사항을 고려해야 합니다.  
  
-   사용자를 인증하거나 특정 사용자의 액세스를 제한하려는 경우 데이터 서비스의 보안 요구 사항을 확인해야 합니다. 자세한 내용은 [Securing WCF Data Services](../../../../docs/framework/data/wcf/securing-wcf-data-services.md)을 참조하세요.  
  
-   HTTP 검사 프로그램은 요청 및 응답 메시지의 내용을 검사할 수 있도록 하여 데이터 서비스를 디버깅할 때 아주 유용할 수 있습니다. 원시 패킷을 표시할 수 있는 네트워크 패킷 분석기를 사용하여 데이터 서비스와 주고받는 HTTP 요청 및 응답을 검사할 수 있습니다.  
  
-   일반적인 작업을 수행할 때보다 데이터 서비스를 디버깅할 때 데이터 서비스에서 발생하는 오류에 대한 자세한 정보가 필요할 수 있습니다. <xref:System.Data.Services.DataServiceConfiguration.UseVerboseErrors%2A> 에서 <xref:System.Data.Services.DataServiceConfiguration> 속성을 `true` 로 설정하고 데이터 서비스 클래스에서 <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A> 특성의 <xref:System.ServiceModel.Description.ServiceDebugBehavior> 속성을 `true`로 설정하여 데이터 서비스에서 추가 오류 정보를 가져올 수 있습니다. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] 은 [WCF Data Services 디버깅](http://go.microsoft.com/fwlink/?LinkId=201868)게시물을 참조하세요. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 에서 추적 기능을 설정하여 HTTP 메시징 계층에서 발생하는 예외를 확인할 수도 있습니다. 자세한 내용은 [Configuring Tracing](../../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md)을 참조하세요.  
  
-   일반적으로 데이터 서비스는 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 응용 프로그램 프로젝트로 개발되지만 데이터 서비스를 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 에서 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)]웹 사이트 프로젝트로 만들 수도 있습니다. 두 가지 프로젝트 유형의 차이점에 대 한 정보를 참조 하십시오. [NIB: 웹 응용 프로그램 프로젝트와 Visual Studio에서 웹 사이트 프로젝트 비교](http://msdn.microsoft.com/library/2861815e-f5a2-4378-a2f8-b8a86dc012f5)합니다.  
  
-   **에서** 새 항목 추가 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)]대화 상자를 사용하여 데이터 서비스를 만들면 데이터 서비스는 IIS에서 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 에 의해 호스트됩니다. [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 및 IIS가 데이터 서비스의 기본 호스트지만 다른 호스팅 옵션도 지원됩니다. 자세한 내용은 참조 [데이터 서비스 호스팅](../../../../docs/framework/data/wcf/hosting-the-data-service-wcf-data-services.md)합니다.  
  
## <a name="deploying-wcf-data-services"></a>WCF Data Services 배포  
 WCF Data Services에서는 데이터 서비스를 호스트하는 프로세스를 유연성 있게 선택할 수 있도록 합니다. [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 를 사용하여 데이터 서비스를 다음 플랫폼에 배포할 수 있습니다.  
  
-   **IIS에서 호스트되는 웹 서버**  
  
     데이터 서비스를 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 프로젝트로 개발하는 경우 표준 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 배포 프로세스를 사용하여 IIS 웹 서버에 배포할 수 있습니다.  [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 는 배포 중인 데이터 서비스를 호스트하는 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]프로젝트의 종류에 따라 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 에 대해 다음과 같은 배포 기술을 제공합니다.  
  
    -   **ASP.NET 웹 응용 프로그램을 위한 배포 기술**  
  
        -   [웹 배포 패키지](http://msdn.microsoft.com/library/1f9713c8-9540-494c-b80d-9893b970ad6f)  
  
        -   [One-click 게시](http://msdn.microsoft.com/library/59226246-99ad-4aec-975d-7c61e8a8911c)  
  
    -   **ASP.NET 웹 사이트를 위한 배포 기술**  
  
        -   [웹 사이트 복사 도구](http://msdn.microsoft.com/library/b819aed4-014b-427e-be80-02317b1bb003)  
  
        -   [웹 사이트 게시 도구](http://msdn.microsoft.com/library/d0a1a20f-15be-4940-9485-cb8e4aa8181b)  
  
        -   [XCopy](http://msdn.microsoft.com/library/4312c651-2119-49be-bbeb-ee28bdbfe71e)  
  
     [!INCLUDE[crabout](../../../../includes/crabout-md.md)]배포 옵션에 대 한 프로그램 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 응용 프로그램 참조 [Visual Studio 및 ASP.NET에 대 한 웹 배포 개요](http://msdn.microsoft.com/library/99bd1927-b59f-4e02-87b4-55c6ba2adbc3)합니다.  
  
    > [!TIP]
    >  데이터 서비스를 IIS에 배포하기 전에 IIS가 실행 중인 웹 서버로의 배포를 테스트했는지 확인해야 합니다. 자세한 내용은 [방법: IIS에서 실행되는 WCF Data Services 개발](../../../../docs/framework/data/wcf/how-to-develop-a-wcf-data-service-running-on-iis.md)을 참조하십시오.  
  
-   **Windows Azure**  
  
     [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)]용 Microsoft Azure Tools를 사용하여 데이터 서비스를 Microsoft Azure에 배포할 수 있습니다. [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] Microsoft 다운로드 센터 [에서](http://go.microsoft.com/fwlink/?LinkID=201848)용 Windows Azure 도구를 다운로드할 수 있습니다. Windows Azure에 데이터 서비스를 배포하는[!INCLUDE[crabout](../../../../includes/crabout-md.md)] 은 [Windows Azure에서 OData 서비스 배포](http://go.microsoft.com/fwlink/?LinkId=201847)를 참조하세요.  
  
### <a name="deployment-considerations"></a>배포 고려 사항  
 데이터 서비스를 배포할 때 다음 사항을 고려해야 합니다.  
  
-   [!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)] 공급자를 사용하는 데이터 서비스를 배포하여 SQL Server 데이터베이스에 액세스하는 경우 데이터 서비스 배포와 함께 데이터 구조, 데이터 또는 둘 다를 전파해야 할 수 있습니다. [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 는 대상 데이터베이스에서 이 작업을 수행하기 위해 스크립트(.sql 파일)를 자동으로 만들 수 있으며, 이러한 스크립트는 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 응용 프로그램의 웹 배포 패키지에 포함할 수 있습니다. 자세한 내용은 참조 [NIB: 방법:는 데이터베이스와 웹 응용 프로그램 프로젝트를 배포](http://msdn.microsoft.com/library/683b33f1-8a3d-45cf-af6e-61ab50fc518b)합니다. [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 웹 사이트의 경우에는 **의** 데이터베이스 게시 마법사 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)]를 사용하여 이 작업을 수행할 수 있습니다. 자세한 내용은 [데이터베이스 게시 마법사를 사용 하 여 데이터베이스 배포](http://msdn.microsoft.com/library/1e3682e7-8b57-4da6-a393-af9640ccf8b7)을 참조하세요.  
  
-   [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 에는 기본 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 구현이 포함되기 때문에 Windows Server AppFabric을 사용하여 Windows Server에서 실행되는 IIS에 배포된 데이터 서비스를 모니터링할 수 있습니다. Windows Server AppFabric을 사용하여 데이터 서비스를 모니터링[!INCLUDE[crabout](../../../../includes/crabout-md.md)] 은 [Windows Server AppFabric으로 WCF Data Services 추적](http://go.microsoft.com/fwlink/?LinkID=202005)게시물을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 서비스 호스팅](../../../../docs/framework/data/wcf/hosting-the-data-service-wcf-data-services.md)  
 [WCF Data Services 보안](../../../../docs/framework/data/wcf/securing-wcf-data-services.md)  
 [WCF Data Services 정의](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)
