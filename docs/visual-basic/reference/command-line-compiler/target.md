---
title: -대상 (Visual Basic)
ms.date: 03/13/2018
ms.prod: .net
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- target compiler options [Visual Basic]
- -target compiler options [Visual Basic]
- /target compiler options [Visual Basic]
ms.assetid: e0954147-548b-461f-9c4b-a8f88845616c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8596cb7d43b2c54b46dedc40488ed1b4e2c31b69
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="-target-visual-basic"></a>-대상 (Visual Basic)
컴파일러 출력의 형식을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
-target:{exe | library | module | winexe | appcontainerexe | winmdobj}  
```  
  
## <a name="remarks"></a>설명  
 다음 표에서 요약의 효과 `-target` 옵션입니다.  
  
|**옵션**|**동작**|  
|----------------|------------------|  
|`-target:exe`|컴파일러가 실행 콘솔 응용 프로그램을 만들도록 합니다.<br /><br /> 이것이 하지 않으면 기본 옵션 `-target` 옵션을 지정 합니다. 실행 파일 확장명이.exe 인 만들어집니다.<br /><br /> 지정 하지 않으면는 `/out` 옵션을 출력 파일 이름 포함 하는 입력된 파일의 이름으로 사용 된 `Sub Main` 프로시저 합니다.<br /><br /> 하나의 `Sub Main` 프로시저는.exe로 컴파일되는 소스 코드 파일에 필요 합니다. 사용 하 여는 `-main` 컴파일러 옵션을 포함 하는 클래스가 지정 된 `Sub Main` 프로시저입니다.|  
|`-target:library`|컴파일러가 동적 연결 라이브러리 (DLL)를 만듭니다.<br /><br /> 동적 연결 라이브러리 파일 확장명.dll 만들어집니다.<br /><br /> 지정 하지 않으면는 `-out` 출력 파일 이름 옵션을 첫 번째 입력된 파일의 이름으로 사용 합니다.<br /><br /> DLL을 빌드할 때는 `Sub Main` 절차가 필요 하지 않습니다.|  
|`-target:module`|컴파일러가 어셈블리에 추가할 수 있는 모듈을 만듭니다.<br /><br /> .Netmodule 확장명이 출력 파일이 생성 됩니다.<br /><br /> .NET 공용 언어 런타임 어셈블리를 하지 않은 파일을 로드할 수 없습니다. 그러나 통합할 수 있습니다 이러한 파일 어셈블리의 어셈블리 매니페스트를 사용 하 여 `-reference`합니다.<br /><br /> 두 모듈을 사용 하 여 어셈블리 매니페스트에 통합 해야 다른 모듈의 내부 형식을 참조 하는 한 모듈의 코드가 `-reference`합니다.<br /><br /> [-addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md) 옵션 모듈에서 메타 데이터를 가져옵니다.|  
|`-target:winexe`|컴파일러가 실행 가능한 Windows 기반 응용 프로그램을 만들려고 합니다.<br /><br /> 실행 파일 확장명이.exe 인 만들어집니다. Windows 기반 응용 프로그램은 두 가지 중 하나에서 사용자 인터페이스를 제공 하는 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 클래스 라이브러리 또는 Win32 Api와 합니다.<br /><br /> 지정 하지 않으면는 `-out` 옵션을 출력 파일 이름 포함 하는 입력된 파일의 이름으로 사용 된 `Sub Main` 프로시저 합니다.<br /><br /> 하나의 `Sub Main` 프로시저는.exe로 컴파일되는 소스 코드 파일에 필요 합니다. 코드에 둘 이상의 클래스에 있는 경우에는 `Sub Main` 프로시저를 사용 하 여는 `-main` 컴파일러 옵션을 포함 하는 클래스가 지정는 `Sub Main` 프로시저|  
|`-target:appcontainerexe`|컴파일러가 실행 가능한 Windows 기반 응용 프로그램에서 응용 프로그램 컨테이너에서 실행 해야 하는 만들려고 합니다. 이 설정은 사용자에 사용할 [!INCLUDE[win8_appname_long](~/includes/win8-appname-long-md.md)] 응용 프로그램입니다.<br /><br /> **appcontainerexe** 설정은 약간의 특성 필드에는 [이식 가능한 실행](http://go.microsoft.com/fwlink/p/?LinkId=236960) 파일입니다. 이 비트는 앱 같은 앱 컨테이너에서 실행 해야 함을 나타냅니다. 오류가 발생 하는 경우이 비트가 설정 되 면는 `CreateProcess` 메서드는 응용 프로그램 컨테이너 외부의 응용 프로그램을 시작 하려고 합니다. 이 비트가 설정 외에도 **-/target: appcontainerexe** 같습니다 **-/target: winexe**합니다.<br /><br /> 실행 파일 확장명이.exe 인 만들어집니다.<br /><br /> 사용 하 여 별도로 지정 하지 않으면는 `-out` 출력 파일 이름 포함 하는 입력된 파일의 이름으로 사용 옵션을는 `Sub Main` 프로시저입니다.<br /><br /> 하나의 `Sub Main` 프로시저는.exe로 컴파일되는 소스 코드 파일에 필요 합니다. 코드에 있는 둘 이상의 클래스를 포함 하는 경우는 `Sub Main` 프로시저를 사용 하 여는 `-main` 컴파일러 옵션을 포함 하는 클래스가 지정 된 `Sub Main` 프로시저|  
|`-target:winmdobj`|컴파일러에서 Windows 런타임 이진 (.winmd) 파일로 변환할 수 있는 중간 파일을 만들려고 합니다. .Winmd 파일은 관리 되는 언어 프로그램 뿐만 아니라 JavaScript 및 c + + 프로그램에서 사용할 수 있습니다.<br /><br /> .Winmdobj 확장명이 중간 파일이 생성 됩니다.<br /><br /> 사용 하 여 별도로 지정 하지 않으면는 `-out` 출력 파일 이름 옵션을 첫 번째 입력된 파일의 이름으로 사용 합니다. A `Sub Main` 프로시저는 필요 하지 않습니다.<br /><br /> .Winmdobj 파일에 대 한 입력으로 사용할 수 있도록 설계 되 고 <xref:Microsoft.Build.Tasks.WinMDExp> 내보내기 도구를 Windows 메타 데이터 (WinMD) 파일입니다. WinMD 파일의.winmd 확장명 및 해당 JavaScript, c + +, 및 Windows 런타임 사용 원본 라이브러리 및 WinMD 정의에서 코드를 포함 합니다.|  
  
 지정 하지 않으면 `-target:module`, `-target` 하면는 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 어셈블리 매니페스트를 출력 파일에 추가 합니다.  
  
 Vbc.exe의 각 인스턴스를 생성, 많아야 한 출력 파일입니다. 와 같은 컴파일러 옵션을 지정 하는 경우 `-out` 또는 `-target` 둘 이상의 시간, 마지막 트랜잭션이 처리 효과에 배치 됩니다. 컴파일에서 모든 파일에 대 한 정보를 매니페스트에 추가 됩니다. 모든 출력 파일을 사용 하 여 만든 것을 제외한 파일 `-target:module` 매니페스트에 어셈블리 메타 데이터를 포함 합니다. 사용 하 여 [Ildasm.exe (IL 디스어셈블러)](https://msdn.microsoft.com/library/f7dy01k1) 출력 파일에 메타 데이터를 볼 수 있습니다.  
  
 `-target`의 약식은 `-t`입니다.  
  
### <a name="to-set--target-in-the-visual-studio-ide"></a>Visual Studio IDE에서 대상-설정 하려면  
  
1.  **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 **속성**을 클릭합니다.   
  
2.  **응용 프로그램** 탭을 클릭합니다.  
  
3.  값을 수정 된 **응용 프로그램 종류** 상자입니다.  
  
## <a name="example"></a>예제  
 다음 코드에서는 `in.vb`만들기, `in.dll`:  
  
```console
vbc -target:library in.vb  
```  
  
## <a name="see-also"></a>참고 항목  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
 [-main](../../../visual-basic/reference/command-line-compiler/main.md)  
 [-out (Visual Basic)](../../../visual-basic/reference/command-line-compiler/out.md)  
 [-참조 (Visual Basic)](../../../visual-basic/reference/command-line-compiler/reference.md)  
 [-addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md)  
 [-moduleassemblyname](../../../visual-basic/reference/command-line-compiler/moduleassemblyname.md)  
 [어셈블리 및 전역 어셈블리 캐시](../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)  
 [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
