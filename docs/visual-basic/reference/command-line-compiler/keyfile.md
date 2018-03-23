---
title: -keyfile
ms.date: 03/10/2018
ms.prod: .net
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- /keyfile compiler option [Visual Basic]
- keyfile compiler option [Visual Basic]
- -keyfile compiler option [Visual Basic]
ms.assetid: ffa82a4b-517a-4c6c-9889-5bae7b534bb8
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 02169f1f43ba93b68dc47f5bad038b78d3635a80
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="-keyfile"></a>-keyfile
어셈블리에 강력한 이름을 지정하는 키 또는 키 쌍이 포함된 파일을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
``` 
-keyfile:file  
```  
  
## <a name="arguments"></a>인수  
 `file`  
 필수. 키가 포함 된 파일입니다. 파일 이름에 공백이 있으면 이름을 따옴표로 묶습니다 ("").  
  
## <a name="remarks"></a>설명  
 컴파일러는 공개 키를 어셈블리 매니페스트에 삽입 한 다음 개인 키와 함께 최종 어셈블리에 서명 합니다. 키 파일을 생성 하려면 입력 `sn -k file` 명령줄에서. 자세한 내용은 [Sn.exe (강력한 이름 도구)]을 참조 하십시오.[Sn.exe (강력한 이름 도구)](../../../framework/tools/sn-exe-strong-name-tool.md)).  
  
 사용 하 여 컴파일하면 `-target:module`, 키 파일의 이름이 모듈에 저장 되 고 있는 어셈블리를 컴파일할 때 만들어진 어셈블리 [/addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md)합니다.  
  
 [-keycontainer](../../../visual-basic/reference/command-line-compiler/keycontainer.md)를 사용하여 암호화 정보를 컴파일러에 전달할 수도 있습니다. 부분 서명된 어셈블리가 필요한 경우 [-delaysign](../../../visual-basic/reference/command-line-compiler/delaysign.md)을 사용합니다.  
  
 사용자 지정 특성으로이 옵션을 지정할 수도 있습니다 (<xref:System.Reflection.AssemblyKeyFileAttribute>) Microsoft 중간 언어 모듈의 소스 코드에서.  
  
 둘 다 경우 `-keyfile` 및 [-keycontainer](../../../visual-basic/reference/command-line-compiler/keycontainer.md) 지정 (명령줄 옵션이 나 사용자 지정 특성) 동일한 컴파일에서 컴파일러가 키 컨테이너를 먼저 시도 합니다. 키 컨테이너를 찾으면 키 컨테이너의 정보를 사용하여 어셈블리가 서명됩니다. 컴파일러에서 키 컨테이너를 찾지 못하면 지정 된 파일 시도 `-keyfile`합니다. 이 작업은 성공, 어셈블리 키 파일의 정보로 서명 되 고 키 정보는 키 컨테이너에 설치 된 경우 (비슷합니다 `sn -i`) 다음 컴파일에 키 컨테이너를 사용할 수 있도록 합니다.  
  
 키 파일에는 공개 키만 포함될 수 있습니다.  
  
 참조 [and using strong-named Assemblies](../../../framework/app-domains/create-and-use-strong-named-assemblies.md) 어셈블리 서명에 대 한 자세한 내용은 합니다.  
  
> [!NOTE]
>  `-keyfile` 옵션 내에서 사용할 수 없는 [!INCLUDE[vsprvs](~/includes/vsprvs-md.md)] 개발 환경; 명령줄에서 컴파일할 경우에 사용 가능 합니다.  
  
## <a name="example"></a>예제  
 다음 코드는 소스 파일을 컴파일하 `Input.vb` 및 키 파일을 지정 합니다.  
  
```console  
vbc -keyfile:myfile.sn input.vb  
```  
  
## <a name="see-also"></a>참고 항목  
 [어셈블리 및 전역 어셈블리 캐시](../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
 [-참조 (Visual Basic)](../../../visual-basic/reference/command-line-compiler/reference.md)  
 [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
