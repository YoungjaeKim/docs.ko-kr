---
title: Windows Forms DataGridView 컨트롤에서 새 레코드에 행 사용
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-winforms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- DataGridView control [Windows Forms], adding rows for new records
- rows [Windows Forms], new records
- DataGridView control [Windows Forms], data entry
ms.assetid: 6110f1ea-9794-442c-a98a-f104a1feeaf4
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: e349a33c90d08606da09ebdf32de6dedb8d6a52c
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="using-the-row-for-new-records-in-the-windows-forms-datagridview-control"></a>Windows Forms DataGridView 컨트롤에서 새 레코드에 행 사용
사용 하는 경우는 <xref:System.Windows.Forms.DataGridView> 응용 프로그램에서 데이터 편집을 위해 종종 하려는 사용자에 게 데이터 저장소에 새 데이터 행을 추가 하는 기능을 제공 합니다. <xref:System.Windows.Forms.DataGridView> 제어는 항상 마지막 행으로 표시 되어 새 레코드에 대 한 행을 제공 하 여이 기능을 지원 합니다. 행 머리글에 별표 (*) 기호로 표시 됩니다. 다음 섹션에서는 프로그램 새 레코드에 대 한 행을 사용 하도록 설정할 때 고려해 야 하는 기능 중 일부에 대해 설명 합니다.  
  
## <a name="displaying-the-row-for-new-records"></a>새 레코드에 대 한 행을 표시합니다.  
 사용 하 여는 <xref:System.Windows.Forms.DataGridView.AllowUserToAddRows%2A> 새 레코드에 대 한 행이 표시 되는지 여부를 나타내는 속성입니다. 이 속성의 기본값은 `true`입니다.  
  
 데이터 바인딩된 대/소문자를 새 레코드에 대 한 행이 표시 될 경우는 <xref:System.Windows.Forms.DataGridView.AllowUserToAddRows%2A> 컨트롤의 속성 및 <xref:System.ComponentModel.IBindingList.AllowNew%2A?displayProperty=nameWithType> 데이터 소스의 속성은 모두 `true`합니다. 중 하나에 해당 하는 경우 `false` 다음 행에 표시 되지 것입니다.  
  
## <a name="populating-the-row-for-new-records-with-default-data"></a>기본 데이터와 함께 새 레코드에 대 한 행을 채우기  
 현재 행으로 새 레코드에 대 한 행을 선택할 때의 <xref:System.Windows.Forms.DataGridView> 발생는 <xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded> 이벤트입니다.  
  
 이 이벤트는 새에 대 한 액세스를 제공 <xref:System.Windows.Forms.DataGridViewRow> 기본 데이터와 함께 새 행을 채울 수 있습니다. 자세한 내용은 참조 [하는 방법: Windows Forms DataGridView 컨트롤에 새 행에 대 한 기본 값 지정](../../../../docs/framework/winforms/controls/specify-default-values-for-new-rows-in-the-datagrid.md)  
  
## <a name="the-rows-collection"></a>행 컬렉션  
 새 레코드에 대 한 행에 포함 되어는 <xref:System.Windows.Forms.DataGridView> 컨트롤의 <xref:System.Windows.Forms.DataGridView.Rows%2A> 컬렉션 두 가지 측면에서 다르게 하지만 동작:  
  
-   새 레코드에 대 한 행을 제거할 수 없습니다는 <xref:System.Windows.Forms.DataGridView.Rows%2A> 컬렉션 프로그래밍 방식으로 합니다. <xref:System.InvalidOperationException> 이 시도 하는 경우에 throw 됩니다. 또한 사용자 새 레코드에 대 한 행을 삭제할 수 없습니다. <xref:System.Windows.Forms.DataGridViewRowCollection.Clear%2A?displayProperty=nameWithType> 메서드에서이 행을 제거 하지 않습니다는 <xref:System.Windows.Forms.DataGridView.Rows%2A> 컬렉션입니다.  
  
-   새 레코드에 대 한 행 다음 행을 추가할 수 있습니다. <xref:System.InvalidOperationException> 이 시도 하는 경우 발생 합니다. 결과적으로, 새 레코드에 대 한 행은 항상 마지막 행에는 <xref:System.Windows.Forms.DataGridView> 제어 합니다. 메서드에서 <xref:System.Windows.Forms.DataGridViewRowCollection> 행을 추가 하는-<xref:System.Windows.Forms.DataGridViewRowCollection.Add%2A>, <xref:System.Windows.Forms.DataGridViewRowCollection.AddCopy%2A>, 및 <xref:System.Windows.Forms.DataGridViewRowCollection.AddCopies%2A>-모든 메서드를 호출 삽입 내부적으로 새 레코드에 대 한 행이 있는 경우.  
  
