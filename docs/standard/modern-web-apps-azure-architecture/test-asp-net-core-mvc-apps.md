---
title: ASP.NET Core MVC 앱 테스트
description: ASP.NET Core 및 Azure를 사용하여 최신 웹 응용 프로그램 설계 | ASP.NET Core MVC 앱 테스트
author: ardalis
ms.author: wiwagn
ms.date: 10/08/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: d23d0accc33fb8335dff602d6e1d6c8689972906
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/23/2017
---
# <a name="test-aspnet-core-mvc-apps"></a>ASP.NET Core MVC 앱 테스트

> _"제품 단위 테스트가 마음에 들지 않으면 대부분의 고객도 이 테스트를 좋아하지 않을 것입니다."_
> - 익명 -

## <a name="summary"></a>요약

복잡한 소프트웨어는 변경에 대응하여 예기치 않은 방식으로 실패할 수 있습니다. 따라서 변경 후 테스트는 가장 사소한(또는 가장 중요하지 않은) 응용 프로그램을 제외한 모든 응용 프로그램에 필요합니다. 수동 테스트는 소프트웨어를 테스트하는 데 있어 속도가 가장 느리고, 안정성이 가장 낮고, 비용이 가장 많이 드는 방법입니다. 그러나 응용 프로그램을 테스트할 수 있도록 설계되지 않은 경우 사용 가능한 유일한 방법일 수 있습니다. 10장에 나와 있는 아키텍처 원칙에 따라 작성된 응용 프로그램은 단위 테스트를 수행할 수 있어야 하며, ASP.NET Core 응용 프로그램은 자동화된 통합 및 기능 테스트도 지원해야 합니다.

## <a name="kinds-of-automated-tests"></a>자동화된 테스트의 종류

소프트웨어 응용 프로그램에 대한 자동화된 테스트에는 여러 종류가 있습니다. 가장 간단하고 가장 낮은 수준의 테스트는 단위 테스트입니다. 약간 더 높은 수준에서 통합 테스트와 기능 테스트가 있습니다. UI 테스트, 부하 테스트, 스트레스 테스트 및 스모크 테스트와 같은 다른 종류의 테스트는 이 문서에서 다루지 않습니다.

### <a name="unit-tests"></a>단위 테스트

단위 테스트는 응용 프로그램 논리의 단일 부분을 테스트합니다. 아닌 항목 중 일부를 나열하여 자세히 설명할 수 있습니다. 단위 테스트는 코드에서 종속성 또는 인프라와 작동하는 방식을 테스트하지 않으므로 통합 테스트가 필요합니다. 단위 테스트는 코드가 작성된 프레임워크를 테스트하지 않습니다. 즉 이 프레임워크가 작동한다고 가정하거나, 그렇지 않으면 버그를 기록하고 해결 방법을 코딩합니다. 단위 테스트는 메모리와 프로세스에서 전적으로 실행됩니다. 파일 시스템, 네트워크 또는 데이터베이스와 통신하지 않습니다. 단위 테스트는 코드만 테스트해야 합니다.

단위 테스트는 외부 종속성 없이 코드의 단일 단위만 테스트한다는 사실 때문에 매우 빠르게 실행되어야 합니다. 따라서 단위 테스트의 수백 개 테스트 도구 모음을 몇 초 안에 실행할 수 있어야 합니다. 모든 푸시를 공유 소스 제어 저장소로 수행하기 전에 빌드 서버에 있는 모든 자동화된 빌드를 사용하여 자주 실행하는 것이 좋습니다.

### <a name="integration-tests"></a>통합 테스트

