---
title: DataGrid 컨트롤의 크기 조정 옵션
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-wpf
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- DataGrid control [WPF], sizing
- size [WPF], DataGrid
- automatically size DataGrid [WPF]
ms.assetid: 96a0e47e-b010-4302-98ef-2daac446d8db
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 4219dc88a263b73aa89812a2f841a920c804796b
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="sizing-options-in-the-datagrid-control"></a>DataGrid 컨트롤의 크기 조정 옵션
다양 한 옵션을 제어할 수 있는 방법을 <xref:System.Windows.Controls.DataGrid> 크기가 자동으로 조정 합니다. <xref:System.Windows.Controls.DataGrid>, 개별 행과 열에는 <xref:System.Windows.Controls.DataGrid>를 내용에 자동으로 크기가 조정 되도록 설정할 수 있습니다, 또는 특정 값으로 설정할 수 있습니다. 기본적으로는 <xref:System.Windows.Controls.DataGrid> 확장 및 해당 내용의 크기에 맞게 축소 됩니다.  
  
## <a name="sizing-the-datagrid"></a>DataGrid를 크기 조정  
  
### <a name="cautions-when-using-automatic-sizing"></a>자동 크기 조정 사용 시 주의 사항  
 기본적으로는 <xref:System.Windows.FrameworkElement.Height%2A> 및 <xref:System.Windows.FrameworkElement.Width%2A> 의 속성은 <xref:System.Windows.Controls.DataGrid> 로 설정 <xref:System.Double.NaN?displayProperty=nameWithType> ("`Auto`" XAML에서), 및 <xref:System.Windows.Controls.DataGrid> 해당 내용의 크기에 따라 조정 됩니다.  
  
 와 같은 자식 크기 제한 하지 않는 컨테이너 안에 배치 되는 경우는 <xref:System.Windows.Controls.Canvas> 또는 <xref:System.Windows.Controls.StackPanel>, <xref:System.Windows.Controls.DataGrid> 는 컨테이너의 표시 범위 밖 늘어나고 스크롤 막대가 표시 되지 것입니다. 이 문제에는 사용 편의성과 성능 모두에 영향을 줄 합니다.  
  
 하는 경우 데이터 집합에 바인딩된 경우는 <xref:System.Windows.FrameworkElement.Height%2A> 의 <xref:System.Windows.Controls.DataGrid> 가 바인딩된 데이터 집합의 각 데이터 항목에 대 한 행을 추가 하려면 계속 제한 되지 않습니다. 이 발생할 수 있습니다는 <xref:System.Windows.Controls.DataGrid> 행을 추가할 때 응용 프로그램의 표시 범위 밖에 증가할 수 있습니다. <xref:System.Windows.Controls.DataGrid> 표시 되지 것입니다 스크롤 막대가 예제의 때문에 해당 <xref:System.Windows.FrameworkElement.Height%2A> 계속 새 행을 수용 하기 위해 증가 됩니다.  
  
 각 행에 대 한 개체를 만들는 <xref:System.Windows.Controls.DataGrid>합니다. 큰 데이터 집합을 사용 하는 경우 및 허용 하면는 <xref:System.Windows.Controls.DataGrid> 많은 개체가 생성 자동으로 크기를 자동으로, 응용 프로그램의 성능이 저하 될 합니다.  
  
 큰 데이터 집합으로 작업할 때 이러한 문제를 방지 하려면 것이 좋습니다 구체적으로 설정 하는 <xref:System.Windows.FrameworkElement.Height%2A> 의 <xref:System.Windows.Controls.DataGrid> 제한 하는 컨테이너에 저장 하거나 해당 <xref:System.Windows.FrameworkElement.Height%2A>와 같은 <xref:System.Windows.Controls.Grid>합니다. 때는 <xref:System.Windows.FrameworkElement.Height%2A> 액세스가 제한 된 <xref:System.Windows.Controls.DataGrid> 내의 지정 된 행만 만들어집니다 <xref:System.Windows.FrameworkElement.Height%2A>, 새 데이터를 표시 하는 데 필요한 만큼 이러한 행을 재활용 합니다.  
  
