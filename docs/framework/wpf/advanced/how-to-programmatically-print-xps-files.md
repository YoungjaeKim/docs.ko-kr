---
title: '방법: 프로그래밍 방식으로 XPS 파일 인쇄'
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-wpf
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- printing XPS files programmatically [WPF]
- XPS files [WPF], printing programmatically
ms.assetid: 0b1c0a3f-b19e-43d6-bcc9-eb3ec4e555ad
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 0b58e617fb04ecaba45ed655dc650459e89453dd
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="how-to-programmatically-print-xps-files"></a>방법: 프로그래밍 방식으로 XPS 파일 인쇄
한 오버 로드를 사용할 수 있습니다는 <xref:System.Printing.PrintQueue.AddJob%2A> 인쇄 하려면 메서드 [!INCLUDE[TLA#tla_xps](../../../../includes/tlasharptla-xps-md.md)] 는 여는 파일을 <xref:System.Windows.Controls.PrintDialog> 또는 원칙적으로 모든 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 전혀 합니다.  
  
 인쇄할 수 있습니다 [!INCLUDE[TLA#tla_xps](../../../../includes/tlasharptla-xps-md.md)] 다를 사용 하 여 파일 <xref:System.Windows.Xps.XpsDocumentWriter.Write%2A> 및 <xref:System.Windows.Xps.XpsDocumentWriter.WriteAsync%2A> 의 메서드는 <xref:System.Windows.Xps.XpsDocumentWriter>합니다. 이에 대한 자세한 내용은 [XPS 문서를 인쇄](http://msdn.microsoft.com/library/849555c8-0c4e-48c0-86bc-a5494c69b36c)합니다.  
  
 다른 방법으로 인쇄 [!INCLUDE[TLA#tla_xps](../../../../includes/tlasharptla-xps-md.md)] 사용 하는 것은 <xref:System.Windows.Controls.PrintDialog.PrintDocument%2A> 또는 <xref:System.Windows.Controls.PrintDialog.PrintVisual%2A> 의 메서드는 <xref:System.Windows.Controls.PrintDialog> 제어 합니다. [인쇄 호출 대화 상자](../../../../docs/framework/wpf/advanced/how-to-invoke-a-print-dialog.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 세 매개 변수를 사용 하는 주요 단계 <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> 메서드는 다음과 같습니다. 아래 예제에서 자세히 설명합니다.  
  
1.  프린터가 XPSDrv 프린터인지 확인합니다. XPSDrv에 대한 자세한 내용은 [인쇄 개요](../../../../docs/framework/wpf/advanced/printing-overview.md)를 참조하세요.  
  
2.  프린터가 XPSDrv 프린터가 아닌 경우 스레드 아파트를 단일 스레드로 설정합니다.  
  
3.  인쇄 서버 및 인쇄 대기열 개체를 인스턴스화합니다.  
  
4.  작업 이름, 인쇄할 파일을 지정 하는 메서드를 호출 및 <xref:System.Boolean> 프린터는 XPSDrv 프린터 인지 여부를 나타내는 플래그입니다.  
  
 아래 예제에서는 디렉터리에서 [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 파일을 모두 일괄 처리 인쇄하는 방법을 보여 줍니다. 세 매개 변수는 디렉터리를 지정 하 라는 메시지를 응용 프로그램이 있지만 <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> 메서드에 필요 하지 않는 한 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]합니다. 전달할 수 있는는 [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 파일 이름 및 경로가 있는 코드 경로에서 사용할 수 있습니다.  
  
 3 개의 매개 변수 <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> 오버 로드 <xref:System.Printing.PrintQueue.AddJob%2A> 단일 스레드 아파트에서 실행 해야 때마다는 <xref:System.Boolean> 매개 변수는 `false`, 비 XPSDrv 프린터를 사용 하는 경우 이어야 합니다. 그러나 [!INCLUDE[TLA#tla_net](../../../../includes/tlasharptla-net-md.md)]의 기본 아파트 상태는 다중 스레드입니다. 이 예제에서 XPSDrv가 아닌 프린터를 가정하므로 이 기본값을 뒤집어야 합니다.  
  
 두 가지 방법으로 기본값을 변경할 수 있습니다. 한 가지 방법은 단순히 추가 하는 <xref:System.STAThreadAttribute> (즉, "`[System.STAThreadAttribute()]`") 응용 프로그램의 첫 번째 줄 바로 위에 `Main` 메서드 (일반적으로 "`static void Main(string[] args)`"). 그러나 많은 응용 프로그램이 필요 하는 `Main` 메서드는 다중 스레드 아파트 상태를 가져야 하는 두 번째 방법은 하므로:에 대 한 호출을 배치 <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> 아파트 상태가 설정 되는 별도 스레드에서 <xref:System.Threading.ApartmentState.STA> 와 <xref:System.Threading.Thread.SetApartmentState%2A>합니다. 아래 예제에서는 두 번째 방법을 사용합니다.  
  
 인스턴스화하여 먼저 적절 하 게 한 <xref:System.Threading.Thread> 개체와 전달는 **PrintXPS** 으로 메서드는 <xref:System.Threading.ThreadStart> 매개 변수입니다. **PrintXPS** 메서드는 샘플의 뒷부분에 정의됩니다. 그런 다음 스레드는 단일 스레드 아파트로 설정됩니다. `Main` 메서드의 나머지 코드는 새 스레드를 시작합니다.  
  
 예제의 핵심은 `static`**BatchXPSPrinter.PrintXPS** 메서드에 있습니다. 인쇄 서버와 인쇄 대기열을 만든 후에 메서드는 사용자에게 [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 파일을 포함하는 디렉터리를 묻는 메시지를 표시합니다. 디렉터리의 존재 및 *.xps 파일의 존재의 유효성을 검사한 후에 메서드는 인쇄 대기열에 이러한 각 파일을 추가합니다. 이 예제에서는 프린터가 있는지 비 XPSDrv 전달 되므로 가정 `false` 의 마지막 매개 변수로 <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> 메서드. 이런 이유로 메서드는 프린터의 페이지 설명 언어로 변환하도록 시도하기 전에 파일에서 [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 표시의 유효성을 검사합니다. 유효성 검사에 실패하면 예외가 throw됩니다. 예제 코드는 예외를 catch하고 사용자에게 알린 후에 계속해서 [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 파일을 처리합니다.  
  
 [!code-csharp[BatchPrintXPSFiles#BatchPrintXPSFiles](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BatchPrintXPSFiles/CSharp/Program.cs#batchprintxpsfiles)]
 [!code-vb[BatchPrintXPSFiles#BatchPrintXPSFiles](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BatchPrintXPSFiles/visualbasic/program.vb#batchprintxpsfiles)]  
  
 XPSDrv 프린터를 사용하는 경우 마지막 매개 변수를 `true`로 설정할 수 있습니다. 이 경우에 [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)]가 프린터의 페이지 설명 언어이므로 메서드는 유효성을 검사하거나 다른 페이지 설명 언어로 변환하지 않고 파일을 프린터로 보냅니다. 모르는 디자인 타임에 있는지 여부는 응용 프로그램을 사용할 XPSDrv 프린터, 응용 프로그램을 읽고 수정할 수 있습니다는 <xref:System.Printing.PrintQueue.IsXpsDevice%2A> 속성 및 내용에 따라 분기 합니다.  
  
 초기에 [!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)] 및 [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)]를 릴리스한 후에 즉시 사용 가능한 몇 개의 XPSDrv 프린터가 있으므로 XPSDrv 프린터인 XPSDrv가 아닌 프린터를 가장해야 합니다. 이렇게 하려면 응용 프로그램을 실행하는 컴퓨터의 다음 레지스트리 키에 있는 파일의 목록에 Pipelineconfig.xml을 추가합니다.  
  
 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Print\Environments\Windows NT x86\Drivers\Version-3\\*\<PseudoXPSPrinter>*\DependentFiles  
  
 여기서 *\<PseudoXPSPrinter>*는 인쇄 대기열입니다. 그런 다음 컴퓨터를 다시 부팅해야 합니다.  
  
 이 가장을 사용 하면 주고 `true` 의 마지막 매개 변수로 <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> 있지만 예외를 발생 하지 않고  *\<PseudoXPSPrinter >* 는 XPSDrv 프린터를 실제로 가비지만 인쇄 됩니다.  
  
 **참고** 편의를 위해 위의 예제에서는 *.xps 확장의 존재를 파일이 [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)]인 테스트로 사용합니다. 그러나 [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 파일이 이 확장명일 필요는 없습니다. [isXPS.exe(isXPS 규칙 도구)](http://msdn.microsoft.com/library/bfbb433f-7ab6-417a-90f0-71443d76bcb3)는 [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)]의 유효성을 검사하기 위해 파일을 테스트하는 한 가지 방법입니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Printing.PrintQueue>  
 <xref:System.Printing.PrintQueue.AddJob%2A>  
 <xref:System.Threading.ApartmentState>  
 <xref:System.STAThreadAttribute>  
 [XPS](http://www.microsoft.com/xps)  
 [XPS 문서를 인쇄합니다.](http://msdn.microsoft.com/library/849555c8-0c4e-48c0-86bc-a5494c69b36c)  
 [관리 되는 관리 되지 않는 스레딩](http://msdn.microsoft.com/library/db425c20-4b2f-4433-bf96-76071c7881e5)  
 [isXPS.exe(isXPS 규칙 도구)](http://msdn.microsoft.com/library/bfbb433f-7ab6-417a-90f0-71443d76bcb3)  
 [WPF의 문서](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)  
 [인쇄 개요](../../../../docs/framework/wpf/advanced/printing-overview.md)
