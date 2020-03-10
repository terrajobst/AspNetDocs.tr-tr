---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
title: 'Öğretici: SignalR 2 ve MVC 5 ile gerçek zamanlı sohbet | Microsoft Docs'
author: bradygaster
description: Bu öğreticide, gerçek zamanlı bir sohbet uygulaması oluşturmak için ASP.NET SignalR 2 ' nin nasıl kullanılacağı gösterilmektedir. SignalR 'yi MVC 5 uygulamasına eklersiniz.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 80bfe5fb-bdfc-41fe-ac43-2132e5d69fac
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 5671e4f0123ca2b0cb5314336cf4411467feac70
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78537046"
---
# <a name="tutorial-real-time-chat-with-signalr-2-and-mvc-5"></a><span data-ttu-id="3991c-104">Öğretici: SignalR 2 ve MVC 5 ile gerçek zamanlı sohbet</span><span class="sxs-lookup"><span data-stu-id="3991c-104">Tutorial: Real-time chat with SignalR 2 and MVC 5</span></span>

<span data-ttu-id="3991c-105">Bu öğreticide, gerçek zamanlı bir sohbet uygulaması oluşturmak için ASP.NET SignalR 2 ' nin nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3991c-105">This tutorial shows how to use ASP.NET SignalR 2 to create a real-time chat application.</span></span> <span data-ttu-id="3991c-106">Bir MVC 5 uygulamasına SignalR ekleyin ve ileti göndermek ve görüntülemek için bir sohbet görünümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3991c-106">You add SignalR to an MVC 5 application and create a chat view to send and display messages.</span></span>

<span data-ttu-id="3991c-107">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="3991c-107">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3991c-108">Projeyi ayarlama</span><span class="sxs-lookup"><span data-stu-id="3991c-108">Set up the project</span></span>
> * <span data-ttu-id="3991c-109">Örneği çalıştırma</span><span class="sxs-lookup"><span data-stu-id="3991c-109">Run the sample</span></span>
> * <span data-ttu-id="3991c-110">Kodu inceleme</span><span class="sxs-lookup"><span data-stu-id="3991c-110">Examine the code</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="3991c-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="3991c-111">Prerequisites</span></span>

* <span data-ttu-id="3991c-112">[ASP.NET ve web geliştirme](https://visualstudio.microsoft.com/downloads/) iş yüküyle **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="3991c-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="3991c-113">Projeyi ayarlama</span><span class="sxs-lookup"><span data-stu-id="3991c-113">Set up the Project</span></span>

<span data-ttu-id="3991c-114">Bu bölümde, Visual Studio 2017 ve SignalR 2 kullanarak boş bir ASP.NET MVC 5 uygulaması oluşturma, SignalR kitaplığını ekleme ve sohbet uygulaması oluşturma işlemlerinin nasıl yapılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3991c-114">This section shows how to use Visual Studio 2017 and SignalR 2 to create an empty ASP.NET MVC 5 application, add the SignalR library, and create the chat application.</span></span>

1. <span data-ttu-id="3991c-115">Visual Studio 'da .NET Framework 4,5 ' C# i hedefleyen bir ASP.NET uygulaması oluşturun, bunu SignalRChat olarak adlandırın ve Tamam ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3991c-115">In Visual Studio, create a C# ASP.NET application that targets .NET Framework 4.5, name it SignalRChat, and click OK.</span></span>

    ![Web oluştur](tutorial-getting-started-with-signalr-and-mvc/_static/image1.png)

1. <span data-ttu-id="3991c-117">**Yeni ASP.NET Web uygulaması-SignalRMvcChat**' de **MVC** ' yi ve ardından **kimlik doğrulamasını Değiştir**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="3991c-117">In **New ASP.NET Web Application - SignalRMvcChat**, select **MVC** and then select **Change Authentication**.</span></span>

1. <span data-ttu-id="3991c-118">**Kimlik doğrulamasını Değiştir**' de **kimlik doğrulaması yok** ' u ve **Tamam**' ı tıklatın</span><span class="sxs-lookup"><span data-stu-id="3991c-118">In **Change Authentication**, select **No Authentication** and click **OK**.</span></span>

    ![Kimlik doğrulaması yok seçin](tutorial-getting-started-with-signalr-and-mvc/_static/image2.png)

1. <span data-ttu-id="3991c-120">**Yeni ASP.NET Web uygulaması-SignalRMvcChat**' de **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="3991c-120">In **New ASP.NET Web Application - SignalRMvcChat**, select **OK**.</span></span>

1. <span data-ttu-id="3991c-121">**Çözüm Gezgini**, projeye sağ tıklayın ve > **Yeni öğe** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="3991c-121">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="3991c-122">**Yeni öğe Ekle-signalrchat**' te, **yüklü** > **Visual C#**  > **Web** > **SignalR** ' i seçin ve ardından **SignalR hub sınıfı (v2)** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="3991c-122">In **Add New Item - SignalRChat**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="3991c-123">Sınıfı *ChatHub* olarak adlandırın ve projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3991c-123">Name the class *ChatHub* and add it to the project.</span></span>

    <span data-ttu-id="3991c-124">Bu adım, *ChatHub.cs* sınıf dosyasını oluşturur ve proje Için SignalR 'yi destekleyen bir betik dosyaları ve derleme başvuruları kümesi ekler.</span><span class="sxs-lookup"><span data-stu-id="3991c-124">This step creates the *ChatHub.cs* class file and adds a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="3991c-125">Yeni *ChatHub.cs* Class dosyasındaki kodu şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="3991c-125">Replace the code in the new *ChatHub.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample1.cs)]

1. <span data-ttu-id="3991c-126">**Çözüm Gezgini**, projeye sağ tıklayın ve > **sınıfı** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="3991c-126">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="3991c-127">Yeni sınıf *başlangıcını* adlandırın ve projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3991c-127">Name the new class *Startup* and add it to the project.</span></span>

1. <span data-ttu-id="3991c-128">*Startup.cs* Class dosyasındaki kodu şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="3991c-128">Replace the code in the *Startup.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample2.cs)]

