---
title: -코드 페이지 (Visual Basic)
ms.date: 03/09/2018
ms.prod: .net
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- -codepage compiler option [Visual Basic]
- codepage compiler option [Visual Basic]
- -codepage compiler option [Visual Basic]
ms.assetid: be36ec33-6800-4505-838c-4124564f5cc9
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 736b35f51657aa7b21a6a077d70f5e9ff0d4fb85
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="-codepage-visual-basic"></a>-코드 페이지 (Visual Basic)
컴파일할 때 모든 소스 코드 파일에 사용할 코드 페이지를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
-codepage:id  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`id`|필수. 컴파일러에서 지정한 코드 페이지를 사용 하 여 `id` 소스 파일의 인코딩을 해석할 수 있습니다.|  
  
## <a name="remarks"></a>설명  
 특정 인코딩을 사용 하 여 저장 된 소스 코드를 컴파일하는 데 사용할 수 있습니다 `-codepage` 코드 페이지를 사용 해야 지정할 수 있습니다. `-codepage` 옵션 컴파일에 모든 소스 코드 파일에 적용 됩니다. 자세한 내용은 참조 [.NET Framework의 문자 인코딩](http://msdn.microsoft.com/library/bf6d9823-4c2d-48af-b280-919c5af66ae9)합니다.  
  
 `-codepage` 옵션에는 소스 코드 파일의 현재 ANSI 코드 페이지, Unicode 또는 u t F-8을 사용 하 여 서명을 사용 하 여이 저장 된 경우 필요 하지 않습니다. [!INCLUDE[vsprvs](~/includes/vsprvs-md.md)] 사용자에서 다른 인코딩을 지정 하지 않은 경우 기본적으로 모든 소스 코드 파일의 현재 ANSI 코드 페이지와 저장 된 **인코딩** 대화 상자. [!INCLUDE[vsprvs](~/includes/vsprvs-md.md)] 사용 하 여는 **인코딩** 대화 상자를 다른 코드 페이지와 함께 저장 하는 소스 코드 파일을 엽니다.  
  
> [!NOTE]
>  `-codepage` 옵션 내에서 사용할 수 없는 [!INCLUDE[vsprvs](~/includes/vsprvs-md.md)] 개발 환경; 명령줄에서 컴파일할 경우에 사용 가능 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
