---
title: .NET Compiler Platform SDK 구문 모델 사용
description: 이 개요에서는 구문 노드를 이해하고 조작하는 데 사용하는 형식에 대한 이해를 제공합니다.
author: billwagner
ms.author: wiwagn
ms.date: 10/15/2017
ms.topic: conceptual
ms.prod: .net
ms.devlang: devlang-csharp
ms.custom: mvc
ms.openlocfilehash: 09d07e6257ad7d32d75328a8c1850888b4d0b937
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="work-with-syntax"></a>구문 작업

**구문 트리**는 컴파일러 API에서 노출하는 기본 데이터 구조입니다. 이러한 트리는 소스 코드의 어휘 및 구문 구조를 나타냅니다. 두 가지 중요한 용도를 제공합니다.

1. 사용자의 프로젝트에서 소스 코드의 구문 구조를 보고 처리하도록 IDE, 추가 기능, 코드 분석 도구 및 리팩터링과 같은 도구 허용
2. 직접 텍스트 편집을 사용하지 않고 자연스러운 방식으로 소스 코드를 만들고, 수정하고, 다시 정렬하도록 리팩터링 및 IDE와 같은 도구 활성화 트리를 만들고 조작하여 도구는 쉽게 소스 코드를 만들고 다시 정렬할 수 있습니다.

## <a name="syntax-trees"></a>구문 트리

구문 트리는 컴파일, 코드 분석, 바인딩, 리팩터링, IDE 기능 및 코드 생성에 사용되는 기본 구조입니다. 소스 코드의 어떠한 부분도 먼저 식별되고 잘 알려진 많은 구조적 언어 요소 중 하나로 분류되지 않고 인식되지 않습니다. 

구문 트리에는 세 가지 주요 특성이 있습니다. 첫 번째 특성은 구문 트리가 최고의 충실도로 모든 원본 정보를 저장하는 것입니다. 즉 구문 트리가 공백, 설명 및 전처리기 지시문을 포함하여 원본 텍스트에서 발견되는 모든 정보, 모든 문법 구문, 모든 어휘 토큰 및 사이의 모든 다른 것을 포함하는 것을 의미합니다. 예를 들어 원본에서 언급된 각 리터럴은 입력된 대로 정확하게 표시됩니다. 구문 트리는 프로그램이 불완전하거나 형식이 잘못된 경우 구문 트리에 건너뛰거나 누락된 토큰을 표시하여 소스 코드의 오류를 나타냅니다.  

이는 두 번째 구문 트리의 특성을 활성화합니다. 파서에서 가져온 구문 트리는 구문 분석된 정확한 텍스트를 생성할 수 있습니다. 구문 노드에서 해당 노드를 기반으로 하는 하위 트리의 텍스트 표현을 가져올 수 있습니다. 구문 트리가 원본 텍스트를 생성하고 편집하는 방법으로 사용될 수 있다는 것을 의미합니다. 암시적으로 해당 텍스트를 만든 트리를 만들고, 변경 내용에서 새 트리를 기존 트리로 만들어 구문 트리를 편집하여 텍스트를 효과적으로 편집했습니다. 

구문 트리의 세 번째 특성은 변경할 수 없으며 스레드로부터 안전하다는 것입니다.  즉, 트리를 얻으면 이는 코드의 현재 상태의 스냅숏이며 변경되지 않습니다. 따라서 여러 사용자는 잠금 또는 중복 없이 서로 다른 스레드에서 동시에 동일한 구문 트리와 상호 작용할 수 있습니다. 트리를 변경할 수 없으며 트리에 직접 수정을 만들 수 없으므로 팩터리 메서드는 트리의 추가 스냅숏을 만들어 구문 트리를 만들고 수정하도록 돕습니다. 트리는 기본 노드를 다시 사용하는 방법에서 효율적이므로 빠르게 작은 추가 메모리로 새 버전을 다시 빌드할 수 있습니다.

구문 트리는 비터미널 구조 요소가 다른 요소를 부모로 삼는 문자 그대로 트리 데이터 구조입니다. 각 구문 트리는 노드, 토큰 및 기타 정보로 구성되어 있습니다.  

