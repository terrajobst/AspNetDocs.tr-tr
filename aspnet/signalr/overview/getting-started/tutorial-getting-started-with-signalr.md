---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr
title: 'Öğretici: SignalR 2 ile gerçek zamanlı sohbet | Microsoft Docs'
author: bradygaster
description: Bu öğreticide SignalR kullanarak gerçek zamanlı bir sohbet uygulaması oluşturma işlemi gösterilir. SignalR 'yi boş bir ASP.NET Web uygulamasına eklersiniz.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: a8b3b778-f009-4369-85c7-e90f9878d8b4
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: bc4ef190b6e36812b6fe7ca4e16eb763431e0e82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536983"
---
# <a name="tutorial-real-time-chat-with-signalr-2"></a><span data-ttu-id="b405a-104">Öğretici: SignalR 2 ile gerçek zamanlı sohbet</span><span class="sxs-lookup"><span data-stu-id="b405a-104">Tutorial: Real-time chat with SignalR 2</span></span>

<span data-ttu-id="b405a-105">Bu öğreticide, SignalR kullanarak gerçek zamanlı bir sohbet uygulaması oluşturma işlemlerinin nasıl yapılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b405a-105">This tutorial shows you how to use SignalR to create a real-time chat application.</span></span> <span data-ttu-id="b405a-106">SignalR 'i boş bir ASP.NET Web uygulamasına eklersiniz ve ileti göndermek ve göstermek için bir HTML sayfası oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b405a-106">You add SignalR to an empty ASP.NET web application and create an HTML page to send and display messages.</span></span>

<span data-ttu-id="b405a-107">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="b405a-107">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b405a-108">Projeyi ayarlama</span><span class="sxs-lookup"><span data-stu-id="b405a-108">Set up the project</span></span>
> * <span data-ttu-id="b405a-109">Örneği çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b405a-109">Run the sample</span></span>
> * <span data-ttu-id="b405a-110">Kodu inceleme</span><span class="sxs-lookup"><span data-stu-id="b405a-110">Examine the code</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="b405a-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="b405a-111">Prerequisites</span></span>

