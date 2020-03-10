---
uid: signalr/overview/advanced/dependency-injection
title: SignalR 'de bağımlılık ekleme | Microsoft Docs
author: bradygaster
description: Bu konuda kullanılan yazılım sürümleri, .NET 4,5 SignalR sürüm 2 ' nin önceki sürümleri hakkında bilgi Için bu konunun önceki sürümlerini Visual Studio 2013...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: a14121ae-02cf-4024-8af0-9dd0dc810690
msc.legacyurl: /signalr/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 52978b10b6c131ac8eff4535216cc60b43fdf3de
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78537333"
---
# <a name="dependency-injection-in-signalr"></a><span data-ttu-id="b6fbf-103">SignalR’da Bağımlılık Ekleme</span><span class="sxs-lookup"><span data-stu-id="b6fbf-103">Dependency Injection in SignalR</span></span>

<span data-ttu-id="b6fbf-104">, [Mike Ison](https://github.com/MikeWasson), [Patrick fleti](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="b6fbf-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="b6fbf-105">Bu konuda kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="b6fbf-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="b6fbf-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="b6fbf-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="b6fbf-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="b6fbf-107">.NET 4.5</span></span>
> - <span data-ttu-id="b6fbf-108">SignalR sürüm 2</span><span class="sxs-lookup"><span data-stu-id="b6fbf-108">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="b6fbf-109">Bu konunun önceki sürümleri</span><span class="sxs-lookup"><span data-stu-id="b6fbf-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="b6fbf-110">SignalR 'nin önceki sürümleri hakkında daha fazla bilgi için bkz. [SignalR daha eski sürümleri](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="b6fbf-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="b6fbf-111">Sorular ve açıklamalar</span><span class="sxs-lookup"><span data-stu-id="b6fbf-111">Questions and comments</span></span>
>
> <span data-ttu-id="b6fbf-112">Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="b6fbf-113">Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="b6fbf-114">Bağımlılık ekleme, nesneler arasında sabit kodlanmış bağımlılıkları kaldırmanın bir yoludur. bu sayede, bir nesnenin bağımlılıklarını test etmek için (sahte nesneleri kullanarak) veya çalışma zamanı davranışını değiştirmek kolaylaşır.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-114">Dependency injection is a way to remove hard-coded dependencies between objects, making it easier to replace an object's dependencies, either for testing (using mock objects) or to change run-time behavior.</span></span> <span data-ttu-id="b6fbf-115">Bu öğreticide, SignalR hub 'larda bağımlılık ekleme işlemlerinin nasıl gerçekleştirileceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-115">This tutorial shows how to perform dependency injection on SignalR hubs.</span></span> <span data-ttu-id="b6fbf-116">Ayrıca, SignalR ile IOC kapsayıcılarını nasıl kullanacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-116">It also shows how to use IoC containers with SignalR.</span></span> <span data-ttu-id="b6fbf-117">Bir IOC kapsayıcısı, bağımlılık ekleme için genel bir çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-117">An IoC container is a general framework for dependency injection.</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="b6fbf-118">Bağımlılık ekleme nedir?</span><span class="sxs-lookup"><span data-stu-id="b6fbf-118">What is Dependency Injection?</span></span>

<span data-ttu-id="b6fbf-119">Bağımlılık ekleme konusunda zaten bilgi sahibiyseniz bu bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-119">Skip this section if you are already familiar with dependency injection.</span></span>

<span data-ttu-id="b6fbf-120">*Bağımlılık ekleme* (dı), nesnelerin kendi bağımlılıklarını oluşturmadan sorumlu olmayan bir modeldir.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-120">*Dependency injection* (DI) is a pattern where objects are not responsible for creating their own dependencies.</span></span> <span data-ttu-id="b6fbf-121">İşte, bu, bir değer olarak motive etmek için basit bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-121">Here is a simple example to motivate DI.</span></span> <span data-ttu-id="b6fbf-122">İletileri günlüğe kaydetmek için gereken bir nesneniz olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-122">Suppose you have an object that needs to log messages.</span></span> <span data-ttu-id="b6fbf-123">Günlüğe kaydetme arabirimi tanımlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b6fbf-123">You might define a logging interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="b6fbf-124">Nesneniz, iletileri günlüğe kaydetmek için bir `ILogger` oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b6fbf-124">In your object, you can create an `ILogger` to log messages:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="b6fbf-125">Bu işe yarar, ancak en iyi tasarım değildir.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-125">This works, but it's not the best design.</span></span> <span data-ttu-id="b6fbf-126">`FileLogger` başka bir `ILogger` uygulamasıyla değiştirmek istiyorsanız `SomeComponent`değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-126">If you want to replace `FileLogger` with another `ILogger` implementation, you will have to modify `SomeComponent`.</span></span> <span data-ttu-id="b6fbf-127">Birçok farklı nesnenin `FileLogger`kullanduymasını, bunların tümünü değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-127">Supposing that a lot of other objects use `FileLogger`, you will need to change all of them.</span></span> <span data-ttu-id="b6fbf-128">Ya da tek bir `FileLogger` yapmaya karar verirseniz, uygulama genelinde de değişiklikler yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-128">Or if you decide to make `FileLogger` a singleton, you'll also need to make changes throughout the application.</span></span>

<span data-ttu-id="b6fbf-129">Daha iyi bir yaklaşım, nesne içine bir `ILogger` eklemek — örneğin, bir Oluşturucu bağımsız değişkeni kullanarak:</span><span class="sxs-lookup"><span data-stu-id="b6fbf-129">A better approach is to "inject" an `ILogger` into the object—for example, by using a constructor argument:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="b6fbf-130">Artık, hangi `ILogger` kullanacağınızı seçmeden nesne sorumlu değildir.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-130">Now the object is not responsible for selecting which `ILogger` to use.</span></span> <span data-ttu-id="b6fbf-131">Kendisine bağımlı nesneleri değiştirmeden `ILogger` uygulamaları geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-131">You can switch `ILogger` implementations without changing the objects that depend on it.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="b6fbf-132">Bu düzene [Oluşturucu Ekleme](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)adı verilir.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-132">This pattern is called [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="b6fbf-133">Başka bir model, bir ayarlayıcı yöntemi veya özelliği aracılığıyla bağımlılığı ayarladığınız ayarlayıcı ekleme işlemi olur.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-133">Another pattern is setter injection, where you set the dependency through a setter method or property.</span></span>

## <a name="simple-dependency-injection-in-signalr"></a><span data-ttu-id="b6fbf-134">SignalR 'de basit bağımlılık ekleme</span><span class="sxs-lookup"><span data-stu-id="b6fbf-134">Simple Dependency Injection in SignalR</span></span>

<span data-ttu-id="b6fbf-135">[SignalR Ile çalışmaya](../getting-started/tutorial-getting-started-with-signalr.md)başlama öğreticiden sohbet uygulamasını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-135">Consider the Chat application from the tutorial [Getting Started with SignalR](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="b6fbf-136">Bu uygulamadaki Merkez sınıfı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b6fbf-136">Here is the hub class from that application:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="b6fbf-137">Göndermeden önce sohbet iletilerini sunucuda depolamak istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-137">Suppose that you want to store chat messages on the server before sending them.</span></span> <span data-ttu-id="b6fbf-138">Bu işlevi soyutlayan bir arabirim tanımlayabilir ve arabirimi `ChatHub` sınıfına eklemek için DI kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-138">You might define an interface that abstracts this functionality, and use DI to inject the interface into the `ChatHub` class.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="b6fbf-139">Tek sorun, bir SignalR uygulamasının doğrudan hub oluşturmamalıdır; SignalR bunları sizin için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-139">The only problem is that a SignalR application does not directly create hubs; SignalR creates them for you.</span></span> <span data-ttu-id="b6fbf-140">Varsayılan olarak, SignalR bir hub sınıfının parametresiz bir oluşturucuya sahip olmasını bekler.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-140">By default, SignalR expects a hub class to have a parameterless constructor.</span></span> <span data-ttu-id="b6fbf-141">Ancak, hub örnekleri oluşturmak için bir işlevi kolayca kaydedebilir ve bu işlevi, DI işlemini gerçekleştirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-141">However, you can easily register a function to create hub instances, and use this function to perform DI.</span></span> <span data-ttu-id="b6fbf-142">**Globalhost. DependencyResolver. Register**çağırarak işlevi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-142">Register the function by calling **GlobalHost.DependencyResolver.Register**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

<span data-ttu-id="b6fbf-143">Artık `ChatHub` bir örnek oluşturması gerektiğinde SignalR bu anonim işlevi çağıracaktır.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-143">Now SignalR will invoke this anonymous function whenever it needs to create a `ChatHub` instance.</span></span>

## <a name="ioc-containers"></a><span data-ttu-id="b6fbf-144">IoC kapsayıcıları</span><span class="sxs-lookup"><span data-stu-id="b6fbf-144">IoC Containers</span></span>

<span data-ttu-id="b6fbf-145">Önceki kod, basit durumlar için uygundur.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-145">The previous code is fine for simple cases.</span></span> <span data-ttu-id="b6fbf-146">Ancak yine de şunu yazmanız gerekiyordu:</span><span class="sxs-lookup"><span data-stu-id="b6fbf-146">But you still had to write this:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

<span data-ttu-id="b6fbf-147">Birçok bağımlılığı olan karmaşık bir uygulamada, bu "kablolama" kodunun çoğunu yazmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-147">In a complex application with many dependencies, you might need to write a lot of this "wiring" code.</span></span> <span data-ttu-id="b6fbf-148">Özellikle bağımlılıklar iç içe ise, bu kod bakımını yapmak zor olabilir.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-148">This code can be hard to maintain, especially if dependencies are nested.</span></span> <span data-ttu-id="b6fbf-149">Ayrıca birim testi de zordur.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-149">It is also hard to unit test.</span></span>

<span data-ttu-id="b6fbf-150">Bir çözüm bir IOC kapsayıcısı kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-150">One solution is to use an IoC container.</span></span> <span data-ttu-id="b6fbf-151">Bir IOC kapsayıcısı, bağımlılıkları yönetmekten sorumlu bir yazılım bileşenidir. Türleri kapsayıcıya kaydeder ve sonra nesneleri oluşturmak için kapsayıcıyı kullanın.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-151">An IoC container is a software component that is responsible for managing dependencies.You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="b6fbf-152">Kapsayıcı, bağımlılık ilişkilerini otomatik olarak belirler.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-152">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="b6fbf-153">Birçok IOC kapsayıcısı ayrıca nesne ömrü ve kapsamı gibi şeyleri denetlemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-153">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="b6fbf-154">"IoC", bir çerçevenin uygulama koduna çağırdığı genel bir model olan "denetimin INVERSION" anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-154">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="b6fbf-155">Bir IOC kapsayıcısı, nesnelerinizi sizin için oluşturur, bu da normal denetim akışını "tersine çevirir".</span><span class="sxs-lookup"><span data-stu-id="b6fbf-155">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>

## <a name="using-ioc-containers-in-signalr"></a><span data-ttu-id="b6fbf-156">SignalR 'de IOC kapsayıcıları kullanma</span><span class="sxs-lookup"><span data-stu-id="b6fbf-156">Using IoC Containers in SignalR</span></span>

<span data-ttu-id="b6fbf-157">Sohbet uygulaması, bir IOC kapsayıcısından faydalanmak için büyük olasılıkla çok basittir.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-157">The Chat application is probably too simple to benefit from an IoC container.</span></span> <span data-ttu-id="b6fbf-158">Bunun yerine [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) örneğine göz atalım.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-158">Instead, let's look at the [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) sample.</span></span>

<span data-ttu-id="b6fbf-159">StockTicker örneği iki ana sınıfı tanımlar:</span><span class="sxs-lookup"><span data-stu-id="b6fbf-159">The StockTicker sample defines two main classes:</span></span>

- <span data-ttu-id="b6fbf-160">`StockTickerHub`: istemci bağlantılarını yöneten hub sınıfı.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-160">`StockTickerHub`: The hub class, which manages client connections.</span></span>
- <span data-ttu-id="b6fbf-161">`StockTicker`: stok fiyatlarını tutan ve düzenli aralıklarla güncelleştiren bir tek.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-161">`StockTicker`: A singleton that holds stock prices and periodically updates them.</span></span>

<span data-ttu-id="b6fbf-162">`StockTickerHub`, `StockTicker` tekil öğesine bir başvuru tutar `StockTicker` ancak `StockTickerHub`için **IHV Ubconnectioncontext** 'e bir başvuru barındırır.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-162">`StockTickerHub` holds a reference to the `StockTicker` singleton, while `StockTicker` holds a reference to the **IHubConnectionContext** for the `StockTickerHub`.</span></span> <span data-ttu-id="b6fbf-163">`StockTickerHub` örneklerle iletişim kurmak için bu arabirimi kullanır.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-163">It uses this interface to communicate with `StockTickerHub` instances.</span></span> <span data-ttu-id="b6fbf-164">(Daha fazla bilgi için bkz. [ASP.NET SignalR Ile sunucu yayını](../getting-started/tutorial-server-broadcast-with-signalr.md).)</span><span class="sxs-lookup"><span data-stu-id="b6fbf-164">(For more information, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).)</span></span>

<span data-ttu-id="b6fbf-165">Bu bağımlılıklara bir bit eklemek için bir IOC kapsayıcısı kullanabiliriz.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-165">We can use an IoC container to untangle these dependencies a bit.</span></span> <span data-ttu-id="b6fbf-166">İlk olarak, `StockTickerHub` ve `StockTicker` sınıflarını basitleşelim.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-166">First, let's simplify the `StockTickerHub` and `StockTicker` classes.</span></span> <span data-ttu-id="b6fbf-167">Aşağıdaki kodda, ihtiyaç duyduğumuz parçalar hakkında yorum yaptı.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-167">In the following code, I've commented out the parts that we don't need.</span></span>

<span data-ttu-id="b6fbf-168">Parametresiz oluşturucuyu `StockTickerHub`kaldırın.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-168">Remove the parameterless constructor from `StockTickerHub`.</span></span> <span data-ttu-id="b6fbf-169">Bunun yerine, her zaman, hub 'ı oluşturmak için DI 'yi kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-169">Instead, we will always use DI to create the hub.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

<span data-ttu-id="b6fbf-170">StockTicker için Singleton örneğini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-170">For StockTicker, remove the singleton instance.</span></span> <span data-ttu-id="b6fbf-171">Daha sonra, StockTicker ömrünü denetlemek için IoC kapsayıcısını kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-171">Later, we'll use the IoC container to control the StockTicker lifetime.</span></span> <span data-ttu-id="b6fbf-172">Ayrıca, oluşturucuyu genel hale getirin.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-172">Also, make the constructor public.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

<span data-ttu-id="b6fbf-173">Daha sonra, `StockTicker`için bir arabirim oluşturarak kodu yeniden düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-173">Next, we can refactor the code by creating an interface for `StockTicker`.</span></span> <span data-ttu-id="b6fbf-174">Bu arabirimi, `StockTickerHub` `StockTicker` sınıfından ayırmak için kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-174">We'll use this interface to decouple the `StockTickerHub` from the `StockTicker` class.</span></span>

<span data-ttu-id="b6fbf-175">Visual Studio bu tür yeniden düzenleme kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-175">Visual Studio makes this kind of refactoring easy.</span></span> <span data-ttu-id="b6fbf-176">StockTicker.cs dosyasını açın, `StockTicker` sınıfı bildirimine sağ tıklayın ve yeniden **Düzenle** ... seçeneğini belirleyin. **Arabirimi Ayıkla**.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-176">Open the file StockTicker.cs, right-click on the `StockTicker` class declaration, and select **Refactor** ... **Extract Interface**.</span></span>

![](dependency-injection/_static/image1.png)

<span data-ttu-id="b6fbf-177">**Arabirimi Ayıkla** Iletişim kutusunda **Tümünü Seç**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-177">In the **Extract Interface** dialog, click **Select All**.</span></span> <span data-ttu-id="b6fbf-178">Diğer varsayılan değerleri bırakın.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-178">Leave the other defaults.</span></span> <span data-ttu-id="b6fbf-179">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-179">Click **OK**.</span></span>

![](dependency-injection/_static/image2.png)

<span data-ttu-id="b6fbf-180">Visual Studio `IStockTicker`adlı yeni bir arabirim oluşturur ve ayrıca `IStockTicker`türetmeye `StockTicker` değişir.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-180">Visual Studio creates a new interface named `IStockTicker`, and also changes `StockTicker` to derive from `IStockTicker`.</span></span>

<span data-ttu-id="b6fbf-181">IStockTicker.cs dosyasını açın ve arabirimi **genel**' e değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-181">Open the file IStockTicker.cs and change the interface to **public**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

<span data-ttu-id="b6fbf-182">`StockTickerHub` sınıfında, iki `StockTicker` örneğini `IStockTicker`olarak değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b6fbf-182">In the `StockTickerHub` class, change the two instances of `StockTicker` to `IStockTicker`:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

<span data-ttu-id="b6fbf-183">`IStockTicker` arabirimi oluşturmak kesinlikle gerekli değildir, ancak uygulamanızın uygulamanızdaki bileşenler arasında Eşleneni azaltmaya nasıl yardımcı olduğunu göstermek istiyorum.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-183">Creating an `IStockTicker` interface isn't strictly necessary, but I wanted to show how DI can help to reduce coupling between components in your application.</span></span>

## <a name="add-the-ninject-library"></a><span data-ttu-id="b6fbf-184">Nekleme kitaplığını ekleme</span><span class="sxs-lookup"><span data-stu-id="b6fbf-184">Add the Ninject Library</span></span>

<span data-ttu-id="b6fbf-185">.NET için çok sayıda açık kaynaklı IFC kapsayıcısı vardır.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-185">There are many open-source IoC containers for .NET.</span></span> <span data-ttu-id="b6fbf-186">Bu öğretici için [Nekleme](http://www.ninject.org/)'yi kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-186">For this tutorial, I'll use [Ninject](http://www.ninject.org/).</span></span> <span data-ttu-id="b6fbf-187">(Diğer popüler kitaplıklar, [role](http://www.castleproject.org/) [Spring.net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity)ve [StructureMap](http://docs.structuremap.net)içerir.)</span><span class="sxs-lookup"><span data-stu-id="b6fbf-187">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity), and [StructureMap](http://docs.structuremap.net).)</span></span>

<span data-ttu-id="b6fbf-188">[Nekleme kitaplığını](https://nuget.org/packages/Ninject/3.0.1.10)yüklemek Için NuGet Paket Yöneticisi 'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-188">Use NuGet Package Manager to install the [Ninject library](https://nuget.org/packages/Ninject/3.0.1.10).</span></span> <span data-ttu-id="b6fbf-189">Visual Studio 'da, **Araçlar** menüsünden **NuGet Paket Yöneticisi** > **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-189">In Visual Studio, from the **Tools** menu select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="b6fbf-190">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="b6fbf-190">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a><span data-ttu-id="b6fbf-191">SignalR bağımlılık çözümleyicisini değiştirme</span><span class="sxs-lookup"><span data-stu-id="b6fbf-191">Replace the SignalR Dependency Resolver</span></span>

<span data-ttu-id="b6fbf-192">SignalR içinde Nekleme kullanmak için, **Defaultdependencyresolver**'dan türeyen bir sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-192">To use Ninject within SignalR, create a class that derives from **DefaultDependencyResolver**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

<span data-ttu-id="b6fbf-193">Bu sınıf, **Defaultdependencyresolver**'ın **GetService** ve **GetServices** yöntemlerini geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-193">This class overrides the **GetService** and **GetServices** methods of **DefaultDependencyResolver**.</span></span> <span data-ttu-id="b6fbf-194">SignalR, hub örnekleri ve ayrıca SignalR tarafından dahili olarak kullanılan çeşitli hizmetler dahil olmak üzere çalışma zamanında çeşitli nesneler oluşturmak için bu yöntemleri çağırır.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-194">SignalR calls these methods to create various objects at runtime, including hub instances, as well as various services used internally by SignalR.</span></span>

- <span data-ttu-id="b6fbf-195">**GetService** yöntemi bir türün tek bir örneğini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-195">The **GetService** method creates a single instance of a type.</span></span> <span data-ttu-id="b6fbf-196">Nekleme çekirdeğinin **TryGet** yöntemini çağırmak için bu yöntemi geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-196">Override this method to call the Ninject kernel's **TryGet** method.</span></span> <span data-ttu-id="b6fbf-197">Bu yöntem null döndürürse, varsayılan çözümleyiciye geri dönün.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-197">If that method returns null, fall back to the default resolver.</span></span>
- <span data-ttu-id="b6fbf-198">**GetServices** yöntemi, belirtilen türde nesnelerin bir koleksiyonunu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-198">The **GetServices** method creates a collection of objects of a specified type.</span></span> <span data-ttu-id="b6fbf-199">Neklemesine ait sonuçları varsayılan çözümleyiciyle sonuçlarla birleştirmek için bu yöntemi geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-199">Override this method to concatenate the results from Ninject with the results from the default resolver.</span></span>

## <a name="configure-ninject-bindings"></a><span data-ttu-id="b6fbf-200">Nekleme bağlamalarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b6fbf-200">Configure Ninject Bindings</span></span>

<span data-ttu-id="b6fbf-201">Şimdi tür bağlamaları bildirmek için Nekleme kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-201">Now we'll use Ninject to declare type bindings.</span></span>

<span data-ttu-id="b6fbf-202">Uygulamanızın Startup.cs sınıfını açın (`readme.txt`' deki paket yönergelerine göre el ile oluşturduğunuz veya projenize kimlik doğrulaması eklenerek oluşturulan).</span><span class="sxs-lookup"><span data-stu-id="b6fbf-202">Open your application's Startup.cs class (that you either created manually as per the package instructions in `readme.txt`, or that was created by adding authentication to your project).</span></span> <span data-ttu-id="b6fbf-203">`Startup.Configuration` yönteminde Nekleme kapsayıcısını oluşturun ve Nekleme, *çekirdeği*çağırır.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-203">In the `Startup.Configuration` method, create the Ninject container, which Ninject calls the *kernel*.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

<span data-ttu-id="b6fbf-204">Özel bağımlılık çözümleyicimizin bir örneğini oluşturun:</span><span class="sxs-lookup"><span data-stu-id="b6fbf-204">Create an instance of our custom dependency resolver:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

<span data-ttu-id="b6fbf-205">`IStockTicker` için aşağıdaki şekilde bir bağlama oluşturun:</span><span class="sxs-lookup"><span data-stu-id="b6fbf-205">Create a binding for `IStockTicker` as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample17.cs)]

<span data-ttu-id="b6fbf-206">Bu kod iki şeyi söyleyerek.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-206">This code is saying two things.</span></span> <span data-ttu-id="b6fbf-207">İlk olarak, uygulama bir `IStockTicker`ihtiyaç duyduğunda, çekirdek bir `StockTicker`örneği oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-207">First, whenever the application needs an `IStockTicker`, the kernel should create an instance of `StockTicker`.</span></span> <span data-ttu-id="b6fbf-208">İkincisi, `StockTicker` sınıfı tek bir nesne olarak oluşturulmuş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-208">Second, the `StockTicker` class should be a created as a singleton object.</span></span> <span data-ttu-id="b6fbf-209">Nekleme nesnenin bir örneğini oluşturur ve her istek için aynı örneği döndürür.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-209">Ninject will create one instance of the object, and return the same instance for each request.</span></span>

<span data-ttu-id="b6fbf-210">**Iubconnectioncontext** için aşağıdaki şekilde bir bağlama oluşturun:</span><span class="sxs-lookup"><span data-stu-id="b6fbf-210">Create a binding for **IHubConnectionContext** as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

<span data-ttu-id="b6fbf-211">Bu kod, bir **Ihubconnection**döndüren anonim bir işlev oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-211">This code creates an anonymous function that returns an **IHubConnection**.</span></span> <span data-ttu-id="b6fbf-212">**Whenınjectedinto** yöntemi, neklemesine bu işlevi yalnızca `IStockTicker` örnekleri oluştururken kullanmasını söyler.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-212">The **WhenInjectedInto** method tells Ninject to use this function only when creating `IStockTicker` instances.</span></span> <span data-ttu-id="b6fbf-213">Bunun nedeni, SignalR 'nin, dahili olarak **IHV Ubconnectioncontext** örnekleri oluşturduğunu ve SignalR 'nin bunları nasıl oluşturduğunu geçersiz kılmak istemedik.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-213">The reason is that SignalR creates **IHubConnectionContext** instances internally, and we don't want to override how SignalR creates them.</span></span> <span data-ttu-id="b6fbf-214">Bu işlev yalnızca `StockTicker` sınıfımız için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-214">This function only applies to our `StockTicker` class.</span></span>

<span data-ttu-id="b6fbf-215">Bir hub yapılandırması ekleyerek bağımlılık çözümleyicisini **Mapsignalr** yöntemine geçirin:</span><span class="sxs-lookup"><span data-stu-id="b6fbf-215">Pass the dependency resolver into the **MapSignalR** method by adding a hub configuration:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

<span data-ttu-id="b6fbf-216">Örnek başlangıç sınıfındaki Startup. ConfigureSignalR yöntemini yeni parametresiyle güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="b6fbf-216">Update the Startup.ConfigureSignalR method in the sample's Startup class with the new parameter:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

<span data-ttu-id="b6fbf-217">Şimdi SignalR, varsayılan çözümleyici yerine **Mapsignalr**içinde belirtilen çözümleyici 'yi kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-217">Now SignalR will use the resolver specified in **MapSignalR**, instead of the default resolver.</span></span>

<span data-ttu-id="b6fbf-218">`Startup.Configuration`için kod listesinin tamamı aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-218">Here is the complete code listing for `Startup.Configuration`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample21.cs)]

<span data-ttu-id="b6fbf-219">Visual Studio 'da StockTicker uygulamasını çalıştırmak için F5 'e basın.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-219">To run the StockTicker application in Visual Studio, press F5.</span></span> <span data-ttu-id="b6fbf-220">Tarayıcı penceresinde `http://localhost:*port*/SignalR.Sample/StockTicker.html`' a gidin.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-220">In the browser window, navigate to `http://localhost:*port*/SignalR.Sample/StockTicker.html`.</span></span>

![](dependency-injection/_static/image3.png)

<span data-ttu-id="b6fbf-221">Uygulama daha önce olduğu gibi tamamen aynı işlevselliğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-221">The application has exactly the same functionality as before.</span></span> <span data-ttu-id="b6fbf-222">(Bir açıklama için bkz. [ASP.NET SignalR Ile sunucu yayını](../getting-started/tutorial-server-broadcast-with-signalr.md).) Davranışı değiştirmedik; kodu test etmek, sürdürmek ve geliştirmek için daha kolay hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="b6fbf-222">(For a description, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).) We haven't changed the behavior; just made the code easier to test, maintain, and evolve.</span></span>
