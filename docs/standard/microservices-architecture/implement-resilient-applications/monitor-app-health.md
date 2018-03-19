---
title: "상태 모니터링"
description: "컨테이너화된 .NET 응용 프로그램용 .NET 마이크로 서비스 아키텍처 | 상태 모니터링"
keywords: "Docker, 마이크로 서비스, ASP.NET, 컨테이너"
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 12/11/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.topic: article
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 76821e27613335609527b867a6b94dac551f6235
ms.sourcegitcommit: 15316053918995cc1380163a7d7e7edd5c44e6d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2018
---
# <a name="health-monitoring"></a>상태 모니터링

상태 모니터링은 컨테이너 및 마이크로 서비스의 상태에 대해 거의 실시간으로 정보를 제공할 수 있습니다. 상태 모니터링은 마이크로 서비스를 작동하는 데 있어 여러 가지 측면에서 매우 중요하며, 나중에 설명하는 대로 오케스트레이터에서 응용 프로그램을 부분적으로 업그레이드할 때 특히 중요합니다.

마이크로 서비스 기반 응용 프로그램은 종종 하트비트 또는 상태 검사를 사용하여 성능 모니터, 스케줄러 및 오케스트레이터에서 다양한 서비스를 추적할 수 있도록 합니다. 서비스에서 요구 시 또는 일정에 따라 "활성(I’m alive)" 신호를 보낼 수 없는 경우, 업데이트를 배포할 때 응용 프로그램이 위험에 직면할 수 있고, 단순히 오류를 너무 늦게 감지하여 연속 오류를 방지할 수 없음으로써 심각한 중단 상태에 놓일 수도 있습니다.

일반적인 모델에서 서비스는 상태에 대한 보고서를 보내고, 해당 정보를 집계하여 응용 프로그램 상태 전체에 대한 보기를 제공합니다. 오케스트레이터를 사용하는 경우 클러스터가 적절하게 작동할 수 있도록 오케스트레이터의 클러스터에 상태 정보를 제공할 수 있습니다. 응용 프로그램에 맞게 사용자 지정된 고품질 상태 보고에 투자하는 경우 실행 중인 응용 프로그램에 대한 문제를 훨씬 쉽게 검색하고 해결할 수 있습니다.

## <a name="implementing-health-checks-in-aspnet-core-services"></a>ASP.NET Core 서비스에서 상태 검사 구현

