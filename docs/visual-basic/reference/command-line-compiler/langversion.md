---
title: -langversion (Visual Basic)
ms.date: 03/10/2018
ms.prod: .net
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- /langversion compiler option [Visual Basic]
- langversion compiler option [Visual Basic]
- -langversion compiler option [Visual Basic]
ms.assetid: 59b7b0c8-2dde-4e9b-94e7-0237f7e0bafb
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: d9b91bf8efa6fabd21d257e51062dc881ab288f5
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="-langversion-visual-basic"></a>-langversion (Visual Basic)
컴파일러가 지정된 된 Visual Basic 언어 버전에 포함 되어 있는 구문만 허용 하도록 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
-langversion:version  
```  
  
## <a name="arguments"></a>인수  
 `version`  
 필수. 컴파일 중에 사용할 언어 버전입니다. 사용 가능한 값은 `9`, `9.0`, `10`, 및 `10.0`합니다.  
  
## <a name="remarks"></a>설명  
 `-langversion` 옵션 컴파일러에서는 허용 되는 구문을 지정 합니다. 예를 들어 언어 버전이 9.0에 인지를 지정 하면 컴파일러 버전 10.0에만 유효 하 고 이후 구문에 대 한 오류를 생성 합니다.  
  
 해당 대상 다른 버전의.NET Framework 응용 프로그램을 개발 하는 경우이 옵션을 사용할 수 있습니다. 예를 들어.NET Framework 3.5를 대상으로 하는 경우 언어 버전 10.0에서에서 구문을 사용 하는지 확인 하려면이 옵션을 사용할 수 있습니다.  
  
 설정할 수 있습니다 `-langversion` 직접 명령줄을 사용 해야만 합니다. 자세한 내용은 [특정 대상 .NET Framework 버전 지정](/visualstudio/ide/targeting-a-specific-dotnet-framework-version)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 코드에서는 `sample.vb` Visual Basic 9.0에 대 한 합니다.  
  
```console  
vbc -langversion:9.0 sample.vb  
```  
  
## <a name="see-also"></a>참고 항목  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
 [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)  
 [특정 대상 .NET Framework 버전 지정](/visualstudio/ide/targeting-a-specific-dotnet-framework-version)
