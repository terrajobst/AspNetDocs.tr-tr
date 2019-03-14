---
title: Razor bileşenleri bağımlılık ekleme
author: guardrex
description: Bileşenlerine eklenen sağlayarak Blazor ve Razor bileşenleri uygulamaları yerleşik hizmetleri nasıl kullanabileceğinizi öğrenin.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/dependency-injection
ms.openlocfilehash: 6ce8fa74f20145f48797d267c20ef2593368b941
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57071367"
---
# <a name="razor-components-dependency-injection"></a><span data-ttu-id="f8c13-103">Razor bileşenleri bağımlılık ekleme</span><span class="sxs-lookup"><span data-stu-id="f8c13-103">Razor Components dependency injection</span></span>

<span data-ttu-id="f8c13-104">By [Rainer Stropek](https://www.timecockpit.com)</span><span class="sxs-lookup"><span data-stu-id="f8c13-104">By [Rainer Stropek](https://www.timecockpit.com)</span></span>

<span data-ttu-id="f8c13-105">[Bağımlılık ekleme (dı)](/aspnet/core/fundamentals/dependency-injection) yerleşiktir.</span><span class="sxs-lookup"><span data-stu-id="f8c13-105">[Dependency injection (DI)](/aspnet/core/fundamentals/dependency-injection) is built-in.</span></span> <span data-ttu-id="f8c13-106">Uygulamaları, eklenen bileşenlerine sağlayarak yerleşik hizmetlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8c13-106">Apps can use built-in services by having them injected into components.</span></span> <span data-ttu-id="f8c13-107">Uygulamalar ayrıca özel hizmetler tanımlar ve DI aracılığıyla kullanılabilir hale.</span><span class="sxs-lookup"><span data-stu-id="f8c13-107">Apps can also define custom services and make them available via DI.</span></span>

## <a name="dependency-injection"></a><span data-ttu-id="f8c13-108">Bağımlılık ekleme</span><span class="sxs-lookup"><span data-stu-id="f8c13-108">Dependency injection</span></span>

<span data-ttu-id="f8c13-109">DI, merkezi bir konumda yapılandırılmış hizmetlerine erişmek için kullanılan bir tekniktir.</span><span class="sxs-lookup"><span data-stu-id="f8c13-109">DI is a technique for accessing services configured in a central location.</span></span> <span data-ttu-id="f8c13-110">Bu yararlı olabilir:</span><span class="sxs-lookup"><span data-stu-id="f8c13-110">This can be useful to:</span></span>

* <span data-ttu-id="f8c13-111">Bir hizmet sınıfı tek bir örneği arasında birçok bileşen paylaşma (olarak bilinen bir *singleton* hizmeti).</span><span class="sxs-lookup"><span data-stu-id="f8c13-111">Share a single instance of a service class across many components (known as a *singleton* service).</span></span>
* <span data-ttu-id="f8c13-112">Belirli somut hizmet sınıflardan bileşenleri ayırın ve yalnızca soyutlama başvurun.</span><span class="sxs-lookup"><span data-stu-id="f8c13-112">Decouple components from particular concrete service classes and only reference abstractions.</span></span> <span data-ttu-id="f8c13-113">Örneğin, bir arabirim `IDataAccess` somut bir sınıf tarafından uygulanan `DataAccess`.</span><span class="sxs-lookup"><span data-stu-id="f8c13-113">For example, an interface `IDataAccess` is implemented by a concrete class `DataAccess`.</span></span> <span data-ttu-id="f8c13-114">Bir bileşen kullandığında DI almak için bir `IDataAccess` uygulaması bileşeni, somut bir türde eşleşmiş değil.</span><span class="sxs-lookup"><span data-stu-id="f8c13-114">When a component uses DI to receive an `IDataAccess` implementation, the component isn't coupled to the concrete type.</span></span> <span data-ttu-id="f8c13-115">Uygulama, belki de birim testlerinde sahte bir uygulama için değişiklik yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="f8c13-115">The implementation can be swapped, perhaps to a mock implementation in unit tests.</span></span>

<span data-ttu-id="f8c13-116">DI sistemi bileşenlerine services örneğini sağlama için sorumludur.</span><span class="sxs-lookup"><span data-stu-id="f8c13-116">The DI system is responsible for supplying instances of services to components.</span></span> <span data-ttu-id="f8c13-117">Böylece Hizmetleri kendilerini hizmetleri hakkında daha fazla güvenebileceğiniz DI de bağımlılıkları yinelemeli olarak çözümler.</span><span class="sxs-lookup"><span data-stu-id="f8c13-117">DI also resolves dependencies recursively so that services themselves can depend on further services.</span></span> <span data-ttu-id="f8c13-118">DI uygulama başlangıcı sırasında yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="f8c13-118">DI is configured during startup of the app.</span></span> <span data-ttu-id="f8c13-119">Örnek bu konunun ilerleyen bölümlerinde gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f8c13-119">An example is shown later in this topic.</span></span>

## <a name="add-services-to-di"></a><span data-ttu-id="f8c13-120">DI için hizmet ekleyin</span><span class="sxs-lookup"><span data-stu-id="f8c13-120">Add services to DI</span></span>

<span data-ttu-id="f8c13-121">Yeni bir uygulama oluşturduktan sonra incelemek `Startup.ConfigureServices` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="f8c13-121">After creating a new app, examine the `Startup.ConfigureServices` method:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Add custom services here
}
```

<span data-ttu-id="f8c13-122">`ConfigureServices` Yöntemi geçirilir bir [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection), hizmet tanımlayıcısı nesneleri listesi verilmiştir ([ServiceDescriptor](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor)).</span><span class="sxs-lookup"><span data-stu-id="f8c13-122">The `ConfigureServices` method is passed an [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection), which is a list of service descriptor objects ([ServiceDescriptor](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor)).</span></span> <span data-ttu-id="f8c13-123">Hizmet, hizmet koleksiyonu için hizmet tanımlayıcıları sağlayarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="f8c13-123">Services are added by providing service descriptors to the service collection.</span></span> <span data-ttu-id="f8c13-124">Aşağıdaki kod örneği, bir kavramı gösterir:</span><span class="sxs-lookup"><span data-stu-id="f8c13-124">The following code sample demonstrates the concept:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton<IDataAccess, DataAccess>();
}
```

