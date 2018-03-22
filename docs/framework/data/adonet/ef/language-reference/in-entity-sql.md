---
title: IN(Entity SQL)
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-ado
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 51662950-ee01-4857-b7b9-311dd8515966
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload:
- dotnet
ms.openlocfilehash: d32e5012b4acbf0ecd6830f549de5dccf79bb38b
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="in-entity-sql"></a>IN(Entity SQL)
컬렉션에 일치하는 값이 있는지 여부를 확인합니다.  
  
## <a name="syntax"></a>구문  
  
```  
value [ NOT ] IN expression  
```  
  
## <a name="arguments"></a>인수  
 `value`  
 일치시킬 값을 반환하는 모든 유효한 식입니다.  
  
 [NOT]  
 IN의 `Boolean` 결과를 부정하도록 지정합니다.  
  
 `expression`  
 일치 여부를 테스트할 컬렉션을 반환하는 모든 유효한 식입니다. 모든 식은 형식이 같거나 기본 형식 또는 파생 형식이 `value`이어야 합니다.  
  
## <a name="return-value"></a>반환 값  
 값이 컬렉션에 있으면 `true`이고, 값 또는 컬렉션이 null이면 null이고, 그렇지 않으면 `false`입니다. NOT IN을 사용하면 IN의 결과가 부정됩니다.  
  
## <a name="example"></a>예  
 다음 Entity SQL 쿼리에서는 IN 연산자를 사용하여 컬렉션에 일치하는 값이 있는지 여부를 결정합니다. 쿼리는 AdventureWorks Sales 모델을 기반으로 합니다. 이 쿼리를 컴파일하고 실행하려면 다음 단계를 수행하세요.  
  
1.  [방법: StructuralType 결과를 반환하는 쿼리 실행](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md)의 절차를 따릅니다.  
  
2.  다음 쿼리를 `ExecuteStructuralTypeQuery` 메서드에 인수로 전달합니다.  
  
 [!code-csharp[DP EntityServices Concepts 2#IN](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#in)]  
  
## <a name="see-also"></a>참고 항목  
 [엔터티 SQL 참조](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)
