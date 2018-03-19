---
title: "&lt;추가&gt; webRequestModules (네트워크 설정)에 대 한 요소"
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
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/webRequestModules/add
- http://schemas.microsoft.com/.NetConfiguration/v2.0#add
helpviewer_keywords:
- <webRequestModules>, add element
- webRequestModules, add element
- add element, webRequestModules
- <add> element, webRequestModules
ms.assetid: 47ec4adc-f39f-4bcd-8680-1ec21fd26890
caps.latest.revision: 
author: mcleblanc
ms.author: markl
manager: markl
ms.workload:
- dotnet
ms.openlocfilehash: 9b7d2c0f52ea42fcb98be149ab005cd67c2db46a
ms.sourcegitcommit: 15316053918995cc1380163a7d7e7edd5c44e6d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2018
---
# <a name="ltaddgt-element-for-webrequestmodules-network-settings"></a>&lt;추가&gt; webRequestModules (네트워크 설정)에 대 한 요소
응용 프로그램에 사용자 지정 웹 요청 모듈을 추가합니다.  
  
 \<configuration>  
\<system.net>  
\<webRequestModules>  
\<add>  
  
## <a name="syntax"></a>구문  
  
```xml  
<add   
  prefix="URI prefix"   
  type="type_fullname, assembly_fullname"   
/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|**특성**|**설명**|  
|-------------------|---------------------|  
|`prefix`|이 웹 요청 모듈에서 처리 요청에 대 한 URI 접두사입니다.|  
|`type`|정규화 된 형식 이름 (으로 표시는 <xref:System.Type.FullName%2A> 속성)와 어셈블리 이름 (가리키는 <xref:System.Reflection.Assembly.FullName%2A> 속성)을이 웹 요청 모듈을 구현 하는 쉼표로 구분 합니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|**요소**|**설명**|  
|-----------------|---------------------|  
|[webRequestModules](../../../../../docs/framework/configure-apps/file-schema/network/webrequestmodules-element-network-settings.md)|네트워크 호스트에서 정보를 요청 하는 데는 모듈을 지정 합니다.|  
  
## <a name="remarks"></a>설명  
 `prefix` 특성 지정 된 웹 요청 모듈을 사용 하는 URI 접두사를 정의 합니다. 웹 요청 모듈은 일반적으로 HTTP 또는 FTP와 같은 특정 프로토콜을 처리 하도록 등록 되어 있지만 서버에서 경로 또는 특정 서버에 요청을 처리 하도록 등록할 수 있습니다.  
  
 URI 일치 하는 접두사에 전달 되 면 웹 요청 모듈 만들어집니다는 <xref:System.Net.WebRequest.Create%2A?displayProperty=nameWithType> 메서드.  
  
 에 대 한 값은 `prefix` 특성에는 예를 들어 "http"는 유효한 URI의 선행 문자를 사용 해야 합니다. 또는 "http://www.contoso.com"입니다.  
  
 에 대 한 값은 `type` 특성 유효한 형식 이름 및 쉼표로 구분 하 여 해당 어셈블리 이름 이어야 합니다.  
  
## <a name="configuration-files"></a>구성 파일  
 이 요소는 응용 프로그램 구성 파일 또는 컴퓨터 구성 파일(Machine.config)에서 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 HTTP에 대 한 사용자 지정 웹 요청 모듈을 등록 합니다. 지정된 된 모듈에 대 한 올바른 값으로 PublicKeyToken 및 버전에 대 한 값 바꿔야 합니다.  
  
```xml  
<configuration>  
  <system.net>  
    <webRequestModules>  
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