1. <span data-ttu-id="3991c-129">**Çözüm Gezgini**, **denetleyiciler** > **HomeController.cs**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="3991c-129">In **Solution Explorer**, select **Controllers** > **HomeController.cs**.</span></span>

1. <span data-ttu-id="3991c-130">Bu yöntemi *HomeController.cs*ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3991c-130">Add this method to the *HomeController.cs*.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample3.cs)]

    <span data-ttu-id="3991c-131">Bu yöntem, daha sonraki bir adımda oluşturduğunuz **sohbet** görünümünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="3991c-131">This method returns the **Chat** view that you create in a later step.</span></span>

1. <span data-ttu-id="3991c-132">**Çözüm Gezgini**' de, **Görünümler** > **giriş**' e sağ tıklayın ve >  **Görünüm** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="3991c-132">In **Solution Explorer**, right-click **Views** > **Home**, and select **Add** >  **View**.</span></span>

1. <span data-ttu-id="3991c-133">**Görünüm Ekle**' de, yeni görünüm **sohbeti** ' nı adlandırın ve **Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="3991c-133">In **Add View**, name the new view **Chat** and select **Add**.</span></span>

1. <span data-ttu-id="3991c-134">**Chat. cshtml** içeriğini şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="3991c-134">Replace the contents of **Chat.cshtml** with this code:</span></span>

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample4.cshtml)]

1. <span data-ttu-id="3991c-135">**Çözüm Gezgini**' de **betikler**' ı genişletin.</span><span class="sxs-lookup"><span data-stu-id="3991c-135">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="3991c-136">JQuery ve SignalR için betik kitaplıkları projede görülebilir.</span><span class="sxs-lookup"><span data-stu-id="3991c-136">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="3991c-137">Paket Yöneticisi, SignalR betiklerinin daha yeni bir sürümünü yüklemiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="3991c-137">The package manager may have installed a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="3991c-138">Kod bloğundaki betik başvurularının projedeki betik dosyalarının sürümlerine karşılık geldiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="3991c-138">Check that the script references in the code block correspond to the versions of the script files in the project.</span></span>

    <span data-ttu-id="3991c-139">Özgün kod bloğundan gelen betik başvuruları:</span><span class="sxs-lookup"><span data-stu-id="3991c-139">Script references from the original code block:</span></span>

    ```cshtml
    <!--Script references. -->
    <!--The jQuery library is required and is referenced by default in _Layout.cshtml. -->
    <!--Reference the SignalR library. -->
    <script src="~/Scripts/jquery.signalR-2.1.0.min.js"></script>
    ```

1. <span data-ttu-id="3991c-140">Eşleşmiyorsa, *. cshtml* dosyasını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="3991c-140">If they don't match, update the *.cshtml* file.</span></span>

