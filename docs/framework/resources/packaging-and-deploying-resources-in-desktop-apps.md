---
title: 데스크톱 응용 프로그램의 리소스 패키징 및 배포
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-bcl
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- deploying applications [.NET Framework], resources
- resource files, deploying
- hub-and-spoke resource deployment model
- resource files, packaging
- application resources, packaging
- single resource assembly
- satellite assemblies
- default culture for applications
- names [.NET Framework], resources
- fallback process for resources
- grouping cultures
- application resources, deploying
- application resources, naming conventions
- culture, packaging and deploying resources
- resource files, naming conventions
- packaging application resources
- application resources, fallback processes
- resource files, fallback processes
- localizing resources
- neutral cultures
ms.assetid: b224d7c0-35f8-4e82-a705-dd76795e8d16
caps.latest.revision: ''
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 479ab530ddf02fa3701a7f6f3699258d0eab727e
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="packaging-and-deploying-resources-in-desktop-apps"></a>데스크톱 응용 프로그램의 리소스 패키징 및 배포
응용 프로그램은 <xref:System.Resources.ResourceManager> 클래스가 나타내는 .NET Framework 리소스 관리자를 사용하여 지역화된 리소스를 검색합니다. 리소스 관리자는 허브 및 스포크 모델이 리소스 패키지 및 배포에 사용된다고 가정합니다. 허브는 지역화할 수 없는 실행 코드와 중립 또는 기본 문화권이라고 하는 단일 문화권의 리소스를 포함하는 주 어셈블리입니다. 기본 문화권은 응용 프로그램의 대체 문화권으로, 지역화된 리소스를 찾을 수 없는 경우 해당 리소스가 사용되는 문화권입니다. 각 스포크는 단일 문화권의 리소스를 포함하지만 코드는 포함하지 않는 위성 어셈블리에 연결됩니다.  
  
 이 모델에는 다음과 같은 몇 가지 이점이 있습니다.  
  
-   응용 프로그램을 배포한 후 새로운 문화권에 대한 리소스를 증분 방식으로 추가할 수 있습니다. 문화권 관련 리소스의 후속 개발에 상당한 시간이 필요할 수 있기 때문에 주 응용 프로그램을 먼저 릴리스한 다음 나중에 문화권 관련 리소스를 제공할 수 있습니다.  
  
-   응용 프로그램을 다시 컴파일하지 않고 응용 프로그램의 위성 어셈블리를 업데이트하고 변경할 수 있습니다.  
  
-   응용 프로그램은 특정 문화권에 필요한 리소스를 포함하는 위성 어셈블리만 로드해야 합니다. 이렇게 하면 시스템 리소스의 사용을 훨씬 줄일 수 있습니다.  
  
 그러나 이 모델에는 다음과 같은 단점도 있습니다.  
  
-   여러 개의 리소스 집합을 관리해야 합니다.  
  
-   여러 구성을 테스트해야 하기 때문에 응용 프로그램을 테스트하는 초기 비용이 증가합니다. 장기적으로는 여러 개의 병렬 국제 버전을 테스트 및 유지 관리하는 것보다 여러 개의 위성 어셈블리가 있는 핵심 응용 프로그램 하나를 테스트하는 것이 더 쉽고 저렴합니다.  
  
