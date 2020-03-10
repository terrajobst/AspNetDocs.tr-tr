---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
title: '4\. Bölüm: modeller ve veri erişimi | Microsoft Docs'
author: jongalloway
description: Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 4\. bölüm, modelleri ve veri erişimini içerir.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: ab55ca81-ab9b-44a0-8700-dc6da2599335
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
msc.type: authoredcontent
ms.openlocfilehash: 402be340f1ea3344675e7b859cea8c5130cfc8ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559677"
---
# <a name="part-4-models-and-data-access"></a><span data-ttu-id="377f5-104">4\. Bölüm: Modeller ve Veri Erişimi</span><span class="sxs-lookup"><span data-stu-id="377f5-104">Part 4: Models and Data Access</span></span>

<span data-ttu-id="377f5-105">[Jon Galloway](https://github.com/jongalloway) tarafından</span><span class="sxs-lookup"><span data-stu-id="377f5-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="377f5-106">MVC müzik deposu, Web geliştirme için ASP.NET MVC ve Visual Studio 'nun nasıl kullanılacağını anlatan bir öğretici uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="377f5-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="377f5-107">MVC müzik deposu, çevrimiçi olarak müzik albümlerini satan ve temel site yönetimi, Kullanıcı oturum açma ve alışveriş sepeti işlevlerini uygulayan basit bir örnek depolama uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="377f5-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="377f5-108">Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır.</span><span class="sxs-lookup"><span data-stu-id="377f5-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="377f5-109">4\. bölüm, modelleri ve veri erişimini içerir.</span><span class="sxs-lookup"><span data-stu-id="377f5-109">Part 4 covers Models and Data Access.</span></span>

<span data-ttu-id="377f5-110">Şimdiye kadar, Denetleyicilerimizden "kukla verileri" görüntüleme şablonlarımızla geçirdik.</span><span class="sxs-lookup"><span data-stu-id="377f5-110">So far, we've just been passing "dummy data" from our Controllers to our View templates.</span></span> <span data-ttu-id="377f5-111">Şimdi gerçek bir veritabanını yedeklemeye hazırız.</span><span class="sxs-lookup"><span data-stu-id="377f5-111">Now we're ready to hook up a real database.</span></span> <span data-ttu-id="377f5-112">Bu öğreticide, veritabanı altyapımız olarak SQL Server Compact sürümünün (genellikle SQL CE olarak adlandırılır) nasıl kullanılacağını ele alacağız.</span><span class="sxs-lookup"><span data-stu-id="377f5-112">In this tutorial we'll be covering how to use SQL Server Compact Edition (often called SQL CE) as our database engine.</span></span> <span data-ttu-id="377f5-113">SQL CE, herhangi bir yükleme veya yapılandırma gerektirmeyen ücretsiz, katıştırılmış, dosya tabanlı bir veritabanıdır. Bu, yerel geliştirme için gerçekten uygun hale getirir.</span><span class="sxs-lookup"><span data-stu-id="377f5-113">SQL CE is a free, embedded, file based database that doesn't require any installation or configuration, which makes it really convenient for local development.</span></span>

## <a name="database-access-with-entity-framework-code-first"></a><span data-ttu-id="377f5-114">Entity Framework kodla veritabanı erişimi-Ilk</span><span class="sxs-lookup"><span data-stu-id="377f5-114">Database access with Entity Framework Code-First</span></span>

<span data-ttu-id="377f5-115">Veritabanını sorgulamak ve güncelleştirmek için ASP.NET MVC 3 projelerine dahil edilen Entity Framework (EF) desteğini kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="377f5-115">We'll use the Entity Framework (EF) support that is included in ASP.NET MVC 3 projects to query and update the database.</span></span> <span data-ttu-id="377f5-116">EF, geliştiricilerin bir veritabanında depolanan verileri nesne yönelimli bir şekilde sorgulamasını ve güncelleştirmesini sağlayan esnek bir nesne ilişkisel eşleme (ORM) veri API 'sidir.</span><span class="sxs-lookup"><span data-stu-id="377f5-116">EF is a flexible object relational mapping (ORM) data API that enables developers to query and update data stored in a database in an object-oriented way.</span></span>

<span data-ttu-id="377f5-117">Entity Framework sürüm 4, önce kod adlı bir geliştirme paradigmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="377f5-117">Entity Framework version 4 supports a development paradigm called code-first.</span></span> <span data-ttu-id="377f5-118">Kod-önce basit sınıflar ("düz eski" CLR nesnelerinden POCO olarak da bilinir) yazarak model nesnesi oluşturmanıza olanak sağlar ve hatta sınıfınızdan anında veritabanı oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="377f5-118">Code-first allows you to create model object by writing simple classes (also known as POCO from "plain-old" CLR objects), and can even create the database on the fly from your classes.</span></span>

### <a name="changes-to-our-model-classes"></a><span data-ttu-id="377f5-119">Model sınıflarımızda yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="377f5-119">Changes to our Model Classes</span></span>

<span data-ttu-id="377f5-120">Bu öğreticide Entity Framework veritabanı oluşturma özelliğinden yararlanacağız.</span><span class="sxs-lookup"><span data-stu-id="377f5-120">We will be leveraging the database creation feature in Entity Framework in this tutorial.</span></span> <span data-ttu-id="377f5-121">Bunu yapmadan önce, model sınıflarımızda daha sonra kullanacağımız bazı şeyleri eklemek için birkaç küçük değişiklik yapalim.</span><span class="sxs-lookup"><span data-stu-id="377f5-121">Before we do that, though, let's make a few minor changes to our model classes to add in some things we'll be using later on.</span></span>

#### <a name="adding-the-artist-model-classes"></a><span data-ttu-id="377f5-122">Sanatçı model sınıfları ekleme</span><span class="sxs-lookup"><span data-stu-id="377f5-122">Adding the Artist Model Classes</span></span>

<span data-ttu-id="377f5-123">Albümlerimiz sanatçılarla ilişkilendirilecektir, bu nedenle bir sanatçının tanımlanabilmesi için basit bir model sınıfı ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="377f5-123">Our Albums will be associated with Artists, so we'll add a simple model class to describe an Artist.</span></span> <span data-ttu-id="377f5-124">Aşağıda gösterilen kodu kullanarak Artist.cs adlı modeller klasörüne yeni bir sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="377f5-124">Add a new class to the Models folder named Artist.cs using the code shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample1.cs)]

#### <a name="updating-our-model-classes"></a><span data-ttu-id="377f5-125">Model Sınıflarımızı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="377f5-125">Updating our Model Classes</span></span>

<span data-ttu-id="377f5-126">Albüm sınıfını aşağıda gösterildiği gibi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="377f5-126">Update the Album class as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample2.cs)]

