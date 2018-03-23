---
title: /debug(Visual Basic)
ms.date: 03/10/2018
ms.prod: .net
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- debug compiler switches
- /debug compiler option [Visual Basic]
- -debug compiler option [Visual Basic]
- debug compiler option [Visual Basic]
ms.assetid: c2b0bea5-1d5e-499f-9bd5-4f6c6b715ea2
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7430a3ac85a86ed5528af9ea830da530208749eb
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="-debug-visual-basic"></a>-디버그 (Visual Basic)
컴파일러가 디버깅 정보를 생성 하 여 출력 파일에 배치 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
-debug[+ | -]  
' -or-  
-debug:[full | pdbonly]  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`+` &#124; `-`|선택 사항입니다. 지정 `+` 또는 `/debug` 컴파일러가 디버깅 정보를 생성 하 여.pdb 파일에 배치 합니다. 지정 `-` 지정 하지 않는 것과 동일한 결과가 `/debug`합니다.|  
|`full` &#124; `pdbonly`|선택 사항입니다. 컴파일러에서 생성되는 디버깅 정보 형식을 지정합니다. 지정 하지 않으면 `/debug:pdbonly`, 기본값은 `full`, 실행 중인 프로그램에 디버거를 연결할 수 있습니다. `pdbonly` 인수를 사용 하면 디버거에서 프로그램을 시작 하지만 실행 중인 프로그램에 디버거 연결 하는 경우에 어셈블리 언어 코드를 표시 하는 경우 소스 코드 디버깅.|  
  
## <a name="remarks"></a>설명  
 디버그 빌드를 만들려면 이 옵션을 사용합니다. 지정 하지 않으면 `/debug`, `/debug+`, 또는 `/debug:full`, 프로그램의 출력 파일을 디버깅할 수 없습니다.  
  
 기본적으로 디버깅 정보 생성 되지는 (`/debug-`). 디버깅 정보를 내보내는 지정 `/debug` 또는 `/debug+`합니다.  
  
 응용 프로그램의 디버그 성능을 구성하는 방법에 대한 자세한 내용은 [쉽게 디버깅할 수 있도록 이미지 만들기](../../../framework/debug-trace-profile/making-an-image-easier-to-debug.md)를 참조하세요.  
  
|Visual Studio 통합된 개발 환경에서 디버그-설정 하려면|  
|---|  
|1.  **솔루션 탐색기**에서 프로젝트를 선택한 상태에서 **프로젝트** 메뉴에서 **속성**을 클릭합니다. <br />2.  **컴파일** 탭을 클릭합니다.<br />3.  **고급 컴파일 옵션**을 클릭합니다.<br />4.  값을 수정 된 **디버그 정보 생성** 상자입니다.|  
  
## <a name="example"></a>예제  
 출력 파일에 디버깅 정보를 저장 하는 다음 예제에서는 `App.exe`합니다.  
  
```  
vbc -debug -out:app.exe test.vb  
```  
  
## <a name="see-also"></a>참고 항목  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
 [/bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md)  
 [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
