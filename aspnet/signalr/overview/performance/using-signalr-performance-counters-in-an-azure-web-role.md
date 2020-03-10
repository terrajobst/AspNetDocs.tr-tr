---
uid: signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
title: Azure Web rolünde SignalR performans sayaçlarını kullanma | Microsoft Docs
author: guardrex
description: Azure Web rolünde SignalR performans sayaçlarını yüklemek ve kullanmak.
keywords: ASP. NET, SignalR, performans sayacı, Azure Web rolü
ms.author: bradyg
ms.date: 10/03/2018
ms.assetid: 2a127d3b-21ed-4cc9-bec0-cdab4e742a25
msc.legacyurl: /signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
msc.type: authoredcontent
ms.openlocfilehash: 969a2ce43a7cb8d649555daf282f900401c0c914
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578983"
---
# <a name="using-signalr-performance-counters-in-an-azure-web-role"></a><span data-ttu-id="e7886-104">Azure Web rolünde SignalR performans sayaçlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="e7886-104">Using SignalR performance counters in an Azure Web Role</span></span>

<span data-ttu-id="e7886-105">[Luke Latham](https://github.com/guardrex) tarafından</span><span class="sxs-lookup"><span data-stu-id="e7886-105">By [Luke Latham](https://github.com/guardrex)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="e7886-106">SignalR performans sayaçları, uygulamanızın performansını bir Azure Web rolünde izlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e7886-106">SignalR performance counters are used to monitor your app's performance in an Azure Web Role.</span></span> <span data-ttu-id="e7886-107">Sayaçlar Microsoft Azure Tanılama tarafından yakalanır.</span><span class="sxs-lookup"><span data-stu-id="e7886-107">The counters are captured by Microsoft Azure Diagnostics.</span></span> <span data-ttu-id="e7886-108">Azure 'da SignalR performans sayaçlarını, tek başına veya şirket içi uygulamalar için kullanılan aynı araç olan *SignalR. exe*ile birlikte yüklersiniz.</span><span class="sxs-lookup"><span data-stu-id="e7886-108">You install SignalR performance counters on Azure with *signalr.exe*, the same tool used for standalone or on-premises apps.</span></span> <span data-ttu-id="e7886-109">Azure rolleri geçici olduğundan, bir uygulamayı başlangıçtan sonra SignalR performans sayaçlarını yükleyecek ve kaydedecek şekilde yapılandırırsınız.</span><span class="sxs-lookup"><span data-stu-id="e7886-109">Since Azure roles are transient, you configure an app to install and register SignalR performance counters upon startup.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7886-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="e7886-110">Prerequisites</span></span>

* <span data-ttu-id="e7886-111">Visual Studio 2015 veya [2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)</span><span class="sxs-lookup"><span data-stu-id="e7886-111">Visual Studio 2015 or [2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)</span></span>
* <span data-ttu-id="e7886-112">[Visual Studio için MICROSOFT Azure SDK](https://azure.microsoft.com/downloads/) 'sı **: SDK 'yı yükledikten sonra makinenizi yeniden başlatın.**</span><span class="sxs-lookup"><span data-stu-id="e7886-112">[Microsoft Azure SDK for Visual Studio](https://azure.microsoft.com/downloads/) **Note: Restart your machine after installing the SDK.**</span></span>
* <span data-ttu-id="e7886-113">Microsoft Azure abonelik: ücretsiz bir Azure deneme hesabına kaydolmak Için bkz. [Azure Ücretsiz deneme](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="e7886-113">Microsoft Azure subscription: To sign up for a free Azure trial account, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="creating-an-azure-web-role-application-that-exposes-signalr-performance-counters"></a><span data-ttu-id="e7886-114">SignalR performans sayaçlarını kullanıma sunan bir Azure Web rolü uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="e7886-114">Creating an Azure Web Role application that exposes SignalR performance counters</span></span>

1. <span data-ttu-id="e7886-115">Visual Studio'yu açın.</span><span class="sxs-lookup"><span data-stu-id="e7886-115">Open Visual Studio.</span></span>

2. <span data-ttu-id="e7886-116">Visual Studio 'da **dosya** > **Yeni** > **Proje**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e7886-116">In Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="e7886-117">**Yeni proje** iletişim kutusunda, sol taraftaki **Visual C#**  > **bulut** kategorisini seçin ve ardından **Azure bulut hizmeti** şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="e7886-117">In the **New Project** dialog box, select the **Visual C#** > **Cloud** category on the left, and then select the **Azure Cloud Service** template.</span></span> <span data-ttu-id="e7886-118">Uygulamayı **Signalrperfcounters** olarak adlandırın ve **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e7886-118">Name the app **SignalRPerfCounters** and select **OK**.</span></span>

   ![Yeni bulut uygulaması](using-signalr-performance-counters-in-an-azure-web-role/_static/image1.png)

   > [!NOTE]
   > <span data-ttu-id="e7886-120">**Bulut** şablonu kategorisini veya **Azure bulut hizmeti** şablonunu görmüyorsanız, Visual Studio 2017 için **Azure geliştirme** iş yükünü yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7886-120">If you don't see the **Cloud** template category or the **Azure Cloud Service** template, you need to install the **Azure development** workload for Visual Studio 2017.</span></span> <span data-ttu-id="e7886-121">Visual Studio Yükleyicisi açmak için **Yeni proje** iletişim kutusunun sol alt tarafındaki **Visual Studio yükleyicisi aç** bağlantısını seçin.</span><span class="sxs-lookup"><span data-stu-id="e7886-121">Choose the **Open Visual Studio Installer** link on the bottom-left side of the **New Project** dialog to open Visual Studio Installer.</span></span> <span data-ttu-id="e7886-122">**Azure geliştirme** iş yükünü seçin ve sonra iş yükünü yüklemeye başlamak için **Değiştir** ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="e7886-122">Select the **Azure development** workload, and then choose **Modify** to start installing the workload.</span></span>
   >
   > ![Visual Studio Yükleyicisi Azure geliştirme iş yükü](using-signalr-performance-counters-in-an-azure-web-role/_static/azure-development-workload.png)

4. <span data-ttu-id="e7886-124">**Yeni Microsoft Azure bulut hizmeti** iletişim kutusunda **ASP.NET Web rolü** ' nü seçin ve rolü projeye eklemek için > düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="e7886-124">In the **New Microsoft Azure Cloud Service** dialog, select **ASP.NET Web Role** and select the > button to add the role to the project.</span></span> <span data-ttu-id="e7886-125">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e7886-125">Select **OK**.</span></span>

   ![ASP.NET Web rolü Ekle](using-signalr-performance-counters-in-an-azure-web-role/_static/image2.png)

5. <span data-ttu-id="e7886-127">**Yeni ASP.NET Web uygulaması-WebRole1** Iletişim kutusunda **MVC** şablonunu seçin ve ardından **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e7886-127">In the **New ASP.NET Web Application - WebRole1** dialog, select the **MVC** template, and then select **OK**.</span></span>

   ![MVC ve Web API 'SI ekleme](using-signalr-performance-counters-in-an-azure-web-role/_static/image3.png)

6. <span data-ttu-id="e7886-129">**Çözüm Gezgini**' de, **WebRole1**altında *Diagnostics. wadcfgx* dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="e7886-129">In **Solution Explorer**, open the *diagnostics.wadcfgx* file under **WebRole1**.</span></span>

   ![Çözüm Gezgini Diagnostics. wadcfgx](using-signalr-performance-counters-in-an-azure-web-role/_static/image4.png)

7. <span data-ttu-id="e7886-131">Dosyanın içeriğini aşağıdaki yapılandırmayla değiştirin ve dosyayı kaydedin:</span><span class="sxs-lookup"><span data-stu-id="e7886-131">Replace the contents of the file with the following configuration and save the file:</span></span>

   [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample1.xml)]

8. <span data-ttu-id="e7886-132">**NuGet paket yöneticisi** > **Araçlar** ' dan **Paket Yöneticisi konsolunu** açın.</span><span class="sxs-lookup"><span data-stu-id="e7886-132">Open the **Package Manager Console** from **Tools** > **NuGet Package Manager**.</span></span> <span data-ttu-id="e7886-133">SignalR 'nin en son sürümünü ve SignalR yardımcı programları paketini yüklemek için aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="e7886-133">Enter the following commands to install the latest version of SignalR and the SignalR utilities package:</span></span>

   [!code-powershell[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample2.ps1)]

9. <span data-ttu-id="e7886-134">Uygulamayı başlatıldığında veya geri dönüştürüldüğünde, SignalR performans sayaçlarını rol örneğine yükleyecek şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e7886-134">Configure the app to install the SignalR performance counters into the role instance when it starts up or recycles.</span></span> <span data-ttu-id="e7886-135">**Çözüm Gezgini**, **WebRole1** projesine sağ tıklayın ve > **Yeni klasör** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e7886-135">In **Solution Explorer**, right-click on the **WebRole1** project and select **Add** > **New Folder**.</span></span> <span data-ttu-id="e7886-136">Yeni klasör *başlangıcını*adlandırın.</span><span class="sxs-lookup"><span data-stu-id="e7886-136">Name the new folder *Startup*.</span></span>

   ![Başlangıç klasörü Ekle](using-signalr-performance-counters-in-an-azure-web-role/_static/image5.png)

10. <span data-ttu-id="e7886-138">*SignalR. exe* dosyasını ( **Microsoft. Aspnet. SignalR. utils** paketi ile eklendi) \<projesi klasöründen kopyalayın >/SignalRPerfCounters/Packages/Microsoft.Aspnet.SignalR.utils. önceki adımda oluşturduğunuz *Başlangıç* klasörü için sürüm >/tools\<.</span><span class="sxs-lookup"><span data-stu-id="e7886-138">Copy the *signalr.exe* file (added with the **Microsoft.AspNet.SignalR.Utils** package) from \<project folder>/SignalRPerfCounters/packages/Microsoft.AspNet.SignalR.Utils.\<version>/tools to the *Startup* folder you created in the previous step.</span></span>

11. <span data-ttu-id="e7886-139">**Çözüm Gezgini**, *Başlangıç* klasörüne sağ tıklayın ve > **var olan öğeyi** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e7886-139">In **Solution Explorer**, right-click the *Startup* folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="e7886-140">Görüntülenen iletişim kutusunda *SignalR. exe* ' yi seçin ve **Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e7886-140">In the dialog that appears, select *signalr.exe* and select **Add**.</span></span>

    ![SignalR. exe ' yi projeye Ekle](using-signalr-performance-counters-in-an-azure-web-role/_static/image6.png)

12. <span data-ttu-id="e7886-142">Oluşturduğunuz *Başlangıç* klasörüne sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e7886-142">Right-click on the *Startup* folder you created.</span></span> <span data-ttu-id="e7886-143"> > **Yeni öğe** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e7886-143">Select **Add** > **New Item**.</span></span> <span data-ttu-id="e7886-144">**Genel** düğümünü seçin, **metin dosyası**' nı seçin ve yeni öğe *signalrperfcounterınstall. cmd*olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="e7886-144">Select the **General** node, select **Text File**, and name the new item *SignalRPerfCounterInstall.cmd*.</span></span> <span data-ttu-id="e7886-145">Bu komut dosyası, SignalR performans sayaçlarını Web rolüne yükler.</span><span class="sxs-lookup"><span data-stu-id="e7886-145">This command file will install the SignalR performance counters into the web role.</span></span>

    ![SignalR performans sayacı yüklemesi toplu iş dosyası oluşturma](using-signalr-performance-counters-in-an-azure-web-role/_static/image7.png)

13. <span data-ttu-id="e7886-147">Visual Studio, *Signalrperfcounterınstall. cmd* dosyasını oluşturduğunda ana pencerede otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="e7886-147">When Visual Studio creates the *SignalRPerfCounterInstall.cmd* file, it will automatically open in the main window.</span></span> <span data-ttu-id="e7886-148">Dosyanın içeriğini aşağıdaki komut dosyasıyla değiştirin, sonra dosyayı kaydedip kapatın.</span><span class="sxs-lookup"><span data-stu-id="e7886-148">Replace the contents of the file with the following script, then save and close the file.</span></span> <span data-ttu-id="e7886-149">Bu betik, SignalR performans sayaçlarını rol örneğine ekleyen *SignalR. exe*' yi yürütür.</span><span class="sxs-lookup"><span data-stu-id="e7886-149">This script executes *signalr.exe*, which adds the SignalR performance counters to the role instance.</span></span>

    [!code-console[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample3.cmd)]

14. <span data-ttu-id="e7886-150">**Çözüm Gezgini**'da *SignalR. exe* dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="e7886-150">Select the *signalr.exe* file in **Solution Explorer**.</span></span> <span data-ttu-id="e7886-151">Dosyanın **özelliklerinde**, **her zaman kopyalamak**için **Çıkış Dizinine Kopyala** ' yı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e7886-151">In the file's **Properties**, set **Copy to Output Directory** to **Copy Always**.</span></span>

    ![Her zaman kopyalamak için çıkış dizinine Kopyala ayarla](using-signalr-performance-counters-in-an-azure-web-role/_static/image8.png)

15. <span data-ttu-id="e7886-153">*Signalrperfcounterınstall. cmd* dosyası için önceki adımı tekrarlayın.</span><span class="sxs-lookup"><span data-stu-id="e7886-153">Repeat the previous step for the *SignalRPerfCounterInstall.cmd* file.</span></span>

16. <span data-ttu-id="e7886-154">*Signalrperfcounterınstall. cmd* dosyasına sağ tıklayın ve **birlikte Aç**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e7886-154">Right-click on the *SignalRPerfCounterInstall.cmd* file and select **Open With**.</span></span> <span data-ttu-id="e7886-155">Görüntülenen iletişim kutusunda **Ikili düzenleyici** ' yi seçin ve **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e7886-155">In the dialog that appears, select **Binary Editor** and select **OK**.</span></span>

    ![Ikili düzenleyiciyle aç](using-signalr-performance-counters-in-an-azure-web-role/_static/image9.png)

17. <span data-ttu-id="e7886-157">İkili düzenleyicide, dosyadaki önde gelen baytları seçin ve silin.</span><span class="sxs-lookup"><span data-stu-id="e7886-157">In the binary editor, select any leading bytes in the file and delete them.</span></span> <span data-ttu-id="e7886-158">Dosyayı kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="e7886-158">Save and close the file.</span></span>

    ![Baştaki baytları Sil](using-signalr-performance-counters-in-an-azure-web-role/_static/image10.png)

18. <span data-ttu-id="e7886-160">*ServiceDefinition. csdef* ' i açın ve hizmet başlatıldığında *Signalrperfcounterınstall. cmd* dosyasını yürüten bir başlangıç görevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e7886-160">Open *ServiceDefinition.csdef* and add a startup task that executes the *SignalrPerfCounterInstall.cmd* file when the service starts up:</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample4.xml?highlight=4-7)]

19. <span data-ttu-id="e7886-161">`Views/Shared/_Layout.cshtml` açın ve dosya sonundan jQuery paket betiğini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e7886-161">Open `Views/Shared/_Layout.cshtml` and remove the jQuery bundle script from the end of the file.</span></span>

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample5.cshtml)]

20. <span data-ttu-id="e7886-162">Sunucuda `increment` yöntemi sürekli çağıran bir JavaScript istemcisi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e7886-162">Add a JavaScript client that continuously calls the `increment` method on the server.</span></span> <span data-ttu-id="e7886-163">`Views/Home/Index.cshtml` açın ve içeriği şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="e7886-163">Open `Views/Home/Index.cshtml` and replace the contents with the following code:</span></span>

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample6.cshtml)]