<span data-ttu-id="377f5-127">Sonra, tarz sınıfına aşağıdaki güncelleştirmeleri yapın.</span><span class="sxs-lookup"><span data-stu-id="377f5-127">Next, make the following updates to the Genre class.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample3.cs)]

### <a name="adding-the-app_data-folder"></a><span data-ttu-id="377f5-128">Uygulama\_veri klasörü ekleniyor</span><span class="sxs-lookup"><span data-stu-id="377f5-128">Adding the App\_Data folder</span></span>

<span data-ttu-id="377f5-129">SQL Server Express veritabanı dosyalarını tutmak için projenize bir uygulama\_veri dizini ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="377f5-129">We'll add an App\_Data directory to our project to hold our SQL Server Express database files.</span></span> <span data-ttu-id="377f5-130">Uygulama\_verileri, veritabanı erişimi için zaten doğru güvenlik erişimi izinlerine sahip olan ASP.NET içinde özel bir dizindir.</span><span class="sxs-lookup"><span data-stu-id="377f5-130">App\_Data is a special directory in ASP.NET which already has the correct security access permissions for database access.</span></span> <span data-ttu-id="377f5-131">Proje menüsünde ASP.NET klasörü Ekle ' yi ve ardından App\_verileri ' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="377f5-131">From the Project menu, select Add ASP.NET Folder, then App\_Data.</span></span>

![](mvc-music-store-part-4/_static/image1.png)

