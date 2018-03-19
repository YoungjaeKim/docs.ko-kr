---
title: ".NET Framework에서 내게 필요한 옵션의 새로운 기능"
ms.custom: updateeachrelease
ms.date: 10/13/2017
ms.prod: .net-framework
ms.technology:
- dotnet-clr
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- what's new [.NET Framework]
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 5f17550bc0cc4919f00dc93c8e92d258b38c4f76
ms.sourcegitcommit: 1c0b0f082b3f300e54b4d069b317ac724c88ddc3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/16/2018
---
# <a name="whats-new-in-accessibility-in-the-net-framework"></a>.NET Framework에서 내게 필요한 옵션의 새로운 기능

.NET Framework는 응용 프로그램을 사용자에게 더욱 액세스 가능하도록 만드는 것을 목표로 합니다. 내게 필요한 옵션 기능을 통해 응용 프로그램은 사용자에게 보조 기술에 대한 적절한 환경을 제공할 수 있습니다. .NET Framework 4.7.1부터 .NET Framework에 개발자가 액세스 가능한 응용 프로그램을 만들도록 허용하는 다수의 내게 필요한 옵션 개선 사항이 포함되어 있습니다. 

새로운 내게 필요한 옵션 기능은 .NET Framework 4.7.1 이상을 대상으로 하는 응용 프로그램에 대해 기본적으로 활성화되어 있습니다. 또한 이전 버전의 .NET Framework를 대상으로 하지만 .NET Framework 4.7.1 이상에서 실행되는 응용 프로그램은 응용 프로그램의 구성 파일의 [`<runtime>`](~/docs/framework/configure-apps/file-schema/runtime/index.md) 섹션에서 [`<AppContextSwitchOverrides>`](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 요소에 다음 스위치를 추가하여 레거시 내게 필요한 옵션 동작을 옵트아웃할 수 있습니다(따라서 .NET Framework 4.7.1에서 내게 필요한 옵션 개선 사항으로 옵트인). 

```xml
<runtime>
    <!-- AppContextSwitchOverrides value attribute is in the form of 'key1=true|false;key2=true|false  -->
    <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false" />
</runtime>
```

마찬가지로 4.7.1부터 시작하는 .NET Framework의 버전을 대상으로 하는 응용 프로그램은 응용 프로그램의 구성 파일의 [`<runtime>`](~/docs/framework/configure-apps/file-schema/runtime/index.md) 섹션에서 [`<AppContextSwitchOverrides>`](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 요소에 다음 스위치를 추가하여 내게 필요한 옵션 기능을 비활성화할 수 있습니다. 

```xml
<runtime>
    <!-- AppContextSwitchOverrides value attribute is in the form of 'key1=true|false;key2=true|false  -->
    <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=true" />
</runtime>
```

## <a name="whats-new-in-accessibility-in-the-net-framework-471"></a>.NET Framework 4.7.1에서 내게 필요한 옵션의 새로운 기능

.NET Framework 4.7.1에는 다음과 같은 영역의 새로운 내게 필요한 옵션 기능이 포함됩니다.

- [WPF(Windows Presentation Foundation)](#windows-presentation-foundation-wpf)

- [Windows Forms](#windows-forms-accessibility-improvements)

### <a name="windows-presentation-foundation-wpf"></a>WPF(Windows Presentation Foundation)

**화면 판독기 개선 사항**

내게 필요한 옵션 개선 사항이 활성화된 경우 .NET Framework 4.7.1에는 화면 판독기에 영향을 주는 다음과 같은 향상 기능이 포함되어 있습니다.

- .NET Framework 4.7 이전 버전에서 <xref:System.Windows.Controls.Expander> 컨트롤은 단추로 화면 판독기에서 공지되었습니다. .NET Framework 4.7.1부터 확장/축소 가능한 그룹으로 올바르게 공지됩니다.

- .NET Framework 4.7 이전 버전에서 <xref:System.Windows.Controls.DataGridCell> 컨트롤은 “사용자 지정”으로 화면 판독기에서 공지되었습니다. .NET Framework 4.7.1부터 이제 데이터 표 셸(지역화된)로 올바르게 공지됩니다.
 
- .NET Framework 4.7.1부터 화면 판독기는 편집 가능한 <xref:System.Windows.Controls.ComboBox>의 이름을 공지합니다.

- .NET Framework 4.7 이전 버전에서 <xref:System.Windows.Controls.PasswordBox> 컨트롤은 "보기에 항목 없음"으로 공지되었거나 그렇지 않은 경우 잘못된 동작이 있었습니다. 이 문제는 .NET Framework 4.7.1부터 수정되었습니다.     

**UIAutomation LiveRegion 지원**

내레이터와 같은 화면 판독기는 사용자가 일반적으로 포커스가 있는 UI 콘텐츠의 텍스트 음성 변환 출력에 의해 응용 프로그램의 UI 콘텐츠를 읽는 데 도움을 줍니다. 그러나 UI 요소가 변경되고 포커스가 없는 경우 사용자는 알림을 받지 못하고 중요한 정보를 놓칠 수 있습니다. 라이브 영역은 이 문제를 해결하는 것을 목표로 합니다. 개발자는 화면 판독기 또는 다른 UIAutomation 클라이언트에게 UI 요소에 중요한 변경 내용이 만들어졌음을 알리는 데 사용할 수 있습니다. 화면 판독기는 사용자에게 이 변경 내용을 알리는 방법 및 시점을 결정할 수 있습니다. 

라이브 영역을 지원하기 위해 다음과 같은 API가 WPF에 추가되었습니다.

- **LiveSetting** 속성 및 **LiveRegionChanged** 이벤트를 식별하는 <xref:System.Windows.Automation.AutomationElementIdentifiers.LiveSettingProperty?displayProperty=nameWithType> 및 <xref:System.Windows.Automation.AutomationElementIdentifiers.LiveRegionChangedEvent?displayProperty=nameWithType> 필드 XAML을 사용하여 설정할 수 있습니다.

- 화면 판독기에 사용자에 대한 UI 변경 내용의 중요성을 알리는 **AutomationProperties.LiveSetting** 연결된 속성

- **AutomationProperties.LiveSetting** 연결된 속성을 식별하는 <xref:System.Windows.Automation.AutomationProperties.LiveSettingProperty?displayProperty=nameWithType> 속성
 
- **LiveSetting** 값을 제공하도록 재정의될 수 있는 <xref:System.Windows.Automation.Peers.AutomationPeer.GetLiveSettingCore%2A?displayProperty=nameWithType> 메서드

- **LiveSetting** 값을 가져오고 설정하는 <xref:System.Windows.Automation.AutomationProperties.GetLiveSetting%2A?displayProperty=nameWithType> 및 <xref:System.Windows.Automation.AutomationProperties.SetLiveSetting%2A?displayProperty=nameWithType> 메서드
 
- 다음 가능한 **LiveSetting** 값을 정의하는 <xref:System.Windows.Automation.AutomationLiveSetting?displayProperty=nameWithType> 열거형

   - <xref:System.Windows.Automation.AutomationLiveSetting.Off?displayProperty=nameWithType>. 라이브 영역의 콘텐츠가 변경된 경우 요소는 알림을 보내지 않습니다.   
   - <xref:System.Windows.Automation.AutomationLiveSetting.Polite?displayProperty=nameWithType>. 라이브 영역의 콘텐츠가 변경된 경우 요소는 비중단 알림을 보냅니다.   

  - <xref:System.Windows.Automation.AutomationLiveSetting.Assertive?displayProperty=nameWithType>. 라이브 영역의 콘텐츠가 변경된 경우 요소는 중단 알림을 보냅니다.   

다음 예제와 같이 관심 있는 요소에 **AutomationProperties.LiveSetting** 속성을 설정하여 LiveRegion을 만들 수 있습니다.   

```xaml
<TextBlock Name="myTextBlock" AutomationProperties.LiveSetting="Assertive">announcement</TextBlock>
```

라이브 영역에 있는 데이터가 변경되고 화면 판독기에 알려야 하는 경우 다음 샘플과 같이 명시적으로 이벤트를 발생시킵니다.

```csharp
var peer = FrameworkElementAutomationPeer.FromElement(myTextBlock);

peer.RaiseAutomationEvent(AutomationEvents.LiveRegionChanged);
```
```vb
Dim peer = FrameworkElementAutomationPeer.FromElement(myTextBlock)
peer.RaiseAutomationEvent(AutomationEvents.LiveRegionChanged)

```

**고대비**

.NET Framework 4.7.1부터 다양한 WPF 컨트롤에 고대비의 개선 사항이 만들어졌습니다. <xref:System.Windows.SystemParameters.HighContrast%2A> 테마가 설정된 경우 이제 표시됩니다. 여기에는 다음이 포함됩니다.

- <xref:System.Windows.Controls.Expander> 컨트롤

    <xref:System.Windows.Controls.Expander> 컨트롤에 대한 포커스 시각적 개체는 이제 표시됩니다. <xref:System.Windows.Controls.ComboBox>, <xref:System.Windows.Controls.ListBox> 및 <xref:System.Windows.Controls.RadioButton> 컨트롤에 대한 키보드 시각적 개체도 표시됩니다. 예:

    이전: 
    
    ![내게 필요한 옵션 개선 사항 이전의 포커스가 있는 Expander 컨트롤](media/expander-before.png)

    이후: 

    ![내게 필요한 옵션 개선 사항 이후의 포커스가 있는 Expander 컨트롤](media/expander-after.png)

- <xref:System.Windows.Controls.CheckBox> 및 <xref:System.Windows.Controls.RadioButton> 컨트롤
 
    <xref:System.Windows.Controls.CheckBox> 및 <xref:System.Windows.Controls.RadioButton> 컨트롤의 텍스트는 이제 고대비 테마에서 선택하면 쉽게 볼 수 있습니다. 예:

    이전: 

    ![내게 필요한 옵션 개선 사항 이전의 포커스가 있는 고대비 라디오 단추](media/radio-button-before.png)
    
    이후: 

    ![내게 필요한 옵션 개선 사항 이후의 포커스가 있는 고대비 라디오 단추](media/radio-button-after.png)

- <xref:System.Windows.Controls.ComboBox> 컨트롤
 
    .NET Framework 4.7.1부터 비활성화된 <xref:System.Windows.Controls.ComboBox> 컨트롤의 테두리는 비활성화된 텍스트와 동일한 색입니다. 예:
    
    이전: 

     ![내게 필요한 옵션 개선 사항 이전의 콤보 상자 비활성화된 테두리 및 텍스트](media/combo-disabled-before.png)

    이후:   

     ![내게 필요한 옵션 개선 사항 이후의 콤보 상자 비활성화된 테두리 및 텍스트](media/combo-disabled-after.png)

    또한 비활성화되고 포커스가 있는 단추는 올바른 테마 색을 사용합니다.

    이전:

    ![내게 필요한 옵션 개선 사항 이전의 단추 테마 색](media/button-themes-before.png) 
    
    이후: 

    ![내게 필요한 옵션 개선 사항 이후의 단추 테마 색](media/button-themes-after.png) 

    마지막으로 .NET Framework 4.7 이전 버전에서 <xref:System.Windows.Controls.ComboBox> 컨트롤의 스타일을 `Toolbar.ComboBoxStyleKey`로 설정하면 드롭다운 화살표가 표시되지 않았습니다. 이 문제는 .NET Framework 4.7.1부터 수정되었습니다. 예:

    이전: 

    ![내게 필요한 옵션 개선 사항 이전의 Toolbar.ComboBoxStyleKey](media/comboboxstylekey-before.png) 
    
    이후: 

    ![내게 필요한 옵션 개선 사항 이후의 Toolbar.ComboBoxStyleKey](media/comboboxstylekey-after.png) 

- <xref:System.Windows.Controls.DataGrid> 컨트롤

    .NET Framework 4.7.1부터 <xref:System.Windows.Controls.DataGrid> 컨트롤의 정렬 표시기 화살표는 이제 올바른 테마 색을 사용합니다. 예:

    이전: 

    ![내게 필요한 옵션 개선 사항 이전의 정렬 표시기 화살표](media/sort-indicator-before.png) 
    
    이후:   
 
    ![내게 필요한 옵션 개선 사항 이후의 정렬 표시기 화살표](media/sort-indicator-after.png) 
    
    또한 .NET Framework 4.7 이전 버전에서 기본 링크 스타일은 고대비 모드의 마우스에서 잘못된 색으로 변경되었습니다. 이는 .NET Framework 4.7.1부터 해결되었습니다. 마찬가지로 <xref:System.Windows.Controls.DataGrid> 확인란 열은 .NET Framework 4.7.1부터 키보드 포커스 피드백에 대해 예상되는 색을 사용합니다.

    이전: 

    ![내게 필요한 옵션 개선 사항 이전의 DataGrid 기본 링크 스타일](media/default-link-style-before.png) 
 
    이후:    
  
    ![내게 필요한 옵션 개선 사항 이후의 DataGrid 기본 링크 스타일](media/default-link-style-after.png)  

.NET Framework 4.7.1에서 WPF 내게 필요한 옵션 개선 사항에 대한 자세한 내용은 [WPF의 내게 필요한 옵션 개선 사항](../migration-guide/retargeting/4.7-4.7.1.md#accessibility-improvements-in-wpf)을 참조하세요.

## <a name="windows-forms-accessibility-improvements"></a>Windows Forms 내게 필요한 옵션 개선 사항

.NET Framework 4.7.1에서 WinForms(Windows Forms)는 다음 영역에서 내게 필요한 옵션 변경 내용을 포함합니다.

**고대비 모드에서 향상된 표시**

.NET Framework 4.7.1부터 다양한 WinForms 컨트롤은 운영 체제에서 사용할 수 있는 고대비 모드의 향상된 렌더링을 제공합니다. Windows 10은 일부 고대비 시스템 색에 대한 값을 변경했으며 Windows Forms는 Windows 10 Win32 프레임워크를 기반으로 합니다. 최상의 환경을 위해 최신 버전의 Windows를 실행하고 테스트 응용 프로그램에 app.manifest 파일을 추가하여 최신 OS로 옵트인하고 다음과 같이 보이도록 Windows 10 지원되는 OS 줄에 대한 주석을 제거합니다.

```xml
<!-- Windows 10 -->
<supportedOS Id=”{8e0f7a12-bfb3-4fe8-b9a5-48fd50a15a9a}” />
```
고대비 변경 내용의 몇 가지 예는 다음과 같습니다.

- <xref:System.Windows.Forms.MenuStrip> 항목의 확인 표시는 보기가 쉽습니다.

- 선택하면 비활성화된 <xref:System.Windows.Forms.MenuStrip> 항목이 보기가 쉽습니다.

- 선택된 <xref:System.Windows.Forms.Button> 컨트롤의 텍스트는 선택 영역 색과 대비됩니다.

- 비활성화된 텍스트는 읽기가 쉽습니다. 예:

    이전:

    ![내게 필요한 옵션 개선 사항 이전의 비활성화된 텍스트](media/wf-disabled-before.png) 

    이후:

    ![내게 필요한 옵션 개선 사항 이후의 비활성화된 텍스트](media/wf-disabled-after.png) 

- 스레드 예외 대화 상자의 고대비 개선 사항입니다.

**향상된 내레이터 지원**

.NET Framework 4.7.1에서 Windows Forms는 내레이터에 대한 다음과 같은 내게 필요한 옵션 개선 사항을 포함합니다.

- <xref:System.Windows.Forms.MonthCalendar> 컨트롤은 내레이터 및 다른 UI 자동화 도구로 액세스할 수 있습니다.

- <xref:System.Windows.Forms.CheckedListBox> 컨트롤은 항목의 선택 상태가 변경되어 목록 항목의 값을 변경했음을 사용자에게 알릴 때 내레이터에 알립니다.
 
- <xref:System.Windows.Forms.DataGridViewCell> 컨트롤은 올바른 읽기 전용 상태를 내레이터에 보고합니다.
 
- 내레이터는 이제 비활성화된 <xref:System.Windows.Forms.ToolStripMenuItem> 텍스트를 읽을 수 있는 반면 이전에는 비활성화된 메뉴 항목을 건너뛰었습니다.

**UIAutomation 내게 필요한 옵션 패턴에 대한 향상된 지원**

.NET Framework 4.7.1부터 내게 필요한 옵션 기술 도구의 개발자는 API 내게 필요한 옵션의 일반 패턴 및 여러 WinForms 컨트롤에 대한 속성을 활용할 수 있습니다. 이러한 내게 필요한 옵션 개선 사항은 다음을 포함합니다.

- <xref:System.Windows.Forms.ComboBox> 및 <xref:System.Windows.Forms.ToolStripSplitButton>은 이제 [확장/축소 패턴](../ui-automation/implementing-the-ui-automation-expandcollapse-control-pattern.md)을 지원합니다.
 
- <xref:System.Windows.Forms.DataGridViewCheckBoxCell>은 이제 [토글 패턴](../ui-automation/implementing-the-ui-automation-toggle-control-pattern.md)을 지원합니다.
 
- <xref:System.Windows.Forms.ToolStripItem> 컨트롤은 <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.Name> 속성 및 [확장/축소 패턴](../ui-automation/implementing-the-ui-automation-expandcollapse-control-pattern.md)을 지원합니다.

- <xref:System.Windows.Forms.NumericUpDown> 및 <xref:System.Windows.Forms.DomainUpDown> 컨트롤은 <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.Name> 속성을 지원합니다.

**향상된 속성 브라우저 환경**

.NET Framework 4.7.1부터 Windows Forms는 다음을 포함합니다.

- 다양한 드롭다운 선택 창을 통한 향상된 키보드 탐색
- 불필요한 탭 정지의 감소
- 컨트롤 형식의 향상된 보고
- 향상된 내레이터 동작
 
## <a name="see-also"></a>참고 항목
[.NET Framework의 새로운 기능](whats-new.md)   
 
