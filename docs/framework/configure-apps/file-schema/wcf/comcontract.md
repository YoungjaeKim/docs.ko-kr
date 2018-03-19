---
title: '&lt;comContract&gt;'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3f8e1c0c-cfdf-4c79-ac65-c64e9323a51c
caps.latest.revision: 
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 8fa70ba3cf8e66411812b84821e80772c9930f7c
ms.sourcegitcommit: 15316053918995cc1380163a7d7e7edd5c44e6d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2018
---
# <a name="ltcomcontractgt"></a>&lt;comContract&gt;
COM+ 통합 서비스 계약을 지정합니다.  
  
 \<system.ServiceModel>  
\<comContracts>  
  
## <a name="syntax"></a>구문  
  
```xml  
<comContracts>  
  <comContract  
      contract="string"  
      namespace="string"  
      name="string"  
      requireSession="Boolean">  
      <exposedMethods>  
         <exposedMethod name="string" />  
      </exposedMethods>  
      <userDefinedTypes>  
         <userDefinedType name="string"  
            typeLibID="string"  
            typeLibVersion="string"  
            typeDefID="string">  
         </userDefinedType>  
      </userDefinedTypes>  
      <persistableTypes>  
         <persistableType id="string"  
            name="string">  
         </persistableType>  
      </persistableTypes>  
  </comContract>  
</comContracts>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|계약(contract)|계약 형식을 포함하는 문자열입니다.|  
|name|계약 이름을 포함하는 문자열입니다.|  
|namespace|계약 네임스페이스를 포함하는 문자열입니다.|  
|requiresSession|계약을 세션 바인딩에서만 사용할 수 있는지 여부를 지정하는 부울 값입니다. 서비스가 초기화될 때 통합 런타임에서는 사용될 바인딩 형식과 이 설정이 일치하는지 확인합니다. 계약의 바인딩 중 하나 이상이 충돌할 경우 예외가 생성됩니다. 이 속성이 `false`이고 단방향 채널을 사용하며 [out] 매개 변수가 있을 경우에도 예외가 생성됩니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|persistableTypes|모든 지속 형식입니다.|  
|userDefinedTypes|서비스 계약에 포함될 UDT(사용자 정의 형식) 컬렉션입니다.|  
|exposedMethods|COM+ 구성 요소의 인터페이스가 웹 서비스로 공개될 때 노출되는 COM+ 메서드 컬렉션입니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|comContracts|`comContract` 요소의 컬렉션을 포함합니다.|  
  
## <a name="remarks"></a>설명  
 COM + 통합 서비스 계약은 현재 제한 되며는 "http://tempuri.org" 네임 스페이스, 계약 이름은 지원 COM 인터페이스에서 파생 됩니다. 그러나 구성 파일에서`comContracts` 섹션 및 `comContract` 요소를 사용하여 대안을 지정할 수 있습니다. 예를 들어 다음 구성을 사용하여 포함시킬 네임스페이스, 계약 이름, 사용자 정의 형식 및 서비스 계약의 기타 설정을 지정할 수 있습니다.  
  
```xml  
<comContracts>  
  <comContract  
      contract="{5163B1E7-F0CF-4B6A-9A02-4AB654F34284}"  
      namespace="http://tempuri.org/5163B1E7-F0CF-4B6A-9A02-4AB654F34284"  
      name="_Broker"  
      requireSession="true">  
      <exposedMethods>  
         <exposedMethod name="BuyStock" />  
         <exposedMethod name="SellStock" />  
         <exposedMethod name="ExecuteTransaction" />  
      </exposedMethods>  
  </comContract>  
</comContracts>  
```  
  
 지정된 네임스페이스와 계약 이름은 서비스가 초기화될 때 생성된 서비스 설명에 적용됩니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.ServiceModel.Configuration.ComContractElementCollection>  
 <xref:System.ServiceModel.Configuration.ComContractElementCollection>  
 <xref:System.ServiceModel.Configuration.ComContractElement>  
 [\<comContracts>](../../../../../docs/framework/configure-apps/file-schema/wcf/comcontracts.md)  
 [COM+ 응용 프로그램과 통합](../../../../../docs/framework/wcf/feature-details/integrating-with-com-plus-applications.md)  
 [방법: COM+ 서비스 설정 구성](../../../../../docs/framework/wcf/feature-details/how-to-configure-com-service-settings.md)
