---
title: Docker 앱에 대한 개발 워크플로
description: 컨테이너화된 .NET 응용 프로그램을 위한 .NET 마이크로 서비스 아키텍처 | Docker 앱에 대한 개발 워크플로
keywords: Docker, 마이크로 서비스, ASP.NET, 컨테이너
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 10/18/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.topic: article
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 9c3df50430117936fd0b9d4390cb84e02085e48d
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="development-workflow-for-docker-apps"></a>Docker 앱에 대한 개발 워크플로

응용 프로그램 개발 수명 주기는 각 개발자의 컴퓨터에서 시작되며, 개발자는 자신의 컴퓨터에서 선호하는 언어를 사용하여 로컬로 응용 프로그램 코드를 작성하고 테스트합니다. 개발자가 어떤 언어, 프레임워크, 플랫폼을 선택하든 이 워크플로를 사용하면 개발자는 항상 Docker 컨테이너를 로컬로 개발하고 테스트하게 됩니다.

각 컨테이너(Docker 이미지의 인스턴스)는 다음 구성 요소를 포함합니다.

-   운영 체제 선택(예: Linux 배포판, Windows Nano Server 또는 Windows Server Core).

-   개발자가 추가한 파일(응용 프로그램 이진 파일 등).

-   구성 정보(환경 설정 및 종속성).

## <a name="workflow-for-developing-docker-container-based-applications"></a>Docker 컨테이너 기반 응용 프로그램을 개발하기 위한 워크플로

이 섹션에서는 Docker 컨테이너 기반 응용 프로그램에 대한 *내부 루프* 개발 워크플로를 설명합니다. 내부 루프 워크플로란 광범위한 DevOps 워크플로를 고려하지 않고 개발자의 컴퓨터에서 수행되는 개발 작업에만 집중한다는 의미입니다. 환경을 설정하는 초기 단계는 한 번만 수행되므로 포함되지 않습니다.

응용 프로그램은 개발자 고유의 서비스와 추가 라이브러리(종속성)로 구성됩니다. 다음은 그림 5-1처럼 일반적으로 Docker 응용 프로그램을 빌드할 때 수행하는 기본 단계입니다.

![](./media/image1.png)

**그림 5-1.** Docker 컨테이너화된 앱 개발을 위한 단계별 워크플로

이 가이드에서는 전체 프로세스를 자세히 설명하고 모든 주요 단계는 Visual Studio 환경을 중심으로 설명합니다.

