---
title: ".NET에서 문자열 채우기"
ms.custom: 
ms.date: 03/15/2018
ms.prod: .net
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- strings [.NET Framework], padding
- white space
- PadRight method
- PadLeft method
- padding strings
ms.assetid: 84a9f142-3244-4c90-ba02-21af9bbaff71
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: bf90c841c8fff21dd423fcd19613b5eb46a2c80c
ms.sourcegitcommit: 1c0b0f082b3f300e54b4d069b317ac724c88ddc3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/16/2018
---
# <a name="padding-strings-in-net"></a>.NET에서 문자열 채우기

다음 <xref:System.String> 메서드 중 하나를 사용하여 원래 문자열에 선행 또는 후행 문자를 지정된 총 길이까지 추가해 새로 구성된 문자열을 만듭니다. 안쪽 여백 문자는 공백이나 지정된 문자일 수 있습니다. 결과 문자열은 오른쪽 맞춤 또는 왼쪽 맞춤으로 표시됩니다. 원래 문자열의 길이가 원하는 총 길이보다 크거나 같은 경우 안쪽 여백 메서드는 변경되지 않은 원래 문자열을 반환합니다. 자세한 내용은 <xref:System.String.PadLeft%2A?displayProperty=nameWithType> 및 <xref:System.String.PadRight%2A?displayProperty=nameWithType> 메서드의 두 오버로드의 **반환** 섹션을 참조하세요.
  
|메서드 이름|사용|  
|-----------------|---------|  
|<xref:System.String.PadLeft%2A?displayProperty=nameWithType>|선행 문자로 문자열의 지정한 총 길이를 채웁니다.|  
|<xref:System.String.PadRight%2A?displayProperty=nameWithType>|후행 문자로 문자열의 지정한 총 길이를 채웁니다.|  
  
## <a name="padleft"></a>PadLeft  
 <xref:System.String.PadLeft%2A?displayProperty=nameWithType> 메서드는 지정된 총 길이에 맞도록 필요한 만큼 선행 채움 문자를 원래 문자열에 연결하여 새 문자열을 만듭니다. <xref:System.String.PadLeft%28System.Int32%29?displayProperty=nameWithType> 메서드는 공백을 채움 문자로 사용하며, <xref:System.String.PadLeft%28System.Int32%2CSystem.Char%29?displayProperty=nameWithType> 메서드를 사용하면 고유한 채움 문자를 지정할 수 있습니다.  
  
 다음 코드 예제에서는 <xref:System.String.PadLeft%2A> 메서드를 사용하여 20자 길이의 새 문자열을 만듭니다. 이 예제에서는 콘솔에 "`--------Hello World!`"를 표시합니다.  
  
 [!code-cpp[Conceptual.String.BasicOps#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/padding.cpp#3)]
 [!code-csharp[Conceptual.String.BasicOps#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/padding.cs#3)]
 [!code-vb[Conceptual.String.BasicOps#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/padding.vb#3)]  
  
## <a name="padright"></a>PadRight  
 <xref:System.String.PadRight%2A?displayProperty=nameWithType> 메서드는 지정된 총 길이에 맞도록 필요한 만큼 후행 채움 문자를 원래 문자열에 연결하여 새 문자열을 만듭니다. <xref:System.String.PadRight%28System.Int32%29?displayProperty=nameWithType> 메서드는 공백을 채움 문자로 사용하며, <xref:System.String.PadRight%28System.Int32%2CSystem.Char%29?displayProperty=nameWithType> 메서드를 사용하면 고유한 채움 문자를 지정할 수 있습니다.  
  
 다음 코드 예제에서는 <xref:System.String.PadRight%2A> 메서드를 사용하여 20자 길이의 새 문자열을 만듭니다. 이 예제에서는 콘솔에 "`Hello World!--------`"를 표시합니다.  
  
 [!code-cpp[Conceptual.String.BasicOps#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/padding.cpp#4)]
 [!code-csharp[Conceptual.String.BasicOps#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/padding.cs#4)]
 [!code-vb[Conceptual.String.BasicOps#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/padding.vb#4)]  
  
## <a name="see-also"></a>참고 항목  
 [기본적인 문자열 작업](../../../docs/standard/base-types/basic-string-operations.md)
