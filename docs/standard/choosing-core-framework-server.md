---
title: 서버 앱에 대해 .NET Core와 .NET Framework 중에 선택
description: .NET에서 서버 앱을 구축할 때 고려해야 할 .NET 구현에 대한 가이드입니다.
author: cartermp
ms.author: mairaw
ms.date: 03/15/2018
ms.topic: article
ms.prod: .net
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: c07b0b760e2a46faea574eef3575409bac773942
ms.sourcegitcommit: 15316053918995cc1380163a7d7e7edd5c44e6d7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2018
---
# <a name="choosing-between-net-core-and-net-framework-for-server-apps"></a>서버 앱에 대해 .NET Core와 .NET Framework 중에 선택

.NET에서 서버 쪽 응용 프로그램을 구축하는 데 지원되는 두 가지 구현은 .NET Framework 및 .NET Core입니다. 두 구현은 여러 가지 동일한 구성 요소를 공유하므로 둘 간에 코드를 공유할 수 있습니다. 그러나 두 구현 간에는 기본적인 차이가 있으며 수행할 항목에 따라 선택이 달라집니다.  이 문서에서는 각각 사용하는 경우에 대한 지침을 제공합니다.

다음과 같은 경우에는 서버 응용 프로그램에 .NET Core를 사용합니다.

* 플랫폼 간 요구 사항이 있습니다.
* 마이크로 서비스를 대상으로 합니다.
* Docker 컨테이너를 사용하고 있습니다.
* 고성능 및 확장 가능한 시스템이 필요합니다.
* .NET 버전이 응용 프로그램별로 함께 필요합니다.

다음과 같은 경우에는 서버 응용 프로그램에 .NET Framework를 사용합니다.

* 앱이 현재 .NET Framework를 사용합니다(마이그레이션하는 대신 확장 권장).
* 앱이 .NET Core에 사용할 수 없는 타사 .NET 라이브러리 또는 NuGet 패키지를 사용합니다.
* 앱이 .NET Core에 사용할 수 없는 .NET 기술을 사용합니다.
* 앱이 .NET Core를 지원하지 않는 플랫폼을 사용합니다.

## <a name="when-to-choose-net-core"></a>.NET Core를 선택하는 경우

다음 섹션에서는 앞에서 설명한 .NET Core를 선택해야 하는 이유에 대해 좀 더 자세히 설명합니다.

### <a name="cross-platform-needs"></a>플랫폼 간 요구 사항

응용 프로그램(웹/서비스)이 여러 플랫폼 (Windows, Linux 및 macOS)에서 실행되어야 하는 경우 .NET Core를 사용합니다.

