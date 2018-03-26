---
title: 공용 스키마 컬렉션
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-ado
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 50127ced-2ac8-4d7a-9cd1-5c98c655ff03
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload:
- dotnet
ms.openlocfilehash: 893093900b3fc4276f9bd7143b1f235a5ba98f90
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="common-schema-collections"></a>공용 스키마 컬렉션
공통 스키마 컬렉션은 각 .NET Framework 관리 공급자를 통해 구현되는 스키마 컬렉션입니다. 호출 하 여 지원 되는 스키마 컬렉션의 목록을 확인 하려면.NET Framework 관리 공급자를 쿼리할 수 있습니다는 **GetSchema** 메서드를 인수 없이, 또는 "metadatacollections 라는" 스키마 컬렉션 이름을 사용 합니다. 그러면 지원되는 스키마 컬렉션의 목록, 각자 지원하는 제약 조건 수 및 사용하는 식별자 부분 수가 포함된 <xref:System.Data.DataTable>이 반환됩니다. 이 컬렉션은 필요한 모든 열을 설명합니다. 공급자는 필요에 따라 열을 추가할 수 있습니다. 예를 들어, `SqlClient` 및 `OracleClient`는 ParameterName 을 Restrictions 컬렉션에 추가합니다.  
  
 공급자는 필수 열의 값을 판단할 수 없는 경우 null을 반환합니다.  
  
 사용 하는 방법에 대 한 자세한 내용은 **GetSchema** 메서드 참조 [GetSchema 및 Schema 컬렉션](../../../../docs/framework/data/adonet/getschema-and-schema-collections.md)합니다.  
  
## <a name="metadatacollections"></a>MetaDataCollections  
 이 스키마 컬렉션에서는 데이터베이스에 연결하기 위해 현재 사용되는 .NET Framework 관리 공급자에서 지원되는 모든 스키마 컬렉션에 대한 정보를 노출합니다.  
  
|열 이름|데이터 형식|설명|  
|----------------|--------------|-----------------|  
|CollectionName|string|에 전달할 컬렉션의 이름에서 **GetSchema** 메서드 컬렉션을 반환 합니다.|  
|NumberOfRestrictions|int|컬렉션에 지정할 수 있는 제한의 수입니다.|  
|NumberOfIdentifierParts|int|복합 식별자/데이터베이스 개체 이름의 부분 개수. 예를 들어, SQL Server에서는 테이블에 대한 부분이 3개이고 열에 대한 4개입니다. Oracle에서는 테이블에 대한 부분이 2개이고 열에 대한 부분이 3개입니다.|  
  
## <a name="datasourceinformation"></a>DataSourceInformation  
 이 스키마 컬렉션에서는 .NET Framework 관리 공급자가 현재 연결되어 있는 데이터 소스에 대한 정보를 노출합니다.  
  
