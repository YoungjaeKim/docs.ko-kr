---
title: 형식화된 데이터 집합에 주석 지정
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-ado
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- csharp
- vb
ms.assetid: f82aaa62-321e-4c8a-b51b-9d1114700170
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload:
- dotnet
ms.openlocfilehash: cc09f3f9b43b70b7f9b302d7a9d75428b5a0e6c7
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="annotating-typed-datasets"></a>형식화된 데이터 집합에 주석 지정
주석을 사용하면 원본으로 사용하는 스키마를 수정하지 않고 형식화된 <xref:System.Data.DataSet>의 요소 이름을 수정할 수 있습니다. 기본 스키마에서 요소의 이름 수정로 인해 형식화 된 **데이터 집합** 않는 하지 데이터 원본에 없는 뿐만 아니라 데이터 원본에 없는 개체에 대 한 참조를 손실 되는 개체를 참조 하도록 합니다.  
  
 주석을 사용 하면 사용자 지정할 수 있습니다 개체의 이름을 입력 한 **DataSet** 더 의미 있는 이름으로 만드는 코드의 가독성 및 형식화 된 **DataSet** 그대로 유지 하면서 사용 하도록 클라이언트에 대 한 보다 쉽게 기본 스키마를 그대로 유지 합니다. 에 대 한 다음 스키마 요소 예를 들어는 **고객** 목차는 **Northwind** 데이터베이스는 **DataRow** 의 개체 이름  **CustomersRow** 및 <xref:System.Data.DataRowCollection> 라는 **고객**합니다.  
  
```xml  
<xs:element name="Customers">  
  <xs:complexType>  
    <xs:sequence>  
      <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
    </xs:sequence>  
  </xs:complexType>  
</xs:element>  
```  
  
 A **DataRowCollection** 이름 **고객** 클라이언트 코드에서 적절 한 의미 하지만 **DataRow** 이름 **CustomersRow** 잘못 된 것입니다 단일 개체 이므로 또한, 공통 시나리오 개체 참조 하지 않고는 **행** 식별자 대신는 단순히로 간주 하 고는 **고객** 개체입니다. 솔루션에 대 한 새 이름을 식별 하는 스키마에 주석을 추가 하는 것은 **DataRow** 및 **DataRowCollection** 개체입니다. 다음 코드는 이전 스키마에 주석을 단 것입니다.  
  
```xml  
<xs:element name="Customers" codegen:typedName="Customer" codegen:typedPlural="Customers">  
  <xs:complexType>  
    <xs:sequence>  
      <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
    </xs:sequence>  
  </xs:complexType>  
</xs:element>  
```  
  
 지정 하는 **typedName** 값 **고객** 됩니다는 **DataRow** 의 개체 이름 **고객**합니다. 지정 하는 **typedPlural** 값 **고객** 유지는 **DataRowCollection** 이름 **고객**합니다.  
  
 다음 표에서는 사용할 수 있는 주석을 보여 줍니다.  
  
|주석|설명|  
|----------------|-----------------|  
|**typedName**|개체의 이름입니다.|  
|**typedPlural**|개체 컬렉션의 이름입니다.|  
|**typedParent**|부모 관계에서 참조될 때의 개체 이름입니다.|  
|**typedChildren**|자식 관계에서 개체를 반환하기 위한 메서드의 이름입니다.|  
|**nullValue**|원본 값이 있으면 **DBNull**합니다. 다음 표를 참조 하십시오 **nullValue** 주석입니다. 기본값은 **_throw**합니다.|  
  
 다음 표에서에 지정 될 수 있는 값을 보여 줍니다.는 **nullValue** 주석입니다.  
  
|nullValue 값|설명|  
|---------------------|-----------------|  
|*대체 값*|반환될 값을 지정합니다. 반환되는 값은 요소의 형식과 일치해야 합니다. 예를 들어, `nullValue="0"`을 사용하여 null 정수 필드에 0을 반환합니다.|  
|**_throw**|예외를 throw합니다. 이 값이 기본값입니다.|  
|**_null**|기본 형식이 발견되면 null 참조를 반환하거나 예외를 throw합니다.|  
|**_empty**|문자열에 대해 반환 **String.Empty**, 그렇지 않으면 빈 생성자에서 만든 개체를 반환 합니다. 기본 형식이 발견되면 예외를 throw합니다.|  
  
 다음 표에서 형식화 된 개체에 대 한 기본 값을 보여 줍니다. **DataSet** 및 사용할 수 있는 주석입니다.  
  
