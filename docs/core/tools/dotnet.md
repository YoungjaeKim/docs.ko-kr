---
title: dotnet 명령 - .NET Core CLI
description: dotnet 명령(.NET Core CLI 도구에 대한 일반 드라이버) 및 사용법에 대해 알아봅니다.
author: mairaw
ms.author: mairaw
ms.date: 03/20/2018
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.workload:
- dotnetcore
ms.openlocfilehash: 2d22124cb613152df402046541650f3262e7e202
ms.sourcegitcommit: 6f967c86dde55472440f0c8669b0e910ee3c53ba
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="dotnet-command"></a>dotnet 명령

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet` - 명령줄 명령을 실행하기 위한 일반 드라이버입니다.

## <a name="synopsis"></a>개요

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)
```
dotnet [command] [arguments] [--additional-deps] [--additionalprobingpath] [-d|--diagnostics]
    [--fx-version] [-h|--help] [--info] [--roll-forward-on-no-candidate-fx] [-v|--verbosity] [--version]
```
# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)
```
dotnet [command] [arguments] [--additionalprobingpath] [-d|--diagnostics] [--fx-version]
    [-h|--help] [--info] [-v|--verbosity] [--version]
```
---

## <a name="description"></a>설명

`dotnet`은 CLI(명령줄 인터페이스) 도구 체인에 대한 일반 드라이버입니다. 자체적으로 호출되어 간단한 사용 방법을 제공합니다.

각 특정 기능은 명령으로 구현됩니다. 기능을 사용하려면 [`dotnet build`](dotnet-build.md)와 같이 `dotnet`뒤에 명령을 지정합니다. 명령 다음에 오는 모든 인수는 고유한 인수입니다.

`dotnet` 자체가 명령으로 사용되는 유일한 경우는 [프레임워크 종속 앱](../deploying/index.md)을 실행하는 경우입니다. `dotnet` 동사 뒤에 응용 프로그램 DLL을 지정하여 응용 프로그램을 실행합니다(예: `dotnet myapp.dll`).

## <a name="options"></a>옵션

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

`--additional-deps <PATH>`

추가적인 *deps.json* 파일의 경로입니다.

`--additionalprobingpath <PATH>`

검색 정책 및 검색할 어셈블리를 포함하는 경로입니다.

`-d|--diagnostics`

진단 출력을 사용합니다.

`--fx-version <VERSION>`

응용 프로그램 실행에 사용할 설치된 .NET Core 런타임의 버전입니다.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다. `dotnet`과 함께 사용되는 경우 사용 가능한 명령 목록도 출력합니다.

`--info`

현재 운영 체제, 버전에 대한 SHA 커밋 및 기타 정보 등 CLI 도구 및 환경에 대한 자세한 정보를 출력합니다.

`--roll-forward-on-no-candidate-fx`

 후보 공유 프레임워크에서는 롤포워드하지 않습니다.

`-v|--verbosity <LEVEL>`

명령의 세부 정보 표시 수준을 설정합니다. 허용되는 값은 `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, `diag[nostic]`입니다. 모든 명령에서 지원되지 않습니다. 이 옵션을 사용할 수 있는지 확인하려면 특정 명령 페이지를 참조하세요.

`--version`

사용 중인 .NET Core SDK 버전을 출력합니다.

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`--additionalprobingpath <PATH>`

검색 정책 및 검색할 어셈블리를 포함하는 경로입니다.

`-d|--diagnostics`

진단 출력을 사용합니다.

`--fx-version <VERSION>`

응용 프로그램 실행에 사용할 설치된 .NET Core 런타임의 버전입니다.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다. `dotnet`과 함께 사용되는 경우 사용 가능한 명령 목록도 출력합니다.

`--info`

현재 운영 체제, 버전에 대한 SHA 커밋 및 기타 정보 등 CLI 도구 및 환경에 대한 자세한 정보를 출력합니다.

`-v|--verbosity <LEVEL>`

