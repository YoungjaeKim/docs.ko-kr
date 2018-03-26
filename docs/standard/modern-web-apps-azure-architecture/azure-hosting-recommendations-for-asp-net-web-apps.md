---
title: ASP.NET Core 웹앱에 대한 Azure 호스팅 권장 사항
description: ASP.NET Core 및 Azure를 사용하여 최신 웹 응용 프로그램 설계 | ASP.NET 웹앱에 대한 Azure 호스팅 권장 사항
author: ardalis
ms.author: wiwagn
ms.date: 10/07/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 868f1b7ce452be9e29b921888f90d128e074ba13
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/23/2017
---
# <a name="azure-hosting-recommendations-for-aspnet-core-web-apps"></a>ASP.NET Core 웹앱에 대한 Azure 호스팅 권장 사항

> "모든 기간 업무 리더는 IT 부서를 거치지 않고 클라우드(SaaS라고도 함)에서 응용 프로그램을 다운로드한 후 잡지를 구독하듯 사용료를 지불합니다. 그리고 서비스가 더 이상 필요하지 않으면 사용하지 않는 장비를 굳이 한 구석에 남겨둘 필요 없이 구독을 취소하기만 하면 됩니다.”  
> _\- Gartner 분석가 Daryl Plummer_

## <a name="summary"></a>요약

응용 프로그램의 요구 사항 및 아키텍처가 무엇이든 Windows Azure는 이를 지원할 수 있습니다. 호스팅 요구 사항은 수십 가지 서비스로 이루어진 매우 복잡한 응용 프로그램에 대한 정적 웹 사이트처럼 간단할 수 있습니다. ASP.NET Core 모놀리식 웹 응용 프로그램 및 지원 서비스에 권장되는 잘 알려진 구성이 몇 가지 있습니다. 아래 권장 사항은 모든 응용 프로그램, 개별 프로세스 또는 데이터에 관계없이 호스팅할 리소스의 종류에 따라 그룹화되어 있습니다.

## <a name="web-applications"></a>웹 응용 프로그램

웹 응용 프로그램은 다음을 통해 호스팅할 수 있습니다.

-   App Service Web Apps

-   컨테이너

-   Azure Service Fabric

-   VM(가상 머신)

이 중에서 App Service Web Apps는 대부분의 시나리오에 권장되는 접근 방법입니다. 마이크로 서비스 아키텍처의 경우 컨테이너 기반 접근 방식 또는 서비스 패브릭을 고려합니다. 응용 프로그램을 실행하는 컴퓨터에 대한 더 세부적인 제어가 필요할 경우 Azure Virtual Machines를 고려합니다.

### <a name="app-service-web-apps"></a>App Service Web Apps

App Service Web Apps는 웹 응용 프로그램 호스팅에 최적화된 완벽하게 관리되는 플랫폼을 제공합니다. 이는 비즈니스 논리에 집중할 수 있게 해주는 PaaS(Platform-as-a-service) 솔루션이며, Azure는 앱 실행 및 확장에 필요한 인프라를 관리합니다. App Service Web Apps의 몇 가지 주요 기능:

-   DevOps 최적화(지속적인 통합 및 업데이트, 여러 환경, A/B 테스트, 스크립팅 지원)

-   세계적인 규모 및 고가용성

-   SaaS 플랫폼 및 온-프레미스 데이터에 대한 연결

-   보안 및 규정 준수

-   Visual Studio 통합

Azure App Service는 대부분의 웹앱에 가장 적합한 선택입니다. 배포 및 관리가 플랫폼에 통합되어 있고, 사이트가 높은 트래픽 부하를 처리하기 위해 빠르게 확장될 수 있으며, 기본 제공되는 부하 분산 및 트래픽 관리자가 고가용성을 제공합니다. 온라인 마이그레이션 도구를 사용하여 기존 사이트를 Azure App Service로 쉽게 이동하거나, 웹 응용 프로그램 갤러리에서 오픈 소스 응용 프로그램을 사용하거나, 원하는 프레임워크와 도구를 사용하여 새 사이트를 만들 수 있습니다. Webjob 기능을 사용하면 백그라운드 작업 처리를 App Service 웹앱에 쉽게 추가할 수 있습니다.

### <a name="containers-and-azure-container-service"></a>컨테이너 및 Azure Container Service

