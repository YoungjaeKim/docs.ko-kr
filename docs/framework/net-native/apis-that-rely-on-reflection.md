---
title: 리플렉션을 사용하는 API
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f9532629-6594-4a41-909f-d083f30a42f3
caps.latest.revision: ''
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 49ac12bcae3fd85744961a6e3b81129178c2c323
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="apis-that-rely-on-reflection"></a>리플렉션을 사용하는 API
코드에서 리플렉션이 사용되는지 여부가 확실치 않아 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 도구 체인이 런타임에 필요한 메타데이터를 보존하지 않는 경우가 있습니다. 이 항목에서는 리플렉션 API의 일부로는 간주되지 않지만 리플렉션을 사용해야 정상적으로 실행되는 몇 가지 일반적인 API 또는 프로그래밍 패턴에 대해 설명합니다. 소스 코드에서 이러한 API를 사용하는 경우 해당 API 호출 시 런타임에 [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md) 예외 또는 일부 기타 예외가 발생하지 않도록 API에 대한 정보를 런타임 지시문(.rd.xml) 파일에 추가할 수 있습니다.  
  
## <a name="typemakegenerictype-method"></a>Type.MakeGenericType 메서드  
 다음과 같은 코드를 사용해 `AppClass<T>` 메서드를 호출하여 제네릭 형식 <xref:System.Type.MakeGenericType%2A?displayProperty=nameWithType>를 동적으로 인스턴스화할 수 있습니다.  
  
 [!code-csharp[ProjectN#1](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/type_makegenerictype1.cs#1)]  
  
 이 코드가 런타임에 정상적으로 실행되려면 여러 메타데이터 항목이 필요합니다. 그 중 첫 번째는 인스턴스화되지 않은 제네릭 형식 `Browse`에 대한 `AppClass<T>` 메타데이터입니다.  
  
```xml  
<Type Name="App1.AppClass`1" Browse="Required PublicAndInternal" />  
```  
  
 이 메타데이터가 있으면 <xref:System.Type.GetType%28System.String%2CSystem.Boolean%29?displayProperty=nameWithType> 메서드가 정상적으로 호출되며 유효한 <xref:System.Type> 개체가 반환됩니다.  
  
 그러나 인스턴스화되지 않은 제네릭 형식에 대한 메타데이터를 추가하더라도 <xref:System.Type.MakeGenericType%2A?displayProperty=nameWithType> 메서드를 호출하면 [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md) 예외가 throw됩니다.  
  
```  
This operation cannot be carried out as metadata for the following type was removed for performance reasons:  
  
App1.AppClass`1<System.Int32>.  
```  
  
 다음 런타임 지시문을 런타임 지시문 파일에 추가하여 `Activate`를 통한 `AppClass<T>`의 특정 인스턴스화에 대해 <xref:System.Int32?displayProperty=nameWithType> 메타데이터를 추가할 수 있습니다.  
  
```xml  
<TypeInstantiation Name="App1.AppClass" Arguments="System.Int32"   
                   Activate="Required Public" />  
```  
  
 `AppClass<T>`를 통한 각 인스턴스화에서는 별도의 지시문이 필요합니다(<xref:System.Type.MakeGenericType%2A?displayProperty=nameWithType> 메서드를 사용하여 작성되며 정적으로 사용되지 않는 경우).  
  
## <a name="methodinfomakegenericmethod-method"></a>MethodInfo.MakeGenericMethod 메서드  
 `Class1` 클래스에 제네릭 메서드 `GetMethod<T>(T t)`가 포함되어 있는 경우 다음과 같은 코드를 사용하여 리플렉션을 통해 `GetMethod`를 호출할 수 있습니다.  
  
 [!code-csharp[ProjectN#2](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/makegenericmethod1.cs#2)]  
  
 이 코드를 정상적으로 실행하려면 다음과 같은 여러 메타데이터 항목이 필요합니다.  
  
-   해당 메서드를 호출할 형식에 대한 `Browse` 메타데이터  
  
-   호출하려는 메서드에 대한 `Browse` 메타데이터.  public 메서드의 경우 포함 형식에 대한 public `Browse` 메타데이터를 추가하면 메서드도 포함됩니다.  
  
-   호출하려는 메서드에 대한 동적 메타데이터([!INCLUDE[net_native](../../../includes/net-native-md.md)] 도구 체인에 의해 리플렉션 호출 대리자가 제거되지 않도록 함). 메서드에 대한 동적 메타데이터가 누락되면 <xref:System.Reflection.MethodInfo.MakeGenericMethod%2A?displayProperty=nameWithType> 메서드 호출 시 다음 예외가 throw됩니다.  
  
    ```  
    MakeGenericMethod() cannot create this generic method instantiation because the instantiation was not metadata-enabled: 'App1.Class1.GenMethod<Int32>(Int32)'.  
    ```  
  
 다음 런타임 지시문을 사용하면 필요한 모든 메타데이터를 사용할 수 있습니다.  
  
```xml  
<Type Name="App1.Class1" Browse="Required PublicAndInternal">  
   <MethodInstantiation Name="GenMethod" Arguments="System.Int32" Dynamic="Required"/>  
</Type>  
```  
  
 동적으로 호출되는 메서드의 서로 다른 각 인스턴스화에는 `MethodInstantiation` 지시문이 필요하며, 각 인스턴스화 인수를 반영하기 위해 `Arguments` 요소가 업데이트됩니다.  
  
## <a name="arraycreateinstance-and-typemaketypearray-methods"></a>Array.CreateInstance 및 Type.MakeTypeArray 메서드  
 다음 예제에서는 <xref:System.Type.MakeArrayType%2A?displayProperty=nameWithType> 형식에 대해 <xref:System.Array.CreateInstance%2A?displayProperty=nameWithType> 및 `Class1` 메서드를 호출합니다.  
  
 [!code-csharp[ProjectN#3](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/array1.cs#3)]  
  
 배열 메타데이터가 없으면 다음 오류가 발생합니다.  
  
```  
This operation cannot be carried out as metadata for the following type was removed for performance reasons:  
  
App1.Class1[]  
  
Unfortunately, no further information is available.  
```  
  
 배열 형식을 동적으로 인스턴스화하려면 해당 형식에 대한 `Browse` 메타데이터가 필요합니다.  다음 런타임 지시문을 사용하면 `Class1[]`을 동적으로 인스턴스화할 수 있습니다.  
  
```xml  
<Type Name="App1.Class1[]" Browse="Required Public" />  
```  
  
## <a name="see-also"></a>참고 항목  
 [시작](../../../docs/framework/net-native/getting-started-with-net-native.md)  
 [런타임 지시문(rd.xml) 구성 파일 참조](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)
