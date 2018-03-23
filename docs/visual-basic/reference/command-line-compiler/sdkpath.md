---
title: -sdkpath
ms.date: 07/20/2015
ms.prod: .net
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- sdkpath
- -sdkpath
helpviewer_keywords:
- -sdkpath compiler option [Visual Basic]
- /sdkpath compiler option [Visual Basic]
- sdkpath compiler option [Visual Basic]
ms.assetid: fec8a3f1-b791-4a37-8af7-344859f8212d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 53362c2eb5517d9230ea88975745315d6db7f1ba
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="-sdkpath"></a>-sdkpath
Mscorlib.dll 및 Microsoft.VisualBasic.dll의 위치를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
-sdkpath:path  
```  
  
## <a name="arguments"></a>인수  
 `path`  
 Mscorlib.dll 및 Microsoft.VisualBasic.dll 컴파일에 사용할의 버전이 포함 된 디렉터리입니다. 이 경로 로드 될 때까지 확인 되지 않습니다. 디렉터리 이름을 따옴표로 묶습니다 ("")에 공백이 있는 경우.  
  
## <a name="remarks"></a>설명  
 이 옵션은 지시는 [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] 컴파일러에 기본이 아닌 위치에서 mscorlib.dll 및 Microsoft.VisualBasic.dll 파일을 로드 합니다. `-sdkpath` 옵션으로 사용할 수 있도록 설계 된 [-netcf](../../../visual-basic/reference/command-line-compiler/netcf.md)합니다. [!INCLUDE[Compact](~/includes/compact-md.md)] 이러한 서로 다른 버전을 사용 하 여 형식 및 장치에서 찾을 수 없는 언어 기능 사용을 방지 하기 위해 라이브러리를 지원 합니다.  
  
> [!NOTE]
>  `-sdkpath` 옵션은 Visual Studio 개발 환경 내에서 사용할 수 없습니다; 명령줄에서 컴파일할 경우에 사용할 수는 있습니다. `-sdkpath` 옵션을 설정 하는 경우는 [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] 장치 프로젝트를 로드 합니다.  
  
 해당 컴파일러를 사용 하 여 Visual Basic 런타임 라이브러리에 대 한 참조 없이 컴파일하여 해야 지정할 수는 `-vbruntime` 컴파일러 옵션입니다. 자세한 내용은 참조 [-vbruntime](../../../visual-basic/reference/command-line-compiler/vbruntime.md)합니다.  
  
## <a name="example"></a>예제  
 다음 코드에서는 `Myfile.vb` 와 [!INCLUDE[Compact](~/includes/compact-md.md)]의 기본 설치 디렉터리에 있는 Mscorlib.dll 및 Microsoft.VisualBasic.dll의 버전을 사용 하는 [!INCLUDE[Compact](~/includes/compact-md.md)] C 드라이브에 있습니다. 일반적으로 가장 최신 버전의 사용은 [!INCLUDE[Compact](~/includes/compact-md.md)]합니다.  
  
```console
vbc -netcf -sdkpath:"c:\Program Files\Microsoft Visual Studio .NET 2003\CompactFrameworkSDK\v1.0.5000\Windows CE " myfile.vb  
```  
  
## <a name="see-also"></a>참고 항목  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
 [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)  
 [-netcf](../../../visual-basic/reference/command-line-compiler/netcf.md)  
 [-vbruntime](../../../visual-basic/reference/command-line-compiler/vbruntime.md)
