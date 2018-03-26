---
title: ASP.NET Core 서비스 및 웹앱 테스트
description: 컨테이너화된 .NET 응용 프로그램을 위한 .NET 마이크로 서비스 아키텍처 | ASP.NET Core 서비스 및 웹앱 테스트
keywords: Docker, 마이크로 서비스, ASP.NET, 컨테이너
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 12/11/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.topic: article
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 596f588aae8c0814e5b40d29c4bf5723f944c5ac
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2018
---
# <a name="testing-aspnet-core-services-and-web-apps"></a>ASP.NET Core 서비스 및 웹앱 테스트

컨트롤러는 모든 ASP.NET Core MVC 서비스와 ASP.NET MVC Web 응용 프로그램의 핵심 요소입니다. 따라서 응용 프로그램에서 의도한 대로 동작한다고 확신할 수 있어야 합니다. 자동화된 테스트를 통해 이러한 확신을 얻고 오류가 발생하기 전에 미리 검색할 수 있습니다.

컨트롤러가 유효한 입력 또는 무효한 입력을 기반으로 어떻게 동작하는지를 테스트하고 컨트롤러가 수행하는 비즈니스 결과를 바탕으로 컨트롤러 응답을 테스트 해야 합니다. 마이크로 서비스 테스트에는 다음의 유형이 있습니다.

-   단위 테스트. 단위 테스트는 해댱 응용 프로그램의 개별 구성 요소가 예상 대로 작동하는지 확인합니다. 어설션은 구성 요소 API를 테스트합니다.

-   통합 테스트. 통합 테스트는 구성 요소 간 상호 작용이 데이터베이스와 같은 외부 아티팩트에 대해 예상 대로 작동하는지 확인 합니다. 어설션은 구성 요소 API, UI 또는 데이터베이스 I/O, 로깅 등의 작업 부작용을 테스트할 수 있습니다.

-   각 마이크로 서비스에 대한 기능 테스트. 이 테스트는 해당 응용 프로그램이 사용자의 관점에서 예상 대로 작동하는지 확인합니다.

-   서비스 테스트. 이 테스트는 다중 서비스 동시 테스트를 포함하여 종단 간 서비스 사용 사례를 테스트했는지 확인합니다. 이러한 종류의 테스트를 위해서는 먼저 환경을 준비 해야 합니다. 이 경우 준비는 곧 서비스 시작을 의미합니다(예를 들어, docker-compose를 사용하여).

### <a name="implementing-unit-tests-for-aspnet-core-web-apis"></a>ASP.NET Core Web API에 대한 단위 테스트 구현

단위 테스트는 인프라 및 종속성으로부터 격리된 상태에서 응용 프로그램의 일부를 테스트하는 것입니다. 컨트롤러 논리를 단위 테스트하는 경우 단일 작업이나 방법의 콘텐츠만 테스트되고, 종속성 또는 프레임워크 자체의 동작은 테스트되지 않습니다. 단위 테스트는 구성 요소 간의 상호 작용 문제를 검색하지 않습니다. 이 문제는 통합 테스트의 목적입니다.

컨트롤러 작업을 단위 테스트할 때에는 동작에만 집중해야 합니다. 컨트롤러 단위 테스트는 필터, 라우팅, 모델 바인딩 같은 것들이 필요 없습니다. 단위 테스트는 하나를 테스트하는 데 집중하기 때문에 일반적으로 작성 방법이 간단하고 신속하게 실행할 수 있습니다. 잘 작성된 단위 테스트 집합은 많은 오버헤드 없이 자주 실행할 수 있습니다.

단위 테스트는 xUnit.net, MSTest, Moq, NUnit 같은 프레임 워크 테스트를 기반으로 구현됩니다. eShopOnContainers 샘플 응용 프로그램에 대해서는 XUnit 사용하고 있습니다.