데이터베이스 및 파일 시스템과 같은 인프라와 상호 작용하는 코드를 캡슐화하는 것이 좋지만, 여전히 해당 코드 중 일부를 사용할 수 있고 이를 테스트하려고 할 수도 있습니다. 또한 응용 프로그램의 종속성이 완전히 해결되면 코드 계층이 예상대로 상호 작용하는지도 확인해야 합니다. 이 작업은 통합 테스트에서 수행해야 합니다. 통합 테스트는 종종 외부 종속성 및 인프라를 사용하므로 단위 테스트에 비해 속도가 더 느리고 설정하기도 더 어렵습니다. 따라서 단위 테스트를 사용하여 테스트할 수 있는 작업은 통합 테스트에서 테스트하지 않아야 합니다. 지정된 시나리오를 단위 테스트에서 테스트할 수 있으면 단위 테스트를 사용하여 테스트해야 합니다. 그렇게 할 수 없으면 통합 테스트를 사용하는 것이 좋습니다.

통합 테스트에는 단위 테스트보다 더 복잡한 설정 및 해체 절차가 포함되는 경우가 있습니다. 예를 들어 실제 데이터베이스에 대한 통합 테스트에는 각 테스트를 실행하기 전에 데이터베이스를 알려진 상태로 되돌릴 방법이 필요합니다. 새 테스트가 추가되고 프로덕션 데이터베이스 스키마가 진화함에 따라 이러한 테스트 스크립트의 크기와 복잡성이 증가하는 경향이 있습니다. 많은 대형 시스템에서 공유 소스 제어에 대한 변경 내용을 체크 인하기 전에 개발자 워크스테이션에 대한 통합 테스트의 전체 제품군을 실행하는 것은 비현실적입니다. 이러한 경우 통합 테스트는 빌드 서버에서 실행할 수 있습니다.

LocalFileImageService 구현 클래스는 id가 지정된 특정 폴더에서 이미지 파일의 바이트를 가져와서 반환하기 위한 논리를 구현합니다.

```cs
public class LocalFileImageService : IImageService
{
    private readonly IHostingEnvironment _env;
    public LocalFileImageService(IHostingEnvironment env)
    {
        _env = env;
    }
    public byte[] GetImageBytesById(int id)
    {
        try
        {
            var contentRoot = _env.ContentRootPath + "//Pics";
            var path = Path.Combine(contentRoot, id + ".png");
            return File.ReadAllBytes(path);
```

### <a name="functional-tests"></a>기능 테스트

통합 테스트는 개발자의 관점에서 작성되어 시스템의 일부 구성 요소가 모두 제대로 작동하는지 확인합니다. 기능 테스트는 사용자의 관점에서 작성되며, 요구 사항에 따라 시스템의 정확성을 확인합니다. 다음 인용문은 단위 테스트와 비교하여 기능 테스트를 생각하는 방법에 대한 유용한 유사성을 제공합니다.

> "시스템 개발은 집의 건축에 비유되는 경우가 많습니다. 이 비유가 그다지 정확한 것은 아니지만 단위 테스트와 기능 테스트의 차이점을 이해하기 위해 확장할 수 있습니다. 단위 테스트는 집의 건축 현장을 방문하는 건물 감독관과 유사합니다. 그는 집의 다양한 내부 시스템, 기초, 골조, 전기, 배관 등에 초점을 맞추고 있습니다. 그는 집의 구성 부분이 안전하게 제대로 작동하는지, 즉, 건축 법규를 충족하는지 확인(테스트)합니다. 이 시나리오의 기능 테스트는 이 건축 현장을 방문하는 주택 소유자와 유사합니다. 그는 내부 시스템이 적절히 작동하고 건물 감독관이 자신의 임무를 수행하고 있다고 가정합니다. 주택 소유자는 이 집에서 사는 것이 어떤 것일지에 초점을 맞추고 있습니다. 그는 집이 어떻게 보이는지, 여러 방이 편안한 크기인지, 집이 가족의 요구에 부응하는지, 아침 햇살이 드는 좋은 장소에 창문이 있는지 등에 관심이 있습니다. 주택 소유자는 사용자의 관점에서 집에 대한 기능 테스트를 수행하고 있습니다. 한편 건물 감독관은 건축가의 관점에서 집에 대한 단위 테스트를 수행하고 있습니다."

