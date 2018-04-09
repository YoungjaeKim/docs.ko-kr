---
title: 메서드 매개 변수(C# 참조)
ms.date: 07/20/2015
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
helpviewer_keywords:
- methods [C#], parameters
- method parameters [C#]
- parameters [C#]
ms.assetid: 680e39ff-775b-48b0-9f47-4186a5bfc4a1
caps.latest.revision: 8
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 35d96066deb866e02f6bf624121376fe3ae94373
ms.sourcegitcommit: 935d5267c44f9bce801468ef95f44572f1417e8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="method-parameters-c-reference"></a>메서드 매개 변수(C# 참조)

[in](../../../csharp/language-reference/keywords/in-parameter-modifier.md), [ref](../../../csharp/language-reference/keywords/ref.md) 또는 [out](../../../csharp/language-reference/keywords/out-parameter-modifier.md) 없이 메서드에 대해 선언된 매개 변수는 값으로 호출된 메서드에 전달됩니다. 메서드에서 해당 값을 변경할 수 있지만, 제어가 호출하는 프로시저로 다시 전달되면 변경된 값이 보존되지 않습니다. 메서드 매개 변수 키워드를 사용하여 이 동작을 변경할 수 있습니다.  
  
 이 섹션에서는 메서드 매개 변수를 선언할 때 사용할 수 있는 키워드를 설명합니다.  
  
-   [params](../../../csharp/language-reference/keywords/params.md)는 이 매개 변수가 가변 개수의 인수를 사용할 수 있음을 지정합니다.
  
-   [in](../../../csharp/language-reference/keywords/in-parameter-modifier.md)은 이 매개 변수를 참조로 전달할 수 있지만 호출된 메서드로만 읽을 수 있음을 지정합니다.
  
-   [ref](../../../csharp/language-reference/keywords/ref.md)는 이 매개 변수를 참조로 전달할 수 있고 호출된 메서드로 읽거나 쓸 수 있음을 지정합니다.
  
-   [out](../../../csharp/language-reference/keywords/out-parameter-modifier.md)는 이 매개 변수가 참조로 전달되고 호출된 메서드에 의해 기록되도록 지정합니다.
  
## <a name="see-also"></a>참고 항목  
 [C# 참조](../../../csharp/language-reference/index.md)  
 [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
 [C# 키워드](../../../csharp/language-reference/keywords/index.md)
