---
title: "무명 메서드(C# 프로그래밍 가이드)"
ms.date: 07/20/2015
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
helpviewer_keywords:
- anonymous methods [C#]
- methods [C#], anonymous
- delegates [C#], anonymous methods
ms.assetid: a62441fa-f0a3-4acb-9aa6-93762a635275
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 96e78257c5aab84562cd8cdb336bb5a91ba59534
ms.sourcegitcommit: 83dd5ec003e788ccb3e33f3412a7af39ae347646
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="anonymous-methods-c-programming-guide"></a>무명 메서드(C# 프로그래밍 가이드)
2.0 이전의 C# 버전에서 [delegate](../../../csharp/language-reference/keywords/delegate.md)를 선언하는 유일한 방법은 [명명된 메서드](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md)를 사용하는 것이었습니다. C# 2.0에서는 무명 메서드가 도입되었고, C# 3.0 이상에서는 람다 식이 인라인 코드를 작성하는 기본 방법으로 무명 메서드를 대체합니다. 그러나 이 항목의 무명 메서드 관련 정보는 람다 식에도 적용됩니다. 무명 메서드가 람다 식에서 찾을 수 없는 기능을 제공하는 한 가지 경우가 있습니다. 무명 메서드를 사용하여 매개 변수 목록을 생략할 수 있습니다. 즉, 무명 메서드를 여러 시그니처를 가진 대리자로 변환할 수 있습니다. 람다 식에서는 이 작업이 불가능합니다. 람다 식에 대한 자세한 내용은 [람다 식](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)을 참조하세요.  
  
 무명 메서드를 만드는 것은 기본적으로 코드 블록을 대리자 매개 변수로 전달하는 방법 중 하나입니다. 다음 두 가지 예제를 살펴보세요.  
  
 [!code-csharp[csProgGuideDelegates#6](../../../csharp/programming-guide/delegates/codesnippet/CSharp/anonymous-methods_1.cs)]  
  
 [!code-csharp[csProgGuideDelegates#5](../../../csharp/programming-guide/delegates/codesnippet/CSharp/anonymous-methods_2.cs)]  
  
 무명 메서드를 사용하면 별도 메서드를 만들 필요가 없기 때문에 대리자를 인스턴스화하는 코딩 오버헤드가 줄어듭니다.  
  
 예를 들어 메서드를 만드는 것이 불필요한 오버헤드처럼 보일 수도 있는 경우 대리자 대신 코드 블록을 지정하는 것이 유용할 수 있습니다. 좋은 예로 새 스레드를 시작하는 경우를 들 수 있습니다. 이 클래스는 스레드를 만들며, 대리자에 대한 추가 메서드를 만들지 않고 스레드에서 실행하는 코드도 포함합니다.  
  
 [!code-csharp[csProgGuideDelegates#7](../../../csharp/programming-guide/delegates/codesnippet/CSharp/anonymous-methods_3.cs)]  
  
## <a name="remarks"></a>설명  
 무명 메서드의 매개 변수 범위는 *무명 메서드 블록*입니다.  
  
 대상이 블록 외부에 있을 경우 [goto](../../../csharp/language-reference/keywords/goto.md), [break](../../../csharp/language-reference/keywords/break.md), [continue](../../../csharp/language-reference/keywords/continue.md) 등의 점프 문을 무명 메서드 블록 내부에 사용하는 것은 오류입니다. 대상이 블록 내부에 있을 경우 `goto`, `break`, `continue` 등의 점프 문을 무명 메서드 블록 외부에 사용하는 것도 오류입니다.  
  
 범위에 무명 메서드 선언이 포함된 지역 변수 및 매개 변수를 무명 메서드의 *외부* 변수라고 합니다. 예를 들어 다음 코드 세그먼트에서 `n`은 외부 변수입니다.  
  
 [!code-csharp[csProgGuideDelegates#8](../../../csharp/programming-guide/delegates/codesnippet/CSharp/anonymous-methods_4.cs)]  
  
 외부 변수 `n`에 대한 참조는 대리자를 만들 때 *캡처*됩니다. 지역 변수와 달리 캡처된 변수의 수명은 무명 메서드를 참조하는 대리자가 가비지 수집에 적격할 때까지 연장됩니다.  
  
 무명 메서드는 외부 범위의 [in](../../../csharp/language-reference/keywords/in.md), [ref](../../../csharp/language-reference/keywords/ref.md) 또는 [out](../../../csharp/language-reference/keywords/out-parameter-modifier.md) 매개 변수에 액세스할 수 없습니다.  
  
 안전하지 않은 코드는 *무명 메서드 블록* 내에서 액세스할 수 없습니다.  
  
 [is](../../../csharp/language-reference/keywords/is.md) 연산자의 왼쪽에는 무명 메서드를 사용할 수 없습니다.  
  
## <a name="example"></a>예  
 다음 예제에서는 대리자를 인스턴스화하는 다음 두 가지 방법을 보여 줍니다.  
  
-   무명 메서드에 대리자 연결  
  
-   명명된 메서드(`DoWork`)에 대리자 연결  
  
 각각의 경우 대리자를 호출할 때 메시지가 표시됩니다.  
  
 [!code-csharp[csProgGuideDelegates#4](../../../csharp/programming-guide/delegates/codesnippet/CSharp/anonymous-methods_5.cs)]  
  
## <a name="see-also"></a>참고 항목  
 [C# 참조](../../../csharp/language-reference/index.md)  
 [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
 [대리자](../../../csharp/programming-guide/delegates/index.md)  
 [람다 식](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)  
 [안전하지 않은 코드 및 포인터](../../../csharp/programming-guide/unsafe-code-pointers/index.md)  
 [메서드](../../../csharp/programming-guide/classes-and-structs/methods.md)  
 [명명된 메서드 및 무명 메서드가 있는 대리자](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md)
