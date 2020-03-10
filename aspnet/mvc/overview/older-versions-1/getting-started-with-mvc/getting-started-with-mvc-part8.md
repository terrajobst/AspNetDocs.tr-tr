---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
title: Modele sütun ekleme | Microsoft Docs
author: shanselman
description: Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir. Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturun.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 7ae696b9-348f-4993-8ebb-a838acbe0c28
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
msc.type: authoredcontent
ms.openlocfilehash: 1cf092c3db3959d6f47006f1be2ba82833c5dc06
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543584"
---
# <a name="adding-a-column-to-the-model"></a><span data-ttu-id="1fbf0-104">Modele Sütun Ekleme</span><span class="sxs-lookup"><span data-stu-id="1fbf0-104">Adding a Column to the Model</span></span>

<span data-ttu-id="1fbf0-105">[Scott Hanselman](https://github.com/shanselman) tarafından</span><span class="sxs-lookup"><span data-stu-id="1fbf0-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="1fbf0-106">Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="1fbf0-107">Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="1fbf0-108">Diğer ASP.NET MVC öğreticileri ve örneklerini bulmak için [ASP.NET MVC öğrenme merkezini](../../../index.md) ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="1fbf0-109">Bu bölümde, veritabanımızın şemasında nasıl değişiklik yapacağımız ve uygulamamız içindeki değişiklikleri işleyebiliriz.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-109">In this section we are going to walk through how we can make changes to the schema of our database, and handle the changes within our application.</span></span>

<span data-ttu-id="1fbf0-110">Film tablosuna bir "derecelendirme" sütunu ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-110">Let's add a "Rating" Column to the Movie table.</span></span> <span data-ttu-id="1fbf0-111">IDE 'ye dönün ve Veritabanı Gezgini tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-111">Go back to the IDE and click the Database Explorer.</span></span> <span data-ttu-id="1fbf0-112">Film tablosuna sağ tıklayıp tablo tanımını aç ' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-112">Right click the Movie table and select Open Table Definition.</span></span>

<span data-ttu-id="1fbf0-113">Aşağıda görüldüğü gibi bir "derecelendirme" sütunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-113">Add a "Rating" column as seen below.</span></span> <span data-ttu-id="1fbf0-114">Artık hiç derecelendirme olmadığından, sütun null değerlere izin verebilir.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-114">Since we don't have any Ratings now, the column can allow nulls.</span></span> <span data-ttu-id="1fbf0-115">Kaydet’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-115">Click Save.</span></span>

<span data-ttu-id="1fbf0-116">[![filmlerini tabloları Düzenle](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1fbf0-116">[![Editing Movies Table](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)</span></span>

<span data-ttu-id="1fbf0-117">Sonra, Çözüm Gezgini dönün ve filmler. edmx dosyasını açın (\Modeller klasöründe bulunur).</span><span class="sxs-lookup"><span data-stu-id="1fbf0-117">Next, return to the Solution Explorer and open up the Movies.edmx file (which is in the \Models folder).</span></span> <span data-ttu-id="1fbf0-118">Tasarım yüzeyine (beyaz alan) sağ tıklayın ve modeli veritabanından Güncelleştir ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-118">Right click on the design surface (the white area) and select Update Model from Database.</span></span>

<span data-ttu-id="1fbf0-119">[![filmler-Microsoft Visual Web Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="1fbf0-119">[![Movies - Microsoft Visual Web Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)</span></span>

<span data-ttu-id="1fbf0-120">Bu, "Güncelleştirme Sihirbazı" nı başlatacaktır.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-120">This will launch the "Update Wizard".</span></span> <span data-ttu-id="1fbf0-121">İçindeki Yenile sekmesine tıklayın ve son ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-121">Click the Refresh tab within it and click Finish.</span></span> <span data-ttu-id="1fbf0-122">Ardından, film modeli sınıfımız yeni sütunla güncelleştirilecektir.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-122">Our Movie model class will then be updated with the new column.</span></span>

![Güncelleştirme Sihirbazı (2)](getting-started-with-mvc-part8/_static/image5.png)

<span data-ttu-id="1fbf0-124">Son ' a tıkladıktan sonra modelimizin film varlığına yeni derecelendirme sütununun eklendiğini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-124">After clicking Finish, you can see the new Rating Column has been added to the Movie Entity in our model.</span></span>

<span data-ttu-id="1fbf0-125">[![filmi varlık](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="1fbf0-125">[![Movie Entity](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)</span></span>

<span data-ttu-id="1fbf0-126">Veritabanı modeline bir sütun ekledik, ancak görünümler bunun hakkında bilgi sahibi değil.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-126">We've added a column in the database model, but the Views don't know about it.</span></span>

## <a name="update-views-with-model-changes"></a><span data-ttu-id="1fbf0-127">Model değişiklikleriyle görünümleri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="1fbf0-127">Update Views with Model Changes</span></span>

<span data-ttu-id="1fbf0-128">Yeni derecelendirme sütununu yansıtmak için görünüm şablonlarımızı güncelleştirebilmemiz için birkaç yol vardır.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-128">There are a few ways we could update our view templates to reflect the new Rating column.</span></span> <span data-ttu-id="1fbf0-129">Bu görünümleri Görünüm Ekle iletişim kutusu aracılığıyla oluşturduğumuz için bunları silip yeniden oluşturarız.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-129">Since we created these Views by generating them via the Add View dialog, we could delete them and recreate them again.</span></span> <span data-ttu-id="1fbf0-130">Bununla birlikte, genellikle insanlar ilk scafkatnesten görünüm şablonlarında değişiklikler yapmış olur ve oluşturma için KIMLIK alanına yaptığımız gibi alanları el ile eklemek veya silmek olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-130">However, typically people will have already made modifications to their View templates from the initial scaffolded generation and will want to add or delete fields manually, just as we did with the ID field for Create.</span></span>

<span data-ttu-id="1fbf0-131">\Views\Movies\Index.aspx şablonunu açın ve film tablosunun baş &lt;&gt;derecelendirme&lt;/TH&gt; ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-131">Open up the \Views\Movies\Index.aspx template and add a &lt;th&gt;Rating&lt;/th&gt; to the head of the Movie table.</span></span> <span data-ttu-id="1fbf0-132">Tarzı sonra mayın ekledim.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-132">I added mine after Genre.</span></span> <span data-ttu-id="1fbf0-133">Ardından, aynı sütun konumunda, ancak aşağı doğru, yeni Derecelendirmem için bir satır ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-133">Then, in the same column position but lower down, add a line to output our new Rating.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample1.aspx)]

<span data-ttu-id="1fbf0-134">Son Index. aspx şablonumuz şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="1fbf0-134">Our final Index.aspx template will look like this:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample2.aspx)]

<span data-ttu-id="1fbf0-135">Daha sonra \Views\Movies\Create.aspx şablonunu açıp yeni derecelendirme özelliği için bir etiket ve metin kutusu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1fbf0-135">Let's then open up the \Views\Movies\Create.aspx template and add a Label and Textbox for our new Rating property:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample3.aspx)]

<span data-ttu-id="1fbf0-136">Son Create. aspx şablonumuz bu şekilde görünür ve tarayıcının başlığını ve ikincil &lt;H2&gt; başlığını burada "film oluşturma" gibi bir şekilde değiştirelim!</span><span class="sxs-lookup"><span data-stu-id="1fbf0-136">Our final Create.aspx template will look like this, and let's change our browser's title and secondary &lt;h2&gt; title to something like "Create a Movie" while we're in here!</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample4.aspx)]

<span data-ttu-id="1fbf0-137">Uygulamanızı çalıştırın ve şimdi oluştur sayfasına eklenen veritabanında yeni bir alanınız var.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-137">Run your app and now you've got a new field in the database that's been added to the Create page.</span></span> <span data-ttu-id="1fbf0-138">Yeni bir film ekleyin-bu kez bir derecelendirmeye sahip ve Oluştur ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-138">Add a new Movie - this time with a Rating - and click Create.</span></span>

<span data-ttu-id="1fbf0-139">[Film oluşturma-Windows Internet Explorer ![](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="1fbf0-139">[![Create a Movie - Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)</span></span>

<span data-ttu-id="1fbf0-140">Oluştur ' a tıkladıktan sonra, yeni filmin veritabanındaki yeni derecelendirme sütunuyla listelendiği dizin sayfasına gönderilir</span><span class="sxs-lookup"><span data-stu-id="1fbf0-140">After you click Create, you're sent to the Index page where you new Movie is listed with the new Rating Column in the database</span></span>

<span data-ttu-id="1fbf0-141">[![film listesi-Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="1fbf0-141">[![Movie List - Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)</span></span>

<span data-ttu-id="1fbf0-142">Bu temel öğretici, denetleyicileri oluşturma, bunları görünümlerle ilişkilendirme ve sabit kodlanmış verileri geçirme konusunda çalışmaya başladım.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-142">This basic tutorial got you started making Controllers, associating them with Views and passing around hard-coded data.</span></span> <span data-ttu-id="1fbf0-143">Daha sonra bir veritabanı oluşturulup tasarlıyoruz ve veri yerleştirdik.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-143">Then we created and designed a Database and put some data it in.</span></span> <span data-ttu-id="1fbf0-144">Veritabanından alınan verileri aldık ve bir HTML tablosunda görüntüliyoruz.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-144">We retrieved the data from the database and displayed it in an HTML table.</span></span> <span data-ttu-id="1fbf0-145">Daha sonra kullanıcının Web uygulamasının içinden veritabanına veri eklemesine izin veren bir oluşturma formu ekledik.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-145">Then we added a Create form that let the user add data to the database themselves from within the Web Application.</span></span> <span data-ttu-id="1fbf0-146">Doğrulama ekledik, sonra doğrulamayı istemci tarafında JavaScript 'ı kullanacak şekilde yaptık.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-146">We added validation, then made the validation use JavaScript on the client-side.</span></span> <span data-ttu-id="1fbf0-147">Son olarak, veritabanını yeni bir veri sütunu içerecek şekilde değiştirdik ve bu yeni verileri oluşturmak ve göstermek için iki sayfamızı güncelleştiririz.</span><span class="sxs-lookup"><span data-stu-id="1fbf0-147">Finally, we changed the database to include a new column of data, then updated our two pages to create and display this new data.</span></span>

<span data-ttu-id="1fbf0-148">Artık ASP.NET MVC hakkında daha fazla bilgi edinmek için [https://asp.net/mvc](https://asp.net/mvc) ' de ara düzeyi Öğreticimize "[MVC müzik mağazamız](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)" ve birçok video ve kaynak üzerinde geçiş yapmayı öneririz!</span><span class="sxs-lookup"><span data-stu-id="1fbf0-148">I now encourage you to move on to our intermediate-level tutorial "[MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)" as well as the many videos and resources at [https://asp.net/mvc](https://asp.net/mvc) to learn even more about ASP.NET MVC!</span></span>

<span data-ttu-id="1fbf0-149">Keyfini çıkarın!</span><span class="sxs-lookup"><span data-stu-id="1fbf0-149">Enjoy!</span></span>

- <span data-ttu-id="1fbf0-150">Scott Hanselman-Twitter 'da [http://hanselman.com](http://hanselman.com) ve [@shanselman](http://twitter.com/shanselman) .</span><span class="sxs-lookup"><span data-stu-id="1fbf0-150">Scott Hanselman - [http://hanselman.com](http://hanselman.com) and [@shanselman](http://twitter.com/shanselman) on Twitter.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="1fbf0-151">Öncekini</span><span class="sxs-lookup"><span data-stu-id="1fbf0-151">Previous</span></span>](getting-started-with-mvc-part7.md)
