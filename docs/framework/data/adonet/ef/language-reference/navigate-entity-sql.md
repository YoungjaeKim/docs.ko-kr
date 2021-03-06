---
title: NAVIGATE (Entity SQL)
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f107f29d-005f-4e39-a898-17f163abb1d0
caps.latest.revision: "3"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: e6d61e3fb03a1e0ee0cdf344bd61167ad3046a13
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="navigate-entity-sql"></a>NAVIGATE (Entity SQL)
엔터티 사이에 설정된 관계를 탐색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
navigate(instance-expresssion, [relationship-type], [to-end [, from-end] ])  
```  
  
## <a name="arguments"></a>인수  
 `instance-expresssion`  
 엔터티의 인스턴스입니다.  
  
 `relationship-type`  
 CSDL(개념 스키마 정의 언어) 파일에 지정된, 관계의 형식 이름입니다. `relationship-type` 로 한정 됩니다 \<네임 스페이스 >.\< 관계 유형 이름 >.  
  
 `to`  
 관계의 끝 부분입니다.  
  
 `from`  
 관계의 시작 부분입니다.  
  
## <a name="return-value"></a>반환 값  
 끝 End의 카디널리티가 1인 경우 반환 값은 `Ref<T>`이고, 끝 End의 카디널리티가 n인 경우 반환 값은 `Collection<Ref<T>>`입니다.  
  
## <a name="remarks"></a>설명  
 관계는 EDM( [!INCLUDE[adonet_edm](../../../../../../includes/adonet-edm-md.md)] )에서 기본 클래스 구문입니다. 둘 이상의 엔터티 형식 간에 관계를 설정할 수 있으며 사용자는 한쪽(엔터티)에서 다른 쪽으로 관계를 탐색할 수 있습니다. `from` 및 `to` 는 관계 내의 이름 확인에 모호성이 없는 경우에 한해 조건부로 사용 가능합니다.  
  
 NAVIGATE는 O 및 C 공간에서 유효합니다.  
  
 탐색 구문의 일반적인 형태는 다음과 같습니다.  
  
 navigate(`instance-expresssion`, `relationship-type`, [ `to-end` [, `from-end` ] ] )  
  
 예를 들면 다음과 같습니다.  
  
```  
Select o.Id, navigate(o, OrderCustomer, Customer, Order)  
From LOB.Orders as o  
```  
  
 여기서 OrderCustomer는 `relationship`이고, Customer와 Order는 각각 관계의 `to-end` (고객)와 `from-end` (주문)입니다. OrderCustomer가 n:1 관계 경우 탐색 식의 결과 형식이 Ref\<고객 > 합니다.  
  
 이 식이 좀 더 단순화된 형태는 다음과 같습니다.  
  
```  
Select o.Id, navigate(o, OrderCustomer)  
From LOB.Orders as o  
```  
  
 위와 비슷하게 다음 형태의 쿼리에서 탐색 식은 생성 컬렉션 < Ref\<순서 >> 합니다.  
  
```  
Select c.Id, navigate(c, OrderCustomer, Order, Customer)  
From LOB.Customers as c  
```  
  
 인스턴스 식은 엔터티/참조 형식이어야 합니다.  
  
## <a name="example"></a>예  
 다음 Entity SQL 쿼리는 NAVIGATE 연산자를 사용하여 Address 및 SalesOrderHeader 엔터티 형식 사이에 설정된 관계를 탐색합니다. 쿼리는 AdventureWorks Sales 모델을 기반으로 합니다. 이 쿼리를 컴파일하고 실행하려면 다음 단계를 수행하세요.  
  
1.  [How to: Execute a Query that Returns StructuralType Results](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md)의 절차를 따릅니다.  
  
2.  다음 쿼리를 `ExecuteStructuralTypeQuery` 메서드에 인수로 전달합니다.  
  
 [!code-csharp[DP EntityServices Concepts 2#NAVIGATE](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#navigate)]  
  
## <a name="see-also"></a>참고 항목  
 [엔터티 SQL 참조](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)  
 [방법: 탐색와 관계 탐색 연산자](../../../../../../docs/framework/data/adonet/ef/language-reference/navigate-entity-sql.md)