ASP.NET Core 마이크로 서비스 또는 웹 응용 프로그램을 개발할 때 ASP.NET 팀에서 `HealthChecks`라는 라이브러리를 사용할 수 있습니다. 초기 릴리스는 이 [GitHub 리포지토리](https://github.com/dotnet-architecture/HealthChecks)에서 사용할 수 있습니다.

이 라이브러리는 사용하기 쉽고 응용 프로그램에 필요한 특정 외부 리소스(예: SQL Server 데이터베이스 또는 원격 API)가 사용할 수 있습니다. 작동하는지 확인할 수 있는 기능을 제공합니다. 이 라이브러리를 사용하면 나중에 설명하는 대로 정상 리소스에 대한 의미를 결정할 수도 있습니다.

이 라이브러리를 사용하려면 먼저 마이크로 서비스에서 라이브러리를 사용해야 합니다. 다음으로, 상태 보고서를 쿼리하는 프런트 엔드 응용 프로그램이 필요합니다. 프런트 엔드 응용 프로그램은 사용자 지정 보고 응용 프로그램이거나 성능 상태에 따라 대응할 수 있는 오케스트레이터 자체일 수 있습니다.

### <a name="using-the-healthchecks-library-in-your-back-end-aspnet-microservices"></a>백 엔드 ASP.NET 마이크로 서비스에서 HealthChecks 라이브러리 사용

eShopOnContainers 샘플 응용 프로그램에서 HealthChecks 라이브러리가 사용되는 방식을 확인할 수 있습니다. 시작하려면 각 마이크로 서비스에 대한 성능 상태를 구성하는 항목을 정의해야 합니다. 샘플 응용 프로그램에서 마이크로 서비스 API가 HTTP를 통해 액세스할 수 있고 관련 SQL Server 데이터베이스도 사용할 수 있으면 마이크로 서비스가 정상입니다.

나중에 HealthChecks 라이브러리를 NuGet 패키지로 설치할 수 있습니다. 그러나 이 문서를 작성한 시점 이후로는 코드를 솔루션의 일부로 다운로드하고 컴파일해야 합니다. 복제에 사용할 수 있는 코드가 https://github.com/dotnet-architecture/HealthChecks 솔루션을 다음 폴더에 복사 합니다.

  - src/common
  - src/Microsoft.AspNetCore.HealthChecks
  - src/Microsoft.Extensions.HealthChecks
  - src/Microsoft.Extensions.HealthChecks.SqlServer

Azure(Microsoft.Extensions.HealthChecks.AzureStorage)에 대한 것과 같은 추가 검사를 사용할 수도 있지만, 이 버전의 eShopOnContainers에는 Azure에 대한 종속성이 없으므로 이러한 검사는 필요하지 않습니다. eShopOnContainers는 ASP.NET Core를 기반으로 하므로 ASP.NET 상태 검사가 필요하지 않습니다.

그림 10-6에서는 모든 마이크로 서비스에서 구성 요소로 사용할 준비가 된 Visual Studio의 HealthChecks 라이브러리를 보여 줍니다.

![](./media/image6.png)

**그림 10-6** Visual Studio 솔루션의 ASP.NET Core HealthChecks 라이브러리 소스 코드

앞에서 소개한 대로 각 마이크로 서비스 프로젝트에서 가장 먼저 수행할 작업은 세 가지 HealthChecks 라이브러리에 대한 참조를 추가하는 것입니다. 그런 다음, 해당 마이크로 서비스에서 수행하려는 상태 검사 작업을 추가합니다. 이러한 작업은 기본적으로 다른 마이크로 서비스(HttpUrlCheck) 또는 데이터베이스(현재의 SQL Server 데이터베이스에 대한 SqlCheck\*)에 종속됩니다. 작업은 각 ASP.NET 마이크로 서비스 또는 ASP.NET 웹 응용 프로그램의 Startup 클래스 내에 추가합니다.

각 서비스 또는 웹 응용 프로그램은 HTTP 또는 데이터베이스 종속성을 모두 하나의 AddHealthCheck 메서드로 추가하여 구성해야 합니다. 예를 들어 eShopOnContainers의 MVC 웹 응용 프로그램은 여러 서비스에 종속되므로 상태 검사에 몇 가지 AddCheck 메서드가 추가됩니다.

예를 들어 다음 코드에서 카탈로그 마이크로 서비스가 SQL Server 데이터베이스에 대한 종속성을 추가하는 방법을 확인할 수 있습니다.

```csharp
// Startup.cs from Catalog.api microservice
//
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        // Add framework services
        services.AddHealthChecks(checks =>
        {
            checks.AddSqlCheck("CatalogDb", Configuration["ConnectionString"]);
        });
        // Other services
    }
}
```

그러나 eShopOnContainers의 MVC 웹 응용 프로그램에는 나머지 마이크로 서비스에 대한 여러 종속성이 있습니다. 따라서 다음 예제와 같이 각 마이크로 서비스에 대해 하나의 AddUrlCheck 메서드를 호출합니다.

```csharp
// Startup.cs from the MVC web app
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddMvc();
        services.Configure<AppSettings>(Configuration);
        services.AddHealthChecks(checks =>
        {
            checks.AddUrlCheck(Configuration["CatalogUrl"]);
            checks.AddUrlCheck(Configuration["OrderingUrl"]);
            checks.AddUrlCheck(Configuration["BasketUrl"]);
            checks.AddUrlCheck(Configuration["IdentityUrl"]);
        });
    }
}
```

따라서 마이크로 서비스는 모든 검사가 정상일 때까지 "정상" 상태를 제공하지 않습니다.

마이크로 서비스가 서비스 또는 SQL Server에 종속되지 않으면 정상("OK") 검사를 추가해야 합니다. 다음 코드는 eShopOnContainers basket.api 마이크로 서비스에서 제공합니다. (장바구니 마이크로 서비스에서 Redis 캐시를 사용하지만, 라이브러리에는 아직 Redis 상태 검사 공급자가 포함되어 있지 않습니다.)

```csharp
services.AddHealthChecks(checks =>
{
    checks.AddValueTaskCheck("HTTP Endpoint", () => new
        ValueTask<IHealthCheckResult>(HealthCheckResult.Healthy("Ok")));
});
```

서비스 또는 웹 응용 프로그램에서 상태 검사 엔드포인트를 공개하려면 UseHealthChecks(\[*url\_for\_health\_checks*\]) 확장 메서드를 사용하도록 설정해야 합니다. 이 메서드는 아래 코드와 같이 UseKestrel 바로 뒤에 ASP.NET Core 서비스 또는 웹 응용 프로그램의 Program 클래스의 main 메서드에서 WebHostBuilder 수준으로 이동합니다.

```csharp
namespace Microsoft.eShopOnContainers.WebMVC
{
    public class Program
    {
        public static void Main(string[] args)
        {
            var host = new WebHostBuilder()
                .UseKestrel()
                .UseHealthChecks("/hc")
                .UseContentRoot(Directory.GetCurrentDirectory())
                .UseIISIntegration()
                .UseStartup<Startup>()
                .Build();
            host.Run();
        }
    }
}
```

프로세스는 다음과 같이 작동합니다. 각 마이크로 서비스에서 /hc 엔드포인트를 공개합니다. 이 엔드포인트는 HealthChecks 라이브러리 ASP.NET Core 미들웨어에서 만들어집니다. 해당 엔드포인트가 호출되면 Startup 클래스의 AddHealthChecks 메서드에 구성된 상태 검사를 모두 실행합니다.

UseHealthChecks 메서드에는 포트 또는 경로가 필요합니다. 해당 포트 또는 경로는 서비스의 성능 상태를 확인하는 데 사용할 엔드포인트입니다. 예를 들어 카탈로그 마이크로 서비스는/hc 경로를 사용합니다.

### <a name="caching-health-check-responses"></a>상태 검사 응답 캐싱

서비스에서 DoS(서비스 거부) 공격이 발생하지 않도록 하려거나 단순히 리소스를 너무 자주 검사하여 서비스 성능에 영향을 미치지 않으려고 하는 경우에는 각 상태 검사에 대해 반환을 캐시하고 캐시 기간을 구성할 수 있습니다.

기본적으로 캐시 기간은 내부적으로 5분으로 설정되지만, 다음 코드와 같이 각 상태 검사에 대한 해당 캐시 기간을 변경할 수 있습니다.

```csharp
checks.AddUrlCheck(Configuration["CatalogUrl"],1); // 1 min as cache duration
```

### <a name="querying-your-microservices-to-report-about-their-health-status"></a>마이크로 서비스를 쿼리하여 성능 상태에 대해 보고

여기서 설명한 대로 상태 검사를 구성한 경우 Docker에서 마이크로 서비스가 실행되면 브라우저에서 정상인지 여부를 직접 확인할 수 있습니다. (이 경우 컨테이너 포트를 Docker 호스트 외부에 게시해야 localhost 또는 외부 Docker 호스트 IP를 통해 컨테이너에 액세스할 수 있습니다.) 그림 10-7에서는 브라우저의 요청과 해당 응답을 보여 줍니다.

![](./media/image7.png)

**그림 10-7** 브라우저에서 단일 서비스의 성능 상태 검사

이 테스트에서는 catalog.api 마이크로 서비스(5101 포트에서 실행 중)가 정상이며, JSON에서 200 HTTP 상태 및 상태 정보를 반환한다는 것을 확인할 수 있습니다. 또한 이 서비스는 내부적으로 SQL Server 데이터베이스 종속성의 상태를 검사했고 상태 검사에서 직접 정상으로 보고되었음을 의미합니다.

## <a name="using-watchdogs"></a>Watchdog 사용

Watchdog은 앞에서 소개한 HealthChecks 라이브러리로 쿼리하여 서비스 전반의 상태와 로드를 감시하고 마이크로 서비스에 대한 상태를 보고할 수 있는 별도의 서비스입니다. 이렇게 하면 단일 서비스의 보기를 기반으로 하여 검색되지 않는 오류를 방지할 수 있습니다. 또한 Watchdog은 사용자 개입 없이 알려진 조건에 대한 수정 작업을 수행할 수 있는 코드를 호스팅하는 데 적합한 위치입니다.

eShopOnContainers 샘플에는 그림 10-8과 같이 샘플 상태 검사 보고서를 표시하는 웹 페이지가 포함되어 있습니다. 이는 단지 eShopOnContainers에서 마이크로 서비스 및 웹 응용 프로그램의 상태를 보여 줄 뿐이므로 가장 간단한 Watchdog입니다. 일반적으로 비정상 상태가 검색되면 Watchdog에서 작업을 수행합니다.

![](./media/image8.png)

**그림 10-8** eShopOnContainers의 샘플 상태 검사 보고서

요약하면, ASP.NET Core HealthChecks 라이브러리의 ASP.NET 미들웨어는 각 마이크로 서비스에 대해 단일 상태 검사 엔드포인트를 제공합니다. 이렇게 하면 내부에 정의된 모든 상태 검사가 실행되고, 모든 검사에 따라 전체 성능 상태가 반환됩니다.

HealthChecks 라이브러리는 향후 외부 리소스에 대한 새로운 상태 검사를 통해 확장할 수 있습니다. 예를 들어 나중에 Redis 캐시 및 다른 데이터베이스에 대한 상태 검사가 라이브러리에 제공될 예정입니다. 라이브러리를 사용하면 여러 서비스 또는 응용 프로그램 종속성을 통해 상태를 보고할 수 있고, 이러한 상태 검사에 따라 작업을 수행할 수 있습니다.

## <a name="health-checks-when-using-orchestrators"></a>오케스트레이터 사용 시의 상태 검사

Docker Swarm, Kubernetes 및 Service Fabric과 같은 오케스트레이션은 마이크로 서비스의 가용성을 모니터링하기 위해 정기적으로 마이크로 서비스 테스트 요청을 보내 상태 검사를 수행합니다. 오케스트레이터에서 비정상 서비스/컨테이너로 인식하면 해당 인스턴스에 대한 요청 라우팅을 중지합니다. 또한 일반적으로 해당 컨테이너의 새 인스턴스를 만듭니다.

예를 들어 대부분의 오케스트레이터에서 상태 검사를 사용하여 가동 중지 시간이 없는 배포를 관리할 수 있습니다. 서비스/컨테이너의 상태가 정상으로 변경될 때만 오케스트레이터에서 트래픽을 서비스/컨테이너 인스턴스로 라우팅하기 시작합니다.

상태 모니터링은 오케스트레이터에서 응용 프로그램 업그레이드를 수행할 때 특히 중요합니다. Azure Service Fabric과 같은 일부 오케스트레이터는 서비스를 단계별로 업데이트합니다. 예를 들어 응용 프로그램 업그레이드마다 클러스터 표면의 1/5을 업데이트할 수 있습니다. 동시에 업그레이드되는 노드 집합을 *업그레이드 도메인*이라고 합니다. 각 업그레이드 도메인을 업그레이드하고 사용자가 사용할 수 있게 되면, 먼저 해당 업그레이드 도메인이 상태 검사를 통과한 후에 배포가 다음 업그레이드 도메인으로 이동해야 합니다.

서비스 상태의 또 다른 측면은 서비스의 메트릭을 보고하는 것입니다. 이는 Service Fabric과 같은 일부 오케스트레이터의 상태 모델에 대한 고급 기능입니다. 메트릭은 리소스 사용량의 균형을 조정하는 데 사용되므로 오케스트레이터를 사용할 때 중요합니다. 또한 메트릭은 시스템 상태를 나타내는 지표가 될 수 있습니다. 예를 들어 많은 마이크로 서비스가 있는 응용 프로그램이 있을 수 있으며, 각 인스턴스에서 RPS(초당 요청 수)를 보고합니다. 한 서비스에서 다른 서비스보다 더 많은 리소스(메모리, 프로세서 등)를 사용하는 경우, 오케스트레이터는 클러스터에서 서비스 인스턴스를 이동하여 리소스 사용률을 유지하려고 할 수도 있습니다.

Azure Service Fabric을 사용하는 경우 단순한 상태 검사보다 더 향상된 고급 기능을 갖춘 자체의 [상태 모니터링 모델](https://docs.microsoft.com/azure/service-fabric/service-fabric-health-introduction)을 제공합니다.

## <a name="advanced-monitoring-visualization-analysis-and-alerts"></a>고급 모니터링: 시각화, 분석 및 경고

모니터링의 마지막 부분은 이벤트 스트림을 시각화하고, 서비스 성능에 대해 보고하고, 문제가 검색되면 경고하는 것입니다. 이 모니터링 측면에 대해 서로 다른 솔루션을 사용할 수 있습니다.

[ASP.NET Core HealthChecks](https://github.com/aspnet/HealthChecks)에 대해 설명할 때 보여 준 사용자 지정 페이지와 같이 서비스 상태를 표시하는 간단한 사용자 지정 응용 프로그램을 사용할 수 있습니다. 또는 Azure Application Insights 및 Operations Management Suite와 같은 고급 도구를 사용하여 이벤트 스트림에 따라 경고를 발생시킬 수도 있습니다.

마지막으로 모든 이벤트 스트림을 저장하는 경우 Microsoft Power BI 또는 타사 솔루션(예: Kibana 또는 Splunk)을 사용하여 데이터를 시각화할 수 있습니다.

## <a name="additional-resources"></a>추가 자료

-   **ASP.NET Core HealthChecks** (초기 릴리스) [*https://github.com/aspnet/HealthChecks/*](https://github.com/aspnet/HealthChecks/)

-   **서비스 패브릭 상태 모니터링 소개**
    [*https://docs.microsoft.com/azure/service-fabric/service-fabric-health-introduction*](https://docs.microsoft.com/azure/service-fabric/service-fabric-health-introduction)

-   **Azure 응용 프로그램 통찰력**
    [*https://azure.microsoft.com/services/application-insights/*](https://azure.microsoft.com/services/application-insights/)

-   **Microsoft Operations Management Suite**
    [*https://www.microsoft.com/en-us/cloud-platform/operations-management-suite*](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite)

>[!div class="step-by-step"]
[이전] (implement-circuit-breaker-pattern.md) [다음] (../secure-net-microservices-web-applications/index.md)
