---
uid: aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
title: Katana 'da Windows kimlik doğrulamasını etkinleştirme | Microsoft Docs
author: MikeWasson
description: "Bu makalede, Katana 'da Windows kimlik doğrulamasının nasıl etkinleştirileceği gösterilmektedir. İki senaryo vardır: IIS kullanarak Katana barındırmak ve HttpListener 'ı Self-Host kat 'a kullanma..."
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 82324ef0-3b75-4f63-a217-76ef4036ec93
msc.legacyurl: /aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
msc.type: authoredcontent
ms.openlocfilehash: 3d81e7e1bf13ab63417378fba0c5ab80213f404b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617182"
---
# <a name="enabling-windows-authentication-in-katana"></a><span data-ttu-id="f11ea-104">Katana’da Windows Kimlik Doğrulamasını Etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f11ea-104">Enabling Windows Authentication in Katana</span></span>

<span data-ttu-id="f11ea-105">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="f11ea-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="f11ea-106">Bu makalede, Katana 'da Windows kimlik doğrulamasının nasıl etkinleştirileceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f11ea-106">This article shows how to enable Windows Authentication in Katana.</span></span> <span data-ttu-id="f11ea-107">İki senaryo ele alınmaktadır: Katana barındırmak için IIS kullanma ve özel bir işlemde bağımsız olarak kendi kendine konak Katana eklemek için HttpListener kullanma.</span><span class="sxs-lookup"><span data-stu-id="f11ea-107">It covers two scenarios: Using IIS to host Katana, and using HttpListener to self-host Katana in a custom process.</span></span> <span data-ttu-id="f11ea-108">Bu makaleyi gözden geçirmek için Barry Dorrans, David Matson ve Chris 'e teşekkür ederiz.</span><span class="sxs-lookup"><span data-stu-id="f11ea-108">Thanks to Barry Dorrans, David Matson, and Chris Ross for reviewing this article.</span></span>

