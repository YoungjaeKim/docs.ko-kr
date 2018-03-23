---
title: -highentropyva (Visual Basic)
ms.date: 03/10/2018
ms.prod: .net
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- highentropyva compiler option (Visual Basic)
- /highentropyva compiler option (Visual Basic)
ms.assetid: ff25f20a-6ca2-467b-9e52-5cf439f5028e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 12d40e5acda73786ee88d16bacd9bc5f69400be8
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="-highentropyva-visual-basic"></a>-highentropyva (Visual Basic)
나타냅니다 64 비트 실행 파일 또는로 표시 된 실행 개체는 [/platform:anycpu](../../../visual-basic/reference/command-line-compiler/platform.md) 컴파일러 옵션은 높은 엔트로피 주소 공간 레이아웃 불규칙화 (ASLR)를 지원 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
-highentropyva[+ | -]  
```  
  
## <a name="arguments"></a>인수  
 `+` &#124; `-`  
 선택 사항입니다. 기본적으로 해제 되어 옵션 또는 지정 하는 경우 `-highentropyva-`합니다. 지정 하는 경우에 옵션은 `-highentropyva` 또는 `-highentropyva+`합니다.  
  
## <a name="remarks"></a>설명  
 이 옵션을 지정 하면 Windows 커널의 호환 되는 버전 커널 ASLR의 일부로 프로세스의 주소 공간 레이아웃을 임의 할 때 보다 높은 수준의 엔트로피를 사용할 수 있습니다. 커널에서 더 높은 수준의 엔트로피를 사용 하는 경우 스택 및 힙과 같은 메모리 영역에 더 많은 주소를 할당할 수 있습니다. 따라서 특정 메모리 영역의 위치를 추측하기 어려워집니다.  
  
 이 옵션이 설정 되는 대상 실행 파일 및 모든 모듈에는 해당 모듈 64 비트 프로세스로 실행 하는 경우 4 기가바이트 (GB) 보다 큰 포인터 값을 처리 있어야 그에 따라 달라 지는 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
 [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