|열 이름|데이터 형식|설명|  
|----------------|--------------|-----------------|  
|CompositeIdentifierSeparatorPattern|string|복합 식별자의 복합 구분 기호와 일치하는 정규식입니다. 예를 들어 "\\." (SQL Server 용) 또는 "@&#124;\\." (Oracle의 경우)입니다.<br /><br /> 복합 식별자는 일반적으로 용도 데이터베이스 개체 이름에 대 한 예를 들어:, pubs.dbo.authors 또는 pubs@dbo.authors합니다.<br /><br /> SQL Server에 대 한 정규식을 사용 하 여 "\\."입니다. Oracleclient를 사용 하 여 "@&#124;\\."입니다.<br /><br /> ODBC의 경우 Catalog_name_seperator를 사용합니다.<br /><br /> OLE DB의 경우 DBLITERAL_CATALOG_SEPARATOR 또는 DBLITERAL_SCHEMA_SEPARATOR를 사용합니다.|  
|DataSourceProductName|string|"Oracle" 또는 "SQLServer"와 같은 공급자에서 액세스하는 제품의 이름입니다.|  
|DataSourceProductVersion|string|공급자에서 액세스하는 제품의 버전을 Microsoft 형식이 아닌 데이터 소스 기본 형식으로 나타냅니다.<br /><br /> 경우에 따라 DataSourceProductVersion과 DataSourceProductVersionNormalized는 동일한 값입니다. OLE DB 및 ODBC의 경우 이 값은 항상 기본 API에서 동일한 함수 호출로 매핑될 때와 같습니다.|  
|DataSourceProductVersionNormalized|string|`String.Compare()`와 비교할 수 있는 데이터 소스의 표준화된 버전. 이 형식은 버전 10이 버전 1과 버전 2 사이에 정렬되지 않도록 공급자의 모든 버전에서 일관성이 유지됩니다.<br /><br /> 예를 들어 Oracle 공급자는 Oracle 8i 데이터 소스 "08.01.07.04.01"을 반환 하 게 하는 정규화 된 버전에 대 한 "nn.nn.nn.nn.nn"의 형식을 사용 합니다. SQL Server는 일반적인 Microsoft "nn.nn.nnnn" 형식을 사용 합니다.<br /><br /> 경우에 따라 DataSourceProductVersion과 DataSourceProductVersionNormalized는 동일한 값입니다. OLE DB 및 ODBC의 경우 이 값은 항상 기본 API에서 동일한 함수 호출로 매핑될 때와 같습니다.|  
|GroupByBehavior|<xref:System.Data.Common.GroupByBehavior>|GROUP BY 절의 열과 선택 목록의 집계되지 않은 열 간의 관계를 지정합니다.|  
|IdentifierPattern|string|식별자와 일치하고 일치하는 식별자 값이 있는 정규식입니다. 예를 들어, &quot;[A-Za-z0-9_#$]&quot;입니다.|  
|IdentifierCase|<xref:System.Data.Common.IdentifierCase>|따옴표로 묶지 않은 식별자의 대/소문자 구분 여부를 나타냅니다.|  
|OrderByColumnsInSelect|bool|ORDER BY 절의 열이 선택 목록에 들어 있어야 하는지 여부를 지정합니다. true 값은 선택 목록에 있어야 함을 나타내며 false 값은 선택 목록에 있을 필요가 없음을 나타냅니다.|  
|ParameterMarkerFormat|string|매개 변수 형식을 지정하는 방법을 나타내는 형식 문자열입니다.<br /><br /> 명명된 매개 변수를 데이터 소스에서 지원하는 경우 매개 변수 이름의 형식이 지정되어야 하는 위치가 이 문자열의 첫 번째 자리 표시자여야 합니다.<br /><br /> 예를 들어, 데이터 소스에 ':' 접두사가 붙은 명명된 매개 변수가 필요한 경우에는 “:{0}”입니다. 이 문자열을 “p1”이라는 매개 변수 이름으로 형식을 지정하는 경우 결과 문자열은 “:p1”입니다.<br /><br /> 데이터 소스 매개 변수 접두사가 필요로 하는 경우는 ' @', 것 ' {'이 (0)와 매개 변수를 지정 합니다. 결과를 라는 이름이 이미 들어 있지만 "@p1"정규식은 단순히"@p1"입니다.<br /><br /> 명명 된 매개 변수가 필요 하지 않으며 사용 하는 데이터 원본에는 '?' 형식 문자열을 간단 하 게 지정할 수 있습니다. 문자 '?', 매개 변수 이름은 무시 됩니다. OLE DB의 경우에는 ‘?’가 반환됩니다.|  
|ParameterMarkerPattern|string|매개 변수 표식과 일치하는 정규식입니다. 매개 변수 이름이 있는 경우 일치하는 매개 변수 이름 값을 가집니다.<br /><br /> 예를 들어, 매개 변수 이름에 포함될 ‘@’ 선행 문자와 함께 명명된 매개 변수를 지원하는 경우 정규식은 “(@[A-Za-z0-9_$#]*)”입니다.<br /><br /> 그러나 명명 된 매개 변수를 지원 되는 경우는 ':' 일은 문자가 매개 변수 이름의 일부가 아니므로,: ": ([z0-9_$ #]\*)"입니다.<br /><br /> 물론 데이터 소스에서 명명된 매개 변수를 지원하는 경우 정규식은 단순히 &quot;?&quot;입니다.|  
|ParameterNameMaxLength|int|매개 변수 이름의 최대 길이(문자 수)입니다. Visual Studio에서는 매개 변수 이름이 지원되는 경우 최대 길이에 대한 최소 값을 30자로 간주합니다.<br /><br /> 데이터 소스에서 명명된 매개 변수를 지원하지 않는 경우 이 속성은 0을 반환합니다.|  
|ParameterNamePattern|string|유효 매개 변수 이름과 일치하는 정규식입니다. 매개 변수 이름에 사용할 수 있는 문자에 관한 규칙은 데이터 소스마다 다릅니다.<br /><br /> Visual Studio에서는 매개 변수 이름이 지원되는 경우 문자 "\p{Lu}\p{Ll}\p{Lt}\p{Lm}\p{Lo}\p{Nl}\p{Nd}"를 매개 변수 이름에 사용할 수 있는 최소 지원 문자 집합으로 간주합니다.|  
|QuotedIdentifierPattern|string|따옴표로 묶은 식별자와 일치하고 따옴표를 제외한 일치하는 식별자 값이 있는 정규식입니다. 예를 들어 큰따옴표로 따옴표 붙은 식별자를 식별 하는 데 사용 하는 데이터 원본,이 됩니다: "(([^\\"]&#124;\\"\\") *) "입니다.|  
|QuotedIdentifierCase|<xref:System.Data.Common.IdentifierCase>|따옴표로 묶은 식별자의 대/소문자 구분 여부를 나타냅니다.|  
|StatementSeparatorPattern|string|문 구분 기호와 일치하는 정규식입니다.|  
|StringLiteralPattern|string|문자 리터럴과 일치하고 일치하는 리터럴 값이 있는 정규식입니다. 예를 들어, 작은 따옴표 문자열을 식별 하는 데 사용 하는 데이터 원본,이 됩니다: "('([^']&#124;'') *')"'|  
|SupportedJoinOperators|<xref:System.Data.Common.SupportedJoinOperators>|데이터 소스에서 지원하는 SQL 조인 문의 형식을 지정합니다.|  
  
## <a name="datatypes"></a>DataTypes  
 이 스키마 컬렉션에서는 .NET Framework 관리 공급자가 현재 연결되어 있는 데이터베이스에서 지원하는 데이터 형식에 대한 정보를 노출합니다.  
  
|열 이름|데이터 형식|설명|  
|----------------|--------------|-----------------|  
|TypeName|string|공급자별 데이터 형식 이름입니다.|  
|ProviderDbType|int|매개 변수 형식을 지정할 때 사용해야 하는 공급자별 형식 값입니다. 예를 들어, SqlDbType.Money 또는 OracleType.Blob입니다.|  
|ColumnSize|long|숫자가 아닌 열 또는 매개 변수의 길이는 공급자에서 이 형식에 대해 정의된 길이 또는 최대값을 나타냅니다.<br /><br /> 문자 데이터의 경우 이 값은 데이터 소스에 정의한 최대값 또는 정의된 길이(단위)입니다. Oracle에는 일부 문자 데이터 형식에 대해 길이를 지정하고 나서 실제 저장소 크기를 지정하는 개념이 있습니다. 이 개념에서는 Oracle의 단위 길이만을 정의합니다.<br /><br /> 날짜/시간 데이터 형식의 경우, 최대값에서 소수로 나타낸 시간(초)의 정밀도를 허용한다고 가정할 때 문자열 표시의 길이입니다.<br /><br /> 데이터 형식이 숫자이면 이 값은 데이터 형식의 최대 정밀도에 대한 상한 값입니다.|  
|CreateFormat|string|이 열을 CREATE TABLE과 같은 데이터 정의 문에 추가하는 방법을 나타내는 형식 문자열입니다. CreateParameter 배열의 각 요소는 형식 문자열에 “매개 변수 표식”으로 나타나야 합니다.<br /><br /> 예를 들어, SQL 데이터 형식 DECIMAL에는 정밀도와 배율이 필요합니다. 이 경우, 형식 문자열은 “DECIMAL({0},{1})”입니다.|  
|CreateParameters|string|이 데이터 형식의 열을 만들 때 지정해야 하는 생성 매개 변수입니다. 각 생성 매개 변수는 문자열로 나열되며 제공되는 순서대로 쉼표로 구분됩니다.<br /><br /> 예를 들어, SQL 데이터 형식 DECIMAL에는 정밀도와 배율이 필요합니다. 이 경우, 생성 매개 변수에는 &quot;정밀도, 배율&quot; 문자열이 포함되어야 합니다.<br /><br /> 정밀도 10과 배율 2를 사용하여 DECIMAL 열을 만들기 위한 텍스트 명령에서 CreateFormat의 값은 DECIMAL({0},{1})”이며 전체 형식 사양은 DECIMAL(10,2)입니다.|  
|데이터 형식|string|.NET Framework 형식의 데이터 형식 이름입니다.|  
|IsAutoincrementable|bool|true - 이 데이터 형식의 값이 자동 증분됩니다.<br /><br /> false - 이 데이터 형식의 값이 자동 증분되지 않습니다.<br /><br /> 이 값은 이 데이터 형식 열의 자동 증분 여부를 나타낼 뿐, 이 형식의 모든 열이 자동 증분되도록 지정하지는 않습니다.|  
|IsBestMatch|bool|true - 데이터 형식이 데이터 저장소의 모든 데이터 형식과 DataType 열의 값으로 나타낸 .NET Framework 데이터 형식 사이에서 정확히 일치합니다.<br /><br /> false - 데이터 형식이 정확히 일치하지 않습니다.<br /><br /> DataType 열의 값이 동일한 각 행 집합의 경우, IsBestMatch 열은 하나의 행에서만 true로 설정됩니다.|  
|IsCaseSensitive|bool|true - 데이터 형식이 문자 형식이며 대/소문자를 구분합니다.<br /><br /> false - 데이터 형식이 문자 형식이 아니거나 대/소문자를 구분하지 않습니다.|  
|IsFixedLength|bool|true - DDL(데이터 정의 언어)에서 만든 이 데이터 형식의 열 길이가 고정 길이입니다.<br /><br /> false - DDL에서 만든 이 데이터 형식의 열 길이가 가변 길이입니다.<br /><br /> DBNull.Value - 공급자가 이 필드를 고정 길이 열에 매핑할지 아니면 가변 길이 열에 매핑할지를 알 수 없습니다.|  
|IsFixedPrecisionScale|bool|true - 데이터 형식의 정밀도와 배율이 고정되어 있습니다.<br /><br /> false - 데이터 형식의 정밀도와 배율이 고정되어 있지 않습니다.|  
|IsLong|bool|true - 데이터 형식에 매우 긴 데이터가 포함되며, 매우 긴 데이터의 정의는 공급자별로 다릅니다.<br /><br /> false - 데이터 형식에 매우 긴 데이터가 포함되지 않습니다.|  
|IsNullable|bool|true - Null 허용 데이터 형식입니다.<br /><br /> false - Null 허용 데이터 형식이 아닙니다.<br /><br /> DBNull.Value - 데이터 형식이 Null 허용인지 여부를 알 수 없습니다.|  
|IsSearchable|bool|true - LIKE 조건부를 제외한 모든 연산자와 함께 데이터 형식을 WHERE 절에서 사용할 수 있습니다.<br /><br /> false - LIKE 조건부를 제외한 모든 연산자와 함께 데이터 형식을 WHERE 절에서 사용할 수 없습니다.|  
|IsSearchableWithLike|bool|true - LIKE 조건부와 함께 데이터 형식을 사용할 수 있습니다.<br /><br /> false - LIKE 조건부와 함께 데이터 형식을 사용할 수 없습니다.|  
|IsUnsigned|bool|true - 부호 없는 데이터 형식입니다.<br /><br /> false - 부호 있는 데이터 형식입니다.<br /><br /> DBNull.Value - 데이터 형식에 해당되지 않습니다.|  
|MaximumScale|short|형식 표시기가 숫자 형식인 경우 소수점 오른쪽에 허용되는 최대 자리수입니다. 그렇지 않으면 DBNull.Value입니다.|  
|MinimumScale|short|형식 표시기가 숫자 형식인 경우 소수점 오른쪽에 허용되는 최소 자리수입니다. 그렇지 않으면 DBNull.Value입니다.|  
|IsConcurrencyType|bool|true - 행이 변경될 때마다 데이터베이스에서 데이터 형식을 업데이트하며 열의 값이 모든 이전 값과 다릅니다.<br /><br /> false - 행이 변경될 때마다 데이터베이스에서 데이터 형식을 업데이트하지 않습니다.<br /><br /> DBNull.Value - 데이터베이스에서 이 데이터 형식을 지원하지 않습니다.|  
|IsLiteralSupported|bool|true - 데이터 형식을 리터럴로 표현할 수 있습니다.<br /><br /> false - 데이터 형식을 리터럴로 표현할 수 없습니다.|  
|LiteralPrefix|string|지정한 리터럴에 적용된 접두사입니다.|  
|LiteralSuffix|string|지정한 리터럴에 적용된 접미사입니다.|  
|NativeDataType|문자열|NativeDataType은 OLE DB 형식의 데이터 형식을 노출시키기 위한 OLE DB 특정 열입니다.|  
  
## <a name="restrictions"></a>제한  
 이 스키마 컬렉션에서는 데이터베이스에 연결하기 위해 현재 사용되는 .NET Framework 관리 공급자에서 지원하는 제한에 대한 정보를 노출시킵니다.  
  
|열 이름|데이터 형식|설명|  
|----------------|--------------|-----------------|  
|CollectionName|string|이러한 제한이 적용되는 컬렉션의 이름입니다.|  
|RestrictionName|string|컬렉션에서 제한의 이름입니다.|  
|RestrictionDefault|string|무시됩니다.|  
|RestrictionNumber|int|특정 제한이 속한 Restrictions 컬렉션의 실제 위치입니다.|  
  
## <a name="reservedwords"></a>ReservedWords  
 이 스키마 컬렉션에서는 .NET Framework 관리 공급자가 현재 연결되어 있는 데이터베이스에서 예약된 단어에 대한 정보를 노출합니다.  
  
|열 이름|데이터 형식|설명|  
|----------------|--------------|-----------------|  
|ReservedWord|string|공급자 관련 예약어입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 스키마 정보 검색](../../../../docs/framework/data/adonet/retrieving-database-schema-information.md)  
 [GetSchema 및 Schema 컬렉션](../../../../docs/framework/data/adonet/getschema-and-schema-collections.md)  
 [ADO.NET 관리되는 공급자 및 데이터 집합 개발자 센터](http://go.microsoft.com/fwlink/?LinkId=217917)
