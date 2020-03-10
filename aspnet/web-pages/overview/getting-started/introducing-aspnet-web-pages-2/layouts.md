---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
title: ASP.NET Web sayfalarına giriş-tutarlı bir düzen oluşturma | Microsoft Docs
author: Rick-Anderson
description: Bu öğreticide, ASP.NET Web sayfaları kullanan bir sitedeki Sayfalar için tutarlı bir görünüm oluşturmak üzere mizanpajları nasıl kullanabileceğiniz gösterilmektedir. Bunu tamamladığınızı varsaymaktadır...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: c85ec591-f8d7-4882-b763-de6ab9f3df7a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
msc.type: authoredcontent
ms.openlocfilehash: 678eb7089e95e3d221d6b2d82034a62aefa75757
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78526693"
---
# <a name="introducing-aspnet-web-pages---creating-a-consistent-layout"></a><span data-ttu-id="bd774-104">ASP.NET Web sayfalarına giriş-tutarlı bir düzen oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd774-104">Introducing ASP.NET Web Pages - Creating a Consistent Layout</span></span>

<span data-ttu-id="bd774-105">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="bd774-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="bd774-106">Bu öğreticide, ASP.NET Web sayfaları kullanan bir sitedeki Sayfalar için tutarlı bir görünüm oluşturmak üzere *mizanpajları* nasıl kullanabileceğiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="bd774-106">This tutorial shows you how to use *layouts* to create a consistent look for the pages on a site that uses ASP.NET Web Pages.</span></span> <span data-ttu-id="bd774-107">[ASP.NET Web sayfalarındaki veritabanı verilerini silerek](https://go.microsoft.com/fwlink/?LinkId=251584)seriyi tamamladığınız varsayılır.</span><span class="sxs-lookup"><span data-stu-id="bd774-107">It assumes you have completed the series through [Deleting Database Data in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251584).</span></span>
> 
> <span data-ttu-id="bd774-108">Öğrenecekleriniz:</span><span class="sxs-lookup"><span data-stu-id="bd774-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="bd774-109">Düzen sayfası ne olur?</span><span class="sxs-lookup"><span data-stu-id="bd774-109">What a layout page is.</span></span>
> - <span data-ttu-id="bd774-110">Düzen sayfalarını dinamik içerikle birleştirme.</span><span class="sxs-lookup"><span data-stu-id="bd774-110">How to combine layout pages with dynamic content.</span></span>
> - <span data-ttu-id="bd774-111">Değerleri bir düzen sayfasına geçirme.</span><span class="sxs-lookup"><span data-stu-id="bd774-111">How to pass values to a layout page.</span></span>

## <a name="about-layouts"></a><span data-ttu-id="bd774-112">Düzenler hakkında</span><span class="sxs-lookup"><span data-stu-id="bd774-112">About Layouts</span></span>

<span data-ttu-id="bd774-113">Şimdiye kadar oluşturduğunuz sayfaların hepsi, tek başına sayfaları tamamlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="bd774-113">The pages you've created so far have all been complete, standalone pages.</span></span> <span data-ttu-id="bd774-114">Hepsi aynı siteye aittir, ancak ortak bir öğe veya standart görünüm içermez.</span><span class="sxs-lookup"><span data-stu-id="bd774-114">They all belong to the same site, but they don't have any common elements or a standard look.</span></span>

