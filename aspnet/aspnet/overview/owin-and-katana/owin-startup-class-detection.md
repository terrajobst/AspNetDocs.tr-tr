---
uid: aspnet/overview/owin-and-katana/owin-startup-class-detection
title: OWıN başlangıç sınıfı algılama | Microsoft Docs
author: Praburaj
description: Bu öğreticide, hangi OWıN başlangıç sınıfının yüklendiğini nasıl yapılandıracağınız gösterilmektedir. OWıN hakkında daha fazla bilgi için bkz. proje Katana 'Ya genel bakış. Bu öğretici...
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 08257f55-36f4-4e39-9c88-2a5602838c79
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-startup-class-detection
msc.type: authoredcontent
ms.openlocfilehash: e1670c32049ec33dd4d1941a091a429d3929c452
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617049"
---
# <a name="owin-startup-class-detection"></a><span data-ttu-id="dc32e-105">OWIN Başlangıç Sınıfı Algılama</span><span class="sxs-lookup"><span data-stu-id="dc32e-105">OWIN Startup Class Detection</span></span>

> <span data-ttu-id="dc32e-106">Bu öğreticide, hangi OWıN başlangıç sınıfının yüklendiğini nasıl yapılandıracağınız gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="dc32e-106">This tutorial shows how to configure which OWIN startup class is loaded.</span></span> <span data-ttu-id="dc32e-107">OWıN hakkında daha fazla bilgi için bkz. [Proje Katana 'Ya genel bakış](an-overview-of-project-katana.md).</span><span class="sxs-lookup"><span data-stu-id="dc32e-107">For more information on OWIN, see [An Overview of Project Katana](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="dc32e-108">Bu öğretici, Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ), Praburaj Thiagarajan ve Howard dierking ( [@howard\_Dierking](https://twitter.com/howard_dierking) ) tarafından yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="dc32e-108">This tutorial was written by Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ), Praburaj Thiagarajan, and Howard Dierking ( [@howard\_dierking](https://twitter.com/howard_dierking) ).</span></span>
>
> ## <a name="prerequisites"></a><span data-ttu-id="dc32e-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="dc32e-109">Prerequisites</span></span>
>
> [<span data-ttu-id="dc32e-110">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="dc32e-110">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)

## <a name="owin-startup-class-detection"></a><span data-ttu-id="dc32e-111">OWIN Başlangıç Sınıfı Algılama</span><span class="sxs-lookup"><span data-stu-id="dc32e-111">OWIN Startup Class Detection</span></span>

 <span data-ttu-id="dc32e-112">Her OWıN uygulamasının, uygulama ardışık düzeni için bileşenleri belirttiğiniz bir başlangıç sınıfı vardır.</span><span class="sxs-lookup"><span data-stu-id="dc32e-112">Every OWIN Application has a startup class where you specify components for the application pipeline.</span></span> <span data-ttu-id="dc32e-113">Seçtiğiniz barındırma modeline (OwinHost, IIS ve IIS-Express) bağlı olarak, başlangıç sınıfınızı çalışma zamanına bağlamak için kullanabileceğiniz farklı yollar vardır.</span><span class="sxs-lookup"><span data-stu-id="dc32e-113">There are different ways you can connect your startup class with the runtime, depending on the hosting model you choose (OwinHost, IIS, and IIS-Express).</span></span> <span data-ttu-id="dc32e-114">Bu öğreticide gösterilen başlangıç sınıfı, her barındırma uygulamasında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="dc32e-114">The startup class shown in this tutorial can be used in every hosting application.</span></span> <span data-ttu-id="dc32e-115">Aşağıdaki yaklaşımlardan birini kullanarak başlangıç sınıfını barındırma çalışma zamanına bağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="dc32e-115">You connect the startup class with the hosting runtime using one of the these approaches:</span></span>

1. <span data-ttu-id="dc32e-116">**Adlandırma kuralı**: Katana, derleme adı veya genel ad alanıyla eşleşen ad alanında `Startup` adlı bir sınıfı arar.</span><span class="sxs-lookup"><span data-stu-id="dc32e-116">**Naming Convention**: Katana looks for a class named `Startup` in namespace matching the assembly name or the global namespace.</span></span>
2. <span data-ttu-id="dc32e-117">**Owinstartup özniteliği**: Bu, çoğu geliştiricilerin başlangıç sınıfını belirtmek için gereken yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="dc32e-117">**OwinStartup Attribute**: This is the approach most developers will take to specify the startup class.</span></span> <span data-ttu-id="dc32e-118">Aşağıdaki öznitelik, başlangıç sınıfını `StartupDemo` ad alanındaki `TestStartup` sınıfına ayarlar.</span><span class="sxs-lookup"><span data-stu-id="dc32e-118">The following attribute will set the startup class to the `TestStartup` class in the `StartupDemo` namespace.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample1.cs)]

   <span data-ttu-id="dc32e-119">`OwinStartup` öznitelik, adlandırma kuralını geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="dc32e-119">The `OwinStartup` attribute overrides the naming convention.</span></span> <span data-ttu-id="dc32e-120">Ayrıca, Bu öznitelikle kolay bir ad belirtebilirsiniz, ancak kolay bir ad kullanmak için yapılandırma dosyasında `appSetting` öğesini de kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="dc32e-120">You can also specify a friendly name with this attribute, however, using a friendly name requires you to also use the `appSetting` element in the configuration file.</span></span>
