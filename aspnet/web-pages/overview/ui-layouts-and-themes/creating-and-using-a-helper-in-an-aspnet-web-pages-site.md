---
uid: web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
title: ASP.NET Web Pages (Razor) sitesinde yardımcı oluşturma ve kullanma | Microsoft Docs
author: Rick-Anderson
description: Bu makalede, bir ASP.NET Web Pages (Razor) Web sitesinde nasıl yardımcı oluşturulacağı açıklanır. Yardımcı, kod ve perf için biçimlendirme içeren yeniden kullanılabilir bir bileşendir...
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 46bff772-01e0-40f0-9ae6-9e18c5442ee6
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 380663951094c9fc7d5f0601e30995fa073a204b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563513"
---
# <a name="creating-and-using-a-helper-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="81f20-104">ASP.NET Web Pages (Razor) sitesinde yardımcı oluşturma ve kullanma</span><span class="sxs-lookup"><span data-stu-id="81f20-104">Creating and Using a Helper in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="81f20-105">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="81f20-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="81f20-106">Bu makalede, bir ASP.NET Web Pages (Razor) Web sitesinde nasıl yardımcı oluşturulacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="81f20-106">This article describes how to create a helper in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="81f20-107">*Yardımcı* , sıkıcı veya karmaşık olabilecek bir görevi gerçekleştirmek için kod ve biçimlendirme içeren yeniden kullanılabilir bir bileşendir.</span><span class="sxs-lookup"><span data-stu-id="81f20-107">A *helper* is a reusable component that includes code and markup to perform a task that might be tedious or complex.</span></span>
> 
> <span data-ttu-id="81f20-108">**Şunları öğreneceksiniz:**</span><span class="sxs-lookup"><span data-stu-id="81f20-108">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="81f20-109">Basit bir yardımcı oluşturma ve kullanma.</span><span class="sxs-lookup"><span data-stu-id="81f20-109">How to create and use a simple helper.</span></span>
> 
> <span data-ttu-id="81f20-110">Makalesinde sunulan ASP.NET özellikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="81f20-110">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="81f20-111">`@helper` sözdizimi.</span><span class="sxs-lookup"><span data-stu-id="81f20-111">The `@helper` syntax.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="81f20-112">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="81f20-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="81f20-113">ASP.NET Web sayfaları (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="81f20-113">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="81f20-114">Bu öğretici, ASP.NET Web Pages 2 ile de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="81f20-114">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="overview-of-helpers"></a><span data-ttu-id="81f20-115">Yardımcıların Özeti</span><span class="sxs-lookup"><span data-stu-id="81f20-115">Overview of Helpers</span></span>