<span data-ttu-id="bd774-115">Çoğu sitede tutarlı bir görünüm ve düzen vardır.</span><span class="sxs-lookup"><span data-stu-id="bd774-115">Most sites do have a consistent look and layout.</span></span> <span data-ttu-id="bd774-116">Örneğin, [Microsoft.com/Web](https://www.microsoft.com/web/) sitesine giderseniz ve sonra da sayfaların tümünün bir genel düzene ve görsel temaya bağlı olduğunu görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="bd774-116">For example, if you go to the [Microsoft.com/web](https://www.microsoft.com/web/) site and look around, you see that the pages all adhere to an overall layout and to a visual theme:</span></span>

![Üstbilginin, gezinti alanının, içerik alanının ve altbilginin yerleşimini gösteren Microsoft.com/web site sayfası](layouts/_static/image1.png)

<span data-ttu-id="bd774-118">Bu düzeni oluşturmanın *verimsiz* bir yolu, sayfalarınızın her birinde ayrı bir üst bilgi, gezinti çubuğu ve alt bilgi tanımlamak olacaktır.</span><span class="sxs-lookup"><span data-stu-id="bd774-118">An *inefficient* way to create this layout would be to define a header, navigation bar, and footer separately on each of your pages.</span></span> <span data-ttu-id="bd774-119">Her seferinde aynı biçimlendirmeyi çoğaltmaktan olursunuz.</span><span class="sxs-lookup"><span data-stu-id="bd774-119">You'd be duplicating the same markup each time.</span></span> <span data-ttu-id="bd774-120">Bir şeyi değiştirmek isterseniz (örneğin, alt bilgiyi güncelleştirmek), her bir sayfayı ayrı olarak değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd774-120">If you wanted to change something (for example, update the footer), you'd have to change each page separately.</span></span>

<span data-ttu-id="bd774-121">Bu, *Düzen sayfalarının* geldiği yerdir.</span><span class="sxs-lookup"><span data-stu-id="bd774-121">That's where *layout pages* come in.</span></span> <span data-ttu-id="bd774-122">ASP.NET Web sayfalarında, sitenizdeki sayfalar için genel bir kapsayıcı sağlayan bir düzen sayfası tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd774-122">In ASP.NET Web Pages, you can define a layout page that provides an overall container for pages on your site.</span></span> <span data-ttu-id="bd774-123">Örneğin, Düzen sayfası üstbilgiyi, gezinti alanını ve altbilgiyi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="bd774-123">For example, the layout page can contain the header, navigation area, and footer.</span></span> <span data-ttu-id="bd774-124">Düzen sayfası, ana içeriğin gittiği bir yer tutucu içerir.</span><span class="sxs-lookup"><span data-stu-id="bd774-124">The layout page includes a placeholder where the main content goes.</span></span>

<span data-ttu-id="bd774-125">Daha sonra, yalnızca bu sayfa için biçimlendirmeyi ve kodu içeren bireysel içerik sayfalarını tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd774-125">You can then define individual content pages that contain the markup and the code for only that page.</span></span> <span data-ttu-id="bd774-126">İçerik sayfalarının HTML sayfalarının tamamı olması gerekmez; `<body>` bir öğesi olması bile gerekmez.</span><span class="sxs-lookup"><span data-stu-id="bd774-126">Content pages don't have to be complete HTML pages; they don't even have to have a `<body>` element.</span></span> <span data-ttu-id="bd774-127">Ayrıca, ASP.NET içeriğini hangi düzen sayfasına göstermek istediğinizi söyleyen bir kod satırı da vardır.</span><span class="sxs-lookup"><span data-stu-id="bd774-127">They also have a line of code that tells ASP.NET what layout page you want to display the content in.</span></span> <span data-ttu-id="bd774-128">Bu ilişkinin nasıl çalıştığını kabaca gösteren bir resim aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="bd774-128">Here's a picture that shows roughly how this relationship works:</span></span>

![İki içerik sayfası ve bu sayfaların sığması için bir düzen sayfası gösteren kavramsal diyagram](layouts/_static/image2.png)

<span data-ttu-id="bd774-130">Bu etkileşim, işlem sırasında gördüğünüz zaman anlaşılması kolay bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="bd774-130">This interaction is easy to understand when you see it in action.</span></span> <span data-ttu-id="bd774-131">Bu öğreticide, film sayfalarınızı bir düzen kullanacak şekilde değiştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="bd774-131">In this tutorial, you'll change your movies pages to use a layout.</span></span>

## <a name="adding-a-layout-page"></a><span data-ttu-id="bd774-132">Düzen sayfası ekleme</span><span class="sxs-lookup"><span data-stu-id="bd774-132">Adding a Layout Page</span></span>

<span data-ttu-id="bd774-133">Ana içerik için bir üst bilgi, alt bilgi ve bir alanı olan tipik bir sayfa düzeni tanımlayan bir düzen sayfası oluşturarak başlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="bd774-133">You'll start by creating a layout page that defines a typical page layout with a header, footer, and an area for the main content.</span></span> <span data-ttu-id="bd774-134">Webpagesfilmlerini sitesinde, *\_Layout. cshtml*ADLı bir cshtml sayfası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bd774-134">In the WebPagesMovies site, add a CSHTML page named *\_Layout.cshtml*.</span></span>

<span data-ttu-id="bd774-135">Önde gelen alt çizgi (`_`) karakteri önemlidir.</span><span class="sxs-lookup"><span data-stu-id="bd774-135">The leading underscore ( `_` ) character is significant.</span></span> <span data-ttu-id="bd774-136">Bir sayfanın adı alt çizgiyle başlıyorsa, ASP.NET bu sayfayı tarayıcıya doğrudan göndermez.</span><span class="sxs-lookup"><span data-stu-id="bd774-136">If a page's name starts with an underscore, ASP.NET won't directly send that page to the browser.</span></span> <span data-ttu-id="bd774-137">Bu kural, siteniz için gerekli olan, ancak kullanıcıların doğrudan isteyememesi gereken sayfaları tanımlamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="bd774-137">This convention lets you define pages that are required for your site but that users shouldn't be able to request directly.</span></span>

<span data-ttu-id="bd774-138">Sayfadaki içeriği aşağıdaki gibi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="bd774-138">Replace the content in the page with the following:</span></span>

[!code-html[Main](layouts/samples/sample1.html)]

<span data-ttu-id="bd774-139">Görebileceğiniz gibi, bu biçimlendirme yalnızca, sayfada üç bölümü ve üç bölümü tutacak bir `<div>` öğesini tanımlamak için `<div>` öğelerini kullanan HTML 'dir.</span><span class="sxs-lookup"><span data-stu-id="bd774-139">As you can see, this markup is just HTML that uses `<div>` elements to define three sections in the page plus one more `<div>` element to hold the three sections.</span></span> <span data-ttu-id="bd774-140">Alt bilgi, sayfada bu konumdaki geçerli yılı işleyecek Razor kodu: `@DateTime.Now.Year`bir bit içerir.</span><span class="sxs-lookup"><span data-stu-id="bd774-140">The footer contains a bit of Razor code: `@DateTime.Now.Year`, which will render the current year at that location in the page.</span></span>

<span data-ttu-id="bd774-141">*Filmler. css*adlı bir stil sayfasının bağlantısı olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="bd774-141">Notice that there's a link to a style sheet named *Movies.css*.</span></span> <span data-ttu-id="bd774-142">Stil sayfası, öğelerin fiziksel düzeninin ayrıntılarının tanımlanacaktır.</span><span class="sxs-lookup"><span data-stu-id="bd774-142">The style sheet is where the details of the physical layout of the elements will be defined.</span></span> <span data-ttu-id="bd774-143">Bunu bir süre içinde oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="bd774-143">You'll create that in a moment.</span></span>

<span data-ttu-id="bd774-144">Bu *\_Layout. cshtml* sayfasındaki tek olağan dışı özellik `@Render.Body()` satırdır.</span><span class="sxs-lookup"><span data-stu-id="bd774-144">The only unusual feature in this *\_Layout.cshtml* page is the `@Render.Body()` line.</span></span> <span data-ttu-id="bd774-145">Bu düzen başka bir sayfayla birleştirildiğinde içeriğin gideceleceği yer tutucudur.</span><span class="sxs-lookup"><span data-stu-id="bd774-145">That's the placeholder where the content will go when this layout is merged with another page.</span></span>

## <a name="adding-a-css-file"></a><span data-ttu-id="bd774-146">. Css dosyası ekleme</span><span class="sxs-lookup"><span data-stu-id="bd774-146">Adding a .css File</span></span>

<span data-ttu-id="bd774-147">Sayfadaki öğelerin gerçek düzenlemesini (görünüm) tanımlamanın tercih edilen yolu, geçişli stil sayfası (CSS) kuralları kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="bd774-147">The preferred way to define the actual arrangement (that is, appearance) of elements on the page is to use cascading style sheet (CSS) rules.</span></span> <span data-ttu-id="bd774-148">Bu nedenle, yeni düzeniniz için kurallara sahip bir *. css* dosyası oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="bd774-148">So you'll create a *.css* file that has the rules for your new layout.</span></span>

<span data-ttu-id="bd774-149">WebMatrix 'te sitenizin kökünü seçin.</span><span class="sxs-lookup"><span data-stu-id="bd774-149">In WebMatrix, select the root of your site.</span></span> <span data-ttu-id="bd774-150">Ardından şeridin **dosyalar** sekmesinde, **Yeni** düğmesinin altındaki oka ve ardından **Yeni klasör**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd774-150">Then in the **Files** tab of the ribbon, click the arrow under the **New** button and then click **New Folder**.</span></span>

![Şeritte Yeni ' yeni klasör ' seçeneği.](layouts/_static/image3.png)

<span data-ttu-id="bd774-152">Yeni klasör *stillerini*adlandırın.</span><span class="sxs-lookup"><span data-stu-id="bd774-152">Name the new folder *Styles*.</span></span>

![' Styles ' yeni klasörünü adlandırma](layouts/_static/image4.png)

<span data-ttu-id="bd774-154">Yeni *Stiller* klasörünün Içinde, *filmler. css*adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bd774-154">Inside the new *Styles* folder, create a file named *Movies.css*.</span></span>

![Yeni bir filmler. css dosyası oluşturma](layouts/_static/image5.png)

<span data-ttu-id="bd774-156">Yeni *. css* dosyasının içeriğini aşağıdakiler ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="bd774-156">Replace the contents of the new *.css* file with the following:</span></span>

[!code-css[Main](layouts/samples/sample2.css)]

<span data-ttu-id="bd774-157">İki şeyi aklınızda bulundurmanız dışında bu CSS kuralları hakkında çok daha fazla bilgi vermeyiz.</span><span class="sxs-lookup"><span data-stu-id="bd774-157">We won't say much about these CSS rules, except to note two things.</span></span> <span data-ttu-id="bd774-158">Bir tane, yazı tiplerinin ve boyutların ayarlanmasına ek olarak, kuralların üst bilgi, alt bilgi ve ana içerik alanının konumunu oluşturmak için mutlak konumlandırmayı kullanmasına de olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="bd774-158">One is that in addition to setting fonts and sizes, the rules use absolute positioning to establish the location of the header, footer, and main content area.</span></span> <span data-ttu-id="bd774-159">CSS 'ye konumlandırmayı yeni başladıysanız W3Schools sitesinde [CSS konumlandırma](http://www.w3schools.com/css/css_positioning.asp) öğreticisini okuyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd774-159">If you're new to positioning in CSS, you can read the [CSS Positioning](http://www.w3schools.com/css/css_positioning.asp) tutorial at the W3Schools site.</span></span>

<span data-ttu-id="bd774-160">Diğer bir deyişle, en altta, *filmler. cshtml* dosyasında ilk olarak tanımlanmış stil kurallarını kopyaladık.</span><span class="sxs-lookup"><span data-stu-id="bd774-160">The other thing to note is that at the bottom, we've copied the style rules that were originally defined individually in the *Movies.cshtml* file.</span></span> <span data-ttu-id="bd774-161">Bu kurallar, tabloya şeritler ekleyen biçimlendirme `WebGrid` Yardımcısı oluşturmak için [ASP.NET Web Pages öğreticisi kullanılarak verileri görüntüleme](https://go.microsoft.com/fwlink/?LinkId=251580) öğreticisinde kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="bd774-161">These rules were used in the [Introduction to Displaying Data by Using ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251580) tutorial to make the `WebGrid` helper render markup that added stripes to the table.</span></span> <span data-ttu-id="bd774-162">(Stil tanımları için bir *. css* dosyası kullanacaksanız, içindeki tüm site için stil kurallarını da koyabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="bd774-162">(If you're going to use a *.css* file for style definitions, you might as well put the style rules for the whole site in it.)</span></span>

## <a name="updating-the-movies-file-to-use-the-layout"></a><span data-ttu-id="bd774-163">Film dosyasını düzeni kullanmak üzere güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="bd774-163">Updating the Movies File to Use the Layout</span></span>

<span data-ttu-id="bd774-164">Artık yeni düzeni kullanmak için sitenizdeki mevcut dosyaları güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd774-164">Now you can update the existing files in your site to use the new layout.</span></span> <span data-ttu-id="bd774-165">*Filmler. cshtml* dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="bd774-165">Open the *Movies.cshtml* file.</span></span> <span data-ttu-id="bd774-166">En üstte, kodun ilk satırı olarak aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd774-166">At the top, as the first line of code, add the following:</span></span>

[!code-csharp[Main](layouts/samples/sample3.cs)]

<span data-ttu-id="bd774-167">Sayfa artık bu şekilde başlatılır:</span><span class="sxs-lookup"><span data-stu-id="bd774-167">The page now starts out this way:</span></span>

[!code-cshtml[Main](layouts/samples/sample4.cshtml?highlight=2)]

<span data-ttu-id="bd774-168">Bu bir kod satırı, *film* sayfası çalıştırıldığında, onun *\_Layout. cshtml* dosyası ile birleştirildiğini ASP.net söyler.</span><span class="sxs-lookup"><span data-stu-id="bd774-168">This one line of code tells ASP.NET that when the *Movies* page runs, it should be merged with the *\_Layout.cshtml* file.</span></span>

<span data-ttu-id="bd774-169">*Filmler. cshtml* dosyası artık bir düzen sayfası kullandığından, *\_Layout. cshtml* dosyası tarafından ele alınan *filmler. cshtml* sayfasından biçimlendirmeyi kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd774-169">Since the *Movies.cshtml* file now uses a layout page, you can remove the markup from the *Movies.cshtml* page that's taken care of by the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="bd774-170">`<!DOCTYPE>`, `<html>`ve `<body>` etiketleri açıp kapatmak için yararlanın.</span><span class="sxs-lookup"><span data-stu-id="bd774-170">Take out the `<!DOCTYPE>`, `<html>`, and `<body>` opening and closing tags.</span></span> <span data-ttu-id="bd774-171">Artık bir *. css* dosyasında bu kurallara sahip olduğunuz için kılavuzun stil kurallarını içeren tüm `<head>` öğesi ve içeriğini alın.</span><span class="sxs-lookup"><span data-stu-id="bd774-171">Take out the entire `<head>` element and its contents, which includes the style rules for the grid, since you've now got those rules in a *.css* file.</span></span> <span data-ttu-id="bd774-172">Bu sırada, var olan `<h1>` öğesini bir `<h2>` öğesiyle değiştirin; Düzen sayfasında zaten bir `<h1>` öğesidir.</span><span class="sxs-lookup"><span data-stu-id="bd774-172">While you're at it, change the existing `<h1>` element to an `<h2>` element; you have an `<h1>` element in the layout page already.</span></span> <span data-ttu-id="bd774-173">`<h2>` metni "filmleri Listele" olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="bd774-173">Change the `<h2>` text to "List Movies".</span></span>

<span data-ttu-id="bd774-174">Normalde, bu tür değişiklikleri içerik sayfasında yapmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="bd774-174">Normally you wouldn't have to make these sorts of changes in a content page.</span></span> <span data-ttu-id="bd774-175">Sitenizi bir düzen sayfasıyla başlattığınızda, ile başlamak için bu öğeler olmadan içerik sayfaları oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="bd774-175">When you start your site out with a layout page, you create content pages without all these elements to begin with.</span></span> <span data-ttu-id="bd774-176">Bu durumda, tek başına bir sayfayı düzen kullanan bir sayfaya dönüştürüyorsunuz, bu yüzden Temizleme biraz daha vardır.</span><span class="sxs-lookup"><span data-stu-id="bd774-176">In this case, though, you're converting a standalone page to one that uses a layout, so there's a bit of cleanup.</span></span>

<span data-ttu-id="bd774-177">İşiniz bittiğinde, *filmler. cshtml* sayfası aşağıdakine benzer şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="bd774-177">When you're finished, the *Movies.cshtml* page will look like the following:</span></span>

[!code-cshtml[Main](layouts/samples/sample5.cshtml)]

### <a name="testing-the-layout"></a><span data-ttu-id="bd774-178">Düzeni test etme</span><span class="sxs-lookup"><span data-stu-id="bd774-178">Testing the Layout</span></span>

<span data-ttu-id="bd774-179">Artık düzenin neye benzediklerine bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd774-179">Now you can see what the layout looks like.</span></span> <span data-ttu-id="bd774-180">WebMatrix 'te, *filmler. cshtml* sayfasına sağ tıklayın ve **tarayıcıda Başlat**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="bd774-180">In WebMatrix, right-click the *Movies.cshtml* page and select **Launch in browser**.</span></span> <span data-ttu-id="bd774-181">Tarayıcı sayfayı görüntülediğinde bu sayfada şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="bd774-181">When the browser displays the page, it looks like this page:</span></span>

![Düzen kullanılarak işlenen filmler sayfası](layouts/_static/image6.png)

<span data-ttu-id="bd774-183">ASP.NET, filmler. cshtml sayfasının içeriğini `RenderBody` yönteminin olduğu *\_Layout. cshtml* sayfasına birleştirmiştir.</span><span class="sxs-lookup"><span data-stu-id="bd774-183">ASP.NET has merged the content of the Movies.cshtml page into the *\_Layout.cshtml* page right where the `RenderBody` method is.</span></span> <span data-ttu-id="bd774-184">Kuşkusuz *\_Layout. cshtml* sayfası, sayfanın görünümünü tanımlayan bir *. css* dosyasına başvurur.</span><span class="sxs-lookup"><span data-stu-id="bd774-184">And of course the *\_Layout.cshtml* page references a *.css* file that defines the look of the page.</span></span>

## <a name="updating-the-addmovie-page-to-use-the-layout"></a><span data-ttu-id="bd774-185">Düzen kullanmak için AddMovie sayfasını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="bd774-185">Updating the AddMovie Page to Use the Layout</span></span>

<span data-ttu-id="bd774-186">Düzenlerinizin gerçek avantajı, bunları sitenizdeki tüm sayfalar için kullanabilmeniz olabilir.</span><span class="sxs-lookup"><span data-stu-id="bd774-186">The real benefit of layouts is that you can use them for all the pages in your site.</span></span> <span data-ttu-id="bd774-187">*Addmovie. cshtml* sayfasını açın.</span><span class="sxs-lookup"><span data-stu-id="bd774-187">Open the *AddMovie.cshtml* page.</span></span>

<span data-ttu-id="bd774-188">*Addmovie. cshtml* sayfasının, doğrulama hata iletilerinin görünümünü tanımlamak için BAŞLANGıÇTA bazı CSS kurallarına sahip olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bd774-188">You might remember that the *AddMovie.cshtml* page originally had some CSS rules in it to define the look of validation error messages.</span></span> <span data-ttu-id="bd774-189">Siteniz için artık bir *. css* dosyanız olduğundan, bu kuralları *. css* dosyasına taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd774-189">Since you have a *.css* file for your site now, you can move those rules to the *.css* file.</span></span> <span data-ttu-id="bd774-190">Bunları *Addmovie. cshtml* dosyasından kaldırın ve bunları *filmle. css* dosyasının altına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bd774-190">Remove them from the *AddMovie.cshtml* file and add them to the bottom of the *Movies.css* file.</span></span> <span data-ttu-id="bd774-191">Aşağıdaki kuralları taşııyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="bd774-191">You are moving the following rules:</span></span>

[!code-css[Main](layouts/samples/sample6.css)]

<span data-ttu-id="bd774-192">Şimdi de,. cshtml için yaptığınız *Addmovie. cshtml* dosyasında aynı değişiklik türlerini yapın. *cshtml* — `Layout="~/_Layout.cshtml;` ekleyin ve artık gereksiz olan HTML işaretlemesini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="bd774-192">Now make the same sorts of changes in *AddMovie.cshtml* that you did for *Movies.cshtml* — add `Layout="~/_Layout.cshtml;` and remove the HTML markup that's now extraneous.</span></span> <span data-ttu-id="bd774-193">`<h1>` öğesini `<h2>`olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="bd774-193">Change the `<h1>` element to `<h2>`.</span></span> <span data-ttu-id="bd774-194">İşiniz bittiğinde, sayfa şu örneğe benzer şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="bd774-194">When you're done, the page will look like this example:</span></span>

[!code-cshtml[Main](layouts/samples/sample7.cshtml)]

<span data-ttu-id="bd774-195">Sayfayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bd774-195">Run the page.</span></span> <span data-ttu-id="bd774-196">Şimdi şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="bd774-196">Now it looks like this illustration:</span></span>

![' Film ekleme ' sayfası düzen kullanılarak işlendi](layouts/_static/image7.png)

<span data-ttu-id="bd774-198">Sitedeki sayfalarda benzer değişiklikler yapmak istiyorsunuz — *Editmovie. cshtml* ve *deletemovie. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="bd774-198">You want to make similar changes to the pages in the site — *EditMovie.cshtml* and *DeleteMovie.cshtml*.</span></span> <span data-ttu-id="bd774-199">Ancak, bunu yapmadan önce mizanpajda çok daha esnek hale getiren başka bir değişiklik yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd774-199">However, before you do, you can make another change to the layout that makes it a little more flexible.</span></span>

## <a name="passing-title-information-to-the-layout-page"></a><span data-ttu-id="bd774-200">Başlık bilgilerini düzen sayfasına geçirme</span><span class="sxs-lookup"><span data-stu-id="bd774-200">Passing Title Information to the Layout Page</span></span>

<span data-ttu-id="bd774-201">Oluşturduğunuz *\_Layout. cshtml* sayfasının "film Sitem" olarak ayarlanmış bir `<title>` öğesi vardır.</span><span class="sxs-lookup"><span data-stu-id="bd774-201">The *\_Layout.cshtml* page that you created has a `<title>` element that's set to "My Movie Site".</span></span> <span data-ttu-id="bd774-202">Çoğu tarayıcı bu öğenin içeriğini bir sekmede metin olarak görüntüler:</span><span class="sxs-lookup"><span data-stu-id="bd774-202">Most browsers display the content of this element as the text on a tab:</span></span>

![Bir tarayıcı sekmesinde görünen sayfanın &lt;başlığı&gt; öğesi](layouts/_static/image8.png)

<span data-ttu-id="bd774-204">Bu başlık bilgileri geneldir.</span><span class="sxs-lookup"><span data-stu-id="bd774-204">This title information is generic.</span></span> <span data-ttu-id="bd774-205">Başlık metninin geçerli sayfaya daha özgü olmasını istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="bd774-205">Suppose that you want the title text to be more specific to the current page.</span></span> <span data-ttu-id="bd774-206">(Başlık metni, sayfanızın hakkında ne olduğunu belirlemek için arama motorları tarafından da kullanılır.) *Film. cshtml* veya *addmovie. cshtml* gibi bir içerik sayfasından düzen sayfasına bilgi geçirebilir ve sonra bu bilgileri, düzen sayfasının ne yaptığını özelleştirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd774-206">(The title text is also used by search engines to determine what your page is about.) You can pass information from a content page like *Movies.cshtml* or *AddMovie.cshtml* to the layout page, and then use that information to customize what the layout page renders.</span></span>

<span data-ttu-id="bd774-207">*Filmler. cshtml* sayfasını yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="bd774-207">Open the *Movies.cshtml* page again.</span></span> <span data-ttu-id="bd774-208">Üstteki kodda aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd774-208">In the code at the top, add the following line:</span></span>

[!code-csharp[Main](layouts/samples/sample8.cs)]

<span data-ttu-id="bd774-209">`Page` nesnesi tüm *. cshtml* sayfalarında kullanılabilir ve bu amaçla, yani bir sayfa ile düzeni arasında bilgi paylaşmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bd774-209">The `Page` object is available on all *.cshtml* pages and is for this purpose, namely to share information between a page and its layout.</span></span>

<span data-ttu-id="bd774-210">*\_Layout. cshtml* sayfasını açın.</span><span class="sxs-lookup"><span data-stu-id="bd774-210">Open the *\_Layout.cshtml* page.</span></span> <span data-ttu-id="bd774-211">`<title>` öğesini şu biçimlendirme gibi görünecek şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="bd774-211">Change the `<title>` element so that it looks like this markup:</span></span>

[!code-html[Main](layouts/samples/sample9.html)]

<span data-ttu-id="bd774-212">Bu kod, sayfada bu konumda `Page.Title` özelliğindeki her şeyi işler.</span><span class="sxs-lookup"><span data-stu-id="bd774-212">This code renders whatever is in the `Page.Title` property right at that location in the page.</span></span>

<span data-ttu-id="bd774-213">*Filmler. cshtml* sayfasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bd774-213">Run the *Movies.cshtml* page.</span></span> <span data-ttu-id="bd774-214">Bu kez tarayıcı sekmesi `Page.Title`değeri olarak ne geçtiğini gösterir:</span><span class="sxs-lookup"><span data-stu-id="bd774-214">This time the browser tab shows what you passed as the value of `Page.Title`:</span></span>

![Dinamik olarak oluşturulan başlığı gösteren bir tarayıcı sekmesi](layouts/_static/image9.png)

<span data-ttu-id="bd774-216">İsterseniz, sayfa kaynağını tarayıcıda görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="bd774-216">If you want, view the page source in the browser.</span></span> <span data-ttu-id="bd774-217">`<title>` öğesinin `<title>List Movies</title>`olarak işlendiğine bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd774-217">You can see that the `<title>` element is rendered as `<title>List Movies</title>`.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="bd774-218">**Sayfa nesnesi**</span><span class="sxs-lookup"><span data-stu-id="bd774-218">**The Page Object**</span></span>
> 
> <span data-ttu-id="bd774-219">`Page` yararlı bir özelliği dinamik bir nesne — `Title` özelliği sabit veya ayrılmış bir ad değildir.</span><span class="sxs-lookup"><span data-stu-id="bd774-219">A useful feature of `Page` is that it's a dynamic object — the `Title` property is not a fixed or reserved name.</span></span> <span data-ttu-id="bd774-220">`Page` nesnesinin bir değeri için *herhangi* bir ad kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd774-220">You can use *any* name for a value of the `Page` object.</span></span> <span data-ttu-id="bd774-221">Örneğin, `Page.CurrentName` veya `Page.MyPage`adlı bir özellik kullanarak başlığı kolayca geçirtiniz.</span><span class="sxs-lookup"><span data-stu-id="bd774-221">For example, you could as easily have passed the title by using a property named `Page.CurrentName` or `Page.MyPage`.</span></span> <span data-ttu-id="bd774-222">Tek kısıtlama, adının özelliklerin adlandırılması için normal kurallara uymalıdır.</span><span class="sxs-lookup"><span data-stu-id="bd774-222">The only restriction is that the name has to follow the normal rules for what properties can be named.</span></span> <span data-ttu-id="bd774-223">(Örneğin, ad bir boşluk içeremez.)</span><span class="sxs-lookup"><span data-stu-id="bd774-223">(For example, the name can't contain a space.)</span></span>
> 
> <span data-ttu-id="bd774-224">`Page` nesnesini kullanarak istediğiniz sayıda değeri geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd774-224">You can pass any number of values by using the `Page` object.</span></span> <span data-ttu-id="bd774-225">Film bilgilerini düzen sayfasına geçirmek isterseniz, `Page.MovieTitle` ve `Page.Genre` ve `Page.MovieYear`gibi bir değer kullanarak değerleri geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd774-225">If you wanted to pass movie information to the layout page, you could pass values by using something like `Page.MovieTitle` and `Page.Genre` and `Page.MovieYear`.</span></span> <span data-ttu-id="bd774-226">(Veya bilgileri depolamak için oluşturduğunuz diğer adlar.) Tek gereksinim — büyük olasılıkla açık olan — içerik sayfasında ve Düzen sayfasında aynı adları kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd774-226">(Or any other names that you invented to store the information.) The only requirement — which is probably obvious — is that you have to use the same names in the content page and the layout page.</span></span>
> 
> <span data-ttu-id="bd774-227">`Page` nesnesini kullanarak geçirdiğiniz bilgiler, yalnızca Düzen sayfasında görüntülenecek metinle sınırlı değildir.</span><span class="sxs-lookup"><span data-stu-id="bd774-227">The information you pass by using the `Page` object isn't limited to just text to display on the layout page.</span></span> <span data-ttu-id="bd774-228">Düzen sayfasına bir değer geçirebilir ve ardından Düzen sayfasındaki kod, sayfanın bir bölümünün görüntülenip görüntülenmeyeceğini, hangi *CSS* dosyasının kullanılacağını vb. karar vermek için bu değeri kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="bd774-228">You can pass a value to the layout page, and then code in the layout page can use the value to decide whether to display a section of the page, what *.css* file to use, and so on.</span></span> <span data-ttu-id="bd774-229">`Page` nesnesinde geçirdiğiniz değerler, kodda kullandığınız diğer değerler gibidir.</span><span class="sxs-lookup"><span data-stu-id="bd774-229">The values you pass in the `Page` object are like any other values that you use in code.</span></span> <span data-ttu-id="bd774-230">Yalnızca değerler içerik sayfasında olur ve düzen sayfasına geçirilir.</span><span class="sxs-lookup"><span data-stu-id="bd774-230">It's just that the values originate in the content page and are passed to the layout page.</span></span>