|개체/메서드/이벤트|기본|주석|  
|---------------------------|-------------|----------------|  
|**DataTable**|TableNameDataTable|typedPlural|  
|**DataTable** 메서드|NewTableNameRow<br /><br /> AddTableNameRow<br /><br /> DeleteTableNameRow|typedName|  
|**DataRowCollection**|TableName|typedPlural|  
|**DataRow**|TableNameRow|typedName|  
|**DataColumn**|DataTable.ColumnNameColumn<br /><br /> DataRow.ColumnName|typedName|  
|**Property**|PropertyName|typedName|  
|**자식** 접근자|GetChildTableNameRows|typedChildren|  
|**부모** 접근자|TableNameRow|typedParent|  
|**데이터 집합** 이벤트|TableNameRowChangeEvent<br /><br /> TableNameRowChangeEventHandler|typedName|  
  
 사용 하려면 입력 **DataSet** 주석, 다음을 포함 해야 **xmlns** XML 스키마 정의 언어 (XSD) 스키마에서 참조 합니다. (데이터베이스 테이블에서 xsd를 만들려면 <xref:System.Data.DataSet.WriteXmlSchema%2A> 또는 [Visual Studio에서 데이터 집합 작업](http://msdn.microsoft.com/library/8bw9ksd6.aspx)).  
  
```  
xmlns:codegen="urn:schemas-microsoft-com:xml-msprop"  
```  
  
 다음은 주석이 있는 샘플 스키마를 노출 하는 **고객** 목차는 **Northwind** 와 관계를 사용 하 여 데이터베이스의 **주문** 포함 된 테이블입니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema id="CustomerDataSet"   
      xmlns:codegen="urn:schemas-microsoft-com:xml-msprop"  
      xmlns=""   
      xmlns:xs="http://www.w3.org/2001/XMLSchema"   
      xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="CustomerDataSet" msdata:IsDataSet="true">  
    <xs:complexType>  
      <xs:choice maxOccurs="unbounded">  
        <xs:element name="Customers" codegen:typedName="Customer" codegen:typedPlural="Customers">  
          <xs:complexType>  
            <xs:sequence>  
              <xs:element name="CustomerID"  
codegen:typedName="CustomerID" type="xs:string" minOccurs="0" />  
              <xs:element name="CompanyName"  
codegen:typedName="CompanyName" type="xs:string" minOccurs="0" />  
              <xs:element name="Phone" codegen:typedName="Phone" codegen:nullValue="" type="xs:string" minOccurs="0" />  
            </xs:sequence>  
          </xs:complexType>  
        </xs:element>  
        <xs:element name="Orders" codegen:typedName="Order" codegen:typedPlural="Orders">  
          <xs:complexType>  
            <xs:sequence>  
              <xs:element name="OrderID" codegen:typedName="OrderID"  
type="xs:int" minOccurs="0" />  
              <xs:element name="CustomerID"  
codegen:typedName="CustomerID"                  codegen:nullValue="" type="xs:string" minOccurs="0" />  
              <xs:element name="EmployeeID"  
codegen:typedName="EmployeeID" codegen:nullValue="0"   
type="xs:int" minOccurs="0" />  
              <xs:element name="OrderAdapter"  
codegen:typedName="OrderAdapter" codegen:nullValue="1980-01-01T00:00:00"   
type="xs:dateTime" minOccurs="0" />  
            </xs:sequence>  
          </xs:complexType>  
        </xs:element>  
      </xs:choice>  
    </xs:complexType>  
    <xs:unique name="Constraint1">  
      <xs:selector xpath=".//Customers" />  
      <xs:field xpath="CustomerID" />  
    </xs:unique>  
    <xs:keyref name="CustOrders" refer="Constraint1"  
codegen:typedParent="Customer" codegen:typedChildren="GetOrders">  
      <xs:selector xpath=".//Orders" />  
      <xs:field xpath="CustomerID" />  
    </xs:keyref>  
  </xs:element>  
</xs:schema>  
```  
  
 다음 코드 예제를 사용 하 여 강력한 형식의 **DataSet** 샘플 스키마에서 생성 합니다. 하나 사용 하 여 <xref:System.Data.SqlClient.SqlDataAdapter> 채우는 데는 **고객** 테이블과 다른 <xref:System.Data.SqlClient.SqlDataAdapter> 채우는 데는 **Orders** 테이블입니다. 강력한 형식의 **DataSet** 정의 **Datarelation**합니다.  
  
```vb  
' Assumes a valid SqlConnection object named connection.  
Dim customerAdapter As SqlDataAdapter = New SqlDataAdapter( _  
    "SELECT CustomerID, CompanyName, Phone FROM Customers", &  
    connection)  
Dim orderAdapter As SqlDataAdapter = New SqlDataAdapter( _  
    "SELECT OrderID, CustomerID, EmployeeID, OrderAdapter FROM Orders", &  
    connection)  
  
' Populate a strongly typed DataSet.  
connection.Open()  
Dim customers As CustomerDataSet = New CustomerDataSet()  
customerAdapter.Fill(customers, "Customers")  
orderAdapter.Fill(customers, "Orders")  
connection.Close()  
  
' Add a strongly typed event.  
AddHandler customers.Customers.CustomerChanged, &  
    New CustomerDataSet.CustomerChangeEventHandler( _  
    AddressOf OnCustomerChanged)  
  
' Add a strongly typed DataRow.  
Dim newCustomer As CustomerDataSet.Customer = _  
    customers.Customers.NewCustomeromer()  
newCustomer.CustomerID = "NEW01"  
newCustomer.CompanyName = "My New Company"  
customers.Customers.AddCustomer(newCustomer)  
  
' Navigate the child relation.  
Dim customer As CustomerDataSet.Customer  
Dim order As CustomerDataSet.Order  
  
For Each customer In customers.Customers  
  Console.WriteLine(customer.CustomerID)  
  For Each order In customer.GetOrders()  
    Console.WriteLine(vbTab & order.OrderID)  
  Next  
Next  
  
Private Shared Sub OnCustomerChanged( _  
    sender As Object, e As CustomerDataSet.CustomerChangeEvent)  
  
End Sub  
```  
  
```csharp  
// Assumes a valid SqlConnection object named connection.  
SqlDataAdapter customerAdapter = new SqlDataAdapter(  
    "SELECT CustomerID, CompanyName, Phone FROM Customers",  
    connection);  
SqlDataAdapter orderAdapter = new SqlDataAdapter(  
    "SELECT OrderID, CustomerID, EmployeeID, OrderAdapter FROM Orders",   
    connection);  
  
// Populate a strongly typed DataSet.  
connection.Open();  
CustomerDataSet customers = new CustomerDataSet();  
customerAdapter.Fill(customers, "Customers");  
orderAdapter.Fill(customers, "Orders");  
connection.Close();  
  
// Add a strongly typed event.  
customers.Customers.CustomerChanged += new   
  CustomerDataSet.CustomerChangeEventHandler(OnCustomerChanged);  
  
// Add a strongly typed DataRow.  
CustomerDataSet.Customer newCustomer =   
    customers.Customers.NewCustomeromer();  
newCustomer.CustomerID = "NEW01";  
newCustomer.CompanyName = "My New Company";  
customers.Customers.AddCustomer(newCustomer);  
  
// Navigate the child relation.  
foreach(CustomerDataSet.Customer customer in customers.Customers)  
{  
  Console.WriteLine(customer.CustomerID);  
  foreach(CustomerDataSet.Order order in customer.GetOrders())  
    Console.WriteLine("\t" + order.OrderID);  
}  
  
protected static void OnCustomerChanged(object sender, CustomerDataSet.CustomerChangeEvent e)  
    {  
  
    }  
```  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Data.DataColumnCollection>  
 <xref:System.Data.DataSet>  
 [형식화된 데이터 집합](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/typed-datasets.md)  
 [DataSet, DataTable 및 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)  
 [ADO.NET 관리되는 공급자 및 데이터 집합 개발자 센터](http://go.microsoft.com/fwlink/?LinkId=217917)
