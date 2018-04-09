---
title: 문자열(C# 프로그래밍 가이드)
ms.date: 07/20/2015
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
helpviewer_keywords:
- C# language, strings
- strings [C#]
ms.assetid: 21580405-cb25-4541-89d5-037846a38b07
caps.latest.revision: 41
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 9478900be008588597c1dd9e75f704c751ebe344
ms.sourcegitcommit: 935d5267c44f9bce801468ef95f44572f1417e8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="strings-c-programming-guide"></a>문자열(C# 프로그래밍 가이드)
문자열은 값이 텍스트인 <xref:System.String> 형식의 개체입니다. 내부적으로 텍스트는 <xref:System.Char> 개체의 순차적 읽기 전용 컬렉션으로 저장됩니다. C# 문자열의 끝에 null 종료 문자가 없으므로 C# 문자열에는 포함된 null 문자('\0')를 여러 개 사용할 수 있습니다. 문자열의 <xref:System.String.Length%2A> 속성은 유니코드 문자 수가 아닌 포함된 `Char` 개체 수를 나타냅니다. 문자열에서 개별 유니코드 코드 포인트에 액세스하려면 <xref:System.Globalization.StringInfo> 개체를 사용합니다.  
  
## <a name="string-vs-systemstring"></a>문자열과 System.String  
 C#에서 `string` 키워드는 <xref:System.String>의 별칭입니다. 따라서 `String` 및 `string`은 동일하며 원하는 명명 규칙을 사용할 수 있습니다. `String` 클래스는 문자열을 안전하게 작성, 조작 및 비교할 수 있도록 다양한 메서드를 제공합니다. 또한 C# 언어는 일반적인 문자열 작업을 간소화 하기 위해 일부 연산자를 오버로드합니다. 키워드에 대한 자세한 내용은 [string](../../../csharp/language-reference/keywords/string.md)을 참조하세요. 형식 및 메서드에 대한 자세한 내용은 <xref:System.String>을 참조하세요.  
  
## <a name="declaring-and-initializing-strings"></a>문자열 선언 및 초기화  
 다음 예제에서와 같이 다양한 방법으로 문자열을 선언하고 초기화할 수 있습니다.  
  
 [!code-csharp[csProgGuideStrings#1](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_1.cs)]  
  
 문자 배열이 포함된 문자열을 초기화할 경우를 제외하고는 문자열 개체를 만들기 위해 [new](../../../csharp/language-reference/keywords/new-operator.md) 연산자를 사용하지 않습니다.  
  
 문자열 길이가 0인 새 <xref:System.String> 개체를 만들려면 <xref:System.String.Empty> 상수 값이 포함된 문자열을 초기화하세요. 빈 문자열을 문자열 리터럴로 나타내면 ""로 표시됩니다. [null](../../../csharp/language-reference/keywords/null.md) 대신 <xref:System.String.Empty> 값이 포함된 문자열을 초기화하면 <xref:System.NullReferenceException> 발생을 줄일 수 있습니다. 액세스하기 전에 문자열의 값을 확인하려면 정적 <xref:System.String.IsNullOrEmpty%28System.String%29> 메서드를 사용하세요.  
  
## <a name="immutability-of-string-objects"></a>문자열 개체의 불변성  
 문자열 개체는 *변경할 수 없습니다*. 즉, 생성된 후에는 바꿀 수 없습니다. 실제로 문자열을 수정하는 것으로 나타나는 모든 <xref:System.String> 메서드 및 C# 연산자는 새로운 문자열 개체에 결과를 반환합니다. 다음 예제에서 `s1` 및 `s2`의 콘텐츠는 단일 문자열을 형성하도록 연결되며, 두 개의 원본 문자열은 변경되지 않습니다. `+=` 연산자는 결합된 콘텐츠를 포함하는 새 문자열을 만듭니다. 새 개체는 `s1` 변수에 할당되며, 참조를 유지하는 변수가 없으므로 `s1`에 할당된 원래 개체는 가비지 수집을 위해 해제됩니다.  
  
 [!code-csharp[csProgGuideStrings#2](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_2.cs)]  
  
 문자열 "수정"은 실제로 새 문자열을 만드는 것이므로 문자열에 대한 참조를 만들 때 주의해야 합니다. 문자열에 대한 참조를 만든 후 원래 문자열을 "수정"하더라도 참조는 문자열을 수정할 때 만든 새 개체가 아니라 원래 개체를 계속 가리킵니다. 이 동작은 다음 코드에서 볼 수 있습니다.  
  
 [!code-csharp[csProgGuideStrings#25](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_3.cs)]  
  
 원래 문자열에 대한 검색 및 바꾸기 작업과 같이, 수정을 기반으로 하는 새 문자열 작성 방법에 대한 자세한 내용은 [방법: 문자열 콘텐츠 수정](../../how-to/modify-string-contents.md)을 참조하세요.  
  
## <a name="regular-and-verbatim-string-literals"></a>일반 및 축자 문자열 리터럴  
 다음 예제와 같이 C#에서 제공하는 이스케이프 문자를 포함해야 하는 경우 일반 문자열 리터럴을 사용합니다.  
  
 [!code-csharp[csProgGuideStrings#3](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_4.cs)]  
  
 문자열 텍스트에 백슬래시 문자가 포함된 경우 가독성을 높이고 편의를 위해 축자 문자열을 사용합니다(예: 파일 경로). 축자 문자열에서는 문자열 텍스트의 일부로 줄 바꿈 문자가 유지되므로 여러 줄 문자열을 초기화하는 데 사용할 수 있습니다. 축자 문자열 내에 따옴표를 포함하려면 큰따옴표를 사용하세요. 다음 예제에서는 몇 가지 일반적인 축자 문자열에 대한 사용을 보여 줍니다.  
  
 [!code-csharp[csProgGuideStrings#4](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_5.cs)]  
  
## <a name="string-escape-sequences"></a>문자열 이스케이프 시퀀스  
  
|이스케이프 시퀀스|문자 이름|유니코드 인코딩|  
|---------------------|--------------------|----------------------|  
|\\'|작은따옴표|0x0027|  
|\\"|큰따옴표|0x0022|  
|\\\\ |백슬래시|0x005C|  
|\0|Null|0x0000|  
|\a|경고|0x0007|  
|\b|백스페이스|0x0008|  
|\f|폼 피드|0x000C|  
|\n|줄 바꿈|0x000A|  
|\r|캐리지 리턴|0x000D|  
|\t|가로 탭|0x0009|  
|\U|서로게이트 쌍의 경우 유니코드 이스케이프 시퀀스|\Unnnnnnnn|  
|\u|유니코드 이스케이프 시퀀스|\u0041 = "A"|  
|\v|세로 탭|0x000B|  
|\x|길이가 변하는 경우를 제외하고 "\u"와 유사한 유니코드 이스케이프 시퀀스합니다.|\x0041 = "A"|  
  
> [!NOTE]
>  컴파일 시 축자 문자열은 모두 동일한 이스케이프 시퀀스가 포함된 일반 문자열로 변환됩니다. 따라서 디버거 조사식 창에서 축자 문자열을 확인할 경우 소스 코드의 축자 버전이 아니라 컴파일러에 의해 추가된 이스케이프 문자가 나타납니다. 예를 들어 축자 문자열 @"C:\files.txt"는 조사식 창에 "c:\\\files.txt"로 나타납니다.  
  
## <a name="format-strings"></a>형식 문자열  
 형식 문자열은 콘텐츠가 런타임 시 동적으로 결정될 수 있는 문자열입니다. 정적 <xref:System.String.Format%2A> 메서드를 사용하고, 런타임 시 다른 값으로 바뀔 자리 표시자를 중괄호에 포함하여 형식 문자열을 만들 수 있습니다. 다음 예제에서는 형식 문자열을 사용하여 루프의 각 반복의 결과를 출력합니다.  
  
 [!code-csharp[csProgGuideStrings#26](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_6.cs)]  
  
 <xref:System.Console.WriteLine%2A> 메서드를 한 번 오버로드하면 형식 문자열을 매개 변수로 가져옵니다. 따라서 메서드에 대한 명시적 호출이 없어도 형식 문자열 리터럴을 포함할 수 있습니다. 그러나 <xref:System.Diagnostics.Trace.WriteLine%2A>은 형식 문자열이 아닌 문자열만 허용하므로, <xref:System.Diagnostics.Trace.WriteLine%2A> 메서드를 사용하여 Visual Studio **출력** 창에 디버그 출력을 표시할 경우에는 <xref:System.String.Format%2A> 메서드를 명시적으로 호출해야 합니다. 형식 문자열에 대한 자세한 내용은 [형식 서식 지정](../../../standard/base-types/formatting-types.md)을 참조하세요.  
  
## <a name="substrings"></a>부분 문자열  
 부분 문자열은 문자열에 포함된 임의의 문자 시퀀스입니다. 원래 문자열 일부에서 새 문자열을 만들려면 <xref:System.String.Substring%2A> 메서드를 사용하세요. <xref:System.String.IndexOf%2A> 메서드를 사용하면 부분 문자열 항목을 하나 이상 검색할 수 있습니다. 지정된 부분 문자열의 모든 항목을 새 문자열로 바꾸려면 <xref:System.String.Replace%2A> 메서드를 사용하세요. <xref:System.String.Substring%2A> 메서드와 마찬가지로, <xref:System.String.Replace%2A>는 실제로 새 문자열을 반환하며, 원래 문자열은 수정되지 않습니다. 자세한 내용은 [방법: 문자열 검색](../../how-to/search-strings.md) 및 [방법: 문자열 내용 수정](../../how-to/modify-string-contents.md)을 참조하세요.  
  
 [!code-csharp[csProgGuideStrings#7](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_7.cs)]  
  
## <a name="accessing-individual-characters"></a>개별 문자 액세스  
 다음 예제와 같이 인덱스 값이 있는 배열 표기법을 사용하여 개별 문자에 대한 읽기 전용 액세스 권한을 얻을 수 있습니다.  
  
 [!code-csharp[csProgGuideStrings#9](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_8.cs)]  
  
 문자열에서 개별 문자를 수정해야 하는 기능이 <xref:System.String> 메서드에서 제공되지 않는 경우에는 <xref:System.Text.StringBuilder> 개체를 사용하여 개별 문자를 "현재 위치"에서 수정한 후 새 문자열을 만들어 <xref:System.Text.StringBuilder> 메서드로 결과를 저장할 수 있습니다. 다음 예제에서는 특정 방식으로 원래 문자열을 수정한 다음 나중에 사용할 수 있도록 결과를 저장해야 한다고 가정합니다.  
  
 [!code-csharp[csProgGuideStrings#8](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_9.cs)]  
  
## <a name="null-strings-and-empty-strings"></a>null 문자열 및 빈 문자열  
 빈 문자열은 문자가 포함되지 않은 <xref:System.String?displayProperty=nameWithType> 개체의 인스턴스입니다. 빈 문자열은 빈 텍스트 필드를 나타내는 다양한 프로그래밍 시나리오에서 자주 사용됩니다. 빈 문자열은 유효한 <xref:System.String?displayProperty=nameWithType> 개체이므로 빈 문자열에 대해 메서드를 호출할 수 있습니다. 빈 문자열은 다음과 같이 초기화됩니다.  
  
```  
string s = String.Empty;  
```  
  
 반면, null 문자열은 <xref:System.String?displayProperty=nameWithType> 개체의 인스턴스를 참조하지 않으므로 null 문자열에서 메서드를 호출하려고 하면 <xref:System.NullReferenceException>이 발생합니다. 그러나 다른 문자열과 연결 및 비교 작업에서는 null 문자열을 사용할 수 있습니다. 다음 예제에는 null 문자열에 대한 참조로 예외가 발생하거나 발생하지 않는 몇 가지 경우가 나와 있습니다.  
  
 [!code-csharp[csProgGuideStrings#27](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_10.cs)]  
  
## <a name="using-stringbuilder-for-fast-string-creation"></a>빠른 문자열 생성을 위한 StringBuilder 사용  
 .NET에서 문자열 작업은 고도로 최적화되어 있으므로 대부분의 경우 성능에 크게 영향을 주지 않습니다. 그러나 수백 번 또는 수천 번 실행하는 타이트 루프와 같은 일부 시나리오에서는 문자열 작업이 성능에 영향을 미칠 수 있습니다. 프로그램이 여러 문자열 조작을 수행하는 경우에는 <xref:System.Text.StringBuilder> 클래스에서 개선된 성능을 제공하는 문자열 버퍼를 만듭니다. <xref:System.Text.StringBuilder> 문자열을 사용하면 개별 문자를 다시 할당할 수도 있지만 기본 제공 문자열 데이터 형식을 지원하지는 않습니다. 예를 들어 이 코드는 새 문자열을 만들지 않고 문자열의 콘텐츠를 변경합니다.  
  
 [!code-csharp[csProgGuideStrings#20](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_11.cs)]  
  
 이 예제에서 <xref:System.Text.StringBuilder> 개체는 숫자 형식 집합에서 문자열을 만드는 데 사용됩니다.  
  
 [!code-csharp[csProgGuideStrings#15](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_12.cs)]  
  
## <a name="strings-extension-methods-and-linq"></a>문자열, 확장 메서드 및 LINQ  
 <xref:System.String> 형식이 <xref:System.Collections.Generic.IEnumerable%601>을 구현하므로 문자열에서 <xref:System.Linq.Enumerable> 클래스에 정의된 확장 메서드를 사용할 수 있습니다. 시각적인 혼란을 방지하기 위해 <xref:System.String> 형식의 경우 이러한 메서드가 IntelliSense에서 제외되지만, 제외되더라도 사용할 수는 있습니다. 문자열에서 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리 식을 사용할 수도 있습니다. 자세한 내용은 [LINQ 및 문자열](../../../csharp/programming-guide/concepts/linq/linq-and-strings.md)을 참조하세요.  
  
## <a name="related-topics"></a>관련 항목  
  
|항목|설명|  
|-----------|-----------------|  
|[방법: 문자열 내용 수정](../../how-to/modify-string-contents.md)|문자열을 변환하고 문자열의 내용을 수정하는 기술을 보여 줍니다.|  
|[방법: 문자열 비교](../../how-to/compare-strings.md)|문자열의 서수 및 문화권 비교를 수행하는 방법을 보여 줍니다.|  
|[방법: String.Split을 사용하여 문자열 구문 분석](../../how-to/parse-strings-using-split.md)|`String.Split` 메서드 문자열을 사용하여 문자열을 구문 분석하는 방법을 보여 주는 코드 예제가 포함되어 있습니다.|  
|[방법: 문자열 검색](../../how-to/search-strings.md)|문자열에서 특정 텍스트 또는 패턴에 대해 검색을 사용하는 방법을 설명합니다.|  
|[방법: 문자열이 숫자 값을 나타내는지 확인](../../../csharp/programming-guide/strings/how-to-determine-whether-a-string-represents-a-numeric-value.md)|문자열에 올바른 숫자 값이 있는지 여부를 확인할 수 있도록 문자열을 안전하게 구문 분석하는 방법을 보여 줍니다.|  
|[방법: 문자열을 DateTime으로 변환](../../../csharp/programming-guide/strings/how-to-convert-a-string-to-a-datetime.md)|"01/24/2008"과 같은 문자열을 <xref:System.DateTime?displayProperty=nameWithType> 개체로 변환하는 방법을 보여 줍니다.|  
|[기본적인 문자열 작업](../../../../docs/standard/base-types/basic-string-operations.md)|<xref:System.String?displayProperty=nameWithType> 및 <xref:System.Text.StringBuilder?displayProperty=nameWithType> 메서드를 사용하여 기본적인 문자열 작업을 수행하는 항목에 대한 링크를 제공합니다.|  
|[문자열 구문 분석](../../../../docs/standard/base-types/parsing-strings.md)|문자열에 문자 또는 공백을 삽입하는 방법을 설명합니다.|  
|[문자열 비교](../../../../docs/standard/base-types/comparing.md)|문자열을 비교하는 방법에 대한 정보가 포함되어 있으며, C# 및 Visual Basic의 예제를 제공합니다.|  
|[StringBuilder 클래스 사용](../../../standard/base-types/stringbuilder.md)|<xref:System.Text.StringBuilder> 클래스를 사용하여 동적 문자열 개체를 만들고 수정하는 방법을 설명합니다.|  
|[LINQ 및 문자열](../../../csharp/programming-guide/concepts/linq/linq-and-strings.md)|LINQ 쿼리를 사용하여 다양한 문자열 작업을 수행하는 방법에 대한 정보를 제공합니다.|  
|[C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)|C#에서 프로그래밍 구문을 설명하는 항목에 대한 링크를 제공합니다.|  
