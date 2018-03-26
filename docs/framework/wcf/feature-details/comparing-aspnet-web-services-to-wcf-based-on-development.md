---
title: 개발을 기반으로 ASP.NET 웹 서비스와 WCF 비교
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f362d00e-ce82-484f-9d4f-27e579d5c320
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: c12bd11cee62cd769f7dffc142806fa5ab1b0137
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="comparing-aspnet-web-services-to-wcf-based-on-development"></a>개발을 기반으로 ASP.NET 웹 서비스와 WCF 비교
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]에는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 응용 프로그램을 ASP.NET 웹 서비스처럼 프로그래밍하고 구성하며 동작을 모방하도록 할 수 있는 ASP.NET 호환 모드 옵션이 있습니다. 다음 단원에서는 ASP.NET 웹 서비스와 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]를 사용하여 응용 프로그램을 개발하는 데 필요한 사항을 기반으로 이 두 가지 기술을 비교합니다.  
  
## <a name="data-representation"></a>데이터 표현  
 ASP.NET을 사용하여 웹 서비스를 개발하는 경우 일반적으로 서비스에서 사용할 복합 데이터 형식을 정의하는 것부터 시작합니다. ASP.NET에서는 <xref:System.Xml.Serialization.XmlSerializer>를 사용하여 .NET Framework 형식으로 표현된 데이터를 서비스와의 전송을 위한 XML로 변환하고 XML로 받은 데이터를 .NET Framework 개체로 변환합니다. ASP.NET 서비스에서 사용할 복합 데이터 형식을 정의하려면 <xref:System.Xml.Serialization.XmlSerializer>가 XML로 또는 XML에서 serialize할 수 있는 .NET Framework 클래스를 정의해야 합니다. 이러한 클래스는 수동으로 작성하거나, 명령줄 XML 스키마/데이터 형식 지원 유틸리티인 xsd.exe를 사용하여 XML 스키마의 형식 정의에서 생성할 수 있습니다.  
  
 아래 목록에서는 <xref:System.Xml.Serialization.XmlSerializer>가 XML로 또는 XML에서 serialize할 수 있는 .NET Framework 클래스를 정의할 때 알아야 할 주요 사항을 설명합니다.  
  
-   .NET Framework 개체의 public 필드와 속성만 XML로 변환됩니다.  
  
-   클래스가 <xref:System.Collections.IEnumerable> 또는 <xref:System.Collections.ICollection> 인터페이스를 구현하는 경우에만 컬렉션 클래스의 인스턴스를 XML로 serialize할 수 있습니다.  
  
-   <xref:System.Collections.IDictionary>과 같은 <xref:System.Collections.Hashtable> 인터페이스를 구현하는 클래스는 XML로 serialize할 수 없습니다.  
  
-   클래스의 인스턴스가 XML로 표현되는 방식을 제어하기 위해 <xref:System.Xml.Serialization> 네임스페이스의 여러 가지 특성 형식을 .NET Framework 클래스와 클래스의 멤버에 추가할 수 있습니다.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 응용 프로그램 개발 역시 일반적으로 복합 형식을 정의하는 것부터 시작합니다. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]를 ASP.NET 웹 서비스와 동일한 .NET Framework 형식을 사용하도록 만들 수 있습니다.  
  
 다음 샘플 코드에서와 같이 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]<xref:System.Runtime.Serialization.DataContractAttribute> 및 <xref:System.Runtime.Serialization.DataMemberAttribute>를 .NET Framework 형식에 추가하여 해당 형식의 인스턴스가 XML로 serialize되도록 지정하고 이 형식에서 serialize되는 특정 필드 또는 속성을 표시할 수 있습니다.  
  
```  
//Example One:   
[DataContract]  
public class LineItem  
{  
    [DataMember]  
    public string ItemNumber;  
    [DataMember]  
    public decimal Quantity;  
    [DataMember]  
    public decimal UnitPrice;  
}  
  
//Example Two:   
public class LineItem  
{  
    [DataMember]  
    private string itemNumber;  
    [DataMember]  
    private decimal quantity;  
    [DataMember]  
    private decimal unitPrice;  
  
    public string ItemNumber  
    {  
      get  
      {  
          return this.itemNumber;  
      }  
  
      set  
      {  
          this.itemNumber = value;  
      }  
    }  
  
    public decimal Quantity  
    {  
        get  
        {  
            return this.quantity;  
        }  
  
        set  
        {  
            this.quantity = value;  
        }  
    }  
  
    public decimal UnitPrice  
    {  
      get  
      {  
          return this.unitPrice;  
      }  
  
      set  
      {  
          this.unitPrice = value;  
      }  
    }  
}  
  
//Example Three:   
public class LineItem  
{  
     private string itemNumber;  
     private decimal quantity;  
     private decimal unitPrice;  
  
     [DataMember]  
     public string ItemNumber  
     {  
       get  
       {  
          return this.itemNumber;  
       }  
  
       set  
       {  
           this.itemNumber = value;  
       }  
     }  
  
     [DataMember]  
     public decimal Quantity  
     {  
          get  
          {  
              return this.quantity;  
          }  
  
          set  
          {  
             this.quantity = value;  
          }  
     }  
  
     [DataMember]  
     public decimal UnitPrice  
     {  
          get  
          {  
              return this.unitPrice;  
          }  
  
          set  
          {  
              this.unitPrice = value;  
          }  
     }  
}  
```  
  
 <xref:System.Runtime.Serialization.DataContractAttribute>는 형식의 필드 또는 속성을 0개 이상 serialize하도록 지정하고, <xref:System.Runtime.Serialization.DataMemberAttribute>는 특정 필드 또는 속성을 serialize하도록 지정합니다. <xref:System.Runtime.Serialization.DataContractAttribute>는 클래스 또는 구조체에 적용될 수 있습니다. <xref:System.Runtime.Serialization.DataMemberAttribute>는 필드 또는 속성에 적용될 수 있으며, 이 특성이 적용되는 필드와 속성은 public 또는 private일 수 있습니다. <xref:System.Runtime.Serialization.DataContractAttribute>가 적용된 형식의 인스턴스를 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 데이터 계약이라고 합니다. 이러한 인스턴스는 <xref:System.Runtime.Serialization.DataContractSerializer>를 사용하여 XML로 serialize됩니다.  
  
 아래 목록에서는 <xref:System.Runtime.Serialization.DataContractSerializer>와 <xref:System.Xml.Serialization.XmlSerializer>를 사용할 때의 중요한 차이점과 <xref:System.Xml.Serialization> 네임스페이스의 다양한 특성에 대해 설명합니다.  
  
