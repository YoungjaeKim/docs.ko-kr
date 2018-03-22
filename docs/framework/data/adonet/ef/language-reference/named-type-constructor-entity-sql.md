---
title: 명명된 형식 생성자(Entity SQL)
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-ado
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 549dea04-d93d-4c87-a292-f81b1598dbfd
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload:
- dotnet
ms.openlocfilehash: b572d09b812d43fa64e30a3058da9af01d29b747
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="named-type-constructor-entity-sql"></a>명명된 형식 생성자(Entity SQL)
엔터티 형식이나 복합 형식과 같은 개념적 모델 명목 형식의 인스턴스를 만드는 데 사용됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
[{identifier. }] identifier( [expression [{, expression }]] )  
```  
  
## <a name="arguments"></a>인수  
 `identifier`  
 단순 식별자 또는 따옴표 붙은 식별자인 값입니다. 자세한 내용은 참조 하십시오 [식별자](../../../../../../docs/framework/data/adonet/ef/language-reference/identifiers-entity-sql.md)  
  
 `expression`  
 형식의 특성으로서, 형식 선언에 나타나는 것과 동일한 순서일 것으로 가정됩니다.  
  
## <a name="return-value"></a>반환 값  
 명명된 복합 형식 및 엔터티 형식의 인스턴스입니다.  
  
## <a name="remarks"></a>설명  
 다음 예제에서는 명목 형식 및 복합 형식을 생성하는 방법을 보여 줍니다.  
  
 다음 식은 `Person` 형식의 인스턴스를 만듭니다.  
  
 `Person("abc", 12)`  
  
 다음 식은 복합 형식의 인스턴스를 만듭니다.  
  
 `MyModel.ZipCode(‘98118’, ‘4567’)`  
  
 다음 식은 중첩된 복합 형식의 인스턴스를 만듭니다.  
  
 `MyModel.AddressInfo('My street address', 'Seattle', 'WA', MyModel.ZipCode('98118', '4567'))`  
  
 다음 식은 중첩된 복합 형식을 가진 엔터티의 인스턴스를 만듭니다.  
  
 `MyModel.Person("Bill", MyModel.AddressInfo('My street address', 'Seattle', 'WA', MyModel.ZipCode('98118', '4567')))`  
  
 다음 예제에서는 복합 형식의 속성을 null로 초기화하는 방법을 보여 줍니다.`MyModel.ZipCode(‘98118’, null)`  
  
## <a name="example"></a>예  
 다음 Entity SQL 쿼리에서는 명명된 형식 생성자를 사용하여 개념적 모델 형식의 인스턴스를 만듭니다. 쿼리는 AdventureWorks Sales 모델을 기반으로 합니다. 이 쿼리를 컴파일하고 실행하려면 다음 단계를 수행하세요.  
  
1.  [방법: StructuralType 결과를 반환하는 쿼리 실행](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md)의 절차를 따릅니다.  
  
2.  다음 쿼리를 `ExecuteStructuralTypeQuery` 메서드에 인수로 전달합니다.  
  
 [!code-csharp[DP EntityServices Concepts 2#NAMED_TYPE_CONSTRUCTOR](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#named_type_constructor)]  
  
## <a name="see-also"></a>참고 항목  
 [형식 생성](../../../../../../docs/framework/data/adonet/ef/language-reference/constructing-types-entity-sql.md)  
 [엔터티 SQL 참조](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)
