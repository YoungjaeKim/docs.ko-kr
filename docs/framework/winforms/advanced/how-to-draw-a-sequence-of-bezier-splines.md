---
title: "방법: &#233;시퀀스로 Draw; zier 곡선 스플라인"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- splines [Windows Forms], drawing Bezier
- Bezier splines [Windows Forms], drawing sequence of
ms.assetid: 37a0bedb-20c2-4cf0-91fa-a5509e826b30
caps.latest.revision: "9"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: f5bdd9ae29dcbb8397d2fe645e240572aad32a19
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-draw-a-sequence-of-b233zier-splines"></a>방법: &#233;시퀀스로 Draw; zier 곡선 스플라인
사용할 수는 <xref:System.Drawing.Graphics.DrawBeziers%2A> 의 메서드는 <xref:System.Drawing.Graphics> 클래스 일련의 그릴를 베 지 어 스플라인을 연결 합니다.  
  
## <a name="example"></a>예  
 다음 예제에서는 두 개의 연결 된 베 지 어 스플라인을 구성 된 곡선을 그립니다. 첫 번째 베 지 어 스플라인의 끝점에는 두 번째 베 지 어 스플라인의 시작 지점입니다.  
  
 다음 그림에서는 연결 된 스플라인 7 개의 점이 및 보여 줍니다.  
  
 ![베 지 어 스플라인을](../../../../docs/framework/winforms/advanced/media/bezierspline2.png "BezierSpline2")  
  
 [!code-csharp[System.Drawing.ConstructingDrawingCurves#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.ConstructingDrawingCurves#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/VB/Class1.vb#11)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows forms에서 사용하도록 설계되었으며 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기의 매개 변수인 <xref:System.Windows.Forms.PaintEventArgs> `e`가 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Windows Forms의 그래픽 및 그리기](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)  
 [GDI+의 3차원 곡선 스플라인](../../../../docs/framework/winforms/advanced/bezier-splines-in-gdi.md)  
 [곡선 구성 및 그리기](../../../../docs/framework/winforms/advanced/constructing-and-drawing-curves.md)
