---
title: BETWEEN(Entity SQL)
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-ado
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4dcdd754-ae01-4e78-bf28-8a117fb2b73e
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload:
- dotnet
ms.openlocfilehash: 3b27aee261e9195c2cb5f15e369cf26de4c0691a
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="between-entity-sql"></a>BETWEEN(Entity SQL)
식의 결과 값이 지정된 범위에 속하는지 여부를 결정합니다. [!INCLUDE[esql](../../../../../../includes/esql-md.md)] BETWEEN 식의 기능은 Transact-SQL BETWEEN 식의 기능과 동일합니다.  
  
## <a name="syntax"></a>구문  
  
```  
expression [ NOT ] BETWEEN begin_expression AND end_expression    
```  
  
## <a name="arguments"></a>인수  
 `expression`  
 `begin_expression`과 `end_expression`으로 정의된 범위 내에서 테스트할 모든 유효한 식입니다. `expression`의 형식은 `begin_expression`과 `end_expression` 두 가지 모두의 형식과 같아야 합니다.  
  
 `begin_expression`  
 모든 유효한 식입니다. `begin_expression`의 형식은 `expression`과 `end_expression` 두 가지 모두의 형식과 같아야 합니다. `begin_expression`은 `end_expression`보다 작아야 합니다. 그렇지 않으면 반환 값이 무효화됩니다.  
  
 `end_expression`  
 모든 유효한 식입니다. `end_expression`의 형식은 `expression`과 `begin_expression` 두 가지 모두의 형식과 같아야 합니다.  
  
 NOT  
 BETWEEN의 결과를 무효화하도록 지정합니다.  
  
 AND  
 `expression`이 `begin_expression`과 `end_expression` 범위 내에 있어야 함을 나타내는 자리 표시자 역할을 합니다.  
  
## <a name="return-value"></a>반환 값  
 `true`이 `expression`과 `begin_expression`이 가리키는 범위에 있으면 `end_expression`이고, 그렇지 않으면 `false`입니다. `null`이 `expression`이거나 `null` 또는 `begin_expression`이 `end_expression`이면 `null`이 반환됩니다.  
  
## <a name="remarks"></a>설명  
 범위에서 해당 시작 값과 끝 값을 제외하려면 BETWEEN 대신 보다 큼(>) 및 보다 작음(<) 연산자를 사용합니다.  
  
## <a name="example"></a>예  
 다음 Entity SQL 쿼리에서는 BETWEEN 연산자를 사용하여 식의 결과 값이 지정된 범위에 속하는지 여부를 결정합니다. 쿼리는 AdventureWorks Sales 모델을 기반으로 합니다. 이 쿼리를 컴파일하고 실행하려면 다음 단계를 수행하세요.  
  
1.  [방법: StructuralType 결과를 반환하는 쿼리 실행](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md)의 절차를 따릅니다.  
  
2.  다음 쿼리를 `ExecuteStructuralTypeQuery` 메서드에 인수로 전달합니다.  
  
 [!code-csharp[DP EntityServices Concepts 2#BETWEEN](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#between)]  
  
## <a name="see-also"></a>참고 항목  
 [엔터티 SQL 참조](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)
