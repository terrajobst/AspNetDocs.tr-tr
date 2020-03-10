---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
title: OData v4 Istemci uygulaması oluşturma (C#) | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 47202362-3808-4add-9a69-c9d1f91d5e4e
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
msc.type: authoredcontent
ms.openlocfilehash: a0016cf2cc7bffe6268664395ccb38e140090310
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556296"
---
# <a name="create-an-odata-v4-client-app-c"></a><span data-ttu-id="93482-102">OData v4 İstemci Uygulaması Oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="93482-102">Create an OData v4 Client App (C#)</span></span>

<span data-ttu-id="93482-103">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="93482-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="93482-104">Önceki öğreticide CRUD işlemlerini destekleyen temel bir OData hizmeti oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="93482-104">In the previous tutorial, you created a basic OData service that supports CRUD operations.</span></span> <span data-ttu-id="93482-105">Şimdi hizmet için bir istemci oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="93482-105">Now let's create a client for the service.</span></span>

<span data-ttu-id="93482-106">Visual Studio 'nun yeni bir örneğini başlatın ve yeni bir konsol uygulaması projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="93482-106">Start a new instance of Visual Studio and create a new console application project.</span></span> <span data-ttu-id="93482-107">**Yeni proje** iletişim kutusunda,  **C# Visual** &gt; **Windows Masaüstü**&gt; **yüklü** &gt; **şablonları** ' nı seçin ve **konsol uygulaması** şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="93482-107">In the **New Project** dialog, select **Installed** &gt; **Templates** &gt; **Visual C#** &gt; **Windows Desktop**, and select the **Console Application** template.</span></span> <span data-ttu-id="93482-108">Projeyi &quot;ProductsApp&quot;olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="93482-108">Name the project &quot;ProductsApp&quot;.</span></span>

![](create-an-odata-v4-client-app/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="93482-109">Ayrıca, konsol uygulamasını OData hizmetini içeren aynı Visual Studio çözümüne ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="93482-109">You can also add the console app to the same Visual Studio solution that contains the OData service.</span></span>

## <a name="install-the-odata-client-code-generator"></a><span data-ttu-id="93482-110">OData Istemci kod oluşturucuyu yükler</span><span class="sxs-lookup"><span data-stu-id="93482-110">Install the OData Client Code Generator</span></span>

<span data-ttu-id="93482-111">**Araçlar** menüsünde **Uzantılar ve güncelleştirmeler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="93482-111">From the **Tools** menu, select **Extensions and Updates**.</span></span> <span data-ttu-id="93482-112">**Çevrimiçi** &gt; **Visual Studio Galerisi**' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="93482-112">Select **Online** &gt; **Visual Studio Gallery**.</span></span> <span data-ttu-id="93482-113">Arama kutusuna &quot;OData Istemci kodu Oluşturucu&quot;aratın.</span><span class="sxs-lookup"><span data-stu-id="93482-113">In the search box, search for &quot;OData Client Code Generator&quot;.</span></span> <span data-ttu-id="93482-114">VSıX 'i yüklemek için **İndir** 'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="93482-114">Click **Download** to install the VSIX.</span></span> <span data-ttu-id="93482-115">Visual Studio 'Yu yeniden başlatmanız istenebilir.</span><span class="sxs-lookup"><span data-stu-id="93482-115">You might be prompted to restart Visual Studio.</span></span>

[![](create-an-odata-v4-client-app/_static/image3.png)](create-an-odata-v4-client-app/_static/image2.png)

## <a name="run-the-odata-service-locally"></a><span data-ttu-id="93482-116">OData hizmetini yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="93482-116">Run the OData Service Locally</span></span>

<span data-ttu-id="93482-117">Visual Studio 'dan ProductService projesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="93482-117">Run the ProductService project from Visual Studio.</span></span> <span data-ttu-id="93482-118">Varsayılan olarak, Visual Studio uygulama köküne bir tarayıcı başlatır.</span><span class="sxs-lookup"><span data-stu-id="93482-118">By default, Visual Studio launches a browser to the application root.</span></span> <span data-ttu-id="93482-119">URI 'yi aklınızda bulunan Bu, bir sonraki adımda gerekli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="93482-119">Note the URI; you will need this in the next step.</span></span> <span data-ttu-id="93482-120">Uygulamayı çalışır durumda bırakın.</span><span class="sxs-lookup"><span data-stu-id="93482-120">Leave the application running.</span></span>

![](create-an-odata-v4-client-app/_static/image4.png)

> [!NOTE]
> <span data-ttu-id="93482-121">Her iki projeyi de aynı çözüme yerleştirirseniz, ProductService projesini hata ayıklama olmadan çalıştırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="93482-121">If you put both projects in the same solution, make sure to run the ProductService project without debugging.</span></span> <span data-ttu-id="93482-122">Bir sonraki adımda, konsol uygulama projesini değiştirirken hizmeti çalışır durumda tutmanız gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="93482-122">In the next step, you will need to keep the service running while you modify the console application project.</span></span>

## <a name="generate-the-service-proxy"></a><span data-ttu-id="93482-123">Hizmet proxy 'Si oluşturma</span><span class="sxs-lookup"><span data-stu-id="93482-123">Generate the Service Proxy</span></span>

<span data-ttu-id="93482-124">Hizmet proxy 'si OData hizmetine erişim yöntemlerini tanımlayan bir .NET sınıfıdır.</span><span class="sxs-lookup"><span data-stu-id="93482-124">The service proxy is a .NET class that defines methods for accessing the OData service.</span></span> <span data-ttu-id="93482-125">Proxy, Yöntem çağrılarını HTTP isteklerine çevirir.</span><span class="sxs-lookup"><span data-stu-id="93482-125">The proxy translates method calls into HTTP requests.</span></span> <span data-ttu-id="93482-126">Bir [T4 şablonu](https://msdn.microsoft.com/library/bb126445.aspx)çalıştırarak proxy sınıfını oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="93482-126">You will create the proxy class by running a [T4 template](https://msdn.microsoft.com/library/bb126445.aspx).</span></span>

<span data-ttu-id="93482-127">Projeye sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="93482-127">Right-click the project.</span></span> <span data-ttu-id="93482-128">&gt; **Yeni öğe** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="93482-128">Select **Add** &gt; **New Item**.</span></span>

![](create-an-odata-v4-client-app/_static/image5.png)

<span data-ttu-id="93482-129">**Yeni öğe Ekle** iletişim kutusunda,  **C# Visual Items** &gt; **Code** &gt; **OData Client**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="93482-129">In the **Add New Item** dialog, select **Visual C# Items** &gt; **Code** &gt; **OData Client**.</span></span> <span data-ttu-id="93482-130">Şablonu &quot;ProductClient.tt&quot;olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="93482-130">Name the template &quot;ProductClient.tt&quot;.</span></span> <span data-ttu-id="93482-131">**Ekle** ' ye tıklayın ve Güvenlik Uyarısı ' na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="93482-131">Click **Add** and click through the security warning.</span></span>

[![](create-an-odata-v4-client-app/_static/image7.png)](create-an-odata-v4-client-app/_static/image6.png)

<span data-ttu-id="93482-132">Bu noktada, yoksayabilirsiniz bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="93482-132">At this point, you'll get an error, which you can ignore.</span></span> <span data-ttu-id="93482-133">Visual Studio şablonu otomatik olarak çalıştırır, ancak şablonda önce bazı yapılandırma ayarları gerekir.</span><span class="sxs-lookup"><span data-stu-id="93482-133">Visual Studio automatically runs the template, but the template needs some configuration settings first.</span></span>

[![](create-an-odata-v4-client-app/_static/image9.png)](create-an-odata-v4-client-app/_static/image8.png)

<span data-ttu-id="93482-134">ProductClient. OData. config dosyasını açın. `Parameter` öğesinde, ProductService projesinden URI 'yi (önceki adımda) yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="93482-134">Open the file ProductClient.odata.config. In the `Parameter` element, paste in the URI from the ProductService project (previous step).</span></span> <span data-ttu-id="93482-135">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="93482-135">For example:</span></span>

[!code-xml[Main](create-an-odata-v4-client-app/samples/sample1.xml)]

[![](create-an-odata-v4-client-app/_static/image11.png)](create-an-odata-v4-client-app/_static/image10.png)

<span data-ttu-id="93482-136">Şablonu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="93482-136">Run the template again.</span></span> <span data-ttu-id="93482-137">Çözüm Gezgini ' de, ProductClient.tt dosyasına sağ tıklayın ve **özel araç Çalıştır**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="93482-137">In Solution Explorer, right click the ProductClient.tt file and select **Run Custom Tool**.</span></span>

<span data-ttu-id="93482-138">Şablon, proxy 'yi tanımlayan ProductClient.cs adlı bir kod dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="93482-138">The template creates a code file named ProductClient.cs that defines the proxy.</span></span> <span data-ttu-id="93482-139">Uygulamanızı geliştirirken, OData uç noktasını değiştirirseniz, proxy 'yi güncelleştirmek için şablonu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="93482-139">As you develop your app, if you change the OData endpoint, run the template again to update the proxy.</span></span>

![](create-an-odata-v4-client-app/_static/image12.png)

## <a name="use-the-service-proxy-to-call-the-odata-service"></a><span data-ttu-id="93482-140">OData hizmetini çağırmak için hizmet proxy 'sini kullanma</span><span class="sxs-lookup"><span data-stu-id="93482-140">Use the Service Proxy to Call the OData Service</span></span>

<span data-ttu-id="93482-141">Program.cs dosyasını açın ve ortak kodu aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="93482-141">Open the file Program.cs and replace the boilerplate code with the following.</span></span>

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample2.cs)]

<span data-ttu-id="93482-142">*Serviceurı* değerini daha önce gelen hizmet URI 'siyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="93482-142">Replace the value of *serviceUri* with the service URI from earlier.</span></span>

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample3.cs)]

<span data-ttu-id="93482-143">Uygulamayı çalıştırdığınızda, aşağıdakilerden çıkış yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="93482-143">When you run the app, it should output the following:</span></span>

[!code-console[Main](create-an-odata-v4-client-app/samples/sample4.cmd)]
