---
title: ref(C# 참조)
ms.date: 03/06/2018
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- ref_CSharpKeyword
- ref
helpviewer_keywords:
- parameters [C#], ref
- ref keyword [C#]
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 63f984f4004cfce9694e7e7405ec2477bc370731
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/23/2018
---
# <a name="ref-c-reference"></a>ref(C# 참조)

`ref` 키워드는 참조로 전달되는 값을 나타냅니다. 다음 세 가지 컨텍스트에서 사용됩니다. 

- 메서드 시그니처 및 메서드 호출에서 인수를 메서드에 참조로 전달합니다. 자세한 내용은 [참조로 인수 전달](#passing-an-argument-by-reference)을 참조하세요.

- 메서드 시그니처에서 값을 호출자에게 참조로 반환합니다. 자세한 내용은 [참조 반환 값](#reference-return-values)을 참조하세요.

- 멤버 본문에서 참조 반환 값이 호출자가 수정하려는 참조로 로컬에 저장되거나 일반적으로 로컬 변수가 참조를 기준으로 다른 값에 액세스 함을 나타냅니다. 자세한 내용은 [참조 로컬](#ref-locals)을 참조하세요.

## <a name="passing-an-argument-by-reference"></a>참조로 인수 전달

메서드의 매개 변수 목록에 사용되는 경우 `ref` 키워드는 인수가 값이 아니라 참조로 전달됨을 나타냅니다. 인수를 참조로 전달하는 경우 호출된 메서드의 인수 변경 내용이 호출 메서드에 반영됩니다. 예를 들어 호출자가 지역 변수 식 또는 배열 요소 액세스 식을 전달하는 경우 호출된 메서드에서 ref 매개 변수가 참조하는 개체를 바꾸면 메서드 반환 시 호출자의 지역 변수 또는 배열 요소가 새 개체를 참조합니다.

> [!NOTE]
>  참조로 전달의 개념과 참조 형식의 개념을 혼동해서는 안 됩니다. 이 두 개념은 서로 다릅니다. 메서드 매개 변수는 값 형식이든 참조 형식이든 관계없이 `ref`를 통해 수정할 수 있으며, 참조로 전달되는 경우 값 형식은 boxing되지 않습니다.  

`ref` 매개 변수를 사용하려면 다음 예제에 나와 있는 것처럼 메서드 정의와 호출 메서드가 모두 `ref` 키워드를 명시적으로 사용해야 합니다.  

[!code-csharp-interactive[csrefKeywordsMethodParams#6](../../../../samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#1)]

`ref` 또는 `in` 매개 변수로 전달하는 인수는 전달 전에 초기화해야 합니다. 이러한 방식은 인수를 전달하기 전에 명시적으로 초기화할 필요가 없는 [out](out-parameter-modifier.md) 매개 변수와는 다릅니다.

클래스의 멤버는 `ref`, `in` 또는 `out`만 다른 서명을 포함할 수 없습니다. 특정 형식의 두 멤버가 하나는 `ref` 매개 변수를 포함하고 다른 하나는 `out` 또는 `in` 매개 변수를 포함한다는 것 외에는 차이가 없으면 컴파일러 오류가 발생합니다. 예를 들어 다음 코드는 컴파일되지 않습니다.  

```csharp
class CS0663_Example
{
    // Compiler error CS0663: "Cannot define overloaded 
    // methods that differ only on ref and out".
    public void SampleMethod(out int i) { }
    public void SampleMethod(ref int i) { }
}
```
그러나 다음 예제에 나와 있는 것처럼 메서드 하나에는 `ref`, `in` 또는 `out` 매개 변수가 포함되어 있고 다른 하나에는 값 매개 변수가 포함되어 있으면 메서드를 오버로드할 수 있습니다.
  
[!code-csharp[csrefKeywordsMethodParams#6](../../../../samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#2)]
  
 숨기기나 재정의와 같이 서명이 일치해야 하는 다른 상황에서는 `in`, `ref` 및 `out`이 서명의 일부가 되며 서로 일치하지 않습니다.  
  
 속성은 변수가 아니라 메서드이며 `ref` 매개 변수로 전달할 수 없습니다.  
  
 배열 전달 방법에 대한 자세한 내용은 [ref 및 out을 사용하여 배열 전달](../../../csharp/programming-guide/arrays/passing-arrays-using-ref-and-out.md)을 참조하세요.  
  
 다음과 같은 종류의 메서드에는 `ref`, `in` 및 `out` 키워드를 사용할 수 없습니다.  
  
- [async](../../../csharp/language-reference/keywords/async.md) 한정자를 사용하여 정의하는 비동기 메서드  
- [yield return](../../../csharp/language-reference/keywords/yield.md) 또는 `yield break` 문을 포함하는 반복기 메서드  

## <a name="passing-an-argument-by-reference-an-example"></a>참조로 인수 전달: 예제

앞의 예제에서는 값 형식을 참조로 전달합니다. `ref` 키워드를 사용하여 참조 형식을 참조로 전달할 수도 있습니다. 참조 형식을 참조로 전달하는 경우 호출된 메서드는 참조 매개 변수가 호출자에서 참조하는 개체를 바꿀 수 있습니다. 개체의 저장 위치는 참조 매개 변수의 값으로 메서드에 전달됩니다. 매개 변수의 저장 위치에서 값을 변경하여 새 개체를 가리키도록 하면 호출자가 참조하는 저장 위치도 변경됩니다. 다음 예제에서는 참조 형식 인스턴스를 `ref` 매개 변수로 전달합니다.   
  
[!code-csharp[csrefKeywordsMethodParams#6](../../../../samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#3)]

참조 형식을 참조 및 값으로 전달하는 방법에 대한 자세한 내용은 [참조-형식 매개 변수 전달](../../../csharp/programming-guide/classes-and-structs/passing-reference-type-parameters.md)을 참조하세요.
  
## <a name="reference-return-values"></a>참조 반환 값

참조 반환 값(또는 ref return)은 메서드가 호출자에게 참조로 반환하는 값입니다. 즉, 호출자가 메서드에서 반환된 값을 수정할 수 있으며 해당 변경 내용이 메서드를 포함하는 개체의 상태에 반영됩니다. 

참조 반환 값은 `ref` 키워드를 사용하여 정의됩니다.

- 메서드 시그니처에서. 예를 들어 다음 메서드 시그니처는 `GetCurrentPrice` 메서드가 <xref:System.Decimal> 값을 참조로 반환함을 나타냅니다.

   ```csharp
   public ref decimal GetCurrentValue()
   ``` 
- 메서드의 `return` 문에서 반환된 `return` 토큰과 변수 간에. 예:
 
   ```csharp
   return ref DecimalArray[0];
   ``` 

호출자가 개체 상태를 수정하려면 참조 반환 값을 [참조 로컬](#ref-locals)로 명시적으로 정의된 변수에 저장해야 합니다. 

예를 들어 [참조 반환 및 참조 로컬 예제](#a-ref-returns-and-ref-locals-example)를 참조하세요.

## <a name="ref-locals"></a>참조 로컬

참조 지역 변수는 `return ref`을 사용하여 반환된 값을 참조하는 데 사용됩니다.  참조 지역 변수를 초기화하고 참조 반환 값에 할당해야 합니다. 참조 로컬 값의 수정 내용은 메서드가 값을 참조로 반환하는 개체 상태에 반영됩니다.

변수 선언 앞, 값을 참조로 반환하는 메서드 호출 직전에 `ref` 키워드를 사용하여 참조 로컬을 정의합니다. 

예를 들어 다음 문은 `GetEstimatedValue` 메서드에서 반환되는 참조 로컬 값을 정의합니다.

```csharp
ref decimal estValue = ref Building.GetEstimatedValue();
```

동일한 방법으로 참조로 값에 액세스할 수 있습니다. 경우에 따라 참조로 값에 액세스하면 비용이 많이 들 수 있는 복사 작업을 피함으로써 성능이 향상됩니다. 예를 들어, 다음 명령문은 값을 참조하는 데 사용되는 참조 로컬 값을 정의하는 방법을 보여줍니다.

```csharp
ref VeryLargeStruct reflocal = ref veryLargeStruct;
```

두 예에서 `ref` 키워드는 두 위치에 모두 사용해야 합니다. 그렇지 않으면 컴파일러 오류 CS8172, "값을 사용하여 참조 형식 변수를 초기화할 수 없습니다."가 생성됩니다. 
 
## <a name="a-ref-returns-and-ref-locals-example"></a>참조 반환 및 참조 로컬 예제

다음 예제에서는 두 개의 <xref:System.String> 필드 `Title` 및 `Author`가 있는 `Book` 클래스를 정의합니다. 또한 `Book` 개체의 private 배열을 포함하는 `BookCollection` 클래스를 정의합니다. 개별 책 개체는 해당 `GetBookByTitle` 메서드를 호출하여 참조로 반환됩니다.

[!code-csharp[csrefKeywordsMethodParams#6](../../../../samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#4)]

호출자가 `GetBookByTitle` 메서드에서 참조 로컬로 반환된 값을 저장하는 경우 호출자가 반환 값을 변경하면 다음 예제와 같이 `BookCollection` 개체에 변경 내용이 반영됩니다.

[!code-csharp[csrefKeywordsMethodParams#6](../../../../samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#5)]

## <a name="c-language-specification"></a>C# 언어 사양  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [C# 참조](../../../csharp/language-reference/index.md)  
 [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
 [매개 변수 전달](../../../csharp/programming-guide/classes-and-structs/passing-parameters.md)  
 [메서드 매개 변수](../../../csharp/language-reference/keywords/method-parameters.md)  
 [C# 키워드](../../../csharp/language-reference/keywords/index.md)