<span data-ttu-id="bd774-231">*Addmovie. cshtml* sayfasını açın ve *addmovie. cshtml* sayfası için bir başlık sağlayan kodun en üstüne bir satır ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd774-231">Open the *AddMovie.cshtml* page and add a line to the top of the code that provides a title for the *AddMovie.cshtml* page:</span></span>

[!code-csharp[Main](layouts/samples/sample10.cs)]

<span data-ttu-id="bd774-232">*Addmovie. cshtml* sayfasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bd774-232">Run the *AddMovie.cshtml* page.</span></span> <span data-ttu-id="bd774-233">Yeni başlığı burada görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bd774-233">You see the new title there:</span></span>

![Dinamik olarak oluşturulan ' film ekleme ' başlığını gösteren bir tarayıcı sekmesi](layouts/_static/image10.png)

## <a name="updating-the-remaining-pages-to-use-the-layout"></a><span data-ttu-id="bd774-235">Yerleşimi kullanmak için kalan sayfaları güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="bd774-235">Updating the Remaining Pages to Use the Layout</span></span>

<span data-ttu-id="bd774-236">Artık sitenizdeki diğer sayfaları, yeni düzeni kullanacak şekilde tamamlayabilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd774-236">Now you can finish the remaining pages in your site so that they use the new layout.</span></span> <span data-ttu-id="bd774-237">Sırasıyla *Editmovie. cshtml* ve *deletemovie. cshtml* dosyasını açın ve her birinde aynı değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="bd774-237">Open *EditMovie.cshtml* and *DeleteMovie.cshtml* in turn and make the same changes in each.</span></span>

