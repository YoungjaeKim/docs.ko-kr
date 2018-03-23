---
title: 서비스 메타데이터에서 WCF 클라이언트 생성
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 27f8f545-cc44-412a-b104-617e0781b803
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 9eedf84d1dccb8bc2540aca7e6bd338b4e58326d
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/23/2018
---
# <a name="generating-a-wcf-client-from-service-metadata"></a>서비스 메타데이터에서 WCF 클라이언트 생성
이 항목에서는 Svcutil.exe의 여러 가지 스위치를 사용하여 메타데이터 문서에서 클라이언트를 생성하는 방법에 대해 설명합니다.  
  
 메타데이터 문서는 지속적인 저장소에 있거나 온라인으로 검색할 수 있습니다. 온라인 검색은 WS-MetadataExchange 프로토콜이나 Microsoft Discovery(DISCO) 프로토콜을 따릅니다. Svcutil.exe는 다음 메타데이터 요청을 생성하고 동시에 메타데이터를 검색합니다.  
  
-   제공된 주소에 대한 WS-MetadataExchange(MEX) 요청  
  
-   `/mex`가 추가된 제공된 주소에 대한 MEX 요청  
  
-   한 DISCO 요청 (사용 하는 [DiscoveryClientProtocol](http://go.microsoft.com/fwlink/?LinkId=94777) ASP.NET 웹 서비스에서) 주어진된 주소에 있습니다.  
  
 Svcutil.exe는 WSDL(웹 서비스 기술 언어)을 기반으로 하는 클라이언트 또는 서비스로부터 받은 정책 파일을 생성합니다. UPN(User Principal Name)은 사용자 이름을 "@"으로 연결한 다음 FQDN(정규화된 도메인 이름)을 추가하여 생성합니다. 그러나 Active Directory에 등록 한 사용자의이 형식은 올바르지 않으며 도구에서 생성 한 UPN으로 인해 다음과 같은 오류 메시지와 함께 Kerberos 인증의는 실패: **로그온 시도가 실패 했습니다.** 이 문제를 해결하려면 이 도구에서 생성한 클라이언트 파일을 수동으로 수정합니다.  
  
```  
svcutil.exe [/t:code]  <metadataDocumentPath>* | <url>* | <epr>  
```  
  
## <a name="referencing-and-sharing-types"></a>형식 참조 및 공유  
  
|옵션|설명|  
|------------|-----------------|  
|**/reference:\<파일 경로 >**|지정한 어셈블리에서 형식을 참조합니다. 클라이언트를 생성할 때 이 옵션을 사용하여 가져오는 메타데이터를 나타내는 형식이 포함될 수 있는 어셈블리를 지정합니다.<br /><br /> 약식: `/r`|  
|**/excludeType:\<type>**|참조된 계약 형식에서 제외할 정규화된 형식 이름 또는 정규화된 어셈블리 형식 이름을 지정합니다.<br /><br /> 약식: `/et`|  
  
## <a name="choosing-a-serializer"></a>Serializer 선택  
  
|옵션|설명|  
|------------|-----------------|  
|**/serializer:Auto**|serializer를 자동으로 선택합니다. `DataContract` serializer가 사용됩니다. 이 작업에 실패할 경우 `XmlSerializer`가 사용됩니다.<br /><br /> 약식: `/ser:Auto`|  
|**/serializer:DataContractSerializer**|serialization 및 deserialization을 위해 `DataContract` serializer를 사용하는 데이터 형식을 생성합니다.<br /><br /> 약식: `/ser:DataContractSerializer`|  
|**/serializer:XmlSerializer**|serialization 및 deserialization을 위해 `XmlSerializer`를 사용하는 데이터 형식을 생성합니다.<br /><br /> 약식: `/ser:XmlSerializer`|  
|**/importXmlTypes**|비 `DataContract` 형식을 `DataContract` 형식으로 가져오도록 `IXmlSerializable` serializer를 구성합니다.<br /><br /> 약식: `/ixt`|  
|**/dataContractOnly**|`DataContract` 형식에 대한 코드만 생성합니다. `ServiceContract` 형식이 생성됩니다.<br /><br /> 이 옵션에 대한 로컬 메타데이터 파일만 지정해야 합니다.<br /><br /> 약식: `/dconly`|  
  
## <a name="choosing-a-language-for-the-client"></a>클라이언트에 대한 언어 선택  
  
|옵션|설명|  
|------------|-----------------|  
|**/language:\<language>**|코드 생성에 사용할 프로그래밍 언어를 지정합니다. Machine.config 파일에 등록된 언어 이름 또는 <xref:System.CodeDom.Compiler.CodeDomProvider>에서 상속된 클래스의 정규화된 이름을 입력합니다.<br /><br /> 값: c#, cs, csharp, vb, vbs, visualbasic, vbscript, javascript, c++, mc, cpp<br /><br /> 기본값: csharp<br /><br /> 약식: `/l`<br /><br /> [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [CodeDomProvider 클래스](http://go.microsoft.com/fwlink/?LinkId=94778)합니다.|  
  
## <a name="choosing-a-namespace-for-the-client"></a>클라이언트에 대한 네임스페이스 선택  
  
|옵션|설명|  
|------------|-----------------|  
|**/namespace:\<string,string>**|WSDL 또는 XML 스키마 `targetNamespace`에서 CLR(공용 언어 런타임) 네임스페이스로 매핑을 지정합니다. `targetNamespace`에 와일드카드(*)를 사용하여 해당 CLR 네임스페이스에 명시적으로 매핑하지 않고 모든 `targetNamespaces`를 매핑합니다.<br /><br /> 메시지 계약 이름이 작업 이름과 충돌하지 않도록 하려면 이중 콜론(`::`)을 사용하여 형식 참조를 한정하거나 이름이 고유한지 확인합니다.<br /><br /> 기본값: `DataContracts`에 대한 스키마 문서의 대상 네임스페이스에서 파생됩니다. 기본 네임스페이스는 생성된 다른 모든 형식에 사용됩니다.<br /><br /> 약식: `/n`|  
  
## <a name="choosing-a-data-binding"></a>데이터 바인딩 선택  
  
|옵션|설명|  
|------------|-----------------|  
|**/enableDataBinding**|모든 <xref:System.ComponentModel.INotifyPropertyChanged> 형식에 `DataContract` 인터페이스를 구현하여 데이터 바인딩을 사용할 수 있습니다.<br /><br /> 약식: `/edb`|  
  
## <a name="generating-configuration"></a>구성 생성  
  
|옵션|설명|  
|------------|-----------------|  
|**/config:\<configFile>**|생성된 구성 파일에 대한 파일 이름을 지정합니다.<br /><br /> 기본값: output.config|  
|**/mergeConfig**|기존 파일을 덮어쓰는 대신 생성된 구성을 기존 파일에 병합합니다.|  
|**/noConfig**|구성 파일을 생성하지 않습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [메타데이터 사용](../../../../docs/framework/wcf/feature-details/using-metadata.md)  
 [메타데이터 아키텍처 개요](../../../../docs/framework/wcf/feature-details/metadata-architecture-overview.md)