* <span data-ttu-id="b405a-112">[ASP.NET ve web geliştirme](https://visualstudio.microsoft.com/downloads/) iş yüküyle **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="b405a-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="b405a-113">Projeyi ayarlama</span><span class="sxs-lookup"><span data-stu-id="b405a-113">Set up the Project</span></span>

<span data-ttu-id="b405a-114">Bu bölümde, boş bir ASP.NET Web uygulaması oluşturmak, SignalR eklemek ve sohbet uygulaması oluşturmak için Visual Studio 2017 ve SignalR 2 ' nin nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b405a-114">This section shows how to use Visual Studio 2017 and SignalR 2 to create an empty ASP.NET web application, add SignalR, and create the chat application.</span></span>

1. <span data-ttu-id="b405a-115">Visual Studio 'da bir ASP.NET Web uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b405a-115">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![Web oluştur](tutorial-getting-started-with-signalr/_static/image2.png)

1. <span data-ttu-id="b405a-117">**New ASP.NET Project-SignalRChat** penceresinde **boş** bırakın ve **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b405a-117">In the **New ASP.NET Project - SignalRChat** window, leave **Empty** selected and select **OK**.</span></span>

1. <span data-ttu-id="b405a-118">**Çözüm Gezgini**, projeye sağ tıklayın ve > **Yeni öğe** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="b405a-118">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="b405a-119">**Yeni öğe Ekle-signalrchat**' te, **yüklü** > **Visual C#**  > **Web** > **SignalR** ' i seçin ve ardından **SignalR hub sınıfı (v2)** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="b405a-119">In **Add New Item - SignalRChat**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="b405a-120">Sınıfı *ChatHub* olarak adlandırın ve projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b405a-120">Name the class *ChatHub* and add it to the project.</span></span>

    <span data-ttu-id="b405a-121">Bu adım, *ChatHub.cs* sınıf dosyasını oluşturur ve proje Için SignalR 'yi destekleyen bir betik dosyaları ve derleme başvuruları kümesi ekler.</span><span class="sxs-lookup"><span data-stu-id="b405a-121">This step creates the *ChatHub.cs* class file and adds a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="b405a-122">Yeni *ChatHub.cs* Class dosyasındaki kodu şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b405a-122">Replace the code in the new *ChatHub.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]

1. <span data-ttu-id="b405a-123">**Çözüm Gezgini**, projeye sağ tıklayın ve > **Yeni öğe** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="b405a-123">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="b405a-124">**Yeni öğe Ekle-signalrchat** ' in **yüklü** > **Visual C#**  > **Web** ' i seçip **owın başlangıç sınıfı**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="b405a-124">In **Add New Item - SignalRChat** select **Installed** > **Visual C#** > **Web**  and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="b405a-125">Sınıfın *başlangıcını* adlandırın ve projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b405a-125">Name the class *Startup* and add it to the project.</span></span>

1. <span data-ttu-id="b405a-126">*Başlangıç* sınıfındaki varsayılan kodu şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b405a-126">Replace the default code in *Startup* class with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="b405a-127">**Çözüm Gezgini**' de projeye sağ tıklayın ve > **HTML sayfası** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="b405a-127">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="b405a-128">Yeni sayfa *dizinini* adlandırın ve **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b405a-128">Name the new page *index* and select **OK**.</span></span>

1. <span data-ttu-id="b405a-129">**Çözüm Gezgini**, oluşturduğunuz HTML sayfasına sağ tıklayın ve **Başlangıç sayfası olarak ayarla**' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="b405a-129">In **Solution Explorer**, right-click the HTML page you created and select **Set as Start Page**.</span></span>

1. <span data-ttu-id="b405a-130">HTML sayfasındaki varsayılan kodu şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b405a-130">Replace the default code in the HTML page with this code:</span></span>

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]

1. <span data-ttu-id="b405a-131">**Çözüm Gezgini**' de **betikler**' ı genişletin.</span><span class="sxs-lookup"><span data-stu-id="b405a-131">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="b405a-132">JQuery ve SignalR için betik kitaplıkları projede görülebilir.</span><span class="sxs-lookup"><span data-stu-id="b405a-132">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b405a-133">Paket Yöneticisi, SignalR betiklerinin daha yeni bir sürümünü yüklemiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="b405a-133">The package manager may have installed a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="b405a-134">Kod bloğundaki betik başvurularının projedeki betik dosyalarının sürümlerine karşılık geldiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="b405a-134">Check that the script references in the code block correspond to the versions of the script files in the project.</span></span>

    <span data-ttu-id="b405a-135">Özgün kod bloğundan gelen betik başvuruları:</span><span class="sxs-lookup"><span data-stu-id="b405a-135">Script references from the original code block:</span></span>

    ```html
    <!--Script references. -->
    <!--Reference the jQuery library. -->
    <script src="Scripts/jquery-3.1.1.min.js" ></script>
    <!--Reference the SignalR library. -->
    <script src="Scripts/jquery.signalR-2.2.1.min.js"></script>
    ```

1. <span data-ttu-id="b405a-136">Eşleşiyorlarsa, *. html* dosyasını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="b405a-136">If they don't match, update the *.html* file.</span></span>

1. <span data-ttu-id="b405a-137">Menü çubuğundan **dosya** > **Tümünü Kaydet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="b405a-137">From the menu bar, select **File** > **Save All**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="b405a-138">Örneği çalıştırın</span><span class="sxs-lookup"><span data-stu-id="b405a-138">Run the Sample</span></span>

1. <span data-ttu-id="b405a-139">Araç çubuğunda, **betik hata ayıklamayı** açın ve ardından yürütme düğmesini seçerek örneği hata ayıklama modunda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b405a-139">In the toolbar, turn on **Script Debugging** and then select the play button to run the sample in Debug mode.</span></span>

    ![Kullanıcı adını girin](tutorial-getting-started-with-signalr/_static/image3.png)

