---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
title: ASP.NET MVC 4 bağımlılığı ekleme | Microsoft Docs
author: rick-anderson
description: 'Note: Bu uygulamalı laboratuvar, ASP.NET MVC ve ASP.NET MVC 4 filtrelerinin temel bilgisine sahip olduğunuzu varsayar. Daha önce ASP.NET MVC 4 filtrelerini kullanmadıysanız rec...'
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 84c7baca-1c54-4c44-8f52-4282122d6acb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 15c9d4dcb9e2c6b9f6adf54d65d15737b32cca3b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78560615"
---
# <a name="aspnet-mvc-4-dependency-injection"></a><span data-ttu-id="38860-104">ASP.NET MVC 4 Bağımlılık Ekleme</span><span class="sxs-lookup"><span data-stu-id="38860-104">ASP.NET MVC 4 Dependency Injection</span></span>

<span data-ttu-id="38860-105">[Web 'de Camps ekibine](https://twitter.com/webcamps) göre</span><span class="sxs-lookup"><span data-stu-id="38860-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="38860-106">Web Camps eğitim setini indirin</span><span class="sxs-lookup"><span data-stu-id="38860-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="38860-107">Bu uygulamalı laboratuvar, **ASP.NET MVC** ve **ASP.NET MVC 4 filtrelerinin**temel bilgisine sahip olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="38860-107">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC** and **ASP.NET MVC 4 filters**.</span></span> <span data-ttu-id="38860-108">Daha önce **ASP.NET MVC 4 filtrelerini** kullanmadıysanız, **ASP.NET MVC özel eylem filtreleri** uygulamalı laboratuvarına gitmeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="38860-108">If you have not used **ASP.NET MVC 4 filters** before, we recommend you to go over **ASP.NET MVC Custom Action Filters** Hands-on Lab.</span></span>

> [!NOTE]
> <span data-ttu-id="38860-109">Tüm örnek kod ve kod parçacıkları, [Microsoft-Web/Webkamptraıningkit yayımlarından](https://aka.ms/webcamps-training-kit)erişilebilen Web Camps eğitim seti ' ne dahildir.</span><span class="sxs-lookup"><span data-stu-id="38860-109">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="38860-110">Bu laboratuvara özgü proje, [ASP.NET MVC 4 bağımlılığı ekleme](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection)adresinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="38860-110">The project specific to this lab is available at [ASP.NET MVC 4 Dependency Injection](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection).</span></span>

<span data-ttu-id="38860-111">**Nesne yönelimli programlama** paradigması 'nda nesneler, katkıda bulunanlar ve tüketiciler bulunan bir işbirliği modelinde birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="38860-111">In **Object Oriented Programming** paradigm, objects work together in a collaboration model where there are contributors and consumers.</span></span> <span data-ttu-id="38860-112">Doğal olarak, bu iletişim modeli nesneler ve bileşenler arasında bağımlılıklar oluşturur ve karmaşıklık arttıkça yönetilmesi zor hale gelir.</span><span class="sxs-lookup"><span data-stu-id="38860-112">Naturally, this communication model generates dependencies between objects and components, becoming difficult to manage when complexity increases.</span></span>

<span data-ttu-id="38860-113">![Sınıf bağımlılıkları ve model karmaşıklığı](aspnet-mvc-4-dependency-injection/_static/image1.png "Sınıf bağımlılıkları ve model karmaşıklığı")</span><span class="sxs-lookup"><span data-stu-id="38860-113">![Class dependencies and model complexity](aspnet-mvc-4-dependency-injection/_static/image1.png "Class dependencies and model complexity")</span></span>

<span data-ttu-id="38860-114">*Sınıf bağımlılıkları ve model karmaşıklığı*</span><span class="sxs-lookup"><span data-stu-id="38860-114">*Class dependencies and model complexity*</span></span>

<span data-ttu-id="38860-115">Büyük olasılıkla, istemci nesnelerinin genellikle hizmet konumundan sorumlu olduğu, **fabrika modelini** ve arabirim ile uygulama arasındaki ayrımı hakkında bilgi sahibi olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-115">You have probably heard about the **Factory Pattern** and the separation between the interface and the implementation using services, where the client objects are often responsible for service location.</span></span>

<span data-ttu-id="38860-116">Bağımlılık ekleme deseninin, denetimin Inversion öğesinin belirli bir uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="38860-116">The Dependency Injection pattern is a particular implementation of Inversion of Control.</span></span> <span data-ttu-id="38860-117">**Denetimin INVERSION (IOC)** , nesnelerin işlerini yapmak için kullandıkları başka nesneler oluşturmayacağı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="38860-117">**Inversion of Control (IoC)** means that objects do not create other objects on which they rely to do their work.</span></span> <span data-ttu-id="38860-118">Bunun yerine, bir dış kaynaktan (örneğin, bir XML yapılandırma dosyası) ihtiyaç duydukları nesneleri alırlar.</span><span class="sxs-lookup"><span data-stu-id="38860-118">Instead, they get the objects that they need from an outside source (for example, an xml configuration file).</span></span>

<span data-ttu-id="38860-119">**Bağımlılık ekleme (dı)** , bu, genellikle Oluşturucu parametrelerini geçiren ve özellikleri ayarlanmış bir çerçeve bileşeni tarafından nesne müdahalesi olmadan yapıldığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="38860-119">**Dependency Injection (DI)** means that this is done without the object intervention, usually by a framework component that passes constructor parameters and set properties.</span></span>

<a id="The_Dependency_Injection_DI_Design_Pattern"></a>
### <a name="the-dependency-injection-di-design-pattern"></a><span data-ttu-id="38860-120">Bağımlılık ekleme (dı) tasarım deseninin</span><span class="sxs-lookup"><span data-stu-id="38860-120">The Dependency Injection (DI) Design Pattern</span></span>

<span data-ttu-id="38860-121">Yüksek düzeyde, bağımlılık ekleme 'nin amacı, bir istemci sınıfının (örneğin *, golfçü*) bir arabirim (ör. *Iclub*) karşılayan bir şeye ihtiyaç duymaktır.</span><span class="sxs-lookup"><span data-stu-id="38860-121">At a high level, the goal of Dependency Injection is that a client class (e.g. *the golfer*) needs something that satisfies an interface (e.g. *IClub*).</span></span> <span data-ttu-id="38860-122">Somut türün ne olduğunu (ör. *Woodclub, ıronkulüler, Dilimgeclub* veya *putterkulüler*), başka birinin (örneğin, iyi bir *Caddy*) işlemesini istiyor.</span><span class="sxs-lookup"><span data-stu-id="38860-122">It doesn't care what the concrete type is (e.g. *WoodClub, IronClub, WedgeClub* or *PutterClub*), it wants someone else to handle that (e.g. a good *caddy*).</span></span> <span data-ttu-id="38860-123">ASP.NET MVC 'deki bağımlılık Çözümleyicisi, başka bir yere (ör. bir kapsayıcı veya *sinek torbası*) bağımlılık mantığınızı kaydetmenize izin verebilir.</span><span class="sxs-lookup"><span data-stu-id="38860-123">The Dependency Resolver in ASP.NET MVC can allow you to register your dependency logic somewhere else (e.g. a container or a *bag of clubs*).</span></span>

<span data-ttu-id="38860-124">![Bağımlılık ekleme diyagramı](aspnet-mvc-4-dependency-injection/_static/image2.png "Bağımlılık ekleme çizimi")</span><span class="sxs-lookup"><span data-stu-id="38860-124">![Dependency Injection diagram](aspnet-mvc-4-dependency-injection/_static/image2.png "Dependency Injection illustration")</span></span>

<span data-ttu-id="38860-125">*Bağımlılık ekleme-Golf benzerleme vurguladı*</span><span class="sxs-lookup"><span data-stu-id="38860-125">*Dependency Injection - Golf analogy*</span></span>

<span data-ttu-id="38860-126">Bağımlılık ekleme deseninin ve denetimin Inversion kullanmanın avantajları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="38860-126">The advantages of using Dependency Injection pattern and Inversion of Control are the following:</span></span>

- <span data-ttu-id="38860-127">Sınıf bağlantısını azaltır</span><span class="sxs-lookup"><span data-stu-id="38860-127">Reduces class coupling</span></span>
- <span data-ttu-id="38860-128">Kodu yeniden kullanma artırır</span><span class="sxs-lookup"><span data-stu-id="38860-128">Increases code reusing</span></span>
- <span data-ttu-id="38860-129">Kod bakımumu geliştirir</span><span class="sxs-lookup"><span data-stu-id="38860-129">Improves code maintainability</span></span>
- <span data-ttu-id="38860-130">Uygulama testini geliştirir</span><span class="sxs-lookup"><span data-stu-id="38860-130">Improves application testing</span></span>

> [!NOTE]
> <span data-ttu-id="38860-131">Bağımlılık ekleme bazen soyut fabrika tasarım düzeniyle karşılaştırılır, ancak her iki yaklaşım arasında hafif bir farklılık vardır.</span><span class="sxs-lookup"><span data-stu-id="38860-131">Dependency Injection is sometimes compared with Abstract Factory Design Pattern, but there is a slight difference between both approaches.</span></span> <span data-ttu-id="38860-132">Dı, fabrikaları ve kayıtlı Hizmetleri çağırarak bağımlılıkları çözümlemek için arka planda çalışan bir çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="38860-132">DI has a Framework working behind to solve dependencies by calling the factories and the registered services.</span></span>

<span data-ttu-id="38860-133">Bağımlılık ekleme modelini anladığınıza göre, bu laboratuvarın tamamında ASP.NET MVC 4 ' te nasıl uygulanacağını öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-133">Now that you understand the Dependency Injection Pattern, you will learn throughout this lab how to apply it in ASP.NET MVC 4.</span></span> <span data-ttu-id="38860-134">Bir veritabanı erişim hizmeti eklemek için **denetleyicilerde** bağımlılık ekleme 'yi kullanmaya başlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="38860-134">You will start using Dependency Injection in the **Controllers** to include a database access service.</span></span> <span data-ttu-id="38860-135">Daha sonra, bir hizmeti kullanmak ve bilgileri göstermek için **görünümlere** bağımlılık ekleme işlemini uygulayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="38860-135">Next, you will apply Dependency Injection to the **Views** to consume a service and show information.</span></span> <span data-ttu-id="38860-136">Son olarak, ASP.NET MVC 4 filtrelerinden bir özel eylem filtresi ekleme.</span><span class="sxs-lookup"><span data-stu-id="38860-136">Finally, you will extend the DI to ASP.NET MVC 4 Filters, injecting a custom action filter in the solution.</span></span>

<span data-ttu-id="38860-137">Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="38860-137">In this Hands-on Lab, you will learn how to:</span></span>

- <span data-ttu-id="38860-138">NuGet paketlerini kullanarak bağımlılık ekleme için Unity ile ASP.NET MVC 4 ' ü tümleştirin</span><span class="sxs-lookup"><span data-stu-id="38860-138">Integrate ASP.NET MVC 4 with Unity for Dependency Injection using NuGet Packages</span></span>
- <span data-ttu-id="38860-139">ASP.NET MVC denetleyicisi içinde bağımlılık ekleme kullanma</span><span class="sxs-lookup"><span data-stu-id="38860-139">Use Dependency Injection inside an ASP.NET MVC Controller</span></span>
- <span data-ttu-id="38860-140">ASP.NET MVC görünümü içinde bağımlılık ekleme kullanma</span><span class="sxs-lookup"><span data-stu-id="38860-140">Use Dependency Injection inside an ASP.NET MVC View</span></span>
- <span data-ttu-id="38860-141">Bağımlılık ekleme Işlemini bir ASP.NET MVC eylem filtresi içinde kullanma</span><span class="sxs-lookup"><span data-stu-id="38860-141">Use Dependency Injection inside an ASP.NET MVC Action Filter</span></span>

> [!NOTE]
> <span data-ttu-id="38860-142">Bu laboratuvar, bağımlılık çözümlemesi için Unity. Mvc3 NuGet paketini kullanıyor, ancak herhangi bir bağımlılık ekleme çerçevesini ASP.NET MVC 4 ile çalışacak şekilde uyarlamak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="38860-142">This Lab is using Unity.Mvc3 NuGet Package for dependency resolution, but it is possible to adapt any Dependency Injection Framework to work with ASP.NET MVC 4.</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="38860-143">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="38860-143">Prerequisites</span></span>

<span data-ttu-id="38860-144">Bu Laboratuvarı tamamlayabilmeniz için aşağıdaki öğelere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="38860-144">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="38860-145">[Web veya üst için Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (nasıl yükleneceğine ilişkin yönergeler Için [Ek A](#AppendixA) oku).</span><span class="sxs-lookup"><span data-stu-id="38860-145">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="38860-146">Kurulum</span><span class="sxs-lookup"><span data-stu-id="38860-146">Setup</span></span>

<span data-ttu-id="38860-147">**Kod parçacıklarını yükleme**</span><span class="sxs-lookup"><span data-stu-id="38860-147">**Installing Code Snippets**</span></span>

<span data-ttu-id="38860-148">Kolaylık olması için, bu laboratuvar boyunca yönettiğiniz kodun çoğu Visual Studio kod parçacıkları olarak sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="38860-148">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="38860-149">Kod parçacıklarını yüklemek için **.\Source\Setup\CodeSnippets.vsi** dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="38860-149">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="38860-150">Visual Studio Code parçacıkları hakkında bilginiz yoksa ve bunları nasıl kullanacağınızı öğrenmek isterseniz, [Ek B: kod parçacıkları&quot;kullanarak](#AppendixB) bu belgedeki eke başvurabilirsiniz &quot;.</span><span class="sxs-lookup"><span data-stu-id="38860-150">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="38860-151">Alıştırmalarda</span><span class="sxs-lookup"><span data-stu-id="38860-151">Exercises</span></span>

<span data-ttu-id="38860-152">Bu uygulamalı laboratuvar aşağıdaki alýþtýrmalardan oluşur:</span><span class="sxs-lookup"><span data-stu-id="38860-152">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="38860-153">Alıştırma 1: ekleme a Controller</span><span class="sxs-lookup"><span data-stu-id="38860-153">Exercise 1: Injecting a Controller</span></span>](#Exercise1)
2. [<span data-ttu-id="38860-154">Alıştırma 2: ekleme a View</span><span class="sxs-lookup"><span data-stu-id="38860-154">Exercise 2: Injecting a View</span></span>](#Exercise2)
3. [<span data-ttu-id="38860-155">Alıştırma 3: ekleme filtreleri</span><span class="sxs-lookup"><span data-stu-id="38860-155">Exercise 3: Injecting Filters</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="38860-156">Her alıştırma, alıştırmaları tamamladıktan sonra elde etmeniz gereken sonuç çözümünü içeren bir **son** klasör ile birlikte sunulur.</span><span class="sxs-lookup"><span data-stu-id="38860-156">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="38860-157">Bu çözümü, alýþtýrmalar üzerinden çalışarak daha fazla yardıma ihtiyacınız varsa kılavuz olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-157">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="38860-158">Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **30 dakika**.</span><span class="sxs-lookup"><span data-stu-id="38860-158">Estimated time to complete this lab: **30 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Injecting_a_Controller"></a>
### <a name="exercise-1-injecting-a-controller"></a><span data-ttu-id="38860-159">Alıştırma 1: ekleme a Controller</span><span class="sxs-lookup"><span data-stu-id="38860-159">Exercise 1: Injecting a Controller</span></span>

<span data-ttu-id="38860-160">Bu alıştırmada, bir NuGet paketi kullanarak Unity 'yi tümleştirerek ASP.NET MVC denetleyicilerindeki bağımlılık ekleme işlemini nasıl kullanacağınızı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-160">In this exercise, you will learn how to use Dependency Injection in ASP.NET MVC Controllers by integrating Unity using a NuGet Package.</span></span> <span data-ttu-id="38860-161">Bu nedenle, verileri veri erişiminden ayırmak için MvcMusicStore denetleyicilerinize hizmetleri dahil edersiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-161">For that reason, you will include services into your MvcMusicStore controllers to separate the logic from the data access.</span></span> <span data-ttu-id="38860-162">Hizmetler, **Unity**'Nin yardımıyla bağımlılık ekleme kullanılarak çözülecektir, denetleyici oluşturucuda yeni bir bağımlılık oluşturur.</span><span class="sxs-lookup"><span data-stu-id="38860-162">The services will create a new dependency in the controller constructor, which will be resolved using Dependency Injection with the help of **Unity**.</span></span>

<span data-ttu-id="38860-163">Bu yaklaşım, daha esnek ve bakım ve test etme işlemlerini daha kolay olan, daha az bağlanmış uygulamalar oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="38860-163">This approach will show you how to generate less coupled applications, which are more flexible and easier to maintain and test.</span></span> <span data-ttu-id="38860-164">Ayrıca, ASP.NET MVC 'nin Unity ile nasıl tümleştirileceğini öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-164">You will also learn how to integrate ASP.NET MVC with Unity.</span></span>

<a id="About_StoreManager_Service"></a>
#### <a name="about-storemanager-service"></a><span data-ttu-id="38860-165">StoreManager hizmeti hakkında</span><span class="sxs-lookup"><span data-stu-id="38860-165">About StoreManager Service</span></span>

<span data-ttu-id="38860-166">Başlangıç çözümünde belirtilen MVC müzik deposu artık **StoreService**adlı depolama denetleyicisi verilerini yöneten bir hizmet içeriyor.</span><span class="sxs-lookup"><span data-stu-id="38860-166">The MVC Music Store provided in the begin solution now includes a service that manages the Store Controller data named **StoreService**.</span></span> <span data-ttu-id="38860-167">Mağaza hizmeti uygulamasını aşağıda bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-167">Below you will find the Store Service implementation.</span></span> <span data-ttu-id="38860-168">Tüm yöntemlerin model varlıkları döndürdüğüne unutmayın.</span><span class="sxs-lookup"><span data-stu-id="38860-168">Note that all the methods return Model entities.</span></span>

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample1.cs)]

<span data-ttu-id="38860-169">Başlangıç çözümünden **Storecontroller** artık **StoreService**kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="38860-169">**StoreController** from the begin solution now consumes **StoreService**.</span></span> <span data-ttu-id="38860-170">Tüm veri başvuruları **Storecontroller**'dan kaldırılmıştır ve artık **StoreService**kullanan herhangi bir yöntemi değiştirmeden geçerli veri erişim sağlayıcısını değiştirmek mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="38860-170">All the data references were removed from **StoreController**, and now possible to modify the current data access provider without changing any method that consumes **StoreService**.</span></span>

<span data-ttu-id="38860-171">**Storecontroller** uygulamasının sınıf oluşturucusunun Içinde **StoreService** 'e bağımlılığı olduğunu aşağıda bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-171">You will find below that the **StoreController** implementation has a dependency with **StoreService** inside the class constructor.</span></span>

> [!NOTE]
> <span data-ttu-id="38860-172">Bu alıştırmada tanıtılan bağımlılık, **denetimin INVERSION** (IOC) ile ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="38860-172">The dependency introduced in this exercise is related to **Inversion of Control** (IoC).</span></span>
> 
> <span data-ttu-id="38860-173">**Storecontroller** sınıf oluşturucusu, sınıfının içinden hizmet çağrıları gerçekleştirmek için gerekli olan bir **ıtoreservice** tür parametresi alır.</span><span class="sxs-lookup"><span data-stu-id="38860-173">The **StoreController** class constructor receives an **IStoreService** type parameter, which is essential to perform service calls from inside the class.</span></span> <span data-ttu-id="38860-174">Ancak **Storecontroller** , ASP.NET MVC ile çalışmak için herhangi bir denetleyicinin olması gereken varsayılan oluşturucuyu (parametresiz) uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="38860-174">However, **StoreController** does not implement the default constructor (with no parameters) that any controller must have to work with ASP.NET MVC.</span></span>
> 
> <span data-ttu-id="38860-175">Bağımlılığı çözümlemek için, denetleyicinin bir soyut fabrika tarafından oluşturulması gerekir (belirtilen türde herhangi bir nesne döndüren bir sınıf).</span><span class="sxs-lookup"><span data-stu-id="38860-175">To resolve the dependency, the controller has to be created by an abstract factory (a class that returns any object of the specified type).</span></span>

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="38860-176">Parametresiz bir Oluşturucu bildirildiği için, sınıf, hizmet nesnesini göndermeden StoreController oluşturmayı denediğinde bir hata alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="38860-176">You will get an error when the class tries to create the StoreController without sending the service object, as there is no parameterless constructor declared.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Running_the_Application"></a>
#### <a name="task-1---running-the-application"></a><span data-ttu-id="38860-177">Görev 1-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="38860-177">Task 1 - Running the Application</span></span>

<span data-ttu-id="38860-178">Bu görevde, uygulama mantığındaki veri erişimini ayıran mağaza denetleyicisine hizmeti içeren BEGIN uygulamasını çalıştıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="38860-178">In this task, you will run the Begin application, which includes the service into the Store Controller that separates the data access from the application logic.</span></span>

<span data-ttu-id="38860-179">Uygulamayı çalıştırırken, denetleyici hizmeti varsayılan olarak bir parametre olarak geçirilmediğinden bir özel durum alırsınız:</span><span class="sxs-lookup"><span data-stu-id="38860-179">When running the application, you will receive an exception, as the controller service is not passed as a parameter by default:</span></span>

1. <span data-ttu-id="38860-180">**Source\Ex01-Injecting Controller\Begin**dizininde bulunan **Başlangıç** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="38860-180">Open the **Begin** solution located in **Source\Ex01-Injecting Controller\Begin**.</span></span>

   1. <span data-ttu-id="38860-181">Devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="38860-181">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="38860-182">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="38860-182">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="38860-183">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38860-183">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="38860-184">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="38860-184">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="38860-185">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="38860-185">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="38860-186">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-186">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="38860-187">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="38860-187">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="38860-188">Uygulamayı hata ayıklamadan çalıştırmak için **CTRL + F5** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="38860-188">Press **Ctrl + F5** to run the application without debugging.</span></span> <span data-ttu-id="38860-189">**Bu nesne için tanımlı olmayan &quot;oluşturucu**&quot;hata iletisini alırsınız:</span><span class="sxs-lookup"><span data-stu-id="38860-189">You will get the error message &quot;**No parameterless constructor defined for this object**&quot;:</span></span>

    <span data-ttu-id="38860-190">![ASP.NET MVC başlangıç uygulaması çalıştırılırken hata oluştu](aspnet-mvc-4-dependency-injection/_static/image3.png "ASP.NET MVC başlangıç uygulaması çalıştırılırken hata oluştu")</span><span class="sxs-lookup"><span data-stu-id="38860-190">![Error while running ASP.NET MVC Begin Application](aspnet-mvc-4-dependency-injection/_static/image3.png "Error while running ASP.NET MVC Begin Application")</span></span>

    <span data-ttu-id="38860-191">*ASP.NET MVC başlangıç uygulaması çalıştırılırken hata oluştu*</span><span class="sxs-lookup"><span data-stu-id="38860-191">*Error while running ASP.NET MVC Begin Application*</span></span>
3. <span data-ttu-id="38860-192">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="38860-192">Close the browser.</span></span>

<span data-ttu-id="38860-193">Aşağıdaki adımlarda, bu denetleyiciye gereken bağımlılığı eklemek için müzik deposu çözümünde çalışacaksınız.</span><span class="sxs-lookup"><span data-stu-id="38860-193">In the following steps you will work on the Music Store Solution to inject the dependency this controller needs.</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Including_Unity_into_MvcMusicStore_Solution"></a>
#### <a name="task-2---including-unity-into-mvcmusicstore-solution"></a><span data-ttu-id="38860-194">2\. görev-MvcMusicStore çözümüne Unity dahil</span><span class="sxs-lookup"><span data-stu-id="38860-194">Task 2 - Including Unity into MvcMusicStore Solution</span></span>

<span data-ttu-id="38860-195">Bu görevde, çözüme **Unity. Mvc3** NuGet paketini dahil edersiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-195">In this task, you will include **Unity.Mvc3** NuGet Package to the solution.</span></span>

> [!NOTE]
> <span data-ttu-id="38860-196">Unity. Mvc3 paketi ASP.NET MVC 3 için tasarlandı, ancak ASP.NET MVC 4 ile tamamen uyumludur.</span><span class="sxs-lookup"><span data-stu-id="38860-196">Unity.Mvc3 package was designed for ASP.NET MVC 3, but it is fully compatible with ASP.NET MVC 4.</span></span>
> 
> <span data-ttu-id="38860-197">Unity, örnek ve tür saklama için isteğe bağlı desteği olan hafif, genişletilebilir bir bağımlılık ekleme kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="38860-197">Unity is a lightweight, extensible dependency injection container with optional support for instance and type interception.</span></span> <span data-ttu-id="38860-198">Bu, herhangi bir tür .NET uygulamasında kullanmak için genel amaçlı bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="38860-198">It is a general-purpose container for use in any type of .NET application.</span></span> <span data-ttu-id="38860-199">Bağımlılık ekleme mekanizmalarda bulunan tüm ortak özellikleri sağlar: nesne oluşturma, gereksinimlerin soyutlaması, çalışma zamanında bağımlılıkları belirterek ve esneklik, kapsayıcıya bileşen yapılandırmasını erteleyerek.</span><span class="sxs-lookup"><span data-stu-id="38860-199">It provides all the common features found in dependency injection mechanisms including: object creation, abstraction of requirements by specifying dependencies at runtime and flexibility, by deferring the component configuration to the container.</span></span>

1. <span data-ttu-id="38860-200">**Mvcmusicstore** projesinde **Unity. Mvc3** NuGet paketini yükler.</span><span class="sxs-lookup"><span data-stu-id="38860-200">Install **Unity.Mvc3** NuGet Package in the **MvcMusicStore** project.</span></span> <span data-ttu-id="38860-201">Bunu yapmak için, **diğer Windows** | **Görünüm** ' den **Paket Yöneticisi konsolunu** açın.</span><span class="sxs-lookup"><span data-stu-id="38860-201">To do this, open the **Package Manager Console** from **View** | **Other Windows**.</span></span>
2. <span data-ttu-id="38860-202">Şu komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="38860-202">Run the following command.</span></span>

    <span data-ttu-id="38860-203">PMC</span><span class="sxs-lookup"><span data-stu-id="38860-203">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-dependency-injection/samples/sample3.ps1)]

    <span data-ttu-id="38860-204">![Unity. Mvc3 NuGet paketi yükleniyor](aspnet-mvc-4-dependency-injection/_static/image4.png "Unity. Mvc3 NuGet paketi yükleniyor")</span><span class="sxs-lookup"><span data-stu-id="38860-204">![Installing Unity.Mvc3 NuGet Package](aspnet-mvc-4-dependency-injection/_static/image4.png "Installing Unity.Mvc3 NuGet Package")</span></span>

    <span data-ttu-id="38860-205">*Unity. Mvc3 NuGet paketi yükleniyor*</span><span class="sxs-lookup"><span data-stu-id="38860-205">*Installing Unity.Mvc3 NuGet Package*</span></span>
3. <span data-ttu-id="38860-206">**Unity. Mvc3** paketi yüklendikten sonra Unity yapılandırmasını basitleştirmek için otomatik olarak eklediği dosya ve klasörleri keşfedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-206">Once the **Unity.Mvc3** package is installed, explore the files and folders it automatically adds in order to simplify Unity configuration.</span></span>

    <span data-ttu-id="38860-207">![Unity. Mvc3 paketi yüklendi](aspnet-mvc-4-dependency-injection/_static/image5.png "Unity. Mvc3 paketi yüklendi")</span><span class="sxs-lookup"><span data-stu-id="38860-207">![Unity.Mvc3 package installed](aspnet-mvc-4-dependency-injection/_static/image5.png "Unity.Mvc3 package installed")</span></span>

    <span data-ttu-id="38860-208">*Unity. Mvc3 paketi yüklendi*</span><span class="sxs-lookup"><span data-stu-id="38860-208">*Unity.Mvc3 package installed*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Registering_Unity_in_Globalasaxcs_Application_Start"></a>
#### <a name="task-3---registering-unity-in-globalasaxcs-application_start"></a><span data-ttu-id="38860-209">Görev 3-Global.asax.cs uygulamasında Unity kaydetme\_başlangıç</span><span class="sxs-lookup"><span data-stu-id="38860-209">Task 3 - Registering Unity in Global.asax.cs Application\_Start</span></span>

<span data-ttu-id="38860-210">Bu görevde, **Global.asax.cs** ' de bulunan **uygulama\_start** metodunu, Unity önyükleyici başlatıcısını çağırmak için güncelleştiğini ve sonra bağımlılık ekleme Için kullanacağınız hizmet ve denetleyiciyi kaydeden önyükleyici dosyasını güncelleştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-210">In this task, you will update the **Application\_Start** method located in **Global.asax.cs** to call the Unity Bootstrapper initializer and then, update the Bootstrapper file registering the Service and Controller you will use for Dependency Injection.</span></span>

1. <span data-ttu-id="38860-211">Şimdi, Unity kapsayıcısını ve bağımlılık çözümleyici 'yi Başlatan dosya olan önyükleyici 'yi yedektacaksınız.</span><span class="sxs-lookup"><span data-stu-id="38860-211">Now, you will hook up the Bootstrapper which is the file that initializes the Unity container and Dependency Resolver.</span></span> <span data-ttu-id="38860-212">Bunu yapmak için **Global.asax.cs** açın ve **uygulama\_start** yöntemine aşağıdaki vurgulanmış kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="38860-212">To do this, open **Global.asax.cs** and add the following highlighted code within the **Application\_Start** method.</span></span>

    <span data-ttu-id="38860-213">(Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex01-Unity 'Yi Başlat*)</span><span class="sxs-lookup"><span data-stu-id="38860-213">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Initialize Unity*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample4.cs)]
2. <span data-ttu-id="38860-214">**Bootstrapper.cs** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="38860-214">Open **Bootstrapper.cs** file.</span></span>
3. <span data-ttu-id="38860-215">Şu ad alanlarını ekleyin: **Mvcmusicstore. Services** ve **MusicStore. Controllers**.</span><span class="sxs-lookup"><span data-stu-id="38860-215">Include the following namespaces: **MvcMusicStore.Services** and **MusicStore.Controllers**.</span></span>

    <span data-ttu-id="38860-216">(Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex01-önyükleyici ekleme ad alanı*)</span><span class="sxs-lookup"><span data-stu-id="38860-216">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Bootstrapper Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample5.cs)]
4. <span data-ttu-id="38860-217">**Buildunitycontainer** yönteminin Içeriğini, depo denetleyicisi ve mağaza hizmetini kaydeden aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="38860-217">Replace **BuildUnityContainer** method's content with the following code that registers Store Controller and Store Service.</span></span>

    <span data-ttu-id="38860-218">(Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex01-kayıt depolama denetleyicisi ve hizmeti*)</span><span class="sxs-lookup"><span data-stu-id="38860-218">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Register Store Controller and Service*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample6.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="38860-219">Görev 4-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="38860-219">Task 4 - Running the Application</span></span>

<span data-ttu-id="38860-220">Bu görevde, şimdi Unity 'yi dahil ettikten sonra yüklenebildiğini doğrulamak için uygulamayı çalıştıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="38860-220">In this task, you will run the application to verify that it can now be loaded after including Unity.</span></span>

1. <span data-ttu-id="38860-221">Uygulamayı çalıştırmak için **F5** tuşuna basın, uygulamanın artık herhangi bir hata iletisi görüntülenmeden yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="38860-221">Press **F5** to run the application, the application should now load without showing any error message.</span></span>

    <span data-ttu-id="38860-222">![Uygulama bağımlılık ekleme ile çalıştırılıyor](aspnet-mvc-4-dependency-injection/_static/image6.png "Uygulama bağımlılık ekleme ile çalıştırılıyor")</span><span class="sxs-lookup"><span data-stu-id="38860-222">![Running Application with Dependency Injection](aspnet-mvc-4-dependency-injection/_static/image6.png "Running Application with Dependency Injection")</span></span>

    <span data-ttu-id="38860-223">*Uygulama bağımlılık ekleme ile çalıştırılıyor*</span><span class="sxs-lookup"><span data-stu-id="38860-223">*Running Application with Dependency Injection*</span></span>
2. <span data-ttu-id="38860-224">**/Store**'a gidin.</span><span class="sxs-lookup"><span data-stu-id="38860-224">Browse to **/Store**.</span></span> <span data-ttu-id="38860-225">Bu işlem, artık **Unity**kullanılarak oluşturulan **storecontroller**'ı çağırır.</span><span class="sxs-lookup"><span data-stu-id="38860-225">This will invoke **StoreController**, which is now created using **Unity**.</span></span>

    <span data-ttu-id="38860-226">![MVC müzik deposu](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC müzik deposu")</span><span class="sxs-lookup"><span data-stu-id="38860-226">![MVC Music Store](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC Music Store")</span></span>

    <span data-ttu-id="38860-227">*MVC müzik deposu*</span><span class="sxs-lookup"><span data-stu-id="38860-227">*MVC Music Store*</span></span>
3. <span data-ttu-id="38860-228">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="38860-228">Close the browser.</span></span>

<span data-ttu-id="38860-229">Aşağıdaki alıştırmalarda, bağımlılık ekleme kapsamının ASP.NET MVC görünümleri ve eylem filtreleri içinde kullanmak için nasıl uzatılacağınızı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-229">In the following exercises you will learn how to extend the Dependency Injection scope to use it inside ASP.NET MVC Views and Action Filters.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Injecting_a_View"></a>
### <a name="exercise-2-injecting-a-view"></a><span data-ttu-id="38860-230">Alıştırma 2: ekleme a View</span><span class="sxs-lookup"><span data-stu-id="38860-230">Exercise 2: Injecting a View</span></span>

<span data-ttu-id="38860-231">Bu alıştırmada, Unity tümleştirmesi için ASP.NET MVC 4 ' ün yeni özelliklerine sahip bir görünümde bağımlılık ekleme işlemini nasıl kullanacağınızı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-231">In this exercise, you will learn how to use Dependency Injection in a view with the new features of ASP.NET MVC 4 for Unity integration.</span></span> <span data-ttu-id="38860-232">Bunu yapmak için mağaza tarama görünümü içinde bir ileti ve aşağıda bir görüntü gösteren özel bir hizmet çağıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="38860-232">In order to do that, you will call a custom service inside the Store Browse View, which will show a message and an image below.</span></span>

<span data-ttu-id="38860-233">Ardından, projeyi Unity ile tümleştirecaksınız ve bağımlılıkları eklemek için özel bir bağımlılık Çözümleyicisi oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="38860-233">Then, you will integrate the project with Unity and create a custom dependency resolver to inject the dependencies.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Creating_a_View_that_Consumes_a_Service"></a>
#### <a name="task-1---creating-a-view-that-consumes-a-service"></a><span data-ttu-id="38860-234">Görev 1-bir hizmeti tüketen bir görünüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="38860-234">Task 1 - Creating a View that Consumes a Service</span></span>

<span data-ttu-id="38860-235">Bu görevde, yeni bir bağımlılık oluşturmak için hizmet çağrısı gerçekleştiren bir görünüm oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="38860-235">In this task, you will create a view that performs a service call to generate a new dependency.</span></span> <span data-ttu-id="38860-236">Hizmet, bu çözüme dahil olan basit bir mesajlaşma hizmeti ile oluşur.</span><span class="sxs-lookup"><span data-stu-id="38860-236">The service consists in a simple messaging service included in this solution.</span></span>

1. <span data-ttu-id="38860-237">**Source\Ex02-Injecting View\Begin** klasöründe bulunan **BEGIN** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="38860-237">Open the **Begin** solution located in the **Source\Ex02-Injecting View\Begin** folder.</span></span> <span data-ttu-id="38860-238">Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-238">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="38860-239">Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="38860-239">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="38860-240">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="38860-240">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="38860-241">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38860-241">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="38860-242">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="38860-242">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="38860-243">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="38860-243">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="38860-244">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-244">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="38860-245">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="38860-245">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="38860-246">Daha fazla bilgi için şu makaleye bakın: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span><span class="sxs-lookup"><span data-stu-id="38860-246">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="38860-247">**/Services**içindeki **kaynak \varlıklar** klasöründe bulunan **MessageService.cs** ve **IMessageService.cs** sınıflarını dahil edin.</span><span class="sxs-lookup"><span data-stu-id="38860-247">Include the **MessageService.cs** and the **IMessageService.cs** classes located in the **Source \Assets** folder in **/Services**.</span></span> <span data-ttu-id="38860-248">Bunu yapmak için, **Hizmetler** klasörü öğesine sağ tıklayın ve **Varolan öğe Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="38860-248">To do this, right-click **Services** folder and select **Add Existing Item**.</span></span> <span data-ttu-id="38860-249">Dosyaların konumuna gidin ve bunları dahil edin.</span><span class="sxs-lookup"><span data-stu-id="38860-249">Browse to the files' location and include them.</span></span>

    <span data-ttu-id="38860-250">![Ileti hizmeti ve hizmet arabirimi ekleniyor](aspnet-mvc-4-dependency-injection/_static/image8.png "Ileti hizmeti ve hizmet arabirimi ekleniyor")</span><span class="sxs-lookup"><span data-stu-id="38860-250">![Adding Message Service and Service Interface](aspnet-mvc-4-dependency-injection/_static/image8.png "Adding Message Service and Service Interface")</span></span>

    <span data-ttu-id="38860-251">*Ileti hizmeti ve hizmet arabirimi ekleniyor*</span><span class="sxs-lookup"><span data-stu-id="38860-251">*Adding Message Service and Service Interface*</span></span>

    > [!NOTE]
    > <span data-ttu-id="38860-252">**Imessageservice** arabirimi, **MessageService** sınıfı tarafından uygulanan iki özelliği tanımlar.</span><span class="sxs-lookup"><span data-stu-id="38860-252">The **IMessageService** interface defines two properties implemented by the **MessageService** class.</span></span> <span data-ttu-id="38860-253">Bu özellikler-**ileti** ve **ImageUrl**-ileti ve görüntülenecek görüntünün URL 'sini depolar.</span><span class="sxs-lookup"><span data-stu-id="38860-253">These properties -**Message** and **ImageUrl**- store the message and the URL of the image to be displayed.</span></span>
3. <span data-ttu-id="38860-254">Projenin kök klasöründe **/Pages** klasörünü oluşturun ve sonra **MyBasePage.cs** sınıfını **source\varlıklarından**ekleyin.</span><span class="sxs-lookup"><span data-stu-id="38860-254">Create the folder **/Pages** in the project's root folder, and then add the existing class **MyBasePage.cs** from **Source\Assets**.</span></span> <span data-ttu-id="38860-255">İçinden kalıtımla alacak temel sayfa aşağıdaki yapıya sahiptir.</span><span class="sxs-lookup"><span data-stu-id="38860-255">The base page you will inherit from has the following structure.</span></span>

    <span data-ttu-id="38860-256">![Sayfalar klasörü](aspnet-mvc-4-dependency-injection/_static/image9.png "Sayfalar klasörü")</span><span class="sxs-lookup"><span data-stu-id="38860-256">![Pages folder](aspnet-mvc-4-dependency-injection/_static/image9.png "Pages folder")</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample7.cs)]
4. <span data-ttu-id="38860-257">**/Views/Store** klasöründen **gözataal. cshtml** görünümünü açın ve **MyBasePage.cs**adresinden devralma yapın.</span><span class="sxs-lookup"><span data-stu-id="38860-257">Open **Browse.cshtml** view from **/Views/Store** folder, and make it inherit from **MyBasePage.cs**.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample8.cshtml)]
5. <span data-ttu-id="38860-258">Bir görüntü ve hizmet tarafından alınan bir ileti görüntülemek için, **Gözden** geçirme görünümünde **MessageService** 'e bir çağrı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="38860-258">In the **Browse** view, add a call to **MessageService** to display an image and a message retrieved by the service.</span></span>
   <span data-ttu-id="38860-259">(C#)</span><span class="sxs-lookup"><span data-stu-id="38860-259">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample9.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Including_a_Custom_Dependency_Resolver_and_a_Custom_View_Page_Activator"></a>
#### <a name="task-2---including-a-custom-dependency-resolver-and-a-custom-view-page-activator"></a><span data-ttu-id="38860-260">Görev 2-özel bir bağımlılık Çözümleyicisi ve özel bir görünüm sayfası Etkinleştirici dahil</span><span class="sxs-lookup"><span data-stu-id="38860-260">Task 2 - Including a Custom Dependency Resolver and a Custom View Page Activator</span></span>

<span data-ttu-id="38860-261">Önceki görevde, içinde bir hizmet çağrısı gerçekleştirmek için bir görünümün içine yeni bir bağımlılık eklendi.</span><span class="sxs-lookup"><span data-stu-id="38860-261">In the previous task, you injected a new dependency inside a view to perform a service call inside it.</span></span> <span data-ttu-id="38860-262">Şimdi, ASP.NET MVC bağımlılık ekleme arabirimlerini **ıviewpageetkinleştirici** ve **ıdependencyresolver**uygulayarak bu bağımlılığı çöztecaksınız.</span><span class="sxs-lookup"><span data-stu-id="38860-262">Now, you will resolve that dependency by implementing the ASP.NET MVC Dependency Injection interfaces **IViewPageActivator** and **IDependencyResolver**.</span></span> <span data-ttu-id="38860-263">Çözümdeki bir **ıdependencyresolver** uygulaması, Unity kullanarak hizmet alımı ile ilgilenecektir.</span><span class="sxs-lookup"><span data-stu-id="38860-263">You will include in the solution an implementation of **IDependencyResolver** that will deal with the service retrieval by using Unity.</span></span> <span data-ttu-id="38860-264">Daha sonra, görünümlerin oluşturulmasını çözecek bir **ıviewpagesemblyınterface** özel uygulaması dahil edersiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-264">Then, you will include another custom implementation of **IViewPageActivator** interface that will solve the creation of the views.</span></span>

> [!NOTE]
> <span data-ttu-id="38860-265">ASP.NET MVC 3 ' den itibaren, bağımlılık ekleme için uygulama, Hizmetleri kaydetme arabirimlerini basitleştirdi.</span><span class="sxs-lookup"><span data-stu-id="38860-265">Since ASP.NET MVC 3, the implementation for Dependency Injection had simplified the interfaces to register services.</span></span> <span data-ttu-id="38860-266">**Idependencyresolver** ve **ıviewpageetkinleştirici** , bağımlılık ekleme için ASP.NET MVC 3 özelliklerinin bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="38860-266">**IDependencyResolver** and **IViewPageActivator** are part of ASP.NET MVC 3 features for Dependency Injection.</span></span>
> 
> <span data-ttu-id="38860-267">**-Idependencyresolver** arabirimi önceki ımvcservicelocator 'un yerini almıştır.</span><span class="sxs-lookup"><span data-stu-id="38860-267">**- IDependencyResolver** interface replaces the previous IMvcServiceLocator.</span></span> <span data-ttu-id="38860-268">Idependencyresolver 'ın uygulayıcıları, hizmet veya hizmet koleksiyonunun bir örneğini döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="38860-268">Implementers of IDependencyResolver must return an instance of the service or a service collection.</span></span>
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample10.cs)]
> 
> <span data-ttu-id="38860-269">**-Iviewpageetkinleştirici** arabirimi, görünüm sayfalarının bağımlılık ekleme yoluyla nasıl örneklendiği konusunda daha ayrıntılı denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="38860-269">**- IViewPageActivator** interface provides more fine-grained control over how view pages are instantiated via dependency injection.</span></span> <span data-ttu-id="38860-270">**Iviewpageetkinleştirici** arabirimini uygulayan sınıflar, bağlam bilgilerini kullanarak görünüm örnekleri oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="38860-270">The classes that implement **IViewPageActivator** interface can create view instances using context information.</span></span>
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample11.cs)]