Web API 컨트롤러에 대한 단위 테스트를 작성하는 경우 C\#에서 새 키워드를 직접 사용해 컨트롤러 클래스를 인스턴스화함으로써 가능한 한 빨리 테스트를 실행합니다. 다음 예제에서는 테스트 프레임 워크처럼 [XUnit](https://xunit.github.io/)을 사용하는 경우 이 작업을 수행하는 방법을 보여 줍니다.

```csharp
[Fact]
public void Add_new_Order_raises_new_event()
{
    // Arrange
    var street = " FakeStreet ";
    var city = "FakeCity";
    // Other variables omitted for brevity ...
    // Act
    var fakeOrder = new Order(new Address(street, city, state, country, zipcode),
        cardTypeId, cardNumber,
        cardSecurityNumber, cardHolderName,
        cardExpiration);
    // Assert
    Assert.Equal(fakeOrder.DomainEvents.Count, expectedResult);
}
```

### <a name="implementing-integration-and-functional-tests-for-each-microservice"></a>각 마이크로 서비스에 대한 통합 및 기능 테스트 구현

설명한 것 처럼 통합 테스트 및 기능 테스트는 서로 다른 목표 및 목적을 갖고 있습니다. 그러나 ASP.NET Core 컨트롤러를 테스트할 때 목표 및 목적을 구현하는 방법은 비슷하므로 이 절에서는 통합 테스트에 집중하겠습니다.

통합 테스트는 응용 프로그램의 구성 요소가 조합할 때 제대로 작동하는지 확인합니다. ASP.NET Core는 네트워크 오버헤드 없이 요청을 처리하는 데 사용할 수 있는 기본 테스트 웹 호스트 및 단위 테스트 프레임 워크를 사용하는 통합 테스트를 지원합니다.

단위 테스트와 달리 통합 테스트는 데이터베이스, 파일 시스템, 네트워크 리소스, 웹 요청 및 응답 같은 응용 프로그램 인프라 문제가 자주 포함됩니다. 단위 테스트는 이런 문제 대신에 모조 또는 모의 개체를 사용합니다. 하지만 통합 테스트의 목적은 해당 시스템이 이런 시스템과 예상 대로 잘 작동해 통합 테스트에 모조 또는 모의 개체를 사용하지 않도록 확인하는 것입니다. 대신, 사용자는 다른 서비스에서 서비스 호출 또는 데이터베이스 액세스 같은 인프라를 포함시킬 수 있습니다.

통합 테스트는 단위 테스트보다 코드의 더 큰 세그먼트를 실행하고 또한 인프라 요소에 의존하기 때문에 통합 테스트는 단위 테스트보다 크기가 커져 느린 경향이 있습니다. 따라서 통합 테스트를 얼마나 많이 작성하고 실행할 것인지 제한을 두는 것이 좋습니다.

ASP.NET Core는 네트워크 오버헤드 없이 HTTP 요청을 처리하는 데 사용할 수 있는 기본 테스트 웹 호스트를 포함합니다. 이는 실제 웹 호스트를 사용하는 경우보다 더 빠르게 이런 테스트를 실행할 수 있다는 의미입니다. 테스트 웹 호스트는 Microsoft.AspNetCore.TestHost로서 NuGet 구성 요소에서 사용할 수 있으며, 또한 통합 테스트 프로젝트에 추가할 수 있고 ASP.NET Core 응용 프로그램을 호스트하는 데 사용할 수 있습니다.

다음 코드에서 확인할 수 있듯이 ASP.NET Core 컨트롤러에 대한 통합 테스트를 만드는 경우 테스트 호스트를 통해 컨트롤러를 인스턴스화합니다. 이는 HTTP 요청에 비견될 수 있지만 보다 빠르게 실행 됩니다.