명령의 세부 정보 표시 수준을 설정합니다. 허용되는 값은 `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, `diag[nostic]`입니다. 모든 명령에서 지원되지 않습니다. 이 옵션을 사용할 수 있는지 확인하려면 특정 명령 페이지를 참조하세요.

`--version`

사용 중인 .NET Core SDK 버전을 출력합니다.

---

## <a name="dotnet-commands"></a>dotnet 명령

### <a name="general"></a>일반

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

| 명령                             | 함수                                                            |
| ----------------------------------- | ------------------------------------------------------------------- |
| [dotnet build](dotnet-build.md)     | .NET Core 응용 프로그램을 빌드합니다.                                     |
| [dotnet clean](dotnet-clean.md)     | 빌드 출력을 정리합니다.                                              |
| [dotnet help](dotnet-help.md)       | 명령에 대한 자세한 온라인 설명서를 표시합니다.           |
| [dotnet migrate](dotnet-migrate.md) | 유효한 Preview 2 프로젝트를 .NET Core SDK 1.0 프로젝트로 마이그레이션합니다.  |
| [dotnet msbuild](dotnet-msbuild.md) | MSBuild 명령줄에 대한 액세스 권한을 제공합니다.                        |
| [dotnet new](dotnet-new.md)         | 지정한 템플릿에 대해 C# 또는 F# 프로젝트를 초기화합니다.                |
| [dotnet pack](dotnet-pack.md)       | 코드의 NuGet 패키지를 만듭니다.                               |
| [dotnet publish](dotnet-publish.md) | .NET Framework 종속형 또는 자체 포함 응용 프로그램을 게시합니다. |
| [dotnet restore](dotnet-restore.md) | 지정된 응용 프로그램에 대한 종속성을 복원합니다.                  |
| [dotnet run](dotnet-run.md)         | 소스에서 응용 프로그램을 실행합니다.                                   |
| [dotnet sln](dotnet-sln.md)         | 솔루션 파일에 프로젝트를 추가, 제거 및 나열하는 옵션입니다.       |
| [dotnet store](dotnet-store.md)     | 어셈블리를 런타임 패키지 저장소에 저장합니다.                     |
| [dotnet test](dotnet-test.md)       | Test Runner를 사용하여 테스트를 실행합니다.                                     |

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

| 명령                             | 함수                                                            |
| ----------------------------------- | ------------------------------------------------------------------- |
| [dotnet build](dotnet-build.md)     | .NET Core 응용 프로그램을 빌드합니다.                                     |
| [dotnet clean](dotnet-clean.md)     | 빌드 출력을 정리합니다.                                              |
| [dotnet migrate](dotnet-migrate.md) | 유효한 Preview 2 프로젝트를 .NET Core SDK 1.0 프로젝트로 마이그레이션합니다.  |
| [dotnet msbuild](dotnet-msbuild.md) | MSBuild 명령줄에 대한 액세스 권한을 제공합니다.                        |
| [dotnet new](dotnet-new.md)         | 지정한 템플릿에 대해 C# 또는 F# 프로젝트를 초기화합니다.                |
| [dotnet pack](dotnet-pack.md)       | 코드의 NuGet 패키지를 만듭니다.                               |
| [dotnet publish](dotnet-publish.md) | .NET Framework 종속형 또는 자체 포함 응용 프로그램을 게시합니다. |
| [dotnet restore](dotnet-restore.md) | 지정된 응용 프로그램에 대한 종속성을 복원합니다.                  |
| [dotnet run](dotnet-run.md)         | 소스에서 응용 프로그램을 실행합니다.                                   |
| [dotnet sln](dotnet-sln.md)         | 솔루션 파일에 프로젝트를 추가, 제거 및 나열하는 옵션입니다.       |
| [dotnet test](dotnet-test.md)       | Test Runner를 사용하여 테스트를 실행합니다.                                     |

---

### <a name="project-references"></a>프로젝트 참조

명령 | 함수
--- | ---
[dotnet add reference](dotnet-add-reference.md) | 프로젝트 참조를 추가합니다.
[dotnet list reference](dotnet-list-reference.md) | 프로젝트 참조를 나열합니다.
[dotnet remove reference](dotnet-remove-reference.md) | 프로젝트 참조를 제거합니다.

### <a name="nuget-packages"></a>NuGet 패키지

명령 | 함수
--- | ---
[dotnet add package](dotnet-add-package.md) | NuGet 패키지를 추가합니다.
[dotnet remove package](dotnet-remove-package.md) | NuGet 패키지를 제거합니다.

### <a name="nuget-commands"></a>NuGet 명령

명령 | 함수
--- | ---
[dotnet nuget delete](dotnet-nuget-delete.md) | 서버에서 패키지를 삭제하거나 목록에서 제거합니다.
[dotnet nuget locals](dotnet-nuget-locals.md) | http-request 캐시, 임시 캐시 또는 시스템 전체의 글로벌 패키지 폴더와 같은 로컬 NuGet 리소스를 지우거나 목록에 포함합니다.
[dotnet nuget push](dotnet-nuget-push.md) | 서버에 패키지를 푸시하고 게시합니다.

## <a name="examples"></a>예제

컴파일하고 실행할 수 있는 샘플 .NET Core 콘솔 응용 프로그램을 초기화합니다.

`dotnet new console`

지정된 응용 프로그램에 대한 종속성을 복원합니다.

`dotnet restore`

[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

지정된 디렉터리에서 프로젝트 및 해당 종속성을 빌드합니다.

`dotnet build`

이름이 `myapp.dll`인 프레임워크 종속형 앱을 실행합니다.

`dotnet myapp.dll`

## <a name="environment-variables"></a>환경 변수

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

`DOTNET_PACKAGES`

주 패키지 캐시입니다. 설정하지 않으면 기본적으로 Unix에서는 `$HOME/.nuget/packages`, Windows에서는 `%HOME%\NuGet\Packages`로 지정됩니다.

`DOTNET_SERVICING`

런타임을 로드할 때 공유 호스트에서 사용할 서비스 인덱스의 위치를 지정합니다.

`DOTNET_CLI_TELEMETRY_OPTOUT`

.NET Core 도구 사용에 대한 데이터를 수집하여 Microsoft에 전송할지 여부를 지정합니다. 원격 분석 기능을 옵트아웃하려면 `true`(값 `true`, `1` 또는 `yes` 허용)로 설정하고, 원격 분석 기능을 옵트인하려면 `false`(값 `false`, `0` 또는 `no` 허용)로 설정합니다. 설정하지 않으면 기본적으로 `false`이고 원격 분석 기능은 활성화됩니다.

`DOTNET_MULTILEVEL_LOOKUP`

전역 위치에서 .NET Core 런타임, 공유 프레임워크 또는 SDK가 확인되는지 여부를 지정합니다. 설정하지 않은 경우 기본값은 `true`입니다. 전역 위치에서 확인하지 않고 격리된 .NET Core 설치를 가지려면 `false`로 설정합니다(값 `0` 또는 `false`는 허용됨). 다중 수준의 조회에 대한 자세한 내용은 [다중 수준 SharedFX 조회](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/multilevel-sharedfx-lookup.md)를 참조하세요.

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`DOTNET_PACKAGES`

주 패키지 캐시입니다. 설정하지 않으면 기본적으로 Unix에서는 `$HOME/.nuget/packages`, Windows에서는 `%HOME%\NuGet\Packages`로 지정됩니다.

`DOTNET_SERVICING`

런타임을 로드할 때 공유 호스트에서 사용할 서비스 인덱스의 위치를 지정합니다.

`DOTNET_CLI_TELEMETRY_OPTOUT`

.NET Core 도구 사용에 대한 데이터를 수집하여 Microsoft에 전송할지 여부를 지정합니다. 원격 분석 기능을 옵트아웃하려면 `true`(값 `true`, `1` 또는 `yes` 허용)로 설정하고, 원격 분석 기능을 옵트인하려면 `false`(값 `false`, `0` 또는 `no` 허용)로 설정합니다. 설정하지 않으면 기본적으로 `false`이고 원격 분석 기능은 활성화됩니다.

---
