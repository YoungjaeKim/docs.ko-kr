---
title: '방법: 기본 Windows Communication Foundation 서비스 호스트 및 실행'
ms.date: 03/30/2017
ms.prod: .net-framework
ms.technology:
- dotnet-clr
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF services [WCF]
- WCF services [WCF], running
ms.assetid: 31774d36-923b-4e2d-812e-aa190127266f
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 1e1c00abfec36622f5da493165259fb1786ab8d6
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="how-to-host-and-run-a-basic-windows-communication-foundation-service"></a>방법: 기본 Windows Communication Foundation 서비스 호스트 및 실행
이 작업은 기본 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 응용 프로그램을 만드는 데 필요한 6가지 작업 중 세 번째 작업입니다. 모든 6 가지 작업의 개요를 참조 하십시오.는 [초보자를 위한 자습서](../../../docs/framework/wcf/getting-started-tutorial.md) 항목입니다.  
  
 이 항목에서는 콘솔 응용 프로그램에서 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 서비스를 호스팅하는 방법에 대해 설명합니다. 이 절차는 다음 단계로 구성됩니다.  
  
-   서비스를 호스팅할 콘솔 응용 프로그램 프로젝트를 만듭니다.  
  
-   서비스에 대한 서비스 호스트를 만듭니다.  
  
-   메타데이터 교환을 사용하도록 설정합니다.  
  
-   서비스 호스트를 엽니다.  
  
 이 작업에서 작성된 전체 코드 목록은 이 절차 다음에 나오는 다음 예제에 제공되어 있습니다.  
  
## <a name="to-create-a-new-console-application-to-host-the-service"></a>서비스를 호스팅할 새 콘솔 응용 프로그램을 만들려면  
  
1.  선택 하면, Getting Started 솔루션을 마우스 오른쪽 단추로 클릭 하 여 새 콘솔 응용 프로그램 프로젝트 만들기 **추가**, **새 프로젝트**합니다. 에 **새 프로젝트 추가** 대화에서 대화 선택의 왼쪽 **Windows** 아래 **C#** 또는 **VB**합니다. 선택 대화 상자 가운데에서 **콘솔 응용 프로그램**합니다. 프로젝트 이름으로 GettingStartedHost를 지정합니다.  
  
2.  마우스 오른쪽 단추로 클릭 하 여 GettingStartedHost 프로젝트의 대상 프레임 워크로.NET Framework 4.5로 설정 **GettingStartedHost** 솔루션 탐색기에서 선택 하 고 **속성**합니다. 드롭다운 목록에서 레이블이 **대상 프레임 워크** 선택 **.NET Framework 4.5**합니다. VB 프로젝트는 약간 다릅니다. GettingStartedHost 프로젝트 속성 대화 상자에서 대상 프레임 워크를 설정를 클릭 하 고 **컴파일** 화면 왼쪽에 탭을 클릭 한 다음는 **고급 컴파일 옵션** 대화 상자의 왼쪽 아래 모퉁이에 있는 단추입니다. 그런 다음 선택 **.NET Framework 4.5** 드롭다운 상자에서 **대상 프레임 워크**합니다.  
  
     설정의 대상 프레임 워크 하면 [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] 를 눌러 솔루션을 다시 로드 **확인** 대화 상자가 나타나면 합니다.  
  
3.  마우스 오른쪽 단추로 클릭 하 여 GettingStartedLib 프로젝트에 대 한 참조를 GettingStartedHost 프로젝트에 추가 된 **참조** 고 솔루션 탐색기에서 GettingStartedHost 프로젝트의 폴더 **참조 추가** . 에 **참조 추가** 대화 상자에서 **솔루션** 대화 및 대화 상자와 클릭의 가운데에서 GettingStartedLib를 선택의 왼쪽에 **추가**합니다. 이제 GettingStartedLib에 정의된 형식을 GettingStartedHost 프로젝트에서 사용할 수 있습니다.  
  
4.  마우스 오른쪽 단추로 클릭 하 여 System.ServiceModel에 대 한 참조를 GettingStartedHost 프로젝트에 추가 된 **참조** 선택 솔루션 탐색기에서 GettingStartedHost 프로젝트의 폴더 **추가** 참조입니다. 에 **참조 추가** 대화 선택 **프레임 워크** 대화 상자의 왼쪽에 있습니다. 검색 어셈블리 텍스트 상자에 `System.ServiceModel`을 입력합니다. 선택 대화 상자 가운데에서 **System.ServiceModel**, 클릭는 **추가** 단추를 클릭 하 고는 **닫기** 단추입니다. 주 메뉴에서 모두 저장 단추를 클릭하여 솔루션을 저장합니다.  
  
