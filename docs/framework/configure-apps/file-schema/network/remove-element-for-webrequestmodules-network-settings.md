---
title: "&lt;제거&gt; webRequestModules (네트워크 설정)에 대 한 요소"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/webRequestModules/remove
- http://schemas.microsoft.com/.NetConfiguration/v2.0#remove
helpviewer_keywords:
- remove element, webRequestModules
- webRequestModules, remove element
- <remove> element, webRequestModules
- <webRequestModules>, remove element
ms.assetid: dd84d2fe-2f4f-457a-9d3c-441d0d21cc10
caps.latest.revision: 
author: mcleblanc
ms.author: markl
manager: markl
ms.workload:
- dotnet
ms.openlocfilehash: 391e5f2a7d9d8076ba9e9a3057e3d8899e2ce672
ms.sourcegitcommit: 15316053918995cc1380163a7d7e7edd5c44e6d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2018
---
# <a name="ltremovegt-element-for-webrequestmodules-network-settings"></a>&lt;제거&gt; webRequestModules (네트워크 설정)에 대 한 요소
응용 프로그램에서 사용자 지정 웹 요청 모듈을 제거합니다.  
  
 \<configuration>  
\<system.net>  
\<webRequestModules>  
\<remove>  
  
## <a name="syntax"></a>구문  
  
```xml  
<remove   
  prefix="URI prefix"   
/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|**특성**|**설명**|  
|-------------------|---------------------|  
|`prefix`|이 웹 요청 모듈에서 처리 요청에 대 한 URI 접두사입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|**요소**|**설명**|  
|-----------------|---------------------|  
|[webRequestModules](../../../../../docs/framework/configure-apps/file-schema/network/webrequestmodules-element-network-settings.md)|네트워크 호스트에서 정보를 요청 하는 데는 모듈을 지정 합니다.|  
  
## <a name="remarks"></a>설명  
 `remove` 요소에 지정된 된 URI 접두사에 대 한 등록된 웹 요청 모듈 제거 합니다.  
  
 에 대 한 값은 `prefix` 특성에는 예를 들어 "http"는 유효한 URI의 선행 문자를 사용 해야 합니다. 또는 "http://www.contoso.com"입니다.  
  
## <a name="configuration-files"></a>구성 파일  
 이 요소는 응용 프로그램 구성 파일 또는 컴퓨터 구성 파일(Machine.config)에서 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 HTTP에 대 한 기존 웹 요청 모듈을 제거 하 고 만든 다음 www.contoso.com에 대 한 HTTP 요청에 대 한 새 사용자 지정 웹 요청 모듈을 등록 합니다.  
  
```xml  
<configuration>  
  <system.net>  
    <webRequestModules>  
      <remove prefix="http">  
      <add prefix="http"  
           type="System.Net.HttpRequestCreator, System, Version=2.0.3600.0,  
           Culture=neutral, PublicKeyToken=b77a5c561934e089"  
      />  
    </webRequestModules>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Net.WebRequest>  
 [네트워크 설정 스키마](../../../../../docs/framework/configure-apps/file-schema/network/index.md)
