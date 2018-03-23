---
title: -doc
ms.date: 03/10/2018
ms.prod: .net
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- doc compiler option [Visual Basic]
- -doc compiler option [Visual Basic]
- /doc compiler option [Visual Basic]
ms.assetid: 5fc32ec9-a149-4648-994c-a8d0cccd0a65
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0948b9ef0675541ca595bb297e01e62c9d79a181
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="-doc"></a>-doc
XML 파일에 대해 문서 주석을 처리합니다.  
  
## <a name="syntax"></a>구문  
  
```  
-doc[+ | -]  
' -or-  
-doc:file  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`+` &#124; `-`|선택 사항입니다. 지정 +, 또는 그냥 `-doc`, 컴파일러가 문서 정보를 생성 하는 XML 파일에 배치 합니다. 지정 `-` 지정 하지 않는 것과 같습니다 `-doc`, 하므로 문서 정보가 만들 수 없습니다.|  
|`file`|`-doc:`를 사용하는 경우 필수입니다. 컴파일의 소스 코드 파일에서 사용 되는 출력 XML 파일을 지정 합니다. 파일 이름에 공백이 있으면 이름을 따옴표로 묶습니다 ("").|  
  
## <a name="remarks"></a>설명  
 `-doc` 옵션 컴파일러 문서 주석을 포함 하는 XML 파일을 생성 하는지 여부를 제어 합니다. 사용 하는 경우는 `-doc:file` 구문에서 `file` 매개 변수는 XML 파일의 이름을 지정 합니다. 사용 하는 경우 `-doc` 또는 `-doc+`, 컴파일러에서는 실행 파일 또는 작성 하는 라이브러리에서 XML 파일 이름을 가져옵니다. 사용 하는 경우 `-doc-` 지정 하지 않으면 또는 `-doc` 옵션을 컴파일러를 XML 파일로 만들지 않습니다.  
  
 소스 코드 파일 문서 주석을 다음 정의 앞 입력할 수 있습니다.  
  
-   사용자 정의 형식는 [클래스](../../../visual-basic/language-reference/statements/class-statement.md) 또는 [인터페이스](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
-   멤버는 필드와 같은 [이벤트](../../../visual-basic/language-reference/statements/event-statement.md), [속성](../../../visual-basic/language-reference/statements/property-statement.md), [함수](../../../visual-basic/language-reference/statements/function-statement.md), 또는 [서브루틴](../../../visual-basic/language-reference/statements/sub-statement.md)합니다.  
  
 생성 된 XML 파일을 사용 하는 [!INCLUDE[vsprvs](~/includes/vsprvs-md.md)] [IntelliSense](/visualstudio/ide/using-intellisense) 기능, XML 파일의 파일 이름을 지원 하려는 어셈블리와 동일 합니다. 어셈블리에서 참조 되는 경우 되도록 XML 파일을 어셈블리와 동일한 디렉터리에 있는지 확인은 [!INCLUDE[vsprvs](~/includes/vsprvs-md.md)] 프로젝트.xml 파일과 함께 검색 합니다. XML 문서 파일 intellisense는 프로젝트 내 또는 프로젝트에서 참조 하는 프로젝트 내에서 코드에 대 한 작동 하려면 필요 하지 않습니다.  
  
 사용 하 여 컴파일하지 않으면 `/target:module`, XML 파일에는 태그가 포함 된 `<assembly></assembly>`합니다. 이러한 태그는 컴파일의 출력 파일에 대 한 어셈블리 매니페스트를 포함 하는 파일의 이름을 지정 합니다.  
  
 참조 [XML 주석 태그](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md) 코드 주석에서 문서를 생성 하는 방법에 대 한 합니다.  
  
|Visual Studio에서 doc 통합 개발 환경 설정-|  
|---|  
|1.  **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 **속성**을 클릭합니다. <br />2.  **컴파일** 탭을 클릭합니다.<br />3.  값을 설정는 **XML 문서 파일 생성** 상자입니다.|  
  
## <a name="example"></a>예제  
 참조 [Your 코드를 XML로 문서화](../../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md) 샘플입니다.  
  
## <a name="see-also"></a>참고 항목  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
 [코드를 XML로 문서화](../../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md)