-   <xref:System.Xml.Serialization.XmlSerializer> 및 <xref:System.Xml.Serialization> 네임스페이스의 특성은 .NET Framework 형식을 XML 스키마에 정의된 유효한 형식에 매핑할 수 있도록 고안되었으므로 .NET Framework 형식을 XML로 표현하는 방식을 매우 자세하게 제어할 수 있습니다. <xref:System.Runtime.Serialization.DataContractSerializer>, <xref:System.Runtime.Serialization.DataContractAttribute> 및 <xref:System.Runtime.Serialization.DataMemberAttribute>는 형식을 XML로 표현하는 방식을 거의 제어하지 않습니다. 형식과 해당 필드 또는 속성을 XML로 표현하는 데 사용되는 네임스페이스와 이름, 그리고 필드와 속성이 XML로 나타나는 순서만 지정할 수 있습니다.  
  
    ```  
    [DataContract(  
    Namespace="urn:Contoso:2006:January:29",  
    Name="LineItem")]  
    public class LineItem  
    {  
         [DataMember(Name="ItemNumber",IsRequired=true,Order=0)]  
         public string itemNumber;  
         [DataMember(Name="Quantity",IsRequired=false,Order = 1)]  
         public decimal quantity;  
         [DataMember(Name="Price",IsRequired=false,Order = 2)]  
         public decimal unitPrice;  
    }  
    ```  
  
     .NET 형식을 표현하는 데 사용되는 XML의 구조에 관한 다른 모든 요소는 <xref:System.Runtime.Serialization.DataContractSerializer>에 의해 결정됩니다.  
  
-   형식을 XML로 표현하는 방식에 대해 많은 제어를 허용하지 않기 때문에 <xref:System.Runtime.Serialization.DataContractSerializer>에 대해 serialization 프로세스의 예측이 매우 쉽고, 따라서 최적화가 더 용이합니다. <xref:System.Runtime.Serialization.DataContractSerializer> 디자인의 실질적 이점은 약 10% 정도의 성능 향상에 있습니다.  
  
-   <xref:System.Xml.Serialization.XmlSerializer>에서 사용하는 특성은 XML로 serialize될 형식의 필드 또는 속성을 표시하지 않지만, <xref:System.Runtime.Serialization.DataMemberAttribute>에서 사용하는 <xref:System.Runtime.Serialization.DataContractSerializer>는 serialize될 필드 또는 속성을 명시적으로 보여 줍니다. 따라서 데이터 계약은 응용 프로그램에서 보내고 받을 데이터의 구조에 대한 명시적 계약이라고 할 수 있습니다.  
  
-   <xref:System.Xml.Serialization.XmlSerializer>는 .NET 개체의 public 멤버만 XML로 변환할 수 있지만 <xref:System.Runtime.Serialization.DataContractSerializer>는 개체 멤버의 액세스 한정자에 관계없이 이러한 멤버를 XML로 변환할 수 있습니다.  
  
-   형식의 public이 아닌 멤버를 XML로 serialize할 수 있기 때문에 <xref:System.Runtime.Serialization.DataContractSerializer>에는 XML로 serialize할 수 있는 .NET 형식의 다양성에 대한 제한이 더 적습니다. 특히 <xref:System.Collections.Hashtable> 인터페이스를 구현하는 <xref:System.Collections.IDictionary>과 같은 XML 형식으로 변환할 수 있습니다. 일반적으로 <xref:System.Runtime.Serialization.DataContractSerializer>는 형식의 정의를 수정하거나 형식을 위한 래퍼를 개발하지 않고도 기존 .NET 형식의 인스턴스를 XML로 serialize할 수 있는 가능성이 훨씬 더 높습니다.  
  
-   <xref:System.Runtime.Serialization.DataContractSerializer>가 형식의 public이 아닌 멤버에 액세스할 수 있다는 점에 기인한 또 다른 결과는 <xref:System.Xml.Serialization.XmlSerializer>와 달리 완전 신뢰가 필요하다는 점입니다. 완전 신뢰 코드 액세스 권한이 있으면 코드를 실행하는 자격 증명을 사용하여 액세스할 수 있는 컴퓨터의 모든 리소스에 액세스할 수 있습니다. 완전 신뢰 코드는 컴퓨터의 모든 리소스에 대한 액세스 권한을 부여하므로 이 옵션을 사용할 때는 주의를 기울여야 합니다.  
  
-   <xref:System.Runtime.Serialization.DataContractSerializer>는 버전 관리를 위한 일부 지원을 통합합니다.  
  
    -   <xref:System.Runtime.Serialization.DataMemberAttribute>에는 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> 속성이 있습니다. 이 속성에는 새 버전의 데이터 계약에 추가된, 이전 버전에는 없었던 멤버에 대해 false 값을 할당할 수 있기 때문에 새 버전의 계약이 있는 응용 프로그램에서 이전 버전을 처리할 수 있습니다.  
  
    -   데이터 계약에서 <xref:System.Runtime.Serialization.IExtensibleDataObject> 인터페이스를 구현하도록 함으로써 <xref:System.Runtime.Serialization.DataContractSerializer>가 새 버전의 데이터 계약에 정의된 멤버를 이전 버전의 계약을 사용하는 응용 프로그램을 통해 전달하도록 허용할 수 있습니다.  
  
 이러한 모든 차이점에도 불구하고 <xref:System.Xml.Serialization.XmlSerializer>에서 기본적으로 형식을 serialize하는 XML은 해당 XML에 대한 네임스페이스가 명시적으로 정의되어 있는 경우 <xref:System.Runtime.Serialization.DataContractSerializer>에서 형식을 serialize하는 XML과 의미상 동일합니다. 따라서 다음과 같이 두 serializer에서 사용하는 특성을 가지고 있는 클래스는 <xref:System.Xml.Serialization.XmlSerializer>와 <xref:System.Runtime.Serialization.DataContractAttribute>에서 의미상 동일한 XML로 변환됩니다.  
  
```  
[Serializable]  
[XmlRoot(Namespace="urn:Contoso:2006:January:29")]  
[DataContract(Namespace="urn:Contoso:2006:January:29")]  
public class LineItem  
{  
     [DataMember]  
     public string ItemNumber;  
     [DataMember]  
     public decimal Quantity;  
     [DataMember]  
     public decimal UnitPrice;  
}  
```  
  
 Windows 소프트웨어 개발 키트 (SDK) 명령줄 도구가 포함 된 [ServiceModel Metadata 유틸리티 도구 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)합니다. ASP.NET 웹 서비스와 함께 사용 되는 xsd.exe 도구와 같은 Svcutil.exe XML 스키마에서.NET 데이터 형식의 정의 생성할 수 있습니다. <xref:System.Runtime.Serialization.DataContractSerializer>에서 XML 스키마에 의해 정의된 형식의 XML을 내보낼 수 있으면 이러한 형식은 데이터 계약이 됩니다. 그렇지 않으면 이러한 형식은 <xref:System.Xml.Serialization.XmlSerializer>를 사용하여 serialize됩니다. Svcutil.exe 도구는 또한 `/dataContractOnly` 스위치를 사용하여 데이터 계약에서 XML 스키마를 생성할 수도 있습니다.  
  