## <a name="syntax-nodes"></a>구문 노드

구문 노드는 구문 트리의 기본 요소 중 하나입니다. 이러한 노드는 선언, 명령문, 절 및 식과 같은 구문 구조를 나타냅니다. 구문 노드의 각 범주는 <xref:Microsoft.CodeAnalysis.SyntaxNode?displayProperty=nameWithType>에서 파생되는 별도 클래스로 나타냅니다. 노드 클래스의 집합은 확장할 수 없습니다. 

모든 구문 노드는 구문 트리에서 비터미널 노드입니다. 즉, 항상 다른 노드 및 토큰을 자식으로 갖습니다. 다른 노드의 자식으로 각 노드는 <xref:Microsoft.CodeAnalysis.SyntaxNode.Parent?displayProperty=nameWithType> 속성을 통해 액세스할 수 있는 부모 노드를 갖습니다. 노드 및 트리를 변경할 수 없기 때문에 부모 노드는 변경되지 않습니다. 트리의 루트는 null 부모를 갖습니다.  

각 노드에는 원본 텍스트에서의 위치에 따라 순서대로 자식 노드의 목록을 반환하는 <xref:Microsoft.CodeAnalysis.SyntaxNode.ChildNodes?displayProperty=nameWithType> 메서드가 있습니다. 이 목록은 토큰을 포함하지 않습니다. 각 노드에는 해당 노드를 기반으로 하는 하위 트리에 존재하는 모든 노드, 토큰 또는 기타 정보의 목록을 나타내는 <xref:Microsoft.CodeAnalysis.SyntaxNode.DescendantNodes%2A>, <xref:Microsoft.CodeAnalysis.SyntaxNode.DescendantTokens%2A> 또는 <xref:Microsoft.CodeAnalysis.SyntaxNode.DescendantTrivia%2A> 등의 하위 목록을 검사하는 메서드가 있습니다.  

또한 각 구문 노드 하위 클래스는 강력한 형식의 속성을 통해 동일한 모든 자식을 노출합니다. 예를 들어 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax> 노드 클래스에는 이진 연산자, <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Left>, <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.OperatorToken> 및 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Right>에 해당하는 3개의 추가 속성이 있습니다. <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Left> 및 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Right>의 형식은 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.ExpressionSyntax>이며 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.OperatorToken>의 형식은 <xref:Microsoft.CodeAnalysis.SyntaxToken>입니다.

일부 구문 노드에는 선택적 자식이 있습니다. 예를 들어 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.IfStatementSyntax>에는 선택적 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.ElseClauseSyntax>가 있습니다. 자식이 없는 경우 속성은 null을 반환합니다. 

## <a name="syntax-tokens"></a>구문 토큰

구문 토큰은 코드의 가장 작은 구문 조각을 나타내는 언어 문법의 터미널입니다. 다른 노드 또는 토큰의 부모가 아닙니다. 구문 토큰은 키워드, 식별자, 리터럴 및 문장 부호로 구성됩니다. 

효율성 향상을 위해 <xref:Microsoft.CodeAnalysis.SyntaxToken> 형식은 CLR 값 형식입니다. 따라서 구문 노드와 달리 표시되는 토큰의 종류에 따라 의미가 있는 속성을 조합하여 모든 종류의 토큰에 대해 하나의 구문만 있습니다.

예를 들어 정수 리터럴 토큰은 숫자 값을 나타냅니다. 토큰이 포괄하는 원시 원본 텍스트 이외에 리터럴 토큰에는 디코딩된 정확한 정수 값을 알려 주는 <xref:Microsoft.CodeAnalysis.SyntaxToken.Value> 속성이 있습니다. 많은 기본 형식 중 하나일 수 있으므로 이 속성은 <xref:System.Object>로 입력됩니다.