1. <span data-ttu-id="38860-271">Projenin kök klasöründe/**Factory** klasörünü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="38860-271">Create the /**Factories** folder in the project's root folder.</span></span>
2. <span data-ttu-id="38860-272">**/Sources/Assets/** to **factory** klasöründen çözümünüze **CustomViewPageActivator.cs** ekleyin.</span><span class="sxs-lookup"><span data-stu-id="38860-272">Include **CustomViewPageActivator.cs** to your solution from **/Sources/Assets/** to **Factories** folder.</span></span> <span data-ttu-id="38860-273">Bunu yapmak için **/Factory** klasörüne sağ tıklayın, Ekle ' yi seçin.  **Mevcut öğe** ve ardından **CustomViewPageActivator.cs**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="38860-273">To do that, right-click the **/Factories** folder, select **Add | Existing Item** and then select **CustomViewPageActivator.cs**.</span></span> <span data-ttu-id="38860-274">Bu sınıf, Unity kapsayıcısını tutmak için **ıviewpageetkinleştirici** arabirimini uygular.</span><span class="sxs-lookup"><span data-stu-id="38860-274">This class implements the **IViewPageActivator** interface to hold the Unity Container.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample12.cs)]

    > [!NOTE]
    > <span data-ttu-id="38860-275">**Customviewpageetkinleştirici** , bir Unity kapsayıcısı kullanarak bir görünümün oluşturulmasını yönetmekten sorumludur.</span><span class="sxs-lookup"><span data-stu-id="38860-275">**CustomViewPageActivator** is responsible for managing the creation of a view by using a Unity container.</span></span>