<span data-ttu-id="bd774-238">Düzen sayfasına bağlanan kod satırını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd774-238">Add the line of code that links to the layout page:</span></span>

[!code-csharp[Main](layouts/samples/sample11.cs)]

<span data-ttu-id="bd774-239">Sayfanın başlığını ayarlamak için bir satır ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd774-239">Add a line to set the title of the page:</span></span>

[!code-csharp[Main](layouts/samples/sample12.cs)]

<span data-ttu-id="bd774-240">veya:</span><span class="sxs-lookup"><span data-stu-id="bd774-240">or:</span></span>

[!code-csharp[Main](layouts/samples/sample13.cs)]

<span data-ttu-id="bd774-241">Tüm gereksiz HTML işaretlemesini kaldır — temel olarak yalnızca `<body>` öğesi içindeki bitleri bırakın (artı en üstteki kod bloğu).</span><span class="sxs-lookup"><span data-stu-id="bd774-241">Remove all the extraneous HTML markup — basically, leave only the bits that are inside the `<body>` element (plus the code block at the top).</span></span>

<span data-ttu-id="bd774-242">`<h1>` öğesini bir `<h2>` öğesi olacak şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="bd774-242">Change the `<h1>` element to be an `<h2>` element.</span></span>

<span data-ttu-id="bd774-243">Bu değişiklikleri yaptığınızda, her birini test edin ve doğru şekilde görüntülendiğinden ve başlığın doğru olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="bd774-243">When you've made these changes, test each and make sure that it's displaying properly and that the title is correct.</span></span>

