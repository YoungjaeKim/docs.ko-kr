---
title: 문자열 보간 - C#
description: C# 6에서 문자열 보간이 작동하는 방법 알아보기
keywords: .NET, .NET Core, C#, 문자열
author: mgroves
ms.author: wiwagn
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: f8806f6b-3ac7-4ee6-9b3e-c524d5301ae9
ms.openlocfilehash: a9578d006861b987871071961437345c378a5b58
ms.sourcegitcommit: 935d5267c44f9bce801468ef95f44572f1417e8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="string-interpolation-in-c"></a>C#의 문자열 보간 #

문자열 보간은 문자열의 자리 표시자가 문자열 변수의 값으로 바뀌는 방식입니다. C# 6 이전에는 이 작업을 위해 <xref:System.String.Format%2A?displayProperty=nameWithType>을 사용했습니다. 이 방법도 괜찮지만 번호가 매겨진 자리 표시자를 사용하므로 읽기가 더 어렵고 좀 더 길 수 있습니다.

다른 프로그래밍 언어의 경우 한동안 문자열 보간이 기본적으로 제공되었습니다. 예를 들면 PHP의 경우 다음과 같습니다.

```php
$name = "Jonas";
echo "My name is $name.";
// This will output "My name is Jonas."
```

C# 6에서는 마침내 문자열 보간 스타일을 갖추게 되었습니다. 문자열 앞에 `$`를 사용하여 변수/식을 값으로 대체해야 함을 나타낼 수 있습니다.

## <a name="prerequisites"></a>전제 조건
.NET Core를 실행하려면 컴퓨터에 설정해야 합니다. [.NET Core](https://www.microsoft.com/net/core) 페이지에서 설치 지침을 확인할 수 있습니다.
Windows, Ubuntu Linux, macOS 또는 Docker 컨테이너에서 이 응용 프로그램을 실행할 수 있습니다. 선호하는 코드 편집기를 설치해야 합니다. 아래 설명에서는 오픈 소스 플랫폼 간 편집기인 [Visual Studio Code](https://code.visualstudio.com/)를 사용합니다. 그러나 익숙한 어떤 도구도 사용 가능합니다.

## <a name="create-the-application"></a>응용 프로그램 만들기

이제 모든 도구를 설치했으므로 새로운 .NET Core 응용 프로그램을 만들어 보겠습니다. 명령줄 생성기를 사용하려면 프로젝트에 대해 `interpolated`와 같은 디렉터리를 만들고 즐겨 사용하는 셸에서 다음 명령을 실행합니다.

```
dotnet new console
```

이 명령은 프로젝트 파일 *interpolated.csproj* 및 소스 코드 파일 *Program.cs*를 사용하여 기본 .NET Core 프로젝트를 만듭니다. `dotnet restore`를 실행하여 이 프로젝트를 컴파일하는 데 필요한 종속성을 복원해야 합니다.

[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

이 프로그램을 실행하려면 `dotnet run`을 사용합니다. 콘솔에 "Hello, World" 출력이 표시됩니다.



## <a name="intro-to-string-interpolation"></a>문자열 보간 소개

<xref:System.String.Format%2A?displayProperty=nameWithType>을 사용하여 문자열에 따라 인수로 대체되는 문자열에서 "자리 표시자"를 지정합니다. 예를 들면 다음과 같습니다.

[!code-csharp[String.Format example](../../../samples/snippets/csharp/new-in-6/string-interpolation.cs#StringFormatExample)]  

그러면 "My name is Matt Groves"가 출력됩니다.

C# 6에서 `String.Format`을 사용하는 대신, 앞에 `$` 기호를 붙인 다음 문자열에 직접 변수를 사용하여 보간된 문자열을 정의합니다. 예를 들면 다음과 같습니다.

[!code-csharp[Interpolation example](../../../samples/snippets/csharp/new-in-6/string-interpolation.cs#InterpolationExample)]  

단순히 변수를 사용할 필요는 없습니다. 대괄호 안에 어떤 식도 사용 가능합니다. 예를 들면 다음과 같습니다.

[!code-csharp[Interpolation expression example](../../../samples/snippets/csharp/new-in-6/string-interpolation.cs#InterpolationExpressionExample)]  

다음이 출력됩니다.

```
This is line number 1
This is line number 2
This is line number 3
This is line number 4
This is line number 5
```

## <a name="how-string-interpolation-works"></a>문자열 보간이 작동하는 방법

내부적으로 이 문자열 보간 구문은 컴파일러에서 `String.Format`로 변환됩니다. 따라서 [`String.Format` 이전에 String.Format으로 수행했던 것과 동일한 형식의 작업](../../standard/base-types/formatting-types.md)을 수행할 수 있습니다.

예를 들어 안쪽 여백 및 숫자 서식을 추가할 수 있습니다.

[!code-csharp[Interpolation formatting example](../../../samples/snippets/csharp/new-in-6/string-interpolation.cs#InterpolationFormattingExample)]  

위 예제는 다음과 같은 결과를 출력합니다.

```
998        5,177.67
999        6,719.30
1000       9,910.61
1001       529.34
1002       1,349.86
1003       2,660.82
1004       6,227.77
```

변수 이름이 없는 경우 컴파일 타임 오류가 생성됩니다.

예를 들면 다음과 같습니다.

```csharp
var animal = "fox";
var localizeMe = $"The {adj} brown {animal} jumped over the lazy {otheranimal}";
var adj = "quick";
Console.WriteLine(localizeMe);
```

이를 컴파일하면 오류가 발생합니다.
 
* `Cannot use local variable 'adj' before it is declared` - `adj` 변수는 보간된 문자열 *이후*까지 선언되지 않았습니다.
* `The name 'otheranimal' does not exist in the current context` - `otheranimal`이라는 변수가 선언된 적이 없었습니다.

## <a name="localization-and-internationalization"></a>지역화 및 국제화

보간된 문자열은 국제화에 유용할 수 있는 <xref:System.IFormattable?displayProperty=nameWithType> 및 <xref:System.FormattableString?displayProperty=nameWithType>을 지원합니다.

기본적으로 보간된 문자열은 현재 문화권을 사용합니다. 다른 문화권을 사용하려면 보간된 문자열을 `IFormattable`로 캐스팅합니다. 예를 들면 다음과 같습니다.

[!code-csharp[Interpolation internationalization example](../../../samples/snippets/csharp/new-in-6/string-interpolation.cs#InterpolationInternationalizationExample)]  

## <a name="conclusion"></a>결론 

이 자습서에서는 C# 6의 문자열 보간 기능을 사용하는 방법을 알아보았습니다. 이 기능은 기본적으로 고급 사용법에 대한 주의 사항을 사용하여 단순한 `String.Format` 문을 작성하는 정확한 방법입니다. 자세한 내용은 [문자열 보간](../../csharp//language-reference/tokens/interpolated.md) 토픽을 참조하세요.