3. <span data-ttu-id="38860-276">**/Sources/varlıklarından** **/factory** klasöründen **UnityDependencyResolver.cs** dosyasını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="38860-276">Include **UnityDependencyResolver.cs** file from **/Sources/Assets** to **/Factories** folder.</span></span> <span data-ttu-id="38860-277">Bunu yapmak için **/Factory** klasörüne sağ tıklayın, Ekle ' yi seçin.  **Varolan öğe** ve ardından **UnityDependencyResolver.cs** dosyası ' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="38860-277">To do that, right-click the **/Factories** folder, select **Add | Existing Item** and then select **UnityDependencyResolver.cs** file.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample13.cs)]

    > [!NOTE]
    > <span data-ttu-id="38860-278">**Unitydependencyresolver** sınıfı, Unity için özel bir dependencyresolver.</span><span class="sxs-lookup"><span data-stu-id="38860-278">**UnityDependencyResolver** class is a custom DependencyResolver for Unity.</span></span> <span data-ttu-id="38860-279">Unity kapsayıcısı içinde bir hizmet bulunamazsa, taban çözümleyici gönderilir.</span><span class="sxs-lookup"><span data-stu-id="38860-279">When a service cannot be found inside the Unity container, the base resolver is invocated.</span></span>

<span data-ttu-id="38860-280">Aşağıdaki görevde her iki uygulama da modelin hizmetlerin ve görünümlerin konumunu bilmesini sağlamak için kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="38860-280">In the following task both implementations will be registered to let the model know the location of the services and the views.</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_-_Registering_for_Dependency_Injection_within_Unity_container"></a>
#### <a name="task-3---registering-for-dependency-injection-within-unity-container"></a><span data-ttu-id="38860-281">Görev 3-Unity kapsayıcısı içinde bağımlılık ekleme için kaydetme</span><span class="sxs-lookup"><span data-stu-id="38860-281">Task 3 - Registering for Dependency Injection within Unity container</span></span>

