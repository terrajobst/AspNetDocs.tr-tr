---
uid: web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
title: Windows Phone 8 uygulamasından Web API 'SI çağırma (C#)-ASP.NET 4. x
author: rmcmurray
description: 'Kod ile öğretici: ASP.NET 4. x içinde bir Windows Phone 8 uygulamasına kitapların kataloğunu sağlayan bir ASP.NET Web API uygulaması oluşturun.'
ms.author: riande
ms.date: 10/09/2013
ms.custom: seoapril2019
ms.assetid: b9775f41-352a-4f82-baa6-23e95b342e20
msc.legacyurl: /web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
msc.type: authoredcontent
ms.openlocfilehash: c5da14a6856f551343b6fb14f0aedc659e792f6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614739"
---
# <a name="calling-web-api-from-a-windows-phone-8-application-c"></a><span data-ttu-id="3bbb0-103">Windows Phone 8 Uygulamasından Web API'sine Çağrı Yapma (C#)</span><span class="sxs-lookup"><span data-stu-id="3bbb0-103">Calling Web API from a Windows Phone 8 Application (C#)</span></span>

<span data-ttu-id="3bbb0-104">[Robert McMurray](https://github.com/rmcmurray) tarafından</span><span class="sxs-lookup"><span data-stu-id="3bbb0-104">by [Robert McMurray](https://github.com/rmcmurray)</span></span>

<span data-ttu-id="3bbb0-105">Bu öğreticide, Windows Phone 8 uygulamasına kitap kataloğu sağlayan bir ASP.NET Web API uygulamasından oluşan tam uçtan uca bir senaryo oluşturmayı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-105">In this tutorial, you will learn how to create a complete end-to-end scenario consisting of an ASP.NET Web API application that provides a catalog of books to a Windows Phone 8 application.</span></span>

### <a name="overview"></a><span data-ttu-id="3bbb0-106">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="3bbb0-106">Overview</span></span>

<span data-ttu-id="3bbb0-107">ASP.NET Web API gibi yeniden ESUIT Hizmetleri, sunucu tarafı ve istemci tarafı uygulamalar için mimari soyutlayarak geliştiriciler için HTTP tabanlı uygulamaların oluşturulmasını basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-107">RESTful services like ASP.NET Web API simplify the creation of HTTP-based applications for developers by abstracting the architecture for server-side and client-side applications.</span></span> <span data-ttu-id="3bbb0-108">Web API geliştiricilerin, iletişim için özel bir soket tabanlı protokol oluşturmak yerine yalnızca uygulama için önkoşul HTTP yöntemlerini yayımlaması gerekir (örneğin: GET, POST, PUT, DELETE) ve istemci uygulama geliştiricilerinin yalnızca kullanması gerekir uygulamaları için gerekli olan HTTP yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-108">Instead of creating a proprietary socket-based protocol for communication, Web API developers simply need to publish the requisite HTTP methods for their application, (for example: GET, POST, PUT, DELETE), and client application developers only need to consume the HTTP methods that are necessary for their application.</span></span>

<span data-ttu-id="3bbb0-109">Bu uçtan uca öğreticide, Web API 'sini kullanarak aşağıdaki projeleri oluşturma hakkında bilgi edineceksiniz:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-109">In this end-to-end tutorial, you will learn how to use Web API to create the following projects:</span></span>

- <span data-ttu-id="3bbb0-110">[Bu öğreticinin ilk bölümünde](#STEP1), bir kitap kataloğunu yönetmek Için tüm oluşturma, okuma, güncelleştirme ve SILME (CRUD) işlemlerini destekleyen bir ASP.NET Web API uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-110">In the [first part of this tutorial](#STEP1), you will create an ASP.NET Web API application that supports all of the Create, Read, Update, and Delete (CRUD) operations to manage a book catalog.</span></span> <span data-ttu-id="3bbb0-111">Bu uygulama, MSDN 'den [örnek xml dosyasını (Books. xml)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-111">This application will use the [Sample XML File (books.xml)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) from MSDN.</span></span>
- <span data-ttu-id="3bbb0-112">[Bu öğreticinin ikinci bölümünde](#STEP2), Web API uygulamanızdan verileri alan etkileşimli bir Windows Phone 8 uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-112">In the [second part of this tutorial](#STEP2), you will create an interactive Windows Phone 8 application that retrieves the data from your Web API application.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="3bbb0-113">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="3bbb0-113">Prerequisites</span></span>

- <span data-ttu-id="3bbb0-114">Windows Phone 8 SDK yüklü Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3bbb0-114">Visual Studio 2013 with the Windows Phone 8 SDK installed</span></span>
- <span data-ttu-id="3bbb0-115">Hyper-V yüklü 64 bitlik bir sistemde Windows 8 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="3bbb0-115">Windows 8 or later on a 64-bit system with Hyper-V installed</span></span>
- <span data-ttu-id="3bbb0-116">Ek gereksinimlerin listesi için [WINDOWS Phone SDK 8,0](https://www.microsoft.com/download/details.aspx?id=35471) Indirme sayfasındaki *sistem gereksinimleri* bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-116">For a list of additional requirements, see the *System Requirements* section on the [Windows Phone SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471) download page.</span></span>

> [!NOTE]
> <span data-ttu-id="3bbb0-117">Yerel sisteminizdeki Web API 'SI ve Windows Phone 8 projeleri arasındaki bağlantıyı test etecekseniz, test ortamınızı ayarlamak için *[Windows Phone 8 öykünücüsünü yerel bir bilgisayarda Web API uygulamalarına bağlama](https://go.microsoft.com/fwlink/?LinkId=324014)* makalesindeki yönergeleri izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-117">If you are going to test the connectivity between Web API and Windows Phone 8 projects on your local system, you will need to follow the instructions in the *[Connecting the Windows Phone 8 Emulator to Web API Applications on a Local Computer](https://go.microsoft.com/fwlink/?LinkId=324014)* article to set up your testing environment.</span></span>

<a id="STEP1"></a>
### <a name="step-1-creating-the-web-api-bookstore-project"></a><span data-ttu-id="3bbb0-118">1\. Adım: Web API kitaplığı projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="3bbb0-118">Step 1: Creating the Web API Bookstore Project</span></span>

<span data-ttu-id="3bbb0-119">Bu uçtan uca öğreticinin ilk adımı, tüm CRUD işlemlerini destekleyen bir Web API projesi oluşturmaktır; Bu öğreticinin [Adım 2](#STEP2) ' de bu çözüme Windows Phone uygulama projesini ekleneceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-119">The first step of this end-to-end tutorial is to create a Web API project that supports all of the CRUD operations; note that you will add the Windows Phone application project to this solution in [Step 2](#STEP2) of this tutorial.</span></span>

1. <span data-ttu-id="3bbb0-120">**Visual Studio 2013**açın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-120">Open **Visual Studio 2013**.</span></span>
2. <span data-ttu-id="3bbb0-121">**Dosya**ve ardından **Yeni**' ye ve ardından **Proje**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-121">Click **File**, then **New**, and then **Project**.</span></span>
3. <span data-ttu-id="3bbb0-122">**Yeni proje** iletişim kutusu görüntülendiğinde, **yüklü**' i, ardından **Şablonlar** **' C#ı ve** ardından **Web**' i genişletin.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-122">When the **New Project** dialog box is displayed, expand **Installed**, then **Templates**, then **Visual C#**, and then **Web**.</span></span>

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image2.png)](calling-web-api-from-a-windows-phone-8-application/_static/image1.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                <span data-ttu-id="3bbb0-123">Genişletmek için görüntü öğesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="3bbb0-123">Click image to expand</span></span>                                                                |

4. <span data-ttu-id="3bbb0-124">**ASP.NET Web uygulamasını**vurgulayın, proje adı için **kitaplığı** girin ve ardından **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-124">Highlight **ASP.NET Web Application**, enter **BookStore** for the project name, and then click **OK**.</span></span>
5. <span data-ttu-id="3bbb0-125">**Yeni ASP.NET projesi** iletişim kutusu görüntülendiğinde, **Web API** şablonunu seçin ve ardından **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-125">When the **New ASP.NET Project** dialog box is displayed, select the **Web API** template, and then click **OK**.</span></span>

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image4.png)](calling-web-api-from-a-windows-phone-8-application/_static/image3.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                <span data-ttu-id="3bbb0-126">Genişletmek için görüntü öğesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="3bbb0-126">Click image to expand</span></span>                                                                |

6. <span data-ttu-id="3bbb0-127">Web API projesi açıldığında, projeden örnek denetleyiciyi kaldırın:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-127">When the Web API project opens, remove the sample controller from the project:</span></span>

    1. <span data-ttu-id="3bbb0-128">Çözüm Gezgini ' nde **denetleyiciler** klasörünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-128">Expand the **Controllers** folder in the solution explorer.</span></span>
    2. <span data-ttu-id="3bbb0-129">**ValuesController.cs** dosyasına sağ tıklayın ve ardından **Sil**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-129">Right-click the **ValuesController.cs** file, and then click **Delete**.</span></span>
    3. <span data-ttu-id="3bbb0-130">Silmeyi onaylamanız istendiğinde **Tamam** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-130">Click **OK** when prompted to confirm the deletion.</span></span>
7. <span data-ttu-id="3bbb0-131">Web API projesine bir XML veri dosyası ekleyin; Bu dosya, kitaplığı kataloğunun içeriğini içerir:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-131">Add an XML data file to the Web API project; this file contains the contents of the bookstore catalog:</span></span>

   1. <span data-ttu-id="3bbb0-132">Çözüm Gezgini ' nde **uygulama\_veri** klasörüne sağ tıklayın, ardından **Ekle**' ye ve ardından **Yeni öğe**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-132">Right-click the **App\_Data** folder in the solution explorer, then click **Add**, and then click **New Item**.</span></span>
   2. <span data-ttu-id="3bbb0-133">**Yeni öğe Ekle** iletişim kutusu görüntülendiğinde, **XML dosya** şablonunu vurgulayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-133">When the **Add New Item** dialog box is displayed, highlight the **XML File** template.</span></span>
   3. <span data-ttu-id="3bbb0-134">Dosyayı **Books. xml**olarak adlandırın ve **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-134">Name the file **Books.xml**, and then click **Add**.</span></span>
   4. <span data-ttu-id="3bbb0-135">**Books. xml** dosyası AÇıLDıĞıNDA, MSDN 'deki örnek **kitaplar. xml** dosyasındaki dosyadaki kodu XML ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-135">When the **Books.xml** file is opened, replace the code in the file with the XML from the sample **books.xml** file on MSDN:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample1.xml)]
   5. <span data-ttu-id="3bbb0-136">XML dosyasını kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-136">Save and close the XML file.</span></span>

8. <span data-ttu-id="3bbb0-137">Kitaplığı modelini Web API projesine ekleyin; Bu model, kitaplığı uygulaması için oluşturma, okuma, güncelleştirme ve silme (CRUD) mantığını içerir:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-137">Add the bookstore model to the Web API project; this model contains the Create, Read, Update, and Delete (CRUD) logic for the bookstore application:</span></span>

   1. <span data-ttu-id="3bbb0-138">Çözüm Gezgini ' nde **modeller** klasörüne sağ tıklayın, ardından **Ekle**' ye ve ardından **sınıf**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-138">Right-click the **Models** folder in the solution explorer, then click **Add**, and then click **Class**.</span></span>
   2. <span data-ttu-id="3bbb0-139">**Yeni öğe Ekle** iletişim kutusu görüntülendiğinde, sınıf dosyasını **BookDetails.cs**olarak adlandırın ve **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-139">When the **Add New Item** dialog box is displayed, name the class file **BookDetails.cs**, and then click **Add**.</span></span>
   3. <span data-ttu-id="3bbb0-140">**BookDetails.cs** dosyası açıldığında, dosyadaki kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-140">When the **BookDetails.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample2.cs)]
   4. <span data-ttu-id="3bbb0-141">**BookDetails.cs** dosyasını kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-141">Save and close the **BookDetails.cs** file.</span></span>

9. <span data-ttu-id="3bbb0-142">Kitaplığı denetleyicisi 'ni Web API projesine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-142">Add the bookstore controller to the Web API project:</span></span>

   1. <span data-ttu-id="3bbb0-143">Çözüm Gezgini ' nde **denetleyiciler** klasörüne sağ tıklayın, ardından **Ekle**' ye tıklayın ve ardından **Denetleyici**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-143">Right-click the **Controllers** folder in the solution explorer, then click **Add**, and then click **Controller**.</span></span>
   2. <span data-ttu-id="3bbb0-144">**Yapı Iskelesi Ekle** iletişim kutusu görüntülendiğinde, **Web API 2 denetleyici-boş**' ı vurgulayın ve **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-144">When the **Add Scaffold** dialog box is displayed, highlight **Web API 2 Controller - Empty**, and then click **Add**.</span></span>
   3. <span data-ttu-id="3bbb0-145">**Denetleyici Ekle** iletişim kutusu görüntülendiğinde, denetleyici **bookscontroller**adını adlandırın ve ardından **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-145">When the **Add Controller** dialog box is displayed, name the controller **BooksController**, and then click **Add**.</span></span>
   4. <span data-ttu-id="3bbb0-146">**BooksController.cs** dosyası açıldığında, dosyadaki kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-146">When the **BooksController.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample3.cs)]
   5. <span data-ttu-id="3bbb0-147">**BooksController.cs** dosyasını kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-147">Save and close the **BooksController.cs** file.</span></span>

10. <span data-ttu-id="3bbb0-148">Hataları denetlemek için Web API uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-148">Build the Web API application to check for errors.</span></span>

<a id="STEP2"></a>
### <a name="step-2-adding-the-windows-phone-8-bookstore-catalog-project"></a><span data-ttu-id="3bbb0-149">2\. Adım: Windows Phone 8 kitaplığı Katalog projesini ekleme</span><span class="sxs-lookup"><span data-stu-id="3bbb0-149">Step 2: Adding the Windows Phone 8 Bookstore Catalog Project</span></span>

<span data-ttu-id="3bbb0-150">Bu uçtan uca senaryonun sonraki adımı, Windows Phone 8 için katalog uygulaması oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-150">The next step of this end-to-end scenario is to create the catalog application for Windows Phone 8.</span></span> <span data-ttu-id="3bbb0-151">Bu uygulama, varsayılan kullanıcı arabirimi için *Windows Phone veri bağlama uygulama* şablonunu kullanır ve veri kaynağı olarak Bu öğreticinin [1. ADıMıNDA](#STEP1) oluşturduğunuz Web API uygulamasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-151">This application will use the *Windows Phone Databound App* template for the default user interface, and it will use the Web API application that you created in [Step 1](#STEP1) of this tutorial as the data source.</span></span>

1. <span data-ttu-id="3bbb0-152">Çözüm Gezgini ' nde bulunan **kitaplığı** çözümüne sağ tıklayın, ardından **Ekle**' ye ve ardından **Yeni proje**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-152">Right-click the **BookStore** solution in the in the solution explorer, then click **Add**, and then **New Project**.</span></span>
2. <span data-ttu-id="3bbb0-153">**Yeni proje** iletişim kutusu görüntülendiğinde, **yüklü**' i ve ardından **görsel C#** ' i genişletin ve ardından **Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-153">When the **New Project** dialog box is displayed, expand **Installed**, then **Visual C#**, and then **Windows Phone**.</span></span>
3. <span data-ttu-id="3bbb0-154">**Windows Phone veriye bağlı uygulamayı**vurgulayın, ad Için **bookcatalog** girin ve ardından **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-154">Highlight **Windows Phone Databound App**, enter **BookCatalog** for the name, and then click **OK**.</span></span>
4. <span data-ttu-id="3bbb0-155">Json.NET NuGet paketini **Bookcatalog** projesine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-155">Add the Json.NET NuGet package to the **BookCatalog** project:</span></span>

    1. <span data-ttu-id="3bbb0-156">Çözüm Gezgini ' nde **Bookcatalog** projesi için **Başvurular** ' a sağ tıklayın ve ardından **NuGet Paketlerini Yönet**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-156">Right-click **References** for the **BookCatalog** project in the solution explorer, and then click **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="3bbb0-157">**NuGet Paketlerini Yönet** iletişim kutusu görüntülendiğinde, **çevrimiçi** bölümünü genişletin ve **NuGet.org**vurgulayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-157">When the **Manage NuGet Packages** dialog box is displayed, expand the **Online** section, and highlight **nuget.org**.</span></span>
    3. <span data-ttu-id="3bbb0-158">Arama alanına **JSON.net** girin ve arama simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-158">Enter **Json.NET** in the search field and click the search icon.</span></span>
    4. <span data-ttu-id="3bbb0-159">Arama sonuçlarında **JSON.net** vurgulayın ve ardından **Install**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-159">Highlight **Json.NET** in the search results, and then click **Install**.</span></span>
    5. <span data-ttu-id="3bbb0-160">Yükleme tamamlandığında **Kapat**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-160">When the installation has completed, click **Close**.</span></span>
5. <span data-ttu-id="3bbb0-161">Bookdetails modelini **bookcatalog** projesine ekleyin; Bu, kitaplığı sınıfının genel bir modelini içerir:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-161">Add the **BookDetails** model to the **BookCatalog** project; this contains a generic model of the bookstore class:</span></span>

   1. <span data-ttu-id="3bbb0-162">Çözüm Gezgini ' nde **Bookcatalog** projesine sağ tıklayın, ardından **Ekle**' ye ve ardından **Yeni klasör**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-162">Right-click the **BookCatalog** project in the solution explorer, then click **Add**, and then click **New Folder**.</span></span>
   2. <span data-ttu-id="3bbb0-163">Yeni klasör **modellerini**adlandırın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-163">Name the new folder **Models**.</span></span>
   3. <span data-ttu-id="3bbb0-164">Çözüm Gezgini ' nde **modeller** klasörüne sağ tıklayın, ardından **Ekle**' ye ve ardından **sınıf**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-164">Right-click the **Models** folder in the solution explorer, then click **Add**, and then click **Class**.</span></span>
   4. <span data-ttu-id="3bbb0-165">**Yeni öğe Ekle** iletişim kutusu görüntülendiğinde, sınıf dosyasını **BookDetails.cs**olarak adlandırın ve **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-165">When the **Add New Item** dialog box is displayed, name the class file **BookDetails.cs**, and then click **Add**.</span></span>
   5. <span data-ttu-id="3bbb0-166">**BookDetails.cs** dosyası açıldığında, dosyadaki kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-166">When the **BookDetails.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample4.cs)]
   6. <span data-ttu-id="3bbb0-167">**BookDetails.cs** dosyasını kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-167">Save and close the **BookDetails.cs** file.</span></span>

6. <span data-ttu-id="3bbb0-168">**MainViewModel.cs** sınıfını, KITAPLıĞı Web API uygulamasıyla iletişim kuracak işlevselliği içerecek şekilde güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-168">Update the **MainViewModel.cs** class to include the functionality to communicate with the BookStore Web API application:</span></span>

   1. <span data-ttu-id="3bbb0-169">Çözüm Gezgini ' nde **Viewmodeller** klasörünü genişletin ve ardından **MainViewModel.cs** dosyasına çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-169">Expand the **ViewModels** folder in the solution explorer, and then double-click the **MainViewModel.cs** file.</span></span>
   2. <span data-ttu-id="3bbb0-170">**MainViewModel.cs** dosyası açıldığında, dosyadaki kodu aşağıdaki kodla değiştirin; `apiUrl` sabitinin değerini, Web API 'nizin gerçek URL 'siyle güncelleştirmeniz gerektiğini unutmayın:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-170">When the **MainViewModel.cs** file is opened, replace the code in the file with the following; note that you will need to update the value of the `apiUrl` constant with the actual URL of your Web API:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample5.cs)]
   3. <span data-ttu-id="3bbb0-171">**MainViewModel.cs** dosyasını kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-171">Save and close the **MainViewModel.cs** file.</span></span>

7. <span data-ttu-id="3bbb0-172">**MainPage. xaml** dosyasını, uygulama adını özelleştirmek için güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-172">Update the **MainPage.xaml** file to customize the application name:</span></span>

   1. <span data-ttu-id="3bbb0-173">Çözüm Gezgini 'nde **MainPage. xaml** dosyasına çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-173">Double-click the **MainPage.xaml** file in the solution explorer.</span></span>
   2. <span data-ttu-id="3bbb0-174">**MainPage. xaml** dosyası açıldığında aşağıdaki kod satırlarını bulun:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-174">When the **MainPage.xaml** file is opened, locate the following lines of code:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample6.xml)]
   3. <span data-ttu-id="3bbb0-175">Bu satırları aşağıdakiler ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-175">Replace those lines with the following:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample7.xml)]
   4. <span data-ttu-id="3bbb0-176">**MainPage. xaml** dosyasını kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-176">Save and close the **MainPage.xaml** file.</span></span>

8. <span data-ttu-id="3bbb0-177">Görüntülenecek öğeleri özelleştirmek için **Ayrıntılar Page. xaml** dosyasını güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-177">Update the **DetailsPage.xaml** file to customize the displayed items:</span></span>

   1. <span data-ttu-id="3bbb0-178">Çözüm Gezgini 'nde, **Ayrıntılar Page. xaml** dosyasına çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-178">Double-click the **DetailsPage.xaml** file in the solution explorer.</span></span>
   2. <span data-ttu-id="3bbb0-179">**Ayrıntılar Page. xaml** dosyası açıldığında aşağıdaki kod satırlarını bulun:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-179">When the **DetailsPage.xaml** file is opened, locate the following lines of code:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample8.xml)]
   3. <span data-ttu-id="3bbb0-180">Bu satırları aşağıdakiler ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-180">Replace those lines with the following:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample9.xml)]
   4. <span data-ttu-id="3bbb0-181">**Ayrıntılar Page. xaml** dosyasını kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-181">Save and close the **DetailsPage.xaml** file.</span></span>

9. <span data-ttu-id="3bbb0-182">Hataları denetlemek için Windows Phone uygulamayı derleyin.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-182">Build the Windows Phone application to check for errors.</span></span>

### <a name="step-3-testing-the-end-to-end-solution"></a><span data-ttu-id="3bbb0-183">3\. Adım: uçtan uca çözümü test etme</span><span class="sxs-lookup"><span data-stu-id="3bbb0-183">Step 3: Testing the End-to-End Solution</span></span>

<span data-ttu-id="3bbb0-184">Bu öğreticinin *Önkoşullar* bölümünde belirtildiği gibi, yerel sisteminizdeki Web API 'si ve Windows Phone 8 projeleri arasındaki bağlantıyı sınarken, test ortamınızı ayarlamak için *[Windows Phone 8 öykünücüsünü yerel BIR bilgisayardaki Web API uygulamalarına bağlama](https://go.microsoft.com/fwlink/?LinkId=324014)* makalesindeki yönergeleri izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-184">As mentioned in the *Prerequisites* section of this tutorial, when you are testing the connectivity between Web API and Windows Phone 8 projects on your local system, you will need to follow the instructions in the *[Connecting the Windows Phone 8 Emulator to Web API Applications on a Local Computer](https://go.microsoft.com/fwlink/?LinkId=324014)* article to set up your testing environment.</span></span>

<span data-ttu-id="3bbb0-185">Test ortamı yapılandırıldıktan sonra, Windows Phone uygulamasını başlangıç projesi olarak ayarlamanız gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="3bbb0-185">Once you have the testing environment configured, you will need to set the Windows Phone application as the startup project.</span></span> <span data-ttu-id="3bbb0-186">Bunu yapmak için, Çözüm Gezgini ' nde **Bookcatalog** uygulamasını vurgulayın ve ardından **Başlangıç projesi olarak ayarla**' ya tıklayın:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-186">To do so, highlight the **BookCatalog** application in the solution explorer, and then click **Set as StartUp Project**:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image6.png)](calling-web-api-from-a-windows-phone-8-application/_static/image5.png) |
| --- |
| <span data-ttu-id="3bbb0-187">Genişletmek için görüntü öğesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="3bbb0-187">Click image to expand</span></span> |

<span data-ttu-id="3bbb0-188">F5 tuşuna bastığınızda, Visual Studio her iki Windows Phone öykünücüyü başlatır ve &quot;bu, uygulama verileri Web API 'sinden alınırken&quot; ileti bekleyin:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-188">When you press F5, Visual Studio will start both the Windows Phone Emulator, which will display a &quot;Please Wait&quot; message while the application data is retrieved from your Web API:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image8.png)](calling-web-api-from-a-windows-phone-8-application/_static/image7.png) |
| --- |
| <span data-ttu-id="3bbb0-189">Genişletmek için görüntü öğesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="3bbb0-189">Click image to expand</span></span> |

<span data-ttu-id="3bbb0-190">Her şey başarılı olursa kataloğun görüntülendiğini görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-190">If everything is successful, you should see the catalog displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image10.png)](calling-web-api-from-a-windows-phone-8-application/_static/image9.png) |
| --- |
| <span data-ttu-id="3bbb0-191">Genişletmek için görüntü öğesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="3bbb0-191">Click image to expand</span></span> |

<span data-ttu-id="3bbb0-192">Herhangi bir kitap başlığına dokunduğunuzda, uygulama kitap açıklamasını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-192">If you tap on any book title, the application will display the book description:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image12.png)](calling-web-api-from-a-windows-phone-8-application/_static/image11.png) |
| --- |
| <span data-ttu-id="3bbb0-193">Genişletmek için görüntü öğesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="3bbb0-193">Click image to expand</span></span> |

<span data-ttu-id="3bbb0-194">Uygulama Web API 'niz ile iletişim kuramıyorsa, bir hata iletisi görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-194">If the application cannot communicate with your Web API, an error message will be displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image14.png)](calling-web-api-from-a-windows-phone-8-application/_static/image13.png) |
| --- |
| <span data-ttu-id="3bbb0-195">Genişletmek için görüntü öğesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="3bbb0-195">Click image to expand</span></span> |

<span data-ttu-id="3bbb0-196">Hata iletisine dokunduğunuzda, hatayla ilgili ek ayrıntılar görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="3bbb0-196">If you tap on the error message, any additional details about the error will be displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image16.png)](calling-web-api-from-a-windows-phone-8-application/_static/image15.png) |
|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                 <span data-ttu-id="3bbb0-197">Genişletmek için görüntü öğesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="3bbb0-197">Click image to expand</span></span>                                                                 |