3. <span data-ttu-id="dc32e-121">**Yapılandırma dosyasındaki appSetting öğesi**: `appSetting` öğesi `OwinStartup` özniteliğini ve adlandırma kuralını geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="dc32e-121">**The appSetting element in the Configuration file**: The `appSetting` element overrides the `OwinStartup` attribute and naming convention.</span></span> <span data-ttu-id="dc32e-122">Birden çok başlangıç sınıfına sahip olabilirsiniz (her biri bir `OwinStartup` özniteliği kullanarak) ve aşağıdakine benzer bir biçimlendirme kullanarak bir yapılandırma dosyasına hangi başlangıç sınıfının yükleneceğini yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="dc32e-122">You can have multiple startup classes (each using an `OwinStartup` attribute) and configure which startup class will be loaded in a configuration file using markup similar to the following:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample2.xml)]

   <span data-ttu-id="dc32e-123">Başlangıç sınıfını ve derlemeyi açıkça belirten aşağıdaki anahtar de kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="dc32e-123">The following key, which explicitly specifies the startup class and assembly can also be used:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample3.xml)]

   <span data-ttu-id="dc32e-124">Yapılandırma dosyasındaki aşağıdaki XML `ProductionConfiguration`kolay bir başlangıç sınıfı adı belirtir.</span><span class="sxs-lookup"><span data-stu-id="dc32e-124">The following XML in the configuration file specifies a friendly startup class name of `ProductionConfiguration`.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample4.xml)]

   <span data-ttu-id="dc32e-125">Yukarıdaki biçimlendirme, kolay bir ad belirten ve `ProductionStartup2` sınıfının çalışmasına neden olan aşağıdaki `OwinStartup` özniteliğiyle kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="dc32e-125">The above markup must be used with the following `OwinStartup` attribute which specifies a friendly name and causes the `ProductionStartup2` class to run.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample5.cs?highlight=1,16)]
4. <span data-ttu-id="dc32e-126">OWıN başlangıç bulmayı devre dışı bırakmak için, Web. config dosyasında `"false"` bir değeri ile `appSetting owin:AutomaticAppStartup` ekleyin.</span><span class="sxs-lookup"><span data-stu-id="dc32e-126">To disable OWIN startup discovery add the `appSetting owin:AutomaticAppStartup` with a value of `"false"` in the web.config file.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample6.xml)]

## <a name="create-an-aspnet-web-app-using-owin-startup"></a><span data-ttu-id="dc32e-127">OWıN başlangıcını kullanarak bir ASP.NET Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="dc32e-127">Create an ASP.NET Web App using OWIN Startup</span></span>

1. <span data-ttu-id="dc32e-128">Boş bir Asp.Net Web uygulaması oluşturun ve bunu **Startupdemo**olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="dc32e-128">Create an empty Asp.Net web application and name it **StartupDemo**.</span></span> <span data-ttu-id="dc32e-129">-NuGet Paket Yöneticisi 'ni kullanarak `Microsoft.Owin.Host.SystemWeb` 'i yükler.</span><span class="sxs-lookup"><span data-stu-id="dc32e-129">- Install `Microsoft.Owin.Host.SystemWeb` using the NuGet package manager.</span></span> <span data-ttu-id="dc32e-130">**Araçlar** menüsünde, **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="dc32e-130">From the **Tools** menu, select **NuGet Package Manager**, and then **Package Manager Console**.</span></span> <span data-ttu-id="dc32e-131">Aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="dc32e-131">Enter the following command:</span></span>

    [!code-powershell[Main](owin-startup-class-detection/samples/sample7.ps1)]