### <a name="setting-the-datagrid-size"></a>DataGrid 크기 설정  
 <xref:System.Windows.Controls.DataGrid> 자동으로 크기를 지정 된 경계 내에서 설정할 수 있습니다 또는 <xref:System.Windows.Controls.DataGrid> 특정 크기를 설정할 수 있습니다. 다음 표에서 컨트롤을 설정할 수 있는 속성을 보여 줍니다.는 <xref:System.Windows.Controls.DataGrid> 크기입니다.  
  
|속성|설명|  
|--------------|-----------------|  
|<xref:System.Windows.FrameworkElement.Height%2A>|에 대 한 특정 높이 설정의 <xref:System.Windows.Controls.DataGrid>합니다.|  
|<xref:System.Windows.FrameworkElement.MaxHeight%2A>|높이 대 한 상한을 설정는 <xref:System.Windows.Controls.DataGrid>합니다. <xref:System.Windows.Controls.DataGrid> 이 높이 도달할 때까지 세로로 늘어납니다.|  
|<xref:System.Windows.FrameworkElement.MinHeight%2A>|설정의 높이 대 한 하한값은 <xref:System.Windows.Controls.DataGrid>합니다. <xref:System.Windows.Controls.DataGrid> 이 높이 도달할 때까지 세로로 축소 됩니다.|  
|<xref:System.Windows.FrameworkElement.Width%2A>|에 대 한 특정 너비를 설정의 <xref:System.Windows.Controls.DataGrid>합니다.|  
|<xref:System.Windows.FrameworkElement.MaxWidth%2A>|너비에 대 한 상한을 설정는 <xref:System.Windows.Controls.DataGrid>합니다. <xref:System.Windows.Controls.DataGrid> 이 너비에 도달할 때까지 가로로 늘어납니다.|  
|<xref:System.Windows.FrameworkElement.MinWidth%2A>|너비에 대 한 하한값을 설정 합니다.는 <xref:System.Windows.Controls.DataGrid>합니다. <xref:System.Windows.Controls.DataGrid> 이 너비에 도달할 때까지 가로로 줄어듭니다.|  
  
## <a name="sizing-rows-and-row-headers"></a>행 및 행 머리글 크기 조정  
  
### <a name="datagrid-rows"></a>DataGrid 행  
 기본적으로는 <xref:System.Windows.Controls.DataGrid> 행의 <xref:System.Windows.FrameworkElement.Height%2A> 속성이 <xref:System.Double.NaN?displayProperty=nameWithType> ("`Auto`" XAML에서), 행 높이 해당 내용의 크기를 확장 합니다. 모든 행의 높이 <xref:System.Windows.Controls.DataGrid> 설정 하 여 지정할 수는 <xref:System.Windows.Controls.DataGrid.RowHeight%2A?displayProperty=nameWithType> 속성입니다. 사용자가 행 머리글 구분선을 끌어서 행 높이 변경할 수 있습니다.  
  
### <a name="datagrid-row-headers"></a>DataGrid 행 머리글  
 행 머리글을 표시 하려면는 <xref:System.Windows.Controls.DataGrid.HeadersVisibility%2A> 속성으로 설정 되어 있어야 <xref:System.Windows.Controls.DataGridHeadersVisibility.Row?displayProperty=nameWithType> 또는 <xref:System.Windows.Controls.DataGridHeadersVisibility.All?displayProperty=nameWithType>합니다. 기본적으로 행 머리글이 표시 되 고 자동으로 해당 콘텐츠에 맞게 크기를 조정 합니다. 행 머리글을 설정 하 여 특정 너비를 지정할 수 있습니다는 <xref:System.Windows.Controls.DataGrid.RowHeaderWidth%2A?displayProperty=nameWithType> 속성입니다.  
  
