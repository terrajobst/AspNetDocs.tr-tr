---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
title: 'Öğretici: SignalR 1. x ve MVC 4 ile çalışmaya başlama | Microsoft Docs'
author: bradygaster
description: Gerçek zamanlı bir sohbet uygulaması derlemek için ASP.NET SignalR ve ASP.NET MVC 4 kullanın.
ms.author: bradyg
ms.date: 03/29/2013
ms.assetid: eeef9f73-6de3-49f9-b50b-9af22108f2ce
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 9186915df6d5de6bc20dfc0adabc54056d2f3a8c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579571"
---
# <a name="tutorial-getting-started-with-signalr-1x-and-mvc-4"></a><span data-ttu-id="731dd-103">Öğretici: SignalR 1.x ve MVC 4 ile Çalışmaya Başlama</span><span class="sxs-lookup"><span data-stu-id="731dd-103">Tutorial: Getting Started with SignalR 1.x and MVC 4</span></span>

<span data-ttu-id="731dd-104">, [Patrick Fleti](https://github.com/pfletcher), [Tim teebken](https://github.com/timlt)</span><span class="sxs-lookup"><span data-stu-id="731dd-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="731dd-105">Bu öğreticide, gerçek zamanlı bir sohbet uygulaması oluşturmak için ASP.NET SignalR 'nin nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="731dd-105">This tutorial shows how to use ASP.NET SignalR to create a real-time chat application.</span></span> <span data-ttu-id="731dd-106">Bir MVC 4 uygulamasına SignalR ekleyeceksiniz ve ileti göndermek ve görüntülemek için bir sohbet görünümü oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="731dd-106">You will add SignalR to an MVC 4 application and create a chat view to send and display messages.</span></span>

## <a name="overview"></a><span data-ttu-id="731dd-107">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="731dd-107">Overview</span></span>

<span data-ttu-id="731dd-108">Bu öğretici, ASP.NET SignalR ve ASP.NET MVC 4 ile gerçek zamanlı web uygulaması geliştirmeyi sağlar.</span><span class="sxs-lookup"><span data-stu-id="731dd-108">This tutorial introduces you to real-time web application development with ASP.NET SignalR and ASP.NET MVC 4.</span></span> <span data-ttu-id="731dd-109">Öğretici, [SignalR kullanmaya başlama öğreticisi](tutorial-getting-started-with-signalr.md)ile aynı sohbet uygulama kodunu kullanır, ancak bunu Internet şablonuna DAYALı bir MVC 4 uygulamasına eklemeyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="731dd-109">The tutorial uses the same chat application code as the [SignalR Getting Started tutorial](tutorial-getting-started-with-signalr.md), but shows how to add it to an MVC 4 application based on the Internet template.</span></span>

<span data-ttu-id="731dd-110">Bu konu başlığında aşağıdaki SignalR geliştirme görevlerini öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="731dd-110">In this topic you will learn the following SignalR development tasks:</span></span>

- <span data-ttu-id="731dd-111">SignalR kitaplığı bir MVC 4 uygulamasına ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="731dd-111">Adding the SignalR library to an MVC 4 application.</span></span>
- <span data-ttu-id="731dd-112">İstemcilere içerik göndermek için bir hub sınıfı oluşturma.</span><span class="sxs-lookup"><span data-stu-id="731dd-112">Creating a hub class to push content to clients.</span></span>
- <span data-ttu-id="731dd-113">Bir Web sayfasında, iletileri göndermek ve merkezi 'nden güncelleştirme göstermek için SignalR jQuery kitaplığını kullanma.</span><span class="sxs-lookup"><span data-stu-id="731dd-113">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="731dd-114">Aşağıdaki ekran görüntüsünde, bir tarayıcıda çalışan tamamlanmış sohbet uygulaması gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="731dd-114">The following screen shot shows the completed chat application running in a browser.</span></span>

![Sohbet örnekleri](tutorial-getting-started-with-signalr-and-mvc-4/_static/image2.png)

<span data-ttu-id="731dd-116">Başlıklı</span><span class="sxs-lookup"><span data-stu-id="731dd-116">Sections:</span></span>

- [<span data-ttu-id="731dd-117">Projeyi ayarlama</span><span class="sxs-lookup"><span data-stu-id="731dd-117">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="731dd-118">Örneği çalıştırın</span><span class="sxs-lookup"><span data-stu-id="731dd-118">Run the Sample</span></span>](#run)
- [<span data-ttu-id="731dd-119">Kodu inceleyin</span><span class="sxs-lookup"><span data-stu-id="731dd-119">Examine the Code</span></span>](#code)
- [<span data-ttu-id="731dd-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="731dd-120">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="731dd-121">Projeyi ayarlama</span><span class="sxs-lookup"><span data-stu-id="731dd-121">Set up the Project</span></span>

<span data-ttu-id="731dd-122">Ön koşullar:</span><span class="sxs-lookup"><span data-stu-id="731dd-122">Prerequisites:</span></span>

- <span data-ttu-id="731dd-123">Visual Studio 2010 SP1, Visual Studio 2012 veya Visual Studio 2012 Express.</span><span class="sxs-lookup"><span data-stu-id="731dd-123">Visual Studio 2010 SP1, Visual Studio 2012, or Visual Studio 2012 Express.</span></span> <span data-ttu-id="731dd-124">Visual Studio yoksa, ücretsiz Visual Studio 2012 Express geliştirme aracını almak için [ASP.net İndirmeleri](https://www.asp.net/downloads) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="731dd-124">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2012 Express Development Tool.</span></span>
- <span data-ttu-id="731dd-125">Visual Studio 2010 için [ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683)' ü yüklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="731dd-125">For Visual Studio 2010, install [ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683).</span></span>

<span data-ttu-id="731dd-126">Bu bölümde, ASP.NET MVC 4 uygulamasının nasıl oluşturulacağı, SignalR kitaplığının nasıl ekleneceği ve sohbet uygulamasının nasıl oluşturulacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="731dd-126">This section shows how to create an ASP.NET MVC 4 application, add the SignalR library, and create the chat application.</span></span>

1. 1. <span data-ttu-id="731dd-127">Visual Studio 'da bir ASP.NET MVC 4 uygulaması oluşturun, SignalRChat olarak adlandırın ve Tamam ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="731dd-127">In Visual Studio create an ASP.NET MVC 4 application, name it SignalRChat, and click OK.</span></span>

        > [!NOTE]
        > <span data-ttu-id="731dd-128">VS 2010 ' de çerçeve sürümü açılan denetiminde **.NET Framework 4** ' ü seçin.</span><span class="sxs-lookup"><span data-stu-id="731dd-128">In VS 2010, select **.NET Framework 4** in the Framework version dropdown control.</span></span> <span data-ttu-id="731dd-129">SignalR kodu 4 ve 4,5 .NET Framework sürümler üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="731dd-129">SignalR code runs on .NET Framework versions 4 and 4.5.</span></span>

        ![MVC web oluştur](tutorial-getting-started-with-signalr-and-mvc-4/_static/image3.png)
      2. <span data-ttu-id="731dd-131">Internet uygulaması şablonunu seçin, **birim testi projesi oluşturma**seçeneğini temizleyin ve Tamam ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="731dd-131">Select the Internet Application template, clear the option to **Create a unit test project**, and click OK.</span></span>

         ![MVC internet sitesi oluştur](tutorial-getting-started-with-signalr-and-mvc-4/_static/image4.png)
      3. <span data-ttu-id="731dd-133">**Araçlar > NuGet paket yöneticisi > Paket Yöneticisi konsolu** ' nu açın ve aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="731dd-133">Open the **Tools > NuGet Package Manager > Package Manager Console** and run the following command.</span></span> <span data-ttu-id="731dd-134">Bu adım, bir dizi betik dosyası ve SignalR işlevselliğini etkinleştiren derleme başvuruları projesine ekler.</span><span class="sxs-lookup"><span data-stu-id="731dd-134">This step adds to the project a set of script files and assembly references that enable SignalR functionality.</span></span>

         `install-package Microsoft.AspNet.SignalR -Version 1.1.3`
      4. <span data-ttu-id="731dd-135">**Çözüm Gezgini** betikler klasörünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="731dd-135">In **Solution Explorer** expand the Scripts folder.</span></span> <span data-ttu-id="731dd-136">SignalR için betik kitaplıklarının projeye eklendiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="731dd-136">Note that script libraries for SignalR have been added to the project.</span></span>

         ![Kitaplık başvuruları](tutorial-getting-started-with-signalr-and-mvc-4/_static/image6.png)
      5. <span data-ttu-id="731dd-138">**Çözüm Gezgini**, projeye sağ tıklayın, Ekle ' yi seçin **| Yeni klasör**ve **hub**adlı yeni bir klasör ekleyin.</span><span class="sxs-lookup"><span data-stu-id="731dd-138">In **Solution Explorer**, right-click the project, select **Add | New Folder**, and add a new folder named **Hubs**.</span></span>
      6. <span data-ttu-id="731dd-139">**Hub** klasörüne sağ tıklayın, Ekle ' ye tıklayın.  **Sınıfını**ve C# **ChatHub.cs**adlı yeni bir sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="731dd-139">Right-click the **Hubs** folder, click **Add | Class**, and create a new C# class named **ChatHub.cs**.</span></span> <span data-ttu-id="731dd-140">Bu sınıfı, tüm istemcilere ileti gönderen bir SignalR sunucu hub 'ı olarak kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="731dd-140">You will use this class as a SignalR server hub that sends messages to all clients.</span></span>

> [!NOTE]
> <span data-ttu-id="731dd-141">Visual Studio 2012 kullanıyorsanız ve [ASP.NET and Web Tools 2012,2 güncelleştirmesini](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation)yüklediyseniz, hub sınıfını oluşturmak Için yeni SignalR öğe şablonunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="731dd-141">If you use Visual Studio 2012 and have installed the [ASP.NET and Web Tools 2012.2 update](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation), you can use the new SignalR item template to create the hub class.</span></span> <span data-ttu-id="731dd-142">Bunu yapmak için, **hub** klasörüne sağ tıklayın, Ekle ' ye tıklayın.  **Yeni öğe**, **SignalR hub sınıfı (v1)** öğesini seçin ve sınıfı **ChatHub.cs**olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="731dd-142">To do that, right-click the **Hubs** folder, click **Add | New Item**, select **SignalR Hub Class (v1)**, and name the class **ChatHub.cs**.</span></span>

1. <span data-ttu-id="731dd-143">**ChatHub** sınıfındaki kodu aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="731dd-143">Replace the code in the **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample1.cs)]
2. <span data-ttu-id="731dd-144">Projenin **Global. asax** dosyasını açın ve `Application_Start` yönteminde kodun ilk satırı olarak `RouteTable.Routes.MapHubs();` yöntemine bir çağrı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="731dd-144">Open the **Global.asax** file for the project, and add a call to the method `RouteTable.Routes.MapHubs();` as the first line of code in the `Application_Start` method.</span></span> <span data-ttu-id="731dd-145">Bu kod, SignalR hub 'ları için varsayılan yolu kaydeder ve başka yollar kaydedilmeden önce çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="731dd-145">This code registers the default route for SignalR hubs and must be called before you register any other routes.</span></span> <span data-ttu-id="731dd-146">Tamamlanan `Application_Start` yöntemi aşağıdaki örneğe benzer şekilde görünür.</span><span class="sxs-lookup"><span data-stu-id="731dd-146">The completed `Application_Start` method looks like the following example.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample2.cs)]
3. <span data-ttu-id="731dd-147">**Controllers/HomeController. cs** dosyasında bulunan `HomeController` sınıfını düzenleyin ve aşağıdaki yöntemi sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="731dd-147">Edit the `HomeController` class found in **Controllers/HomeController.cs** and add the following method to the class.</span></span> <span data-ttu-id="731dd-148">Bu yöntem, daha sonraki bir adımda oluşturacağınız **sohbet** görünümünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="731dd-148">This method returns the **Chat** view that you will create in a later step.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample3.cs)]
4. <span data-ttu-id="731dd-149">Yeni oluşturduğunuz `Chat` yönteminin içine sağ tıklayın ve yeni bir görünüm dosyası oluşturmak için **Görünüm Ekle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="731dd-149">Right-click within the `Chat` method you just created, and click **Add View** to create a new view file.</span></span>
5. <span data-ttu-id="731dd-150">**Görünüm Ekle** iletişim kutusunda, **Düzen veya ana sayfa** (diğer onay kutularını temizleyin) kullanmak için onay kutusunun seçili olduğundan emin olun ve ardından **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="731dd-150">In the **Add View** dialog, make sure the check box is selected to **Use a layout or master page** (clear the other check boxes), and then click **Add**.</span></span>

    ![Görünüm ekleme](tutorial-getting-started-with-signalr-and-mvc-4/_static/image8.png)
6. <span data-ttu-id="731dd-152">**Chat. cshtml**adlı yeni görünüm dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="731dd-152">Edit the new view file named **Chat.cshtml**.</span></span> <span data-ttu-id="731dd-153">&lt;H2&gt; etiketinden sonra, aşağıdaki &lt;div&gt; bölümünü ve `@section scripts` kod bloğunu sayfaya yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="731dd-153">After the &lt;h2&gt; tag, paste the following &lt;div&gt; section and `@section scripts` code block into the page.</span></span> <span data-ttu-id="731dd-154">Bu betik, sayfanın sohbet iletileri göndermesini ve sunucudan ileti görüntülemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="731dd-154">This script enables the page to send chat messages and display messages from the server.</span></span> <span data-ttu-id="731dd-155">Sohbet görünümü için kodun tamamı aşağıdaki kod bloğunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="731dd-155">The complete code for the chat view appears in the following code block.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="731dd-156">Visual Studio projenize SignalR ve diğer betik kitaplıklarını eklediğinizde, Paket Yöneticisi bu konuda gösterilen sürümlerden daha yeni olan betiklerin sürümlerini yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="731dd-156">When you add SignalR and other script libraries to your Visual Studio project, the Package Manager might install versions of the scripts that are more recent than the versions shown in this topic.</span></span> <span data-ttu-id="731dd-157">Kodunuzda betik başvurularının projenizde yüklü olan betik kitaplıklarının sürümleriyle eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="731dd-157">Make sure that the script references in your code match the versions of the script libraries installed in your project.</span></span>

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample4.cshtml)]
7. <span data-ttu-id="731dd-158">Projenin **Tümünü kaydedin** .</span><span class="sxs-lookup"><span data-stu-id="731dd-158">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="731dd-159">Örneği çalıştırın</span><span class="sxs-lookup"><span data-stu-id="731dd-159">Run the Sample</span></span>