### <a name="creating-a-connection-string-in-the-webconfig-file"></a><span data-ttu-id="377f5-132">Web. config dosyasında bir bağlantı dizesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="377f5-132">Creating a Connection String in the web.config file</span></span>

<span data-ttu-id="377f5-133">Entity Framework Web sitesinin yapılandırma dosyasına birkaç satır ekleyecek ve bu sayede veritabanınıza nasıl bağlanacağını biliyor.</span><span class="sxs-lookup"><span data-stu-id="377f5-133">We will add a few lines to the website's configuration file so that Entity Framework knows how to connect to our database.</span></span> <span data-ttu-id="377f5-134">Projenin kökünde bulunan Web. config dosyasına çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="377f5-134">Double-click on the Web.config file located in the root of the project.</span></span>

![](mvc-music-store-part-4/_static/image2.png)

<span data-ttu-id="377f5-135">Bu dosyanın en altına kaydırın ve aşağıda gösterildiği gibi, doğrudan son satırın üzerine bir &lt;connectionStrings&gt; bölümü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="377f5-135">Scroll to the bottom of this file and add a &lt;connectionStrings&gt; section directly above the last line, as shown below.</span></span>

[!code-xml[Main](mvc-music-store-part-4/samples/sample4.xml)]

### <a name="adding-a-context-class"></a><span data-ttu-id="377f5-136">Bağlam sınıfı ekleme</span><span class="sxs-lookup"><span data-stu-id="377f5-136">Adding a Context Class</span></span>

<span data-ttu-id="377f5-137">Modeller klasörüne sağ tıklayın ve MusicStoreEntities.cs adlı yeni bir sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="377f5-137">Right-click the Models folder and add a new class named MusicStoreEntities.cs.</span></span>

![](mvc-music-store-part-4/_static/image3.png)

<span data-ttu-id="377f5-138">Bu sınıf Entity Framework veritabanı bağlamını temsil eder ve bizim için oluşturma, okuma, güncelleştirme ve silme işlemlerini işleymeyecektir.</span><span class="sxs-lookup"><span data-stu-id="377f5-138">This class will represent the Entity Framework database context, and will handle our create, read, update, and delete operations for us.</span></span> <span data-ttu-id="377f5-139">Bu sınıfın kodu aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="377f5-139">The code for this class is shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample5.cs)]

<span data-ttu-id="377f5-140">Bu, başka bir yapılandırma, özel arabirimler vb. değildir. DbContext temel sınıfını genişleterek, MusicStoreEntities sınıfımız bizim için veritabanı işlemlerimizi işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="377f5-140">That's it - there's no other configuration, special interfaces, etc. By extending the DbContext base class, our MusicStoreEntities class is able to handle our database operations for us.</span></span> <span data-ttu-id="377f5-141">Şimdi bağlandığımızdan, veritabanımızda bazı ek bilgilerden yararlanmak için model sınıflarımıza birkaç özellik ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="377f5-141">Now that we've got that hooked up, let's add a few more properties to our model classes to take advantage of some of the additional information in our database.</span></span>

### <a name="adding-our-store-catalog-data"></a><span data-ttu-id="377f5-142">Mağaza kataloğu verilerimizi ekleme</span><span class="sxs-lookup"><span data-stu-id="377f5-142">Adding our store catalog data</span></span>

<span data-ttu-id="377f5-143">Yeni oluşturulan bir veritabanına "tohum" verileri ekleyen Entity Framework özelliğinden yararlanacağız.</span><span class="sxs-lookup"><span data-stu-id="377f5-143">We will take advantage of a feature in Entity Framework which adds "seed" data to a newly created database.</span></span> <span data-ttu-id="377f5-144">Bu, mağaza kataloğumuzu bir tarzın, sanatçıların ve albümlerin bir listesi ile önceden dolduracaktır.</span><span class="sxs-lookup"><span data-stu-id="377f5-144">This will pre-populate our store catalog with a list of Genres, Artists, and Albums.</span></span> <span data-ttu-id="377f5-145">Bu öğreticide daha önce kullanılan site tasarım dosyalarımı içeren MvcMusicStore-Assets. zip indirmesi-kod adlı bir klasörde bulunan bu çekirdek verilerle bir sınıf dosyasına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="377f5-145">The MvcMusicStore-Assets.zip download - which included our site design files used earlier in this tutorial - has a class file with this seed data, located in a folder named Code.</span></span>

