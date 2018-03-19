---
title: "인덱서 사용(C# 프로그래밍 가이드)"
ms.date: 07/20/2015
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
helpviewer_keywords:
- indexers [C#], about indexers
ms.assetid: df70e1a2-3ce3-4aba-ad80-4b2f3538699f
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 17bbfabe8a53fc51e81434d0a2bd9fb2b29c4695
ms.sourcegitcommit: 83dd5ec003e788ccb3e33f3412a7af39ae347646
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="using-indexers-c-programming-guide"></a>인덱서 사용(C# 프로그래밍 가이드)
인덱서는 클라이언트 응용 프로그램이 배열처럼 액세스할 수 있는 [class](../../../csharp/language-reference/keywords/class.md), [struct](../../../csharp/language-reference/keywords/struct.md), [interface](../../../csharp/language-reference/keywords/interface.md)를 만들 수 있게 해주는 편리한 구문입니다. 인덱서는 내부 컬렉션 또는 배열을 캡슐화하는 데 주로 사용되는 형식에서 자주 구현됩니다. 예를 들어 24시간 동안 10회 기록된 화씨온도를 나타내는 TempRecord라는 클래스가 있다고 가정합니다. 이 클래스에는 온도를 나타내는 float 형식의 “temps” 배열과 온도가 기록된 날짜를 나타내는 <xref:System.DateTime>이 포함되어 있습니다. 이 클래스에서 인덱서를 구현하면 클라이언트가 TempRecord 인스턴스의 온도에 `float temp = tr.temps[4]` 대신 `float temp = tr[4]`로 액세스할 수 있습니다. 인덱서 표기법은 클라이언트 응용 프로그램에 대한 구문을 간소화할 뿐 아니라 클래스와 해당 용도를 다른 개발자가 이해하기 쉽게 만듭니다.  
  
 클래스 또는 구조체에서 인덱서를 선언하려면 다음 예제와 같이 [this](../../../csharp/language-reference/keywords/this.md) 키워드를 사용합니다.  
  
```  
public int this[int index]    // Indexer declaration  
{  
    // get and set accessors  
}  
```  
  
## <a name="remarks"></a>설명  
 인덱서의 형식과 해당 매개 변수의 형식은 최소한 인덱서 자체만큼 액세스 가능해야 합니다. 접근성 수준에 대한 자세한 내용은 [액세스 한정자](../../../csharp/language-reference/keywords/access-modifiers.md)를 참조하세요.  
  
 인터페이스와 함께 인덱서를 사용하는 방법에 대한 자세한 내용은 [인터페이스 인덱서](../../../csharp/programming-guide/indexers/indexers-in-interfaces.md)를 참조하세요.  
  
 인덱서의 시그니처는 정식 매개 변수의 형식 및 개수로 구성됩니다. 정식 매개 변수의 이름이나 인덱서 형식은 포함되지 않습니다. 동일한 클래스에서 둘 이상의 인덱서를 선언하는 경우 다른 시그니처가 있어야 합니다.  
  
 인덱서 값은 변수로 분류되지 않으므로 인덱서 값을 [ref](../../../csharp/language-reference/keywords/ref.md) 또는 [out](../../../csharp/language-reference/keywords/out-parameter-modifier.md) 매개 변수로 전달할 수 없습니다.  
  
 다른 언어에서 사용할 수 있는 이름을 인덱서에 제공하려면 선언에 `name` 특성을 사용합니다. 예:  
  
```  
[System.Runtime.CompilerServices.IndexerName("TheItem")]  
public int this [int index]   // Indexer declaration  
{  
}  
```  
  
 이 인덱서의 이름은 `TheItem`입니다. 이름 특성을 제공하지 않을 경우 기본 이름은 `Item`입니다.  
  
## <a name="example-1"></a>예제 1  
  
### <a name="description"></a>설명  
 다음 예제에서는 전용 배열 필드, `temps`, 인덱서를 선언하는 방법을 보여 줍니다. 인덱서를 사용하면 `tempRecord[i]` 인스턴스에 직접 액세스할 수 있습니다. 인덱서를 사용하지 않으려면 배열을 [public](../../../csharp/language-reference/keywords/public.md) 멤버로 선언하고 해당 멤버인 `tempRecord.temps[i]`에 직접 액세스합니다.  
  
 인덱서의 액세스가 `Console.Write` 문 등에서 평가될 때 [get](../../../csharp/language-reference/keywords/get.md) 접근자가 호출됩니다. 따라서 `get` 접근자가 없으면 컴파일 시간 오류가 발생합니다.  
  
### <a name="code"></a>코드  
 [!code-csharp[csProgGuideIndexers#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-indexers_1.cs)]  
  
## <a name="indexing-using-other-values"></a>다른 값을 사용하여 인덱싱  
 C#에서는 인덱스 형식이 정수로 제한되지 않습니다. 예를 들어 인덱서와 함께 문자열을 사용하면 유용할 수 있습니다. 이러한 인덱서는 컬렉션에서 문자열을 검색하고 적절한 값을 반환하여 구현할 수 있습니다. 접근자를 오버로드할 수 있기 때문에 문자열 및 정수 버전이 공존할 수 있습니다.  
  
## <a name="example-2"></a>예제 2  
  
### <a name="description"></a>설명  
 이 예제에서는 요일을 저장하는 클래스를 선언합니다. 문자열인 요일 이름을 사용하고 해당 정수를 반환하는 `get` 접근자가 선언됩니다. 예를 들어 일요일이면 0을 반환하고, 월요일이면 1을 반환합니다.  
  
### <a name="code"></a>코드  
 [!code-csharp[csProgGuideIndexers#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-indexers_2.cs)]  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 인덱서의 보안과 안정성을 향상할 수 있는 다음 두 가지 방법이 있습니다.  
  
-   클라이언트 코드에서 잘못된 인덱스 값을 전달할 가능성을 처리하는 일부 유형의 오류 처리 전략을 통합해야 합니다. 이 항목의 앞부분에 있는 첫 번째 예제에서 TempRecord 클래스는 클라이언트 코드에서 입력을 인덱서에 전달하기 전에 확인할 수 있게 해주는 Length 속성을 제공합니다. 인덱서 자체 안에 오류 처리 코드를 넣을 수도 있습니다. 사용자를 위해 인덱서 접근자 내에서 throw하는 모든 예외를 문서화해야 합니다.  
  
-   `get` 및 [set](../../../csharp/language-reference/keywords/set.md) 접근자의 접근성을 적절하게 제한적으로 설정합니다. 특히 `set` 접근자의 경우 이 작업이 중요합니다. 자세한 내용은 [접근자 액세스 가능성 제한](../../../csharp/programming-guide/classes-and-structs/restricting-accessor-accessibility.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
 [인덱서](../../../csharp/programming-guide/indexers/index.md)  
 [속성](../../../csharp/programming-guide/classes-and-structs/properties.md)
