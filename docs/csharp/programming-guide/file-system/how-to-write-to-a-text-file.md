---
title: '방법: 텍스트 파일에 쓰기(C# 프로그래밍 가이드)'
ms.date: 07/20/2015
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- TextWriter.WriteLine
- StreamWriter.Close
helpviewer_keywords:
- files [C#], text files
- text, writing to files [C#]
ms.assetid: 2e99f184-d88b-4719-a7f1-d9ec482aa809
caps.latest.revision: 23
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: fa6de76e3981e0f05b5b192045043422a8a912aa
ms.sourcegitcommit: 935d5267c44f9bce801468ef95f44572f1417e8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="how-to-write-to-a-text-file-c-programming-guide"></a>방법: 텍스트 파일에 쓰기(C# 프로그래밍 가이드)
다음 코드 예제에서는 파일에 텍스트를 쓰는 여러 가지 방법을 보여 줍니다. 처음 두 예에서는 <xref:System.IO.File?displayProperty=nameWithType> 클래스의 정적 편의 메서드를 사용하여 `IEnumerable<string>`의 각 요소와 문자열을 텍스트 파일에 씁니다. 예제 3에서는 파일에 쓸 때 각 줄을 개별적으로 처리해야 하는 경우 파일에 텍스트를 추가하는 방법을 보여 줍니다. 예제 1-3에서는 파일의 기존 내용을 모두 덮어쓰지만 예제 4에서는 기존 파일에 텍스트를 추가하는 방법을 보여 줍니다.  
  
 이 예에서는 파일에 모든 문자열 리터럴을 작성합니다. 파일에 작성된 텍스트의 서식을 지정하려면 <xref:System.String.Format%2A> 메서드 또는 C# [문자열 보간](../../../csharp/language-reference/tokens/interpolated.md) 기능을 사용합니다.  
  
## <a name="example"></a>예  
 [!code-csharp[csFilesandFolders#3](../../../csharp/programming-guide/file-system/codesnippet/CSharp/how-to-write-to-a-text-file_1.cs)]  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 다음 조건에서 예외가 발생합니다.  
  
-   파일이 있지만 읽기 전용인 경우  
  
-   경로 이름이 너무 긴 경우  
  
-   디스크가 꽉 찬 경우  
  
## <a name="see-also"></a>참고 항목  
 [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
 [파일 시스템 및 레지스트리(C# 프로그래밍 가이드)](../../../csharp/programming-guide/file-system/index.md)  
 [샘플: 응용 프로그램 저장소에 컬렉션 저장](http://code.msdn.microsoft.com/CSWinStoreAppSaveCollection-bed5d6e6)