## <a name="sizing-columns-and-column-headers"></a>열 및 열 머리글 크기 조정  
  
### <a name="datagrid-columns"></a>DataGrid 열  
 <xref:System.Windows.Controls.DataGrid> 의 값을 사용 하는 <xref:System.Windows.Controls.DataGridLength> 및 <xref:System.Windows.Controls.DataGridLengthUnitType> 절대 또는 자동 크기 조정 모드를 지정 하는 구조입니다.  
  
 다음 표에서에서 제공한 가치를 보여 줍니다.는 <xref:System.Windows.Controls.DataGridLengthUnitType> 구조입니다.  
  
|이름|설명|  
|----------|-----------------|  
|<xref:System.Windows.Controls.DataGridLengthUnitType.Auto>|자동 모드 크기를 크기 조정 기본 <xref:System.Windows.Controls.DataGrid> 열 셀 및 열 머리글의 내용에 기반 합니다.|  
|<xref:System.Windows.Controls.DataGridLengthUnitType.SizeToCells>|셀 기반 자동 모드 크기 조정 <xref:System.Windows.Controls.DataGrid> 열 열 머리글을 포함 하지 않습니다는 열에서 셀의 내용을 기반으로 합니다.|  
|<xref:System.Windows.Controls.DataGridLengthUnitType.SizeToHeader>|헤더 기반 자동 모드 크기 조정 <xref:System.Windows.Controls.DataGrid> 열만에 열 머리글의 내용에 기반 합니다.|  
|<xref:System.Windows.Controls.DataGridLengthUnitType.Pixel>|픽셀 기반 모드 크기 조정 <xref:System.Windows.Controls.DataGrid> 열 제공 된 숫자 값에 기반 합니다.|  
|<xref:System.Windows.Controls.DataGridLengthUnitType.Star>|배율 크기 조정 모드 가중치에 따라 사용 가능한 공간을 배분에 사용 됩니다.<br /><br /> XAML에서 별표 값 n * 여기서 n 나타냅니다는 숫자 값으로 표시 됩니다. 1\* 같습니다 \*합니다. 예를 들어 두 개의 열에는 <xref:System.Windows.Controls.DataGrid> 너비가 \* 2\*, 첫 번째 열으로 받습니다 사용 가능한 공간에의 한 부분 및 두 번째 열을 두 개의 부분 사용 가능한 공간을 받습니다.|  
  
 <xref:System.Windows.Controls.DataGridLengthConverter> 클래스를 사용 하 여 숫자 또는 문자열 값 사이의 데이터를 변환할 수 있습니다 및 <xref:System.Windows.Controls.DataGridLength> 값입니다.  
  
 기본적으로는 <xref:System.Windows.Controls.DataGrid.ColumnWidth%2A?displayProperty=nameWithType> 속성이 <xref:System.Windows.Controls.DataGridLength.SizeToHeader%2A>, 및 <xref:System.Windows.Controls.DataGridColumn.Width%2A?displayProperty=nameWithType> 속성이 <xref:System.Windows.Controls.DataGridLength.Auto%2A>합니다. 크기 조정 모드로 설정 되 면 <xref:System.Windows.Controls.DataGridLength.Auto%2A> 또는 <xref:System.Windows.Controls.DataGridLength.SizeToCells%2A>, 자신의 상당히 폭넓은 표시 된 콘텐츠 너비에 열 크기가 계속 커집니다. 스크롤할 때 이러한 크기 조정 모드 하면 열이 확장 콘텐츠 인 경우 현재 열 크기 스크롤될 보다 큰 합니다. 콘텐츠 스크롤되어 열이 축소 되지 않습니다.  
  
 열에는 <xref:System.Windows.Controls.DataGrid> 특정 크기에 열을 설정할 수 있습니다 또는 지정 된 경계 내 에서만 자동으로 크기를 설정할 수도 있습니다. 다음 표에서 열 크기를 제어 하도록 설정할 수 있는 속성을 보여 줍니다.  
  
