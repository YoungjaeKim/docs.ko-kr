---
title: "F # 둘러보기"
description: "F # 프로그래밍 언어에서이 둘러보기는 샘플 코드의 주요 기능 중 일부를 검사 합니다."
keywords: "visual f #, f #, 기능 프로그래밍,.NET, 둘러보기"
author: cartermp
ms.author: phcart
ms.date: 02/28/2018
ms.topic: article
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: 49775139-082e-442f-b5a2-dd402399b5d2
ms.openlocfilehash: 7327573a25aa62af28570b4a8662235f3e41a972
ms.sourcegitcommit: 83dd5ec003e788ccb3e33f3412a7af39ae347646
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="tour-of-f"></a>F # 둘러보기 #

F #에 대 한 자세한 내용은 읽기 및 쓰기 F # 코드는 가장 좋은 방법은 합니다.  이 문서는 역할을 F # 언어의 주요 기능 중 몇 가지를 안내 하 고 컴퓨터에서 실행할 수 있는 몇 가지 코드 조각을 사용 하면 됩니다.  개발 환경 설정에 대 한 자세한 내용은, 체크 아웃 [시작](tutorials/getting-started/index.md)합니다.

두 가지 기본 개념인 F #: 함수 및 형식이 있습니다.  이 둘러보기가 개념에 해당 하는 언어의 기능을 강조 됩니다.

## <a name="functions-and-modules"></a>함수 및 모듈

F # 프로그램의 가장 기본적인 조각 ***함수*** 구조로 구성 ***모듈***합니다.  [함수](language-reference/functions/index.md) 출력을 생성 하는 입력에 대해 작업을 수행 하 고 아래에 구성 됩니다 [모듈](language-reference/modules.md)는 F #에서 항목을 그룹화 하는 기본 방법입니다.  사용 하 여 정의 된는 [ `let` 바인딩](language-reference/functions/let-bindings.md), 함수 이름을 지정 하 고 해당 인수를 정의 합니다.