```csharp
public class PrimeWebDefaultRequestShould
{
    private readonly TestServer _server;
    private readonly HttpClient _client;

    public PrimeWebDefaultRequestShould()
    {
        // Arrange
        _server = new TestServer(new WebHostBuilder()
           .UseStartup<Startup>());
           _client = _server.CreateClient();
    }

    [Fact]
    public async Task ReturnHelloWorld()
    {
        // Act
        var response = await _client.GetAsync("/");
        response.EnsureSuccessStatusCode();
        var responseString = await response.Content.ReadAsStringAsync();
        // Assert
        Assert.Equal("Hello World!", responseString);
    }
}
```

#### <a name="additional-resources"></a>추가 자료

-   **Steve Smith. 테스트 컨트롤러** (ASP.NET 코어) [*https://docs.microsoft.com/aspnet/core/mvc/controllers/testing*](/aspnet/core/mvc/controllers/testing)

-   **Steve Smith. 통합 테스트** (ASP.NET 코어) [*https://docs.microsoft.com/aspnet/core/testing/integration-testing*](/aspnet/core/testing/integration-testing)

-   **.NET Core dotnet 테스트를 사용 하 여의 단위 테스트**
    [*https://docs.microsoft.com/dotnet/core/testing/unit-testing-with-dotnet-test*](../../../core/testing/unit-testing-with-dotnet-test.md)

-   **xUnit.net**. 공식 사이트입니다.
    [*https://xunit.github.io/*](https://xunit.github.io/)

-   **단위 테스트 기본 사항입니다.**
    [*https://msdn.microsoft.com/library/hh694602.aspx*](https://msdn.microsoft.com/library/hh694602.aspx)

-   **Moq**. GitHub 리포지토리
    [*https://github.com/moq/moq*](https://github.com/moq/moq)

-   **NUnit**. 공식 사이트입니다.
    [*https://www.nunit.org/*](https://www.nunit.org/)

### <a name="implementing-service-tests-on-a-multi-container-application"></a>다중 컨테이너 응용 프로그램에서 서비스 테스트 구현 

앞서 언급한 것처럼 다중 컨테이너 응용 프로그램을 테스트할 경우 모든 마이크로 서비스는 Docker 호스트 또는 컨테이너 클러스터 내에서 실행해야 합니다. 여러 마이크로 서비스가 관련된 다중 작업을 포함하는 종단간 서비스 테스트는 docker-compose(또는 오케스트레이터를 사용하는 경우 이와 비슷한 메커니즘)를 실행해 Docker 호스트에서 전체 응용 프로그램을 배포하고 시작하도록 요청합니다. 전체 응용 프로그램 및 이의 모든 서비스가 실행되면, 종단 간 통합 및 기능 테스트를 실행할 수 있습니다.

다음과 같은 몇 가지 방법을 사용할 수 있습니다. 해당 응용 프로그램(또는 docker-compose.ci.build.yml과 같은 유사한 응용 프로그램)을 배포하기 위해 사용하는 docker-compose.yml 파일에서 사용자는 솔루션 수준에서 [Dotnet 테스트](../../../core/tools/dotnet-test.md)를 사용하기 위해 진입점을 확장할 수 있습니다. 또한 대상으로 하는 이미지에서 테스트를 실행하는 다른 컴포즈 파일을 사용할 수 있습니다. 컨테이너의 데이터베이스와 마이크로 서비스를 포함하는 통합 테스트용 다른 구성 파일을 사용하여, 테스트를 실행하기 전에 관련 데이터가 항상 원래 상태로 재설정되도록 할수 있습니다.

컴포즈 응용 프로그램이 실행되면 Visual Studio를 실행하는 경우 중단점 및 예외를 이용할 수 있습니다. 또는 Docker 컨테이너를 지원하는 Visual Studio Team Services 또는 다른 CI/CD 시스템의 CI 파이프라인에서 자동으로 통합 테스트를 실행할 수 있습니다.

>[!div class="step-by-step"]
[이전] (subscribe-events.md) [다음] (../microservice-ddd-cqrs-patterns/index.md)
