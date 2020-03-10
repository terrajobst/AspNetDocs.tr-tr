---
uid: aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
title: OWıN ve Katana ile çalışmaya başlama | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 09/27/2013
ms.assetid: 6dae249f-5ac6-4f6e-bc49-13bcd5a54a70
msc.legacyurl: /aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
msc.type: authoredcontent
ms.openlocfilehash: 4dfd7b8ebb2bb48d7ef800fd522b79a7b4a045c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584674"
---
# <a name="getting-started-with-owin-and-katana"></a><span data-ttu-id="e1295-102">OWIN ve Katana ile Çalışmaya Başlama</span><span class="sxs-lookup"><span data-stu-id="e1295-102">Getting Started with OWIN and Katana</span></span>

<span data-ttu-id="e1295-103">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="e1295-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="e1295-104">[.Net Için açık Web arabirimi (OWıN)](http://owin.org/) , .NET Web sunucuları ile Web uygulamaları arasında bir soyutlama tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e1295-104">[Open Web Interface for .NET (OWIN)](http://owin.org/) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="e1295-105">OWIN, Web sunucusunu uygulamadan ayırarak .NET Web geliştirme için ara yazılım oluşturmayı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="e1295-105">By decoupling the web server from the application, OWIN makes it easier to create middleware for .NET web development.</span></span> <span data-ttu-id="e1295-106">Ayrıca, OWIN, Web uygulamalarının diğer konaklara&#8212;, örneğin bir Windows hizmetinde veya başka bir işlemde kendi kendine barındırılmasına yönelik bağlantı noktasını daha kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="e1295-106">Also, OWIN makes it easier to port web applications to other hosts&#8212;for example, self-hosting in a Windows service or other process.</span></span>

<span data-ttu-id="e1295-107">OWIN, bir uygulama değil, topluluğa ait bir belirtimdir.</span><span class="sxs-lookup"><span data-stu-id="e1295-107">OWIN is a community-owned specification, not an implementation.</span></span> <span data-ttu-id="e1295-108">Katana proje, Microsoft tarafından geliştirilen açık kaynaklı bir OWIN bileşenleri kümesidir.</span><span class="sxs-lookup"><span data-stu-id="e1295-108">The Katana project is a set of open-source OWIN components developed by Microsoft.</span></span> <span data-ttu-id="e1295-109">Hem OWIN hem de Katana 'ya genel bir bakış için bkz. [Proje Katana 'Ya genel bakış](an-overview-of-project-katana.md).</span><span class="sxs-lookup"><span data-stu-id="e1295-109">For a general overview of both OWIN and Katana, see [An Overview of Project Katana](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="e1295-110">Bu makalede, başlamak için hemen koda atlayacağım.</span><span class="sxs-lookup"><span data-stu-id="e1295-110">In this article, I will jump right into code to get started.</span></span>

<span data-ttu-id="e1295-111">Bu öğretici [Visual Studio 2013 Sürüm adayını](https://go.microsoft.com/fwlink/?LinkId=306566)kullanır, ancak Visual Studio 2012 ' i de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1295-111">This tutorial uses [Visual Studio 2013 Release Candidate](https://go.microsoft.com/fwlink/?LinkId=306566), but you can also use Visual Studio 2012.</span></span> <span data-ttu-id="e1295-112">Visual Studio 2012 ' de birkaç adım daha farklı olduğundan, aşağıda notlıyorum.</span><span class="sxs-lookup"><span data-stu-id="e1295-112">A few of the steps are different in Visual Studio 2012, which I note below.</span></span>

## <a name="host-owin-in-iis"></a><span data-ttu-id="e1295-113">IIS 'de OWIN Konağı</span><span class="sxs-lookup"><span data-stu-id="e1295-113">Host OWIN in IIS</span></span>

<span data-ttu-id="e1295-114">Bu bölümde, IIS 'de OWıN barındırılırsınız.</span><span class="sxs-lookup"><span data-stu-id="e1295-114">In this section, we'll host OWIN in IIS.</span></span> <span data-ttu-id="e1295-115">Bu seçenek, bir OWIN işlem hattının esneklik ve bir şekilde bir arada olmasını, IIS 'nin yetişkinlere yönelik özellik kümesiyle birlikte sağlar.</span><span class="sxs-lookup"><span data-stu-id="e1295-115">This option gives you the flexibility and composability of an OWIN pipeline together with the mature feature set of IIS.</span></span> <span data-ttu-id="e1295-116">Bu seçeneği kullanarak OWIN uygulaması ASP.NET istek ardışık düzeninde çalışır.</span><span class="sxs-lookup"><span data-stu-id="e1295-116">Using this option, the OWIN application runs in the ASP.NET request pipeline.</span></span>

<span data-ttu-id="e1295-117">İlk olarak, yeni bir ASP.NET Web uygulaması projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e1295-117">First, create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="e1295-118">(Visual Studio 2012 ' de ASP.NET boş Web uygulaması proje türünü kullanın.)</span><span class="sxs-lookup"><span data-stu-id="e1295-118">(In Visual Studio 2012, use the ASP.NET Empty Web Application project type.)</span></span>

![](getting-started-with-owin-and-katana/_static/image1.png)

<span data-ttu-id="e1295-119">**Yeni ASP.NET projesi** Iletişim kutusunda **boş** şablonu seçin.</span><span class="sxs-lookup"><span data-stu-id="e1295-119">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span>

![](getting-started-with-owin-and-katana/_static/image2.png)

### <a name="add-nuget-packages"></a><span data-ttu-id="e1295-120">NuGet paketleri Ekle</span><span class="sxs-lookup"><span data-stu-id="e1295-120">Add NuGet Packages</span></span>

<span data-ttu-id="e1295-121">Ardından, gerekli NuGet paketlerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e1295-121">Next, add the required NuGet packages.</span></span> <span data-ttu-id="e1295-122">**Araçlar** menüsünde **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="e1295-122">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="e1295-123">Paket Yöneticisi konsolu penceresinde aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="e1295-123">In the Package Manager Console window, type the following command:</span></span>

`install-package Microsoft.Owin.Host.SystemWeb –Pre`

![](getting-started-with-owin-and-katana/_static/image3.png)

### <a name="add-a-startup-class"></a><span data-ttu-id="e1295-124">Başlangıç sınıfı ekleme</span><span class="sxs-lookup"><span data-stu-id="e1295-124">Add a Startup Class</span></span>

<span data-ttu-id="e1295-125">Ardından, bir OWıN başlangıç sınıfı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e1295-125">Next, add an OWIN startup class.</span></span> <span data-ttu-id="e1295-126">Çözüm Gezgini, projeye sağ tıklayın ve **Ekle**' yi ve ardından **Yeni öğe**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e1295-126">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span> <span data-ttu-id="e1295-127">**Yeni öğe Ekle** Iletişim kutusunda **owın başlangıç sınıfı**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="e1295-127">In the **Add New Item** dialog, select **Owin Startup class**.</span></span> <span data-ttu-id="e1295-128">Başlangıç sınıfını yapılandırma hakkında daha fazla bilgi için, bkz. [Owın başlangıç sınıfı algılama](owin-startup-class-detection.md).</span><span class="sxs-lookup"><span data-stu-id="e1295-128">For more info on configuring the startup class, see [OWIN Startup Class Detection](owin-startup-class-detection.md).</span></span>

![](getting-started-with-owin-and-katana/_static/image4.png)

<span data-ttu-id="e1295-129">`Startup1.Configuration` yöntemine aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e1295-129">Add the following code to the `Startup1.Configuration` method:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample1.cs?highlight=3)]

<span data-ttu-id="e1295-130">Bu kod, OWıN ardışık düzenine bir **Microsoft. Owin. ıowincontext** örneği alan bir işlev olarak uygulanan basit bir ara yazılım parçası ekler.</span><span class="sxs-lookup"><span data-stu-id="e1295-130">This code adds a simple piece of middleware to the OWIN pipeline, implemented as a function that receives a **Microsoft.Owin.IOwinContext** instance.</span></span> <span data-ttu-id="e1295-131">Sunucu bir HTTP isteği aldığında, OWıN işlem hattı ara yazılımı çağırır.</span><span class="sxs-lookup"><span data-stu-id="e1295-131">When the server receives an HTTP request, the OWIN pipeline invokes the middleware.</span></span> <span data-ttu-id="e1295-132">Ara yazılım, yanıt için içerik türünü ayarlar ve yanıt gövdesini yazar.</span><span class="sxs-lookup"><span data-stu-id="e1295-132">The middleware sets the content type for the response and writes the response body.</span></span>

> [!NOTE]
> <span data-ttu-id="e1295-133">OWıN başlangıç sınıfı şablonu Visual Studio 2013 kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e1295-133">The OWIN Startup class template is available in Visual Studio 2013.</span></span> <span data-ttu-id="e1295-134">Visual Studio 2012 kullanıyorsanız, yalnızca `Startup1`adlı yeni bir boş sınıf ekleyin ve aşağıdaki kodu yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="e1295-134">If you are using Visual Studio 2012, just add a new empty class named `Startup1`, and paste in the following code:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample2.cs)]

### <a name="run-the-application"></a><span data-ttu-id="e1295-135">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="e1295-135">Run the Application</span></span>

<span data-ttu-id="e1295-136">Hata ayıklamaya başlamak için F5 'e basın.</span><span class="sxs-lookup"><span data-stu-id="e1295-136">Press F5 to begin debugging.</span></span> <span data-ttu-id="e1295-137">Visual Studio, `http://localhost:*port*/`için bir tarayıcı penceresi açar.</span><span class="sxs-lookup"><span data-stu-id="e1295-137">Visual Studio will open a browser window to `http://localhost:*port*/`.</span></span> <span data-ttu-id="e1295-138">Sayfa aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="e1295-138">The page should look like the following:</span></span>

![](getting-started-with-owin-and-katana/_static/image5.png)

## <a name="self-host-owin-in-a-console-application"></a><span data-ttu-id="e1295-139">Konsol uygulamasındaki Self-Host OWIN</span><span class="sxs-lookup"><span data-stu-id="e1295-139">Self-Host OWIN in a Console Application</span></span>

<span data-ttu-id="e1295-140">Bu uygulamayı IIS barındırmanın özel bir işlemde kendi kendine barındırılmasına dönüştürmek çok kolay.</span><span class="sxs-lookup"><span data-stu-id="e1295-140">It's easy to convert this application from IIS hosting to self-hosting in a custom process.</span></span> <span data-ttu-id="e1295-141">IIS barındırma ile IIS, hem HTTP sunucusu hem de hizmeti barındıran işlem olarak davranır.</span><span class="sxs-lookup"><span data-stu-id="e1295-141">With IIS hosting, IIS acts as both the HTTP server and as the process that hosts the service.</span></span> <span data-ttu-id="e1295-142">Kendi kendine barındırma ile, uygulamanız süreci oluşturur ve HTTP sunucusu olarak **HttpListener** sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="e1295-142">With self-hosting, your application creates the process and uses the **HttpListener** class as the HTTP server.</span></span>

<span data-ttu-id="e1295-143">Visual Studio 'da yeni bir konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e1295-143">In Visual Studio, create a new console application.</span></span> <span data-ttu-id="e1295-144">Paket Yöneticisi konsolu penceresinde aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="e1295-144">In the Package Manager Console window, type the following command:</span></span>

`Install-Package Microsoft.Owin.SelfHost -Pre`

<span data-ttu-id="e1295-145">Bu öğreticinin 1. bölümünde projeye `Startup1` bir sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e1295-145">Add a `Startup1` class from part 1 of this tutorial to the project.</span></span> <span data-ttu-id="e1295-146">Bu sınıfı değiştirmenize gerek yok.</span><span class="sxs-lookup"><span data-stu-id="e1295-146">You don't need to modify this class.</span></span>

<span data-ttu-id="e1295-147">Uygulamanın `Main` yöntemini aşağıdaki şekilde uygulayın.</span><span class="sxs-lookup"><span data-stu-id="e1295-147">Implement the application's `Main` method as follows.</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample3.cs)]

<span data-ttu-id="e1295-148">Konsol uygulamasını çalıştırdığınızda, sunucu `http://localhost:9000`dinlemeye başlar.</span><span class="sxs-lookup"><span data-stu-id="e1295-148">When you run the console application, the server starts listening to `http://localhost:9000`.</span></span> <span data-ttu-id="e1295-149">Bu adrese bir Web tarayıcısında gittiğinizde, "Merhaba Dünya" sayfasını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="e1295-149">If you navigate to this address in a web browser, you will see the "Hello world" page.</span></span>

![](getting-started-with-owin-and-katana/_static/image6.png)

## <a name="add-owin-diagnostics"></a><span data-ttu-id="e1295-150">OWıN tanılamayı ekleme</span><span class="sxs-lookup"><span data-stu-id="e1295-150">Add OWIN Diagnostics</span></span>

<span data-ttu-id="e1295-151">Microsoft. Owin. Diagnostics paketi işlenmemiş özel durumları yakalayan ve hata ayrıntıları içeren bir HTML sayfası görüntüleyen ara yazılım içerir.</span><span class="sxs-lookup"><span data-stu-id="e1295-151">The Microsoft.Owin.Diagnostics package contains middleware that catches unhandled exceptions and displays an HTML page with error details.</span></span> <span data-ttu-id="e1295-152">Bu sayfa, bazen "[sarı ekran](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)hatası" (Ysod) olarak adlandırılan ASP.NET hata sayfasına benzer şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="e1295-152">This page functions much like the ASP.NET error page that is sometimes called the "[yellow screen of death](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)" (YSOD).</span></span> <span data-ttu-id="e1295-153">YSOD gibi, Katana hata sayfası geliştirme sırasında faydalıdır, ancak üretim modunda devre dışı bırakmak iyi bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="e1295-153">Like the YSOD, the Katana error page is useful during development, but it's a good practice to disable it in production mode.</span></span>

<span data-ttu-id="e1295-154">Tanılama paketini projenize yüklemek için, Paket Yöneticisi konsol penceresine aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="e1295-154">To install the Diagnostics package in your project, type the following command in the Package Manager Console window:</span></span>

`install-package Microsoft.Owin.Diagnostics –Pre`

<span data-ttu-id="e1295-155">`Startup1.Configuration` yöntemdeki kodu aşağıdaki gibi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="e1295-155">Change the code in your `Startup1.Configuration` method as follows:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample4.cs?highlight=4,9-12)]

