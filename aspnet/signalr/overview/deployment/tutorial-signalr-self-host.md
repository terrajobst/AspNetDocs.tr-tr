---
uid: signalr/overview/deployment/tutorial-signalr-self-host
title: 'Öğretici: SignalR Self-Host | Microsoft Docs'
author: bradygaster
description: Bu öğreticide, şirket içinde barındırılan bir SignalR 2 sunucusu oluşturma ve bir JavaScript istemcisiyle buna bağlanma işlemlerinin nasıl yapılacağı gösterilmektedir. Eğitim V 'de kullanılan yazılım sürümleri...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 400db427-27af-4f2f-abf0-5486d5e024b5
msc.legacyurl: /signalr/overview/deployment/tutorial-signalr-self-host
msc.type: authoredcontent
ms.openlocfilehash: 41c8c3803923e76ef238a5c5937cbe7f81e6aa82
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74578576"
---
# <a name="tutorial-signalr-self-host"></a><span data-ttu-id="cb81b-104">Öğretici: Şirket İçinde SignalR Barındırma</span><span class="sxs-lookup"><span data-stu-id="cb81b-104">Tutorial: SignalR Self-Host</span></span>

<span data-ttu-id="cb81b-105">, [Patrick Fleti](https://github.com/pfletcher) tarafından</span><span class="sxs-lookup"><span data-stu-id="cb81b-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[<span data-ttu-id="cb81b-106">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="cb81b-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/SignalR-Self-Host-Sample-6da0f383)

> <span data-ttu-id="cb81b-107">Bu öğreticide, şirket içinde barındırılan bir SignalR 2 sunucusu oluşturma ve bir JavaScript istemcisiyle buna bağlanma işlemlerinin nasıl yapılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="cb81b-107">This tutorial shows how to create a self-hosted SignalR 2 server, and how to connect to it with a JavaScript client.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="cb81b-108">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="cb81b-108">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="cb81b-109">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="cb81b-109">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="cb81b-110">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="cb81b-110">.NET 4.5</span></span>
> - <span data-ttu-id="cb81b-111">SignalR sürüm 2</span><span class="sxs-lookup"><span data-stu-id="cb81b-111">SignalR version 2</span></span>
>
>
>
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a><span data-ttu-id="cb81b-112">Visual Studio 2012 'yi bu öğreticiyle kullanma</span><span class="sxs-lookup"><span data-stu-id="cb81b-112">Using Visual Studio 2012 with this tutorial</span></span>
>
>
> <span data-ttu-id="cb81b-113">Visual Studio 2012 'yi bu öğreticiyle kullanmak için şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="cb81b-113">To use Visual Studio 2012 with this tutorial, do the following:</span></span>
>
> - <span data-ttu-id="cb81b-114">[Paket yöneticinize](http://docs.nuget.org/docs/start-here/installing-nuget) en son sürüme güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="cb81b-114">Update your [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) to the latest version.</span></span>
> - <span data-ttu-id="cb81b-115">[Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)'ni yükleme.</span><span class="sxs-lookup"><span data-stu-id="cb81b-115">Install the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> - <span data-ttu-id="cb81b-116">Web platformu yükleyicisinde, **Visual Studio 2012 için ASP.NET and Web Tools 2013,1**' i arayın ve yükleme yapın.</span><span class="sxs-lookup"><span data-stu-id="cb81b-116">In the Web Platform Installer, search for and install **ASP.NET and Web Tools 2013.1 for Visual Studio 2012**.</span></span> <span data-ttu-id="cb81b-117">Bu, **Merkez**gibi SignalR sınıfları Için Visual Studio şablonlarını yükler.</span><span class="sxs-lookup"><span data-stu-id="cb81b-117">This will install Visual Studio templates for SignalR classes such as **Hub**.</span></span>
> - <span data-ttu-id="cb81b-118">Bazı şablonlar ( **Owın başlangıç sınıfı**gibi) kullanılamayacak; Bunlar için bunun yerine bir sınıf dosyası kullanın.</span><span class="sxs-lookup"><span data-stu-id="cb81b-118">Some templates (such as **OWIN Startup Class**) will not be available; for these, use a Class file instead.</span></span>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="cb81b-119">Sorular ve açıklamalar</span><span class="sxs-lookup"><span data-stu-id="cb81b-119">Questions and comments</span></span>
>
> <span data-ttu-id="cb81b-120">Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun.</span><span class="sxs-lookup"><span data-stu-id="cb81b-120">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="cb81b-121">Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb81b-121">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="cb81b-122">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="cb81b-122">Overview</span></span>

<span data-ttu-id="cb81b-123">Bir SignalR sunucusu, genellikle IIS 'deki bir ASP.NET uygulamasında barındırılır, ancak Self-Host kitaplığını kullanarak kendiliğinden barındırılabilen (bir konsol uygulaması veya Windows hizmeti gibi).</span><span class="sxs-lookup"><span data-stu-id="cb81b-123">A SignalR server is usually hosted in an ASP.NET application in IIS, but it can also be self-hosted (such as in a console application or Windows service) using the self-host library.</span></span> <span data-ttu-id="cb81b-124">Bu kitaplık, SignalR 2 ' nin tümü gibi, OWıN üzerinde oluşturulmuştur ([.net Için açık Web arabirimi](http://owin.org)).</span><span class="sxs-lookup"><span data-stu-id="cb81b-124">This library, like all of SignalR 2, is built on OWIN ([Open Web Interface for .NET](http://owin.org)).</span></span> <span data-ttu-id="cb81b-125">OWIN, .NET Web sunucuları ile Web uygulamaları arasında bir soyutlama tanımlar.</span><span class="sxs-lookup"><span data-stu-id="cb81b-125">OWIN defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="cb81b-126">OWIN, Web uygulamasını sunucusundan ayırır, bu da bir Web uygulamasını kendi işleminizde IIS dışında bir Web uygulaması barındırmak için ideal hale getirir.</span><span class="sxs-lookup"><span data-stu-id="cb81b-126">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>

<span data-ttu-id="cb81b-127">IIS 'de barındırılamayan nedenler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="cb81b-127">Reasons for not hosting in IIS include:</span></span>

- <span data-ttu-id="cb81b-128">IIS olmadan var olan bir sunucu grubu gibi IIS 'nin kullanılamadığı veya istenmediğinde ortamlar.</span><span class="sxs-lookup"><span data-stu-id="cb81b-128">Environments where IIS is not available or desirable, such as an existing server farm without IIS.</span></span>
- <span data-ttu-id="cb81b-129">IIS 'nin performans ek yükünün önlenebilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb81b-129">The performance overhead of IIS needs to be avoided.</span></span>
- <span data-ttu-id="cb81b-130">SignalR işlevselliği, bir Windows hizmeti, Azure Worker rolü veya başka bir işlemde çalışan mevcut bir uygulamaya eklenir.</span><span class="sxs-lookup"><span data-stu-id="cb81b-130">SignalR functionality is to be added to an existing application that runs in a Windows Service, Azure worker role, or other process.</span></span>

<span data-ttu-id="cb81b-131">Bir çözüm, performans nedenleriyle kendi kendine ana bilgisayar olarak geliştiriliyorsa, performans avantajını belirleyebilmek için IIS 'de barındırılan uygulamayı da sınamanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="cb81b-131">If a solution is being developed as self-host for performance reasons, it's recommended to also test the application hosted in IIS to determine the performance benefit.</span></span>

<span data-ttu-id="cb81b-132">Bu öğretici aşağıdaki bölümleri içerir:</span><span class="sxs-lookup"><span data-stu-id="cb81b-132">This tutorial contains the following sections:</span></span>

- [<span data-ttu-id="cb81b-133">Sunucu oluşturuluyor</span><span class="sxs-lookup"><span data-stu-id="cb81b-133">Creating the server</span></span>](#server)
- [<span data-ttu-id="cb81b-134">Bir JavaScript istemcisiyle sunucuya erişme</span><span class="sxs-lookup"><span data-stu-id="cb81b-134">Accessing the server with a JavaScript client</span></span>](#js)

<a id="server"></a>

## <a name="creating-the-server"></a><span data-ttu-id="cb81b-135">Sunucu oluşturuluyor</span><span class="sxs-lookup"><span data-stu-id="cb81b-135">Creating the server</span></span>

<span data-ttu-id="cb81b-136">Bu öğreticide, bir konsol uygulamasında barındırılan bir sunucu oluşturacaksınız, ancak sunucu, Windows hizmeti veya Azure çalışan rolü gibi herhangi bir işlem sıralaması içinde barındırılabilir.</span><span class="sxs-lookup"><span data-stu-id="cb81b-136">In this tutorial, you'll create a server that's hosted in a console application, but the server can be hosted in any sort of process, such as a Windows service or Azure worker role.</span></span> <span data-ttu-id="cb81b-137">Bir Windows hizmetinde bir SignalR sunucusunu barındırmak için örnek kod için, bkz. [bir Windows hizmetinde kendi kendine barındırma SignalR](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3).</span><span class="sxs-lookup"><span data-stu-id="cb81b-137">For sample code for hosting a SignalR server in a Windows Service, see [Self-Hosting SignalR in a Windows Service](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3).</span></span>

1. <span data-ttu-id="cb81b-138">Yönetici ayrıcalıklarıyla Visual Studio 2013 açın.</span><span class="sxs-lookup"><span data-stu-id="cb81b-138">Open Visual Studio 2013 with administrator privileges.</span></span> <span data-ttu-id="cb81b-139">**Dosya**, **Yeni proje**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="cb81b-139">Select **File**, **New Project**.</span></span> <span data-ttu-id="cb81b-140">**Şablonlar** bölmesindeki **görsel C#**  düğümü altında **Windows** ' u seçin ve **konsol uygulaması** şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="cb81b-140">Select **Windows** under the **Visual C#** node in the **Templates** pane, and select the **Console Application** template.</span></span> <span data-ttu-id="cb81b-141">"SignalRSelfHost" adlı yeni projeyi adlandırın ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cb81b-141">Name the new project "SignalRSelfHost" and click **OK**.</span></span>

    ![](tutorial-signalr-self-host/_static/image1.png)
2. <span data-ttu-id="cb81b-142">**Araçlar** > **nuget** Paket Yöneticisi > **Paket Yöneticisi konsolu**' nu seçerek NuGet Paket Yöneticisi konsolunu açın.</span><span class="sxs-lookup"><span data-stu-id="cb81b-142">Open the NuGet package manager console by selecting **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="cb81b-143">Paket Yöneticisi konsolunda aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="cb81b-143">In the package manager console, enter the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample1.ps1)]

    <span data-ttu-id="cb81b-144">Bu komut, SignalR 2 Self-Host kitaplıklarını projeye ekler.</span><span class="sxs-lookup"><span data-stu-id="cb81b-144">This command adds the SignalR 2 Self-Host libraries to the project.</span></span>
4. <span data-ttu-id="cb81b-145">Paket Yöneticisi konsolunda aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="cb81b-145">In the package manager console, enter the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample2.ps1)]

    <span data-ttu-id="cb81b-146">Bu komut, Microsoft. Owin. CORS kitaplığını projeye ekler.</span><span class="sxs-lookup"><span data-stu-id="cb81b-146">This command adds the Microsoft.Owin.Cors library to the project.</span></span> <span data-ttu-id="cb81b-147">Bu kitaplık, SignalR barındıran uygulamalar ve farklı etki alanlarında bir Web sayfası istemcisi için gerekli olan etki alanları arası destek için kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="cb81b-147">This library will be used for cross-domain support, which is required for applications that host SignalR and a web page client in different domains.</span></span> <span data-ttu-id="cb81b-148">SignalR sunucusunu ve Web istemcisini farklı bağlantı noktalarında barındırabileceksiniz, bu, bu bileşenler arasındaki iletişim için etki alanları arası iletişim için etkinleştirilmesi gerektiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="cb81b-148">Since you'll be hosting the SignalR server and the web client on different ports, this means that cross-domain must be enabled for communication between these components.</span></span>
5. <span data-ttu-id="cb81b-149">Program.cs içeriğini aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="cb81b-149">Replace the contents of Program.cs with the following code.</span></span>

    [!code-csharp[Main](tutorial-signalr-self-host/samples/sample3.cs)]

    <span data-ttu-id="cb81b-150">Yukarıdaki kod üç sınıf içerir:</span><span class="sxs-lookup"><span data-stu-id="cb81b-150">The above code includes three classes:</span></span>

    - <span data-ttu-id="cb81b-151">**Program**, yürütmenin birincil yolunu tanımlayan **Main** yöntemi de dahil.</span><span class="sxs-lookup"><span data-stu-id="cb81b-151">**Program**, including the **Main** method defining the primary path of execution.</span></span> <span data-ttu-id="cb81b-152">Bu yöntemde, **Başlangıç** türü bir Web UYGULAMASı belirtilen URL 'de başlatılır (`http://localhost:8080`).</span><span class="sxs-lookup"><span data-stu-id="cb81b-152">In this method, a web application of type **Startup** is started at the specified URL (`http://localhost:8080`).</span></span> <span data-ttu-id="cb81b-153">Uç noktada güvenlik gerekliyse, SSL uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="cb81b-153">If security is required on the endpoint, SSL can be implemented.</span></span> <span data-ttu-id="cb81b-154">Daha fazla bilgi için bkz. [nasıl yapılır: SSL sertifikası Ile bağlantı noktası yapılandırma](https://msdn.microsoft.com/library/ms733791.aspx) .</span><span class="sxs-lookup"><span data-stu-id="cb81b-154">See [How to: Configure a Port with an SSL Certificate](https://msdn.microsoft.com/library/ms733791.aspx) for more information.</span></span>
    - <span data-ttu-id="cb81b-155">**Başlangıç**, SignalR Server için yapılandırmayı içeren sınıf (Bu öğreticinin kullandığı tek yapılandırma `UseCors`) ve `MapSignalR`çağrısı, projedeki tüm Hub nesneleri için yollar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cb81b-155">**Startup**, the class containing the configuration for the SignalR server (the only configuration this tutorial uses is the call to `UseCors`), and the call to `MapSignalR`, which creates routes for any Hub objects in the project.</span></span>
    - <span data-ttu-id="cb81b-156">Uygulamanın istemcilere sağlayacağız SignalR hub sınıfı olan **Myhub**.</span><span class="sxs-lookup"><span data-stu-id="cb81b-156">**MyHub**, the SignalR Hub class that the application will provide to clients.</span></span> <span data-ttu-id="cb81b-157">Bu sınıf tek bir yönteme **sahiptir ve istemcileri, diğer**tüm bağlı istemcilere bir ileti yayınlamak için çağıracaktır.</span><span class="sxs-lookup"><span data-stu-id="cb81b-157">This class has a single method, **Send**, that clients will call to broadcast a message to all other connected clients.</span></span>
6. <span data-ttu-id="cb81b-158">Uygulamayı derleyin ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cb81b-158">Compile and run the application.</span></span> <span data-ttu-id="cb81b-159">Sunucunun çalıştırıldığı adresin bir konsol penceresinde gösterilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb81b-159">The address that the server is running should show in a console window.</span></span>

    ![](tutorial-signalr-self-host/_static/image2.png)
7. <span data-ttu-id="cb81b-160">Yürütme `System.Reflection.TargetInvocationException was unhandled`özel durumla başarısız olursa, Visual Studio 'Yu yönetici ayrıcalıklarıyla yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb81b-160">If execution fails with the exception `System.Reflection.TargetInvocationException was unhandled`, you will need to restart Visual Studio with administrator privileges.</span></span>
8. <span data-ttu-id="cb81b-161">Sonraki bölüme geçmeden önce uygulamayı durdurun.</span><span class="sxs-lookup"><span data-stu-id="cb81b-161">Stop the application before proceeding to the next section.</span></span>

<a id="js"></a>

## <a name="accessing-the-server-with-a-javascript-client"></a><span data-ttu-id="cb81b-162">Bir JavaScript istemcisiyle sunucuya erişme</span><span class="sxs-lookup"><span data-stu-id="cb81b-162">Accessing the server with a JavaScript client</span></span>

<span data-ttu-id="cb81b-163">Bu bölümde, Başlangıç [öğreticisinde](../getting-started/tutorial-getting-started-with-signalr.md)aynı JavaScript istemcisini kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="cb81b-163">In this section, you'll use the same JavaScript client from the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="cb81b-164">İstemcide yalnızca bir değişiklik yapacağız. Bu, hub URL 'sini açıkça tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cb81b-164">We'll only make one modification to the client, which is to explicitly define the hub URL.</span></span> <span data-ttu-id="cb81b-165">Şirket içinde barındırılan bir uygulamayla, sunucu bağlantı URL 'siyle aynı adreste olmayabilir (ters proxy 'ler ve yük dengeleyiciler nedeniyle), URL 'nin açıkça tanımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb81b-165">With a self-hosted application, the server may not necessarily be at the same address as the connection URL (due to reverse proxies and load balancers), so the URL needs to be defined explicitly.</span></span>

1. <span data-ttu-id="cb81b-166">**Çözüm Gezgini**, çözüme sağ tıklayın ve **Ekle**, **Yeni proje**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="cb81b-166">In **Solution Explorer**, right-click on the solution and select **Add**, **New Project**.</span></span> <span data-ttu-id="cb81b-167">**Web** düğümünü seçin ve **ASP.NET Web uygulaması** şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="cb81b-167">Select the **Web** node, and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="cb81b-168">Projeyi "JavascriptClient" olarak adlandırın ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cb81b-168">Name the project "JavascriptClient" and click **OK**.</span></span>

    ![](tutorial-signalr-self-host/_static/image3.png)
2. <span data-ttu-id="cb81b-169">**Boş** şablonu seçin ve kalan seçenekleri seçilmemiş olarak bırakın.</span><span class="sxs-lookup"><span data-stu-id="cb81b-169">Select the **Empty** template, and leave the remaining options unselected.</span></span> <span data-ttu-id="cb81b-170">**Proje oluştur**' u seçin.</span><span class="sxs-lookup"><span data-stu-id="cb81b-170">Select **Create Project**.</span></span>

    ![](tutorial-signalr-self-host/_static/image4.png)
3. <span data-ttu-id="cb81b-171">Paket Yöneticisi konsolunda, **varsayılan proje** açılır penceresinde "JavascriptClient" projesini seçin ve aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="cb81b-171">In the package manager console, select the "JavascriptClient" project in the **Default project** drop-down, and execute the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample4.ps1)]

    <span data-ttu-id="cb81b-172">Bu komut, istemcisinde ihtiyacınız olan SignalR ve JQuery kitaplıklarını yükleme.</span><span class="sxs-lookup"><span data-stu-id="cb81b-172">This command installs the SignalR and JQuery libraries that you'll need in the client.</span></span>
4. <span data-ttu-id="cb81b-173">Projenize sağ tıklayın ve **Ekle**, **Yeni öğe**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="cb81b-173">Right-click on your project and select **Add**, **New Item**.</span></span> <span data-ttu-id="cb81b-174">**Web** düğümünü SEÇIN ve HTML sayfası ' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="cb81b-174">Select the **Web** node, and select HTML Page.</span></span> <span data-ttu-id="cb81b-175">Sayfayı **default. html**olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="cb81b-175">Name the page **Default.html**.</span></span>

    ![](tutorial-signalr-self-host/_static/image5.png)
5. <span data-ttu-id="cb81b-176">Yeni HTML sayfasının içeriğini aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="cb81b-176">Replace the contents of the new HTML page with the following code.</span></span> <span data-ttu-id="cb81b-177">Buradaki betik başvurularının, projenin betikler klasöründeki betiklerin eşleştiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="cb81b-177">Verify that the script references here match the scripts in the Scripts folder of the project.</span></span>

    [!code-html[Main](tutorial-signalr-self-host/samples/sample5.html?highlight=31-32)]

    <span data-ttu-id="cb81b-178">Aşağıdaki kod (Yukarıdaki kod örneğinde vurgulanan), başlangıç öğreticisinde (kodu SignalR sürüm 2 Beta 'ya yükseltmenin yanı sıra) kullanılan istemciye yaptığınız bir ektir.</span><span class="sxs-lookup"><span data-stu-id="cb81b-178">The following code (highlighted in the code sample above) is the addition that you've made to the client used in the Getting Stared tutorial (in addition to upgrading the code to SignalR version 2 beta).</span></span> <span data-ttu-id="cb81b-179">Bu kod satırı, sunucuda SignalR için temel bağlantı URL 'sini açık olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="cb81b-179">This line of code explicitly sets the base connection URL for SignalR on the server.</span></span>

    [!code-javascript[Main](tutorial-signalr-self-host/samples/sample6.js)]
6. <span data-ttu-id="cb81b-180">Çözüme sağ tıklayın ve **Başlangıç projelerini ayarla...** seçeneğini belirleyin. **Birden çok başlangıç projesi** radyo düğmesini seçin ve her Iki projenin **eylemini** **Başlat**olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="cb81b-180">Right-click on the solution, and select **Set Startup Projects...**. Select the **Multiple startup projects** radio button, and set both projects' **Action** to **Start**.</span></span>

    ![](tutorial-signalr-self-host/_static/image6.png)
7. <span data-ttu-id="cb81b-181">"Default. html" öğesine sağ tıklayın ve **Başlangıç sayfası olarak ayarla**' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="cb81b-181">Right-click on "Default.html" and select **Set As Start Page**.</span></span>
8. <span data-ttu-id="cb81b-182">Uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cb81b-182">Run the application.</span></span> <span data-ttu-id="cb81b-183">Sunucu ve sayfa başlatılır.</span><span class="sxs-lookup"><span data-stu-id="cb81b-183">The server and page will launch.</span></span> <span data-ttu-id="cb81b-184">Sayfa sunucu başlatılmadan önce yüklenirse Web sayfasını yeniden yüklemeniz gerekebilir (veya hata ayıklayıcıda **devam et** ' i seçin).</span><span class="sxs-lookup"><span data-stu-id="cb81b-184">You may need to reload the web page (or select **Continue** in the debugger) if the page loads before the server is started.</span></span>
9. <span data-ttu-id="cb81b-185">Tarayıcıda, sorulduğunda bir Kullanıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="cb81b-185">In the browser, provide a username when prompted.</span></span> <span data-ttu-id="cb81b-186">Sayfanın URL 'sini başka bir tarayıcı sekmesine veya pencereye kopyalayın ve farklı bir Kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="cb81b-186">Copy the page's URL into another browser tab or window and provide a different username.</span></span> <span data-ttu-id="cb81b-187">Başlangıç öğreticisinde olduğu gibi, bir tarayıcı bölmesinden diğerine ileti gönderebileceksiniz.</span><span class="sxs-lookup"><span data-stu-id="cb81b-187">You will be able to send messages from one browser pane to the other, as in the Getting Started tutorial.</span></span>
