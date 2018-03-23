---
title: -vbruntime
ms.date: 03/13/2018
ms.prod: .net
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbruntime
- -vbruntime
helpviewer_keywords:
- vbruntime compiler option [Visual Basic]
- -vbruntime compiler option [Visual Basic]
- /vbruntime compiler option [Visual Basic]
ms.assetid: 1aa0239e-511a-4c29-957d-fd72877b350a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e6c6529fabddc75fb6ac751e0314011f05db7869
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="-vbruntime"></a>-vbruntime
컴파일러에서 Visual Basic 런타임 라이브러리에 대한 참조 없이 컴파일하거나 특정 런타임 라이브러리를 참조하여 컴파일하도록 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
-vbruntime:{ - | + | * | path }  
```  
  
## <a name="arguments"></a>인수  
 \-  
 Visual Basic 런타임 라이브러리에 대 한 참조 없이 컴파일하십시오.  
  
 \+  
 기본 Visual Basic 런타임 라이브러리에 대 한 참조를 사용 하 여 컴파일하십시오.  
  
 \*  
 Visual Basic 런타임 라이브러리에 대 한 참조 없이 컴파일하고 어셈블리를 Visual Basic 런타임 라이브러리에서 core 기능을 포함 합니다.  
  
 `path`  
 지정된 된 라이브러리 (DLL)에 대 한 참조를 사용 하 여 컴파일하십시오.  
  
## <a name="remarks"></a>설명  
 `-vbruntime` 컴파일러 옵션을 사용 하면 컴파일러는 Visual Basic 런타임 라이브러리에 대 한 참조 없이 컴파일하도록 할지 지정할 수 있습니다. Visual Basic 런타임 라이브러리에 대 한 참조 없이 컴파일하는 경우 Visual Basic 런타임 도우미에 대 한 호출을 생성 하는 코드 또는 언어 구문에 대해 오류 또는 경고가 기록 됩니다. (A *Visual Basic 런타임 도우미* 는 특정 언어 의미 체계를 실행 하는 런타임 시 호출 되는 Microsoft.VisualBasic.dll에 정의 된 함수입니다.)  
  
 `-vbruntime+` 옵션 생성 되지 않았을 때 발생 하는 동작과 같습니다 `-vbruntime` 스위치를 지정 합니다. 사용할 수는 `-vbruntime+` 이전 재정의 하는 옵션 `-vbruntime` 스위치입니다.  
  
 대부분의 개체는 `My` 형식을 사용할 수 없는 사용 하는 경우는 `-vbruntime-` 또는 `-vbruntime:path` 옵션입니다.  
  
## <a name="embedding-visual-basic-runtime-core-functionality"></a>Visual Basic 런타임 핵심 기능을 포함합니다.  
 `-vbruntime*` 옵션을 사용 하면 런타임 라이브러리에 대 한 참조 없이 컴파일할 수 있습니다. 대신, Visual Basic 런타임 라이브러리의 핵심 기능을 사용자 어셈블리에 포함 됩니다. 응용 프로그램이 Visual Basic 런타임에 포함 하지 않는 플랫폼에서 실행 하는 경우이 옵션을 사용할 수 있습니다.  
  
 다음 런타임 멤버가 포함 됩니다.  
  
-   <xref:Microsoft.VisualBasic.CompilerServices.Conversions> 클래스  
  
-   <xref:Microsoft.VisualBasic.Strings.AscW%28System.Char%29> 메서드  
  
-   <xref:Microsoft.VisualBasic.Strings.AscW%28System.String%29> 메서드  
  
-   <xref:Microsoft.VisualBasic.Strings.ChrW%28System.Int32%29> 메서드  
  
-   <xref:Microsoft.VisualBasic.Constants.vbBack> 상수  
  
-   <xref:Microsoft.VisualBasic.Constants.vbCr> 상수  
  
-   <xref:Microsoft.VisualBasic.Constants.vbCrLf> 상수  
  
-   <xref:Microsoft.VisualBasic.Constants.vbFormFeed> 상수  
  
-   <xref:Microsoft.VisualBasic.Constants.vbLf> 상수  
  
-   <xref:Microsoft.VisualBasic.Constants.vbNewLine> 상수  
  
-   <xref:Microsoft.VisualBasic.Constants.vbNullChar> 상수  
  
-   <xref:Microsoft.VisualBasic.Constants.vbNullString> 상수  
  
-   <xref:Microsoft.VisualBasic.Constants.vbTab> 상수  
  
-   <xref:Microsoft.VisualBasic.Constants.vbVerticalTab> 상수  
  
-   일부 개체는 `My` 유형  
  
 사용 하 여 컴파일하는 경우는 `-vbruntime*` 옵션과 코드 핵심 기능이 포함 되어 있지 않으면 Visual Basic 런타임 라이브러리에서 멤버 참조, 컴파일러는 멤버를 사용할 수 있는지를 나타내는 오류를 반환 합니다.  
  
## <a name="referencing-a-specified-library"></a>지정된 된 라이브러리 참조  
 사용할 수는 `path` 인수를 기본 Visual Basic 런타임 라이브러리 대신 사용자 지정 런타임 라이브러리에 대 한 참조를 사용 하 여 컴파일합니다.  
  
 경우에 대 한 값은 `path` 인수는 DLL에는 정규화 된 경로, 컴파일러에서 런타임 라이브러리와 해당 파일을 사용 합니다. 경우에 대 한 값은 `path` 인수가 DLL에는 정규화 된 경로, Visual Basic 컴파일러 현재 폴더에서 식별 된 DLL에 대 한 가장 먼저 검색 합니다. 사용 하 여 지정 된 경로에서 검색 한 다음는 [-sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md) 컴파일러 옵션입니다. 경우는 `-sdkpath` 컴파일러 옵션이 사용 되지 않으면, 컴파일러는.NET Framework 폴더에 식별 된 DLL에 대 한 검색 (`%systemroot%\Microsoft.NET\Framework\versionNumber`).  
  
## <a name="example"></a>예제  
 사용 하는 방법을 보여 주는 다음 예제는 `-vbruntime` 옵션을 사용자 지정 라이브러리에 대 한 참조를 사용 하 여 컴파일합니다.  
  
```console
vbc -vbruntime:C:\VBLibraries\CustomVBLibrary.dll  
```  
  
## <a name="see-also"></a>참고 항목  
 [Visual Basic 코어 – Visual Studio 2010 s p 1의 새로운 컴파일 모드](http://blogs.msdn.com/b/vbteam/archive/2011/01/10/vb-core-new-compilation-mode-in-visual-studio-2010-sp1.aspx)  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
 [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)  
 [-sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md)