<span data-ttu-id="377f5-146">Kod/modeller klasörü içinde, SampleData.cs dosyasını bulun ve aşağıda gösterildiği gibi, projemizdeki modeller klasörüne bırakın.</span><span class="sxs-lookup"><span data-stu-id="377f5-146">Within the Code / Models folder, locate the SampleData.cs file and drop it into the Models folder in our project, as shown below.</span></span>

![](mvc-music-store-part-4/_static/image4.png)

<span data-ttu-id="377f5-147">Şimdi bu SampleData sınıfı hakkında Entity Framework söylemek için bir kod satırı eklememiz gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="377f5-147">Now we need to add one line of code to tell Entity Framework about that SampleData class.</span></span> <span data-ttu-id="377f5-148">Projenin kökündeki Global. asax dosyasına çift tıklayarak açın ve aşağıdaki satırı uygulama\_başlangıç yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="377f5-148">Double-click on the Global.asax file in the root of the project to open it and add the following line to the top the Application\_Start method.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample6.cs)]

<span data-ttu-id="377f5-149">Bu noktada, projemiz için Entity Framework yapılandırmak üzere gereken işi tamamladık.</span><span class="sxs-lookup"><span data-stu-id="377f5-149">At this point, we've completed the work necessary to configure Entity Framework for our project.</span></span>

## <a name="querying-the-database"></a><span data-ttu-id="377f5-150">Veritabanını Sorgulama</span><span class="sxs-lookup"><span data-stu-id="377f5-150">Querying the Database</span></span>

<span data-ttu-id="377f5-151">Şimdi StoreController 'ı, bunun yerine "kukla verileri" kullanmak yerine, tüm bilgilerini sorgulamak için veritabanımıza çağrı yapalım.</span><span class="sxs-lookup"><span data-stu-id="377f5-151">Now let's update our StoreController so that instead of using "dummy data" it instead calls into our database to query all of its information.</span></span> <span data-ttu-id="377f5-152">StoreDB adlı bir MusicStoreEntities sınıfının örneğini tutmak için **Storecontroller** üzerinde bir alan bildirerek başlayacağız:</span><span class="sxs-lookup"><span data-stu-id="377f5-152">We'll start by declaring a field on the **StoreController** to hold an instance of the MusicStoreEntities class, named storeDB:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample7.cs)]

### <a name="updating-the-store-index-to-query-the-database"></a><span data-ttu-id="377f5-153">Veritabanını sorgulamak için mağaza dizinini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="377f5-153">Updating the Store Index to query the database</span></span>

<span data-ttu-id="377f5-154">MusicStoreEntities sınıfı Entity Framework tarafından korunur ve veritabanımızda her tablo için bir koleksiyon özelliği sunar.</span><span class="sxs-lookup"><span data-stu-id="377f5-154">The MusicStoreEntities class is maintained by the Entity Framework and exposes a collection property for each table in our database.</span></span> <span data-ttu-id="377f5-155">Veritabanımızda tüm tarzları almak için StoreController 'ın Dizin eylemini güncelleştirelim.</span><span class="sxs-lookup"><span data-stu-id="377f5-155">Let's update our StoreController's Index action to retrieve all Genres in our database.</span></span> <span data-ttu-id="377f5-156">Daha önce bunu, dize verilerini sabit kodlayarak yaptık.</span><span class="sxs-lookup"><span data-stu-id="377f5-156">Previously we did this by hard-coding string data.</span></span> <span data-ttu-id="377f5-157">Artık bunun yerine yalnızca Entity Framework Context Generes koleksiyonunu kullanabiliriz:</span><span class="sxs-lookup"><span data-stu-id="377f5-157">Now we can instead just use the Entity Framework context Generes collection:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample8.cs)]

