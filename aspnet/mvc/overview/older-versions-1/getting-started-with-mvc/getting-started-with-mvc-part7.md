---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
title: Modele doğrulama ekleme | Microsoft Docs
author: shanselman
description: Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir. Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturun.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: aa7b3e8e-e23d-49f1-b160-f99a7f2982bd
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
msc.type: authoredcontent
ms.openlocfilehash: 9403be574324c34edf93bef1e0e4fd7ba68a3a9d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543647"
---
# <a name="adding-validation-to-the-model"></a><span data-ttu-id="19bd9-104">Modele Doğrulama Ekleme</span><span class="sxs-lookup"><span data-stu-id="19bd9-104">Adding Validation to the Model</span></span>

<span data-ttu-id="19bd9-105">[Scott Hanselman](https://github.com/shanselman) tarafından</span><span class="sxs-lookup"><span data-stu-id="19bd9-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="19bd9-106">Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir.</span><span class="sxs-lookup"><span data-stu-id="19bd9-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="19bd9-107">Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="19bd9-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="19bd9-108">Diğer ASP.NET MVC öğreticileri ve örneklerini bulmak için [ASP.NET MVC öğrenme merkezini](../../../index.md) ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="19bd9-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="19bd9-109">Bu bölümde, uygulamamız içinde giriş doğrulamasını etkinleştirmek için gereken desteği uygulayacağız.</span><span class="sxs-lookup"><span data-stu-id="19bd9-109">In this section we are going to implement the support necessary to enable input validation within our application.</span></span> <span data-ttu-id="19bd9-110">Veritabanı içeriğimizin her zaman doğru olduğundan ve geçerli olmayan film verilerini girerken son kullanıcılara faydalı hata iletileri sağlamasına emin olacağız.</span><span class="sxs-lookup"><span data-stu-id="19bd9-110">We'll ensure that our database content is always correct, and provide helpful error messages to end users when they try and enter Movie data which is not valid.</span></span> <span data-ttu-id="19bd9-111">Film sınıfına küçük bir doğrulama mantığı ekleyerek başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="19bd9-111">We'll begin by adding a little validation logic to the Movie class.</span></span>

<span data-ttu-id="19bd9-112">Model klasörüne sağ tıklayın ve sınıf Ekle ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="19bd9-112">Right click on the Model folder and select Add Class.</span></span> <span data-ttu-id="19bd9-113">Sınıf filminizi adlandırın.</span><span class="sxs-lookup"><span data-stu-id="19bd9-113">Name your class Movie.</span></span>

<span data-ttu-id="19bd9-114">Daha önce film varlığı modelini oluşturduğumuz, IDE bir film sınıfı oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="19bd9-114">When we created the Movie Entity Model earlier, the IDE created a Movie class.</span></span> <span data-ttu-id="19bd9-115">Aslında, film sınıfının bir bölümü bir dosyada ve başka bir bölümde olabilir.</span><span class="sxs-lookup"><span data-stu-id="19bd9-115">In fact, part of the Movie class can be in one file and part in another.</span></span> <span data-ttu-id="19bd9-116">Buna kısmi bir sınıf denir.</span><span class="sxs-lookup"><span data-stu-id="19bd9-116">This is called a Partial Class.</span></span> <span data-ttu-id="19bd9-117">Film sınıfını başka bir dosyadan genişletecekiz.</span><span class="sxs-lookup"><span data-stu-id="19bd9-117">We're going to extend the Movie class from another file.</span></span>

<span data-ttu-id="19bd9-118">Sisteme doğrulama ipuçları veren bazı özniteliklerle "arkadaş sınıfına" işaret eden kısmi bir film sınıfı oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="19bd9-118">We'll create a partial movie class that points to a "buddy class" with some attributes that will give validation hints to the system.</span></span> <span data-ttu-id="19bd9-119">Başlığı ve fiyatı gerekli olarak işaretleyecek ve ayrıca fiyatın belirli bir aralıkta yer aldığı insist.</span><span class="sxs-lookup"><span data-stu-id="19bd9-119">We'll mark the Title and Price as Required, and also insist that the Price be within a certain range.</span></span> <span data-ttu-id="19bd9-120">Modeller klasörüne sağ tıklayın ve sınıf Ekle ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="19bd9-120">Right click the Models folder and select Add Class.</span></span> <span data-ttu-id="19bd9-121">Sınıf filminizi adlandırın ve Tamam düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="19bd9-121">Name your class Movie and Click the OK button.</span></span> <span data-ttu-id="19bd9-122">Kısmi film sınıfımız şöyle görünür.</span><span class="sxs-lookup"><span data-stu-id="19bd9-122">Here's what our partial Movie class looks like.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part7/samples/sample1.cs)]

<span data-ttu-id="19bd9-123">Uygulamanızı yeniden çalıştırın ve 100 üzerinden fiyata sahip bir filmi girmeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="19bd9-123">Re-Run your application and try to enter a movie with a price over 100.</span></span> <span data-ttu-id="19bd9-124">Formu gönderdikten sonra bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="19bd9-124">You'll get an error after you've submitted the form.</span></span> <span data-ttu-id="19bd9-125">Hata sunucu tarafında yakalanır ve form gönderildikten sonra gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="19bd9-125">The error is caught on the server side and occurs after the Form is POSTed.</span></span> <span data-ttu-id="19bd9-126">ASP.NET MVC 'nin yerleşik HTML yardımcıların hata iletisini görüntülemesi ve metin kutusu öğelerinde ABD için değerleri korumak üzere yeterince akıllı olduğunu fark edin:</span><span class="sxs-lookup"><span data-stu-id="19bd9-126">Notice how ASP.NET MVC's built-in HTML helpers were smart enough to display the error message and maintain the values for us within the textbox elements:</span></span>

<span data-ttu-id="19bd9-127">[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="19bd9-127">[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)</span></span>

<span data-ttu-id="19bd9-128">Bu harika bir işe yarar, ancak kullanıcıya sunucu dahil etmeden önce istemci tarafında, hemen bir şekilde söyleyebildiğimiz için bu iyi bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="19bd9-128">This works great, but it'd be nice if we could tell the user on the client-side, immediately, before the server gets involved.</span></span>

<span data-ttu-id="19bd9-129">JavaScript ile bazı istemci tarafı doğrulanmasını etkinleştirelim.</span><span class="sxs-lookup"><span data-stu-id="19bd9-129">Let's enable some client-side validation with JavaScript.</span></span>

## <a name="adding-client-side-validation"></a><span data-ttu-id="19bd9-130">Istemci tarafı doğrulama ekleme</span><span class="sxs-lookup"><span data-stu-id="19bd9-130">Adding Client-Side Validation</span></span>

<span data-ttu-id="19bd9-131">Film sınıfımızın zaten bazı doğrulama öznitelikleri olduğundan, Create. aspx görünüm şablonumuza birkaç JavaScript dosyası eklememiz ve istemci tarafı doğrulamanın gerçekleşmesini sağlamak için bir kod satırı eklemeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="19bd9-131">Since our Movie class already has some validation attributes, we'll just need to add a few JavaScript files to our Create.aspx View template and add a line of code to enable client-side validation to take place.</span></span>

<span data-ttu-id="19bd9-132">VWD içinden Görünümlerimize/film klasörmize gidip Create. aspx ' i açın.</span><span class="sxs-lookup"><span data-stu-id="19bd9-132">From within VWD go our Views/Movie folder and open up Create.aspx.</span></span>

<span data-ttu-id="19bd9-133">Çözüm Gezgini betikler klasörünü açın ve aşağıdaki üç komut dosyasını &lt;Head&gt; etiketi içinde sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="19bd9-133">Open up the Scripts folder in the Solution Explorer and drag the following three scripts to within the &lt;head&gt; tag.</span></span>

- <span data-ttu-id="19bd9-134">MicrosoftAjax.js</span><span class="sxs-lookup"><span data-stu-id="19bd9-134">MicrosoftAjax.js</span></span>
- <span data-ttu-id="19bd9-135">MicrosoftMvcValidation.js</span><span class="sxs-lookup"><span data-stu-id="19bd9-135">MicrosoftMvcValidation.js</span></span>

<span data-ttu-id="19bd9-136">Bu komut dosyalarının bu sırada görünmesini istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="19bd9-136">You want these script files to appear in this order.</span></span>

[!code-html[Main](getting-started-with-mvc-part7/samples/sample2.html)]

<span data-ttu-id="19bd9-137">Ayrıca, bu tek satırı HTML. BeginForm üzerine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="19bd9-137">Also, add this single line above the Html.BeginForm:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part7/samples/sample3.aspx)]

