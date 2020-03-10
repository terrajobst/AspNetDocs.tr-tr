---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: Veritabanı oluşturma | Microsoft Docs
author: microsoft
description: 2\. adım, Nerdakşam yemeği uygulamamız için akşam yemeği ve RSVP verilerinin tümünü tutan veritabanını oluşturma adımlarını gösterir.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: b0aa7c8cdf741f44e09ed18e2b2f73fe6bf786ae
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581006"
---
# <a name="create-a-database"></a><span data-ttu-id="7e0e8-103">Veritabanı Oluşturma</span><span class="sxs-lookup"><span data-stu-id="7e0e8-103">Create a Database</span></span>

<span data-ttu-id="7e0e8-104">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="7e0e8-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="7e0e8-105">PDF 'YI indir</span><span class="sxs-lookup"><span data-stu-id="7e0e8-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="7e0e8-106">Bu, ASP.NET MVC 1 kullanarak küçük, ancak tam bir Web uygulamasının nasıl oluşturulacağını gösteren ücretsiz bir ["Nerdakşam yemeği" uygulama öğreticisinin](introducing-the-nerddinner-tutorial.md) 2. adımından oluşur.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-106">This is step 2 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="7e0e8-107">2\. adım, Nerdakşam yemeği uygulamamız için akşam yemeği ve RSVP verilerinin tümünü tutan veritabanını oluşturma adımlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-107">Step 2 shows the steps to create the database holding all of the dinner and RSVP data for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="7e0e8-108">ASP.NET MVC 3 kullanıyorsanız, [MVC 3 Ile çalışmaya başlama](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC müzik mağazası](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) öğreticilerini izlemeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-2-creating-the-database"></a><span data-ttu-id="7e0e8-109">Nerdakşam yemeği adım 2: veritabanını oluşturma</span><span class="sxs-lookup"><span data-stu-id="7e0e8-109">NerdDinner Step 2: Creating the Database</span></span>

<span data-ttu-id="7e0e8-110">Nerdakşam yemeği uygulamamız için tüm akşam yemeği ve RSVP verilerini depolamak üzere bir veritabanı kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-110">We'll be using a database to store all of the Dinner and RSVP data for our NerdDinner application.</span></span>

