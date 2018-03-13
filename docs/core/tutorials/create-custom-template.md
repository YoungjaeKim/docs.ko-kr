---
title: "dotnet new에 대한 사용자 지정 템플릿 만들기"
description: "이 재미있는 자습서에서 dotnet new 명령에 대한 사용자 지정 템플릿을 만드는 방법을 알아봅니다."
keywords: ".NET, .NET Core, 템플릿, 템플릿 지정, 자습서, dotnet new"
author: guardrex
ms.author: mairaw
ms.date: 08/12/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 519b910a-6efe-4394-9b81-0546aa3e7462
ms.workload:
- dotnetcore
ms.openlocfilehash: bf523ead40d0e3cc9148b48d5c7a4a84d3d5cb81
ms.sourcegitcommit: d95a91d685565f4d95c8773b558752864a6a3d7e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2018
---
# <a name="create-a-custom-template-for-dotnet-new"></a>dotnet new에 대한 사용자 지정 템플릿 만들기

이 자습서에서는 다음을 수행하는 방법을 보여 줍니다.

- 기존 프로젝트 또는 새 콘솔 앱 프로젝트에서 기본 템플릿을 만듭니다.
- nuget.org 또는 로컬 *nupkg* 파일을 통해 배포하기 위해 템플릿을 압축합니다.
- nuget.org, 로컬 *nupkg* 파일 또는 로컬 파일 시스템에서 템플릿을 설치합니다.
- 템플릿을 제거합니다.

