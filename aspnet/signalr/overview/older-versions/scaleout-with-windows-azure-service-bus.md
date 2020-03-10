---
uid: signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
title: SignalR ölçeği Azure Service Bus (SignalR 1. x) | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 501db899-e68c-49ff-81b2-1dc561bfe908
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: e64f84db00b571c01ea52f48d1ac1af46698d391
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558417"
---
# <a name="signalr-scaleout-with-azure-service-bus-signalr-1x"></a><span data-ttu-id="e4e1d-102">Azure Service Bus ile SignalR Ölçeğini Genişletme (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="e4e1d-102">SignalR Scaleout with Azure Service Bus (SignalR 1.x)</span></span>

<span data-ttu-id="e4e1d-103">, [Mike Ison](https://github.com/MikeWasson), [Patrick fleti](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="e4e1d-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="e4e1d-104">Bu öğreticide, her rol örneğine ileti dağıtmak için Service Bus arka düzlemi kullanarak bir SignalR uygulamasını bir Windows Azure Web rolüne dağıtacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-104">In this tutorial, you will deploy a SignalR application to a Windows Azure Web Role, using the Service Bus backplane to distribute messages to each role instance.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

<span data-ttu-id="e4e1d-105">Ön koşullar:</span><span class="sxs-lookup"><span data-stu-id="e4e1d-105">Prerequisites:</span></span>

- <span data-ttu-id="e4e1d-106">Bir Windows Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-106">A Windows Azure account.</span></span>
- <span data-ttu-id="e4e1d-107">[Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="e4e1d-107">The [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span></span>
- <span data-ttu-id="e4e1d-108">Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-108">Visual Studio 2012.</span></span>

<span data-ttu-id="e4e1d-109">Service Bus geri düzlemi, [Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), sürüm 1,1 Service Bus ile de uyumludur.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-109">The service bus backplane is also compatible with [Service Bus for Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), version 1.1.</span></span> <span data-ttu-id="e4e1d-110">Ancak, Windows Server için Service Bus sürüm 1,0 ile uyumlu değildir.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-110">However, it is not compatible with version 1.0 of Service Bus for Windows Server.</span></span>

## <a name="pricing"></a><span data-ttu-id="e4e1d-111">Fiyatlandırma</span><span class="sxs-lookup"><span data-stu-id="e4e1d-111">Pricing</span></span>

<span data-ttu-id="e4e1d-112">Service Bus arkadüzlemi ileti göndermek için konuları kullanır.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-112">The Service Bus backplane uses topics to send messages.</span></span> <span data-ttu-id="e4e1d-113">En son fiyatlandırma bilgileri için bkz. [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="e4e1d-113">For the latest pricing information, see [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span></span> <span data-ttu-id="e4e1d-114">Bu yazma sırasında, $1 ' den küçük bir ayda 1.000.000 ileti gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-114">At the time of this writing, you can send 1,000,000 messages per month for less than $1.</span></span> <span data-ttu-id="e4e1d-115">Backdüzlemi, bir SignalR hub yöntemi çağrısı için bir Service Bus iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-115">The backplane sends a service bus message for each invocation of a SignalR hub method.</span></span> <span data-ttu-id="e4e1d-116">Bağlantılar için bazı denetim mesajları de vardır, bağlantıları geri bırakabilir, grupların katılımını ve bu şekilde devam eder.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-116">There are also some control messages for connections, disconnections, joining or leaving groups, and so forth.</span></span> <span data-ttu-id="e4e1d-117">Çoğu uygulamada, ileti trafiğinin büyük bölümü hub yöntemi etkinleştirmeleri olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-117">In most applications, the majority of the message traffic will be hub method invocations.</span></span>

## <a name="overview"></a><span data-ttu-id="e4e1d-118">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="e4e1d-118">Overview</span></span>

<span data-ttu-id="e4e1d-119">Ayrıntılı öğreticiye girmeden önce, ne yapabileceğinize ilişkin hızlı bir genel bakış sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-119">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="e4e1d-120">Yeni bir Service Bus ad alanı oluşturmak için Windows Azure portal kullanın.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-120">Use the Windows Azure portal to create a new Service Bus namespace.</span></span>
2. <span data-ttu-id="e4e1d-121">Bu NuGet paketlerini uygulamanıza ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e4e1d-121">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="e4e1d-122">Microsoft. AspNet. SignalR</span><span class="sxs-lookup"><span data-stu-id="e4e1d-122">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="e4e1d-123">Microsoft. AspNet. SignalR. ServiceBus</span><span class="sxs-lookup"><span data-stu-id="e4e1d-123">Microsoft.AspNet.SignalR.ServiceBus</span></span>](http://www.nuget.org/packages/SignalR.WindowsAzureServiceBus)
3. <span data-ttu-id="e4e1d-124">Bir SignalR uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-124">Create a SignalR application.</span></span>
4. <span data-ttu-id="e4e1d-125">Geri düzlemi yapılandırmak için aşağıdaki kodu Global. asax öğesine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e4e1d-125">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

<span data-ttu-id="e4e1d-126">Her uygulama için, "YourAppName" için farklı bir değer seçin.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-126">For each application, pick a different value for "YourAppName".</span></span> <span data-ttu-id="e4e1d-127">Birden çok uygulama arasında aynı değeri kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-127">Do not use the same value across multiple applications.</span></span>

## <a name="create-the-azure-services"></a><span data-ttu-id="e4e1d-128">Azure hizmetlerini oluşturma</span><span class="sxs-lookup"><span data-stu-id="e4e1d-128">Create the Azure Services</span></span>

<span data-ttu-id="e4e1d-129">[Bulut hizmeti oluşturma ve dağıtma](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)bölümünde açıklandığı gibi bir bulut hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-129">Create a Cloud Service, as described in [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span> <span data-ttu-id="e4e1d-130">"Nasıl yapılır: hızlı oluşturma kullanarak bulut hizmeti oluşturma" bölümündeki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-130">Follow the steps in the section "How to: Create a cloud service using Quick Create".</span></span> <span data-ttu-id="e4e1d-131">Bu öğreticide, bir sertifikayı karşıya yüklemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-131">For this tutorial, you do not need to upload a certificate.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

<span data-ttu-id="e4e1d-132">[Service Bus konu/abonelik kullanma](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)bölümünde açıklandığı gibi yeni bir Service Bus ad alanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-132">Create a new Service Bus namespace, as described in [How to Use Service Bus Topics/Subscriptions](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span></span> <span data-ttu-id="e4e1d-133">"Hizmet ad alanı oluşturma" bölümündeki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-133">Follow the steps in the section "Create a Service Namespace".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="e4e1d-134">Bulut hizmeti ve Service Bus ad alanı için aynı bölgeyi seçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-134">Make sure to select the same region for the cloud service and the Service Bus namespace.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="e4e1d-135">Visual Studio projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e4e1d-135">Create the Visual Studio Project</span></span>

<span data-ttu-id="e4e1d-136">Visual Studio’yu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-136">Start Visual Studio.</span></span> <span data-ttu-id="e4e1d-137">**Dosya** menüsünden **Yeni Proje**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-137">From the **File** menu, click **New Project**.</span></span>

<span data-ttu-id="e4e1d-138">**Yeni proje** iletişim kutusunda, **görsel C#** ' i genişletin.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-138">In the **New Project** dialog box, expand **Visual C#**.</span></span> <span data-ttu-id="e4e1d-139">**Yüklü şablonlar**altında **bulut** ' u ve ardından **Windows Azure bulut hizmeti**' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-139">Under **Installed Templates**, select **Cloud** and then select **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="e4e1d-140">Varsayılan .NET Framework 4,5 ' i tutun.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-140">Keep the default .NET Framework 4.5.</span></span> <span data-ttu-id="e4e1d-141">Uygulamayı ChatService olarak adlandırın ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-141">Name the application ChatService and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

<span data-ttu-id="e4e1d-142">**Yeni Windows Azure bulut hizmeti** iletişim kutusunda ASP.NET MVC 4 Web rolü ' nü seçin.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-142">In the **New Windows Azure Cloud Service** dialog, select ASP.NET MVC 4 Web Role.</span></span> <span data-ttu-id="e4e1d-143">Rolü çözümünüze eklemek için sağ ok düğmesine ( **&gt;** ) tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-143">Click the right-arrow button (**&gt;**) to add the role to your solution.</span></span>

<span data-ttu-id="e4e1d-144">Fareyi yeni rolün üzerine getirin, bu nedenle kurşun kalem simgesi görünür.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-144">Hover the mouse over the new role, so the pencil icon visible.</span></span> <span data-ttu-id="e4e1d-145">Rolü yeniden adlandırmak için bu simgeye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-145">Click this icon to rename the role.</span></span> <span data-ttu-id="e4e1d-146">Rolü "SignalRChat" olarak adlandırın ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-146">Name the role "SignalRChat" and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

<span data-ttu-id="e4e1d-147">**Yeni ASP.NET MVC 4 proje** sihirbazında **Internet uygulaması**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-147">In the **New ASP.NET MVC 4 Project** wizard, select **Internet Application**.</span></span> <span data-ttu-id="e4e1d-148">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-148">Click **OK**.</span></span> <span data-ttu-id="e4e1d-149">Proje Sihirbazı iki proje oluşturur:</span><span class="sxs-lookup"><span data-stu-id="e4e1d-149">The project wizard creates two projects:</span></span>

- <span data-ttu-id="e4e1d-150">ChatService: Bu proje Windows Azure uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-150">ChatService: This project is the Windows Azure application.</span></span> <span data-ttu-id="e4e1d-151">Azure rollerini ve diğer yapılandırma seçeneklerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-151">It defines the Azure roles and other configuration options.</span></span>
- <span data-ttu-id="e4e1d-152">SignalRChat: Bu proje ASP.NET MVC 4 projem.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-152">SignalRChat: This project is your ASP.NET MVC 4 project.</span></span>

## <a name="create-the-signalr-chat-application"></a><span data-ttu-id="e4e1d-153">SignalR sohbet uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="e4e1d-153">Create the SignalR Chat Application</span></span>

<span data-ttu-id="e4e1d-154">Sohbet uygulamasını oluşturmak için, [SignalR ve MVC 4 Ile çalışmaya](tutorial-getting-started-with-signalr-and-mvc-4.md)başlama öğreticisindeki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-154">To create the chat application, follow the steps in the tutorial [Getting Started with SignalR and MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span></span>

<span data-ttu-id="e4e1d-155">Gerekli kitaplıkları yüklemek için NuGet kullanın.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-155">Use NuGet to install the required libraries.</span></span> <span data-ttu-id="e4e1d-156">**Araçlar** menüsünde **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-156">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="e4e1d-157">**Paket Yöneticisi konsolu** penceresinde aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="e4e1d-157">In the **Package Manager Console** window, enter the following commands:</span></span>

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

<span data-ttu-id="e4e1d-158">Paketleri Windows Azure projesi yerine ASP.NET MVC projesine yüklemek için `-ProjectName` seçeneğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-158">Use the `-ProjectName` option to install the packages to the ASP.NET MVC project, rather than the Windows Azure project.</span></span>

## <a name="configure-the-backplane"></a><span data-ttu-id="e4e1d-159">Arka düzlemi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e4e1d-159">Configure the Backplane</span></span>

<span data-ttu-id="e4e1d-160">Uygulamanızın Global. asax dosyasında aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e4e1d-160">In your application's Global.asax file, add the following code:</span></span>

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

<span data-ttu-id="e4e1d-161">Artık Service Bus Bağlantı dizenizi almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-161">Now you need to get your service bus connection string.</span></span> <span data-ttu-id="e4e1d-162">Azure portal, oluşturduğunuz Service Bus ad alanını seçin ve erişim anahtarı simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-162">In the Azure portal, select the service bus namespace that you created and click the Access Key icon.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

<span data-ttu-id="e4e1d-163">Bağlantı dizesini panoya kopyalayın, ardından *ConnectionString* değişkenine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-163">Copy the connection string to the clipboard, then paste it into the *connectionString* variable.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a><span data-ttu-id="e4e1d-164">Azure’a dağıtma</span><span class="sxs-lookup"><span data-stu-id="e4e1d-164">Deploy to Azure</span></span>

<span data-ttu-id="e4e1d-165">Çözüm Gezgini ' de, ChatService projesinin içindeki **Roller** klasörünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-165">In Solution Explorer, expand the **Roles** folder inside the ChatService project.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

<span data-ttu-id="e4e1d-166">SignalRChat rolüne sağ tıklayın ve **Özellikler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-166">Right-click the SignalRChat role and select **Properties**.</span></span> <span data-ttu-id="e4e1d-167">**Yapılandırma** sekmesini seçin. **Örnekler** altında 2 ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-167">Select the **Configuration** tab. Under **Instances** select 2.</span></span> <span data-ttu-id="e4e1d-168">VM boyutunu **çok küçük**olarak da ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-168">You can also set the VM size to **Extra Small**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

<span data-ttu-id="e4e1d-169">Değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-169">Save the changes.</span></span>

<span data-ttu-id="e4e1d-170">Çözüm Gezgini, ChatService projesine sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-170">In Solution Explorer, right-click the ChatService project.</span></span> <span data-ttu-id="e4e1d-171">**Yayımla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-171">Select **Publish**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

<span data-ttu-id="e4e1d-172">Windows Azure 'a ilk kez yayımladıysanız, kimlik bilgilerinizi indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-172">If this is your first time publishing to Windows Azure, you must download your credentials.</span></span> <span data-ttu-id="e4e1d-173">**Yayımla** sihirbazında, "kimlik bilgilerini Indirmek Için oturum aç" a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-173">In the **Publish** wizard, click "Sign in to download credentials".</span></span> <span data-ttu-id="e4e1d-174">Bu, Windows Azure portal oturum açmanızı ve bir yayımlama ayarları dosyası indirmeyi ister.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-174">This will prompt you to sign into the Windows Azure portal and download a publish settings file.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

<span data-ttu-id="e4e1d-175">**Içeri aktar** ' a tıklayın ve indirdiğiniz yayınlama ayarları dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-175">Click **Import** and select the publish settings file that you downloaded.</span></span>

<span data-ttu-id="e4e1d-176">**İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-176">Click **Next**.</span></span> <span data-ttu-id="e4e1d-177">**Yayımlama ayarları** iletişim kutusunda, **bulut hizmeti**altında, daha önce oluşturduğunuz bulut hizmetini seçin.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-177">In the **Publish Settings** dialog, under **Cloud Service**, select the cloud service that you created earlier.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

<span data-ttu-id="e4e1d-178">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-178">Click **Publish**.</span></span> <span data-ttu-id="e4e1d-179">Uygulamanın dağıtılması ve VM 'Lerin başlatılması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-179">It can take a few minutes to deploy the application and start the VMs.</span></span>

<span data-ttu-id="e4e1d-180">Artık sohbet uygulamasını çalıştırdığınızda, rol örnekleri Service Bus bir konu kullanarak Azure Service Bus üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-180">Now when you run the chat application, the role instances communicate through Azure Service Bus, using a Service Bus topic.</span></span> <span data-ttu-id="e4e1d-181">Konu başlığı, birden çok aboneye izin veren bir ileti kuyruğu.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-181">A topic is a message queue that allows multiple subscribers.</span></span>

<span data-ttu-id="e4e1d-182">Geri düzlemi, konuyu ve abonelikleri otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-182">The backplane automatically creates the topic and the subscriptions.</span></span> <span data-ttu-id="e4e1d-183">Abonelikler ve ileti etkinliğini görmek için Azure portal açın, Service Bus ad alanını seçin ve "konular" a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-183">To see the subscriptions and message activity, open the Azure portal, select the Service Bus namespace, and click on "Topics".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

<span data-ttu-id="e4e1d-184">İleti etkinliğinin panoda gösterilmesi birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-184">It make take a few minutes for the message activity to show up in the dashboard.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

<span data-ttu-id="e4e1d-185">SignalR, konu ömrünü yönetir.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-185">SignalR manages the topic lifetime.</span></span> <span data-ttu-id="e4e1d-186">Uygulamanız dağıtıldığı sürece konuları el ile silmeye veya konudaki ayarları değiştirmeye çalışmayın.</span><span class="sxs-lookup"><span data-stu-id="e4e1d-186">As long as your application is deployed, don't try to manually delete topics or change settings on the topic.</span></span>
