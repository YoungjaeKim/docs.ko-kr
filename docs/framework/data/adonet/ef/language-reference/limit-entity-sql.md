---
title: LIMIT(Entity SQL)
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-ado
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c22ffede-0a52-44d1-99b9-4a91e651e1b9
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload:
- dotnet
ms.openlocfilehash: c0b2a421b1187fcf88278b66f3225133330a3033
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="limit-entity-sql"></a>LIMIT(Entity SQL)
ORDER BY 절에서 LIIMIT 하위 절을 사용하여 물리적 페이징을 수행할 수 있습니다. LIMIT 절은 ORDER BY 절과 별도로 사용할 수 없습니다.  
  
## <a name="syntax"></a>구문  
  
```  
[ LIMIT n ]  
```  
  
## <a name="arguments"></a>인수  
 `n`  
 선택할 항목의 개수입니다.  
  
 LIMIT 식 하위 절이 ORDER BY 절에 있으면 쿼리는 정렬 지정에 따라 정렬되고 결과 행의 수는 LIMIT 식으로 제한됩니다. 예를 들어, LIMIT 5는 결과 집합을 다섯 개의 인스턴스 또는 행으로 제한합니다. LIMIT는 ORDER BY 절이 반드시 있어야 한다는 점을 제외하고는 TOP와 동일합니다. SKIP 및 LIMIT 절은 각각 ORDER BY 절과 함께 사용할 수 있습니다.  
  
> [!NOTE]
>  TOP 한정자와 SKIP 하위 절이 모두 같은 쿼리 식에 있는 경우 Entity SQL 쿼리는 유효하지 않은 것으로 간주됩니다. TOP 식을 변경하여 쿼리를 LIMIT 식에 다시 써야 합니다.  
  
## <a name="example"></a>예  
 다음 Entity SQL 쿼리는 LIMIT와 함께 ORDER BY 연산자를 사용하여 SELECT 문에서 반환되는 개체에 적용하는 정렬 순서를 지정합니다. 쿼리는 AdventureWorks Sales 모델을 기반으로 합니다. 이 쿼리를 컴파일하고 실행하려면 다음 단계를 수행하세요.  
  
1.  [방법: StructuralType 결과를 반환하는 쿼리 실행](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md)의 절차를 따릅니다.  
  
2.  다음 쿼리를 `ExecuteStructuralTypeQuery` 메서드에 인수로 전달합니다.  
  
 [!code-csharp[DP EntityServices Concepts 2#LIMIT](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#limit)]  
  
## <a name="see-also"></a>참고 항목  
 [ORDER BY](../../../../../../docs/framework/data/adonet/ef/language-reference/order-by-entity-sql.md)  
 [방법: 쿼리를 통해 페이지 결과](http://msdn.microsoft.com/library/ffc0f920-e7de-42e0-9b12-ef356421d030)  
 [페이징](../../../../../../docs/framework/data/adonet/ef/language-reference/paging-entity-sql.md)  
 [TOP](../../../../../../docs/framework/data/adonet/ef/language-reference/top-entity-sql.md)
