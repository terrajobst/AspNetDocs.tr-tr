---
uid: web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
title: Azure çalışan rolünde Host ASP.NET Web API 2-ASP.NET 4. x
author: MikeWasson
description: "Öğretici: Web API çerçevesini Self barındırmak için OWıN kullanarak bir Azure çalışan rolünde ASP.NET Web API 'SI barındırın."
ms.author: riande
ms.date: 04/02/2014
ms.custom: seoapril2019
ms.assetid: 6980ee2e-d6b0-4a08-8fb6-ab96362dd0e3
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: ec9904e0bff090be0f504036ae73977cfca0cb31
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556632"
---
# <a name="host-aspnet-web-api-2-in-an-azure-worker-role"></a><span data-ttu-id="af59f-103">Azure çalışan rolünde Host ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="af59f-103">Host ASP.NET Web API 2 in an Azure Worker Role</span></span>

<span data-ttu-id="af59f-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="af59f-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="af59f-105">Bu öğreticide, Web API çerçevesini Self barındırmak için OWIN kullanılarak Azure çalışan rolünde ASP.NET Web API 'sinin nasıl barındıralınacağını gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="af59f-105">This tutorial shows how to host ASP.NET Web API in an Azure Worker Role, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="af59f-106">[.Net Için açık Web arabirimi](http://owin.org/) (owın), .NET Web sunucuları ile Web uygulamaları arasında bir soyutlama tanımlar.</span><span class="sxs-lookup"><span data-stu-id="af59f-106">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="af59f-107">OWIN, Web uygulamasını sunucudan ayırır, bu da bir Web uygulamasını kendi işleminizde, IIS dışında (örneğin, bir Azure çalışan rolü içinde) kendine barındırmak için ideal hale getirir.</span><span class="sxs-lookup"><span data-stu-id="af59f-107">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS–for example, inside an Azure worker role.</span></span>
>
> <span data-ttu-id="af59f-108">Bu öğreticide, kendi kendini barındırmak için kullanılan bir HTTP sunucusu sağlayan Microsoft. Owin. Host. HttpListener paketini kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="af59f-108">In this tutorial, you'll use the Microsoft.Owin.Host.HttpListener package, which provides an HTTP server that be used to self-host OWIN applications.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="af59f-109">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="af59f-109">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="af59f-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="af59f-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="af59f-111">Web API 2</span><span class="sxs-lookup"><span data-stu-id="af59f-111">Web API 2</span></span>
> - [<span data-ttu-id="af59f-112">.NET 2,3 için Azure SDK</span><span class="sxs-lookup"><span data-stu-id="af59f-112">Azure SDK for .NET 2.3</span></span>](https://azure.microsoft.com/downloads/)

## <a name="create-a-microsoft-azure-project"></a><span data-ttu-id="af59f-113">Microsoft Azure projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="af59f-113">Create a Microsoft Azure Project</span></span>

<span data-ttu-id="af59f-114">Visual Studio 'Yu yönetici ayrıcalıklarıyla başlatın.</span><span class="sxs-lookup"><span data-stu-id="af59f-114">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="af59f-115">Azure işlem öykünücüsü kullanılarak uygulamanın yerel olarak hata ayıklaması için yönetici ayrıcalıkları gerekir.</span><span class="sxs-lookup"><span data-stu-id="af59f-115">Administrator privileges are needed to debug the application locally, using the Azure compute emulator.</span></span>

<span data-ttu-id="af59f-116">**Dosya** menüsünde **Yeni**' ye ve ardından **Proje**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="af59f-116">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="af59f-117">**Yüklü şablonlardan**, Visual C#altında **bulut** ' a ve ardından **Windows Azure bulut hizmeti**' ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="af59f-117">From **Installed Templates**, under Visual C#, click **Cloud** and then click **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="af59f-118">Projeyi "AzureApp" olarak adlandırın ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="af59f-118">Name the project "AzureApp" and click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image2.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image1.png)

<span data-ttu-id="af59f-119">**Yeni Windows Azure bulut hizmeti** Iletişim kutusunda **çalışan rolü**' ne çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="af59f-119">In the **New Windows Azure Cloud Service** dialog, double-click **Worker Role**.</span></span> <span data-ttu-id="af59f-120">Varsayılan adı bırakın ("WorkerRole1").</span><span class="sxs-lookup"><span data-stu-id="af59f-120">Leave the default name ("WorkerRole1").</span></span> <span data-ttu-id="af59f-121">Bu adım çözüme bir çalışan rolü ekler.</span><span class="sxs-lookup"><span data-stu-id="af59f-121">This step adds a worker role to the solution.</span></span> <span data-ttu-id="af59f-122">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="af59f-122">Click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image4.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image3.png)

<span data-ttu-id="af59f-123">Oluşturulan Visual Studio çözümü iki proje içerir:</span><span class="sxs-lookup"><span data-stu-id="af59f-123">The Visual Studio solution that is created contains two projects:</span></span>

- <span data-ttu-id="af59f-124">&quot;AzureApp&quot;, Azure uygulamasının rollerini ve yapılandırmasını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="af59f-124">&quot;AzureApp&quot; defines the roles and configuration for the Azure application.</span></span>
- <span data-ttu-id="af59f-125">&quot;WorkerRole1&quot;, çalışan rolü için kodu içerir.</span><span class="sxs-lookup"><span data-stu-id="af59f-125">&quot;WorkerRole1&quot; contains the code for the worker role.</span></span>

<span data-ttu-id="af59f-126">Genel olarak, bir Azure uygulaması birden çok rol içerebilir, ancak bu öğretici tek bir rol kullanıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="af59f-126">In general, an Azure application can contain multiple roles, although this tutorial uses a single role.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="af59f-127">Web API 'sini ve OWIN paketlerini ekleyin</span><span class="sxs-lookup"><span data-stu-id="af59f-127">Add the Web API and OWIN Packages</span></span>

<span data-ttu-id="af59f-128">**Araçlar** menüsünde **NuGet Paket Yöneticisi**' ne ve ardından **Paket Yöneticisi konsolu**' na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="af59f-128">From the **Tools** menu, click **NuGet Package Manager**, then click **Package Manager Console**.</span></span>

<span data-ttu-id="af59f-129">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="af59f-129">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a><span data-ttu-id="af59f-130">HTTP uç noktası ekleme</span><span class="sxs-lookup"><span data-stu-id="af59f-130">Add an HTTP Endpoint</span></span>

<span data-ttu-id="af59f-131">Çözüm Gezgini ' de, AzureApp projesini genişletin.</span><span class="sxs-lookup"><span data-stu-id="af59f-131">In Solution Explorer, expand the AzureApp project.</span></span> <span data-ttu-id="af59f-132">Roller düğümünü genişletin, WorkerRole1 öğesine sağ tıklayın ve **Özellikler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="af59f-132">Expand the Roles node, right-click WorkerRole1, and select **Properties**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image6.png)

<span data-ttu-id="af59f-133">**Uç noktalar**' a ve ardından **uç nokta Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="af59f-133">Click **Endpoints**, and then click **Add Endpoint**.</span></span>

<span data-ttu-id="af59f-134">**Protokol** açılan listesinde "http" öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="af59f-134">In the **Protocol** dropdown list, select "http".</span></span> <span data-ttu-id="af59f-135">**Genel bağlantı noktası** ve **özel bağlantı noktası**alanına 80 yazın.</span><span class="sxs-lookup"><span data-stu-id="af59f-135">In **Public Port** and **Private Port**, type 80.</span></span> <span data-ttu-id="af59f-136">Bu bağlantı noktası numaraları farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="af59f-136">These port numbers can be different.</span></span> <span data-ttu-id="af59f-137">Genel bağlantı noktası, istemcilerin role bir istek gönderdiklerinde kullandıkları şeydir.</span><span class="sxs-lookup"><span data-stu-id="af59f-137">The public port is what clients use when they send a request to the role.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image8.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image7.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="af59f-138">Self-Host için Web API 'YI yapılandırma</span><span class="sxs-lookup"><span data-stu-id="af59f-138">Configure Web API for Self-Host</span></span>

<span data-ttu-id="af59f-139">Çözüm Gezgini ' de, WorkerRole1 projesine sağ tıklayın ve yeni bir sınıf eklemek için / **sınıfı** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="af59f-139">In Solution Explorer, right click the WorkerRole1 project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="af59f-140">`Startup`sınıfı adlandırın.</span><span class="sxs-lookup"><span data-stu-id="af59f-140">Name the class `Startup`.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image9.png)

<span data-ttu-id="af59f-141">Bu dosyadaki tüm ortak kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="af59f-141">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample2.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="af59f-142">Web API denetleyicisi ekleme</span><span class="sxs-lookup"><span data-stu-id="af59f-142">Add a Web API Controller</span></span>

<span data-ttu-id="af59f-143">Sonra, bir Web API denetleyici sınıfı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="af59f-143">Next, add a Web API controller class.</span></span> <span data-ttu-id="af59f-144">WorkerRole1 projesine sağ tıklayın ve / **sınıfı** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="af59f-144">Right-click the WorkerRole1 project and select **Add** / **Class**.</span></span> <span data-ttu-id="af59f-145">Test denetleyicisi sınıfını adlandırın.</span><span class="sxs-lookup"><span data-stu-id="af59f-145">Name the class TestController.</span></span> <span data-ttu-id="af59f-146">Bu dosyadaki tüm ortak kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="af59f-146">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample3.cs)]