편집기/CLI 개발 접근 방식을 사용하는 경우(예: macOS 또는 Windows에서 Visual Studio Code와 Docker CLI 사용) 일반적으로 Visual Studio를 사용할 때보다 모든 단계를 더 자세히 알아야 합니다. CLI 환경에서 작업하는 방법에 대한 자세한 내용은 전자책 [컨테이너화된 Docker 응용 프로그램 수명 주기와 Microsoft 플랫폼 및 도구](http://aka.ms/dockerlifecycleebook/)를 참조하세요.

Visual Studio 2015 또는 Visual Studio 2017을 사용하는 경우 이러한 단계의 상당 부분이 자동으로 처리되므로 생산성이 대폭 향상됩니다. Visual Studio 2017을 사용하고 다중 컨테이너 응용 프로그램을 대상으로 하는 경우에 특히 그렇습니다. 예를 들어 마우스 클릭 한 번이면 Visual Studio가 응용 프로그램의 구성을 사용하여 Dockerfile 및 docker-compose.yml 파일을 프로젝트에 추가합니다. Visual Studio에서 응용 프로그램을 실행하면 Visual Studio가 Docker 이미지를 작성하고 Docker에서 바로 다중 컨테이너 응용 프로그램을 실행하며, 심지어 여러 컨테이너를 한꺼번에 디버깅할 수도 있습니다. 이러한 기능은 개발 속도를 향상합니다.

그러나 Visual Studio가 이러한 단계를 자동으로 처리한다고 해서 Docker 내부에서 발생하는 일에 대해 전혀 몰라도 된다는 뜻은 아닙니다. 따라서 이어지는 지침에서 모든 단계를 자세히 살펴보겠습니다.

![](./media/image2.png)

## <a name="step-1-start-coding-and-create-your-initial-application-or-service-baseline"></a>1단계: 코딩을 시작하고 초기 응용 프로그램 또는 서비스 기준 만들기

Docker 응용 프로그램 개발은 Docker 없이 응용 프로그램을 개발하는 방법과 비슷합니다. 다른 점은 Docker를 개발하는 동안 로컬 환경의 Docker 컨테이너 내에서 실행되는 응용 프로그램을 배포하고 테스트한다는 점입니다. 컨테이너는 Linux 컨테이너일 수도 있고 Windows 컨테이너일 수도 있습니다.

### <a name="set-up-your-local-environment-with-visual-studio"></a>Visual Studio를 사용하여 로컬 환경 설정

시작하려면 다음 지침에 설명된 대로 Windows용 [Docker CE(Community Edition)](https://www.docker.com/community-edition)를 설치합니다.

[Windows용 Docker CE 시작](https://docs.docker.com/docker-for-windows/)

또한 Visual Studio 2017을 설치해야 합니다. Visual Studio 2017은 컨테이너 디버깅 등 더 많은 Docker 관련 기능을 지원하므로 Visual Studio 2015에 Visual Studio Tools for Docker 추가 기능을 사용하는 것보다 편리합니다. 그림 5-2처럼 설치 과정에서 **.NET Core 및 Docker** 워크로드를 선택하면 Visual Studio 2017에 Docker용 도구가 포함됩니다.

![](./media/image3.png)

**그림 5-2**. Visual Studio 2017을 설치하는 동안 **.NET Core 및 Docker** 워크로드 선택

심지어 응용 프로그램에서 Docker를 사용하도록 설정하고 Docker에 배포 및 테스트하기 전에도 일반 .NET에서 응용 프로그램 코딩을 시작할 수 있습니다(컨테이너를 사용하려는 경우 일반적으로 .NET Core). 하지만 되도록이면 빨리 Docker에서 작업을 시작하는 것이 좋습니다. 실제로 사용하게 될 환경이고 문제를 최대한 신속하게 검색할 수 있기 때문입니다. 이렇게 하도록 권장하는 이유는 Visual Studio를 사용하면 거의 투명한 것처럼 느껴지는 Docker를 손쉽게 작업할 수 있기 때문입니다. 가장 대표적인 예로 Visual Studio에서 다중 컨테이너 응용 프로그램을 디버깅하는 경우를 들 수 있습니다.

### <a name="additional-resources"></a>추가 자료

-   **Windows용 Docker CE 시작**
    [*https://docs.docker.com/docker-for-windows/*](https://docs.docker.com/docker-for-windows/)

-   **Visual Studio 2017**
    [*https://www.visualstudio.com/downloads/*](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs)

![](./media/image4.png)

## <a name="step-2-create-a-dockerfile-related-to-an-existing-net-base-image"></a>2단계. 기존 .NET 기본 이미지와 관련된 Dockerfile 만들기

Visual Studio에서 자동으로 배포하든 아니면 Docker CLI(docker run 및 docker-compose 명령)를 사용하여 수동으로 배포하든, 빌드하려는 각 사용자 지정 이미지에 대한 Dockerfile과 배포할 각 컨테이너에 대한 Dockerfile이 필요합니다. 응용 프로그램이 단일 사용자 지정 서비스를 포함하는 경우 단일 Dockerfile이 필요합니다. 응용 프로그램이 여러 서비스를 포함하는 경우(마이크로 서비스 아키텍처처럼) 서비스마다 하나의 Dockerfile이 필요합니다.

Dockerfile은 응용 프로그램 또는 서비스의 루트 폴더에 배치됩니다. 컨테이너의 응용 프로그램 또는 서비스를 설정하고 실행하는 방법을 Docker에 알려주는 명령을 포함하고 있습니다. 코드를 사용하여 수동으로 Dockerfile을 만들어서 .NET 종속성과 함께 프로젝트에 추가할 수 있습니다.

Visual Studio와 Docker용 도구를 사용하면 마우스 클릭 몇 번으로 이 작업을 처리할 수 있습니다. Visual Studio 2017에서 새 프로젝트를 만들 때 그림 5-3처럼 **컨테이너(Docker) 지원 사용**이라는 옵션이 있습니다.

![](./media/image5.png)

**그림 5-3**. Visual Studio 2017에서 새 프로젝트를 만들 때 Docker 지원을 사용하도록 설정

그림 5-4처럼 Visual Studio에서 프로젝트 파일을 마우스 오른쪽 단추로 클릭하고 **Docker 프로젝트 지원 추가** 옵션을 선택하여 새 프로젝트 또는 기존 프로젝트에서 Docker 지원을 사용하도록 설정할 수도 있습니다.

![](./media/image6.png)

**그림 5-4**. 기존 Visual Studio 2017 프로젝트에서 Docker 지원을 사용하도록 설정

프로젝트에서 수행하는 이 작업(ASP.NET 웹 응용 프로그램 또는 웹 API 서비스 같은)은 필요한 구성을 사용하여 Dockerfile을 프로젝트에 추가합니다. 또한 전체 솔루션에 대한 docker compose.yml 파일을 추가합니다. 다음 섹션에서는 이러한 각 파일에 입력되는 정보를 살펴보겠습니다. Visual Studio에서 이 작업을 자동으로 수행할 수 있지만, Dockerfile에 어떤 정보가 들어가는지 알아두는 것이 좋습니다.

### <a name="option-a-creating-a-project-using-an-existing-official-net-docker-image"></a>옵션 A: 기존의 공식 .NET Docker 이미지를 사용하여 프로젝트 만들기

일반적으로 [Docker Hub](https://hub.docker.com/) 레지스트리의 공식 리포지토리에서 얻을 수 있는 기본 이미지를 기반으로 컨테이너에 대한 사용자 지정 이미지를 빌드합니다. Visual Studio에서 Docker 지원을 사용하도록 설정하면 내부에서 이와 같은 일이 발생합니다. Dockerfile은 기존 aspnetcore 이미지를 사용합니다.

앞에서 선택하는 프레임워크 및 운영 체제에 따라 어떤 Docker 이미지와 리포지토리를 사용할 수 있는지 설명했습니다. 예를 들어 ASP.NET Core(Linux 또는 Windows)를 사용하려는 경우 사용할 이미지는 microsoft/aspnetcore:2.0입니다. 따라서 컨테이너에 사용할 기본 Docker 이미지만 지정하면 됩니다. 그 방법은 Dockerfile에 FROM microsoft/aspnetcore:2.0을 추가하는 것입니다. 이 작업은 Visual Studio가 자동으로 수행하지만, 버전을 업데이트하려면 직접 이 값을 업데이트합니다.

버전 번호가 있는 Docker Hub의 공식 .NET 이미지 리포지토리를 사용하면 모든 컴퓨터에서(개발, 테스트 및 프로덕션 포함) 동일한 언어 기능을 사용할 수 있습니다.

다음 예제에서는 ASP.NET Core 컨테이너에 대한 샘플 Dockerfile을 보여줍니다.

```
FROM microsoft/aspnetcore:2.0
  
ARG source
  
WORKDIR /app
  
EXPOSE 80
  
COPY ${source:-obj/Docker/publish} .
  
ENTRYPOINT ["dotnet", " MySingleContainerWebApp.dll "]
```

이 예에서 컨테이너는 공식 ASP.NET Core Docker 버전 2.0 이미지(Linux 및 Windows용 다중 아키텍처)를 기반으로 합니다. 이것은 설정 `FROM microsoft/aspnetcore:2.0`입니다. (이 기본 이미지에 대한 자세한 내용은 [ASP.NET Core Docker 이미지](https://hub.docker.com/r/microsoft/aspnetcore/) 페이지 및 [.NET Core Docker 이미지](https://hub.docker.com/r/microsoft/dotnet/) 페이지를 참조하세요.) 또한 Dockerfile에서, 런타임에 사용할 TCP 포트(이 예에서는 EXPOSE 설정을 사용하여 구성한 대로 포트 80)에서 수신 대기하라고 Docker에 지시해야 합니다.

사용하는 언어 및 프레임워크에 따라 Dockerfile에서 추가 구성 설정을 지정할 수 있습니다. 예를 들어 \["dotnet", "MySingleContainerWebApp.dll"\]이 포함된 ENTRYPOINT 줄은 Docker에 .NET Core 응용 프로그램을 실행하라고 알려줍니다. SDK 및 .NET Core CLI(dotnet CLI)를 사용하여 .NET 응용 프로그램을 빌드하고 실행하는 경우 이 설정이 달라집니다. 결론적으로 ENTRYPOINT 줄 및 기타 설정은 개발자가 응용 프로그램에 대해 선택하는 언어 및 플랫폼에 따라 달라집니다.

### <a name="additional-resources"></a>추가 자료

-   **.NET Core 응용 프로그램에 대한 Docker 이미지 작성**
    [*https://docs.microsoft.com/dotnet/core/docker/building-net-docker-images*](../../../core/docker/building-net-docker-images.md)

-   **고유의 이미지 빌드**. 공식 Docker 설명서에 있습니다.
    [*https://docs.docker.com/engine/tutorials/dockerimages/*](https://docs.docker.com/engine/tutorials/dockerimages/)

### <a name="using-multi-arch-image-repositories"></a>다중 아키텍처 이미지 리포지토리 사용

단일 리포지토리는 Linux 이미지 및 Windows 이미지 같은 플랫폼 변형을 포함할 수 있습니다. 이 기능을 통해 Microsoft 같은 공급업체(기본 이미지 작성자)는 여러 플랫폼(즉, Linux 및 Windows)을 처리하는 단일 리포지토리를 만들 수 있습니다. 예를 들어 Docker Hub 레지스트리에서 제공되는 [microsoft/dotnet](https://hub.docker.com/r/microsoft/aspnetcore/) 리포지토리는 동일한 리포지토리 이름을 사용하여 Linux 및 Windows Nano Server에 대한 지원을 제공합니다.

태그를 지정하는 경우 다음과 같이 명시적인 플랫폼을 대상으로 지정합니다.

-   **microsoft/aspnetcore:2.0.0-jessie**

        .NET Core 2.0 runtime-only on Linux 

-   **microsoft/aspnetcore:2.0.0-nanoserver**

        .NET Core 2.0 runtime-only on Windows Nano Server

그러나 이것은 2017년 중순 이후에 나온 새 기능이며, 동일한 이미지 이름을 지정하고 동일한 태그를 지정하는 경우 새로운 다중 아키텍처 이미지(예: 다중 아키텍처를 지원하는 aspnetcore 이미지)는 다음 예제와 같이 개발자가 배포하는 Docker 호스트 OS에 따라 Linux 또는 Windows 버전을 사용합니다.

-   **microsoft/aspnetcore:2.0**

        Multi-arch: .NET Core 2.0 runtime-only on Linux or Windows Nano Server depending on the Docker host OS

이와 같이, Windows 호스트에서 이미지를 끌어오면 Windows 변형을 끌어오고, Linux 호스트에서 동일한 이미지 이름을 끌어오면 Linux 변형을 끌어옵니다.

### <a name="option-b-creating-your-base-image-from-scratch"></a>옵션 B: 기본 이미지를 처음부터 새로 만들기

개발자 고유의 Docker 기본 이미지를 처음부터 새로 만들 수 있습니다. 이 시나리오는 Docker를 시작하는 분들에게는 권장하지 않지만, 자신만의 고유한 기본 이미지 비트를 설정하고 싶은 분들은 그렇게 하셔도 됩니다.

### <a name="additional-resources"></a>추가 자료

-   **다중 아키텍처 .NET Core 이미지**.
https://github.com/dotnet/announcements/issues/14 
-   **기본 이미지 만들기**. 공식 Docker 설명서입니다.
    [*https://docs.docker.com/engine/userguide/eng-image/baseimages/*](https://docs.docker.com/engine/userguide/eng-image/baseimages/)

![](./media/image7.png)

## <a name="step-3-create-your-custom-docker-images-and-embed-your-application-or-service-in-them"></a>3단계. 고유의 사용자 지정 Docker 이미지를 만들고 그 안에 응용 프로그램 또는 서비스 포함

응용 프로그램의 서비스마다 관련 이미지를 만들어야 합니다. 응용 프로그램이 단일 서비스 또는 웹 응용 프로그램으로 구성된 경우 단일 이미지만 필요합니다.

Docker 이미지는 Visual Studio에서 자동으로 빌드됩니다. 다음 단계는 편집기/CLI 워크플로에만 필요하며 내부적으로 발생하는 동작에 대한 이해를 돕기 위해 설명되었습니다.

개발자는 완료된 기능 또는 변경 내용을 소스 제어 시스템(예: GitHub)으로 푸시할 때까지 로컬로 개발 및 테스트해야 합니다. 즉, Docker 이미지를 만들고 로컬 Docker 호스트(Windows 또는 Linux VM)에 컨테이너를 배포한 후 로컬 컨테이너에 대해 실행, 테스트 및 디버그해야 합니다.

로컬 환경에서 Docker CLI 및 Dockerfile을 사용하여 사용자 지정 이미지를 만들려면 그림 5-5처럼 docker build 명령을 사용합니다.

![](./media/image8.png)

**그림 5-5**. 사용자 지정 Docker 이미지 만들기

필요에 따라 프로젝트 폴더에서 직접 docker 빌드를 실행하는 대신, 먼저 dotnet publish를 실행하여 필수 .NET 라이브러리와 이진 파일로 배포 가능 폴더를 생성한 후 docker build 명령을 사용할 수 있습니다.

이렇게 하면 cesardl/netcore-webapi-microservice-docker:first라는 이름의 Docker 이미지가 만들어집니다. 이 경우 첫 번째는 특정 버전을 나타내는 태그입니다. 구성된 Docker 응용 프로그램에 대해 만들어야 하는 사용자 지정 이미지마다 이 단계를 반복할 수 있습니다.

또한 응용 프로그램이 여러 컨테이너로 구성된 경우(즉, 다중 컨테이너 응용 프로그램인 경우) docker-compose up --build 명령을 사용하여 관련 docker-compose.yml 파일에 노출된 메타데이터를 통해 단일 명령으로 모든 관련 이미지를 만들 수 있습니다.

그림 5-6처럼 docker images 명령을 사용하여 로컬 리포지토리에서 기존 이미지를 찾을 수 있습니다.

![](./media/image9.png)

**그림 5-6.** docker images 명령을 사용하여 기존 이미지 보기

### <a name="creating-docker-images-with-visual-studio"></a>Visual Studio로 Docker 이미지 만들기

Visual Studio를 사용하여 Docker가 지원되는 프로젝트를 만드는 경우 이미지를 명시적으로 만들지 마세요. 그 대신, F5 키를 눌러 Docker화된 응용 프로그램 또는 서비스를 실행하면 자동으로 이미지가 만들어집니다. 이 단계는 Visual Studio에서 자동으로 실행되며 사용자에게는 보이지 않습니다. 하지만 내부적으로 어떤 일이 발생하는지 알아두어야 합니다.

![](./media/image10.png)

## <a name="step-4-define-your-services-in-docker-composeyml-when-building-a-multi-container-docker-application"></a>4단계. 다중 컨테이너 Docker 응용 프로그램을 빌드할 때 docker compose.yml 파일에서 서비스 정의

[docker compose.yml](https://docs.docker.com/compose/compose-file/) 파일을 사용하여 배포 명령을 통해 구성된 응용 프로그램으로 배포할 관련 서비스 집합을 정의할 수 있습니다.

docker-compose.yml 파일을 사용하려면 기본 또는 루트 솔루션 폴더에 다음 예제와 비슷한 콘텐츠가 있는 파일을 만들어야 합니다.

```yml
version: '3'
  
services:

  webmvc:
    image: eshop/web
    environment:
      - CatalogUrl=http://catalog.api
      - OrderingUrl=http://ordering.api
    ports:
      - "80:80"
    depends_on:
      - catalog.api
      - ordering.api

  catalog.api:
    image: eshop/catalog.api
    environment: 
      - ConnectionString=Server=sql.data;Database=CatalogDB;…
    ports:
      - "81:80"
    depends_on:
      - sql.data

  ordering.api:
    image: eshop/ordering.api
    environment:
      - ConnectionString=Server=sql.data;Database=OrderingDb;…
    ports:
      - "82:80"
    extra_hosts:
      - "CESARDLBOOKVHD:10.0.75.1"
    depends_on:
      - sql.data

  sql.data:
    image: mssql-server-linux:latest
    environment:
      - SA_PASSWORD=Pass@word
      - ACCEPT_EULA=Y
    ports:
      - "5433:1433"

```

이 docker-compose.yml 파일은 단순화되고 병합된 버전입니다. 항상 적용되는 각 컨테이너에 대한 정적인 구성 데이터(사용자 지정 이미지처럼)와 연결 문자열처럼 배포 환경에 종속된 구성 정보를 포함합니다. 이후 섹션에서는 환경 및 실행 유형(디버그 또는 릴리스)에 따라 docker-compose.yml 구성을 여러 docker-compose 파일로 분할하고 값을 재정의하는 방법을 알아보겠습니다.

docker-compose.yml 파일 예제에서는 컨테이너로 실행되는 SQL Server for Linux를 기반으로 webmvc 서비스(웹 응용 프로그램), 2개의 마이크로 서비스(catalog.api 및 ordering.api), 1개의 데이터 원본 컨테이너, sql.data의 총 5개 서비스를 정의합니다. 각 서비스는 컨테이너로 배포되므로 각 서비스에 Docker 이미지가 필요합니다.

docker-compose.yml 파일은 사용되는 컨테이너뿐 아니라 개별적으로 구성되는 방법까지 지정합니다. 예를 들어 .yml 파일의 webmvc 컨테이너 정의는 다음과 같은 일을 합니다.

-   미리 빌드된 eshop/web:latest 이미지를 사용합니다. 그러나 docker-compose 파일의 빌드: 섹션을 기반으로 한 추가 구성을 사용하여 docker-compose 실행의 일부로 빌드되도록 이미지를 구성할 수도 있습니다.

-   두 환경 변수(CatalogUrl 및 OrderingUrl)를 초기화합니다.

-   컨테이너에 노출된 포트 80을 호스트 컴퓨터의 포트 80으로 전달합니다.

-   depends\_on 설정을 사용하여 웹앱을 카탈로그 및 주문 서비스와 연결합니다. 이렇게 하면 서비스는 이러한 서비스가 시작될 때까지 대기합니다.

이후 섹션에서 마이크로 서비스 및 다중 컨테이너 앱을 구현하는 방법을 알아볼 때 docker-compose.yml 파일을 다시 한 번 살펴보겠습니다.

### <a name="working-with-docker-composeyml-in-visual-studio-2017"></a>Visual Studio 2017에서 docker-compose.yml 파일 작업

그림 5-7처럼 Visual Studio 솔루션에서 서비스 프로젝트에 Docker 솔루션 지원을 추가하면 Visual Studio는 프로젝트에 Dockerfile을 추가하고 Dockerfile은 docker-compose.yml 파일을 통해 솔루션에서 서비스 섹션(프로젝트)을 추가합니다. 다중 컨테이너 솔루션 구성을 시작하는 쉬운 방법입니다. 그런 다음, docker-compose.yml 파일을 열고 추가 기능을 업데이트할 수 있습니다.

![](./media/image6.png)

**그림 5-7**. ASP.NET Core 프로젝트를 마우스 오른쪽 단추로 클릭하여 Visual Studio 2017에 Docker 지원 추가

Visual Studio에 Docker 지원을 추가하면 프로젝트에 Dockerfile이 추가될 뿐 아니라 솔루션 수준에서 설정된 docker-compose.yml 파일에 구성 정보가 추가됩니다.

Visual Studio에서 솔루션에 Docker 지원을 추가하면 그림 5-8처럼 추가된 docker-compose.yml 파일을 포함하는 새 노드(docker-compose.dcproj 프로젝트 파일에 있는)가 솔루션 탐색기에 표시됩니다.

![](./media/image11.PNG)

**그림 5-8**. Visual Studio 2017 솔루션 탐색기에 추가된 **docker-compose** 트리 노드

docker-compose up 명령을 사용하여 단일 docker-compose.yml 파일이 있는 다중 컨테이너 응용 프로그램을 배포할 수 있습니다. 그러나 Visual Studio에서 그룹으로 추가하므로 개발자는 환경(개발 또는 프로덕션) 및 실행 형식(릴리스 또는 디버그)에 따라 값을 재정의할 수 있습니다. 이 기능에 대한 내용은 이후 섹션에서 설명하겠습니다.

![](./media/image12.png)

## <a name="step-5-build-and-run-your-docker-application"></a>5단계. Docker 응용 프로그램을 빌드하고 실행

응용 프로그램에 단일 컨테이너만 있는 경우 응용 프로그램을 Docker 호스트(VM 또는 실제 서버)에 배포하여 실행할 수 있습니다. 그러나 응용 프로그램에 여러 서비스가 있는 경우에는 단일 CLI 명령(docker-compose up)을 사용하여 또는 이 명령을 내부적으로 실행하는 Visual Studio를 사용하여 구성된 응용 프로그램으로 배포할 수 있습니다. 다양한 옵션을 살펴보겠습니다.

### <a name="option-a-running-a-single-container-with-docker-cli"></a>옵션 A: Docker CLI로 단일 컨테이너 실행

그림 5-9처럼 docker run 명령을 사용하여 Docker 컨테이너를 실행할 수 있습니다.

```
  docker run -t -d -p 80:5000 cesardl/netcore-webapi-microservice-docker:first
```

![](./media/image13.png)

**그림 5-9**. docker run 명령을 사용하여 Docker 컨테이너 실행

이 경우 이 명령은 컨테이너의 내부 포트 5000을 호스트 컴퓨터의 포트 80에 바인딩합니다. 즉, 호스트가 포트 80에서 수신 대기하고 컨테이너의 포트 5000에 전달합니다.

### <a name="option-b-running-a-multi-container-application"></a>옵션 B: 다중 컨테이너 응용 프로그램 실행

대부분의 엔터프라이즈 시나리오에서 Docker 응용 프로그램은 여러 서비스로 구성되며, 따라서 그림 5-10처럼 다중 컨테이너 응용 프로그램을 실행해야 합니다.

![](./media/image14.png)

**그림 5-10**. Docker 컨테이너가 배포된 VM

#### <a name="running-a-multi-container-application-with-the-docker-cli"></a>Docker CLI를 사용하여 다중 컨테이너 응용 프로그램 실행

Docker CLI를 사용하여 다중 컨테이너 응용 프로그램을 실행하려면 docker-compose up 명령을 실행하면 됩니다. 이 명령은 솔루션 수준에서 docker-compose.yml 파일을 사용하여 다중 컨테이너 응용 프로그램을 배포합니다. 그림 5-11은 기본 프로젝트 디렉터리에서 명령을 실행할 때의 결과를 보여주며, docker-compose.yml 파일이 포함되어 있습니다.

![](./media/image15.png)

**그림 5-11**. docker-compose up 명령을 실행할 때의 결과 예제

docker-compose up 명령을 실행하면 그림 5-10에 보이는 VM처럼 응용 프로그램 및 관련 컨테이너가 Docker 호스트에 배포됩니다.

#### <a name="running-and-debugging-a-multi-container-application-with-visual-studio"></a>Visual Studio로 다중 컨테이너 응용 프로그램 실행 및 디버깅 

Visual Studio 2017을 사용하여 다중 컨테이너 응용 프로그램을 실행하는 방법이 더 이상 간단할 수 없습니다. 다중 컨테이너 응용 프로그램을 실행할 수 있을 뿐 아니라, 일반적인 중단점을 설정하여 Visual Studio에서 직접 모든 컨테이너를 디버그할 수 있습니다.

앞서 언급했듯이, 솔루션 내의 프로젝트에 Docker 솔루션 지원을 추가할 때마다 해당 프로젝트가 전역(솔루션 수준) docker-compose.yml 파일에서 구성되며, 따라서 전체 솔루션을 한꺼번에 실행 또는 디버그할 수 있습니다. Visual Studio는 Docker 솔루션 지원이 사용되는 각 프로젝트에 대해 하나의 컨테이너를 시작하고, 모든 내부 단계(dotnet 게시, dotnet 빌드 등)를 자동으로 수행합니다.

여기서 중요한 점은, 그림 5-12처럼 Visual Studio 2017에는 F5 키 작업에 대한 추가 **Docker** 명령이 있다는 것입니다. 이 옵션을 통해 솔루션 수준에서 docker-compose.yml 파일에 정의된 모든 컨테이너를 실행하여 다중 컨테이너 응용 프로그램을 디버깅할 수 있습니다. 다중 컨테이너 솔루션을 디버그하는 기능이 있다는 것은 서로 다른 프로젝트(컨테이너)마다 하나씩 여러 중단점을 지정할 수 있으며, Visual Studio에서 디버깅할 때 여러 프로젝트에서 정의되어 여러 컨테이너에서 실행되는 중단점에서 중지된다는 의미입니다.

![](./media/image16.png)

**그림 5-12**. Visual Studio 2017에서 다중 컨테이너 앱 실행

### <a name="additional-resources"></a>추가 자료

-   **원격 Docker 호스트에 ASP.NET 컨테이너 배포**
    [*https://docs.microsoft.com/azure/vs-azure-tools-docker-hosting-web-apps-in-docker*](https://docs.microsoft.com/azure/vs-azure-tools-docker-hosting-web-apps-in-docker)

### <a name="a-note-about-testing-and-deploying-with-orchestrators"></a>오케스트레이터를 사용하여 테스트 및 배포하는 내용에 대한 메모

docker-compose up 및 docker run 명령(또는 Visual Studio에서 컨테이너를 실행하고 디버깅)은 개발 환경에서 컨테이너를 테스트하기에 충분합니다. 하지만 Docker Swarm, Mesosphere DC/OS 또는 Kubernetes 같은 Docker 클러스터와 오케스트레이터를 대상으로 하는 경우에는 이 방법을 사용하면 안 됩니다. [Docker Swarm 모드](https://docs.docker.com/engine/swarm/)(Windows용 및 Mac용 Docker CE 버전 1.12부터 사용 가능) 같은 클러스터를 사용하는 경우 단일 서비스에 대한 [docker service create](https://docs.docker.com/engine/reference/commandline/service_create/) 같은 추가 명령을 사용하여 배포하고 테스트해야 합니다. 여러 컨테이너로 구성된 응용 프로그램을 배포하는 경우 [docker compose bundle](https://docs.docker.com/compose/reference/bundle/) 및 [docker deploy myBundleFile](https://docs.docker.com/engine/reference/commandline/deploy/)을 사용하여 구성된 응용 프로그램을 *스택*으로 배포합니다. 자세한 내용은 Docker 설명서의 블로그 게시물 [실험적 분산 응용 프로그램 번들 소개](https://blog.docker.com/2016/06/docker-app-bundle/)를 참조하세요. Docker 사이트에서 찾을 수 있습니다.

[DC/OS](https://mesosphere.com/blog/2015/09/02/dcos-cli-command-line-tool-datacenter/) 및 [Kubernetes](http://kubernetes.io/docs/user-guide/deployments/)의 경우 다양한 배포 명령 및 스크립트를 사용합니다.

![](./media/image17.png)

## <a name="step-6-test-your-docker-application-using-your-local-docker-host"></a>6단계. 로컬 Docker 호스트를 사용하여 Docker 응용 프로그램 테스트

이 단계는 응용 프로그램에서 하는 일에 따라 달라집니다. 단일 컨테이너 또는 서비스로 배포되는 간단한 .NET Core 웹 응용 프로그램에서는 그림 5-13처럼 Docker 호스트에서 브라우저를 열고 해당 사이트로 이동하여 서비스에 액세스할 수 있습니다. (Dockerfile의 구성이 컨테이너를 호스트에 있는 80 이외의 포트로 매핑하는 경우 호스트 포트를 URL에 포함합니다.)

![](./media/image18.png)

**그림 5-13**. localhost를 사용하여 로컬로 Docker 응용 프로그램을 테스트하는 예제

localhost가 Docker 호스트 IP를 가리키지 않는 경우(Docker CE를 사용하는 경우 기본적으로 Docker 호스트 IP를 가리켜야 함) 서비스를 탐색하려면 컴퓨터 네트워크 카드의 IP 주소를 사용합니다.

브라우저에서 이 URL은 우리가 살펴보고 있는 특정 컨테이너 예제에 대한 포트 80을 사용합니다. 그러나 내부적으로는 요청이 포트 5000으로 리디렉션됩니다. 왜냐하면 이전 단계에서 설명했듯이 docker run 명령을 사용하여 이와 같은 방법으로 배포되었기 때문입니다.

그림 5-14처럼 터미널에서 curl을 사용하여 응용 프로그램을 테스트할 수도 있습니다. Windows에 설치된 Docker에서 기본 Docker 호스트 IP는 컴퓨터의 실제 IP 주소와는 별개로 항상 10.0.75.1입니다.

![](./media/image19.png)

**그림 5-14**. curl을 사용하여 로컬로 Docker 응용 프로그램을 테스트하는 예제

### <a name="testing-and-debugging-containers-with-visual-studio-2017"></a>Visual Studio 2017을 사용하여 컨테이너 테스트 및 디버깅

Visual Studio 2017을 사용하여 컨테이너를 실행하고 디버깅할 때 컨테이너 없이 실행할 때와 거의 동일한 방법으로 .NET 응용 프로그램을 디버그할 수 있습니다.

### <a name="testing-and-debugging-without-visual-studio"></a>Visual Studio 없이 디버깅 및 테스트

편집기/CLI 방식을 사용하여 개발하는 경우 컨테이너를 디버깅하기가 훨씬 어려우며 추적을 생성하여 디버그하는 것이 좋습니다.

### <a name="additional-resources"></a>추가 자료

-   **로컬 Docker 컨테이너에서 앱 디버깅**
    [*https://docs.microsoft.com/azure/vs-azure-tools-docker-edit-and-refresh*](https://docs.microsoft.com/azure/vs-azure-tools-docker-edit-and-refresh)

-   **Steve Lasker. Docker를 사용하여 ASP.NET Core 앱 빌드, 디버그, 배포.** 비디오.
    [*https://channel9.msdn.com/Events/Visual-Studio/Visual-Studio-2017-Launch/T115*](https://channel9.msdn.com/Events/Visual-Studio/Visual-Studio-2017-Launch/T115)

## <a name="simplified-workflow-when-developing-containers-with-visual-studio"></a>Visual Studio를 사용하여 컨테이너를 개발할 때의 간소화된 워크플로

Visual Studio를 사용하면 편집기/CLI 방식을 사용할 때보다 워크플로가 훨씬 간단합니다. Dockerfile 및 docker-compose.yml 파일과 관련하여 Docker에 필요한 대부분의 단계는 그림 5-15처럼 숨겨져 있거나 Visual Studio를 통해 간소화됩니다.

![](./media/image20.png)

**그림 5-15**. Visual Studio를 사용하여 배포할 때의 간소화된 워크플로

또한 2단계(프로젝트에 Docker 지원 추가)를 한 번만 수행하면 됩니다. 따라서 다른 개발에서 .NET을 사용하여 수행하는 일반적인 개발 작업과 워크플로가 비슷합니다. 내부에서 어떤 동작이 발생하는지(이미지 빌드 프로세스, 사용하는 기본 이미지, 컨테이너 배포 등) 알아야 하며, 때로는 Dockerfile 또는 docker-compose.yml 파일을 편집하여 동작을 사용자 지정해야 합니다. 하지만 Visual Studio를 사용하여 대부분의 작업이 대폭 간소화되므로 개발자의 생산성이 크게 향상됩니다.

### <a name="additional-resources"></a>추가 자료

-   **Steve Lasker. Visual Studio 2017을 사용한 .NET Docker 개발**
    [*https://channel9.msdn.com/Events/Visual-Studio/Visual-Studio-2017-Launch/T111*](https://channel9.msdn.com/Events/Visual-Studio/Visual-Studio-2017-Launch/T111)

-   **Jeffrey T. Fritz. 새로운 Visual Studio용 Docker 도구로 컨테이너에 .NET Core 앱 배치**
    [*https://blogs.msdn.microsoft.com/webdev/2016/11/16/new-docker-tools-for-visual-studio/*](https://blogs.msdn.microsoft.com/webdev/2016/11/16/new-docker-tools-for-visual-studio/)

## <a name="using-powershell-commands-in-a-dockerfile-to-set-up-windows-containers"></a>DockerFile에서 PowerShell 명령을 사용하여 Windows 컨테이너 설정 

[Windows 컨테이너](https://msdn.microsoft.com/en-us/virtualization/windowscontainers/about/about_overview)를 사용하면 Docker 생태계의 나머지 부분과 동일한 도구로 기존 Windows 응용 프로그램을 Docker 이미지로 변환하고 배포할 수 있습니다. Windows 컨테이너를 사용하려면 다음 예제와 같이 Dockerfile에서 PowerShell 명령을 실행합니다.

```
FROM microsoft/windowsservercore
  
LABEL Description="IIS" Vendor="Microsoft" Version="10"
  
RUN powershell -Command Add-WindowsFeature Web-Server
  
CMD [ "ping", "localhost", "-t" ]
```

이 예에서는 PowerShell 명령(RUN 설정)을 통해 Windows Server Core 기본 이미지(FROM 설정)를 사용하고 IIS를 설치합니다. 비슷한 방법으로 PowerShell 명령을 사용하여 ASP.NET 4.x, .NET 4.6 또는 다른 Windows 소프트웨어 같은 추가 구성 요소를 설치할 수도 있습니다. 예를 들어 Dockerfile의 다음 명령은 ASP.NET 4.5를 설치합니다.

```
RUN powershell add-windowsfeature web-asp-net45
```

### <a name="additional-resources"></a>추가 자료

-   **aspnet-docker/Dockerfile.** Windows 기능을 포함하도록 dockerfile에서 실행되는 Powershell 명령 예제.
    [*https://github.com/Microsoft/aspnet-docker/blob/master/4.6.2/Dockerfile*](https://github.com/Microsoft/aspnet-docker/blob/master/4.6.2/Dockerfile)

>[!div class="step-by-step"]
[이전] (index.md) [다음] (../net-core-single-containers-linux-windows-server-hosts/index.md)
