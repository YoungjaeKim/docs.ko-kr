---
title: x:Null 태그 확장명
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-wpf
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- NullExtension
- x:NullExtension
- x:Null
- "Null"
- xNull
helpviewer_keywords:
- Null markup extension in XAML [XAML Services]
- x:Null markup extension [XAML Services]
- XAML [XAML Services], x:Null markup extension
ms.assetid: 2e3ccc21-4996-481d-91b5-3910d8b3bfa3
caps.latest.revision: ''
author: wadepickett
ms.author: wpickett
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 5b10d759a4f79eabe973a0fcd60736428e46f659
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/22/2017
---
# <a name="xnull-markup-extension"></a>x:Null 태그 확장명
지정 `null` XAML 멤버에 대 한 값으로.  
  
## <a name="xaml-attribute-usage"></a>XAML 특성 사용  
  
```xaml  
<object property="{x:Null}" .../>  
```  
  
## <a name="remarks"></a>설명  
 에 null 참조에 대 한 키워드 [!INCLUDE[TLA#tla_cshrp](../../../includes/tlasharptla-cshrp-md.md)] 및 [!INCLUDE[TLA#tla_cpp](../../../includes/tlasharptla-cpp-md.md)] null입니다. [!INCLUDE[TLA#tla_visualb](../../../includes/tlasharptla-visualb-md.md)] null 참조에 대 한 키워드는 `Nothing`, 항상 사용 되지만 `{x:Null}` XAML 사용에 관계 없이 XAML과 연결 하는 코드 숨김 언어도 합니다.  
  
 `x:Null` 태그 확장은 설정 가능한 속성이 없습니다.  
  
 널 사용은 종종 clr XAML 멤버 노출 연관 <xref:System.Nullable%601> 값입니다.  
  
 `x:Null` 태그 확장, 모든 XAML 태그 확장 처럼 중괄호를 사용 하 여 (`{,}`) 이스케이프를 리터럴 또는 이벤트 처리기 참조 이외의 특성 값의 처리에 대 한 합니다. 특성 구문은 이러한 태그 확장 가장 자주 사용 되는 구문입니다. 개체 요소 구문 `<x:Null />` 은 기술적으로 가능 하지만 때문에 거의 사용 되지 않습니다는 `x:Null` 태그 확장에는 위치 매개 변수 또는 생성 인수 없습니다.  
  
 태그 확장에 대 한 정보를 참조 하십시오. [태그 확장명 및 WPF XAML](../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)합니다.  
  
 이 태그 확장에 대 한 처리 정의한.NET Framework XAML 서비스에서는 <xref:System.Windows.Markup.NullExtension> 클래스입니다.  
  
## <a name="wpf-usage-notes"></a>WPF 사용 정보  
 `null` 참조 형식 종속성 속성에 대 한 초기 설정 되지 않은 값일 필요는 없습니다. 초기 기본값 각 종속성 속성에 따라 다를 수 있습니다 및 속성별 메타 데이터에 따라 만들어집니다. 많은 종속성 속성이 동의 하지 않으면 `null` 태그 또는 유효성 검사 콜백 구현 때문에 코드를 통해 값으로. 종속성 속성에 대 한 자세한 내용은 참조 [종속성 속성 개요](../../../docs/framework/wpf/advanced/dependency-properties-overview.md)합니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Windows.DependencyProperty.UnsetValue>  
 [XAML 개요(WPF)](../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)  
 [태그 확장 및 WPF XAML](../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)