<span data-ttu-id="f8c13-125">Hizmetler aşağıdaki yaşam süreleri ile yapılandırılabilir:</span><span class="sxs-lookup"><span data-stu-id="f8c13-125">Services can be configured with the following lifetimes:</span></span>

| <span data-ttu-id="f8c13-126">Yöntem</span><span class="sxs-lookup"><span data-stu-id="f8c13-126">Method</span></span>      | <span data-ttu-id="f8c13-127">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f8c13-127">Description</span></span> |
| ----------- | ----------- |
| [<span data-ttu-id="f8c13-128">singleton</span><span class="sxs-lookup"><span data-stu-id="f8c13-128">Singleton</span></span>](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.singleton#Microsoft_Extensions_DependencyInjection_ServiceDescriptor_Singleton__1_System_Func_System_IServiceProvider___0__) | <span data-ttu-id="f8c13-129">DI oluşturur bir *tek örnek* hizmeti.</span><span class="sxs-lookup"><span data-stu-id="f8c13-129">DI creates a *single instance* of the service.</span></span> <span data-ttu-id="f8c13-130">Bu hizmet gerektiren tüm bileşenleri bu örneğe bir başvuru alırsınız.</span><span class="sxs-lookup"><span data-stu-id="f8c13-130">All components requiring this service receive a reference to this instance.</span></span> |
| [<span data-ttu-id="f8c13-131">Geçici</span><span class="sxs-lookup"><span data-stu-id="f8c13-131">Transient</span></span>](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.transient) | <span data-ttu-id="f8c13-132">Bu hizmet bir bileşen gereken her durumda aldığı bir *yeni örneği* hizmeti.</span><span class="sxs-lookup"><span data-stu-id="f8c13-132">Whenever a component requires this service, it receives a *new instance* of the service.</span></span> |
| [<span data-ttu-id="f8c13-133">Kapsamlı</span><span class="sxs-lookup"><span data-stu-id="f8c13-133">Scoped</span></span>](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.scoped) | <span data-ttu-id="f8c13-134">İstemci tarafı Blazor şu anda DI kapsamları kavramı yoktur.</span><span class="sxs-lookup"><span data-stu-id="f8c13-134">Client-side Blazor doesn't currently have the concept of DI scopes.</span></span> <span data-ttu-id="f8c13-135">`Scoped` gibi davranır `Singleton`.</span><span class="sxs-lookup"><span data-stu-id="f8c13-135">`Scoped` behaves like `Singleton`.</span></span> <span data-ttu-id="f8c13-136">Ancak, ASP.NET Core Razor bileşenleri desteklemek `Scoped` yaşam süresi.</span><span class="sxs-lookup"><span data-stu-id="f8c13-136">However, ASP.NET Core Razor Components support the `Scoped` lifetime.</span></span> <span data-ttu-id="f8c13-137">Bir Razor bileşeninde bir kapsamlı hizmet kayıt bağlantısı kapsamlıdır.</span><span class="sxs-lookup"><span data-stu-id="f8c13-137">In a Razor Component, a scoped service registration is scoped to the connection.</span></span> <span data-ttu-id="f8c13-138">Kapsamlı hizmetlerini kullanarak bu nedenle, geçerli kullanıcıya kapsamlı hizmetler için tercih edilir (istemci-tarafı çalıştırmak için geçerli amaç olsa bile tarayıcıda).</span><span class="sxs-lookup"><span data-stu-id="f8c13-138">For this reason, using scoped services is preferred for services that should be scoped to the current user (even if the current intent is to run client-side in the browser).</span></span> |

<span data-ttu-id="f8c13-139">ASP.NET Core DI sistemde DI sistem dayanır.</span><span class="sxs-lookup"><span data-stu-id="f8c13-139">The DI system is based on the DI system in ASP.NET Core.</span></span> <span data-ttu-id="f8c13-140">Daha fazla bilgi için [ASP.NET Core bağımlılık ekleme](/aspnet/core/fundamentals/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="f8c13-140">For more information, see [Dependency injection in ASP.NET Core](/aspnet/core/fundamentals/dependency-injection).</span></span>

## <a name="default-services"></a><span data-ttu-id="f8c13-141">Varsayılan hizmetler</span><span class="sxs-lookup"><span data-stu-id="f8c13-141">Default services</span></span>

<span data-ttu-id="f8c13-142">Varsayılan hizmetler, bir app service koleksiyonunu otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="f8c13-142">Default services are automatically added to the service collection of an app.</span></span> <span data-ttu-id="f8c13-143">Aşağıdaki tabloda sağlanan yararlı varsayılan hizmetlerden bazıları gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f8c13-143">The following table shows some of the useful default services provided.</span></span>

| <span data-ttu-id="f8c13-144">Yöntem</span><span class="sxs-lookup"><span data-stu-id="f8c13-144">Method</span></span>       | <span data-ttu-id="f8c13-145">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f8c13-145">Description</span></span> |
| ------------ | ----------- |
| [<span data-ttu-id="f8c13-146">HttpClient</span><span class="sxs-lookup"><span data-stu-id="f8c13-146">HttpClient</span></span>](/dotnet/api/system.net.http.httpclient) | <span data-ttu-id="f8c13-147">HTTP istekleri göndermek ve bir URI (tekli) tarafından tanımlanan bir kaynaktan HTTP yanıtları almak için yöntemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="f8c13-147">Provides methods for sending HTTP requests and receiving HTTP responses from a resource identified by a URI (singleton).</span></span> <span data-ttu-id="f8c13-148">Unutmayın, bu örneği `HttpClient` tarayıcı arka planda HTTP trafiğini işlemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="f8c13-148">Note that this instance of `HttpClient` uses the browser for handling the HTTP traffic in the background.</span></span> <span data-ttu-id="f8c13-149">[HttpClient.BaseAddress](/dotnet/api/system.net.http.httpclient.baseaddress) uygulama taban URI öneki otomatik olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="f8c13-149">[HttpClient.BaseAddress](/dotnet/api/system.net.http.httpclient.baseaddress) is automatically set to the base URI prefix of the app.</span></span> <span data-ttu-id="f8c13-150">`HttpClient` yalnızca istemci-tarafı Blazor uygulamalar için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8c13-150">`HttpClient` is only provided to client-side Blazor apps.</span></span> |
| `IJSRuntime` | <span data-ttu-id="f8c13-151">Çağrıları gönderilen bir JavaScript çalışma zamanı örneğini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f8c13-151">Represents an instance of a JavaScript runtime to which calls may be dispatched.</span></span> <span data-ttu-id="f8c13-152">Daha fazla bilgi için bkz. <xref:razor-components/javascript-interop>.</span><span class="sxs-lookup"><span data-stu-id="f8c13-152">For more information, see <xref:razor-components/javascript-interop>.</span></span> |
| `IUriHelper` | <span data-ttu-id="f8c13-153">URI ve gezinti durumu (tekli) ile çalışmak için Yardımcıları.</span><span class="sxs-lookup"><span data-stu-id="f8c13-153">Helpers for working with URIs and navigation state (singleton).</span></span> <span data-ttu-id="f8c13-154">`IUriHelper` Her iki istemci-tarafı Blazor ve ASP.NET Core Razor bileşenleri uygulama sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8c13-154">`IUriHelper` is provided to both client-side Blazor and ASP.NET Core Razor Components apps.</span></span> |

<span data-ttu-id="f8c13-155">Varsayılan şablon tarafından eklenen varsayılan hizmet sağlayıcısı yerine özel hizmetler sağlayıcısı kullanmak mümkün olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f8c13-155">Note that it is possible to use a custom services provider instead of the default service provider that's added by the default template.</span></span> <span data-ttu-id="f8c13-156">Bir özel hizmet sağlayıcısı, tabloda listelenen varsayılan hizmetleri otomatik olarak sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="f8c13-156">A custom service provider doesn't automatically provide the default services listed in the table.</span></span> <span data-ttu-id="f8c13-157">Bu hizmetler yeni hizmet sağlayıcısına açıkça eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="f8c13-157">Those services must be added to the new service provider explicitly.</span></span>

## <a name="request-a-service-in-a-component"></a><span data-ttu-id="f8c13-158">Bir bileşen içinde bir hizmet isteği</span><span class="sxs-lookup"><span data-stu-id="f8c13-158">Request a service in a component</span></span>

<span data-ttu-id="f8c13-159">Hizmetleri hizmet koleksiyonuna eklendikten sonra bileşenlerin Razor şablonlarına kullanarak yerleştirilebilir `@inject` Razor yönergesi.</span><span class="sxs-lookup"><span data-stu-id="f8c13-159">Once services are added to the service collection, they can be injected into the components' Razor templates using the `@inject` Razor directive.</span></span> <span data-ttu-id="f8c13-160">`@inject` iki parametreye sahiptir:</span><span class="sxs-lookup"><span data-stu-id="f8c13-160">`@inject` has two parameters:</span></span>

* <span data-ttu-id="f8c13-161">Tür adı: Eklenecek hizmetin türü.</span><span class="sxs-lookup"><span data-stu-id="f8c13-161">Type name: The type of the service to inject.</span></span>
* <span data-ttu-id="f8c13-162">Özellik adı: Eklenen app service alma özelliğinin adı.</span><span class="sxs-lookup"><span data-stu-id="f8c13-162">Property name: The name of the property receiving the injected app service.</span></span> <span data-ttu-id="f8c13-163">Not, özelliği el ile oluşturma gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="f8c13-163">Note that the property doesn't require manual creation.</span></span> <span data-ttu-id="f8c13-164">Derleyici, bir özellik oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f8c13-164">The compiler creates the property.</span></span>

<span data-ttu-id="f8c13-165">Birden çok `@inject` deyimleri, farklı hizmetlerde eklenmek üzere kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f8c13-165">Multiple `@inject` statements can be used to inject different services.</span></span>

<span data-ttu-id="f8c13-166">Aşağıdaki örnek nasıl kullanılacağını gösterir `@inject`.</span><span class="sxs-lookup"><span data-stu-id="f8c13-166">The following example shows how to use `@inject`.</span></span> <span data-ttu-id="f8c13-167">Uygulama hizmeti `Services.IDataAccess` bileşenin özelliğine eklenen `DataRepository`.</span><span class="sxs-lookup"><span data-stu-id="f8c13-167">The service implementing `Services.IDataAccess` is injected into the component's property `DataRepository`.</span></span> <span data-ttu-id="f8c13-168">Kodu yalnızca nasıl kullandığını unutmayın `IDataAccess` Özet:</span><span class="sxs-lookup"><span data-stu-id="f8c13-168">Note how the code is only using the `IDataAccess` abstraction:</span></span>

```csharp
@page "/customer-list"
@using Services
@inject IDataAccess DataRepository

<ul>
    @if (Customers != null)
    {
        @foreach (var customer in Customers)
        {
            <li>@customer.FirstName @customer.LastName</li>
        }
    }
</ul>

@functions {
    private IReadOnlyList<Customer> Customers;

    protected override async Task OnInitAsync()
    {
        // The property DataRepository received an implementation
        // of IDataAccess through dependency injection. Use 
        // DataRepository to obtain data from the server.
        Customers = await DataRepository.GetAllCustomersAsync();
    }
}
```

<span data-ttu-id="f8c13-169">Dahili olarak oluşturulan özelliğe (`DataRepository`) ile donatılmış `InjectAttribute` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f8c13-169">Internally, the generated property (`DataRepository`) is decorated with the `InjectAttribute` attribute.</span></span> <span data-ttu-id="f8c13-170">Genellikle, bu öznitelik, doğrudan kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="f8c13-170">Typically, this attribute isn't used directly.</span></span> <span data-ttu-id="f8c13-171">Bir temel sınıf bileşenleri için gereklidir ve eklenen özellikler için temel sınıf, gerekli ayrıca `InjectAttribute` elle eklenebilir:</span><span class="sxs-lookup"><span data-stu-id="f8c13-171">If a base class is required for components and injected properties are also required for the base class, `InjectAttribute` can be manually added:</span></span>

```csharp
public class ComponentBase : BlazorComponent
{
    // Dependency injection works even if using the
    // InjectAttribute in a component's base class.
    [Inject]
    protected IDataAccess DataRepository { get; set; }
    ...
}
```

<span data-ttu-id="f8c13-172">Temel sınıftan türetilmiş bileşenlerinde `@inject` yönergesi gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="f8c13-172">In components derived from the base class, the `@inject` directive isn't required.</span></span> <span data-ttu-id="f8c13-173">`InjectAttribute` Temel sınıfını yeterlidir:</span><span class="sxs-lookup"><span data-stu-id="f8c13-173">The `InjectAttribute` of the base class is sufficient:</span></span>

```csharp
@page "/demo"
@inherits ComponentBase

<h1>...</h1>
...
```

## <a name="dependency-injection-in-services"></a><span data-ttu-id="f8c13-174">Hizmetleri bağımlılık ekleme</span><span class="sxs-lookup"><span data-stu-id="f8c13-174">Dependency injection in services</span></span>

<span data-ttu-id="f8c13-175">Karmaşık services ek hizmetleri gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="f8c13-175">Complex services might require additional services.</span></span> <span data-ttu-id="f8c13-176">Önceki örnekte, `DataAccess` gerektirebilir `HttpClient` varsayılan hizmeti.</span><span class="sxs-lookup"><span data-stu-id="f8c13-176">In the prior example, `DataAccess` might require the `HttpClient` default service.</span></span> <span data-ttu-id="f8c13-177">`@inject` veya `InjectAttribute` Hizmetleri'nde kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="f8c13-177">`@inject` or the `InjectAttribute` can't be used in services.</span></span> <span data-ttu-id="f8c13-178">*Oluşturucu ekleme* yerine kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f8c13-178">*Constructor injection* must be used instead.</span></span> <span data-ttu-id="f8c13-179">Gerekli hizmetler, hizmetin oluşturucusuna parametre ekleyerek eklenir.</span><span class="sxs-lookup"><span data-stu-id="f8c13-179">Required services are added by adding parameters to the service's constructor.</span></span> <span data-ttu-id="f8c13-180">Bağımlılık ekleme hizmet oluşturduğu zaman, oluşturucuda gerektirir ve uygun şekilde sağlayan hizmetler tanır.</span><span class="sxs-lookup"><span data-stu-id="f8c13-180">When dependency injection creates the service, it recognizes the services it requires in the constructor and provides them accordingly.</span></span>

<span data-ttu-id="f8c13-181">Aşağıdaki kod örneği, bir kavramı gösterir:</span><span class="sxs-lookup"><span data-stu-id="f8c13-181">The following code sample demonstrates the concept:</span></span>

```csharp
public class DataAccess : IDataAccess
{
    // The constructor receives an HttpClient via dependency
    // injection. HttpClient is a default service.
    public DataAccess(HttpClient client)
    {
        ...
    }
    ...
}
```

<span data-ttu-id="f8c13-182">Oluşturucu ekleme için aşağıdaki önkoşulları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="f8c13-182">Note the following prerequisites for constructor injection:</span></span>

* <span data-ttu-id="f8c13-183">Bağımsız değişkenleri tüm bağımlılık ekleme tarafından yerine getirilmesi bir oluşturucusu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f8c13-183">There must be one constructor whose arguments can all be fulfilled by dependency injection.</span></span> <span data-ttu-id="f8c13-184">DI tarafından kapsanmayan ek parametreler için varsayılan değerleri belirtilirse izin verildiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f8c13-184">Note that additional parameters not covered by DI are allowed if default values are specified for them.</span></span>
* <span data-ttu-id="f8c13-185">Geçerli bir oluşturucusu olmalıdır *genel*.</span><span class="sxs-lookup"><span data-stu-id="f8c13-185">The applicable constructor must be *public*.</span></span>
* <span data-ttu-id="f8c13-186">Yalnızca geçerli bir oluşturucusu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f8c13-186">There must only be one applicable constructor.</span></span> <span data-ttu-id="f8c13-187">Bir belirsizlik durumunda DI özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f8c13-187">In case of an ambiguity, DI throws an exception.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f8c13-188">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f8c13-188">Additional resources</span></span>

* [<span data-ttu-id="f8c13-189">ASP.NET core'da bağımlılık ekleme</span><span class="sxs-lookup"><span data-stu-id="f8c13-189">Dependency injection in ASP.NET Core</span></span>](/aspnet/core/fundamentals/dependency-injection)
