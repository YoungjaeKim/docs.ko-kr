---
title: "튜플(F#)"
description: "F # 튜플, 명명 되지 않았지만 순서가 지정 된 값의 그룹에 알아봅니다."
keywords: "visual f#, f#, 함수형 프로그래밍"
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: 35069073-9a82-410f-8dea-912e2a152e6d
ms.openlocfilehash: 996566f2baaea8ab01e5c80e53caea82e9684714
ms.sourcegitcommit: d95a91d685565f4d95c8773b558752864a6a3d7e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2018
---
# <a name="tuples"></a>튜플

A *튜플* 은 명명 되지 않았지만 순서가 지정 된 값의 그룹입니다.  튜플 참조 형식 또는 구조체 일 수 있습니다.

## <a name="syntax"></a>구문

```fsharp
(element, ... , element)
struct(element, ... ,element )
```
## <a name="remarks"></a>설명
각 *요소* 위 구문에서 올바른 F # 식일 수 있습니다.

## <a name="examples"></a>예제
튜플의 예로 쌍, 삼중 쌍, 등과 같은 종류나 다른 종류의를 들 수 있습니다. 몇 가지 예는 다음 코드에 나와 있습니다.

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/basic-examples.fsx#L6-L21)]
    
## <a name="obtaining-individual-values"></a>개별 값 가져오기
사용할 수 있습니다 패턴 일치를 액세스 하 여 튜플 요소에 이름을 할당 다음 코드에 나와 있는 것 처럼.

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/basic-examples.fsx#L27-L29)]

외부의 패턴 일치를 통해 튜플을 해체 또한 수는 `match` 식을 통해 `let` 바인딩:

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/basic-examples.fsx#L34-L37)]

Or 패턴 수 튜플 함수에 대 한 입력으로 일치 합니다.

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/basic-examples.fsx#L43-L47)]

튜플의 요소가 하나만 필요한 경우 와일드 카드 문자 (밑줄) 필요 하지 않은 값에 대 한 새 이름을 않도록 하기 위해 사용할 수 있습니다.

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/basic-examples.fsx#L53-L54)]

구조체 튜플로 참조 튜플에서 요소를 복사 하는 또한 간단 합니다.

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/basic-examples.fsx#L62-L66)]

함수 `fst` 및 `snd` (튜플만 참조) 첫 번째 반환 하 고 각각 요소 튜플의 두 번째입니다.

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/basic-examples.fsx#L72-L73)]

튜플의 세 번째 요소를 반환 하는 기본 제공 함수가 있지만 쉽게 작성할 수 있습니다 하나 다음과 같습니다.

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/basic-examples.fsx#L78-L78)]

일반적으로 개별 튜플 요소에 액세스 하려면 패턴 일치를 사용 하는 것이 좋습니다.

## <a name="using-tuples"></a>튜플을 사용 하 여
튜플 다음 예제와 같이 함수에서 여러 값을 반환 하는 편리한 방법을 제공 합니다. 이 예에서는 정수 나누기를 반올림된 한 결과 튜플 쌍의 첫 번째 멤버로 작업과 쌍의 두 번째 구성원으로 나머지를 반환 합니다.

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/basic-examples.fsx#L83-L86)]

튜플 사용할 수도 있습니다 함수 인수로 일반적인 함수 구문 암시 하는 함수 인수 암시적 커리 방지 하려는 경우.

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/basic-examples.fsx#L88-L88)]

함수를 정의 하는 일반적인 구문을 `let sum a b = a + b` 다음 코드에 나와 있는 것 처럼는 함수의 첫 번째 인수를 부분 적용 되는 함수를 정의할 수 있습니다.

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/basic-examples.fsx#L90-L94)]

튜플을 매개 변수로 사용 하면 변환이 비활성화 합니다. 자세한 내용은의 "인수 부분 응용 프로그램" 참조 [함수](functions/index.md)합니다.

