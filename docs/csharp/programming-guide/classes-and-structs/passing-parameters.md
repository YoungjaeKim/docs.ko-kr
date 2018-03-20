---
title: "매개 변수 전달(C# 프로그래밍 가이드)"
ms.date: 07/20/2015
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
helpviewer_keywords:
- parameters [C#], passing
- passing parameters [C#]
- arguments [C#]
- methods [C#], passing parameters
- C# language, method parameters
ms.assetid: a5c3003f-7441-4710-b8b1-c79de77e0b77
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 34746c83f54ecc2f6e8125bcff1464a89f853e09
ms.sourcegitcommit: 83dd5ec003e788ccb3e33f3412a7af39ae347646
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="passing-parameters-c-programming-guide"></a>매개 변수 전달(C# 프로그래밍 가이드)
C#에서는 인수를 값 또는 참조로 매개 변수에 전달할 수 있습니다. 참조로 전달하면 함수 멤버, 메서드, 속성, 인덱서, 연산자 및 생성자가 매개 변수의 값을 변경하고 해당 변경 내용을 호출 환경에서 유지할 수 있습니다. 값 변경의 목적으로 매개 변수를 참조로 전달하려면 `ref` 또는 `out` 키워드를 사용합니다. 값을 변경하지 않고 복사 방지 목적으로 참조로 전달하려면 `in` 한정자를 사용합니다. 간단히 설명하기 위해 이 항목의 예제에서는 `ref` 키워드만 사용됩니다. `in`, `ref` 및 `out` 간의 차이점에 대한 자세한 내용은 [in](../../../csharp/language-reference/keywords/in-parameter-modifier.md), [ref](../../../csharp/language-reference/keywords/ref.md), [out](../../../csharp/language-reference/keywords/out-parameter-modifier.md) 및 [ref 및 out을 사용하여 배열 전달](../../../csharp/programming-guide/arrays/passing-arrays-using-ref-and-out.md)을 참조하세요.  
  
 다음 예제에서는 값 및 참조 매개 변수 간의 차이점을 보여 줍니다.  
  
 [!code-csharp[csProgGuideParameters#10](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/passing-parameters_1.cs)]  
  
 자세한 내용은 다음 항목을 참조하세요.  
  
-   [값 형식 매개 변수 전달](../../../csharp/programming-guide/classes-and-structs/passing-value-type-parameters.md)  
  
-   [참조 형식 매개 변수 전달](../../../csharp/programming-guide/classes-and-structs/passing-reference-type-parameters.md)  
  
## <a name="c-language-specification"></a>C# 언어 사양  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
 [메서드](../../../csharp/programming-guide/classes-and-structs/methods.md)
