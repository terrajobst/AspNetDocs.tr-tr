---
uid: signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
title: 'Öğretici: SignalR 2 ile yüksek frekanslı gerçek zamanlı uygulama oluşturma | Microsoft Docs'
author: bradygaster
description: Bu öğreticide, yüksek frekanslı mesajlaşma işlevselliği sağlamak için ASP.NET SignalR kullanan bir Web uygulamasının nasıl oluşturulacağı gösterilmektedir.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 9f969dda-78ea-4329-b1e3-e51c02210a2b
msc.legacyurl: /signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 2503e90735d6cfa445ee08c9e43f8443aa106096
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600448"
---
# <a name="tutorial-create-high-frequency-real-time-app-with-signalr-2"></a><span data-ttu-id="748d7-103">Öğretici: SignalR 2 ile yüksek frekanslı gerçek zamanlı uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="748d7-103">Tutorial: Create high-frequency real-time app with SignalR 2</span></span>

<span data-ttu-id="748d7-104">Bu öğreticide, yüksek frekanslı mesajlaşma işlevselliği sağlamak için ASP.NET SignalR 2 kullanan bir Web uygulamasının nasıl oluşturulacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="748d7-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide high-frequency messaging functionality.</span></span> <span data-ttu-id="748d7-105">Bu durumda, "yüksek frekanslı mesajlaşma", sunucunun güncelleştirmeleri sabit bir hızda göndermesi anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="748d7-105">In this case, "high-frequency messaging" means the server sends updates at a fixed rate.</span></span> <span data-ttu-id="748d7-106">Saniyede en fazla 10 ileti gönderirsiniz.</span><span class="sxs-lookup"><span data-stu-id="748d7-106">You send up to 10 messages a second.</span></span>

<span data-ttu-id="748d7-107">Oluşturduğunuz uygulama, kullanıcıların sürükleyebilmesi için bir şekil görüntüler.</span><span class="sxs-lookup"><span data-stu-id="748d7-107">The application you create displays a shape that users can drag.</span></span> <span data-ttu-id="748d7-108">Sunucu, bağlı olan tüm tarayıcılarda şeklin konumunu, zamanlanmış güncelleştirmeleri kullanarak sürüklenen şeklin konumuyla eşleşecek şekilde güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="748d7-108">The server updates the position of the shape in all connected browsers to match the position of the dragged shape using timed updates.</span></span>

<span data-ttu-id="748d7-109">Bu öğreticide tanıtılan kavramların gerçek zamanlı oyun ve diğer simülasyon uygulamalarına yönelik uygulamaları vardır.</span><span class="sxs-lookup"><span data-stu-id="748d7-109">Concepts introduced in this tutorial have applications in real-time gaming and other simulation applications.</span></span>

<span data-ttu-id="748d7-110">Bu öğreticide şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="748d7-110">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="748d7-111">Projeyi ayarlama</span><span class="sxs-lookup"><span data-stu-id="748d7-111">Set up the project</span></span>
> * <span data-ttu-id="748d7-112">Temel uygulamayı oluşturma</span><span class="sxs-lookup"><span data-stu-id="748d7-112">Create the base application</span></span>
> * <span data-ttu-id="748d7-113">Uygulama başlatıldığında hub 'a eşle</span><span class="sxs-lookup"><span data-stu-id="748d7-113">Map to the hub when app starts</span></span>
> * <span data-ttu-id="748d7-114">İstemciyi ekleme</span><span class="sxs-lookup"><span data-stu-id="748d7-114">Add the client</span></span>
> * <span data-ttu-id="748d7-115">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="748d7-115">Run the app</span></span>
> * <span data-ttu-id="748d7-116">İstemci döngüsünü ekleme</span><span class="sxs-lookup"><span data-stu-id="748d7-116">Add the client loop</span></span>
> * <span data-ttu-id="748d7-117">Sunucu döngüsünü ekleyin</span><span class="sxs-lookup"><span data-stu-id="748d7-117">Add the server loop</span></span>
> * <span data-ttu-id="748d7-118">Kesintisiz animasyon ekle</span><span class="sxs-lookup"><span data-stu-id="748d7-118">Add smooth animation</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="748d7-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="748d7-119">Prerequisites</span></span>

* <span data-ttu-id="748d7-120">**ASP.net ve Web geliştirme** iş yüküyle [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) .</span><span class="sxs-lookup"><span data-stu-id="748d7-120">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="748d7-121">Projeyi ayarlama</span><span class="sxs-lookup"><span data-stu-id="748d7-121">Set up the project</span></span>

