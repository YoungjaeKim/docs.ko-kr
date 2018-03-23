---
title: 엔터티 SQL 참조
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-ado
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 61ce7ee1-ffe2-477d-8a9f-835b0a11d900
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload:
- dotnet
ms.openlocfilehash: ac05ec8a8732da383a4e33e84c669aa29660a0da
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/23/2018
---
# <a name="entity-sql-reference"></a>엔터티 SQL 참조
이 단원에는 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 참조 항목이 포함되어 있습니다. 이 항목에는 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 작업이 요약되고 범주별로 그룹화되어 있습니다.  
  
## <a name="arithmetic-operators"></a>산술 연산자  
 산술 연산자는 하나 이상의 숫자 데이터 형식으로 구성된 두 식에 대해 수치 연산을 수행합니다. 다음 표에서는 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 산술 연산자를 보여 줍니다.  
  
|연산자|사용|  
|--------------|---------|  
|[+(더하기)](../../../../../../docs/framework/data/adonet/ef/language-reference/add.md)|더하기|  
|"/ (나누기)"|나누기|  
|[% (모듈로)](../../../../../../docs/framework/data/adonet/ef/language-reference/modulo-entity-sql.md)|나누기의 나머지를 반환합니다.|  
|[*(곱하기)](../../../../../../docs/framework/data/adonet/ef/language-reference/multiply-entity-sql.md)|곱하기|  
|[-(음수)](../../../../../../docs/framework/data/adonet/ef/language-reference/negative-entity-sql.md)|부정|  
|[-(빼기)](../../../../../../docs/framework/data/adonet/ef/language-reference/subtract-entity-sql.md)|빼기|  
  
## <a name="canonical-functions"></a>정식 함수  
 정식 함수는 모든 데이터 공급자에서 지원되며 모든 쿼리 기술에 사용될 수 있습니다. 다음 표에서는 정식 함수를 보여 줍니다.  
  
|함수|형식|  
|--------------|----------|  
|[집계 Entity SQL 정식 함수](../../../../../../docs/framework/data/adonet/ef/language-reference/aggregate-canonical-functions.md)|집계 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 정식 함수에 대해 설명합니다.|  
|[수학 정식 함수](../../../../../../docs/framework/data/adonet/ef/language-reference/math-canonical-functions.md)|수식 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 정식 함수에 대해 설명합니다.|  
|[문자열 정식 함수](../../../../../../docs/framework/data/adonet/ef/language-reference/string-canonical-functions.md)|문자열 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 정식 함수에 대해 설명합니다.|  
|[날짜 및 시간 정식 함수](../../../../../../docs/framework/data/adonet/ef/language-reference/date-and-time-canonical-functions.md)|날짜 및 시간 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 정식 함수에 대해 설명합니다.|  
|[비트 정식 함수](../../../../../../docs/framework/data/adonet/ef/language-reference/bitwise-canonical-functions.md)|비트 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 정식 함수에 대해 설명합니다.|  
|[기타 정식 함수](../../../../../../docs/framework/data/adonet/ef/language-reference/other-canonical-functions.md)|비트, 날짜/시간, 문자열, 수식, 집계 등으로 분류되지 않는 함수에 대해 설명합니다.|  
  
## <a name="comparison-operators"></a>비교 연산자  
 비교 연산자는 `Byte`, `Int16`, `Int32`, `Int64`, `Double`, `Single`, `Decimal`, `String`, `DateTime`, `Date`, `Time`, `DateTimeOffset` 형식에 대해 정의됩니다. 비교 연산자를 적용하기 전에 피연산자에 대해 암시적 형식 승격이 발생합니다. 비교 연산자는 항상 부울 값을 생성합니다. 피연산자 중 하나 이상이 `null`이면 결과는 `null`입니다.  
  
 `Boolean` 형식과 같이 ID를 가진 모든 개체 형식에 대해 같음 및 다름이 정의됩니다. ID를 가진 기본 개체가 아닌 개체가 같은 ID를 공유할 경우 서로 같다고 간주됩니다. 다음 표에는 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 비교 연산자가 나와 있습니다.  
  
