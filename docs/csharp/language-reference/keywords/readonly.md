---
title: "readonly(C# 참조)"
ms.date: 07/20/2015
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- readonly_CSharpKeyword
- readonly
helpviewer_keywords:
- readonly keyword [C#]
ms.assetid: 2f8081f6-0de2-4903-898d-99696c48d2f4
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 175eebf6e49e79db1ff86689599416a10827a792
ms.sourcegitcommit: 83dd5ec003e788ccb3e33f3412a7af39ae347646
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="readonly-c-reference"></a>readonly(C# 참조)
`readonly` 키워드는 필드에 사용할 수 있는 한정자입니다. 필드 선언에 `readonly` 한정자가 포함되어 있는 경우 선언에 의해 추가된 필드에 대한 할당은 선언의 일부로서 또는 같은 클래스의 생성자에서만 발생할 수 있습니다.  
  
## <a name="readonly-field-example"></a>읽기 전용 필드 예제  
 이 예제에서는 클래스 생성자에서 값이 할당되지만, `year` 필드의 값을 `ChangeYear` 메서드에서 변경할 수 없습니다.  
  
 [!code-csharp[csrefKeywordsModifiers#14](../../../csharp/language-reference/keywords/codesnippet/CSharp/readonly_1.cs)]  
  
 다음 컨텍스트에서만 `readonly` 필드에 값을 할당할 수 있습니다.  
  
-   변수가 선언에서 초기화될 때. 예를 들면 다음과 같습니다.  
  
    ```  
    public readonly int y = 5;  
    ```  
  
-   인스턴스 필드의 경우 필드 선언이 포함된 클래스의 인스턴스 생성자에서, 또는 정적 필드의 경우 필드 선언이 포함된 클래스의 정적 생성자에서. `readonly` 필드를 [out](../../../csharp/language-reference/keywords/out-parameter-modifier.md) 또는 [ref](../../../csharp/language-reference/keywords/ref.md)로 전달하는 것이 유효한 컨텍스트는 이러한 경우뿐입니다.  
  
> [!NOTE]
>  `readonly` 키워드와 [const](../../../csharp/language-reference/keywords/const.md) 키워드와 다릅니다. `const` 필드는 필드 선언에서만 초기화될 수 있습니다. `readonly` 필드는 선언이나 생성자에서 초기화될 수 있습니다. 따라서 `readonly` 필드는 사용된 생성자에 따라 다른 값을 가질 수 있습니다. 또한 `const` 필드는 컴파일 시간 상수인 반면, `readonly` 필드는 다음 예제와 같이 런타임 상수에 사용될 수 있습니다.  
  
```  
public static readonly uint timeStamp = (uint)DateTime.Now.Ticks;  
```  
  
## <a name="comparing-readonly-and-non-readonly-instance-fields"></a>읽기 전용과 읽기 전용이 아닌 인스턴스 필드 비교  
 [!code-csharp[csrefKeywordsModifiers#15](../../../csharp/language-reference/keywords/codesnippet/CSharp/readonly_2.cs)]  
  
 위의 예제에서 다음과 같은 문을 사용하는 경우  
  
 `p2.y = 66;        // Error`  
  
 컴파일러 오류 메시지가 표시됩니다.  
  
 `The left-hand side of an assignment must be an l-value`  
  
 상수에 값을 할당하려고 할 때 표시되는 것과 같은 오류입니다.  
  
## <a name="c-language-specification"></a>C# 언어 사양  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [C# 참조](../../../csharp/language-reference/index.md)  
 [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
 [C# 키워드](../../../csharp/language-reference/keywords/index.md)  
 [한정자](../../../csharp/language-reference/keywords/modifiers.md)  
 [const](../../../csharp/language-reference/keywords/const.md)  
 [필드](../../../csharp/programming-guide/classes-and-structs/fields.md)