### <a name="to-host-the-service"></a>서비스를 호스트하려면  
  
-   편집할 Program.cs 또는 Module.vb 파일을 열고 다음 코드를 입력합니다.  
  
    ```csharp
    // program.cs  
    using System;  
    using System.Collections.Generic;  
    using System.Linq;  
    using System.Text;  
    using System.ServiceModel;  
    using GettingStartedLib;  
    using System.ServiceModel.Description;   
  
    namespace GettingStartedHost  
    {  
        class Program  
        {  
            static void Main(string[] args)  
            {  
                // Step 1 Create a URI to serve as the base address.  
                Uri baseAddress = new Uri("http://localhost:8000/GettingStarted/");  
  
                // Step 2 Create a ServiceHost instance  
                ServiceHost selfHost = new ServiceHost(typeof(CalculatorService), baseAddress);  
  
                try  
                {  
                    // Step 3 Add a service endpoint.  
                    selfHost.AddServiceEndpoint(typeof(ICalculator), new WSHttpBinding(), "CalculatorService");  
  
                    // Step 4 Enable metadata exchange.  
                    ServiceMetadataBehavior smb = new ServiceMetadataBehavior();  
                    smb.HttpGetEnabled = true;  
                    selfHost.Description.Behaviors.Add(smb);  
  
                    // Step 5 Start the service.  
                    selfHost.Open();  
                    Console.WriteLine("The service is ready.");  
                    Console.WriteLine("Press <ENTER> to terminate service.");  
                    Console.WriteLine();  
                    Console.ReadLine();  
  
                    // Close the ServiceHostBase to shutdown the service.  
                    selfHost.Close();  
                }  
                catch (CommunicationException ce)  
                {  
                    Console.WriteLine("An exception occurred: {0}", ce.Message);  
                    selfHost.Abort();  
                }  
            }  
        }  
    }  
    ```  
  
    ```vb
    'Module1.vb  
    Imports System  
    Imports System.ServiceModel  
    Imports System.ServiceModel.Description  
    Imports GettingStartedLibVB.GettingStartedLib  
  
    Module Service  
  
        Class Program  
            Shared Sub Main()  
                ' Step 1 Create a URI to serve as the base address  
                Dim baseAddress As New Uri("http://localhost:8000/ServiceModelSamples/Service")  
  
                ' Step 2 Create a ServiceHost instance  
                Dim selfHost As New ServiceHost(GetType(CalculatorService), baseAddress)  
                Try  
  
                    ' Step 3 Add a service endpoint  
                    ' Add a service endpoint  
                    selfHost.AddServiceEndpoint( _  
                        GetType(ICalculator), _  
                        New WSHttpBinding(), _  
                        "CalculatorService")  
  
                    ' Step 4 Enable metadata exchange.  
                    Dim smb As New ServiceMetadataBehavior()  
                    smb.HttpGetEnabled = True  
                    selfHost.Description.Behaviors.Add(smb)  
  
                    ' Step 5 Start the service  
                    selfHost.Open()  
                    Console.WriteLine("The service is ready.")  
                    Console.WriteLine("Press <ENTER> to terminate service.")  
                    Console.WriteLine()  
                    Console.ReadLine()  
  
                    ' Close the ServiceHostBase to shutdown the service.  
                    selfHost.Close()  
                Catch ce As CommunicationException  
                    Console.WriteLine("An exception occurred: {0}", ce.Message)  
                    selfHost.Abort()  
                End Try  
            End Sub  
        End Class  
  
    End Module  
    ```  
  
    1.  1단계 - 서비스의 기본 주소를 보유할 URI 클래스의 인스턴스를 만듭니다. 서비스는 기본 주소와 선택적 URI를 포함하는 URL로 식별됩니다. 기본 주소 형식은 다음과 같습니다: [전송]:// [컴퓨터 이름 또는 도메인] [: 선택적 포트 번호] / [선택적 URI 세그먼트] 계산기 서비스에 대 한 기본 주소는 HTTP 전송을 사용 하 여 로컬 호스트, 포트 8000 및 URI 세그먼트 "GettingStarted",  
  
    2.  2단계 - 서비스를 호스팅할 <xref:System.ServiceModel.ServiceHost> 클래스의 인스턴스를 만듭니다. 생성자는 서비스 계약을 구현하는 클래스 형식과 서비스의 기본 주소, 두 가지 매개 변수를 사용합니다.  
  
    3.  3 단계-만듭니다는 <!--zz <xref:System.ServiceModel.ServiceEndpoint>--> ` System.ServiceModel.ServiceEndpoint` 인스턴스. 서비스 끝점은 주소, 바인딩 및 서비스 계약으로 구성되어 있습니다. <!--zz <xref:System.ServiceModel.ServiceEndpoint>--> ` System.ServiceModel.ServiceEndpoint` 생성자 따라서 서비스 계약 인터페이스 형식, 바인딩 및 주소를 사용 합니다. 서비스 계약은 사용자가 정의한 `ICalculator`이며 서비스 형식에 구현합니다. 이 예제에 사용된 바인딩은 WS-* 사양을 따르는 끝점에 연결하는 데 사용되는 기본 바인딩인 <xref:System.ServiceModel.WSHttpBinding>입니다. WCF 바인딩에 대 한 자세한 내용은 참조 하십시오. [WCF 바인딩 개요](../../../docs/framework/wcf/bindings-overview.md)합니다. 끝점을 식별하기 위해 주소가 기본 주소에 추가됩니다. 이 코드에 지정 된 주소는 "CalculatorService" 끝점에 대 한 정규화 된 주소 이므로 `"http://localhost:8000/GettingStarted/CalculatorService"` .NET Framework 4.0을 사용 하는 경우 선택적 이상을 서비스 끝점을 추가 합니다. 이러한 버전에서 코드 또는 구성에 끝점이 추가되지 않으면 WCF가 기본 주소의 각 결합에 기본 끝점 하나씩을 추가하고 서비스에서 구현한 계약을 추가합니다. 기본에 대 한 자세한 내용은 끝점 참조 [끝점 주소 지정](../../../docs/framework/wcf/specifying-an-endpoint-address.md)합니다. [!INCLUDE[crabout](../../../includes/crabout-md.md)] , [Simplified Configuration](../../../docs/framework/wcf/simplified-configuration.md) 및 [Simplified Configuration for WCF Services](../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).  
  
        > [!IMPORTANT]
        >  .NET Framework 4 이상을 사용할 때 서비스 끝점 추가는 선택 사항입니다. 이러한 버전에서 코드 또는 구성에 끝점이 추가되지 않으면 WCF가 기본 주소의 각 결합에 기본 끝점 하나씩을 추가하고 서비스에서 구현한 계약을 추가합니다. 기본에 대 한 자세한 내용은 끝점 참조 [끝점 주소 지정](../../../docs/framework/wcf/specifying-an-endpoint-address.md)합니다. [!INCLUDE[crabout](../../../includes/crabout-md.md)] , [Simplified Configuration](../../../docs/framework/wcf/simplified-configuration.md) 및 [Simplified Configuration for WCF Services](../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).  
  
    4.  4단계 - 메타데이터 교환을 사용하도록 설정합니다. 클라이언트는 메타데이터 교환을 사용하여 서비스 작업을 호출하는 데 사용되는 프록시를 생성합니다. 메타 데이터 교환을 만들 수 있도록는 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 인스턴스를 설정의 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A> 속성을 `true`, 동작을 추가 하 고는 <!--zz <xref:System.ServiceModel.ServiceHost.Behaviors%2A>  --> `System.ServiceModel.ServiceHost.Behaviors%2A` 의 컬렉션은 <xref:System.ServiceModel.ServiceHost> 인스턴스.  
  
    5.  5단계 - <xref:System.ServiceModel.ServiceHost>를 열어 들어오는 메시지를 수신합니다. 코드는 사용자가 Enter를 누를 때까지 기다립니다. 이를 수행하지 않으면 응용 프로그램이 즉시 닫히고 서비스가 종료합니다. 또한 사용된 try/catch 블록도 주의하십시오. <xref:System.ServiceModel.ServiceHost>를 인스턴스화한 후에는 나머지 코드가 try/catch 블록에 배치됩니다. 안전 하 게에서 throw 된 예외를 catch 하는 방법에 대 한 자세한 내용은 <xref:System.ServiceModel.ServiceHost>, 참조 [Using 문과 문제 방지](../../../docs/framework/wcf/samples/avoiding-problems-with-the-using-statement.md)  
  