|연산자|설명|  
|--------------|-----------------|  
|[=(같음)](../../../../../../docs/framework/data/adonet/ef/language-reference/equals-entity-sql.md)|두 식이 같은지 비교합니다.|  
|[>(보다 큼)](../../../../../../docs/framework/data/adonet/ef/language-reference/greater-than-entity-sql.md)|두 식을 비교하여 왼쪽 식의 값이 오른쪽 식의 값보다 큰지 여부를 결정합니다.|  
|[>=(크거나 같음)](../../../../../../docs/framework/data/adonet/ef/language-reference/greater-than-or-equal-to-entity-sql.md)|두 식을 비교하여 왼쪽 식의 값이 오른쪽 식의 값보다 크거나 같은지 여부를 결정합니다.|  
|[&AMP;#91;하지&AMP;#93; NULL](../../../../../../docs/framework/data/adonet/ef/language-reference/isnull-entity-sql.md)|쿼리 식이 null인지 여부를 결정합니다.|  
|[<(보다 작음)](../../../../../../docs/framework/data/adonet/ef/language-reference/less-than-entity-sql.md)|두 식을 비교하여 왼쪽 식의 값이 오른쪽 식의 값보다 작은지 여부를 결정합니다.|  
|[<=(작거나 같음)](../../../../../../docs/framework/data/adonet/ef/language-reference/less-than-or-equal-to-entity-sql.md)|두 식을 비교하여 왼쪽 식의 값이 오른쪽 식의 값보다 작거나 같은지 여부를 결정합니다.|  
|[&#91;NOT&#93; BETWEEN](../../../../../../docs/framework/data/adonet/ef/language-reference/between-entity-sql.md)|식의 결과 값이 지정된 범위에 속하는지 여부를 결정합니다.|  
|[!=(같지 않음)](../../../../../../docs/framework/data/adonet/ef/language-reference/not-equal-to-entity-sql.md)|두 식을 비교하여 왼쪽 식의 값이 오른쪽 식의 값과 다른지 여부를 결정합니다.|  
|[&#91;NOT&#93; LIKE](../../../../../../docs/framework/data/adonet/ef/language-reference/like-entity-sql.md)|특정 문자열이 지정된 패턴과 일치하는지 여부를 결정합니다.|  
  
## <a name="logical-and-case-expression-operators"></a>논리 및 Case 식 연산자  
 논리 연산자는 조건의 진위 여부를 테스트합니다. CASE 식은 부울 식 집합을 계산하여 결과를 결정합니다. 다음 표에서는 논리 및 CASE 식 연산자를 보여 줍니다.  
  
|연산자|설명|  
|--------------|-----------------|  
|[& & (논리적 AND)](../../../../../../docs/framework/data/adonet/ef/language-reference/and-entity-sql.md)|논리적 AND|  
|[! (논리적 NOT)](../../../../../../docs/framework/data/adonet/ef/language-reference/not-entity-sql.md)|논리적 NOT|  
|[&#124;&#124;(논리적 OR)](../../../../../../docs/framework/data/adonet/ef/language-reference/or-entity-sql.md)|논리적 OR|  
|[CASE](../../../../../../docs/framework/data/adonet/ef/language-reference/case-entity-sql.md)|부울 식 집합을 계산하여 결과를 확인합니다.|  
|[THEN](../../../../../../docs/framework/data/adonet/ef/language-reference/then-entity-sql.md)|결과 [때](http://msdn.microsoft.com/library/6233fe9f-00b0-460e-8372-64e138a5f998) true로 평가 될 때 절.|  
  
## <a name="query-operators"></a>쿼리 연산자  
 쿼리 연산자는 엔터티 데이터를 반환하는 쿼리 식을 정의하는 데 사용됩니다. 다음 표에서는 쿼리 연산자를 보여 줍니다.  
  
|연산자|사용|  
|--------------|---------|  
|[FROM](../../../../../../docs/framework/data/adonet/ef/language-reference/from-entity-sql.md)|사용 되는 컬렉션을 지정 [선택](../../../../../../docs/framework/data/adonet/ef/language-reference/select-entity-sql.md) 문.|  
|[GROUP BY](../../../../../../docs/framework/data/adonet/ef/language-reference/group-by-entity-sql.md)|쿼리에 의해 반환 된 개체를 그룹 지정 ([선택](../../../../../../docs/framework/data/adonet/ef/language-reference/select-entity-sql.md)) 배치 하는 식입니다.|  
|[GroupPartition](../../../../../../docs/framework/data/adonet/ef/language-reference/grouppartition-entity-sql.md)|집계가 관련되는 그룹 파티션에서 예측된 인수 값의 컬렉션을 반환합니다.|  
|[HAVING](../../../../../../docs/framework/data/adonet/ef/language-reference/having-entity-sql.md)|그룹이나 집계에 대한 검색 조건을 지정합니다.|  
|[LIMIT](../../../../../../docs/framework/data/adonet/ef/language-reference/limit-entity-sql.md)|함께 사용 된 [ORDER BY](../../../../../../docs/framework/data/adonet/ef/language-reference/order-by-entity-sql.md) 수행된 된 물리적 페이징 절.|  
|[ORDER BY](../../../../../../docs/framework/data/adonet/ef/language-reference/order-by-entity-sql.md)|반환 되는 개체에 사용 되는 정렬 순서를 지정 된 [선택](../../../../../../docs/framework/data/adonet/ef/language-reference/select-entity-sql.md) 문.|  
|[SELECT](../../../../../../docs/framework/data/adonet/ef/language-reference/select-entity-sql.md)|쿼리 결과로 반환되는 프로젝션의 요소를 지정합니다.|  
|[SKIP](../../../../../../docs/framework/data/adonet/ef/language-reference/skip-entity-sql.md)|함께 사용 된 [ORDER BY](../../../../../../docs/framework/data/adonet/ef/language-reference/order-by-entity-sql.md) 수행된 된 물리적 페이징 절.|  
|[TOP](../../../../../../docs/framework/data/adonet/ef/language-reference/top-entity-sql.md)|쿼리 결과에서 첫 번째 행 집합만 반환됨을 지정합니다.|  
|[WHERE](../../../../../../docs/framework/data/adonet/ef/language-reference/where-entity-sql.md)|쿼리에서 반환된 데이터를 조건에 따라 필터링합니다.|  
  
## <a name="reference-operators"></a>참조 연산자  
 참조는 특정 엔터티 집합 내의 특정 엔터티를 가리키는 논리 포인터(외래 키)입니다. [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 다음 연산자를 생성, 해체 및 참조를 통해 탐색을 지원 합니다.  
  
|연산자|사용|  
|--------------|---------|  
|[CREATEREF](../../../../../../docs/framework/data/adonet/ef/language-reference/createref-entity-sql.md)|엔터티 집합의 엔터티에 대한 참조를 만듭니다.|  
|[DEREF](../../../../../../docs/framework/data/adonet/ef/language-reference/deref-entity-sql.md)|참조 값을 역참조하고 이 역참조의 결과를 생성합니다.|  
|[KEY](../../../../../../docs/framework/data/adonet/ef/language-reference/key-entity-sql.md)|참조 또는 엔터티 식의 키를 추출합니다.|  
|[NAVIGATE](../../../../../../docs/framework/data/adonet/ef/language-reference/navigate-entity-sql.md)|엔터티 형식 간의 관계를 탐색할 수 있습니다.|  
|[REF](../../../../../../docs/framework/data/adonet/ef/language-reference/ref-entity-sql.md)|엔터티 인스턴스에 대한 참조를 반환합니다.|  
  
## <a name="set-operators"></a>집합 연산자  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 여러 가지 강력한 집합 연산을 제공합니다. 집합 연산자 UNION, INTERSECT, EXCEPT, 같은 TRANSACT-SQL 연산자와 유사한 것 여기에 및 EXISTS입니다. [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 중복 항목 제거(SET), 멤버 자격 테스트(IN), 조인(JOIN) 등을 위한 연산자도 지원합니다. 다음 표에서는 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 집합 연산자를 보여 줍니다.  
  
|연산자|사용|  
|--------------|---------|  
|[ANYELEMENT](../../../../../../docs/framework/data/adonet/ef/language-reference/anyelement-entity-sql.md)|다중값 컬렉션에서 요소를 추출합니다.|  
|[EXCEPT](../../../../../../docs/framework/data/adonet/ef/language-reference/except-entity-sql.md)|EXCEPT 피연산자 오른쪽 쿼리 식에서 반환되지 않은 모든 고유한 값 컬렉션을 EXCEPT 피연산자 왼쪽에 있는 쿼리 식에서 반환합니다.|  
|[&#91;NOT&#93; EXISTS](../../../../../../docs/framework/data/adonet/ef/language-reference/exists-entity-sql.md)|컬렉션이 비어 있는지 확인합니다.|  
|[FLATTEN](../../../../../../docs/framework/data/adonet/ef/language-reference/flatten-entity-sql.md)|여러 컬렉션의 컬렉션을 하나의 결합된 컬렉션으로 변환합니다.|  
|[&AMP;#91;하지&AMP;#93; IN](../../../../../../docs/framework/data/adonet/ef/language-reference/in-entity-sql.md)|컬렉션에 일치하는 값이 있는지 여부를 확인합니다.|  
|[INTERSECT](../../../../../../docs/framework/data/adonet/ef/language-reference/intersect-entity-sql.md)|INTERSECT 피연산자의 왼쪽과 오른쪽에 있는 두 쿼리 식에서 반환된 고유한 값의 컬렉션을 반환합니다.|  
|[OVERLAPS](../../../../../../docs/framework/data/adonet/ef/language-reference/overlaps-entity-sql.md)|두 컬렉션에 공통 요소가 있는지 여부를 확인합니다.|  
|[SET](../../../../../../docs/framework/data/adonet/ef/language-reference/set-entity-sql.md)|중복 요소가 모두 제거된 새 컬렉션을 생성하여 개체 컬렉션을 집합으로 변환하는 데 사용됩니다.|  
|[UNION](../../../../../../docs/framework/data/adonet/ef/language-reference/union-entity-sql.md)|두 개 이상의 쿼리 결과를 단일 컬렉션으로 결합합니다.|  
  
## <a name="type-operators"></a>형식 연산자  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 생성, 쿼리 및 조작 하는 식 (값)의 형식을 허용 하는 작업을 제공 합니다. 다음 표에서는 형식에 사용되는 연산자를 보여 줍니다.  
  
|연산자|사용|  
|--------------|---------|  
|[CAST](../../../../../../docs/framework/data/adonet/ef/language-reference/cast-entity-sql.md)|데이터 형식의 식을 다른 형식의 식으로 변환합니다.|  
|[COLLECTION](../../../../../../docs/framework/data/adonet/ef/language-reference/collection-entity-sql.md)|에 사용 되는 [함수](../../../../../../docs/framework/data/adonet/ef/language-reference/function-entity-sql.md) 작업의 엔터티 형식 또는 복합 형식의 컬렉션을 선언 합니다.|  
|[&AMP;#91;하지&AMP;#93; OF](../../../../../../docs/framework/data/adonet/ef/language-reference/isof-entity-sql.md)|식의 형식이 지정된 형식 또는 그 하위 형식인지 여부를 확인합니다.|  
|[OFTYPE](../../../../../../docs/framework/data/adonet/ef/language-reference/oftype-entity-sql.md)|쿼리 식에서 특정 형식을 가진 개체 컬렉션을 반환합니다.|  
|[명명된 형식 생성자](../../../../../../docs/framework/data/adonet/ef/language-reference/named-type-constructor-entity-sql.md)|엔터티 형식이나 복합 형식의 인스턴스를 만드는 데 사용됩니다.|  
|[MULTISET](../../../../../../docs/framework/data/adonet/ef/language-reference/multiset-entity-sql.md)|값 목록에서 multiset 인스턴스를 만듭니다.|  
|[ROW](../../../../../../docs/framework/data/adonet/ef/language-reference/row-entity-sql.md)|값 하나 이상을 기반으로 하여 구조적으로 형식화된 익명 레코드를 생성합니다.|  
|[TREAT](../../../../../../docs/framework/data/adonet/ef/language-reference/treat-entity-sql.md)|특정 기본 형식의 개체를 지정된 파생 형식의 개체로 처리합니다.|  
  
## <a name="other-operators"></a>기타 연산자  
 다음 표에서 다른 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 연산자입니다.  
  
|연산자|사용|  
|--------------|---------|  
|[+(문자열 연결)](../../../../../../docs/framework/data/adonet/ef/language-reference/string-concatenation-entity-sql.md)|[!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서 문자열을 연결하는 데 사용됩니다.|  
|[. (멤버 액세스)](../../../../../../docs/framework/data/adonet/ef/language-reference/member-access-entity-sql.md)|구조 개념적 모델 형식 인스턴스의 속성 또는 필드 값에 액세스하는 데 사용됩니다.|  
|[--(설명)](../../../../../../docs/framework/data/adonet/ef/language-reference/comment-entity-sql.md)|[!INCLUDE[esql](../../../../../../includes/esql-md.md)] 주석을 포함합니다.|  
|[FUNCTION](../../../../../../docs/framework/data/adonet/ef/language-reference/function-entity-sql.md)|Entity SQL 쿼리에서 실행할 수 있는 인라인 함수를 정의합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Entity SQL 언어](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-language.md)