## <a name="parting-thoughts-about-layout-pages"></a><span data-ttu-id="bd774-244">Düzen sayfaları hakkında düşünce</span><span class="sxs-lookup"><span data-stu-id="bd774-244">Parting Thoughts About Layout Pages</span></span>

<span data-ttu-id="bd774-245">Bu öğreticide, bir *\_Layout. cshtml* sayfası oluşturdunuz ve içeriği başka bir sayfadan birleştirmek için `RenderBody` metodunu kullandınız.</span><span class="sxs-lookup"><span data-stu-id="bd774-245">In this tutorial you created a *\_Layout.cshtml* page and used the `RenderBody` method to merge content from another page.</span></span> <span data-ttu-id="bd774-246">Bu, Web sayfalarında düzenleri kullanmaya yönelik temel bir modeldir.</span><span class="sxs-lookup"><span data-stu-id="bd774-246">That's the basic pattern for using layouts in Web Pages.</span></span>

<span data-ttu-id="bd774-247">Düzen sayfalarında burada kapsamadığımız ek özellikler vardır.</span><span class="sxs-lookup"><span data-stu-id="bd774-247">Layout pages have additional features that we didn't cover here.</span></span> <span data-ttu-id="bd774-248">Örneğin, düzen sayfalarını iç içe geçirebilirsiniz — bir düzen sayfası başka bir başvuruya başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="bd774-248">For example, you can nest layout pages — one layout page can in turn reference another.</span></span> <span data-ttu-id="bd774-249">İç içe yerleştirilmiş düzenler, farklı düzenleri gerektiren bir sitenin alt bölümleri ile çalışıyorsanız yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="bd774-249">Nested layouts can be useful if you're working with subsections of a site that require different layouts.</span></span> <span data-ttu-id="bd774-250">Ayrıca, Düzen sayfasında adlandırılmış bölümleri ayarlamak için ek Yöntemler (örneğin, `RenderSection`) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd774-250">You can also use additional methods (for example, `RenderSection`) to set up named sections in the layout page.</span></span>

