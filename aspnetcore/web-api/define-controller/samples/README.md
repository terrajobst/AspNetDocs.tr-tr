---
ms.openlocfilehash: b6f39dd0dedb38961eb021cde355f7ec83283195
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57066075"
---
# <a name="aspnet-core-web-api-controller-sample"></a><span data-ttu-id="69403-101">ASP.NET Core Web API denetleyicisi örneği</span><span class="sxs-lookup"><span data-stu-id="69403-101">ASP.NET Core Web API Controller Sample</span></span>

<span data-ttu-id="69403-102">Bu örnek uygulama aşağıdaki projeleri oluşur:</span><span class="sxs-lookup"><span data-stu-id="69403-102">This sample app consists of the following projects:</span></span>

- <span data-ttu-id="69403-103">\**WebApiSample.Api.22*: .NET Core 2.2 hedefleyen bir ASP.NET Core 2.2 projesi.</span><span class="sxs-lookup"><span data-stu-id="69403-103">\**WebApiSample.Api.22*: An ASP.NET Core 2.2 project targeting .NET Core 2.2.</span></span>
- <span data-ttu-id="69403-104">**WebApiSample.Api.21**: .NET Core 2.1 hedefleyen bir ASP.NET Core 2.1 projesi.</span><span class="sxs-lookup"><span data-stu-id="69403-104">**WebApiSample.Api.21**: An ASP.NET Core 2.1 project targeting .NET Core 2.1.</span></span>
- <span data-ttu-id="69403-105">**WebApiSample.Api.Pre21**: .NET Core 2.0 hedefleyen bir ASP.NET Core 2.0 projesi.</span><span class="sxs-lookup"><span data-stu-id="69403-105">**WebApiSample.Api.Pre21**: An ASP.NET Core 2.0 project targeting .NET Core 2.0.</span></span>
- <span data-ttu-id="69403-106">**WebApiSample.DataAccess**: 2 Web API projeleri için bir veri erişim katmanı olarak hizmet veren bir .NET Standard 2.0 sınıf kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="69403-106">**WebApiSample.DataAccess**: A .NET Standard 2.0 class library serving as a data access tier for the 2 Web API projects.</span></span>

<span data-ttu-id="69403-107">Bu örnek, Web API denetleyicisi oluşturma çeşidi gösterir:</span><span class="sxs-lookup"><span data-stu-id="69403-107">This sample illustrates variations of Web API controller creation:</span></span>

- [<span data-ttu-id="69403-108">Sınıf ControllerBase türetin.</span><span class="sxs-lookup"><span data-stu-id="69403-108">Derive class from ControllerBase</span></span>](https://docs.microsoft.com/aspnet/core/web-api#derive-class-from-controllerbase)
- [<span data-ttu-id="69403-109">Sınıf ApiControllerAttribute ile Not Ekle</span><span class="sxs-lookup"><span data-stu-id="69403-109">Annotate class with ApiControllerAttribute</span></span>](https://docs.microsoft.com/aspnet/core/web-api#annotate-class-with-apicontrollerattribute)