1. <span data-ttu-id="731dd-160">Projeyi hata ayıklama modunda çalıştırmak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="731dd-160">Press F5 to run the project in debug mode.</span></span>
2. <span data-ttu-id="731dd-161">Tarayıcı adres satırında, **/Home/chat** ' i proje için varsayılan sayfanın URL 'sine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="731dd-161">In the browser address line, append **/home/chat** to the URL of the default page for the project.</span></span> <span data-ttu-id="731dd-162">Sohbet sayfası bir tarayıcı örneğinde yüklenir ve Kullanıcı adı ister.</span><span class="sxs-lookup"><span data-stu-id="731dd-162">The Chat page loads in a browser instance and prompts for a user name.</span></span>

    ![Kullanıcı adını girin](tutorial-getting-started-with-signalr-and-mvc-4/_static/image9.png)
3. <span data-ttu-id="731dd-164">Bir kullanıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="731dd-164">Enter a user name.</span></span>
4. <span data-ttu-id="731dd-165">Tarayıcının adres satırındaki URL 'YI kopyalayın ve bu iki tarayıcı örneği açmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="731dd-165">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="731dd-166">Her tarayıcı örneğinde benzersiz bir Kullanıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="731dd-166">In each browser instance, enter a unique user name.</span></span>
5. <span data-ttu-id="731dd-167">Her tarayıcı örneğinde bir açıklama ekleyin ve **Gönder**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="731dd-167">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="731dd-168">Yorumlar Tüm tarayıcı örneklerinde görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="731dd-168">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="731dd-169">Bu basit sohbet uygulaması, sunucuda tartışma bağlamını korumaz.</span><span class="sxs-lookup"><span data-stu-id="731dd-169">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="731dd-170">Merkez tüm geçerli kullanıcılara yorum yayınlar.</span><span class="sxs-lookup"><span data-stu-id="731dd-170">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="731dd-171">Daha sonra sohbete katılması olan kullanıcılar, bu kişilerin eklendiği zamandan eklenen iletileri görür.</span><span class="sxs-lookup"><span data-stu-id="731dd-171">Users who join the chat later will see messages added from the time they join.</span></span>
6. <span data-ttu-id="731dd-172">Aşağıdaki ekran görüntüsünde, bir tarayıcıda çalışan sohbet uygulaması gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="731dd-172">The following screen shot shows the chat application running in a browser.</span></span>

    ![Sohbet tarayıcıları](tutorial-getting-started-with-signalr-and-mvc-4/_static/image11.png)
