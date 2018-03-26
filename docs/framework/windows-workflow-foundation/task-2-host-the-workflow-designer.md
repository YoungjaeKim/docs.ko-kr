---
title: '작업 2: 워크플로 디자이너 호스팅'
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0a29b138-270d-4846-b78e-2b875e34e501
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 991f3d25a81e90ab779936c993ec7dd09a71b794
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="task-2-host-the-workflow-designer"></a>작업 2: 워크플로 디자이너 호스팅
이 항목에서는 [!INCLUDE[wfd1](../../../includes/wfd1-md.md)] 응용 프로그램에서 [!INCLUDE[avalon1](../../../includes/avalon1-md.md)] 인스턴스를 호스트하는 절차를 설명합니다.  
  
 절차는 구성의 **그리드** 디자이너에 포함 된 컨트롤의 인스턴스를 프로그래밍 방식으로 만듭니다는 <xref:System.Activities.Presentation.WorkflowDesigner> 기본값을 포함 하 <xref:System.Activities.Statements.Sequence> 활동을 제공 하기 디자이너 메타 데이터를 등록 합니다. 모든 기본 제공 활동 및 호스트에 대 한 디자이너 지원을 [!INCLUDE[wfd2](../../../includes/wfd2-md.md)] 에 [!INCLUDE[avalon2](../../../includes/avalon2-md.md)] 응용 프로그램입니다.  
  
### <a name="to-host-the-workflow-designer"></a>워크플로 디자이너를 호스트하려면  
  
1.  만든는 HostingApplication 열기 프로젝트 [작업 1: 새 Windows Presentation Foundation 응용 프로그램 만들기](../../../docs/framework/windows-workflow-foundation/task-1-create-a-new-wpf-app.md)합니다.  
  
2.  [!INCLUDE[wfd2](../../../includes/wfd2-md.md)]를 쉽게 사용할 수 있도록 창의 크기를 조정합니다. 이 위해 선택 **MainWindow** 디자이너를 표시 하려면 F4 키를 누릅니다.는 **속성** 창에는 **레이아웃** 섹션, 설정는 **너비** 값 600에 및 **높이** 350의 값입니다.  
  
3.  선택 하 여 표 이름을 설정는 **그리드** 디자이너에서 패널 (안의 상자를 클릭는 **MainWindow**) 설정의 **이름** 맨 위에 있는 속성은  **속성** 을 "grid1"입니다.  
  
4.  에 **속성** 창에서 줄임표를 클릭 (**...** ) 옆에 `ColumnDefinitions` 속성을 열고는 **컬렉션 편집기** 대화 상자.  
  
5.  에 **컬렉션 편집기** 대화 상자를 클릭는 **추가** 단추를 세 번 레이아웃에 세 개의 열을 삽입 합니다. 첫 번째 열이 포함 됩니다는 **도구 상자**, 두 번째 열을 호스팅하는 [!INCLUDE[wfd2](../../../includes/wfd2-md.md)], 세 번째 열은 속성 검사자에 사용 됩니다.  
  
6.  설정의 `Width` 가운데 열의 값으로 속성을 "4 *"입니다.  
  
7.  **확인** 을 클릭하여 변경 내용을 저장합니다. 다음 XAML이 MainWindow.xaml 파일에 추가됩니다.  
  
    ```xml  
    <Grid Name="grid1">  
        <Grid.ColumnDefinitions>  
            <ColumnDefinition />  
            <ColumnDefinition Width="4*" />  
            <ColumnDefinition />  
        </Grid.ColumnDefinitions>  
    </Grid>  
    ```  
  