21. <span data-ttu-id="e7886-164">**WebRole1** projesinde *hub 'lar*adlı yeni bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e7886-164">Create a new folder in the **WebRole1** project named *Hubs*.</span></span> <span data-ttu-id="e7886-165">**Çözüm Gezgini** *hub* klasörüne sağ tıklayın ve > **Yeni öğe** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e7886-165">Right-click the *Hubs* folder in **Solution Explorer** and select **Add** > **New Item**.</span></span> <span data-ttu-id="e7886-166">**Yeni öğe Ekle** iletişim kutusunda, **Web** > **SignalR** kategorisini seçin ve ardından **SignalR hub sınıfı (v2)** öğe şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="e7886-166">In the **Add New Item** dialog box, select the **Web** > **SignalR** category, and then select the **SignalR Hub Class (v2)** item template.</span></span> <span data-ttu-id="e7886-167">Yeni hub *MyHub.cs* ' ı adlandırın ve **Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e7886-167">Name the new hub *MyHub.cs* and select **Add**.</span></span>

    ![SignalR hub sınıfı yeni öğe Ekle iletişim kutusunda hub klasörüne ekleniyor](using-signalr-performance-counters-in-an-azure-web-role/_static/image13.png)

22. <span data-ttu-id="e7886-169">*MyHub.cs* , ana pencerede otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="e7886-169">*MyHub.cs* will automatically open in the main window.</span></span> <span data-ttu-id="e7886-170">İçeriği aşağıdaki kodla değiştirin, sonra dosyayı kaydedip kapatın:</span><span class="sxs-lookup"><span data-stu-id="e7886-170">Replace the contents with the following code, then save and close the file:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample7.cs)]

