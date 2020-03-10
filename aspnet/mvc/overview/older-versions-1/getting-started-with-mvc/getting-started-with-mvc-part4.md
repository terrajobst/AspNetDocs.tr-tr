---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
title: Veritabanı oluşturma | Microsoft Docs
author: shanselman
description: Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir. Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturun.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 742df67f-484d-4ef3-af6b-8c791e556b43
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
msc.type: authoredcontent
ms.openlocfilehash: 995db714ce6365415d06dc458aee84a31c7c8fd6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581440"
---
# <a name="creating-a-database"></a><span data-ttu-id="0cf70-104">Veritabanı Oluşturma</span><span class="sxs-lookup"><span data-stu-id="0cf70-104">Creating a Database</span></span>

<span data-ttu-id="0cf70-105">[Scott Hanselman](https://github.com/shanselman) tarafından</span><span class="sxs-lookup"><span data-stu-id="0cf70-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="0cf70-106">Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir.</span><span class="sxs-lookup"><span data-stu-id="0cf70-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="0cf70-107">Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="0cf70-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="0cf70-108">Diğer ASP.NET MVC öğreticileri ve örneklerini bulmak için [ASP.NET MVC öğrenme merkezini](../../../index.md) ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="0cf70-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="0cf70-109">Bu bölümde, film Verilerimizi depolamak ve almak için kullanacağımız yeni bir SQL Express veritabanı oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="0cf70-109">In this section we are going to create a new SQL Express database that we'll use to store and retrieve our movie data.</span></span> <span data-ttu-id="0cf70-110">Visual Web Developer IDE içinden Görünüm ' ü seçin | Sunucu Gezgini.</span><span class="sxs-lookup"><span data-stu-id="0cf70-110">From within the Visual Web Developer IDE, select View | Server Explorer.</span></span> <span data-ttu-id="0cf70-111">Veri bağlantıları ' na sağ tıklayıp bağlantı ekle... ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0cf70-111">Right click on Data Connections and click Add Connection...</span></span>

![AddConnection](getting-started-with-mvc-part4/_static/image1.png)

<span data-ttu-id="0cf70-113">Veri kaynağı seç iletişim kutusunda Microsoft SQL Server ' ı seçin ve devam ' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="0cf70-113">In the Choose Data Source dialog, select Microsoft SQL Server and select Continue.</span></span>

![](getting-started-with-mvc-part4/_static/image2.png)

<span data-ttu-id="0cf70-114">Bağlantı Ekle iletişim kutusunda, sunucu adınız için ".\SQLEXPRESS" yazın ve yeni veritabanınızın adı olarak "Filmler" yazın.</span><span class="sxs-lookup"><span data-stu-id="0cf70-114">In the Add Connection dialog, enter ".\SQLEXPRESS" for your Server Name, and enter "Movies" as the name for your new database.</span></span>

<span data-ttu-id="0cf70-115">[![bağlantı iletişim kutusu Ekle](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="0cf70-115">[![Add Connection dialog](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)</span></span>

<span data-ttu-id="0cf70-116">Tamam ' a tıkladığınızda bu veritabanını oluşturmak isteyip istemediğiniz sorulur.</span><span class="sxs-lookup"><span data-stu-id="0cf70-116">Click OK and you'll be asked if you want to create that database.</span></span> <span data-ttu-id="0cf70-117">Evet ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="0cf70-117">Select yes.</span></span>

<span data-ttu-id="0cf70-118">[![film oluşturmak mı istiyorsunuz?](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="0cf70-118">[![Create Movies?](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)</span></span>

<span data-ttu-id="0cf70-119">Artık Sunucu Gezgini boş bir veritabanınız var.</span><span class="sxs-lookup"><span data-stu-id="0cf70-119">Now you've got an empty database in Server Explorer.</span></span>

![Yeni Tablo Ekle](getting-started-with-mvc-part4/_static/image7.png)

<span data-ttu-id="0cf70-121">Tablolar ' a sağ tıklayıp tablo Ekle ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0cf70-121">Right click on Tables and click Add Table.</span></span> <span data-ttu-id="0cf70-122">Tablo Tasarımcısı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="0cf70-122">The Table Designer will appear.</span></span> <span data-ttu-id="0cf70-123">Kimlik, başlık, ReleaseDate, tarz ve fiyat için sütun ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0cf70-123">Add columns for Id, Title, ReleaseDate, Genre, and Price.</span></span> <span data-ttu-id="0cf70-124">KIMLIK sütununa sağ tıklayıp birincil anahtarı ayarla ' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0cf70-124">Right click on the ID column and click set Primary Key.</span></span> <span data-ttu-id="0cf70-125">Tasarım alanlarım şu şekilde görünür.</span><span class="sxs-lookup"><span data-stu-id="0cf70-125">Here's what my design areas looks like.</span></span>

<span data-ttu-id="0cf70-126">[![veritabanı tablo Düzenleyicisi](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="0cf70-126">[![Database Table Editor](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)</span></span>

<span data-ttu-id="0cf70-127">Ayrıca, kimlik sütununu seçin ve aşağıdaki sütun özellikleri altında "kimlik belirtimi" ni "Evet" olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0cf70-127">Also, select the Id column and under Column Properties below change "Identity Specification" to "Yes."</span></span>

<span data-ttu-id="0cf70-128">[![IsIdentity-Column özellikleri](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="0cf70-128">[![IsIdentity - Column Properties](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)</span></span>

<span data-ttu-id="0cf70-129">Bitirdiğinizde, araç çubuğundaki Kaydet simgesine tıklayın veya dosya ' yı seçin | Menüden kaydedin ve tablonuzu "**film**" (tekil) olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="0cf70-129">When you've got it done, click the Save icon in the toolbar or select File | Save from the menu, and name your table "**Movie**" (singular).</span></span> <span data-ttu-id="0cf70-130">Bir veritabanı ve tablo aldık!</span><span class="sxs-lookup"><span data-stu-id="0cf70-130">We've got a database and a table!</span></span>

<span data-ttu-id="0cf70-131">[![ad seçin](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="0cf70-131">[![Choose Name](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)</span></span>

<span data-ttu-id="0cf70-132">Sunucu Gezgini ' ye dönüp film tablosuna sağ tıklayıp "tablo verilerini göster" i seçin.</span><span class="sxs-lookup"><span data-stu-id="0cf70-132">Go back to Server Explorer and right click the Movie table, then select "Show Table Data."</span></span> <span data-ttu-id="0cf70-133">Veritabanınızda bazı veriler olduğundan birkaç film girin.</span><span class="sxs-lookup"><span data-stu-id="0cf70-133">Enter a few movies so our database has some data.</span></span>

<span data-ttu-id="0cf70-134">[Veritabanı tablosu düzenlemesini ![](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)</span><span class="sxs-lookup"><span data-stu-id="0cf70-134">[![Database Table Editing](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)</span></span>

## <a name="creating-a-model"></a><span data-ttu-id="0cf70-135">Model Oluşturma</span><span class="sxs-lookup"><span data-stu-id="0cf70-135">Creating a Model</span></span>

<span data-ttu-id="0cf70-136">Şimdi, IDE 'nin sağ tarafındaki Çözüm Gezgini geri dönün ve modeller klasörüne sağ tıklayıp Ekle | ' yi seçin. Yeni öğe.</span><span class="sxs-lookup"><span data-stu-id="0cf70-136">Now, switch back to the Solution Explorer on the right hand side of the IDE and right-click on the Models folder and select Add | New Item.</span></span>

<span data-ttu-id="0cf70-137">[![addnewmodelıdıtem](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="0cf70-137">[![addnewmodelitem](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)</span></span>

<span data-ttu-id="0cf70-138">Yeni veritabanımızda bir varlık modeli oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="0cf70-138">We're going to create an Entity Model from our new database.</span></span> <span data-ttu-id="0cf70-139">Bu, projemizi, veritabanımızın içindeki verileri sorgulamanızı ve işlememizi kolaylaştıran bir sınıf kümesi ekler.</span><span class="sxs-lookup"><span data-stu-id="0cf70-139">This will add a set of classes to our project that makes it easy for us to query and manipulate the data within our database.</span></span> <span data-ttu-id="0cf70-140">İletişim kutusunun sol tarafındaki veri düğümünü seçin ve ardından ADO.NET Varlık Veri Modeli öğesi şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="0cf70-140">Select the Data node on the left-hand side of the dialog, and then select the ADO.NET Entity Data Model item template.</span></span> <span data-ttu-id="0cf70-141">It. edmx olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="0cf70-141">Name it Movies.edmx.</span></span>

<span data-ttu-id="0cf70-142">[AddNewDataModel ![](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)</span><span class="sxs-lookup"><span data-stu-id="0cf70-142">[![AddNewDataModel](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)</span></span>

<span data-ttu-id="0cf70-143">"Ekle" düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0cf70-143">Click the "Add" button.</span></span> <span data-ttu-id="0cf70-144">Bu daha sonra "Varlık Veri Modeli Sihirbazı" nı başlatacaktır.</span><span class="sxs-lookup"><span data-stu-id="0cf70-144">This will then launch the "Entity Data Model Wizard".</span></span>

<span data-ttu-id="0cf70-145">Açılan yeni iletişim kutusunda veritabanından oluştur ' u seçin.</span><span class="sxs-lookup"><span data-stu-id="0cf70-145">In the new dialog that pops up, select Generate from Database.</span></span> <span data-ttu-id="0cf70-146">Yeni bir veritabanı oluşturduğumuzdan, yalnızca yeni veritabanımız ve tablosuyla ilgili Entity Framework söylememiz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0cf70-146">Since we've just made a database, we'll only need to tell the Entity Framework about our new database and its table.</span></span> <span data-ttu-id="0cf70-147">Veritabanı bağlantınızı web uygulamamız yapılandırması ' nda kaydetmek için Ileri ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0cf70-147">Click Next to save our database connection in our web application's configuration.</span></span> <span data-ttu-id="0cf70-148">Şimdi tablolar ve film onay kutusunu işaretleyip son ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0cf70-148">Now, check the Tables and Movie checkbox and click Finish.</span></span>

<span data-ttu-id="0cf70-149">[![Varlık Veri Modeli Sihirbazı](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)</span><span class="sxs-lookup"><span data-stu-id="0cf70-149">[![Entity Data Model Wizard](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)</span></span>

<span data-ttu-id="0cf70-150">Şimdi yeni film tabloımızı Entity Framework Designer görebilir ve koddan bu tabloya erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cf70-150">Now we can see our new Movie table in the Entity Framework Designer and access it from code.</span></span>

<span data-ttu-id="0cf70-151">[![filmler-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="0cf70-151">[![Movies - Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)</span></span>

<span data-ttu-id="0cf70-152">Tasarım yüzeyinde bir "film" sınıfı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cf70-152">On the design surface you can see a "Movie" class.</span></span> <span data-ttu-id="0cf70-153">Bu sınıf, veritabanımızda "film" tablosuyla eşlenir ve içindeki her bir özellik tabloyla eşleşen bir sütunla eşlenir.</span><span class="sxs-lookup"><span data-stu-id="0cf70-153">This class maps to the "Movie" table in our database, and each property within it maps to a column with the table.</span></span> <span data-ttu-id="0cf70-154">Bir "film" sınıfının her örneği, "film" tablosu içindeki bir satıra karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="0cf70-154">Each instance of a "Movie" class will correspond to a row within the "Movie" table.</span></span>

<span data-ttu-id="0cf70-155">Entity Framework tarafından kullanılan varsayılan adlandırma ve eşleme kurallarını beğenmezseniz, bunları değiştirmek veya özelleştirmek için Entity Framework tasarımcısını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cf70-155">If you don't like the default naming and mapping conventions used by the Entity Framework, you can use the Entity Framework designer to change or customize them.</span></span> <span data-ttu-id="0cf70-156">Bu uygulama için Varsayılanları kullanacağız ve dosyayı olduğu gibi kaydetmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="0cf70-156">For this application we'll use the defaults and just save the file as-is.</span></span>

<span data-ttu-id="0cf70-157">Şimdi, bazı gerçek verilerle çalışalım!</span><span class="sxs-lookup"><span data-stu-id="0cf70-157">Now, let's work with some real data!</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0cf70-158">[Önceki](getting-started-with-mvc-part3.md)
> [İleri](getting-started-with-mvc-part5.md)</span><span class="sxs-lookup"><span data-stu-id="0cf70-158">[Previous](getting-started-with-mvc-part3.md)
[Next](getting-started-with-mvc-part5.md)</span></span>
