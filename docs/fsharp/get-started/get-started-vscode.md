---
title: "Visual Studio Code에서 F #으로 시작."
description: "Visual Studio Code 및 Ionide 플러그 인 suite F #을 사용 하는 방법에 알아봅니다."
keywords: "visual f #, f #, 함수형 프로그래밍,.NET, Visual Studio Code vscode Ionide"
author: cartermp
ms.author: phcart
ms.date: 02/28/2018
ms.topic: article
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: 49775139-082e-442f-b5a2-dd402399b5d2
ms.openlocfilehash: c452e791b27bc3f32e137a515011d953005344c6
ms.sourcegitcommit: 83dd5ec003e788ccb3e33f3412a7af39ae347646
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="get-started-with-f-in-visual-studio-code"></a>Visual Studio Code에서 F #으로 시작.

작성할 수 있습니다 F # [Visual Studio Code](https://code.visualstudio.com) 와 [Ionide 플러그 인](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-fsharp)는 뛰어난 플랫폼 간 사용할 수 있는 경량 IDE (Integrade 개발 Enivronment) 경험을 얻을 수 IntelliSense 및 기본 코드 리팩터링 합니다.  방문 [Ionide.io](http://ionide.io) 플러그 인 집합에 대 한 자세한 내용을 보려면 합니다.

## <a name="prerequisites"></a>전제 조건

