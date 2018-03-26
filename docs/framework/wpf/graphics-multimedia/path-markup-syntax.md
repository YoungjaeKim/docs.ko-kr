---
title: 경로 태그 구문
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
- attribute usage in XAML [WPF]
- XAML [WPF], attribute usage
- graphics [WPF], PathGeometry class
- XAML [WPF], object element usage
ms.assetid: b8586241-a02d-486e-9223-e1e98e047f41
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 9cd8f9b14f114060ebec8e336c1212d61fa19c83
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="path-markup-syntax"></a>경로 태그 구문
그러나 경로에 대해서는 [Shape 및 기본 그리기 개요 WPF에서에서](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md) 및 [기 하 도형 개요](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md),이 항목에 자세히 설명 경로 지정 하는 데 강력 하 고 복잡 한 최소 언어 더 조밀 하 게 사용 하 여 기 하 도형 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]합니다.  
  
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>전제 조건  
 이 항목을 이해 하려면의 기본 기능에 잘 알고 있어야 <xref:System.Windows.Media.Geometry> 개체입니다. 자세한 내용은 참조는 [기 하 도형 개요](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)합니다.  
  
<a name="abouthisdocument"></a>   
## <a name="streamgeometry-and-pathfigurecollection-mini-languages"></a>StreamGeometry 및 PathFigureCollection 미니 언어  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 기하학적 경로 설명 하기 위해 미니 언어를 제공 하는 두 개의 클래스를 제공: <xref:System.Windows.Media.StreamGeometry> 및 <xref:System.Windows.Media.PathFigureCollection>합니다.  
  
