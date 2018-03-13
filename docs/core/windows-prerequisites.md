---
title: "Windows에서 .NET Core의 필수 구성 요소"
description: "Windows 컴퓨터에서 .NET Core 응용프로그램을 개발 및 실행하기 위해 필요한 종속성이 무엇인지 살펴보세요."
author: JRAlexander
ms.author: johalex
ms.date: 03/02/2018
ms.topic: article
ms.prod: .net-core
ms.workload:
- dotnetcore
ms.openlocfilehash: 48102f3fb7fa6e93238eefff0e7f1ecbed4d8409
ms.sourcegitcommit: d3cfda0943364aaf6ccd574f55f584576c8a4fee
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="prerequisites-for-net-core-on-windows"></a>Windows에서 .NET Core의 필수 구성 요소

이 문서에서는 Windows에서 .NET Core 응용 프로그램을 개발하는 데 필요한 종속성을 보여 줍니다. 다음에 나오는 지원되는 OS 버전 및 종속성은 Windows에서 .NET Core 앱을 개발하기 위한 세 가지 방법에 적용됩니다.

* [명령줄](tutorials/using-with-xplat-cli.md)
* [Visual Studio 2017](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs)
* [Visual Studio Code](https://code.visualstudio.com/)

## <a name="net-core-supported-windows-versions"></a>.NET Core가 지원되는 Windows 버전

.NET Core는 다음 버전에서 지원됩니다.

* Windows 7 SP1
* Windows 8.1
* Windows 10 1주년 업데이트(버전 1607) 이상 버전
* Windows Server 2008 R2 SP1(전체 서버 또는 Server Core)
* Windows Server 2012 SP1(전체 서버 또는 Server Core)
* Windows Server 2012 R2(전체 서버 또는 Server Core)
* Windows Server 2016(전체 서버, Server Core 또는 Nano Server)

.NET Core 2.x가 지원되는 운영 체제의 전체 목록은 [.NET Core 2.x - Supported OS Versions](https://github.com/dotnet/core/blob/master/release-notes/2.0/2.0-supported-os.md)(.NET Core 2.x - 지원되는 OS 버전)를 참조하세요.

.NET Core 1.x가 지원되는 운영 체제의 전체 목록은 [.NET Core 1.x Supported OS Versions](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0-supported-os.md)(.NET Core 1.x가 지원되는 OS 버전)를 참조하세요.

## <a name="net-core-dependencies"></a>.NET Core 종속성

.NET Core 1.1 이전 버전을 Windows 10 및 Windows Server 2016보다 이전 버전의 Windows에서 실행하는 경우 Visual C++ 재배포 가능 패키지가 필요합니다. 이 종속성은 .NET Core 설치 관리자에 의해 자동으로 설치됩니다.

다음과 같은 경우에는 [Microsoft Visual C++ 2015 재배포 가능 패키지 업데이트 3](https://www.microsoft.com/download/details.aspx?id=52685)을 수동으로 설치해야 합니다.

* [설치 관리자 스크립트](./tools/dotnet-install-script.md)를 사용하여 .NET Core 설치.
* 자체 포함된 .NET Core 응용 프로그램 배포.
* 원본에서 제품 빌드.
* *.zip* 파일을 통해 .NET Core 설치. 여기에는 빌드/CI/CD 서버가 포함될 수 있습니다.

> [!NOTE]
> *Windows 7 및 Windows Server 2008 컴퓨터만 해당:* 설치된 Windows가 최신 버전이며 Windows 업데이트를 통해 설치된 핫픽스 [KB2533623](https://support.microsoft.com/help/2533623)이 포함되어 있는지 확인하세요.

## <a name="prerequisites-with-visual-studio-2017"></a>Visual Studio 2017 필수 구성 요소

.NET Core SDK를 사용하여 .NET Core 응용 프로그램을 개발하기 위해 원하는 편집기를 사용할 수 있습니다. [Visual Studio 2017](#visual-studio-2017)에서는 Windows 기반 .NET Core 앱에 대한 통합 개발 환경을 제공합니다.

[릴리스 정보](/visualstudio/releasenotes/vs2017-relnotes)에서 Visual Studio 2017의 변경 내용에 대해 자세히 알아볼 수 있습니다.

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

Visual Studio 2017에서 .NET Core 2.x 앱을 개발하려면:

 1. **기타 도구 집합** 섹션에서 **.NET Core 플랫폼 간 개발** 워크로드를 선택하고 [Visual Studio 2017 버전 15.3.0 이상을 다운로드하여 설치](/visualstudio/install/install-visual-studio)합니다.

![".NET Core 플랫폼 간 개발" 워크플로가 선택된 Visual Studio 2017 설치 스크린샷](./media/windows-prerequisites/vs-15-3-workloads.jpg)

**.NET Core 플랫폼 간 개발** 도구 집합이 설치된 후 Visual Studio 2017에서는 기본적으로 .NET Core 1.x를 사용합니다. .NET Core 2.x SDK를 설치하여 Visual Studio 2017에 .NET Core 2.x 지원을 가져옵니다.

 2. [.NET Core 2.x SDK](https://www.microsoft.com/net/download/core)를 설치합니다.
 3. 다음 지침에 따라 기존 또는 새로운 .NET Core 1.x 프로젝트의 대상을 .NET Core 2.x로 변경합니다.
    * **프로젝트** 메뉴에서 **속성**을 선택합니다.
    * **대상 프레임워크** 선택 메뉴에서 값을 **.NET Core 2.0**으로 설정합니다.

![“.NET Core 2.0” 대상 프레임워크 메뉴 항목을 선택한 Visual Studio 2017 응용 프로그램 프로젝트 속성의 스크린샷](./media/windows-prerequisites/Targeting-dotnetCore2.png)

.NET Core 2.x SDK가 설치된 후 Visual Studio 2017에서는 기본적으로 .NET Core SDK 2.x를 사용하고 다음 작업을 지원합니다.

* 기존 .NET Core 1.x 프로젝트를 열고, 빌드하고, 실행합니다.
* .NET Core 1.x 프로젝트의 대상을 .NET Core 2.x로 변경하고 빌드 및 실행합니다.
* 새로운 .NET Core 2.x 프로젝트를 만듭니다.

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

Visual Studio에서 .NET Core 1.x 앱을 개발하려면 **기타 도구 집합** 섹션에서 **“.NET Core 플랫폼 간 개발”** 워크로드를 선택하고 [Visual Studio 2017 RTM(버전 15.0.26228.4) 이상을 다운로드하여 설치](/visualstudio/install/install-visual-studio)합니다.

![".NET Core 플랫폼 간 개발" 워크플로가 선택된 Visual Studio 2017 설치 스크린샷](./media/windows-prerequisites/vs_workloads.jpg)

> [!IMPORTANT]
> .NET Core 1.x 개발에 Visual Studio 2015를 사용할 수 있지만 다음 이유로 권장하지 않습니다.
  > * .NET Core 도구는 지원되지 않는 미리 보기 버전입니다.
  > * 프로젝트는 더 이상 사용되지 않는 project.json을 기반으로 작성되었습니다.
>
> 프로젝트 형식 변경에 대한 자세한 내용은 [변경 내용에 대한 대략적인 개요](./tools/cli-msbuild-architecture.md)를 참조하세요.
---

> [!TIP]
> Visual Studio 2017 버전을 확인하려면:
>
> * **도움말** 메뉴에서 **Microsoft Visual Studio 정보**를 선택합니다.
> * **Microsoft Visual Studio 정보** 대화 상자에서 버전 번호를 확인합니다.
>   * .NET Core 2.1 미리 보기 1 앱의 경우 Visual Studio 2017 버전 15.6 미리 보기 6 이상.
>   * .NET Core 2.0 앱의 경우 Visual Studio 2017 버전 15.3 이상.
>   * .NET Core 1.x 앱의 경우 Visual Studio 2017 버전 15.0 이상.