1. <span data-ttu-id="b405a-141">Tarayıcı açıldığında, sohbet Kimliğiniz için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="b405a-141">When the browser opens, enter a name for your chat identity.</span></span>

1. <span data-ttu-id="b405a-142">Tarayıcıdan URL 'YI kopyalayın, iki farklı tarayıcı açın ve adres çubuklarına URL 'Leri yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b405a-142">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="b405a-143">Her tarayıcıda benzersiz bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="b405a-143">In each browser, enter a unique name.</span></span>

1. <span data-ttu-id="b405a-144">Şimdi bir açıklama ekleyin ve **Gönder**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="b405a-144">Now, add a comment and select **Send**.</span></span> <span data-ttu-id="b405a-145">Bunu diğer tarayıcılarda yineleyin.</span><span class="sxs-lookup"><span data-stu-id="b405a-145">Repeat that in the other browsers.</span></span> <span data-ttu-id="b405a-146">Açıklamalar gerçek zamanlı olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="b405a-146">The comments appear in real-time.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b405a-147">Bu basit sohbet uygulaması, sunucuda tartışma bağlamını korumaz.</span><span class="sxs-lookup"><span data-stu-id="b405a-147">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="b405a-148">Merkez tüm geçerli kullanıcılara yorum yayınlar.</span><span class="sxs-lookup"><span data-stu-id="b405a-148">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="b405a-149">Daha sonra sohbete katılması olan kullanıcılar, bu kişilerin eklendiği zamandan eklenen iletileri görür.</span><span class="sxs-lookup"><span data-stu-id="b405a-149">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="b405a-150">Sohbet uygulamasının üç farklı tarayıcıda nasıl çalıştığını görün.</span><span class="sxs-lookup"><span data-stu-id="b405a-150">See how the chat application runs in three different browsers.</span></span> <span data-ttu-id="b405a-151">Tom, anve, ve Çiğdem iletileri gönderirken tüm tarayıcıların gerçek zamanlı olarak güncelleştirilmesi:</span><span class="sxs-lookup"><span data-stu-id="b405a-151">When Tom, Anand, and Susan send messages, all browsers update in real time:</span></span>

    ![Üç tarayıcıda da aynı sohbet geçmişi görüntülenir](tutorial-getting-started-with-signalr/_static/image4.png)

1. <span data-ttu-id="b405a-153">**Çözüm Gezgini**, çalışan uygulamanın **komut dosyası belgeleri** düğümünü inceleyin.</span><span class="sxs-lookup"><span data-stu-id="b405a-153">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="b405a-154">SignalR kitaplığının çalışma zamanında oluşturduğu *Hublar* adlı bir betik dosyası vardır.</span><span class="sxs-lookup"><span data-stu-id="b405a-154">There's a script file named *hubs* that the SignalR library generates at runtime.</span></span> <span data-ttu-id="b405a-155">Bu dosya jQuery betiği ile sunucu tarafı kodu arasındaki iletişimi yönetir.</span><span class="sxs-lookup"><span data-stu-id="b405a-155">This file manages the communication between jQuery script and server-side code.</span></span>

    ![Betik belgeleri düğümünde otomatik olarak oluşturulan hub betiği](tutorial-getting-started-with-signalr/_static/image5.png)

## <a name="examine-the-code"></a><span data-ttu-id="b405a-157">Kodu inceleyin</span><span class="sxs-lookup"><span data-stu-id="b405a-157">Examine the Code</span></span>

