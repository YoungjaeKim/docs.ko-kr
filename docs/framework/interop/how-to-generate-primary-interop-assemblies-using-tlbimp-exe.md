---
title: "방법: Tlbimp.exe를 사용하여 주 Interop 어셈블리 생성"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- primary interop assemblies, generating
- Tlbimp.exe
- Type Library Importer
ms.assetid: 5419011c-6e57-40f6-8c65-386db8f7a651
caps.latest.revision: 
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: bdf39da2a597d75479a2a3ed3d60132a0f7e7def
ms.sourcegitcommit: d95a91d685565f4d95c8773b558752864a6a3d7e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2018
---
# <a name="how-to-generate-primary-interop-assemblies-using-tlbimpexe"></a>방법: Tlbimp.exe를 사용하여 주 Interop 어셈블리 생성
주 interop 어셈블리를 생성하는 다음 두 가지 방법이 있습니다.  
  
-   [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)]에서 제공하는 [형식 라이브러리 가져오기(Tlbimp.exe)](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md) 사용.  
  
     주 interop 어셈블리를 생성하는 가장 간단한 방법은 [Tlbimp.exe(형식 라이브러리 가져오기)](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md)를 사용하는 것입니다. Tlbimp.exe는 다음과 같은 보호 기능을 제공합니다.  
  
    -   중첩된 형식 라이브러리 참조에 대한 새 interop 어셈블리를 만들기 전에 등록된 다른 주 interop 어셈블리를 확인합니다.  
  
    -   컨테이너 또는 파일 이름을 지정하여 주 interop 어셈블리에 강력한 이름을 제공하지 않으면 주 interop 어셈블리를 내보내지 못합니다.  
  
    -   종속 어셈블리에 대한 참조를 생략하면 주 interop 어셈블리를 내보내지 못합니다.  
  
    -   주 interop 어셈블리가 아닌 종속 어셈블리에 대한 참조를 추가하면 주 interop 어셈블리를 내보내지 못합니다.  
  
-   C#과 같은 CLS(공용 언어 사양)를 준수하는 언어를 사용하여 소스 코드에서 수동으로 주 interop 어셈블리 만들기. 이 접근 방식은 형식 라이브러리를 사용할 수 없는 경우에 유용합니다.  
  
 강력한 이름으로 어셈블리에 서명하려면 암호화 키 쌍이 있어야 합니다. 자세한 내용은 [키 쌍 만들기](../../../docs/framework/app-domains/how-to-create-a-public-private-key-pair.md)를 참조하세요.  
  
### <a name="to-generate-a-primary-interop-assembly-using-tlbimpexe"></a>Tlbimp.exe를 사용하여 주 Interop 어셈블리를 생성하려면  
  
1.  명령 프롬프트에서 다음을 입력합니다.  
  
     **tlbimp** *tlbfile*  **/primary /keyfile:** *filename* **/out:** *assemblyname*  
  
     이 명령에서 *tlbfile*은 COM 형식 라이브러리를 포함하는 파일이고, *filename*은 키 쌍을 포함하는 컨테이너 또는 파일의 이름이고, *assemblyname*은 강력한 이름으로 서명할 어셈블리의 이름입니다.  
  
 주 interop 어셈블리는 다른 주 interop 어셈블리만 참조할 수 있습니다. 어셈블리가 타사 COM 형식 라이브러리의 형식을 참조하는 경우 먼저 게시자로부터 주 interop 어셈블리를 얻어야 고유한 주 interop 어셈블리를 생성할 수 있습니다. 게시자인 경우 참조하는 주 interop 어셈블리를 생성하기 전에 종속 형식 라이브러리에 대한 주 interop 어셈블리를 생성해야 합니다.  
  
 원본 형식 라이브러리와 다른 버전 번호를 가진 종속된 주 interop 어셈블리는 현재 디렉터리에 설치된 경우 검색할 수 없습니다. Windows 레지스트리에 종속된 주 interop 어셈블리를 등록하거나 **/reference** 옵션을 사용하여 Tlbimp.exe가 종속 DLL을 찾을 수 있도록 해야 합니다.  
  
 여러 버전의 형식 라이브러리를 래핑할 수도 있습니다. 자세한 내용은 [방법: 여러 버전의 형식 라이브러리 래핑](https://msdn.microsoft.com/library/79eefe04-a770-4bc3-8ea2-e90ddb8ec31f(v=vs.100))을 참조하세요.  
  
## <a name="example"></a>예  
 다음 예제에서는 COM 형식 라이브러리 `LibUtil.tlb`를 가져오고 키 파일 `CompanyA.snk`를 사용하여 강력한 이름으로 `LibUtil.dll` 어셈블리에 서명합니다. 이 예제에서는 특정 네임스페이스 이름을 생략하여 기본 네임스페이스 `LibUtil`을 생성합니다.  
  
```  
tlbimp LibUtil.tlb /primary /keyfile:CompanyA.snk /out:LibUtil.dll  
```  
  
 보다 설명적인 이름(*VendorName*.*LibraryName* 명명 지침 사용)을 위해 다음 예제에서는 기본 어셈블리 파일 이름 및 네임스페이스 이름을 재정의합니다.  
  
```  
tlbimp LibUtil.tlb /primary /keyfile:CompanyA.snk /namespace:CompanyA.LibUtil /out:CompanyA.LibUtil.dll  
```  
  
 다음 예제에서는 `CompanyA.LibUtil.dll`을 참조하는 `MyLib.tlb`를 가져오고 키 파일 `CompanyB.snk`를 사용하여 강력한 이름으로 `CompanyB.MyLib.dll` 어셈블리에 서명합니다. `CompanyB.MyLib` 네임스페이스에서 기본 네임스페이스 이름을 재정의합니다.  
  
```  
tlbimp MyLib.tlb /primary /keyfile:CompanyB.snk /namespace:CompanyB.MyLib /reference:CompanyA.LibUtil.dll /out:CompanyB.MyLib.dll  
```  
  
## <a name="see-also"></a>참고 항목  
 [방법: 주 Interop 어셈블리 등록](../../../docs/framework/interop/how-to-register-primary-interop-assemblies.md)