7. <span data-ttu-id="731dd-174">**Çözüm Gezgini**, çalışan uygulamanın **komut dosyası belgeleri** düğümünü inceleyin.</span><span class="sxs-lookup"><span data-stu-id="731dd-174">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="731dd-175">Tarayıcınız olarak Internet Explorer kullanıyorsanız, bu düğüm hata ayıklama modunda görünür.</span><span class="sxs-lookup"><span data-stu-id="731dd-175">This node is visible in debug mode if you are using Internet Explorer as your browser.</span></span> <span data-ttu-id="731dd-176">SignalR kitaplığının çalışma zamanında dinamik olarak oluşturduğu **Hublar** adlı bir betik dosyası vardır.</span><span class="sxs-lookup"><span data-stu-id="731dd-176">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="731dd-177">Bu dosya jQuery betiği ile sunucu tarafı kodu arasındaki iletişimi yönetir.</span><span class="sxs-lookup"><span data-stu-id="731dd-177">This file manages the communication between jQuery script and server-side code.</span></span> <span data-ttu-id="731dd-178">Internet Explorer dışında bir tarayıcı kullanıyorsanız, dinamik **hub** dosyasına doğrudan göz atarak da erişebilirsiniz. örneğin, http://mywebsite/signalr/hubs.</span><span class="sxs-lookup"><span data-stu-id="731dd-178">If you use a browser other than Internet Explorer, you can also access the dynamic **hubs** file by browsing to it directly, for example http://mywebsite/signalr/hubs.</span></span>

    ![Oluşturulan Merkez betiği](tutorial-getting-started-with-signalr-and-mvc-4/_static/image13.png)

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="731dd-180">Kodu inceleyin</span><span class="sxs-lookup"><span data-stu-id="731dd-180">Examine the Code</span></span>