<span data-ttu-id="b405a-158">SignalRChat uygulaması iki temel SignalR geliştirme görevi gösterir.</span><span class="sxs-lookup"><span data-stu-id="b405a-158">The SignalRChat application demonstrates two basic SignalR development tasks.</span></span> <span data-ttu-id="b405a-159">Bir hub oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="b405a-159">It shows you how to create a hub.</span></span> <span data-ttu-id="b405a-160">Sunucu, ana düzenleme nesnesi olarak bu hub 'ı kullanır.</span><span class="sxs-lookup"><span data-stu-id="b405a-160">The server uses that hub as the main coordination object.</span></span> <span data-ttu-id="b405a-161">Hub, ileti göndermek ve almak için SignalR jQuery kitaplığını kullanır.</span><span class="sxs-lookup"><span data-stu-id="b405a-161">The hub uses the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs-in-the-chathubcs"></a><span data-ttu-id="b405a-162">ChatHub.cs 'de SignalR hub 'Ları</span><span class="sxs-lookup"><span data-stu-id="b405a-162">SignalR Hubs in the ChatHub.cs</span></span>

<span data-ttu-id="b405a-163">Yukarıdaki kod örneğinde, `ChatHub` sınıfı `Microsoft.AspNet.SignalR.Hub` sınıfından türetilir.</span><span class="sxs-lookup"><span data-stu-id="b405a-163">In the code sample above, the `ChatHub` class derives from the `Microsoft.AspNet.SignalR.Hub` class.</span></span> <span data-ttu-id="b405a-164">`Hub` sınıfından türetmek, bir SignalR uygulaması oluşturmanın kullanışlı bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="b405a-164">Deriving from the `Hub` class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="b405a-165">Hub sınıfınız üzerinde ortak Yöntemler oluşturabilir ve sonra bu yöntemleri bir Web sayfasındaki betiklerden çağırarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b405a-165">You can create public methods on your hub class and then use those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="b405a-166">Sohbet kodunda, istemciler yeni bir ileti göndermek için `ChatHub.Send` yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="b405a-166">In the chat code, clients call the `ChatHub.Send` method to send a new message.</span></span> <span data-ttu-id="b405a-167">Merkez daha sonra `Clients.All.broadcastMessage`çağırarak iletiyi tüm istemcilere gönderir.</span><span class="sxs-lookup"><span data-stu-id="b405a-167">The hub then sends the message to all clients by calling `Clients.All.broadcastMessage`.</span></span>

<span data-ttu-id="b405a-168">`Send` yöntemi çeşitli Merkez kavramlarını gösterir:</span><span class="sxs-lookup"><span data-stu-id="b405a-168">The `Send` method demonstrates several hub concepts:</span></span>

* <span data-ttu-id="b405a-169">İstemcilerin bunları çağırabilmesi için ortak yöntemleri bir hub üzerinde bildirin.</span><span class="sxs-lookup"><span data-stu-id="b405a-169">Declare public methods on a hub so that clients can call them.</span></span>

* <span data-ttu-id="b405a-170">Bu hub 'a bağlı tüm istemcilerle iletişim kurmak için `Microsoft.AspNet.SignalR.Hub.Clients` Dynamic özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="b405a-170">Use the `Microsoft.AspNet.SignalR.Hub.Clients` dynamic property to communicate with all clients connected to this hub.</span></span>