<span data-ttu-id="bd774-251">Düzen sayfaları ve *. css* dosyalarının birleşimi güçlüdür.</span><span class="sxs-lookup"><span data-stu-id="bd774-251">The combination of layout pages and *.css* files is powerful.</span></span> <span data-ttu-id="bd774-252">Sonraki öğretici serisinde gördüğünüz gibi, WebMatrix 'te önceden oluşturulmuş işlevselliğe sahip bir site sağlayan bir *şablonu*temel alan bir site oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd774-252">As you'll see in the next tutorial series, in WebMatrix you can create a site based on a *template*, which gives you a site that has prebuilt functionality in it.</span></span> <span data-ttu-id="bd774-253">Şablonlar, harika görünen ve menüler gibi özelliklere sahip siteler oluşturmak için Düzen sayfalarının ve CSS 'nin iyi bir şekilde kullanılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="bd774-253">The templates make good use of layout pages and CSS to create sites that look great and that have features like menus.</span></span> <span data-ttu-id="bd774-254">Aşağıda, düzen sayfaları ve CSS kullanan özellikleri gösteren bir şablonu temel alan bir sitedeki giriş sayfasının ekran görüntüsü verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="bd774-254">Here's a screenshot of the home page from a site based on a template, showing features that use layout pages and CSS:</span></span>

