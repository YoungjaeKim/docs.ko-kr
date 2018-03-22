---
title: KEY(Entity SQL)
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-ado
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cbaa97a8-c89c-4460-8c74-00474695789f
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload:
- dotnet
ms.openlocfilehash: aa18efd32998f881d49d7ebd71bad0cdf8122457
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="key-entity-sql"></a>KEY(Entity SQL)
참조 또는 엔터티 식의 키를 추출합니다.  
  
## <a name="syntax"></a>구문  
  
```  
KEY(createref_expression)  
```  
  
## <a name="remarks"></a>설명  
 엔터티 키에는 지정한 엔터티 또는 엔터티 참조의 올바른 순서대로 키 값이 포함됩니다. 여러 엔터티 집합이 같은 형식을 기반으로 할 수 있으므로 동일한 키가 각 엔터티 집합에 나타날 수 있습니다. 고유한 참조를 만들려면 `REF`를 사용합니다. KEY 연산자의 반환 형식은 엔터티의 각 키에 해당하는 필드가 같은 순서대로 포함된 행 형식입니다.  
  
 다음 예제에서 Key 연산자는 BadOrder 엔터티에 대한 참조를 전달하고 해당 참조의 키 부분을 반환합니다. 이 경우 `Id` 속성에 해당하는 필드 한 개만 포함된 레코드 형식을 반환합니다.  
  
```  
select Key( CreateRef(LOB.BadOrders, row(o.Id)) )   
from LOB.Orders as o  
```  
  
## <a name="example"></a>예  
 다음 Entity SQL 쿼리에서는 KEY 연산자를 사용하여 형식 참조가 있는 식의 키 부분을 추출합니다. 쿼리는 AdventureWorks Sales 모델을 기반으로 합니다. 이 쿼리를 컴파일하고 실행하려면 다음 단계를 수행하세요.  
  
1.  [방법: StructuralType 결과를 반환하는 쿼리 실행](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md)의 절차를 따릅니다.  
  
2.  다음 쿼리를 `ExecuteStructuralTypeQuery` 메서드에 인수로 전달합니다.  
  
 [!code-csharp[DP EntityServices Concepts 2#KEY](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#key)]  
  
## <a name="see-also"></a>참고 항목  
 [엔터티 SQL 참조](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)  
 [CREATEREF](../../../../../../docs/framework/data/adonet/ef/language-reference/createref-entity-sql.md)  
 [REF](../../../../../../docs/framework/data/adonet/ef/language-reference/ref-entity-sql.md)  
 [DEREF](../../../../../../docs/framework/data/adonet/ef/language-reference/deref-entity-sql.md)
