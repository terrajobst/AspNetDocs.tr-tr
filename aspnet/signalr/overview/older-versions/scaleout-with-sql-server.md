---
uid: signalr/overview/older-versions/scaleout-with-sql-server
title: SignalR ölçeği SQL Server (SignalR 1. x) | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 1dca7967-8296-444a-9533-837eb284e78c
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: 8674b06a2a751c9a7b1c6c9b19782974d0602a62
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536472"
---
# <a name="signalr-scaleout-with-sql-server-signalr-1x"></a><span data-ttu-id="a2f58-102">SQL Server ile SignalR Ölçeğini Genişletme (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="a2f58-102">SignalR Scaleout with SQL Server (SignalR 1.x)</span></span>

<span data-ttu-id="a2f58-103">, [Mike Ison](https://github.com/MikeWasson), [Patrick fleti](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="a2f58-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="a2f58-104">Bu öğreticide, iki ayrı IIS örneğine dağıtılan bir SignalR uygulamasına ileti dağıtmak için SQL Server kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="a2f58-104">In this tutorial, you will use SQL Server to distribute messages across a SignalR application that is deployed in two separate IIS instances.</span></span> <span data-ttu-id="a2f58-105">Bu öğreticiyi tek bir test makinesinde da çalıştırabilirsiniz, ancak tüm etkiyi almak için, SignalR uygulamasını iki veya daha fazla sunucuya dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2f58-105">You can also run this tutorial on a single test machine, but to get the full effect, you need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="a2f58-106">Ayrıca, sunuculardan birine veya ayrı bir adanmış sunucuya SQL Server de yüklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="a2f58-106">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span> <span data-ttu-id="a2f58-107">Diğer bir seçenek ise Azure 'da VM 'Leri kullanarak öğreticiyi çalıştıradır.</span><span class="sxs-lookup"><span data-stu-id="a2f58-107">Another option is to run the tutorial using VMs on Azure.</span></span>

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a><span data-ttu-id="a2f58-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="a2f58-108">Prerequisites</span></span>

<span data-ttu-id="a2f58-109">Microsoft SQL Server 2005 veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="a2f58-109">Microsoft SQL Server 2005 or later.</span></span> <span data-ttu-id="a2f58-110">Arka düzlem SQL Server hem masaüstü hem de sunucu sürümlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="a2f58-110">The backplane supports both desktop and server editions of SQL Server.</span></span> <span data-ttu-id="a2f58-111">SQL Server Compact Edition veya Azure SQL veritabanı 'nı desteklemez.</span><span class="sxs-lookup"><span data-stu-id="a2f58-111">It does not support SQL Server Compact Edition or Azure SQL Database.</span></span> <span data-ttu-id="a2f58-112">(Uygulamanız Azure üzerinde barındırılıyorsa, bunun yerine Service Bus geri düzlemi göz önünde bulundurun.)</span><span class="sxs-lookup"><span data-stu-id="a2f58-112">(If your application is hosted on Azure, consider the Service Bus backplane instead.)</span></span>

## <a name="overview"></a><span data-ttu-id="a2f58-113">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="a2f58-113">Overview</span></span>

<span data-ttu-id="a2f58-114">Ayrıntılı öğreticiye girmeden önce, ne yapabileceğinize ilişkin hızlı bir genel bakış sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a2f58-114">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="a2f58-115">Yeni boş bir veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a2f58-115">Create a new empty database.</span></span> <span data-ttu-id="a2f58-116">Geri düzlemi bu veritabanında gerekli tabloları oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="a2f58-116">The backplane will create the necessary tables in this database.</span></span>
2. <span data-ttu-id="a2f58-117">Bu NuGet paketlerini uygulamanıza ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a2f58-117">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="a2f58-118">Microsoft. AspNet. SignalR</span><span class="sxs-lookup"><span data-stu-id="a2f58-118">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="a2f58-119">Microsoft. AspNet. SignalR. SqlServer</span><span class="sxs-lookup"><span data-stu-id="a2f58-119">Microsoft.AspNet.SignalR.SqlServer</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. <span data-ttu-id="a2f58-120">Bir SignalR uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a2f58-120">Create a SignalR application.</span></span>
4. <span data-ttu-id="a2f58-121">Geri düzlemi yapılandırmak için aşağıdaki kodu Global. asax öğesine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a2f58-121">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

## <a name="configure-the-database"></a><span data-ttu-id="a2f58-122">Veritabanını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a2f58-122">Configure the Database</span></span>

<span data-ttu-id="a2f58-123">Uygulamanın, veritabanına erişmek için Windows kimlik doğrulaması veya SQL Server kimlik doğrulaması kullanıp kullanmayacağını belirleyin.</span><span class="sxs-lookup"><span data-stu-id="a2f58-123">Decide whether the application will use Windows authentication or SQL Server authentication to access the database.</span></span> <span data-ttu-id="a2f58-124">Ne olursa olsun, veritabanı kullanıcısının oturum açma, şema oluşturma ve tablo oluşturma izinlerine sahip olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a2f58-124">Regardless, make sure the database user has permissions to log in, create schemas, and create tables.</span></span>

<span data-ttu-id="a2f58-125">Kullanılacak geri düzlemi için yeni bir veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a2f58-125">Create a new database for the backplane to use.</span></span> <span data-ttu-id="a2f58-126">Veritabanına bir ad verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2f58-126">You can give the database any name.</span></span> <span data-ttu-id="a2f58-127">Veritabanında herhangi bir tablo oluşturmanız gerekmez; geri düzlemi gerekli tabloları oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="a2f58-127">You don't need to create any tables in the database; the backplane will create the necessary tables.</span></span>

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a><span data-ttu-id="a2f58-128">Hizmet Aracısı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a2f58-128">Enable Service Broker</span></span>

<span data-ttu-id="a2f58-129">Arka düzme veritabanı için Hizmet Aracısı etkinleştirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="a2f58-129">It is recommended to enable Service Broker for the backplane database.</span></span> <span data-ttu-id="a2f58-130">Hizmet Aracısı, arka düzlemi güncelleştirmeleri daha verimli bir şekilde almasına olanak sağlayan SQL Server ileti ve kuyruğa alma için yerel destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="a2f58-130">Service Broker provides native support for messaging and queuing in SQL Server, which lets the backplane receive updates more efficiently.</span></span> <span data-ttu-id="a2f58-131">(Ancak, geri düzlem Hizmet Aracısı olmadan da kullanılabilir.)</span><span class="sxs-lookup"><span data-stu-id="a2f58-131">(However, the backplane also works without Service Broker.)</span></span>

<span data-ttu-id="a2f58-132">Hizmet Aracısı etkinleştirilip etkinleştirilmediğini denetlemek için **sys. databases** katalog görünümündeki **\_Broker\_etkin** sütununu sorgulayın.</span><span class="sxs-lookup"><span data-stu-id="a2f58-132">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

<span data-ttu-id="a2f58-133">Hizmet Aracısı etkinleştirmek için aşağıdaki SQL sorgusunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="a2f58-133">To enable Service Broker, use the following SQL query:</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> <span data-ttu-id="a2f58-134">Bu sorgu kilitlenme olarak görünüyorsa, VERITABANıNA bağlı bir uygulama olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="a2f58-134">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>

<span data-ttu-id="a2f58-135">İzlemeyi etkinleştirdiyseniz, izlemeler Hizmet Aracısı etkinleştirilip etkinleştirilmediğini de gösterir.</span><span class="sxs-lookup"><span data-stu-id="a2f58-135">If you have enabled tracing, the traces will also show whether Service Broker is enabled.</span></span>

## <a name="create-a-signalr-application"></a><span data-ttu-id="a2f58-136">SignalR uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2f58-136">Create a SignalR Application</span></span>

<span data-ttu-id="a2f58-137">Bu öğreticilerden birini izleyerek bir SignalR uygulaması oluşturun:</span><span class="sxs-lookup"><span data-stu-id="a2f58-137">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="a2f58-138">SignalR ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a2f58-138">Getting Started with SignalR</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="a2f58-139">SignalR ve MVC 4 ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a2f58-139">Getting Started with SignalR and MVC 4</span></span>](tutorial-getting-started-with-signalr-and-mvc-4.md)