<span data-ttu-id="377f5-158">Daha önce döndürtiğimiz Storeındexviewmodel 'i hala döndürtiğimiz için görünüm şablonumuza hiçbir değişiklik oluşmaması gerekmez; Şimdi veritabanımızdan canlı verileri döndürdük.</span><span class="sxs-lookup"><span data-stu-id="377f5-158">No changes need to happen to our View template since we're still returning the same StoreIndexViewModel we returned before - we're just returning live data from our database now.</span></span>

<span data-ttu-id="377f5-159">Projeyi yeniden çalıştırıp "/Store" URL 'sini ziyaret ettiğimiz zaman, veritabanımızda bulunan tüm tarzlar için bir liste görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="377f5-159">When we run the project again and visit the "/Store" URL, we'll now see a list of all Genres in our database:</span></span>

![](mvc-music-store-part-4/_static/image1.jpg)

### <a name="updating-store-browse-and-details-to-use-live-data"></a><span data-ttu-id="377f5-160">Canlı verileri kullanmak için mağaza gözden geçirme ve ayrıntılarını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="377f5-160">Updating Store Browse and Details to use live data</span></span>

<span data-ttu-id="377f5-161">/Store/gözatmaya? tarzı = *[bazı-tarz]* eylem yöntemiyle, bir tarz adına göre arıyoruz.</span><span class="sxs-lookup"><span data-stu-id="377f5-161">With the /Store/Browse?genre=*[some-genre]* action method, we're searching for a Genre by name.</span></span> <span data-ttu-id="377f5-162">Yalnızca bir sonuç beklediğimiz için, her zaman aynı tarz adı için iki girişi olmaması gerektiğinden, kullanabiliriz. LINQ to içinde uygun tarz nesnesini sorgulamak için tek () uzantısı, buna benzer (henüz bu türü kullanmayın):</span><span class="sxs-lookup"><span data-stu-id="377f5-162">We only expect one result, since we shouldn't ever have two entries for the same Genre name, and so we can use the .Single() extension in LINQ to query for the appropriate Genre object like this (don't type this yet):</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample9.cs)]

<span data-ttu-id="377f5-163">Tek bir yöntem, bir lambda ifadesini parametre olarak alır, bu, adı tanımladığımız değerle eşleşen tek bir tarz nesne istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="377f5-163">The Single method takes a Lambda expression as a parameter, which specifies that we want a single Genre object such that its name matches the value we've defined.</span></span> <span data-ttu-id="377f5-164">Yukarıdaki örnekte, disco ile eşleşen bir ad değeriyle tek bir tarz nesnesi yüklüyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="377f5-164">In the case above, we are loading a single Genre object with a Name value matching Disco.</span></span>

<span data-ttu-id="377f5-165">Bir Entity Framework özelliğinden yararlanarak, daha önce, yüklemek istediğimiz diğer ilgili varlıkları ve tarz nesnesi alındığında belirtmemizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="377f5-165">We'll take advantage of an Entity Framework feature that allows us to indicate other related entities we want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="377f5-166">Bu özelliğe sorgu sonucu şekillendirme adı verilir ve ihtiyaç duyduğumuz tüm bilgileri almak için veritabanına erişmek için gereken sürelerin sayısını azaltmamızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="377f5-166">This feature is called Query Result Shaping, and enables us to reduce the number of times we need to access the database to retrieve all of the information we need.</span></span> <span data-ttu-id="377f5-167">Aldığımız tarz için albümleri önceden getirmek istiyoruz. bu nedenle, ilgili Albümler 'in de isteyeceğini göstermek için sorgumuzu, tarzımızı ("Albümler") içerecek şekilde güncelleştireceğiz.</span><span class="sxs-lookup"><span data-stu-id="377f5-167">We want to pre-fetch the Albums for Genre we retrieve, so we'll update our query to include from Genres.Include("Albums") to indicate that we want related albums as well.</span></span> <span data-ttu-id="377f5-168">Bu, hem tarz hem de albüm verilerimizi tek bir veritabanı isteğinde alacak olduğundan daha etkilidir.</span><span class="sxs-lookup"><span data-stu-id="377f5-168">This is more efficient, since it will retrieve both our Genre and Album data in a single database request.</span></span>

<span data-ttu-id="377f5-169">Açıklamalar sayesinde, güncelleştirilmiş tarama denetleyicisi eylemizin şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="377f5-169">With the explanations out of the way, here's how our updated Browse controller action looks:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample10.cs)]

<span data-ttu-id="377f5-170">Artık her bir tarz için kullanılabilir olan albümleri görüntülemek için mağaza Tarama görünümünü güncelleştirebiliriz.</span><span class="sxs-lookup"><span data-stu-id="377f5-170">We can now update the Store Browse View to display the albums which are available in each Genre.</span></span> <span data-ttu-id="377f5-171">Görünüm şablonunu açın (/Views/Store/Browse.cshtml içinde bulunur) ve aşağıda gösterildiği gibi bir albüm listesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="377f5-171">Open the view template (found in /Views/Store/Browse.cshtml) and add a bulleted list of Albums as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample11.cshtml)]