Azure Container Service를 사용하면 컨테이너화된 응용 프로그램을 실행하도록 미리 구성된 가상 머신 클러스터를 더욱 간편하게 생성, 구성 및 관리할 수 있습니다. Azure Container Service는 인기 있는 오픈 소스 일정 예약 및 오케스트레이션 도구의 최적화된 구성을 사용합니다. 따라서 기존 기술을 사용하거나, 점점 커가는 대규모 전문 커뮤니티를 이용하여 Microsoft Azure에서 컨테이너 기반 응용 프로그램을 배포하고 관리할 수 있습니다.

Azure Container Service를 사용하면 컨테이너화된 응용 프로그램을 실행하도록 미리 구성된 가상 머신 클러스터를 더욱 간편하게 생성, 구성 및 관리할 수 있습니다. Azure Container Service는 인기 있는 오픈 소스 일정 예약 및 오케스트레이션 도구의 최적화된 구성을 사용합니다. 따라서 기존 기술을 사용하거나, 점점 커가는 대규모 전문 커뮤니티를 이용하여 Microsoft Azure에서 컨테이너 기반 응용 프로그램을 배포하고 관리할 수 있습니다.

Azure Container Service의 목표는 현재 Microsoft 고객들 사이에서 널리 사용되는 오픈 소스 도구 및 기술을 사용하여 컨테이너 호스팅 환경을 제공하는 것입니다. 이를 위해 Azure Container Service는 선택한 오케스트레이터(DC/OS, Docker Swarm 또는 Kubernetes)의 표준 API 엔드포인트를 노출합니다. 이 엔드포인트를 사용하면 해당 엔드포인트와 통신할 수 있는 모든 소프트웨어를 활용할 수 있습니다. 예를 들어 Docker Swarm 엔드포인트의 경우 Docker CLI(명령줄 인터페이스)를 사용하도록 선택할 수 있습니다. DC/OS의 경우 DCOS CLI를 선택할 수 있습니다. Kubernetes의 경우 kubectl을 선택할 수 있습니다. 그림 11-1에서는 이러한 엔드포인트를 사용하여 컨테이너 클러스터를 관리하는 방법을 보여줍니다.

![](./media/image11-1.png)

**그림 11-1.** Docker, Kubernetes 또는 DC/OS 엔드포인트를 사용한 Azure Container Service 관리

### <a name="azure-service-fabric"></a>Azure Service Fabric

Service Fabric은 새 앱을 만들거나 마이크로 서비스 아키텍처를 사용하도록 기존 앱을 다시 작성하는 경우에 적합한 선택입니다. 공유된 컴퓨터 풀에서 실행되는 앱은 작게 시작하여 필요에 따라 수백 또는 수천 대 컴퓨터와 함께 대규모로 확장할 수 있습니다. 상태 저장 서비스는 일관되고 안정적인 방식으로 앱 상태를 쉽게 저장할 수 있게 해주고, Service Fabric은 자동으로 서비스 분할, 확장 및 가용성을 관리합니다. Service Fabric은 OWIN(Open Web Interface for .NET) 및 ASP.NET Core를 사용하여 WebAPI를 지원합니다. 또한 Service Fabric은 기본 인프라에 대해 App Service보다 세부적인 제어 기능이나 직접 액세스를 제공합니다. 서버에 원격으로 연결하거나 서버 시작 작업을 구성할 수 있습니다.

### <a name="azure-virtual-machines"></a>Azure Virtual Machines

App Service 또는 Service Fabric에서 실행하려면 상당한 수정이 필요한 기존 응용 프로그램의 경우, 클라우드로의 마이그레이션을 간소화하기 위해 Virtual Machines를 선택할 수 있습니다. 그러나 VM을 올바르게 구성, 보호 및 유지 관리하려면 Azure App Service 및 Service Fabric보다 훨씬 더 많은 시간과 IT 전문 지식이 필요합니다. Azure Virtual Machines를 고려 중인 경우 VM 환경을 패치, 업데이트 및 관리하는 데 필요한 지속적인 유지 관리 노력을 염두에 두어야 합니다. Azure Virtual Machines는 IaaS(Infrastructure-as-a-Service)이며, App Service 및 Service Fabric은 PaaS(Platform-as-a-Service)입니다.

#### <a name="feature-comparison"></a>기능 비교

