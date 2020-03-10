---
uid: signalr/overview/performance/scaleout-with-redis
title: Redsıs ile SignalR ölçeği Microsoft Docs
author: bradygaster
description: Bu konuda kullanılan yazılım sürümleri, .NET 4,5 SignalR sürüm 2 ' nin önceki sürümleri hakkında bilgi Için bu konunun önceki sürümlerini Visual Studio 2013...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 6ecd08c1-e364-4cd7-ad4c-806521911585
msc.legacyurl: /signalr/overview/performance/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 58a7affa1769523955adc76455a1c33be6f49751
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579228"
---
# <a name="signalr-scaleout-with-redis"></a><span data-ttu-id="2b8e2-103">Redis ile SignalR Ölçeğini Genişletme</span><span class="sxs-lookup"><span data-stu-id="2b8e2-103">SignalR Scaleout with Redis</span></span>

<span data-ttu-id="2b8e2-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2b8e2-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="2b8e2-105">Bu konuda kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="2b8e2-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="2b8e2-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="2b8e2-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="2b8e2-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="2b8e2-107">.NET 4.5</span></span>
> - <span data-ttu-id="2b8e2-108">SignalR sürüm 2,4</span><span class="sxs-lookup"><span data-stu-id="2b8e2-108">SignalR version 2.4</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="2b8e2-109">Bu konunun önceki sürümleri</span><span class="sxs-lookup"><span data-stu-id="2b8e2-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="2b8e2-110">SignalR 'nin önceki sürümleri hakkında daha fazla bilgi için bkz. [SignalR daha eski sürümleri](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="2b8e2-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="2b8e2-111">Sorular ve açıklamalar</span><span class="sxs-lookup"><span data-stu-id="2b8e2-111">Questions and comments</span></span>
>
> <span data-ttu-id="2b8e2-112">Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="2b8e2-113">Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="2b8e2-114">Bu öğreticide, iki ayrı IIS örneğine dağıtılan bir SignalR uygulamasına ileti dağıtmak için [redsıs](http://redis.io/) ' i kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-114">In this tutorial, you will use [Redis](http://redis.io/) to distribute messages across a SignalR application that is deployed on two separate IIS instances.</span></span>

<span data-ttu-id="2b8e2-115">Redsıs, bellek içi anahtar-değer deposudur.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-115">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="2b8e2-116">Ayrıca, Yayımla/abone ol modeliyle bir mesajlaşma sistemini destekler.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-116">It also supports a messaging system with a publish/subscribe model.</span></span> <span data-ttu-id="2b8e2-117">SignalR redin backdüzlemi, iletileri diğer sunuculara iletmek için pub/Sub özelliğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-117">The SignalR Redis backplane uses the pub/sub feature to forward messages to other servers.</span></span>

![](scaleout-with-redis/_static/image1.png)

<span data-ttu-id="2b8e2-118">Bu öğretici için üç sunucu kullanacaksınız:</span><span class="sxs-lookup"><span data-stu-id="2b8e2-118">For this tutorial, you will use three servers:</span></span>

- <span data-ttu-id="2b8e2-119">Bir SignalR uygulamasını dağıtmak için kullanacağınız Windows çalıştıran iki sunucu.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-119">Two servers running Windows, which you will use to deploy a SignalR application.</span></span>
- <span data-ttu-id="2b8e2-120">Redo 'u çalıştırmak için kullanacağınız Linux çalıştıran bir sunucu.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-120">One server running Linux, which you will use to run Redis.</span></span> <span data-ttu-id="2b8e2-121">Bu öğreticideki ekran görüntüleri için Ubuntu 12,04 TLS kullandım.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-121">For the screenshots in this tutorial, I used Ubuntu 12.04 TLS.</span></span>

<span data-ttu-id="2b8e2-122">Kullanabileceğiniz üç fiziksel sunucunuz yoksa, Hyper-V ' d e sanal makineler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-122">If you don't have three physical servers to use, you can create VMs on Hyper-V.</span></span> <span data-ttu-id="2b8e2-123">Diğer bir seçenek de Azure 'da VM oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-123">Another option is to create VMs on Azure.</span></span>

<span data-ttu-id="2b8e2-124">Bu öğretici resmi redin uygulamasını kullanmasına karşın, MSOpenTech ' [ın bir Windows bağlantı noktası](https://github.com/MSOpenTech/redis) da vardır.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-124">Although this tutorial uses the official Redis implementation, there is also a [Windows port of Redis](https://github.com/MSOpenTech/redis) from MSOpenTech.</span></span> <span data-ttu-id="2b8e2-125">Kurulum ve yapılandırma farklıdır, ancak başka bir adım aynı şekilde yapılır.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-125">Setup and configuration are different, but otherwise the steps are the same.</span></span>

> [!NOTE]
>
> <span data-ttu-id="2b8e2-126">Redsıs ile SignalR ölçeği, Redsıs kümelerini desteklemez.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-126">SignalR scaleout with Redis does not support Redis clusters.</span></span>

## <a name="overview"></a><span data-ttu-id="2b8e2-127">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="2b8e2-127">Overview</span></span>

<span data-ttu-id="2b8e2-128">Ayrıntılı öğreticiye girmeden önce, ne yapabileceğinize ilişkin hızlı bir genel bakış sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-128">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="2b8e2-129">Redsıs 'i yükleyip Redsıs sunucusunu başlatın.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-129">Install Redis and start the Redis server.</span></span>
2. <span data-ttu-id="2b8e2-130">Bu NuGet paketlerini uygulamanıza ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2b8e2-130">Add these NuGet packages to your application:</span></span>

    - [<span data-ttu-id="2b8e2-131">Microsoft. AspNet. SignalR</span><span class="sxs-lookup"><span data-stu-id="2b8e2-131">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="2b8e2-132">Microsoft. AspNet. SignalR. StackExchangeRedis</span><span class="sxs-lookup"><span data-stu-id="2b8e2-132">Microsoft.AspNet.SignalR.StackExchangeRedis</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.StackExchangeRedis)
    
3. <span data-ttu-id="2b8e2-133">Bir SignalR uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-133">Create a SignalR application.</span></span>
4. <span data-ttu-id="2b8e2-134">Geri düzlemi yapılandırmak için Startup.cs 'e aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2b8e2-134">Add the following code to Startup.cs to configure the backplane:</span></span>

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a><span data-ttu-id="2b8e2-135">Hyper-V üzerinde Ubuntu</span><span class="sxs-lookup"><span data-stu-id="2b8e2-135">Ubuntu on Hyper-V</span></span>

<span data-ttu-id="2b8e2-136">Windows Hyper-V ' d i kullanarak Windows Server 'da kolayca bir Ubuntu VM oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-136">Using Windows Hyper-V, you can easily create an Ubuntu VM on Windows Server.</span></span>

<span data-ttu-id="2b8e2-137">[http://www.ubuntu.com](http://www.ubuntu.com/)'Den Ubuntu ISO dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-137">Download the Ubuntu ISO from [http://www.ubuntu.com](http://www.ubuntu.com/).</span></span>

<span data-ttu-id="2b8e2-138">Hyper-V ' d a yeni bir VM ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-138">In Hyper-V, add a new VM.</span></span> <span data-ttu-id="2b8e2-139">**Sanal sabit diski bağla** adımında, **sanal sabit disk oluştur**' u seçin.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-139">In the **Connect Virtual Hard Disk** step, select **Create a virtual hard disk**.</span></span>

![](scaleout-with-redis/_static/image2.png)

<span data-ttu-id="2b8e2-140">**Yükleme seçenekleri** adımında, **görüntü dosyası (. iso)** seçeneğini belirleyin, **Araştır**' a tıklayın ve Ubuntu yükleme ISO dosyasına gidin.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-140">In the **Installation Options** step, select **Image file (.iso)**, click **Browse**, and browse to the Ubuntu installation ISO.</span></span>

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a><span data-ttu-id="2b8e2-141">Redsıs 'yi Install</span><span class="sxs-lookup"><span data-stu-id="2b8e2-141">Install Redis</span></span>

<span data-ttu-id="2b8e2-142">Redsıs 'yi indirmek ve derlemek için [http://redis.io/download](http://redis.io/download) bölümündeki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-142">Follow the steps at [http://redis.io/download](http://redis.io/download) to download and build Redis.</span></span>

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

<span data-ttu-id="2b8e2-143">Bu, `src` dizininde Redsıs ikililerini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-143">This builds the Redis binaries in the `src` directory.</span></span>

<span data-ttu-id="2b8e2-144">Varsayılan olarak redin parola gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-144">By default, Redis does not require a password.</span></span> <span data-ttu-id="2b8e2-145">Bir parola ayarlamak için, kaynak kodun kök dizininde bulunan `redis.conf` dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-145">To set a password, edit the `redis.conf` file, which is located in the root directory of the source code.</span></span> <span data-ttu-id="2b8e2-146">(Düzenlemeden önce dosyanın yedek kopyasını oluşturun!) `redis.conf`için aşağıdaki yönergeyi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2b8e2-146">(Make a backup copy of the file before you edit it!) Add the following directive to `redis.conf`:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

<span data-ttu-id="2b8e2-147">Şimdi Redsıs sunucusunu başlatın:</span><span class="sxs-lookup"><span data-stu-id="2b8e2-147">Now start the Redis server:</span></span>

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

<span data-ttu-id="2b8e2-148">Redin dinlediği varsayılan bağlantı noktası olan 6379 numaralı bağlantı noktasını açın.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-148">Open port 6379, which is the default port that Redis listens on.</span></span> <span data-ttu-id="2b8e2-149">(Yapılandırma dosyasındaki bağlantı noktası numarasını değiştirebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="2b8e2-149">(You can change the port number in the configuration file.)</span></span>

## <a name="create-the-signalr-application"></a><span data-ttu-id="2b8e2-150">SignalR uygulamasını oluşturma</span><span class="sxs-lookup"><span data-stu-id="2b8e2-150">Create the SignalR Application</span></span>

<span data-ttu-id="2b8e2-151">Bu öğreticilerden birini izleyerek bir SignalR uygulaması oluşturun:</span><span class="sxs-lookup"><span data-stu-id="2b8e2-151">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="2b8e2-152">SignalR 2,0 ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="2b8e2-152">Getting Started with SignalR 2.0</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="2b8e2-153">SignalR 2,0 ve MVC 5 ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="2b8e2-153">Getting Started with SignalR 2.0 and MVC 5</span></span>](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

<span data-ttu-id="2b8e2-154">Daha sonra, sohbet uygulamasını Redsıs ile ölçeği destekleyecek şekilde değiştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-154">Next, we'll modify the chat application to support scaleout with Redis.</span></span> <span data-ttu-id="2b8e2-155">İlk olarak, `Microsoft.AspNet.SignalR.StackExchangeRedis` NuGet paketini projenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-155">First, add the `Microsoft.AspNet.SignalR.StackExchangeRedis` NuGet package to your project.</span></span> <span data-ttu-id="2b8e2-156">Visual Studio 'da, **Araçlar** menüsünden **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-156">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="2b8e2-157">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="2b8e2-157">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

<span data-ttu-id="2b8e2-158">Sonra, Startup.cs dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-158">Next, open the Startup.cs file.</span></span> <span data-ttu-id="2b8e2-159">**Yapılandırma** yöntemine aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2b8e2-159">Add the following code to the **Configuration** method:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- <span data-ttu-id="2b8e2-160">"sunucu" Reddir çalıştıran sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-160">"server" is the name of the server that is running Redis.</span></span>
- <span data-ttu-id="2b8e2-161">*bağlantı* noktası numarası bağlantı noktasıdır</span><span class="sxs-lookup"><span data-stu-id="2b8e2-161">*port* is the port number</span></span>
- <span data-ttu-id="2b8e2-162">"Password" redsıs. conf dosyasında tanımladığınız paroladır.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-162">"password" is the password that you defined in the redis.conf file.</span></span>
- <span data-ttu-id="2b8e2-163">"AppName" herhangi bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-163">"AppName" is any string.</span></span> <span data-ttu-id="2b8e2-164">SignalR, bu adla bir Redsıs pub/Sub kanalı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-164">SignalR creates a Redis pub/sub channel with this name.</span></span>

<span data-ttu-id="2b8e2-165">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="2b8e2-165">For example:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="2b8e2-166">Uygulamayı dağıtma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="2b8e2-166">Deploy and Run the Application</span></span>

<span data-ttu-id="2b8e2-167">SignalR uygulamasını dağıtmak için Windows Server örneklerinizi hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-167">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="2b8e2-168">IIS rolünü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-168">Add the IIS role.</span></span> <span data-ttu-id="2b8e2-169">WebSocket protokolü de dahil olmak üzere "uygulama geliştirme" özellikleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-169">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-redis/_static/image5.png)

<span data-ttu-id="2b8e2-170">Ayrıca yönetim hizmetini de ("Yönetim Araçları" altında listelenmiştir) içerir.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-170">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-redis/_static/image6.png)

<span data-ttu-id="2b8e2-171">**Web Dağıtımı 3,0 ' ü yükler.**</span><span class="sxs-lookup"><span data-stu-id="2b8e2-171">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="2b8e2-172">IIS Yöneticisi 'Ni çalıştırdığınızda, Microsoft Web platformu yüklemenizi ister veya [yükleyiciyi indirebilirsiniz](https://go.microsoft.com/fwlink/?LinkId=255386).</span><span class="sxs-lookup"><span data-stu-id="2b8e2-172">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="2b8e2-173">Platform yükleyicisinde Web Dağıtımı arayın ve Web Dağıtımı 3,0 ' i yükleme</span><span class="sxs-lookup"><span data-stu-id="2b8e2-173">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-redis/_static/image7.png)

<span data-ttu-id="2b8e2-174">Web yönetimi hizmetinin çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-174">Check that the Web Management Service is running.</span></span> <span data-ttu-id="2b8e2-175">Aksi takdirde, hizmeti başlatın.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-175">If not, start the service.</span></span> <span data-ttu-id="2b8e2-176">(Windows hizmetleri listesinde Web yönetimi hizmetini görmüyorsanız, IIS rolünü eklediğinizde Yönetim hizmetini yüklediğinizden emin olun.)</span><span class="sxs-lookup"><span data-stu-id="2b8e2-176">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="2b8e2-177">Varsayılan olarak, Web yönetimi hizmeti TCP bağlantı noktası 8172 ' i dinler.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-177">By default, the Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="2b8e2-178">Windows Güvenlik Duvarı 'nda 8172 numaralı bağlantı noktasında TCP trafiğine izin vermek için yeni bir gelen kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-178">In Windows Firewall, create a new inbound rule to allow TCP traffic on port 8172.</span></span> <span data-ttu-id="2b8e2-179">Daha fazla bilgi için bkz. [güvenlik duvarı kurallarını yapılandırma](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span><span class="sxs-lookup"><span data-stu-id="2b8e2-179">For more information, see [Configuring Firewall Rules](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="2b8e2-180">(VM 'Leri Azure 'da barındırıyorsanız, bunu doğrudan Azure portal yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-180">(If you are hosting the VMs on Azure, you can do this directly in the Azure portal.</span></span> <span data-ttu-id="2b8e2-181">Bkz. [sanal makineye uç noktaları ayarlama](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span><span class="sxs-lookup"><span data-stu-id="2b8e2-181">See [How to Set Up Endpoints to a Virtual Machine](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span></span>

<span data-ttu-id="2b8e2-182">Artık Visual Studio projesini geliştirme makinenizden sunucuya dağıtmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-182">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="2b8e2-183">Çözüm Gezgini, çözüme sağ tıklayın ve **Yayımla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-183">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="2b8e2-184">Web dağıtımı hakkında daha ayrıntılı belgeler için bkz. [Visual Studio Için Web dağıtımı Içerik Haritası ve ASP.net](../../../whitepapers/aspnet-web-deployment-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="2b8e2-184">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="2b8e2-185">Uygulamayı iki sunucuya dağıtırsanız, her bir örneği ayrı bir tarayıcı penceresinde açabilir ve bunların her birinin birinden SignalR iletileri aldıklarından emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-185">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="2b8e2-186">(Kuşkusuz, bir üretim ortamında, iki sunucu bir yük dengeleyicinin arkasına ait olacaktır.)</span><span class="sxs-lookup"><span data-stu-id="2b8e2-186">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-redis/_static/image8.png)

<span data-ttu-id="2b8e2-187">Redsıs 'e gönderilen iletileri görmeyi merak ediyorsanız redsıs ile yüklenen **redsıs-CLI** istemcisini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b8e2-187">If you're curious to see the messages that are sent to Redis, you can use the **redis-cli** client, which installs with Redis.</span></span>

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
