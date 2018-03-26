---
title: ICorProfilerCallback7::ModuleInMemorySymbolsUpdated Method
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
api_name:
- ICorProfiler7.ModuleInMemorySymbolsUpdated
api_location:
- mscorwks.dll
- corprof.idl
api_type:
- COM
ms.assetid: f362a896-3247-4894-9727-e48dbbcd2c78
caps.latest.revision: ''
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 898adf043e425c00d6e311e2f67c53ed65cacb33
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="icorprofilercallback7moduleinmemorysymbolsupdated-method"></a>ICorProfilerCallback7::ModuleInMemorySymbolsUpdated Method
[.NET Framework 4.6.1 이상 버전에서 지원됨]  
  
 메모리 내 모듈과 연관 된 기호 스트림이 업데이트 될 때마다 프로파일러를 알립니다.  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT ModuleInMemorySymbolsUpdated(  
     ModuleID moduleId  
);  
```  
  
#### <a name="parameters"></a>매개 변수  
 `moduleId`  
 메모리 내 모듈과 된 기호 스트림이 업데이트의 식별자입니다.  
  
## <a name="remarks"></a>설명  
 이 콜백을 설정 하 여 제어는 [COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED](../../../../docs/framework/unmanaged-api/profiling/cor-prf-high-monitor-enumeration.md) 이벤트 마스크 플래그를 호출할 때는 [ICorProfilerCallback5::SetEventMask2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo5-seteventmask2-method.md) 메서드.  
  
> [!NOTE]
>  이 이벤트는 암시적으로 만들거나 수정한 통해 기호에 대 한 현재 발생 되지 <xref:System.Reflection.Emit> Api입니다.  
  
 도 경우 기호에에서 제공 된 들겠지만 관리 되는 오버 로드 중 하나에 대 한 호출 <xref:System.Reflection.Assembly.Load*?displayProperty=nameWithType> 메서드를 포함 하는 `rawSymbolStore` 런타임 어셈블리에 대 한 기호를 지정 하려면 인수 기호 데이터 모듈과 함께 실제로 연결 하지 않을 수 있습니다 될 때까지 후의 [ModuleLoadFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-moduleloadfinished-method.md) 콜백이 발생 했습니다. 이 이벤트는 이러한 모듈에 대 한 기호를 수집 하는 이후 기회를 제공 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** 참조 [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)합니다.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v461plus](../../../../includes/net-current-v461plus-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [ModuleLoadFinished 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-moduleloadfinished-method.md)  
 [SetEventMask2 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo5-seteventmask2-method.md)  
 [ICorProfilerCallback7 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback7-interface.md)
