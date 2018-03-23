---
title: WCF 서비스 게시
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c806b253-cd47-4b96-b831-e73cbf08808f
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 823edadf7d387d1a509edbdf839ac6eeece5d41f
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/23/2018
---
# <a name="wcf-service-publishing"></a>WCF 서비스 게시
[!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 서비스 게시는 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 서비스 호스트 및 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 테스트 클라이언트에서 제공하는 초기 개발 환경에서부터 테스트 목적으로 프로덕션 환경에 응용 프로그램을 실제로 배포하는 것에 이르기까지 프로세스를 진행하도록 도와 줍니다. 최종 배포 계획에 커밋하기 전에 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 서비스 게시를 사용하여 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 서비스가 올바르게 수행되고 게시할 준비가 되었는지 확인할 수 있습니다. 또한 테스트 목적으로 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 서비스 라이브러리를 여러 대상 위치에 배포할 수도 있습니다.  
  
## <a name="supported-services-and-target-locations"></a>지원되는 서비스 및 대상 위치  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 서비스 게시에서는 다음과 같은 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 서비스 라이브러리 템플릿 집합과 해당하는 항목 템플릿에서 만든 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 서비스를 게시할 수 있습니다.  
  
-   [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 서비스 라이브러리 템플릿과 항목 템플릿  
  
-   배포 서비스 라이브러리  
  
 이러한 서비스 템플릿을 선택 하 여 찾을 수 있습니다 **파일** -> **새 프로젝트** -> **Visual Basic** 또는 **Visual C#**  ->  **WCF**합니다. 사용 하 여 게시할 수 있습니다 (WCF 워크플로 서비스 응용 프로그램 및 WCF 서비스 응용 프로그램 포함)이이 위치에서 다른 WCF 템플릿을 [One-click 웹 응용 프로그램에 대 한 게시](https://msdn.microsoft.com/library/dd465337\(v=vs.110\).aspx)합니다.  
  
 다음과 같은 대상 위치에 서비스를 게시할 수 있습니다.  
  
-   로컬 IIS  
  
-   파일 시스템  
  
-   FTP 사이트  
  
## <a name="using-wcf-service-publishing"></a>WCF 서비스 게시 사용  
 서비스 구현을 배포하려면 다음 단계를 수행합니다.  
  
1.  상승 된 권한으로 Visual Studio를 엽니다 (실행 파일을 마우스 오른쪽 단추로 클릭 하 고 유틸리티를 실행 하려면 "관리자 권한으로 실행"을 사용 하 여).  이상 버전에서는 사용 하 여 "IIS 메타 베이스 및 iis 6 구성 호환성" 구성 요소를 설치 했는지를 확인 또는 IIS 7.0을 사용 하는 경우 "' Windows 기능 사용 설정 하거나 해제" 제어판에서.  
  
2.  서비스 프로젝트를 열고, 선택 **빌드**->**게시 \<프로젝트 이름 >** 주 메뉴에서에서 프로젝트를 마우스 오른쪽 단추로 클릭 하거나 **솔루션 탐색기**클릭 **게시**합니다.  
  
3.  **게시** 창이 나타납니다. 클릭는 **...** . 단추를 클릭하여 서비스를 배포할 대상 위치를 지정합니다. 로컬 IIS, 파일 시스템 또는 FTP 사이트에 응용 프로그램을 배포 하도록 선택할 수 있습니다. 로컬 IIS에 응용 프로그램을 배포할 경우 웹 사이트를 선택 하 고, 대상 웹 응용 프로그램을 클릭 하 여 만들 수는 **새 웹 응용 프로그램 만들기** 오른쪽 위 모퉁이에서 아이콘입니다.  
  
4.  클릭 한 후 **게시** 주 창에서 Visual Studio 응용 프로그램을 지정한 대상 위치에 배포 및 대상 디렉터리에 Web.config,.svc 및 어셈블리 파일을 복사 합니다. 이어야 합니다. .Svc의 이름은 됩니다 "projectname.servicename.svc"입니다. 서비스를 성공적으로 게시 된 후에 Visual Studio 출력 창의 "연결 하는 하이퍼링크"http://localhost/WebApplicationFolderName"http://localhost/WebApplicationFolderName..."와 비슷합니다는 옥을 찾을 수 있습니다. Ctrl 키를 누르고 링크를 클릭하여 Visual Studio 내에서 브라우저 페이지를 열고 서비스 디렉터리 구조를 볼 수 있습니다.  
  
     사이트를 찾을 수 없으면 IIS에서 디렉터리 브라우저를 사용하도록 설정되지 않았을 수 있습니다. 사용 하도록 설정 하려면 "가능한 해결 방법" 섹션의 팁을 따르십시오. 하이퍼링크 "http://localhost/WebApplicationFolderName" http://localhost/WebApplicationFolderName/ProjectName.ServiceName.svc 또는 있습니다 직접 입력할 수"" 서비스 페이지를 표시 합니다.  
  
 사용할 수 있습니다 **게시** 을 어셈블리, 구성 및 대상 위치에 프로젝트에 정의 된 모든 서비스에 대 한.svc 파일을 복사 하려면 지정한 대상에 기존 파일을 덮어씁니다.  
  
 응용 프로그램을 로컬 IIS에 배포하도록 선택하면 IIS 설치와 관련된 오류가 발생할 수 있습니다. IIS가 제대로 설치되었는지 확인하세요. 브라우저에서 "하이퍼링크"http://localhost"http://localhost"를 입력 하 고 IIS 기본 페이지가 표시 되는지 여부를 확인 합니다.  경우에 따라 IIS에서 ASP.NET 또는 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]의 잘못된 등록 때문에 문제가 발생할 수도 있습니다. Visual Studio 명령 프롬프트를 열고 및 ASP.NET 등록 문제를 해결 하는 명령 "aspnet_regiis.exe-ir"를 실행 하거나 "ServiceModelReg.exe – ia" 명령을 실행 하는 WCF 등록 문제를 해결 수 있습니다.  
  
## <a name="files-generated-for-publishing"></a>게시를 위해 생성되는 파일  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 서비스 라이브러리가 웹 호스트되기 전에 도구에서 어셈블리 파일, Web.config 파일 및 .svc 파일이 생성됩니다. 이러한 파일이 모두 대상 위치에 복사된 후에 서비스가 게시됩니다.  
  
### <a name="assembly-files"></a>어셈블리 파일  
 이 도구를 사용하여 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 서비스를 게시하면 먼저 서비스가 자동으로 빌드되고 빌드 후에 서비스 프로젝트에서 어셈블리 파일이 생성됩니다.  
  
### <a name="svc-file"></a>.SVC 파일  
 게시 작업에서는 각 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 서비스에 대해 버전 유효성 확인을 위해 *.svc 파일이 기존에 있는지 여부와 관계없이 생성됩니다. [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 서비스 라이브러리 및 배포 서비스 라이브러리용과 순차 및 상태 시스템 워크플로 서비스 라이브러리용의 서로 다른 두 가지 svc 파일이 있습니다. 생성 된 \*.svc 파일은 대상 위치의 루트 폴더로 복사 합니다.  
  
### <a name="webconfig-file"></a>Web.config 파일  
 서비스 프로젝트를 특정 대상 위치에 게시할 때마다 Web.config 파일이 만들어집니다.  
  
 생성된 Web.config 파일에는 웹 호스팅에 사용되는 웹 섹션 및 다음과 같은 변경 내용과 함께 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 서비스 라이브러리에 대한 App.config의 내용이 포함됩니다.  
  
-   기본 주소는 제외됩니다.  
  
-   `<diagnostics>` 요소의 설정은 대상 플랫폼의 추적 설정을 유지하기 위해 제외됩니다.  
  
## <a name="publishing-wcf-services-with-non-http-bindings-to-iis"></a>HTTP가 아닌 바인딩을 사용하여 WCF 서비스를 IIS에 게시  
 IIS 7.0 이상을 사용하는 경우 HTTP가 아닌 바인딩을 사용하여 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 서비스를 IIS에 게시할 수 있습니다. 몇 가지 사전 구성 작업을 수행해야 합니다. 자세한 내용은 항목을 참조 하십시오 [Windows Process Activation Service에서의 호스팅](../../../docs/framework/wcf/feature-details/hosting-in-windows-process-activation-service.md)합니다.  
  
## <a name="security"></a>보안  
 IIS는 관리자 계정으로 실행해야 하므로 로컬 IIS에 게시하려면 관리자 권한이 필요합니다. 관리자 권한이 없는 사용자가 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 서비스 게시를 여는 경우 IIS를 대상 위치로 사용할 수 없습니다. 파일 시스템 또는 FTP 사이트에 게시 하는 관리자 권한 없이 작동합니다.  
  
## <a name="see-also"></a>참고 항목  
 [WCF Visual Studio 템플릿](../../../docs/framework/wcf/wcf-vs-templates.md)  
 [WCF 서비스 호스트(WcfSvcHost.exe)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)  
 [WCF 테스트 클라이언트(WcfTestClient.exe)](../../../docs/framework/wcf/wcf-test-client-wcftestclient-exe.md)