| 기능 App Service | Service Fabric | 가상 컴퓨터 |
|---------|----------|----------|
| 거의 즉각적인 배포 | X | X | |
| 재배포 없이 더 많은 컴퓨터로 확장 | X | X | |
| 인스턴스가 콘텐츠와 구성 공유, 확장 시 재배포 또는 재구성할 필요 없음 | X | X | |
| 여러 배포 환경(프로덕션, 준비) | X | X | |
| 자동 OS 업데이트 관리 | X | | |
| 32/64비트 플랫폼 간의 원활한 전환 | X | | |
| Git, FTP를 사용하여 코드 배포 | X | | X |
| WebDeploy를 사용하여 코드 배포 | X | | X |
| TFS를 사용하여 코드 배포 | X | X | X |
| 다중 계층 아키텍처의 호스트 웹 또는 웹 서비스 계층 | X | X | X |
| Service Bus, Storage, SQL Database와 같은 Azure 서비스에 액세스 | X | X | X |
| 모든 사용자 지정 MSI 설치 | | X | X |

## <a name="logical-processes"></a>논리적 프로세스

응용 프로그램의 나머지 부분과 분리될 수 있는 개별 논리 프로세스는 "서버가 없는" 방식으로 Azure Functions에 별도로 배포할 수 있습니다. Azure Functions를 사용하면 코드를 실행할 응용 프로그램 또는 인프라에 대한 걱정 없이 주어진 문제에 필요한 코드를 작성할 수 있습니다. C\#, F\#, Node.js, Python 및 PHP를 포함하는 다양한 프로그래밍 언어 중에서 작업에 가장 생산적인 언어를 선택할 수 있습니다. 대부분의 클라우드 기반 솔루션과 마찬가지로 사용 시간만큼 요금을 지불하고 Azure Functions를 필요에 따라 확장할 수 있습니다.

## <a name="data"></a>데이터

Azure는 다양한 데이터 저장 옵션을 제공하므로, 응용 프로그램이 해당 데이터에 대해 적절한 데이터 공급자를 사용할 수 있습니다.

트랜잭션, 관계형 데이터의 경우 Azure SQL Database가 가장 적합한 옵션입니다. 대부분 읽기 전용인 고성능 데이터의 경우 Azure SQL Database에서 지원하는 Redis 캐시가 적합한 솔루션입니다.

구조화되지 않은 JSON 데이터는 SQL Database 열에서 Azure Storage의 Blob 또는 테이블, DocumentDB에 이르기까지 다양한 방법으로 저장할 수 있습니다. 이 중에서 DocumentDB는 최상의 쿼리 기능을 제공하며, 쿼리를 지원해야 하는 다수의 JSON 기반 문서에 권장되는 옵션입니다.

응용 프로그램 동작을 오케스트레이션하는 데 사용되는 일시적인 명령 또는 이벤트 기반 데이터는 Azure Service Bus 또는 Azure Storage Queue를 사용할 수 있습니다. Azure Storage Bus는 더 많은 유연성을 제공하며 응용 프로그램 내 및 응용 프로그램 간의 중요한 메시징에 권장되는 서비스입니다.

## <a name="architecture-recommendations"></a>아키텍처 권장 사항

응용 프로그램의 요구 사항에 따라 아키텍처가 결정됩니다. 사용 가능한 Azure 서비스는 여러 가지가 있으며, 적절한 서비스를 선택하는 것이 중요합니다. Microsoft는 일반적인 시나리오에 최적화된 일반적인 아키텍처를 식별하는 데 도움이 되는 참조 아키텍처의 갤러리를 제공합니다. 응용 프로그램의 요구 사항과 밀접한 관련이 있거나 적어도 시작점을 제공하는 참조 아키텍처를 바인딩할 수 있습니다.

그림 11-2는 참조 아키텍처의 예를 보여줍니다. 이 다이어그램에서는 마케팅에 최적화된 Sitecore 콘텐츠 관리 시스템 웹 사이트에 권장되는 아키텍처 접근 방식을 설명합니다.

![](./media/image11-2.png)

**그림 11-2.** Sitecore 마케팅 웹 사이트 참조 아키텍처 

**참조 - Azure 호스팅 권장 사항**

-   Azure 솔루션 아키텍처\
    <https://azure.microsoft.com/solutions/architecture/>

-   Azure 개발자 가이드\
    <https://azure.microsoft.com/campaigns/developer-guide/>

-   Azure App Service란?\
    <https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is>

-   Azure App Service, Virtual Machines, Service Fabric 및 클라우드 서비스 비교\
    <https://docs.microsoft.com/azure/app-service-web/choose-web-site-cloud-service-vm>

>[!div class="step-by-step"]
[이전] (development-process-for-azure.md)