![Üst bilgi, gezinti alanı, içerik alanı, isteğe bağlı bölüm ve oturum açma bağlantıları gösteren WebMatrix site şablonu tarafından oluşturulan düzen](layouts/_static/image11.png)

## <a name="complete-listing-for-movie-page-updated-to-use-a-layout-page"></a><span data-ttu-id="bd774-256">Film sayfası için komple liste (Düzen sayfası kullanmak üzere güncelleştirildi)</span><span class="sxs-lookup"><span data-stu-id="bd774-256">Complete Listing for Movie Page (Updated to Use a Layout Page)</span></span>

[!code-cshtml[Main](layouts/samples/sample14.cshtml)]

## <a name="complete-page-listing-for-add-movie-page-updated-for-layout"></a><span data-ttu-id="bd774-257">Film Ekle sayfası için sayfa listesini tamamlar (düzen için güncelleştirildi)</span><span class="sxs-lookup"><span data-stu-id="bd774-257">Complete Page Listing for Add Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample15.cshtml)]

## <a name="complete-page-listing-for-delete-movie-page-updated-for-layout"></a><span data-ttu-id="bd774-258">Filmi Sil sayfasının sayfa listesini tamamlar (düzen için güncelleştirildi)</span><span class="sxs-lookup"><span data-stu-id="bd774-258">Complete Page Listing for Delete Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample16.cshtml)]

