---
title: 마샬링 MDA
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
- marshaling, run-time errors
- marshaling MDA
- managed debugging assistants (MDAs), marshaling
- MDAs (managed debugging assistants), marshaling
ms.assetid: 5433b1f8-b0e5-40c9-a49a-0e5bd213363d
caps.latest.revision: ''
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 83b621f78e3ba4641540f6125ed14d600cc292d1
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="marshaling-mda"></a>마샬링 MDA
`marshaling` MDA(관리 디버깅 도우미)는 CLR이 메서드 매개 변수 또는 구조체 필드에 대한 마샬링 정보를 설정할 때 활성화됩니다. 이 MDA는 JIT 컴파일된 어셈블리에 대해 작동하지 않습니다.  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 이 MDA는 CLR에 아무런 영향을 미치지 않습니다.  
  
## <a name="output"></a>출력  
 MDA에서 관리되는 컨텍스트 및 관리되지 않는 컨텍스트의 매개 변수 또는 필드 형식과 해당 형식을 포함하는 구조체 또는 메서드를 표시합니다.  다음은 필드에 대한 출력 예입니다.  
  
```  
Marshaling from 'Char' to 'ANSI char'  
name="assembly!Namespace.Class::myChar  
```  
  
## <a name="configuration"></a>구성  
 MDA 구성을 통해 관련된 필드 또는 메서드 이름에 따라 보고된 마샬링 정보를 필터링할 수 있습니다.  다음 예제에서는 `methodFilter`, `fieldFilter` 및 `match` 요소를 사용하여 필터를 지정하는 방법을 보여 줍니다.  `name` 특성을 별표(*)로 설정하면 모든 항목과 일치합니다.  
  
```xml  
<mdaConfig>  
  <assistants>  
    <marshaling>  
      <methodFilter>  
        <match name="Method1"/>  
        <match name="Method2"/>  
      </methodFilter>  
      <fieldFilter>  
        <match name="Field1"/>  
        <match name="Field2"/>  
       </fieldFilter>  
    </marshaling>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>  
 [관리 디버깅 도우미를 사용하여 오류 진단](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)  
 [interop 마샬링](../../../docs/framework/interop/interop-marshaling.md)
