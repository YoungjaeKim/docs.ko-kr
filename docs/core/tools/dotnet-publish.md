---
title: "dotnet publish 명령 - .NET Core CLI"
description: "dotnet publish 명령은 .NET Core 프로젝트를 디렉터리에 게시합니다."
author: mairaw
ms.author: mairaw
ms.date: 03/10/2018
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.workload:
- dotnetcore
ms.openlocfilehash: 2aa69217e949b970b632c4fad72838b63c2a8988
ms.sourcegitcommit: 83dd5ec003e788ccb3e33f3412a7af39ae347646
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="dotnet-publish"></a>dotnet publish

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet publish` - 호스팅 시스템에 배포하기 위해 응용 프로그램 및 해당 종속성을 폴더에 압축합니다.

## <a name="synopsis"></a>개요

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

```
dotnet publish [<PROJECT>] [-c|--configuration] [-f|--framework] [--force] [--manifest] [--no-dependencies] [--no-restore] [-o|--output] [-r|--runtime] [--self-contained] [-v|--verbosity] [--version-suffix]
dotnet publish [-h|--help]
```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

```
dotnet publish [<PROJECT>] [-c|--configuration] [-f|--framework] [-o|--output] [-r|--runtime] [-v|--verbosity] [--version-suffix]
dotnet publish [-h|--help]
```

---

## <a name="description"></a>설명

`dotnet publish`는 응용 프로그램을 컴파일하고 프로젝트 파일에 지정된 종속성을 읽은 다음 결과 파일 집합을 디렉터리에 게시합니다. 출력에는 다음이 포함됩니다.

* *dll* 확장과 함께 어셈블리의 IL(중간 언어) 코드
* 프로젝트의 종속성이 모두 포함된 *.deps.json* 파일
* 런타임에 대한 기타 구성 옵션(예: 가비지 수집 유형)뿐만 아니라 응용 프로그램에서 예상하는 공유 런타임을 지정하는 *.runtime.config.json* 파일
* 응용 프로그램의 종속성. 이러한 종속성은 NuGet 캐시에서 출력 폴더로 복사됩니다.

`dotnet publish` 명령의 출력은 실행을 위해 호스팅 시스템(예: 서버, PC, Mac, 랩톱)으로 배포할 준비가 되었으며 응용 프로그램의 배포를 준비하는 공식적으로 지원되는 유일한 방법입니다. 프로젝트에서 지정하는 배포 유형에 따라 호스팅 시스템에 .NET Core 공유 런타임이 설치되어 있을 수도 있고 그렇지 않을 수도 있습니다. 자세한 내용은 [.NET Core 응용 프로그램 배포](../deploying/index.md)를 참조하세요. 게시된 응용 프로그램의 디렉터리 구조에 대해서는 [디렉터리 구조](/aspnet/core/hosting/directory-structure)를 참조하세요.

[!INCLUDE[dotnet restore note + options](~/includes/dotnet-restore-note-options.md)]

## <a name="arguments"></a>인수

`PROJECT`

게시할 프로젝트이며, 지정하지 않을 경우 현재 디렉터리로 기본 설정됩니다.

## <a name="options"></a>옵션

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

`-c|--configuration {Debug|Release}`

빌드 구성을 정의합니다. 기본값은 `Debug`입니다.

`-f|--framework <FRAMEWORK>`

지정한 [대상 프레임워크](../../standard/frameworks.md)에 대한 응용 프로그램을 게시합니다. 프로젝트 파일에 대상 프레임워크를 지정해야 합니다.

`--force`

마지막 복원이 성공한 경우에도 모든 종속성을 강제 확인합니다. 이것은 *project.assets.json* 파일을 삭제하는 것과 같습니다.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`--manifest <PATH_TO_MANIFEST_FILE>`

앱을 통해 게시된 패키지 집합을 잘라내는 데 사용할 하나 이상의 [대상 매니페스트](../deploying/runtime-store.md)를 지정합니다. 매니페스트 파일은 [`dotnet store` 명령](dotnet-store.md) 출력의 일부입니다. 여러 매니페스트를 지정하려면 각 매니페스트에 대해 `--manifest` 옵션을 추가합니다. 이 옵션은 .NET Core 2.0 SDK부터 사용할 수 있습니다.

`--no-dependencies`

프로젝트 간 참조를 무시하고 루트 프로젝트만 복원합니다.

`--no-restore`

명령을 실행할 때 암시적 복원을 수행하지 않습니다.

`-o|--output <OUTPUT_DIRECTORY>`

출력 디렉터리의 경로를 지정합니다. 지정하지 않으면 프레임워크 종속 배포의 경우 *./bin/[configuration]/[framework]/*로, 자체 포함 배포의 경우 *./bin/[configuration]/[framework]/[runtime]*으로 기본 설정됩니다.
상대 경로가 제공되는 경우 생성된 출력 디렉터리는 현재 작업 디렉터리가 아닌 프로젝트 파일 위치에 상대적입니다.

`--self-contained`

대상 컴퓨터에 런타임을 설치할 필요가 없도록 응용 프로그램을 통해 .NET Core 런타임을 게시합니다. 런타임 식별자를 지정할 경우 기본값은 `true`입니다. 다른 배포 형식에 대한 자세한 내용은 [.NET Core 응용 프로그램 배포](../deploying/index.md)를 참조하세요.

`-r|--runtime <RUNTIME_IDENTIFIER>`

지정된 런타임에 대한 응용 프로그램을 게시합니다. [SCD(자체 포함 배포_](../deploying/index.md#self-contained-deployments-scd)를 만들 때 사용됩니다. RID(런타임 식별자) 목록은 [RID 카탈로그](../rid-catalog.md)를 참조하세요. 기본값은 [FDD(프레임워크 종속 배포)](../deploying/index.md#framework-dependent-deployments-fdd)를 게시하는 것입니다.

`-v|--verbosity <LEVEL>`

명령의 세부 정보 표시 수준을 설정합니다. 허용되는 값은 `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, `diag[nostic]`입니다.