> [!NOTE]
>  ASP.NET 웹 서비스에서 <xref:System.Xml.Serialization.XmlSerializer>를 사용하고, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ASP.NET 호환 모드를 통해 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스에서 ASP.NET 웹 서비스의 동작을 모방하는 경우에도 ASP.NET 호환 옵션에서 <xref:System.Xml.Serialization.XmlSerializer>를 사용하도록 제한되지는 않습니다. ASP.NET 호환 모드에서 실행되는 서비스에서 <xref:System.Runtime.Serialization.DataContractSerializer>를 계속 사용할 수 있습니다.  
  
## <a name="service-development"></a>서비스 개발  
 ASP.NET을 사용하여 서비스를 개발하려면 일반적으로 클래스에 <xref:System.Web.Services.WebService> 특성을 추가하고 서비스의 작업이 되는 해당 클래스의 메서드에 <xref:System.Web.Services.WebMethodAttribute>를 추가했었습니다.  
  
```  
[WebService]  
public class Service : T:System.Web.Services.WebService  
{  
    [WebMethod]  
    public string Echo(string input)   
    {  
       return input;  
    }  
}  
```  
  
 ASP.NET 2.0에는 클래스가 아니라 인터페이스에 <xref:System.Web.Services.WebService> 및 <xref:System.Web.Services.WebMethodAttribute> 특성을 추가하고 해당 인터페이스를 구현하기 위해 클래스를 작성하는 옵션이 추가되었습니다.  
  
```  
[WebService]  
public interface IEcho  
{  
    [WebMethod]  
    string Echo(string input);  
}  
  
public class Service : IEcho  
{  
  
   public string Echo(string input)  
   {  
        return input;  
    }  
}  
```  
  
 같은 계약을 여러 가지 방식으로 구현하는 다양한 클래스에 사용할 수 있는 서비스의 수행 작업에 대한 계약은 <xref:System.Web.Services.WebService> 특성을 가진 인터페이스로 구성되므로 이 옵션을 사용하는 것이 좋습니다.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스는 하나 이상의 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 끝점을 정의함으로써 제공합니다. 끝점은 주소, 바인딩 및 서비스 계약으로 정의됩니다. 주소는 서비스가 있는 위치를 정의합니다. 바인딩은 서비스와 통신하는 방법을 지정합니다. 서비스 계약은 서비스에서 수행할 수 있는 작업을 정의합니다.  
  
 일반적으로 서비스 계약은 다음과 같이 인터페이스에 <xref:System.ServiceModel.ServiceContractAttribute> 및 <xref:System.ServiceModel.OperationContractAttribute>를 추가함으로써 정의됩니다.  
  
```  
[ServiceContract]  
public interface IEcho  
{  
     [OperationContract]  
     string Echo(string input);  
}  
```  
  
 <xref:System.ServiceModel.ServiceContractAttribute>는 인터페이스에서 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스 계약을 정의하도록 지정하고, <xref:System.ServiceModel.OperationContractAttribute>는 서비스 계약의 작업을 정의하는 인터페이스의 메서드(있는 경우)를 나타냅니다.  
  
 서비스 계약은 일단 정의되면 다음과 같이 클래스로 하여금 서비스 계약을 정의하는 인터페이스를 구현하도록 함으로써 클래스에서 구현됩니다.  
  
```  
public class Service : IEcho  
{  
    public string Echo(string input)  
    {  
       return input;  
    }  
}  
```  
  
 서비스 계약을 구현하는 클래스를 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 서비스 유형이라고 합니다.  
  
 다음 단계는 주소 및 바인딩을 서비스 유형과 연결하는 것입니다. 이 작업은 일반적으로 구성 파일을 직접 편집하거나 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서 제공되는 구성 편집기를 사용하여 구성 파일에서 수행됩니다. 다음은 구성 파일의 예제입니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
     <system.serviceModel>  
      <services>  
      <service name="Service ">  
       <endpoint   
        address="EchoService"  
        binding="basicHttpBinding"  
        contract="IEchoService "/>  
      </service>  
      </services>  
     </system.serviceModel>  