2. <span data-ttu-id="dc32e-132">Bir OWıN başlangıç sınıfı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="dc32e-132">Add an OWIN startup class.</span></span> <span data-ttu-id="dc32e-133">Visual Studio 2017 ' de projeye sağ tıklayın ve **Sınıf Ekle**' yi seçin.- **Yeni öğe Ekle** iletişim kutusunda, arama alanına *owın* girin ve adı Startup.cs olarak değiştirin ve ardından **Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="dc32e-133">In Visual Studio 2017 right-click the project and select **Add Class**.- In the **Add New Item** dialog box, enter *OWIN* in the search field, and change the name to Startup.cs, and then select **Add**.</span></span>

     ![](owin-startup-class-detection/_static/image1.png)

   <span data-ttu-id="dc32e-134">*Owın başlangıç sınıfını*bir dahaki sefer eklemek Istediğinizde, **Ekle** menüsünde kullanılabilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="dc32e-134">The next time you want to add an *Owin Startup class*, it will be in available from the **Add** menu.</span></span>

     ![](owin-startup-class-detection/_static/image2.png)

   <span data-ttu-id="dc32e-135">Alternatif olarak, projeye sağ tıklayıp **Ekle**' yi ve ardından **Yeni öğe**' yi seçip **owın başlangıç sınıfını**seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dc32e-135">Alternatively, you can right-click the project and select **Add**, then select **New Item**, and then select the **Owin Startup class**.</span></span>

     ![](owin-startup-class-detection/_static/image3.png)

- <span data-ttu-id="dc32e-136">*Startup.cs* dosyasındaki oluşturulan kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="dc32e-136">Replace the generated code in the *Startup.cs* file with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample8.cs?highlight=5,7,15-28,31-34)]

  <span data-ttu-id="dc32e-137">`app.Use` lambda ifadesi, belirtilen ara yazılım bileşenini OWıN ardışık düzenine kaydetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dc32e-137">The `app.Use` lambda expression is used to register the specified middleware component to the OWIN pipeline.</span></span> <span data-ttu-id="dc32e-138">Bu durumda, gelen istek yanıtlanmadan önce gelen isteklerin günlüğe kaydedilmesini ayarlarız.</span><span class="sxs-lookup"><span data-stu-id="dc32e-138">In this case we are setting up logging of incoming requests before responding to the incoming request.</span></span> <span data-ttu-id="dc32e-139">`next` parametresi, işlem hattındaki sonraki bileşene yönelik temsilcidir ( [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) &lt; [Task](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx) &gt;).</span><span class="sxs-lookup"><span data-stu-id="dc32e-139">The `next` parameter is the delegate ( [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) &lt; [Task](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx) &gt; ) to the next component in the pipeline.</span></span> <span data-ttu-id="dc32e-140">`app.Run` lambda ifadesi, ardışık düzeni gelen isteklere takar ve yanıt mekanizmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="dc32e-140">The `app.Run` lambda expression hooks up the pipeline to incoming requests and provides the response mechanism.</span></span>
     > [!NOTE]
     > <span data-ttu-id="dc32e-141">Yukarıdaki kodda `OwinStartup` özniteliği kullanıma sunuyoruz ve `Startup` adlı sınıfı çalıştırma kuralına ulaştınız.-uygulamayı çalıştırmak için ***F5*** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="dc32e-141">In the code above we have commented out the `OwinStartup` attribute and we're relying on the convention of running the class named `Startup` .- Press ***F5*** to run the application.</span></span> <span data-ttu-id="dc32e-142">Birkaç kez Yenile 'yi ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="dc32e-142">Hit refresh a few times.</span></span>

    <span data-ttu-id="dc32e-143">![](owin-startup-class-detection/_static/image4.png) Not: Bu öğreticideki resimlerde gösterilen sayı gördüğünüz sayıyla eşleşmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="dc32e-143">![](owin-startup-class-detection/_static/image4.png) Note: The number shown in the images in this tutorial will not match the number you see.</span></span> <span data-ttu-id="dc32e-144">Milisaniyelik dize, sayfayı yenilediğinizde yeni bir yanıt göstermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dc32e-144">The millisecond string is used to show a new response when you refresh the page.</span></span>
  <span data-ttu-id="dc32e-145">İzleme bilgilerini **Çıkış** penceresinde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dc32e-145">You can see the trace information in the **Output** window.</span></span>

    ![](owin-startup-class-detection/_static/image5.png)