### <a name="to-verify-the-service-is-working"></a>서비스가 작동하는지 확인하려면  
  
1.  [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)]에서 GettingStartedHost 콘솔 응용 프로그램을 실행합니다. [!INCLUDE[wv](../../../includes/wv-md.md)]에서 실행하면서 나중에 운영 체제에서 실행하는 경우 서비스를 관리자 권한으로 실행해야 합니다. [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)]가 관리자 권한으로 실행되었기 때문에 GettingStartedHost도 관리자 권한으로 실행됩니다. 또한 관리자 권한으로 서비스를 실행하는 새 명령 프롬프트를 시작하고 해당 명령 프롬프트 내에서 service.exe를 실행할 수 있습니다.  
  
2.  Internet Explorer를 열고 서비스의 디버그 페이지인 `http://localhost:8000/GettingStarted/CalculatorService`를 찾습니다.  
  
## <a name="example"></a>예제  
 다음 예제에는 자습서의 이전 단계의 서비스 계약과 구현이 포함되어 있으며 콘솔 응용 프로그램에서 서비스를 호스팅합니다.  
  
 이 명령줄 컴파일러로 컴파일하려면 IService1.cs 및 Service1.cs로 컴파일 클래스 라이브러리 참조 `System.ServiceModel.dll`합니다. 그리고 Program.cs를 콘솔 응용 프로그램으로 컴파일합니다.  
  
