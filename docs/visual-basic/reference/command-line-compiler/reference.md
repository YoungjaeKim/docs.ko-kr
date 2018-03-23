---
title: -참조 (Visual Basic)
ms.date: 03/13/2018
ms.prod: .net
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- /reference compiler option [Visual Basic]
- r compiler option [Visual Basic]
- -reference compiler option [Visual Basic]
- /r compiler option [Visual Basic]
- reference compiler option [Visual Basic]
- -r compiler option [Visual Basic]
ms.assetid: 66bdfced-bbf6-43d1-a554-bc0990315737
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ba879dd7079b35bea50c4a6c1d67da7aa57110f6
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="-reference-visual-basic"></a>-참조 (Visual Basic)
컴파일러가 지정 된 어셈블리의 형식 정보 현재 컴파일 중인 프로젝트에서 사용할 수 있게 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
-reference:fileList  
' -or-  
-r:fileList  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`fileList`|필수. 쉼표로 구분된 어셈블리 파일 이름 목록입니다. 파일 이름에 공백이 있으면 이름을 따옴표로 묶습니다.|  
  
## <a name="remarks"></a>설명  
 가져오는 파일 어셈블리 메타 데이터를 포함 해야 합니다. Public 형식만 어셈블리 외부에 표시 됩니다. [/addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md) 옵션 모듈에서 메타 데이터를 가져옵니다.  
  
 어셈블리 (어셈블리 A) 참조 하는 경우는 다른 어셈블리 (어셈블리 B)를 참조 하는 경우를 어셈블리 B를 참조 해야 합니다.  
  
-   어셈블리 A의 형식은 형식에서 상속되거나 어셈블리 B의 인터페이스를 구현합니다.  
  
-   어셈블리 B의 반환 형식이나 매개 변수 형식을 사용하는 필드, 속성, 이벤트 또는 메서드가 호출됩니다.  
  
 사용 하 여 [-libpath](../../../visual-basic/reference/command-line-compiler/libpath.md) 어셈블리 참조 중 하나 이상이 있는 디렉터리를 지정할 수 있습니다.  
  
 어셈블리 (모듈 아님)의 형식을 인식할 수 컴파일러의 경우 해당 형식을 확인할 강제 해야 합니다. 이 수행할 수 있는 방법의 한 가지 예는 형식의 인스턴스를 정의 하는 것입니다. 다른 방법으로 가지는 컴파일러에 대 한 어셈블리의 형식 이름을 확인할 수 있습니다. 예를 들어, 어셈블리의 형식에서 상속 하는 경우 형식 이름에 알려집니다 컴파일러입니다.  
  
 참조에서 일반적으로 사용 되는 Vbc.rsp 지시 파일을 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 어셈블리, 기본적으로 사용 됩니다. 사용 하 여 `-noconfig` 컴파일러에서 Vbc.rsp를 사용 하지 않도록 합니다.  
  
 `-reference`의 약식은 `/r`입니다.  
  
## <a name="example"></a>예제  
 다음 명령에서는 소스 파일 `Input.vb` 의 어셈블리를 참조 하 고 `Metad1.dll` 및 `Metad2.dll` 되려면 `Out.exe`합니다.  
  
```console
vbc -reference:metad1.dll,metad2.dll -out:out.exe input.vb  
```  
  
## <a name="see-also"></a>참고 항목  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
 [-noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)  
 [-대상 (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)  
 [공용](../../../visual-basic/language-reference/modifiers/public.md)  
 [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