<span data-ttu-id="a2f58-140">Daha sonra, SQL Server ile ölçeği desteklemek için sohbet uygulamasını değiştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="a2f58-140">Next, we'll modify the chat application to support scaleout with SQL Server.</span></span> <span data-ttu-id="a2f58-141">İlk olarak, SignalR. SqlServer NuGet paketini projenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a2f58-141">First, add the SignalR.SqlServer NuGet package to your project.</span></span> <span data-ttu-id="a2f58-142">Visual Studio 'da, **Araçlar** menüsünden **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="a2f58-142">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="a2f58-143">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="a2f58-143">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

<span data-ttu-id="a2f58-144">Ardından, Global. asax dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="a2f58-144">Next, open the Global.asax file.</span></span> <span data-ttu-id="a2f58-145">Aşağıdaki kodu **uygulama\_başlangıç** yöntemine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a2f58-145">Add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="a2f58-146">Uygulamayı dağıtma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a2f58-146">Deploy and Run the Application</span></span>

<span data-ttu-id="a2f58-147">SignalR uygulamasını dağıtmak için Windows Server örneklerinizi hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="a2f58-147">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="a2f58-148">IIS rolünü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a2f58-148">Add the IIS role.</span></span> <span data-ttu-id="a2f58-149">WebSocket protokolü de dahil olmak üzere "uygulama geliştirme" özellikleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a2f58-149">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-sql-server/_static/image4.png)