```csharp
// IService1.cs  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Runtime.Serialization;  
using System.ServiceModel;  
using System.Text;  
  
namespace GettingStartedLib  
{  
        [ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples")]  
        public interface ICalculator  
        {  
            [OperationContract]  
            double Add(double n1, double n2);  
            [OperationContract]  
            double Subtract(double n1, double n2);  
            [OperationContract]  
            double Multiply(double n1, double n2);  
            [OperationContract]  
            double Divide(double n1, double n2);  
        }  
}  
```  
  
```csharp
// Service1.cs  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Runtime.Serialization;  
using System.ServiceModel;  
using System.Text;  
  
namespace GettingStartedLib  
{  
    public class CalculatorService : ICalculator  
    {  
        public double Add(double n1, double n2)  
        {  
            double result = n1 + n2;  
            Console.WriteLine("Received Add({0},{1})", n1, n2);  
            // Code added to write output to the console window.  
            Console.WriteLine("Return: {0}", result);  
            return result;  
        }  
  
        public double Subtract(double n1, double n2)  
        {  
            double result = n1 - n2;  
            Console.WriteLine("Received Subtract({0},{1})", n1, n2);  
            Console.WriteLine("Return: {0}", result);  
            return result;  
        }  
  
        public double Multiply(double n1, double n2)  
        {  
            double result = n1 * n2;  
            Console.WriteLine("Received Multiply({0},{1})", n1, n2);  
            Console.WriteLine("Return: {0}", result);  
            return result;  
        }  
  
        public double Divide(double n1, double n2)  
        {  
            double result = n1 / n2;  
            Console.WriteLine("Received Divide({0},{1})", n1, n2);  
            Console.WriteLine("Return: {0}", result);  
            return result;  
        }  
    }  
}  
```  
  
```csharp
//Program.cs  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.ServiceModel;  
using GettingStartedLib;  
using System.ServiceModel.Description;   
  
namespace GettingStartedHost  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            // Step 1 of the address configuration procedure: Create a URI to serve as the base address.  
            Uri baseAddress = new Uri("http://localhost:8000/ServiceModelSamples/Service");  
  
            // Step 2 of the hosting procedure: Create ServiceHost  
            ServiceHost selfHost = new ServiceHost(typeof(CalculatorService), baseAddress);  
  
            try  
            {  
                // Step 3 of the hosting procedure: Add a service endpoint.  
                selfHost.AddServiceEndpoint(typeof(ICalculator), new WSHttpBinding(), "CalculatorService");  
  
                // Step 4 of the hosting procedure: Enable metadata exchange.  
                ServiceMetadataBehavior smb = new ServiceMetadataBehavior();  
                smb.HttpGetEnabled = true;  
                selfHost.Description.Behaviors.Add(smb);  
  
                // Step 5 of the hosting procedure: Start (and then stop) the service.  
                selfHost.Open();  
                Console.WriteLine("The service is ready.");  
                Console.WriteLine("Press <ENTER> to terminate service.");  
                Console.WriteLine();  
                Console.ReadLine();  
  
                // Close the ServiceHostBase to shutdown the service.  
                selfHost.Close();  
            }  
            catch (CommunicationException ce)  
            {  
                Console.WriteLine("An exception occurred: {0}", ce.Message);  
                selfHost.Abort();  
            }  
        }  
    }  
}  
```  
  
```vb
'IService1.vb  
Imports System  
Imports System.ServiceModel  
  
Namespace GettingStartedLib  
  
    <ServiceContract(Namespace:="http://Microsoft.ServiceModel.Samples")> _  
    Public Interface ICalculator  
  
        <OperationContract()> _  
        Function Add(ByVal n1 As Double, ByVal n2 As Double) As Double  
        <OperationContract()> _  
        Function Subtract(ByVal n1 As Double, ByVal n2 As Double) As Double  
        <OperationContract()> _  
        Function Multiply(ByVal n1 As Double, ByVal n2 As Double) As Double  
        <OperationContract()> _  
        Function Divide(ByVal n1 As Double, ByVal n2 As Double) As Double  
    End Interface  
End Namespace  
```  
  
