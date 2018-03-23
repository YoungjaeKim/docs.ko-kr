---
title: -win32icon
ms.date: 03/13/2018
ms.prod: .net
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- win32icon compiler option [Visual Basic]
- -win32icon compiler option [Visual Basic]
- /win32icon compiler option [Visual Basic]
ms.assetid: aecaab01-9353-46c5-941c-6edabd4eff92
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 95b2e2b4542f2e396a136f6a3d9baeb3e0c037a3
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="-win32icon"></a>-win32icon
출력 파일에.ico 파일을 삽입합니다. 이.ico 파일에 출력 파일을 나타내는 **파일 탐색기**합니다.  
  
## <a name="syntax"></a>구문  
  
```  
-win32icon:filename  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`filename`|출력 파일에 추가 하려면.ico 파일입니다. 파일 이름을 따옴표로 묶습니다 ("")에 공백이 있는 경우.|  
  
## <a name="remarks"></a>설명  
 Microsoft Windows 리소스 컴파일러 (RC)와.ico 파일을 만들 수 있습니다. 리소스 컴파일러는 Visual c + + 프로그램; 컴파일할 때 실행 .ico 파일.rc 파일에서 만들어집니다. `-win32icon` 및 `-win32resource` 옵션은 함께 사용할 수 없습니다.  
  
 참조 [-linkresource (Visual Basic)](../../../visual-basic/reference/command-line-compiler/linkresource.md) 참조에는 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 리소스 파일 또는 [-리소스 (Visual Basic)](../../../visual-basic/reference/command-line-compiler/resource.md) 연결할는 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 리소스 파일입니다. 참조 [-win32resource](../../../visual-basic/reference/command-line-compiler/win32resource.md) .res 파일을 가져옵니다.  
  
|Visual Studio IDE에서 win32icon-설정 하려면|  
|---|  
|1.  **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 **속성**을 클릭합니다. <br />2.  **응용 프로그램** 탭을 클릭합니다.<br />3.  값을 수정 된 **아이콘** 상자입니다.|  
  
## <a name="example"></a>예제  
 다음 코드에서는 `In.vb` .ico 파일을 연결 하 고 `Rf.ico`합니다.  
  
```console
vbc -win32icon:rf.ico in.vb  
```  
  
## <a name="see-also"></a>참고 항목  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
 [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