* <span data-ttu-id="b405a-171">İstemcileri güncelleştirmek için istemcide bir işlev (`broadcastMessage` işlevi gibi) çağırın.</span><span class="sxs-lookup"><span data-stu-id="b405a-171">Call a function on the client (like the `broadcastMessage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery-in-the-indexhtml"></a><span data-ttu-id="b405a-172">Dizin. html dosyasındaki SignalR ve jQuery</span><span class="sxs-lookup"><span data-stu-id="b405a-172">SignalR and jQuery in the index.html</span></span>

<span data-ttu-id="b405a-173">Kod örneğindeki *index. html* sayfası, bir SignalR hub 'ı ile iletişim kurmak Için SignalR jQuery kitaplığını nasıl kullanacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="b405a-173">The *index.html* page in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="b405a-174">Kod birçok önemli görevi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="b405a-174">The code carries out many important tasks.</span></span> <span data-ttu-id="b405a-175">Hub 'a başvurmak için bir proxy bildirir, sunucunun istemcilere içerik göndermek için çağıradığına yönelik bir işlev bildirir ve hub 'a ileti göndermeye yönelik bir bağlantı başlatır.</span><span class="sxs-lookup"><span data-stu-id="b405a-175">It declares a proxy to reference the hub, declares a function that the server can call to push content to clients, and it starts a connection to send messages to the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> <span data-ttu-id="b405a-176">JavaScript 'te, sunucu sınıfına ve üyelerine yönelik başvurunun camelCase olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="b405a-176">In JavaScript the reference to the server class and its members has to be camelCase.</span></span> <span data-ttu-id="b405a-177">Kod örneği, JavaScript 'teki C# *ChatHub* sınıfına `chatHub`olarak başvurur.</span><span class="sxs-lookup"><span data-stu-id="b405a-177">The code sample references the C# *ChatHub* class in JavaScript as `chatHub`.</span></span>

<span data-ttu-id="b405a-178">Bu kod bloğunda, betikte bir geri çağırma işlevi oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="b405a-178">In this code block, you create a callback function in the script.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

<span data-ttu-id="b405a-179">Sunucu üzerindeki hub sınıfı, içerik güncelleştirmelerini her bir istemciye göndermek için bu işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="b405a-179">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="b405a-180">HTML-içeriği görüntülemeden önce kodlayan iki satır isteğe bağlıdır ve betik ekleme işlemini önlemenin iyi bir yolunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="b405a-180">The two lines that HTML-encode the content before displaying it are optional and show a good way to prevent script injection.</span></span>

<span data-ttu-id="b405a-181">Bu kod, hub ile bir bağlantı açar.</span><span class="sxs-lookup"><span data-stu-id="b405a-181">This code opens a connection with the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

> [!NOTE]
> <span data-ttu-id="b405a-182">Bu yaklaşım, olay işleyicisi yürütmeden önce kodun bir bağlantı kurmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="b405a-182">This approach ensures that the code establishes a connection before the event handler executes.</span></span>

<span data-ttu-id="b405a-183">Kod bağlantıyı başlatır ve sonra HTML sayfasındaki **Gönder** düğmesine tıklama olayını işlemek için bir işlev geçirir.</span><span class="sxs-lookup"><span data-stu-id="b405a-183">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the HTML page.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="b405a-184">Kodu alma</span><span class="sxs-lookup"><span data-stu-id="b405a-184">Get the code</span></span>

[<span data-ttu-id="b405a-185">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="b405a-185">Download Completed Project</span></span>](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)

## <a name="additional-resources"></a><span data-ttu-id="b405a-186">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b405a-186">Additional resources</span></span>

<span data-ttu-id="b405a-187">SignalR hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="b405a-187">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="b405a-188">SignalR projesi</span><span class="sxs-lookup"><span data-stu-id="b405a-188">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="b405a-189">SignalR GitHub ve örnekleri</span><span class="sxs-lookup"><span data-stu-id="b405a-189">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="b405a-190">SignalR wiki</span><span class="sxs-lookup"><span data-stu-id="b405a-190">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="b405a-191">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b405a-191">Next steps</span></span>

<span data-ttu-id="b405a-192">Bu öğreticide şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b405a-192">In this tutorial you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b405a-193">Projeyi ayarlama</span><span class="sxs-lookup"><span data-stu-id="b405a-193">Set up the project</span></span>
> * <span data-ttu-id="b405a-194">Örneği çalıştırdı</span><span class="sxs-lookup"><span data-stu-id="b405a-194">Ran the sample</span></span>
> * <span data-ttu-id="b405a-195">Kod incelendi</span><span class="sxs-lookup"><span data-stu-id="b405a-195">Examined the code</span></span>

<span data-ttu-id="b405a-196">SignalR ve MVC 5 ' i nasıl kullanacağınızı öğrenmek için sonraki makaleye ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="b405a-196">Advance to the next article to learn how to use SignalR and MVC 5.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b405a-197">SignalR 2 ve MVC 5</span><span class="sxs-lookup"><span data-stu-id="b405a-197">SignalR 2 and MVC 5</span></span>](tutorial-getting-started-with-signalr-and-mvc.md)