8.  **솔루션 탐색기**MainWindow.xaml을 마우스 오른쪽 단추로 클릭 하 고 선택 **코드 보기**합니다. 다음 단계에 따라 코드를 수정합니다.  
  
    1.  다음 네임스페이스를 추가합니다.  
  
        ```csharp  
        using System.Activities;  
        using System.Activities.Core.Presentation;  
        using System.Activities.Presentation;  
        using System.Activities.Presentation.Metadata;  
        using System.Activities.Presentation.Toolbox;  
        using System.Activities.Statements;  
        using System.ComponentModel;  
        ```  
  
    2.  <xref:System.Activities.Presentation.WorkflowDesigner>의 인스턴스를 보관할 전용 멤버 필드를 선언하려면 `MainWindow`에 다음 코드를 추가합니다.  
  
        ```csharp  
        public partial class MainWindow : Window  
        {  
            private WorkflowDesigner wd;  
  
            public MainWindow()  
            {  
                InitializeComponent();  
            }  
        }  
        ```  
  
    3.  다음 `AddDesigner` 메서드를 `MainWindow` 클래스에 추가합니다. 구현 인스턴스를 만듭니다는 <xref:System.Activities.Presentation.WorkflowDesigner>, 추가 <xref:System.Activities.Statements.Sequence> 활동, 다음 grid1의 가운데 열에 배치 하 고 **그리드**합니다.  
  
        ```csharp  
        private void AddDesigner()  
        {  
            //Create an instance of WorkflowDesigner class.  
            this.wd = new WorkflowDesigner();  
  
            //Place the designer canvas in the middle column of the grid.  
            Grid.SetColumn(this.wd.View, 1);  
  
            //Load a new Sequence as default.  
            this.wd.Load(new Sequence());  
  
            //Add the designer canvas to the grid.  
            grid1.Children.Add(this.wd.View);  
        }  
        ```  
  
    4.  디자이너 메타데이터를 등록하여 모든 기본 제공 활동에 대한 디자이너 지원을 추가합니다. 그러면 도구 상자의 활동을 <xref:System.Activities.Statements.Sequence>의 원래 [!INCLUDE[wfd2](../../../includes/wfd2-md.md)] 활동으로 끌어 놓을 수 있습니다. 이렇게 하려면 `RegisterMetadata` 메서드를 `MainWindow` 클래스에 추가합니다.  
  
        ```csharp  
        private void RegisterMetadata()  
        {               
            DesignerMetadata dm = new DesignerMetadata();  
            dm.Register();  
        }  
        ```  
  
         [!INCLUDE[crabout](../../../includes/crabout-md.md)] 참조 활동 디자이너를 등록 [하는 방법: 사용자 지정 활동 디자이너를 만드는](../../../docs/framework/windows-workflow-foundation/how-to-create-a-custom-activity-designer.md)합니다.  
  
    5.  `MainWindow` 클래스 생성자에서 앞에서 선언한 메서드에 호출을 추가하여 디자이너 지원을 위한 메타데이터를 등록하고 <xref:System.Activities.Presentation.WorkflowDesigner>를 만듭니다.  
  
        ```csharp  
        public MainWindow()  
        {  
            InitializeComponent();  
  
            // Register the metadata  
            RegisterMetadata();  
  
            // Add the WFF Designer  
            AddDesigner();  
        }  
        ```  
  
        > [!NOTE]
        >  `RegisterMetadata` 메서드는 <xref:System.Activities.Statements.Sequence> 활동을 포함한 기본 제공 활동의 디자이너 메타데이터를 등록합니다. `AddDesigner` 메서드는 <xref:System.Activities.Statements.Sequence> 활동을 사용하기 때문에 `RegisterMetadata` 메서드를 먼저 호출해야 합니다.  
  
9. F5 키를 눌러 솔루션을 빌드하고 실행합니다.  
  
10. 참조 [작업 3: 도구 상자 및 PropertyGrid 창 만들기](../../../docs/framework/windows-workflow-foundation/task-3-create-the-toolbox-and-propertygrid-panes.md) 추가 하는 방법에 알아보려면 **도구 상자** 및 **PropertyGrid** 재 호스트 된 워크플로 디자이너를 지원 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [워크플로 디자이너 재호스트](../../../docs/framework/windows-workflow-foundation/rehosting-the-workflow-designer.md)  
 [작업 1: 새 Windows Presentation Foundation 응용 프로그램 만들기](../../../docs/framework/windows-workflow-foundation/task-1-create-a-new-wpf-app.md)  
 [작업 3: 도구 상자 및 PropertyGrid 창 만들기](../../../docs/framework/windows-workflow-foundation/task-3-create-the-toolbox-and-propertygrid-panes.md)
