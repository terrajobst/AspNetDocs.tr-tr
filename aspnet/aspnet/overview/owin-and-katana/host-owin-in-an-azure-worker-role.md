---
uid: aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
title: Azure çalışan rolünde ana bilgisayar | Microsoft Docs
author: MikeWasson
description: Bu öğreticide, Microsoft Azure çalışan rolünde nasıl bağımsız olarak OWIN barındırılacağını gösterilmektedir. .NET için açık Web arabirimi (OWıN), .NET Web sunucusu arasında bir soyutlama tanımlıyor...
ms.author: riande
ms.date: 04/11/2014
ms.assetid: 07aa855a-92ee-4d43-ba66-5bfd7de20ee6
msc.legacyurl: /aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: 59d2e0d549427093f8a2424b17af81169b78ef30
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584618"
---
# <a name="host-owin-in-an-azure-worker-role"></a><span data-ttu-id="8b4f6-104">Azure Çalışan Rolünde OWIN Barındırma</span><span class="sxs-lookup"><span data-stu-id="8b4f6-104">Host OWIN in an Azure Worker Role</span></span>

<span data-ttu-id="8b4f6-105">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="8b4f6-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="8b4f6-106">Bu öğreticide, Microsoft Azure çalışan rolünde nasıl bağımsız olarak OWIN barındırılacağını gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-106">This tutorial shows how to self-host OWIN in a Microsoft Azure worker role.</span></span>
>
> <span data-ttu-id="8b4f6-107">[.Net Için açık Web arabirimi](http://owin.org/) (owın), .NET Web sunucuları ile Web uygulamaları arasında bir soyutlama tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-107">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="8b4f6-108">OWIN, Web uygulamasını sunucudan ayırır, bu da bir Web uygulamasını kendi işleminizde, IIS dışında (örneğin, bir Azure çalışan rolü içinde) kendine barındırmak için ideal hale getirir.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-108">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS–for example, inside an Azure worker role.</span></span>
>
> <span data-ttu-id="8b4f6-109">Bu öğreticide, bir OWIN uygulamasını Microsoft Azure çalışan rolünde nasıl barındıralabileceğinizi öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-109">In this tutorial, you'll learn how to self-host an OWIN applications inside a Microsoft Azure worker role.</span></span> <span data-ttu-id="8b4f6-110">Çalışan rolleri hakkında daha fazla bilgi için bkz. [Azure yürütme modelleri](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices).</span><span class="sxs-lookup"><span data-stu-id="8b4f6-110">To learn more about worker roles, see [Azure Execution Models](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="8b4f6-111">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="8b4f6-111">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="8b4f6-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="8b4f6-112">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - [<span data-ttu-id="8b4f6-113">.NET 2,3 için Azure SDK</span><span class="sxs-lookup"><span data-stu-id="8b4f6-113">Azure SDK for .NET 2.3</span></span>](https://azure.microsoft.com/downloads/)
> - [<span data-ttu-id="8b4f6-114">Microsoft. Owin. Selfhost 2.1.0</span><span class="sxs-lookup"><span data-stu-id="8b4f6-114">Microsoft.Owin.Selfhost 2.1.0</span></span>](http://www.nuget.org/packages/Microsoft.Owin.SelfHost/2.1.0)

## <a name="create-a-microsoft-azure-project"></a><span data-ttu-id="8b4f6-115">Microsoft Azure projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="8b4f6-115">Create a Microsoft Azure Project</span></span>

<span data-ttu-id="8b4f6-116">Visual Studio 'Yu yönetici ayrıcalıklarıyla başlatın.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-116">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="8b4f6-117">Azure işlem öykünücüsü kullanılarak uygulamanın yerel olarak hata ayıklaması için yönetici ayrıcalıkları gerekir.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-117">Administrator privileges are needed to debug the application locally, using the Azure compute emulator.</span></span>

<span data-ttu-id="8b4f6-118">**Dosya** menüsünde **Yeni**' ye ve ardından **Proje**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-118">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="8b4f6-119">**Yüklü şablonlardan**, Visual C#altında **bulut** ' a ve ardından **Windows Azure bulut hizmeti**' ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-119">From **Installed Templates**, under Visual C#, click **Cloud** and then click **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="8b4f6-120">Projeyi "AzureApp" olarak adlandırın ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-120">Name the project "AzureApp" and click **OK**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image2.png)](host-owin-in-an-azure-worker-role/_static/image1.png)

<span data-ttu-id="8b4f6-121">**Yeni Windows Azure bulut hizmeti** Iletişim kutusunda **çalışan rolü**' ne çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-121">In the **New Windows Azure Cloud Service** dialog, double-click **Worker Role**.</span></span> <span data-ttu-id="8b4f6-122">Varsayılan adı bırakın ("WorkerRole1").</span><span class="sxs-lookup"><span data-stu-id="8b4f6-122">Leave the default name ("WorkerRole1").</span></span> <span data-ttu-id="8b4f6-123">Bu adım çözüme bir çalışan rolü ekler.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-123">This step adds a worker role to the solution.</span></span> <span data-ttu-id="8b4f6-124">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-124">Click **OK**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image4.png)](host-owin-in-an-azure-worker-role/_static/image3.png)

<span data-ttu-id="8b4f6-125">Oluşturulan Visual Studio çözümü iki proje içerir:</span><span class="sxs-lookup"><span data-stu-id="8b4f6-125">The Visual Studio solution that is created contains two projects:</span></span>

- <span data-ttu-id="8b4f6-126">&quot;AzureApp&quot;, Azure uygulamasının rollerini ve yapılandırmasını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-126">&quot;AzureApp&quot; defines the roles and configuration for the Azure application.</span></span>
- <span data-ttu-id="8b4f6-127">&quot;WorkerRole1&quot;, çalışan rolü için kodu içerir.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-127">&quot;WorkerRole1&quot; contains the code for the worker role.</span></span>

<span data-ttu-id="8b4f6-128">Genel olarak, bir Azure uygulaması birden çok rol içerebilir, ancak bu öğretici tek bir rol kullanıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-128">In general, an Azure application can contain multiple roles, although this tutorial uses a single role.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-owin-self-host-packages"></a><span data-ttu-id="8b4f6-129">OWıN Self-Host paketlerini ekleme</span><span class="sxs-lookup"><span data-stu-id="8b4f6-129">Add the OWIN Self-Host Packages</span></span>

<span data-ttu-id="8b4f6-130">**Araçlar** menüsünde **NuGet Paket Yöneticisi**' ne ve ardından **Paket Yöneticisi konsolu**' na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-130">From the **Tools** menu, click **NuGet Package Manager**, then click **Package Manager Console**.</span></span>

<span data-ttu-id="8b4f6-131">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="8b4f6-131">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](host-owin-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a><span data-ttu-id="8b4f6-132">HTTP uç noktası ekleme</span><span class="sxs-lookup"><span data-stu-id="8b4f6-132">Add an HTTP Endpoint</span></span>

<span data-ttu-id="8b4f6-133">Çözüm Gezgini ' de, AzureApp projesini genişletin.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-133">In Solution Explorer, expand the AzureApp project.</span></span> <span data-ttu-id="8b4f6-134">Roller düğümünü genişletin, WorkerRole1 öğesine sağ tıklayın ve **Özellikler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-134">Expand the Roles node, right-click WorkerRole1, and select **Properties**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image6.png)

<span data-ttu-id="8b4f6-135">**Uç noktalar**' a ve ardından **uç nokta Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-135">Click **Endpoints**, and then click **Add Endpoint**.</span></span>

<span data-ttu-id="8b4f6-136">**Protokol** açılan listesinde "http" öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-136">In the **Protocol** dropdown list, select "http".</span></span> <span data-ttu-id="8b4f6-137">**Genel bağlantı noktası** ve **özel bağlantı noktası**alanına 80 yazın.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-137">In **Public Port** and **Private Port**, type 80.</span></span> <span data-ttu-id="8b4f6-138">Bu bağlantı noktası numaraları farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-138">These port numbers can be different.</span></span> <span data-ttu-id="8b4f6-139">Genel bağlantı noktası, istemcilerin role bir istek gönderdiklerinde kullandıkları şeydir.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-139">The public port is what clients use when they send a request to the role.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image8.png)](host-owin-in-an-azure-worker-role/_static/image7.png)

## <a name="create-the-owin-startup-class"></a><span data-ttu-id="8b4f6-140">OWıN başlangıç sınıfını oluşturma</span><span class="sxs-lookup"><span data-stu-id="8b4f6-140">Create the OWIN Startup Class</span></span>

<span data-ttu-id="8b4f6-141">Çözüm Gezgini ' de, WorkerRole1 projesine sağ tıklayın ve yeni bir sınıf eklemek için / **sınıfı** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-141">In Solution Explorer, right click the WorkerRole1 project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="8b4f6-142">`Startup`sınıfı adlandırın.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-142">Name the class `Startup`.</span></span>

<span data-ttu-id="8b4f6-143">Tüm ortak kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="8b4f6-143">Replace all of the boilerplate code with the following:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample2.cs)]