<span data-ttu-id="377f5-172">Uygulamamızı çalıştırmak ve/Store/gözatmaya? tarzı = Caat 'e gözatmak, sonuçlarımızın Şu anda veritabanından çekilmekte olduğunu gösteriyor ve seçili tarzımızda tüm albümleri görüntülüyor.</span><span class="sxs-lookup"><span data-stu-id="377f5-172">Running our application and browsing to /Store/Browse?genre=Jazz shows that our results are now being pulled from the database, displaying all albums in our selected Genre.</span></span>

![](mvc-music-store-part-4/_static/image2.jpg)

<span data-ttu-id="377f5-173">/Store/Ayrıntılar/[ID] URL 'imizde aynı değişikliği yapacağız ve kukla verilerimizden KIMLIĞI parametre değeriyle eşleşen bir albüm yükleyen bir veritabanı sorgusuyla değiştiririz.</span><span class="sxs-lookup"><span data-stu-id="377f5-173">We'll make the same change to our /Store/Details/[id] URL, and replace our dummy data with a database query which loads an Album whose ID matches the parameter value.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample12.cs)]

<span data-ttu-id="377f5-174">Uygulamamızı çalıştırmak ve/Store/Details/1 adresine gözatımız, sonuçlarımızın artık veritabanından çekilmekte olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="377f5-174">Running our application and browsing to /Store/Details/1 shows that our results are now being pulled from the database.</span></span>

![](mvc-music-store-part-4/_static/image5.png)

<span data-ttu-id="377f5-175">Şimdi mağaza ayrıntıları sayfamız, albüm KIMLIĞI tarafından bir albümü görüntüleyecek şekilde ayarlandığına göre, Ayrıntılar görünümünü bağlamak için **tarama** görünümünü güncelleştirelim.</span><span class="sxs-lookup"><span data-stu-id="377f5-175">Now that our Store Details page is set up to display an album by the Album ID, let's update the **Browse** view to link to the Details view.</span></span> <span data-ttu-id="377f5-176">Önceki bölümde yer alacak şekilde mağaza dizininden Store 'a bağlantı yaptığımız gibi HTML. ActionLink kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="377f5-176">We will use Html.ActionLink, exactly as we did to link from Store Index to Store Browse at the end of the previous section.</span></span> <span data-ttu-id="377f5-177">Aşağıda, tarama görünümünün tüm kaynağı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="377f5-177">The complete source for the Browse view appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample13.cshtml)]

<span data-ttu-id="377f5-178">Artık mağaza sayfamıza, kullanılabilir albümleri listeleyen bir tarz sayfasına gözatabiliriz ve bu albümün ayrıntılarını görüntüleyebilmemiz için bir albüme tıklanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="377f5-178">We're now able to browse from our Store page to a Genre page, which lists the available albums, and by clicking on an album we can view details for that album.</span></span>

![](mvc-music-store-part-4/_static/image6.png)

> [!div class="step-by-step"]
> <span data-ttu-id="377f5-179">[Önceki](mvc-music-store-part-3.md)
> [İleri](mvc-music-store-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="377f5-179">[Previous](mvc-music-store-part-3.md)
[Next](mvc-music-store-part-5.md)</span></span>
