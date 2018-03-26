---
title: XML Value 속성(Visual Basic)
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.XmlPropertyExtensionValue
helpviewer_keywords:
- Value property [Visual Basic]
- Visual Basic code, accessing XML
- XML axis [Visual Basic], Value
- XML Value property [Visual Basic]
ms.assetid: 7ddd057a-a195-4e9b-ad8b-2ee0e615a20f
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: d9294c2d1d83dce3bca2abc22ee9c70296fc8014
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="xml-value-property-visual-basic"></a>XML Value 속성(Visual Basic)
컬렉션의 첫 번째 요소 값에 대 한 액세스를 제공 <xref:System.Xml.Linq.XElement> 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
object.Value  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`object`|필수. <xref:System.Xml.Linq.XElement> 개체의 컬렉션입니다.|  
  
## <a name="return-value"></a>반환 값  
 A `String` 컬렉션의 첫 번째 요소 값이 포함 된 또는 `Nothing` 컬렉션이 비어 있는 경우.  
  
## <a name="remarks"></a>설명  
 <xref:System.Xml.Linq.XElement.Value%2A> 속성을 사용 하면 컬렉션의 첫 번째 요소 값에 액세스 하기가 쉽지 <xref:System.Xml.Linq.XElement> 개체입니다. 이 속성은 먼저는 컬렉션 개체를 하나 이상 포함 되어 있는지 확인 합니다. 이 속성을 반환 하는 경우 컬렉션은 비어, `Nothing`합니다. 이 속성의 값을 반환 하는 그렇지 않은 경우는 <xref:System.Xml.Linq.XElement.Value%2A> 속성 컬렉션의 첫 번째 요소입니다.  
  
> [!NOTE]
>  사용 하 여 XML 특성의 값에 액세스할 때는 '@' 식별자, 특성 값으로 반환 됩니다는 `String` 명시적으로 지정할 필요가 없습니다는 <xref:System.Xml.Linq.XAttribute.Value%2A> 속성입니다.  
  
 컬렉션의 다른 요소에 액세스 하려면 XML 확장 인덱서 속성을 사용할 수 있습니다. 자세한 내용은 참조 [확장 인덱서 속성](../../../visual-basic/language-reference/xml-axis/extension-indexer-property.md)합니다.  
  
## <a name="inheritance"></a>상속  
 대부분의 사용자가 구현 하지 않아도 됩니다 <xref:System.Collections.Generic.IEnumerable%601>, 및이 섹션을 무시할 수 있습니다.  
  
 <xref:System.Xml.Linq.XElement.Value%2A> 속성을 구현 하는 형식에 대 한 확장 속성은 `IEnumerable(Of XElement)`합니다. 이 확장 속성의 바인딩을 확장 메서드의 바인딩과 같은:는 형식이 인터페이스 중 하나를 구현 하는 이름이 "Value" 속성을 정의 하는 경우 해당 속성 보다 우선적으로 확장 속성입니다. 즉,이 <xref:System.Xml.Linq.XElement.Value%2A> 속성을 구현 하는 클래스의 새 속성을 정의 하 여 재정의할 수 있습니다 `IEnumerable(Of XElement)`합니다.  
  
## <a name="example"></a>예제  
 사용 하는 방법을 보여 주는 다음 예제는 <xref:System.Xml.Linq.XElement.Value%2A> 속성 컬렉션의 첫 번째 노드에 액세스 하려면 <xref:System.Xml.Linq.XElement> 개체입니다. 이 예제에서는 자식 축 속성 이라는 모든 자식 노드의 컬렉션을 사용 하 여 `phone` 에 `contact` 개체입니다.  
  
 [!code-vb[VbXMLSamples#15](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-value-property_1.vb)]  
  
 이 코드의 텍스트는 다음과 같습니다.  
  
 `Phone number: 206-555-0144`  
  
## <a name="example"></a>예제  
 다음 예제에는 컬렉션에서 XML 특성의 값을 가져오는 방법을 보여 줍니다 <xref:System.Xml.Linq.XAttribute> 개체입니다. 이 예제에서는 특성 축 속성을 사용 하 여의 값을 표시 하는 `type` 특성의 모든는 `phone` 요소입니다.  
  
 [!code-vb[VbXMLSamples#16](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-value-property_2.vb)]  
  
 이 코드의 텍스트는 다음과 같습니다.  
  
 `home`  
  
 `work`  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Xml.Linq.XElement>  
 <xref:System.Collections.Generic.IEnumerable%601>  
 [XML 축 속성](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)  
 [XML 리터럴](../../../visual-basic/language-reference/xml-literals/index.md)  
 [Visual Basic에서 XML 만들기](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)  
 [확장명 메서드](../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)  
 [확장명 인덱서 속성](../../../visual-basic/language-reference/xml-axis/extension-indexer-property.md)  
 [XML Child 축 속성](../../../visual-basic/language-reference/xml-axis/xml-child-axis-property.md)  
 [XML Attribute 축 속성](../../../visual-basic/language-reference/xml-axis/xml-attribute-axis-property.md)
