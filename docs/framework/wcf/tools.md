---
title: Windows Communication Foundation 도구
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- WCF, tools
- Windows Communication Foundation, tools
ms.assetid: 399a47b4-bfea-434b-8e83-f76b5063d79d
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 6e28158076fcedf8c7d14d598b1c2ba0a25ff1f8
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="windows-communication-foundation-tools"></a>Windows Communication Foundation 도구
Microsoft [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 도구는 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 응용 프로그램을 보다 쉽게 만들고 배포하고 관리할 수 있도록 디자인되었습니다. 이 단원에서는 이러한 도구에 대해 자세하게 설명합니다. 이 도구는 지원되지 않습니다.  
  
 명령줄에서 모든 도구를 실행할 수 있습니다.  
  
 다음 표에서는 이러한 도구를 보여 주고 간단한 설명을 제공합니다.  
  
|도구|설명|  
|----------|-----------------|  
|[ServiceModel Metadata 유틸리티 도구(Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)|메타데이터 문서의 서비스 모델 코드 및 서비스 모델 코드의 메타데이터 문서를 생성합니다.|  
|[개인 키 찾기 도구(FindPrivateKey.exe)](../../../docs/framework/wcf/find-private-key-tool-findprivatekey-exe.md)|지정된 저장소에서 개인 키를 검색합니다.|  
|[ServiceModel 등록 도구(ServiceModelReg.exe)](../../../docs/framework/wcf/servicemodelreg-exe.md)|단일 시스템에서 ServiceModel의 등록 및 등록 취소를 관리합니다.|  
|[COM+ 서비스 모델 구성 도구(ComSvcConfig.exe)](../../../docs/framework/wcf/com-service-model-configuration-tool-comsvcconfig-exe.md)|COM+ 인터페이스가 웹 서비스로 노출되도록 구성합니다.|  
|[Configuration Editor 도구(SvcConfigEditor.exe)](../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md)|WCF 서비스의 구성 설정을 만들고 수정합니다.|  
|[Service Trace Viewer 도구(SvcTraceViewer.exe)](../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)|추적 메시지를 보고 그룹화하며 필터링하여 WCF 서비스에 대한 문제를 진단, 복구 및 확인할 수 있습니다.|  
|[WS-AtomicTransaction 구성 유틸리티(wsatConfig.exe)](../../../docs/framework/wcf/ws-atomictransaction-configuration-utility-wsatconfig-exe.md)|명령줄 도구를 사용하여 기본 WS-AtomicTransaction 지원 설정을 구성합니다.|  
|[WS-AtomicTransaction 구성 MMC 스냅인](../../../docs/framework/wcf/ws-atomictransaction-configuration-mmc-snap-in.md)|MMC 스냅인을 사용하여 기본 WS-AtomicTransaction 지원 설정을 구성합니다.|  
|[워크플로 서비스 등록 도구(WFServicesReg.exe)](../../../docs/framework/wcf/workflow-service-registration-tool-wfservicesreg-exe.md)|Windows 워크플로 서비스를 등록합니다.|  
|[WCF 서비스 호스트(WcfSvcHost.exe)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)|라이브러리 파일(*.dll)에 포함된 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 서비스를 호스팅합니다.|  
|[WCF 테스트 클라이언트(WcfTestClient.exe)](../../../docs/framework/wcf/wcf-test-client-wcftestclient-exe.md)|임의 형식의 매개 변수를 입력하고, 서비스에 해당 입력 내용을 전송하고, 서비스에서 되돌려 보내는 응답을 보는 데 사용할 수 있는 GUI 도구입니다.|  
|[계약 중심 도구](../../../docs/framework/wcf/contract-first-tool.md)|XSD 데이터 계약에서 코드 클래스를 만드는 Visual Studio 빌드 작업입니다.|  
  
 ServiceModelReg.exe, WsatConfig.exe 및 ComSvcConfig.exe를 제외한 모든 이전 도구는 Windows SDK와 함께 제공되며 C:\Program Files\Microsoft SDKs\Windows\v6.0\Bin 폴더 아래에 있습니다.  이 3개의 특정 도구는 C:\Windows\Microsoft.NET\Framework\v3.0\Windows Communication Foundation 아래에 있습니다.