`--version-suffix <VERSION_SUFFIX>`

프로젝트 파일의 버전 필드에서 별표(`*`)를 대신할 버전 접미사를 정의합니다.

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`-c|--configuration {Debug|Release}`

빌드 구성을 정의합니다. 기본값은 `Debug`입니다.

`-f|--framework <FRAMEWORK>`

지정한 [대상 프레임워크](../../standard/frameworks.md)에 대한 응용 프로그램을 게시합니다. 프로젝트 파일에 대상 프레임워크를 지정해야 합니다.

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.

`--manifest <PATH_TO_MANIFEST_FILE>`

앱을 통해 게시된 패키지 집합을 잘라내는 데 사용할 하나 이상의 [대상 매니페스트](../deploying/runtime-store.md)를 지정합니다. 매니페스트 파일은 [`dotnet store` 명령](dotnet-store.md) 출력의 일부입니다. 여러 매니페스트를 지정하려면 각 매니페스트에 대해 `--manifest` 옵션을 추가합니다. 이 옵션은 .NET Core 2.0 SDK부터 사용할 수 있습니다.

`-o|--output <OUTPUT_DIRECTORY>`

출력 디렉터리의 경로를 지정합니다. 지정하지 않으면 프레임워크 종속 배포의 경우 *./bin/[configuration]/[framework]/*로, 자체 포함 배포의 경우 *./bin/[configuration]/[framework]/[runtime]*으로 기본 설정됩니다.
상대 경로가 제공되는 경우 생성된 출력 디렉터리는 현재 작업 디렉터리가 아닌 프로젝트 파일 위치에 상대적입니다.

`-r|--runtime <RUNTIME_IDENTIFIER>`

지정된 런타임에 대한 응용 프로그램을 게시합니다. [SCD(자체 포함 배포_](../deploying/index.md#self-contained-deployments-scd)를 만들 때 사용됩니다. RID(런타임 식별자) 목록은 [RID 카탈로그](../rid-catalog.md)를 참조하세요. 기본값은 [FDD(프레임워크 종속 배포)](../deploying/index.md#framework-dependent-deployments-fdd)를 게시하는 것입니다.

`-v|--verbosity <LEVEL>`

명령의 세부 정보 표시 수준을 설정합니다. 허용되는 값은 `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, `diag[nostic]`입니다.

`--version-suffix <VERSION_SUFFIX>`

프로젝트 파일의 버전 필드에서 별표(`*`)를 대신할 버전 접미사를 정의합니다.

---

## <a name="examples"></a>예제

현재 디렉터리에 있는 프로젝트를 게시합니다.

`dotnet publish`

지정된 프로젝트 파일을 사용하여 응용 프로그램을 게시합니다.

`dotnet publish ~/projects/app1/app1.csproj`

`netcoreapp1.1` 프레임워크를 사용하여 현재 디렉터리에 있는 프로젝트를 게시합니다.

`dotnet publish --framework netcoreapp1.1`

`netcoreapp1.1` 프레임워크 및 `OS X 10.10`에 대한 런타임을 사용하여 현재 응용 프로그램을 게시합니다. 프로젝트 파일에서 이 RID를 나열해야 합니다.

`dotnet publish --framework netcoreapp1.1 --runtime osx.10.11-x64`

현재 응용 프로그램을 게시하지만 프로젝트 간(P2P) 참조를 복원하지 않습니다. 복원 작업 중 루트 프로젝트만 복원합니다(.NET Core SDK 2.0 이상 버전).

`dotnet publish --no-dependencies`

## <a name="see-also"></a>참고 항목

* [대상 프레임워크](../../standard/frameworks.md)
* [RID(런타임 식별자) 카탈로그](../rid-catalog.md)