---
title: "방법: 이미지로 영역 그리기"
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
- images [WPF], painting with
- painting [WPF], with images
- brushes [WPF], painting with images
ms.assetid: 3432c533-1fc7-492d-94ee-0b13d60125ae
caps.latest.revision: "14"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 90e346990696301d27ea329ea4255258562b353c
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-paint-an-area-with-an-image"></a>방법: 이미지로 영역 그리기
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.ImageBrush> 이미지 영역을 그리는 클래스입니다. <xref:System.Windows.Media.ImageBrush> 변수에 지정 된 단일 이미지를 표시 합니다. 해당 <xref:System.Windows.Media.ImageBrush.ImageSource%2A> 속성입니다.  
  
## <a name="example"></a>예  
 다음 예제에서는 그리기는 <xref:System.Windows.Controls.Control.Background%2A> 를 사용 하 여 단추는 <xref:System.Windows.Media.ImageBrush>합니다.  
  
 [!code-csharp[UsingImageBrush_snip#ImageBrushExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/PaintingWithImagesExample.cs#imagebrushexamplewholepage)]  
  
 기본적으로는 <xref:System.Windows.Media.ImageBrush> 완전히 사용자 칠하고 있는 영역을 채우도록 이미지를 확장 합니다. 위의 예제에서는 이미지가 단추를 채우도록 확장되므로 이미지가 왜곡될 수 있습니다. 설정 하 여이 동작을 제어할 수는 <xref:System.Windows.Media.TileBrush.Stretch%2A> 속성 <xref:System.Windows.Media.TileBrush> 를 <xref:System.Windows.Media.Stretch.Uniform> 또는 <xref:System.Windows.Media.Stretch.UniformToFill>, 이미지의 가로 세로 비율을 유지 하도록 브러시에 이르게 합니다.  
  
 설정 하는 경우는 <xref:System.Windows.Media.TileBrush.Viewport%2A> 및 <xref:System.Windows.Media.TileBrush.TileMode%2A> 속성의는 <xref:System.Windows.Media.ImageBrush>, 반복을 만들 수 있습니다. 다음 예제에서는 이미지에서 만들어지는 패턴을 사용하여 단추를 그립니다.  
  
 [!code-csharp[UsingImageBrush_snip#TiledImageBrushExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/TiledImageBrushExample.cs#tiledimagebrushexamplewholepage)]
 [!code-vb[UsingImageBrush_snip#TiledImageBrushExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UsingImageBrush_snip/VisualBasic/TiledImageBrushExample.vb#tiledimagebrushexamplewholepage)]  
  
 에 대 한 자세한 내용은 <xref:System.Windows.Media.ImageBrush> 클래스를 참조 하십시오. [이미지, 그리기, 및 시각적 개체를 사용 하 여 그리기](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)합니다.  
  
 이 코드 예제는 제공 된 큰 예제의 일부는 <xref:System.Windows.Media.ImageBrush> 클래스입니다. 전체 샘플을 참조 하십시오. [ImageBrush 샘플](http://go.microsoft.com/fwlink/?LinkID=160005)합니다.  
  
## <a name="see-also"></a>참고 항목  
 [이미지, 그림 및 시각적 표시로 그리기](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)