</configuration>  
```  
  
 바인딩은 응용 프로그램과의 통신을 위한 프로토콜 집합을 지정합니다. 다음 표에서는 일반 옵션을 나타내는 시스템 제공 바인딩을 보여 줍니다.  
  
|이름|용도|  
|----------|-------------|  
|BasicHttpBinding|WS-BasicProfile 1.1 및 Basic Security Profile 1.0을 지원하는 웹 서비스 및 클라이언트와의 상호 운용성|  
|WSHttpBinding|HTTP를 통한 WS-* 프로토콜을 지원하는 웹 서비스 및 클라이언트와의 상호 운용성|  
|WSDualHttpBinding|이중 HTTP 통신(초기 메시지 수신자가 초기 송신자에게 직접 응답하지 않고, 일정 기간에 걸쳐 WS-* 프로토콜을 따르는 HTTP를 사용하여 원하는 수의 응답을 전송할 수 있음)|  
|WSFederationBinding|HTTP 통신(명시적으로 식별된 자격 증명 공급자가 발행한 자격 증명에 따라 서비스의 리소스에 대한 액세스를 제어할 수 있음)|  
|NetTcpBinding|[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 소프트웨어 엔터티 간의 네트워크를 통한 안정적인 고성능 보안 통신|  
|NetNamedPipeBinding|같은 컴퓨터에 있는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 소프트웨어 엔터티 간의 안정적인 고성능 보안 통신|  
|NetMsmqBinding|[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 소프트웨어 엔터티 간의 MSMQ를 사용한 통신|  
|MsmqIntegrationBinding|[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 소프트웨어 엔터티와 다른 소프트웨어 엔터티 간의 MSMQ를 사용한 통신|  
|NetPeerTcpBinding|[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 소프트웨어 엔터티 간의 Windows 피어 투 피어 네트워킹을 사용한 통신|  
  
 시스템 제공 바인딩인 <xref:System.ServiceModel.BasicHttpBinding>은 ASP.NET 웹 서비스에서 지원되는 프로토콜 집합을 통합합니다.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 응용 프로그램용 사용자 지정 바인딩은 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서 개별 프로토콜을 구현하는 데 사용하는 바인딩 요소 클래스의 컬렉션으로 쉽게 정의됩니다. 새 바인딩 요소를 작성하여 추가 프로토콜을 나타낼 수 있습니다.  
  
 서비스 유형의 내부 동작은 동작이라는 클래스 모음의 속성을 사용하여 조정할 수 있습니다. 다음 예제에서는 <xref:System.ServiceModel.ServiceBehaviorAttribute> 클래스를 사용하여 서비스 유형이 다중 스레드되도록 지정합니다.  
  
```  
[ServiceBehavior(ConcurrencyMode=ConcurrencyMode.Multiple]  
public class DerivativesCalculatorServiceType: IDerivativesCalculator  
```  
  
 <xref:System.ServiceModel.ServiceBehaviorAttribute>와 같은 일부 동작은 특성입니다. 관리자가 설정할 수 있는 속성이 있는 다른 동작은 응용 프로그램의 구성에서 수정할 수 있습니다.  
  
 서비스 유형 프로그래밍에서는 <xref:System.ServiceModel.OperationContext> 클래스가 자주 사용됩니다. 이 클래스의 정적 <xref:System.ServiceModel.OperationContext.Current%2A> 속성은 작업이 실행되고 있는 컨텍스트의 정보에 대한 액세스를 제공합니다. 따라서 <xref:System.ServiceModel.OperationContext>는 <xref:System.Web.HttpContext> 및 <xref:System.EnterpriseServices.ContextUtil> 클래스와 모두 비슷합니다.  
  
## <a name="hosting"></a>호스팅  
 ASP.NET 웹 서비스는 클래스 라이브러리 어셈블리로 컴파일됩니다. 확장명이 .asmx인 서비스 파일이라는 파일이 제공됩니다. 이 파일에는 서비스에 대한 코드를 포함하는 클래스와 이 클래스가 있는 어셈블리를 식별하는 `@ WebService` 지시문이 포함되어 있습니다.  
  
```  
<%@ WebService Language="C#" Class="Service,ServiceAssembly" %>  
```  
  
 서비스 파일은 IIS(인터넷 정보 서비스)의 ASP.NET 응용 프로그램 루트에 복사되고, 어셈블리는 이 응용 프로그램 루트의 \bin 하위 디렉터리에 복사됩니다. 그런 다음 응용 프로그램 루트에 있는 서비스 파일의 URL(Uniform Resource Locator)을 사용하여 이 응용 프로그램에 액세스할 수 있습니다.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스는 IIS 5.1 또는 6.0, IIS 7.0의 일부로 제공되는 WAS(Windows Process Activation Service), 그리고 모든 .NET 응용 프로그램 내에서 즉시 호스트할 수 있습니다. IIS 5.1 또는 6.0에서 서비스를 호스트하려면 이 서비스가 HTTP를 통신 전송 프로토콜로 사용해야 합니다.  
  
 IIS 5.1, 6.0 또는 WAS에서 서비스를 호스트하려면 다음 단계를 수행합니다.  
  
1.  서비스 유형을 클래스 라이브러리 어셈블리로 컴파일합니다.  
  
2.  다음과 같은 서비스 유형을 식별하는 `@ ServiceHost` 지시문이 포함된 서비스 파일(확장명 .svc)로 만듭니다.  
  
    ```  
    <%@ServiceHost language="c#" Service="MyService" %>  
    ```  
  
3.  서비스 파일을 가상 디렉터리에 복사하고 어셈블리를 이 가상 디렉터리의 \bin 하위 디렉터리에 복사합니다.  
  
4.  구성 파일을 가상 디렉터리에 복사하고 파일 이름을 Web.config로 지정합니다.  
  
 그러면 응용 프로그램 루트에 있는 서비스 파일의 URL을 사용하여 해당 응용 프로그램에 액세스할 수 있습니다.  
  
 .NET 응용 프로그램에서 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스를 호스트하려면 서비스 유형을 이 응용 프로그램에서 참조하는 클래스 라이브러리 어셈블리로 컴파일하고, <xref:System.ServiceModel.ServiceHost> 클래스를 사용하여 해당 서비스를 호스트하도록 응용 프로그램을 프로그래밍합니다. 다음은 필요한 기본 프로그래밍 예제입니다.  
  
```  
string httpBaseAddress = "http://www.contoso.com:8000/";  
string tcpBaseAddress = "net.tcp://www.contoso.com:8080/";  
  
Uri httpBaseAddressUri = new Uri(httpBaseAddress);  
Uri tcpBaseAddressUri = new Uri(tcpBaseAddress);  
  
Uri[] baseAdresses = new Uri[] {   
 httpBaseAddressUri,  
 tcpBaseAddressUri};  
  
using(ServiceHost host = new ServiceHost(  
typeof(Service), //"Service" is the name of the service type baseAdresses))  
{  
     host.Open();  
  
     […] //Wait to receive messages  
     host.Close();  
}  
```  
  
 이 예제에서는 <xref:System.ServiceModel.ServiceHost> 생성에서 하나 이상의 전송 프로토콜에 대한 주소가 지정되는 방식을 보여 줍니다. 이러한 주소를 기본 주소라고 합니다.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스의 끝점에 제공되는 주소는 끝점의 호스트에 대한 기본 주소에 상대적인 주소입니다. 호스트에는 통신 전송 프로토콜마다 기본 주소가 하나씩 있을 수 있습니다. 이전 구성 파일의 샘플 구성에서 끝점에 대해 선택된 <xref:System.ServiceModel.BasicHttpBinding>은 HTTP를 전송 프로토콜로 사용하므로 `EchoService` 끝점의 주소는 호스트의 HTTP 기본 주소에 상대적입니다. 앞의 예제에서 호스트의 경우 HTTP 기본 주소는 http://www.contoso.com:8000/합니다. IIS 또는 WAS에서 호스트되는 서비스의 기본 주소는 해당 서비스에 대한 서비스 파일의 URL입니다.  
  
 IIS 또는 WAS에서 호스트되고 전송 프로토콜로 HTTP만 사용하도록 구성된 서비스만 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ASP.NET 호환 모드 옵션을 사용하도록 만들 수 있습니다. 이 옵션을 사용하려면 다음 단계를 수행해야 합니다.  
  
1.  프로그래머는 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute> 특성을 서비스 유형에 추가하여 ASP.NET 호환 모드가 허용되는지 또는 필수인지 지정해야 합니다.  
  
    ```  
    [System.ServiceModel.Activation.AspNetCompatibilityRequirements(  
          RequirementsMode=AspNetCompatbilityRequirementsMode.Require)]  
    public class DerivativesCalculatorServiceType: IDerivativesCalculator  
    ```  
  
2.  관리자는 ASP.NET 호환 모드를 사용하도록 응용 프로그램을 구성해야 합니다.  
  
    ```xml  
    <configuration>  
         <system.serviceModel>  
          <services>  
          […]  
          </services>  
          <serviceHostingEnvironment aspNetCompatibilityEnabled="true"/>  
        </system.serviceModel>  
    </configuration>  
    ```  
  
     서비스 파일의 확장명으로 .svc가 아닌 .asmx를 사용하도록 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 응용 프로그램을 구성할 수도 있습니다.  
  
    ```xml  
    <system.web>  
         <compilation>  
          <compilation debug="true">  
          <buildProviders>  
           <remove extension=".asmx"/>  
           <add extension=".asmx"   
            type="System.ServiceModel.ServiceBuildProvider,   
            Systemm.ServiceModel,   
            Version=3.0.0.0,   
            Culture=neutral,   
            PublicKeyToken=b77a5c561934e089" />  
          </buildProviders>  
          </compilation>  
         </compilation>  
    </system.web>  
    ```  
  
     이 옵션을 사용하면 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]를 사용하도록 서비스를 수정할 때 .asmx 서비스 파일의 URL을 사용하도록 구성된 클라이언트를 수정하지 않아도 됩니다.  
  
## <a name="client-development"></a>클라이언트 개발  
 ASP.NET 웹 서비스용 클라이언트는 .asmx 파일의 URL을 입력으로 제공하는 WSDL.exe 명령줄 도구를 사용하여 생성됩니다. 제공 하는 해당 도구 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 은 [ServiceModel Metadata 유틸리티 도구 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)합니다. 이 도구는 서비스 계약과 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 클라이언트 클래스에 대한 정의를 포함한 코드 모듈을 생성합니다. 또한 서비스의 주소와 바인딩을 포함한 구성 파일도 생성합니다.  
  
 원격 서비스의 클라이언트를 프로그래밍할 때 일반적으로 비동기 패턴에 따라 프로그래밍하는 것이 좋습니다. WSDL.exe 도구로 생성되는 코드는 기본적으로 항상 동기 패턴과 비동기 패턴을 모두 제공합니다. 생성 된 코드는 [ServiceModel Metadata 유틸리티 도구 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 패턴 중 하나에 제공할 수 있습니다. 이 도구는 기본적으로 동기 패턴을 제공합니다. 이 도구를 `/async` 스위치와 함께 실행하면 생성된 코드에서 비동기 패턴을 제공합니다.  
  
 ASP.NET의 WSDL.exe 도구로 생성되는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 클라이언트 클래스에 있는 이름과 Svcutil.exe 도구로 생성되는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 클라이언트 클래스에 있는 이름이 일치하지 않을 수도 있습니다. 특히 <xref:System.Xml.Serialization.XmlSerializer>를 사용하여 serialize되어야 하는 클래스의 속성 이름에는 Svcutil.exe 도구로 생성되는 코드의 경우 기본적으로 Property 접미사가 지정되지만 WSDL.exe 도구로 생성되는 코드의 경우에는 Property 접미사가 지정되지 않습니다.  
  
## <a name="message-representation"></a>메시지 표현  
 ASP.NET 웹 서비스에서 보내고 받는 SOAP 메시지의 헤더를 사용자 지정할 수 있습니다. <xref:System.Web.Services.Protocols.SoapHeader>에서 클래스가 파생되어 헤더의 구조가 정의된 다음 <xref:System.Web.Services.Protocols.SoapHeaderAttribute>가 헤더의 존재를 나타내는 데 사용됩니다.  
  
```  
public class SomeProtocol : SoapHeader  
{  
     public long CurrentValue;  
     public long Total;  
}  
  
[WebService]  
public interface IEcho  
{  
     SomeProtocol ProtocolHeader  
     {  
      get;  
     set;  
     }  
  
     [WebMethod]  
     [SoapHeader("ProtocolHeader")]  
     string PlaceOrders(PurchaseOrderType order);  
}  
  
public class Service: WebService, IEcho  
{  
     private SomeProtocol protocolHeader;  
  
     public SomeProtocol ProtocolHeader  
     {  
         get  
         {  
              return this.protocolHeader;  
         }  
  
         set  
         {  
              this.protocolHeader = value;  
         }  
     }  
  
     string PlaceOrders(PurchaseOrderType order)  
     {  
         long currentValue = this.protocolHeader.CurrentValue;  
     }  
}  
```  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 <xref:System.ServiceModel.MessageContractAttribute>, <xref:System.ServiceModel.MessageHeaderAttribute> 및 <xref:System.ServiceModel.MessageBodyMemberAttribute> 특성을 제공하여 서비스에서 보내고 받는 SOAP 메시지의 구조를 설명합니다.  
  
```  
[DataContract]  
public class SomeProtocol  
{  
     [DataMember]  
     public long CurrentValue;  
     [DataMember]  
     public long Total;  
}  
  
[DataContract]  
public class Item  
{  
     [DataMember]  
     public string ItemNumber;  
     [DataMember]  
     public decimal Quantity;  
     [DataMember]  
     public decimal UnitPrice;  
}  
  
[MessageContract]  
public class ItemMesage  
{  
     [MessageHeader]  
     public SomeProtocol ProtocolHeader;  
     [MessageBody]  
     public Item Content;  
}  
  
[ServiceContract]  
public interface IItemService  
{  
     [OperationContract]  
     public void DeliverItem(ItemMessage itemMessage);  
}  
```  
  
 이 구문은 메시지 구조를 명시적으로 표현하지만 메시지 구조는 ASP.NET 웹 서비스의 코드로 암시됩니다. 또한 ASP.NET 구문에서는 메시지 헤더가 위 예제의 `ProtocolHeader` 속성과 같은 서비스 속성으로 나타나지만 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 구문에서는 메시지 속성으로 더욱 정확하게 나타납니다. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 끝점 구성에 메시지 헤더를 추가할 수도 있습니다.  
  
```xml  
<service name="Service ">  
     <endpoint   
      address="EchoService"  
      binding="basicHttpBinding"  
      contract="IEchoService ">  
      <headers>  
      <dsig:X509Certificate   
       xmlns:dsig="http://www.w3.org/2000/09/xmldsig#">  
       ...  
      </dsig:X509Certificate>  
      </headers>  
     </endpoint>  
</service>  
```  
  
 이 옵션을 사용하면 클라이언트 또는 서비스에 대한 코드에서 인프라 프로토콜 헤더를 참조할 필요가 없습니다. 끝점의 구성 방식에 따라 헤더가 메시지에 추가되기 때문입니다.  
  
## <a name="service-description"></a>서비스 설명  
 쿼리 WSDL을 사용하여 ASP.NET 웹 서비스의 .asmx 파일에 대해 HTTP GET 요청을 발행하면 ASP.NET에서 해당 서비스를 설명하는 WSDL을 생성합니다. 이 WSDL이 요청에 대한 응답으로 반환됩니다.  
  
 ASP.NET 2.0을 통해 서비스가 WS-I(웹 서비스 상호 운용성) 조직의 Basic Profile 1.1과 호환되는지 확인하고 서비스가 WSDL과 호환된다는 클레임을 넣을 수 있게 되었습니다. 다음과 같이 `ConformsTo` 특성의 `EmitConformanceClaims` 및 <xref:System.Web.Services.WebServiceBindingAttribute> 매개 변수를 사용하면 됩니다.  
  
```  
[WebService(Namespace = "http://tempuri.org/")]  
[WebServiceBinding(  
     ConformsTo = WsiProfiles.BasicProfile1_1,  
     EmitConformanceClaims=true)]  
public interface IEcho  
```  
  
 ASP.NET에서 서비스에 대해 생성하는 WSDL을 사용자 지정할 수 있습니다. <xref:System.Web.Services.Description.ServiceDescriptionFormatExtension>의 파생 클래스를 만들어 WSDL에 항목을 추가함으로써 사용자 지정합니다.  
  
 IIS 5.1, 6.0 또는 WAS에서 호스트되는 HTTP 끝점이 있는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스의 .svc 파일에 대해 쿼리 WSDL을 사용하여 HTTP GET 요청을 발행하면 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서 해당 서비스를 설명하는 WSDL로 응답하게 됩니다. httpGetEnabled가 true로 설정된 경우 .NET 응용 프로그램에서 호스트되는 서비스의 HTTP 기본 주소에 대해 쿼리 WSDL을 사용하여 HTTP GET 요청을 실행해도 동일한 효과가 나타납니다.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]를 WS-MetadataExchange 요청에 대해서도 서비스를 설명하기 위해 생성하는 WSDL로 응답합니다. ASP.NET 웹 서비스는 WS-MetadataExchange 요청에 대한 지원을 기본적으로 제공하지 않습니다.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서 생성하는 WSDL을 광범위하게 사용자 지정할 수 있습니다. <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 클래스는 WSDL을 사용자 지정하기 위한 몇 가지 기능을 제공합니다. 또한 WSDL을 생성하지 않고 지정된 URL에서 정적 WSDL 파일을 사용하도록 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]를 구성할 수도 있습니다.  
  
```xml  
<behaviors>  
     <behavior name="DescriptionBehavior">  
     <metadataPublishing   
      enableMetadataExchange="true"   
      enableGetWsdl="true"   
      enableHelpPage="true"   
      metadataLocation=  
      "http://localhost/DerivativesCalculatorService/Service.WSDL"/>  
     </behavior>  
</behaviors>  
```  
  
## <a name="exception-handling"></a>예외 처리  
 ASP.NET 웹 서비스에서 처리되지 않은 예외는 클라이언트에 SOAP 오류로 반환됩니다. 또한 <xref:System.Web.Services.Protocols.SoapException> 클래스의 인스턴스를 명시적으로 throw하고 클라이언트에 전송되는 SOAP 오류의 내용을 세밀하게 제어할 수 있습니다.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스에서는 중요한 정보가 예외를 통해 실수로 노출되지 않도록, 처리되지 않은 예외를 클라이언트에 SOAP 오류로 반환하지 않습니다. 디버깅을 위해 처리되지 않은 예외가 클라이언트에게 반환되도록 하는 구성 설정이 제공됩니다.  
  
 SOAP 오류를 클라이언트에게 반환하려면 데이터 계약 형식을 제네릭 형식으로 사용하여 제네릭 형식의 <xref:System.ServiceModel.FaultException%601> 인스턴스를 throw할 수 있습니다. 또한 <xref:System.ServiceModel.FaultContractAttribute> 특성을 작업에 추가하여 작업에서 발생 가능한 오류를 지정할 수 있습니다.  
  
```  
[DataContract]  
public class MathFault  
{   
     [DataMember]  
     public string operation;  
     [DataMember]  
     public string problemType;  
}  
  
[ServiceContract]  
public interface ICalculator  
{  
     [OperationContract]  
     [FaultContract(typeof(MathFault))]  
     int Divide(int n1, int n2);  
}  
```  
  
 이렇게 하면 가능한 오류가 서비스에 대한 WSDL에 알려지기 때문에 클라이언트 프로그래머가 작업에서 발생할 수 있는 오류를 정확히 예상하고 적절한 catch 문을 작성할 수 있습니다.  
  
```  
try  
{  
     result = client.Divide(value1, value2);  
}  
catch (FaultException<MathFault> e)  
{  
 Console.WriteLine("FaultException<MathFault>: Math fault while doing "  
  + e.Detail.operation   
  + ". Problem: "   
  + e.Detail.problemType);  
}  
```  
  
## <a name="state-management"></a>상태 관리  
 ASP.NET 웹 서비스를 구현하는 데 사용되는 클래스는 <xref:System.Web.Services.WebService>에서 파생될 수 있습니다.  
  
```  
public class Service : WebService, IEcho  
{  
  
 public string Echo(string input)  
 {  
  return input;  
 }  
}  
```  
  
 이러한 경우 <xref:System.Web.Services.WebService> 기본 클래스의 Context 속성을 사용하여 <xref:System.Web.HttpContext> 개체에 액세스하도록 클래스를 프로그래밍할 수 있습니다. <xref:System.Web.HttpContext> 개체를 사용하여 Application 속성을 통해 응용 프로그램 상태 정보를 업데이트 및 검색하고 Session 속성을 통해 세션 상태 정보를 업데이트 및 검색할 수 있습니다.  
  
 ASP.NET에서는 <xref:System.Web.HttpContext>의 Session 속성을 사용하여 액세스되는 세션 상태 정보가 실제로 저장되는 위치를 세부적으로 제어할 수 있습니다. 세션 상태 정보는 쿠키, 데이터베이스, 현재 서버의 메모리 또는 지정된 서버의 메모리에 저장될 수 있습니다. 저장 위치는 서비스의 구성 파일에서 선택됩니다.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 상태 관리를 위한 확장 가능한 개체를 제공합니다. 확장 가능한 개체는 <xref:System.ServiceModel.IExtensibleObject%601>를 구현하는 개체입니다. 가장 중요한 확장 가능한 개체는 <xref:System.ServiceModel.ServiceHostBase> 및 <xref:System.ServiceModel.InstanceContext>입니다. `ServiceHostBase`를 사용하면 같은 호스트에 있는 모든 서비스 유형의 모든 인스턴스에서 액세스할 수 있는 상태를 유지할 수 있으며, `InstanceContext`를 사용하면 서비스 유형의 같은 인스턴스 내에서 실행되는 코드로 액세스할 수 있는 상태를 유지할 수 있습니다.  
  
 여기서 `TradingSystem` 서비스 유형에는 같은 <xref:System.ServiceModel.ServiceBehaviorAttribute> 클라이언트 인스턴스의 모든 호출이 서비스 유형의 같은 인스턴스로 라우트되도록 지정하는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]가 있습니다.  
  
```  
[ServiceBehavior(InstanceContextMode = InstanceContextMode.PerSession)]  
public class TradingSystem: ITradingService  
```  
  
 `DealData` 클래스는 서비스 유형의 같은 인스턴스 내에서 실행되는 코드로 액세스할 수 있는 상태를 정의합니다.  
  
```  
internal class DealData: IExtension<InstanceContext>  
{  
 public string DealIdentifier = null;  
 public Trade[] Trades = null;  
}  
```  
  
 서비스 계약의 작업 중 하나를 구현하는 서비스 유형의 코드에서 `DealData` 상태 개체는 서비스 유형의 현재 인스턴스에 대한 상태에 추가됩니다.  
  
```  
string ITradingService.BeginDeal()  
{  
 string dealIdentifier = Guid.NewGuid().ToString();  
 DealData state = new DealData(dealIdentifier);  
 OperationContext.Current.InstanceContext.Extensions.Add(state);  
 return dealIdentifier;  
}  
```  
  
 그런 다음 이 상태 개체는 서비스 계약의 작업 중 다른 하나를 구현하는 코드로 검색하고 수정할 수 있습니다.  
  
```  
void ITradingService.AddTrade(Trade trade)  
{  
 DealData dealData =  OperationContext.Current.InstanceContext.Extensions.Find<DealData>();  
 dealData.AddTrade(trade);  
}  
```  
  
 ASP.NET에서 <xref:System.Web.HttpContext> 클래스의 상태 정보가 실제로 저장되는 위치를 제어할 수 있지만, 적어도 초기 버전의 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 확장 가능한 개체가 저장되는 위치를 제어할 수 없습니다. 이러한 점이 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스를 위해 ASP.NET 호환 모드를 선택하는 가장 정당한 이유가 됩니다. 구성 가능한 상태 관리가 필수적인 경우 ASP.NET 호환 모드를 채택함으로써 <xref:System.Web.HttpContext> 클래스의 기능을 ASP.NET에서와 똑같은 방식으로 사용할 수 있으며 <xref:System.Web.HttpContext> 클래스를 사용하여 관리되는 상태 정보가 저장되는 위치를 구성할 수도 있습니다.  
  
## <a name="security"></a>보안  
 ASP.NET 웹 서비스의 보안을 유지하기 위한 옵션은 IIS 응용 프로그램의 보안을 유지하는 옵션과 같습니다. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 응용 프로그램은 IIS뿐만 아니라 .NET 실행 파일 내에서도 호스트될 수 있기 때문에 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 응용 프로그램의 보안을 유지하기 위한 옵션은 IIS 기능과 별도로 지정해야 합니다. 그러나 ASP.NET 웹 서비스에 제공되는 기능은 ASP.NET 호환 모드에서 실행되는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스에서도 사용할 수 있습니다.  
  
### <a name="security-authentication"></a>보안: 인증  
 IIS는 응용 프로그램에 대한 액세스를 제어하는 기능을 제공하므로 이 기능을 통해 Windows 인증, 다이제스트 인증, 기본 인증, .NET Passport 인증 등 다양한 모드의 인증을 선택할 수 있습니다. Windows 인증 옵션을 사용하면 ASP.NET 웹 서비스에 대한 액세스를 제어할 수 있습니다. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 응용 프로그램이 IIS 내에서 호스트되는 경우에는 이 응용 프로그램에 대한 익명 액세스를 허용하도록 IIS를 구성하여 다양한 다른 옵션과 함께 Windows 인증을 지원하는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 자체에서 인증을 관리할 수 있도록 해야 합니다. 기본 제공되는 다른 옵션으로는 사용자 이름 토큰, X.509 인증서, SAML 토큰, CardSpace 카드 등이 있으며 사용자 지정 인증 메커니즘을 정의할 수도 있습니다.  
  
### <a name="security-impersonation"></a>보안: 가장  
 ASP.NET에서는 ASP.NET 웹 서비스가 특정 사용자로, 또는 현재 요청에서 제공된 사용자의 자격 증명으로 가장할 수 있도록 하는 ID 요소를 제공합니다. 이 요소를 사용하면 ASP.NET 호환 모드에서 실행되고 있는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 응용 프로그램에서 가장을 구성할 수 있습니다.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 구성 시스템은 가장할 특정 사용자를 지정하기 위한 자체 ID 요소를 제공합니다. 또한 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 클라이언트 및 서비스는 가장을 위해 별도로 구성할 수 있습니다. 클라이언트는 요청을 전송할 때 현재 사용자로 가장하도록 구성할 수 있습니다.  
  
```xml  
<behaviors>  
     <behavior name="DerivativesCalculatorClientBehavior">  
      <clientCredentials>  
      <windows allowedImpersonationLevel="Impersonation"/>  
      </clientCredentials>  
     </behavior>  
</behaviors>  
```  
  
 서비스 작업은 현재 요청에서 제공된 사용자의 자격 증명으로 가장하도록 구성할 수 있습니다.  
  
```  
[OperationBehavior(Impersonation = ImpersonationOption.Required)]  
public void Receive(Message input)  
```  
  
### <a name="security-authorization-using-access-control-lists"></a>보안: 액세스 제어 목록을 사용하여 권한 부여  
 ACL(액세스 제어 목록)을 사용하면 .asmx 파일에 대한 액세스를 제한할 수 있습니다. 그러나 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] .svc 파일에 대한 ACL은 ASP.NET 호환 모드인 경우를 제외하고는 무시됩니다.  
  
### <a name="security-role-based-authorization"></a>보안: 역할 기반 권한 부여  
 IIS Windows 인증 옵션을 ASP.NET 구성 언어로 제공되는 권한 부여 요소와 함께 사용하면 사용자에게 지정된 Windows 그룹 기반의 ASP.NET 웹 서비스에 대한 역할 기반 권한을 쉽게 부여할 수 있습니다. ASP.NET 2.0에는 더 포괄적인 역할 기반 권한 부여 메커니즘인 역할 공급자가 도입되었습니다.  
  
 역할 공급자는 사용자에게 할당된 역할을 쿼리하기 위한 기본 인터페이스를 구현하는 클래스입니다. 각 역할 공급자는 서로 다른 소스에서 해당 정보를 검색하는 방법을 인식하고 있습니다. ASP.NET 2.0은 Microsoft SQL Server 데이터베이스에서 역할 할당을 검색할 수 있는 역할 공급자와 Windows Server 2003 권한 부여 관리자에서 역할 할당을 검색할 수 있는 역할 공급자를 제공합니다.  
  
 실제로 역할 공급자 메커니즘은 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 응용 프로그램을 포함한 모든 .NET 응용 프로그램에서 ASP.NET과 별도로 사용할 수 있습니다. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 응용 프로그램에 대한 다음 샘플 구성에서는 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>를 통해 ASP.NET 역할 공급자를 사용하는 옵션이 선택되는 방식을 보여 줍니다.  
  
```xml  
<system.serviceModel>  
     <services>  
         <service name="Service.ResourceAccessServiceType"   
             behaviorConfiguration="ServiceBehavior">  
             <endpoint   
              address="ResourceAccessService"   
              binding="wsHttpBinding"   
              contract="Service.IResourceAccessContract"/>  
         </service>  
     </services>  
     <behaviors>  
       <behavior name="ServiceBehavior">  
       <serviceAuthorization principalPermissionMode="UseAspNetRoles"/>  
      </behavior>  
     </behaviors>  
</system.serviceModel>  
```  
  
### <a name="security-claims-based-authorization"></a>보안: 클레임 기반 권한 부여  
 클레임에 기반하여 보호되는 리소스에 대한 액세스 권한 부여를 완벽하게 지원하는 것은 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]의 가장 중요한 혁신 중 하나입니다. 클레임은 형식, 권한 및 값으로 구성됩니다. 예를 들어, 운전 면허증을 생각해 보세요. 운전 면허증은 소지인에 대한 클레임 집합으로 구성되는데, 그 중 하나는 소지인의 생년월일입니다. 이 클레임의 형식은 생년월일이고, 값은 운전자의 생년월일입니다. 클레임이 소지인에게 부여하는 권한은 소지인이 클레임 값으로 수행할 수 있는 작업을 지정합니다. 운전자의 생년월일에 대한 클레임의 경우 권한은 단순한 소유입니다. 운전자는 해당 생년월일을 소유하고 있지만 변경하는 등의 작업은 할 수 없습니다. 역할은 단순히 클레임의 한 형식이기 때문에 클레임 기반 인증은 역할 기반 인증을 포함합니다.  
  
 클레임 기반 인증은 클레임 집합을 작업의 액세스 요구 사항과 비교하여 그 결과에 따라 작업에 대한 액세스 권한을 부여하거나 거부함으로써 수행됩니다. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 `ServiceAuthorizationManager`의 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior> 속성에 값을 다시 한 번 할당함으로써 클레임 기반 권한 부여를 실행하는 데 사용할 클래스를 지정할 수 있습니다.  
  
```xml  
<behaviors>  
     <behavior name='ServiceBehavior'>  
     <serviceAuthorization   
     serviceAuthorizationManagerType=  
                   'Service.AccessChecker, Service' />  
     </behavior>  
</behaviors>  
```  
  
 클레임 기반 권한 부여를 실행하는 데 사용되는 클래스는 <xref:System.ServiceModel.ServiceAuthorizationManager>에서 파생되어야 하며, 여기서 `AccessCheck()` 메서드만 재정의해야 합니다. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 서비스 작업이 호출될 때마다 이 메서드를 호출하여 <xref:System.ServiceModel.OperationContext> 개체를 제공하며, 이 개체의 `ServiceSecurityContext.AuthorizationContext` 속성에는 사용자에 대한 클레임이 있습니다. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]는 사용자가 인증을 위해 제공한 보안 토큰으로부터 사용자에 대한 클레임을 조합하는 작업을 수행하므로 이러한 클레임이 해당 작업에 충분한지 여부를 평가하는 간단한 작업만 남게 됩니다.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 모든 종류의 보안 토큰으로부터 클레임을 자동으로 조합합니다. 그러면 클레임 기반 권한 부여 코드가 인증 메커니즘으로부터 완전히 독립되므로 이는 매우 중요한 혁신 중 하나입니다. 반면 ASP.NET에서 ACL 또는 역할을 사용하는 권한 부여는 Windows 인증과 밀접하게 연결됩니다.  
  
### <a name="security-confidentiality"></a>보안: 기밀성  
 IIS에서 응용 프로그램이 HTTPS(Secure Hypertext Transfer Protocol)를 사용하도록 구성하여 ASP.NET 웹 서비스와 교환되는 메시지의 기밀성을 전송 수준에서 보장할 수 있습니다. IIS에서 호스트되는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 응용 프로그램에 대해서도 마찬가지입니다. IIS 외부에서 호스트되는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 응용 프로그램도 보안 전송 프로토콜을 사용하도록 구성할 수 있습니다. 또한 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 응용 프로그램에서 WS-Security 프로토콜을 사용하여 메시지가 전송되기 전에 보안하도록 구성할 수 있습니다. WS-Security를 사용하여 메시지 본문의 보안을 유지하면 메시지가 최종 목적지에 도달하기 전에 중간 단계를 통해 기밀 상태로 전송할 수 있습니다.  
  
## <a name="globalization"></a>전역화  
 ASP.NET 구성 언어를 사용하여 개별 서비스의 문화권을 지정할 수 있습니다. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 ASP.NET 호환 모드인 경우를 제외하고 이러한 구성 설정을 지원하지 않습니다. ASP.NET 호환 모드를 사용하지 않는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스를 지역화하려면 서비스 유형을 문화권별 어셈블리로 컴파일하고 각 문화권별 어셈블리가 별도의 문화권별 끝점을 갖도록 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [용도와 사용되는 표준을 기반으로 ASP.NET 웹 서비스와 WCF 비교](../../../../docs/framework/wcf/feature-details/comparing-aspnet-web-services-to-wcf-based-on-purpose-and-standards-used.md)