<span data-ttu-id="af59f-147">Kolaylık olması için bu denetleyici yalnızca düz metin döndüren iki GET yöntemi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="af59f-147">For simplicity, this controller just defines two GET methods that return plain text.</span></span>

## <a name="start-the-owin-host"></a><span data-ttu-id="af59f-148">OWıN konağını başlatma</span><span class="sxs-lookup"><span data-stu-id="af59f-148">Start the OWIN Host</span></span>

<span data-ttu-id="af59f-149">WorkerRole.cs dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="af59f-149">Open the WorkerRole.cs file.</span></span> <span data-ttu-id="af59f-150">Bu sınıf, çalışan rolü başlatıldığında ve durdurulduğunda çalışan kodu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="af59f-150">This class defines the code that runs when the worker role is started and stopped.</span></span>

<span data-ttu-id="af59f-151">Şu deyimi kullanarak aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="af59f-151">Add the following using statement:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample4.cs)]

<span data-ttu-id="af59f-152">`WorkerRole` sınıfına bir **IDisposable** üyesi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="af59f-152">Add an **IDisposable** member to the `WorkerRole` class:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample5.cs)]

<span data-ttu-id="af59f-153">`OnStart` yönteminde, ana bilgisayarı başlatmak için aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="af59f-153">In the `OnStart` method, add the following code to start the host:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample6.cs?highlight=5)]