<span data-ttu-id="8b4f6-144">`UseWelcomePage` uzantısı yöntemi, sitenizin çalıştığını doğrulamak için uygulamanıza basit bir HTML sayfası ekler.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-144">The `UseWelcomePage` extension method adds a simple HTML page to your application, to verify the site is working.</span></span>

## <a name="start-the-owin-host"></a><span data-ttu-id="8b4f6-145">OWıN konağını başlatma</span><span class="sxs-lookup"><span data-stu-id="8b4f6-145">Start the OWIN Host</span></span>

<span data-ttu-id="8b4f6-146">WorkerRole.cs dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-146">Open the WorkerRole.cs file.</span></span> <span data-ttu-id="8b4f6-147">Bu sınıf, çalışan rolü başlatıldığında ve durdurulduğunda çalışan kodu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-147">This class defines the code that runs when the worker role is started and stopped.</span></span>

<span data-ttu-id="8b4f6-148">Şu deyimi kullanarak aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="8b4f6-148">Add the following using statement:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample3.cs)]

<span data-ttu-id="8b4f6-149">`WorkerRole` sınıfına bir **IDisposable** üyesi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="8b4f6-149">Add an **IDisposable** member to the `WorkerRole` class:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample4.cs)]

<span data-ttu-id="8b4f6-150">`OnStart` yönteminde, ana bilgisayarı başlatmak için aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="8b4f6-150">In the `OnStart` method, add the following code to start the host:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample5.cs?highlight=5)]

