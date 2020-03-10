---
uid: signalr/overview/performance/scaleout-with-windows-azure-service-bus
title: SignalR ölçeği Azure Service Bus | Microsoft Docs
author: bradygaster
description: Bu konuda kullanılan yazılım sürümleri, bu konunun SignalR 1. x sürümü Için .NET 4,5 SignalR sürüm 2 ' nin önceki sürümleri Visual Studio 2013,...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ce1305f9-30fd-49e3-bf38-d0a78dfb06c3
msc.legacyurl: /signalr/overview/performance/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: 73ed95c5027f57c7e390069dcb36b18a3714973f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579179"
---
# <a name="signalr-scaleout-with-azure-service-bus"></a><span data-ttu-id="35151-103">Azure Service Bus ile SignalR Ölçeğini Genişletme</span><span class="sxs-lookup"><span data-stu-id="35151-103">SignalR Scaleout with Azure Service Bus</span></span>

<span data-ttu-id="35151-104">, [Mike Ison](https://github.com/MikeWasson), [Patrick fleti](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="35151-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="35151-105">Bu öğreticide, her rol örneğine ileti dağıtmak için Service Bus arka düzlemi kullanarak bir SignalR uygulamasını bir Windows Azure Web rolüne dağıtacaksınız.</span><span class="sxs-lookup"><span data-stu-id="35151-105">In this tutorial, you will deploy a SignalR application to a Windows Azure Web Role, using the Service Bus backplane to distribute messages to each role instance.</span></span> <span data-ttu-id="35151-106">( [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/)ile Service Bus arka düzlemi de kullanabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="35151-106">(You can also use the Service Bus backplane with [web apps in Azure App Service](https://docs.microsoft.com/azure/app-service-web/).)</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

<span data-ttu-id="35151-107">Ön koşullar:</span><span class="sxs-lookup"><span data-stu-id="35151-107">Prerequisites:</span></span>

- <span data-ttu-id="35151-108">Bir Windows Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="35151-108">A Windows Azure account.</span></span>
- <span data-ttu-id="35151-109">[Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="35151-109">The [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span></span>
- <span data-ttu-id="35151-110">Visual Studio 2012 veya 2013.</span><span class="sxs-lookup"><span data-stu-id="35151-110">Visual Studio 2012 or 2013.</span></span>

<span data-ttu-id="35151-111">Service Bus geri düzlemi, [Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), sürüm 1,1 Service Bus ile de uyumludur.</span><span class="sxs-lookup"><span data-stu-id="35151-111">The service bus backplane is also compatible with [Service Bus for Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), version 1.1.</span></span> <span data-ttu-id="35151-112">Ancak, Windows Server için Service Bus sürüm 1,0 ile uyumlu değildir.</span><span class="sxs-lookup"><span data-stu-id="35151-112">However, it is not compatible with version 1.0 of Service Bus for Windows Server.</span></span>

## <a name="pricing"></a><span data-ttu-id="35151-113">Fiyatlandırma</span><span class="sxs-lookup"><span data-stu-id="35151-113">Pricing</span></span>

<span data-ttu-id="35151-114">Service Bus arkadüzlemi ileti göndermek için konuları kullanır.</span><span class="sxs-lookup"><span data-stu-id="35151-114">The Service Bus backplane uses topics to send messages.</span></span> <span data-ttu-id="35151-115">En son fiyatlandırma bilgileri için bkz. [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="35151-115">For the latest pricing information, see [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span></span> <span data-ttu-id="35151-116">Bu yazma sırasında, $1 ' den küçük bir ayda 1.000.000 ileti gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35151-116">At the time of this writing, you can send 1,000,000 messages per month for less than $1.</span></span> <span data-ttu-id="35151-117">Backdüzlemi, bir SignalR hub yöntemi çağrısı için bir Service Bus iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="35151-117">The backplane sends a service bus message for each invocation of a SignalR hub method.</span></span> <span data-ttu-id="35151-118">Bağlantılar için bazı denetim mesajları de vardır, bağlantıları geri bırakabilir, grupların katılımını ve bu şekilde devam eder.</span><span class="sxs-lookup"><span data-stu-id="35151-118">There are also some control messages for connections, disconnections, joining or leaving groups, and so forth.</span></span> <span data-ttu-id="35151-119">Çoğu uygulamada, ileti trafiğinin büyük bölümü hub yöntemi etkinleştirmeleri olacaktır.</span><span class="sxs-lookup"><span data-stu-id="35151-119">In most applications, the majority of the message traffic will be hub method invocations.</span></span>

## <a name="overview"></a><span data-ttu-id="35151-120">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="35151-120">Overview</span></span>

<span data-ttu-id="35151-121">Ayrıntılı öğreticiye girmeden önce, ne yapabileceğinize ilişkin hızlı bir genel bakış sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="35151-121">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="35151-122">Yeni bir Service Bus ad alanı oluşturmak için Windows Azure portal kullanın.</span><span class="sxs-lookup"><span data-stu-id="35151-122">Use the Windows Azure portal to create a new Service Bus namespace.</span></span>
2. <span data-ttu-id="35151-123">Bu NuGet paketlerini uygulamanıza ekleyin:</span><span class="sxs-lookup"><span data-stu-id="35151-123">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="35151-124">Microsoft. AspNet. SignalR</span><span class="sxs-lookup"><span data-stu-id="35151-124">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - <span data-ttu-id="35151-125">[Microsoft. Aspnet. SignalR. ServiceBus3](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3) veya [Microsoft. Aspnet. SignalR. ServiceBus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus)</span><span class="sxs-lookup"><span data-stu-id="35151-125">[Microsoft.AspNet.SignalR.ServiceBus3](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3) or [Microsoft.AspNet.SignalR.ServiceBus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus)</span></span>
3. <span data-ttu-id="35151-126">Bir SignalR uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="35151-126">Create a SignalR application.</span></span>
4. <span data-ttu-id="35151-127">Geri düzlemi yapılandırmak için Startup.cs 'e aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="35151-127">Add the following code to Startup.cs to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

<span data-ttu-id="35151-128">Bu kod, [Topiccount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx) ve [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)için varsayılan değerlerle birlikte geri düzlemi yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="35151-128">This code configures the backplane with the default values for [TopicCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx) and [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span></span> <span data-ttu-id="35151-129">Bu değerleri değiştirme hakkında daha fazla bilgi için bkz. [SignalR performansı: genişleme ölçümleri](signalr-performance.md#scaleout_metrics).</span><span class="sxs-lookup"><span data-stu-id="35151-129">For information on changing these values, see [SignalR Performance: Scaleout Metrics](signalr-performance.md#scaleout_metrics).</span></span>

<span data-ttu-id="35151-130">Her uygulama için, "YourAppName" için farklı bir değer seçin.</span><span class="sxs-lookup"><span data-stu-id="35151-130">For each application, pick a different value for "YourAppName".</span></span> <span data-ttu-id="35151-131">Birden çok uygulama arasında aynı değeri kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="35151-131">Do not use the same value across multiple applications.</span></span>

## <a name="create-the-azure-services"></a><span data-ttu-id="35151-132">Azure hizmetlerini oluşturma</span><span class="sxs-lookup"><span data-stu-id="35151-132">Create the Azure Services</span></span>

<span data-ttu-id="35151-133">[Bulut hizmeti oluşturma ve dağıtma](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)bölümünde açıklandığı gibi bir bulut hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="35151-133">Create a Cloud Service, as described in [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span> <span data-ttu-id="35151-134">"Nasıl yapılır: hızlı oluşturma kullanarak bulut hizmeti oluşturma" bölümündeki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="35151-134">Follow the steps in the section "How to: Create a cloud service using Quick Create".</span></span> <span data-ttu-id="35151-135">Bu öğreticide, bir sertifikayı karşıya yüklemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="35151-135">For this tutorial, you do not need to upload a certificate.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

<span data-ttu-id="35151-136">[Service Bus konu/abonelik kullanma](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)bölümünde açıklandığı gibi yeni bir Service Bus ad alanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="35151-136">Create a new Service Bus namespace, as described in [How to Use Service Bus Topics/Subscriptions](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span></span> <span data-ttu-id="35151-137">"Hizmet ad alanı oluşturma" bölümündeki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="35151-137">Follow the steps in the section "Create a Service Namespace".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="35151-138">Bulut hizmeti ve Service Bus ad alanı için aynı bölgeyi seçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="35151-138">Make sure to select the same region for the cloud service and the Service Bus namespace.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="35151-139">Visual Studio projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="35151-139">Create the Visual Studio Project</span></span>

<span data-ttu-id="35151-140">Visual Studio’yu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="35151-140">Start Visual Studio.</span></span> <span data-ttu-id="35151-141">**Dosya** menüsünden **Yeni Proje**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="35151-141">From the **File** menu, click **New Project**.</span></span>

<span data-ttu-id="35151-142">**Yeni proje** iletişim kutusunda, **görsel C#** ' i genişletin.</span><span class="sxs-lookup"><span data-stu-id="35151-142">In the **New Project** dialog box, expand **Visual C#**.</span></span> <span data-ttu-id="35151-143">**Yüklü şablonlar**altında **bulut** ' u ve ardından **Windows Azure bulut hizmeti**' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="35151-143">Under **Installed Templates**, select **Cloud** and then select **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="35151-144">Varsayılan .NET Framework 4,5 ' i tutun.</span><span class="sxs-lookup"><span data-stu-id="35151-144">Keep the default .NET Framework 4.5.</span></span> <span data-ttu-id="35151-145">Uygulamayı ChatService olarak adlandırın ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="35151-145">Name the application ChatService and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

<span data-ttu-id="35151-146">**Yeni Windows Azure bulut hizmeti** iletişim kutusunda ASP.NET Web rolü ' nü seçin.</span><span class="sxs-lookup"><span data-stu-id="35151-146">In the **New Windows Azure Cloud Service** dialog, select ASP.NET Web Role.</span></span> <span data-ttu-id="35151-147">Rolü çözümünüze eklemek için sağ ok düğmesine ( **&gt;** ) tıklayın.</span><span class="sxs-lookup"><span data-stu-id="35151-147">Click the right-arrow button (**&gt;**) to add the role to your solution.</span></span>

<span data-ttu-id="35151-148">Fareyi yeni rolün üzerine getirin, bu nedenle kurşun kalem simgesi görünür.</span><span class="sxs-lookup"><span data-stu-id="35151-148">Hover the mouse over the new role, so the pencil icon visible.</span></span> <span data-ttu-id="35151-149">Rolü yeniden adlandırmak için bu simgeye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="35151-149">Click this icon to rename the role.</span></span> <span data-ttu-id="35151-150">Rolü "SignalRChat" olarak adlandırın ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="35151-150">Name the role "SignalRChat" and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

<span data-ttu-id="35151-151">**Yeni ASP.NET projesi** Iletişim kutusunda **MVC**' yi seçin ve Tamam ' ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="35151-151">In the **New ASP.NET Project** dialog, select **MVC**, and click OK.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

<span data-ttu-id="35151-152">Proje Sihirbazı iki proje oluşturur:</span><span class="sxs-lookup"><span data-stu-id="35151-152">The project wizard creates two projects:</span></span>

- <span data-ttu-id="35151-153">ChatService: Bu proje Windows Azure uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="35151-153">ChatService: This project is the Windows Azure application.</span></span> <span data-ttu-id="35151-154">Azure rollerini ve diğer yapılandırma seçeneklerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="35151-154">It defines the Azure roles and other configuration options.</span></span>
- <span data-ttu-id="35151-155">SignalRChat: Bu proje ASP.NET MVC 5 projem.</span><span class="sxs-lookup"><span data-stu-id="35151-155">SignalRChat: This project is your ASP.NET MVC 5 project.</span></span>

## <a name="create-the-signalr-chat-application"></a><span data-ttu-id="35151-156">SignalR sohbet uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="35151-156">Create the SignalR Chat Application</span></span>

<span data-ttu-id="35151-157">Sohbet uygulamasını oluşturmak için, [SignalR ve MVC 5 Ile çalışmaya](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)başlama öğreticisindeki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="35151-157">To create the chat application, follow the steps in the tutorial [Getting Started with SignalR and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<span data-ttu-id="35151-158">Gerekli kitaplıkları yüklemek için NuGet kullanın.</span><span class="sxs-lookup"><span data-stu-id="35151-158">Use NuGet to install the required libraries.</span></span> <span data-ttu-id="35151-159">**Araçlar** menüsünde **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="35151-159">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="35151-160">**Paket Yöneticisi konsolu** penceresinde aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="35151-160">In the **Package Manager Console** window, enter the following commands:</span></span>

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

<span data-ttu-id="35151-161">Paketleri Windows Azure projesi yerine ASP.NET MVC projesine yüklemek için `-ProjectName` seçeneğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="35151-161">Use the `-ProjectName` option to install the packages to the ASP.NET MVC project, rather than the Windows Azure project.</span></span>

## <a name="configure-the-backplane"></a><span data-ttu-id="35151-162">Arka düzlemi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="35151-162">Configure the Backplane</span></span>

<span data-ttu-id="35151-163">Uygulamanızın Startup.cs dosyasında aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="35151-163">In your application's Startup.cs file, add the following code:</span></span>

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

<span data-ttu-id="35151-164">Artık Service Bus Bağlantı dizenizi almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="35151-164">Now you need to get your service bus connection string.</span></span> <span data-ttu-id="35151-165">Azure portal, oluşturduğunuz Service Bus ad alanını seçin ve erişim anahtarı simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="35151-165">In the Azure portal, select the service bus namespace that you created and click the Access Key icon.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

<span data-ttu-id="35151-166">Bağlantı dizesini panoya kopyalayın, ardından *ConnectionString* değişkenine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="35151-166">Copy the connection string to the clipboard, then paste it into the *connectionString* variable.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a><span data-ttu-id="35151-167">Azure’a dağıtma</span><span class="sxs-lookup"><span data-stu-id="35151-167">Deploy to Azure</span></span>

<span data-ttu-id="35151-168">Çözüm Gezgini ' de, ChatService projesinin içindeki **Roller** klasörünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="35151-168">In Solution Explorer, expand the **Roles** folder inside the ChatService project.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

<span data-ttu-id="35151-169">SignalRChat rolüne sağ tıklayın ve **Özellikler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="35151-169">Right-click the SignalRChat role and select **Properties**.</span></span> <span data-ttu-id="35151-170">**Yapılandırma** sekmesini seçin. **Örnekler** altında 2 ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="35151-170">Select the **Configuration** tab. Under **Instances** select 2.</span></span> <span data-ttu-id="35151-171">VM boyutunu **çok küçük**olarak da ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35151-171">You can also set the VM size to **Extra Small**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

<span data-ttu-id="35151-172">Değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="35151-172">Save the changes.</span></span>

<span data-ttu-id="35151-173">Çözüm Gezgini, ChatService projesine sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="35151-173">In Solution Explorer, right-click the ChatService project.</span></span> <span data-ttu-id="35151-174">**Yayımla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="35151-174">Select **Publish**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

<span data-ttu-id="35151-175">Windows Azure 'a ilk kez yayımladıysanız, kimlik bilgilerinizi indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="35151-175">If this is your first time publishing to Windows Azure, you must download your credentials.</span></span> <span data-ttu-id="35151-176">**Yayımla** sihirbazında, "kimlik bilgilerini Indirmek Için oturum aç" a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="35151-176">In the **Publish** wizard, click "Sign in to download credentials".</span></span> <span data-ttu-id="35151-177">Bu, Windows Azure portal oturum açmanızı ve bir yayımlama ayarları dosyası indirmeyi ister.</span><span class="sxs-lookup"><span data-stu-id="35151-177">This will prompt you to sign into the Windows Azure portal and download a publish settings file.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

<span data-ttu-id="35151-178">**Içeri aktar** ' a tıklayın ve indirdiğiniz yayınlama ayarları dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="35151-178">Click **Import** and select the publish settings file that you downloaded.</span></span>

<span data-ttu-id="35151-179">**İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="35151-179">Click **Next**.</span></span> <span data-ttu-id="35151-180">**Yayımlama ayarları** iletişim kutusunda, **bulut hizmeti**altında, daha önce oluşturduğunuz bulut hizmetini seçin.</span><span class="sxs-lookup"><span data-stu-id="35151-180">In the **Publish Settings** dialog, under **Cloud Service**, select the cloud service that you created earlier.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

<span data-ttu-id="35151-181">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="35151-181">Click **Publish**.</span></span> <span data-ttu-id="35151-182">Uygulamanın dağıtılması ve VM 'Lerin başlatılması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="35151-182">It can take a few minutes to deploy the application and start the VMs.</span></span>

<span data-ttu-id="35151-183">Artık sohbet uygulamasını çalıştırdığınızda, rol örnekleri Service Bus bir konu kullanarak Azure Service Bus üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="35151-183">Now when you run the chat application, the role instances communicate through Azure Service Bus, using a Service Bus topic.</span></span> <span data-ttu-id="35151-184">Konu başlığı, birden çok aboneye izin veren bir ileti kuyruğu.</span><span class="sxs-lookup"><span data-stu-id="35151-184">A topic is a message queue that allows multiple subscribers.</span></span>

<span data-ttu-id="35151-185">Geri düzlemi, konuyu ve abonelikleri otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35151-185">The backplane automatically creates the topic and the subscriptions.</span></span> <span data-ttu-id="35151-186">Abonelikler ve ileti etkinliğini görmek için Azure portal açın, Service Bus ad alanını seçin ve "konular" a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="35151-186">To see the subscriptions and message activity, open the Azure portal, select the Service Bus namespace, and click on "Topics".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

<span data-ttu-id="35151-187">İleti etkinliğinin panoda gösterilmesi birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="35151-187">It make take a few minutes for the message activity to show up in the dashboard.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image15.png)

<span data-ttu-id="35151-188">SignalR, konu ömrünü yönetir.</span><span class="sxs-lookup"><span data-stu-id="35151-188">SignalR manages the topic lifetime.</span></span> <span data-ttu-id="35151-189">Uygulamanız dağıtıldığı sürece konuları el ile silmeye veya konudaki ayarları değiştirmeye çalışmayın.</span><span class="sxs-lookup"><span data-stu-id="35151-189">As long as your application is deployed, don't try to manually delete topics or change settings on the topic.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="35151-190">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="35151-190">Troubleshooting</span></span>

<span data-ttu-id="35151-191">**System. InvalidOperationException "desteklenen tek IsolationLevel ' IsolationLevel. Serializable '."**</span><span class="sxs-lookup"><span data-stu-id="35151-191">**System.InvalidOperationException "The only supported IsolationLevel is 'IsolationLevel.Serializable'."**</span></span>

<span data-ttu-id="35151-192">Bu hata, bir işlemin işlem düzeyi `Serializable`dışında bir değere ayarlanmışsa ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="35151-192">This error can occur if the transaction level for an operation is set to something other than `Serializable`.</span></span> <span data-ttu-id="35151-193">Diğer işlem düzeyleriyle hiçbir işlem gerçekleştirilmediğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="35151-193">Verify that no operations are being performed with other transaction levels.</span></span>