## <a name="names-of-tuple-types"></a>튜플 형식의 이름
사용 하는 튜플 된 형식의 이름을 작성 하는 경우는 `*` 요소를 구분 하는 기호입니다. 구성 된 튜플을 대 한는 `int`, `float`, 및 `string`와 같은 `(10, 10.0, "ten")`, 종류는 다음과 같이 작성할 수 있습니다.

```fsharp
int * float * string
```

## <a name="interoperation-with-c-tuples"></a>C# 튜플와의 상호 운용

C# 7 언어 튜플을 도입 되었습니다.  C#의 튜플 struct 이며 구조체 튜플을 F #에서 동일 합니다.  C#과 상호 운용 해야 하는 경우 구조체 튜플을 사용 해야 합니다.

작업을 수행 하는 것과 쉽습니다.  예를 들어 C# 클래스에 튜플을 전달 튜플이 수도 있는 결과 사용할를 가정해 봅니다.

```csharp
namespace CSharpTupleInterop
{
    public static class Example
    {
        public static (int, int) AddOneToXAndY((int x, int y) a) =>
            (a.x + 1, a.y + 1);
    }
}
```

F # 코드에서 구조체 튜플 매개 변수로 전달 하 고 결과 구조체 튜플로 서 사용한 다음 있습니다.

```fsharp
open TupleInterop

let struct (newX, newY) = Example.AddOneToXAndY(struct (1, 2))
// newX is now 2, and newY is now 3
```

### <a name="converting-between-reference-tuples-and-struct-tuples"></a>참조 한 구조체 형식 사이의 변환

참조 한 구조체 완전히 다른 기본 표시를 가지기 때문에 암시적으로 변환 하지 않습니다.  즉, 다음과 같은 코드 컴파일이 되지 않습니다.

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/interop.fsx#L5-L12)]

패턴 해야 하나 튜플에서 일치 하 고 생성할와 구성 요소를 사용 합니다.  예:

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/interop.fsx#L18-L22)]

## <a name="compiled-form-of-reference-tuples"></a>컴파일된 참조 튜플 형식
이 섹션 컴파일되는 하는 경우 튜플 형식에 설명 합니다.  이 정보는.NET Framework 3.5를 대상으로 하지 않는 한 읽을 필요가 또는 더 낮은 아닙니다.

튜플 중 모든 명명 된 여러 제네릭 형식에 하나의 개체로 컴파일됩니다 `System.Tuple`, 인자, 또는 형식 매개 변수 수에는 오버 로드입니다. 튜플 유형이 F # 구문을 인식 하지 않으므로 도구를 사용 하는 경우 또는 C# 또는 Visual Basic 등의 다른 언어에서 볼 때이 폼에 나타납니다. `Tuple` 형식을.NET Framework 4에서 도입 되었습니다. 컴파일러 버전을 사용 하 여 이전 버전의.NET Framework를 대상으로 하는 경우 [System.Tuple](https://msdn.microsoft.com/library/5ac7953d-acdc-4a58-bfb7-c1f6406c0fa3) 2.0 버전의 F # 핵심 라이브러리입니다. 이 라이브러리의 형식에서 2.0, 3.0 및 3.5 버전의.NET Framework를 대상으로 하는 응용 프로그램에만 사용 됩니다. 형식 전달.NET Framework 2.0 및.NET Framework 4 F # 구성 요소 간의 이진 호환성을 보장 하는 데 사용 됩니다.

### <a name="compiled-form-of-struct-tuples"></a>컴파일된 구조체 튜플 형식

구조체 튜플 (예를 들어 `struct (x, y)`)은 참조 튜플 근본적으로 다릅니다.  로 컴파일되는 <xref:System.ValueTuple> 인자, 또는 형식 매개 변수 수에 의해 오버 로드 된 형식입니다.  에 해당 하는 [C# 7 튜플](../../csharp/tuples.md) 및 [Visual Basic 2017 튜플](../../visual-basic/programming-guide/language-features/data-types/tuples.md), 간에 양방향 상호 운용 합니다.

## <a name="see-also"></a>참고 항목
[F# 언어 참조](index.md)

[F# 형식](fsharp-types.md)
