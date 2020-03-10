---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr
title: 'Öğretici: SignalR 1. x ile çalışmaya başlama | Microsoft Docs'
author: bradygaster
description: Bir HTML sayfasında gerçek zamanlı bir sohbet uygulaması oluşturmak için ASP.NET SignalR kullanın.
ms.author: bradyg
ms.date: 02/18/2013
ms.assetid: fdc3599a-5217-44c1-951f-0eec9812dce7
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 87a90b47ae30bee43e0b0c1e078597db54b8e67d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623545"
---
# <a name="tutorial-getting-started-with-signalr-1x"></a><span data-ttu-id="bd5ae-103">Öğretici: SignalR 1.x ile Çalışmaya Başlama</span><span class="sxs-lookup"><span data-stu-id="bd5ae-103">Tutorial: Getting Started with SignalR 1.x</span></span>

<span data-ttu-id="bd5ae-104">, [Patrick Fleti](https://github.com/pfletcher), [Tim teebken](https://github.com/timlt)</span><span class="sxs-lookup"><span data-stu-id="bd5ae-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="bd5ae-105">Bu öğreticide SignalR kullanarak gerçek zamanlı bir sohbet uygulaması oluşturma işlemi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-105">This tutorial shows how to use SignalR to create a real-time chat application.</span></span> <span data-ttu-id="bd5ae-106">SignalR 'i boş bir ASP.NET Web uygulamasına ekleyecek ve ileti göndermek ve göstermek için bir HTML sayfası oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-106">You will add SignalR to an empty ASP.NET web application and create an HTML page to send and display messages.</span></span>

## <a name="overview"></a><span data-ttu-id="bd5ae-107">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="bd5ae-107">Overview</span></span>

<span data-ttu-id="bd5ae-108">Bu öğretici, basit bir tarayıcı tabanlı sohbet uygulamasının nasıl oluşturulduğunu göstererek SignalR geliştirmeyi tanıtır.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-108">This tutorial introduces SignalR development by showing how to build a simple browser-based chat application.</span></span> <span data-ttu-id="bd5ae-109">SignalR kitaplığını boş bir ASP.NET Web uygulamasına ekleyecek, istemcilere ileti göndermek için bir hub sınıfı oluşturacak ve kullanıcıların sohbet iletilerini göndermesini ve almasına imkan tanıyan bir HTML sayfası oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-109">You will add the SignalR library to an empty ASP.NET web application, create a hub class for sending messages to clients, and create an HTML page that lets users send and receive chat messages.</span></span> <span data-ttu-id="bd5ae-110">MVC 4 ' te MVC görünümü kullanarak bir sohbet uygulamasının nasıl oluşturulduğunu gösteren benzer bir öğretici için bkz. [SignalR ve MVC 4 Ile çalışmaya](index.md)başlama.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-110">For a similar tutorial that shows how to create a chat application in MVC 4 using an MVC view, see [Getting Started with SignalR and MVC 4](index.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bd5ae-111">Bu öğretici, SignalR 'nin sürüm (1. x) sürümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-111">This tutorial uses the release (1.x) version of SignalR.</span></span> <span data-ttu-id="bd5ae-112">SignalR 1. x ve 2,0 arasındaki değişikliklerle ilgili ayrıntılar için bkz. [SignalR 1. x projelerini yükseltme](../releases/upgrading-signalr-1x-projects-to-20.md).</span><span class="sxs-lookup"><span data-stu-id="bd5ae-112">For details on changes between SignalR 1.x and 2.0, see [Upgrading SignalR 1.x Projects](../releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<span data-ttu-id="bd5ae-113">SignalR, canlı Kullanıcı etkileşimi veya gerçek zamanlı veri güncelleştirmeleri gerektiren Web uygulamaları oluşturmaya yönelik açık kaynaklı bir .NET kitaplığıdır.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-113">SignalR is an open-source .NET library for building web applications that require live user interaction or real-time data updates.</span></span> <span data-ttu-id="bd5ae-114">Sosyal uygulamalar, çok kullanıcılı Oyunlar, iş birliği ve Haberler, hava durumu veya finans güncelleştirme uygulamaları buna örnek olarak verilebilir.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-114">Examples include social applications, multiuser games, business collaboration, and news, weather, or financial update applications.</span></span> <span data-ttu-id="bd5ae-115">Bunlar genellikle gerçek zamanlı uygulamalar olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-115">These are often called real-time applications.</span></span>

<span data-ttu-id="bd5ae-116">SignalR gerçek zamanlı uygulamalar oluşturma sürecini basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-116">SignalR simplifies the process of building real-time applications.</span></span> <span data-ttu-id="bd5ae-117">İstemci-sunucu bağlantılarını yönetmeyi kolaylaştırmak ve istemcilere içerik güncelleştirmelerini göndermek için bir ASP.NET sunucu kitaplığı ve bir JavaScript istemci kitaplığı içerir.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-117">It includes an ASP.NET server library and a JavaScript client library to make it easier to manage client-server connections and push content updates to clients.</span></span> <span data-ttu-id="bd5ae-118">SignalR kitaplığını mevcut bir ASP.NET uygulamasına ekleyerek gerçek zamanlı işlevselliği elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-118">You can add the SignalR library to an existing ASP.NET application to gain real-time functionality.</span></span>

<span data-ttu-id="bd5ae-119">Öğreticide aşağıdaki SignalR geliştirme görevleri gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="bd5ae-119">The tutorial demonstrates the following SignalR development tasks:</span></span>

- <span data-ttu-id="bd5ae-120">SignalR kitaplığını bir ASP.NET Web uygulamasına ekleme.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-120">Adding the SignalR library to an ASP.NET web application.</span></span>
- <span data-ttu-id="bd5ae-121">İstemcilere içerik göndermek için bir hub sınıfı oluşturma.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-121">Creating a hub class to push content to clients.</span></span>
- <span data-ttu-id="bd5ae-122">Bir Web sayfasında, iletileri göndermek ve merkezi 'nden güncelleştirme göstermek için SignalR jQuery kitaplığını kullanma.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-122">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="bd5ae-123">Aşağıdaki ekran görüntüsünde, bir tarayıcıda çalışan sohbet uygulaması gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-123">The following screen shot shows the chat application running in a browser.</span></span> <span data-ttu-id="bd5ae-124">Her yeni kullanıcı yorum gönderebilir ve Kullanıcı sohbete katıldıktan sonra eklenen açıklamaları görebilir.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-124">Each new user can post comments and see comments added after the user joins the chat.</span></span>

![Sohbet örnekleri](tutorial-getting-started-with-signalr/_static/image1.png)

<span data-ttu-id="bd5ae-126">Başlıklı</span><span class="sxs-lookup"><span data-stu-id="bd5ae-126">Sections:</span></span>

- [<span data-ttu-id="bd5ae-127">Projeyi ayarlama</span><span class="sxs-lookup"><span data-stu-id="bd5ae-127">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="bd5ae-128">Örneği çalıştırın</span><span class="sxs-lookup"><span data-stu-id="bd5ae-128">Run the Sample</span></span>](#run)
- [<span data-ttu-id="bd5ae-129">Kodu inceleyin</span><span class="sxs-lookup"><span data-stu-id="bd5ae-129">Examine the Code</span></span>](#code)
- [<span data-ttu-id="bd5ae-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bd5ae-130">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="bd5ae-131">Projeyi ayarlama</span><span class="sxs-lookup"><span data-stu-id="bd5ae-131">Set up the Project</span></span>

<span data-ttu-id="bd5ae-132">Bu bölümde, boş bir ASP.NET Web uygulaması oluşturma, SignalR ekleme ve sohbet uygulaması oluşturma işlemlerinin nasıl yapılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-132">This section shows how to create an empty ASP.NET web application, add SignalR, and create the chat application.</span></span>

<span data-ttu-id="bd5ae-133">Ön koşullar:</span><span class="sxs-lookup"><span data-stu-id="bd5ae-133">Prerequisites:</span></span>

- <span data-ttu-id="bd5ae-134">Visual Studio 2010 SP1 veya 2012.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-134">Visual Studio 2010 SP1 or 2012.</span></span> <span data-ttu-id="bd5ae-135">Visual Studio yoksa, ücretsiz Visual Studio 2012 Express geliştirme aracını almak için [ASP.net İndirmeleri](https://www.asp.net/downloads) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-135">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2012 Express Development Tool.</span></span>
- <span data-ttu-id="bd5ae-136">[Microsoft ASP.NET and Web Tools 2012,2](https://go.microsoft.com/fwlink/?LinkId=279941).</span><span class="sxs-lookup"><span data-stu-id="bd5ae-136">[Microsoft ASP.NET and Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=279941).</span></span> <span data-ttu-id="bd5ae-137">Visual Studio 2012 için, bu yükleyici, SignalR şablonları dahil olmak üzere Visual Studio 'ya yeni ASP.NET özellikleri ekler.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-137">For Visual Studio 2012, this installer adds new ASP.NET features including SignalR templates to Visual Studio.</span></span> <span data-ttu-id="bd5ae-138">Visual Studio 2010 SP1 için bir yükleyici yoktur, ancak kurulum adımlarında açıklandığı gibi SignalR NuGet paketini yükleyerek öğreticiyi tamamlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-138">For Visual Studio 2010 SP1, an installer is not available but you can complete the tutorial by installing the SignalR NuGet package as described in the setup steps.</span></span>

<span data-ttu-id="bd5ae-139">Aşağıdaki adımlarda, ASP.NET boş bir Web uygulaması oluşturmak ve SignalR kitaplığını eklemek için Visual Studio 2012 kullanılır:</span><span class="sxs-lookup"><span data-stu-id="bd5ae-139">The following steps use Visual Studio 2012 to create an ASP.NET Empty Web Application and add the SignalR library:</span></span>

1. <span data-ttu-id="bd5ae-140">Visual Studio 'da ASP.NET boş bir Web uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-140">In Visual Studio create an ASP.NET Empty Web Application.</span></span>

    ![Boş Web oluştur](tutorial-getting-started-with-signalr/_static/image2.png)
2. <span data-ttu-id="bd5ae-142">Araçlar 'ı seçerek **Paket Yöneticisi konsolunu** açın **| NuGet Paket Yöneticisi | Paket Yöneticisi konsolu**.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-142">Open the **Package Manager Console** by selecting **Tools | NuGet Package Manager | Package Manager Console**.</span></span> <span data-ttu-id="bd5ae-143">Konsol penceresine aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="bd5ae-143">Enter the following command into the console window:</span></span>

    `Install-Package Microsoft.AspNet.SignalR -Version 1.1.3`

    <span data-ttu-id="bd5ae-144">Bu komut, SignalR 1. x ' in en son sürümünü yüklenir.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-144">This command installs the latest version of SignalR 1.x.</span></span>
3. <span data-ttu-id="bd5ae-145">**Çözüm Gezgini**, projeye sağ tıklayın, Ekle ' yi seçin **| Sınıf**.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-145">In **Solution Explorer**, right-click the project, select **Add | Class**.</span></span> <span data-ttu-id="bd5ae-146">Yeni sınıfı **ChatHub**olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-146">Name the new class **ChatHub**.</span></span>
4. <span data-ttu-id="bd5ae-147">**Çözüm Gezgini** betikler düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-147">In **Solution Explorer** expand the Scripts node.</span></span> <span data-ttu-id="bd5ae-148">JQuery ve SignalR için betik kitaplıkları projede görülebilir.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-148">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    ![Kitaplık başvuruları](tutorial-getting-started-with-signalr/_static/image3.png)
5. <span data-ttu-id="bd5ae-150">**ChatHub** sınıfındaki kodu aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-150">Replace the code in the **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]
6. <span data-ttu-id="bd5ae-151">**Çözüm Gezgini**, projeye sağ tıklayın ve ardından Ekle ' ye tıklayın **| Yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-151">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="bd5ae-152">**Yeni öğe Ekle** Iletişim kutusunda **genel uygulama sınıfı** ' nı seçin ve **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-152">In the **Add New Item** dialog, select **Global Application Class** and click **Add**.</span></span>

    ![Genel Ekle](tutorial-getting-started-with-signalr/_static/image4.png)
7. <span data-ttu-id="bd5ae-154">Global.asax.cs sınıfında, belirtilen `using` deyimlerden sonra aşağıdaki `using` deyimlerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-154">Add the following `using` statements after the provided `using` statements in the Global.asax.cs class.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]
8. <span data-ttu-id="bd5ae-155">SignalR hub 'larının varsayılan yolunu kaydetmek için genel sınıfın `Application_Start` metoduna aşağıdaki kod satırını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-155">Add the following line of code in the `Application_Start` method of the Global class to register the default route for SignalR hubs.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample3.cs)]
9. <span data-ttu-id="bd5ae-156">**Çözüm Gezgini**, projeye sağ tıklayın ve ardından Ekle ' ye tıklayın **| Yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-156">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="bd5ae-157">**Yeni öğe Ekle** Iletişim kutusunda HTML sayfası ' nı seçin ve **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-157">In the **Add New Item** dialog, select Html Page and click **Add**.</span></span>
10. <span data-ttu-id="bd5ae-158">**Çözüm Gezgini**' de, yenı oluşturduğunuz HTML sayfasına sağ tıklayın ve **Başlangıç sayfası olarak ayarla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-158">In **Solution Explorer**, right-click the HTML page you just created and click **Set as Start Page**.</span></span>
11. <span data-ttu-id="bd5ae-159">HTML sayfasındaki varsayılan kodu aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-159">Replace the default code in the HTML page with the following code.</span></span>

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample4.html)]
12. <span data-ttu-id="bd5ae-160">Projenin **Tümünü kaydedin** .</span><span class="sxs-lookup"><span data-stu-id="bd5ae-160">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="bd5ae-161">Örneği çalıştırın</span><span class="sxs-lookup"><span data-stu-id="bd5ae-161">Run the Sample</span></span>

1. <span data-ttu-id="bd5ae-162">Projeyi hata ayıklama modunda çalıştırmak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-162">Press F5 to run the project in debug mode.</span></span> <span data-ttu-id="bd5ae-163">HTML sayfası bir tarayıcı örneğinde yüklenir ve Kullanıcı adı ister.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-163">The HTML page loads in a browser instance and prompts for a user name.</span></span>

    ![Kullanıcı adını girin](tutorial-getting-started-with-signalr/_static/image5.png)
2. <span data-ttu-id="bd5ae-165">Bir kullanıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-165">Enter a user name.</span></span>
3. <span data-ttu-id="bd5ae-166">Tarayıcının adres satırındaki URL 'YI kopyalayın ve bu iki tarayıcı örneği açmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-166">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="bd5ae-167">Her tarayıcı örneğinde benzersiz bir Kullanıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-167">In each browser instance, enter a unique user name.</span></span>
4. <span data-ttu-id="bd5ae-168">Her tarayıcı örneğinde bir açıklama ekleyin ve **Gönder**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-168">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="bd5ae-169">Yorumlar Tüm tarayıcı örneklerinde görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-169">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bd5ae-170">Bu basit sohbet uygulaması, sunucuda tartışma bağlamını korumaz.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-170">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="bd5ae-171">Merkez tüm geçerli kullanıcılara yorum yayınlar.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-171">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="bd5ae-172">Daha sonra sohbete katılması olan kullanıcılar, bu kişilerin eklendiği zamandan eklenen iletileri görür.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-172">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="bd5ae-173">Aşağıdaki ekran görüntüsünde, hepsi bir örnek ileti gönderdiğinde güncellenen üç tarayıcı örneğinde çalışan sohbet uygulaması gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="bd5ae-173">The following screen shot shows the chat application running in three browser instances, all of which are updated when one instance sends a message:</span></span>

    ![Sohbet tarayıcıları](tutorial-getting-started-with-signalr/_static/image6.png)
5. <span data-ttu-id="bd5ae-175">**Çözüm Gezgini**, çalışan uygulamanın **komut dosyası belgeleri** düğümünü inceleyin.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-175">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="bd5ae-176">SignalR kitaplığının çalışma zamanında dinamik olarak oluşturduğu **Hublar** adlı bir betik dosyası vardır.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-176">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="bd5ae-177">Bu dosya jQuery betiği ile sunucu tarafı kodu arasındaki iletişimi yönetir.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-177">This file manages the communication between jQuery script and server-side code.</span></span>

    ![Oluşturulan Merkez betiği](tutorial-getting-started-with-signalr/_static/image7.png)

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="bd5ae-179">Kodu inceleyin</span><span class="sxs-lookup"><span data-stu-id="bd5ae-179">Examine the Code</span></span>

<span data-ttu-id="bd5ae-180">SignalR sohbet uygulaması iki temel SignalR geliştirme görevini gösterir: sunucuda ana düzenleme nesnesi olarak bir hub oluşturma ve ileti göndermek ve almak için SignalR jQuery kitaplığı kullanma.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-180">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="bd5ae-181">SignalR hub 'Ları</span><span class="sxs-lookup"><span data-stu-id="bd5ae-181">SignalR Hubs</span></span>

<span data-ttu-id="bd5ae-182">Kod örneğinde, **ChatHub** sınıfı **Microsoft. Aspnet. SignalR. hub** sınıfından türetilir.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-182">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="bd5ae-183">**Hub** sınıfından türetmek, bir SignalR uygulaması oluşturmanın kullanışlı bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-183">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="bd5ae-184">Hub sınıfınız üzerinde ortak Yöntemler oluşturabilir ve ardından bunları bir Web sayfasındaki jQuery komut dosyalarından çağırarak bu yöntemlere erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-184">You can create public methods on your hub class and then access those methods by calling them from jQuery scripts in a web page.</span></span>

<span data-ttu-id="bd5ae-185">Sohbet kodunda, istemciler yeni bir ileti göndermek için **ChatHub. Send** yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-185">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="bd5ae-186">İçindeki hub, iletileri **istemciler. ALL. Yayıniletisi**çağırarak tüm istemcilere gönderir.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-186">The hub in turn sends the message to all clients by calling **Clients.All.broadcastMessage**.</span></span>

<span data-ttu-id="bd5ae-187">**Send** yöntemi çeşitli Merkez kavramlarını gösterir:</span><span class="sxs-lookup"><span data-stu-id="bd5ae-187">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="bd5ae-188">İstemcilerin bunları çağırabilmesi için ortak yöntemleri bir hub üzerinde bildirin.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-188">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="bd5ae-189">Bu hub 'a bağlı tüm istemcilere erişmek için **Microsoft. Aspnet. SignalR. hub. clients** dinamik özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-189">Use the **Microsoft.AspNet.SignalR.Hub.Clients** dynamic property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="bd5ae-190">İstemcileri güncelleştirmek için istemcide jQuery işlevini (`broadcastMessage` işlevi gibi) çağırın.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-190">Call a jQuery function on the client (such as the `broadcastMessage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="bd5ae-191">SignalR ve jQuery</span><span class="sxs-lookup"><span data-stu-id="bd5ae-191">SignalR and jQuery</span></span>

<span data-ttu-id="bd5ae-192">Kod örneğindeki HTML sayfası, SignalR hub 'ı ile iletişim kurmak için SignalR jQuery kitaplığını nasıl kullanacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-192">The HTML page in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="bd5ae-193">Koddaki temel görevler, hub 'a başvurmak için bir proxy bildiriyor, sunucunun istemcilere içerik göndermek için çağırabilir bir işlev bildiriyor ve hub 'a ileti gönderecek bir bağlantı başlatıyor.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-193">The essential tasks in the code are declaring a proxy to reference the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="bd5ae-194">Aşağıdaki kod bir hub için proxy bildirir.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-194">The following code declares a proxy for a hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="bd5ae-195">JQuery içinde, sunucu sınıfına ve üyelerine yönelik başvuru ortası durumunda.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-195">In jQuery the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="bd5ae-196">Kod örneği, jQuery içindeki C# **ChatHub** sınıfına **ChatHub**olarak başvurur.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-196">The code sample references the C# **ChatHub** class in jQuery as **chatHub**.</span></span>

<span data-ttu-id="bd5ae-197">Aşağıdaki kod, komut dosyasında bir geri çağırma işlevi oluşturma işlemi.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-197">The following code is how you create a callback function in the script.</span></span> <span data-ttu-id="bd5ae-198">Sunucu üzerindeki hub sınıfı, içerik güncelleştirmelerini her bir istemciye göndermek için bu işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-198">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="bd5ae-199">HTML 'nin içeriği görüntülemeden önce kodladığı iki satır isteğe bağlıdır ve betik ekleme işlemini önlemenin basit bir yolunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-199">The two lines that HTML encode the content before displaying it are optional and show a simple way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample7.html)]

<span data-ttu-id="bd5ae-200">Aşağıdaki kod, hub ile bir bağlantının nasıl açılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-200">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="bd5ae-201">Kod bağlantıyı başlatır ve sonra HTML sayfasındaki **Gönder** düğmesine tıklama olayını işlemek için bir işlev geçirir.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-201">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the HTML page.</span></span>

> [!NOTE]
> <span data-ttu-id="bd5ae-202">Bu yaklaşım, bağlantının olay işleyicisi yürütmeden önce yöntem.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-202">This approach insures that the connection is established before the event handler executes.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="bd5ae-203">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="bd5ae-203">Next Steps</span></span>

<span data-ttu-id="bd5ae-204">SignalR 'nin gerçek zamanlı web uygulamaları oluşturmak için bir çerçevede olduğunu öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-204">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="bd5ae-205">Ayrıca birkaç SignalR geliştirme görevi öğrendiniz: bir ASP.NET uygulamasına SignalR ekleme, hub sınıfı oluşturma ve hub 'dan ileti gönderme ve alma.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-205">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="bd5ae-206">Bu öğreticide veya diğer SignalR uygulamalarında örnek uygulamayı bir barındırma sağlayıcısına dağıtarak Internet üzerinden kullanılabilir hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-206">You can make the sample application in this tutorial or other SignalR applications available over the Internet by deploying them to a hosting provider.</span></span> <span data-ttu-id="bd5ae-207">Microsoft, ücretsiz bir [Windows Azure deneme hesabında](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)en fazla 10 Web sitesi için ücretsiz web barındırma hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-207">Microsoft offers free web hosting for up to 10 web sites in a free [Windows Azure trial account](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="bd5ae-208">Örnek SignalR uygulamasını dağıtma hakkında yönergeler için bkz. [SignalR Başlarken örneğini bir Windows Azure Web sitesi olarak yayımlama](https://blogs.msdn.com/b/timlee/archive/2013/02/27/deploy-the-signalr-getting-started-sample-as-a-windows-azure-web-site.aspx).</span><span class="sxs-lookup"><span data-stu-id="bd5ae-208">For a walkthrough on how to deploy the sample SignalR application, see [Publish the SignalR Getting Started Sample as a Windows Azure Web Site](https://blogs.msdn.com/b/timlee/archive/2013/02/27/deploy-the-signalr-getting-started-sample-as-a-windows-azure-web-site.aspx).</span></span> <span data-ttu-id="bd5ae-209">Bir Visual Studio Web projesinin bir Windows Azure Web sitesine nasıl dağıtılacağı hakkında ayrıntılı bilgi için, bkz. [Windows Azure Web sitesine bir ASP.NET uygulaması dağıtma](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).</span><span class="sxs-lookup"><span data-stu-id="bd5ae-209">For detailed information about how to deploy a Visual Studio web project to a Windows Azure Web Site, see [Deploying an ASP.NET Application to a Windows Azure Web Site](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).</span></span> <span data-ttu-id="bd5ae-210">(Not: WebSocket aktarımı Şu anda Microsoft Azure Web siteleri için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="bd5ae-210">(Note: The WebSocket transport is not currently supported for Windows Azure Web Sites.</span></span> <span data-ttu-id="bd5ae-211">WebSocket taşıması kullanılabilir olmadığında, SignalR, [SignalR 'ye Giriş konusunun](index.md)aktarımlar bölümünde açıklandığı gibi diğer kullanılabilir taşımaları kullanır.)</span><span class="sxs-lookup"><span data-stu-id="bd5ae-211">When WebSocket transport is not available, SignalR uses the other available transports as described in the Transports section of the [Introduction to SignalR topic](index.md).)</span></span>

<span data-ttu-id="bd5ae-212">Daha gelişmiş bir SignalR gelişmeleri kavramı hakkında daha fazla bilgi edinmek için, SignalR kaynak kodu ve kaynakları için aşağıdaki siteleri ziyaret edin:</span><span class="sxs-lookup"><span data-stu-id="bd5ae-212">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="bd5ae-213">SignalR projesi</span><span class="sxs-lookup"><span data-stu-id="bd5ae-213">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="bd5ae-214">SignalR GitHub ve örnekleri</span><span class="sxs-lookup"><span data-stu-id="bd5ae-214">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="bd5ae-215">SignalR wiki</span><span class="sxs-lookup"><span data-stu-id="bd5ae-215">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