## <a name="add-more-startup-classes"></a><span data-ttu-id="dc32e-146">Daha fazla başlangıç sınıfı ekleyin</span><span class="sxs-lookup"><span data-stu-id="dc32e-146">Add More Startup Classes</span></span>

<span data-ttu-id="dc32e-147">Bu bölümde, başka bir başlangıç sınıfı ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="dc32e-147">In this section we'll add another Startup class.</span></span> <span data-ttu-id="dc32e-148">Uygulamanıza birden çok OWıN başlangıç sınıfı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dc32e-148">You can add multiple OWIN startup class to your application.</span></span> <span data-ttu-id="dc32e-149">Örneğin, geliştirme, test ve üretim için başlangıç sınıfları oluşturmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dc32e-149">For example, you might want to create startup classes for development, testing and production.</span></span>

1. <span data-ttu-id="dc32e-150">Yeni bir OWıN başlangıç sınıfı oluşturun ve `ProductionStartup`adlandırın.</span><span class="sxs-lookup"><span data-stu-id="dc32e-150">Create a new OWIN Startup class and name it `ProductionStartup`.</span></span>
2. <span data-ttu-id="dc32e-151">Oluşturulan kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="dc32e-151">Replace the generated code with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample9.cs?highlight=14-18)]
3. <span data-ttu-id="dc32e-152">Uygulamayı çalıştırmak için Control F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="dc32e-152">Press Control F5 to run the app.</span></span> <span data-ttu-id="dc32e-153">`OwinStartup` özniteliği üretim başlangıç sınıfının çalıştırıldığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="dc32e-153">The `OwinStartup` attribute specifies the production startup class is run.</span></span>

    ![](owin-startup-class-detection/_static/image6.png)
4. <span data-ttu-id="dc32e-154">Başka bir OWıN başlangıç sınıfı oluşturun ve `TestStartup`adlandırın.</span><span class="sxs-lookup"><span data-stu-id="dc32e-154">Create another OWIN Startup class and name it `TestStartup`.</span></span>
5. <span data-ttu-id="dc32e-155">Oluşturulan kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="dc32e-155">Replace the generated code with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample10.cs?highlight=6,14-18)]

   <span data-ttu-id="dc32e-156">Yukarıdaki `OwinStartup` özniteliği aşırı yüklemesi başlangıç sınıfının *kolay* adı olarak `TestingConfiguration` belirtir.</span><span class="sxs-lookup"><span data-stu-id="dc32e-156">The `OwinStartup` attribute overload above specifies `TestingConfiguration` as the *friendly* name of the Startup class.</span></span>
6. <span data-ttu-id="dc32e-157">*Web. config* dosyasını açın ve başlangıç sınıfının kolay adını belirten Owın uygulama başlangıç anahtarını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="dc32e-157">Open the *web.config* file and add the OWIN App startup key which specifies the friendly name of the Startup class:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample11.xml?highlight=3-5)]
7. <span data-ttu-id="dc32e-158">Uygulamayı çalıştırmak için Control F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="dc32e-158">Press Control F5 to run the app.</span></span> <span data-ttu-id="dc32e-159">Uygulama ayarları öğesi bundan sonra, test yapılandırması çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="dc32e-159">The app settings element takes precedent, and the test configuration is run.</span></span>

    ![](owin-startup-class-detection/_static/image7.png)
8. <span data-ttu-id="dc32e-160">`TestStartup` sınıfındaki `OwinStartup` özniteliğinden *kolay* adı kaldırın.</span><span class="sxs-lookup"><span data-stu-id="dc32e-160">Remove the *friendly* name from the `OwinStartup` attribute in the `TestStartup` class.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample12.cs)]
9. <span data-ttu-id="dc32e-161">*Web. config* dosyasındaki Owın uygulama başlangıç anahtarını aşağıdakiler ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="dc32e-161">Replace the OWIN App startup key in the *web.config* file with the following:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample13.xml)]
10. <span data-ttu-id="dc32e-162">Her sınıftaki `OwinStartup` özniteliğini, Visual Studio tarafından oluşturulan varsayılan öznitelik koduna döndürür:</span><span class="sxs-lookup"><span data-stu-id="dc32e-162">Revert the `OwinStartup` attribute in each class to the default attribute code generated by Visual Studio:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample14.cs)]

    <span data-ttu-id="dc32e-163">Aşağıdaki OWIN uygulama başlangıç anahtarlarının her biri, üretim sınıfının çalışmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="dc32e-163">Each of the OWIN App startup keys below will cause the production class to run.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample15.xml)]

    <span data-ttu-id="dc32e-164">Son başlangıç anahtarı başlangıç yapılandırma yöntemini belirtir.</span><span class="sxs-lookup"><span data-stu-id="dc32e-164">The last startup key specifies the startup configuration method.</span></span> <span data-ttu-id="dc32e-165">Aşağıdaki OWIN uygulama başlangıç anahtarı, yapılandırma sınıfının adını `MyConfiguration` değiştirmenize izin verir.</span><span class="sxs-lookup"><span data-stu-id="dc32e-165">The following OWIN App startup key allows you to change the name of the configuration class to `MyConfiguration` .</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample16.xml)]