```vb
'Service1.vb  
Imports System  
Imports System.ServiceModel  
  
Namespace GettingStartedLib  
  
    Public Class CalculatorService  
        Implements ICalculator  
  
        Public Function Add(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Add  
            Dim result As Double = n1 + n2  
            ' Code added to write output to the console window.  
            Console.WriteLine("Received Add({0},{1})", n1, n2)  
            Console.WriteLine("Return: {0}", result)  
            Return result  
        End Function  
  
        Public Function Subtract(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Subtract  
            Dim result As Double = n1 - n2  
            Console.WriteLine("Received Subtract({0},{1})", n1, n2)  
            Console.WriteLine("Return: {0}", result)  
            Return result  
  
        End Function  
  
        Public Function Multiply(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Multiply  
            Dim result As Double = n1 * n2  
            Console.WriteLine("Received Multiply({0},{1})", n1, n2)  
            Console.WriteLine("Return: {0}", result)  
            Return result  
  
        End Function  
  
        Public Function Divide(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Divide  
            Dim result As Double = n1 / n2  
            Console.WriteLine("Received Divide({0},{1})", n1, n2)  
            Console.WriteLine("Return: {0}", result)  
            Return result  
  
        End Function  
    End Class  
End Namespace  
```  
  
```vb
'Module1.vb  
Imports System  
Imports System.ServiceModel  
Imports System.ServiceModel.Description  
Imports GettingStartedLibVB.GettingStartedLib  
  
Module Service  
  
    Class Program  
        Shared Sub Main()  
            ' Step 1 of the address configuration procedure: Create a URI to serve as the base address.  
            Dim baseAddress As New Uri("http://localhost:8000/ServiceModelSamples/Service")  
  
            ' Step 2 of the hosting procedure: Create ServiceHost  
            Dim selfHost As New ServiceHost(GetType(CalculatorService), baseAddress)  
            Try  
  
                ' Step 3 of the hosting procedure: Add a service endpoint.  
                ' Add a service endpoint  
                selfHost.AddServiceEndpoint( _  
                    GetType(ICalculator), _  
                    New WSHttpBinding(), _  
                    "CalculatorService")  
  
                ' Step 4 of the hosting procedure: Enable metadata exchange.  
                ' Enable metadata exchange  
                Dim smb As New ServiceMetadataBehavior()  
                smb.HttpGetEnabled = True  
                selfHost.Description.Behaviors.Add(smb)  
  
                ' Step 5 of the hosting procedure: Start (and then stop) the service.  
                selfHost.Open()  
                Console.WriteLine("The service is ready.")  
                Console.WriteLine("Press <ENTER> to terminate service.")  
                Console.WriteLine()  
                Console.ReadLine()  
  
                ' Close the ServiceHostBase to shutdown the service.  
                selfHost.Close()  
            Catch ce As CommunicationException  
                Console.WriteLine("An exception occurred: {0}", ce.Message)  
                selfHost.Abort()  
            End Try  
        End Sub  
    End Class  
  
End Module  
```  
  
> [!NOTE]
>  이러한 서비스에는 수신 대기를 위해 시스템에 HTTP 주소를 등록할 권한이 있어야 합니다. 관리자 계정에는 이 권한이 있지만, 관리자 이외의 계정에는 HTTP 네임스페이스에 대한 권한을 부여해야 합니다. [!INCLUDE[crabout](../../../includes/crabout-md.md)] 네임 스페이스 예약을 구성을 참조 하는 방법 [HTTP 및 HTTPS 구성](../../../docs/framework/wcf/feature-details/configuring-http-and-https.md)합니다. [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)]에서 실행하는 경우 service.exe는 관리자 권한으로 실행해야 합니다.  
  
 서비스가 실행되고 있습니다. 진행 [하는 방법: 클라이언트 만들기](../../../docs/framework/wcf/how-to-create-a-wcf-client.md)합니다. 문제 해결 정보를 참조 하세요. [초보자를 위한 자습서 문제 해결](../../../docs/framework/wcf/troubleshooting-the-getting-started-tutorial.md)합니다.  
  
## <a name="see-also"></a>참고 항목  
 [시작](../../../docs/framework/wcf/samples/getting-started-sample.md)  
 [자체 호스팅](../../../docs/framework/wcf/samples/self-host.md)
