---
title: "ASP.NET Core 및 Azure를 사용하여 현대식 웹 응용 프로그램 설계"
description: "ASP.NET Core 및 Azure를 사용하여 현대식 웹 응용 프로그램 설계 | 소개"
author: ardalis
ms.author: wiwagn
ms.date: 10/06/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 1140a18aba685f3415d7c599d1b76648bf9924e7
ms.sourcegitcommit: c3957fdb990060559d73cca44ab3e2c7b4d049c0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2018
---
# <a name="architect-modern-web-applications-with-aspnet-core-and-azure"></a>ASP.NET Core 및 Azure를 사용하여 현대식 웹 응용 프로그램 설계

![표지 이미지](./media/cover.jpg)


.NET core 및 ASP.NET Core는 기존의.NET 개발에 비해 여러 가지 이점을 제공합니다. 다음 중 일부 또는 전부가 응용 프로그램의 성공에 중요한 경우 서버 응용 프로그램에 .NET Core를 사용해야 합니다.

-   플랫폼 간 지원

-   마이크로 서비스 사용

-   Docker 컨테이너 사용

-   고성능 및 확장성 요구 사항

-   동일한 서버의 응용 프로그램에서 .NET 버전 병렬 관리

기존 .NET 응용 프로그램은 이러한 요구 사항을 지원할 수 있지만 ASP.NET Core 및 .NET Core는 위의 시나리오에 대한 향상된 지원을 제공하도록 최적화되었습니다.

점점 더 많은 조직에서 Microsoft Azure 같은 서비스를 사용하는 클라우드에 웹 응용 프로그램을 호스팅하기로 선택하고 있습니다. 응용 프로그램 또는 조직에 다음 사항이 중요한 경우 클라우드에서 응용 프로그램을 호스팅하는 것이 좋습니다.

-   데이터 센터 비용에 대한 투자 감소(하드웨어, 소프트웨어, 공간, 유틸리티 등)

-   유동적인 가격 책정(유휴 용량이 아닌 사용량을 기준으로 지불)

-   매우 뛰어난 안정성

-   향상된 앱 이동성: 앱의 배포 위치와 방법을 쉽게 변경

-   유동적인 용량: 실제 요구 사항에 따라 규모 확장 또는 축소

Microsoft Azure에서 호스팅되는 ASP.NET Core 지원 웹 응용 프로그램을 구축하면 기존의 대안보다 수많은 경쟁적 이점을 얻을 수 있습니다. ASP.NET Core는 현대식 웹 응용 프로그램 개발 사례 및 클라우드 호스팅 시나리오에 최적화되어 있습니다. 이 가이드에서는 이러한 기능을 최대한 활용할 수 있도록 ASP.NET Core 응용 프로그램을 설계하는 방법에 알아봅니다.

## <a name="purpose"></a>용도

이 가이드에서는 ASP.NET Core 및 Azure를 사용하는 모놀리식 웹 응용 프로그램을 구축하는 방법에 대한 포괄적인 지침을 제공합니다.

이 가이드는 기업 응용 프로그램을 호스팅하는 Docker, 마이크로 서비스 및 컨테이너 배포에 더욱 중점을 둔 "*Architecting and Developing Containerized and Microservice-based Applications with .NET*"(.NET을 사용하여 컨테이너화된, 마이크로 서비스 기반 응용 프로그램 설계 및 개발)을 보완합니다.

> ### <a name="architecting-and-developing-containerized-microservice-based-apps-in-net"></a>.NET에서 컨테이너화된, 마이크로 서비스 기반 앱 설계 및 개발
> - **전자책**  
> <http://aka.ms/MicroservicesEbook>
> - **예제 응용 프로그램**  
> <http://aka.ms/microservicesarchitecture>

## <a name="who-should-use-this-guide"></a>이 가이드의 대상 사용자

이 가이드의 주요 대상 사용자는 클라우드에서 Microsoft 기술 및 서비스를 사용하여 현대식 웹 응용 프로그램을 구축하는 데 관심 있는 개발자, 개발 책임자 및 설계자입니다.

이차적인 대상 사용자는 이미 ASP.NET 및/또는 Azure에 익숙하고 신규 또는 기존 프로젝트를 위해 ASP.NET Core를 업그레이드하는 것이 적절한지에 관한 정보를 찾고 있는 기술 의사 결정권자입니다.

## <a name="how-you-can-use-this-guide"></a>이 가이드를 사용하는 방법

이 가이드는 현대식 .NET 기술 및 Windows Azure로 웹 응용 프로그램을 구축하는 방법에 중점을 둔, 비교적 작은 문서로 압축되었습니다. 따라서 전제적으로 읽어보면 이러한 응용 프로그램 및 해당 기술 고려 사항의 이해를 위한 기반을 마련할 수 있습니다. 이 가이드와 응용 프로그램 예제는 출발점이나 참고 자료 역할도 할 수 있습니다. 관련 응용 프로그램 예제를 자신의 응용 프로그램을 위한 템플릿으로 사용하거나 응용 프로그램의 구성 요소 부분을 구성하는 방법을 알아보는 용도로 사용하세요. 자신의 응용 프로그램을 위한 옵션을 저울질할 때는 가이드의 원칙과 아키텍처 및 기술 옵션, 의사 결정 고려 사항에 대한 내용을 참조하세요.

이 가이드를 팀에게 자유롭게 전달하여 이러한 고려 사항 및 기회에 대한 공통적인 이해를 도모하세요. 모든 사람이 공통적인 용어 집합과 기본 원칙으로 작업하도록 하면 아키텍처 패턴과 방법의 일관적인 적용을 보장하는 데 도움이 됩니다.

## <a name="references"></a>참조
- **서버 앱에 대해 .NET Core와 .NET Framework 중에 선택**  
<https://docs.microsoft.com/dotnet/standard/choosing-core-framework-server>

>[!div class="step-by-step"]
[다음] (modern-web-applications-characteristics.md)
