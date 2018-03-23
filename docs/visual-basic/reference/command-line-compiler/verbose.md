---
title: -verbose
ms.date: 03/13/2018
ms.prod: .net
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- verbose compiler option [Visual Basic]
- -verbose compiler option [Visual Basic]
- /verbose compiler option [Visual Basic]
ms.assetid: d1aec0c1-0261-421d-9adc-5b13756100be
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f0523409e53a8c7ea34de7dcc24b1bce2885a183
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="-verbose"></a>-verbose
컴파일러가 상태 및 오류에 대 한 자세한 정보 메시지를 생성 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
-verbose[+ | -]  
```  
  
## <a name="arguments"></a>인수  
 `+` &#124; `-`  
 선택 사항입니다. 지정 `-verbose` 지정 하는 것과 같습니다 `-verbose+`, 자세한 정보 메시지를 내보낼 컴파일러가 합니다. 이 옵션의 기본값은 `-verbose-`합니다.  
  
## <a name="remarks"></a>설명  
 `-verbose` 옵션은 컴파일러에서 생성 한 오류의 총 수에 대 한 정보를 표시 합니다. 모듈에 의해 로드 되 고 있는 어셈블리를 보고 하 고 현재 컴파일 중인 파일을 표시 합니다.  
  
> [!NOTE]
>  `-verbose` 옵션은 Visual Studio 개발 환경 내에서 사용할 수 없습니다; 명령줄에서 컴파일할 경우에 사용할 수는 있습니다.  
  
## <a name="example"></a>예제  
 다음 코드에서는 `In.vb` 자세한 상태 정보를 표시 하려면 컴파일러를 안내 합니다.  
  
```console  
vbc -verbose in.vb  
```  
  
## <a name="see-also"></a>참고 항목  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
 [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
