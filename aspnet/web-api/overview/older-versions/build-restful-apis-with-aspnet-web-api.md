---
uid: web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
title: ASP.NET Web API 'SI ile yeniden takip eden API 'Ler oluşturun-ASP.NET 4. x
author: rick-anderson
description: "Uygulamalı laboratuvar: bir Contact Manager uygulaması için basit bir REST API derlemek için ASP.NET 4. x içindeki Web API 'sini kullanın."
ms.author: riande
ms.date: 02/18/2013
ms.custom: seoapril2019
ms.assetid: 87daa99f-3810-407e-b969-dd28a192959d
msc.legacyurl: /web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 35b115d6b4f84084e78e429bbb4842670e57bba4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78621816"
---
# <a name="build-restful-apis-with-aspnet-web-api"></a><span data-ttu-id="fa1f3-103">ASP.NET Web API 'SI ile yeniden takip eden API 'Ler oluşturun</span><span class="sxs-lookup"><span data-stu-id="fa1f3-103">Build RESTful APIs with ASP.NET Web API</span></span>

<span data-ttu-id="fa1f3-104">[Web 'de Camps ekibine](https://twitter.com/webcamps) göre</span><span class="sxs-lookup"><span data-stu-id="fa1f3-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="fa1f3-105">Uygulamalı laboratuvar: bir Contact Manager uygulaması için basit bir REST API derlemek için ASP.NET 4. x içindeki Web API 'sini kullanın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-105">Hands on lab: Use Web API in ASP.NET 4.x to build a simple REST API for a contact manager application.</span></span> <span data-ttu-id="fa1f3-106">Ayrıca API 'yi kullanmak için bir istemci oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-106">You will also build a client to consume the API.</span></span>

<span data-ttu-id="fa1f3-107">Son yıllarda, HTTP 'nin yalnızca HTML sayfaları sunmak için değil net ' in açık olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-107">In recent years, it has become clear that HTTP is not just for serving up HTML pages.</span></span> <span data-ttu-id="fa1f3-108">Ayrıca, Web API 'Leri oluşturmaya yönelik güçlü bir platformdur, bir dizi fiil (GET, POST, vb.) ve *URI 'ler* ve *üstbilgiler*gibi birkaç basit kavram vardır.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-108">It is also a powerful platform for building Web APIs, using a handful of verbs (GET, POST, and so forth) plus a few simple concepts such as *URIs* and *headers*.</span></span> <span data-ttu-id="fa1f3-109">ASP.NET Web API 'SI, HTTP programlamasını basitleştiren bir bileşen kümesidir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-109">ASP.NET Web API is a set of components that simplify HTTP programming.</span></span> <span data-ttu-id="fa1f3-110">ASP.NET MVC çalışma zamanının üzerine inşa edildiğinden, Web API 'SI, HTTP 'nin alt düzey aktarım ayrıntılarını otomatik olarak işler.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-110">Because it is built on top of the ASP.NET MVC runtime, Web API automatically handles the low-level transport details of HTTP.</span></span> <span data-ttu-id="fa1f3-111">Aynı zamanda, Web API 'SI HTTP programlama modelini doğal olarak kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-111">At the same time, Web API naturally exposes the HTTP programming model.</span></span> <span data-ttu-id="fa1f3-112">Aslında, Web API 'sinin bir hedefi HTTP 'nin gerçekliği dışında bir amaç *değildir* .</span><span class="sxs-lookup"><span data-stu-id="fa1f3-112">In fact, one goal of Web API is to *not* abstract away the reality of HTTP.</span></span> <span data-ttu-id="fa1f3-113">Sonuç olarak, Web API 'sinin her ikisi de esnektir ve kolayca genişletilir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-113">As a result, Web API is both flexible and easy to extend.</span></span>  <span data-ttu-id="fa1f3-114">REST mimari stili HTTP 'den yararlanmak için etkili bir yöntem olarak kendini kanıtlamış ve HTTP için geçerli tek yaklaşım olmasa da</span><span class="sxs-lookup"><span data-stu-id="fa1f3-114">The REST architectural style has proven to be an effective way to leverage HTTP - although it is certainly not the only valid approach to HTTP.</span></span> <span data-ttu-id="fa1f3-115">İlgili kişi Yöneticisi, diğer kişiler arasında kişileri listelemek, eklemek ve kaldırmak için bir daha sunacaktır.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-115">The contact manager will expose the RESTful for listing, adding and removing contacts, among others.</span></span> 

<span data-ttu-id="fa1f3-116">Bu laboratuvar, HTTP, REST ve temel bir HTML, JavaScript ve jQuery hakkında temel bir bilginiz olduğunu varsaymaktadır.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-116">This lab requires a basic understanding of HTTP, REST, and assumes you have a basic working knowledge of HTML, JavaScript, and jQuery.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="fa1f3-117">ASP.NET Web sitesi, [https://asp.net/web-api](https://asp.net/web-api)ADRESINDEKI Web API çerçevesine adanmış bir alana sahiptir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-117">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [https://asp.net/web-api](https://asp.net/web-api).</span></span> <span data-ttu-id="fa1f3-118">Bu site, Web API 'siyle ilgili en son bilgileri, örnekleri ve haberleri sağlamaya devam edecek, bu nedenle neredeyse tüm cihazlar veya geliştirme çerçevesiyle sunulan özel Web API 'Leri oluşturma sanatı hakkında daha ayrıntılı bilgi almak istiyorsanız, sık sık kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-118">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>
> > 
> > <span data-ttu-id="fa1f3-119">ASP.NET MVC 4 ' e benzer ASP.NET Web API 'SI, hizmet katmanını denetleyicilerden ayırmak açısından çok daha fazla esneklik sağlar. Bu, kullanılabilir bağımlılık ekleme çerçevelerinin birkaçını oldukça kolay kullanmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-119">ASP.NET Web API, similar to ASP.NET MVC 4, has great flexibility in terms of separating the service layer from the controllers allowing you to use several of the available Dependency Injection frameworks fairly easy.</span></span> <span data-ttu-id="fa1f3-120">MSDN 'de, [buradan](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)yükleyebileceğiniz bir ASP.NET Web API projesinde bağımlılık ekleme Için neklemesine nasıl kullanacağınızı gösteren iyi bir örnek vardır.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-120">There is a good sample in MSDN that shows how to use Ninject for dependency injection in an ASP.NET Web API project that you can download it from [here](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7).</span></span>
> 
> 
> <span data-ttu-id="fa1f3-121">Tüm örnek kod ve kod parçacıkları [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)adresinden erişilebilen Web Camps eğitim seti ' ne dahildir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-121">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="fa1f3-122">Amaçlar</span><span class="sxs-lookup"><span data-stu-id="fa1f3-122">Objectives</span></span>

<span data-ttu-id="fa1f3-123">Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="fa1f3-123">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="fa1f3-124">Yeniden takip eden bir Web API 'SI uygulama</span><span class="sxs-lookup"><span data-stu-id="fa1f3-124">Implement a RESTful Web API</span></span>
- <span data-ttu-id="fa1f3-125">Bir HTML istemcisinden API çağırma</span><span class="sxs-lookup"><span data-stu-id="fa1f3-125">Call the API from an HTML client</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="fa1f3-126">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="fa1f3-126">Prerequisites</span></span>

<span data-ttu-id="fa1f3-127">Bu uygulamalı laboratuvarın tamamlanabilmesi için aşağıdakiler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="fa1f3-127">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="fa1f3-128">[Web veya üst için Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (nasıl yükleneceğine ilişkin yönergeler Için [Ek B](#AppendixB) 'yi okuyun).</span><span class="sxs-lookup"><span data-stu-id="fa1f3-128">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="fa1f3-129">Kurulum</span><span class="sxs-lookup"><span data-stu-id="fa1f3-129">Setup</span></span>

<span data-ttu-id="fa1f3-130">**Kod parçacıklarını yükleme**</span><span class="sxs-lookup"><span data-stu-id="fa1f3-130">**Installing Code Snippets**</span></span>

<span data-ttu-id="fa1f3-131">Kolaylık olması için, bu laboratuvar boyunca yönettiğiniz kodun çoğu Visual Studio kod parçacıkları olarak sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-131">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="fa1f3-132">Kod parçacıklarını yüklemek için **.\Source\Setup\CodeSnippets.vsi** dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-132">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="fa1f3-133">Visual Studio Code parçacıkları hakkında bilginiz yoksa ve bunları nasıl kullanacağınızı öğrenmek istiyorsanız, [Ek A: Ek A: kod parçacıkları&quot;kullanarak](#AppendixA) bu &quot;belgedeki eke başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-133">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="fa1f3-134">Alıştırmalarda</span><span class="sxs-lookup"><span data-stu-id="fa1f3-134">Exercises</span></span>

<span data-ttu-id="fa1f3-135">Bu uygulamalı laboratuvar aşağıdaki Alıştırmayı içerir:</span><span class="sxs-lookup"><span data-stu-id="fa1f3-135">This hands-on lab includes the following exercise:</span></span>

1. [<span data-ttu-id="fa1f3-136">Alıştırma 1: salt okunurdur Web API 'SI oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa1f3-136">Exercise 1: Create a Read-Only Web API</span></span>](#Exercise1)
2. [<span data-ttu-id="fa1f3-137">Alıştırma 2: okuma/yazma Web API 'SI oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa1f3-137">Exercise 2: Create a Read/Write Web API</span></span>](#Exercise2)
3. [<span data-ttu-id="fa1f3-138">Alıştırma 3: bir HTML Istemcisinden Web API 'sini kullanma</span><span class="sxs-lookup"><span data-stu-id="fa1f3-138">Exercise 3: Consume the Web API from an HTML Client</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="fa1f3-139">Her alıştırma, alıştırmaları tamamladıktan sonra elde etmeniz gereken sonuç çözümünü içeren bir **son** klasör ile birlikte sunulur.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-139">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="fa1f3-140">Bu çözümü, alýþtýrmalar üzerinden çalışarak daha fazla yardıma ihtiyacınız varsa kılavuz olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-140">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="fa1f3-141">Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **60 dakika**.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-141">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Create_a_Read-Only_Web_API"></a>
### <a name="exercise-1-create-a-read-only-web-api"></a><span data-ttu-id="fa1f3-142">Alıştırma 1: salt okunurdur Web API 'SI oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa1f3-142">Exercise 1: Create a Read-Only Web API</span></span>

<span data-ttu-id="fa1f3-143">Bu alıştırmada, Contact Manager için salt okunurdur GET yöntemlerini uygulayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-143">In this exercise, you will implement the read-only GET methods for the contact manager.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_API_Project"></a>
#### <a name="task-1---creating-the-api-project"></a><span data-ttu-id="fa1f3-144">Görev 1-API projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa1f3-144">Task 1 - Creating the API Project</span></span>

<span data-ttu-id="fa1f3-145">Bu görevde, yeni ASP.NET Web projesi şablonlarını kullanarak bir Web API web uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-145">In this task, you will use the new ASP.NET web project templates to create a Web API web application.</span></span>

1. <span data-ttu-id="fa1f3-146">**Web Için Visual Studio 2012 Express**'i çalıştırın. bunu yapmak için **başlat** 'a gidip **Web için vs Express** yazın ve **ENTER**tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-146">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="fa1f3-147">**Dosya** menüsünden **Yeni proje**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-147">From the **File** menu, select **New Project**.</span></span> <span data-ttu-id="fa1f3-148">**Görseli C# seçin |** Proje türü ağaç görünümünden Web projesi türü, sonra **ASP.NET MVC 4 Web uygulaması** proje türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-148">Select the **Visual C# | Web** project type from the project type tree view, then select the **ASP.NET MVC 4 Web Application** project type.</span></span> <span data-ttu-id="fa1f3-149">Projenin **adını** *ContactManager* , **çözüm adı** olarak ayarlayın ve ardından **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-149">Set the project's **Name** to *ContactManager* and the **Solution name** to *Begin*, then click **OK**.</span></span>

    <span data-ttu-id="fa1f3-150">![Yeni bir ASP.NET MVC 4,0 Web uygulaması projesi oluşturma](build-restful-apis-with-aspnet-web-api/_static/image1.png "Yeni bir ASP.NET MVC 4,0 Web uygulaması projesi oluşturma")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-150">![Creating a new ASP.NET MVC 4.0 Web Application Project](build-restful-apis-with-aspnet-web-api/_static/image1.png "Creating a new ASP.NET MVC 4.0 Web Application Project")</span></span>

    <span data-ttu-id="fa1f3-151">*Yeni bir ASP.NET MVC 4,0 Web uygulaması projesi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-151">*Creating a new ASP.NET MVC 4.0 Web Application Project*</span></span>
3. <span data-ttu-id="fa1f3-152">ASP.NET MVC 4 proje türü iletişim kutusunda **Web API 'si** proje türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-152">In the ASP.NET MVC 4 project type dialog, select the **Web API** project type.</span></span> <span data-ttu-id="fa1f3-153">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-153">Click **OK**.</span></span>

    <span data-ttu-id="fa1f3-154">![Web API proje türünü belirtme](build-restful-apis-with-aspnet-web-api/_static/image2.png "Web API proje türünü belirtme")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-154">![Specifying the Web API project type](build-restful-apis-with-aspnet-web-api/_static/image2.png "Specifying the Web API project type")</span></span>

    <span data-ttu-id="fa1f3-155">*Web API proje türünü belirtme*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-155">*Specifying the Web API project type*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_the_Contact_Manager_API_Controllers"></a>
#### <a name="task-2---creating-the-contact-manager-api-controllers"></a><span data-ttu-id="fa1f3-156">Görev 2-Contact Manager API denetleyicileri oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa1f3-156">Task 2 - Creating the Contact Manager API Controllers</span></span>

<span data-ttu-id="fa1f3-157">Bu görevde API yöntemlerinin bulunacağı denetleyici sınıflarını oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-157">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="fa1f3-158">**ValuesController.cs** adlı dosyayı **denetleyiciler** klasöründe projeden silin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-158">Delete the file named **ValuesController.cs** within **Controllers** folder from the project.</span></span>
2. <span data-ttu-id="fa1f3-159">Projedeki **denetleyiciler** klasörüne sağ tıklayın ve Ekle ' yi seçin **|** Bağlam menüsünden denetleyici.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-159">Right-click the **Controllers** folder in the project and select **Add | Controller** from the context menu.</span></span>

    <span data-ttu-id="fa1f3-160">![Projeye yeni bir denetleyici ekleniyor](build-restful-apis-with-aspnet-web-api/_static/image3.png "Projeye yeni bir denetleyici ekleniyor")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-160">![Adding a new controller to the project](build-restful-apis-with-aspnet-web-api/_static/image3.png "Adding a new controller to the project")</span></span>

    <span data-ttu-id="fa1f3-161">*Projeye yeni bir denetleyici ekleniyor*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-161">*Adding a new controller to the project*</span></span>
3. <span data-ttu-id="fa1f3-162">Görüntülenen **Denetleyici Ekle** iletişim kutusunda, şablon menüsünden **boş API denetleyicisi** ' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-162">In the **Add Controller** dialog that appears, select **Empty API Controller** from the Template menu.</span></span> <span data-ttu-id="fa1f3-163">Denetleyici sınıfına **contactcontroller**adını adlandırın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-163">Name the controller class **ContactController**.</span></span> <span data-ttu-id="fa1f3-164">Ardından Ekle ' ye tıklayın **.**</span><span class="sxs-lookup"><span data-stu-id="fa1f3-164">Then, click **Add.**</span></span>

    <span data-ttu-id="fa1f3-165">![Yeni bir Web API denetleyicisi oluşturmak için denetleyici Ekle iletişim kutusunu kullanma](build-restful-apis-with-aspnet-web-api/_static/image4.png "Yeni bir Web API denetleyicisi oluşturmak için denetleyici Ekle iletişim kutusunu kullanma")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-165">![Using the Add Controller dialog to create a new Web API controller](build-restful-apis-with-aspnet-web-api/_static/image4.png "Using the Add Controller dialog to create a new Web API controller")</span></span>

    <span data-ttu-id="fa1f3-166">*Yeni bir Web API denetleyicisi oluşturmak için denetleyici Ekle iletişim kutusunu kullanma*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-166">*Using the Add Controller dialog to create a new Web API controller*</span></span>
4. <span data-ttu-id="fa1f3-167">**Contactcontroller**'a aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-167">Add the following code to the **ContactController**.</span></span>

    <span data-ttu-id="fa1f3-168">(Kod parçacığı- *Web API Laboratuvarı-Ex01-Get API yöntemi*)</span><span class="sxs-lookup"><span data-stu-id="fa1f3-168">(Code Snippet - *Web API Lab - Ex01 - Get API Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample1.cs)]
5. <span data-ttu-id="fa1f3-169">Uygulamada hata ayıklamak için **F5**’e basın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-169">Press **F5** to debug the application.</span></span> <span data-ttu-id="fa1f3-170">Bir Web API projesi için varsayılan giriş sayfası görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-170">The default home page for a Web API project should appear.</span></span>

    <span data-ttu-id="fa1f3-171">![Bir ASP.NET Web API uygulamasının varsayılan giriş sayfası](build-restful-apis-with-aspnet-web-api/_static/image5.png "Bir ASP.NET Web API uygulamasının varsayılan giriş sayfası")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-171">![The default home page of an ASP.NET Web API application](build-restful-apis-with-aspnet-web-api/_static/image5.png "The default home page of an ASP.NET Web API application")</span></span>

    <span data-ttu-id="fa1f3-172">*Bir ASP.NET Web API uygulamasının varsayılan giriş sayfası*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-172">*The default home page of an ASP.NET Web API application*</span></span>
6. <span data-ttu-id="fa1f3-173">Internet Explorer penceresinde, **Geliştirici Araçları** penceresini açmak için **F12** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-173">In the Internet Explorer window, press the **F12** key to open the **Developer Tools** window.</span></span> <span data-ttu-id="fa1f3-174">**Ağ** sekmesine tıklayın ve ardından, pencereye ağ trafiği yakalamaya başlamak Için **Yakalamayı Başlat** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-174">Click the **Network** tab, and then click the **Start Capturing** button to begin capturing network traffic into the window.</span></span>

    <span data-ttu-id="fa1f3-175">![Ağ sekmesini açma ve ağ yakalamayı başlatma](build-restful-apis-with-aspnet-web-api/_static/image6.png "Ağ sekmesini açma ve ağ yakalamayı başlatma")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-175">![Opening the network tab and initiating network capture](build-restful-apis-with-aspnet-web-api/_static/image6.png "Opening the network tab and initiating network capture")</span></span>

    <span data-ttu-id="fa1f3-176">*Ağ sekmesini açma ve ağ yakalamayı başlatma*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-176">*Opening the network tab and initiating network capture*</span></span>
7. <span data-ttu-id="fa1f3-177">Tarayıcının adres çubuğuna URL 'YI **/api/Contact** ile ekleyin ve ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-177">Append the URL in the browser's address bar with **/api/contact** and press enter.</span></span> <span data-ttu-id="fa1f3-178">İletim ayrıntıları ağ yakalama penceresinde görünür.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-178">The transmission details will appear in the network capture window.</span></span> <span data-ttu-id="fa1f3-179">Yanıtın MIME türünün **Application/JSON**olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-179">Note that the response's MIME type is **application/json**.</span></span> <span data-ttu-id="fa1f3-180">Bu, varsayılan çıkış biçiminin JSON olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-180">This demonstrates how the default output format is JSON.</span></span>

    <span data-ttu-id="fa1f3-181">![Web API isteğinin çıkışını ağ görünümünde görüntüleme](build-restful-apis-with-aspnet-web-api/_static/image7.png "Web API isteğinin çıkışını ağ görünümünde görüntüleme")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-181">![Viewing the output of the Web API request in the Network view](build-restful-apis-with-aspnet-web-api/_static/image7.png "Viewing the output of the Web API request in the Network view")</span></span>

    <span data-ttu-id="fa1f3-182">*Web API isteğinin çıkışını ağ görünümünde görüntüleme*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-182">*Viewing the output of the Web API request in the Network view*</span></span>

    > [!NOTE]
    > <span data-ttu-id="fa1f3-183">Internet Explorer 10 ' un bu noktada varsayılan davranışı, kullanıcının Web API çağrısından kaynaklanan akışı kaydetmek veya açmak isteyip istememesini ister.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-183">Internet Explorer 10's default behavior at this point will be to ask if the user would like to save or open the stream resulting from the Web API call.</span></span> <span data-ttu-id="fa1f3-184">Çıktı, Web API URL çağrısının JSON sonucunu içeren bir metin dosyası olacaktır.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-184">The output will be a text file containing the JSON result of the Web API URL call.</span></span> <span data-ttu-id="fa1f3-185">Yanıt içeriğini geliştiriciler araç penceresi aracılığıyla izleyebilmek için iletişim kutusunu iptal etme.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-185">Do not cancel the dialog in order to be able to watch the response's content through Developers Tool window.</span></span>
8. <span data-ttu-id="fa1f3-186">Bu API çağrısının yanıtı hakkında daha fazla ayrıntı görmek için **ayrıntılı görünüme git** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-186">Click the **Go to detailed view** button to see more details about the response of this API call.</span></span>

    <span data-ttu-id="fa1f3-187">![Ayrıntılı görünüme geç](build-restful-apis-with-aspnet-web-api/_static/image8.png "Ayrıntılar görünümüne geç")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-187">![Switch to Detailed View](build-restful-apis-with-aspnet-web-api/_static/image8.png "Switch to Details View")</span></span>

    <span data-ttu-id="fa1f3-188">*Ayrıntılı görünüme geç*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-188">*Switch to Detailed View*</span></span>
9. <span data-ttu-id="fa1f3-189">Gerçek JSON yanıt metnini görüntülemek için **yanıt gövdesi** sekmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-189">Click the **Response body** tab to view the actual JSON response text.</span></span>

    <span data-ttu-id="fa1f3-190">![Ağ izleyicisinde JSON çıkış metnini görüntüleme](build-restful-apis-with-aspnet-web-api/_static/image9.png "Ağ izleyicisinde JSON çıkış metnini görüntüleme")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-190">![Viewing the JSON output text in the network monitor](build-restful-apis-with-aspnet-web-api/_static/image9.png "Viewing the JSON output text in the network monitor")</span></span>

    <span data-ttu-id="fa1f3-191">*Ağ izleyicisinde JSON çıkış metnini görüntüleme*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-191">*Viewing the JSON output text in the network monitor*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Creating_the_Contact_Models_and_Augment_the_Contact_Controller"></a>
#### <a name="task-3---creating-the-contact-models-and-augment-the-contact-controller"></a><span data-ttu-id="fa1f3-192">Görev 3-Iletişim modellerini oluşturma ve Iletişim denetleyicisi 'ni artırmak</span><span class="sxs-lookup"><span data-stu-id="fa1f3-192">Task 3 - Creating the Contact Models and Augment the Contact Controller</span></span>

<span data-ttu-id="fa1f3-193">Bu görevde API yöntemlerinin bulunacağı denetleyici sınıflarını oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-193">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="fa1f3-194">**Modeller** klasörüne sağ tıklayın ve Ekle ' yi seçin **| Sınıf...** bağlam menüsünden.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-194">Right-click the **Models** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="fa1f3-195">![Web uygulamasına yeni model ekleme](build-restful-apis-with-aspnet-web-api/_static/image10.png "Web uygulamasına yeni model ekleme")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-195">![Adding a new model to the web application](build-restful-apis-with-aspnet-web-api/_static/image10.png "Adding a new model to the web application")</span></span>

    <span data-ttu-id="fa1f3-196">*Web uygulamasına yeni model ekleme*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-196">*Adding a new model to the web application*</span></span>
2. <span data-ttu-id="fa1f3-197">**Yeni öğe Ekle** iletişim kutusunda yeni dosyayı **Contact.cs** olarak adlandırın ve Ekle ' ye tıklayın **.**</span><span class="sxs-lookup"><span data-stu-id="fa1f3-197">In the **Add New Item** dialog, name the new file **Contact.cs** and click **Add.**</span></span>

    <span data-ttu-id="fa1f3-198">![Yeni kişi sınıfı dosyası oluşturuluyor](build-restful-apis-with-aspnet-web-api/_static/image11.png "Yeni kişi sınıfı dosyası oluşturuluyor")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-198">![Creating the new Contact class file](build-restful-apis-with-aspnet-web-api/_static/image11.png "Creating the new Contact class file")</span></span>

    <span data-ttu-id="fa1f3-199">*Yeni kişi sınıfı dosyası oluşturuluyor*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-199">*Creating the new Contact class file*</span></span>
3. <span data-ttu-id="fa1f3-200">Aşağıdaki Vurgulanan kodu **kişi** sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-200">Add the following highlighted code to the **Contact** class.</span></span>

    <span data-ttu-id="fa1f3-201">(Kod parçacığı- *Web API Laboratuvarı-Ex01-Contact sınıfı*)</span><span class="sxs-lookup"><span data-stu-id="fa1f3-201">(Code Snippet - *Web API Lab - Ex01 - Contact Class*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample2.cs)]
4. <span data-ttu-id="fa1f3-202">**Contactcontroller** sınıfında, **Get** yönteminin yöntem tanımında Word **dizesini** seçin ve Word *kişisi*yazın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-202">In the **ContactController** class, select the word **string** in method definition of the **Get** method, and type the word *Contact*.</span></span> <span data-ttu-id="fa1f3-203">Sözcük içine yazıldıktan sonra, sözcük **kişisinin**başlangıcında bir gösterge görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-203">Once the word is typed in, an indicator will appear at the beginning of the word **Contact**.</span></span> <span data-ttu-id="fa1f3-204">**CTRL** tuşunu basılı tutun ve nokta (.) tuşuna basın ya da farenizi kullanarak, modeller ad alanı için **using** yönergesini otomatik olarak doldurmanız için farenizi kullanarak simge simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-204">Either hold down the **Ctrl** key and press the period (.) key or click the icon using your mouse to open up the assistance dialog in the code editor, to automatically fill in the **using** directive for the Models namespace.</span></span>

    ![Ad alanı bildirimleri için IntelliSense yardımını kullanma](build-restful-apis-with-aspnet-web-api/_static/image12.png)

    <span data-ttu-id="fa1f3-206">*Ad alanı bildirimleri için IntelliSense yardımını kullanma*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-206">*Using Intellisense assistance for namespace declarations*</span></span>
5. <span data-ttu-id="fa1f3-207">**Get** yöntemi için kodu değiştirin, böylece bir iletişim modeli örnekleri dizisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-207">Modify the code for the **Get** method so that it returns an array of Contact model instances.</span></span>

    <span data-ttu-id="fa1f3-208">(Kod parçacığı- *Web API Laboratuvarı-Ex01-kişiler listesi döndürülüyor*)</span><span class="sxs-lookup"><span data-stu-id="fa1f3-208">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample3.cs)]
6. <span data-ttu-id="fa1f3-209">Tarayıcıdaki Web uygulamasında hata ayıklamak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-209">Press **F5** to debug the web application in the browser.</span></span> <span data-ttu-id="fa1f3-210">API 'nin yanıt çıkışında yapılan değişiklikleri görüntülemek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-210">To view the changes made to the response output of the API, perform the following steps.</span></span>

   1. <span data-ttu-id="fa1f3-211">Tarayıcı açıldıktan sonra geliştirici araçları henüz açık değilse **F12** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-211">Once the browser opens, press **F12** if the developer tools are not open yet.</span></span>
   2. <span data-ttu-id="fa1f3-212">**Ağ** sekmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-212">Click the **Network** tab.</span></span>
   3. <span data-ttu-id="fa1f3-213">**Yakalamayı Başlat** düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-213">Press the **Start Capturing** button.</span></span>
   4. <span data-ttu-id="fa1f3-214">**/Api/Contact** URL sonekini adres çubuğundaki URL 'ye ekleyin ve **ENTER** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-214">Add the URL suffix **/api/contact** to the URL in the address bar and press the **Enter** key.</span></span>
   5. <span data-ttu-id="fa1f3-215">**Ayrıntılı görünüme git** düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-215">Press the **Go to detailed view** button.</span></span>
   6. <span data-ttu-id="fa1f3-216">**Yanıt gövdesi** sekmesini seçin. Bir kişi örnekleri dizisinin seri hale getirilmiş formunu temsil eden bir JSON dizesi görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-216">Select the **Response body** tab. You should see a JSON string representing the serialized form of an array of Contact instances.</span></span>

      <span data-ttu-id="fa1f3-217">![Karmaşık bir Web API yöntemi çağrısının JSON seri hale getirilmiş çıkışı](build-restful-apis-with-aspnet-web-api/_static/image13.png "Karmaşık bir Web API yöntemi çağrısının JSON seri hale getirilmiş çıkışı")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-217">![JSON serialized output of a complex Web API method call](build-restful-apis-with-aspnet-web-api/_static/image13.png "JSON serialized output of a complex Web API method call")</span></span>

      <span data-ttu-id="fa1f3-218">*Karmaşık bir Web API yöntemi çağrısının JSON seri hale getirilmiş çıkışı*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-218">*JSON serialized output of a complex Web API method call*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Extracting_Functionality_into_a_Service_Layer"></a>
#### <a name="task-4---extracting-functionality-into-a-service-layer"></a><span data-ttu-id="fa1f3-219">Görev 4-bir hizmet katmanına Işlevsellik ayıklama</span><span class="sxs-lookup"><span data-stu-id="fa1f3-219">Task 4 - Extracting Functionality into a Service Layer</span></span>

<span data-ttu-id="fa1f3-220">Bu görev, geliştiricilerin hizmet işlevlerini denetleyici katmanından ayırmasını kolaylaştırmak için işlevselliği bir hizmet katmanına nasıl çıkarabileceğinizi gösterir ve böylelikle işi gerçekten yapan hizmetlerin yeniden kullanılabilirliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-220">This task will demonstrate how to extract functionality into a Service layer to make it easy for developers to separate their service functionality from the controller layer, thereby allowing reusability of the services that actually do the work.</span></span>

1. <span data-ttu-id="fa1f3-221">Çözüm kökünde yeni bir klasör oluşturun ve BT **Hizmetleri**olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-221">Create a new folder in the solution root and name it **Services**.</span></span> <span data-ttu-id="fa1f3-222">Bunu yapmak için **ContactManager** projesi ' ne sağ tıklayın, **Yeni | klasör** **Ekle** ' yi seçin, BT *Hizmetleri*olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-222">To do this, right-click **ContactManager** project, select **Add** | **New Folder**, name it *Services*.</span></span>

    <span data-ttu-id="fa1f3-223">![Hizmetler klasörü oluşturuluyor](build-restful-apis-with-aspnet-web-api/_static/image14.png "Hizmetler klasörü oluşturuluyor")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-223">![Creating Services folder](build-restful-apis-with-aspnet-web-api/_static/image14.png "Creating Services folder")</span></span>

    <span data-ttu-id="fa1f3-224">*Hizmetler klasörü oluşturuluyor*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-224">*Creating Services folder*</span></span>
2. <span data-ttu-id="fa1f3-225">**Hizmetler** klasörüne sağ tıklayın ve Ekle | ' yi seçin.  **Sınıf...** bağlam menüsünden.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-225">Right-click the **Services** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="fa1f3-226">![Hizmetler klasörüne yeni bir sınıf ekleniyor](build-restful-apis-with-aspnet-web-api/_static/image15.png "Hizmetler klasörüne yeni bir sınıf ekleniyor")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-226">![Adding a new class to the Services folder](build-restful-apis-with-aspnet-web-api/_static/image15.png "Adding a new class to the Services folder")</span></span>

    <span data-ttu-id="fa1f3-227">*Hizmetler klasörüne yeni bir sınıf ekleniyor*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-227">*Adding a new class to the Services folder*</span></span>
3. <span data-ttu-id="fa1f3-228">**Yeni öğe Ekle** iletişim kutusu göründüğünde, yeni sınıf **contactrepository** adını adlandırın ve **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-228">When the **Add New Item** dialog appears, name the new class **ContactRepository** and click **Add**.</span></span>

    <span data-ttu-id="fa1f3-229">![Kişi deposu hizmet katmanının kodunu içeren bir sınıf dosyası oluşturma](build-restful-apis-with-aspnet-web-api/_static/image16.png "Kişi deposu hizmet katmanının kodunu içeren bir sınıf dosyası oluşturma")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-229">![Creating a class file to contain the code for the Contact Repository service layer](build-restful-apis-with-aspnet-web-api/_static/image16.png "Creating a class file to contain the code for the Contact Repository service layer")</span></span>

    <span data-ttu-id="fa1f3-230">*Kişi deposu hizmet katmanının kodunu içeren bir sınıf dosyası oluşturma*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-230">*Creating a class file to contain the code for the Contact Repository service layer*</span></span>
4. <span data-ttu-id="fa1f3-231">Modeller ad alanını dahil etmek için **ContactRepository.cs** dosyasına bir using yönergesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-231">Add a using directive to the **ContactRepository.cs** file to include the models namespace.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample4.cs)]
5. <span data-ttu-id="fa1f3-232">GetAllContacts metodunu uygulamak için aşağıdaki vurgulanmış kodu **ContactRepository.cs** dosyasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-232">Add the following highlighted code to the **ContactRepository.cs** file to implement GetAllContacts method.</span></span>

    <span data-ttu-id="fa1f3-233">(Kod parçacığı- *Web API Laboratuvarı-Ex01-Ilgili kişi deposu*)</span><span class="sxs-lookup"><span data-stu-id="fa1f3-233">(Code Snippet - *Web API Lab - Ex01 - Contact Repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample5.cs)]
6. <span data-ttu-id="fa1f3-234">Zaten açık değilse, **ContactController.cs** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-234">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="fa1f3-235">Aşağıdaki using ifadesini dosyanın ad alanı bildirimi bölümüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-235">Add the following using statement to the namespace declaration section of the file.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample6.cs)]
8. <span data-ttu-id="fa1f3-236">Deponun örneğini temsil eden bir özel alan eklemek için **ContactController.cs** sınıfına aşağıdaki vurgulanmış kodu ekleyin. böylece, sınıf üyelerinin geri kalanı hizmet uygulamasını kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-236">Add the following highlighted code to the **ContactController.cs** class to add a private field to represent the instance of the repository, so that the rest of the class members can make use of the service implementation.</span></span>

    <span data-ttu-id="fa1f3-237">(Kod parçacığı- *Web API Laboratuvarı-Ex01-Ilgili kişi denetleyicisi*)</span><span class="sxs-lookup"><span data-stu-id="fa1f3-237">(Code Snippet - *Web API Lab - Ex01 - Contact Controller*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample7.cs)]
9. <span data-ttu-id="fa1f3-238">**Get** yöntemini, iletişim deposu hizmetini kullanacak şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-238">Change the **Get** method so that it makes use of the contact repository service.</span></span>

    <span data-ttu-id="fa1f3-239">(Kod parçacığı- *Web API Laboratuvarı-Ex01-depo aracılığıyla kişiler listesi döndürülüyor*)</span><span class="sxs-lookup"><span data-stu-id="fa1f3-239">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts via the repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample8.cs)]
