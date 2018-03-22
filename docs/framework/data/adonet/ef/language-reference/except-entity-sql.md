---
title: EXCEPT(Entity SQL)
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-ado
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 69cc23e5-3f8f-4b49-b20e-2f84ff11c80d
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload:
- dotnet
ms.openlocfilehash: 546503d3fc51c863779c26f363721bf81be054b9
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="except-entity-sql"></a>EXCEPT(Entity SQL)
EXCEPT 피연산자 오른쪽 쿼리 식에서 반환되지 않은 모든 고유한 값 컬렉션을 EXCEPT 피연산자 왼쪽에 있는 쿼리 식에서 반환합니다. 모든 식은 형식이 같거나 기본 형식 또는 파생 형식이 `expression`이어야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
expression EXCEPT expression  
```  
  
## <a name="arguments"></a>인수  
 `expression`  
 다른 쿼리 식에서 반환된 컬렉션과 비교할 컬렉션을 반환하는 모든 유효한 쿼리 식입니다.  
  
## <a name="return-value"></a>반환 값  
 형식이 같거나 기본 형식 또는 파생 형식이 `expression`인 컬렉션입니다.  
  
## <a name="remarks"></a>설명  
 EXCEPT는 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 집합 연산자 중 하나입니다. 모든 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 집합 연산자는 왼쪽에서 오른쪽으로 계산됩니다. 다음 표에서는 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 집합 연산자의 우선 순위를 보여 줍니다.  
  
|우선 순위|연산자|  
|----------------|---------------|  
|가장 높음|INTERSECT|  
||UNION<br /><br /> UNION ALL|  
||EXCEPT|  
|가장 낮음|EXISTS<br /><br /> OVERLAPS<br /><br /> FLATTEN<br /><br /> SET|  
  
## <a name="example"></a>예  
 다음 Entity SQL 쿼리에서는 EXCEPT 연산자를 사용하여 두 쿼리 식에서 모든 고유한 값의 컬렉션을 반환합니다. 쿼리는 AdventureWorks Sales 모델을 기반으로 합니다. 이 쿼리를 컴파일하고 실행하려면 다음 단계를 수행하세요.  
  
1.  [방법: StructuralType 결과를 반환하는 쿼리 실행](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md)의 절차를 따릅니다.  
  
2.  다음 쿼리를 `ExecuteStructuralTypeQuery` 메서드에 인수로 전달합니다.  
  
 [!code-csharp[DP EntityServices Concepts 2#EXCEPT](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#except)]  
  
## <a name="see-also"></a>참고 항목  
 [엔터티 SQL 참조](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)