<span data-ttu-id="38860-282">Bu görevde, bağımlılık ekleme işini yapmak için önceki tüm şeyleri bir araya getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-282">In this task, you will put all the previous things together to make Dependency Injection work.</span></span>

<span data-ttu-id="38860-283">Çözümünüz Şu anda aşağıdaki öğelere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="38860-283">Up to now your solution has the following elements:</span></span>

- <span data-ttu-id="38860-284">**MyBaseClass** 'tan devralan ve **MessageService**'i tüketen bir **tarama** görünümü.</span><span class="sxs-lookup"><span data-stu-id="38860-284">A **Browse** View that inherits from **MyBaseClass** and consumes **MessageService**.</span></span>
- <span data-ttu-id="38860-285">Hizmet arabirimi için belirtilen bağımlılık eklenmesine sahip olan bir ara sınıf-**MyBaseClass**.</span><span class="sxs-lookup"><span data-stu-id="38860-285">An intermediate class -**MyBaseClass**- that has dependency injection declared for the service interface.</span></span>
- <span data-ttu-id="38860-286">Hizmet- **MessageService** ve arabirimi **ımessageservice**.</span><span class="sxs-lookup"><span data-stu-id="38860-286">A service - **MessageService** - and its interface **IMessageService**.</span></span>
- <span data-ttu-id="38860-287">Unity- **Unitydependencyresolver** için özel bir bağımlılık Çözümleyicisi; hizmet alımı ile ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="38860-287">A custom dependency resolver for Unity - **UnityDependencyResolver** - that deals with service retrieval.</span></span>
- <span data-ttu-id="38860-288">Sayfayı oluşturan bir görünüm sayfası Etkinleştirici- **Customviewpageetkinleştirici** .</span><span class="sxs-lookup"><span data-stu-id="38860-288">A View Page activator - **CustomViewPageActivator** - that creates the page.</span></span>