## <a name="resource-naming-conventions"></a>리소스 명명 규칙  
 응용 프로그램의 리소스를 패키지할 때는 공용 언어 런타임에서 적용하는 리소스 명명 규칙을 사용하여 이름을 지정해야 합니다. 런타임에서는 문화권 이름으로 리소스를 식별합니다. 각 문화권에는 일반적으로 언어와 관련된 2자의 소문자 문화권 이름과 필요한 경우 국가 또는 지역과 관련된 2자의 대문자 하위 문화권 이름이 조합된 고유한 이름이 지정됩니다. 하위 문화권 이름이 문화권 이름 다음에 추가되고 대시(-)로 구분됩니다. 예를 들어 일본에서 사용되는 일본어는 ja-JP, 미국에서 사용되는 영어는 en-US, 독일에서 사용되는 독일어는 de-DE, 오스트리아에서 사용되는 독일어는 de-AT입니다. 문화권 이름의 전체 목록은 Go Global 개발자 센터에서 [NLS(국가별 언어 지원) API 참조](http://go.microsoft.com/fwlink/?LinkId=200048)를 참조하세요.  
  
> [!NOTE]
>  리소스 파일을 만드는 방법에 대한 자세한 내용은 [리소스 파일 만들기](../../../docs/framework/resources/creating-resource-files-for-desktop-apps.md) 및 [위성 어셈블리 만들기](../../../docs/framework/resources/creating-satellite-assemblies-for-desktop-apps.md)를 참조하세요.  
  
<a name="cpconpackagingdeployingresourcesanchor1"></a>   
## <a name="the-resource-fallback-process"></a>리소스 대체 프로세스  
 리소스를 패키지 및 배포하는 분산형 모델에서는 대체 프로세스를 통해 적절한 리소스를 찾습니다. 응용 프로그램이 사용할 수 없는 지역화된 리소스를 요청할 경우 공용 언어 런타임은 문화권 계층 구조에서 사용자의 응용 프로그램 요청과 가장 일치하는 적절한 대체 리소스를 검색하며, 어떠한 리소스도 찾을 수 없을 때만 예외를 throw합니다. 계층 구조의 각 수준에서 적절한 리소스가 발견되면 런타임에서 해당 리소스를 사용합니다. 리소스가 발견되지 않으면 검색이 다음 수준으로 진행됩니다.  
  
 조회 성능을 향상하려면 주 어셈블리에 <xref:System.Resources.NeutralResourcesLanguageAttribute> 특성을 적용하고 주 어셈블리에서 작동하는 중립 언어의 이름을 전달합니다.  
  
> [!TIP]
>  [ \<relativeBindForResources>](../../../docs/framework/configure-apps/file-schema/runtime/relativebindforresources-element.md) 구성 요소를 사용하여 런타임이 리소스 어셈블리를 검색하는 프로세스 및 리소스 대체 프로세스를 최적화할 수도 있습니다. 자세한 내용은 [리소스 대체 프로세스 최적화](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md#Optimizing) 섹션을 참조하세요.  
  
 리소스 대체 프로세스에는 다음 단계가 포함됩니다.  
  
1.  런타임은 먼저 [전역 어셈블리 캐시](../../../docs/framework/app-domains/gac.md)에서 응용 프로그램에 대해 요청된 문화권과 일치하는 어셈블리를 확인합니다.  
  
     전역 어셈블리 캐시는 많은 응용 프로그램이 공유하는 리소스 어셈블리를 저장할 수 있습니다. 이렇게 하면 만드는 모든 응용 프로그램의 디렉터리 구조에 특정 리소스 집합을 포함할 필요가 없습니다. 런타임은 어셈블리에 대한 참조를 발견할 경우 어셈블리에서 요청된 리소스를 검색합니다. 어셈블리에서 항목을 찾으면 요청된 리소스가 사용됩니다. 항목을 찾지 못하면 검색을 계속합니다.  
  
2.  그다음 런타임은 현재 실행 중인 어셈블리의 디렉터리에서 요청된 문화권과 일치하는 디렉터리를 확인합니다. 디렉터리를 찾으면 해당 디렉터리에서 요청된 문화권에 유효한 위성 어셈블리를 검색합니다. 그다음 런타임은 위성 어셈블리에서 요청된 리소스를 검색합니다. 어셈블리에서 리소스를 찾으면 해당 리소스가 사용됩니다. 리소스를 찾지 못하면 검색을 계속합니다.  
  
3.  그다음 런타임은 Windows Installer를 쿼리하여 요청 시 위성 어셈블리를 설치할지 여부를 확인합니다. 설치할 경우 설치를 처리하고, 어셈블리를 로드한 다음 어셈블리나 요청된 리소스를 검색합니다. 어셈블리에서 리소스를 찾으면 해당 리소스가 사용됩니다. 리소스를 찾지 못하면 검색을 계속합니다.  
  
4.  런타임은 <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 이벤트를 발생시켜 위성 어셈블리를 찾을 수 없음을 나타냅니다. 이벤트를 처리하도록 선택한 경우 이벤트 처리기에서 조회에 해당 리소스가 사용되는 위성 어셈블리에 대한 참조를 반환할 수 있습니다. 이벤트를 처리하지 않는 경우 이벤트 처리기에서 `null`을 반환하고 검색이 계속됩니다.  
  
5.  그다음 런타임은 전역 어셈블리 캐시에서 이번에는 요청된 문화권의 부모 어셈블리를 검색합니다. 부모 어셈블리가 전역 어셈블리 캐시에 있을 경우 런타임은 어셈블리에서 요청된 리소스를 검색합니다.  
  
     부모 문화권은 적절한 대체 문화권으로 정의됩니다. 리소스를 제공하는 것이 예외를 throw하는 것보다 낫기 때문에 부모를 대체 후보로 고려합니다. 이 프로세스를 통해 리소스를 다시 사용할 수도 있습니다. 자식 문화권이 요청된 리소스를 지역화할 필요가 없는 경우에만 부모 수준에 특정 리소스를 포함해야 합니다. 예를 들어 en(중립 영어), en-GB(영국에서 사용되는 영어) 및 en-US(미국에서 사용되는 영어)에 대한 위성 어셈블리를 제공하는 경우 en 위성에 일반적인 용어가 포함되고, en-GB 및 en-US 위성은 차이가 있는 용어에 대한 재정의만 제공할 수 있습니다.  
  
6.  그다음 런타임은 현재 실행 중인 어셈블리의 디렉터리를 검사하여 부모 디렉터리가 포함되어 있는지 확인합니다. 부모 디렉터리가 있을 경우 런타임은 디렉터리에서 부모 문화권에 대한 유효한 위성 어셈블리를 검색합니다. 런타임은 어셈블리를 발견할 경우 어셈블리에서 요청된 리소스를 검색합니다. 리소스를 찾으면 해당 리소스가 사용됩니다. 리소스를 찾지 못하면 검색을 계속합니다.  
  
7.  그다음 런타임은 Windows Installer를 쿼리하여 요청 시 부모 위성 어셈블리를 설치할지 여부를 확인합니다. 설치할 경우 설치를 처리하고, 어셈블리를 로드한 다음 어셈블리나 요청된 리소스를 검색합니다. 어셈블리에서 리소스를 찾으면 해당 리소스가 사용됩니다. 리소스를 찾지 못하면 검색을 계속합니다.  
  
8.  런타임은 <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 이벤트를 발생시켜 적절한 대체 리소스를 찾을 수 없음을 나타냅니다. 이벤트를 처리하도록 선택한 경우 이벤트 처리기에서 조회에 해당 리소스가 사용되는 위성 어셈블리에 대한 참조를 반환할 수 있습니다. 이벤트를 처리하지 않는 경우 이벤트 처리기에서 `null`을 반환하고 검색이 계속됩니다.  
  
9. 그다음 런타임은 앞의 세 단계와 마찬가지로 가능한 여러 수준에서 부모 어셈블리를 검색합니다. 각 문화권에는 <xref:System.Globalization.CultureInfo.Parent%2A?displayProperty=nameWithType> 속성으로 정의된 부모 하나만 있지만 부모가 해당 부모를 포함할 수도 있습니다. 문화권의 <xref:System.Globalization.CultureInfo.Parent%2A> 속성이 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType>을 반환하면 부모 문화권 검색이 중지됩니다. 리소스 대체에서 고정 문화권은 부모 문화권 또는 리소스를 가질 수 있는 문화권으로 간주되지 않습니다.  
  
10. 원래 지정된 문화권 및 모든 부모를 검색했지만 리소스를 찾지 못하면 기본(대체) 문화권의 리소스가 사용됩니다. 일반적으로 기본 문화권의 리소스는 주 응용 프로그램 어셈블리에 포함되어 있습니다. 그러나 <xref:System.Resources.NeutralResourcesLanguageAttribute> 특성의 <xref:System.Resources.NeutralResourcesLanguageAttribute.Location%2A> 속성에 대해 <xref:System.Resources.UltimateResourceFallbackLocation.Satellite> 값을 지정하여 리소스의 최종 대체 위치가 주 어셈블리가 아니라 위성 어셈블리임을 나타낼 수 있습니다.  
  
    > [!NOTE]
    >  기본 리소스는 주 어셈블리와 함께 컴파일할 수 있는 유일한 리소스입니다. <xref:System.Resources.NeutralResourcesLanguageAttribute> 특성을 사용하여 위성 어셈블리를 지정하지 않을 경우 이 리소스가 최종 대체(최종 부모)입니다. 따라서 주 어셈블리에 기본 리소스 집합을 항상 포함하는 것이 좋습니다. 이렇게 하면 예외가 throw되지 않도록 방지하는 데 도움이 됩니다. 기본 리소스 파일을 포함하여 모든 리소스에 대한 대체를 제공하고 문화권별 리소스는 아니라도 사용자에게 항상 리소스가 하나 이상 제공되도록 합니다.  
  
11. 마지막으로, 런타임이 기본(대체) 문화권의 리소스를 찾지 못하면 <xref:System.Resources.MissingManifestResourceException> 또는 <xref:System.Resources.MissingSatelliteAssemblyException> 예외가 throw되어 리소스를 찾을 수 없음을 나타냅니다.  
  
 예를 들어 응용 프로그램이 스페인어(멕시코)(es-MX 문화권)에 대해 지역화된 리소스를 요청한다고 가정해 보세요. 런타임은 먼저 전역 어셈블리 캐시에서 es-MX와 일치하는 어셈블리를 검색하지만 찾지 못합니다. 그다음 런타임은 현재 실행 중인 어셈블리의 디렉터리에서 es-MX 디렉터리를 검색합니다. 이 시도에 실패하여 런타임은 다시 전역 어셈블리 캐시에서 적절한 대체 문화권을 반영하는 부모 어셈블리(이 경우 es(스페인어))를 검색합니다. 부모 어셈블리를 찾지 못하면 런타임은 해당 리소스를 찾을 때까지 부모 어셈블리의 모든 가능한 수준에서 es-MX 문화권을 검색합니다. 리소스를 찾지 못하면 런타임은 기본 문화권의 리소스를 사용합니다.  
  
<a name="Optimizing"></a>   
### <a name="optimizing-the-resource-fallback-process"></a>리소스 대체 프로세스 최적화  
 다음과 같은 경우 런타임이 위성 어셈블리에서 리소스를 검색하는 프로세스를 최적화할 수 있습니다.  
  
-   위성 어셈블리는 코드 어셈블리와 동일한 위치에 배포됩니다. 코드 어셈블리가 [전역 어셈블리 캐시](../../../docs/framework/app-domains/gac.md)에 설치된 경우 위성 어셈블리도 전역 어셈블리 캐시에 설치됩니다. 코드 어셈블리가 디렉터리에 설치된 경우 위성 어셈블리는 해당 디렉터리의 문화권별 폴더에 설치됩니다.  
  
-   위성 어셈블리는 요청 시 설치되지 않습니다.  
  
-   응용 프로그램 코드는 <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 이벤트를 처리하지 않습니다.  
  
 다음 예제와 같이 응용 프로그램 구성 파일에 [\<relativeBindForResources>](../../../docs/framework/configure-apps/file-schema/runtime/relativebindforresources-element.md) 요소를 포함하고 해당 `enabled` 특성을 `true`로 설정하여 위성 어셈블리에 대한 프로브를 최적화합니다.  
  
```xml  
<configuration>  
   <runtime>  
      <relativeBindForResources enabled="true" />  
   </runtime>  
</configuration>  
```  
  
 위성 어셈블리에 대해 최적화된 프로브는 옵트인 기능입니다. 즉, 런타임은 [\<relativeBindForResources>](../../../docs/framework/configure-apps/file-schema/runtime/relativebindforresources-element.md) 요소가 응용 프로그램의 구성 파일에 있고 해당 `enabled` 특성이 `true`로 설정된 경우가 아니면 [리소스 대체 프로세스](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md#cpconpackagingdeployingresourcesanchor1)에 문서화된 단계를 따릅니다. 이런 경우에는 위성 어셈블리 검색 프로세스가 다음과 같이 수정됩니다.  
  
-   런타임은 부모 코드 어셈블리의 위치를 사용하여 위성 어셈블리를 검색합니다. 부모 어셈블리가 전역 어셈블리 캐시에 설치된 경우 런타임은 캐시에서만 검색하고 응용 프로그램 디렉터리에서 검색하지 않습니다. 부모 어셈블리가 응용 프로그램 디렉터리에 설치된 경우 런타임은 응용 프로그램 디렉터리에서만 검색하고 전역 어셈블리 캐시에서 검색하지 않습니다.  
  
-   런타임은 위성 어셈블리의 요청 시 설치에 대해 Windows Installer를 쿼리하지 않습니다.  
  
-   특정 리소스 어셈블리 검색이 실패할 경우 런타임에서 <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 이벤트가 발생하지 않습니다.  
  
### <a name="ultimate-fallback-to-satellite-assembly"></a>위성 어셈블리에 대한 최종 대체  
 필요에 따라 주 어셈블리에서 리소스를 제거하고 런타임이 특정 문화권에 해당하는 위성 어셈블리에서 최종 대체 리소스를 로드하도록 지정할 수 있습니다. 대체 프로세스를 제어하려면 <xref:System.Resources.NeutralResourcesLanguageAttribute.%23ctor%28System.String%2CSystem.Resources.UltimateResourceFallbackLocation%29?displayProperty=nameWithType> 생성자를 사용하고 리소스 관리자가 주 어셈블리 또는 위성 어셈블리에서 대체 리소스를 추출해야 하는지를 지정하는 <xref:System.Resources.UltimateResourceFallbackLocation> 매개 변수의 값을 제공합니다.  
  
 다음 예제에서는 <xref:System.Resources.NeutralResourcesLanguageAttribute> 특성을 사용하여 프랑스어(fr) 언어에 대한 위성 어셈블리에 응용 프로그램의 대체 리소스를 저장합니다.  이 예제에는 `Greeting`이라는 단일 문자열 리소스를 정의하는 두 개의 텍스트 기반 리소스 파일이 있습니다. 첫 번째 resources.fr.txt에는 프랑스어 리소스가 들어 있습니다.  
  
```  
Greeting=Bon jour!  
```  
  
 두 번째 resources,ru.txt에는 러시아어 리소스가 들어 있습니다.  
  
```  
Greeting=Добрый день  
```  
  
 명령줄에서 [리소스 파일 생성기(Resgen.exe)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md)를 실행하여 이러한 두 파일을 .resources 파일로 컴파일합니다.  프랑스어 리소스에 대한 명령은 다음과 같습니다.  
  
 **resgen.exe resources.fr.txt**  
  
 러시아어 리소스에 대한 명령은 다음과 같습니다.  
  
 **resgen.exe resources.ru.txt**  
  
 프랑스어 리소스에 대한 명령줄에서 다음과 같이 [어셈블리 링커(Al.exe)](../../../docs/framework/tools/al-exe-assembly-linker.md) 명령을 실행하여 .resources 파일을 동적 연결 라이브러리에 포함합니다.  
  
 **al /t:lib /embed:resources.fr.resources /culture:fr /out:fr\Example1.resources.dll**  
  
 러시아어 리소스의 경우 다음과 같이 명령을 실행합니다.  
  
 **al /t:lib /embed:resources.ru.resources /culture:ru /out:ru\Example1.resources.dll**  
  
 응용 프로그램 소스 코드는 Example1.cs 또는 Example1.vb라는 파일에 있습니다. <xref:System.Resources.NeutralResourcesLanguageAttribute> 특성을 포함하여 기본 응용 프로그램 리소스가 fr 하위 디렉터리에 있음을 나타냅니다. 리소스 관리자를 인스턴스화하고, `Greeting` 리소스의 값을 검색하여 콘솔에 표시합니다.  
  
 [!code-csharp[Conceptual.Resources.Packaging#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.packaging/cs/example1.cs#1)]
 [!code-vb[Conceptual.Resources.Packaging#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.packaging/vb/example1.vb#1)]  
  
 명령줄에서 다음과 같이 C# 소스 코드를 컴파일할 수 있습니다.  
  
```console 
csc Example1.cs
```
  
 Visual Basic 컴파일러에 대한 명령도 다음과 같이 매우 유사합니다.  
  
```console
vbc Example1.vb
```  
  
 주 어셈블리에 포함된 리소스가 없기 때문에 `/resource` 스위치를 사용하여 컴파일할 필요가 없습니다.  
  
 러시아어 이외의 언어를 사용하는 시스템에서 예제를 실행할 경우 다음과 같은 출력이 표시됩니다.  
  
```  
Bon jour!  
```  
  
## <a name="suggested-packaging-alternative"></a>패키징 대체 방법 제안  
 시간 또는 예산 제약 조건으로 인해 응용 프로그램이 지원하는 모든 하위 문화권의 리소스 집합을 만들지 못할 수도 있습니다. 대신, 부모 문화권에 대해 관련된 모든 하위 문화권이 사용할 수 있는 단일 위성 어셈블리를 만들 수 있습니다. 예를 들어 지역별 영어 리소스를 요청하는 사용자가 검색하는 단일 영어 위성 어셈블리(en) 및 지역별 독일어 리소스를 요청하는 사용자를 위한 단일 독일어 위성 어셈블리(de)를 제공할 수 있습니다. 예를 들어 독일에서 사용되는 독일어(de-DE), 오스트리아에서 사용되는 독일어(de-AT), 스위스에서 사용되는 독일어(de-CH) 요청은 독일어 위성 어셈블리(de)로 대체됩니다. 기본 리소스는 최종 대체라서 대부분의 응용 프로그램 사용자가 요청하는 리소스여야 하므로 이러한 리소스를 선택할 때는 주의하세요. 이 접근 방법은 문화권별 성격이 약한 리소스를 배포하지만 응용 프로그램의 지역화 비용을 훨씬 줄일 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [데스크톱 앱의 리소스](../../../docs/framework/resources/index.md)  
 [전역 어셈블리 캐시](../../../docs/framework/app-domains/gac.md)  
 [리소스 파일 만들기](../../../docs/framework/resources/creating-resource-files-for-desktop-apps.md)  
 [위성 어셈블리 만들기](../../../docs/framework/resources/creating-satellite-assemblies-for-desktop-apps.md)
