---
title: 프로덕션 환경에서 구성 및 microservices 기반 응용 프로그램을 실행 합니다.
description: Microsoft 플랫폼 및 도구를 사용하여 컨테이너화된 Docker 응용 프로그램 수명 주기
keywords: Docker, 마이크로 서비스, ASP.NET, 컨테이너
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 09/22/2017
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 0d7611d07c9995984269e3f7b071154d9b861367
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="run-composed-and-microservices-based-applications-in-production-environments"></a>프로덕션 환경에서 구성 및 microservices 기반 응용 프로그램을 실행 합니다.

여러 microservices 하 여 작성 하는 응용 프로그램 배포의 복잡성을 단순화 하 고는 IT의 관점에서 실행 가능한 확인 하기 위해 orchestrator 클러스터에 배포할 수 필요가 합니다. 없이 orchestrator 클러스터를 배포 하 고 복잡 한 microservices 응용 프로그램을 스케일 아웃 하기 매우 어렵습니다 됩니다.

## <a name="introduction-to-orchestrators-schedulers-and-container-clusters"></a>Orchestrators, 스케줄러, 및 컨테이너 클러스터 소개

이 전자책의 앞부분에 나오는 도입 되었습니다 *클러스터* 및 *스케줄러* 소프트웨어 아키텍처 및 개발에 대 한 토론의 일환으로 합니다. Docker 클러스터의 예로 docker는 Docker Swarm 및 Mesosphere 데이터 센터 운영 체제 (DC/OS). Microsoft Azure 컨테이너 서비스에서 제공 하는 인프라의 일부로 실행할 수 둘 다에 해당 합니다.

때 응용 프로그램은 수평 확장 된 여러 호스트 시스템에서 각각의 호스트 시스템을 관리 하 고 기본 플랫폼의 복잡성을 추상화 하는 기능 편리해 보일 수 있습니다. 정확 하 게 orchestrators 및 스케줄러 제공 기능입니다. 여기에 간략히를 보겠습니다.

-   **스케줄러 * * * *"일정" 관리자 특정 컨테이너를 실행 하는 방법을 설정 하는 호스트 시스템에 서비스 파일을 로드 하는 기능을 말합니다. 컨테이너는 Docker 클러스터에 시작 예약 상에 서 경향이 있습니다. 보다 일반적인 의미에서 서비스 정의 로드 하는 특정 작업을 가리키는 예약 있지만 스케줄러는 필요한 어떤 용량에는 서비스를 관리 하는 호스트의 init 시스템에 연결 합니다.

클러스터 스케줄러에는 여러 목표: 클러스터의 리소스를 효율적으로 사용, 예약 응용 프로그램 신속 하 게 되지 보류 상태로 남겨 두지는 수준의 "공정성," 오류 강력한 되 고 있는 사용자가 제공한 배치 제약 조건, 작업 및 항상 사용 가능 합니다.

-   **오케스트레이션 * * * *플랫폼의 호스트 클러스터에 배포 하는 복잡 하 고 multicontainer 워크 로드에 수명 주기 관리 기능을 확장 합니다. 호스트 인프라를 추상화 하 여 오케스트레이션 도구 전체 클러스터는 단일 배포 대상으로 처리 하는 방법을 사용자가 제공 합니다.

오케스트레이션 프로세스에서는 초기 배치 또는 컨테이너; 당 배포에서 응용 프로그램 관리의 모든 측면을 자동화할 수 있는 플랫폼 및 도구 컨테이너는 호스트의 상태 또는; 성능에 따라 서로 다른 호스트를 이동 버전 관리 및 롤링 업데이트 및 상태 모니터링 확장 및 장애 조치를 지 원하는 기능 등 다양 합니다.

오케스트레이션은 컨테이너 예약, 클러스터 관리 및 수의 프로 비전이 추가 호스트를 참조 하는 광범위 한 용어입니다.

Orchestrators 및 스케줄러에서 제공 하는 기능은 개발 하 고 처음부터 만드는 매우 복잡 하며 따라서 일반적으로 만들려는 오케스트레이션 솔루션을 사용 하 여 공급 업체에서 제공 합니다.


>[!div class="step-by-step"]
[이전] [다음] (관리-프로덕션-docker-environments.md) (index.md)
