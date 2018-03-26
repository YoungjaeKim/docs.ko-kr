---
title: 컴파일러 옵션(F#)
description: 'F # 컴파일러 명령줄 옵션을 사용 하 여 F # 응용 프로그램 및 라이브러리의 컴파일을 제어 합니다.'
keywords: visual f#, f#, 함수형 프로그래밍
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: c797cf0b-5953-4053-8626-0558e9eaf10f
ms.openlocfilehash: 23731832141bc2f74a04c5f4027fc210b5589537
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="compiler-options"></a>컴파일러 옵션

이 항목에서는 F # 컴파일러에 대 한 컴파일러 명령줄 옵션 설명 fsc.exe 합니다. 컴파일 환경에서 프로젝트 속성을 설정 하 여 제어할 수도 있습니다.


## <a name="compiler-options-listed-alphabetically"></a>컴파일러 옵션 사전순 목록
다음 표에서 컴파일러 옵션 사전순 목록를 보여 줍니다. F # 컴파일러 옵션 중 일부는 C# 컴파일러 옵션 비슷합니다. 해당 되는 경우 C# 컴파일러 옵션 항목의 링크가 제공 됩니다.



|컴파일러 옵션|설명|
|---------------|-----------|
|**-a****&lt;output-filename&gt;**|라이브러리를 생성 하 고 해당 파일 이름을 지정 합니다. 이 옵션의 약식 형태는 **-대상: 라이브러리 * * *&lt;filename&gt;**합니다.|
|**--baseaddress:&lt;string&gt;**|빌드할 라이브러리의 기본 주소를 지정 합니다.<br /><br />이 컴파일러 옵션은 이름이 동일한 C# 컴파일러 옵션에 해당 합니다. 자세한 내용은 참조 [ &#47;baseaddress &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/2fdbz5xd.aspx)합니다.|
|**--codepage:&lt;int&gt;**|소스 파일을 읽는 데 사용 되는 코드 페이지를 지정 합니다.<br /><br />이 컴파일러 옵션은 이름이 동일한 C# 컴파일러 옵션에 해당 합니다. 자세한 내용은 참조 [ &#47;코드 페이지 &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/w0kyekyh.aspx)합니다.|
|**--consolecolors**|오류 및 경고 사용 콘솔에 색으로 구분 된 텍스트를 지정 합니다.|
|**--crossoptimize**[**+**&#124;**-**]|크로스 모듈을 최적화를 사용 하지 않도록 설정 하거나 사용 합니다.|
|**--delaysign**[**+**&#124;**-**]|서명을 연기 강력한 이름 키의 공개 부분만 사용 하 여 어셈블리입니다.<br /><br />이 컴파일러 옵션은 이름이 동일한 C# 컴파일러 옵션에 해당 합니다. 자세한 내용은 참조 [ &#47;delaysign &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/ta1sxwy8.aspx)합니다.|
|**--checked**[**+**&#124;**-**]|오버플로 검사의 생성을 비활성화 하거나 사용 합니다.<br /><br />이 컴파일러 옵션은 이름이 동일한 C# 컴파일러 옵션에 해당 합니다. 자세한 내용은 참조 [ &#47;체크 &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/h25wtyxf.aspx)합니다.|
|**--debug**[**+**&#124;**-**]<br /><br />**-g**[**+**&#124;**-**]<br /><br />**--debug**:[**full**&#124;**pdbonly**]<br /><br />**-g:** [**full**&#124;**pdbonly**]|또는 디버그 정보 생성을 비활성화 하거나 생성 하는 디버그 정보의 유형을 지정 합니다. 기본값은 full, 실행 중인 프로그램에 연결할 수 있습니다. 선택 **pdbonly** pdb (프로그램 데이터베이스) 파일에 저장 하는 제한 된 디버깅 정보를 얻을 수 있습니다.<br /><br />이름이 같은 C# 컴파일러 옵션에 해당 합니다. 자세한 내용은 다음 항목을 참조하세요.<br /><br />[&#47;디버그 &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/8cw0bt21.aspx)합니다.|
|**--define:&lt;string&gt;**<br /><br />**-d:&lt;string&gt;**|조건부 컴파일에 사용할 기호를 정의합니다.|
|**--deterministic**[**+**&#124;**-**]|결정적 어셈블리 (모듈 버전 GUID 및 타임 스탬프 포함)를 생성 합니다.  이 와일드 카드 버전 번호를 함께 사용할 수 없습니다 및 포함 된 및 노트북 디버깅 형식만 지원|
|**--doc:&lt;xmldoc-filename&gt;**|지정 된 파일에 XML 문서 주석 생성 하도록 컴파일러에 지시 합니다. 자세한 내용은 참조 [XML 문서](xml-documentation.md)합니다.<br /><br />이 컴파일러 옵션은 이름이 동일한 C# 컴파일러 옵션에 해당 합니다. 자세한 내용은 참조 [ &#47;doc &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/3260k4x7.aspx)합니다.|
|**--fullpaths**|정규화 된 경로 생성 하도록 컴파일러에 지시 합니다.<br /><br />이 컴파일러 옵션은 이름이 동일한 C# 컴파일러 옵션에 해당 합니다. 자세한 내용은 참조 [ &#47;fullpaths &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/d315xc66.aspx)합니다.|
|**--help**<br /><br />**-?**|모든 컴파일러 옵션에 대 한 간략 한 설명을 포함 하 여 사용 정보를 표시 합니다.|
|**--highentropyva**[**+**&#124;**-**]|높은 엔트로피 주소 공간 레이아웃 불규칙화 (ASLR) 강화 된 보안 기능을 사용 하지 않도록 설정 하거나 사용 합니다. 운영 체제 임의 응용 프로그램 (예: 스택 및 힙)에 대 한 인프라 로드 되는 메모리의 위치입니다. 이 옵션을 사용 하도록 설정 하면 운영 체제 64 비트 컴퓨터에서 전체 64 비트 주소 공간을 사용 하이 임의 사용할 수 있습니다.|
|**--keycontainer:&lt;string&gt;**|강력한 이름의 키 컨테이너를 지정합니다.|
|**--keyfile:&lt;filename&gt;**|생성된 된 어셈블리를 서명 하는 데 사용할 공개 키 파일의 이름을 지정 합니다.|
|**--lib:&lt;folder-name&gt;**<br /><br />**-I:&lt;folder-name&gt;**|참조 되는 어셈블리에 대 한 검색할 디렉터리를 지정 합니다.<br /><br />이 컴파일러 옵션은 이름이 동일한 C# 컴파일러 옵션에 해당 합니다. 자세한 내용은 참조 [ &#47;lib &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/s5bac5fx.aspx)합니다.|
|**--linkresource**:**&lt;resource-info&gt;**|어셈블리에 지정된 된 리소스를 연결합니다. 리소스 정보 형식이 *filename*[,*이름*[,*공용*&#124;*개인*]]<br /><br />전체 리소스 파일을 포함 하는 대신은이 옵션을 사용 하 여 단일 리소스 링크는 **-리소스** 옵션입니다.<br /><br />이 컴파일러 옵션은 이름이 동일한 C# 컴파일러 옵션에 해당 합니다. 자세한 내용은 참조 [ &#47;linkresource &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/xawyf94k.aspx)합니다.|
|**--mlcompatibility**|다른 ML 버전과의 호환을 위해 설계 된 기능을 사용할 때 표시 되는 경고를 무시 합니다.|
|**--noframework**|.NET Framework 어셈블리에 대 한 기본 참조를 해제합니다.|
|**--nointerfacedata**|F #을 포함 하는 어셈블리에는 일반적으로 추가 하는 리소스를 생략 컴파일러에 지시-특정 메타 데이터입니다.|
|**--nologo**|배너 텍스트 컴파일러를 시작할 때 표시 되지 않습니다.|
|**--nooptimizationdata**|인라인된 구문을 구현 하는 데 필요한 최적화를만 포함 하도록 컴파일러에 지시 합니다. 크로스 모듈 인라인 제한 되지만 이진 호환성을 향상 시킵니다.|
|**--nowin32manifest**|기본 Win32 매니페스트를 생략 하도록 컴파일러에 지시 합니다.|
|**--nowarn:&lt;int-list&gt;**|번호 순으로 나열 하는 특정 경고를 해제 합니다. 각 경고 번호를 쉼표로 구분 합니다. 컴파일 출력에서 모든 경고에 대 한 경고 번호를 검색할 수 있습니다.<br /><br />이 컴파일러 옵션은 이름이 동일한 C# 컴파일러 옵션에 해당 합니다. 자세한 내용은 참조 [ &#47;nowarn &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/7f28x9z3.aspx)합니다.|
|**--optimize**[**+**&#124;**-**]**[&lt;string-list&gt;]**<br /><br />**-O[+&#124;-] [&lt;string-list&gt;]**|최적화를 사용 하지 않도록 설정 하거나 사용 합니다. 일부 최적화 옵션을 사용 하지 않도록 설정 또는 나열 하 여 선택적으로 사용할 수 있습니다. 이들은: **nojitoptimize**, **nojittracking**, **nolocaloptimize**, **nocrossoptimize**, **notailcalls**.|
|**--out:&lt;output-filename&gt;**<br /><br />**-o:&lt;output-filename&gt;**|컴파일된 어셈블리 또는 모듈의 이름을 지정합니다.<br /><br />이 컴파일러 옵션은 이름이 동일한 C# 컴파일러 옵션에 해당 합니다. 자세한 내용은 참조 [ &#47;아웃 &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/bw3t50f3.aspx)합니다.|
|**--pdb:&lt;pdb-filename&gt;**|출력 디버그 PDB (프로그램 데이터베이스) 파일의 이름을 지정 합니다. 이 옵션 적용 될 때 **-디버그** 옵션도 사용할 수 있습니다.<br /><br />이 컴파일러 옵션은 이름이 동일한 C# 컴파일러 옵션에 해당 합니다. 자세한 내용은 참조 [ &#47;pdb &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/ms228625.aspx)합니다.|
|**--platform:&lt;platform-name&gt;**|생성 된 코드에 지정된 된 플랫폼에만 실행 되도록 지정 (**x86**, **Itanium**, 또는 **x64**), 또는 경우에 플랫폼 이름을 **anycpu**선택 하 든, 생성 된 코드는 모든 플랫폼에서 실행할 수를 지정 합니다.<br /><br />이 컴파일러 옵션은 이름이 동일한 C# 컴파일러 옵션에 해당 합니다. 자세한 내용은 참조 [ &#47;플랫폼 &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/zekwfyz4.aspx)합니다.|
|**--preferreduilang:&lt;lang&gt;**| 기본 출력 언어 문화권 이름 (예: ES-ES, JA-JP)를 지정합니다. |
|**--quotations-debug**|F # 따옴표로 묶인 리터럴을에서 파생 된 및 정의 반영 하는 식에 대 한 추가 정보를 디버깅 내보낼 수를 지정 합니다. 디버그 정보는 F # 식 트리 노드에 대 한 사용자 지정 특성으로 추가 됩니다. 참조 [코드 인용](code-quotations.md) 및 [Expr.CustomAttributes](https://msdn.microsoft.com/library/eb89943f-5f5b-474e-b125-030ca412edb3)합니다.|
|**--reference:&lt;assembly-filename&gt;**<br /><br />**-r** &lt;**assembly-filename&gt;**|코드에서 F # 또는.NET Framework 어셈블리를 사용할 수 있게 컴파일되는 코드입니다.<br /><br />이 컴파일러 옵션은 이름이 동일한 C# 컴파일러 옵션에 해당 합니다. 자세한 내용은 참조 [ &#47;참조 &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/yabyz3h4.aspx)합니다.|
|**--resource:&lt;resource-filename&gt;**|생성된 된 어셈블리에 관리 되는 리소스 파일을 포함합니다.<br /><br />이 컴파일러 옵션은 이름이 동일한 C# 컴파일러 옵션에 해당 합니다. 자세한 내용은 참조 [ &#47;리소스 &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/c0tyye07.aspx)합니다.|
|**--sig**:&lt;**signature-filename&gt;**|생성된 된 어셈블리에 따라 서명 파일을 생성 합니다. 서명 파일에 대 한 자세한 내용은 참조 [서명](signatures.md)합니다.|
|**--simpleresolution**|MSBuild 확인이 아니라 디렉터리 기반의 모노 규칙을 사용 하 여 어셈블리 참조 해결 되도록 지정 합니다. 기본값은 mono 실행 하는 경우를 제외 하 고 MSBuild 확인을 사용 하도록 합니다.|
|**--standalone**|F # 라이브러리와 같은 추가 어셈블리에 대 한 필요 없이 자체적으로 실행 되도록 모든 해당 종속성을 포함 하는 어셈블리를 생성 하도록 지정 합니다.|
|**--staticlink:&lt;assembly-name**&gt;|지정된 된 어셈블리 및이 어셈블리에 종속 된 모든 참조 Dll을 정적으로 연결 합니다. DLL 이름이 아니라 어셈블리 이름을 사용 합니다.|
|**--subsystemversion**|생성된 된 실행 파일에서 사용할 운영 체제 하위 시스템의 버전을 지정 합니다. Windows 8.1, windows 7, Windows Vista 용 6.00 6.01에 6.02를 사용 합니다. 만이 옵션 실행 파일, Dll이 아니라에 적용 하 고 응용 프로그램이 특정 버전의 운영 체제에만 사용할 수 있는 특정 보안 기능에 종속 하는 경우에 사용 해야 합니다. 이 옵션을 사용 하는 경우 사용자가 더 낮은 버전의 운영 체제에서 응용 프로그램을 실행 하는 오류 메시지와 함께 실패 합니다.|
|**--tailcalls**[**+**&#124;**-**]|비상 IL 명령의 스택 프레임을 마무리 재귀 함수에 대 한 다시 사용할 수는 사용 하지 않도록 설정 하거나 사용 합니다. 기본적으로 이 옵션은 사용하도록 설정됩니다.|
|**-대상**: [**exe** &#124; **winexe** &#124; **라이브러리** &#124; **모듈** ]  **&lt;출력 파일 이름&gt;**|생성된 된 컴파일된 코드의 형식 및 파일 이름을 지정합니다.<ul><li>**exe** 콘솔 응용 프로그램을 의미 합니다.<br /></li><li>**winexe** 는 콘솔 응용 프로그램은 표준 입력/출력 스트림 (stdin, stdout 및 stderr) 정의 없는 한다는 점에서 다른 Windows 응용 프로그램을 의미 합니다.<br /></li><li>**라이브러리** 진입점이 없는 어셈블리입니다.<br /></li><li>**모듈** 은 나중에 사용할 수와 다른 모듈 어셈블리는.NET Framework 모듈 (.netmodule).<br /></li><ul/>이 컴파일러 옵션은 이름이 동일한 C# 컴파일러 옵션에 해당 합니다. 자세한 내용은 참조 [ &#47;대상 &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/6h25dztx.aspx)합니다.|
|**--times**|컴파일에 대 한 시간 정보를 표시 합니다.|
|**--utf8output**|U t F-8 인코딩으로 컴파일러 출력을 인쇄할 수 있습니다.|
|**--warn:&lt;warning-level&gt;**|경고 수준 (0 ~ 5)를 설정합니다. 기본값은 3입니다. 각 경고의 심각도 수준을 지정 됩니다. 수준 5는 수준 1 보다 더 적은 심각, 경고를 제공합니다.<br /><br />경고 수준 5는: (재귀 사용 하 여 런타임 시 검사) 21, 22 (**let rec** 순서와 다르게 평가), 45 (전체 추상화) 및 52 (방어 복사). 다른 모든 경고는 수준 2입니다.<br /><br />이 컴파일러 옵션은 이름이 동일한 C# 컴파일러 옵션에 해당 합니다. 자세한 내용은 참조 [ &#47;경고 &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/13b90fz7.aspx)합니다.|
|**--warnon:&lt;int-list&gt;**|기본적으로 해제 되어 수 또는 다른 명령줄 옵션에 의해 사용 하지 않도록 설정 하는 특정 경고를 사용 하도록 설정 합니다. F # 3.0에만 1182 (사용 되지 않는 변수) 경고는 기본적으로 해제 되어 있습니다.|
|**--warnaserror**[**+**&#124;**-**] [**&lt;int-list&gt;**]|경고를 오류로 보고 하는 옵션을 사용 하지 않도록 설정 하거나 사용 합니다. 특정 경고 번호 비활성화 되거나 활성화 될를 제공할 수 있습니다. 명령줄의 뒷부분에 나오는 옵션은 명령줄의 앞부분에 나오는 옵션을 무시 합니다. 예를 들어 오류로 보고 싶지 않은 경고를 지정 하려면 지정 **-warnaserror +-warnaserror-:&lt;int 목록&gt;**합니다.<br /><br />이 컴파일러 옵션은 이름이 동일한 C# 컴파일러 옵션에 해당 합니다. 자세한 내용은 참조 [ &#47;warnaserror &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/406xhdz3.aspx)합니다.|
|**--win32manifest:manifest-filename**|컴파일에 Win32 매니페스트 파일을 추가합니다. 이 컴파일러 옵션은 이름이 동일한 C# 컴파일러 옵션에 해당 합니다. 자세한 내용은 참조 [ &#47;win32manifest &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/bb545961.aspx)합니다.|
|**--win32res:resource-filename**|컴파일에 Win32 리소스 파일을 추가합니다.<br /><br />이 컴파일러 옵션은 이름이 동일한 C# 컴파일러 옵션에 해당 합니다. 자세한 내용은 참조 [ &#47;win32res (&#40;& #35); 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/8f2f5x2e.aspx)합니다.|

## <a name="related-topics"></a>관련 항목


|제목|설명|
|-----|-----------|
|[F# Interactive 옵션](fsharp-interactive-options.md)|F # 인터프리터에 의해 지원 되는 명령줄 옵션 설명 fsi.exe 합니다.|
|[프로젝트 속성 참조](/visualstudio/ide/reference/project-properties-reference)|UI 빌드 옵션을 제공 하는 프로젝트 속성 페이지를 포함 하 여 프로젝트에 대해 설명 합니다.|