<span data-ttu-id="38860-289">**Gezinme** görünümü eklemek Için şimdi Unity kapsayıcısına özel bağımlılık çözümleyici 'yi kaydetmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-289">To inject **Browse** View, you will now register the custom dependency resolver in the Unity container.</span></span>

1. <span data-ttu-id="38860-290">**Bootstrapper.cs** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="38860-290">Open **Bootstrapper.cs** file.</span></span>
2. <span data-ttu-id="38860-291">Hizmeti başlatmak için bir **MessageService** örneğini Unity kapsayıcısına kaydedin:</span><span class="sxs-lookup"><span data-stu-id="38860-291">Register an instance of **MessageService** into the Unity container to initialize the service:</span></span>

    <span data-ttu-id="38860-292">(Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex02-Register Ileti hizmeti*)</span><span class="sxs-lookup"><span data-stu-id="38860-292">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Register Message Service*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample14.cs)]
3. <span data-ttu-id="38860-293">**Mvcmusicstore. Factory** ad alanına bir başvuru ekleyin.</span><span class="sxs-lookup"><span data-stu-id="38860-293">Add a reference to **MvcMusicStore.Factories** namespace.</span></span>

    <span data-ttu-id="38860-294">(Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex02-Factory ad alanı*)</span><span class="sxs-lookup"><span data-stu-id="38860-294">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Factories Namespace*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample15.cs)]
