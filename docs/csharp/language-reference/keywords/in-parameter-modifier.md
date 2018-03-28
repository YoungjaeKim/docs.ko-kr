---
title: in 매개 변수 한정자(C# 참조)
ms.date: 03/06/2018
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
helpviewer_keywords:
- parameters [C#], in
- in parameters [C#]
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 9b8b21e2bdc95829c831ee71f24b47986321b7d0
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/23/2018
---
# <a name="in-parameter-modifier-c-reference"></a>in 매개 변수 한정자(C# 참조)

`in` 키워드를 사용하면 참조를 통해 인수를 전달할 수 있습니다. `in` 인수는 호출된 메서드에서 수정될 수 없는 반면 `ref` 인수는 수정될 수 있다는 것을 제외하고 [ref](ref.md) 또는 [out](out-parameter-modifier.md) 키워드와 같습니다. `out` 인수는 호출자에서 수정되어야 하며 해당 수정 사항은 호출 컨텍스트에서 식별할 수 있습니다.

[!code-csharp-interactive[cs-in-keyword](../../../../samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/InParameterModifier.cs#1)]  

위 예제는 `in` 한정자가 호출 사이트에서 필요하지 않다는 것을 설명합니다. 메서드 선언에만 필요합니다.

> [!NOTE] 
> `in` 키워드는 `foreach` 명령문의 일부 또는 LINQ 쿼리에서 `join` 절의 일부로 형식 매개 변수가 반공변(contravariant)임을 지정하도록 제네릭 형식 매개 변수와 함께 사용될 수도 있습니다. 이러한 컨텍스트에서 `in` 키워드의 사용에 대한 자세한 내용은 모든 해당 사용에 대한 링크를 제공하는 [in](in.md)을 참조하세요.
  
 `in` 인수로 전달되는 변수는 메서드 호출에서 전달되기 전에 초기화되어야 합니다. 그러나 호출된 메서드는 값을 할당하거나 인수를 수정하지 않을 수 있습니다.  
  
 `in`, `ref` 및 `out` 키워드는 서로 다른 런타임 동작을 수행하지만 컴파일 시간에 메서드 시그니처의 일부로 간주되지는 않습니다. 따라서 메서드 하나는 `ref` 또는 `in` 인수를 사용하고 다른 하나는 `out` 인수를 사용한다는 것 외에는 차이점이 없으면 메서드를 오버로드할 수 없습니다. 예를 들어 다음 코드는 컴파일되지 않습니다.  
  
```csharp
class CS0663_Example
{
    // Compiler error CS0663: "Cannot define overloaded 
    // methods that differ only on in, ref and out".
    public void SampleMethod(in int i) { }
    public void SampleMethod(ref int i) { }
}
```
  
`in`의 존재 여부에 따른 오버로드는 허용되지만 컴파일러 경고를 생성합니다.  
  
```csharp
class InOverloads
{
    // Discouraged. Calling SampleMethod(value) is ambiguous.
    public void SampleMethod(in int i) { }
    public void SampleMethod(int i) { }
}
```

속성 또는 상수는 호출 메서드가 해당 값을 수정할 수 없으므로 `in` 매개 변수로 전달될 수 있습니다.
  
다음과 같은 종류의 메서드에는 `in`, `ref` 및 `out` 키워드를 사용할 수 없습니다.  
  
- [async](../../../csharp/language-reference/keywords/async.md) 한정자를 사용하여 정의하는 비동기 메서드  
  
- [yield return](../../../csharp/language-reference/keywords/yield.md) 또는 `yield break` 문을 포함하는 반복기 메서드  

일반적으로 값으로 인수 전달에 필요한 복사 작업을 방지하도록 `in` 인수를 선언합니다. 이는 인수가 복사 작업이 참조로 전달하는 것보다 비용이 많이 드는 구조와 같은 값 유형인 경우에 가장 유용합니다.

> [!WARNING]
>  `in` 매개 변수는 오용되면 더 비쌀 수 있습니다. 컴파일러는 멤버 메서드가 구조체의 상태를 수정하는지 여부를 알 수 없습니다. 컴파일러가 객체가 수정되지 않았는지 여부를 확인할 수 없으면 방어적으로 복사본을 만들고 해당 복사본을 사용하여 멤버 참조를 호출합니다. 모든 가능한 수정은 해당 방어 복사본에 대한 것입니다. 이러한 복사본을 피하는 두 가지 방법은 `in` 매개 변수를 `in` 인수로 전달하거나 구조를 `readonly struct`으로 정의하는 것입니다.

## <a name="c-language-specification"></a>C# 언어 사양  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [C# 참조](../../../csharp/language-reference/index.md)  
 [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
 [C# 키워드](../../../csharp/language-reference/keywords/index.md)  
 [메서드 매개 변수](../../../csharp/language-reference/keywords/method-parameters.md)  
 [값 형식과 참조 의미 체계](../../../csharp/reference-semantics-with-value-types.md)