<span data-ttu-id="f11ea-109">Katana, Microsoft 'un .NET için açık Web arabirimi olan [Owin](http://owin.org/)uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="f11ea-109">Katana is Microsoft's implementation of [OWIN](http://owin.org/), the Open Web Interface for .NET.</span></span> <span data-ttu-id="f11ea-110">OWıN ve Katana 'ya giriş bilgilerini [burada](an-overview-of-project-katana.md)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f11ea-110">You can read an introduction to OWIN and Katana [here](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="f11ea-111">OWIN mimarisi birçok katmana sahiptir:</span><span class="sxs-lookup"><span data-stu-id="f11ea-111">The OWIN architecture has several layers:</span></span>

- <span data-ttu-id="f11ea-112">Ana bilgisayar: OWıN ardışık düzeninin çalıştırıldığı işlemi yönetir.</span><span class="sxs-lookup"><span data-stu-id="f11ea-112">Host: Manages the process in which the OWIN pipeline runs.</span></span>
- <span data-ttu-id="f11ea-113">Sunucu: bir ağ yuvası açar ve istekleri dinler.</span><span class="sxs-lookup"><span data-stu-id="f11ea-113">Server: Opens a network socket and listens for requests.</span></span>
- <span data-ttu-id="f11ea-114">Ara yazılım: HTTP isteğini ve yanıtını Işler.</span><span class="sxs-lookup"><span data-stu-id="f11ea-114">Middleware: Processes the HTTP request and response.</span></span>

<span data-ttu-id="f11ea-115">Katana Şu anda iki sunucu sağladığından, her ikisi de Windows tümleşik kimlik doğrulamasını destekler:</span><span class="sxs-lookup"><span data-stu-id="f11ea-115">Katana currently provides two servers, both of which support Windows Integrated Authentication:</span></span>

- <span data-ttu-id="f11ea-116">**Microsoft. Owin. Host. SystemWeb**.</span><span class="sxs-lookup"><span data-stu-id="f11ea-116">**Microsoft.Owin.Host.SystemWeb**.</span></span> <span data-ttu-id="f11ea-117">ASP.NET işlem hattı ile IIS 'yi kullanır.</span><span class="sxs-lookup"><span data-stu-id="f11ea-117">Uses IIS with the ASP.NET pipeline.</span></span>
- <span data-ttu-id="f11ea-118">**Microsoft. Owin. Host. HttpListener**.</span><span class="sxs-lookup"><span data-stu-id="f11ea-118">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="f11ea-119">[System .net. HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)kullanır.</span><span class="sxs-lookup"><span data-stu-id="f11ea-119">Uses [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx).</span></span> <span data-ttu-id="f11ea-120">Bu sunucu şu anda kendi kendine barındırma Katana olduğunda varsayılan seçenektir.</span><span class="sxs-lookup"><span data-stu-id="f11ea-120">This server is currently the default option when self-hosting Katana.</span></span>

> [!NOTE]
> <span data-ttu-id="f11ea-121">Bu işlevsellik sunucuda zaten mevcut olduğundan Katana, şu anda Windows kimlik doğrulaması için OWıN ara yazılımı sağlamıyor.</span><span class="sxs-lookup"><span data-stu-id="f11ea-121">Katana does not currently provide OWIN middleware for Windows Authentication, because this functionality is already available in the servers.</span></span>

## <a name="windows-authentication-in-iis"></a><span data-ttu-id="f11ea-122">IIS 'de Windows kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="f11ea-122">Windows Authentication in IIS</span></span>

<span data-ttu-id="f11ea-123">Microsoft. Owin. Host. SystemWeb kullanarak IIS 'de Windows kimlik doğrulamasını etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f11ea-123">Using Microsoft.Owin.Host.SystemWeb, you can simply enable Windows Authentication in IIS.</span></span>

<span data-ttu-id="f11ea-124">"ASP.NET Empty Web Application" proje şablonunu kullanarak yeni bir ASP.NET uygulaması oluşturarak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="f11ea-124">Let's start by creating a new ASP.NET application, using the "ASP.NET Empty Web Application" project template.</span></span>

![](enabling-windows-authentication-in-katana/_static/image1.png)

<span data-ttu-id="f11ea-125">Sonra NuGet paketlerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f11ea-125">Next, add NuGet packages.</span></span> <span data-ttu-id="f11ea-126">**Araçlar** menüsünde **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="f11ea-126">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="f11ea-127">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="f11ea-127">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample1.cmd)]

<span data-ttu-id="f11ea-128">Şimdi aşağıdaki kodla `Startup` adlı bir sınıf ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f11ea-128">Now add a class named `Startup` with the following code:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample2.cs)]

<span data-ttu-id="f11ea-129">Bu, IIS üzerinde çalışan OWIN için bir "Hello World" uygulaması oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f11ea-129">That's all you need to create a "Hello world" application for OWIN, running on IIS.</span></span> <span data-ttu-id="f11ea-130">Uygulamada hata ayıklamak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="f11ea-130">Press F5 to debug the application.</span></span> <span data-ttu-id="f11ea-131">"Merhaba Dünya!" görmeniz gerekir</span><span class="sxs-lookup"><span data-stu-id="f11ea-131">You should see "Hello World!"</span></span> <span data-ttu-id="f11ea-132">tarayıcı penceresinde.</span><span class="sxs-lookup"><span data-stu-id="f11ea-132">in the browser window.</span></span>

![](enabling-windows-authentication-in-katana/_static/image2.png)

<span data-ttu-id="f11ea-133">Daha sonra, IIS Express Windows kimlik doğrulamasını etkinleştireceğiz.</span><span class="sxs-lookup"><span data-stu-id="f11ea-133">Next, we'll enable Windows Authentication in IIS Express.</span></span> <span data-ttu-id="f11ea-134">**Görünüm** menüsünden **Özellikler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="f11ea-134">From the **View** menu, select **Properties**.</span></span> <span data-ttu-id="f11ea-135">Proje özelliklerini görüntülemek için Çözüm Gezgini içindeki proje adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f11ea-135">Click on the project name in Solution Explorer to view the project properties.</span></span>

<span data-ttu-id="f11ea-136">**Özellikler** penceresinde, **anonim kimlik doğrulamasını** **devre dışı** olarak ayarlayın ve **Windows kimlik doğrulamasını** **etkin**olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f11ea-136">In the **Properties** window, set **Anonymous Authentication** to **Disabled** and set **Windows Authentication** to **Enabled**.</span></span>

![](enabling-windows-authentication-in-katana/_static/image3.png)

<span data-ttu-id="f11ea-137">Uygulamayı Visual Studio 'dan çalıştırdığınızda IIS Express kullanıcının Windows kimlik bilgilerini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f11ea-137">When you run the application from Visual Studio, IIS Express will require the user's Windows credentials.</span></span> <span data-ttu-id="f11ea-138">Bu, [Fiddler](http://fiddler2.com/home) veya başka bir http hata ayıklama aracı kullanarak bunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f11ea-138">You can see this by using [Fiddler](http://fiddler2.com/home) or another HTTP debugging tool.</span></span> <span data-ttu-id="f11ea-139">Örnek bir HTTP yanıtı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f11ea-139">Here is an example HTTP response:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample3.cmd?highlight=1,5-6)]

<span data-ttu-id="f11ea-140">Bu yanıttaki WWW-kimlik doğrulama üst bilgileri, sunucunun Kerberos veya NTLM kullanan [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) protokolünü desteklediğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="f11ea-140">The WWW-Authenticate headers in this response indicate that the server supports the [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) protocol, which uses either Kerberos or NTLM.</span></span>

<span data-ttu-id="f11ea-141">Daha sonra, uygulamayı bir sunucusuna dağıttığınızda, bu sunucudaki IIS 'de Windows kimlik doğrulamasını etkinleştirmek için [Bu adımları](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) izleyin.</span><span class="sxs-lookup"><span data-stu-id="f11ea-141">Later, when you deploy the application to a server, follow [these steps](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) to enable Windows Authentication in IIS on that server.</span></span>

## <a name="windows-authentication-in-httplistener"></a><span data-ttu-id="f11ea-142">HttpListener 'da Windows kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="f11ea-142">Windows Authentication in HttpListener</span></span>

<span data-ttu-id="f11ea-143">Self-Host Katana için Microsoft. Owin. Host. HttpListener kullanıyorsanız, doğrudan **HttpListener** örneğinde Windows kimlik doğrulamasını etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f11ea-143">If you are using Microsoft.Owin.Host.HttpListener to self-host Katana, you can enable Windows Authentication directly on the **HttpListener** instance.</span></span>

<span data-ttu-id="f11ea-144">İlk olarak yeni bir konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f11ea-144">First, create a new console application.</span></span> <span data-ttu-id="f11ea-145">Sonra NuGet paketlerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f11ea-145">Next, add NuGet packages.</span></span> <span data-ttu-id="f11ea-146">**Araçlar** menüsünde **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="f11ea-146">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="f11ea-147">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="f11ea-147">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample4.cmd)]