10. <span data-ttu-id="fa1f3-240">**Contactcontroller**'ın **Get** yöntemi tanımına bir kesme noktası koyun.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-240">Put a breakpoint on the **ContactController**'s **Get** method definition.</span></span>

   <span data-ttu-id="fa1f3-241">![İletişim denetleyicisine kesme noktaları ekleme](build-restful-apis-with-aspnet-web-api/_static/image17.png "İletişim denetleyicisine kesme noktaları ekleme")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-241">![Adding breakpoints to the contact controller](build-restful-apis-with-aspnet-web-api/_static/image17.png "Adding breakpoints to the contact controller")</span></span>

   <span data-ttu-id="fa1f3-242">*İletişim denetleyicisine kesme noktaları ekleme*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-242">*Adding breakpoints to the contact controller*</span></span>
11. <span data-ttu-id="fa1f3-243">Uygulamayı çalıştırmak için **F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-243">Press **F5** to run the application.</span></span>
12. <span data-ttu-id="fa1f3-244">Tarayıcı açıldığında, geliştirici araçlarını açmak için **F12** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-244">When the browser opens, press **F12** to open the developer tools.</span></span>
13. <span data-ttu-id="fa1f3-245">**Ağ** sekmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-245">Click the **Network** tab.</span></span>
14. <span data-ttu-id="fa1f3-246">**Yakalamayı Başlat** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-246">Click the **Start Capturing** button.</span></span>
15. <span data-ttu-id="fa1f3-247">Adres çubuğuna URL 'YI **/api/Contact** sonekine ekleyin ve **ENTER** tuşuna basarak API denetleyicisini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-247">Append the URL in the address bar with the suffix **/api/contact** and press **Enter** to load the API controller.</span></span>
16. <span data-ttu-id="fa1f3-248">**Get** yöntemi yürütülmeye başladıktan sonra Visual Studio 2012 ' i kesmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-248">Visual Studio 2012 should break once **Get** method begins execution.</span></span>

   <span data-ttu-id="fa1f3-249">![Get yöntemi içinde kesme](build-restful-apis-with-aspnet-web-api/_static/image18.png "Get yöntemi içinde kesme")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-249">![Breaking within the Get method](build-restful-apis-with-aspnet-web-api/_static/image18.png "Breaking within the Get method")</span></span>

   <span data-ttu-id="fa1f3-250">*Get yöntemi içinde kesme*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-250">*Breaking within the Get method*</span></span>
