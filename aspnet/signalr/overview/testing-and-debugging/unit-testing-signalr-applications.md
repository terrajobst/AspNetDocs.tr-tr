---
uid: signalr/overview/testing-and-debugging/unit-testing-signalr-applications
title: Birim testi SignalR uygulamaları | Microsoft Docs
author: bradygaster
description: Bu makalede, SignalR 2,0 'nin birim testi özelliklerinin nasıl kullanılacağı açıklanır.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: d1983524-e0d5-4ee6-9d87-1f552f7cb964
msc.legacyurl: /signalr/overview/testing-and-debugging/unit-testing-signalr-applications
msc.type: authoredcontent
ms.openlocfilehash: 2cf2e88f141d89971439dc1fc4979849f8dded47
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578675"
---
# <a name="unit-testing-signalr-applications"></a><span data-ttu-id="a5319-103">SignalR Uygulamalarına Birim Testi Yapma</span><span class="sxs-lookup"><span data-stu-id="a5319-103">Unit Testing SignalR Applications</span></span>

<span data-ttu-id="a5319-104">, [Patrick Fleti](https://github.com/pfletcher) tarafından</span><span class="sxs-lookup"><span data-stu-id="a5319-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="a5319-105">Bu makalede, SignalR 2 ' nin birim testi özelliklerini kullanma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a5319-105">This article describes using the Unit Testing features of SignalR 2.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="a5319-106">Bu konuda kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="a5319-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="a5319-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="a5319-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="a5319-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="a5319-108">.NET 4.5</span></span>
> - <span data-ttu-id="a5319-109">SignalR sürüm 2</span><span class="sxs-lookup"><span data-stu-id="a5319-109">SignalR version 2</span></span>
>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="a5319-110">Sorular ve açıklamalar</span><span class="sxs-lookup"><span data-stu-id="a5319-110">Questions and comments</span></span>
>
> <span data-ttu-id="a5319-111">Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun.</span><span class="sxs-lookup"><span data-stu-id="a5319-111">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="a5319-112">Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5319-112">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<a id="unit"></a>
## <a name="unit-testing-signalr-applications"></a><span data-ttu-id="a5319-113">Birim testi SignalR uygulamaları</span><span class="sxs-lookup"><span data-stu-id="a5319-113">Unit testing SignalR applications</span></span>

<span data-ttu-id="a5319-114">SignalR uygulamanız için birim testleri oluşturmak için SignalR 2 ' deki birim testi özelliklerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5319-114">You can use the unit test features in SignalR 2 to create unit tests for your SignalR application.</span></span> <span data-ttu-id="a5319-115">SignalR 2, test için hub yöntemlerinizi taklit etmek üzere bir sahte nesne oluşturmak için kullanılabilecek olan [IHV Ubcallerconnectioncontext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) arabirimini içerir.</span><span class="sxs-lookup"><span data-stu-id="a5319-115">SignalR 2 includes the [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) interface, which can be used to create a mock object to simulate your hub methods for testing.</span></span>

<span data-ttu-id="a5319-116">Bu bölümde, [XUnit.net](https://github.com/xunit/xunit) ve [moq](https://github.com/Moq/moq4)kullanarak başlangıç [öğreticisinde](../getting-started/tutorial-getting-started-with-signalr.md) oluşturulan uygulama için birim testleri ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="a5319-116">In this section, you'll add unit tests for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using [XUnit.net](https://github.com/xunit/xunit) and [Moq](https://github.com/Moq/moq4).</span></span>

<span data-ttu-id="a5319-117">XUnit.net, testi denetlemek için kullanılacaktır; MOQ, test için bir [sahte](http://en.wikipedia.org/wiki/Mock_object) nesne oluşturmak üzere kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="a5319-117">XUnit.net will be used to control the test; Moq will be used to create a [mock](http://en.wikipedia.org/wiki/Mock_object) object for testing.</span></span> <span data-ttu-id="a5319-118">İsterseniz, diğer sahte işlem çerçeveleri kullanılabilir; [Ndeğiştirme](http://nsubstitute.github.io/) de iyi bir seçimdir.</span><span class="sxs-lookup"><span data-stu-id="a5319-118">Other mocking frameworks can be used if desired; [NSubstitute](http://nsubstitute.github.io/) is also a good choice.</span></span> <span data-ttu-id="a5319-119">Bu öğreticide, bir arabirim kullanılarak, bir `dynamic` nesnesi (.NET Framework 4 ' te tanıtılan) ve ikincisi kullanarak, sahte nesnenin nasıl ayarlanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a5319-119">This tutorial demonstrates how to set up the mock object in two ways: First, using a `dynamic` object (introduced in .NET Framework 4), and second, using an interface.</span></span>

### <a name="contents"></a><span data-ttu-id="a5319-120">İçindekiler</span><span class="sxs-lookup"><span data-stu-id="a5319-120">Contents</span></span>

<span data-ttu-id="a5319-121">Bu öğretici aşağıdaki bölümleri içerir.</span><span class="sxs-lookup"><span data-stu-id="a5319-121">This tutorial contains the following sections.</span></span>

- [<span data-ttu-id="a5319-122">Dinamik ile birim testi</span><span class="sxs-lookup"><span data-stu-id="a5319-122">Unit testing with Dynamic</span></span>](#dynamic)
- [<span data-ttu-id="a5319-123">Türe göre birim testi</span><span class="sxs-lookup"><span data-stu-id="a5319-123">Unit testing by type</span></span>](#type)

<a id="dynamic"></a>
### <a name="unit-testing-with-dynamic"></a><span data-ttu-id="a5319-124">Dinamik ile birim testi</span><span class="sxs-lookup"><span data-stu-id="a5319-124">Unit testing with Dynamic</span></span>

<span data-ttu-id="a5319-125">Bu bölümde, dinamik bir nesne kullanarak başlangıç [öğreticisinde](../getting-started/tutorial-getting-started-with-signalr.md) oluşturulan uygulama için bir birim testi ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="a5319-125">In this section, you'll add a unit test for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using a dynamic object.</span></span>

1. <span data-ttu-id="a5319-126">Visual Studio 2013 için [xUnit Çalıştırıcısı uzantısını](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099) yükler.</span><span class="sxs-lookup"><span data-stu-id="a5319-126">Install the [XUnit Runner extension](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099) for Visual Studio 2013.</span></span>
2. <span data-ttu-id="a5319-127">[Kullanmaya başlama öğreticisini](../getting-started/tutorial-getting-started-with-signalr.md)ya da tamamlanmış uygulamayı [MSDN kod galerisinden](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)indirin.</span><span class="sxs-lookup"><span data-stu-id="a5319-127">Either complete the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md), or download the completed application from [MSDN Code Gallery](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).</span></span>
3. <span data-ttu-id="a5319-128">Başlarken uygulamasının indirme sürümünü kullanıyorsanız, **Paket Yöneticisi konsolu 'nu** açın ve **geri yükle** ' ye tıklayarak SignalR paketini projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a5319-128">If you are using the download version of the Getting Started application, open **Package Manager Console** and click **Restore** to add the SignalR package to the project.</span></span>

    ![Paketleri geri yükle](unit-testing-signalr-applications/_static/image1.png)
4. <span data-ttu-id="a5319-130">Birim testi için çözüme bir proje ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a5319-130">Add a project to the solution for the unit test.</span></span> <span data-ttu-id="a5319-131">**Çözüm Gezgini** çözümünüzde çözümünüze sağ tıklayın ve **Ekle**, **Yeni proje..** . öğesini seçin. **C#** Düğüm altında **Windows** düğümünü seçin.</span><span class="sxs-lookup"><span data-stu-id="a5319-131">Right-click your solution in **Solution Explorer** and select **Add**, **New Project...**. Under the **C#** node, select the **Windows** node.</span></span> <span data-ttu-id="a5319-132">**Sınıf kitaplığı**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="a5319-132">Select **Class Library**.</span></span> <span data-ttu-id="a5319-133">Yeni projeyi **Testlibrary** olarak adlandırın ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a5319-133">Name the new project **TestLibrary** and click **OK**.</span></span>

    ![Test kitaplığı oluştur](unit-testing-signalr-applications/_static/image2.png)
5. <span data-ttu-id="a5319-135">Test kitaplığı projesine SignalRChat projesine bir başvuru ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a5319-135">Add a reference in the test library project to the SignalRChat project.</span></span> <span data-ttu-id="a5319-136">**Testlibrary** projesine sağ tıklayın ve **Ekle**, **başvuru..** . seçeneğini belirleyin. **Çözüm** düğümü altındaki **Projeler** düğümünü seçin ve **signalrchat**' i kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="a5319-136">Right-click the **TestLibrary** project and select **Add**, **Reference...**. Select the **Projects** node under the **Solution** node, and check **SignalRChat**.</span></span> <span data-ttu-id="a5319-137">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a5319-137">Click **OK**.</span></span>

    ![Proje başvurusu Ekle](unit-testing-signalr-applications/_static/image3.png)
6. <span data-ttu-id="a5319-139">SignalR, moq ve XUnit paketlerini **Testlibrary** projesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a5319-139">Add the SignalR, Moq, and XUnit packages to the **TestLibrary** project.</span></span> <span data-ttu-id="a5319-140">**Paket Yöneticisi konsolunda**, **varsayılan proje** açılan menüsünü **testlibrary**olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a5319-140">In the **Package Manager Console**, set the **Default Project** dropdown to **TestLibrary**.</span></span> <span data-ttu-id="a5319-141">Konsol penceresinde aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a5319-141">Run the following commands in the console window:</span></span>

   - `Install-Package Microsoft.AspNet.SignalR`
   - `Install-Package Moq`
   - `Install-Package XUnit`

     ![Paketleri yükler](unit-testing-signalr-applications/_static/image4.png)
7. <span data-ttu-id="a5319-143">Test dosyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a5319-143">Create the test file.</span></span> <span data-ttu-id="a5319-144">**Testlibrary** projesine sağ tıklayın ve **Ekle...** **' ye tıklayın.**</span><span class="sxs-lookup"><span data-stu-id="a5319-144">Right-click the **TestLibrary** project and click **Add...**, **Class**.</span></span> <span data-ttu-id="a5319-145">Yeni sınıfı **Tests.cs**olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="a5319-145">Name the new class **Tests.cs**.</span></span>
8. <span data-ttu-id="a5319-146">Tests.cs içeriğini aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a5319-146">Replace the contents of Tests.cs with the following code.</span></span>

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample1.cs)]

    <span data-ttu-id="a5319-147">Yukarıdaki kodda, bir test istemcisi, IQ kitaplığı 'ndan (SignalR 2,1 ' [de tür parametresi](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) için `dynamic` atayın), [moq](https://github.com/Moq/moq4) kitaplığındaki `Mock` nesnesi kullanılarak oluşturulur. `IHubCallerConnectionContext` arabirimi, istemcisinde yöntemleri çağırmada kullandığınız ara sunucu nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="a5319-147">In the code above, a test client is created using the `Mock` object from the [Moq](https://github.com/Moq/moq4) library, of type [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (in SignalR 2.1, assign `dynamic` for the type parameter.) The `IHubCallerConnectionContext` interface is the proxy object with which you invoke methods on the client.</span></span> <span data-ttu-id="a5319-148">`broadcastMessage` işlevi daha sonra, `ChatHub` sınıfı tarafından çağrılabilmesi için, sahte istemci için tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a5319-148">The `broadcastMessage` function is then defined for the mock client so that it can be called by the `ChatHub` class.</span></span> <span data-ttu-id="a5319-149">Test motoru daha sonra `ChatHub` sınıfının `Send` yöntemini çağırır ve bu da moclenmiş `broadcastMessage` işlevini çağırır.</span><span class="sxs-lookup"><span data-stu-id="a5319-149">The test engine then calls the `Send` method of the `ChatHub` class, which in turn calls the mocked `broadcastMessage` function.</span></span>
9. <span data-ttu-id="a5319-150">**F6**tuşuna basarak çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a5319-150">Build the solution by pressing **F6**.</span></span>
10. <span data-ttu-id="a5319-151">Birim testini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a5319-151">Run the unit test.</span></span> <span data-ttu-id="a5319-152">Visual Studio 'da **Test**, **Windows**, **Test Gezgini**' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="a5319-152">In Visual Studio, select **Test**, **Windows**, **Test Explorer**.</span></span> <span data-ttu-id="a5319-153">Test Gezgini penceresinde, **Hubsaremockableviadynamıc** öğesine sağ tıklayın ve **Seçili Testleri Çalıştır**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="a5319-153">In the Test Explorer window, right-click **HubsAreMockableViaDynamic** and select **Run Selected Tests**.</span></span>

    ![Test Gezgini](unit-testing-signalr-applications/_static/image5.png)
11. <span data-ttu-id="a5319-155">Testin test Gezgini penceresindeki alt bölmeyi denetleyerek geçtiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a5319-155">Verify that the test passed by checking the lower pane in the Test Explorer window.</span></span> <span data-ttu-id="a5319-156">Pencerede testin geçtiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="a5319-156">The window will show that the test passed.</span></span>

    ![Test geçildi](unit-testing-signalr-applications/_static/image6.png)

<a id="type"></a>
### <a name="unit-testing-by-type"></a><span data-ttu-id="a5319-158">Türe göre birim testi</span><span class="sxs-lookup"><span data-stu-id="a5319-158">Unit testing by type</span></span>

<span data-ttu-id="a5319-159">Bu bölümde, test edilecek yöntemi içeren bir arabirimi kullanarak başlangıç [öğreticisinde](../getting-started/tutorial-getting-started-with-signalr.md) oluşturulan uygulama için bir test ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="a5319-159">In this section, you'll add a test for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using an interface that contains the method to be tested.</span></span>

1. <span data-ttu-id="a5319-160">Yukarıdaki [dinamik öğreticiyle birim testinde](#dynamic) 1-7 arasındaki adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="a5319-160">Complete steps 1-7 in the [Unit testing with Dynamic](#dynamic) tutorial above.</span></span>
2. <span data-ttu-id="a5319-161">Tests.cs içeriğini aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a5319-161">Replace the contents of Tests.cs with the following code.</span></span>

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample2.cs)]

    <span data-ttu-id="a5319-162">Yukarıdaki kodda, test altyapısının bir sahte istemci oluşturması için `broadcastMessage` yönteminin imzasını tanımlayan bir arabirim oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a5319-162">In the code above, an interface is created defining the signature of the `broadcastMessage` method for which the test engine will create a mock client.</span></span> <span data-ttu-id="a5319-163">Daha sonra bir sahte istemci, [ıubcallerconnectioncontext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) türünde `Mock` nesnesi kullanılarak oluşturulur (signalr 2,1 ' de tür parametresi için `dynamic` atayın.) `IHubCallerConnectionContext` arabirimi, istemcisinde yöntemleri çağırmada kullandığınız ara sunucu nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="a5319-163">A mock client is then created using the `Mock` object, of type [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (in SignalR 2.1, assign `dynamic` for the type parameter.) The `IHubCallerConnectionContext` interface is the proxy object with which you invoke methods on the client.</span></span>

    <span data-ttu-id="a5319-164">Test daha sonra bir `ChatHub`örneği oluşturur ve sonra `broadcastMessage` yönteminin bir sahte sürümünü oluşturur ve bu da hub üzerinde `Send` yöntemi çağırarak çağrılır.</span><span class="sxs-lookup"><span data-stu-id="a5319-164">The test then creates an instance of `ChatHub`, and then creates a mock version of the `broadcastMessage` method, which in turn is invoked by calling the `Send` method on the hub.</span></span>
3. <span data-ttu-id="a5319-165">**F6**tuşuna basarak çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a5319-165">Build the solution by pressing **F6**.</span></span>
4. <span data-ttu-id="a5319-166">Birim testini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a5319-166">Run the unit test.</span></span> <span data-ttu-id="a5319-167">Visual Studio 'da **Test**, **Windows**, **Test Gezgini**' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="a5319-167">In Visual Studio, select **Test**, **Windows**, **Test Explorer**.</span></span> <span data-ttu-id="a5319-168">Test Gezgini penceresinde, **Hubsaremockableviadynamıc** öğesine sağ tıklayın ve **Seçili Testleri Çalıştır**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="a5319-168">In the Test Explorer window, right-click **HubsAreMockableViaDynamic** and select **Run Selected Tests**.</span></span>

    ![Test Gezgini](unit-testing-signalr-applications/_static/image7.png)
5. <span data-ttu-id="a5319-170">Testin test Gezgini penceresindeki alt bölmeyi denetleyerek geçtiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a5319-170">Verify that the test passed by checking the lower pane in the Test Explorer window.</span></span> <span data-ttu-id="a5319-171">Pencerede testin geçtiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="a5319-171">The window will show that the test passed.</span></span>

    ![Test geçildi](unit-testing-signalr-applications/_static/image8.png)