<span data-ttu-id="f11ea-148">Şimdi aşağıdaki kodla `Startup` adlı bir sınıf ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f11ea-148">Now add a class named `Startup` with the following code:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample5.cs)]

<span data-ttu-id="f11ea-149">Bu sınıf, öncesinde aynı "Hello World" örneğini uygular, ancak Windows kimlik doğrulamasını da kimlik doğrulama düzeni olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="f11ea-149">This class implements the same "Hello world" example from before, but it also sets Windows Authentication as the authentication scheme.</span></span>

<span data-ttu-id="f11ea-150">`Main` işlevinin içinde OWıN ardışık düzenini başlatın:</span><span class="sxs-lookup"><span data-stu-id="f11ea-150">Inside the `Main` function, start the OWIN pipeline:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample6.cs)]

<span data-ttu-id="f11ea-151">Uygulamanın Windows kimlik doğrulamasını kullandığını onaylamak için Fiddler 'da bir istek gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f11ea-151">You can send a request in Fiddler to confirm that the application is using Windows Authentication:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample7.cmd?highlight=1,4-5)]

## <a name="related-topics"></a><span data-ttu-id="f11ea-152">İlgili Konular</span><span class="sxs-lookup"><span data-stu-id="f11ea-152">Related Topics</span></span>

[<span data-ttu-id="f11ea-153">Project Katana’ya Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f11ea-153">An Overview of Project Katana</span></span>](an-overview-of-project-katana.md)

[<span data-ttu-id="f11ea-154">System .net. HttpListener</span><span class="sxs-lookup"><span data-stu-id="f11ea-154">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener.aspx)

[<span data-ttu-id="f11ea-155">MVC 5 ' te OWıN Forms kimlik doğrulamasını anlama</span><span class="sxs-lookup"><span data-stu-id="f11ea-155">Understanding OWIN Forms Authentication in MVC 5</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/07/03/understanding-owin-forms-authentication-in-mvc-5.aspx)
