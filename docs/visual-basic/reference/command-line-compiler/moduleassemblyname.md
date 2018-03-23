---
title: -moduleassemblyname
ms.date: 03/13/2018
ms.prod: .net
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- moduleassemblyname compiler option [Visual Basic]
- /moduleassemblyname compiler option [Visual Basic]
- -moduleassemblyname compiler option [Visual Basic]
ms.assetid: 013a57b6-f425-4dd3-b333-512d72c42f55
author: rpetrusha
ms.author: ronpett
ms.openlocfilehash: 0a097ea8a7e30f25a0abb877dc496fb81d1c139f
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="-moduleassemblyname"></a>-moduleassemblyname
이 모듈이 속할 어셈블리의 이름을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
-moduleassemblyname:assembly_name  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`assembly_name`|이 모듈의 포함 될 하는 어셈블리의 이름입니다.|  
  
## <a name="remarks"></a>설명  
 컴파일러 프로세스는 `-moduleassemblyname` 경우에만 옵션은 `-target:module` 옵션이 지정 되었습니다. 이 모듈을 만들려면 컴파일러가 합니다. 컴파일러에서 생성 된 모듈은 지정 된 어셈블리에만 유효는 `-moduleassemblyname` 옵션입니다. 다른 어셈블리에 모듈을 배치 하는 경우 런타임 오류가 발생 합니다.  
  
 `-moduleassemblyname` 옵션 다음에 해당할 경우에 필요 합니다.  
  
-   모듈의 데이터 형식에 액세스 해야 하는 `Friend` 는 참조 된 어셈블리의 형식입니다.  
  
-   참조 된 어셈블리에 모듈이 빌드될 어셈블리에 friend 어셈블리 액세스를 부여 합니다.  
  
 모듈을 만드는 방법에 대 한 자세한 내용은 참조 [/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)합니다. Friend 어셈블리에 대 한 자세한 내용은 참조 [Friend 어셈블리](http://msdn.microsoft.com/library/df0c70ea-2c2a-4bdc-9526-df951ad2d055)합니다.  
  
> [!NOTE]
>  `-moduleassemblyname` 옵션은 Visual Studio 개발 환경 내에서 사용할 수 없습니다; 가능 하다는 명령 프롬프트에서 컴파일할 때만 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [방법: 다중 파일 어셈블리 빌드](../../../framework/app-domains/how-to-build-a-multifile-assembly.md)  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
 [-대상 (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)  
 [-main](../../../visual-basic/reference/command-line-compiler/main.md)  
 [-참조 (Visual Basic)](../../../visual-basic/reference/command-line-compiler/reference.md)  
 [-addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md)  
 [어셈블리 및 전역 어셈블리 캐시](../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)  
 [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)  
 [Friend 어셈블리](http://msdn.microsoft.com/library/df0c70ea-2c2a-4bdc-9526-df951ad2d055)