<xref:Microsoft.CodeAnalysis.SyntaxToken.ValueText> 속성은 <xref:Microsoft.CodeAnalysis.SyntaxToken.Value> 속성과 동일한 정보를 알려 주지만 이 속성은 항상 <xref:System.String>으로 입력됩니다. C# 원본 텍스트에서 식별자는 유니코드 이스케이프 문자를 포함할 수 있지만 이스케이프 시퀀스 자체의 구문은 식별자 이름의 일부로 간주되지 않습니다. 따라서 토큰에 포함되는 원시 텍스트는 이스케이프 시퀀스를 포함하지만 <xref:Microsoft.CodeAnalysis.SyntaxToken.ValueText> 속성은 포함하지 않습니다. 대신 이스케이프로 식별되는 유니코드 문자를 포함합니다. 예를 들어 원본 텍스트가 `\u03C0`으로 작성된 식별자를 포함하는 경우 이 토큰에 대한 <xref:Microsoft.CodeAnalysis.SyntaxToken.ValueText> 속성은 `π`를 반환합니다.

## <a name="syntax-trivia"></a>구문 기타 정보

구문 기타 정보는 공백, 설명 및 전처리기 지시문과 같은 코드의 일반적인 이해에 크게 중요하지 않은 원본 텍스트의 일부를 나타냅니다. 구문 토큰과 같이 기타 정보는 값 형식입니다. 단일 <xref:Microsoft.CodeAnalysis.SyntaxTrivia?displayProperty=nameWithType> 형식은 모든 종류의 기타 정보를 설명하는 데 사용됩니다.

기타 정보는 일반 언어 구문의 일부가 아니며 두 토큰 사이의 아무 곳에나 나타날 수 있으므로 노드의 자식으로 구문 트리에 포함되지 않습니다. 리팩터링과 같은 기능을 구현하는 경우 및 원본 텍스트로 최고의 충실도를 유지하는 데 중요하므로 구문 트리의 일부로 존재합니다.

토큰의 <xref:Microsoft.CodeAnalysis.SyntaxToken.LeadingTrivia?displayProperty=nameWithType> 또는 <xref:Microsoft.CodeAnalysis.SyntaxToken.TrailingTrivia?displayProperty=nameWithType> 컬렉션을 검사하여 기타 정보에 액세스할 수 있습니다. 원본 텍스트를 구문 분석할 때 기타 정보의 시퀀스는 토큰과 연결됩니다. 일반적으로 토큰은 다음 토큰까지 동일한 줄의 다음에 모든 기타 정보를 소유합니다. 해당 줄 다음의 모든 기타 정보는 다음 토큰으로 연결됩니다. 원본 파일의 첫 번째 토큰은 모든 초기 기타 정보를 가져오고 파일에 있는 기타 정보의 마지막 시퀀스는 파일 끝 토큰으로 고정됩니다. 그렇지 않으면 0의 너비를 갖습니다.

구문 노드 및 토큰과 달리 구문 기타 정보는 부모가 없습니다. 아직 트리의 일부이며 각각은 단일 토큰에 연결되어 있으므로 <xref:Microsoft.CodeAnalysis.SyntaxTrivia.Token?displayProperty=nameWithType> 속성을 사용하여 연결된 토큰에 액세스할 수 있습니다.

## <a name="spans"></a>범위

각 노드, 토큰 또는 기타 정보는 원본 텍스트 내의 해당 위치와 구성된 문자 수를 알고 있습니다. 텍스트 위치는 0부터 시작하는 `char` 인덱스인 32비트 정수로 표현됩니다. <xref:Microsoft.CodeAnalysis.Text.TextSpan> 개체는 시작 위치 및 문자 수이며 정수로 표현됩니다. <xref:Microsoft.CodeAnalysis.Text.TextSpan>의 길이가 0인 경우 두 문자 사이의 위치를 나타냅니다.

각 노드에 두 개의 <xref:Microsoft.CodeAnalysis.Text.TextSpan> 속성: <xref:Microsoft.CodeAnalysis.SyntaxNode.Span*> 및 <xref:Microsoft.CodeAnalysis.SyntaxNode.FullSpan*>합니다. 