<span data-ttu-id="8b4f6-151">**WebApp. Start** yöntemi owın konağını başlatır.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-151">The **WebApp.Start** method starts the OWIN host.</span></span> <span data-ttu-id="8b4f6-152">`Startup` sınıfının adı, yöntemin tür parametresidir.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-152">The name of the `Startup` class is a type parameter to the method.</span></span> <span data-ttu-id="8b4f6-153">Kurala göre, ana bilgisayar bu sınıfın `Configure` yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-153">By convention, the host will call the `Configure` method of this class.</span></span>

<span data-ttu-id="8b4f6-154">*\_uygulama* örneğinin atılırken `OnStop` geçersiz kılın:</span><span class="sxs-lookup"><span data-stu-id="8b4f6-154">Override the `OnStop` to dispose of the *\_app* instance:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample6.cs)]

<span data-ttu-id="8b4f6-155">WorkerRole.cs için kodun tamamı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="8b4f6-155">Here is the complete code for WorkerRole.cs:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample7.cs)]

<span data-ttu-id="8b4f6-156">Çözümü oluşturun ve F5 tuşuna basarak uygulamayı Azure Işlem öykünücüsünde yerel olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-156">Build the solution, and press F5 to run the application locally in the Azure Compute Emulator.</span></span> <span data-ttu-id="8b4f6-157">Güvenlik duvarınızın ayarlarına bağlı olarak, güvenlik duvarınız aracılığıyla öykünücüye izin vermeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-157">Depending on your firewall settings, you might need to allow the emulator through your firewall.</span></span>