<span data-ttu-id="748d7-122">Bu bölümde, projeyi Visual Studio 2017 ' de oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="748d7-122">In this section, you create the project in Visual Studio 2017.</span></span>

<span data-ttu-id="748d7-123">Bu bölümde, Visual Studio 2017 kullanarak boş bir ASP.NET Web uygulaması oluşturma ve SignalR ve jQuery. UI kitaplıklarını ekleme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="748d7-123">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application and add the SignalR and jQuery.UI libraries.</span></span>

1. <span data-ttu-id="748d7-124">Visual Studio 'da bir ASP.NET Web uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="748d7-124">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![Web oluştur](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

1. <span data-ttu-id="748d7-126">**Yeni ASP.NET Web uygulaması-Moveshaayaklı Mo** penceresinde **boş** bırakın ve **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="748d7-126">In the **New ASP.NET Web Application - MoveShapeDemo** window, leave **Empty** selected and select **OK**.</span></span>

1. <span data-ttu-id="748d7-127">**Çözüm Gezgini**, projeye sağ tıklayın ve > **Yeni öğe** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="748d7-127">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="748d7-128">**Yeni öğe Ekle-moveshaayaklı Mo**'da, **yüklü** > **Visual C#**  > **Web** > **SignalR** ' i seçin ve ardından **SignalR hub sınıfı (v2)** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="748d7-128">In **Add New Item - MoveShapeDemo**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="748d7-129">Sınıfı *Moveshapehub* olarak adlandırın ve projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="748d7-129">Name the class *MoveShapeHub* and add it to the project.</span></span>

    <span data-ttu-id="748d7-130">Bu adım *MoveShapeHub.cs* sınıf dosyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="748d7-130">This step creates the *MoveShapeHub.cs* class file.</span></span> <span data-ttu-id="748d7-131">Aynı anda, bir dizi betik dosyası ve proje için SignalR 'yi destekleyen derleme başvuruları ekler.</span><span class="sxs-lookup"><span data-stu-id="748d7-131">Simultaneously, it adds  a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="748d7-132">**Araçlar** > **NuGet Paket Yöneticisi** > **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="748d7-132">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

1. <span data-ttu-id="748d7-133">**Paket Yöneticisi konsolu**'nda şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="748d7-133">In **Package Manager Console**, run this command:</span></span>

    ```console
    Install-Package jQuery.UI.Combined
    ```

    <span data-ttu-id="748d7-134">Komutu jQuery kullanıcı arabirimi kitaplığını yükleme.</span><span class="sxs-lookup"><span data-stu-id="748d7-134">The command installs the jQuery UI library.</span></span> <span data-ttu-id="748d7-135">Şekle animasyon eklemek için bunu kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="748d7-135">You use it to animate the shape.</span></span>

1. <span data-ttu-id="748d7-136">**Çözüm Gezgini**' de betikler düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="748d7-136">In **Solution Explorer**, expand the Scripts node.</span></span>

    ![Betik kitaplığı başvuruları](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

    <span data-ttu-id="748d7-138">JQuery, jQueryUI ve SignalR için betik kitaplıkları projede görünür.</span><span class="sxs-lookup"><span data-stu-id="748d7-138">Script libraries for jQuery, jQueryUI, and SignalR are visible in the project.</span></span>

## <a name="create-the-base-application"></a><span data-ttu-id="748d7-139">Temel uygulamayı oluşturma</span><span class="sxs-lookup"><span data-stu-id="748d7-139">Create the base application</span></span>

<span data-ttu-id="748d7-140">Bu bölümde, bir tarayıcı uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="748d7-140">In this section, you create a browser application.</span></span> <span data-ttu-id="748d7-141">Uygulama, her fare taşıma olayı sırasında şeklin konumunu sunucuya gönderir.</span><span class="sxs-lookup"><span data-stu-id="748d7-141">The app sends the location of the shape to the server during each mouse move event.</span></span> <span data-ttu-id="748d7-142">Sunucu, bu bilgileri tüm bağlı istemcilere gerçek zamanlı olarak yayınlar.</span><span class="sxs-lookup"><span data-stu-id="748d7-142">The server broadcasts this information to all other connected clients in real time.</span></span> <span data-ttu-id="748d7-143">Daha sonraki bölümlerde bu uygulama hakkında daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="748d7-143">You learn more about this application in later sections.</span></span>

1. <span data-ttu-id="748d7-144">*MoveShapeHub.cs* dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="748d7-144">Open the *MoveShapeHub.cs* file.</span></span>

1. <span data-ttu-id="748d7-145">*MoveShapeHub.cs* dosyasındaki kodu şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="748d7-145">Replace the code in the *MoveShapeHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.cs)]