<span data-ttu-id="a2f58-150">Ayrıca yönetim hizmetini de ("Yönetim Araçları" altında listelenmiştir) içerir.</span><span class="sxs-lookup"><span data-stu-id="a2f58-150">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-sql-server/_static/image5.png)

<span data-ttu-id="a2f58-151">**Web Dağıtımı 3,0 ' ü yükler.**</span><span class="sxs-lookup"><span data-stu-id="a2f58-151">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="a2f58-152">IIS Yöneticisi 'Ni çalıştırdığınızda, Microsoft Web platformu yüklemenizi ister veya [yükleyiciyi indirebilirsiniz](https://go.microsoft.com/fwlink/?LinkId=255386).</span><span class="sxs-lookup"><span data-stu-id="a2f58-152">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="a2f58-153">Platform yükleyicisinde Web Dağıtımı arayın ve Web Dağıtımı 3,0 ' i yükleme</span><span class="sxs-lookup"><span data-stu-id="a2f58-153">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-sql-server/_static/image6.png)

<span data-ttu-id="a2f58-154">Web yönetimi hizmetinin çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="a2f58-154">Check that the Web Management Service is running.</span></span> <span data-ttu-id="a2f58-155">Aksi takdirde, hizmeti başlatın.</span><span class="sxs-lookup"><span data-stu-id="a2f58-155">If not, start the service.</span></span> <span data-ttu-id="a2f58-156">(Windows hizmetleri listesinde Web yönetimi hizmetini görmüyorsanız, IIS rolünü eklediğinizde Yönetim hizmetini yüklediğinizden emin olun.)</span><span class="sxs-lookup"><span data-stu-id="a2f58-156">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="a2f58-157">Son olarak, TCP için 8172 numaralı bağlantı noktasını açın.</span><span class="sxs-lookup"><span data-stu-id="a2f58-157">Finally, open port 8172 for TCP.</span></span> <span data-ttu-id="a2f58-158">Bu, Web Dağıtımı aracının kullandığı bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="a2f58-158">This is the port that the Web Deploy tool uses.</span></span>

<span data-ttu-id="a2f58-159">Artık Visual Studio projesini geliştirme makinenizden sunucuya dağıtmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="a2f58-159">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="a2f58-160">Çözüm Gezgini, çözüme sağ tıklayın ve **Yayımla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2f58-160">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="a2f58-161">Web dağıtımı hakkında daha ayrıntılı belgeler için bkz. [Visual Studio Için Web dağıtımı Içerik Haritası ve ASP.net](../../../whitepapers/aspnet-web-deployment-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="a2f58-161">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="a2f58-162">Uygulamayı iki sunucuya dağıtırsanız, her bir örneği ayrı bir tarayıcı penceresinde açabilir ve bunların her birinin birinden SignalR iletileri aldıklarından emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2f58-162">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="a2f58-163">(Kuşkusuz, bir üretim ortamında, iki sunucu bir yük dengeleyicinin arkasına ait olacaktır.)</span><span class="sxs-lookup"><span data-stu-id="a2f58-163">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-sql-server/_static/image7.png)

<span data-ttu-id="a2f58-164">Uygulamayı çalıştırdıktan sonra, SignalR 'nin veritabanında otomatik olarak tablo oluşturduğunu görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a2f58-164">After you run the application, you can see that SignalR has automatically created tables in the database:</span></span>

![](scaleout-with-sql-server/_static/image8.png)

<span data-ttu-id="a2f58-165">SignalR tabloları yönetir.</span><span class="sxs-lookup"><span data-stu-id="a2f58-165">SignalR manages the tables.</span></span> <span data-ttu-id="a2f58-166">Uygulamanız dağıtıldığı sürece satırları silmeyin, tabloyu değiştirmez ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="a2f58-166">As long as your application is deployed, don't delete rows, modify the table, and so forth.</span></span>