출처: [단위 테스트 및 기능 테스트](http://www.softwaretestingtricks.com/2007/01/unit-testing-versus-functional-tests.html)

"개발자로서 우리는 두 가지 방법에서 실패합니다. 즉 작업을 잘못 빌드하거나 잘못된 작업을 빌드합니다."라고 말하고 싶습니다. 단위 테스트를 통해 작업을 올바르게 빌드할 수 있으며, 기능 테스트를 통해 올바른 작업을 빌드할 수 있습니다.

기능 테스트는 시스템 수준에서 작동하므로 어느 정도의 UI 자동화가 필요할 수 있습니다. 일반적으로 기능 테스트는 통합 테스트와 마찬가지로 일종의 테스트 인프라에서도 작동합니다. 이로 인해 단위 테스트와 통합 테스트보다 더 느리고 더 불안정합니다. 사용자가 예상하는 대로 시스템이 제대로 작동하는지 확신할 수 있을 만큼 많은 기능 테스트만 수행해야 합니다.

### <a name="testing-pyramid"></a>피라미드형 테스트

Martin Fowler는 피라미드형 테스트에 대해 글을 썼으며. 그 예는 그림 9-1에 나와 있습니다.

![](./media/image9-1.png)

그림 9-1 피라미드형 테스트

피라미드의 서로 다른 계층과 상대적인 크기는 여러 종류의 테스트와 응용 프로그램에 대해 작성해야 하는 횟수를 나타냅니다. 여기서 볼 수 있듯이, 더 작은 계층의 기능 테스트와 함께 작은 계층의 통합 테스트 계층에서 지원하는 큰 기반의 단위 테스트를 구성하는 것이 좋습니다. 각 계층에는 이상적으로 하위 계층에서 적절하게 수행할 수 없는 테스트만 있어야 합니다. 특정 시나리오에 필요한 테스트 종류를 결정할 때에는 피라미드형 테스트를 명심하세요.

### <a name="what-to-test"></a>테스트 항목

자동화된 테스트를 작성하는 데 익숙하지 않은 개발자에게 발생하는 일반적인 문제는 테스트 항목에 있습니다. 좋은 출발점은 조건부 논리를 테스트하는 것입니다. 조건문(if-else, switch 등)에 따라 동작이 바뀌는 메서드가 있는 경우 특정 조건에 대한 올바른 동작을 확인하기 위해 최소한 두 가지 테스트를 수행할 수 있어야 합니다. 코드에 오류 조건이 있는 경우 코드를 통해 "정상 경로"에 대한 테스트(오류 없음)를 하나 이상 작성하고, "비정상 경로"에 대한 테스트(오류 또는 비정상 결과 있음)를 하나 이상 작성하여 오류 발생 시 응용 프로그램이 예상대로 작동하는지 확인하는 것이 좋습니다. 마지막으로, 코드 검사와 같은 메트릭에 집중하는 것이 아니라 실패할 수 있는 작업을 테스트하는 데 집중하려고 합니다. 일반적으로 코드 검사가 더 많을수록 좋습니다. 그러나 매우 복잡하고 업무상 중요한 메서드에 대한 몇 가지 테스트를 작성하는 경우, 테스트 코드 검사 메트릭을 향상시키기 위해 일반적으로 자동 속성 테스트를 작성하는 것보다 더 효과적으로 시간을 사용합니다.

## <a name="organizing-test-projects"></a>테스트 프로젝트 구성

테스트 프로젝트는 구성할 수 있지만 가장 효과적으로 작동합니다. 테스트를 유형별(단위 테스트, 통합 테스트) 및 테스트 기능별(프로젝트별, 네임스페이스별)로 구분하는 것이 좋습니다. 이 분리가 단일 테스트 프로젝트 또는 여러 테스트 프로젝트 내의 폴더로 구성되는지는 디자인상의 결정입니다. 하나의 프로젝트가 가장 간단하지만, 여러 테스트가 포함된 대규모 프로젝트의 경우 또는 다른 테스트 집합을 더 쉽게 실행하기 위해 몇 가지 여러 테스트 프로젝트를 사용할 수 있습니다. 많은 팀에서 테스트 중인 프로젝트를 기반으로 하여 테스트 프로젝트를 구성하며, 프로젝트가 여러 개 있는 응용 프로그램의 경우, 특히 각 프로젝트의 테스트 종류에 따라 해당 프로젝트를 여전히 분석하는 경우 많은 테스트 프로젝트를 수행할 수 있습니다. 절충 방법으로, 테스트 프로젝트 내에 테스트할 프로젝트(및 클래스)를 나타내는 폴더를 포함하여 응용 프로그램마다 테스트 종류별로 하나의 프로젝트를 갖습니다.

일반적인 방법은 응용 프로그램 프로젝트를 'src' 폴더 아래에 구성하고, 응용 프로그램의 테스트 프로젝트를 병렬 'tests' 폴더 아래에 구성하는 것입니다. 이 구성이 유용할 경우 Visual Studio에서 일치하는 솔루션 폴더를 만들 수 있습니다.

![](./media/image9-2.png)

그림 9-2 솔루션의 테스트 구성

원하는 테스트 프레임워크를 사용할 수 있습니다. xUnit 프레임워크는 제대로 작동하며 모든 ASP.NET Core 및 EF Core 테스트가 작성된 것입니다. 그림 9-3에 표시된 템플릿을 사용하여 Visual Studio에서 또는 dotnet new xunit을 사용하여 CLI에서 xUnit 테스트 프로젝트를 추가할 수 있습니다.

![](./media/image9-3.png)

그림 9-3 Visual Studio에서 xUnit 테스트 프로젝트 추가

### <a name="test-naming"></a>테스트 이름 지정

테스트 이름은 일관된 방식으로 각 테스트의 기능을 나타내는 이름으로 지정해야 합니다. 크게 성공한 한 가지 방법은 테스트할 클래스와 메서드에 따라 테스트 클래스의 이름을 지정하는 것입니다. 이에 따라 많은 소규모 테스트 클래스가 만들어지지만 각 테스트에서 수행하는 역할이 매우 명확하게 됩니다. 테스트할 클래스와 메서드를 식별하도록 테스트 클래스 이름을 설정하면 테스트 메서드 이름을 사용하여 테스트할 동작을 지정할 수 있습니다. 여기에는 예상되는 동작과 이 동작을 생성해야 하는 모든 입력 또는 가정이 포함되어야 합니다. 몇 가지 테스트 이름 예제는 다음과 같습니다.

-   CatalogControllerGetImage.CallsImageServiceWithId

-   CatalogControllerGetImage.LogsWarningGivenImageMissingException

-   CatalogControllerGetImage.ReturnsFileResultWithBytesGivenSuccess

-   CatalogControllerGetImage.ReturnsNotFoundResultGivenImageMissingException

이 방법의 변형은 다음과 같이 각 테스트 클래스 이름을 "Should"로 끝내고 시제를 약간 수정합니다.

-   CatalogControllerGetImage**Should**.**Call**ImageServiceWithId

-   CatalogControllerGetImage**Should**.**Log**WarningGivenImageMissingException

일부 팀에서는 두 번째 명명 방법이 다소 장황하지만 더 명확하다고 생각합니다. 어떤 경우이든 테스트 동작에 대한 통찰력을 제공하는 명명 규칙을 사용하여 하나 이상의 테스트가 실패하는 경우 해당 이름에서 실패한 사례에 대해 분명하게 파악할 수 있도록 합니다. 테스트 결과에서 볼 때 값이 제공되지 않으므로 테스트 이름은 ControllerTests.Test1과 같이 모호하게 지정하지 마세요.

많은 소규모 테스트 클래스를 생성하는 위와 같은 명명 규칙을 따르는 경우 폴더와 네임스페이스를 사용하여 테스트를 자세히 구성하는 것이 좋습니다. 그림 9-4에서는 여러 테스트 프로젝트 내에서 폴더별로 테스트를 구성하는 방법 중 하나를 보여 줍니다.

![](./media/image9-4.png)

**그림 9-4** 테스트할 클래스에 따라 폴더별로 테스트 클래스 구성

물론, 특정 응용 프로그램 클래스에 많은 메서드(이에 따라 많은 테스트 클래스)가 있는 경우 응용 프로그램 클래스에 해당하는 폴더에 이를 배치하는 것이 좋습니다. 이 구성은 다른 위치의 폴더에 파일을 구성하는 방법과 같습니다. 다른 파일이 많이 포함된 폴더에 3-4개보다 많은 관련 파일이 있는 경우 해당 파일을 자체의 하위 폴더로 이동하는 것이 도움이 되는 경우가 많습니다.

## <a name="unit-testing-aspnet-core-apps"></a>ASP.NET Core 앱 단위 테스트

잘 디자인된 ASP.NET Core 응용 프로그램에서 대부분의 복잡성과 비즈니스 논리는 비즈니스 엔터티 및 다양한 서비스에 캡슐화됩니다. 컨트롤러, 필터, viewmodel 및 뷰와 함께 ASP.NET Core MVC 응용 프로그램 자체에는 단위 테스트가 거의 필요하지 않습니다. 지정된 작업의 기능 대부분은 작업 메서드 자체의 외부에 있습니다. 단위 테스트를 사용하여 라우팅 또는 전역 오류 처리가 올바르게 작동하는지를 테스트하는 것은 효과적으로 수행할 수 없습니다. 마찬가지로, 모델 유효성 검사, 인증 및 권한 부여 필터를 포함하여 모든 필터는 단위 테스트할 수 없습니다. 이러한 동작 소스가 없는 경우 대부분의 작업 메서드는 사소하게 작아야 하며, 이러한 메서드를 사용하는 컨트롤러와 관계없이 테스트할 수 있는 서비스에 대량의 작업을 위임해야 합니다.

단위 테스트를 위해 코드를 리팩터링해야 하는 경우가 있습니다. 여기에는 인프라에 대해 직접 코딩하는 대신 테스트하려는 코드의 추상화에 액세스하기 위해 추상화 식별 및 종속성 주입 사용이 자주 포함됩니다. 예를 들어 이미지를 표시하는 다음과 같은 간단한 작업 메서드를 살펴보겠습니다.

```cs
[HttpGet("[controller]/pic/{id}")]
public IActionResult GetImage(int id)
{
    var contentRoot = _env.ContentRootPath + "//Pics";
    var path = Path.Combine(contentRoot, id + ".png");
    Byte[] b = System.IO.File.ReadAllBytes(path);
    return File(b, "image/png");
}
```

이 메서드를 단위 테스트하는 것은 파일 시스템에서 읽는 데 사용하는 System.IO.File에 직접 종속되기 때문에 어렵습니다. 이 동작을 테스트하여 예상대로 작동하는지 확인할 수 있지만, 실제 파일을 사용하여 수행하는 경우 통합 테스트가 됩니다. 이 메서드의 경로는 테스트할 수 없다는 점을 유념해야 합니다. 잠시 후에 기능 테스트를 통해 이를 수행하는 방법을 살펴보겠습니다.

파일 시스템 동작을 직접 단위 테스트할 수 없고 경로를 테스트할 수 없는 경우 테스트할 대상은 무엇일까요? 단위 테스트를 가능하게 하기 위해 리팩터링한 후에 오류 처리와 같은 일부 테스트 사례와 누락된 동작을 발견할 수 있습니다. 파일을 찾을 수 없는 경우 메서드에서 어떻게 할까요? 어떻게 해야 할까요? 이 예제에서 리팩터링된 메서드는 다음과 같습니다.

```cs
[HttpGet("[controller]/pic/{id}")\]
public IActionResult GetImage(int id)
{
    byte[] imageBytes;
    try
    {
        imageBytes = _imageService.GetImageBytesById(id);
    }
    catch (CatalogImageMissingException ex)
    {
        _logger.LogWarning($"No image found for id: {id}");
        return NotFound();
    }
    return File(imageBytes, "image/png");
}
```

\_logger 및 \_imageService는 모두 종속성으로 삽입됩니다. 이제 작업 메서드에 전달된 동일한 ID가 \_imageService에 전달되고 결과 바이트가 FileResult의 일부로 반환되는지 테스트할 수 있습니다. 또한 오류 로깅이 예상대로 수행되는지, 그리고 이미지가 누락된 경우 중요한 응용 프로그램 동작이라고 가정하고(즉, 개발자가 문제를 진단하기 위해 추가한 임시 코드가 아님) NotFound 결과가 반환되는지도 테스트할 수 있습니다. 실제 파일 논리는 별도의 구현 서비스로 이동되었으며, 누락된 파일의 경우 응용 프로그램별 예외를 반환하도록 보강되었습니다. 통합 테스트를 사용하여 이 구현을 독립적으로 테스트할 수 있습니다.

## <a name="integration-testing-aspnet-core-apps"></a>ASP.NET Core 앱 통합 테스트

```cs
    }
        catch (FileNotFoundException ex)
        {
            throw new CatalogImageMissingException(ex);
        }
    }
}
```

이 서비스는 별도의 서비스로 리팩터링되기 전에 CatalogController 코드에서 수행한 것처럼 IHostingEnvironment를 사용합니다. 이 코드는 IHostingEnvironment를 사용하는 컨트롤러의 유일한 코드였기 때문에 CatalogController의 생성자에서 해당 종속성이 제거되었습니다.

이 서비스가 제대로 작동하는지 테스트하려면 알려진 테스트 이미지 파일을 만들고 서비스에서 지정된 특정 입력을 반환하는지 확인해야 합니다. 실제로 테스트하려는 동작(여기서는 파일 시스템에서 읽기)에서 모의 개체를 사용하지 않도록 주의해야 합니다. 그러나 모의 개체는 여전히 통합 테스트를 설정하는 데 유용할 수 있습니다. 이 경우 IHostingEnvironment를 모의하여 ContentRootPath에서 테스트 이미지에 사용할 폴더를 가리킬 수 있습니다. 작업 통합 테스트 클래스 전체는 다음과 같습니다.

```cs
public class LocalFileImageServiceGetImageBytesById
{
    private byte[] _testBytes = new byte[] { 0x01, 0x02, 0x03 };
    private readonly Mock<IHostingEnvironment> _mockEnvironment = new Mock<IHostingEnvironment>();
    private int _testImageId = 123;
    private string _testFileName = "123.png";
    public LocalFileImageServiceGetImageBytesById()
    {
        // create folder if necessary
        Directory.CreateDirectory(Path.Combine(GetFileDirectory(), "Pics"));
        string filePath = GetFilePath(_testFileName);
        System.IO.File.WriteAllBytes(filePath, _testBytes);
        _mockEnvironment.SetupGet<string>(m => m.ContentRootPath).Returns(GetFileDirectory());
    }
    private string GetFilePath(string fileName)
    {
        return Path.Combine(GetFileDirectory(), "Pics", fileName);
        }
            private string GetFileDirectory()
        {
            var location = System.Reflection.Assembly.GetEntryAssembly().Location;
            return Path.GetDirectoryName(location);
        }

        [Fact]
        public void ReturnsFileContentResultGivenValidId()
        {
            var fileService = new LocalFileImageService(_mockEnvironment.Object);
            var result = fileService.GetImageBytesById(_testImageId);
            Assert.Equal(_testBytes, result);
        }
    }
```

> [!NOTE]
> 테스트 자체는 매우 간단합니다. 즉 대부분의 코드가 시스템을 구성하고 테스트 인프라(이 경우 디스크에서 읽을 실제 파일)를 만드는 데 필요합니다. 이는 대개 단위 테스트보다 복잡한 설정 작업이 필요한 통합 테스트에 일반적입니다.

## <a name="functional-testing-aspnet-core-apps"></a>ASP.NET Core 앱 기능 테스트

ASP.NET Core 응용 프로그램의 경우 TestServer 클래스를 사용하면 기능 테스트를 매우 쉽게 작성할 수 있습니다. 응용 프로그램에서 일반적으로 수행하는 것처럼 WebHostBuilder를 사용하여 TestServer를 구성합니다. 이 WebHostBuilder는 응용 프로그램의 실제 호스트와 동일하게 구성해야 하지만, 테스트를 더 쉽게 수행할 수 있는 측면은 모두 수정할 수 있습니다. 대부분의 경우 동일한 TestServer를 여러 테스트 사례에 다시 사용하므로 다시 사용할 수 있는 메서드(아마도 기본 클래스)에 캡슐화할 수 있습니다.

```cs
public abstract class BaseWebTest
{
    protected readonly HttpClient _client;
    protected string _contentRoot;

    public BaseWebTest()
    {
        _client = GetClient();
    }
    
    protected HttpClient GetClient()
    {
        var startupAssembly = typeof(Startup).GetTypeInfo().Assembly;
        _contentRoot = GetProjectPath("src", startupAssembly);
        var builder = new WebHostBuilder()
        .UseContentRoot(_contentRoot)
        .UseStartup&lt;Startup&gt;();
        var server = new TestServer(builder);
        var client = server.CreateClient();
        return client;
    }
}
```

GetProjectPath 메서드는 웹 프로젝트(샘플 솔루션 다운로드)에 대한 실제 경로를 반환하기만 합니다. 이 경우 WebHostBuilder는 웹 응용 프로그램의 콘텐츠 루트의 위치를 간단하게 지정하고 실제 웹 응용 프로그램에서 사용하는 동일한 Startup 클래스를 참조합니다. TestServer를 사용하려면 표준 System.Net.HttpClient 형식을 사용하여 요청을 작성합니다. TestServer는 TestServer에서 실행되는 응용 프로그램에 요청할 준비가 된 미리 구성된 클라이언트를 제공하는 유용한 CreateClient 메서드를 노출합니다. ASP.NET Core 응용 프로그램에 대한 기능 테스트를 작성하는 경우 이 클라이언트(위의 기본 테스트에서 보호된 \_client 멤버로 설정됨)를 사용합니다.

```cs
public class CatalogControllerGetImage : BaseWebTest
{
    [Fact]
    public async Task ReturnsFileContentResultGivenValidId()
    {
        var testFilePath = Path.Combine(_contentRoot, "pics//1.png");
        var expectedFileBytes = File.ReadAllBytes(testFilePath);
        var response = await _client.GetAsync("/catalog/pic/1");
        response.EnsureSuccessStatusCode();
        var streamResponse = await response.Content.ReadAsStreamAsync();
        byte[] byteResult;
        using (var ms = new MemoryStream())
        {
            streamResponse.CopyTo(ms);
            byteResult = ms.ToArray();
        }
        Assert.Equal(expectedFileBytes, byteResult);
    }
}
```

이 기능 테스트는 해당 위치에 있을 수 있는 모든 미들웨어, 필터, 바인더 등을 포함하여 ASP.NET Core MVC 응용 프로그램 스택 전체를 수행합니다. 지정된 경로("/catalog/pic/1")가 알려진 위치에 있는 파일에 대해 예상된 바이트 배열을 반환하는지 확인합니다. 실제 웹 서버를 설정하지 않아도 이렇게 하므로 테스트를 위해 실제 웹 서버를 사용할 때 발생할 수 있는 많은 오류(예: 방화벽 설정 문제)를 방지할 수 있습니다. TestServer에 대해 실행되는 기능 테스트는 일반적으로 통합 및 단위 테스트보다 느리지만 네트워크를 통해 테스트 웹 서버에 실행되는 테스트보다 훨씬 빠릅니다.

>[!div class="step-by-step"]
[이전] (work-with-data-in-asp-net-core-apps.md) [다음] (development-process-for-azure.md)
