---
title: -refout (Visual Basic)
ms.date: 03/16/2018
ms.prod: .net
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- /refout
helpviewer_keywords:
- refout compiler option [Visual Basic]
- /refout compiler option [Visual Basic]
- -refout compiler option [Visual Basic]
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d6075b92efd1eec9797fca248e97a325bd5df4bb
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/23/2018
---
# <a name="-refout-visual-basic"></a>-refout (Visual Basic)

**-refout** 옵션은 참조 어셈블리가 출력되어야 하는 파일 경로를 지정합니다.

[!INCLUDE[compiler-options](~/includes/compiler-options.md)]

## <a name="syntax"></a>구문

```console
-refout:filepath
```

## <a name="arguments"></a>인수

 `filepath` 경로 참조 어셈블리의 파일 이름입니다. 일반적으로 주 어셈블리의 하위 폴더에는 것이 있어야 합니다. 권장되는 규칙(MSBuild에서 사용됨)은 주 어셈블리에 상대적으로 “ref/” sub-폴더에 참조 어셈블리를 배치하는 것입니다. 모든 폴더 `filepath` 있어야; 컴파일러에서 만들 하지 않습니다. 

## <a name="remarks"></a>설명

Visual Basic에서는 `-refout` 버전부터 15.3 전환 합니다.

참조 어셈블리는 메타 데이터는 있지만 구현 코드가 없는 포함 하는 메타 데이터 전용 어셈블리입니다. 익명 형식을 제외한 모든 항목에 대 한 형식 및 멤버 정보가 포함 됩니다. 단일 메서드 본문 바뀝니다 `throw null` 문. 사용 하기 위한 이유 `throw null` (본문이 없습니다) 대비 메서드 본문은 PEVerify 실행 하 고 (따라서 메타 데이터의 완전성 유효성 검사)를 전달할 수 있도록 합니다.

참조 어셈블리는 어셈블리 수준 포함 [ReferenceAssembly](xref:System.Runtime.CompilerServices.ReferenceAssemblyAttribute) 특성입니다. 이 특성을 소스에서 지정할 수 있습니다. 이렇게 하면 컴파일러가 특성을 합성할 필요가 없습니다. 이 특성으로 인해 런타임 실행에 대 한 참조 어셈블리를 로드 하지 않습니다 (그러나 여전히 있을 수 있습니다는 리플렉션 전용 컨텍스트에 로드). 어셈블리를 반영 하는 도구를 참조 어셈블리를 리플렉션 전용으로 로드를 확인 해야 합니다. 그렇지 않으면 런타임에서 throw 된 <xref:System.BadImageFormatException>합니다.

`-refout` 및 [`-refonly`](refonly-compiler-option.md) 옵션은 함께 사용할 수 없습니다.

## <a name="see-also"></a>참고 항목
[-refonly](refonly-compiler-option.md)   
[Visual Basic 명령줄 컴파일러](index.md)  
[샘플 컴파일 명령줄](sample-compilation-command-lines.md)  