4. <span data-ttu-id="38860-295">**Customviewpageetkinleştirici** öğesini Unity kapsayıcısına bir görünüm sayfası Etkinleştirici olarak Kaydet:</span><span class="sxs-lookup"><span data-stu-id="38860-295">Register **CustomViewPageActivator** as a View Page activator into the Unity container:</span></span>

    <span data-ttu-id="38860-296">(Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex02-Register Customviewpageetkinleştirici*)</span><span class="sxs-lookup"><span data-stu-id="38860-296">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Register CustomViewPageActivator*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample16.cs)]
5. <span data-ttu-id="38860-297">ASP.NET MVC 4 varsayılan bağımlılık çözümleyicisini **Unitydependencyresolver**örneğiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="38860-297">Replace ASP.NET MVC 4 default dependency resolver with an instance of **UnityDependencyResolver**.</span></span> <span data-ttu-id="38860-298">Bunu yapmak için, **Initialize** Yöntemi içeriğini aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="38860-298">To do this, replace **Initialize** method content with the following code:</span></span>

    <span data-ttu-id="38860-299">(Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex02-güncelleştirme bağımlılık Çözümleyicisi*)</span><span class="sxs-lookup"><span data-stu-id="38860-299">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Update Dependency Resolver*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample17.cs)]

    > [!NOTE]
    > <span data-ttu-id="38860-300">ASP.NET MVC varsayılan bağımlılık çözümleyici sınıfı sağlar.</span><span class="sxs-lookup"><span data-stu-id="38860-300">ASP.NET MVC provides a default dependency resolver class.</span></span> <span data-ttu-id="38860-301">Unity için oluşturduğumuz özel bağımlılık çözümleyicilerine göre çalışmak için, bu çözümleyici değiştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="38860-301">To work with custom dependency resolvers as the one we have created for unity, this resolver has to be replaced.</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="38860-302">Görev 4-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="38860-302">Task 4 - Running the Application</span></span>

<span data-ttu-id="38860-303">Bu görevde, mağaza tarayıcısının hizmeti tükettiğini ve görüntüyü ve alınan iletiyi gösterdiğini doğrulamak için uygulamayı çalıştıracaksınız:</span><span class="sxs-lookup"><span data-stu-id="38860-303">In this task, you will run the application to verify that the Store Browser consumes the service and shows the image and the message retrieved:</span></span>

1. <span data-ttu-id="38860-304">Uygulamayı çalıştırmak için **F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="38860-304">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="38860-305">Tarzlar menüsünde **rock** ' e tıklayın ve **MessageService** 'in görünüme nasıl eklendiğini ve hoş geldiniz iletisini ve görüntüsünü nasıl yüklei görün.</span><span class="sxs-lookup"><span data-stu-id="38860-305">Click **Rock** within the Genres Menu and see how the **MessageService** was injected to the view and loaded the welcome message and the image.</span></span> <span data-ttu-id="38860-306">Bu örnekte, &quot;**Rock**&quot;:</span><span class="sxs-lookup"><span data-stu-id="38860-306">In this example, we are entering to &quot;**Rock**&quot;:</span></span>

    <span data-ttu-id="38860-307">![MVC müzik deposu-görünüm ekleme](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC müzik deposu-görünüm ekleme")</span><span class="sxs-lookup"><span data-stu-id="38860-307">![MVC Music Store - View Injection](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC Music Store - View Injection")</span></span>

    <span data-ttu-id="38860-308">*MVC müzik deposu-görünüm ekleme*</span><span class="sxs-lookup"><span data-stu-id="38860-308">*MVC Music Store - View Injection*</span></span>
3. <span data-ttu-id="38860-309">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="38860-309">Close the browser.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Injecting_Action_Filters"></a>
### <a name="exercise-3-injecting-action-filters"></a><span data-ttu-id="38860-310">Alıştırma 3: ekleme eylem filtreleri</span><span class="sxs-lookup"><span data-stu-id="38860-310">Exercise 3: Injecting Action Filters</span></span>

<span data-ttu-id="38860-311">Önceki uygulamalı laboratuvar **özel eylem filtrelerinde** , filtre özelleştirme ve ekleme ile çalıştık.</span><span class="sxs-lookup"><span data-stu-id="38860-311">In the previous Hands-On lab **Custom Action Filters** you have worked with filters customization and injection.</span></span> <span data-ttu-id="38860-312">Bu alıştırmada, Unity kapsayıcısını kullanarak bağımlılık ekleme ile filtrelerin nasıl ekleneceğini öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-312">In this exercise, you will learn how to inject filters with Dependency Injection by using the Unity container.</span></span> <span data-ttu-id="38860-313">Bunu yapmak için, müzik deposu çözümüne, sitenin etkinliğini izleyen özel bir eylem filtresi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-313">To do that, you will add to the Music Store solution a custom action filter that will trace the activity of the site.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Including_the_Tracking_Filter_in_the_Solution"></a>
#### <a name="task-1---including-the-tracking-filter-in-the-solution"></a><span data-ttu-id="38860-314">Görev 1-çözüm içindeki Izleme Filtresi dahil</span><span class="sxs-lookup"><span data-stu-id="38860-314">Task 1 - Including the Tracking Filter in the Solution</span></span>

<span data-ttu-id="38860-315">Bu görevde,, olayları izlemek için özel bir eylem filtresi olan müzik deposuna dahil edersiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-315">In this task, you will include in the Music Store a custom action filter to trace events.</span></span> <span data-ttu-id="38860-316">Özel eylem filtresi kavramları zaten önceki laboratuvarda&quot;&quot;özel eylem filtrelerinde değerlendirildiğinden, filtre sınıfını bu laboratuvarın varlıklar klasöründen dahil eder ve ardından Unity için bir filtre sağlayıcısı oluşturursunuz:</span><span class="sxs-lookup"><span data-stu-id="38860-316">As custom action filter concepts are already treated in the previous Lab &quot;Custom Action Filters&quot;, you will just include the filter class from the Assets folder of this lab, and then create a Filter Provider for Unity:</span></span>

1. <span data-ttu-id="38860-317">**Source\ex03-ekleme Action Filter\begın** Folder konumundaki **Begin** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="38860-317">Open the **Begin** solution located in the **Source\Ex03 - Injecting Action Filter\Begin** folder.</span></span> <span data-ttu-id="38860-318">Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-318">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="38860-319">Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="38860-319">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="38860-320">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="38860-320">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="38860-321">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38860-321">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="38860-322">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="38860-322">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="38860-323">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="38860-323">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="38860-324">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-324">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="38860-325">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="38860-325">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="38860-326">Daha fazla bilgi için şu makaleye bakın: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span><span class="sxs-lookup"><span data-stu-id="38860-326">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="38860-327">**/Sources/varlıklarından** **/filters** klasöründen **TraceActionFilter.cs** dosyasını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="38860-327">Include **TraceActionFilter.cs** file from **/Sources/Assets** to **/Filters** folder.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample18.cs)]

    > [!NOTE]
    > <span data-ttu-id="38860-328">Bu özel eylem filtresi ASP.NET izlemeyi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="38860-328">This custom action filter performs ASP.NET tracing.</span></span> <span data-ttu-id="38860-329">Daha fazla başvuru için &quot;ASP.NET MVC 4 yerel ve dinamik eylem filtrelerini&quot; Laboratuvarı kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-329">You can check &quot;ASP.NET MVC 4 local and Dynamic Action Filters&quot; Lab for more reference.</span></span>