23. <span data-ttu-id="e7886-171">*[Crank. exe](signalr-connection-density-testing-with-crank.md)* , SignalR kod temeli ile birlikte sunulan bir bağlantı yoğunluğu test aracıdır.</span><span class="sxs-lookup"><span data-stu-id="e7886-171">*[Crank.exe](signalr-connection-density-testing-with-crank.md)* is a connection density testing tool provided with the SignalR codebase.</span></span> <span data-ttu-id="e7886-172">Crank kalıcı bir bağlantı gerektirdiğinden, test ederken kullanmak için sitenize bir tane ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e7886-172">Since Crank requires a persistent connection, you add one to your site for use when testing.</span></span> <span data-ttu-id="e7886-173">**WebRole1** projesine *Persistentconnections*adlı yeni bir klasör ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e7886-173">Add a new folder to the **WebRole1** project called *PersistentConnections*.</span></span> <span data-ttu-id="e7886-174">Bu klasöre sağ tıklayın ve > sınıfı **Ekle** 'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e7886-174">Right-click this folder and select **Add** > **Class**.</span></span> <span data-ttu-id="e7886-175">Yeni sınıf dosyasını *MyPersistentConnections.cs* olarak adlandırın ve **Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e7886-175">Name the new class file *MyPersistentConnections.cs* and select **Add**.</span></span>

