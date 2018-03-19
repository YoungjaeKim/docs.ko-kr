---
title: "C# 7.2의 새로운 기능"
description: "C# 7.2의 새로운 기능에 대한 개요입니다."
keywords: "C# 언어 디자인, 7.2, Visual Studio 2017,"
author: billwagner
ms.author: wiwagn
ms.date: 08/16/2017
ms.topic: article
ms.prod: .net
ms.devlang: devlang-csharp
ms.openlocfilehash: db22c9251fa5e9f5a9cb66af6ec8b193b88e0eb3
ms.sourcegitcommit: 83dd5ec003e788ccb3e33f3412a7af39ae347646
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="whats-new-in-c-72"></a>C# 7.2의 새로운 기능

C# 7.2는 다양한 유용한 기능을 추가하는 또 하나의 지점 릴리스입니다.
이 릴리스의 한 테마는 불필요한 복사 또는 할당 없이 값 유형을 사용하여 보다 효율적으로 작동하고 있습니다. 

나머지 기능은 작지만 멋진 기능입니다.

C# 7.2는 [언어 버전 선택](csharp-7-1.md#language-version-selection) 구성 요소를 사용하여 컴파일러 언어 버전을 선택합니다.

이 릴리스의 새로운 언어 기능은 다음과 같습니다.

* [값 형식과 참조 의미 체계](#reference-semantics-with-value-types)
  - 참조 의미 체계를 사용하는 값 유형으로 작동할 수 있는 구문 개선의 조합입니다.
* [뒤에 오지 않는 명명된 인수](#non-trailing-named-arguments)
  - 명명된 인수 뒤에는 위치 인수가 올 수 있습니다.
* [숫자 리터럴의 선행 밑줄](#leading-underscores-in-numeric-literals)
  - 숫자 리터럴은 이제 인쇄된 숫자 앞에 선행 밑줄이 있을 수 있습니다.
* [`private protected` 액세스 한정자](#private-protected-access-modifier)
  - `private protected` 액세스 한정자는 동일한 어셈블리의 파생된 클래스에 대해 액세스를 사용합니다.

## <a name="reference-semantics-with-value-types"></a>값 형식과 참조 의미 체계

7.2에 도입된 언어 기능을 사용하면 참조 의미 체계를 사용하면서 값 형식을 처리할 수 있습니다. 참조 유형 사용과 관련된 메모리를 할당하지 않으면서 값 형식 복사를 최소화하여 성능을 향상시키도록 설계되어 있습니다. 포함된 기능은 다음과 같습니다.

 - 매개 변수의 `in` 한정자는 인수가 참조에 의해 전달되지만 호출된 메서드에 의해 수정되지 않도록 지정합니다.
 - 메서드의 `ref readonly` 한정자는 메서드가 참조별 값을 반환하지만 해당 개체에 대한 쓰기를 허용하지 않음을 나타내기 위해 반환합니다.
 - `readonly struct` 선언은 구조체가 변경 가능하지 않으며 `in` 매개 변수로서 멤버 메서드로 전달되어야 함을 나타냅니다.
 - `ref struct` 선언은 구조체 유형이 관리되는 메모리에 직접 액세스하고 항상 스택에 할당되어야 함을 나타냅니다.

[참조 의미 체계와 함께 값 형식 사용](../reference-semantics-with-value-types.md)에서 모든 변경 사항에 대해 자세히 읽을 수 있습니다.

## <a name="non-trailing-named-arguments"></a>뒤에 오지 않는 명명된 인수

명명된 인수가 올바른 위치에 있을 때 메서드 호출은 이제 위치 인수보다 앞에 있는 명명된 인수를 사용할 수 있습니다. 자세한 내용은 [명명된 인수 및 선택적 인수](../programming-guide/classes-and-structs/named-and-optional-arguments.md)를 참조하세요.

## <a name="leading-underscores-in-numeric-literals"></a>숫자 리터럴의 선행 밑줄

C# 7.0에서는 자릿수 구분 기호에 대한 지원을 구현해도 `_`이 리터럴 값의 첫 번째 문자가 되는 것을 허용하지 않았습니다. 16진수 및 이진 숫자 리터럴은 이제 `_`로 시작될 수 있습니다. 

예:

```csharp
int binaryValue = 0b_0101_0101;
```

## <a name="private-protected-access-modifier"></a>_private protected_ 액세스 한정자

마지막으로, 새로운 복합 액세스 한정자인 `private protected`는 동일한 어셈블리에 선언된 클래스 또는 파생 클래스를 포함하여 멤버에 액세스할 수 있음을 나타냅니다. `protected internal`은 동일한 어셈블리에 있는 파생 클래스나 클래스에 의한 액세스를 허용하지만 `private protected`는 동일한 어셈블리에서 선언된 파생 유형에 대한 액세스를 제한합니다.

자세한 내용은 언어 참조의 [액세스 한정자](../language-reference/keywords/access-modifiers.md)를 참조하세요.