3. <span data-ttu-id="38860-330">**FilterProvider.cs** boş sınıfını **/Filters.** klasörüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="38860-330">Add the empty class **FilterProvider.cs** to the project in the folder **/Filters.**</span></span>
4. <span data-ttu-id="38860-331">**FilterProvider.cs**içinde **System. Web. Mvc** ve **Microsoft. Yöntemler. Unity** ad alanlarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="38860-331">Add the **System.Web.Mvc** and **Microsoft.Practices.Unity** namespaces in **FilterProvider.cs**.</span></span>

    <span data-ttu-id="38860-332">(Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex03-filtre sağlayıcısı ad alanları ekleme*)</span><span class="sxs-lookup"><span data-stu-id="38860-332">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample19.cs)]
5. <span data-ttu-id="38860-333">Sınıfın **IFilterProvider** arabiriminden devralmasını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="38860-333">Make the class inherit from **IFilterProvider** Interface.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample20.cs)]
6. <span data-ttu-id="38860-334">**FilterProvider** sınıfına bir **ıunitycontainer** özelliği ekleyin ve kapsayıcıyı atamak için bir sınıf Oluşturucu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="38860-334">Add a **IUnityContainer** property in the **FilterProvider** class, and then create a class constructor to assign the container.</span></span>

    <span data-ttu-id="38860-335">(Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex03-filtre sağlayıcısı Oluşturucusu*)</span><span class="sxs-lookup"><span data-stu-id="38860-335">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider Constructor*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample21.cs)]

    > [!NOTE]
    > <span data-ttu-id="38860-336">Filtre sağlayıcısı sınıf Oluşturucusu içinde **Yeni** bir nesne oluşturmamıyor.</span><span class="sxs-lookup"><span data-stu-id="38860-336">The filter provider class constructor is not creating a **new** object inside.</span></span> <span data-ttu-id="38860-337">Kapsayıcı bir parametre olarak geçirilir ve bağımlılık Unity tarafından çözülür.</span><span class="sxs-lookup"><span data-stu-id="38860-337">The container is passed as a parameter, and the dependency is solved by Unity.</span></span>
7. <span data-ttu-id="38860-338">**FilterProvider** sınıfında, **IFilterProvider** arabiriminden **GetFilters** yöntemini uygulayın.</span><span class="sxs-lookup"><span data-stu-id="38860-338">In the **FilterProvider** class, implement the method **GetFilters** from **IFilterProvider** interface.</span></span>

    <span data-ttu-id="38860-339">(Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex03-filtre sağlayıcısı GetFilters*)</span><span class="sxs-lookup"><span data-stu-id="38860-339">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider GetFilters*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample22.cs)]

<a id="Ex3Task2"></a>

<a id="Task_2_-_Registering_and_Enabling_the_Filter"></a>
#### <a name="task-2---registering-and-enabling-the-filter"></a><span data-ttu-id="38860-340">Görev 2-filtreyi kaydetme ve etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="38860-340">Task 2 - Registering and Enabling the Filter</span></span>

<span data-ttu-id="38860-341">Bu görevde site izlemeyi etkinleştirecektir.</span><span class="sxs-lookup"><span data-stu-id="38860-341">In this task, you will enable site tracking.</span></span> <span data-ttu-id="38860-342">Bunu yapmak için, izlemeye başlamak için filtreyi **Bootstrapper.cs BuildUnityContainer** yöntemine kaydedersiniz:</span><span class="sxs-lookup"><span data-stu-id="38860-342">To do that, you will register the filter in **Bootstrapper.cs BuildUnityContainer** method to start tracing:</span></span>

1. <span data-ttu-id="38860-343">Proje kökünde bulunan **Web. config** dosyasını açın ve System. Web grubunda izleme izlemeyi etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="38860-343">Open **Web.config** located in the project root and enable trace tracking at System.Web group.</span></span>

    [!code-xml[Main](aspnet-mvc-4-dependency-injection/samples/sample23.xml)]
2. <span data-ttu-id="38860-344">Proje kökünde **Bootstrapper.cs** öğesini açın.</span><span class="sxs-lookup"><span data-stu-id="38860-344">Open **Bootstrapper.cs** at project root.</span></span>
3. <span data-ttu-id="38860-345">**Mvcmusicstore. Filters** ad alanına bir başvuru ekleyin.</span><span class="sxs-lookup"><span data-stu-id="38860-345">Add a reference to the **MvcMusicStore.Filters** namespace.</span></span>

    <span data-ttu-id="38860-346">(Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex03-önyükleyici ekleme ad alanı*)</span><span class="sxs-lookup"><span data-stu-id="38860-346">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Bootstrapper Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample24.cs)]
4. <span data-ttu-id="38860-347">**Buildunitycontainer** yöntemini seçin ve filtreyi Unity kapsayıcısına kaydedin.</span><span class="sxs-lookup"><span data-stu-id="38860-347">Select the **BuildUnityContainer** method and register the filter in the Unity Container.</span></span> <span data-ttu-id="38860-348">Filtre sağlayıcısını ve eylem filtresini kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="38860-348">You will have to register the filter provider as well as the action filter.</span></span>

    <span data-ttu-id="38860-349">(Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex03-Register FilterProvider ve ActionFilter*)</span><span class="sxs-lookup"><span data-stu-id="38860-349">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Register FilterProvider and ActionFilter*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample25.cs)]

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="38860-350">Görev 3-uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="38860-350">Task 3 - Running the Application</span></span>

<span data-ttu-id="38860-351">Bu görevde, uygulamayı çalıştıracaksınız ve özel eylem filtresinin etkinliğin izlenmesini test edersiniz:</span><span class="sxs-lookup"><span data-stu-id="38860-351">In this task, you will run the application and test that the custom action filter is tracing the activity:</span></span>

1. <span data-ttu-id="38860-352">Uygulamayı çalıştırmak için **F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="38860-352">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="38860-353">Tarzlar menüsünde **rock** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38860-353">Click **Rock** within the Genres Menu.</span></span> <span data-ttu-id="38860-354">İsterseniz daha fazla tarzya gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-354">You can browse to more genres if you want to.</span></span>

    <span data-ttu-id="38860-355">![Müzik Deposu](aspnet-mvc-4-dependency-injection/_static/image11.png "Müzik Deposu")</span><span class="sxs-lookup"><span data-stu-id="38860-355">![Music Store](aspnet-mvc-4-dependency-injection/_static/image11.png "Music Store")</span></span>

    <span data-ttu-id="38860-356">*Müzik Deposu*</span><span class="sxs-lookup"><span data-stu-id="38860-356">*Music Store*</span></span>
3. <span data-ttu-id="38860-357">Uygulama Izleme sayfasını görmek için **/Trace.exe** öğesine gidin ve **Ayrıntıları görüntüle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38860-357">Browse to **/Trace.axd** to see the Application Trace page, and then click **View Details**.</span></span>

    <span data-ttu-id="38860-358">![Uygulama Izleme günlüğü](aspnet-mvc-4-dependency-injection/_static/image12.png "Uygulama Izleme günlüğü")</span><span class="sxs-lookup"><span data-stu-id="38860-358">![Application Trace Log](aspnet-mvc-4-dependency-injection/_static/image12.png "Application Trace Log")</span></span>

    <span data-ttu-id="38860-359">*Uygulama Izleme günlüğü*</span><span class="sxs-lookup"><span data-stu-id="38860-359">*Application Trace Log*</span></span>

    <span data-ttu-id="38860-360">![Uygulama Izleme-Istek ayrıntıları](aspnet-mvc-4-dependency-injection/_static/image13.png "Uygulama Izleme-Istek ayrıntıları")</span><span class="sxs-lookup"><span data-stu-id="38860-360">![Application Trace - Request Details](aspnet-mvc-4-dependency-injection/_static/image13.png "Application Trace - Request Details")</span></span>

    <span data-ttu-id="38860-361">*Uygulama Izleme-Istek ayrıntıları*</span><span class="sxs-lookup"><span data-stu-id="38860-361">*Application Trace - Request Details*</span></span>
4. <span data-ttu-id="38860-362">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="38860-362">Close the browser.</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="38860-363">Özet</span><span class="sxs-lookup"><span data-stu-id="38860-363">Summary</span></span>

<span data-ttu-id="38860-364">Bu uygulamalı Laboratuvarı tamamlayarak, bir NuGet paketi kullanarak Unity 'yi tümleştirerek ASP.NET MVC 4 ' te bağımlılık ekleme 'nin nasıl kullanılacağını öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-364">By completing this Hands-On Lab you have learned how to use Dependency Injection in ASP.NET MVC 4 by integrating Unity using a NuGet Package.</span></span> <span data-ttu-id="38860-365">Bunu başarmak için, denetleyiciler, görünümler ve eylem filtreleri içinde bağımlılık ekleme 'yi kullandınız.</span><span class="sxs-lookup"><span data-stu-id="38860-365">To achieve that, you have used Dependency Injection inside controllers, views and action filters.</span></span>