전체 샘플에 대한 자습서를 수행하려면 [샘플 프로젝트 템플릿](https://github.com/dotnet/dotnet-template-samples/tree/master/16-nuget-package)을 다운로드합니다. 샘플 템플릿은 NuGet 배포에 사용되도록 구성됩니다.

다운로드된 샘플을 파일 시스템 배포에서 사용하려면 다음을 수행합니다.

- 샘플의 *content* 폴더를 한 수준 위의 *GarciaSoftware.ConsoleTemplate.CSharp* 폴더로 이동합니다.
- 빈 *content* 폴더를 삭제합니다.
- *nuspec* 파일을 삭제합니다.

## <a name="prerequisites"></a>전제 조건

- [.NET Core 2.0 SDK](https://www.microsoft.com/net/core) 이상 버전을 설치합니다.
- 참조 항목 [dotnet new에 대한 사용자 지정 템플릿](../tools/custom-templates.md)을 읽어보세요.

## <a name="create-a-template-from-a-project"></a>프로젝트에서 템플릿 만들기

컴파일 및 실행되는 것으로 확인한 기존 프로젝트를 사용하거나 하드 드라이브의 폴더에서 새 콘솔 앱 프로젝트를 만듭니다. 이 자습서에서는 프로젝트 폴더 이름은 사용자 프로필의 *Documents\Templates*에 저장된 *GarciaSoftware.ConsoleTemplate.CSharp*입니다. 이 자습서의 프로젝트 템플릿 이름은 *\<회사 이름>.\<템플릿 형식>.\<프로그래밍 언어>*이지만, 프로젝트와 템플릿에 원하는 이름을 지정할 수 있습니다.

1. 프로젝트의 루트에 *.template.config*라는 폴더를 추가합니다.
1. *.template.config* 폴더 내부에서 *template.json* 파일을 만들어 템플릿을 구성합니다. 에 대 한 자세한 정보와 멤버 정의 대 한는 *template.json* 파일, 참조는 [새 dotnet 용 사용자 지정 템플릿](../tools/custom-templates.md#templatejson) 항목 및 [ *template.json* JSON 스키마 저장소에서 스키마](http://json.schemastore.org/template)합니다.

```json
{
    "$schema": "http://json.schemastore.org/template",
    "author": "Catalina Garcia",
    "classifications": [ "Common", "Console" ],
    "identity": "GarciaSoftware.ConsoleTemplate.CSharp",
    "name": "Garcia Software Console Application",
    "shortName": "garciaconsole"
}
```

템플릿이 완료됩니다. 현재는 템플릿 배포를 위한 두 가지 옵션이 있습니다. 이 자습서를 계속하려면 어느 것이든 경로를 선택합니다.

1. [NuGet 배포](#use-nuget-distribution): NuGet 또는 로컬 *nupkg* 파일에서 템플릿을 설치하고 설치된 템플릿을 사용합니다.
2. [파일 시스템 배포](#use-file-system-distribution).

## <a name="use-nuget-distribution"></a>NuGet 배포 사용

### <a name="pack-the-template-into-a-nuget-package"></a>템플릿을 NuGet 패키지로 압축

1. NuGet 패키지에 대한 폴더를 만듭니다. 자습서의 경우 폴더 이름 *GarciaSoftware.ConsoleTemplate.CSharp*가 사용되고 폴더는 사용자 프로필의 *Documents\NuGetTemplates* 폴더 내부에 만들어집니다. 새 템플릿 폴더 내부에 *content*라는 폴더를 만들어 프로젝트 파일을 저장합니다.
1. 프로젝트 폴더의 콘텐츠와 함께 *.template.config/template.json* 파일을 직접 만든 *content* 폴더로 복사합니다.
1. *콘텐츠* 폴더 옆에 [*nuspec* 파일](/nuget/create-packages/creating-a-package)을 추가합니다. 패키지 콘텐츠를 설명하고 NuGet 패키지를 만드는 프로세스를 적용하는 XML 매니페스트 파일입니다.
   
   ![NuGet 패키지의 레이아웃을 보여 주는 디렉터리 구조](./media/create-custom-template/nugetdirectorylayout.png)

1. *nuspec* 파일의 **\<packageTypes>** 요소 내부에는 **\<packageType>** 요소와 `Template`의 `name` 특성 값이 포함됩니다. *content* 폴더와 *nuspec* 파일은 동일한 디렉터리에 있어야 합니다. 표에서는 템플릿을 NuGet 패키지로 생성하는 데 필요한 최소 *nuspec* 파일 요소를 보여 줍니다.

   | 요소            | 형식   | 설명 |
   | ------------------ | ------ | ----------- |
   | **\<authors>**     | string | nuget.org에서 프로필 이름과 일치하는, 쉼표로 구분된 패키지 작성자 목록입니다. 작성자는 nuget.org의 NuGet 갤러리에 표시되고 동일한 작성자가 패키지를 상호 참조하는 데 사용됩니다. |
   | **\<description>** | string | UI 표시를 위한 패키지에 대한 자세한 설명입니다. |
   | **\<id>**          | string | nuget.org 또는 무엇이든 패키지가 상주하는 갤러리에서 고유해야 하는 대/소문자를 구분하지 않는 패키지 식별자입니다. ID는 URL에 유효하지 않은 공백이나 문자를 포함할 수 없고 일반적으로 .NET 네임스페이스 규칙을 따릅니다. 자세한 내용은 [고유한 패키지 식별자 선택 및 버전 번호 설정](/nuget/create-packages/creating-a-package#choosing-a-unique-package-identifier-and-setting-the-version-number)을 참조하세요. |
   | **\<packageType>** | string | **\<metadata>** 요소 중 **\<packageTypes>** 요소 내부에 이 요소를 삽입합니다. **\<packageType>** 요소의 `name` 특성을 `Template`으로 설정합니다. |
   | **\<version>**     | string | major.minor.patch 패턴을 따르는 패키지 버전입니다. 버전 번호는 [시험판 버전](/nuget/create-packages/prerelease-packages#semantic-versioning)의 설명대로 시험판 접미사를 포함할 수 있습니다. |

   전체 *nuspec* 파일 스키마는 [.nuspec reference](/nuget/schema/nuspec)(.nuspec 참조)를 참조하세요.

   자습서에 사용된 *nuspec* 파일의 이름은 *GarciaSoftware.ConsoleTemplate.CSharp.nuspec*이고 이 파일은 다음 콘텐츠를 포함합니다.

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
     <metadata>
       <id>GarciaSoftware.ConsoleTemplate.CSharp</id>
       <version>1.0.0</version>
       <description>
         Creates the Garcia Software console app.
       </description>
       <authors>Catalina Garcia</authors>
       <packageTypes>
         <packageType name="Template" />
       </packageTypes>
     </metadata>
   </package>
   ```

1. `nuget pack <PATH_TO_NUSPEC_FILE>` 명령을 사용하여 [패키지를 만듭니다](/nuget/create-packages/creating-a-package#creating-the-package). 다음 명령은 NuGet 자산을 저장하는 폴더가 *C:\Users\\\<USER>\Documents\Templates\GarciaSoftware.ConsoleTemplate.CSharp\*라고 가정합니다. 하지만 시스템에서 폴더가 어디에 있든지 `nuget pack` 명령은 *nuspec* 파일의 경로를 허용합니다.

   ```console
   nuget pack C:\Users\<USER>\Documents\NuGetTemplates\GarciaSoftware.ConsoleTemplate.CSharp\GarciaSoftware.ConsoleTemplate.CSharp.nuspec
   ```

### <a name="publishing-the-package-to-nugetorg"></a>nuget.org에 패키지 게시

NuGet 패키지를 게시하려면 [패키지 만들기 및 게시](/nuget/quickstart/create-and-publish-a-package#publish-the-package) 항목의 지침을 따릅니다. 그러나 게시된 후에는 삭제할 수 없고 목록에서만 제거되므로 자습서 템플릿을 NuGet에 게시하지 않는 것이 좋습니다. 이제 *nupkg* 파일 형식의 NuGet 패키지가 준비되었으므로 아래 지침에 따라 로컬 *nupkg* 파일에서 직접 템플릿을 설치해 보세요.

### <a name="install-the-template-from-a-nuget-package"></a>NuGet 패키지에서 템플릿 설치

#### <a name="install-the-template-from-the-local-nupkg-file"></a>로컬 *nupkg* 파일에서 템플릿 설치

직접 생성한 *nupkg* 파일에서 템플릿을 설치하려면 `dotnet new` 명령과 `-i|--install` 옵션을 함께 사용하고 *nupkg* 파일 경로를 제공합니다.

```console
dotnet new -i C:\Users\<USER>\GarciaSoftware.ConsoleTemplate.CSharp.1.0.0.nupkg
```

#### <a name="install-the-template-from-a-nuget-package-stored-at-nugetorg"></a>nuget.org에 저장된 NuGet 패키지에서 템플릿 설치

nuget.org에 저장된 NuGet 패키지에서 템플릿을 설치하려면 `dotnet new` 명령을 `-i|--install` 옵션과 함께 사용하고 NuGet 패키지 이름을 제공합니다.

```console
dotnet new -i GarciaSoftware.ConsoleTemplate.CSharp
```

> [!NOTE]
> 예제는 데모용으로만 제공됩니다. nuget.org에는 `GarciaSoftware.ConsoleTemplate.CSharp` NuGet 패키지가 없으므로 NuGet에서 테스트 템플릿을 게시 및 사용하지 않는 것이 좋습니다. 명령을 실행해도 템플릿이 설치되지 않습니다. 그러나 이전 섹션 [로컬 nupkg 파일에서 템플릿 설치](#install-the-template-from-the-local-nupkg-file)에 설명된 대로 로컬 파일 시스템에서 직접 *nupkg* 파일을 참조하면 nuget.org에 게시되지 않은 템플릿을 설치할 수 있습니다.

nuget.org의 패키지에서 템플릿을 설치하는 방법의 생생한 예제를 확인하려면 [NUnit 3 template for dotnet-new](https://www.nuget.org/packages/NUnit3.DotNetNew.Template/)(dotnet-new에 대한 NUnit 3 템플릿)를 사용하면 됩니다. 이 템플릿은 NUnit 유닛 테스트를 사용하도록 프로젝트를 설정합니다. 다음 명령을 사용하여 템플릿을 설치합니다.

```console
dotnet new -i NUnit3.DotNetNew.Template
```

`dotnet new -l`을 사용하여 템플릿을 나열하면 템플릿 목록에서 *nunit*의 짧은 이름을 가진 *NUnit 3 테스트 프로젝트*가 표시됩니다. 다음 섹션에서 템플릿을 사용할 준비가 되었습니다.

![다른 설치된 템플릿과 함께 NUnit 템플릿을 보여 주는 콘솔 창](./media/create-custom-template/nunit1.png)

### <a name="create-a-project-from-the-template"></a>템플릿에서 프로젝트 만들기

NuGet에서 템플릿이 설치된 후 템플릿 엔진의 출력을 배치할 디렉터리에서 `dotnet new <TEMPLATE>` 명령을 실행하여 템플릿을 사용합니다(`-o|--output` 옵션을 사용하여 특정 디렉터리를 지정하는 경우 제외). 자세한 내용은 [`dotnet new` 옵션](~/docs/core/tools/dotnet-new.md#options)을 참조하세요. 템플릿의 짧은 이름을 `dotnet new` 명령에 직접 제공합니다. NUnit 템플릿에서 프로젝트를 만들려면 다음 명령을 실행합니다.

```console
dotnet new nunit
```

콘솔에서는 프로젝트가 만들어지고 프로젝트의 패키지가 복원되는 것을 보여 줍니다. 명령이 실행된 후 프로젝트를 사용할 준비가 되었습니다.

![NUnit 프로젝트를 만들고 프로젝트 종속성을 복원할 때 dotnet new 명령의 출력을 보여 주는 콘솔 창](./media/create-custom-template/nunit2.png)

### <a name="to-uninstall-a-template-from-a-nuget-package-stored-at-nugetorg"></a>nuget.org에 저장된 NuGet 패키지에서 템플릿을 제거하려면

```console
dotnet new -u GarciaSoftware.ConsoleTemplate.CSharp
```

> [!NOTE]
> 예제는 데모용으로만 제공됩니다. nuget.org에 저장되거나 .NET Core SDK와 함께 설치되는 `GarciaSoftware.ConsoleTemplate.CSharp` NuGet 패키지는 없습니다. 명령을 실행하면 패키지/템플릿이 제거되지 않고 다음 예외가 표시됩니다.
> 
> > 'GarciaSoftware.ConsoleTemplate.CSharp'라는 제거할 항목을 찾을 수 없습니다.

이미 설치한 [dotnet-new에 대한 NUnit 3 템플릿](https://www.nuget.org/packages/NUnit3.DotNetNew.Template/)을 제거하려면 다음 명령을 사용합니다.

```console
dotnet new -u NUnit3.DotNetNew.Template
```

### <a name="uninstall-the-template-from-a-local-nupkg-file"></a>로컬 nupkg 파일에서 템플릿 제거

템플릿을 제거하려는 경우 *nupkg* 파일의 경로를 사용하지 마세요. *`dotnet new -u <PATH_TO_NUPKG_FILE>`을 사용하여 템플릿을 제거하는 시도가 실패합니다.* `id`를 통해 패키지를 참조합니다.

```console
dotnet new -u GarciaSoftware.ConsoleTemplate.CSharp.1.0.0
```

## <a name="use-file-system-distribution"></a>파일 시스템 배포 사용

템플릿을 배포하려면 프로젝트 템플릿 폴더를 네트워크에서 사용자가 액세스할 수 있는 위치에 배치합니다. `dotnet new` 명령을 `-i|--install` 옵션과 함께 사용하여 템플릿 폴더(프로젝트 및 *.template.config* 폴더가 포함된 프로젝트 폴더)의 경로를 지정합니다.

이 자습서에서는 프로젝트 템플릿이 사용자 프로필의 *Documents/Templates* 폴더에 저장된다고 가정합니다. 해당 위치에서 \<USER>를 사용자의 프로필 이름으로 바꾸는 다음 명령을 사용하여 템플릿을 설치합니다.

```console
dotnet new -i C:\Users\<USER>\Documents\Templates\GarciaSoftware.ConsoleTemplate.CSharp
```

### <a name="create-a-project-from-the-template"></a>템플릿에서 프로젝트 만들기

파일 시스템에서 템플릿이 설치된 후 템플릿 엔진의 출력을 배치할 디렉터리에서 `dotnet new <TEMPLATE>` 명령을 실행하여 템플릿을 사용합니다(`-o|--output` 옵션을 사용하여 특정 디렉터리를 지정하는 경우 제외). 자세한 내용은 [`dotnet new` 옵션](~/docs/core/tools/dotnet-new.md#options)을 참조하세요. 템플릿의 짧은 이름을 `dotnet new` 명령에 직접 제공합니다.

*C:\Users\\\<USER>\Documents\Projects\MyConsoleApp*에 만들어진 새 프로젝트 폴더에서 `garciaconsole` 템플릿을 기반으로 프로젝트를 만듭니다.

```console
dotnet new garciaconsole
```

### <a name="uninstall-the-template"></a>템플릿 제거

로컬 파일 시스템의 *C:\Users\\\<USER>\Documents\Templates\GarciaSoftware.ConsoleTemplate.CSharp*에서 템플릿을 만든 경우 `-u|--uninstall` 스위치와 템플릿 폴더 경로를 사용하여 템플릿을 제거합니다.

```console
dotnet new -u C:\Users\<USER>\Documents\Templates\GarciaSoftware.ConsoleTemplate.CSharp
```

> [!NOTE]
> 로컬 파일 시스템에서 템플릿을 제거하려면 경로를 정규화해야 합니다. 예를 들어 *C:\Users\\\<USER>\Documents\Templates\GarciaSoftware.ConsoleTemplate.CSharp* will work, but *./GarciaSoftware.ConsoleTemplate.CSharp*는 작동하지 않습니다.
> 마지막의 종료하는 디렉터리 슬래시도 템플릿 경로에 포함하지 마세요.

## <a name="see-also"></a>참고 항목

[dotnet/templating GitHub repo Wiki](https://github.com/dotnet/templating/wiki)(dotnet/templating GitHub 리포지토리 Wiki)  
[dotnet/dotnet-template-samples GitHub repo](https://github.com/dotnet/dotnet-template-samples)(dotnet/dotnet-template-samples GitHub 리포지토리)  
[How to create your own templates for dotnet new](https://blogs.msdn.microsoft.com/dotnet/2017/04/02/how-to-create-your-own-templates-for-dotnet-new/)(dotnet new에 대한 사용자 지정 템플릿을 만드는 방법)  
[*template.json* JSON 스키마 저장소에 대 한 스키마](http://json.schemastore.org/template)  
