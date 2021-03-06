---
title: "방법: Enter 키를 누르는 시점 감지"
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
- Enter key [WPF], detecting
- keys [WPF], Enter
ms.assetid: a66f39d2-ef4a-43a5-b454-a4ea0fe88655
caps.latest.revision: "11"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 21bb0dc8a38f8b49a4f5372c9dfc1e17e5114d6a
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-detect-when-the-enter-key-pressed"></a>방법: Enter 키를 누르는 시점 감지
시기를 감지 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Input.Key.Enter> 키보드의 키를 누르면 됩니다.  
  
 이 예제는 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 파일 및 코드 숨김 파일입니다.  
  
## <a name="example"></a>예  
 누를 때는 <xref:System.Windows.Input.Key.Enter> 키에 <xref:System.Windows.Controls.TextBox>, 텍스트 상자에 입력의 다른 영역에 표시는 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]합니다.  
  
 다음 [!INCLUDE[TLA2#tla_titlexaml](../../../../includes/tla2sharptla-titlexaml-md.md)] 구성 된 사용자 인터페이스를 만들고는 <xref:System.Windows.Controls.StackPanel>, <xref:System.Windows.Controls.TextBlock>, 및 <xref:System.Windows.Controls.TextBox>합니다.  
  
 [!code-xaml[keydown#KeyDownUI](../../../../samples/snippets/csharp/VS_Snippets_Wpf/KeyDown/CSharp/Window1.xaml#keydownui)]  
  
 다음 코드 숨김 만듭니다는 <xref:System.Windows.UIElement.KeyDown> 이벤트 처리기입니다.  키를 누르면가 <xref:System.Windows.Input.Key.Enter> 키, 메시지에 표시 되는 <xref:System.Windows.Controls.TextBlock>합니다.  
  
 [!code-csharp[keydown#KeyDownSample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/KeyDown/CSharp/Window1.xaml.cs#keydownsample)]
 [!code-vb[keydown#KeyDownSample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/KeyDown/VisualBasic/Window1.xaml.vb#keydownsample)]  
  
## <a name="see-also"></a>참고 항목  
 [입력 개요](../../../../docs/framework/wpf/advanced/input-overview.md)  
 [라우트된 이벤트 개요](../../../../docs/framework/wpf/advanced/routed-events-overview.md)
