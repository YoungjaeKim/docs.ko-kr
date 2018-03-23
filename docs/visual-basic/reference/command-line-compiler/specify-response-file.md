---
title: '@(지시 파일 지정)(Visual Basic)'
ms.date: 03/13/2018
ms.prod: .net
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- '@ (Specify Response File) compiler option [Visual Basic]'
ms.assetid: a6847eaa-e5f9-4303-9421-45b55484b9ca
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: af66000208dee0896792892a52dc6acdf5cb1e37
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="-specify-response-file-visual-basic"></a>@(지시 파일 지정)(Visual Basic)
컴파일러 옵션을 포함 하는 파일 및 컴파일할 소스 코드 파일을 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
@response_file  
```  
  
## <a name="arguments"></a>인수  
 `response_file`  
 필수. 컴파일러 옵션이 나 컴파일할 소스 코드 파일을 나열 하는 파일입니다. 파일 이름을 따옴표로 묶습니다 ("")에 공백이 있는 경우.  
  
## <a name="remarks"></a>설명  
 컴파일러는 컴파일러 옵션 및 명령줄에 지정 된 것 처럼 응답 파일에 지정 된 소스 코드 파일을 처리 합니다.  
  
 컴파일에서 지시 파일을 여러 개를 지정 하려면 다음과 같은 여러 지시 파일 옵션을 지정 합니다.  
  
```  
@file1.rsp @file2.rsp  
```  
  
 응답 파일, 여러 컴파일러 옵션 및 소스 코드 파일을 한 줄에 나타날 수 있습니다. 단일 컴파일러 옵션 사양 (여러 줄으로 나타낼 수 없습니다)는 한 줄에 나타나야 합니다. 응답 파일에는로 시작 하는 주석을 포함할 수는 `#` 기호입니다.  
  
 하나 이상의 응답 파일에 지정 된 옵션은 명령줄에 지정 된 옵션을 결합할 수 있습니다. 컴파일러는으로 명령 옵션을 처리 합니다. 따라서, 명령줄 인수는 지시 파일에 이전에 나열 된 옵션을 재정의할 수 있습니다. 반대로, 응답 파일에에서 있는 옵션 명령줄 또는 다른 지시 파일에서 이전에 나열 된 옵션을 재정의 합니다.  
  
 Visual Basic에서 Vbc.exe 파일과 동일한 디렉터리에 있는 Vbc.rsp 파일을 제공 합니다. Vbc.rsp 파일을 하지 않는 한 기본적으로 포함 되는 `-noconfig` 옵션을 사용 합니다. 자세한 내용은 참조 [-noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)합니다.  
  
> [!NOTE]
>  `@` 옵션은 Visual Studio 개발 환경 내에서 사용할 수 없습니다; 명령줄에서 컴파일할 경우에 사용할 수는 있습니다.  
  
## <a name="example"></a>예제  
 샘플 응답 파일에서 다음 줄은 합니다.  
  
```console
# build the first output file  
-target:exe   
-out:MyExe.exe  
source1.vb   
source2.vb  
```  
  
## <a name="example"></a>예제  
 다음 예제에서는 사용 하는 `@` 라는 지시 파일 옵션 `File1.rsp`합니다.  
  
```console
vbc @file1.rsp  
```  
  
## <a name="see-also"></a>참고 항목  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
 [-noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)  
 [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
