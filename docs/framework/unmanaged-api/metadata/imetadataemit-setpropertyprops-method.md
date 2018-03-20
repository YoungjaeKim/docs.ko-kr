---
title: "IMetaDataEmit::SetPropertyProps 메서드"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name:
- IMetaDataEmit.SetPropertyProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetPropertyProps
helpviewer_keywords:
- SetPropertyProps method [.NET Framework metadata]
- IMetaDataEmit::SetPropertyProps method [.NET Framework metadata]
ms.assetid: e2501fc8-b2bc-4dcc-9205-e3acd5a53ffe
topic_type:
- apiref
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 47bbd703c0b1d1b2038b4a6e5dc3aa677e02babe
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/22/2017
---
# <a name="imetadataemitsetpropertyprops-method"></a>IMetaDataEmit::SetPropertyProps 메서드
이전 호출에서 정의한 속성에 대 한 메타 데이터에 저장 하는 기능을 설정 [DefineProperty 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-defineproperty-method.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT SetPropertyProps (   
    [in]  mdProperty      pr,   
    [in]  DWORD           dwPropFlags,   
    [in]  DWORD           dwCPlusTypeFlag,   
    [in]  void const      *pValue,   
    [in]  ULONG           cchValue,   
    [in]  mdMethodDef     mdSetter,   
    [in]  mdMethodDef     mdGetter,   
    [in]  mdMethodDef     rmdOtherMethods[]   
);  
```  
  
#### <a name="parameters"></a>매개 변수  
 `pr`  
 [in] 변경할 속성에 대 한 토큰  
  
 `dwPropFlags`  
 [in] 속성 플래그입니다.  
  
 `dwCPlusTypeFlag`  
 [in] 형식 속성의 기본값입니다.  
  
 `pValue`  
 [in] 속성에 대 한 기본 값입니다.  
  
 `cchValue`  
 [in] \(유니코드) 수의 문자 `pValue`합니다.  
  
 `mdSetter`  
 [in] 속성 값을 설정 하는 메서드.  
  
 `mdGetter`  
 [in] 속성 값을 가져오는 하는 메서드.  
  
 `rmdOtherMethods[]`  
 [in] 배열 속성에 연결 된 다른 방법입니다. 이 배열의 종료는 `mdTokenNil` 토큰입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** 참조 [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)합니다.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MSCorEE.dll에서 리소스로 사용  
  
 **.NET framework 버전:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [IMetaDataEmit 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)  
 [IMetaDataEmit2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)
