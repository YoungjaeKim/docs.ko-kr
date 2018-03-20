---
title: "포인터 형식(C# 프로그래밍 가이드)"
ms.date: 07/20/2015
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
helpviewer_keywords:
- unsafe code [C#], pointers
- pointers [C#]
ms.assetid: 3319faf9-336d-4148-9af2-1da2579cdd1e
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: fe7b926bdf9f662d25f2fe960b51fc8254b7aa3a
ms.sourcegitcommit: 83dd5ec003e788ccb3e33f3412a7af39ae347646
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="pointer-types-c-programming-guide"></a>포인터 형식(C# 프로그래밍 가이드)
안전하지 않은 컨텍스트에서는 형식이 포인터 형식, 값 형식 또는 참조 형식이 될 수 있습니다. 포인터 형식 선언은 다음 형식 중 하나를 사용합니다.  
  
```  
type* identifier;  
void* identifier; //allowed but not recommended  
```  
  
 포인터 형식은 다음과 같은 형식일 수 있습니다.  
  
-   [sbyte](../../../csharp/language-reference/keywords/sbyte.md), [byte](../../../csharp/language-reference/keywords/byte.md), [short](../../../csharp/language-reference/keywords/short.md), [ushort](../../../csharp/language-reference/keywords/ushort.md), [int](../../../csharp/language-reference/keywords/int.md), [uint](../../../csharp/language-reference/keywords/uint.md), [long](../../../csharp/language-reference/keywords/long.md), [ulong](../../../csharp/language-reference/keywords/ulong.md), [char](../../../csharp/language-reference/keywords/char.md), [float](../../../csharp/language-reference/keywords/float.md), [double](../../../csharp/language-reference/keywords/double.md), [decimal](../../../csharp/language-reference/keywords/decimal.md), or [bool](../../../csharp/language-reference/keywords/bool.md).  
  
-   모든 [enum](../../../csharp/language-reference/keywords/enum.md) 형식  
  
-   임의의 포인터 형식  
  
-   관리되지 않는 형식의 필드만 포함하는 임의의 사용자 정의 구조체 형식  
  
 포인터 형식은 [개체](../../../csharp/language-reference/keywords/object.md)에서 상속되지 않으며 포인터 형식과 `object`는 서로 변환되지 않습니다. 또한 boxing과 unboxing은 포인터를 지원하지 않습니다. 그러나 다른 포인터 형식 간의 변환 및 포인터 형식과 정수 형식 사이의 변환은 허용됩니다.  
  
 동일한 선언에서 여러 포인터를 선언하는 경우 별표(*)는 기본 형식에만 함께 사용되고 각 포인터 이름의 접두사로는 사용되지 않습니다. 예:  
  
```  
int* p1, p2, p3;   // Ok  
int *p1, *p2, *p3;   // Invalid in C#  
```  
  
 개체 참조는 포인터가 해당 개체 참조를 가리키는 경우에도 가비지 수집될 수 있으므로 포인터는 참조나 참조가 들어 있는 [구조체](../../../csharp/language-reference/keywords/struct.md)를 가리킬 수 없습니다. 가비지 수집기는 포인터 형식에서 개체를 가리키는지 여부를 추적하지 않습니다.  
  
 `myType*` 형식의 포인터 변수 값은 `myType` 형식의 변수 주소입니다. 다음은 포인터 형식 선언의 예제입니다.  
  
|예제|설명|  
|-------------|-----------------|  
|`int* p`|`p`는 정수에 대한 포인터입니다.|  
|`int** p`|`p`는 정수에 대한 포인터를 가리키는 포인터입니다.|  
|`int*[] p`|`p`는 정수에 대한 포인터의 1차원 배열입니다.|  
|`char* p`|`p`는 문자에 대한 포인터입니다.|  
|`void* p`|`p`는 알 수 없는 형식에 대한 포인터입니다.|  
  
 포인터 간접 참조 연산자 *를 사용하면 포인터 변수가 가리키는 위치의 내용에 액세스할 수 있습니다. 예를 들어, 다음 선언을 참조하십시오.  
  
```  
int* myVariable;  
```  
  
 여기서 `*myVariable` 식은 `int`에 포함된 주소에 있는 `myVariable` 변수를 가리킵니다.  
  
 [fixed 문](../../../csharp/language-reference/keywords/fixed-statement.md) 및 [포인터 변환](../../../csharp/programming-guide/unsafe-code-pointers/pointer-conversions.md) 항목에 포인터에 대한 몇 가지 예제가 나와 있습니다.  다음 예제는 `unsafe` 키워드 및 `fixed` 문에 대한 필요성과 정수 포인터를 증분하는 방법을 보여줍니다.  이 코드를 실행하려면 콘솔 응용 프로그램의 주 함수에 붙여 넣습니다. **프로젝트 디자이너**에서 안전하지 않은 코드를 사용하도록 설정해야 합니다. 메뉴 모음에서 **프로젝트**, **속성**을 선택한 다음 **빌드** 탭에서 **안전하지 않은 코드 허용**을 선택합니다.  
  
```  
// Normal pointer to an object.  
int[] a = new int[5] {10, 20, 30, 40, 50};  
// Must be in unsafe code to use interior pointers.  
unsafe  
{  
    // Must pin object on heap so that it doesn't move while using interior pointers.  
    fixed (int* p = &a[0])  
    {  
        // p is pinned as well as object, so create another pointer to show incrementing it.  
        int* p2 = p;  
        Console.WriteLine(*p2);  
        // Incrementing p2 bumps the pointer by four bytes due to its type ...  
        p2 += 1;  
        Console.WriteLine(*p2);  
        p2 += 1;  
        Console.WriteLine(*p2);  
        Console.WriteLine("--------");  
        Console.WriteLine(*p);  
        // Deferencing p and incrementing changes the value of a[0] ...  
        *p += 1;  
        Console.WriteLine(*p);  
        *p += 1;  
        Console.WriteLine(*p);  
    }  
}  
  
Console.WriteLine("--------");  
Console.WriteLine(a[0]);  
Console.ReadLine();  
  
// Output:  
//10  
//20  
//30  
//--------  
//10  
//11  
//12  
//--------  
//12  
```  
  
 `void*` 형식의 포인터에는 간접 참조 연산자를 적용할 수 없습니다. 그러나 캐스트를 사용하여 void 포인터를 다른 포인터 형식으로 변환하거나 반대로 변환할 수 있습니다.  
  
 포인터는 `null`일 수 있습니다. null 포인터에 간접 참조 연산자를 적용할 때 발생하는 동작은 구현에 따라 다릅니다.  
  
 메서드 사이에 포인터를 전달하면 정의되지 않은 동작이 발생할 수 있다는 사실에 주의해야 합니다. `in`, `out` 또는 `ref` 매개 변수를 통해, 또는 함수 결과로 지역 변수에 포인터를 반환하는 메서드를 고려합니다. fixed 블록에서 포인터가 설정되면 이 포인터가 가리키는 변수의 고정 상태가 해제될 수 있습니다.  
  
 다음 표에서는 안전하지 않은 컨텍스트에서 포인터에 대해 수행할 수 있는 연산자와 문을 보여 줍니다.  
  
|연산자/문|사용|  
|-------------------------|---------|  
|*|포인터 간접 참조를 수행합니다.|  
|->|포인터를 통해 구조체 멤버에 액세스합니다.|  
|[]|포인터를 인덱싱합니다.|  
|`&`|변수 주소를 가져옵니다.|  
|++ 및 --|포인터를 증가 및 감소시킵니다.|  
|+ 및 -|포인터 연산을 수행합니다.|  
|==, !=, \<, >, \<= 및 >=|포인터를 비교합니다.|  
|`stackalloc`|스택에 메모리를 할당합니다.|  
|`fixed` 문|해당 주소를 찾을 수 있도록 임시로 변수를 고정합니다.|  
  
## <a name="c-language-specification"></a>C# 언어 사양  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
 [안전하지 않은 코드 및 포인터](../../../csharp/programming-guide/unsafe-code-pointers/index.md)  
 [포인터 변환](../../../csharp/programming-guide/unsafe-code-pointers/pointer-conversions.md)  
 [포인터 식](../../../csharp/programming-guide/unsafe-code-pointers/pointer-expressions.md)  
 [유형](../../../csharp/language-reference/keywords/types.md)  
 [unsafe](../../../csharp/language-reference/keywords/unsafe.md)  
 [fixed 문](../../../csharp/language-reference/keywords/fixed-statement.md)  
 [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)  
 [boxing 및 unboxing](../../../csharp/programming-guide/types/boxing-and-unboxing.md)