[!code-fsharp[BasicFunctions](../../samples/snippets/fsharp/tour.fs#L101-L133)]

`let` 바인딩은 다른 언어의 변수과 유사한 이름을에 연결한 값도 있습니다.  `let` 바인딩은 ***변경할 수 없는*** 기본적으로 의미 하는 값 또는 함수의 이름에 바인딩된 후 변경할 수는 현재 위치입니다.  이 알고리즘은 변수는 다른 언어의 반대 ***변경 가능한***, 즉 해당 값에서에서 변경할 수 있습니다 언제 든 시간입니다.  사용할 수는 변경할 수 있는 바인딩을 필요 하면 `let mutable ...` 구문입니다.

[!code-fsharp[Immutability](../../samples/snippets/fsharp/tour.fs#L75-L94)]

## <a name="numbers-booleans-and-strings"></a>숫자, 부울 및 문자열

.NET 언어로 F #에서는 동일한 기본 [기본 형식](language-reference/primitive-types.md) .NET에 존재 합니다.

다양 한 숫자 형식은 F #에서 표현 되는 다음과 같습니다.

[!code-fsharp[Numbers](../../samples/snippets/fsharp/tour.fs#L49-L68)]

다음 부울 값은 하 고 다음과 같은 기본 조건부 논리를 수행 합니다.

[!code-fsharp[Bools](../../samples/snippets/fsharp/tour.fs#L142-L152)]

다음은 어떤 basic [문자열](language-reference/strings.md) 조작 같습니다:

[!code-fsharp[Strings](../../samples/snippets/fsharp/tour.fs#L158-L180)]

## <a name="tuples"></a>튜플

[튜플](language-reference/tuples.md) F #에서 큰 문제가 됩니다.  이들은 값 자체 처리 될 수 있는 명명 되지 않은 되지만 순서가 지정 된 값의 그룹입니다.  다른 값에서 집계 된 값으로 볼 합니다.  함수에서 여러 값이 반환 또는 임시 게 편의 대 한 값 그룹화 편리 하 게 같은 다양 한 용도로 갖게 됩니다.

[!code-fsharp[Tuples](../../samples/snippets/fsharp/tour.fs#L186-L203)]

F # 4.1을 기준으로 만들 수도 있습니다 `struct` 튜플 합니다.  이러한도 완벽 하 게 상호 작용도 C# 7/Visual Basic 15 튜플을 `struct` 튜플:

[!code-fsharp[Tuples](../../samples/snippets/fsharp/tour.fs#L205-L218)]

때문에 유의 해야 `struct` 튜플은 값 형식, 튜플, 참조 하도록 암시적으로 변환할 수 없으므로 또는 그 반대의 경우도 마찬가지입니다.  명시적으로 참조 및 구조체 튜플 간에 변환 해야 합니다.

## <a name="pipelines-and-composition"></a>파이프라인 및 구성

연산자는 파이프 (`|>`, `<|`, `||>`, `<||`, `|||>`, `<|||`)와 컴퍼지션 연산자 (`>>` 및 `<<`) F #에서 데이터를 처리할 때 널리 사용 됩니다.  이러한 연산자는 유연한 방식 "파이프라인" 함수를 설정할 수 있는 함수입니다.  다음 예제에서는 간단한 기능 파이프라인 빌드를 이러한 연산자를 활용할 수 있습니다는 방법을 안내 합니다.

[!code-fsharp[Pipelines](../../samples/snippets/fsharp/tour.fs#L227-L300)]

만든 위의 샘플 목록 처리 함수를 첫 번째 클래스 기능을 포함 하 여 F #의 여러 기능을 사용 하 고 [부분 응용 프로그램](language-reference/functions/index.md#partial-application-of-arguments)합니다.  각 이러한 개념에 대 한 심층적 이해가, 다소 고급 될 수 있지만 명확 해야 얼마나 쉽게 파이프라인을 만들 때 데이터를 처리 하기 위해 함수를 사용할 수 있습니다.

## <a name="lists-arrays-and-sequences"></a>목록, 배열 및 시퀀스

목록, 배열 및 시퀀스는 F # 핵심 라이브러리의 세 가지 기본 컬렉션 형식.

[나열](language-reference/lists.md) 는 동일한 형식의 요소 정렬 되 고 변경할 수 없는 컬렉션입니다.  즉, 열거형, 하지만 임의 액세스 및 연결에 대 한 선택에 대 한 보관 경우 큰 있을 경우 단일 연결 목록은 합니다.  이이 달리 일반적으로 목록을 나타내는 단일 연결 목록을 사용 하지 않는 다른 인기 있는 언어의 목록입니다.

[!code-fsharp[Lists](../../samples/snippets/fsharp/tour.fs#L309-L359)]

[배열](language-reference/arrays.md) 은 고정 된 크기 *변경 가능한* 같은 형식의 요소 컬렉션입니다.  이들은 요소에 대 한 빠른 임의 액세스를 지원 하며 F # 나열 방금 연속 된 메모리 블록을 되기 때문에 보다 빠릅니다.

[!code-fsharp[Arrays](../../samples/snippets/fsharp/tour.fs#L368-L407)]

[시퀀스](language-reference/sequences.md) 논리 일련의 요소는 동일한 유형의 모든 됩니다.  이들은 Lists와 Arrays, 모든 논리 일련의 요소에 "보기" 있을 수는 보다 일반적인 형식입니다.  또한 서식을 수 있기 때문에 ***지연***, 즉, 요소는 필요할 때만 계산할 수 있습니다.

[!code-fsharp[Sequences](../../samples/snippets/fsharp/tour.fs#L418-L452)]

## <a name="recursive-functions"></a>재귀 함수

컬렉션 또는 시퀀스의 요소를 처리 합니다. 일반적으로 템플릿과 [재귀](language-reference/functions/index.md#recursive-functions) F #에서.  F #에 루프 및 명령형 프로그래밍 비교에 대 한 지원으로 재귀 것 보다 쉽게 정확성을 보장할 수 있기 때문에 좋습니다.

>[!NOTE]
다음 예제에서는 패턴 일치를 통해 사용 하는 `match` 식입니다.  이 기본 구조가이 문서의 뒷부분에 나오는 다룹니다.

[!code-fsharp[RecursiveFunctions](../../samples/snippets/fsharp/tour.fs#L461-L500)]

F #도 마무리 호출 최적화에 대 한 완벽 하 게 지원 있습니다 루프 구성으로 빠르게는 재귀 호출을 최적화할 수 있습니다.

## <a name="record-and-discriminated-union-types"></a>기록 및 구별 된 공용 구조체 유형

기록 및 공용 구조체 유형은 F # 코드에서 사용 되는 두 가지 기본 데이터 형식 이며 일반적으로 F # 프로그램에서 데이터를 나타내는 가장 좋은 방법은 있습니다.  이렇게 이름을 바꾸면 클래스와 유사 하 다른 언어에서 주요 차이점 중 하나 이지만 구조적 같음 의미 체계가 있는 있습니다.  즉, "기본적 으로" 비슷합니다 일치는 간단 하 게-확인 하나는 다른 수와 같습니다.

[레코드](language-reference/records.md) 선택적 멤버 (예: 메서드)와 명명 된 값에 대 한 집계 됩니다.  C# 또는 Java에 잘 알고 있다면 다음 이러한 느끼지 것 POCOs 또는 POJOs-비슷한 방금 구조적으로 같은지 서 공식 절차입니다.

[!code-fsharp[Records](../../samples/snippets/fsharp/tour.fs#L507-L559)]

F # 4.1을 기준으로 나타낼 수도 있습니다 레코드로 `struct`s입니다.  이러한 용도로 `[<Struct>]` 특성:

[!code-fsharp[Records](../../samples/snippets/fsharp/tour.fs#L561-L568)]

[구별 된 공용 구조체 (DUs)](language-reference/discriminated-unions.md) 의 명명 된 폼의 경우 숫자가 될 수 있는 값입니다.  데이터 형식에 저장 된 여러 고유 값 중 하나일 수 있습니다.

[!code-fsharp[Unions](../../samples/snippets/fsharp/tour.fs#L575-L631)]

DUs로 사용할 수도 있습니다 *단일 대/소문자 구별 된 공용 구조체*, 기본 형식 모델링 하는 도메인에 도움이 되도록 합니다.  종종 시간, 문자열 및 다른 기본 형식과 특정 한 의미를 제공 하므로 및를 표현 하기 위해 사용 됩니다.  그러나 데이터의 기본 표현만을 사용 하 여 실수로 잘못 된 값을 할당할 때 발생할 수 있습니다!  각 유형의 단일 사례의 공용 구조체의 고유 정보를 나타내는이 시나리오에서는 정확성을 적용할 수 있습니다.

[!code-fsharp[Unions](../../samples/snippets/fsharp/tour.fs#L633-L654)]

위의 샘플에서 보여 주듯이에 단일 사례 구별 된 공용 구조체, 기본 값을 명시적으로 unwrap 해야 있습니다.

또한 DUs 기능도 사용할 재귀 정의 트리, 기본적으로 재귀적 데이터를 쉽게 표현할 수 있습니다.  예를 들어 있는 이진 검색 트리를 표시 하는 방법 여기는 `exists` 및 `insert` 함수입니다.

[!code-fsharp[Unions](../../samples/snippets/fsharp/tour.fs#L656-L683)]

DUs 데이터 형식에서 트리의 재귀 구조를 나타낼 수 있습니다, 때문에이 재귀 구조에 대 한 작동은 간단 하며 정확성을 보장 합니다.  아래와 같이 에서도 패턴 일치에서 지원 됩니다.

또한 DUs로 나타낼 수 있습니다 `struct`와 s는 `[<Struct>]` 특성:

[!code-fsharp[Unions](../../samples/snippets/fsharp/tour.fs#L685-L696)]

그러나 이렇게 할 때 염두에 두 가지 주요 사항 있습니다.

1. DU 구조체를 재귀적으로 정의 될 수 없습니다.
2. DU 구조체에는 각 해당 경우에 대 한 고유한 이름을 가져야 합니다.

위의 따르도록 실패 하면 컴파일 오류가 발생 합니다.

## <a name="pattern-matching"></a>패턴 일치

[패턴 일치](language-reference/pattern-matching.md) 은 F # 언어는 기능 정확성 F # 형식에 대해 작업을 사용 하도록 설정 합니다.  위의 샘플에서 이와 많은 양의 `match x with ...` 구문입니다.  이 구조를 사용 하면 컴파일러에서 일치 하는 철저 한 패턴을 통해 데이터 형식을 사용 하는 경우 모든 가능한 사례 수에 대 한 계정 해도 데이터 형식의 "shape" 이해할 수 있습니다.  올바른지 만큼 강력한 이며 컴파일 타임에 런타임 문제가 리라 어떤 "리프트"를 영리 하 게 사용할 수 있습니다.

[!code-fsharp[PatternMatching](../../samples/snippets/fsharp/tour.fs#L705-L739)]

줄임을 사용할 수도 있습니다 `function` 패턴 일치를 위해 사용 하도록 하는 함수를 작성 하는 경우 유용 구문을 [부분 응용 프로그램](language-reference/functions/index.md#partial-application-of-arguments):

[!code-fsharp[PatternMatching](../../samples/snippets/fsharp/tour.fs#L741-L759)]

사용 하는 단어로 것은 `_` 패턴입니다.  로 알려져는 [와일드 카드 패턴](language-reference/pattern-matching.md#wildcard-pattern), "기능이 문제가 있습니다" 방법도 방법입니다.  실수로 철저 한 패턴 일치를 무시 하 고 더 이상 사용 하 여 주의 하지 않은 경우 컴파일 타임 강요에서 이점을 얻을 수 편리 하지만 `_`합니다.  분해 된 형식의 특정 부분에 대 한 중요 하지 않으면 할 경우 유용 때 패턴을 일치 또는 마지막 절 식과 일치 하는 패턴의 의미 있는 모든 사례를 열거 했습니다.

[활성 패턴](language-reference/active-patterns.md) 패턴 일치를 사용 하는 다른 강력한 구성 됩니다.  패턴 일치 호출 사이트에서 분해 하는 사용자 지정 양식, 입력된 데이터를 분할할 수 있습니다 수 있습니다.  또한 매개 변수화 할 수, 되므로 다음 파티션 함수로 정의 합니다.  확장 활성 패턴을 지원 하기 위해 앞의 예제는 다음과 같습니다.

[!code-fsharp[ActivePatterns](../../samples/snippets/fsharp/tour.fs#L761-L783)]

## <a name="optional-types"></a>선택적 형식

구별 된 공용 구조체 유형의 특수 한 사례는는 F # 핵심 라이브러리의 부분이 아니라는 유용한 옵션 종류입니다.

[옵션 종류](language-reference/options.md) 는 두 가지 경우 중 하나를 나타내는 형식이:는 값 또는 전혀 nothing입니다.  값 수 또는 특정 작업으로 발생 하지 않을 수 있는 모든 시나리오에서 사용 됩니다.  다음 런타임 문제 보다는 컴파일 타임 문제가 있어서 두 경우를 고려 하 여 강제로 합니다.  Api에서 종종 사용 됩니다 여기서 `null` 나타내는 데 사용 됩니다 "없음" 대신에 대해 걱정할 필요가 없도록 `NullReferenceException` 대부분의 경우에서.

[!code-fsharp[Options](../../samples/snippets/fsharp/tour.fs#L791-L811)]

## <a name="units-of-measure"></a>측정 단위

F #의 형식 시스템의 한 가지 고유한 특징 측정 단위를 통해 숫자 리터럴에 대 한 컨텍스트를 제공할 수 있다는 점입니다.

[측정 단위](language-reference/units-of-measure.md) 미터, 등의 단위를 숫자 유형 연관 시킬 수 있는 함수 작업을 수행 숫자 리터럴을 보다는 단위에 있습니다.  그러면 컴파일러가 특정 컨텍스트에서 의미가에 전달 된 숫자 리터럴 형식, 작업의 종류와 관련 된 런타임 오류 헤드를 확인할 수 있습니다.

[!code-fsharp[UnitsOfMeasure](../../samples/snippets/fsharp/tour.fs#L818-L839)]

F # 핵심 라이브러리는 다양 한 SI 단위 유형과 단위 변환 정의합니다.  자세한 내용을 보려면 체크 아웃 된 [Microsoft.FSharp.Data.UnitSystems.SI Namespace](https://msdn.microsoft.com/visualfsharpdocs/conceptual/microsoft.fsharp.data.unitsystems.si-namespace-%5bfsharp%5d)합니다.

## <a name="classes-and-interfaces"></a>클래스 및 인터페이스

F #에.NET 클래스에 대 한 완벽 하 게 지원 [인터페이스](language-reference/interfaces.md), [추상 클래스](language-reference/abstract-classes.md), [상속](language-reference/inheritance.md)등입니다.

[클래스](language-reference/classes.md) .NET 개체를 나타내는 속성, 메서드 및 이벤트를 사용할 수 있는 해당 [멤버](language-reference/members/index.md)합니다.

[!code-fsharp[Classes](../../samples/snippets/fsharp/tour.fs#L848-L877)]

제네릭 클래스 정의 매우 간단 이기도 합니다.

[!code-fsharp[Classes](../../samples/snippets/fsharp/tour.fs#L884-L905)]

인터페이스를 구현 하려면 하나를 사용 `interface ... with` 구문 또는 [개체 식](language-reference/object-expressions.md)합니다.

[!code-fsharp[Classes](../../samples/snippets/fsharp/tour.fs#L912-L931)]

## <a name="which-types-to-use"></a>사용 하는 형식

중요 한 질문에 대 한 잠재 고객 클래스, 레코드, 구분 된 공용 구조체 및 튜플의 현재 상태: 하는 언제 사용 하나요?  요소와 마찬가지로 대부분의 수명, 대답 하면 상황에 따라 다릅니다.

튜플은 자체를 값으로 임시 집계 값의를 사용 하는 함수에서 여러 값을 반환 하는 데 적합 합니다.

레코드는 "의 다음 단계인" Tuples, 레이블 및 선택적 멤버에 대 한 지원을 이름이 필요 합니다.  데이터 전송 중인 프로그램을 통해 낮은 공식 절차 표현에 대 한 훌륭한 않은 것입니다.  구조적 같음 했기 때문에 비교를 통해 사용 하기 쉬운 됩니다.

구별 된 공용 구조체는 여러 가지 있지만 핵심 장점은 모든 가능한 "셰이프에 대해" 데이터를 가질 수 있는 계정에 패턴 일치와 함께에서를 사용할 수입니다.  

클래스는 엄청난 양의 정보를 나타내고도 기능에 해당 정보를 연결 해야 하는 경우 등의 이유로 적합 합니다.  경험상,으로 개념적으로 일부 데이터에 연결 되어 있는 기능을 사용 하는 경우 클래스 및 개체 지향 프로그래밍의 원칙을 사용 하 여 큰 장점은 합니다.  클래스는 또한 기본 데이터 형식을 C# 및 Visual Basic의 경우와 상호 작용할 때 이러한 언어 클래스를 사용 하 여 거의 모든 항목에 대 한 합니다.

## <a name="next-steps"></a>다음 단계

이제 살펴보았으므로 언어의 기본 기능 중 일부를 첫 번째 F # 프로그램 작성을 준비 해야 합니다!  체크 아웃 [시작](tutorials/getting-started/index.md) 개발 환경을 설정 하 고 일부 코드를 작성 하는 방법을 배울 수 있습니다.

좀 더 배우려면를 위한 다음 단계를 든 수 있지만 권장 [고급 값으로 함수](introduction-to-functional-programming/functions-as-first-class-values.md) <!--[Introduction to Functional Programming in F#](introduction-to-functional-programming/index.md)--> 핵심 함수형 프로그래밍 개념에 익숙하지 얻으려고 합니다.  이러한 필수 견고한 프로그램 F #에서 작성 됩니다.

또한 체크 아웃의 [F # 언어 참조](language-reference/index.md) 개념 콘텐츠의 광범위 한 F # 상에 서 볼 수 있습니다.