<span data-ttu-id="8b4f6-158">İşlem öykünücüsü uç noktaya bir yerel IP adresi atar.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-158">The compute emulator assigns a local IP address to the endpoint.</span></span> <span data-ttu-id="8b4f6-159">Işlem öykünücüsü Kullanıcı arabirimini görüntüleyerek IP adresini bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-159">You can find the IP address by viewing the Compute Emulator UI.</span></span> <span data-ttu-id="8b4f6-160">Görev çubuğu bildirim alanında öykünücü simgesine sağ tıklayın ve **Işlem öykünücüsü Kullanıcı arabirimini göster**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-160">Right-click the emulator icon in the task bar notification area, and select **Show Compute Emulator UI**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image10.png)](host-owin-in-an-azure-worker-role/_static/image9.png)

<span data-ttu-id="8b4f6-161">Hizmet dağıtımları, dağıtım [kimlik], hizmet ayrıntıları altındaki IP adresini bulun.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-161">Find the IP address under Service Deployments, deployment [id], Service Details.</span></span> <span data-ttu-id="8b4f6-162">Bir Web tarayıcısı açın ve http:\/\/*Address*adresine gidin; burada *Adres* , Işlem öykünücüsü tarafından atanan IP adresidir; Örneğin, `http://127.0.0.1:80`.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-162">Open a web browser and navigate to http:\/\/*address*, where *address* is the IP address assigned by the compute emulator; for example, `http://127.0.0.1:80`.</span></span> <span data-ttu-id="8b4f6-163">OWıN karşılama sayfasını görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="8b4f6-163">You should see the OWIN welcome page:</span></span>

![](host-owin-in-an-azure-worker-role/_static/image11.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="8b4f6-164">Azure’a dağıtma</span><span class="sxs-lookup"><span data-stu-id="8b4f6-164">Deploy to Azure</span></span>

<span data-ttu-id="8b4f6-165">Bu adım için bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-165">For this step, you must have an Azure account.</span></span> <span data-ttu-id="8b4f6-166">Henüz bir hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-166">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8b4f6-167">Ayrıntılar için bkz. [ücretsiz deneme Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="8b4f6-167">For details, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="8b4f6-168">Çözüm Gezgini, AzureApp projesine sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-168">In Solution Explorer, right-click the AzureApp project.</span></span> <span data-ttu-id="8b4f6-169">**Yayımla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-169">Select **Publish**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image12.png)

<span data-ttu-id="8b4f6-170">Azure hesabınızda oturum açmadıysanız **oturum aç**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-170">If you are not signed in to your Azure account, click **Sign In**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image14.png)](host-owin-in-an-azure-worker-role/_static/image13.png)

<span data-ttu-id="8b4f6-171">Oturum açtıktan sonra bir abonelik seçin ve **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-171">After you are signed in, choose a subscription and click **Next**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image16.png)](host-owin-in-an-azure-worker-role/_static/image15.png)

<span data-ttu-id="8b4f6-172">Bulut hizmeti için bir ad girin ve bir bölge seçin.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-172">Enter a name for the cloud service and choose a region.</span></span> <span data-ttu-id="8b4f6-173">**Oluştur**'u tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-173">Click **Create**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image17.png)

<span data-ttu-id="8b4f6-174">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-174">Click **Publish**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image19.png)](host-owin-in-an-azure-worker-role/_static/image18.png)

<span data-ttu-id="8b4f6-175">Azure etkinlik günlüğü penceresinde dağıtım ilerleme durumu gösterilir.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-175">The Azure Activity Log window shows the progress of the deployment.</span></span> <span data-ttu-id="8b4f6-176">Uygulama dağıtıldığında `http://appname.cloudapp.net/`gidin; burada *appname* , bulut hizmetinizin adıdır.</span><span class="sxs-lookup"><span data-stu-id="8b4f6-176">When the app is deployed, browse to `http://appname.cloudapp.net/`, where *appname* is the name of your cloud service.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8b4f6-177">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="8b4f6-177">Additional Resources</span></span>

- [<span data-ttu-id="8b4f6-178">Project Katana’ya Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="8b4f6-178">An Overview of Project Katana</span></span>](an-overview-of-project-katana.md)
- [<span data-ttu-id="8b4f6-179">GitHub üzerinde Katana proje</span><span class="sxs-lookup"><span data-stu-id="8b4f6-179">Katana Project on GitHub</span></span>](https://github.com/aspnet/AspNetKatana/)
