---
title: "F# 가이드"
description: "이 가이드에서는 F #,.NET에서 실행 되는 함수형 프로그래밍 언어에 대 한 다양 한 교육 자료에 대 한 개요를 제공 합니다."
author: jackfoxy
ms.author: phcart
ms.date: 02/28/2018
ms.topic: article
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: ea27fb37-dad1-4bd4-a3cc-4f5c70767ae9
ms.openlocfilehash: b7cf3feb5699f85bf09a47f008fdaf70ac7c8d77
ms.sourcegitcommit: 83dd5ec003e788ccb3e33f3412a7af39ae347646
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="f-guide"></a>F# 가이드

F #은.NET에서 실행 되는 함수형 프로그래밍 언어입니다. 또한 blend 기능 및 개체 프로그래밍 문제에 대 한 실용적인 솔루션에 대 한 사용자에 게 알려주는 개체에 대 한 완전 한 지원을 제공 합니다.

```fsharp
open System // Get access to functionality in System namespace.

// Function: takes a name and produces a greeting.
let getGreeting name =
    sprintf "Hello, %s! Isn't F# great?" name

// Use the EntryPoint attribute to run the program.
[<EntryPoint>]
let main args =
    args                     // Use F# pipe operators to send the args into some functions.
    |> Array.map getGreeting // Turn each name into a friendly greeting.
    |> Array.iter printfn    // Print them!

    0
```

F #은 본래 생산성에 대 한 합니다. F #에 대 한 도구 지원을 유비쿼터스 이며 다양 한 고급 기능입니다.

## <a name="learning-f"></a>F # 학습 #

[F # 둘러보기](tour.md) 코드 샘플은 주요 언어 기능의 개요를 제공 합니다. F #에 새로 고 언어의 작동 방식에 대해 하려고 할 경우에 권장 됩니다.

[Visual Studio에서 F #으로 시작 하려면](get-started/get-started-visual-studio.md) Windows에 속해 있으며 사용할 것 전체 Visual Studio IDE (Integraded 개발 환경) 하는 경우.

[Mac 용 Visual Studio에서 F #으로 시작](get-started/get-started-with-visual-studio-for-mac.md) macOS에 속해 있으며 Visual Studio IDE를 사용 하려는 경우.

[Visual Studio Code에서 F #으로 시작 하려면](get-started/get-started-vscode.md) 경우 플랫폼 간 경량 및 IDE 기능이 포함 된 발생 합니다.

[F #으로.NET Core CLI 시작](get-started/get-started-command-line.md) 명령줄 도구를 사용 하려는 경우.

## <a name="references"></a>참조

[F # 언어 참조](language-reference/index.md) 은 F # 언어의 모든 기능에 대 한 공식 하 고 포괄적인 참조 합니다. 각 문서는 구문에 설명 하 고 코드 샘플을 보여 줍니다. 특정 문서를 찾습니다는 목차에서 필터 표시줄을 사용할 수 있습니다.

[F # 핵심 라이브러리 참조가](https://msdn.microsoft.com/visualfsharpdocs/conceptual/fsharp-core-library-reference) F # 핵심 라이브러리에 대 한 API 참조 됩니다.

## <a name="additional-guides"></a>추가 가이드

[F # 재미와 수익에 대 한](https://swlaschin.gitbooks.io/fsharpforfunandprofit/content/) 는 종합적이 고 매우 자세한 र ् थ 학습 F #은 합니다. 내용과 작성자는 F # 커뮤니티에서 사랑 합니다. 대상 사용자는 주로 개발자에 게 개체 지향 프로그래밍 배경.

[F # 프로그래밍 Wikibook](https://en.wikibooks.org/wiki/F_Sharp_Programming) 학습 F #에 대 한 wikibook 됩니다. F # 커뮤니티의 제품 이기도합니다. 대상 그룹은 F #을 사용 하면 약간의 개체 지향 프로그래밍 배경을 처음 접하는 사용자입니다.

## <a name="learn-f-through-videos"></a>F # 비디오를 통한 학습

[YouTube에서 F # 자습서](https://www.youtube.com/watch?v=c7eNDJN758U) F # Visual Studio를 사용 하 여, 1.5 시간의 과정 동안 다양 한 좋은 예를 보여 주는에 충분히 소개 합니다. 대상 그룹에는 F #를 처음 접하는 Visual Studio 개발자입니다.

[F #을 사용한 프로그래밍 소개](https://www.youtube.com/watch?v=Teak30_pXHk&list=PLEoMzSkcN8oNiJ67Hd7oRGgD1d4YBxYGC) 훌륭한 비디오 일련의 기본 편집기로 Visual Studio 코드를 사용 하 여입니다. 비디오 시리즈를 시작한 RPG 비디오 텍스트 기반 게임을 빌드하는 것과 끝납니다. 대상 사용자는 개발자 처음인 F # 및 Visual Studio Code (또는 간단한 IDE) 선호입니다.

[F #에 대 한 개발자를 위한 Visual Studio 2017의 새로운](https://www.linkedin.com/learning/what-s-new-in-visual-studio-2017-for-f-sharp-for-developers) 은 Visual Studio 2017에서 F #에 대 한 새로운 기능 중 일부를 보여 주는 비디오 과정입니다. 대상 그룹에는 F #를 처음 접하는 Visual Studio 개발자입니다.

## <a name="other-useful-resources"></a>기타 유용한 리소스

[F # 코드 조각 웹 사이트](http://www.fssnip.net) massive 완전 초보자를 위한에서 고급 코드 조각에 이르기까지 F #에서 모든 작업 하는 방법을 보여 주는 코드 조각 집합이 포함 되어 있습니다.

[F # 소프트웨어 Foundation Slack](http://fsharp.org/guides/slack/) 좋은 곳은 초보자를 위한 및 전문가 게 모두 매우 활성화가 있으며 프로그래머 세계에서 가장 F # 채팅에 사용할 수 있는의 일부입니다. 조인 하는 것이 좋습니다.

## <a name="the-f-software-foundation"></a>F# Software Foundation

Microsoft 기본 개발자의 F # 언어와 Visual Studio에서 해당 도구 이지만, F #는 또한 뒷받침 되며는 독립적인 foundation는 F # 소프트웨어 Foundation (FSSF).

F# Software Foundation의 임무는 F# 프로그래밍 언어를 홍보하고 보호하고 발전시키며, F# 프로그래머의 다양한 국제 커뮤니티의 성장을 지원하고 용이하게 만드는 것입니다.

자세한 내용을 알아보고 참여하려면 [fsharp.org](http://fsharp.org)를 참조하세요. 조인, 무료 및 foundation의 F # 개발자의 네트워크를 포기 하 고치지 않을!