## <a name="using-owinhostexe"></a><span data-ttu-id="dc32e-166">Owinhost. exe kullanma</span><span class="sxs-lookup"><span data-stu-id="dc32e-166">Using Owinhost.exe</span></span>

1. <span data-ttu-id="dc32e-167">Web. config dosyasını aşağıdaki biçimlendirme ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="dc32e-167">Replace the Web.config file with the following markup:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample17.xml?highlight=3-6)]

   <span data-ttu-id="dc32e-168">Bu durumda `TestStartup`, son anahtar kazanır.</span><span class="sxs-lookup"><span data-stu-id="dc32e-168">The last key wins, so in this case `TestStartup` is specified.</span></span>
2. <span data-ttu-id="dc32e-169">PMC 'den Owinhost 'u yükler:</span><span class="sxs-lookup"><span data-stu-id="dc32e-169">Install Owinhost from the PMC:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample18.cmd)]
3. <span data-ttu-id="dc32e-170">Uygulama klasörüne ( *Web. config* dosyasını içeren klasör) gidin ve komut istemine şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="dc32e-170">Navigate to the application folder (the folder containing the *Web.config* file) and in a command prompt and type:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample19.cmd)]

   <span data-ttu-id="dc32e-171">Komut penceresinde şunları gösterilecektir:</span><span class="sxs-lookup"><span data-stu-id="dc32e-171">The command window will show:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample20.cmd)]
4. <span data-ttu-id="dc32e-172">URL `http://localhost:5000/`bir tarayıcı başlatın.</span><span class="sxs-lookup"><span data-stu-id="dc32e-172">Launch a browser with the URL `http://localhost:5000/`.</span></span>

    ![](owin-startup-class-detection/_static/image8.png)

   <span data-ttu-id="dc32e-173">OwinHost, yukarıda listelenen başlangıç kurallarını kabul eden bir.</span><span class="sxs-lookup"><span data-stu-id="dc32e-173">OwinHost honored the startup conventions listed above.</span></span>
5. <span data-ttu-id="dc32e-174">Komut penceresinde, OwinHost programından çıkmak için ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="dc32e-174">In the command window, press Enter to exit OwinHost.</span></span>
6. <span data-ttu-id="dc32e-175">`ProductionStartup` sınıfında, bir *Üretim yapılandırmasının*kolay adını belirten aşağıdaki Owınstartup özniteliğini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="dc32e-175">In the `ProductionStartup` class, add the following OwinStartup attribute which specifies a friendly name of *ProductionConfiguration*.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample21.cs)]
7. <span data-ttu-id="dc32e-176">Komut istemine şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="dc32e-176">In the command prompt and type:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample22.cmd)]

   <span data-ttu-id="dc32e-177">Üretim başlangıç sınıfı yüklenir.</span><span class="sxs-lookup"><span data-stu-id="dc32e-177">The Production startup class is loaded.</span></span>
    ![](owin-startup-class-detection/_static/image9.png)

   <span data-ttu-id="dc32e-178">Uygulamamız birden çok başlangıç sınıfına sahiptir ve bu örnekte, çalışma zamanına kadar hangi başlangıç sınıfının yükleneceğini erteliyoruz.</span><span class="sxs-lookup"><span data-stu-id="dc32e-178">Our application has multiple startup classes, and in this example we have deferred which startup class to load until runtime.</span></span>
8. <span data-ttu-id="dc32e-179">Aşağıdaki çalışma zamanı başlatma seçeneklerini sınayın:</span><span class="sxs-lookup"><span data-stu-id="dc32e-179">Test the following runtime startup options:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample23.cmd)]