<span data-ttu-id="19bd9-138">IDE içinde gösterilen kod aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="19bd9-138">Here's the code shown within the IDE.</span></span>

<span data-ttu-id="19bd9-139">[![filmler-Microsoft Visual Web Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="19bd9-139">[![Movies - Microsoft Visual Web Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)</span></span>

<span data-ttu-id="19bd9-140">Uygulamanızı çalıştırın ve/Movies/Create yeniden ziyaret edin ve herhangi bir veri girmeden oluştur ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="19bd9-140">Run your application and visit /Movies/Create again, and click Create without entering any data.</span></span> <span data-ttu-id="19bd9-141">Hata iletileri, sunucu Flash olmadan hemen görünür ve bu, verileri sunucuya geri gönderme ile ilişkilendirdik.</span><span class="sxs-lookup"><span data-stu-id="19bd9-141">The error messages appear immediately without the page flash that we associate with sending data all the way back to the server.</span></span> <span data-ttu-id="19bd9-142">Bunun nedeni, ASP.NET MVC 'nin hem istemcide (JavaScript kullanılarak) hem de sunucusunda girişi doğrulamadır.</span><span class="sxs-lookup"><span data-stu-id="19bd9-142">This is because ASP.NET MVC is now validating the input on both the client (using JavaScript) and on the server.</span></span>

<span data-ttu-id="19bd9-143">[![oluştur-Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="19bd9-143">[![Create - Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)</span></span>

<span data-ttu-id="19bd9-144">Bu iyi bir fikir!</span><span class="sxs-lookup"><span data-stu-id="19bd9-144">This is looking good!</span></span> <span data-ttu-id="19bd9-145">Şimdi veritabanına başka bir sütun ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="19bd9-145">Let's now add one additional column to the database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="19bd9-146">[Önceki](getting-started-with-mvc-part6.md)
> [İleri](getting-started-with-mvc-part8.md)</span><span class="sxs-lookup"><span data-stu-id="19bd9-146">[Previous](getting-started-with-mvc-part6.md)
[Next](getting-started-with-mvc-part8.md)</span></span>