## <a name="visual-customization-of-the-row-for-new-records"></a>새 레코드에 대 한 행의 시각적 사용자 지정  
 지정한 행에 기반 하는 새 레코드에 대 한 행을 만들 때는 <xref:System.Windows.Forms.DataGridView.RowTemplate%2A> 속성입니다. 이 행에 대해 지정 되지 않은 모든 셀 스타일은 다른 속성에서 상속 됩니다. 셀 스타일 상속 하는 방법에 대 한 자세한 내용은 참조 [Windows Forms DataGridView 컨트롤의 셀 스타일](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)합니다.  
  
 각 셀에서 새 레코드를 검색에 대 한 행의 셀에서 표시 되는 초기 값 <xref:System.Windows.Forms.DataGridViewCell.DefaultNewRowValue%2A> 속성입니다. 형식의 셀에 대 한 <xref:System.Windows.Forms.DataGridViewImageCell>,이 속성은 자리 표시자 이미지 반환 합니다. 그렇지 않으면이 속성은 반환 `null`합니다. 사용자 지정 값을 반환 하려면이 속성을 재정의할 수 있습니다. 그러나, 이러한 초기 값으로 바꿀 수 있습니다는 <xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded> 포커스가 새 레코드에 대 한 행을 입력할 때 이벤트 처리기입니다.  
  
 화살표 또는 별표는이 행의이 헤더에 대 한 표준 아이콘 공개적으로 노출 되지 않습니다. 사용자 지정 만들기 해야 아이콘을 사용자 지정 하려는 경우 <xref:System.Windows.Forms.DataGridViewRowHeaderCell> 클래스입니다.  
  
 표준 아이콘 사용는 <xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A> 의 속성은 <xref:System.Windows.Forms.DataGridViewCellStyle> 행 머리글 셀에서 사용에서 합니다. 완전히 표시할 수 있는 공간이 없는 경우에 표준 아이콘 렌더링 되지 않습니다.  
  
 행 머리글 셀에 설정 하는 문자열 값 및 텍스트 및 아이콘에 대 한 공간이 충분 하지 않은 경우 아이콘이 먼저 삭제 됩니다.  
  
## <a name="sorting"></a>정렬  
 바인딩되지 않은 모드의 끝에 새 레코드가 추가 항상 됩니다는 <xref:System.Windows.Forms.DataGridView> 사용자의 콘텐츠를 정렬 하는 경우에는 <xref:System.Windows.Forms.DataGridView>합니다. 사용자를 올바른 위치로; 행을 정렬 하려면 정렬을 다시 적용 해야 합니다. 이 동작은 비슷합니다는 <xref:System.Windows.Forms.ListView> 제어 합니다.  
  
 데이터 바인딩 및 가상 모드의 경우 삽입 동작에서는 정렬이 적용 될 때 데이터 모델의 구현에 종속 됩니다. 에 대 한 [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)], 행이 올바른 위치에 즉시 정렬 됩니다.  
  
## <a name="other-notes-on-the-row-for-new-records"></a>새 레코드에 대 한 행의 기타 참고 사항  
 설정할 수 없습니다.는 <xref:System.Windows.Forms.DataGridViewRow.Visible%2A> 속성을이 행의 `false`합니다. <xref:System.InvalidOperationException> 이 시도 하는 경우 발생 합니다.  
  
 항상 새 레코드의 행을 선택 하지 않은 상태에서 만들어집니다.  
  
## <a name="virtual-mode"></a>가상 모드  
 가상 모드 구현 하는 경우에 행 추가 롤백할 시점을 및 데이터 모델에 새 레코드에 대 한 행을 필요로 하는 시기를 추적 해야 합니다. 이 기능의 정확한 구현은 구현에 따라 데이터 모델 및 해당 트랜잭션 의미 체계의 예를 들어, 커밋 범위는 셀 또는 행 수준에서 인지 합니다. 자세한 내용은 참조 [Windows Forms DataGridView 컨트롤의 가상 모드](../../../../docs/framework/winforms/controls/virtual-mode-in-the-windows-forms-datagridview-control.md)합니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Windows.Forms.DataGridView>  
 <xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded?displayProperty=nameWithType>  
 [Windows Forms DataGridView 컨트롤의 데이터 입력](../../../../docs/framework/winforms/controls/data-entry-in-the-windows-forms-datagridview-control.md)  
 [방법: Windows Forms DataGridView 컨트롤에서 새 행에 기본값 지정](../../../../docs/framework/winforms/controls/specify-default-values-for-new-rows-in-the-datagrid.md)