24. <span data-ttu-id="e7886-176">Visual Studio, *MyPersistentConnections.cs* dosyasını ana pencerede açar.</span><span class="sxs-lookup"><span data-stu-id="e7886-176">Visual Studio will open the *MyPersistentConnections.cs* file in the main window.</span></span> <span data-ttu-id="e7886-177">İçeriği aşağıdaki kodla değiştirin, sonra dosyayı kaydedip kapatın:</span><span class="sxs-lookup"><span data-stu-id="e7886-177">Replace the contents with the following code, then save and close the file:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample8.cs)]

25. <span data-ttu-id="e7886-178">`Startup` sınıfını kullanarak, OWıN başlatıldığında SignalR nesneleri başlatılır.</span><span class="sxs-lookup"><span data-stu-id="e7886-178">Using the `Startup` class, the SignalR objects start when OWIN starts up.</span></span> <span data-ttu-id="e7886-179">*Startup.cs* açın veya oluşturun ve içeriğini şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="e7886-179">Open or create *Startup.cs* and replace the contents with the following code:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample9.cs)]

    <span data-ttu-id="e7886-180">Yukarıdaki kodda `OwinStartup` özniteliği, OWıN 'u başlatmak için bu sınıfı işaretler.</span><span class="sxs-lookup"><span data-stu-id="e7886-180">In the code above, the `OwinStartup` attribute marks this class to start OWIN.</span></span> <span data-ttu-id="e7886-181">`Configuration` yöntemi SignalR 'yi başlatır.</span><span class="sxs-lookup"><span data-stu-id="e7886-181">The `Configuration` method starts SignalR.</span></span>