1. <span data-ttu-id="3991c-141">Menü çubuğundan **dosya** > **Tümünü Kaydet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="3991c-141">From the menu bar, select **File** > **Save All**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="3991c-142">Örneği çalıştırın</span><span class="sxs-lookup"><span data-stu-id="3991c-142">Run the Sample</span></span>

1. <span data-ttu-id="3991c-143">Araç çubuğunda, **betik hata ayıklamayı** açın ve ardından yürütme düğmesini seçerek örneği hata ayıklama modunda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3991c-143">In the toolbar, turn on **Script Debugging** and then select the play button to run the sample in Debug mode.</span></span>

    ![Kullanıcı adını girin](tutorial-getting-started-with-signalr-and-mvc/_static/image3.png)

1. <span data-ttu-id="3991c-145">Tarayıcı açıldığında, sohbet Kimliğiniz için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="3991c-145">When the browser opens, enter a name for your chat identity.</span></span>

1. <span data-ttu-id="3991c-146">Tarayıcıdan URL 'YI kopyalayın, iki farklı tarayıcı açın ve adres çubuklarına URL 'Leri yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="3991c-146">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="3991c-147">Her tarayıcıda benzersiz bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="3991c-147">In each browser, enter a unique name.</span></span>

1. <span data-ttu-id="3991c-148">Şimdi bir açıklama ekleyin ve **Gönder**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="3991c-148">Now, add a comment and select **Send**.</span></span> <span data-ttu-id="3991c-149">Bunu diğer tarayıcılarda yineleyin.</span><span class="sxs-lookup"><span data-stu-id="3991c-149">Repeat that in the other browsers.</span></span> <span data-ttu-id="3991c-150">Açıklamalar gerçek zamanlı olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="3991c-150">The comments appear in real time.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3991c-151">Bu basit sohbet uygulaması, sunucuda tartışma bağlamını korumaz.</span><span class="sxs-lookup"><span data-stu-id="3991c-151">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="3991c-152">Merkez tüm geçerli kullanıcılara yorum yayınlar.</span><span class="sxs-lookup"><span data-stu-id="3991c-152">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="3991c-153">Daha sonra sohbete katılması olan kullanıcılar, bu kişilerin eklendiği zamandan eklenen iletileri görür.</span><span class="sxs-lookup"><span data-stu-id="3991c-153">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="3991c-154">Sohbet uygulamasının üç farklı tarayıcıda nasıl çalıştığını görün.</span><span class="sxs-lookup"><span data-stu-id="3991c-154">See how the chat application runs in three different browsers.</span></span> <span data-ttu-id="3991c-155">Tom, anve, ve Çiğdem iletileri gönderirken tüm tarayıcıların gerçek zamanlı olarak güncelleştirilmesi:</span><span class="sxs-lookup"><span data-stu-id="3991c-155">When Tom, Anand, and Susan send messages, all browsers update in real time:</span></span>

    ![Üç tarayıcıda da aynı sohbet geçmişi görüntülenir](tutorial-getting-started-with-signalr-and-mvc/_static/image4.png)

1. <span data-ttu-id="3991c-157">**Çözüm Gezgini**, çalışan uygulamanın **komut dosyası belgeleri** düğümünü inceleyin.</span><span class="sxs-lookup"><span data-stu-id="3991c-157">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="3991c-158">SignalR kitaplığının çalışma zamanında oluşturduğu *Hublar* adlı bir betik dosyası vardır.</span><span class="sxs-lookup"><span data-stu-id="3991c-158">There's a script file named *hubs* that the SignalR library generates at runtime.</span></span> <span data-ttu-id="3991c-159">Bu dosya jQuery betiği ile sunucu tarafı kodu arasındaki iletişimi yönetir.</span><span class="sxs-lookup"><span data-stu-id="3991c-159">This file manages the communication between jQuery script and server-side code.</span></span>

    ![Betik belgeleri düğümünde otomatik olarak oluşturulan hub betiği](tutorial-getting-started-with-signalr-and-mvc/_static/image5.png)

## <a name="examine-the-code"></a><span data-ttu-id="3991c-161">Kodu inceleyin</span><span class="sxs-lookup"><span data-stu-id="3991c-161">Examine the Code</span></span>