-   사용 하면는 <xref:System.Windows.Media.StreamGeometry> 형식의 속성을 설정할 때 최소 언어 <xref:System.Windows.Media.Geometry>와 같은 <xref:System.Windows.UIElement.Clip%2A> 속성은 <xref:System.Windows.UIElement> 또는 <xref:System.Windows.Shapes.Path.Data%2A> 속성의는 <xref:System.Windows.Shapes.Path> 요소입니다. 다음 예제에서는 특성 구문을 사용 하 여 한 <xref:System.Windows.Media.StreamGeometry>합니다.  
  
     [!code-xaml[GeometrySample_snip_XAML#GraphicsMMStreamGeometryAttributeSyntaxInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample_snip_XAML/CS/MiniLanguageExample.xaml#graphicsmmstreamgeometryattributesyntaxinline)]  
  
-   사용 하면는 <xref:System.Windows.Media.PathFigureCollection> 설정 하는 경우 최소 언어는 <xref:System.Windows.Media.PathGeometry.Figures%2A> 속성은 <xref:System.Windows.Media.PathGeometry>합니다. 다음 예제는 특성 구문을 사용 하 여 한 <xref:System.Windows.Media.PathFigureCollection> 에 대 한는 <xref:System.Windows.Media.PathGeometry>합니다.  
  
     [!code-xaml[GeometrySample_snip_XAML#GraphicsMMPathFigureCollectionAttributeSyntaxInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample_snip_XAML/CS/MiniLanguageExample.xaml#graphicsmmpathfigurecollectionattributesyntaxinline)]  
  
 앞의 예제에서 볼 수 있는 것처럼 두 개의 미니 언어는 매우 비슷합니다. 사용할 수는 항상는 <xref:System.Windows.Media.PathGeometry> 사용할 수 있는 경우에는 <xref:System.Windows.Media.StreamGeometry>너무; 어떤 언제 사용 하나요? 사용 하 여 한 <xref:System.Windows.Media.StreamGeometry> 경로를 수정 하며 만든 후 필요 하지 않을 때 사용 하 여 한 <xref:System.Windows.Media.PathGeometry> 경로를 수정 해야 하는 경우.  
  
 간의 차이점에 대 한 자세한 내용은 <xref:System.Windows.Media.PathGeometry> 및 <xref:System.Windows.Media.StreamGeometry> 개체 참조는 [기 하 도형 개요](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)합니다.  
  
### <a name="a-note-about-white-space"></a>공백에 대한 참고 사항  
 간단히 말해서 이어지는 구문 섹션에는 단일 공백이 표시되지만 단일 공백이 표시되는 모든 위치에서 여러 개의 공백을 사용해도 됩니다.  
  
 두 개의 숫자를 실제로 쉼표나 공백으로 구분할 필요는 없으나 결과 문자열이 모호하지 않는 한도에서만 허용됩니다. 예를 들어, `2..3` 은 실제로: "2"입니다. ".3"의 두 숫자입니다. 마찬가지로, `2-3` 은 "2"와 "-3"입니다. 명령 앞뒤에는 공백이 필요하지 않습니다.  
  
### <a name="syntax"></a>구문  
 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 사용 구문에 대 한 특성을 <xref:System.Windows.Media.StreamGeometry> 는 선택적 구성 <xref:System.Windows.Media.FillRule> 값 및 하나 이상의 그림 설명 합니다.  
  
|StreamGeometry XAML 특성 사용|  
|-----------------------------------------|  
|`<` *object* *property* `="`[ `fillRule`] `figureDescription`[ `figureDescription`]* `" ... />`|  
  
 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 사용 구문에 대 한 특성을 <xref:System.Windows.Media.PathFigureCollection> 하나 이상의 그림 설명으로 구성 됩니다.  
  
|PathFigureCollection XAML 특성 사용|  
|-----------------------------------------------|  
|`<` *object* *property* `="` `figureDescription`[ `figureDescription`]* `" ... />`|  
  
|용어|설명|  
|----------|-----------------|  
|*fillRule*|<xref:System.Windows.Media.FillRule?displayProperty=nameWithType><br /><br /> 지정 여부는 <xref:System.Windows.Media.StreamGeometry> 사용 하 여는 <xref:System.Windows.Media.FillRule.EvenOdd> 또는 <xref:System.Windows.Media.FillRule.Nonzero> <xref:System.Windows.Media.PathGeometry.FillRule%2A>합니다.<br /><br /> -   `F0` 지정 된 <xref:System.Windows.Media.FillRule.EvenOdd> 채우기 규칙입니다.<br />-   `F1` 지정 된 <xref:System.Windows.Media.FillRule.Nonzero> 채우기 규칙입니다.<br /><br /> 하위 경로 기본 동작을 사용 하 여이 명령을 생략 하면 <xref:System.Windows.Media.FillRule.EvenOdd>합니다. 이 명령을 지정하는 경우 맨 앞에 배치해야 합니다.|  
|*figureDescription*|이동 명령, 그리기 명령 및 선택적 닫기 명령으로 구성된 그림입니다.<br /><br /> `moveCommand` `drawCommands`  `[` `closeCommand` `]`|  
|*moveCommand*|그림의 시작점을 지정하는 이동 명령입니다. 참조는 [이동 명령을](#themovecommand) 섹션.|  
|*drawCommands*|그림의 콘텐츠를 설명하는 하나 이상의 그리기 명령입니다. 참조는 [그리기 명령](#drawcommands) 섹션.|  
|*closeCommand*|그림을 닫는 선택적 닫기 명령입니다. 참조는 [닫기 명령을](#closecommand) 섹션.|  
  
<a name="themovecommand"></a>   
## <a name="move-command"></a>이동 명령  
 새 그림의 시작점을 지정합니다.  
  
|구문|  
|------------|  
|`M` *startPoint*<br /><br /> 또는<br /><br /> `m` *startPoint*|  
  
|용어|설명|  
|----------|-----------------|  
|*startPoint*|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 새 그림의 시작점입니다.|  
  
 대문자 `M` 나타냅니다 `startPoint` 값이 절대 값인지; 소문자 `m` 나타냅니다 `startPoint` 이전 시점에 대 한 오프셋은 또는 (0, 0) 존재 하지 않는 경우. 이동 명령 뒤에 여러 점을 나열하는 경우 선 명령을 지정했어도 해당 점으로 선이 그려집니다.  
  
<a name="drawcommands"></a>   
## <a name="draw-commands"></a>그리기 명령  
 그리기 명령은 여러 도형 명령으로 구성될 수 있습니다. 선, 수평선, 수직선, 입방형 3차원 곡선, 정방형 3차원 곡선, 부드러운 입방형 3차원 곡선, 부드러운 정방형 3차원 곡선 및 타원형 호 등의 도형 명령을 사용할 수 있습니다.  
  
 대문자 또는 소문자를 사용하여 각 명령을 입력합니다. 대문자는 절대값을 나타내고 소문자는 상대값을 나타냅니다. 해당 세그먼트에 대한 제어점은 이전 예제의 끝점을 기준으로 합니다. 동일한 형식의 둘 이상의 명령을 순차적으로 입력할 때 중복 명령 입력; 생략할 수 있습니다. 예를 들어 `L 100,200 300,400` 같습니다 `L 100,200 L 300,400`합니다. 다음 표에서 **이동** 및 **그리기** 명령입니다.  
  
### <a name="line-command"></a>선 명령  
 현재 점과 지정된 끝점 간에 직선을 만듭니다. `l 20 30` 및 `L 20,30` 은 유효한 예 **줄** 명령입니다.  
  
|구문|  
|------------|  
|`L` *endPoint*<br /><br /> 또는<br /><br /> `l` *endPoint*|  
  
|용어|설명|  
|----------|-----------------|  
|*endPoint*|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 선의 끝점입니다.|  

대문자 `L` 나타냅니다 `endPoint` 값이 절대 값인지; 소문자 `l` 나타냅니다 `endPoint` 이전 시점에 대 한 오프셋은 또는 (0, 0) 존재 하지 않는 경우.

### <a name="horizontal-line-command"></a>수평선 명령  
 현재 점과 지정된 x 좌표 간에 수평선을 만듭니다. `H 90`은 유효한 수평선 명령의 예입니다.

  
|구문|  
|------------|  
|`H`  *x*<br /><br /> 또는<br /><br /> `h`  *x*|  
  
|용어|설명|  
|----------|-----------------|  
|*x*|<xref:System.Double?displayProperty=nameWithType><br /><br /> 선 끝점의 x 좌표입니다.|  
  
대문자 `H` 나타냅니다 `x` 값이 절대 값인지; 소문자 `h` 나타냅니다 `x` 이전 시점에 대 한 오프셋은 또는 (0, 0) 존재 하지 않는 경우.
  
### <a name="vertical-line-command"></a>수직선 명령  
 현재 점과 지정된 y 좌표 간에 수직선을 만듭니다. `v 90`은 유효한 수직선 명령의 예입니다.

  
|구문|  
|------------|  
|`V`  *y*<br /><br /> 또는<br /><br /> `v`  *y*|  
  
|용어|설명|  
|----------|-----------------|  
|*y*|<xref:System.Double?displayProperty=nameWithType><br /><br /> 선 끝점의 y 좌표입니다.|  

대문자 `V` 나타냅니다 `y` 값이 절대 값인지; 소문자 `v` 나타냅니다 `y` 이전 시점에 대 한 오프셋은 또는 (0, 0) 존재 하지 않는 경우.  
    
### <a name="cubic-bezier-curve-command"></a>입방형 3차원 곡선 명령  
 지정 된 두 개의 제어점을 사용 하 여 현재 지점과 지정한 끝점 간의 입방 형 3 차원 곡선을 만듭니다 (`controlPoint`1 및 `controlPoint`2). `C 100,200 200,400 300,200`은 유효한 곡선 명령의 예입니다.  
  
|구문|  
|------------|  
|`C` `controlPoint`1`controlPoint`2`endPoint`<br /><br /> 또는<br /><br /> `c` `controlPoint`1`controlPoint`2`endPoint`|  
  
|용어|설명|  
|----------|-----------------|  
|`controlPoint`1|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 곡선의 시작 접선을 결정하는 곡선의 첫 번째 제어점입니다.|  
|`controlPoint`2|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 곡선의 끝 접선을 결정하는 곡선의 두 번째 제어점입니다.|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 곡선을 그릴 지점입니다.|  
  
### <a name="quadratic-bezier-curve-command"></a>정방형 3차원 곡선 명령  
 지정 된 제어점을 사용 하 여 현재 지점과 지정한 끝점 사이 정방형 3 차원 곡선을 만듭니다 (`controlPoint`). `q 100,200 300,200`은 유효한 정방형 3차원 곡선 명령의 예입니다.  
  
|구문|  
|------------|  
|`Q` `controlPoint` `endPoint`<br /><br /> 또는<br /><br /> `q` `controlPoint` `endPoint`|  
  
|용어|설명|  
|----------|-----------------|  
|`controlPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 곡선의 시작 및 끝 접선을 결정하는 곡선의 제어점입니다.|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 곡선을 그릴 지점입니다.|  
  
### <a name="smooth-cubic-bezier-curve-command"></a>부드러운 입방형 3차원 곡선 명령  
 현재 점과 지정된 끝점 간에 입방형 3차원 곡선을 만듭니다. 첫 번째 제어점은 현재 점을 기준으로 이전 명령의 두 번째 제어점의 리플렉션으로 간주됩니다. 이전 명령이 없거나 이전 명령이 입방형 3차원 곡선 명령 또는 부드러운 입방 형 3차원 곡선 명령이 아닌 경우 첫 번째 제어점이 현재 점과 일치한다고 가정합니다. 두 번째 제어점, 곡선의 끝에 대 한 제어 지점으로 지정 `controlPoint`2입니다. 예를 들어 `S 100,200 200,300` 올바른 부드러운 입방 형 3 베 지 어 곡선 명령입니다.  
  
|구문|  
|------------|  
|`S` `controlPoint`2`endPoint`<br /><br /> 또는<br /><br /> `s` `controlPoint`2`endPoint`|  
  
|용어|설명|  
|----------|-----------------|  
|`controlPoint`2|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 곡선의 끝 접선을 결정하는 곡선의 제어점입니다.|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 곡선을 그릴 지점입니다.|  
  
### <a name="smooth-quadratic-bezier-curve-command"></a>부드러운 정방형 3차원 곡선 명령  
 현재 점과 지정된 끝점 간에 정방형 3차원 곡선을 만듭니다. 제어점은 현재 점을 기준으로 이전 명령의 제어점의 리플렉션으로 간주됩니다. 이전 명령이 없거나 이전 명령이 정방형 3차원 곡선 명령 또는 부드러운 정방 형 3차원 곡선 명령이 아닌 경우 제어점이 현재 점과 일치합니다.  
  
|구문|  
|------------|  
|`T` `controlPoint` `endPoint`<br /><br /> 또는<br /><br /> `t` `controlPoint` `endPoint`|  
  
|용어|설명|  
|----------|-----------------|  
|`controlPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 곡선의 시작 접선을 결정하는 곡선의 제어점입니다.|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 곡선을 그릴 지점입니다.|  
  
### <a name="elliptical-arc-command"></a>타원형 호 명령  
 현재 점과 지정된 끝점 간에 타원형 호를 만듭니다.  
  
|구문|  
|------------|  
|`A` `size` `rotationAngle` `isLargeArcFlag` `sweepDirectionFlag` `endPoint`<br /><br /> 또는<br /><br /> `a` `size` `rotationAngle` `isLargeArcFlag` `sweepDirectionFlag` `endPoint`|  
  
|용어|설명|  
|----------|-----------------|  
|`size`|<xref:System.Windows.Size?displayProperty=nameWithType><br /><br /> 원호의 X 및 y 반지름입니다.|  
|`rotationAngle`|<xref:System.Double?displayProperty=nameWithType><br /><br /> 타원의 회전 각도입니다.|  
|`isLargeArcFlag`|호의 각도가 180도보다 커야 하면 1로 설정하고, 그렇지 않으면 0으로 설정합니다.|  
|`sweepDirectionFlag`|호가 양의 각도 방향으로 그려지면 1로 설정하고, 그렇지 않으면 0으로 설정합니다.|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 호를 그리는 점입니다.|  
  
<a name="closecommand"></a>   
## <a name="the-close-command"></a>닫기 명령  
 현재 그림을 끝내고 현재 점을 그림의 시작 점에 연결하는 선을 만듭니다. 이 명령은 그림의 마지막 세그먼트와 첫 번째 세그먼트 사이에 선 조인(모서리)을 만듭니다.  
  
|구문|  
|------------|  
|`Z`<br /><br /> 또는<br /><br /> `z`|  

<a name="pointsyntax"></a>   
## <a name="point-syntax"></a>점 구문  
 점의 x 및 y 좌표를 설명 합니다. 여기서 (0, 0)은 왼쪽된 위 모퉁이입니다.
  
|구문|  
|------------|  
|`x` `,` `y`<br /><br /> 또는<br /><br /> `x` `y`|  
  
|용어|설명|  
|----------|-----------------|  
|`x`|<xref:System.Double?displayProperty=nameWithType><br /><br /> 점의 X 좌표입니다.|  
|`y`|<xref:System.Double?displayProperty=nameWithType><br /><br /> 점의 Y 좌표입니다.|  
  
<a name="specialvalues"></a>   
## <a name="special-values"></a>특수 값  
 표준 숫자 값 대신 다음과 같은 특수 값을 사용할 수도 있습니다. 이러한 값은 대/소문자를 구분합니다.  
  
 Infinity  
 나타냅니다 <xref:System.Double.PositiveInfinity?displayProperty=nameWithType>합니다.  
  
 -Infinity  
 나타냅니다 <xref:System.Double.NegativeInfinity?displayProperty=nameWithType>합니다.  
  
 NaN  
 나타냅니다 <xref:System.Double.NaN?displayProperty=nameWithType>합니다.  
  
 과학적 표기법을 사용할 수도 있습니다. 예를 들어 `+1.e17` 유효한 값이 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Windows.Shapes.Path>  
 <xref:System.Windows.Media.StreamGeometry>  
 <xref:System.Windows.Media.PathGeometry>  
 <xref:System.Windows.Media.PathFigureCollection>  
 [WPF에서 Shape 및 기본 그리기 개요](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md)  
 [Geometry 개요](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)  
 [방법 항목](../../../../docs/framework/wpf/graphics-multimedia/geometries-how-to-topics.md)
