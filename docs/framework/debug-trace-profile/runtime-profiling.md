---
title: 런타임 프로파일링
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- performance counters
- common language runtime, profiling
- Perfmon.exe
- System Monitor
- profiling
- runtime, profiling
- profiling applications
- Performance Console
ms.assetid: ccd68284-f3a8-47b8-bc3f-92e5fe3a1640
caps.latest.revision: ''
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 4a8f3af4878e0f6911fcc55ec76b26649d517b3b
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/22/2017
---
# <a name="runtime-profiling"></a>런타임 프로파일링
프로파일링은 모든 개발 또는 배포 시나리오에서 성능 데이터를 수집하는 방법입니다. 이 섹션은 응용 프로그램 성능에 대한 정보를 수집하려는 개발자 및 시스템 관리자를 위한 것입니다.  
  
## <a name="tracking-performance-using-the-performance-monitor-perfmonexe"></a>성능 모니터(Perfmon.exe)를 사용하여 성능 추적  
 성능 모니터는 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 응용 프로그램 프로파일링에 사용하는 가장 쉬운 도구입니다. 성능 모니터는 공용 언어 런타임과 [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)]이 함께 설치된 .NET Framework 성능 카운터의 데이터를 그래픽으로 표시합니다. 이러한 카운터를 사용하여 메모리 관리에서 JIT(just-in-time) 컴파일러 성능에 이르기까지 모든 것을 모니터링할 수 있습니다. 이렇게 하여 응용 프로그램이 사용하는 리소스에 대해 알 수 있으며 이는 응용 프로그램의 성능에 대한 간접적인 측정입니다. 이러한 카운터를 사용하여 응용 프로그램이 내부적으로 작동하는 방식을 이해할 수 있습니다.  
  
#### <a name="to-run-perfmonexe-on-windows-vista-and-later-versions"></a>Windows Vista 이상 버전에서 Perfmon.exe를 실행하려면  
  
1.  명령 프롬프트에서 **perfmon**를 입력합니다. **성능 모니터** 콘솔이 나타납니다.  
  
2.  **모니터링 도구** 폴더에서 **성능 모니터**를 클릭합니다.  
  
3.  성능 모니터 도구 모음에서 **추가** 아이콘(더하기 기호)이 있는 경우 클릭합니다. 아이콘이 없는 경우 모니터 창을 마우스 오른쪽 단추로 클릭하고 **카운터 추가** 옵션을 선택합니다.  
  
     그러면 **카운터 추가** 대화 상자가 열립니다. **사용 가능한 카운터** 목록 상자에 사용 가능한 성능 개체가 표시됩니다. 메모리 관리(**.NET CLR 메모리**), 상호 운용성(**.NET CLR Interop**), 예외 처리(**.NET CLR 예외**) 및 다중 스레딩(**.NET CLR LocksAndThreads**)에 대한 개체를 비롯한 .NET Framework 응용 프로그램에 대해 다수의 미리 정의된 개체가 있습니다. 각 성능 개체에는 많은 개별 성능 카운터가 포함됩니다. 성능 모니터에서 사용할 수 있는 성능 카운터 목록은 [Performance Counters](../../../docs/framework/debug-trace-profile/performance-counters.md)이 함께 설치된 .NET Framework 성능 카운터의 데이터를 그래픽으로 표시합니다.  
  
4.  지원되는 개별 성능 카운터의 목록을 보려면 성능 개체의 이름 옆에 있는 확인란을 선택합니다.  
  
5.  보려는 성능 카운터를 클릭합니다.  
  
6.  **선택한 개체의 인스턴스** 목록 상자에서 **\<All instances>**를 클릭하여 공용 언어 런타임에 대한 성능 카운터를 전역적으로(시스템 전체에서) 모니터링하도록 지정합니다.  
  
     또는  
  
     **선택한 개체의 인스턴스** 목록 상자에서 응용 프로그램 이름을 클릭하여 해당 응용 프로그램에 대한 성능 카운터를 모니터링합니다.  
  
     여러 버전의 런타임을 구분하거나 이름이 같은 여러 응용 프로그램의 차이를 분명히 보여 주려면 레지스트리 키도 수정해야 합니다. 자세한 내용은 [성능 카운터 및 In-Process Side-By-Side 응용 프로그램](../../../docs/framework/debug-trace-profile/performance-counters-and-in-process-side-by-side-applications.md)을 참조하세요.  
  
> [!NOTE]
>  성능 콘솔이 실행되는 동안 새로운 성능 카운터가 설치되면 새로운 카운터를 표시하기 위해 성능 콘솔을 중지하고 다시 시작합니다.  
  
 특정 영역이나 원격 공유에 있는 어셈블리를 프로파일링하려면 성능 카운터를 실행하는 컴퓨터에서 원격 어셈블리를 완전히 신뢰해야 합니다. 어셈블리를 충분히 신뢰하지 않는 경우 성능 카운터가 작동하지 않습니다. 여러 다른 영역에 신뢰를 부여하는 데 관한 내용은 [Caspol.exe(코드 액세스 보안 정책 도구)](../../../docs/framework/tools/caspol-exe-code-access-security-policy-tool.md)를 참조하세요.  
  
> [!NOTE]
>  [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 가 설치된 시스템에서 성능 모니터는 **를 사용하여 개발된 응용 프로그램의 일부 범주(예:** .NET CLR 데이터 **및**.NET CLR 네트워킹 [!INCLUDE[net_v11_short](../../../includes/net-v11-short-md.md)])에서 성능 카운터에 대한 데이터를 표시하지 않을 수 있습니다. 이 경우, [\<forcePerformanceCounterUniqueSharedMemoryReads>](../../../docs/framework/configure-apps/file-schema/runtime/forceperformancecounteruniquesharedmemoryreads-element.md) 요소를 응용 프로그램의 구성 파일에 추가하여 성능 모니터가 이 데이터를 표시하도록 구성할 수 있습니다.  
  
## <a name="reading-and-creating-performance-counters-programmatically"></a>프로그래밍 방식으로 성능 카운터 읽기 및 만들기  
 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 은 성능 콘솔에서 사용할 수 있는 동일한 성능 정보를 프로그래밍 방식으로 액세스하기 위해 사용할 수 있는 클래스를 제공합니다. 또한 이러한 클래스를 사용하여 사용자 지정 성능 카운터를 만들 수도 있습니다. 다음 표에서는 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]에서 제공하는 일부 성능 모니터링 클래스에 대해 설명합니다.  
  
|클래스|설명|  
|-----------|-----------------|  
|<xref:System.Diagnostics.PerformanceCounter?displayProperty=nameWithType>|Windows NT 성능 카운터 구성 요소를 나타냅니다. 이 클래스를 사용하여 기존의 미리 정의된 카운터 또는 사용자 지정 카운터를 읽고 성능 데이터를 사용자 지정 카운터에 쓰거나 게시할 수 있습니다.|  
|<xref:System.Diagnostics.PerformanceCounterCategory?displayProperty=nameWithType>|컴퓨터에서 카운터 및 카운터 범주를 조작하기 위한 여러 메서드를 제공합니다.|  
|<xref:System.Diagnostics.PerformanceCounterInstaller?displayProperty=nameWithType>|`PerformanceCounter` 구성 요소에 대해 설치 관리자를 지정합니다.|  
|<xref:System.Diagnostics.PerformanceCounterType?displayProperty=nameWithType>|`NextValue` 에 대한 `PerformanceCounter`메서드를 계산하는 수식을 지정합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [성능 카운터](../../../docs/framework/debug-trace-profile/performance-counters.md)