<span data-ttu-id="e1295-156">Şimdi, Visual Studio 'Nun özel durum üzerinde kesintiye uğramaması için, uygulamayı hata ayıklamadan çalıştırmak için CTRL + F5 kullanın.</span><span class="sxs-lookup"><span data-stu-id="e1295-156">Now use CTRL+F5 to run the application without debugging, so that Visual Studio will not break on the exception.</span></span> <span data-ttu-id="e1295-157">Uygulama, `http://localhost/fail`' a gitene kadar, uygulamanın özel durumu oluşturulduğu noktada, önceki ile aynı şekilde davranır.</span><span class="sxs-lookup"><span data-stu-id="e1295-157">The application behaves the same as before, until you navigate to `http://localhost/fail`, at which point the application throws the exception.</span></span> <span data-ttu-id="e1295-158">Hata sayfası ara yazılımı, özel durumu yakalar ve hata hakkında bilgi içeren bir HTML sayfası görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e1295-158">The error page middleware will catch the exception and display an HTML page with information about the error.</span></span> <span data-ttu-id="e1295-159">Yığın, sorgu dizesi, tanımlama bilgileri, istek üst bilgisi ve OWıN ortam değişkenlerini görmek için sekmelere tıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1295-159">You can click the tabs to see the stack, query string, cookies, request header, and OWIN environment variables.</span></span>

![](getting-started-with-owin-and-katana/_static/image7.png)

## <a name="next-steps"></a><span data-ttu-id="e1295-160">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="e1295-160">Next Steps</span></span>

- [<span data-ttu-id="e1295-161">OWIN Başlangıç Sınıfı Algılama</span><span class="sxs-lookup"><span data-stu-id="e1295-161">OWIN Startup Class Detection</span></span>](owin-startup-class-detection.md)
- [<span data-ttu-id="e1295-162">OWıN kullanarak Self-Host ASP.NET Web API 'SI</span><span class="sxs-lookup"><span data-stu-id="e1295-162">Use OWIN to Self-Host ASP.NET Web API</span></span>](../../../web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)
- [<span data-ttu-id="e1295-163">OWIN 'ı kullanarak kendi kendini barındırın SignalR</span><span class="sxs-lookup"><span data-stu-id="e1295-163">Use OWIN to Self-Host SignalR</span></span>](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)
