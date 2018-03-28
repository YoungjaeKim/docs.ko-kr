---
title: '방법: 단일 파일 어셈블리 만들기'
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-bcl
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- assembly manifest, single-file assemblies
- library assemblies
- command-line compilers
- assemblies [.NET Framework], single-file
- output file name for assemblies
- code modules
- single-file assemblies
ms.assetid: a6063221-43a5-4d3e-814c-288a4ec69aec
caps.latest.revision: ''
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 80fa584a21a3bdfb9392021959d777139daafd04
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="how-to-build-a-single-file-assembly"></a>방법: 단일 파일 어셈블리 만들기
가장 단순한 형식의 어셈블리인 단일 파일 어셈블리에는 형식 정보 및 구현과 [어셈블리 매니페스트](../../../docs/framework/app-domains/assembly-manifest.md)가 포함되어 있습니다. 명령줄 컴파일러 또는 [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)]를 사용하여 단일 파일 어셈블리를 만들 수 있습니다. 기본적으로 컴파일러는 확장명이 .exe인 어셈블리 파일을 만듭니다.  
  
> [!NOTE]
>  C# 및 Visual Basic용 [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)]는 단일 파일 어셈블리를 만드는 경우에만 사용할 수 있습니다. 다중 파일 어셈블리를 만들려면 명령줄 컴파일러나 Visual C++용 [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)]를 사용해야 합니다.  
  
 다음 절차에는 명령줄 컴파일러를 사용하여 단일 파일 어셈블리를 만드는 방법을 보여 줍니다.  
  
### <a name="to-create-an-assembly-with-an-exe-extension"></a>확장명이 .exe인 어셈블리를 만들려면  
  
1.  명령 프롬프트에 다음 명령을 입력합니다.  
  
     \<*compiler command*> \<*module name*>  
  
     이 명령에서 *compiler command*는 코드 모듈에서 사용되는 언어에 대한 컴파일러 명령이고, *module name*은 어셈블리로 컴파일할 코드 모듈의 이름입니다.  
  
 다음 예제에서는 `myCode`라는 코드 모듈에서 `myCode.exe` 어셈블리를 만듭니다.  
  
```console
csc myCode.cs  
```  

```console
vbc myCode.vb  
```  
  
#### <a name="to-create-an-assembly-with-an-exe-extension-and-specify-the-output-file-name"></a>확장명이 .exe인 어셈블리를 만들고 출력 파일 이름을 지정하려면  
  
1.  명령 프롬프트에 다음 명령을 입력합니다.  
  
     \<*compiler command*> **/out:**\<*file name*> \<*module name*>  
  
     이 명령에서 *compiler command*는 코드 모듈에서 사용되는 언어에 대한 컴파일러 명령이고, *file name*은 출력 파일 이름이고, *module name*은 어셈블리로 컴파일할 코드 모듈의 이름입니다.  
  
 다음 예제에서는 `myCode`라는 코드 모듈에서 `myAssembly.exe` 어셈블리를 만듭니다.  
  
```console  
csc -out:myAssembly.exe myCode.cs  
```  
  
```console
vbc -out:myAssembly.exe myCode.vb  
```  
  
## <a name="creating-library-assemblies"></a>라이브러리 어셈블리 만들기  
 라이브러리 어셈블리는 클래스 라이브러리와 비슷합니다. 다른 어셈블리에서 참조되는 형식을 포함하지만 실행을 시작할 진입점이 없습니다.  
  
#### <a name="to-create-a-library-assembly"></a>라이브러리 어셈블리를 만들려면  
  
1.  명령 프롬프트에 다음 명령을 입력합니다.  
  
     \<*compiler command*> **-t:library** \<*module name*>  
  
     이 명령에서 *compiler command*는 코드 모듈에서 사용되는 언어에 대한 컴파일러 명령이고, *module name*은 어셈블리로 컴파일할 코드 모듈의 이름입니다. **-out:** 옵션 등의 다른 컴파일러 옵션을 사용할 수도 있습니다.  
  
 다음 예제에서는 `myCode`라는 코드 모듈에서 `myCodeAssembly.dll`이라는 라이브러리 어셈블리를 만듭니다.  
  
```console  
csc -out:myCodeLibrary.dll -t:library myCode.cs  
```  
  
```console
vbc -out:myCodeLibrary.dll -t:library myCode.vb  
```  
  
## <a name="see-also"></a>참고 항목  
 [어셈블리 만들기](../../../docs/framework/app-domains/create-assemblies.md)  
 [다중 파일 어셈블리](../../../docs/framework/app-domains/multifile-assemblies.md)  
 [방법: 다중 파일 어셈블리 빌드](../../../docs/framework/app-domains/how-to-build-a-multifile-assembly.md)  
 [어셈블리를 사용한 프로그래밍](../../../docs/framework/app-domains/programming-with-assemblies.md)
