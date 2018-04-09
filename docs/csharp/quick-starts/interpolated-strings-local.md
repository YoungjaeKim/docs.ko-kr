---
title: 보간된 문자열 자습서 - C# 로컬 빠른 시작
description: 보간된 문자열에 관한 이 빠른 시작에서는 더 큰 문자열에 식의 결과를 포함하는 C# 코드를 작성합니다.
author: rpetrusha
ms.author: ronpet
ms.date: 01/11/2018
ms.topic: get-started-article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.custom: mvc
ms.openlocfilehash: 1edd2b9f59d1933547c4152343f226a86ad90216
ms.sourcegitcommit: 935d5267c44f9bce801468ef95f44572f1417e8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="interpolated-strings"></a>보간된 문자열

이 빠른 시작에서는 C#에서 보간된 문자열을 사용하여 단일 출력 문자열에 값을 삽입하는 방법을 설명합니다. C# 코드를 작성하고 컴파일 및 실행 결과를 확인합니다. 이 빠른 시작은 문자열에 값을 삽입하고, 이러한 값을 다양한 방식으로 서식화하는 일련의 단원으로 구성됩니다.

이 빠른 시작에서는 개발에 사용할 수 있는 컴퓨터가 있다고 예상합니다. .NET 항목 [Get Started in 10 minutes](https://www.microsoft.com/net/core)(10분 안에 시작)에는 Mac, PC 또는 Linux의 로컬 개발 환경 설정에 대한 지침이 포함되어 있습니다. 사용할 명령에 대한 간단한 개요는 [로컬 빠른 시작 소개](local-environment.md)에 나와 있으며, 이 소개에는 자세한 정보에 대한 링크도 함께 있습니다. 

## <a name="create-an-interpolated-string"></a>보간된 문자열 만들기

**interpolated-quickstart**라는 디렉터리를 만듭니다. 현재 디렉터리로 만들고 콘솔 창에서 다음 명령을 실행합니다.

```console
dotnet new console -n interpolated -o .
```

이 명령은 현재 디렉터리에 새 .NET Core 콘솔 응용 프로그램을 만듭니다.

원하는 편집기에서 **Program.cs**를 열고 `Console.WriteLine("Hello World!");` 줄을 다음 코드로 바꿉니다. 여기서 `<name>`을 사용자 이름으로 바꿉니다.

```csharp
var name = "<name>";
Console.WriteLine($"Hello, {name}. It's a pleasure to meet you!");
```
콘솔 창에 `dotnet run`을 입력하여 이 코드를 사용해 봅니다. 프로그램을 실행하면 인사말에 사용자 이름이 포함된 단일 문자열이 표시됩니다. <xref:System.Console.WriteLine%2A> 메서드 호출에 포함된 문자열은 *보간된 문자열*입니다. 이는 포함 코드가 들어있는 문자열에서 단일 문자열(*결과 문자열*이라고 함)을 생성할 수 있게 해주는 일종의 템플릿입니다. 보간된 문자열은 문자열에 값을 삽입하거나 문자열을 연결(함께 조인)하는 데 특히 유용합니다. 
    
다음 간단한 예제에서는 모든 보간된 문자열이 포함해야 하는 두 가지 요소를 보여 줍니다. 

- `$` 문자로 시작한 후 여는 따옴표 문자가 다음에 나오는 문자열 리터럴. `$` 기호와 따옴표 문자 사이에는 공백이 없어야 합니다. (공백을 포함하면 어떻게 되는지 확인하려면 `$` 문자 뒤에 공백을 삽입하고 파일을 저장한 후 콘솔 창에 `dotnet run`을 입력하여 프로그램을 다시 실행합니다. C# 컴파일러가 "오류 CS1056: 예기치 않은 문자 '$'"라는 오류 메시지를 표시합니다.) 

- 하나 이상의 *보간된 식*. 보간된 식은 열기 및 닫기 중괄호(`{` 및 `}`)로 표시됩니다. 중괄호 안에 값을 반환(`null` 포함)하는 C# 식을 배치할 수 있습니다. 

몇 가지 다른 데이터 형식을 포함하는 보간된 문자열 예제를 더 살펴보겠습니다.
    
## <a name="include-different-data-types"></a>다양한 데이터 형식 포함

이전 섹션에서는 한 문자열을 다른 문자열 내에 삽입하는 데 보간된 문자열을 사용했습니다. 하지만 보간된 문자열 식은 모든 데이터 형식일 수 있습니다. 여러 데이터 형식의 값을 포함하는 보간된 문자열을 살펴보겠습니다. 
    
다음 예제에서는 `Vegetable` 개체, `Unit` 열거형의 멤버, <xref:System.DateTime> 값 및 <xref:System.Decimal> 값이 있는 보간된 식을 포함합니다. 편집기에서 모든 C# 코드를 다음 코드로 바꾼 후 `console run` 명령을 사용하여 실행합니다.

```csharp
using System;

public class Vegetable
{
   public Vegetable(string name) => Name = name;
   
   public string Name { get; }
   
   public override string ToString() => Name;
}

public class Example
{
   public enum Unit { item, pound, ounce, dozen };
   
   public static void Main()
   {
      var item = new Vegetable("eggplant");
      var date = DateTime.Now;
      var price = 1.99m;
      var unit = Unit.item;
      Console.WriteLine($"On {date}, the price of {item} was {price} per {unit}.");
   }
}
```
    
두 번째 보간된 식에는 콘솔에 표시되는 결과 문자열의 `item` 개체가 포함되며, 이 경우 "eggplant"가 결과 문자열에 삽입됩니다. 보간된 식의 형식이 문자열이 아닌 경우 C# 컴파일러가 다음을 수행하기 때문입니다.

- 보간된 식이 `null`이면 보간된 식은 빈 문자열("" 또는 <xref:System.String.Empty?displayProperty=nameWithType>)을 반환합니다.

- 보간된 식이 `null`이 아닌 경우, 보간된 식 형식의 `ToString` 메서드가 호출됩니다. `Vegetable.ToString` 메서드 정의 앞에 주석 기호(`//`)를 넣어 정의를 주석 처리하여 테스트할 수 있습니다. 출력에서 "eggplant" 문자열은 형식 이름 "Vegetable"로 바뀌며 이것이 <xref:System.Object.ToString?displayProperty=nameWithType> 메서드의 기본 동작입니다.   

이 예제의 출력에서 날짜는 매우 정확하며(eggplant 가격은 초마다 달라지지 않음), 가격 값은 통화 단위를 나타내지 않습니다. 다음 섹션에서는 보간된 식에서 반환된 문자열 형식을 제어하여 해당 문제를 해결하는 방법을 알아봅니다.

## <a name="control-the-formatting-of-interpolated-expressions"></a>보간된 식의 서식 제어

이전 섹션에서는 형식이 잘못 지정된 두 개의 문자열을 결과 문자열에 삽입했습니다. 하나는 날짜만 적절한 날짜 및 시간 값이었습니다. 두 번째는 통화 단위를 나타내지 않는 가격이었습니다. 두 가지 문제는 쉽게 해결할 수 있습니다. 보간된 식은 특정 형식의 서식을 제어하는 *형식 문자열*을 포함할 수 있습니다. 다음 줄에 표시된 것처럼 이전 예제의 `Console.WriteLine`에 대한 호출을 수정하여 날짜 및 가격 필드의 형식 지정자를 포함시킵니다.

```csharp
Console.WriteLine($"On {date:d}, the price of {item} was {price:C2} per {unit}.");
```
    
콜론과 형식 문자열을 사용하여 보간된 식에 따라 형식 문자열을 지정합니다. "d"는 간단한 날짜 형식을 나타내는 [표준 날짜 및 시간 형식 문자열](../../standard/base-types/standard-date-and-time-format-strings.md#the-short-date-d-format-specifier)입니다. "C2"는 소수점 뒤 두 자릿수를 포함하는 통화 값으로 숫자를 나타내는 [표준 숫자 형식 문자열](../../standard/base-types/standard-numeric-format-strings.md#the-currency-c-format-specifier)입니다.

.NET 표준 라이브러리의 많은 형식은 미리 정의된 형식 문자열 집합을 지원합니다. 여기에는 모든 숫자 형식과 날짜 및 시간 형식이 포함됩니다. 형식 문자열을 지원하는 형식의 전체 목록을 보려면 [.NET의 서식 지정 형식](../../standard/base-types/formatting-types.md) 문서의 [형식 문자열 및 .NET 클래스 라이브러리 형식](../../standard/base-types/formatting-types.md#stringRef)을 참조하세요. 모든 형식에서 형식 문자열 집합을 지원할 수 있으며, 기존 형식에 대한 사용자 지정 서식을 제공하는 사용자 지정 서식 확장을 개발할 수도 있습니다. <xref:System.ICustomFormatter> 구현을 제공한 사용자 지정 서식에 대한 자세한 내용은 [.NET의 서식 지정 형식](../../standard/base-types/formatting-types.md) 문서의 [ICustomFormatter를 사용한 사용자 지정 서식 지정](../../standard/base-types/formatting-types.md#custom-formatting-with-icustomformatter)을 참조하세요.

텍스트 편집기에서 형식 문자열을 수정하고, 변경할 때마다 프로그램을 다시 실행하여 날짜 및 시간의 서식과 숫자 값에 미치는 영향을 확인해 보세요. `{date:d}`의 "d"를 "t"(짧은 시간 형식 표시), "y"(연도 및 월 표시) 및 "yyyy"(연도를 4자리 숫자로 표시)로 변경합니다. `{price:C2}`의 "C2"를 "e"(지수 표기) 및 "F3"(소수점 뒤 세 자릿수의 숫자 값)으로 변경합니다.

서식을 제어하는 것 외에도, 보간된 식에서 반환된 문자열의 필드 너비와 문자열 맞춤을 제어할 수 있습니다. 다음 섹션에서 이 작업을 수행하는 방법을 알아봅니다.

## <a name="control-the-field-width-and-alignment-of-interpolated-expressions"></a>필드 너비와 보간된 식의 맞춤을 제어합니다.

일반적으로 보간된 식에서 반환된 문자열은 결과 문자열에 포함되며 선행 또는 후행 공백이 없습니다. 특히 데이터 집합을 사용하여 작업하는 경우에는 보간된 식을 사용하여 필드 너비와 해당 맞춤을 지정할 수 있습니다. 이것을 확인하려면 텍스트 편집기에서 모든 코드를 다음 코드로 바꾼 후 `console run`을 입력하여 프로그램을 실행합니다.
    
```csharp
using System;
using System.Collections.Generic;

public class Example
{
   public static void Main()
   {
      var titles = new Dictionary<string, string>();
      titles.Add("Doyle, Arthur Conan", "Hound of the Baskervilles, The");
      titles.Add("London, Jack", "Call of the Wild, The");
      titles.Add("Shakespeare, William", "Tempest, The");

      Console.WriteLine("Author and Title List");
      Console.WriteLine($"\n{"Author",-25}    {"Title",30}\n");
      foreach (var title in titles)
         Console.WriteLine($"{title.Key,-25}     {title.Value,30}");
   }
}
```
    
작성자의 이름은 왼쪽 맞춤되며 이들이 작성한 제목은 오른쪽 맞춤됩니다. 식 뒤에 쉼표(",")를 추가하고 필더 너비를 지정하여 맞춤을 지정합니다. 필드 너비가 양수이면 필드는 오른쪽 맞춤입니다.

```text
{expression, width}
```

필드 너비가 음수이면 필드는 왼쪽 맞춤입니다.

```text
{expression, -width}
```

다음 코드처럼 `{"Author",-25}` 및 `{title.Key,-25}` 보간된 식에서 음수 기호를 제거하고 예제를 다시 실행해 보세요.

```csharp
Console.WriteLine($"\n{"Author",25}    {"Title",30}\n");
foreach (var title in titles)
   Console.WriteLine($"{title.Key,25}     {title.Value,30}");
```

이때 작성자 정보는 오른쪽 맞춤입니다.

필드 너비 및 형식 문자열을 단일 보간된 식으로 결합할 수 있습니다. 필드 너비가 먼저 나오고 그 다음으로, 콜론 및 형식 문자열이 나옵니다. `Main` 메서드 내에 있는 모든 코드를 다음 코드로 바꾸면, 필드 너비가 정의된 세 가지 형식 지정된 문자열이 표시됩니다. 그런 다음 `dotnet run` 명령을 입력하여 프로그램을 실행합니다.

```csharp
Console.WriteLine($"{DateTime.Now,-20:d} Hour {DateTime.Now,-10:HH} {1063.342,15:N2} feet");
```
다음과 같은 출력을 얻을 수 있습니다.

```console
1/11/2018            Hour 09                1,063.34 feet
```

보간된 문자열 빠른 시작을 완료했습니다. 
    
자체 개발 환경에서 [배열 및 컬렉션](arrays-and-collections.md) 빠른 시작을 계속할 수 있습니다.

C# 참조의 [문자열 보간](../language-reference/tokens/interpolated.md) 토픽에서 보간된 문자열에 대해 자세히 알아볼 수 있습니다.
