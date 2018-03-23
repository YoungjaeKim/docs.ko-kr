---
title: -linkresource (Visual Basic)
ms.date: 03/10/2018
ms.prod: .net
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- /linkresource compiler option [Visual Basic]
- -linkresource compiler option [Visual Basic]
- linkresource compiler option [Visual Basic]
- /linkres compiler option [Visual Basic]
- linkres compiler option [Visual Basic]
- -linkres compiler option [Visual Basic]
ms.assetid: cf4dcad8-17b7-404c-9184-29358aa05b15
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 33b84631e0c09521a6f4ff9e06b2a80e0885862e
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="-linkresource-visual-basic"></a>-linkresource (Visual Basic)
관리되는 리소스에 대한 링크를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
-linkresource:filename[,identifier[,public|private]]  
' -or-  
-linkres:filename[,identifier[,public|private]]  
```  
  
## <a name="arguments"></a>인수  
 `filename`  
 필수. 어셈블리에 연결할 리소스 파일입니다. 파일 이름에 공백이 있으면 이름을 따옴표로 묶습니다 ("").  
  
 `identifier`  
 선택 사항입니다. 리소스에 대 한 논리적 이름입니다. 리소스를 로드 하는 데 사용 되는 이름입니다. 기본값은 파일 이름입니다. 파일 인지 공개 또는 개인 어셈블리 매니페스트에 예를 들어 지정할 수 있습니다: `-linkres:filename.res,myname.res,public`합니다. 기본적으로 `filename` 어셈블리에 공개 합니다.  
  
## <a name="remarks"></a>설명  
 `-linkresource` 옵션은 출력 파일에 리소스 파일을 포함 하지 않습니다; 사용 된 `-resource` 이 작업을 수행 하는 옵션입니다.  
  
 `-linkresource` 옵션 중 하나 필요로 `-target` 옵션 이외의 `-target:module`합니다.  
  
 경우 `filename` 는 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 만들어진 리소스 파일, 예를 들어 여는 [Resgen.exe (리소스 파일 생성기)](http://msdn.microsoft.com/library/8ef159de-b660-4bec-9213-c3fbc4d1c6f4) 또는 개발 환경에서의 멤버와 액세스할 수 있습니다는 <xref:System.Resources> 네임 스페이스입니다. 자세한 내용은 <xref:System.Resources.ResourceManager>을 참조하세요. 로 시작 하는 메서드를 사용 하 여 런타임 시 다른 모든 리소스에 액세스 하려면 `GetManifestResource` 에 <xref:System.Reflection.Assembly> 클래스입니다.  
  
 모든 파일 형식 파일 이름일 수 있습니다. 예를 들어 네이티브 DLL을 어셈블리의 일부로 설정하면 전역 어셈블리 캐시에 설치하고 어셈블리의 관리 코드에서 액세스할 수 있습니다.  
  
 `-linkresource`의 약식은 `-linkres`입니다.  
  
> [!NOTE]
>  `-linkresource` 옵션은 Visual Studio 개발 환경에서 사용할 수 없습니다; 가능 하다는 명령줄에서 컴파일할 때만 합니다.  
  
## <a name="example"></a>예제  
 다음 코드에서는 `in.vb` 리소스 파일에 대 한 링크 `rf.resource`합니다.  
  
```console  
vbc -linkresource:rf.resource in.vb  
```  
  
## <a name="see-also"></a>참고 항목  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
 [-대상 (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)  
 [-리소스 (Visual Basic)](../../../visual-basic/reference/command-line-compiler/resource.md)  
 [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
