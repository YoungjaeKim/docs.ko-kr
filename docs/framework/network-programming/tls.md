---
title: ".NET Framework와 함께 전송 계층 보안 (TLS) 모범 사례"
description: ".NET Framework와 함께 보안 TLS (전송 계층)를 사용 하 여 모범 사례를 설명"
ms.date: 03/15/2018
ms.prod: .net-framework
ms.topic: article
helpviewer_keywords:
- sending data, Internet security
- protocols, Internet security
- Network security
- network resources, Internet security
- receiving data, Internet security
- authentication [.NET Framework], Internet security
- Internet, security
- security [.NET Framework], Internet
- permissions [.NET Framework], Internet
author: blowdart
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 64829eee5b21a44acb18cbec9b901d77d49cab90
ms.sourcegitcommit: 32172ca05d5dcce7ef3d327b9c8639c736e0fe2b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2018
---
# <a name="transport-layer-security-tls-best-practices-with-the-net-framework"></a>.NET Framework와 함께 전송 계층 보안 (TLS) 모범 사례

보안 TLS (전송 계층) 프로토콜은 인터넷을 통해 전달 되는 정보의 개인 정보를 보호 하도록 설계 된 산업 표준입니다. [TLS 1.2](https://tools.ietf.org/html/rfc5246) 는 출시 하는 최신 표준 및 이전 버전 보다 향상 된 보안 기능을 제공 합니다. TLS 1.2로 대체 됩니다 [TLS 1.3](https://tools.ietf.org/html/draft-ietf-tls-tls13-22)합니다. 이 문서에서는 TLS 프로토콜을 사용 하는.NET Framework 응용 프로그램을 보호 하는 권장 사항을 제공 합니다.

TLS 버전.NET Framework 응용 프로그램 보안이 유지 되도록 해야 **하지** 하드 코딩 될 합니다. .NET framework 응용 프로그램에는 운영 체제 (OS)에서 지원 되는 TLS 버전을 사용 해야 합니다.

이 문서는 개발자를 대상으로 합니다.

- 사용 하 여 직접는 <xref:System.Net> Api (예를 들어 <xref:System.Net.Http.HttpClient?displayProperty=nameWithType> 및 <xref:System.Net.Security.SslStream?displayProperty=nameWithType>).
- WCF 클라이언트 및 서비스를 사용 하 여를 사용 하 여 직접는 <xref:System.ServiceModel?displayProperty=nameWithType> 네임 스페이스입니다.
- 사용 하 여 [Azure 클라우드 서비스](https://azure.microsoft.com/services/cloud-services/) 웹 및 작업자 역할을 호스트 하 고 응용 프로그램을 실행 합니다. 참조는 [Azure 클라우드 서비스](#azure-cloud-services) 섹션.

하는 것이 좋습니다 있습니다.

- .NET Framework 4.7 또는 앱에서 이후 버전을 대상입니다. 대상.NET Framework 4.7.1 또는 WCF 응용 프로그램에 이후 버전입니다.
- TLS 버전을 지정 하지 마십시오. TLS 버전을 결정 하는 OS를 사용 하도록 코드를 구성 합니다.
- TLS 또는 SSL 버전을 지정 하지 않는 것을 확인 하려면 철저 한 코드 감사를 수행 합니다.

응용 프로그램 수 있습니다는 OS TLS 버전을 선택:

- 자동으로 이용할 새 프로토콜 TLS 1.3 등 나중에 추가 합니다.
- 운영 체제 보안 아니어야 검색 되는 프로토콜을 차단 합니다.

섹션 [코드를 감사 하 고 코드를 변경](#audit-your-code-and-make-code-changes) 감사 및 코드를 업데이트에 대해 설명 합니다.

이 문서에는 응용 프로그램을 대상으로 및에서 실행 되는.NET Framework의 버전에 사용할 수 있는 가장 강력한 보안을 사용 하는 방법을 설명 합니다. 보안 프로토콜 및 버전을 명시적으로 설정 하는 응용 프로그램을 다른 대안은 부족 opts 및.NET Framework 및 OS 기본 동작을 옵트아웃 opts 합니다. TLS 1.2 연결을 협상할 수 있는 응용 프로그램을 사용 하도록 하려는 경우 명시적으로 낮은 TLS 버전 설정 TLS 1.2 연결이 되지 않습니다.

하드 코딩 프로토콜 버전을 피할 수 없는 경우 TLS 1.2를 지정 하는 것이 좋습니다. 식별 하 고 TLS 1.0 종속성 제거에 대 한 지침을 다운로드는 [TLS 1.0 문제 해결](https://www.microsoft.com/download/details.aspx?id=55266) 백서입니다.

WCF 지원 TLS1.0, 1.1 및 1.2에.NET Framework 4.7 기본값으로 합니다. .NET Framework 4.7.1 부터는 WCF 기본적으로 운영 체제 버전을 구성 합니다. 응용 프로그램이 명시적으로 구성 된 경우 `SslProtocols.None`, WCF에서는 NetTcp 전송을 사용 하 여 운영 체제 기본 설정을 사용 합니다.

이 문서는 GitHub 문제에 대 한 질문 수 [보안 TLS (전송 계층).NET Framework와 함께 유용한](https://github.com/dotnet/docs/issues/4675)합니다.

## <a name="audit-your-code-and-make-code-changes"></a>코드를 감사 하 고 코드 변경

ASP.NET 응용 프로그램에 대 한 검사는 `<system.web><httpRuntime targetFramework>` 요소의 _web.config_ 를 의도 한 버전의.NET Framework를 사용 하는지 확인 합니다.

Windows Forms 및 기타 응용 프로그램에 대 한 참조 [하는 방법:.NET Framework의 버전을 대상](/visualstudio/ide/how-to-target-a-version-of-the-dotnet-framework)합니다.

다음 섹션에서는 사용 하 여 특정 TLS 또는 SSL 버전을 사용 하지 않는다고 확인 합니다.

## <a name="if-your-app-targets-net-framework-47-or-later-versions"></a>.NET Framework 4.7 또는 이후 버전 앱을 대상으로 하는 경우

다음 섹션에서는 특정 TLS 또는 SSL 버전을 사용 하지 않는다고 확인 하는 방법을 보여 줍니다.

### <a name="for-http-networking"></a>HTTP 네트워킹에 대 한

<xref:System.Net.ServicePointManager>기본적으로.NET Framework 4.7 및 이상 버전에서 사용 하 여 운영 체제에서 가장 적합 한 보안 프로토콜 및 버전을 선택 합니다. 기본 OS 최선의 선택을 얻기 위해 가능 하면을 설정 하지 않습니다에 대 한 값은 <xref:System.Net.ServicePointManager.SecurityProtocol> 속성입니다. 그렇지 않으면 <xref:System.Net.SecurityProtocolType.SystemDefault>로 설정합니다.

.NET Framework 4.7 또는 HTTP 네트워킹에 대 한 이후 버전을 대상으로 하는 경우에이 문서의 나머지 부분에서는 적합 하지 않습니다.

### <a name="for-tcp-sockets-networking"></a>TCP 소켓 네트워킹에 대 한

<xref:System.Net.Security.SslStream>기본적으로.NET Framework 4.7 및 이상 버전에서 사용 하 여 운영 체제에서 가장 적합 한 보안 프로토콜 및 버전을 선택 합니다. 기본 OS 최선의 선택을 가능 하면 하지 않는 사용의 메서드 오버 로드 <xref:System.Net.Security.SslStream> 명시적 걸리는 <xref:System.Security.Authentication.SslProtocols> 매개 변수입니다. 그렇지 않으면 전달 <xref:System.Security.Authentication.SslProtocols.None?displayProperty=nameWithType>합니다. 사용 하지 않는 것이 좋습니다 <xref:System.Security.Authentication.SslProtocols.Default>설정 `SslProtocols.Default` 를 사용 하면 SSL 3.0 /TLS 1.0의 사용 및 TLS 1.2를 방지 합니다.

에 대 한 값을 설정 하지 않습니다는 <xref:System.Net.ServicePointManager.SecurityProtocol> 속성 (HTTP 네트워킹 사용).

메서드 오버 로드를 사용 하지 않는 <xref:System.Net.Security.SslStream> 명시적 걸리는 <xref:System.Security.Authentication.SslProtocols> 매개 변수 (TCP 소켓은 네트워킹). .NET Framework 4.7 이상 버전에 앱의 대상을 변경할 때 모범 사례 권장 사항을 수행 합니다.

네트워킹 소켓 TCP에 대 한.NET Framework 4.7 또는 이후 버전을 대상으로 하는 경우에이 항목의 나머지 부분에서는 적합 하지 않습니다.

<a name="wcf-tcp-cert"></a>

### <a name="for-wcf-tcp-transport-using-transport-security-with-certificate-credentials"></a>WCF TCP에 대 한 전송 보안을 사용 하 여 인증서 자격 증명으로 전송

WCF는.NET Framework의 나머지 부분과 동일한 네트워킹 스택을 사용합니다.

4.7.1 대상으로 하는 경우 WCF OS 명시적으로 구성 하지 않는 한 기본적으로 가장 적합 한 보안 프로토콜을 선택 하려면 허용 하도록 구성 됩니다.

- 응용 프로그램 구성 파일입니다.
- **또는**, 소스 코드에서 응용 프로그램에서 합니다.

기본적으로.NET Framework 4.7 및 이후 버전 TLS 1.2를 사용 하도록 구성 하 고 TLS 1.1 또는 TLS 1.0을 사용 하 여 연결을 허용 합니다. OS 사용 하도록 바인딩을 구성 하 여 가장 적합 한 보안 프로토콜을 선택할 수 있도록 WCF 구성 <xref:System.Security.Authentication.SslProtocols.None?displayProperty=nameWithType>합니다. 에 설정 될 수 <xref:System.ServiceModel.TcpTransportSecurity.SslProtocols>합니다. `SslProtocols.None` 액세스할 수 있습니다 <xref:System.ServiceModel.NetTcpSecurity.Transport>합니다. `NetTcpSecurity.Transport` 액세스할 수 있습니다 <xref:System.ServiceModel.NetTcpBinding.Security>합니다.

사용자 지정 바인딩을 사용 하 여:

- OS를 설정 하 여 가장 적합 한 보안 프로토콜을 선택할 수 있도록 WCF 구성 <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement.SslProtocols> 사용할 <xref:System.Security.Authentication.SslProtocols.None?displayProperty=nameWithType>합니다.
- **또는** 구성 경로 사용 하는 프로토콜 구성 `system.serviceModel/bindings/customBinding/binding/sslStreamSecurity:sslProtocols`합니다.

본인이 **하지** 사용자 지정 바인딩을 사용 하 여 **및** 구성을 사용 하 여 WCF 바인딩을 설정 하 고, 구성 경로 사용 하는 프로토콜 설정 `system.serviceModel/bindings/netTcpBinding/binding/security/transport:sslProtocols`합니다.

### <a name="for-wcf-message-security-with-certificate-credentials"></a>인증서 자격 증명으로 WCF 메시지 보안

.NET framework 4.7 및 기본적으로 이후 버전에 지정 된 프로토콜을 사용 하 여는 <xref:System.Net.ServicePointManager.SecurityProtocol> 속성입니다. 경우는 [AppContextSwitch](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) `Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols` 로 설정 된 `true`, WCF, TLS 1.0까지 가장 적합 한 프로토콜을 선택 합니다.

## <a name="if-your-app-targets-a-net-framework-version-earlier-than-47"></a>앱 4.7 이전의.NET Framework 버전을 대상으로 하는 경우

다음 섹션에서는 사용 하 여 특정 TLS 또는 SSL 버전을 설정 하지 않은 것을 확인 하도록 코드를 감사 합니다.

### <a name="for-net-framework-46---462-and-not-wfc"></a>.NET Framework 4.6-4.6.2 및 하지 WFC 용

설정의 `DontEnableSystemDefaultTlsVersions` `AppContext` 전환할 `false`합니다. 참조 [AppContext 스위치를 통해 보안 구성](#configuring-security-via-appcontext-switches)합니다.

### <a name="for-wcf-using-net-framework-46---462-using-tcp-transport-security-with-certificate-credentials"></a>.NET Framework 4.6-4.6.2 TCP 전송 보안을 사용 하 여 인증서 자격 증명으로 사용 하 여 WCF에 대 한

최신 OS 패치를 설치 해야 합니다. 참조 [보안 업데이트](#security-updates)합니다.

WCF 프레임 워크 프로토콜 버전을 명시적으로 구성 하지 않는 한 TLS 1.2까지 사용할 수 있는 가장 높은 프로토콜을 자동으로 선택 합니다. 자세한 내용은 이전 섹션을 참조 하십시오. [인증서 자격 증명으로 전송 보안을 사용 하 여 WCF TCP에 대 한 전송](#wcf-tcp-cert)합니다.

### <a name="for-net-framework-35---451-and-not-wcf"></a>.NET Framework 3.5가 4.5.1과 하지 WCF에 대 한

.NET Framework 4.7 이상 버전에 앱을 업그레이드 하는 것이 좋습니다. 업그레이드할 수 없으면 다음 단계를 수행 합니다. 특정 시점에 나중에 응용 프로그램이 실패할 수 있습니다를.NET Framework 4.7 또는 이후 버전으로 업그레이드 될 때까지 합니다.

설정의 [SchUseStrongCrypto](#schusestrongcrypto) 및 [SystemDefaultTlsVersions](#systemdefaulttlsversions) 레지스트리 키를 1입니다. 참조 [Windows 레지스트리를 통해 보안 구성](#configuring-security-via-the-windows-registry)합니다. .NET Framework 버전 3.5가 지원는 `SchUseStrongCrypto` 명시적 TLS 값은 전달 하는 때에 플래그를 지정 합니다.

.NET Framework 3.5를 실행 하는 경우 프로그램에서 TLS 1.2를 지정할 수 있도록 핫 패치를 설치 해야 합니다.

| [KB3154518](https://support.microsoft.com/kb/3154518) | Windows 7 SP1 및 서버 2008 R2 s p 1에서.NET Framework 3.5.1에에서 안정성 롤업 HR-1605-TLS 시스템 기본 버전에 대 한 지원 포함 |
| --- | --- |
| [KB3154519](https://support.microsoft.com/kb/3154519) | 안정성 롤업 HR-1605-TLS 시스템 기본 버전 Windows Server 2012에서.NET Framework 3.5에 포함 된에 대 한 지원 |
| [KB3154520](https://support.microsoft.com/kb/3154520) | 안정성 롤업 HR-1605-Windows 8.1 및 Windows Server 2012 r 2에서.NET Framework 3.5에 포함 된 TLS 시스템 기본 버전에 대 한 지원 |
| [KB3156421](https://support.microsoft.com/kb/3156421) | .NET Framework 4.5.2와 Windows에서 4.5.1에 대 한 1605 핫픽스 롤업 3154521 |

### <a name="for-wcf-using-net-framework-35---452-using-tcp-transport-security-with-certificate-credentials"></a>.NET Framework 3.5 4.5.2 TCP 전송 보안을 사용 하 여 인증서 자격 증명으로 사용 하 여 WCF에 대 한

이러한 버전의 WCF 프레임 워크는 SSL 3.0 및 TLS 1.0 값을 사용 하도록 하드 코드 된 합니다. 이러한 값을 변경할 수 없습니다. 업데이트 하 고, TLS 1.1 및 1.2를 사용 하려면 NET Framework 4.6 이상 버전에 대상 다시 지정 해야 합니다.

## <a name="if-your-app-targets-net-framework-35"></a>응용 프로그램.NET Framework 3.5를 대상으로 하는 경우

보안 프로토콜.NET framework 또는 운영 체제 선택 하도록 하는 대신 보안 프로토콜을 설정 명시적으로 해야 하는 경우 추가 `SecurityProtocolTypeExtensions` 및 `SslProtocolsExtension` 코드를 열거 합니다. `SecurityProtocolTypeExtensions` 및 `SslProtocolsExtension` 에 대 한 값을 포함할 `Tls12`, `Tls11`, 및 `SystemDefault` 값입니다. 참조 [TLS 시스템 기본 버전 Windows 8.1 및 Windows Server 2012 r 2에서.NET Framework 3.5에 포함 된에 대 한 지원을](https://support.microsoft.com/help/3154520/support-for-tls-system-default-versions-included-in-the--net-framework)합니다.

<a name="configuring-security-via-appcontext-switches"></a>

## <a name="configuring-security-via-appcontext-switches-for-net-framework-46-or-later-versions"></a>(또는 대 한.NET Framework 4.6 이상 버전) 전환 AppContext 통해 보안 구성

[AppContext](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 이 섹션에서 설명 하는 스위치와 관련 된 경우 응용 프로그램 대상 또는.NET Framework 4.6 이상 버전에서 실행 합니다. 되어야 하는지 여부를 기본적으로 또는 명시적으로 설정 하 여 스위치 `false` 가능한 경우. 하나 또는 두 스위치를 통해 보안을 구성 하려면 다음 값을 지정 하지 보안 프로토콜 코드; 이렇게 하면 지금 재정의 스위치입니다.

스위치 HTTP 네트워킹을 진행 하 고 있는지 여부를 구분해 서 (<xref:System.Net.ServicePointManager>) 또는 TCP 소켓 네트워킹 (<xref:System.Net.Security.SslStream>).

### <a name="switchsystemnetdontenableschusestrongcrypto"></a>Switch.System.Net.DontEnableSchUseStrongCrypto

값이 `false` 에 대 한 `Switch.System.Net.DontEnableSchUseStrongCrypto` 강력한 암호화를 사용 하도록 앱을 발생 합니다. 값이 `false` 에 대 한 `DontEnableSchUseStrongCrypto` 더 안전한 네트워크 프로토콜 (TLS 1.2, TLS 1.1 및 TLS 1.0)을 사용 하 고 안전 하지 않은 프로토콜을 차단 합니다. 자세한 내용은 참조 하십시오. [The SCH_USE_STRONG_CRYPTO 플래그](#the-schusestrongcrypto-flag)합니다. 값이 `true` 앱에 대 한 강력한 암호화를 사용 하지 않도록 설정 합니다.

앱이.NET Framework 4.6 이상을 대상으로,이 스위치의 기본값은 `false`합니다. 권장 되는 보안 기본값입니다. 응용 프로그램.NET Framework 4.6에서 실행 되지만 이전 버전을 대상, 스위치의 기본값은 `true`합니다. 이 경우 명시적으로 설정 해야 `false`합니다.

`DontEnableSchUseStrongCrypto` 값만 있어야 `true` 강력한 암호화를 지원 하지 않는 업그레이드할 수 없는 레거시 서비스에 연결 하는 데 필요 합니다.

### <a name="switchsystemnetdontenablesystemdefaulttlsversions"></a>Switch.System.Net.DontEnableSystemDefaultTlsVersions

값이 `false` 에 대 한 `Switch.System.Net.DontEnableSystemDefaultTlsVersions` 하면 앱이 운영 체제의 프로토콜을 선택 하려면 허용 합니다. 값이 `true` 하면 앱이.NET Framework에 의해 선택 되는 프로토콜을 사용 합니다.

앱이 대상.NET Framework 4.7 또는 이후 버전으로,이 스위치의 기본값은 `false`합니다. 권장 되는 보안 기본값입니다. 응용 프로그램에서.NET Framework 4.7 이상 버전에서 실행 되 표시 되지만 이전 버전을 대상으로 하는 경우 스위치 기본적으로 `true`합니다. 이 경우 명시적으로 설정 해야 `false`합니다.

### <a name="switchsystemservicemodeldisableusingservicepointmanagersecurityprotocols"></a>Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols

값이 `false` 에 대 한 `Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols` 응용 프로그램에 정의 된 값을 사용 하도록 `ServicePointManager.SecurityProtocols` 인증서 자격 증명을 사용 하 여 메시지 보안에 대 한 합니다. 값이 `true` TLS1.0까지 사용할 수 있는 가장 높은 프로토콜을 사용 하 여

.NET Framework 4.7 및 이상 버전을 대상으로 하는 응용 프로그램에서는이 기본값 `false`합니다. .NET Framework 4.6.2를 대상으로 하는 응용 프로그램에 대 한 이전 버전에서는이 기본값 및 `true`합니다.

### <a name="switchsystemservicemodeldontenablesystemdefaulttlsversions"></a>Switch.System.ServiceModel.DontEnableSystemDefaultTlsVersions

값이 `false` 에 대 한 `Switch.System.ServiceModel.DontEnableSystemDefaultTlsVersions` 운영 체제의 프로토콜을 선택 하려면 허용 하는 기본 구성을 설정 합니다. 값이 `true` TLS1.2까지 사용할 수 있는 가장 높은 프로토콜에 기본값을 설정 합니다.

.NET Framework 4.7.1 및 이상 버전을 대상으로 하는 응용 프로그램에서는이 기본값 `false`합니다. 4.7 및 이전 버전의.NET Framework를 대상으로 하는 응용 프로그램에서는이 기본값 `true`합니다.

TLS 프로토콜에 대 한 자세한 내용은 참조 [완화: TLS 프로토콜](../migration-guide/mitigation-tls-protocols.md)합니다. 에 대 한 자세한 내용은 `AppContext` 스위치, 참조 [ `<AppContextSwitchOverrides> Element` ](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md)합니다.

## <a name="configuring-security-via-the-windows-registry"></a>Windows 레지스트리를 통해 보안 구성

하나 또는 둘 다 설정 하는 경우 `AppContext` 스위치 사용 하지 않을,이 섹션에 설명 된 Windows 레지스트리 키를 가진 앱에서 사용 하는 보안 프로토콜을 제어할 수 있습니다. 하나 또는 둘 다 사용할 수는 `AppContext` 전환 앱 버전을 대상으로.NET Framework 4.6을 이전 하거나 구성 파일을 편집할 수 없습니다. 레지스트리 보안을 구성 하려면 다음 값을 지정 하지 보안 프로토콜 코드; 이렇게 하면 지금 재정의 레지스트리 합니다.

레지스트리 키의 이름을 해당 이름이 비슷합니다 `AppContext` 없이 스위치는 `DontEnable` 이름 앞에 있습니다. 예를 들어는 `AppContext` 전환 `DontEnableSchUseStrongCrypto` 레지스트리 키 라고 [SchUseStrongCrypto](#schusestrongcrypto)합니다.

이러한 키가 최신 보안 패치는 모든.NET Framework 버전에서 사용할 수 있습니다. 참조 [보안 업데이트](#security-updates)합니다.

모든 레지스트리 키 아래에 설명 된 동일한 효과가 HTTP 네트워킹을 진행 하 고 있는지 여부를 (<xref:System.Net.ServicePointManager>) 또는 TCP 소켓 네트워킹 (<xref:System.Net.Security.SslStream>).

### <a name="schusestrongcrypto"></a>SchUseStrongCrypto

`HKEY_LOCAL_MACHINE\SOFTWARE\[Wow6432Node\]Microsoft\.NETFramework\<VERSION>: SchUseStrongCrypto` 레지스트리 키에 DWORD 형식의 값입니다. 값이 1 이면 강력한 암호화를 사용 하도록 앱. 강력한 암호화는 더 안전한 네트워크 프로토콜 (TLS 1.2, TLS 1.1 및 TLS 1.0)을 사용 하 여 및 안전 하지 않은 프로토콜을 차단 합니다. 값이 0 강력한 암호화를 해제합니다. 자세한 내용은 참조 [The SCH_USE_STRONG_CRYPTO 플래그](#the-schusestrongcrypto-flag)합니다.

앱이.NET Framework 4.6 이상을 대상으로,이 키 값이 1 기본값으로 됩니다. 권장 되는 보안 기본값입니다. 앱.NET Framework 4.6에서 실행 되지만 이전 버전을 대상 키 기본값은 0입니다. 이 경우 1로 해당 값을 명시적으로 설정 해야 합니다.

이 키에는 업그레이드할 수 없습니다 및 강력한 암호화를 지원 하지 않는 레거시 서비스에 연결 해야 하는 경우 값이 0 있어야 합니다.

### <a name="systemdefaulttlsversions"></a>SystemDefaultTlsVersions

`HKEY_LOCAL_MACHINE\SOFTWARE\[Wow6432Node\]Microsoft\.NETFramework\<VERSION>: SystemDefaultTlsVersions` 레지스트리 키에 DWORD 형식의 값입니다. 값이 1에 운영 체제의 프로토콜을 선택할 수 있도록 앱을 하면 됩니다. 값이 0 하면 앱이.NET Framework에 의해 선택 되는 프로토콜을 사용 합니다.

`<VERSION>` (.NET Framework 3.5)에 대 한 v4.0.30319 (.NET Framework 4 이상) 또는 v 2.0.50727 이어야 합니다.

앱이 대상.NET Framework 4.7 또는 이후 버전으로,이 키 값이 1 기본값으로 됩니다. 권장 되는 보안 기본값입니다. 응용 프로그램에서.NET Framework 4.7 이상 버전에서 실행 되 표시 되지만 이전 버전을 대상 키의 기본값인 0 됩니다. 이 경우 1로 해당 값을 명시적으로 설정 해야 합니다.

자세한 내용은 참조 하십시오. [누적 업데이트에 대 한 Windows 10 버전 1511 및 Windows Server 2016 Technical Preview 4: 2016 년 5 월 10 일](https://support.microsoft.com/help/3156421/cumulative-update-for-windows-10-version-1511-and-windows-server-2016)합니다.

참조에 대 한 자세한 내용은.NET framework 3.5.1, [TLS 시스템 기본 버전 서버 2008 R2 SP1 및 Windows 7 s p 1에.NET Framework 3.5.1에에서 포함 된에 대 한 지원을](https://support.microsoft.com/help/3154518/support-for-tls-system-default-versions-included-in-the--net-framework)합니다.

다음 _합니다. REG_ 파일에서 레지스트리 키와는 변형 가장 안전한 값으로 설정 합니다.

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v2.0.50727]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001
```

## <a name="configuring-schannel-protocols-in-the-windows-registry"></a>Windows 레지스트리에 Schannel 프로토콜을 구성합니다.

프로토콜 협상 하는 클라이언트 및/또는 서버 응용 프로그램을 통해 세분화 된 제어에 대 한 레지스트리를 사용할 수 있습니다. 응용 프로그램의 네트워킹 Schannel 통과 (에 대 한 다른 이름인 [보안 채널](https://msdn.microsoft.com/library/windows/desktop/aa380123)합니다. 구성 하 여 `Schannel`, 앱의 동작을 구성할 수 있습니다.

로 시작는 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols` 레지스트리 키입니다. 해당 키 하에서 집합의 모든 하위 키를 만들 수 있습니다 `SSL 2.0`, `SSL 3.0`, `TLS 1.0`, `TLS 1.1`, 및 `TLS 1.2`합니다. 각 해당 하위 키 아래에서 하위 키를 만들 수 있습니다 `Client` 및/또는 `Server`합니다. 아래 `Client` 및 `Server`, DWORD 값을 만들 수 `DisabledByDefault` (0 또는 1) 및 `Enabled` (0 또는 0xFFFFFFFF).

## <a name="the-schusestrongcrypto-flag"></a>SCH_USE_STRONG_CRYPTO 플래그

사용 되는 경우 (기본적으로 여는 `AppContext` 전환, 또는 Windows 레지스트리에서),.NET Framework를 사용 하 여는 `SCH_USE_STRONG_CRYPTO` 앱 TLS 보안 프로토콜을 요청 하면 플래그 합니다. `SCH_USE_STRONG_CRYPTO` 으로 플래그를 기본적으로 활성화 수 있습니다는 `AppContext` 전환, 또는 레지스트리에 합니다. 운영 체제에 플래그를 전달 `Schannel`알려진된 취약 한 암호화 알고리즘을 사용 하지 않도록 명령, 도구 모음 및 더 나은 상호 운용성을 위해 그렇지 않으면 사용할 수 있는 TLS/SSL 프로토콜 버전을 암호화 합니다. 자세한 내용은 다음을 참조하세요.

- [보안 채널](https://msdn.microsoft.com/library/windows/desktop/aa380123)
- [SCHANNEL_CRED 구조](https://msdn.microsoft.com/library/windows/desktop/aa379810)

`SCH_USE_STRONG_CRYPTO` 플래그에 전달 됩니다 `Schannel` 명시적으로 사용 하는 경우는 `Tls` (TLS 1.0) `Tls11`, 또는 `Tls12` 열거의 값 <xref:System.Net.SecurityProtocolType> 또는 <xref:System.Security.Authentication.SslProtocols>합니다.

## <a name="security-updates"></a>보안 업데이트

이 문서에서 모범 사례를 설치 하는 최신 보안 업데이트에 따라 다릅니다. 이 업데이트에는 고급.NET Framework 4.7 및 이후 기능을 사용 하는 기능 포함 되어 있습니다. 최신 보안 업데이트는 (경우에 이전 버전을 대상) 앱에서.NET Framework 4.7 이상 버전에서 실행 되는 경우 중요 합니다.

운영 체제의 TLS 사용 하 여 가장 적합 한 버전을 선택할 수 있도록.NET Framework 업데이트를 설치 해야 이상:

- [.NET Framework 2017 년 8 월 미리 보기 품질 롤업의](https://blogs.msdn.microsoft.com/dotnet/2017/08/16/net-framework-august-2017-preview-of-quality-rollup)합니다.
- **또는** 는 [.NET Framework 2017 년 9 월 보안 및 품질 롤업](https://blogs.msdn.microsoft.com/dotnet/2017/09/12/net-framework-september-2017-security-and-quality-rollup)합니다.

참고 항목:

- [.NET framework 버전 및 종속성](../migration-guide/versions-and-dependencies.md)
- [방법: 설치 된.NET Framework 버전 결정](../migration-guide/how-to-determine-which-versions-are-installed.md)합니다.

## <a name="support-for-tls-12"></a>TLS 1.2에 대 한 지원

TLS 1.2, 운영 체제 및.NET Framework 버전을 협상 하도록 응용 프로그램 둘 다 TLS 1.2를 지원 해야 합니다.

**TLS 1.2를 지원 하도록 운영 체제 요구 사항**

를 사용 하거나 지 원하는 시스템에서 TLS 1.1 및 TLS 1.2를 다시 사용 하려면 참조 [보안 TLS (전송 계층) 레지스트리 설정을](/windows-server/security/tls/tls-registry-settings)합니다.

| **OS** | **TLS 1.2 지원** |
| --- | --- |
| Windows 10</br>Windows Server 2016 | 지원 되며 기본적으로 사용 됩니다. |
| Windows 8.1</br>Windows Server 2012 R2 | 지원 되며 기본적으로 사용 됩니다. |
| Windows 8.0</br>Windows Server 2012 | 지원 되며 기본적으로 사용 됩니다. |
| Windows 7 SP1</br>Windows Server 2008 R2 SP1 | 기본적으로 사용 안 함 하지만 지원. 참조는 [보안 TLS (전송 계층) 레지스트리 설정을](/windows-server/security/tls/tls-registry-settings) TLS 1.2를 사용 하는 방법에 대 한 자세한 내용은 웹 페이지입니다. |
| Windows Server 2008 | TLS 1.1 및 TLS 1.2에 대 한 지원에는 업데이트를 해야합니다. 참조 [Windows Server 2008 s p 2에서 TLS 1.1 및 TLS 1.2에 대 한 지원을 추가할 업데이트를](https://support.microsoft.com/help/4019276/update-to-add-support-for-tls-1-1-and-tls-1-2-in-windows-server-2008-s)합니다. |
| Windows Vista | 지원되지 않습니다. |

각 버전의 Windows에서 기본적으로 설정 되어 프로토콜을 TLS/SSL에 대 한 정보를 참조 하십시오. [TLS/SSL (Schannel SSP)의 프로토콜](https://msdn.microsoft.com/library/windows/desktop/mt808159)합니다.

**.NET Framework 3.5와 함께 TLS 1.2를 지원 하기 위한 요구 사항**

이 표에서.NET Framework 3.5와 함께 TLS 1.2를 지원 해야 합니다. 운영 체제 업데이트를 보여 줍니다. 모든 운영 체제 업데이트를 적용 하는 것이 좋습니다.

| **OS** | **.NET Framework 3.5와 함께 TLS 1.2를 지 원하는 데 필요한 최소 업데이트** |
| --- | --- |
| Windows 10</br>Windows Server 2016 | [Windows 10 버전 1511 용 누적 업데이트 및 Windows Server 2016 Technical Preview 4: 2016 년 5 월 10 일](https://support.microsoft.com/help/3156421/cumulative-update-for-windows-10-version-1511-and-windows-server-2016) |
| Windows 8.1</br>Windows Server 2012 R2 | [TLS 시스템 기본 버전 Windows 8.1 및 Windows Server 2012 r 2에서.NET Framework 3.5에 포함 된에 대 한 지원](https://support.microsoft.com/help/3154520/support-for-tls-system-default-versions-included-in-the--net-framework) |
| Windows 8.0</br>Windows Server 2012 | [TLS 시스템 기본 버전 Windows Server 2012에서.NET Framework 3.5에 포함 된에 대 한 지원](https://support.microsoft.com/help/3154519/support-for-tls-system-default-versions-included-in-the--net-framework) |
| Windows 7 SP1</br>Windows Server 2008 R2 SP1 | [TLS 시스템 기본 버전 서버 2008 R2 SP1 및 Windows 7 s p 1에.NET Framework 3.5.1에에서 포함 된에 대 한 지원](https://support.microsoft.com/help/3154518/support-for-tls-system-default-versions-included-in-the--net-framework) |
| Windows Server 2008 | [TLS 시스템 기본 버전.NET Framework 2.0 s p 2에서 Windows Vista SP2 및 Server 2008 s p 2에 포함 된에 대 한 지원](https://support.microsoft.com/help/3154517/support-for-tls-system-default-versions-included-in-the--net-framework) |
| Windows Vista | 지원 안 함 |

## <a name="azure-cloud-services"></a>Azure Cloud Services

사용 중인 경우 [Azure 클라우드 서비스](https://azure.microsoft.com/services/cloud-services/) 웹 및 작업자 역할을 호스트 하 고 응용 프로그램을 실행 TLS 1.2 지원에 고려해 야 할 사항이 몇 가지 고려 사항 사항이 있습니다.

### <a name="net-framework-47-is-not-installed-on-azure-guest-os-by-default"></a>.NET framework 4.7는 기본적으로 Azure 게스트 OS에 설치 되어 있지

최신 Azure 게스트 OS 제품군 5 릴리스 (Windows Server 2016)에 설치 된 최신 버전 4.6.2입니다. 각 Azure 게스트 OS에 설치 된.NET Framework의 버전을 보려면 참조는 [Azure 게스트 OS 릴리스 및 SDK 호환성 매트릭스](https://docs.microsoft.com/azure/cloud-services/cloud-services-guestos-update-matrix)합니다.

Azure 게스트 OS 버전에서 사용할 수 없으면.NET Framework 버전을 대상으로 하는 응용 프로그램을 직접 설치 해야 합니다. 참조 [Azure 클라우드 서비스 역할에.NET 설치](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-install-dotnet)합니다. 프레임 워크 설치를 다시 시작이 필요한 경우 서비스 역할이 준비 상태를 입력 하기 전에 다시 시작할 수 있습니다.

### <a name="azure-guest-os-registry-settings"></a>Azure 게스트 OS 레지스트리 설정

Azure 게스트 OS 이미지에 대 한 [Azure 클라우드 서비스](https://azure.microsoft.com/services/cloud-services/) 이미는 `SchUseStrongCrypto` 레지스트리 키 값이 1로 설정 합니다. 자세한 내용은 참조 [SchUseStrongCrypto](#schusestrongcrypto)합니다.

설정의 [SystemDefaultTlsVersions](#systemdefaulttlsversions) 레지스트리 키를 1입니다. 참조 [Windows 레지스트리를 통해 보안 구성](#configuring-security-via-the-windows-registry)합니다.