<span data-ttu-id="af59f-154">**WebApp. Start** yöntemi owın konağını başlatır.</span><span class="sxs-lookup"><span data-stu-id="af59f-154">The **WebApp.Start** method starts the OWIN host.</span></span> <span data-ttu-id="af59f-155">`Startup` sınıfının adı, yöntemin tür parametresidir.</span><span class="sxs-lookup"><span data-stu-id="af59f-155">The name of the `Startup` class is a type parameter to the method.</span></span> <span data-ttu-id="af59f-156">Kurala göre, ana bilgisayar bu sınıfın `Configure` yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="af59f-156">By convention, the host will call the `Configure` method of this class.</span></span>

<span data-ttu-id="af59f-157">*\_uygulama* örneğinin atılırken `OnStop` geçersiz kılın:</span><span class="sxs-lookup"><span data-stu-id="af59f-157">Override the `OnStop` to dispose of the *\_app* instance:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample7.cs)]

<span data-ttu-id="af59f-158">WorkerRole.cs için kodun tamamı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="af59f-158">Here is the complete code for WorkerRole.cs:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample8.cs)]

<span data-ttu-id="af59f-159">Çözümü oluşturun ve F5 tuşuna basarak uygulamayı Azure Işlem öykünücüsünde yerel olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="af59f-159">Build the solution, and press F5 to run the application locally in the Azure Compute Emulator.</span></span> <span data-ttu-id="af59f-160">Güvenlik duvarınızın ayarlarına bağlı olarak, güvenlik duvarınız aracılığıyla öykünücüye izin vermeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="af59f-160">Depending on your firewall settings, you might need to allow the emulator through your firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="af59f-161">Aşağıdakiler gibi bir özel durum alırsanız, geçici çözüm için lütfen [Bu blog gönderisine](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) bakın.</span><span class="sxs-lookup"><span data-stu-id="af59f-161">If you get an exception like the following, please see [this blog post](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) for a workaround.</span></span> <span data-ttu-id="af59f-162">"Dosya veya derleme ' Microsoft. Owin, Version = 2.0.2.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35 ' veya bağımlılıklarından biri yüklenemedi.</span><span class="sxs-lookup"><span data-stu-id="af59f-162">"Could not load file or assembly 'Microsoft.Owin, Version=2.0.2.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies.</span></span> <span data-ttu-id="af59f-163">Konumlandırılan derlemenin bildirim tanımı derleme başvurusuyla eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="af59f-163">The located assembly's manifest definition does not match the assembly reference.</span></span> <span data-ttu-id="af59f-164">(HRESULT özel durumu: 0x80131040) "</span><span class="sxs-lookup"><span data-stu-id="af59f-164">(Exception from HRESULT: 0x80131040)"</span></span>