<span data-ttu-id="731dd-181">SignalR sohbet uygulaması iki temel SignalR geliştirme görevini gösterir: sunucuda ana düzenleme nesnesi olarak bir hub oluşturma ve ileti göndermek ve almak için SignalR jQuery kitaplığı kullanma.</span><span class="sxs-lookup"><span data-stu-id="731dd-181">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="731dd-182">SignalR hub 'Ları</span><span class="sxs-lookup"><span data-stu-id="731dd-182">SignalR Hubs</span></span>

<span data-ttu-id="731dd-183">Kod örneğinde, **ChatHub** sınıfı **Microsoft. Aspnet. SignalR. hub** sınıfından türetilir.</span><span class="sxs-lookup"><span data-stu-id="731dd-183">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="731dd-184">**Hub** sınıfından türetmek, bir SignalR uygulaması oluşturmanın kullanışlı bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="731dd-184">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="731dd-185">Hub sınıfınız üzerinde ortak Yöntemler oluşturabilir ve ardından bunları bir Web sayfasındaki jQuery komut dosyalarından çağırarak bu yöntemlere erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="731dd-185">You can create public methods on your hub class and then access those methods by calling them from jQuery scripts in a web page.</span></span>

<span data-ttu-id="731dd-186">Sohbet kodunda, istemciler yeni bir ileti göndermek için **ChatHub. Send** yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="731dd-186">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="731dd-187">İçindeki hub, iletileri **istemcileri. ALL. addNewMessageToPage**çağırarak tüm istemcilere gönderir.</span><span class="sxs-lookup"><span data-stu-id="731dd-187">The hub in turn sends the message to all clients by calling **Clients.All.addNewMessageToPage**.</span></span>