26. <span data-ttu-id="e7886-182">**F5**tuşuna basarak Microsoft Azure öykünücüsü uygulamanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="e7886-182">Test your application in the Microsoft Azure Emulator by pressing **F5**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e7886-183">**Mapsignalr**'de bir **FileLoadException** ile karşılaşırsanız, *Web. config* dosyasındaki bağlama yeniden yönlendirmelerini aşağıdaki şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="e7886-183">If you encounter a **FileLoadException** at **MapSignalR**, change the binding redirects in *web.config* to the following:</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample12.xml?highlight=3,7)]

27. <span data-ttu-id="e7886-184">Bir dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="e7886-184">Wait about one minute.</span></span> <span data-ttu-id="e7886-185">Visual Studio 'da Cloud Explorer araç penceresini açın ( > **bulut Gezginini** **görüntüleyin** ) ve yolu `(Local)/Storage Accounts/(Development)/Tables`genişletin.</span><span class="sxs-lookup"><span data-stu-id="e7886-185">Open the Cloud Explorer tool window in Visual Studio (**View** > **Cloud Explorer**) and expand the path `(Local)/Storage Accounts/(Development)/Tables`.</span></span> <span data-ttu-id="e7886-186">**WADPerformanceCountersTable**çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e7886-186">Double-click **WADPerformanceCountersTable**.</span></span> <span data-ttu-id="e7886-187">Tablo verilerinde SignalR sayaçlarını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7886-187">You should see SignalR counters in the table data.</span></span> <span data-ttu-id="e7886-188">Tabloyu görmüyorsanız, Azure depolama kimlik bilgilerinizi yeniden girmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="e7886-188">If you don't see the table, you may need to re-enter your Azure Storage credentials.</span></span> <span data-ttu-id="e7886-189">Tabloyu **Cloud Explorer** 'da görmek için **Yenile** düğmesini seçmeniz veya tablodaki verileri görmek Için tablo aç penceresindeki **Yenile** düğmesini seçmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="e7886-189">You may need to select the **Refresh** button to see the table in **Cloud Explorer** or select the **Refresh** button in the open table window to see data in the table.</span></span>

    ![Visual Studio Cloud Explorer 'da WAD performans sayaçları tablosunu seçme](using-signalr-performance-counters-in-an-azure-web-role/_static/image11.png)

    ![WAD performans sayaçları tablosunda toplanan sayaçları gösterme](using-signalr-performance-counters-in-an-azure-web-role/_static/image12.png)

28. <span data-ttu-id="e7886-192">Uygulamanızı bulutta test etmek için, **ServiceConfiguration. Cloud. cscfg** dosyasını güncelleştirin ve `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` geçerli bir Azure depolama hesabı bağlantı dizesi olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e7886-192">To test your application in the cloud, update the **ServiceConfiguration.Cloud.cscfg** file and set the `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` to a valid Azure Storage account connection string.</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample10.xml)]

29. <span data-ttu-id="e7886-193">Uygulamayı Azure aboneliğinize dağıtın.</span><span class="sxs-lookup"><span data-stu-id="e7886-193">Deploy the application to your Azure subscription.</span></span> <span data-ttu-id="e7886-194">Bir uygulamayı Azure 'a dağıtma hakkında ayrıntılı bilgi için bkz. [bulut hizmeti oluşturma ve dağıtma](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span><span class="sxs-lookup"><span data-stu-id="e7886-194">For details on how to deploy an application to Azure, see [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span>

30. <span data-ttu-id="e7886-195">Birkaç dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="e7886-195">Wait a few minutes.</span></span> <span data-ttu-id="e7886-196">**Cloud Explorer**'da, yukarıda yapılandırdığınız depolama hesabını bulun ve içinde `WADPerformanceCountersTable` tablosunu bulun.</span><span class="sxs-lookup"><span data-stu-id="e7886-196">In **Cloud Explorer**, locate the storage account you configured above and find the `WADPerformanceCountersTable` table in it.</span></span> <span data-ttu-id="e7886-197">Tablo verilerinde SignalR sayaçlarını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7886-197">You should see SignalR counters in the table data.</span></span> <span data-ttu-id="e7886-198">Tabloyu görmüyorsanız, Azure depolama kimlik bilgilerinizi yeniden girmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="e7886-198">If you don't see the table, you may need to re-enter your Azure Storage credentials.</span></span> <span data-ttu-id="e7886-199">Tabloyu **Cloud Explorer** 'da görmek için **Yenile** düğmesini seçmeniz veya tablodaki verileri görmek Için tablo aç penceresindeki **Yenile** düğmesini seçmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="e7886-199">You may need to select the **Refresh** button to see the table in **Cloud Explorer** or select the **Refresh** button in the open table window to see data in the table.</span></span>

<span data-ttu-id="e7886-200">Bu öğreticide kullanılan özgün içerik için özel [Marrichard](https://social.msdn.microsoft.com/profile/Martin+Richard) 'e teşekkür ederiz.</span><span class="sxs-lookup"><span data-stu-id="e7886-200">Special thanks to [Martin Richard](https://social.msdn.microsoft.com/profile/Martin+Richard) for the original content used in this tutorial.</span></span>