<span data-ttu-id="af59f-165">İşlem öykünücüsü uç noktaya bir yerel IP adresi atar.</span><span class="sxs-lookup"><span data-stu-id="af59f-165">The compute emulator assigns a local IP address to the endpoint.</span></span> <span data-ttu-id="af59f-166">Işlem öykünücüsü Kullanıcı arabirimini görüntüleyerek IP adresini bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af59f-166">You can find the IP address by viewing the Compute Emulator UI.</span></span> <span data-ttu-id="af59f-167">Görev çubuğu bildirim alanında öykünücü simgesine sağ tıklayın ve **Işlem öykünücüsü Kullanıcı arabirimini göster**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="af59f-167">Right-click the emulator icon in the task bar notification area, and select **Show Compute Emulator UI**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image11.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image10.png)

<span data-ttu-id="af59f-168">Hizmet dağıtımları, dağıtım [kimlik], hizmet ayrıntıları altındaki IP adresini bulun.</span><span class="sxs-lookup"><span data-stu-id="af59f-168">Find the IP address under Service Deployments, deployment [id], Service Details.</span></span> <span data-ttu-id="af59f-169">Bir Web tarayıcısı açın ve http://<em>Address</em>/test/1 adresine gidin; burada <em>Adres</em> , Işlem öykünücüsü tarafından atanan IP adresidir; Örneğin, `http://127.0.0.1:80/test/1`.</span><span class="sxs-lookup"><span data-stu-id="af59f-169">Open a web browser and navigate to http://<em>address</em>/test/1, where <em>address</em> is the IP address assigned by the compute emulator; for example, `http://127.0.0.1:80/test/1`.</span></span> <span data-ttu-id="af59f-170">Web API denetleyicisinden yanıtı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="af59f-170">You should see the response from the Web API controller:</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image12.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="af59f-171">Azure’a dağıtma</span><span class="sxs-lookup"><span data-stu-id="af59f-171">Deploy to Azure</span></span>

<span data-ttu-id="af59f-172">Bu adım için bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="af59f-172">For this step, you must have an Azure account.</span></span> <span data-ttu-id="af59f-173">Henüz bir hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af59f-173">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="af59f-174">Ayrıntılar için bkz. [ücretsiz deneme Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="af59f-174">For details, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="af59f-175">Çözüm Gezgini, AzureApp projesine sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="af59f-175">In Solution Explorer, right-click the AzureApp project.</span></span> <span data-ttu-id="af59f-176">**Yayımla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="af59f-176">Select **Publish**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image13.png)

<span data-ttu-id="af59f-177">Azure hesabınızda oturum açmadıysanız **oturum aç**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="af59f-177">If you are not signed in to your Azure account, click **Sign In**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image15.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image14.png)

<span data-ttu-id="af59f-178">Oturum açtıktan sonra bir abonelik seçin ve **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="af59f-178">After you are signed in, choose a subscription and click **Next**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image17.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image16.png)

<span data-ttu-id="af59f-179">Bulut hizmeti için bir ad girin ve bir bölge seçin.</span><span class="sxs-lookup"><span data-stu-id="af59f-179">Enter a name for the cloud service and choose a region.</span></span> <span data-ttu-id="af59f-180">**Oluştur**'u tıklatın.</span><span class="sxs-lookup"><span data-stu-id="af59f-180">Click **Create**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image18.png)

<span data-ttu-id="af59f-181">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="af59f-181">Click **Publish**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image20.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image19.png)

<span data-ttu-id="af59f-182">Azure etkinlik günlüğü penceresinde dağıtım ilerleme durumu gösterilir.</span><span class="sxs-lookup"><span data-stu-id="af59f-182">The Azure Activity Log window shows the progress of the deployment.</span></span> <span data-ttu-id="af59f-183">Uygulama dağıtıldığında http://appname.cloudapp.net/test/1gidin.</span><span class="sxs-lookup"><span data-stu-id="af59f-183">When the app is deployed, browse to http://appname.cloudapp.net/test/1.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image21.png)

## <a name="additional-resources"></a><span data-ttu-id="af59f-184">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="af59f-184">Additional Resources</span></span>

- [<span data-ttu-id="af59f-185">Project Katana’ya Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="af59f-185">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)
- [<span data-ttu-id="af59f-186">GitHub üzerinde Katana proje</span><span class="sxs-lookup"><span data-stu-id="af59f-186">Katana Project on GitHub</span></span>](https://github.com/aspnet/AspNetKatana)