<span data-ttu-id="7e0e8-111">Aşağıdaki adımlarda, ücretsiz SQL Server Express sürümünü kullanarak veritabanı oluşturma ( [Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)v2 'yi kullanarak kolayca yükleyebileceğiniz) gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-111">The steps below show creating the database using the free SQL Server Express edition (which you can easily install using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)).</span></span> <span data-ttu-id="7e0e8-112">Yazılacak tüm kodlar hem SQL Server Express hem de tam SQL Server ile birlikte çalışacak.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-112">All of the code we'll write works with both SQL Server Express and the full SQL Server.</span></span>

### <a name="creating-a-new-sql-server-express-database"></a><span data-ttu-id="7e0e8-113">Yeni bir SQL Server Express veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7e0e8-113">Creating a new SQL Server Express database</span></span>

<span data-ttu-id="7e0e8-114">Web projemizi sağ tıklayıp ardından **&gt;yeni öğe Ekle** menü komutunu seçerek başlayacağız:</span><span class="sxs-lookup"><span data-stu-id="7e0e8-114">We'll begin by right-clicking on our web project, and then select the **Add-&gt;New Item** menu command:</span></span>

![](create-a-database/_static/image1.png)

<span data-ttu-id="7e0e8-115">Bu işlem, Visual Studio 'nun "yeni öğe Ekle" iletişim kutusunu getirir.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-115">This will bring up Visual Studio's "Add New Item" dialog.</span></span> <span data-ttu-id="7e0e8-116">"Veri" kategorisine göre filtreleyecek ve "veritabanı SQL Server" öğe şablonunu seçeceğiz:</span><span class="sxs-lookup"><span data-stu-id="7e0e8-116">We'll filter by the "Data" category and select the "SQL Server Database" item template:</span></span>

![](create-a-database/_static/image2.png)

<span data-ttu-id="7e0e8-117">"Nerdakşam. mdf" oluşturmak istediğimiz SQL Server Express veritabanını adı vereceğiz ve Tamam ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-117">We'll name the SQL Server Express database we want to create "NerdDinner.mdf" and hit ok.</span></span> <span data-ttu-id="7e0e8-118">Daha sonra Visual Studio, bu dosyayı \app\_veri dizinimize eklemek isteyip istemediğini sorar (bir dizin zaten hem okuma hem de yazma güvenlik ACL 'Leri ile kuruldu):</span><span class="sxs-lookup"><span data-stu-id="7e0e8-118">Visual Studio will then ask us if we want to add this file to our \App\_Data directory (which is a directory already setup with both read and write security ACLs):</span></span>

![](create-a-database/_static/image3.png)

<span data-ttu-id="7e0e8-119">"Evet" i tıklayacağız ve yeni veritabanımız Çözüm Gezgini oluşturulacak ve şu eklenecektir:</span><span class="sxs-lookup"><span data-stu-id="7e0e8-119">We'll click "Yes" and our new database will be created and added to our Solution Explorer:</span></span>

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a><span data-ttu-id="7e0e8-120">Veritabanımız içinde tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="7e0e8-120">Creating Tables within our Database</span></span>

<span data-ttu-id="7e0e8-121">Artık yeni bir boş veritabanı var.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-121">We now have a new empty database.</span></span> <span data-ttu-id="7e0e8-122">Buraya tablo ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-122">Let's add some tables to it.</span></span>

<span data-ttu-id="7e0e8-123">Bunu yapmak için, Visual Studio içindeki "Sunucu Gezgini" sekme penceresine giderek veritabanlarını ve sunucuları yönetebilmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-123">To do this we'll navigate to the "Server Explorer" tab window within Visual Studio, which enables us to manage databases and servers.</span></span> <span data-ttu-id="7e0e8-124">Uygulamamızın \app\_Data klasöründe depolanan SQL Server Express veritabanları, Sunucu Gezgini içinde otomatik olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-124">SQL Server Express databases stored in the \App\_Data folder of our application will automatically show up within the Server Explorer.</span></span> <span data-ttu-id="7e0e8-125">İsteğe bağlı olarak, listeye ek SQL Server veritabanları (yerel ve uzak) eklemek için "Sunucu Gezgini" penceresinin en üstündeki "veritabanına Bağlan" simgesine de tıklayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7e0e8-125">We can optionally use the "Connect to Database" icon on the top of the "Server Explorer" window to add additional SQL Server databases (both local and remote) to the list as well:</span></span>

![](create-a-database/_static/image5.png)

<span data-ttu-id="7e0e8-126">Nerdakşam yemeği veritabanımız için bir tane olmak üzere bir tane olmak üzere, dinlerimizi depolamak için bir tane ve diğeri de RSVP kabulleri izlemek için diğerini.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-126">We will add two tables to our NerdDinner database – one to store our Dinners, and the other to track RSVP acceptances to them.</span></span> <span data-ttu-id="7e0e8-127">Veritabanımız içindeki "tablolar" klasörüne sağ tıklayıp "yeni tablo Ekle" menü komutunu seçerek yeni tablolar oluşturuyoruz:</span><span class="sxs-lookup"><span data-stu-id="7e0e8-127">We can create new tables by right-clicking on the "Tables" folder within our database and choosing the "Add New Table" menu command:</span></span>

![](create-a-database/_static/image6.png)

<span data-ttu-id="7e0e8-128">Bu, tablomızın şemasını yapılandırmamızı sağlayan bir Tablo Tasarımcısı açar.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-128">This will open up a table designer that allows us to configure the schema of our table.</span></span> <span data-ttu-id="7e0e8-129">"Dinlenebilir" tablomız için 10 veri sütunu ekleyeceğiz:</span><span class="sxs-lookup"><span data-stu-id="7e0e8-129">For our "Dinners" table we will add 10 columns of data:</span></span>

![](create-a-database/_static/image7.png)

<span data-ttu-id="7e0e8-130">"DinnerID" sütununun tablo için benzersiz bir birincil anahtar olmasını istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-130">We want the "DinnerID" column to be a unique primary key for the table.</span></span> <span data-ttu-id="7e0e8-131">Bunu, "DinnerID" sütununa sağ tıklayıp "birincil anahtarı ayarla" menü öğesini seçerek yapılandırabiliriz:</span><span class="sxs-lookup"><span data-stu-id="7e0e8-131">We can configure this by right-clicking on the "DinnerID" column and choosing the "Set Primary Key" menu item:</span></span>

![](create-a-database/_static/image8.png)

<span data-ttu-id="7e0e8-132">Bir birincil anahtar DinnerID yapmanın yanı sıra, tabloya yeni veri satırları eklendikçe değeri otomatik olarak artan bir "kimlik" sütunu olarak yapılandırmak istiyoruz (yani ilk eklenen akşam yemeği satırı, ikinci eklenen satır için bir DinnerID 1 olacaktır) DinnerID, vb. olur.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-132">In addition to making DinnerID a primary key, we also want configure it as an "identity" column whose value is automatically incremented as new rows of data are added to the table (meaning the first inserted Dinner row will have a DinnerID of 1, the second inserted row will have a DinnerID of 2, etc).</span></span>

<span data-ttu-id="7e0e8-133">Bunu, "DinnerID" sütununu seçerek yapabiliriz ve ardından "sütun özellikleri" düzenleyicisini kullanarak sütunda "(kimlik)" özelliğini "Evet" olarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-133">We can do this by selecting the "DinnerID" column and then use the "Column Properties" editor to set the "(Is Identity)" property on the column to "Yes".</span></span> <span data-ttu-id="7e0e8-134">Standart kimlik varsayılanlarını (1 ' den başlar ve her yeni akşam yemeği satırında 1 artışı) kullanacağız:</span><span class="sxs-lookup"><span data-stu-id="7e0e8-134">We will use the standard identity defaults (start at 1 and increment 1 on each new Dinner row):</span></span>

![](create-a-database/_static/image9.png)

<span data-ttu-id="7e0e8-135">Daha sonra CTRL-S yazarak veya **dosya&gt;kaydet** menü komutunu kullanarak tabloımızı kaydedeceğiz.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-135">We'll then save our table by typing Ctrl-S or by using the **File-&gt;Save** menu command.</span></span> <span data-ttu-id="7e0e8-136">Bu, tabloyu adı etmemizi ister.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-136">This will prompt us to name the table.</span></span> <span data-ttu-id="7e0e8-137">"Dinetleri" olarak adlandırın:</span><span class="sxs-lookup"><span data-stu-id="7e0e8-137">We'll name it "Dinners":</span></span>

![](create-a-database/_static/image10.png)

<span data-ttu-id="7e0e8-138">Yeni dinlenebilir tablomız, Sunucu Gezgini 'nde veritabanı içinde görünür.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-138">Our new Dinners table will then show up within our database in the server explorer.</span></span>

<span data-ttu-id="7e0e8-139">Daha sonra yukarıdaki adımları yineleyecektir ve bir "RSVP" tablosu oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-139">We'll then repeat the above steps and create a "RSVP" table.</span></span> <span data-ttu-id="7e0e8-140">Bu tabloda 3 sütun vardır.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-140">This table with have 3 columns.</span></span> <span data-ttu-id="7e0e8-141">RsvpID Column öğesini birincil anahtar olarak ayarlayacağız ve ayrıca bunu bir kimlik sütunu oluşturacak:</span><span class="sxs-lookup"><span data-stu-id="7e0e8-141">We will setup the RsvpID column as the primary key, and also make it an identity column:</span></span>

![](create-a-database/_static/image11.png)

<span data-ttu-id="7e0e8-142">Bunu kaydedeceğiz ve "RSVP" adına sunacağız.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-142">We'll save it and give it the name "RSVP".</span></span>

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a><span data-ttu-id="7e0e8-143">Tablolar arasında yabancı anahtar Ilişkisi ayarlama</span><span class="sxs-lookup"><span data-stu-id="7e0e8-143">Setting up a Foreign Key Relationship between Tables</span></span>

<span data-ttu-id="7e0e8-144">Artık veritabanımızda iki tablo var.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-144">We now have two tables within our database.</span></span> <span data-ttu-id="7e0e8-145">Son şema tasarım adımımız, her bir akşam yemeği satırını buna uygulanan sıfır veya daha fazla RSVP satırıyla ilişkilendirebilmemiz için, bu iki tablo arasında "bire çok" bir ilişki kurmak olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-145">Our last schema design step will be to setup a "one-to-many" relationship between these two tables – so that we can associate each Dinner row with zero or more RSVP rows that apply to it.</span></span> <span data-ttu-id="7e0e8-146">Bunu, RSVP tablosunun "DinnerID" sütununu "dinlenebilir" tablosundaki "DinnerID" sütunuyla bir yabancı anahtar ilişkisine sahip olacak şekilde yapılandırarak yapacağız.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-146">We will do this by configuring the RSVP table's "DinnerID" column to have a foreign-key relationship to the "DinnerID" column in the "Dinners" table.</span></span>

<span data-ttu-id="7e0e8-147">Bunu yapmak için, Sunucu Gezgini 'nde çift tıklayarak, Tablo Tasarımcısı içindeki RSVP tablosunu açacağız.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-147">To do this we'll open up the RSVP table within the table designer by double-clicking it in the server explorer.</span></span> <span data-ttu-id="7e0e8-148">Bundan sonra, içinde "DinnerID" sütununu seçeceğiz, sağ tıklayıp "Ilişkiler..." seçeneğini belirleyin. bağlam menüsü komutu:</span><span class="sxs-lookup"><span data-stu-id="7e0e8-148">We'll then select the "DinnerID" column within it, right-click, and choose the "Relationships…" context menu command:</span></span>

![](create-a-database/_static/image12.png)

<span data-ttu-id="7e0e8-149">Bu, tablolar arasındaki ilişkileri ayarlamak için kullandığımız bir iletişim kutusu getirir:</span><span class="sxs-lookup"><span data-stu-id="7e0e8-149">This will bring up a dialog that we can use to setup relationships between tables:</span></span>

![](create-a-database/_static/image13.png)

<span data-ttu-id="7e0e8-150">İletişim kutusuna yeni bir ilişki eklemek için "Ekle" düğmesine tıklayacağız.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-150">We'll click the "Add" button to add a new relationship to the dialog.</span></span> <span data-ttu-id="7e0e8-151">İlişki eklendikten sonra, iletişim kutusunun sağındaki özellik kılavuzunda bulunan "tablolar ve sütun belirtimi" ağaç görünümü düğümünü genişleteceğiz ve ardından "..." sağ taraftaki düğme:</span><span class="sxs-lookup"><span data-stu-id="7e0e8-151">Once a relationship has been added, we'll expand the "Tables and Column Specification" tree-view node within the property grid to the right of the dialog, and then click the "…" button to the right of it:</span></span>

![](create-a-database/_static/image14.png)

<span data-ttu-id="7e0e8-152">"..." Seçeneğine tıklan düğme, ilişkiye hangi tabloların ve sütunların dahil olduğunu belirtmemizi sağlayan başka bir iletişim kutusu getirir ve ilişkiyi de vermemizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-152">Clicking the "…" button will bring up another dialog that allows us to specify which tables and columns are involved in the relationship, as well as allow us to name the relationship.</span></span>

<span data-ttu-id="7e0e8-153">Birincil anahtar tablosunu "dinlenebilir" olacak şekilde değiştirecek ve birincil anahtar olarak dinlenebilir tablosu içindeki "DinnerID" sütununu seçeceğiz.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-153">We will change the Primary Key Table to be "Dinners", and select the "DinnerID" column within the Dinners table as the primary key.</span></span> <span data-ttu-id="7e0e8-154">RSVP tablomız yabancı anahtar tablosu ve RSVP olacaktır. DinnerID sütunu yabancı anahtar olarak ilişkilendirilir:</span><span class="sxs-lookup"><span data-stu-id="7e0e8-154">Our RSVP table will be the foreign-key table, and the RSVP.DinnerID column will be associated as the foreign-key:</span></span>

![](create-a-database/_static/image15.png)

<span data-ttu-id="7e0e8-155">Artık RSVP tablosundaki her bir satır, akşam yemeği tablosundaki bir satırla ilişkilendirilecektir.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-155">Now each row in the RSVP table will be associated with a row in the Dinner table.</span></span> <span data-ttu-id="7e0e8-156">SQL Server, ABD için bilgi tutarlılığını koruyacak ve geçerli bir akşam yemeği satırına işaret etmezse yeni bir RSVP satırı eklememizi önlemektir.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-156">SQL Server will maintain referential integrity for us – and prevent us from adding a new RSVP row if it does not point to a valid Dinner row.</span></span> <span data-ttu-id="7e0e8-157">Ayrıca, kendisine başvuruda bulunan RSVP satırları varsa, bir akşam yemeği satırını silmemizi önler.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-157">It will also prevent us from deleting a Dinner row if there are still RSVP rows referring to it.</span></span>

### <a name="adding-data-to-our-tables"></a><span data-ttu-id="7e0e8-158">Tablolarımıza veri ekleme</span><span class="sxs-lookup"><span data-stu-id="7e0e8-158">Adding Data to our Tables</span></span>

<span data-ttu-id="7e0e8-159">Dinlenebilir tablolarımızla bazı örnek veriler ekleyerek bitelim.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-159">Let's finish by adding some sample data to our Dinners table.</span></span> <span data-ttu-id="7e0e8-160">Tabloya sağ tıklayıp Sunucu Gezgini, "tablo verilerini göster" komutunu seçerek tabloya veri ekleyebiliriz:</span><span class="sxs-lookup"><span data-stu-id="7e0e8-160">We can add data to a table by right-clicking on it within the Server Explorer and choosing the "Show Table Data" command:</span></span>

![](create-a-database/_static/image16.png)

<span data-ttu-id="7e0e8-161">Uygulamayı uygulamaya başladığımızda daha sonra kullanacağımız birkaç akşam yemeği verisi satırı ekleyeceğiz:</span><span class="sxs-lookup"><span data-stu-id="7e0e8-161">We'll add a few rows of Dinner data that we can use later as we start implementing the application:</span></span>

![](create-a-database/_static/image17.png)

### <a name="next-step"></a><span data-ttu-id="7e0e8-162">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="7e0e8-162">Next Step</span></span>

<span data-ttu-id="7e0e8-163">Veritabanı oluşturma işlemi tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-163">We've finished creating our database.</span></span> <span data-ttu-id="7e0e8-164">Şimdi, sorgulamak ve güncelleştirmek için kullanabileceğiz model sınıfları oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="7e0e8-164">Let's now create model classes that we can use to query and update it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7e0e8-165">[Önceki](create-a-new-aspnet-mvc-project.md)
> [İleri](build-a-model-with-business-rule-validations.md)</span><span class="sxs-lookup"><span data-stu-id="7e0e8-165">[Previous](create-a-new-aspnet-mvc-project.md)
[Next](build-a-model-with-business-rule-validations.md)</span></span>