있어야 [git 설치](https://git-scm.com/download) 및 사용할 수 있도록 경로에 Ionide 프로젝트 템플릿을 사용 합니다.  입력 하 여 올바르게 설치 되었는지 확인할 수 `git --version` 고 키를 눌러 명령 프롬프트에서 **Enter**합니다.

### <a name="macostabmacos"></a>[macOS](#tab/macos)

사용 하 여 Ionide [모노](http://www.mono-project.com)합니다.  Homebrew를 통해 모노 macOS에 설치 하는 가장 쉬운 방법은 됩니다.  단순히 터미널에 다음을 입력 합니다.

```
brew install mono
```

또한 설치 해야는 [.NET Core SDK](https://www.microsoft.com/net/download)합니다.

### <a name="linuxtablinux"></a>[Linux](#tab/linux)

Linux에서 Ionide 또한 사용 하 여 [모노](https://www.mono-project.com)합니다. Debian 또는 Ubuntu 인 경우 다음을 사용할 수 있습니다.

```
sudo apt-get update
sudo apt-get install mono-complete fsharp
```

또한 설치 해야는 [.NET Core SDK](https://www.microsoft.com/net/download)합니다.

### <a name="windowstabwindows"></a>[Windows](#tab/windows)

Windows를 사용 하는 경우 해야 [F #를 지 원하는 Visual Studio 설치](get-started-visual-studio.md#installing-f)합니다. 작성, 컴파일 및 F # 코드를 실행 하는 데 필요한 모든 구성 요소를 설치 합니다.

또한 설치 해야는 [.NET Core SDK](https://www.microsoft.com/net/download/)합니다.

---

## <a name="installing-visual-studio-code-and-the-ionide-plugin"></a>Visual Studio Code 및 Ionide 플러그 인 설치

Visual Studio Code에서 설치할 수는 [code.visualstudio.com](https://code.visualstudio.com) 웹 사이트입니다. 그런 다음 두 가지 방법으로 Ionide 플러그 인을 찾을 수 있습니다.

1. 명령 팔레트 (Ctrl + Shift + P windows에서는 ⌘ + macOS, Ctrl + Shift + P linux에서 Shift + P)를 사용 하 하 고 다음을 입력.

    ```
    >ext install Ionide
    ```

2. 확장명 아이콘 및 "Ionide"에 대 한 검색을 클릭 합니다.

    ![](media/getting-started-vscode/vscode-ext.png)

Visual Studio 코드에서 지원 되는 F #에 필요한 유일한 플러그 인 [Ionide fsharp](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-fsharp)합니다. 그러나 설치할 수도 있습니다 [Ionide 모조](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-FAKE) 을 받을 [가짜](https://fsharp.github.io/FAKE/) 지원 및 [Ionide Paket](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-Paket) 가져오려는 [Paket](https://fsprojects.github.io/Paket/) 지원 합니다. 가짜 및 Paket는 프로젝트를 빌드하고 각각 종속성을 관리 하기 위한 추가 F # 커뮤니티 도구입니다.

## <a name="creating-your-first-project-with-ionide"></a>Ionide를 사용 하 여 첫 번째 프로젝트 만들기

새 F # 프로젝트를 만들려면 (수 이름을 바꾸는) 인 새 폴더에 Visual Studio Code를 엽니다.

![](media/getting-started-vscode/vscode-open-dir.png)

그런 다음 명령 팔레트 (Ctrl + Shift + P windows에서는 ⌘ + macOS, Ctrl + Shift + P linux에서 Shift + P)를 열고 다음을 입력 합니다.

```
>f#: New Project
```

연결 된 값이 고 [FORGE](https://github.com/fsharp-editing/Forge) 프로젝트.  다음과 같이 표시되어야 합니다.

![](media/getting-started-vscode/vscode-new-proj.png)

> [!NOTE]
위의 표시 되지 않으면 명령 팔레트에서 다음 명령을 실행 하 여 서식 파일을 새로 고쳐 보세요: `>F#: Refresh Project Templates`합니다.

F #:: "새 프로젝트"를 클릭 하 여 선택 **Enter**는이 단계로 이동 합니다.

![](media/getting-started-vscode/vscode-proj-type.png)

이렇게 하면 특정 유형의 프로젝트에 대 한 템플릿을 선택 됩니다.  없는 다음와 같은 몇 가지 옵션이 여기에서 [FsLab](https://fslab.org) 데이터 과학을 위한 서식 파일 또는 [Suave](https://suave.io) 웹 프로그래밍을 위한 서식 파일입니다.  이 문서에서는 `classlib` 템플릿을 하므로 하는 강조 표시 하 고 적중 **Enter**합니다.  다음 단계는 다음과 같은 도달 하 게 됩니다.

![](media/getting-started-vscode/vscode-new-dir.png)

이렇게 하면 원하는 경우 다른 디렉터리에 있는 프로젝트를 만들 수 있습니다.  비워 둡니다 지금은.  프로젝트는 현재 디렉터리에 만들어집니다.  누른 **Enter**, 다음 단계에 도달 합니다.

![](media/getting-started-vscode/vscode-proj-name.png)

이렇게 하면 프로젝트 이름을 지정 합니다.  사용 하 여 F # [파스칼식 대 / 소문자로](http://c2.com/cgi/wiki?PascalCase) 프로젝트 이름에 대 한 합니다.  이 문서에서는 `ClassLibraryDemo` 이름으로 합니다.  프로젝트에 사용할 이름을 입력 하 여, 적중 **Enter**합니다.

이전 단계 단계를 수행 하는 경우 Visual Studio 코드 작업 영역 왼쪽에을 다음과 같은 받습니다.

![](media/getting-started-vscode/vscode-new-proj-explorer.png)

이 서식 파일에서는 몇 가지 유용한 있습니다 오류가 생성 됩니다.

1. F # 프로젝트 자체를 아래에서 `ClassLibraryDemo` 폴더입니다.
2. 통해 패키지를 추가 하기 위한 올바른 디렉터리 구조 [ `Paket` ](https://fsprojects.github.io/Paket/)합니다.
3. 플랫폼 간 빌드 스크립트와 [ `FAKE` ](https://fsharp.github.io/FAKE/)합니다.
4. `paket.exe` 있습니다에 대 한 종속성을 해결 하 고 패키지를 가져올 수 있는 실행 파일입니다.
5. A `.gitignore` Git 기반 소스 제어에이 프로젝트를 추가 하려는 경우 파일입니다.

## <a name="writing-some-code"></a>일부 코드 작성

열기는 *ClassLibraryDemo* 폴더입니다.  다음 파일이 표시 되어야 합니다.

1. `ClassLibraryDemo.fs`를 정의 하는 클래스와 F # 구현 파일입니다.
2. `CassLibraryDemo.fsproj`를이 프로젝트를 빌드하는 데는 F # 프로젝트 파일입니다.
3. `Script.fsx`는 F # 스크립트 파일이 소스 파일을 로드 합니다.
4. `paket.references`Paket 파일을 프로젝트 종속성을 지정 합니다.

열기 `Script.fsx`, 그 후에 다음 코드를 추가 합니다.

[!code-fsharp[ToPigLatin](../../../samples/snippets/fsharp/getting-started/to-pig-latin.fsx)]

이 함수는 형태의 단어 변환 [Pig 라틴](https://en.wikipedia.org/wiki/Pig_Latin)합니다.  다음 단계에서는 F # 대화형 (FSI)를 사용 하 여 평가 하는 것입니다.

전체 함수 (11 줄 이어야 함)를 강조 표시 합니다.  강조 표시 되 면 보유는 **Alt** 키 및 적중 **Enter**합니다.  아래 팝업 창을 보면 하 고 다음과 같이 표시 됩니다.

![](media/getting-started-vscode/vscode-fsi.png)

이 세 가지 했습니다.

1. FSI 프로세스를 시작 합니다.
2. FSI 프로세스를 통해 강조 표시 된 코드를 전송.
3. FSI 프로세스를 통해 전송 된 코드를 평가 합니다.

통해 보낸 되었으므로 [함수](../language-reference/functions/index.md), 이제 FSI 해당 함수를 호출할 수 있습니다!  대화형 창에서 다음을 입력 합니다.

```fsharp
toPigLatin "banana";;
```

다음과 같은 결과가 나타납니다.

```fsharp
val it : string = "ananabay"
```

이제 첫 번째 문자로 함께 보겠습니다. 다음을 입력하세요.

```fsharp
toPigLatin "apple";;
```

다음과 같은 결과가 나타납니다.

```fsharp
val it : string = "appleyay"
```

예상 대로 작동 하는 함수 표시 됩니다.  축 하 합니다, 방금 Visual Studio 코드에서 첫 번째 F # 함수를 작성 하 고 FSI를 사용 하 여 확인!

>[!NOTE]
FSI에서 줄 종결 되는지 알 수 있습니다, 처럼 `;;`합니다.  즉, FSI를 사용 하면 여러 줄을 입력할 수 있습니다.  `;;` 끝 FSI 코드가 완료 되었을 때를 알 수 있습니다.

## <a name="explaining-the-code"></a>코드를 설명합니다.

코드 실제로 수행 하는 방법에 대 한 잘 모르는 경우 다음 단계별 마법사은입니다.

볼 수 있듯이 `toPigLatin` 단어 입력으로 사용 되 고 단어의 Pig 라틴 문자 표현으로 변환 하는 함수가 됩니다.  이 규칙은 다음과 같습니다.

단어의 첫 번째 문자는 함께 시작 되 면 ""이 얼 간 단어의 끝에 추가 합니다.  함께 시작 되지 않는다면 해당 첫 번째 문자는 단어의 끝으로 이동 합니다. 및 "집니다"를 추가 합니다.

FSI에서 다음을 알 수 있습니다.

```
val toPigLatin : word:string -> string
```

이 없다는 `toPigLatin` 에서 사용 하는 함수는 `string` 입력으로 (호출 `word`)를 반환 하는 값 및 `string`합니다.  로 알려져는 [함수의 형식 서명이](https://fsharpforfunandprofit.com/posts/function-signatures/), F # 코드를 이해 하는 F #의 기본적인 부분입니다.  Visual Studio 코드의 함수 위로 가져가면에 다음이 표시도 됩니다.

함수 본문에서 두 가지 부분을 확인할 수 있습니다.

1. 호출 하는 내부 함수 `isVowel`, 하는 경우 지정 된 문자를 결정 합니다 (`c`)를 통해 제공 된 패턴 중 하 나와 일치 하는 경우를 확인 하 여이 모음인 [패턴 일치](../language-reference/pattern-matching.md):

   [!code-fsharp[ToPigLatin](../../../samples/snippets/fsharp/getting-started/to-pig-latin.fsx#L2-L6)]

2. [ `if..then..else` ](../language-reference/conditional-expressions-if-then-else.md) 인지에 따라 첫 번째 문자에 모음이 고 입력된 된 문자를 벗어나는 반환 값을 생성 하는 검사 첫 번째 문자 식에 모음이 되었거나:

   [!code-fsharp[ToPigLatin](../../../samples/snippets/fsharp/getting-started/to-pig-latin.fsx#L8-L11)]

흐름 `toPigLatin` 있으므로:

입력된 단어의 첫 번째 문자에 모음이 있는지 확인 하십시오.  인 경우 단어의 끝에 ""이 얼 간을 연결입니다.  그렇지 않으면 첫 번째 문자가 단어의 끝으로 이동 및 "집니다"를 추가 합니다.

이 대 한 확인 해야 할 사항이 하나는:는 많은 다른 언어와 달리 하셨습니까 함수에서 반환할 수 없는 명시적 명령입니다.  F #은 식 기반 이며 함수의 본문에서 반환 값 때문입니다.  때문에 `if..then..else` 은 자체는 식의 본문은 `then` 블록 또는 본문에는 `else` 블록 입력된 값에 따라 반환 됩니다.

## <a name="moving-your-script-code-into-the-implementation-file"></a>구현 파일에 스크립트 코드를 이동

이 문서의 이전 섹션에는 F # 코드를 작성 합니다. 일반적인 첫 번째 단계는 설명: FSI를 대화형으로 실행 하는 초기 함수를 작성 합니다.  이 복제 기반 개발, 여기서 REPL은 "읽기 평가 인쇄 루프" 라고 합니다.  작업 결과가 있는 될 때까지 기능을 시험해 좋은 방법입니다.

복제 기반 개발의 다음 단계는 F # 구현 파일에 작업 코드를 옮기는 것입니다.  그런 다음 컴파일될 수 F # 컴파일러에 의해 실행 될 수 있는 어셈블리에 있습니다.

를 시작 하려면 열기 `ClassLibraryDemo.fs`합니다.  일부 코드는 이미에 있는 알 수 있습니다.  계속 진행 하 고 클래스 정의 삭제 하지만을 남겨 두어야는 [ `namespace` ](../language-reference/namespaces.md) 위쪽에 선언 합니다.

다음으로 새 만듭니다 [ `module` ](../language-reference/modules.md) 호출 `PigLatin` 복사는 `toPigLatin` 따라서 함수에:

[!code-fsharp[ToPigLatin](../../../samples/snippets/fsharp/getting-started/pig-latin.fs#L1-L14)]

C# 또는 Visual Basic 프로젝트에서 코드를 호출 하려는 경우 일반적인 접근 방식 및 F # 코드에서는 함수를 구성할 수는 여러 가지 방법 중 하나입니다.

을 열고는 `Script.fsx` 다시 파일을 전체 삭제 `toPigLatin` 작동할 수 있지만 파일에 다음 두 줄을 유지 해야 합니다.

```
#load "ClassLibraryDemo.fs"
open ClassLibraryDemo
```

첫 번째 줄에 로드 하는 데 스크립팅을 FSI 필요한 `ClassLibraryDemo.fs`합니다.  두 번째 줄은 편의 위해: 생략 하는 것은 선택 사항 이지만 입력할 필요가 `open ClassLibraryDemo` FSI 창 상태로 전환 하려는 경우에 `ToPigLatin` 범위로 모듈입니다.

그런 다음 FSI 창에서 사용 하 여 함수 호출의 `PigLatin` 앞에서 정의한 모듈:

```
> PigLatin.toPigLatin "banana";;
val it : string = "ananabay"
> PigLatin.toPigLatin "apple";;
val it : string = "appleyay"
```

성공  이전에 동일한 결과를 가져오지만 이제 F # 구현 파일에서 로드 됩니다.  주요 차이점은 F # 소스 파일 FSI에서 뿐 아니라 어디서 나 실행할 수 있는 어셈블리로 컴파일되는 합니다.

## <a name="summary"></a>요약

이 문서에서는 지금까지 학습:

1. Ionide와 Visual Studio 코드를 설정 하는 방법.
2. Ionide와 첫 번째 F # 프로젝트를 만드는 방법.
3. Ionide에서 첫 번째 F # 함수를 작성 한 후 FSI에서 실행 F # 스크립트를 사용 하는 방법입니다.
4. F # 소스를 스크립트 코드를 마이그레이션하고 FSI에서 해당 코드를 호출 하는 방법.

코드를 작성할 훨씬 더 많은 F # Visual Studio Code 및 Ionide 사용 하 여 이제 정답입니다.

## <a name="troubleshooting"></a>문제 해결

여기 몇 가지 방법으로 충돌할 수 있는 특정 문제를 해결할 수 있습니다.

1. 코드 편집 Ionide의는 기능을 가져오려면 F # 파일 Visual Studio Code 작업 영역에서 열려 있는 폴더 내에서 디스크에 저장 해야 합니다.
2. 시스템에 변경 작업을 수행 하거나 Visual Studio 코드 열려 Ionide 필수 구성 요소를 설치, Visual Studio 코드를 다시 시작 합니다.
3. F # 컴파일러 및 F # interactive 정식 경로 사용 하지 않고 명령줄에서 사용할 수 있는지 확인 합니다.  입력 하 여 그렇게 할 수 `fsc` F # 컴파일러에 대 한 명령줄의 및 `fsi` 또는 `fsharpi` 에 대 한 Visual F # 도구 창 및 linux/Mac에서 모노에 각각.
4. 프로젝트 디렉터리에 잘못 된 문자가 있으면 Ionide 작동 하지 않을 수 있습니다.  이 경우 프로젝트 디렉터리를 이름을 바꿉니다.
5. 작업 Ionide 명령 중 없음, 확인 프로그램 [Visual Studio Code keybindings](https://code.visualstudio.com/docs/customization/keybindings#_customizing-shortcuts) 경우 재정의 중인에 실수로 볼 수 있습니다.
6. 컴퓨터에 Ionide 나뉘어집니다 위에 해당는 문제를 해결 하는 경우를 제거해 보세요는 `ionide-fsharp` 컴퓨터에 디렉터리 플러그 인 도구 모음을 다시 설치 합니다.

Ionide는 오픈 소스 프로젝트 작성 및 F # 커뮤니티의 회원이 유지 관리 합니다.  문제를 보고 하 고에 참가할 수 정도 하십시오는 [Ionide VSCode: FSharp GitHub 리포지토리](https://github.com/ionide/ionide-vscode-fsharp)합니다.

보고서에 문제가 있는 경우 따르십시오 [문제를 보고할 때 사용 하는 로그를 가져오기 위한 지침은](https://github.com/ionide/ionide-vscode-fsharp#how-to-get-logs-for-debugging--issue-reporting)합니다.

Ionide 개발자 및 F #에서 커뮤니티에서 도움을 요청할 수도 있습니다는 [Ionide Gitter 채널](https://gitter.im/ionide/ionide-project)합니다.

## <a name="next-steps"></a>다음 단계

F # 및 언어의 기능에 대 한 자세한 내용은 체크 아웃 [둘러보기의 F #](../tour.md)합니다.

## <a name="see-also"></a>참고 항목

[F# 둘러보기](../tour.md)

[F# 언어 참조](../language-reference/index.md)

[함수](../language-reference/functions/index.md)

[모듈](../language-reference/modules.md)

[네임스페이스](../language-reference/namespaces.md)

[VSCode Ionide: FSharp](https://github.com/ionide/ionide-vscode-fsharp)
