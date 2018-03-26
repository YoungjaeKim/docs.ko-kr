---
title: '방법: Windows Forms DataGridView 컨트롤에서 개별 셀에 도구 설명 추가'
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-winforms
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- tooltips [Windows Forms], adding to data grids
- DataGridView control [Windows Forms], adding tooltips
- data grids [Windows Forms], adding tooltips
ms.assetid: 2a81f9de-d58b-4ea8-bc0b-8d93c2f4cf78
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: a533f4cbf5000489e774ba8661c3ab03cea4948a
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="how-to-add-tooltips-to-individual-cells-in-a-windows-forms-datagridview-control"></a>방법: Windows Forms DataGridView 컨트롤에서 개별 셀에 도구 설명 추가
기본적으로 도구 설명의 값을 표시 하려면 사용 <xref:System.Windows.Forms.DataGridView> 너무 작아 전체 내용을 표시할 수 있는 셀입니다. 그러나에 개별 셀에 대 한 도구 설명 텍스트 값을 설정 하려면이 동작을 재정의할 수 있습니다. 셀의 내용에 대 한 대체 설명을 사용자에 게 제공 하기 위해 또는 셀에 대 한 추가 정보를 표시 하려면 유용 합니다. 예를 들어 상태 아이콘을 표시 하는 행이 있는 경우 도구 설명을 사용 하 여 텍스트 설명을 제공 하는 것이 좋습니다.  
  
 셀 수준 도구 설명의 표시를 설정 하 여 비활성화할 수도 있습니다는 <xref:System.Windows.Forms.DataGridView.ShowCellToolTips%2A?displayProperty=nameWithType> 속성을 `false`합니다.  
  
### <a name="to-add-a-tooltip-to-a-cell"></a>셀 도구 설명을 추가 하려면  
  
-   <xref:System.Windows.Forms.DataGridViewCell.ToolTipText%2A?displayProperty=nameWithType> 속성을 설정합니다.  
  
     [!code-cpp[System.Windows.Forms.DataGridViewCell.ToolTipText#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewCell.ToolTipText/cpp/datagridviewcell.tooltiptext.cpp#1)]
     [!code-csharp[System.Windows.Forms.DataGridViewCell.ToolTipText#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewCell.ToolTipText/CS/datagridviewcell.tooltiptext.cs#1)]
     [!code-vb[System.Windows.Forms.DataGridViewCell.ToolTipText#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewCell.ToolTipText/VB/datagridviewcell.tooltiptext.vb#1)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
  
-   이 예제에는 다음 사항이 필요합니다.  
  
-   A <xref:System.Windows.Forms.DataGridView> 라는 컨트롤 `dataGridView1` 라는 열이 포함 된 `Rating` 문자열 값의 1-4 개의 별표를 표시 하기 위한 ("*") 기호입니다. <xref:System.Windows.Forms.DataGridView.CellFormatting> 컨트롤의 이벤트는 이벤트 처리기 메서드 예제에 나와 연결 되어야 합니다.  
  
-   <xref:System?displayProperty=nameWithType> 및 <xref:System.Windows.Forms?displayProperty=nameWithType> 어셈블리에 대한 참조  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 바인딩하는 경우는 <xref:System.Windows.Forms.DataGridView> 외부 데이터 원본에 대 한 제어 또는 가상 모드 구현 하 여 사용자 지정 데이터 소스를 제공 하 고, 성능 문제가 발생할 수 있습니다. 많은 양의 데이터를 작업할 때 성능 저하를 방지 하려면 처리는 <xref:System.Windows.Forms.DataGridView.CellToolTipTextNeeded> 설정이 아닌 이벤트는 <xref:System.Windows.Forms.DataGridViewCell.ToolTipText%2A> 여러 셀의 속성입니다. 처리할 때이 이벤트는 셀의 값을 가져오는 <xref:System.Windows.Forms.DataGridViewCell.ToolTipText%2A> 속성 이벤트를 발생의 값을 반환 하 고는 <xref:System.Windows.Forms.DataGridViewCellToolTipTextNeededEventArgs.ToolTipText%2A?displayProperty=nameWithType> 속성으로 이벤트 처리기 지정 합니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Windows.Forms.DataGridView>  
 <xref:System.Windows.Forms.DataGridView.ShowCellToolTips%2A?displayProperty=nameWithType>  
 <xref:System.Windows.Forms.DataGridView.CellToolTipTextNeeded?displayProperty=nameWithType>  
 <xref:System.Windows.Forms.DataGridViewCell>  
 <xref:System.Windows.Forms.DataGridViewCell.ToolTipText%2A?displayProperty=nameWithType>  
 [Windows Forms DataGridView 컨트롤에서 셀, 행 및 열 프로그래밍](../../../../docs/framework/winforms/controls/programming-with-cells-rows-and-columns-in-the-datagrid.md)
