---
title: .NET 네이티브 시작
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fc9e04e8-2d05-4870-8cd6-5bd276814afc
caps.latest.revision: ''
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 56ff06c17eda8483c7d067af9fb39a402d2f6ea5
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="getting-started-with-net-native"></a>.NET 네이티브 시작
새로운 Windows 10용 Windows 앱을 작성하든지 기존 Windows 스토어 앱을 마이그레이션하든지 상관없이 동일한 절차 집합을 따르면 됩니다. [!INCLUDE[net_native](../../../includes/net-native-md.md)] 앱을 만들려면 다음 단계를 수행합니다.  
  
1.  [Windows 10을 대상으로 하는 UWP(유니버설 Windows 플랫폼) 앱을 개발하고](#Step1)앱의 디버그 빌드를 테스트하여 제대로 작동하는지 확인합니다.  
  
2.  [추가 리플렉션 및 serialization 사용을 처리합니다](#Step2).  
  
3.  [앱의 릴리스 빌드를 배포하고 테스트합니다](#Step3).  
  
4.  [누락된 메타데이터 문제를 수동으로 해결](#Step4)하고 [3단계](#Step3)를 반복하여 모든 문제를 해결합니다.  
  
> [!NOTE]
>  기존 Windows 스토어 앱을 [!INCLUDE[net_native](../../../includes/net-native-md.md)]로 마이그레이션하는 경우 [Windows 스토어 앱을 .NET 네이티브로 마이그레이션](../../../docs/framework/net-native/migrating-your-windows-store-app-to-net-native.md).  
  
<a name="Step1"></a>   
## <a name="step-1-develop-and-test-debug-builds-of-your-uwp-app"></a>1단계: UWP 앱의 디버그 빌드 개발 및 테스트  
 새 앱을 개발하든지 기존 앱을 마이그레이션하든지 상관없이 모든 Windows 앱에 동일한 프로세스를 따릅니다.  
  
1.  Visual C# 또는 Visual Basic용 유니버설 Windows 앱 템플릿을 사용하여 Visual Studio에서 새 UWP 프로젝트를 만듭니다. 기본적으로 모든 UWP 응용 프로그램은 CoreCLR을 대상으로 하며 해당 릴리스 빌드는 .NET 네이티브 도구 체인을 사용하여 컴파일됩니다.  
  
2.  .NET 네이티브 도구 체인을 사용하는 UWP 앱 프로젝트 컴파일과 도구 체인이 없는 프로젝트 컴파일 간에 알려진 호환성 문제가 몇 가지 있습니다. 자세한 내용은 [마이그레이션 가이드](../../../docs/framework/net-native/migrating-your-windows-store-app-to-net-native.md) 를 참조하세요.  
  
 이제는 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 노출 영역에 대해 로컬 시스템이나 시뮬레이터에서 실행되는 C# 또는 Visual Basic 코드를 작성할 수 있습니다.  
  
> [!IMPORTANT]
>  앱을 개발할 때는 코드에서 serialization 또는 리플렉션 사용을 파악합니다.  
  
 기본적으로 디버그 빌드는 신속한 F5 배포를 사용할 수 있도록 JIT 컴파일되지만, 릴리스 빌드는 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 미리 컴파일 기술을 사용하여 컴파일됩니다. 이는 .NET 네이티브 도구 체인을 사용하여 프로젝트를 컴파일하기 전에 앱의 디버그 빌드를 빌드하고 테스트하여 정상적으로 작동되는지 확인해야 한다는 의미입니다.  
  
<a name="Step2"></a>   
## <a name="step-2-handle-additional-reflection-and-serialization-usage"></a>2단계: 추가 리플렉션 및 serialization 사용 처리  
 프로젝트를 만들 때 런타임 지시문 파일인 Default.rd.xml이 해당 프로젝트에 자동으로 추가됩니다. C#으로 개발하는 경우 프로젝트의 **Properties** 폴더에 있습니다. Visual Basic으로 개발하는 경우 프로젝트의 **My Project** 폴더에 있습니다.  
  
> [!NOTE]
>  런타임 지시문 파일이 필요한 이유에 대한 배경 정보를 제공하는 .NET 네이티브 컴파일 프로세스의 개요는 [.NET 네이티브 및 컴파일](../../../docs/framework/net-native/net-native-and-compilation.md)을 참조하세요.  
  
 런타임 지시문 파일은 앱에서 런타임에 필요한 메타데이터를 정의하는 데 사용됩니다. 일부 경우에는 파일의 기본 버전이 적절할 수도 있습니다. 그러나 serialization 또는 리플렉션을 사용하는 일부 코드는 런타임 지시문 파일에서 추가 항목을 필요로 할 수 있습니다.  
  
 **serialization**  
 직렬 변환기에는 두 가지 범주가 있으며 두 범주 모두 런타임 지시문 파일에 추가 항목이 필요합니다.  
  
-   리플렉션을 기반으로 하지 않는 serializer. <xref:System.Runtime.Serialization.DataContractSerializer>, <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>, <xref:System.Xml.Serialization.XmlSerializer> 클래스와 같이 .NET Framework 클래스 라이브러리에 포함된 serializer는 리플렉션을 사용하지 않습니다. 그러나 serialize 또는 deserialize할 개체에 따라 코드를 생성해야 합니다.  자세한 내용은 [Serialization and Metadata](../../../docs/framework/net-native/serialization-and-metadata.md)의 "Microsoft 직렬 변환기" 섹션을 참조하세요.  
  
-   타사 직렬 변환기. 타사 serialization 라이브러리(가장 일반적인 라이브러리는 Newtonsoft JSON serializer)는 대개 리플렉션을 기반으로 하며, *.rd.xml 파일에 개체 serialization 및 deserialization을 지원하기 위한 항목이 필요합니다. 자세한 내용은 [Serialization and Metadata](../../../docs/framework/net-native/serialization-and-metadata.md)의 "타사 직렬 변환기" 섹션을 참조하세요.  
  
 **리플렉션을 사용하는 메서드**  
 코드에서 리플렉션이 사용되는지가 분명하지 않은 경우가 있습니다. 일부 공통 API 또는 프로그래밍 패턴은 리플렉션 API의 일부로는 간주되지 않지만 리플렉션을 사용해야 올바르게 실행됩니다. 여기에는 다음과 같은 형식 인스턴스화 및 메서드 생성 메서드가 포함됩니다.  
  
-   <xref:System.Type.MakeGenericType%2A?displayProperty=nameWithType> 메서드  
  
-   <xref:System.Array.CreateInstance%2A?displayProperty=nameWithType> 및 <xref:System.Type.MakeArrayType%2A?displayProperty=nameWithType> 메서드  
  
-   <xref:System.Reflection.MethodInfo.MakeGenericMethod%2A?displayProperty=nameWithType> 메서드  
  
 자세한 내용은 [APIs That Rely on Reflection](../../../docs/framework/net-native/apis-that-rely-on-reflection.md)을 참조하세요.  
  
> [!NOTE]
>  런타임 지시문 파일에 사용되는 형식 이름은 정규화된 이름이어야 합니다. 예를 들어 파일이 "String"이 아닌 "System.String"을 지정해야 합니다.  
  
<a name="Step3"></a>   
## <a name="step-3-deploy-and-test-the-release-builds-of-your-app"></a>3단계: 앱의 릴리스 빌드 배포 및 테스트  
 런타임 지시문 파일을 업데이트한 후에는 앱의 릴리스 빌드를 다시 빌드하고 배포할 수 있습니다. .NET 네이티브 이진 파일은 프로젝트 **속성** 대화 상자 **컴파일** 탭의 **빌드 출력 경로** 텍스트 상자에 지정된 디렉터리의 ILC.out 하위 디렉터리에 저장됩니다. 이 폴더에 없는 이진 파일은 .NET 네이티브로 컴파일되지 않은 것입니다. 각각의 대상 플랫폼에서 앱을 철저하게 테스트하고 오류 시나리오를 비롯한 모든 시나리오를 테스트합니다.  
  
 앱이 정상적으로 작동하지 않는 경우(특히 런타임에 [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md) 또는 [MissingInteropDataException](../../../docs/framework/net-native/missinginteropdataexception-class-net-native.md) 예외가 throw되는 경우) 다음 섹션인 [4단계: 수동으로 누락된 메타데이터 문제 해결](#Step4)의 지침을 따릅니다. 첫째 예외를 사용하도록 설정하면 이러한 버그를 찾는 데 도움이 될 수 있습니다.  
  
 앱의 디버그 빌드를 테스트 및 디버그했으며 [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md) 및 [MissingInteropDataException](../../../docs/framework/net-native/missinginteropdataexception-class-net-native.md) 예외가 제거되었음을 확인했으면 앱을 최적화된 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 앱으로 테스트해야 합니다. 이렇게 하려면 활성 프로젝트 구성을 **디버그** 에서 **릴리스**로 변경합니다.  
  
<a name="Step4"></a>   
## <a name="step-4-manually-resolve-missing-metadata"></a>4단계: 수동으로 누락된 메타데이터 문제 해결  
 데스크톱에서는 발생하지 않지만 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 에서는 발생하는 가장 흔한 오류는 런타임 [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md), [MissingInteropDataException](../../../docs/framework/net-native/missinginteropdataexception-class-net-native.md)또는 [MissingRuntimeArtifactException](../../../docs/framework/net-native/missingruntimeartifactexception-class-net-native.md) 예외입니다. 경우에 따라서는 메타데이터가 없어서 예측할 수 없는 동작이 발생하거나 앱 자체에도 오류가 발생할 수 있습니다. 이 섹션에서는 런타임 지시문 파일에 지시문을 추가하여 이러한 예외를 디버그 및 해결하는 방법을 설명합니다. 런타임 지시문 형식에 대한 자세한 내용은 [런타임 지시문(rd.xml) 구성 파일 참조](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)를 참조하세요. 런타임 지시문을 추가한 후에는 다시 [앱을 배포 및 테스트](#Step3)하고 예외가 더 이상 발생하지 않을 때까지 새로 발생하는 [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md), [MissingInteropDataException](../../../docs/framework/net-native/missinginteropdataexception-class-net-native.md) 및 [MissingRuntimeArtifactException](../../../docs/framework/net-native/missingruntimeartifactexception-class-net-native.md) 예외를 해결해야 합니다.  
  
> [!TIP]
>  코드 변경 시 앱을 복원하려면 런타임 지시문을 대략적으로 지정합니다.  런타임 지시문은 멤버 수준이 아닌 네임스페이스 및 형식 수준에 추가하는 것이 좋습니다. 복원력을 높이면 이진 파일이 커지고 컴파일 시간이 길어질 수 있습니다.  
  
 누락된 메타데이터 예외를 해결할 때는 다음 문제를 고려해야 합니다.  
  
-   예외가 발생하기 전에 앱이 수행하려 했던 작업  
  
    -   예를 들어 데이터 바인딩, 데이터 serialize/deserialize, 리플렉션 API 직접 사용 등을 시도했을 수 있습니다.  
  
-   이 사례가 해당 형식에만 국한된 것인지 아니면 다른 형식에서도 같은 문제가 발생할 것으로 예상되는지 여부  
  
    -   앱 개체 모델에서 형식을 serialize할 때 [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md) 예외가 throw된 경우를 예로 들어 보겠습니다.  이때 serialize할 다른 형식을 알고 있으면 해당 형식 또는 코드 구성 효율성에 따라 해당 형식의 포함 네임스페이스에 대해 런타임 지시문을 동시에 추가할 수 있습니다.  
  
-   리플렉션을 사용하지 않도록 코드를 다시 작성할 수 있는지 여부  
  
    -   필요한 형식을 알고 있는 경우 코드에 `dynamic` 키워드가 사용되는지 여부  
  
    -   보다 효율적인 대안을 사용할 수 있는 경우 코드가 리플렉션을 사용하는 메서드를 호출하는지 여부  
  
> [!NOTE]
>  리플렉션의 차이로 인해 발생하는 문제를 처리하는 방법과, 데스크톱 앱 및 [!INCLUDE[net_native](../../../includes/net-native-md.md)]에서 메타데이터 사용 가능 여부에 대한 자세한 내용은 [APIs That Rely on Reflection](../../../docs/framework/net-native/apis-that-rely-on-reflection.md).  
  
 앱을 테스트할 때 발생하는 예외 및 기타 문제를 처리하는 몇 가지 구체적인 예제는 다음 항목을 참조하세요.  
  
-   [예: 데이터를 바인딩하는 경우 예외 처리](../../../docs/framework/net-native/example-handling-exceptions-when-binding-data.md)  
  
-   [예: 동적 프로그래밍 문제 해결](../../../docs/framework/net-native/example-troubleshooting-dynamic-programming.md)  
  
-   [.NET 네이티브 앱의 런타임 예외](../../../docs/framework/net-native/runtime-exceptions-in-net-native-apps.md)  
  
## <a name="see-also"></a>참고 항목  
 [런타임 지시문(rd.xml) 구성 파일 참조](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)  
 [NIB:.NET 네이티브 설치 및 구성](http://msdn.microsoft.com/library/7c9bc375-8b87-4c33-bede-72d513e362ec)  
 [.NET 네이티브 및 컴파일](../../../docs/framework/net-native/net-native-and-compilation.md)  
 [리플렉션 및 .NET 네이티브](../../../docs/framework/net-native/reflection-and-net-native.md)  
 [리플렉션을 사용하는 API](../../../docs/framework/net-native/apis-that-rely-on-reflection.md)  
 [Serialization 및 메타데이터](../../../docs/framework/net-native/serialization-and-metadata.md)  
 [Windows 스토어 앱을 .NET 네이티브로 마이그레이션](../../../docs/framework/net-native/migrating-your-windows-store-app-to-net-native.md)
