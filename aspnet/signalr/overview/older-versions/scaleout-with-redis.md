---
uid: signalr/overview/older-versions/scaleout-with-redis
title: Redsıs ile SignalR ölçeğini genişletme (SignalR 1. x) | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 6abecf80-8ffa-41ba-b0d9-1d9edbe7687b
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 5079cf3fa773faeac911eddc75dc66e94ad98bb0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536563"
---
# <a name="signalr-scaleout-with-redis-signalr-1x"></a><span data-ttu-id="ff7b6-102">Redis ile SignalR Ölçeğini Genişletme (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="ff7b6-102">SignalR Scaleout with Redis (SignalR 1.x)</span></span>

<span data-ttu-id="ff7b6-103">, [Mike Ison](https://github.com/MikeWasson), [Patrick fleti](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="ff7b6-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="ff7b6-104">Bu öğreticide, iki ayrı IIS örneğine dağıtılan bir SignalR uygulamasına ileti dağıtmak için [redsıs](http://redis.io/) ' i kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-104">In this tutorial, you will use [Redis](http://redis.io/) to distribute messages across a SignalR application that is deployed on two separate IIS instances.</span></span>

<span data-ttu-id="ff7b6-105">Redsıs, bellek içi anahtar-değer deposudur.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-105">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="ff7b6-106">Ayrıca, Yayımla/abone ol modeliyle bir mesajlaşma sistemini destekler.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-106">It also supports a messaging system with a publish/subscribe model.</span></span> <span data-ttu-id="ff7b6-107">SignalR redin backdüzlemi, iletileri diğer sunuculara iletmek için pub/Sub özelliğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-107">The SignalR Redis backplane uses the pub/sub feature to forward messages to other servers.</span></span>

![](scaleout-with-redis/_static/image1.png)

<span data-ttu-id="ff7b6-108">Bu öğretici için üç sunucu kullanacaksınız:</span><span class="sxs-lookup"><span data-stu-id="ff7b6-108">For this tutorial, you will use three servers:</span></span>

- <span data-ttu-id="ff7b6-109">Bir SignalR uygulamasını dağıtmak için kullanacağınız Windows çalıştıran iki sunucu.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-109">Two servers running Windows, which you will use to deploy a SignalR application.</span></span>
- <span data-ttu-id="ff7b6-110">Redo 'u çalıştırmak için kullanacağınız Linux çalıştıran bir sunucu.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-110">One server running Linux, which you will use to run Redis.</span></span> <span data-ttu-id="ff7b6-111">Bu öğreticideki ekran görüntüleri için Ubuntu 12,04 TLS kullandım.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-111">For the screenshots in this tutorial, I used Ubuntu 12.04 TLS.</span></span>

<span data-ttu-id="ff7b6-112">Kullanabileceğiniz üç fiziksel sunucunuz yoksa, Hyper-V ' d e sanal makineler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-112">If you don't have three physical servers to use, you can create VMs on Hyper-V.</span></span> <span data-ttu-id="ff7b6-113">Diğer bir seçenek de Azure 'da VM oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-113">Another option is to create VMs on Azure.</span></span>

<span data-ttu-id="ff7b6-114">Bu öğretici resmi redin uygulamasını kullanmasına karşın, MSOpenTech ' [ın bir Windows bağlantı noktası](https://github.com/MSOpenTech/redis) da vardır.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-114">Although this tutorial uses the official Redis implementation, there is also a [Windows port of Redis](https://github.com/MSOpenTech/redis) from MSOpenTech.</span></span> <span data-ttu-id="ff7b6-115">Kurulum ve yapılandırma farklıdır, ancak başka bir adım aynı şekilde yapılır.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-115">Setup and configuration are different, but otherwise the steps are the same.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="ff7b6-116">Redsıs ile SignalR ölçeği, Redsıs kümelerini desteklemez.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-116">SignalR scaleout with Redis does not support Redis clusters.</span></span>

## <a name="overview"></a><span data-ttu-id="ff7b6-117">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="ff7b6-117">Overview</span></span>

<span data-ttu-id="ff7b6-118">Ayrıntılı öğreticiye girmeden önce, ne yapabileceğinize ilişkin hızlı bir genel bakış sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-118">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="ff7b6-119">Redsıs 'i yükleyip Redsıs sunucusunu başlatın.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-119">Install Redis and start the Redis server.</span></span>
2. <span data-ttu-id="ff7b6-120">Bu NuGet paketlerini uygulamanıza ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ff7b6-120">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="ff7b6-121">Microsoft. AspNet. SignalR</span><span class="sxs-lookup"><span data-stu-id="ff7b6-121">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="ff7b6-122">Microsoft. AspNet. SignalR. Redsıs</span><span class="sxs-lookup"><span data-stu-id="ff7b6-122">Microsoft.AspNet.SignalR.Redis</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.Redis)
3. <span data-ttu-id="ff7b6-123">Bir SignalR uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-123">Create a SignalR application.</span></span>
4. <span data-ttu-id="ff7b6-124">Geri düzlemi yapılandırmak için aşağıdaki kodu Global. asax öğesine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ff7b6-124">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a><span data-ttu-id="ff7b6-125">Hyper-V üzerinde Ubuntu</span><span class="sxs-lookup"><span data-stu-id="ff7b6-125">Ubuntu on Hyper-V</span></span>

<span data-ttu-id="ff7b6-126">Windows Hyper-V ' d i kullanarak Windows Server 'da kolayca bir Ubuntu VM oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-126">Using Windows Hyper-V, you can easily create an Ubuntu VM on Windows Server.</span></span>

<span data-ttu-id="ff7b6-127">[http://www.ubuntu.com](http://www.ubuntu.com/)'Den Ubuntu ISO dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-127">Download the Ubuntu ISO from [http://www.ubuntu.com](http://www.ubuntu.com/).</span></span>

<span data-ttu-id="ff7b6-128">Hyper-V ' d a yeni bir VM ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-128">In Hyper-V, add a new VM.</span></span> <span data-ttu-id="ff7b6-129">**Sanal sabit diski bağla** adımında, **sanal sabit disk oluştur**' u seçin.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-129">In the **Connect Virtual Hard Disk** step, select **Create a virtual hard disk**.</span></span>

![](scaleout-with-redis/_static/image2.png)

<span data-ttu-id="ff7b6-130">**Yükleme seçenekleri** adımında, **görüntü dosyası (. iso)** seçeneğini belirleyin, **Araştır**' a tıklayın ve Ubuntu yükleme ISO dosyasına gidin.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-130">In the **Installation Options** step, select **Image file (.iso)**, click **Browse**, and browse to the Ubuntu installation ISO.</span></span>

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a><span data-ttu-id="ff7b6-131">Redsıs 'yi Install</span><span class="sxs-lookup"><span data-stu-id="ff7b6-131">Install Redis</span></span>

<span data-ttu-id="ff7b6-132">Redsıs 'yi indirmek ve derlemek için [http://redis.io/download](http://redis.io/download) bölümündeki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-132">Follow the steps at [http://redis.io/download](http://redis.io/download) to download and build Redis.</span></span>

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

<span data-ttu-id="ff7b6-133">Bu, `src` dizininde Redsıs ikililerini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-133">This builds the Redis binaries in the `src` directory.</span></span>

<span data-ttu-id="ff7b6-134">Varsayılan olarak redin parola gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-134">By default, Redis does not require a password.</span></span> <span data-ttu-id="ff7b6-135">Bir parola ayarlamak için, kaynak kodun kök dizininde bulunan `redis.conf` dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-135">To set a password, edit the `redis.conf` file, which is located in the root directory of the source code.</span></span> <span data-ttu-id="ff7b6-136">(Düzenlemeden önce dosyanın yedek kopyasını oluşturun!) `redis.conf`için aşağıdaki yönergeyi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ff7b6-136">(Make a backup copy of the file before you edit it!) Add the following directive to `redis.conf`:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

<span data-ttu-id="ff7b6-137">Şimdi Redsıs sunucusunu başlatın:</span><span class="sxs-lookup"><span data-stu-id="ff7b6-137">Now start the Redis server:</span></span>

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

<span data-ttu-id="ff7b6-138">Redin dinlediği varsayılan bağlantı noktası olan 6379 numaralı bağlantı noktasını açın.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-138">Open port 6379, which is the default port that Redis listens on.</span></span> <span data-ttu-id="ff7b6-139">(Yapılandırma dosyasındaki bağlantı noktası numarasını değiştirebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="ff7b6-139">(You can change the port number in the configuration file.)</span></span>

## <a name="create-the-signalr-application"></a><span data-ttu-id="ff7b6-140">SignalR uygulamasını oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff7b6-140">Create the SignalR Application</span></span>

<span data-ttu-id="ff7b6-141">Bu öğreticilerden birini izleyerek bir SignalR uygulaması oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ff7b6-141">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="ff7b6-142">SignalR ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ff7b6-142">Getting Started with SignalR</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="ff7b6-143">SignalR ve MVC 4 ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ff7b6-143">Getting Started with SignalR and MVC 4</span></span>](tutorial-getting-started-with-signalr-and-mvc-4.md)

<span data-ttu-id="ff7b6-144">Daha sonra, sohbet uygulamasını Redsıs ile ölçeği destekleyecek şekilde değiştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-144">Next, we'll modify the chat application to support scaleout with Redis.</span></span> <span data-ttu-id="ff7b6-145">İlk olarak, projenize SignalR. Redsıs NuGet paketini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-145">First, add the SignalR.Redis NuGet package to your project.</span></span> <span data-ttu-id="ff7b6-146">Visual Studio 'da, **Araçlar** menüsünden **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-146">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="ff7b6-147">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="ff7b6-147">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

<span data-ttu-id="ff7b6-148">Ardından, Global. asax dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-148">Next, open the Global.asax file.</span></span> <span data-ttu-id="ff7b6-149">Aşağıdaki kodu **uygulama\_başlangıç** yöntemine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ff7b6-149">Add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- <span data-ttu-id="ff7b6-150">"sunucu" Reddir çalıştıran sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-150">"server" is the name of the server that is running Redis.</span></span>
- <span data-ttu-id="ff7b6-151">*bağlantı* noktası numarası bağlantı noktasıdır</span><span class="sxs-lookup"><span data-stu-id="ff7b6-151">*port* is the port number</span></span>
- <span data-ttu-id="ff7b6-152">"Password" redsıs. conf dosyasında tanımladığınız paroladır.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-152">"password" is the password that you defined in the redis.conf file.</span></span>
- <span data-ttu-id="ff7b6-153">"AppName" herhangi bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-153">"AppName" is any string.</span></span> <span data-ttu-id="ff7b6-154">SignalR, bu adla bir Redsıs pub/Sub kanalı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-154">SignalR creates a Redis pub/sub channel with this name.</span></span>

<span data-ttu-id="ff7b6-155">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ff7b6-155">For example:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="ff7b6-156">Uygulamayı dağıtma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="ff7b6-156">Deploy and Run the Application</span></span>

<span data-ttu-id="ff7b6-157">SignalR uygulamasını dağıtmak için Windows Server örneklerinizi hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-157">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="ff7b6-158">IIS rolünü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-158">Add the IIS role.</span></span> <span data-ttu-id="ff7b6-159">WebSocket protokolü de dahil olmak üzere "uygulama geliştirme" özellikleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-159">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-redis/_static/image5.png)

<span data-ttu-id="ff7b6-160">Ayrıca yönetim hizmetini de ("Yönetim Araçları" altında listelenmiştir) içerir.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-160">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-redis/_static/image6.png)

<span data-ttu-id="ff7b6-161">**Web Dağıtımı 3,0 ' ü yükler.**</span><span class="sxs-lookup"><span data-stu-id="ff7b6-161">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="ff7b6-162">IIS Yöneticisi 'Ni çalıştırdığınızda, Microsoft Web platformu yüklemenizi ister veya [yükleyiciyi indirebilirsiniz](https://go.microsoft.com/fwlink/?LinkId=255386).</span><span class="sxs-lookup"><span data-stu-id="ff7b6-162">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="ff7b6-163">Platform yükleyicisinde Web Dağıtımı arayın ve Web Dağıtımı 3,0 ' i yükleme</span><span class="sxs-lookup"><span data-stu-id="ff7b6-163">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-redis/_static/image7.png)

<span data-ttu-id="ff7b6-164">Web yönetimi hizmetinin çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-164">Check that the Web Management Service is running.</span></span> <span data-ttu-id="ff7b6-165">Aksi takdirde, hizmeti başlatın.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-165">If not, start the service.</span></span> <span data-ttu-id="ff7b6-166">(Windows hizmetleri listesinde Web yönetimi hizmetini görmüyorsanız, IIS rolünü eklediğinizde Yönetim hizmetini yüklediğinizden emin olun.)</span><span class="sxs-lookup"><span data-stu-id="ff7b6-166">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="ff7b6-167">Varsayılan olarak, Web yönetimi hizmeti TCP bağlantı noktası 8172 ' i dinler.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-167">By default, the Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="ff7b6-168">Windows Güvenlik Duvarı 'nda 8172 numaralı bağlantı noktasında TCP trafiğine izin vermek için yeni bir gelen kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-168">In Windows Firewall, create a new inbound rule to allow TCP traffic on port 8172.</span></span> <span data-ttu-id="ff7b6-169">Daha fazla bilgi için bkz. [güvenlik duvarı kurallarını yapılandırma](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span><span class="sxs-lookup"><span data-stu-id="ff7b6-169">For more information, see [Configuring Firewall Rules](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="ff7b6-170">(VM 'Leri Azure 'da barındırıyorsanız, bunu doğrudan Azure portal yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-170">(If you are hosting the VMs on Azure, you can do this directly in the Azure portal.</span></span> <span data-ttu-id="ff7b6-171">Bkz. [sanal makineye uç noktaları ayarlama](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span><span class="sxs-lookup"><span data-stu-id="ff7b6-171">See [How to Set Up Endpoints to a Virtual Machine](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span></span>

<span data-ttu-id="ff7b6-172">Artık Visual Studio projesini geliştirme makinenizden sunucuya dağıtmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-172">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="ff7b6-173">Çözüm Gezgini, çözüme sağ tıklayın ve **Yayımla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-173">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="ff7b6-174">Web dağıtımı hakkında daha ayrıntılı belgeler için bkz. [Visual Studio Için Web dağıtımı Içerik Haritası ve ASP.net](../../../whitepapers/aspnet-web-deployment-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="ff7b6-174">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="ff7b6-175">Uygulamayı iki sunucuya dağıtırsanız, her bir örneği ayrı bir tarayıcı penceresinde açabilir ve bunların her birinin birinden SignalR iletileri aldıklarından emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-175">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="ff7b6-176">(Kuşkusuz, bir üretim ortamında, iki sunucu bir yük dengeleyicinin arkasına ait olacaktır.)</span><span class="sxs-lookup"><span data-stu-id="ff7b6-176">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-redis/_static/image8.png)

<span data-ttu-id="ff7b6-177">Redsıs 'e gönderilen iletileri görmeyi merak ediyorsanız redsıs ile yüklenen **redsıs-CLI** istemcisini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff7b6-177">If you're curious to see the messages that are sent to Redis, you can use the **redis-cli** client, which installs with Redis.</span></span>

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