<span data-ttu-id="3991c-162">SignalR sohbet uygulaması iki temel SignalR geliştirme görevi gösterir.</span><span class="sxs-lookup"><span data-stu-id="3991c-162">The SignalR chat application demonstrates two basic SignalR development tasks.</span></span> <span data-ttu-id="3991c-163">Bir hub oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="3991c-163">It shows you how to create a hub.</span></span> <span data-ttu-id="3991c-164">Sunucu, ana düzenleme nesnesi olarak bu hub 'ı kullanır.</span><span class="sxs-lookup"><span data-stu-id="3991c-164">The server uses that hub as the main coordination object.</span></span> <span data-ttu-id="3991c-165">Hub, ileti göndermek ve almak için SignalR jQuery kitaplığını kullanır.</span><span class="sxs-lookup"><span data-stu-id="3991c-165">The hub uses the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs-in-the-chathubcs"></a><span data-ttu-id="3991c-166">ChatHub.cs 'de SignalR hub 'Ları</span><span class="sxs-lookup"><span data-stu-id="3991c-166">SignalR Hubs in the ChatHub.cs</span></span>

<span data-ttu-id="3991c-167">Kod örneğinde, `ChatHub` sınıfı `Microsoft.AspNet.SignalR.Hub` sınıfından türetilir.</span><span class="sxs-lookup"><span data-stu-id="3991c-167">In the code sample, the `ChatHub` class derives from the `Microsoft.AspNet.SignalR.Hub` class.</span></span> <span data-ttu-id="3991c-168">`Hub` sınıfından türetmek, bir SignalR uygulaması oluşturmanın kullanışlı bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="3991c-168">Deriving from the `Hub` class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="3991c-169">Hub sınıfınız üzerinde ortak Yöntemler oluşturabilir ve ardından bunları bir Web sayfasındaki betiklerden çağırarak bu yöntemlere erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3991c-169">You can create public methods on your hub class and then access those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="3991c-170">Sohbet kodunda, istemciler yeni bir ileti göndermek için `ChatHub.Send` yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="3991c-170">In the chat code, clients call the `ChatHub.Send` method to send a new message.</span></span> <span data-ttu-id="3991c-171">İçindeki hub, `Clients.All.addNewMessageToPage`çağırarak iletiyi tüm istemcilere gönderir.</span><span class="sxs-lookup"><span data-stu-id="3991c-171">The hub in turn sends the message to all clients by calling `Clients.All.addNewMessageToPage`.</span></span>

<span data-ttu-id="3991c-172">`Send` yöntemi çeşitli Merkez kavramlarını gösterir:</span><span class="sxs-lookup"><span data-stu-id="3991c-172">The `Send` method demonstrates several hub concepts:</span></span>

* <span data-ttu-id="3991c-173">İstemcilerin bunları çağırabilmesi için ortak yöntemleri bir hub üzerinde bildirin.</span><span class="sxs-lookup"><span data-stu-id="3991c-173">Declare public methods on a hub so that clients can call them.</span></span>

* <span data-ttu-id="3991c-174">Bu hub 'a bağlı tüm istemcilerle iletişim kurmak için `Microsoft.AspNet.SignalR.Hub.Clients` Dynamic özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="3991c-174">Use the `Microsoft.AspNet.SignalR.Hub.Clients` dynamic property to communicate with all clients connected to this hub.</span></span>