<span data-ttu-id="81f20-116">Sitenizdeki farklı sayfalarda aynı görevleri gerçekleştirmeniz gerekiyorsa, bir yardımcı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81f20-116">If you need to perform the same tasks on different pages in your site, you can use a helper.</span></span> <span data-ttu-id="81f20-117">ASP.NET Web sayfaları bir dizi yardımcı içerir ve indirebileceğiniz ve yükleyebileceğiniz pek çok daha vardır.</span><span class="sxs-lookup"><span data-stu-id="81f20-117">ASP.NET Web Pages includes a number of helpers, and there are many more that you can download and install.</span></span> <span data-ttu-id="81f20-118">(ASP.NET Web sayfalarındaki yerleşik yardımcılar listesi, [ASP.NET API hızlı başvurusu](https://go.microsoft.com/fwlink/?LinkId=202907)' nda listelenmiştir.) Mevcut yardımcıların hiçbiri gereksinimlerinizi karşılamıyorsa, kendi yardımcınızın oluşturulmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81f20-118">(A list of the built-in helpers in ASP.NET Web Pages is listed in the [ASP.NET API Quick Reference](https://go.microsoft.com/fwlink/?LinkId=202907).) If none of the existing helpers meet your needs, you can create your own helper.</span></span>

<span data-ttu-id="81f20-119">Yardımcı, birden çok sayfada ortak bir kod bloğu kullanmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="81f20-119">A helper lets you use a common block of code across multiple pages.</span></span> <span data-ttu-id="81f20-120">Sayfanızda genellikle normal paragraflardan ayrı olarak ayarlanan bir dekont öğesi oluşturmak istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="81f20-120">Suppose that in your page you often want to create a note item that's set apart from normal paragraphs.</span></span> <span data-ttu-id="81f20-121">Büyük olasılıkla, bir kenarlık içeren bir kutu olarak stillendirilmiş bir `<div>` öğesi olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="81f20-121">Perhaps the note is created as a `<div>` element that's styled as a box with a border.</span></span> <span data-ttu-id="81f20-122">Her bir notun görüntülenmesini istediğiniz her seferinde aynı biçimlendirmeyi bir sayfaya eklemek yerine, biçimlendirmeyi bir yardımcı olarak paketleyebilir.</span><span class="sxs-lookup"><span data-stu-id="81f20-122">Rather than add this same markup to a page every time you want to display a note, you can package the markup as a helper.</span></span> <span data-ttu-id="81f20-123">Daha sonra, tek bir kod satırıyla ihtiyacınız olan her yerde nota ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81f20-123">You can then insert the note with a single line of code anywhere you need it.</span></span>

<span data-ttu-id="81f20-124">Bunun gibi bir yardımcı kullanmak, sayfalarınızın her birinde kodu daha basit ve daha kolay okunabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="81f20-124">Using a helper like this makes the code in each of your pages simpler and easier to read.</span></span> <span data-ttu-id="81f20-125">Ayrıca, notlarınızın nasıl görüneceğini değiştirmeniz gerekiyorsa, biçimlendirmeyi tek bir yerde değiştirebilirsiniz, ancak bu da sitenizin korunmasını kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="81f20-125">It also makes it easier to maintain your site, because if you need to change how the notes look, you can change the markup in one place.</span></span>

## <a name="creating-a-helper"></a><span data-ttu-id="81f20-126">Yardımcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="81f20-126">Creating a Helper</span></span>

<span data-ttu-id="81f20-127">Bu yordam, yalnızca açıklandığı gibi, notun oluşturulduğu yardımcıyı nasıl oluşturacağınız gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="81f20-127">This procedure shows you how to create the helper that creates the note, as just described.</span></span> <span data-ttu-id="81f20-128">Bu basit bir örnektir ancak özel yardımcı, ihtiyacınız olan herhangi bir biçimlendirme ve ASP.NET kodu içerebilir.</span><span class="sxs-lookup"><span data-stu-id="81f20-128">This is a simple example, but the custom helper can include any markup and ASP.NET code that you need.</span></span>

1. <span data-ttu-id="81f20-129">Web sitesinin kök klasöründe, *uygulama\_kodu*adlı bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="81f20-129">In the root folder of the website, create a folder named *App\_Code*.</span></span> <span data-ttu-id="81f20-130">Bu, ASP.NET ' de, yardımcılar gibi bileşenler için kod koyabileceğiniz ayrılmış bir klasör adıdır.</span><span class="sxs-lookup"><span data-stu-id="81f20-130">This is a reserved folder name in ASP.NET where you can put code for components like helpers.</span></span>
2. <span data-ttu-id="81f20-131">*Uygulama\_kodu* klasöründe yeni bir *. cshtml* dosyası oluşturun ve *myyardımcıları. cshtml*olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="81f20-131">In the *App\_Code* folder create a new *.cshtml* file and name it *MyHelpers.cshtml*.</span></span>
3. <span data-ttu-id="81f20-132">Var olan içeriği aşağıdaki ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="81f20-132">Replace the existing content with the following:</span></span>

    [!code-cshtml[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    <span data-ttu-id="81f20-133">Kod, `MakeNote`adlı yeni bir yardımcı bildirmek için `@helper` sözdizimini kullanır.</span><span class="sxs-lookup"><span data-stu-id="81f20-133">The code uses the `@helper` syntax to declare a new helper named `MakeNote`.</span></span> <span data-ttu-id="81f20-134">Bu belirli yardımcı, metin ve biçimlendirme birleşimini içerebilen `content` adlı bir parametreyi geçirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="81f20-134">This particular helper lets you pass a parameter named `content` that can contain a combination of text and markup.</span></span> <span data-ttu-id="81f20-135">Yardımcı, dizeyi `@content` değişkenini kullanarak notun gövdesine ekler.</span><span class="sxs-lookup"><span data-stu-id="81f20-135">The helper inserts the string into the note body using the `@content` variable.</span></span>

    <span data-ttu-id="81f20-136">Dosyanın *myhelper. cshtml*olarak adlandırıldığına, ancak yardımcının `MakeNote`adlandırıldığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="81f20-136">Notice that the file is named *MyHelpers.cshtml*, but the helper is named `MakeNote`.</span></span> <span data-ttu-id="81f20-137">Birden çok özel yardımcıları tek bir dosyaya yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81f20-137">You can put multiple custom helpers into a single file.</span></span>
4. <span data-ttu-id="81f20-138">Dosyayı kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="81f20-138">Save and close the file.</span></span>

## <a name="using-the-helper-in-a-page"></a><span data-ttu-id="81f20-139">Bir sayfada yardımcı kullanma</span><span class="sxs-lookup"><span data-stu-id="81f20-139">Using the Helper in a Page</span></span>

1. <span data-ttu-id="81f20-140">Kök klasörde, *TestHelper. cshtml*adlı yeni bir boş dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="81f20-140">In the root folder, create a new blank file called *TestHelper.cshtml*.</span></span>
2. <span data-ttu-id="81f20-141">Dosyaya aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="81f20-141">Add the following code to the file:</span></span>

    [!code-html[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample2.html)]

    <span data-ttu-id="81f20-142">Oluşturduğunuz yardımcı 'yı çağırmak için, `@` ve ardından yardımcı, bir nokta ve ardından yardımcı adı olan dosya adı ' nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="81f20-142">To call the helper you created, use `@` followed by the file name where the helper is, a dot, and then the helper name.</span></span> <span data-ttu-id="81f20-143">( *App\_Code* klasöründe birden çok klasörünüz varsa, yardımcı uygulamanızı herhangi bir iç içe klasör düzeyinde çağırmak için `@FolderName.FileName.HelperName` sözdizimini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81f20-143">(If you had multiple folders in the *App\_Code* folder, you could use the syntax `@FolderName.FileName.HelperName` to call your helper within any nested folder level).</span></span> <span data-ttu-id="81f20-144">Parantez içinde tırnak işaretleri içine eklediğiniz metin, yardımcının Web sayfasındaki notun bir parçası olarak görüntüleyeceği metindir.</span><span class="sxs-lookup"><span data-stu-id="81f20-144">The text that you add in quotation marks within the parentheses is the text that the helper will display as part of the note in the web page.</span></span>
3. <span data-ttu-id="81f20-145">Sayfayı kaydedin ve bir tarayıcıda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="81f20-145">Save the page and run it in a browser.</span></span> <span data-ttu-id="81f20-146">Yardımcı, iki paragraf arasında Yardımcısı nerede olduğunu doğrudan bir şekilde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="81f20-146">The helper generates the note item right where you called the helper: between the two paragraphs.</span></span>

    ![Tarayıcıdaki sayfanın yanı sıra, belirtilen metnin etrafına bir kutu yerleştiren nasıl yardımcı olan biçimlendirme gösteren ekran görüntüsü.](creating-and-using-a-helper-in-an-aspnet-web-pages-site/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="81f20-148">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="81f20-148">Additional Resources</span></span>

<span data-ttu-id="81f20-149">[Razor Yardımcısı olarak yatay menü](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341).</span><span class="sxs-lookup"><span data-stu-id="81f20-149">[Horizontal menu as a Razor helper](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341).</span></span> <span data-ttu-id="81f20-150">Mike Pope tarafından yapılan bu blog girişi, biçimlendirme, CSS ve kod kullanarak bir yardımcı olarak yatay bir menü oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="81f20-150">This blog entry by Mike Pope shows how to create a horizontal menu as a helper using markup, CSS, and code.</span></span>

<span data-ttu-id="81f20-151">[WebMatrix ve ASP.net mvc3 için ASP.NET Web sayfaları yardımcılarını kullanarak HTML5](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx)'yi kullanma.</span><span class="sxs-lookup"><span data-stu-id="81f20-151">[Leveraging HTML5 in ASP.NET Web Pages Helpers for WebMatrix and ASP.NET MVC3](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx).</span></span> <span data-ttu-id="81f20-152">Sam Abkıham tarafından bu blog girdisi HTML5 `Canvas` öğesi işleyen bir yardımcı gösterir.</span><span class="sxs-lookup"><span data-stu-id="81f20-152">This blog entry by Sam Abraham shows a helper that renders an HTML5 `Canvas` element.</span></span>

<span data-ttu-id="81f20-153">[WebMatrix 'te @Helpers ve @Functions arasındaki fark](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix).</span><span class="sxs-lookup"><span data-stu-id="81f20-153">[The Difference Between @Helpers and @Functions in WebMatrix](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix).</span></span> <span data-ttu-id="81f20-154">Mike Brind tarafından yapılan bu blog girdisi `@helper` sözdizimini ve `@function` sözdizimini ve ne zaman kullanılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="81f20-154">This blog entry by Mike Brind describes `@helper` syntax and `@function` syntax and when to use each.</span></span>
