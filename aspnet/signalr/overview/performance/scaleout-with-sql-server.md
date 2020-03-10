---
uid: signalr/overview/performance/scaleout-with-sql-server
title: SignalR ölçeği SQL Server | Microsoft Docs
author: bradygaster
description: Bu konuda kullanılan yazılım sürümleri, .NET 4,5 SignalR sürüm 2 ' nin önceki sürümleri hakkında bilgi Için bu konunun önceki sürümlerini Visual Studio 2013...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 98358b6e-9139-4239-ba3a-2d7dd74dd664
msc.legacyurl: /signalr/overview/performance/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: 709a9ebf8f3396842bee0d87e621c00ae1418ec1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579186"
---
# <a name="signalr-scaleout-with-sql-server"></a><span data-ttu-id="33133-103">SQL Server ile SignalR Ölçeğini Genişletme</span><span class="sxs-lookup"><span data-stu-id="33133-103">SignalR Scaleout with SQL Server</span></span>

<span data-ttu-id="33133-104">, [Mike Ison](https://github.com/MikeWasson), [Patrick fleti](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="33133-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="33133-105">Bu konuda kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="33133-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="33133-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="33133-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="33133-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="33133-107">.NET 4.5</span></span>
> - <span data-ttu-id="33133-108">SignalR sürüm 2</span><span class="sxs-lookup"><span data-stu-id="33133-108">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="33133-109">Bu konunun önceki sürümleri</span><span class="sxs-lookup"><span data-stu-id="33133-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="33133-110">SignalR 'nin önceki sürümleri hakkında daha fazla bilgi için bkz. [SignalR daha eski sürümleri](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="33133-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="33133-111">Sorular ve açıklamalar</span><span class="sxs-lookup"><span data-stu-id="33133-111">Questions and comments</span></span>
>
> <span data-ttu-id="33133-112">Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun.</span><span class="sxs-lookup"><span data-stu-id="33133-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="33133-113">Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33133-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="33133-114">Bu öğreticide, iki ayrı IIS örneğine dağıtılan bir SignalR uygulamasına ileti dağıtmak için SQL Server kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="33133-114">In this tutorial, you will use SQL Server to distribute messages across a SignalR application that is deployed in two separate IIS instances.</span></span> <span data-ttu-id="33133-115">Bu öğreticiyi tek bir test makinesinde da çalıştırabilirsiniz, ancak tüm etkiyi almak için, SignalR uygulamasını iki veya daha fazla sunucuya dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="33133-115">You can also run this tutorial on a single test machine, but to get the full effect, you need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="33133-116">Ayrıca, sunuculardan birine veya ayrı bir adanmış sunucuya SQL Server de yüklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="33133-116">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span> <span data-ttu-id="33133-117">Diğer bir seçenek ise Azure 'da VM 'Leri kullanarak öğreticiyi çalıştıradır.</span><span class="sxs-lookup"><span data-stu-id="33133-117">Another option is to run the tutorial using VMs on Azure.</span></span>

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a><span data-ttu-id="33133-118">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="33133-118">Prerequisites</span></span>

<span data-ttu-id="33133-119">Microsoft SQL Server 2005 veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="33133-119">Microsoft SQL Server 2005 or later.</span></span> <span data-ttu-id="33133-120">Arka düzlem SQL Server hem masaüstü hem de sunucu sürümlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="33133-120">The backplane supports both desktop and server editions of SQL Server.</span></span> <span data-ttu-id="33133-121">SQL Server Compact Edition veya Azure SQL veritabanı 'nı desteklemez.</span><span class="sxs-lookup"><span data-stu-id="33133-121">It does not support SQL Server Compact Edition or Azure SQL Database.</span></span> <span data-ttu-id="33133-122">(Uygulamanız Azure üzerinde barındırılıyorsa, bunun yerine Service Bus geri düzlemi göz önünde bulundurun.)</span><span class="sxs-lookup"><span data-stu-id="33133-122">(If your application is hosted on Azure, consider the Service Bus backplane instead.)</span></span>

## <a name="overview"></a><span data-ttu-id="33133-123">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="33133-123">Overview</span></span>

<span data-ttu-id="33133-124">Ayrıntılı öğreticiye girmeden önce, ne yapabileceğinize ilişkin hızlı bir genel bakış sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="33133-124">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="33133-125">Yeni boş bir veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="33133-125">Create a new empty database.</span></span> <span data-ttu-id="33133-126">Geri düzlemi bu veritabanında gerekli tabloları oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="33133-126">The backplane will create the necessary tables in this database.</span></span>
2. <span data-ttu-id="33133-127">Bu NuGet paketlerini uygulamanıza ekleyin:</span><span class="sxs-lookup"><span data-stu-id="33133-127">Add these NuGet packages to your application:</span></span>

    - [<span data-ttu-id="33133-128">Microsoft. AspNet. SignalR</span><span class="sxs-lookup"><span data-stu-id="33133-128">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="33133-129">Microsoft. AspNet. SignalR. SqlServer</span><span class="sxs-lookup"><span data-stu-id="33133-129">Microsoft.AspNet.SignalR.SqlServer</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. <span data-ttu-id="33133-130">Bir SignalR uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="33133-130">Create a SignalR application.</span></span>
4. <span data-ttu-id="33133-131">Geri düzlemi yapılandırmak için Startup.cs 'e aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="33133-131">Add the following code to Startup.cs to configure the backplane:</span></span>

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

   <span data-ttu-id="33133-132">Bu kod, geri düzlemi [Tablecount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx) ve [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)için varsayılan değerlerle yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="33133-132">This code configures the backplane with the default values for [TableCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx) and [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span></span> <span data-ttu-id="33133-133">Bu değerleri değiştirme hakkında daha fazla bilgi için bkz. [SignalR performansı: genişleme ölçümleri](signalr-performance.md#scaleout_metrics).</span><span class="sxs-lookup"><span data-stu-id="33133-133">For information on changing these values, see [SignalR Performance: Scaleout Metrics](signalr-performance.md#scaleout_metrics).</span></span>

## <a name="configure-the-database"></a><span data-ttu-id="33133-134">Veritabanını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="33133-134">Configure the Database</span></span>

<span data-ttu-id="33133-135">Uygulamanın, veritabanına erişmek için Windows kimlik doğrulaması veya SQL Server kimlik doğrulaması kullanıp kullanmayacağını belirleyin.</span><span class="sxs-lookup"><span data-stu-id="33133-135">Decide whether the application will use Windows authentication or SQL Server authentication to access the database.</span></span> <span data-ttu-id="33133-136">Ne olursa olsun, veritabanı kullanıcısının oturum açma, şema oluşturma ve tablo oluşturma izinlerine sahip olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="33133-136">Regardless, make sure the database user has permissions to log in, create schemas, and create tables.</span></span>

<span data-ttu-id="33133-137">Kullanılacak geri düzlemi için yeni bir veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="33133-137">Create a new database for the backplane to use.</span></span> <span data-ttu-id="33133-138">Veritabanına bir ad verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33133-138">You can give the database any name.</span></span> <span data-ttu-id="33133-139">Veritabanında herhangi bir tablo oluşturmanız gerekmez; geri düzlemi gerekli tabloları oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="33133-139">You don't need to create any tables in the database; the backplane will create the necessary tables.</span></span>

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a><span data-ttu-id="33133-140">Hizmet Aracısı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="33133-140">Enable Service Broker</span></span>

<span data-ttu-id="33133-141">Arka düzme veritabanı için Hizmet Aracısı etkinleştirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="33133-141">It is recommended to enable Service Broker for the backplane database.</span></span> <span data-ttu-id="33133-142">Hizmet Aracısı, arka düzlemi güncelleştirmeleri daha verimli bir şekilde almasına olanak sağlayan SQL Server ileti ve kuyruğa alma için yerel destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="33133-142">Service Broker provides native support for messaging and queuing in SQL Server, which lets the backplane receive updates more efficiently.</span></span> <span data-ttu-id="33133-143">(Ancak, geri düzlem Hizmet Aracısı olmadan da kullanılabilir.)</span><span class="sxs-lookup"><span data-stu-id="33133-143">(However, the backplane also works without Service Broker.)</span></span>

<span data-ttu-id="33133-144">Hizmet Aracısı etkinleştirilip etkinleştirilmediğini denetlemek için **sys. databases** katalog görünümündeki **\_Broker\_etkin** sütununu sorgulayın.</span><span class="sxs-lookup"><span data-stu-id="33133-144">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

<span data-ttu-id="33133-145">Hizmet Aracısı etkinleştirmek için aşağıdaki SQL sorgusunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="33133-145">To enable Service Broker, use the following SQL query:</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> <span data-ttu-id="33133-146">Bu sorgu kilitlenme olarak görünüyorsa, VERITABANıNA bağlı bir uygulama olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="33133-146">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>

<span data-ttu-id="33133-147">İzlemeyi etkinleştirdiyseniz, izlemeler Hizmet Aracısı etkinleştirilip etkinleştirilmediğini de gösterir.</span><span class="sxs-lookup"><span data-stu-id="33133-147">If you have enabled tracing, the traces will also show whether Service Broker is enabled.</span></span>

## <a name="create-a-signalr-application"></a><span data-ttu-id="33133-148">SignalR uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="33133-148">Create a SignalR Application</span></span>

<span data-ttu-id="33133-149">Bu öğreticilerden birini izleyerek bir SignalR uygulaması oluşturun:</span><span class="sxs-lookup"><span data-stu-id="33133-149">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="33133-150">SignalR 2,0 ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="33133-150">Getting Started with SignalR 2.0</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="33133-151">SignalR 2,0 ve MVC 5 ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="33133-151">Getting Started with SignalR 2.0 and MVC 5</span></span>](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

<span data-ttu-id="33133-152">Daha sonra, SQL Server ile ölçeği desteklemek için sohbet uygulamasını değiştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="33133-152">Next, we'll modify the chat application to support scaleout with SQL Server.</span></span> <span data-ttu-id="33133-153">İlk olarak, SignalR. SqlServer NuGet paketini projenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="33133-153">First, add the SignalR.SqlServer NuGet package to your project.</span></span> <span data-ttu-id="33133-154">Visual Studio 'da, **Araçlar** menüsünden **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="33133-154">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="33133-155">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="33133-155">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

<span data-ttu-id="33133-156">Sonra, Startup.cs dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="33133-156">Next, open the Startup.cs file.</span></span> <span data-ttu-id="33133-157">**Yapılandırma** yöntemine aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="33133-157">Add the following code to the **Configure** method:</span></span>

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="33133-158">Uygulamayı dağıtma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="33133-158">Deploy and Run the Application</span></span>

<span data-ttu-id="33133-159">SignalR uygulamasını dağıtmak için Windows Server örneklerinizi hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="33133-159">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="33133-160">IIS rolünü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="33133-160">Add the IIS role.</span></span> <span data-ttu-id="33133-161">WebSocket protokolü de dahil olmak üzere "uygulama geliştirme" özellikleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="33133-161">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-sql-server/_static/image4.png)

<span data-ttu-id="33133-162">Ayrıca yönetim hizmetini de ("Yönetim Araçları" altında listelenmiştir) içerir.</span><span class="sxs-lookup"><span data-stu-id="33133-162">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-sql-server/_static/image5.png)

<span data-ttu-id="33133-163">**Web Dağıtımı 3,0 ' ü yükler.**</span><span class="sxs-lookup"><span data-stu-id="33133-163">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="33133-164">IIS Yöneticisi 'Ni çalıştırdığınızda, Microsoft Web platformu yüklemenizi ister veya [yükleyiciyi indirebilirsiniz](https://go.microsoft.com/fwlink/?LinkId=255386).</span><span class="sxs-lookup"><span data-stu-id="33133-164">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="33133-165">Platform yükleyicisinde Web Dağıtımı arayın ve Web Dağıtımı 3,0 ' i yükleme</span><span class="sxs-lookup"><span data-stu-id="33133-165">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-sql-server/_static/image6.png)

<span data-ttu-id="33133-166">Web yönetimi hizmetinin çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="33133-166">Check that the Web Management Service is running.</span></span> <span data-ttu-id="33133-167">Aksi takdirde, hizmeti başlatın.</span><span class="sxs-lookup"><span data-stu-id="33133-167">If not, start the service.</span></span> <span data-ttu-id="33133-168">(Windows hizmetleri listesinde Web yönetimi hizmetini görmüyorsanız, IIS rolünü eklediğinizde Yönetim hizmetini yüklediğinizden emin olun.)</span><span class="sxs-lookup"><span data-stu-id="33133-168">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="33133-169">Son olarak, TCP için 8172 numaralı bağlantı noktasını açın.</span><span class="sxs-lookup"><span data-stu-id="33133-169">Finally, open port 8172 for TCP.</span></span> <span data-ttu-id="33133-170">Bu, Web Dağıtımı aracının kullandığı bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="33133-170">This is the port that the Web Deploy tool uses.</span></span>

<span data-ttu-id="33133-171">Artık Visual Studio projesini geliştirme makinenizden sunucuya dağıtmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="33133-171">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="33133-172">Çözüm Gezgini, çözüme sağ tıklayın ve **Yayımla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="33133-172">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="33133-173">Web dağıtımı hakkında daha ayrıntılı belgeler için bkz. [Visual Studio Için Web dağıtımı Içerik Haritası ve ASP.net](../../../whitepapers/aspnet-web-deployment-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="33133-173">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="33133-174">Uygulamayı iki sunucuya dağıtırsanız, her bir örneği ayrı bir tarayıcı penceresinde açabilir ve bunların her birinin birinden SignalR iletileri aldıklarından emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33133-174">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="33133-175">(Kuşkusuz, bir üretim ortamında, iki sunucu bir yük dengeleyicinin arkasına ait olacaktır.)</span><span class="sxs-lookup"><span data-stu-id="33133-175">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-sql-server/_static/image7.png)

<span data-ttu-id="33133-176">Uygulamayı çalıştırdıktan sonra, SignalR 'nin veritabanında otomatik olarak tablo oluşturduğunu görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="33133-176">After you run the application, you can see that SignalR has automatically created tables in the database:</span></span>

![](scaleout-with-sql-server/_static/image8.png)

<span data-ttu-id="33133-177">SignalR tabloları yönetir.</span><span class="sxs-lookup"><span data-stu-id="33133-177">SignalR manages the tables.</span></span> <span data-ttu-id="33133-178">Uygulamanız dağıtıldığı sürece satırları silmeyin, tabloyu değiştirmez ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="33133-178">As long as your application is deployed, don't delete rows, modify the table, and so forth.</span></span>