17. <span data-ttu-id="fa1f3-251">Devam etmek için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-251">Press **F5** to continue.</span></span>
18. <span data-ttu-id="fa1f3-252">Zaten odağa sahip değilse Internet Explorer 'a geri dönün.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-252">Go back to Internet Explorer if it is not already in focus.</span></span> <span data-ttu-id="fa1f3-253">Ağ yakalama penceresini aklınızda edin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-253">Note the network capture window.</span></span>

    <span data-ttu-id="fa1f3-254">![Web API çağrısının sonuçlarını gösteren Internet Explorer 'da ağ görünümü](build-restful-apis-with-aspnet-web-api/_static/image19.png "Web API çağrısının sonuçlarını gösteren Internet Explorer 'da ağ görünümü")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-254">![Network view in Internet Explorer showing results of the Web API call](build-restful-apis-with-aspnet-web-api/_static/image19.png "Network view in Internet Explorer showing results of the Web API call")</span></span>

    <span data-ttu-id="fa1f3-255">*Web API çağrısının sonuçlarını gösteren Internet Explorer 'da ağ görünümü*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-255">*Network view in Internet Explorer showing results of the Web API call*</span></span>
19. <span data-ttu-id="fa1f3-256">**Ayrıntılı görünüme git** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-256">Click the **Go to detailed view** button.</span></span>
20. <span data-ttu-id="fa1f3-257">**Yanıt gövdesi** sekmesine tıklayın. API çağrısının JSON çıkışını ve hizmet katmanının aldığı iki kişiyi nasıl temsil ettiğini aklınızda edin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-257">Click the **Response body** tab. Note the JSON output of the API call, and how it represents the two contacts retrieved by the service layer.</span></span>

    <span data-ttu-id="fa1f3-258">![Web API 'sindeki JSON çıkışını Geliştirici Araçları penceresinde görüntüleme](build-restful-apis-with-aspnet-web-api/_static/image20.png "Web API 'sindeki JSON çıkışını Geliştirici Araçları penceresinde görüntüleme")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-258">![Viewing the JSON output from the Web API in the developer tools window](build-restful-apis-with-aspnet-web-api/_static/image20.png "Viewing the JSON output from the Web API in the developer tools window")</span></span>

    <span data-ttu-id="fa1f3-259">*Web API 'sindeki JSON çıkışını Geliştirici Araçları penceresinde görüntüleme*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-259">*Viewing the JSON output from the Web API in the developer tools window*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Create_a_ReadWrite_Web_API"></a>
### <a name="exercise-2-create-a-readwrite-web-api"></a><span data-ttu-id="fa1f3-260">Alıştırma 2: okuma/yazma Web API 'SI oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa1f3-260">Exercise 2: Create a Read/Write Web API</span></span>

<span data-ttu-id="fa1f3-261">Bu alıştırmada, veri düzenlemesi özellikleriyle etkinleştirmek üzere ilgili kişi Yöneticisi için POST ve PUT yöntemlerini uygulayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-261">In this exercise, you will implement POST and PUT methods for the contact manager to enable it with data-editing features.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Opening_the_Web_API_Project"></a>
#### <a name="task-1---opening-the-web-api-project"></a><span data-ttu-id="fa1f3-262">Görev 1-Web API projesi açılıyor</span><span class="sxs-lookup"><span data-stu-id="fa1f3-262">Task 1 - Opening the Web API Project</span></span>

<span data-ttu-id="fa1f3-263">Bu görevde, alıştırma 1 ' de oluşturulan Web API projesini geliştirmeye hazırlanacaktır, böylece kullanıcı girişi kabul edebilir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-263">In this task, you will prepare to enhance the Web API project created in Exercise 1 so that it can accept user input.</span></span>

1. <span data-ttu-id="fa1f3-264">**Web Için Visual Studio 2012 Express**'i çalıştırın. bunu yapmak için **başlat** 'a gidip **Web için vs Express** yazın ve **ENTER**tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-264">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="fa1f3-265">**Kaynak/Ex02-ReadWriteWebAPI/BEGIN/** Folder konumunda bulunan **Başlangıç** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-265">Open the **Begin** solution located at **Source/Ex02-ReadWriteWebAPI/Begin/** folder.</span></span> <span data-ttu-id="fa1f3-266">Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-266">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="fa1f3-267">Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-267">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="fa1f3-268">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-268">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="fa1f3-269">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-269">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="fa1f3-270">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-270">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="fa1f3-271">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-271">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="fa1f3-272">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-272">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="fa1f3-273">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-273">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="fa1f3-274">**Hizmetler/ContactRepository. cs** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-274">Open the **Services/ContactRepository.cs** file.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Adding_Data-Persistence_Features_to_the_Contact_Repository_Implementation"></a>
#### <a name="task-2---adding-data-persistence-features-to-the-contact-repository-implementation"></a><span data-ttu-id="fa1f3-275">Görev 2-Ilgili kişi deposu uygulamasına veri kalıcılığı özellikleri ekleme</span><span class="sxs-lookup"><span data-stu-id="fa1f3-275">Task 2 - Adding Data-Persistence Features to the Contact Repository Implementation</span></span>

<span data-ttu-id="fa1f3-276">Bu görevde, alıştırma 1 ' de oluşturulan Web API projesinin ContactRepository sınıfını, Kullanıcı girişini ve yeni Iletişim örneklerini kalıcı hale getirebilmesi için kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-276">In this task, you will augment the ContactRepository class of the Web API project created in Exercise 1 so that it can persist and accept user input and new Contact instances.</span></span>

1. <span data-ttu-id="fa1f3-277">Bu alıştırmada daha sonra Web sunucusu önbellek öğesi anahtar adının adını temsil etmek için **Contactrepository** sınıfına aşağıdaki sabiti ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-277">Add the following constant to the **ContactRepository** class to represent the name of the web server cache item key name later in this exercise.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample9.cs)]
2. <span data-ttu-id="fa1f3-278">**Contactrepository** öğesine aşağıdaki kodu içeren bir Oluşturucu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-278">Add a constructor to the **ContactRepository** containing the following code.</span></span>

    <span data-ttu-id="fa1f3-279">(Kod parçacığı- *Web API Laboratuvarı-Ex02-kişi deposu Oluşturucusu*)</span><span class="sxs-lookup"><span data-stu-id="fa1f3-279">(Code Snippet - *Web API Lab - Ex02 - Contact Repository Constructor*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample10.cs)]
3. <span data-ttu-id="fa1f3-280">**Getallcontacts** yönteminin kodunu aşağıda gösterildiği gibi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-280">Modify the code for the **GetAllContacts** method as demonstrated below.</span></span>

    <span data-ttu-id="fa1f3-281">(Kod parçacığı- *Web API Laboratuvarı-Ex02-tüm kişileri al*)</span><span class="sxs-lookup"><span data-stu-id="fa1f3-281">(Code Snippet - *Web API Lab - Ex02 - Get All Contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="fa1f3-282">Bu örnek, tanıtım amaçlıdır ve Web sunucusunun önbelleğini bir depolama ortamı olarak kullanacaktır. böylece, değerler oturum depolama mekanizması veya Istek depolama ömrü kullanmak yerine birden fazla istemciye aynı anda kullanılabilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-282">This example is for demonstration purposes and will use the web server's cache as a storage medium, so that the values will be available to multiple clients simultaneously, rather than use a Session storage mechanism or a Request storage lifetime.</span></span> <span data-ttu-id="fa1f3-283">Bunlardan biri, Web sunucusu önbelleğinin Entity Framework, XML depolama alanını veya başka bir çeşitliliğini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-283">One could use Entity Framework, XML storage, or any other variety in place of the web server cache.</span></span>
4. <span data-ttu-id="fa1f3-284">Kişi kaydetme işini yapmak için **Contactrepository** sınıfına **savecontact** adlı yeni bir yöntem uygulayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-284">Implement a new method named **SaveContact** to the **ContactRepository** class to do the work of saving a contact.</span></span> <span data-ttu-id="fa1f3-285">**Savecontact** yöntemi tek bir **iletişim** parametresi almalıdır ve başarılı veya başarısız olduğunu belirten bir Boole değeri döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-285">The **SaveContact** method should take a single **Contact** parameter and return a Boolean value indicating success or failure.</span></span>

    <span data-ttu-id="fa1f3-286">(Kod parçacığı- *Web API Laboratuvarı-Ex02-SaveContact metodunu uygulama*)</span><span class="sxs-lookup"><span data-stu-id="fa1f3-286">(Code Snippet - *Web API Lab - Ex02 - Implementing the SaveContact Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample12.cs)]

<a id="Exercise3"></a>

<a id="Exercise_3_Consume_the_Web_API_from_an_HTML_Client"></a>
### <a name="exercise-3-consume-the-web-api-from-an-html-client"></a><span data-ttu-id="fa1f3-287">Alıştırma 3: bir HTML Istemcisinden Web API 'sini kullanma</span><span class="sxs-lookup"><span data-stu-id="fa1f3-287">Exercise 3: Consume the Web API from an HTML Client</span></span>

<span data-ttu-id="fa1f3-288">Bu alıştırmada, Web API 'sini çağırmak için bir HTML İstemcisi oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-288">In this exercise, you will create an HTML client to call the Web API.</span></span> <span data-ttu-id="fa1f3-289">Bu istemci JavaScript kullanarak Web API 'SI ile veri değişimi kolaylaştırır ve sonuçları HTML biçimlendirmesi kullanarak bir Web tarayıcısında görüntüler.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-289">This client will facilitate data exchange with the Web API using JavaScript and will display the results in a web browser using HTML markup.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Displaying_Contacts"></a>
#### <a name="task-1---modifying-the-index-view-to-provide-a-gui-for-displaying-contacts"></a><span data-ttu-id="fa1f3-290">Görev 1-kişileri görüntülemek için bir GUI sağlamak üzere dizin görünümünü değiştirme</span><span class="sxs-lookup"><span data-stu-id="fa1f3-290">Task 1 - Modifying the Index View to Provide a GUI for Displaying Contacts</span></span>

<span data-ttu-id="fa1f3-291">Bu görevde, Web uygulamasının varsayılan dizin görünümünü, mevcut kişilerin listesini bir HTML tarayıcısında görüntüleme gereksinimini destekleyecek şekilde değiştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-291">In this task, you will modify the default Index view of the web application to support the requirement of displaying the list of existing contacts in an HTML browser.</span></span>

1. <span data-ttu-id="fa1f3-292">Zaten açık değilse, **Web Için Visual Studio 2012 Express 'i** açın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-292">Open **Visual Studio 2012 Express for Web** if it is not already open.</span></span>
2. <span data-ttu-id="fa1f3-293">**Kaynak/Ex03-ConsumingWebAPI/BEGIN/** Folder konumunda bulunan **Başlangıç** çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-293">Open the **Begin** solution located at **Source/Ex03-ConsumingWebAPI/Begin/** folder.</span></span> <span data-ttu-id="fa1f3-294">Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-294">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="fa1f3-295">Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-295">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="fa1f3-296">Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-296">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="fa1f3-297">**NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-297">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="fa1f3-298">Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-298">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="fa1f3-299">NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-299">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="fa1f3-300">NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-300">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="fa1f3-301">Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-301">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="fa1f3-302">**Görünümler/giriş** klasöründe bulunan **Index. cshtml** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-302">Open the **Index.cshtml** file located at **Views/Home** folder.</span></span>
4. <span data-ttu-id="fa1f3-303">Div öğesi içindeki HTML kodunu, aşağıdaki koda benzeymek üzere ID **gövdesi** ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-303">Replace the HTML code within the div element with id **body** so that it looks like the following code.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample13.html)]
5. <span data-ttu-id="fa1f3-304">Web API 'sine HTTP isteği gerçekleştirmek için, dosyanın alt kısmına aşağıdaki JavaScript kodunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-304">Add the following Javascript code at the bottom of the file to perform the HTTP request to the Web API.</span></span>

    [!code-cshtml[Main](build-restful-apis-with-aspnet-web-api/samples/sample14.cshtml)]
6. <span data-ttu-id="fa1f3-305">Zaten açık değilse, **ContactController.cs** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-305">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="fa1f3-306">**Contactcontroller** sınıfının **Get** yöntemine bir kesme noktası koyun.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-306">Place a breakpoint on the **Get** method of the **ContactController** class.</span></span>

    <span data-ttu-id="fa1f3-307">![API denetleyicisinin Get yöntemine bir kesme noktası yerleştirme](build-restful-apis-with-aspnet-web-api/_static/image21.png "API denetleyicisinin Get yöntemine bir kesme noktası yerleştirme")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-307">![Placing a breakpoint on the Get method of the API controller](build-restful-apis-with-aspnet-web-api/_static/image21.png "Placing a breakpoint on the Get method of the API controller")</span></span>

    <span data-ttu-id="fa1f3-308">*API denetleyicisinin Get yöntemine bir kesme noktası yerleştirme*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-308">*Placing a breakpoint on the Get method of the API controller*</span></span>
8. <span data-ttu-id="fa1f3-309">Projeyi çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-309">Press **F5** to run the project.</span></span> <span data-ttu-id="fa1f3-310">Tarayıcı, HTML belgesini yükler.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-310">The browser will load the HTML document.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fa1f3-311">Uygulamanızın kök URL 'sine göz attığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-311">Ensure that you are browsing to the root URL of your application.</span></span>
9. <span data-ttu-id="fa1f3-312">Sayfa yüklendiğinde ve JavaScript yürütüldükten sonra, kesme noktası isabet eder ve kod yürütmesi denetleyicide duraklatılır.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-312">Once the page loads and the JavaScript executes, the breakpoint will be hit and the code execution will pause in the controller.</span></span>

    <span data-ttu-id="fa1f3-313">![Web için VS Express kullanarak Web API çağrılarında hata ayıklama](build-restful-apis-with-aspnet-web-api/_static/image22.png "Web için VS Express kullanarak Web API çağrılarında hata ayıklama")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-313">![Debugging into the Web API calls using VS Express for Web](build-restful-apis-with-aspnet-web-api/_static/image22.png "Debugging into the Web API calls using VS Express for Web")</span></span>

    <span data-ttu-id="fa1f3-314">*Web için Visual Studio 2012 Express kullanarak Web API çağrısında hata ayıklama*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-314">*Debugging into the Web API call using Visual Studio 2012 Express for Web*</span></span>
10. <span data-ttu-id="fa1f3-315">Görünümü tarayıcıda yüklemeye devam etmek için kesme noktasını kaldırın ve **F5** 'e veya hata ayıklama araç çubuğunun **devam** düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-315">Remove the breakpoint and press **F5** or the debugging toolbar's **Continue** button to continue loading the view in the browser.</span></span> <span data-ttu-id="fa1f3-316">Web API çağrısı tamamlandıktan sonra, Web API çağrısından döndürülen kişileri tarayıcıda liste öğeleri olarak görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-316">Once the Web API call completes you should see the contacts returned from the Web API call displayed as list items in the browser.</span></span>

    <span data-ttu-id="fa1f3-317">![Tarayıcıda liste öğeleri olarak görünen API çağrısının sonuçları](build-restful-apis-with-aspnet-web-api/_static/image23.png "Tarayıcıda liste öğeleri olarak görünen API çağrısının sonuçları")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-317">![Results of the API call displayed in the browser as list items](build-restful-apis-with-aspnet-web-api/_static/image23.png "Results of the API call displayed in the browser as list items")</span></span>

    <span data-ttu-id="fa1f3-318">*Tarayıcıda liste öğeleri olarak görünen API çağrısının sonuçları*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-318">*Results of the API call displayed in the browser as list items*</span></span>
11. <span data-ttu-id="fa1f3-319">Hata ayıklamayı durdurun.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-319">Stop debugging.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Creating_Contacts"></a>
#### <a name="task-2---modifying-the-index-view-to-provide-a-gui-for-creating-contacts"></a><span data-ttu-id="fa1f3-320">Görev 2-kişi oluşturmak için bir GUI sağlamak üzere dizin görünümünü değiştirme</span><span class="sxs-lookup"><span data-stu-id="fa1f3-320">Task 2 - Modifying the Index View to Provide a GUI for Creating Contacts</span></span>

<span data-ttu-id="fa1f3-321">Bu görevde, MVC uygulamasının dizin görünümünü değiştirmeye devam edersiniz.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-321">In this task, you will continue to modify the Index view of the MVC application.</span></span> <span data-ttu-id="fa1f3-322">HTML sayfasına kullanıcı girişini yakalayan ve yeni bir kişi oluşturmak için Web API 'sine gönderecek bir form eklenir ve GUI 'den tarihi toplamak için yeni bir Web API denetleyicisi yöntemi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-322">A form will be added to the HTML page that will capture user input and send it to the Web API to create a new Contact, and a new Web API controller method will be created to collect date from the GUI.</span></span>

1. <span data-ttu-id="fa1f3-323">**ContactController.cs** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-323">Open the **ContactController.cs** file.</span></span>
2. <span data-ttu-id="fa1f3-324">Aşağıdaki kodda gösterildiği gibi, **Post** adlı denetleyici sınıfına yeni bir yöntem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-324">Add a new method to the controller class named **Post** as shown in the following code.</span></span>

    <span data-ttu-id="fa1f3-325">(Kod parçacığı- *Web API Laboratuvarı-Ex03-post yöntemi*)</span><span class="sxs-lookup"><span data-stu-id="fa1f3-325">(Code Snippet - *Web API Lab - Ex03 - Post Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample15.cs)]
3. <span data-ttu-id="fa1f3-326">Zaten açık değilse, **Index. cshtml** dosyasını Visual Studio 'da açın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-326">Open the **Index.cshtml** file in Visual Studio if it is not already open.</span></span>
4. <span data-ttu-id="fa1f3-327">Önceki göreve eklediğiniz sıralanmamış listeden hemen sonra, aşağıdaki HTML kodunu dosyaya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-327">Add the HTML code below to the file just after the unordered list you added in the previous task.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample16.html)]
5. <span data-ttu-id="fa1f3-328">Belgenin alt kısmındaki komut dosyası öğesi içinde, bir HTTP POST çağrısı kullanarak verileri Web API 'sine gönderecek olan düğme tıklama olaylarını işlemek için aşağıdaki vurgulanmış kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-328">Within the script element at the bottom of the document, add the following highlighted code to handle button-click events, which will post the data to the Web API using an HTTP POST call.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample17.html)]
6. <span data-ttu-id="fa1f3-329">**ContactController.cs**içinde **Post** yöntemine bir kesme noktası koyun.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-329">In **ContactController.cs**, place a breakpoint on the **Post** method.</span></span>
7. <span data-ttu-id="fa1f3-330">Uygulamayı tarayıcıda çalıştırmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-330">Press **F5** to run the application in the browser.</span></span>
8. <span data-ttu-id="fa1f3-331">Sayfa tarayıcıya yüklendikten sonra, yeni bir kişi adı ve kimliği yazın ve **Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-331">Once the page is loaded in the browser, type in a new contact name and Id and click the **Save** button.</span></span>

    <span data-ttu-id="fa1f3-332">![Tarayıcıda yüklenen istemci HTML belgesi](build-restful-apis-with-aspnet-web-api/_static/image24.png "Tarayıcıda yüklenen istemci HTML belgesi")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-332">![The client HTML document loaded in the browser](build-restful-apis-with-aspnet-web-api/_static/image24.png "The client HTML document loaded in the browser")</span></span>

    <span data-ttu-id="fa1f3-333">*Tarayıcıda yüklenen istemci HTML belgesi*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-333">*The client HTML document loaded in the browser*</span></span>
9. <span data-ttu-id="fa1f3-334">**Post** yönteminde hata ayıklayıcı penceresi kesildiğinde, **iletişim** parametresinin özelliklerine göz atın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-334">When the debugger window breaks in the **Post** method, take a look at the properties of the **contact** parameter.</span></span> <span data-ttu-id="fa1f3-335">Değerler, forma girdiğiniz verilerle eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-335">The values should match the data you entered in the form.</span></span>

    <span data-ttu-id="fa1f3-336">![İstemciden Web API 'sine gönderilen kişi nesnesi](build-restful-apis-with-aspnet-web-api/_static/image25.png "İstemciden Web API 'sine gönderilen kişi nesnesi")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-336">![The Contact object being sent to the Web API from the client](build-restful-apis-with-aspnet-web-api/_static/image25.png "The Contact object being sent to the Web API from the client")</span></span>

    <span data-ttu-id="fa1f3-337">*İstemciden Web API 'sine gönderilen kişi nesnesi*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-337">*The Contact object being sent to the Web API from the client*</span></span>
10. <span data-ttu-id="fa1f3-338">**Yanıt** değişkeni oluşturuluncaya kadar hata ayıklayıcıdaki yöntemi adım adım yapın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-338">Step through the method in the debugger until the **response** variable has been created.</span></span> <span data-ttu-id="fa1f3-339">Hata ayıklayıcıda **Yereller** penceresinde İnceleme yapıldığında tüm özelliklerin ayarlandığını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-339">Upon inspection in the **Locals** window in the debugger, you'll see that all the properties have been set.</span></span>

   <span data-ttu-id="fa1f3-340">![Hata ayıklayıcıda oluşturma sonrasında yanıt](build-restful-apis-with-aspnet-web-api/_static/image26.png "Hata ayıklayıcıda oluşturma sonrasında yanıt")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-340">![The response following creation in the debugger](build-restful-apis-with-aspnet-web-api/_static/image26.png "The response following creation in the debugger")</span></span>

   <span data-ttu-id="fa1f3-341">*Hata ayıklayıcıda oluşturma sonrasında yanıt*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-341">*The response following creation in the debugger*</span></span>
11. <span data-ttu-id="fa1f3-342">**F5** tuşuna basarsanız veya hata ayıklayıcıda **devam et** ' e tıkladığınızda istek tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-342">If you press **F5** or click **Continue** in the debugger the request will complete.</span></span> <span data-ttu-id="fa1f3-343">Tarayıcıya geri döndüğünüzde, yeni kişi **Contactrepository** uygulamasıyla depolanan kişiler listesine eklenir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-343">Once you switch back to the browser, the new contact has been added to the list of contacts stored by the **ContactRepository** implementation.</span></span>

   <span data-ttu-id="fa1f3-344">![Tarayıcı, yeni kişi örneğinin başarıyla oluşturulmasını yansıtır](build-restful-apis-with-aspnet-web-api/_static/image27.png "Tarayıcı, yeni kişi örneğinin başarıyla oluşturulmasını yansıtır")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-344">![The browser reflects successful creation of the new contact instance](build-restful-apis-with-aspnet-web-api/_static/image27.png "The browser reflects successful creation of the new contact instance")</span></span>

   <span data-ttu-id="fa1f3-345">*Tarayıcı, yeni kişi örneğinin başarıyla oluşturulmasını yansıtır*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-345">*The browser reflects successful creation of the new contact instance*</span></span>

> [!NOTE]
> <span data-ttu-id="fa1f3-346">Ayrıca, bu uygulamayı Azure 'a dağıtmak için [Ek C: Web dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlama](#AppendixC).</span><span class="sxs-lookup"><span data-stu-id="fa1f3-346">Additionally, you can deploy this application to Azure following [Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixC).</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="fa1f3-347">Özet</span><span class="sxs-lookup"><span data-stu-id="fa1f3-347">Summary</span></span>

<span data-ttu-id="fa1f3-348">Bu laboratuvar, sizi yeni ASP.NET Web API çerçevesine ve Framework kullanan yeniden Web API 'Lerinin uygulamasına sunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-348">This lab has introduced you to the new ASP.NET Web API framework and to the implementation of RESTful Web APIs using the framework.</span></span> <span data-ttu-id="fa1f3-349">Buradan, bu laboratuvara bir örnek olarak sağlanmaktansa, hizmetin herhangi bir sayıda mekanizmayı ve bir düzeyini kullanarak veri kalıcılığını kolaylaştıran yeni bir depo oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-349">From here, you could create a new repository that facilitates data persistence using any number of mechanisms and wire that service up rather than the simple one provided as an example in this lab.</span></span> <span data-ttu-id="fa1f3-350">Web API 'SI, HTTP ve JSON veya XML 'yi destekleyen herhangi bir dilde yazılmış HTML olmayan istemcilerden gelen iletişimi etkinleştirme gibi birçok ek özelliği destekler.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-350">Web API supports a number of additional features, such as enabling communication from non-HTML clients written in any language that supports HTTP and JSON or XML.</span></span> <span data-ttu-id="fa1f3-351">Bir Web API 'sini tipik bir Web uygulaması dışında barındırma özelliği de mümkündür ve bunun yanı sıra kendi serileştirme biçimlerinizi oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-351">The ability to host a Web API outside of a typical web application is also possible, as well as is the ability to create your own serialization formats.</span></span>

<span data-ttu-id="fa1f3-352">ASP.NET Web sitesi, [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api)ADRESINDEKI Web API çerçevesine adanmış bir alana sahiptir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-352">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api).</span></span> <span data-ttu-id="fa1f3-353">Bu site, Web API 'siyle ilgili en son bilgileri, örnekleri ve haberleri sağlamaya devam edecek, bu nedenle neredeyse tüm cihazlar veya geliştirme çerçevesiyle sunulan özel Web API 'Leri oluşturma sanatı hakkında daha ayrıntılı bilgi almak istiyorsanız, sık sık kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-353">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="fa1f3-354">Ek A: kod parçacıkları kullanma</span><span class="sxs-lookup"><span data-stu-id="fa1f3-354">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="fa1f3-355">Kod parçacıkları ile, ihtiyacınız olan tüm koda parmaklarınızın elinizin altında olmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-355">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="fa1f3-356">Laboratuvar belgesi, aşağıdaki şekilde gösterildiği gibi, bunları yalnızca ne zaman kullanacağınızı söyleyecektir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-356">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="fa1f3-357">![Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma](build-restful-apis-with-aspnet-web-api/_static/image28.png "Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-357">![Using Visual Studio code snippets to insert code into your project](build-restful-apis-with-aspnet-web-api/_static/image28.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="fa1f3-358">*Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-358">*Using Visual Studio code snippets to insert code into your project*</span></span>

<a id="CodeSnippetUsingKeyBoard"></a>

<a id="To_add_a_code_snippet_using_the_keyboard_C_only"></a>
### <a name="to-add-a-code-snippet-using-the-keyboard-c-only"></a><span data-ttu-id="fa1f3-359">Klavyeyi kullanarak bir kod parçacığı eklemek için (C# yalnızca)</span><span class="sxs-lookup"><span data-stu-id="fa1f3-359">To add a code snippet using the keyboard (C# only)</span></span>

1. <span data-ttu-id="fa1f3-360">Kodu eklemek istediğiniz yere imleci yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-360">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="fa1f3-361">Kod parçacığı adını yazmaya başlayın (boşluk veya tire olmadan).</span><span class="sxs-lookup"><span data-stu-id="fa1f3-361">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="fa1f3-362">IntelliSense, eşleşen kod parçacıklarının adlarını gösterdiği gibi izleyin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-362">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="fa1f3-363">Doğru kod parçacığını seçin (veya tüm kod parçacığının adı seçilene kadar yazmaya devam edin).</span><span class="sxs-lookup"><span data-stu-id="fa1f3-363">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="fa1f3-364">Kod parçacığını imleç konumuna eklemek için SEKME tuşuna iki kez basın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-364">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

    <span data-ttu-id="fa1f3-365">![Kod parçacığı adını yazmaya başlayın](build-restful-apis-with-aspnet-web-api/_static/image29.png "Kod parçacığı adını yazmaya başlayın")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-365">![Start typing the snippet name](build-restful-apis-with-aspnet-web-api/_static/image29.png "Start typing the snippet name")</span></span>

    <span data-ttu-id="fa1f3-366">*Kod parçacığı adını yazmaya başlayın*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-366">*Start typing the snippet name*</span></span>

    <span data-ttu-id="fa1f3-367">![Vurgulanan parçacığı seçmek için Tab tuşuna basın](build-restful-apis-with-aspnet-web-api/_static/image30.png "Vurgulanan parçacığı seçmek için Tab tuşuna basın")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-367">![Press Tab to select the highlighted snippet](build-restful-apis-with-aspnet-web-api/_static/image30.png "Press Tab to select the highlighted snippet")</span></span>

    <span data-ttu-id="fa1f3-368">*Vurgulanan parçacığı seçmek için Tab tuşuna basın*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-368">*Press Tab to select the highlighted snippet*</span></span>

    <span data-ttu-id="fa1f3-369">![Sekmeye tekrar basın ve kod parçacığı genişletilir](build-restful-apis-with-aspnet-web-api/_static/image31.png "Sekmeye tekrar basın ve kod parçacığı genişletilir")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-369">![Press Tab again and the snippet will expand](build-restful-apis-with-aspnet-web-api/_static/image31.png "Press Tab again and the snippet will expand")</span></span>

    <span data-ttu-id="fa1f3-370">*Sekmeye tekrar basın ve kod parçacığı genişletilir*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-370">*Press Tab again and the snippet will expand*</span></span>

<a id="CodeSnippetUsingMouse"></a>

<a id="To_add_a_code_snippet_using_the_mouse_C_Visual_Basic_and_XML"></a>
### <a name="to-add-a-code-snippet-using-the-mouse-c-visual-basic-and-xml"></a><span data-ttu-id="fa1f3-371">Fareyi kullanarak bir kod parçacığı eklemek için (C#, VISUAL BASIC ve XML)</span><span class="sxs-lookup"><span data-stu-id="fa1f3-371">To add a code snippet using the mouse (C#, Visual Basic and XML)</span></span>

1. <span data-ttu-id="fa1f3-372">Kod parçacığını eklemek istediğiniz yere sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-372">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="fa1f3-373">Kod **parçacığı Ekle** ' yi ve ardından **kod parçacıklarını**seçin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-373">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="fa1f3-374">Listeden tıklatarak ilgili kod parçacığını seçin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-374">Pick the relevant snippet from the list, by clicking on it.</span></span>

    <span data-ttu-id="fa1f3-375">![Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.](build-restful-apis-with-aspnet-web-api/_static/image32.png "Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-375">![Right-click where you want to insert the code snippet and select Insert Snippet](build-restful-apis-with-aspnet-web-api/_static/image32.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

    <span data-ttu-id="fa1f3-376">*Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-376">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

    <span data-ttu-id="fa1f3-377">![Listeden tıklatarak ilgili kod parçacığını seçin](build-restful-apis-with-aspnet-web-api/_static/image33.png "Listeden tıklatarak ilgili kod parçacığını seçin")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-377">![Pick the relevant snippet from the list, by clicking on it](build-restful-apis-with-aspnet-web-api/_static/image33.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

    <span data-ttu-id="fa1f3-378">*Listeden tıklatarak ilgili kod parçacığını seçin*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-378">*Pick the relevant snippet from the list, by clicking on it*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="fa1f3-379">Ek B: Web için Visual Studio Express 2012 yükleme</span><span class="sxs-lookup"><span data-stu-id="fa1f3-379">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="fa1f3-380">**[Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)** kullanarak **Web için Microsoft Visual Studio Express 2012** veya başka bir &quot;Express&quot; sürümü yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-380">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="fa1f3-381">Aşağıdaki yönergeler *Microsoft Web Platformu Yükleyicisi*kullanarak *Web Için Visual Studio Express 2012* ' i yüklemek için gereken adımlarda size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-381">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="fa1f3-382">[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)gidin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-382">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="fa1f3-383">Alternatif olarak, Web Platformu Yükleyicisi zaten yüklüyse, <em>Azure SDK&quot;Ile Web için Visual Studio Express 2012</em> &quot;ürün için arama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-383">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="fa1f3-384">**Şimdi yüklensin**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-384">Click on **Install Now**.</span></span> <span data-ttu-id="fa1f3-385">**Web platformu yükleyicinizi** yoksa, önce indirmek ve yüklemek üzere yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-385">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="fa1f3-386">**Web Platformu Yükleyicisi** açıkken, kurulum 'u başlatmak için **yükleme** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-386">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="fa1f3-387">![Visual Studio Express yüklensin](build-restful-apis-with-aspnet-web-api/_static/image34.png "Visual Studio Express yüklensin")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-387">![Install Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="fa1f3-388">*Visual Studio Express yüklensin*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-388">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="fa1f3-389">Tüm ürünlerin lisanslarını ve koşullarını okuyun ve devam etmek için **kabul ediyorum** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-389">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Lisans koşullarını kabul etme](build-restful-apis-with-aspnet-web-api/_static/image35.png)

    <span data-ttu-id="fa1f3-391">*Lisans koşullarını kabul etme*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-391">*Accepting the license terms*</span></span>
5. <span data-ttu-id="fa1f3-392">İndirme ve yükleme işlemi tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-392">Wait until the downloading and installation process completes.</span></span>

    ![Yükleme ilerleme durumu](build-restful-apis-with-aspnet-web-api/_static/image36.png)

    <span data-ttu-id="fa1f3-394">*Yükleme ilerleme durumu*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-394">*Installation progress*</span></span>
6. <span data-ttu-id="fa1f3-395">Yükleme tamamlandığında **son**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-395">When the installation completes, click **Finish**.</span></span>

    ![Yükleme tamamlandı](build-restful-apis-with-aspnet-web-api/_static/image37.png)

    <span data-ttu-id="fa1f3-397">*Yükleme tamamlandı*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-397">*Installation completed*</span></span>
7. <span data-ttu-id="fa1f3-398">Web Platformu Yükleyicisi 'ni kapatmak için **Çıkış** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-398">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="fa1f3-399">Web için Visual Studio Express açmak için **Başlangıç** ekranına gidin ve &quot;**vs Express**&quot;yazmaya başlayın ve ardından **Web için vs Express** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-399">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Web için VS Express kutucuğu](build-restful-apis-with-aspnet-web-api/_static/image38.png)

    <span data-ttu-id="fa1f3-401">*Web için VS Express kutucuğu*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-401">*VS Express for Web tile*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-c-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="fa1f3-402">Ek C: Web Dağıtımı kullanarak ASP.NET MVC 4 uygulaması yayımlama</span><span class="sxs-lookup"><span data-stu-id="fa1f3-402">Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="fa1f3-403">Bu ek, Azure portalından yeni bir Web sitesi oluşturmayı ve Azure tarafından sunulan Web Dağıtımı yayımlama özelliğinden yararlanarak Laboratuvarı izleyerek edindiğiniz uygulamayı yayımlamayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-403">This appendix will show you how to create a new web site from the Azure Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Azure.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a><span data-ttu-id="fa1f3-404">Görev 1-Azure portalından yeni bir Web sitesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa1f3-404">Task 1 - Creating a New Web Site from the Azure Portal</span></span>

1. <span data-ttu-id="fa1f3-405">[Azure yönetim portalı](https://manage.windowsazure.com/) gidin ve aboneliğinizle ilişkili Microsoft kimlik bilgilerini kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-405">Go to the [Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fa1f3-406">Azure ile 10 ASP.NET Web sitesini ücretsiz olarak barındırabilir ve ardından trafiğiniz büyüdükçe ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-406">With Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="fa1f3-407">[Buradan](https://aka.ms/aspnet-hol-azure)kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-407">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="fa1f3-408">![Windows Azure portal oturum açın](build-restful-apis-with-aspnet-web-api/_static/image39.png "Windows Azure portal oturum açın")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-408">![Log on to Windows Azure portal](build-restful-apis-with-aspnet-web-api/_static/image39.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="fa1f3-409">*Portalda oturum açın*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-409">*Log on to Portal*</span></span>
2. <span data-ttu-id="fa1f3-410">Komut çubuğunda **Yeni** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-410">Click **New** on the command bar.</span></span>

    <span data-ttu-id="fa1f3-411">![Yeni bir Web sitesi oluşturma](build-restful-apis-with-aspnet-web-api/_static/image40.png "Yeni bir Web sitesi oluşturma")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-411">![Creating a new Web Site](build-restful-apis-with-aspnet-web-api/_static/image40.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="fa1f3-412">*Yeni bir Web sitesi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-412">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="fa1f3-413">**İşlem** | **Web sitesi**' ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-413">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="fa1f3-414">Sonra **hızlı oluştur** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-414">Then select **Quick Create** option.</span></span> <span data-ttu-id="fa1f3-415">Yeni Web sitesi için kullanılabilir bir URL sağlayın ve **Web sitesi oluştur**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-415">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fa1f3-416">Azure, bulutta çalışan ve yönetebileceğiniz bir Web uygulaması için ana bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-416">Azure is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="fa1f3-417">Hızlı oluştur seçeneği, tamamlanmış bir Web uygulamasını Azure 'a Portal dışından dağıtmanıza izin verir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-417">The Quick Create option allows you to deploy a completed web application to the Azure from outside the portal.</span></span> <span data-ttu-id="fa1f3-418">Bir veritabanı ayarlamaya yönelik adımları içermez.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-418">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="fa1f3-419">![Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma](build-restful-apis-with-aspnet-web-api/_static/image41.png "Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-419">![Creating a new Web Site using Quick Create](build-restful-apis-with-aspnet-web-api/_static/image41.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="fa1f3-420">*Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-420">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="fa1f3-421">Yeni **Web sitesi** oluşturuluncaya kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-421">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="fa1f3-422">Web sitesi oluşturulduktan sonra **URL** sütununun altındaki bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-422">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="fa1f3-423">Yeni Web sitesinin çalışıp çalışmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-423">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="fa1f3-424">![Yeni Web sitesine göz atma](build-restful-apis-with-aspnet-web-api/_static/image42.png "Yeni Web sitesine göz atma")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-424">![Browsing to the new web site](build-restful-apis-with-aspnet-web-api/_static/image42.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="fa1f3-425">*Yeni Web sitesine göz atma*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-425">*Browsing to the new web site*</span></span>

    <span data-ttu-id="fa1f3-426">![Web sitesi çalışıyor](build-restful-apis-with-aspnet-web-api/_static/image43.png "Web sitesi çalışıyor")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-426">![Web site running](build-restful-apis-with-aspnet-web-api/_static/image43.png "Web site running")</span></span>

    <span data-ttu-id="fa1f3-427">*Web sitesi çalışıyor*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-427">*Web site running*</span></span>
6. <span data-ttu-id="fa1f3-428">Portala geri dönün ve yönetim sayfalarını göstermek için **ad** sütununun altındaki Web sitesinin adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-428">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="fa1f3-429">![Web sitesi yönetim sayfalarını açma](build-restful-apis-with-aspnet-web-api/_static/image44.png "Web sitesi yönetim sayfalarını açma")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-429">![Opening the web site management pages](build-restful-apis-with-aspnet-web-api/_static/image44.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="fa1f3-430">*Web sitesi yönetim sayfalarını açma*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-430">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="fa1f3-431">**Pano** sayfasında, **Hızlı bakış** bölümünde, **Yayımlama profilini indir** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-431">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fa1f3-432">*Yayımlama profili* , her etkin yayımlama yöntemi için bir Web uygulamasını Azure 'da yayımlamak için gereken tüm bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-432">The *publish profile* contains all of the information required to publish a web application to a Azure for each enabled publication method.</span></span> <span data-ttu-id="fa1f3-433">Yayımlama profili, bir yayımlama yönteminin etkinleştirildiği her bir uç noktasına bağlanmak ve kimlik doğrulaması yapmak için gereken URL'leri, kullanıcı kimlik bilgilerini ve veritabanı dizelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-433">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="fa1f3-434">**Microsoft WebMatrix 2**, **Web için Microsoft Visual Studio Express** ve **Microsoft Visual Studio 2012** , Web uygulamalarını Azure 'da yayımlamaya yönelik bu programların yapılandırılmasını otomatik hale getirmek için yayımlama profillerini okumayı destekler.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-434">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Azure.</span></span>

    <span data-ttu-id="fa1f3-435">![Web sitesi yayımlama profili indiriliyor](build-restful-apis-with-aspnet-web-api/_static/image45.png "Web sitesi yayımlama profili indiriliyor")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-435">![Downloading the web site publish profile](build-restful-apis-with-aspnet-web-api/_static/image45.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="fa1f3-436">*Web sitesi yayımlama profili indiriliyor*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-436">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="fa1f3-437">Yayımlama profili dosyasını bilinen bir konuma indirin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-437">Download the publish profile file to a known location.</span></span> <span data-ttu-id="fa1f3-438">Bu alıştırmada, Visual Studio 'dan Azure 'da bir Web uygulaması yayınlamak için bu dosyayı nasıl kullanacağınızı göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-438">Further in this exercise you will see how to use this file to publish a web application to Azure from Visual Studio.</span></span>

    <span data-ttu-id="fa1f3-439">![Yayımlama profili dosyası kaydediliyor](build-restful-apis-with-aspnet-web-api/_static/image46.png "Yayımlama profili kaydediliyor")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-439">![Saving the publish profile file](build-restful-apis-with-aspnet-web-api/_static/image46.png "Saving the publish profile")</span></span>

    <span data-ttu-id="fa1f3-440">*Yayımlama profili dosyası kaydediliyor*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-440">*Saving the publish profile file*</span></span>

<a id="ApxCTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="fa1f3-441">Görev 2-veritabanı sunucusunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fa1f3-441">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="fa1f3-442">Uygulamanız SQL Server veritabanlarını kullanıyorsa, bir SQL veritabanı sunucusu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-442">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="fa1f3-443">SQL Server kullanmayan basit bir uygulama dağıtmak istiyorsanız bu görevi atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-443">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="fa1f3-444">Uygulama veritabanını depolamak için bir SQL veritabanı sunucusuna ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-444">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="fa1f3-445">SQL veritabanı sunucularını aboneliğinizden Azure Yönetim Portalı ' nda **SQL veritabanları** | **sunucuları** | **Sunucu panosu**' nda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-445">You can view the SQL Database servers from your subscription in the Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="fa1f3-446">Oluşturulmuş bir sunucunuz yoksa, komut çubuğunda **Ekle** düğmesini kullanarak bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-446">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="fa1f3-447">**Sunucu adını ve URL 'yi, yönetici oturum açma adını ve parolayı**, bunları bir sonraki görevlerde kullanacaksınız gibi bir yere göz atın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-447">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="fa1f3-448">Daha sonraki bir aşamada oluşturulacak şekilde veritabanını henüz oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-448">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="fa1f3-449">![SQL veritabanı sunucu panosu](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL veritabanı sunucu panosu")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-449">![SQL Database Server Dashboard](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="fa1f3-450">*SQL veritabanı sunucu panosu*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-450">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="fa1f3-451">Sonraki görevde, Visual Studio 'dan veritabanı bağlantısını test edersiniz. bu nedenle, yerel IP adresinizi sunucunun **Izin VERILEN IP adresleri**listesine eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-451">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="fa1f3-452">Bunu yapmak için, **Yapılandır**' a tıklayın, **geçerli ISTEMCI IP** adresinden IP ADRESINI seçin ve **Başlangıç IP adresi** ve **bitiş IP adresi** metin kutularına yapıştırın ve ![Add-Client-ip-Address-ok-Button](build-restful-apis-with-aspnet-web-api/_static/image48.png) düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-452">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](build-restful-apis-with-aspnet-web-api/_static/image48.png) button.</span></span>

    ![Istemci IP adresi ekleniyor](build-restful-apis-with-aspnet-web-api/_static/image49.png)

    <span data-ttu-id="fa1f3-454">*Istemci IP adresi ekleniyor*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-454">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="fa1f3-455">**ISTEMCI IP adresi** ızın verilen IP adresleri listesine eklendikten sonra, değişiklikleri onaylamak için **Kaydet** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-455">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![Değişiklikleri Onayla](build-restful-apis-with-aspnet-web-api/_static/image50.png)

    <span data-ttu-id="fa1f3-457">*Değişiklikleri Onayla*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-457">*Confirm Changes*</span></span>

<a id="ApxCTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="fa1f3-458">Görev 3-Web Dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlama</span><span class="sxs-lookup"><span data-stu-id="fa1f3-458">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="fa1f3-459">ASP.NET MVC 4 çözümüne geri dönün.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-459">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="fa1f3-460">**Çözüm Gezgini**Web sitesi projesine sağ tıklayın ve **Yayımla**' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-460">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="fa1f3-461">![Uygulama yayımlanıyor](build-restful-apis-with-aspnet-web-api/_static/image51.png "Uygulamayı Yayımlama")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-461">![Publishing the Application](build-restful-apis-with-aspnet-web-api/_static/image51.png "Publishing the Application")</span></span>

    <span data-ttu-id="fa1f3-462">*Web sitesi yayımlanıyor*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-462">*Publishing the web site*</span></span>
2. <span data-ttu-id="fa1f3-463">İlk görevde kaydettiğiniz yayımlama profilini içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-463">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="fa1f3-464">![Yayımlama profilini içeri aktarma](build-restful-apis-with-aspnet-web-api/_static/image52.png "Yayımlama profilini içeri aktarma")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-464">![Importing the publish profile](build-restful-apis-with-aspnet-web-api/_static/image52.png "Importing the publish profile")</span></span>

    <span data-ttu-id="fa1f3-465">*Yayımlama profili içeri aktarılıyor*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-465">*Importing publish profile*</span></span>
3. <span data-ttu-id="fa1f3-466">**Bağlantıyı doğrula**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-466">Click **Validate Connection**.</span></span> <span data-ttu-id="fa1f3-467">Doğrulama tamamlandıktan sonra **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-467">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fa1f3-468">Bağlantıyı Doğrula düğmesinin yanında yeşil bir onay işareti gördüğünüzde doğrulama tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-468">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="fa1f3-469">![Bağlantı doğrulanıyor](build-restful-apis-with-aspnet-web-api/_static/image53.png "Bağlantı doğrulanıyor")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-469">![Validating connection](build-restful-apis-with-aspnet-web-api/_static/image53.png "Validating connection")</span></span>

    <span data-ttu-id="fa1f3-470">*Bağlantı doğrulanıyor*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-470">*Validating connection*</span></span>
4. <span data-ttu-id="fa1f3-471">**Ayarlar** sayfasında, **veritabanları** bölümü altında, veritabanı bağlantınızın metin kutusunun yanındaki düğmeye (yani **DefaultConnection**) tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-471">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="fa1f3-472">![Web dağıtımı yapılandırması](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web dağıtımı yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-472">![Web deploy configuration](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web deploy configuration")</span></span>

    <span data-ttu-id="fa1f3-473">*Web dağıtımı yapılandırması*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-473">*Web deploy configuration*</span></span>
5. <span data-ttu-id="fa1f3-474">Veritabanı bağlantısını aşağıdaki şekilde yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="fa1f3-474">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="fa1f3-475">**Sunucu adı** ' nda, *TCP:* önekini kullanarak SQL veritabanı sunucunuzun URL 'nizi yazın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-475">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="fa1f3-476">**Kullanıcı adı** ' nda Sunucu Yöneticisi oturum açma adınızı yazın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-476">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="fa1f3-477">**Parola** alanına Sunucu Yöneticisi oturum açma parolanızı yazın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-477">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="fa1f3-478">Yeni bir veritabanı adı yazın, örneğin: *MVC4SampleDB*.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-478">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="fa1f3-479">![Hedef bağlantı dizesi yapılandırılıyor](build-restful-apis-with-aspnet-web-api/_static/image55.png "Hedef bağlantı dizesi yapılandırılıyor")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-479">![Configuring destination connection string](build-restful-apis-with-aspnet-web-api/_static/image55.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="fa1f3-480">*Hedef bağlantı dizesi yapılandırılıyor*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-480">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="fa1f3-481">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-481">Then click **OK**.</span></span> <span data-ttu-id="fa1f3-482">Veritabanını oluşturmak isteyip istemediğiniz sorulduğunda **Evet**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-482">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="fa1f3-483">![Veritabanı oluşturma](build-restful-apis-with-aspnet-web-api/_static/image56.png "Veritabanı dizesi oluşturuluyor")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-483">![Creating the database](build-restful-apis-with-aspnet-web-api/_static/image56.png "Creating the database string")</span></span>

    <span data-ttu-id="fa1f3-484">*Veritabanı oluşturma*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-484">*Creating the database*</span></span>
7. <span data-ttu-id="fa1f3-485">Windows Azure 'da SQL veritabanı 'na bağlanmak için kullanacağınız bağlantı dizesi varsayılan bağlantı metin kutusu içinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-485">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="fa1f3-486">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-486">Then click **Next**.</span></span>

    <span data-ttu-id="fa1f3-487">![SQL veritabanı 'na işaret eden bağlantı dizesi](build-restful-apis-with-aspnet-web-api/_static/image57.png "SQL veritabanı 'na işaret eden bağlantı dizesi")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-487">![Connection string pointing to SQL Database](build-restful-apis-with-aspnet-web-api/_static/image57.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="fa1f3-488">*SQL veritabanı 'na işaret eden bağlantı dizesi*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-488">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="fa1f3-489">**Önizleme** sayfasında **Yayımla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-489">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="fa1f3-490">![Web uygulaması yayımlanıyor](build-restful-apis-with-aspnet-web-api/_static/image58.png "Web uygulaması yayımlanıyor")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-490">![Publishing the web application](build-restful-apis-with-aspnet-web-api/_static/image58.png "Publishing the web application")</span></span>

    <span data-ttu-id="fa1f3-491">*Web uygulaması yayımlanıyor*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-491">*Publishing the web application*</span></span>
9. <span data-ttu-id="fa1f3-492">Yayımlama işlemi tamamlandıktan sonra varsayılan tarayıcınız yayınlanan Web sitesini açar.</span><span class="sxs-lookup"><span data-stu-id="fa1f3-492">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="fa1f3-493">![Windows Azure 'da yayımlanan uygulama](build-restful-apis-with-aspnet-web-api/_static/image59.png "Windows Azure 'da yayımlanan uygulama")</span><span class="sxs-lookup"><span data-stu-id="fa1f3-493">![Application published to Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image59.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="fa1f3-494">*Azure 'da yayımlanan uygulama*</span><span class="sxs-lookup"><span data-stu-id="fa1f3-494">*Application published to Azure*</span></span>