|속성|설명|  
|--------------|-----------------|  
|<xref:System.Windows.Controls.DataGrid.MaxColumnWidth%2A?displayProperty=nameWithType>|모든 열에 대 한 상한을 설정는 <xref:System.Windows.Controls.DataGrid>합니다.|  
|<xref:System.Windows.Controls.DataGridColumn.MaxWidth%2A?displayProperty=nameWithType>|개별 열에 대 한 상한을 설정 합니다. 재정의 <xref:System.Windows.Controls.DataGrid.MaxColumnWidth%2A?displayProperty=nameWithType>합니다.|  
|<xref:System.Windows.Controls.DataGrid.MinColumnWidth%2A?displayProperty=nameWithType>|모든 열에 대 한 하한값을 설정 합니다.는 <xref:System.Windows.Controls.DataGrid>합니다.|  
|<xref:System.Windows.Controls.DataGridColumn.MinWidth%2A?displayProperty=nameWithType>|개별 열에 대 한 하한값을 설정합니다. 재정의 <xref:System.Windows.Controls.DataGrid.MinColumnWidth%2A?displayProperty=nameWithType>합니다.|  
|<xref:System.Windows.Controls.DataGrid.ColumnWidth%2A?displayProperty=nameWithType>|모든 열에 대 한 특정 너비를 설정의 <xref:System.Windows.Controls.DataGrid>합니다.|  
|<xref:System.Windows.Controls.DataGridColumn.Width%2A?displayProperty=nameWithType>|개별 열에 대 한 특정 너비를 설정 합니다. 재정의 <xref:System.Windows.Controls.DataGrid.ColumnWidth%2A?displayProperty=nameWithType>합니다.|  
  
### <a name="datagrid-column-headers"></a>DataGrid 열 머리글  
 기본적으로 <xref:System.Windows.Controls.DataGrid> 열 머리글이 표시 됩니다. 열 머리글을 숨기려면는 <xref:System.Windows.Controls.DataGrid.HeadersVisibility%2A> 속성으로 설정 되어 있어야 <xref:System.Windows.Controls.DataGridHeadersVisibility.Row?displayProperty=nameWithType> 또는 <xref:System.Windows.Controls.DataGridHeadersVisibility.None?displayProperty=nameWithType>합니다. 기본적으로 열 머리글이 표시 되 면 자동으로 크기가 내용에 맞게 합니다. 열 머리글을 설정 하 여 특정 높이 지정할 수 있습니다는 <xref:System.Windows.Controls.DataGrid.ColumnHeaderHeight%2A?displayProperty=nameWithType> 속성입니다.  
  
### <a name="resizing-with-the-mouse"></a>마우스로 크기 조정  
 사용자가 크기를 조정할 수 <xref:System.Windows.Controls.DataGrid> 행과 행 또는 열 머리글 구분선을 끌어서 열입니다. <xref:System.Windows.Controls.DataGrid> 행 또는 열 머리글 구분선을 두 번 클릭 하 여 행과 열의 자동 크기 조정도 지원 합니다. 사용자 특정 열의 크기를 조정 하지 못하도록 하려면 설정는 <xref:System.Windows.Controls.DataGridColumn.CanUserResize%2A?displayProperty=nameWithType> 속성을 `false` 개별 열에 대 한 합니다. 사용자가 모든 열의 크기를 조정 하지 못하도록 하려면 설정는 <xref:System.Windows.Controls.DataGrid.CanUserResizeColumns%2A?displayProperty=nameWithType> 속성을 `false`합니다. 사용자가 모든 행의 크기를 조정 하지 못하도록 하려면 설정는 <xref:System.Windows.Controls.DataGrid.CanUserResizeRows%2A?displayProperty=nameWithType> 속성을 `false`합니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Windows.Controls.DataGrid>  
 <xref:System.Windows.Controls.DataGridColumn>  
 <xref:System.Windows.Controls.DataGridLength>  
 <xref:System.Windows.Controls.DataGridLengthConverter>