<span data-ttu-id="731dd-188">**Send** yöntemi çeşitli Merkez kavramlarını gösterir:</span><span class="sxs-lookup"><span data-stu-id="731dd-188">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="731dd-189">İstemcilerin bunları çağırabilmesi için ortak yöntemleri bir hub üzerinde bildirin.</span><span class="sxs-lookup"><span data-stu-id="731dd-189">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="731dd-190">Bu hub 'a bağlı tüm istemcilere erişmek için **Microsoft. Aspnet. SignalR. hub. clients** özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="731dd-190">Use the **Microsoft.AspNet.SignalR.Hub.Clients** property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="731dd-191">İstemcileri güncelleştirmek için istemcide jQuery işlevini (`addNewMessageToPage` işlevi gibi) çağırın.</span><span class="sxs-lookup"><span data-stu-id="731dd-191">Call a jQuery function on the client (such as the `addNewMessageToPage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="731dd-192">SignalR ve jQuery</span><span class="sxs-lookup"><span data-stu-id="731dd-192">SignalR and jQuery</span></span>

<span data-ttu-id="731dd-193">Kod örneğindeki **chat. cshtml** görünüm dosyası bir SignalR hub 'ı ile iletişim kurmak Için SignalR jQuery kitaplığını nasıl kullanacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="731dd-193">The **Chat.cshtml** view file in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="731dd-194">Koddaki temel görevler, Hub için otomatik olarak oluşturulan ara sunucuya bir başvuru oluşturuyor ve sunucunun istemcilere içerik göndermek için çağırabilir bir işlev bildirmek ve hub 'a ileti göndermek için bir bağlantı başlatmak.</span><span class="sxs-lookup"><span data-stu-id="731dd-194">The essential tasks in the code are creating a reference to the auto-generated proxy for the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="731dd-195">Aşağıdaki kod bir hub için proxy bildirir.</span><span class="sxs-lookup"><span data-stu-id="731dd-195">The following code declares a proxy for a hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="731dd-196">JQuery içinde, sunucu sınıfına ve üyelerine yönelik başvuru ortası durumunda.</span><span class="sxs-lookup"><span data-stu-id="731dd-196">In jQuery the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="731dd-197">Kod örneği, jQuery içindeki C# **ChatHub** sınıfına **ChatHub**olarak başvurur.</span><span class="sxs-lookup"><span data-stu-id="731dd-197">The code sample references the C# **ChatHub** class in jQuery as **chatHub**.</span></span> <span data-ttu-id="731dd-198">JQuery 'teki `ChatHub` sınıfına, içinde C#olduğu gibi geleneksel Pascal büyük küçük harf başvurmak istiyorsanız, ChatHub.cs sınıf dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="731dd-198">If you want to reference the `ChatHub` class in jQuery with conventional Pascal casing as you would in C#, edit the ChatHub.cs class file.</span></span> <span data-ttu-id="731dd-199">`Microsoft.AspNet.SignalR.Hubs` ad alanına başvurmak için `using` bir ifade ekleyin.</span><span class="sxs-lookup"><span data-stu-id="731dd-199">Add a `using` statement to reference the `Microsoft.AspNet.SignalR.Hubs` namespace.</span></span> <span data-ttu-id="731dd-200">Ardından `HubName` özniteliğini `ChatHub` sınıfına ekleyin, örneğin `[HubName("ChatHub")]`.</span><span class="sxs-lookup"><span data-stu-id="731dd-200">Then add the `HubName` attribute to the `ChatHub` class, for example `[HubName("ChatHub")]`.</span></span> <span data-ttu-id="731dd-201">Son olarak, jQuery başvurunuz `ChatHub` sınıfına güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="731dd-201">Finally, update your jQuery reference to the `ChatHub` class.</span></span>

