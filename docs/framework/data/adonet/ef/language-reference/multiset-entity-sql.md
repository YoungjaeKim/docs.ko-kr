---
title: MULTISET (Entity SQL)
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-ado
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: eb90a377-e47a-43a5-b308-e993b6d611e6
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload:
- dotnet
ms.openlocfilehash: 6389051ae1244a2a38699704c67217d9807fe7e4
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="multiset-entity-sql"></a>MULTISET (Entity SQL)
값 목록에서 multiset 인스턴스를 만듭니다. MULTISET 생성자의 모든 값은 호환되는 `T`형식이어야 합니다. 빈 multiset 생성자는 사용할 수 없습니다.  
  
## <a name="syntax"></a>구문  
  
```  
MULTISET ( expression [{, expression }] )  
or  
{ expression [{, expression }] }  
```  
  
## <a name="arguments"></a>인수  
 `expression`  
 유효한 모든 값 목록입니다.  
  
## <a name="return-value"></a>반환 값  
 MULTISET 유형의 컬렉션\<T >.  
  
## <a name="remarks"></a>설명  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 에서는 행 생성자, 개체 생성자, multiset 또는 컬렉션 생성자라는 세 가지 종류의 생성자를 제공합니다. 자세한 내용은 참조 [생성 형식](../../../../../../docs/framework/data/adonet/ef/language-reference/constructing-types-entity-sql.md)합니다.  
  
 multiset 생성자는 값 목록에서 multiset 인스턴스를 만듭니다. 생성자의 모든 값은 호환되는 형식이어야 합니다.  
  
 예를 들어, 다음 식은 정수의 multiset를 만듭니다.  
  
 `MULTISET(1, 2, 3)`  
  
 `{1, 2, 3}`  
  
> [!NOTE]
>  중첩된 multiset 리터럴은 래핑 mutiset에 단일 multiset 요소가 있는 경우(예: `{{1, 2, 3}}`)에만 지원됩니다. 래핑 multiset에 여러 개의 multiset 요소가 있는 경우(예: `{{1, 2}, {3, 4}}`) 중첩된 multiset 리터럴이 지원되지 않습니다.  
  
## <a name="example"></a>예  
 다음 Entity SQL 쿼리에서는 MULTISET 연산자를 사용하여 값 목록에서 multiset 인스턴스를 만듭니다. 쿼리는 AdventureWorks Sales 모델을 기반으로 합니다. 이 쿼리를 컴파일하고 실행하려면 다음 단계를 수행하세요.  
  
1.  [방법: StructuralType 결과를 반환하는 쿼리 실행](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md)의 절차를 따릅니다.  
  
2.  다음 쿼리를 `ExecuteStructuralTypeQuery` 메서드에 인수로 전달합니다.  
  
 [!code-csharp[DP EntityServices Concepts 2#MULTISET](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#multiset)]  
  
## <a name="see-also"></a>참고 항목  
 [형식 생성](../../../../../../docs/framework/data/adonet/ef/language-reference/constructing-types-entity-sql.md)  
 [엔터티 SQL 참조](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)