.NET Core는 앞에서 언급한 운영 체제를 개발 워크스테이션으로 지원합니다. Visual Studio는 Windows 및 macOS용 IDE(통합 개발 환경)를 제공합니다. 또한 macOS, Linux 및 Windows에서 실행되는 Visual Studio Code를 사용할 수 있습니다. Visual Studio Code는 IntelliSense 및 디버깅을 포함하여 .NET Core를 지원합니다. Sublime, Emacs 및 VI 같은 대부분의 타사 편집기는 .NET Core에서 작동합니다. 이러한 타사 편집기는 [Omnisharp](http://www.omnisharp.net/)를 사용하여 편집기 IntelliSense를 가져옵니다. 어떤 코드 편집기도 사용하지 않고, 지원되는 모든 플랫폼에서 사용할 수 있는 [.NET Core CLI 도구](../core/tools/index.md)를 직접 사용할 수도 있습니다.

### <a name="microservices-architecture"></a>마이크로 서비스 아키텍처

마이크로 서비스 아키텍처를 사용하면 서비스 경계를 벗어나 여러 기술을 융합할 수 있습니다. 이러한 기술 융합을 통해 다른 마이크로 서비스나 서비스에서 작동하는 새로운 마이크로 서비스에 .NET Core를 점진적으로 적용할 수 있습니다.  예를 들어 .NET Framework, Java, Ruby 또는 다른 모놀리식 기술로 개발된 서비스나 마이크로 서비스를 융합할 수 있습니다.

사용 가능한 많은 인프라 플랫폼이 있습니다. [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/)은 크고 복잡한 마이크로 서비스 시스템용으로 설계되었습니다. [Azure App Service](https://azure.microsoft.com/services/app-service/)는 상태 비저장 마이크로 서비스에 적합합니다. Docker를 바탕으로 하는 마이크로 서비스 대안의 경우 [컨테이너](#containers) 섹션에 설명된 대로 모든 종류의 마이크로 서비스 접근 방식과 맞습니다. 이러한 모든 플랫폼은 .NET Core를 지원하므로 마이크로 서비스를 호스팅하는 데 적합합니다.

마이크로 서비스 아키텍처에 대한 자세한 내용은 [.NET 마이크로 서비스. 컨테이너화된 .NET 응용 프로그램을 위한 아키텍처](microservices-architecture/index.md)를 참조하세요.

### <a name="containers"></a>컨테이너

컨테이너는 일반적으로 마이크로 서비스 아키텍처와 함께 사용됩니다. 또한 컨테이너는 모든 아키텍처 패턴을 따르는 웹앱 또는 서비스를 컨테이너화하는 데 사용할 수 있습니다. .NET Framework를 Windows 컨테이너에서 사용할 수 있지만 .NET Core의 모듈화된 간단한 특성이 컨테이너에 더 적합합니다. 컨테이너를 만들고 배포할 때 컨테이너 이미지의 크기가 .NET Framework보다 .NET Core를 사용할 때 훨씬 더 작습니다. 플랫폼 간 사용되므로 예를 들어 서버 앱을 Linux Docker 컨테이너에 배포할 수 있습니다.

Docker 컨테이너는 고유한 Linux 또는 Windows 인프라나 [Azure Container Service](https://azure.microsoft.com/services/container-service/) 같은 클라우드 서비스에서 호스트할 수 있습니다. Azure Container Service는 클라우드에서 컨테이너 기반 응용 프로그램을 관리, 오케스트레이션 및 확장할 수 있습니다.

### <a name="a-need-for-high-performance-and-scalable-systems"></a>고성능 및 확장 가능한 시스템에 대한 요구 사항

시스템에 가장 적합한 성능 및 확장성이 필요한 경우 .NET Core와 ASP.NET Core를 선택하는 것이 최고입니다. Windows Server 및 Linux용 고성능 서버 런타임은 [TechEmpower 벤치마크](https://www.techempower.com/benchmarks/#hw=ph&test=plaintext)에서 .NET을 최상의 웹 프레임워크로 만듭니다.

성능 및 확장성은 수백 개의 마이크로 서비스가 실행될 수 있는 마이크로 서비스 아키텍처와 특히 관련이 있습니다. ASP.NET Core를 사용할 경우 시스템은 훨씬 더 적은 수의 서버/VM(가상 컴퓨터)에서 실행됩니다. 감소된 서버/VM으로 인해 인프라 및 호스팅 비용이 절감됩니다.

### <a name="a-need-for-side-by-side-of-net-versions-per-application-level"></a>응용 프로그램 수준별로 .NET 버전이 함께 필요

다른 버전의 .NET에 대한 종속성이 있는 응용 프로그램을 설치하려면 .NET Core를 사용하는 것이 좋습니다. .NET Core를 사용하면 동일한 컴퓨터에서 서로 다른 버전의 .NET Core 런타임을 병렬로 설치할 수 있습니다. 이 병렬 설치는 동일한 서버에서 여러 서비스를 허용하며 각 서비스는 고유한 버전의 .NET Core에 있습니다. 또한 위험을 줄이고 응용 프로그램 업그레이드 및 IT 운영 비용을 절감할 수 있습니다.

## <a name="when-to-choose-net-framework"></a>.NET Framework를 선택하는 경우

.NET Core는 새 응용 프로그램 및 응용 프로그램 패턴에 상당한 이점을 제공합니다. 그러나 많은 기존 시나리오에서는 .NET Framework를 자연스럽게 선택합니다. 일부 서버 응용 프로그램에서는 .NET Framework가 .NET Core로 대체되지 않습니다.

### <a name="current-net-framework-applications"></a>현재 .NET Framework 응용 프로그램

대부분의 경우 기존 응용 프로그램을 .NET Core로 마이그레이션할 필요가 없습니다. 대신 ASP.NET 코어에서 새 웹 서비스를 작성하는 등 기존 응용 프로그램을 확장할 때 .NET Core를 사용하는 것이 좋습니다.

### <a name="a-need-to-use-third-party-net-libraries-or-nuget-packages-not-available-for-net-core"></a>.NET Core에 사용할 수 없는 타사 .NET 라이브러리 또는 NuGet 패키지를 사용해야 하는 필요성

라이브러리는 .NET Standard를 신속하게 수용하고 있습니다. .NET Standard에서는 .NET Core를 포함한 모든 .NET 구현에서 코드를 공유할 수 있습니다. .NET Standard 2.0을 사용하면 훨씬 더 쉬워집니다.

- API 노출 영역이 훨씬 더 커졌습니다. 
- .NET Framework 호환 모드가 도입되었습니다. 이 호환 모드에서는 .NET Standard/.NET Core 프로젝트에서 .NET Framework 라이브러리를 참조할 수 있습니다. 호환 모드에 대한 자세한 내용은 [.NET Standard 2.0 발표](https://blogs.msdn.microsoft.com/dotnet/2017/08/14/announcing-net-standard-2-0/)를 참조하세요.

따라서 라이브러리 또는 NuGet 패키지가 .NET Standard/.NET Core에서 사용할 수 없는 기술을 사용하는 경우에만 .NET Framework를 사용해야 합니다.

### <a name="a-need-to-use-net-technologies-not-available-for-net-core"></a>.NET Core에 사용할 수 없는 .NET 기술을 사용해야 하는 필요성

일부 .NET Framework 기술은 .NET Core에서 사용할 수 없습니다. 그중 일부는 이후 .NET Core 릴리스에서 사용할 수 있습니다. 나머지는 .NET Core에서 대상으로 하는 새 응용 프로그램 패턴에 적용되지 않아 사용하지 못할 수 있습니다. 다음 목록은 .NET Core에서 제공되지 않는 가장 일반적인 기술입니다.

* ASP.NET Web Forms 응용 프로그램: ASP.NET Web Forms는 .NET Framework에서만 사용할 수 있습니다. ASP.NET Core는 ASP.NET Web Forms에 사용할 수 없습니다. .NET Core에 ASP.NET Web Forms를 적용할 계획은 없습니다.

* ASP.NET 웹 페이지 응용 프로그램: ASP.NET 웹 페이지는 ASP.NET Core에 포함되지 않습니다. ASP.NET Core [Razor 페이지](/aspnet/core/mvc/razor-pages/)는 웹 페이지와 많은 유사점이 있습니다.

* ASP.NET SignalR 서버/클라이언트 구현: 현재 [ASP.NET SignalR](https://github.com/aspnet/SignalR)은 ASP.NET Core 2.1과 함께 미리 보기 모드로 제공됩니다.

* WCF 서비스 구현. .NET Core에서 WCF 서비스를 사용할 수 있는 [WCF-클라이언트 라이브러리](https://github.com/dotnet/wcf)가 있더라도 WCF 서버 구현은 현재 .NET Framework에서만 사용할 수 있습니다. 이 시나리오는 .NET Core에 대한 현재 계획의 일부가 아니지만 차후에 고려될 예정입니다.

* 워크플로 관련 서비스: Windows WF(Workflow Foundation), 워크플로 서비스(단일 서비스에서 WCF + WF) 및 WCF Data Services(이전의 “ADO.NET 데이터 서비스”)는 .NET Framework에서만 사용할 수 있습니다.  WF/WCF+WF/WCF Data Services를 .NET Core에 적용할 계획은 없습니다.

* WPF(Windows Presentation Foundation) 및 Windows Forms: WPF 및 Windows Forms 응용 프로그램은 .NET Framework에서만 사용할 수 있습니다. .NET Core로 이식할 예정은 없습니다.

* 언어 지원: Visual Basic 및 F#은 현재 .NET Core에서 지원되지만 일부 프로젝트 형식에서는 지원되지 않습니다. 지원되는 프로젝트 템플릿 목록은 [dotnet new에 대한 템플릿 옵션](../core/tools/dotnet-new.md#arguments)을 참조하세요.

공식 로드맵 외에 다른 프레임워크를 .NET Core로 이식할 수 있습니다. 전체 목록은 [port-to-core](https://github.com/dotnet/corefx/issues?q=is%3Aopen+is%3Aissue+label%3Aport-to-core)로 표시된 CoreFX 문제를 참조하세요. 이 목록이 해당 구성 요소를 .NET Core에 적용하겠다는 Microsoft의 약속을 나타내지는 않습니다. 단순히 커뮤니티의 바람을 파악한 것입니다. `port-to-core`로 표시된 구성 요소에 관심이 있는 경우 GitHub의 토론에 참여하세요. 누락된 내용이 있다고 생각이 들면 새로운 문제를 [CoreFX 리포지토리](https://github.com/dotnet/corefx/issues/new)에 등록하세요.

### <a name="a-need-to-use-a-platform-that-doesnt-support-net-core"></a>.NET Core를 지원하지 않는 플랫폼을 사용하는 필요성

일부 Microsoft 또는 타사 플랫폼에서는 .NET Core를 지원하지 않습니다. 예를 들어 Service Fabric Stateful Reliable Services 및 Service Fabric Reliable Actors와 같은 일부 Azure Services에는 .NET Framework가 필요합니다. 일부 다른 서비스에서는 .NET Core에서 사용할 수 없는 SDK를 제공합니다. 현재 Azure Services는 모두 .NET Core를 사용하므로 이 상황은 전환되고 있습니다. 그 동안에는 클라이언트 SDK 대신 상응하는 REST API를 항상 사용할 수 있습니다.

## <a name="see-also"></a>참고 항목
 [ASP.NET 및 ASP.NET Core 중에서 선택](/aspnet/core/choose-aspnet-framework)  
 [.NET Core 가이드](../core/index.md)  
 [.NET Framework에서 .NET Core로 이식](../core/porting/index.md)  
 [Docker 가이드의 .NET Framework](../framework/docker/index.md)  
 [.NET 구성 요소 개요](components.md)  
 [.NET 마이크로 서비스. 컨테이너화된 .NET 응용 프로그램을 위한 아키텍처](microservices-architecture/index.md)