<span data-ttu-id="38860-366">Aşağıdaki kavramlar ele alınmıştır:</span><span class="sxs-lookup"><span data-stu-id="38860-366">The following concepts were covered:</span></span>

- <span data-ttu-id="38860-367">ASP.NET MVC 4 bağımlılığı ekleme özellikleri</span><span class="sxs-lookup"><span data-stu-id="38860-367">ASP.NET MVC 4 Dependency Injection features</span></span>
- <span data-ttu-id="38860-368">Unity. Mvc3 NuGet paketini kullanarak Unity tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="38860-368">Unity integration using Unity.Mvc3 NuGet Package</span></span>
- <span data-ttu-id="38860-369">Denetleyicilere bağımlılık ekleme</span><span class="sxs-lookup"><span data-stu-id="38860-369">Dependency Injection in Controllers</span></span>
- <span data-ttu-id="38860-370">Görünümlerde bağımlılık ekleme</span><span class="sxs-lookup"><span data-stu-id="38860-370">Dependency Injection in Views</span></span>
- <span data-ttu-id="38860-371">Eylem filtrelerinin bağımlılık ekleme</span><span class="sxs-lookup"><span data-stu-id="38860-371">Dependency injection of Action Filters</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="38860-372">Ek A: Web için Visual Studio Express 2012 yükleme</span><span class="sxs-lookup"><span data-stu-id="38860-372">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="38860-373">**[Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)** kullanarak **Web için Microsoft Visual Studio Express 2012** veya başka bir &quot;Express&quot; sürümü yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-373">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="38860-374">Aşağıdaki yönergeler *Microsoft Web Platformu Yükleyicisi*kullanarak *Web Için Visual Studio Express 2012* ' i yüklemek için gereken adımlarda size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="38860-374">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="38860-375">[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169) kısmına gidin.</span><span class="sxs-lookup"><span data-stu-id="38860-375">Go to [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="38860-376">Alternatif olarak, Web Platformu Yükleyicisi zaten yüklüyse, <em>Microsoft Azure SDK&quot;Ile Web için Visual Studio Express 2012</em> &quot;ürünü açabilir ve bunu arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-376">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="38860-377">**Şimdi yüklensin**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38860-377">Click on **Install Now**.</span></span> <span data-ttu-id="38860-378">**Web platformu yükleyicinizi** yoksa, önce indirmek ve yüklemek üzere yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-378">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="38860-379">**Web Platformu Yükleyicisi** açıkken, kurulum 'u başlatmak için **yükleme** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38860-379">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="38860-380">![Visual Studio Express yüklensin](aspnet-mvc-4-dependency-injection/_static/image14.png "Visual Studio Express yüklensin")</span><span class="sxs-lookup"><span data-stu-id="38860-380">![Install Visual Studio Express](aspnet-mvc-4-dependency-injection/_static/image14.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="38860-381">*Visual Studio Express yüklensin*</span><span class="sxs-lookup"><span data-stu-id="38860-381">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="38860-382">Tüm ürünlerin lisanslarını ve koşullarını okuyun ve devam etmek için **kabul ediyorum** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38860-382">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Lisans koşullarını kabul etme](aspnet-mvc-4-dependency-injection/_static/image15.png)

    <span data-ttu-id="38860-384">*Lisans koşullarını kabul etme*</span><span class="sxs-lookup"><span data-stu-id="38860-384">*Accepting the license terms*</span></span>
5. <span data-ttu-id="38860-385">İndirme ve yükleme işlemi tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="38860-385">Wait until the downloading and installation process completes.</span></span>

    ![Yükleme ilerleme durumu](aspnet-mvc-4-dependency-injection/_static/image16.png)

    <span data-ttu-id="38860-387">*Yükleme ilerleme durumu*</span><span class="sxs-lookup"><span data-stu-id="38860-387">*Installation progress*</span></span>
6. <span data-ttu-id="38860-388">Yükleme tamamlandığında **son**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38860-388">When the installation completes, click **Finish**.</span></span>

    ![Yükleme tamamlandı](aspnet-mvc-4-dependency-injection/_static/image17.png)

    <span data-ttu-id="38860-390">*Yükleme tamamlandı*</span><span class="sxs-lookup"><span data-stu-id="38860-390">*Installation completed*</span></span>
7. <span data-ttu-id="38860-391">Web Platformu Yükleyicisi 'ni kapatmak için **Çıkış** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38860-391">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="38860-392">Web için Visual Studio Express açmak için **Başlangıç** ekranına gidin ve &quot;**vs Express**&quot;yazmaya başlayın ve ardından **Web için vs Express** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38860-392">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Web için VS Express kutucuğu](aspnet-mvc-4-dependency-injection/_static/image18.png)

    <span data-ttu-id="38860-394">*Web için VS Express kutucuğu*</span><span class="sxs-lookup"><span data-stu-id="38860-394">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="38860-395">Ek B: kod parçacıklarını kullanma</span><span class="sxs-lookup"><span data-stu-id="38860-395">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="38860-396">Kod parçacıkları ile, ihtiyacınız olan tüm koda parmaklarınızın elinizin altında olmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38860-396">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="38860-397">Laboratuvar belgesi, aşağıdaki şekilde gösterildiği gibi, bunları yalnızca ne zaman kullanacağınızı söyleyecektir.</span><span class="sxs-lookup"><span data-stu-id="38860-397">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="38860-398">![Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma](aspnet-mvc-4-dependency-injection/_static/image19.png "Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma")</span><span class="sxs-lookup"><span data-stu-id="38860-398">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-dependency-injection/_static/image19.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="38860-399">*Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma*</span><span class="sxs-lookup"><span data-stu-id="38860-399">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="38860-400">***Klavyeyi kullanarak bir kod parçacığı eklemek için (C# yalnızca)***</span><span class="sxs-lookup"><span data-stu-id="38860-400">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="38860-401">Kodu eklemek istediğiniz yere imleci yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="38860-401">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="38860-402">Kod parçacığı adını yazmaya başlayın (boşluk veya tire olmadan).</span><span class="sxs-lookup"><span data-stu-id="38860-402">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="38860-403">IntelliSense, eşleşen kod parçacıklarının adlarını gösterdiği gibi izleyin.</span><span class="sxs-lookup"><span data-stu-id="38860-403">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="38860-404">Doğru kod parçacığını seçin (veya tüm kod parçacığının adı seçilene kadar yazmaya devam edin).</span><span class="sxs-lookup"><span data-stu-id="38860-404">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="38860-405">Kod parçacığını imleç konumuna eklemek için SEKME tuşuna iki kez basın.</span><span class="sxs-lookup"><span data-stu-id="38860-405">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="38860-406">![Kod parçacığı adını yazmaya başlayın](aspnet-mvc-4-dependency-injection/_static/image20.png "Kod parçacığı adını yazmaya başlayın")</span><span class="sxs-lookup"><span data-stu-id="38860-406">![Start typing the snippet name](aspnet-mvc-4-dependency-injection/_static/image20.png "Start typing the snippet name")</span></span>

<span data-ttu-id="38860-407">*Kod parçacığı adını yazmaya başlayın*</span><span class="sxs-lookup"><span data-stu-id="38860-407">*Start typing the snippet name*</span></span>

<span data-ttu-id="38860-408">![Vurgulanan parçacığı seçmek için Tab tuşuna basın](aspnet-mvc-4-dependency-injection/_static/image21.png "Vurgulanan parçacığı seçmek için Tab tuşuna basın")</span><span class="sxs-lookup"><span data-stu-id="38860-408">![Press Tab to select the highlighted snippet](aspnet-mvc-4-dependency-injection/_static/image21.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="38860-409">*Vurgulanan parçacığı seçmek için Tab tuşuna basın*</span><span class="sxs-lookup"><span data-stu-id="38860-409">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="38860-410">![Sekmeye tekrar basın ve kod parçacığı genişletilir](aspnet-mvc-4-dependency-injection/_static/image22.png "Sekmeye tekrar basın ve kod parçacığı genişletilir")</span><span class="sxs-lookup"><span data-stu-id="38860-410">![Press Tab again and the snippet will expand](aspnet-mvc-4-dependency-injection/_static/image22.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="38860-411">*Sekmeye tekrar basın ve kod parçacığı genişletilir*</span><span class="sxs-lookup"><span data-stu-id="38860-411">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="38860-412">***Fareyi kullanarak bir kod parçacığı eklemek için (C#, Visual Basic ve XML)*** 1.</span><span class="sxs-lookup"><span data-stu-id="38860-412">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="38860-413">Kod parçacığını eklemek istediğiniz yere sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38860-413">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="38860-414">Kod **parçacığı Ekle** ' yi ve ardından **kod parçacıklarını**seçin.</span><span class="sxs-lookup"><span data-stu-id="38860-414">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="38860-415">Listeden tıklatarak ilgili kod parçacığını seçin.</span><span class="sxs-lookup"><span data-stu-id="38860-415">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="38860-416">![Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.](aspnet-mvc-4-dependency-injection/_static/image23.png "Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.")</span><span class="sxs-lookup"><span data-stu-id="38860-416">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-dependency-injection/_static/image23.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="38860-417">*Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.*</span><span class="sxs-lookup"><span data-stu-id="38860-417">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="38860-418">![Listeden tıklatarak ilgili kod parçacığını seçin](aspnet-mvc-4-dependency-injection/_static/image24.png "Listeden tıklatarak ilgili kod parçacığını seçin")</span><span class="sxs-lookup"><span data-stu-id="38860-418">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-dependency-injection/_static/image24.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="38860-419">*Listeden tıklatarak ilgili kod parçacığını seçin*</span><span class="sxs-lookup"><span data-stu-id="38860-419">*Pick the relevant snippet from the list, by clicking on it*</span></span>