1. <span data-ttu-id="748d7-146">Dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="748d7-146">Save the file.</span></span>

<span data-ttu-id="748d7-147">`MoveShapeHub` sınıfı, bir SignalR hub 'ının uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="748d7-147">The `MoveShapeHub` class is an implementation of a SignalR hub.</span></span> <span data-ttu-id="748d7-148">[SignalR Ile çalışmaya](tutorial-getting-started-with-signalr.md) başlama öğreticisinde olduğu gibi, hub 'ın istemcilerin doğrudan çağırdığına yönelik bir yöntemi vardır.</span><span class="sxs-lookup"><span data-stu-id="748d7-148">As in the [Getting Started with SignalR](tutorial-getting-started-with-signalr.md) tutorial, the hub has a method that the clients call directly.</span></span> <span data-ttu-id="748d7-149">Bu durumda, istemci, şeklin yeni X ve Y koordinatlarıyla sunucuya bir nesne gönderir.</span><span class="sxs-lookup"><span data-stu-id="748d7-149">In this case, the client sends an object with the new X and Y coordinates of the shape to the server.</span></span> <span data-ttu-id="748d7-150">Bu koordinatlar, diğer tüm bağlı istemcilere göre yapılır.</span><span class="sxs-lookup"><span data-stu-id="748d7-150">Those coordinates get broadcasted to all other connected clients.</span></span> <span data-ttu-id="748d7-151">SignalR, JSON kullanarak bu nesneyi otomatik olarak serileştirir.</span><span class="sxs-lookup"><span data-stu-id="748d7-151">SignalR automatically serializes this object using JSON.</span></span>

<span data-ttu-id="748d7-152">Uygulama `ShapeModel` nesnesini istemciye gönderir.</span><span class="sxs-lookup"><span data-stu-id="748d7-152">The app sends the `ShapeModel` object to the client.</span></span> <span data-ttu-id="748d7-153">Şeklin konumunu depolayan üyelere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="748d7-153">It has members to store the position of the shape.</span></span> <span data-ttu-id="748d7-154">Sunucu üzerindeki nesnenin sürümü, hangi istemci verilerinin depolanmakta olduğunu izlemek için bir üyeye de sahiptir.</span><span class="sxs-lookup"><span data-stu-id="748d7-154">The version of the object on the server also has a member to track which client's data is being stored.</span></span> <span data-ttu-id="748d7-155">Bu nesne, sunucunun istemciye ait verileri geri göndermesini önler.</span><span class="sxs-lookup"><span data-stu-id="748d7-155">This object prevents the server from sending a client's data back to itself.</span></span> <span data-ttu-id="748d7-156">Bu üye, uygulamanın verileri serileştirmesini ve istemciye geri göndermesini önlemek için `JsonIgnore` özniteliğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="748d7-156">This member uses the `JsonIgnore` attribute to keep the application from serializing the data and sending it back to the client.</span></span>

## <a name="map-to-the-hub-when-app-starts"></a><span data-ttu-id="748d7-157">Uygulama başlatıldığında hub 'a eşle</span><span class="sxs-lookup"><span data-stu-id="748d7-157">Map to the hub when app starts</span></span>

<span data-ttu-id="748d7-158">Daha sonra, uygulama başladığında hub ile eşlemeyi ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="748d7-158">Next, you set up mapping to the hub when the application starts.</span></span> <span data-ttu-id="748d7-159">SignalR 2 ' de, bir OWıN başlangıç sınıfı eklendiğinde eşleme oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="748d7-159">In SignalR 2, adding an OWIN startup class creates the mapping.</span></span>

1. <span data-ttu-id="748d7-160">**Çözüm Gezgini**, projeye sağ tıklayın ve > **Yeni öğe** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="748d7-160">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="748d7-161">**Yeni öğe Ekle-moveshaayaklı Mo** ' da **yüklü** > **Visual C#**  > **Web** ' i seçin ve ardından **owın başlangıç sınıfı**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="748d7-161">In **Add New Item - MoveShapeDemo** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="748d7-162">Sınıfın *başlangıcını* adlandırın ve **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="748d7-162">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="748d7-163">*Startup.cs* dosyasındaki varsayılan kodu şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="748d7-163">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.cs)]

<span data-ttu-id="748d7-164">OWıN başlangıç sınıfı, uygulama `Configuration` yöntemini yürüttüğünde `MapSignalR` çağırır.</span><span class="sxs-lookup"><span data-stu-id="748d7-164">The OWIN startup class calls `MapSignalR` when the app executes the `Configuration` method.</span></span> <span data-ttu-id="748d7-165">Uygulama, `OwinStartup` derleme özniteliğini kullanarak sınıfı OWıN başlangıç işlemine ekler.</span><span class="sxs-lookup"><span data-stu-id="748d7-165">The app adds the class to OWIN's startup process using the `OwinStartup` assembly attribute.</span></span>