* <span data-ttu-id="3991c-175">İstemcileri güncelleştirmek için istemcide bir işlev (`addNewMessageToPage` işlevi gibi) çağırın.</span><span class="sxs-lookup"><span data-stu-id="3991c-175">Call a function on the client (like the `addNewMessageToPage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample5.cs)]

### <a name="signalr-and-jquery-chatcshtml"></a><span data-ttu-id="3991c-176">SignalR ve jQuery sohbeti. cshtml</span><span class="sxs-lookup"><span data-stu-id="3991c-176">SignalR and jQuery Chat.cshtml</span></span>

<span data-ttu-id="3991c-177">Kod örneğindeki *chat. cshtml* görünüm dosyası bir SignalR hub 'ı ile iletişim kurmak Için SignalR jQuery kitaplığını nasıl kullanacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="3991c-177">The *Chat.cshtml* view file in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span>  <span data-ttu-id="3991c-178">Kod birçok önemli görevi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="3991c-178">The code carries out many important tasks.</span></span> <span data-ttu-id="3991c-179">Hub için otomatik olarak oluşturulan ara sunucuya bir başvuru oluşturur, sunucunun istemcilere içerik göndermek için çağıradığına yönelik bir işlev bildirir ve hub 'a ileti göndermek için bir bağlantı başlatır.</span><span class="sxs-lookup"><span data-stu-id="3991c-179">It creates a reference to the autogenerated proxy for the hub, declares a function that the server can call to push content to clients, and it starts a connection to send messages to the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="3991c-180">JavaScript 'te, sunucu sınıfına ve üyelerine yönelik başvuru camelCase ' de bulunur.</span><span class="sxs-lookup"><span data-stu-id="3991c-180">In JavaScript, the reference to the server class and its members is in camelCase.</span></span> <span data-ttu-id="3991c-181">Kod örneği, JavaScript 'teki C# `ChatHub` sınıfına `chatHub`olarak başvurur.</span><span class="sxs-lookup"><span data-stu-id="3991c-181">The code sample references the C# `ChatHub` class in JavaScript as `chatHub`.</span></span>

<span data-ttu-id="3991c-182">Bu kod bloğunda, betikte bir geri çağırma işlevi oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="3991c-182">In this code block, you create a callback function in the script.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample7.html)]

<span data-ttu-id="3991c-183">Sunucu üzerindeki hub sınıfı, içerik güncelleştirmelerini her bir istemciye göndermek için bu işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="3991c-183">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="3991c-184">`htmlEncode` işlevine yönelik isteğe bağlı çağrı, sayfada görüntülemeden önce ileti içeriğini HTML olarak kodlamak için bir yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="3991c-184">The optional call to the `htmlEncode` function shows a way to HTML encode the message content before displaying it in the page.</span></span> <span data-ttu-id="3991c-185">Betik ekleme işlemini önlemenin bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="3991c-185">It's a way to prevent script injection.</span></span>

<span data-ttu-id="3991c-186">Bu kod, hub ile bir bağlantı açar.</span><span class="sxs-lookup"><span data-stu-id="3991c-186">This code opens a connection with the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample8.js)]

> [!NOTE]
> <span data-ttu-id="3991c-187">Bu yaklaşım, olay işleyicisi yürütmeden önce bir bağlantı oluşturmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="3991c-187">This approach ensures that you establish a connection before the event handler executes.</span></span>

<span data-ttu-id="3991c-188">Kod bağlantıyı başlatır ve ardından sohbet sayfasındaki **Gönder** düğmesine tıklama olayını işlemek için bir işlev geçirir.</span><span class="sxs-lookup"><span data-stu-id="3991c-188">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the Chat page.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="3991c-189">Kodu alma</span><span class="sxs-lookup"><span data-stu-id="3991c-189">Get the code</span></span>

[<span data-ttu-id="3991c-190">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="3991c-190">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-c366b2f3)

## <a name="additional-resources"></a><span data-ttu-id="3991c-191">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="3991c-191">Additional resources</span></span>

<span data-ttu-id="3991c-192">SignalR hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="3991c-192">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="3991c-193">SignalR projesi</span><span class="sxs-lookup"><span data-stu-id="3991c-193">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="3991c-194">SignalR GitHub ve örnekleri</span><span class="sxs-lookup"><span data-stu-id="3991c-194">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="3991c-195">SignalR wiki</span><span class="sxs-lookup"><span data-stu-id="3991c-195">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="3991c-196">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3991c-196">Next steps</span></span>

<span data-ttu-id="3991c-197">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="3991c-197">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3991c-198">Projeyi ayarlama</span><span class="sxs-lookup"><span data-stu-id="3991c-198">Set up the project</span></span>
> * <span data-ttu-id="3991c-199">Örneği çalıştırdı</span><span class="sxs-lookup"><span data-stu-id="3991c-199">Ran the sample</span></span>
> * <span data-ttu-id="3991c-200">Kod incelendi</span><span class="sxs-lookup"><span data-stu-id="3991c-200">Examined the code</span></span>

<span data-ttu-id="3991c-201">Yüksek frekanslı mesajlaşma işlevselliği sağlamak için ASP.NET SignalR 2 kullanan bir Web uygulamasının nasıl oluşturulacağını öğrenmek için sonraki makaleye ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="3991c-201">Advance to the next article to learn how to create a web application that uses ASP.NET SignalR 2 to provide high-frequency messaging functionality.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="3991c-202">Yüksek frekanslı mesajlaşma ile Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="3991c-202">Web app with high-frequency messaging</span></span>](tutorial-high-frequency-realtime-with-signalr.md)