<span data-ttu-id="731dd-202">Aşağıdaki kod, betikte bir geri çağırma işlevinin nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="731dd-202">The following code shows how to create a callback function in the script.</span></span> <span data-ttu-id="731dd-203">Sunucu üzerindeki hub sınıfı, içerik güncelleştirmelerini her bir istemciye göndermek için bu işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="731dd-203">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="731dd-204">`htmlEncode` işlevine yönelik isteğe bağlı çağrı, komut dosyası ekleme işlemini önlemenin bir yolu olarak, ileti içeriğini sayfada görüntülemeden önce, HTML 'ye kodlama yolunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="731dd-204">The optional call to the `htmlEncode` function shows a way to HTML encode the message content before displaying it in the page, as a way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample7.html)]

<span data-ttu-id="731dd-205">Aşağıdaki kod, hub ile bir bağlantının nasıl açılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="731dd-205">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="731dd-206">Kod bağlantıyı başlatır ve ardından sohbet sayfasındaki **Gönder** düğmesine tıklama olayını işlemek için bir işlev geçirir.</span><span class="sxs-lookup"><span data-stu-id="731dd-206">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the Chat page.</span></span>

> [!NOTE]
> <span data-ttu-id="731dd-207">Bu yaklaşım, olay işleyicisi yürütmeden önce bağlantının kurulabilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="731dd-207">This approach ensures that the connection is established before the event handler executes.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="731dd-208">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="731dd-208">Next Steps</span></span>

<span data-ttu-id="731dd-209">SignalR 'nin gerçek zamanlı web uygulamaları oluşturmak için bir çerçevede olduğunu öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="731dd-209">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="731dd-210">Ayrıca birkaç SignalR geliştirme görevi öğrendiniz: bir ASP.NET uygulamasına SignalR ekleme, hub sınıfı oluşturma ve hub 'dan ileti gönderme ve alma.</span><span class="sxs-lookup"><span data-stu-id="731dd-210">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="731dd-211">Daha gelişmiş bir SignalR gelişmeleri kavramı hakkında daha fazla bilgi edinmek için, SignalR kaynak kodu ve kaynakları için aşağıdaki siteleri ziyaret edin:</span><span class="sxs-lookup"><span data-stu-id="731dd-211">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources :</span></span>

- [<span data-ttu-id="731dd-212">SignalR projesi</span><span class="sxs-lookup"><span data-stu-id="731dd-212">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="731dd-213">SignalR GitHub ve örnekleri</span><span class="sxs-lookup"><span data-stu-id="731dd-213">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="731dd-214">SignalR wiki</span><span class="sxs-lookup"><span data-stu-id="731dd-214">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