## <a name="complete-page-listing-for-edit-movie-page-updated-for-layout"></a><span data-ttu-id="bd774-259">Filmi Düzenle sayfasının sayfa listesini tamamlar (düzen için güncelleştirildi)</span><span class="sxs-lookup"><span data-stu-id="bd774-259">Complete Page Listing for Edit Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample17.cshtml)]

## <a name="coming-up-next"></a><span data-ttu-id="bd774-260">Sonraki adımda</span><span class="sxs-lookup"><span data-stu-id="bd774-260">Coming Up Next</span></span>

<span data-ttu-id="bd774-261">Bir sonraki öğreticide, herkesin görebilmesi için sitenizi Internet 'Te nasıl yayımlayacağınızı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="bd774-261">In the next tutorial, you'll learn how to publish your site to the Internet so everyone can see it.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bd774-262">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="bd774-262">Additional Resources</span></span>

- <span data-ttu-id="bd774-263">[Tutarlı bir görünüm oluşturma](https://go.microsoft.com/fwlink/?LinkID=202891) — mizanpajlarla çalışma hakkında daha ayrıntılı bilgi sağlayan bir makale.</span><span class="sxs-lookup"><span data-stu-id="bd774-263">[Creating a Consistent Look](https://go.microsoft.com/fwlink/?LinkID=202891) — An article that provides some more detail on working with layouts.</span></span> <span data-ttu-id="bd774-264">Ayrıca, içeriğin bazılarını gösteren veya gizleyen bir düzen sayfasına bir değer geçme işlemini açıklar.</span><span class="sxs-lookup"><span data-stu-id="bd774-264">It also describes how to pass a value to a layout page that shows or hides some of the content.</span></span>
- <span data-ttu-id="bd774-265">[Razor Ile Iç Içe yerleştirilmiş düzen sayfaları](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor) — Mike brind blogları, düzen sayfalarının iç içe geçme bir örneğidir.</span><span class="sxs-lookup"><span data-stu-id="bd774-265">[Nested Layout Pages with Razor](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor) — Mike Brind blogs an example of how to nest layout pages.</span></span> <span data-ttu-id="bd774-266">(Sayfaların indirilmesini içerir.)</span><span class="sxs-lookup"><span data-stu-id="bd774-266">(Includes a download of the pages.)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="bd774-267">[Önceki](deleting-data.md)
> [İleri](publishing.md)</span><span class="sxs-lookup"><span data-stu-id="bd774-267">[Previous](deleting-data.md)
[Next](publishing.md)</span></span>
