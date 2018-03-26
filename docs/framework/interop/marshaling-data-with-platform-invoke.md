---
title: 플랫폼 호출을 사용하여 데이터 마샬링
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- cpp
helpviewer_keywords:
- platform invoke, marshaling data
- data marshaling, platform invoke
- marshaling, platform invoke
ms.assetid: dc5c76cf-7b12-406f-b79c-d1a023ec245d
caps.latest.revision: ''
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 24ae6da0b32cf15ee9104bd10ba5fe6bb03a9763
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="marshaling-data-with-platform-invoke"></a>플랫폼 호출을 사용하여 데이터 마샬링
관리되지 않는 라이브러리에서 내보낸 함수를 호출하려면 .NET Framework 응용 프로그램의 관리 코드에 관리되지 않는 함수를 나타내는 함수 프로토타입이 필요합니다. 데이터를 제대로 마샬링하도록 플랫폼에서 호출할 수 있는 프로토타입을 만들려면 다음을 수행해야 합니다.  
  
-   관리 코드의 정적 함수 또는 메서드에 <xref:System.Runtime.InteropServices.DllImportAttribute> 특성을 적용합니다.  
  
-   관리되지 않은 데이터 형식 대신 관리되는 데이터 형식을 사용합니다.  
  
 관리되지 않는 함수와 함께 제공된 설명서를 사용하여 선택적 필드가 포함된 특성을 적용하고 관리되지 않는 형식 대신 관리되는 데이터 형식을 사용하는 방식으로 해당하는 관리되는 프로토타입을 생성할 수 있습니다. **DllImportAttribute**를 적용하는 방법에 대한 자세한 내용은 [관리되지 않는 DLL 함수 사용](../../../docs/framework/interop/consuming-unmanaged-dll-functions.md)을 참조하세요.  
  
 이 섹션에서는 인수를 전달하고 관리되는 라이브러리를 통해 내보낸 함수에서 반환 값을 수신하기 위한 관리되는 함수 프로토타입을 만드는 방법을 보여 주는 샘플을 제공합니다. 샘플에서는 데이터를 명시적으로 마샬링하도록 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 특성과 <xref:System.Runtime.InteropServices.Marshal> 클래스를 사용하는 시기를 보여 줍니다.  
  
## <a name="platform-invoke-data-types"></a>플랫폼 호출 데이터 형식  
 다음 표에는 Win32 API(Wtypes.h에 나열됨) 및 C 스타일 함수에서 사용되는 데이터 형식이 나와 있습니다. 대부분 관리되지 않는 라이브러리에는 이들 데이터 형식을 매개 변수 및 반환 값으로 전달하는 함수가 있습니다. 세 번째 열에는 관리 코드에서 사용하는 것에 해당하는 .NET Framework 기본 제공 값 형식 또는 클래스가 나열됩니다. 경우에 따라 표에 나열된 형식 대신 같은 크기의 형식을 사용할 수 있습니다.  
  
|Wtypes.h의 관리되지 않는 형식|관리되지 않는 C 언어 형식|관리되지 않는 클래스 이름|설명|  
|--------------------------------|-------------------------------|------------------------|-----------------|  
|**HANDLE**|**void\***|<xref:System.IntPtr?displayProperty=nameWithType>|32비트 Windows 운영 체제의 32비트, 64비트 운영 체제의 64비트.|  
|**BYTE**|**unsigned char**|<xref:System.Byte?displayProperty=nameWithType>|8비트|  
|**SHORT**|**short**|<xref:System.Int16?displayProperty=nameWithType>|16비트|  
|**WORD**|**unsigned short**|<xref:System.UInt16?displayProperty=nameWithType>|16비트|  
|**INT**|**int**|<xref:System.Int32?displayProperty=nameWithType>|32비트|  
|**UINT**|**unsigned int**|<xref:System.UInt32?displayProperty=nameWithType>|32비트|  
|**LONG**|**long**|<xref:System.Int32?displayProperty=nameWithType>|32비트|  
|**BOOL**|**long**|<xref:System.Byte>|32비트|  
|**DWORD**|**unsigned long**|<xref:System.UInt32?displayProperty=nameWithType>|32비트|  
|**ULONG**|**unsigned long**|<xref:System.UInt32?displayProperty=nameWithType>|32비트|  
|**CHAR**|**char**|<xref:System.Char?displayProperty=nameWithType>|ANSI로 데코레이트합니다.|  
|**WCHAR**|**wchar_t**|<xref:System.Char?displayProperty=nameWithType>|유니코드로 데코레이트합니다.|  
|**LPSTR**|**char\***|<xref:System.String?displayProperty=nameWithType> 또는 <xref:System.Text.StringBuilder?displayProperty=nameWithType>|ANSI로 데코레이트합니다.|  
|**LPCSTR**|**Const char\***|<xref:System.String?displayProperty=nameWithType> 또는 <xref:System.Text.StringBuilder?displayProperty=nameWithType>|ANSI로 데코레이트합니다.|  
|**LPWSTR**|**wchar_t\***|<xref:System.String?displayProperty=nameWithType> 또는 <xref:System.Text.StringBuilder?displayProperty=nameWithType>|유니코드로 데코레이트합니다.|  
|**LPCWSTR**|**Const wchar_t\***|<xref:System.String?displayProperty=nameWithType> 또는 <xref:System.Text.StringBuilder?displayProperty=nameWithType>|유니코드로 데코레이트합니다.|  
|**FLOAT**|**Float**|<xref:System.Single?displayProperty=nameWithType>|32비트|  
|**DOUBLE**|**Double**|<xref:System.Double?displayProperty=nameWithType>|64비트|  
  
 [!INCLUDE[vbprvblong](../../../includes/vbprvblong-md.md)], C# 및 C++의 해당하는 형식에 대해서는 [.NET Framework 클래스 라이브러리 소개](../../../docs/standard/class-library-overview.md)를 참조하세요.  
  
## <a name="pinvokelibdll"></a>PinvokeLib.dll  
 다음 코드에서는 Pinvoke.dll에서 제공되는 라이브러리 함수를 정의합니다. 이 섹션에 설명된 대부분 샘플이 이 라이브러리를 호출합니다.  
  
### <a name="example"></a>예제  
 [!code-cpp[PInvokeLib#1](../../../samples/snippets/cpp/VS_Snippets_CLR/pinvokelib/cpp/pinvokelib.cpp#1)]  
  
 [!code-cpp[PInvokeLib#2](../../../samples/snippets/cpp/VS_Snippets_CLR/pinvokelib/cpp/pinvokelib.h#2)]
