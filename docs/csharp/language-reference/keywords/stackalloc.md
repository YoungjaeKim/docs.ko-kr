---
title: "stackalloc(C# 참조)"
ms.date: 07/20/2015
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- stackalloc_CSharpKeyword
- stackalloc
helpviewer_keywords:
- stackalloc keyword [C#]
ms.assetid: adc04c28-3ed2-4326-807a-7545df92b852
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 4b9c5328bfa1b0fc9a7751763c7d728096886905
ms.sourcegitcommit: 15316053918995cc1380163a7d7e7edd5c44e6d7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2018
---
# <a name="stackalloc-c-reference"></a>stackalloc(C# 참조)
`stackalloc` 키워드는 스택에 메모리 블록을 할당하기 위해 안전하지 않은 코드 컨텍스트에서 사용됩니다.  
  
```csharp  
int* block = stackalloc int[100];  
```  
  
## <a name="remarks"></a>설명  
 이 키워드는 지역 변수 이니셜라이저에서만 유효합니다. 다음 코드를 실행하면 컴파일러 오류가 발생합니다.  
  
```csharp  
int* block;  
// The following assignment statement causes compiler errors. You  
// can use stackalloc only when declaring and initializing a local   
// variable.  
block = stackalloc int[100];  
```  
  
 포인터 형식이 사용되므로 `stackalloc`에 [안전하지 않은](../../../csharp/language-reference/keywords/unsafe.md) 컨텍스트가 필요합니다. 자세한 내용은 [안전하지 않은 코드 및 포인터](../../../csharp/programming-guide/unsafe-code-pointers/index.md)를 참조하세요.  
  
 `stackalloc`는 C 런타임 라이브러리의 [_alloca](/cpp/c-runtime-library/reference/alloca)와 유사합니다.  
  
 다음 예제에서는 피보나치 시퀀스의 처음 20개 숫자를 계산하고 표시합니다. 각 숫자는 이전 두 숫자의 합계입니다. 코드에서 `int` 형식의 요소 20개를 포함하기에 충분한 크기의 메모리 블록이 힙이 아니라 스택에 할당됩니다. 블록의 주소는 `fib` 포인터에 저장됩니다. 이 메모리에는 가비지 수집이 적용되지 않으므로 [fixed](../../../csharp/language-reference/keywords/fixed-statement.md)를 사용하여 고정할 필요가 없습니다. 메모리 블록의 수명은 이 수명을 정의하는 메서드의 수명으로 제한됩니다. 메서드가 반환되기 전에는 메모리를 해제할 수 없습니다.  
  
## <a name="example"></a>예  
 [!code-csharp[csrefKeywordsOperator#15](../../../csharp/language-reference/keywords/codesnippet/CSharp/stackalloc_1.cs)]  
  
## <a name="security"></a>보안  
 안전하지 않은 코드는 안전한 코드보다 보안 수준이 낮습니다. 그러나 `stackalloc`를 사용하면 CLR(공용 언어 런타임)에서 버퍼 오버런 검색 기능이 자동으로 사용됩니다. 버퍼 오버런이 검색되면 악성 코드가 실행될 가능성을 최소화하기 위해 최대한 빨리 프로세스가 종료됩니다.  
  
## <a name="c-language-specification"></a>C# 언어 사양  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [C# 참조](../../../csharp/language-reference/index.md)  
 [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
 [C# 키워드](../../../csharp/language-reference/keywords/index.md)  
 [연산자 키워드](../../../csharp/language-reference/keywords/operator-keywords.md)  
 [안전하지 않은 코드 및 포인터](../../../csharp/programming-guide/unsafe-code-pointers/index.md)
