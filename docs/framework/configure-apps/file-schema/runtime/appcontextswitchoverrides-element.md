---
title: '&lt;AppContextSwitchOverrides&gt; 요소'
ms.custom: ''
ms.date: 01/08/2018
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-bcl
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- AppContextSwitchOverrides
- compatibility switches
- configuration switches
- configuration
ms.assetid: 4ce07f47-7ddb-4d91-b067-501bd8b88752
caps.latest.revision: ''
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 71888febdc42f0ee65bdcd55a761700eda065bc1
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="ltappcontextswitchoverridesgt-element"></a>&lt;AppContextSwitchOverrides&gt; 요소
<xref:System.AppContext> 클래스에 사용되는 스위치를 하나 이상 정의하여 새 기능의 옵트아웃 메커니즘을 제공합니다.  
  
 \<configuration>  
 \<runtime>  
\<AppContextSwitchOverrides>  
  
## <a name="syntax"></a>구문  
  
```xml  
<AppContextSwitchOverrides value="name1=value1[[;name2=value2];...]" />  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`value`|필수 특성입니다.<br /><br /> 하나 이상의 스위치 이름 및 연결 된 부울 값을 정의합니다.|  
  
### <a name="value-attribute"></a>특성 값  
  
|값|설명|  
|-----------|-----------------|  
|"name=value"|미리 정의 된 스위치 이름과 해당 값 (`true` 또는 `false`). 여러 스위치 이름/값 쌍은 세미콜론으로 구분 됩니다 (";"). .NET Framework에서 지원 되는 미리 정의 된 스위치 이름 목록은 설명 섹션을 참조 합니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 응용 프로그램에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`runtime`|런타임 초기화 옵션에 대한 정보를 포함합니다.|  
  
## <a name="remarks"></a>설명  
 .NET Framework 4.6부터는 `<AppContextSwitchOverrides>` 앱 새 기능을 사용 하거나 라이브러리의 이전 버전과 호환성을 유지 수 있는지 여부를 확인 하려면 API의 호출자를 허용 하는 구성 파일의 요소입니다. 예를 들어, API의 동작을 라이브러리의 두 버전 간의 변경 된 경우는 `<AppContextSwitchOverrides>` 요소 라이브러리의 새로운 기능을 지 원하는 버전에 새 동작을 취소 하기 위해 해당 API의 호출자를 허용 합니다. .NET framework에서 Api를 호출 하는 앱에 대 한는 `<AppContextSwitchOverrides>` 요소 호출자가 해당 앱을 이전 버전의.NET Framework 앱의 포함 하는.NET Framework 버전에서 실행 중인 경우에 새로운 기능을 선택 하도록 대상 수 있습니다 기능입니다.  
  
 `value` 의 특성은 `<AppContextSwitchOverrides>` 요소는 하나 이상의 세미콜론으로 구분 된 이름/값 쌍으로 구성 된 단일 문자열을 구성 합니다.  각 이름은 호환성 스위치를 식별 하 고 해당 값은 부울 (`true` 또는 `false`) 스위치가 설정 되어 있는지 여부를 나타내는입니다. 스위치는 기본적으로 `false`, 라이브러리의 새로운 기능을 제공 합니다. 스위치가 설정 되어 있으면만 이전 기능 제공 (즉, 해당 값은 `true`). 이렇게 하면 라이브러리의 새로운 기능을 취소 하기 위해 이전 동작에 의존 하는 호출자를 허용 하면서 기존 API에 대 한 새 동작을 제공할 수 있습니다.  
  
 .NET Framework에서는 다음 스위치를 지원합니다.  
  
|스위치 이름|설명|도입|  
|-----------------|-----------------|----------------|  
|`Switch.MS.Internal.`<br/>`DoNotApplyLayoutRoundingToMarginsAndBorderThickness`|Windows Presentation Foundation 컨트롤 레이아웃에 대 한 레거시 알고리즘을 사용 하는지 여부를 제어 합니다. 자세한 내용은 [완화: WPF 레이아웃](~/docs/framework/migration-guide/mitigation-wpf-layout.md)을 참조하십시오.|.NET Framework 4.6|  
|`Switch.MS.Internal.`<br/>`UseSha1AsDefaultHashAlgorithmForDigitalSignatures`|서명에 사용 되는 패키지의 부분 PackageDigitalSignatureManager 하 여 기본 알고리즘은 SHA1 또는 s h a 256 있는지 여부를 제어 합니다.|.NET Framework 4.7.1|
|`Switch.System.Activities.`<br/>`UseMD5CryptoServiceProviderForWFDebugger`|로 설정 하면 `false`, FIPS가 설정 된 경우 Visual Studio를 사용 하 여 XAML 기반 워크플로 프로젝트를 디버깅할 수 있습니다. 없으면는 <xref:System.NullReferenceException> System.Activities 어셈블리의 메서드 호출에서 throw 됩니다.|.NET Framework 4.7|
|`Switch.System.Activities.`<br/>`UseMD5ForWFDebugger`|MD5 또는 SHA1 디버거에서 워크플로 인스턴스에 대 한 체크섬을 사용 하는지 여부를 제어 합니다. | .NET Framework 4.7|
|`Switch.System.Drawing.`<br/>`DontSupportPngFramesInIcons`|컨트롤 여부는 <xref:System.Drawing.Icon.ToBitmap%2A?displayProperty=nameWithType> 메서드에서 예외가 throw 때는 <xref:System.Drawing.Icon> 개체에 PNG 프레임이 합니다. 자세한 내용은 [완화: 아이콘 개체의 PNG 프레임](~/docs/framework/migration-guide/mitigation-png-frames-in-icon-objects.md)을 참조하십시오.|.NET Framework 4.6|  
|`Switch.System.Drawing.Printing.`</br>`OptimizePrintPreview`|컨트롤 여부의 성능을 <xref:System.Windows.Forms.PrintPreviewDialog> 네트워크 프린터에 대해 최적화 됩니다. 자세한 내용은 참조 [PrintPreviewDialog 컨트롤 개요](../../../winforms/controls/printpreviewdialog-control-overview-windows-forms.md)합니다.|.NET Framework 4.6|
|`Switch.System.Globalization.NoAsyncCurrentCulture`|비동기 작업 호출 스레드의 컨텍스트를 전달 하지 않는 있는지 여부를 제어 합니다. 자세한 내용은 참조 [CurrentCulture 및 CurrentUICulture 흐름 태스크에 걸쳐](~/docs/framework/migration-guide/retargeting/4.5.2-4.6.md#currentculture-and-currentuiculture-flow-across-tasks)합니다.|.NET Framework 4.6|  
|`Switch.System.IdentityModel.`<br/>`DisableMultipleDNSEntriesInSANCertificate`|컨트롤 여부는 <xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims%2A?displayProperty=nameWithType> 메서드 클레임 유형을 마지막 DNS 항목만 일치 시 키 려 합니다. 자세한 내용은 [완화: X509CertificateClaimSet.FindClaims 메서드](~/docs/framework/migration-guide/mitigation-x509certificateclaimset-findclaims-method.md)를 참조하십시오.|.NET Framework 4.6.1|  
|`Switch.System.IO.BlockLongPaths`|컨트롤 있는지 여부를 보다 긴 경로 `MAX_PATH` (260 자)를 throw 한 <xref:System.IO.PathTooLongException>합니다. 자세한 내용은 참조 [긴 경로 지원](~/docs/framework/migration-guide/retargeting/4.6.1-4.6.2.md#long-path-support)합니다.|.NET Framework 4.6.2|  
|`Switch.System.IO.Compression.ZipFile.`<br/>`UseBackslash`|백슬래시를 사용 하 여 ("\\") 대신 슬래시 ("/")로 경로 구분 기호에는 <xref:System.IO.Compression.ZipArchiveEntry.FullName%2A?displayProperty=nameWithType> 속성입니다. 자세한 내용은 참조 [완화: ZipArchiveEntry.FullName 경로 구분 기호](~/docs/framework/migration-guide/mitigation-ziparchiveentry-fullname-path-separator.md)합니다.|.NET Framework 4.6.1|  
|`Switch.System.IO.Ports.`<br/>`DoNotCatchSerialStreamThreadExceptions`|운영 체제 throw 된 예외를 사용 하 여 만든 백그라운드 스레드에서 있는지 여부를 제어 <xref:System.IO.Ports.SerialPort> 스트림을 프로세스를 종료 합니다.|.NET Framework 4.7.1| 
|`Switch.System.IO.`<br/>`UseLegacyPathHandling`|레거시 경로 정규화 사용 되 고 URI 경로에서 사용할 수 있는지 여부를 제어는 <xref:System.IO.Path.GetDirectoryName%2A?displayProperty=nameWithType> 및 <xref:System.IO.Path.GetPathRoot%2A?displayProperty=nameWithType> 메서드. 자세한 내용은 참조 [완화: 경로 정규화](~/docs/framework/migration-guide/mitigation-path-normalization.md) 및 [완화: 경로 콜론 검사](~/docs/framework/migration-guide/mitigation-path-colon-checks.md)합니다.|.NET Framework 4.6.2|  
|`Switch.System.`<br/>`MemberDescriptorEqualsReturnsFalseIfEquivalent`|같음 비교에 대 한 테스트가 있는지 여부를 제어는 <xref:System.ComponentModel.MemberDescriptor.Category%2A?displayProperty=nameWithType> 한 개체의 속성은 <xref:System.ComponentModel.MemberDescriptor.Description%2A?displayProperty=nameWithType> 두 번째 개체의 속성입니다. 자세한 내용은 참조 [MemberDescriptor.Equals 잘못 구현](~/docs/framework/migration-guide/retargeting/4.6.1-4.6.2.md#incorrect-implementation-of-memberdescriptorequals)합니다.|.NET Framework 4.6.2|  
 `Switch.System.Net.`<br/>`DontCheckCertificateEKUs`|인증서 확장 된 키 사용 (EKU) 개체 식별자 (OID) 유효성 검사를 사용 하지 않습니다. (Eku 확장) 확장 된 키 사용 확장은 키를 사용 하는 응용 프로그램을 나타내는 개체 식별자 (Oid)의 컬렉션입니다.|.NET Framework 4.6|
|`Switch.System.Net.`<br/>`DontEnableSchSendAuxRecord`|SCH_SEND_AUX_RECORD의 사용을 비활성화 하 여 완화 방법은 TLS1.0 브라우저 악용에 대해 SSL/TLS (비스 트)를 사용 하지 않도록 설정 합니다.|.NET Framework 4.6|
|`Switch.System.Net.`<br/>`DontEnableSchUseStrongCrypto`|컨트롤 여부는 <xref:System.Net.ServicePointManager?displayProperty=nameWithType> 및 <xref:System.Net.Security.SslStream?displayProperty=nameWithType> 클래스는 SSL 3.0 프로토콜을 사용할 수 있습니다. 자세한 내용은 [완화: TLS 프로토콜](~/docs/framework/migration-guide/mitigation-tls-protocols.md)을 참조하십시오.|.NET Framework 4.6|
|`Switch.System.Net.`<br/>`DontEnableSystemDefaultTlsVersions`|기본값은 t l s 12, Tls11, Tls 되돌립니다 SystemDefault TLS 버전을 사용 하지 않도록 설정 합니다.|.NET Framework 4.7|
|`Switch.System.Net.`<br/>`DontEnableTlsAlerts`|SslStream TLS 서버 쪽 경고를 해제 합니다.|.NET Framework 4.7|
|`Switch.System.Runtime.Serialization.`<br/>`DoNotUseECMAScriptV6EscapeControlCharacter` |컨트롤 여부는 [DataContractJsonSerializer](xref:System.Runtime.Serialization.Json.DataContractJsonSerializer) ECMAScript V6 및 V8 표준에 따라 일부 제어 문자를 serialize 합니다. 자세한 내용은 [완화: DataContractJsonSerializer로 제어 문자 serialization](Mitigation:%20Serialization%20of%20Control%20Characters%20with%20the%20DataContractJsonSerializer.md)을 참조하세요.| .NET Framework 4.7 |
|`Switch.System.Security.ClaimsIdentity.`<br/>`SetActorAsReferenceWhenCopyingClaimsIdentity`|컨트롤 여부는 <xref:System.Security.Claims.ClaimsIdentity.%23ctor%28System.Security.Principal.IIdentity%29?displayProperty=nameWithType> 생성자는 새 개체의 설정 <xref:System.Security.Claims.ClaimsIdentity.Actor%2A?displayProperty=nameWithType> 기존 개체 참조를 사용 하 여 속성입니다. 자세한 내용은 [완화: ClaimsIdentity 생성자](~/docs/framework/migration-guide/mitigation-claimsidentity-constructor.md)를 참조하세요.|.NET Framework 4.6.2|  
|`Switch.System.Security.Cryptography.`<br/>`AesCryptoServiceProvider.DontCorrectlyResetDecryptor`|컨트롤 있는지 여부를 다시 사용 하려고는 <xref:System.Security.Cryptography.AesCryptoServiceProvider> 암호 해독기를 throw 한 <xref:System.Security.Cryptography.CryptographicException>합니다. 자세한 내용은 AesCryptoServiceProvider 암호 해독기를 재사용 가능한 transform](~/docs/framework/migration-guide/retargeting/4.6.1-4.6.2.md#aescryptoserviceprovider-decryptor-provides-a-reusable-transform) 제공을 참조 하십시오.|.NET Framework 4.6.2|
|`Switch.System.Security.Cryptography.`<br/>`DoNotAddrOfCspParentWindowHandle`|컨트롤 여부의 값은 [CspParameters.ParentWindowHandle](xref:System.Security.Cryptography.CspParameters.ParentWindowHandle) 속성은는 [IntPtr](xref:System.IntPtr) 창의 메모리 위치 처리할 나타냅니다 또는 창 핸들 (HWND) 인지 합니다. 자세한 내용은 [완화: CspParameters.ParentWindowHandle에 HWND 필요](Mitigation:%20CspParameters.ParentWindowHandle%20Expects%20an%20HWND.md)를 참조하세요. |.NET Framework 4.7|   
|`Switch.System.Security.Cryptography.Pkcs.`<br/>`UseInsecureHashAlgorithms`|SHA1 또는 s h a 256 일부 SignedCMS 작업에 대 한 기본값 인지 확인 합니다. |.NET Framework 4.7.1|
|`Switch.System.Security.Cryptography.Xml.`<br/>`UseInsecureHashAlgorithms`|SHA1 또는 s h a 256 일부 SignedXML 작업에 대 한 기본값 인지 확인 합니다. |.NET Framework 4.7.1|
|`Switch.System.ServiceModel.`<br/>`AllowUnsignedToHeader`|결정 여부는 `TransportWithMessageCredential` 보안 모드에서는 메시지를 부호 없는 "to" 헤더가 합니다. 옵트인 스위치입니다. 자세한 내용은 참조 [.NET Framework 4.6.1의에서 런타임 변경 내용](https://msdn.microsoft.com/library/mt592686.aspx#WCF)합니다.|.NET Framework 4.6.1| 
|`Switch.System.ServiceModel.`<br/>`DisableAddressHeaderCollectionValidation`>|컨트롤 여부는 <xref:System.ServiceModel.Channels.AddressHeaderCollection.%23ctor(System.Collections.Generic.IEnumerable{System.ServiceModel.Channels.AddressHeader})> 생성자 throw는 <xref:System.ArgumentException> 요소 중 하나 이면 `null`합니다.|.NET Framework 4.7.1| 
|`Switch.System.ServiceModel.`<br />`DisableCngCertificates`|CSG 키 저장소 공급자 예외가 throw X509 사용 시도가 함께 인증서 있는지 여부를 결정 합니다. 자세한 내용은 참조 [WCF 전송 보안 지원 CNG를 사용 하 여 저장 된 인증서를](~/docs/framework/migration-guide/retargeting/4.6.1-4.6.2.md#wcf-transport-security-supports-certificates-stored-using-cng)합니다.|.NET Framework 4.6.1|
|`Switch.System.ServiceModel.`<br/>`DisableOperationContextAsyncFlow`|재진입 서비스의 인스턴스를 한 번에 실행의 단일 스레드로 제한 하 여 발생 하는 교착 상태를 처리 합니다.|.NET Framework 4.6.2|
|`Switch.System.ServiceModel.`<br/>`DisableUsingServicePointManagerSecurityProtocols`|와 함께 `Switch.System.Net.DontEnableSchUseStrongCrypto`, TLS 1.1 및 TLS 1.2 WCF 메시지 보안을 사용할지 여부를 결정 합니다.|.NET Framework 4.7 |    
|`Switch.System.ServiceModel.`<br/>`UseSha1InMsmqEncryptionAlgorithm`|서명 알고리즘 WCF에서 MSMQ 메시지에 대 한 기본 메시지 SHA1 또는 s h a 256 인지 확인 합니다.|.NET Framework 4.7.1|
|`Switch.System.ServiceModel.`<br/>`UseSha1InPipeConnectionGetHashAlgorithm`|WCF는 SHA1, SHA256 해시 명명 된 파이프에 대 한 임의의 이름을 생성을 사용 하는지 여부를 제어 합니다.|.NET Framework 4.7.1|
|`Switch.System.ServiceProcess.`<br/>`DontThrowExceptionsOnStart`|호출자에 게 서비스를 시작할 때 발생 한 예외는 전파 하는지 여부를 제어는 <xref:System.ServiceProcess.ServiceBase.Run%2A?displayProperty=nameWithType> 메서드.|.NET Framework 4.7.1|
|`Switch.System.Windows.Controls.Grid.`<br/>`StarDefinitionsCanExceedAvailableSpace` |Windows Presentation Foundation 오래 된 알고리즘에 적용 되는지 여부를 결정 (`true`) 또는 새 알고리즘 (`false`)에서 공간을 할당 \*-열입니다. 자세한 내용은 [완화: Grid 컨트롤의 별 열 공간 할당](Mitigation:%20Grid%20Control's%20Space%20Allocation%20to%20Star-columns.md)을 참조하세요. |.NET Framework 4.7 |
|`Switch.System.Windows.Controls.TabControl.`<br/>`SelectionPropertiesCanLagBehindSelectionChangedEvent`|컨트롤 선택 발생 하기 전에 선택한 값 속성의 값을 업데이트 하는지 여부는 선택기 또는 탭 컨트롤에서 항상 변경 이벤트.|.NET Framework 4.7.1|
|`Switch.System.Windows.Forms.`<br />`DontSupportReentrantFilterMessage`|사용자 지정을 허용 하는 코드 opts <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage%2A?displayProperty=nameWithType> 예외를 throw 하지 않고 메시지를 안전 하 게 필터링 하는 구현 때는 <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=nameWithType> 메서드를 호출 합니다. 자세한 내용은 [완화: 사용자 지정 IMessageFilter.PreFilterMessage 구현](~/docs/framework/migration-guide/mitigation-custom-imessagefilter-prefiltermessage-implementations.md)을 참조하십시오.|.NET Framework 4.6.1|  
|`Switch.System.Windows.Input.Stylus.`<br/>`EnablePointerSupport`|여부, 선택적 `WM_POINTER`-기반된 터치/스타일러스 스택을 WPF 응용 프로그램에서 사용할 수 있습니다. 자세한 내용은 참조 [완화: 포인터 기반 터치 및 스타일러스 지원](Mitigation:%20Pointer-based%20Touch%20and%20Stylus%20Support.md) | 
|`Switch.System.Windows.Media.ImageSourceConverter.`<br/>`OverrideExceptionWithNullReferenceException`|레거시 있는지 여부를 제어 [NullReferenceException](xref:System.NullReferenceException) 대신 예외의 원인을 더 구체적으로 나타내는 예외가 throw 됩니다 (같은 [DirectoryNotFoundException](xref:System.IO.DirectoryNotFoundException) 또는 [ FileNotFoundException](xref:System.IO.FileNotFoundException)합니다. 처리에 의존 하는 코드에서 사용 하기 위해 용도가 [NullReferenceException](xref:System.NullReferenceException)합니다. | .NET Framework 4.7 |
|`Switch.UseLegacyAccessibilityFeatures`|컨트롤이 내게 필요한 옵션 기능.NET Framework 4.7.1부터 사용할 수 있는지 여부를 설정 또는 해제 합니다. | .NET Framework 4.7.1 |
|`System.Xml.`<br /><br /> `IgnoreEmptyKeySequences`|XSD 스키마 유효성 검사 하 여 복합 키에 빈 키 시퀀스가 무시 되는지 여부를 제어 합니다. 자세한 내용은 참조 [완화: XML 스키마 유효성 검사](~/docs/framework/migration-guide/mitigation-xml-schema-validation.md)합니다.|.NET Framework 4.6|  
  
> [!NOTE]
>  추가 하는 대신는 `AppContextSwitchOverrides` 응용 프로그램 구성 파일에 요소를 설정할 수도 있습니다는 스위치 프로그래밍 방식으로 호출 하 여는 `static` (C#에서) 또는 `Shared` (Visual Basic)에서는 <xref:System.AppContext.SetSwitch%2A?displayProperty=nameWithType> 메서드.  
  
 라이브러리 개발자 라이브러리의 이후 버전에서 도입 되거나 변경 된 기능을 취소 하기 위해 호출자를 허용 하려면 사용자 지정 스위치 정의할 수도 있습니다. 자세한 내용은 <xref:System.AppContext> 클래스를 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `AppContextSwitchOverrides` 단일 응용 프로그램 호환성 스위치를 정의 하는 요소 `Switch.System.Globalization.NoAsyncCurrentCulture`, 비동기 메서드 호출에 스레드를 넘어서 전달에서 culture에 맞지 않는 합니다.  
  
```xml  
<configuration>  
   <runtime>  
      <AppContextSwitchOverrides value="Switch.System.Globalization.NoAsyncCurrentCulture=true" />  
   </runtime>  
</configuration>  
```  
  
 다음 예제에서는 `AppContextSwitchOverrides` 두 응용 프로그램 호환성 스위치를 정의 하는 요소 `Switch.System.Globalization.NoAsyncCurrentCulture` 및 `Switch.System.IO.BlockLongPaths`합니다. Note 세미콜론 두 개의 이름/값 쌍을 구분 합니다.  
  
```xml  
<configuration>  
    <runtime>  
       <AppContextSwitchOverrides   
          value="Switch.System.Globalization.NoAsyncCurrentCulture=true;Switch.System.IO.BlockLongPaths=true" />  
    </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.AppContext?displayProperty=nameWithType>  
 [\<런타임 > 요소](runtime-element.md)  
 [\<configuration> 요소](../configuration-element.md)