## <a name="add-the-client"></a><span data-ttu-id="748d7-166">İstemciyi ekleme</span><span class="sxs-lookup"><span data-stu-id="748d7-166">Add the client</span></span>

<span data-ttu-id="748d7-167">İstemci için HTML sayfasını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="748d7-167">Add the HTML page for the client.</span></span>

1. <span data-ttu-id="748d7-168">**Çözüm Gezgini**' de projeye sağ tıklayın ve > **HTML sayfası** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="748d7-168">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="748d7-169">Sayfa **varsayılanını** adlandırın ve **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="748d7-169">Name the page **Default** and select **OK**.</span></span>

1. <span data-ttu-id="748d7-170">**Çözüm Gezgini**' de, *default. html* ' ye sağ tıklayın ve **Başlangıç sayfası olarak ayarla**' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="748d7-170">In **Solution Explorer**, right-click *Default.html* and select **Set as Start Page**.</span></span>

1. <span data-ttu-id="748d7-171">*Default. html* dosyasındaki varsayılan kodu şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="748d7-171">Replace the default code in the *Default.html* file with this code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.html?highlight=14-16)]

1. <span data-ttu-id="748d7-172">**Çözüm Gezgini**' de **betikler**' ı genişletin.</span><span class="sxs-lookup"><span data-stu-id="748d7-172">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="748d7-173">JQuery ve SignalR için betik kitaplıkları projede görülebilir.</span><span class="sxs-lookup"><span data-stu-id="748d7-173">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="748d7-174">Paket Yöneticisi, SignalR betiklerinin daha yeni bir sürümünü yüklüyor.</span><span class="sxs-lookup"><span data-stu-id="748d7-174">The package manager installs a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="748d7-175">Kod bloğundaki betik başvurularını projedeki betik dosyalarının sürümlerine karşılık gelecek şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="748d7-175">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

<span data-ttu-id="748d7-176">Bu HTML ve JavaScript kodu `shape`adlı kırmızı bir `div` oluşturur.</span><span class="sxs-lookup"><span data-stu-id="748d7-176">This HTML and JavaScript code creates a red `div` called `shape`.</span></span> <span data-ttu-id="748d7-177">Şeklin, jQuery kitaplığını kullanarak sürükleme davranışını sağlar ve şeklin konumunu sunucuya göndermek için `drag` olayını kullanır.</span><span class="sxs-lookup"><span data-stu-id="748d7-177">It enables the shape's dragging behavior using the jQuery library and uses the `drag` event to send the shape's position to the server.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="748d7-178">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="748d7-178">Run the app</span></span>