<xref:Microsoft.CodeAnalysis.SyntaxNode.Span*> 속성은 노드의 하위 트리에 있는 첫 번째 토큰의 시작부터 마지막 토큰의 끝에 이르는 텍스트 범위입니다. 이 범위는 모든 선행 또는 후행 기타 정보를 포함하지 않습니다.

<xref:Microsoft.CodeAnalysis.SyntaxNode.FullSpan*> 속성은 노드의 일반 범위와 모든 선행 또는 후행 기타 정보의 범위를 포함하는 텍스트 범위입니다.

예를 들어: 

``` csharp
      if (x > 3)
      {
||        // this is bad
          |throw new Exception("Not right.");|  // better exception?||
      }
```

블록 내의 명령문 노드에는 단일 세로 막대(|)로 표시되는 범위가 있습니다. 여기에는 `throw new Exception("Not right.");` 문자가 포함됩니다. 전체 범위는 이중 세로 막대(||)로 표시됩니다. 여기에는 범위와 동일한 문자 및 선행 및 후행 기타 정보와 연결된 문자가 포함됩니다.

## <a name="kinds"></a>종류

각 노드, 토큰 또는 기타 정보에는 표시되는 정확한 구문 요소를 식별하는 <xref:System.Int32?displayProperty=nameWithType> 형식의 <xref:Microsoft.CodeAnalysis.SyntaxNode.RawKind?displayProperty=nameWithType> 속성이 있습니다. 이 값은 언어별 열거형으로 캐스팅될 수 있습니다. 각 언어, C# 또는 VB에는 문법에서 가능한 모든 노드, 토큰 및 기타 정보 요소를 나열하는 단일 `SyntaxKind` 열거형(각각 <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind?displayProperty=nameWithType> 및 <xref:Microsoft.CodeAnalysis.VisualBasic.SyntaxKind?displayProperty=nameWithType>)이 있습니다. 에 액세스 하 여이 변환을 자동으로 수행할 수 있습니다는 <xref:Microsoft.CodeAnalysis.CSharp.CSharpExtensions.Kind*?displayProperty=nameWithType> 또는 <xref:Microsoft.CodeAnalysis.VisualBasic.VisualBasicExtensions.Kind*?displayProperty=nameWithType> 확장 메서드입니다.

<xref:Microsoft.CodeAnalysis.SyntaxToken.RawKind> 속성은 동일한 노드 클래스를 공유하는 구문 노드 형식의 쉬운 명확성을 허용합니다. 토큰 및 기타 정보의 경우 이 속성은 요소의 한 형식을 다른 형식에서 구분하는 유일한 방법입니다. 

예를 들어 단일 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax> 클래스에는 자식으로 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Left>, <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.OperatorToken> 및 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Right>가 있습니다. <xref:Microsoft.CodeAnalysis.CSharp.CSharpExtensions.Kind*> 속성은 구문 노드의 <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind.AddExpression>, <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind.SubtractExpression> 또는 <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind.MultiplyExpression> 종류인지를 구분합니다.

## <a name="errors"></a>오류

원본 텍스트에 구문 오류가 있는 경우에도 원본에 대해 왕복 가능한 전체 구문 트리가 노출됩니다. 파서가 언어의 정의된 구문에 맞지 않는 코드를 발견하면 두 가지 기술 중 하나를 사용하여 구문 트리를 만듭니다.

먼저 파서에 특정 종류의 토큰이 필요하지만 찾을 수 없는 경우 토큰이 필요한 위치의 구문 트리로 누락된 토큰을 삽입할 수 있습니다. 누락된 토큰은 필요한 실제 토큰을 나타내지만 빈 범위를 가지며 해당 <xref:Microsoft.CodeAnalysis.SyntaxNode.IsMissing?displayProperty=nameWithType> 속성은 `true`를 반환합니다.

둘째로 파서는 구문 분석을 계속할 수 있는 토큰을 찾을 때까지 토큰을 건너뛸 수 있습니다. 이 경우 건너뛴 토큰은 <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind.SkippedTokensTrivia> 종류와 함께 기타 정보 노드로 연결됩니다.
