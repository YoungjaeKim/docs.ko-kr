---
title: "방법: TextBox 컨트롤의 텍스트 내용 설정"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- text content [WPF], setting
- TextBox control [WPF], setting text content
ms.assetid: bcd25fc7-a52f-4453-b802-2c8d2b335ab8
caps.latest.revision: "13"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: ef354a986ee71cfa7a8e00a62905ee909d9cf30d
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-set-the-text-content-of-a-textbox-control"></a>방법: TextBox 컨트롤의 텍스트 내용 설정
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Controls.TextBox.Text%2A> 속성의 초기 텍스트 콘텐츠를 설정 하는 <xref:System.Windows.Controls.TextBox> 제어 합니다.  
  
 **참고** 있지만 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 예제의 버전에서 사용할 수는 `<TextBox.Text>` 각 단추의 텍스트 태그 <xref:System.Windows.Controls.TextBox> 콘텐츠, 필요 하지 않습니다 때문에 <xref:System.Windows.Controls.TextBox> 적용 되는 <xref:System.Windows.Markup.ContentPropertyAttribute> 특성을 <xref:System.Windows.Controls.TextBox.Text%2A> 속성입니다. 자세한 내용은 참조 [XAML 개요 (WPF)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)합니다.  
  
## <a name="example"></a>예  
 [!code-xaml[TextBox_MiscCode#_TextBoxSetTextXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_textboxsettextxaml)]  
  
## <a name="example"></a>예  
 [!code-csharp[TextBox_MiscCode#_TextBoxSetText](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_textboxsettext)]
 [!code-vb[TextBox_MiscCode#_TextBoxSetText](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextBox_MiscCode/VisualBasic/Window1.xaml.vb#_textboxsettext)]  
  
## <a name="see-also"></a>참고 항목  
 [TextBox 개요](../../../../docs/framework/wpf/controls/textbox-overview.md)  
 [RichTextBox 개요](../../../../docs/framework/wpf/controls/richtextbox-overview.md)