<span data-ttu-id="748d7-179">Uygulamayı çalıştırmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="748d7-179">You can run the app to se\`e it work.</span></span> <span data-ttu-id="748d7-180">Şekli bir tarayıcı penceresi etrafında sürüklediğinizde, şekil diğer tarayıcılarda da hareket eder.</span><span class="sxs-lookup"><span data-stu-id="748d7-180">When you drag the shape around a browser window, the shape moves in the other browsers too.</span></span>

1. <span data-ttu-id="748d7-181">Araç çubuğunda, **betik hata ayıklamayı** açın ve ardından uygulamayı hata ayıklama modunda çalıştırmak için Yürüt düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="748d7-181">In the toolbar, turn on **Script Debugging** and then select the play button to run the application in Debug mode.</span></span>

    ![Kullanıcı hata ayıklama modunu açıp oynat 'ı seçen kullanıcının ekran görüntüsü.](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)

    <span data-ttu-id="748d7-183">Sağ üst köşedeki kırmızı şekille bir tarayıcı penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="748d7-183">A browser window opens with the red shape in the upper-right corner.</span></span>

1. <span data-ttu-id="748d7-184">Sayfanın URL 'sini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="748d7-184">Copy the page's URL.</span></span>

1. <span data-ttu-id="748d7-185">Başka bir tarayıcı açın ve URL 'YI adres çubuğuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="748d7-185">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="748d7-186">Şekli tarayıcı pencerelerinin birine sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="748d7-186">Drag the shape in one of the browser windows.</span></span> <span data-ttu-id="748d7-187">Diğer tarayıcı penceresindeki şekil aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="748d7-187">The shape in the other browser window follows.</span></span>

<span data-ttu-id="748d7-188">Uygulama bu yöntemi kullanırken çalışır, ancak önerilen bir programlama modeli değildir.</span><span class="sxs-lookup"><span data-stu-id="748d7-188">While the application functions using this method, it's not a recommended programming model.</span></span> <span data-ttu-id="748d7-189">Gönderilen ileti sayısı üst sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="748d7-189">There's no upper limit to the number of messages getting sent.</span></span> <span data-ttu-id="748d7-190">Sonuç olarak, istemciler ve sunucu iletileri ve performansı düşürür.</span><span class="sxs-lookup"><span data-stu-id="748d7-190">As a result, the clients and server get overwhelmed with messages and performance degrades.</span></span> <span data-ttu-id="748d7-191">Ayrıca, uygulama istemcide kopuk bir animasyon görüntüler.</span><span class="sxs-lookup"><span data-stu-id="748d7-191">Also, the app displays a disjointed animation on the client.</span></span> <span data-ttu-id="748d7-192">Bu düzensiz animasyon, şekil her yöntem tarafından anında taşınabileceğinden oluşur.</span><span class="sxs-lookup"><span data-stu-id="748d7-192">This jerky animation happens because the shape moves instantly by each method.</span></span> <span data-ttu-id="748d7-193">Şekil her yeni konuma düzgün şekilde taşınırsa daha iyidir.</span><span class="sxs-lookup"><span data-stu-id="748d7-193">It's better if the shape moves smoothly to each new location.</span></span> <span data-ttu-id="748d7-194">Ardından, bu sorunları nasıl düzelteceğinizi öğrenirsiniz.</span><span class="sxs-lookup"><span data-stu-id="748d7-194">Next, you learn how to fix those issues.</span></span>

## <a name="add-the-client-loop"></a><span data-ttu-id="748d7-195">İstemci döngüsünü ekleme</span><span class="sxs-lookup"><span data-stu-id="748d7-195">Add the client loop</span></span>

<span data-ttu-id="748d7-196">Her fare taşıma olayında şeklin konumunu göndermek gereksiz miktarda ağ trafiği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="748d7-196">Sending the location of the shape on every mouse move event creates an unnecessary amount of network traffic.</span></span> <span data-ttu-id="748d7-197">Uygulamanın, istemciden gelen iletileri azaltması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="748d7-197">The app needs to throttle the messages from the client.</span></span>

<span data-ttu-id="748d7-198">Yeni konum bilgilerini sunucuya sabit bir hızda gönderen bir döngü ayarlamak için JavaScript `setInterval` işlevini kullanın.</span><span class="sxs-lookup"><span data-stu-id="748d7-198">Use the javascript `setInterval` function to set up a loop that sends new position information to the server at a fixed rate.</span></span> <span data-ttu-id="748d7-199">Bu döngü, "oyun döngüsünün" temel bir gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="748d7-199">This loop is a basic representation of a "game loop."</span></span> <span data-ttu-id="748d7-200">Bu, bir oyunun tüm işlevselliğini destekleyen, tekrar tekrar çağrılan bir işlevdir.</span><span class="sxs-lookup"><span data-stu-id="748d7-200">It's a repeatedly called function that drives all the functionality of a game.</span></span>

1. <span data-ttu-id="748d7-201">*Default. html* dosyasındaki istemci kodunu şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="748d7-201">Replace the client code in the *Default.html* file with this code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.html?highlight=14-16)]

    > [!IMPORTANT]
    > <span data-ttu-id="748d7-202">Betik başvurularını yeniden değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="748d7-202">You have to replace the script references again.</span></span> <span data-ttu-id="748d7-203">Projenin, projedeki betiklerin sürümleriyle eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="748d7-203">They must match the versions of the scripts in the project.</span></span>

    <span data-ttu-id="748d7-204">Bu yeni kod `updateServerModel` işlevini ekler.</span><span class="sxs-lookup"><span data-stu-id="748d7-204">This new code adds the `updateServerModel` function.</span></span> <span data-ttu-id="748d7-205">Sabit bir sıklıkta çağrılır.</span><span class="sxs-lookup"><span data-stu-id="748d7-205">It gets called on a fixed frequency.</span></span> <span data-ttu-id="748d7-206">İşlevi, `moved` bayrağı gönderilecek yeni konum verilerinin olduğunu gösterdiğinde, konum verilerini sunucuya gönderir.</span><span class="sxs-lookup"><span data-stu-id="748d7-206">The function sends the position data to the server whenever the `moved` flag indicates that there's new position data to send.</span></span>

1. <span data-ttu-id="748d7-207">Uygulamayı başlatmak için Oynat düğmesini seçin</span><span class="sxs-lookup"><span data-stu-id="748d7-207">Select the play button to start the application</span></span>

1. <span data-ttu-id="748d7-208">Sayfanın URL 'sini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="748d7-208">Copy the page's URL.</span></span>

1. <span data-ttu-id="748d7-209">Başka bir tarayıcı açın ve URL 'YI adres çubuğuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="748d7-209">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="748d7-210">Şekli tarayıcı pencerelerinin birine sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="748d7-210">Drag the shape in one of the browser windows.</span></span> <span data-ttu-id="748d7-211">Diğer tarayıcı penceresindeki şekil aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="748d7-211">The shape in the other browser window follows.</span></span>

<span data-ttu-id="748d7-212">Uygulama, sunucuya gönderilen ileti sayısını kısıtladığından, animasyon ilk olarak düzgün bir şekilde görünmez.</span><span class="sxs-lookup"><span data-stu-id="748d7-212">Since the app throttles the number of messages that get sent to the server, the animation won't appear as smooth did at first.</span></span>

## <a name="add-the-server-loop"></a><span data-ttu-id="748d7-213">Sunucu döngüsünü ekleyin</span><span class="sxs-lookup"><span data-stu-id="748d7-213">Add the server loop</span></span>

<span data-ttu-id="748d7-214">Geçerli uygulamada, sunucudan istemciye gönderilen iletiler, alındıkları sıklıkta zaman aşımına uğrar.</span><span class="sxs-lookup"><span data-stu-id="748d7-214">In the current application, messages sent from the server to the client go out as often as they're received.</span></span> <span data-ttu-id="748d7-215">Bu ağ trafiği, istemcide görtiğimiz gibi benzer bir sorun gösterir.</span><span class="sxs-lookup"><span data-stu-id="748d7-215">This network traffic presents a similar problem as we see on the client.</span></span>

<span data-ttu-id="748d7-216">Uygulama, gerekli olduklarından daha sık ileti gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="748d7-216">The app can send messages more often than they're needed.</span></span> <span data-ttu-id="748d7-217">Bağlantı sonuç olarak taşabilir.</span><span class="sxs-lookup"><span data-stu-id="748d7-217">The connection can become flooded as a result.</span></span> <span data-ttu-id="748d7-218">Bu bölümde, giden iletilerin oranını hedefleyen bir Zamanlayıcı eklemek için sunucunun nasıl güncelleştirileceğini açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="748d7-218">This section describes how to update the server to add a timer that throttles the rate of the outgoing messages.</span></span>

1. <span data-ttu-id="748d7-219">`MoveShapeHub.cs` içeriğini şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="748d7-219">Replace the contents of `MoveShapeHub.cs` with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

1. <span data-ttu-id="748d7-220">Uygulamayı başlatmak için Oynat düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="748d7-220">Select the play button to start the application.</span></span>

1. <span data-ttu-id="748d7-221">Sayfanın URL 'sini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="748d7-221">Copy the page's URL.</span></span>

1. <span data-ttu-id="748d7-222">Başka bir tarayıcı açın ve URL 'YI adres çubuğuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="748d7-222">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="748d7-223">Şekli tarayıcı pencerelerinin birine sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="748d7-223">Drag the shape in one of the browser windows.</span></span>

<span data-ttu-id="748d7-224">Bu kod, `Broadcaster` sınıfını eklemek için istemciyi genişletir.</span><span class="sxs-lookup"><span data-stu-id="748d7-224">This code expands the client to add the `Broadcaster` class.</span></span> <span data-ttu-id="748d7-225">Yeni sınıf, .NET Framework 'teki `Timer` sınıfını kullanarak giden iletileri kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="748d7-225">The new class throttles the outgoing messages using the `Timer` class from the .NET framework.</span></span>

<span data-ttu-id="748d7-226">Hub 'ın geçişli olduğunu öğrenmek iyi bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="748d7-226">It's good to learn that the hub itself is transitory.</span></span> <span data-ttu-id="748d7-227">Her gerektiğinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="748d7-227">It's created every time it's needed.</span></span> <span data-ttu-id="748d7-228">Bu nedenle uygulama, `Broadcaster` tek bir olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="748d7-228">So the app creates the `Broadcaster` as a singleton.</span></span> <span data-ttu-id="748d7-229">`Broadcaster`oluşturma işlemi, gerekene kadar ertelenmesi için yavaş başlatma kullanır.</span><span class="sxs-lookup"><span data-stu-id="748d7-229">It uses lazy initialization to defer the `Broadcaster`'s creation until it's needed.</span></span> <span data-ttu-id="748d7-230">Bu, uygulamanın süreölçeri başlatmadan önce ilk hub örneğini tamamen oluşturduğunu garanti eder.</span><span class="sxs-lookup"><span data-stu-id="748d7-230">That guarantees that the app creates the first hub instance completely before starting the timer.</span></span>

<span data-ttu-id="748d7-231">İstemciler ' `UpdateShape` işlevine yapılan çağrı daha sonra hub 'ın `UpdateModel` yönteminden çıkarılır.</span><span class="sxs-lookup"><span data-stu-id="748d7-231">The call to the clients' `UpdateShape` function is then moved out of the hub's `UpdateModel` method.</span></span> <span data-ttu-id="748d7-232">Uygulama gelen iletileri aldığında artık hemen çağrılmaz.</span><span class="sxs-lookup"><span data-stu-id="748d7-232">It's no longer called immediately whenever the app receives incoming messages.</span></span> <span data-ttu-id="748d7-233">Bunun yerine, uygulama iletileri istemcilere saniyede 25 çağrı hızında gönderir.</span><span class="sxs-lookup"><span data-stu-id="748d7-233">Instead, the app sends the messages to the clients at a rate of 25 calls per second.</span></span> <span data-ttu-id="748d7-234">İşlem, `Broadcaster` sınıfının içinden `_broadcastLoop` Zamanlayıcı tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="748d7-234">The process is  managed by the `_broadcastLoop` timer from within the `Broadcaster` class.</span></span>

<span data-ttu-id="748d7-235">Son olarak, doğrudan hub 'dan istemci yöntemini çağırmak yerine, `Broadcaster` sınıfın şu anda çalışan `_hubContext` hub 'ına bir başvuru alması gerekir.</span><span class="sxs-lookup"><span data-stu-id="748d7-235">Lastly, instead of calling the client method from the hub directly, the `Broadcaster` class needs to get a reference to the currently operating `_hubContext` hub.</span></span> <span data-ttu-id="748d7-236">`GlobalHost`başvurusunu alır.</span><span class="sxs-lookup"><span data-stu-id="748d7-236">It gets the reference with the `GlobalHost`.</span></span>

## <a name="add-smooth-animation"></a><span data-ttu-id="748d7-237">Kesintisiz animasyon ekle</span><span class="sxs-lookup"><span data-stu-id="748d7-237">Add smooth animation</span></span>

<span data-ttu-id="748d7-238">Uygulama neredeyse tamamlandı, ancak bir geliştirme yapabiliriz.</span><span class="sxs-lookup"><span data-stu-id="748d7-238">The application is almost finished, but we could make one more improvement.</span></span> <span data-ttu-id="748d7-239">Uygulama, istemci üzerindeki şekli sunucu iletilerine yanıt olarak kaydırır.</span><span class="sxs-lookup"><span data-stu-id="748d7-239">The app moves the shape on the client in response to server messages.</span></span> <span data-ttu-id="748d7-240">Şeklin konumunu sunucu tarafından verilen yeni konuma ayarlamak yerine, JQuery Kullanıcı arabirimi kitaplığının `animate` işlevini kullanın.</span><span class="sxs-lookup"><span data-stu-id="748d7-240">Instead of setting the position of the shape to the new location given by the server, use the JQuery UI library's `animate` function.</span></span> <span data-ttu-id="748d7-241">Şekli geçerli ve yeni konumu arasında sorunsuzca hareket edebilir.</span><span class="sxs-lookup"><span data-stu-id="748d7-241">It can move the shape smoothly between its current and new position.</span></span>

1. <span data-ttu-id="748d7-242">*Varsayılan. html* dosyasındaki istemcinin `updateShape` yöntemini vurgulanan kodla aynı şekilde güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="748d7-242">Update the client's `updateShape` method in the *Default.html* file to look like the highlighted code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.html?highlight=33-40)]

1. <span data-ttu-id="748d7-243">Uygulamayı başlatmak için Oynat düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="748d7-243">Select the play button to start the application.</span></span>

1. <span data-ttu-id="748d7-244">Sayfanın URL 'sini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="748d7-244">Copy the page's URL.</span></span>

1. <span data-ttu-id="748d7-245">Başka bir tarayıcı açın ve URL 'YI adres çubuğuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="748d7-245">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="748d7-246">Şekli tarayıcı pencerelerinin birine sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="748d7-246">Drag the shape in one of the browser windows.</span></span>

<span data-ttu-id="748d7-247">Şeklin diğer penceredeki hareketi daha az jerbir şekilde görünür.</span><span class="sxs-lookup"><span data-stu-id="748d7-247">The movement of the shape in the other window appears less jerky.</span></span> <span data-ttu-id="748d7-248">Uygulama, gelen ileti başına bir kez ayarlanmaktansa hareketini zamana göre enterpolasyonlar.</span><span class="sxs-lookup"><span data-stu-id="748d7-248">The app interpolates its movement over time rather than being set once per incoming message.</span></span>

<span data-ttu-id="748d7-249">Bu kod, şekli eski konumdan yeni bir konuma taşır.</span><span class="sxs-lookup"><span data-stu-id="748d7-249">This code moves the shape from the old location to the new one.</span></span> <span data-ttu-id="748d7-250">Sunucu, animasyon aralığı boyunca şeklin konumunu verir.</span><span class="sxs-lookup"><span data-stu-id="748d7-250">The server gives the position of the shape over the course of the animation interval.</span></span> <span data-ttu-id="748d7-251">Bu durumda, 100 milisaniyedir.</span><span class="sxs-lookup"><span data-stu-id="748d7-251">In this case, that's 100 milliseconds.</span></span> <span data-ttu-id="748d7-252">Uygulama, yeni animasyon başlamadan önce şekil üzerinde çalışan önceki animasyonu temizler.</span><span class="sxs-lookup"><span data-stu-id="748d7-252">The app clears any previous animation running on the shape before the new animation starts.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="748d7-253">Kodu alın</span><span class="sxs-lookup"><span data-stu-id="748d7-253">Get the code</span></span>

[<span data-ttu-id="748d7-254">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="748d7-254">Download Completed Project</span></span>](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)

## <a name="additional-resources"></a><span data-ttu-id="748d7-255">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="748d7-255">Additional resources</span></span>

<span data-ttu-id="748d7-256">Yeni öğrendiğiniz iletişim paradigması, [SignalR ile oluşturulan ShootR oyunu](https://shootr.azurewebsites.net/)gibi çevrimiçi oyunları ve diğer benzetimleri geliştirmek için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="748d7-256">The communication paradigm you just learned about is useful for developing online games and other simulations, like [the ShootR game created with SignalR](https://shootr.azurewebsites.net/).</span></span>

<span data-ttu-id="748d7-257">SignalR hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="748d7-257">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="748d7-258">SignalR projesi</span><span class="sxs-lookup"><span data-stu-id="748d7-258">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="748d7-259">SignalR GitHub ve örnekleri</span><span class="sxs-lookup"><span data-stu-id="748d7-259">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="748d7-260">SignalR wiki</span><span class="sxs-lookup"><span data-stu-id="748d7-260">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="748d7-261">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="748d7-261">Next steps</span></span>

<span data-ttu-id="748d7-262">Bu öğreticide şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="748d7-262">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="748d7-263">Projeyi ayarlama</span><span class="sxs-lookup"><span data-stu-id="748d7-263">Set up the project</span></span>
> * <span data-ttu-id="748d7-264">Temel uygulama oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="748d7-264">Created the base application</span></span>
> * <span data-ttu-id="748d7-265">Uygulama başlatıldığında hub 'a eşlendi</span><span class="sxs-lookup"><span data-stu-id="748d7-265">Mapped to the hub when app starts</span></span>
> * <span data-ttu-id="748d7-266">İstemci eklendi</span><span class="sxs-lookup"><span data-stu-id="748d7-266">Added the client</span></span>
> * <span data-ttu-id="748d7-267">Uygulamayı çalıştırdım</span><span class="sxs-lookup"><span data-stu-id="748d7-267">Ran the app</span></span>
> * <span data-ttu-id="748d7-268">İstemci döngüsü eklendi</span><span class="sxs-lookup"><span data-stu-id="748d7-268">Added the client loop</span></span>
> * <span data-ttu-id="748d7-269">Sunucu döngüsü eklendi</span><span class="sxs-lookup"><span data-stu-id="748d7-269">Added the server loop</span></span>
> * <span data-ttu-id="748d7-270">Kesintisiz animasyon eklendi</span><span class="sxs-lookup"><span data-stu-id="748d7-270">Added smooth animation</span></span>

<span data-ttu-id="748d7-271">Sunucu yayını işlevselliği sağlamak için ASP.NET SignalR 2 kullanan bir Web uygulamasının nasıl oluşturulacağını öğrenmek için sonraki makaleye ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="748d7-271">Advance to the next article to learn how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="748d7-272">SignalR 2 ve sunucu yayını</span><span class="sxs-lookup"><span data-stu-id="748d7-272">SignalR 2 and server broadcasting</span></span>](tutorial-server-broadcast-with-signalr.md)