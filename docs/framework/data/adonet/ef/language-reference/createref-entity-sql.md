---
title: CREATEREF (Entity SQL)
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-ado
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 489828cf-a335-4449-9360-b0d92eec5481
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload:
- dotnet
ms.openlocfilehash: 8de4266277be31fd51411d4b994f1b5de45f13df
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="createref-entity-sql"></a>CREATEREF (Entity SQL)
entityset의 엔터티에 대한 참조를 작성합니다.  
  
## <a name="syntax"></a>구문  
  
```  
CreateRef(entityset_identifier, row_typed_expression)  
```  
  
## <a name="arguments"></a>인수  
 `entityset_identifier`  
 문자열 리터럴이 아니라 entityset 식별자입니다.  
  
 `row_typed_expression`  
 엔터티 형식의 키 속성에 해당하는 행 형식의 식입니다.  
  
## <a name="remarks"></a>설명  
 `row_typed_expression` 은 엔터티의 키 유형과 구조적으로 동일해야 합니다. 다시 말해서, 필드의 개수와 형식 및 배열 순서가 엔터티 키와 동일해야 합니다.  
  
 아래 예제에서 Order와 BadOrder는 모두 Order 형식의 entityset이며, Id는 Order의 단일 키 속성인 것으로 간주됩니다. 예제에서는 BadOrder의 엔터티에 대한 참조를 생성하는 방법을 설명합니다. 이 참조는 현수 참조일 수 있습니다.  다시 말해서, 참조가 특정 엔터티를 실제로 나타내지 않을 수 있습니다. 이런 경우 해당 참조에 대해 `DEREF` 작업을 수행하면 null이 반환됩니다.  
  
```  
select CreateRef(LOB.BadOrders, row(o.Id))   
from LOB.Orders as o   
```  
  
## <a name="example"></a>예  
 다음 Entity SQL 쿼리는 CREATEREF 연산자를 사용하여 엔터티 집합 내의 엔터티에 대한 참조를 작성합니다. 쿼리는 AdventureWorks Sales 모델을 기반으로 합니다. 이 쿼리를 컴파일하고 실행하려면 다음 단계를 수행하세요.  
  
1.  [방법: StructuralType 결과를 반환하는 쿼리 실행](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md)의 절차를 따릅니다.  
  
2.  다음 쿼리를 `ExecuteStructuralTypeQuery` 메서드에 인수로 전달합니다.  
  
 [!code-csharp[DP EntityServices Concepts 2#CREATEREF](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#createref)]  
  
## <a name="see-also"></a>참고 항목  
 [엔터티 SQL 참조](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)  
 [DEREF](../../../../../../docs/framework/data/adonet/ef/language-reference/deref-entity-sql.md)  
 [KEY](../../../../../../docs/framework/data/adonet/ef/language-reference/key-entity-sql.md)  
 [REF](../../../../../../docs/framework/data/adonet/ef/language-reference/ref-entity-sql.md)
