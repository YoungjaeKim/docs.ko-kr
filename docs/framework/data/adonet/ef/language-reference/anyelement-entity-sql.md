---
title: ANYELEMENT(Entity SQL)
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-ado
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 475a9ad6-8c8d-4f49-9970-af273e5360f1
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload:
- dotnet
ms.openlocfilehash: 6e74fbac9c2c57c653f55f76bf165d7eaebd9cee
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="anyelement-entity-sql"></a>ANYELEMENT(Entity SQL)
다중값 컬렉션에서 요소를 추출합니다.  
  
## <a name="syntax"></a>구문  
  
```  
ANYELEMENT ( expression )  
```  
  
## <a name="arguments"></a>인수  
 `expression`  
 요소를 추출할 컬렉션을 반환하는 유효한 쿼리 식입니다.  
  
## <a name="return-value"></a>반환 값  
 컬렉션의 단일 요소 또는 임의 요소(컬렉션에 여러 요소가 있는 경우)를 반환하거나 컬렉션이 비어 있는 경우 `null`을 반환합니다. 경우 `collection` 형식의 컬렉션인 `Collection<T>`, 다음 `ANYELEMENT(collection)` 형식의 인스턴스를 생성 하는 유효한 식 `T`합니다.  
  
## <a name="remarks"></a>설명  
 ANYELEMENT는 다중값 컬렉션에서 임의의 요소를 추출합니다. 예를 들어, 다음 예제에서는 `Customers`집합에서 singleton 요소를 추출하려고 시도합니다.  
  
```  
ANYELEMENT(Customers)  
```  
  
## <a name="example"></a>예  
 다음 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 쿼리에서는 ANYELEMENT 연산자를 사용하여 다중값 컬렉션에서 요소를 추출합니다. 쿼리는 AdventureWorks Sales 모델을 기반으로 합니다. 이 쿼리를 컴파일하고 실행하려면 다음 단계를 수행하세요.  
  
1.  [방법: StructuralType 결과를 반환하는 쿼리 실행](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md)의 절차를 따릅니다.  
  
2.  다음 쿼리를 `ExecuteStructuralTypeQuery` 메서드에 인수로 전달합니다.  
  
 [!code-csharp[DP EntityServices Concepts 2#ANYELEMENT](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#anyelement)]  
  
## <a name="see-also"></a>참고 항목  
 [엔터티 SQL 참조](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)  
 [null 허용 구조적 형식](../../../../../../docs/framework/data/adonet/ef/language-reference/nullable-structured-types-entity-sql.md)
