---
uid: web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
title: Haritaları bir ASP.NET Web Pages (Razor) sitesinde görüntüleme | Microsoft Docs
author: Rick-Anderson
description: Bu makalede, Bing, Google, MA tarafından sunulan eşleme hizmetlerine bağlı olarak ASP.NET Web Pages (Razor) Web sitesindeki sayfalarda etkileşimli haritalar görüntüleme açıklanmaktadır.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: b5c268dd-ca6a-4562-b94c-a220fcf01f58
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 36f3b753cf312504892872ff54bef49854588990
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638679"
---
# <a name="displaying-maps-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="b7060-103">Haritaları bir ASP.NET Web Pages (Razor) sitesinde görüntüleme</span><span class="sxs-lookup"><span data-stu-id="b7060-103">Displaying Maps in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="b7060-104">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="b7060-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="b7060-105">Bu makalede, ASP.NET Web Pages (Razor) Web sitesindeki sayfalarda, Bing, Google, Map ve Yahoo tarafından sunulan eşleme hizmetlerine bağlı olarak etkileşimli eşlemelerin nasıl görüntüleneceği açıklanır.</span><span class="sxs-lookup"><span data-stu-id="b7060-105">This article explains how to display interactive maps on pages in an ASP.NET Web Pages (Razor) website based on mapping services provided by Bing, Google, MapQuest, and Yahoo.</span></span>
> 
> <span data-ttu-id="b7060-106">Öğrenecekleriniz:</span><span class="sxs-lookup"><span data-stu-id="b7060-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="b7060-107">Bir adrese göre harita oluşturma.</span><span class="sxs-lookup"><span data-stu-id="b7060-107">How to generate a map based on an address.</span></span>
> - <span data-ttu-id="b7060-108">Enlem ve boylam koordinatları temelinde harita oluşturma.</span><span class="sxs-lookup"><span data-stu-id="b7060-108">How to generate a map based on latitude and longitude coordinates.</span></span>
> - <span data-ttu-id="b7060-109">Bing Haritalar Geliştirici hesabını kaydetme ve Bing Haritalar ile kullanmak için bir anahtar alma.</span><span class="sxs-lookup"><span data-stu-id="b7060-109">How to register a Bing Maps Developer Account and get a key to use with Bing Maps.</span></span>
> 
> <span data-ttu-id="b7060-110">Bu, makalesinde sunulan ASP.NET özelliğidir:</span><span class="sxs-lookup"><span data-stu-id="b7060-110">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="b7060-111">`Maps` Yardımcısı.</span><span class="sxs-lookup"><span data-stu-id="b7060-111">The `Maps` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="b7060-112">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="b7060-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="b7060-113">ASP.NET Web sayfaları (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="b7060-113">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="b7060-114">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="b7060-114">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="b7060-115">Bu öğretici WebMatrix 3 ile de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b7060-115">This tutorial also works with WebMatrix 3.</span></span>

<span data-ttu-id="b7060-116">Web sayfalarında, `Maps` Yardımcısı 'nı kullanarak bir sayfada haritaları görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7060-116">In Web Pages, you can display maps on a page by using `Maps` helper.</span></span> <span data-ttu-id="b7060-117">Bir adrese veya boylam ve enlem koordinatlarına göre haritalar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7060-117">You can generate maps based either on an address or on a set of longitude and latitude coordinates.</span></span> <span data-ttu-id="b7060-118">`Maps` sınıfı Bing, Google, Mapınsize ve Yahoo gibi popüler harita altyapılarına çağrı yapmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="b7060-118">The `Maps` class lets you call into popular map engines including Bing, Google, MapQuest, and Yahoo.</span></span>

<span data-ttu-id="b7060-119">Bir sayfaya eşleme eklemek için gereken adımlar, hangi harita altyapılarından bağımsız olarak çağrılacağını göz önüne alınır.</span><span class="sxs-lookup"><span data-stu-id="b7060-119">The steps for adding mapping to a page are the same regardless of which of the map engines you call.</span></span> <span data-ttu-id="b7060-120">Yalnızca Haritayı görüntülemesi için kullanılabilir yöntemler sağlayan bir JavaScript dosya başvurusu eklersiniz ve sonra `Maps` Yardımcısı yöntemlerini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7060-120">You just add a JavaScript file reference that makes available methods to display the map, and then you call methods of the `Maps` helper.</span></span>

<span data-ttu-id="b7060-121">Kullandığınız `Maps` yardımcı yöntemine göre bir harita hizmeti seçersiniz.</span><span class="sxs-lookup"><span data-stu-id="b7060-121">You choose a map service based on which `Maps` helper method you use.</span></span> <span data-ttu-id="b7060-122">Bunlardan herhangi birini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b7060-122">You can use any of these:</span></span>

- `Maps.GetBingHtml`
- `Maps.GetGoogleHtml`
- `Maps.GetYahooHtml`
- `Maps.GetMapQuestHtml`

## <a name="installing-the-pieces-you-need"></a><span data-ttu-id="b7060-123">Ihtiyaç duyduğunuz parçaları yükleme</span><span class="sxs-lookup"><span data-stu-id="b7060-123">Installing the Pieces You Need</span></span>

<span data-ttu-id="b7060-124">Haritaları göstermek için şu parçalara ihtiyacınız vardır:</span><span class="sxs-lookup"><span data-stu-id="b7060-124">To display maps, you need these pieces:</span></span>

- <span data-ttu-id="b7060-125">`Maps` Yardımcısı.</span><span class="sxs-lookup"><span data-stu-id="b7060-125">The `Maps` helper.</span></span> <span data-ttu-id="b7060-126">Bu yardımcı ASP.NET Web yardımcıları kitaplığı sürüm 2 ' dir.</span><span class="sxs-lookup"><span data-stu-id="b7060-126">This helper is in version 2 of the ASP.NET Web Helpers Library.</span></span> <span data-ttu-id="b7060-127">Kitaplığı henüz eklemediyseniz, sitenize bir NuGet paketi olarak yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7060-127">If you haven't already added the library, you can install it in your site as a NuGet package.</span></span> <span data-ttu-id="b7060-128">Ayrıntılar için bkz. [ASP.NET Web Pages sitesinde yardımcıları yükleme](https://go.microsoft.com/fwlink/?LinkId=252372).</span><span class="sxs-lookup"><span data-stu-id="b7060-128">For details, see [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372).</span></span> <span data-ttu-id="b7060-129">(Galeride `microsoft-web-helpers` paketini arayın.)</span><span class="sxs-lookup"><span data-stu-id="b7060-129">(In the Gallery, search for the `microsoft-web-helpers` package.)</span></span>
- <span data-ttu-id="b7060-130">JQuery kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="b7060-130">The jQuery library.</span></span> <span data-ttu-id="b7060-131">Birçok WebMatrix site şablonu, kendi *betik* klasörlerinde jQuery kitaplıklarını zaten içeriyor.</span><span class="sxs-lookup"><span data-stu-id="b7060-131">Several of the WebMatrix site templates already include jQuery libraries in their *Script* folders.</span></span> <span data-ttu-id="b7060-132">Bu kitaplıklara sahip değilseniz, en son jQuery kitaplığını doğrudan [jQuery.org](http://jQuery.org) sitesinden indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7060-132">If you do not have these libraries, you can download the latest jQuery library directly from the [jQuery.org](http://jQuery.org) site.</span></span> <span data-ttu-id="b7060-133">Ya da bir şablon (örneğin, **Başlatıcı site** şablonu) kullanarak yeni bir site oluşturabilir ve ardından bu sitedeki jQuery dosyalarını geçerli sitenize kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7060-133">Or you can create a new site using a template (for example, the **Starter Site** template) and then copy the jQuery files from that site to your current site.</span></span>

<span data-ttu-id="b7060-134">Son olarak, Bing Haritalar 'ı kullanmak istiyorsanız, önce bir (ücretsiz) hesap oluşturmanız ve bir anahtar almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7060-134">Finally, if you want to use Bing maps, you must first create a (free) account and get a key.</span></span> <span data-ttu-id="b7060-135">Bir anahtar almak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="b7060-135">To get a key, follow these steps:</span></span>

1. <span data-ttu-id="b7060-136">[Bing Haritalar Geliştirici hesabında](https://www.microsoft.com/maps/developers/web.aspx)bir hesap oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b7060-136">Create an account on the [Bing Maps Developer Account](https://www.microsoft.com/maps/developers/web.aspx).</span></span> <span data-ttu-id="b7060-137">Bir Microsoft hesabı (Windows Live ID) de olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b7060-137">You must have a Microsoft account (Windows Live ID) as well.</span></span>

    <span data-ttu-id="b7060-138">**Değerlendirme/test**için anahtarı kullanmak istediğinizi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7060-138">You can specify that you want to use the key for **Evaluation/Test**.</span></span> <span data-ttu-id="b7060-139">Kendi bilgisayarınızda WebMatrix ve IIS Express kullanarak eşleme işlevini test ediyorsanız, **site** çalışma alanına gidin ve sitenizin URL 'sini (örneğin `http://localhost:50408`, bağlantı noktası numaranız farklı olsa da) göz önünde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7060-139">If you are testing the mapping function on your own computer using WebMatrix and IIS Express, go the **Site** workspace and note the URL of your site (for example, `http://localhost:50408`, although your port number will probably be different).</span></span> <span data-ttu-id="b7060-140">Kayıt sırasında bu *localhost* adresini site olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7060-140">You can use this *localhost* address as the site when you register.</span></span>
2. <span data-ttu-id="b7060-141">Bir hesap için kaydolduktan sonra Bing Haritalar hesap Merkezi ' ne gidin ve **anahtar oluştur veya görüntüle**' ye tıklayın:</span><span class="sxs-lookup"><span data-stu-id="b7060-141">After you have registered for an account, go to the Bing Maps Account Center and click **Create or view keys**:</span></span>

    ![eşleme-2](displaying-maps-in-an-aspnet-web-pages-site/_static/image1.png)
3. <span data-ttu-id="b7060-143">Bing tarafından oluşturulan anahtarı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b7060-143">Record the key that Bing creates.</span></span>

## <a name="creating-a-map-based-on-an-address-using-google"></a><span data-ttu-id="b7060-144">Bir adrese göre harita oluşturma (Google kullanarak)</span><span class="sxs-lookup"><span data-stu-id="b7060-144">Creating a Map Based on an Address (Using Google)</span></span>

<span data-ttu-id="b7060-145">Aşağıdaki örnek, bir adresi temel alarak Haritayı işleyen bir sayfanın nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b7060-145">The following example shows how to create a page that renders a map based on an address.</span></span> <span data-ttu-id="b7060-146">Bu örnek, Google Maps 'ın nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b7060-146">This example shows how to use Google Maps.</span></span>

1. <span data-ttu-id="b7060-147">Sitenin kökünde *Mapaddress. cshtml* adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b7060-147">Create a file named *MapAddress.cshtml* in the root of the site.</span></span> <span data-ttu-id="b7060-148">Bu sayfa, kendisine geçirdiğiniz bir adresi temel alan bir harita oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b7060-148">This page will generate a map based on an address that you pass to it.</span></span>
2. <span data-ttu-id="b7060-149">Aşağıdaki kodu, var olan içeriğin üzerine yazarak dosyaya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="b7060-149">Copy the following code into the file, overwriting the existing content.</span></span>

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    <span data-ttu-id="b7060-150">Sayfanın aşağıdaki özelliklerine dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="b7060-150">Notice the following features of the page:</span></span>

    - <span data-ttu-id="b7060-151">`<head>` öğesindeki `<script>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="b7060-151">The `<script>` element in the `<head>` element.</span></span> <span data-ttu-id="b7060-152">Örnekte `<script>` öğesi, jQuery kitaplığı, sürüm 1.6.4 'in küçültülmüş (sıkıştırılmış) bir sürümü olan *jQuery-1.6.4. min. js* dosyasına başvurur.</span><span class="sxs-lookup"><span data-stu-id="b7060-152">In the example, the `<script>` element references the *jquery-1.6.4.min.js* file, which is a minified (compressed) version of the jQuery library, version 1.6.4.</span></span> <span data-ttu-id="b7060-153">Başvurunun *. js* dosyasının sitenizin *betikler* klasöründe olduğunu varsaydığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b7060-153">Note that the reference assumes that the *.js* file is in the *Scripts* folder of your site.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="b7060-154">JQuery kitaplığı 'nın farklı bir sürümünü kullanıyorsanız, bu sürüme doğru şekilde işaret ettiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="b7060-154">If you're using a different version of the jQuery library, just make sure that you're pointing to that version correctly.</span></span>
    - <span data-ttu-id="b7060-155">Sayfanın gövdesinde `@Maps.GetGoogleHtml` çağrısı.</span><span class="sxs-lookup"><span data-stu-id="b7060-155">The call to the `@Maps.GetGoogleHtml` in the body of the page.</span></span> <span data-ttu-id="b7060-156">Bir adresi eşlemek için bir adres dizesi geçirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7060-156">To map an address, you must pass an address string.</span></span> <span data-ttu-id="b7060-157">Diğer harita motorları için yöntemler benzer bir şekilde çalışır (`@Maps.GetYahooHtml`, `@Maps.GetMapQuestHtml`).</span><span class="sxs-lookup"><span data-stu-id="b7060-157">The methods for the other map engines work in a similar way (`@Maps.GetYahooHtml`, `@Maps.GetMapQuestHtml`).</span></span>
3. <span data-ttu-id="b7060-158">Sayfayı çalıştırın ve bir adres girin.</span><span class="sxs-lookup"><span data-stu-id="b7060-158">Run the page and enter an address.</span></span> <span data-ttu-id="b7060-159">Sayfada, belirttiğiniz konumu gösteren Google Maps temelinde bir harita görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b7060-159">The page displays a map, based on Google Maps, that shows the location that you specified.</span></span>

     ![eşleme-1](displaying-maps-in-an-aspnet-web-pages-site/_static/image2.png)

## <a name="creating-a-map-based-on-latitude-and-longitude-coordinates-using-bing"></a><span data-ttu-id="b7060-161">Enlem ve boylam koordinatları temelinde harita oluşturma (Bing kullanarak)</span><span class="sxs-lookup"><span data-stu-id="b7060-161">Creating a Map Based on Latitude and Longitude Coordinates (Using Bing)</span></span>

<span data-ttu-id="b7060-162">Bu örnek, koordinatları temel alarak bir haritanın nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b7060-162">This example shows how to create a map based on coordinates.</span></span> <span data-ttu-id="b7060-163">Bu örnek, Bing Haritalar 'ın nasıl kullanılacağını ve Bing anahtarınızı nasıl ekleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="b7060-163">This example shows how to use Bing maps and how to include your Bing key.</span></span> <span data-ttu-id="b7060-164">(Bing anahtar kullanmadan diğer eşleme altyapılarını kullanarak koordinatları temel alan bir harita oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="b7060-164">(You can create a map based on coordinates using the other map engines also, without using a Bing key.)</span></span>

1. <span data-ttu-id="b7060-165">Sitesinin kökünde *Mapkoordinatlar. cshtml* adlı bir dosya oluşturun ve var olan içeriği şu kod ve biçimlendirmeyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b7060-165">Create a file named *MapCoordinates.cshtml* in the root of the site and replace the existing content with the following code and markup:</span></span>

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample2.cshtml)]
2. <span data-ttu-id="b7060-166">`your-key-here`, daha önce oluşturduğunuz Bing Haritalar anahtarıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b7060-166">Replace `your-key-here` with the Bing Maps key that you generated earlier.</span></span>
3. <span data-ttu-id="b7060-167">*Mapkoordinatlar. cshtml* sayfasını çalıştırın, enlem ve boylam koordinatlarını girin ve ardından **haritaya tıklayın!**</span><span class="sxs-lookup"><span data-stu-id="b7060-167">Run the *MapCoordinates.cshtml* page, enter latitude and longitude coordinates, and then click the **Map It!**</span></span> <span data-ttu-id="b7060-168">tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b7060-168">button.</span></span> <span data-ttu-id="b7060-169">(Herhangi bir koordinat bilmiyorsanız, aşağıdakileri deneyin.</span><span class="sxs-lookup"><span data-stu-id="b7060-169">(If you don't know any coordinates, try the following.</span></span> <span data-ttu-id="b7060-170">Bu, Microsoft Redmond kampüs üzerinde bir konumdur.)</span><span class="sxs-lookup"><span data-stu-id="b7060-170">This is a location on the Microsoft Redmond campus.)</span></span>

   - <span data-ttu-id="b7060-171">Enlem: 47.6781005859375</span><span class="sxs-lookup"><span data-stu-id="b7060-171">Latitude: 47.6781005859375</span></span>
   - <span data-ttu-id="b7060-172">Boylam:-122.158317565918</span><span class="sxs-lookup"><span data-stu-id="b7060-172">Longitude: -122.158317565918</span></span>

     <span data-ttu-id="b7060-173">Sayfa, belirttiğiniz koordinatlar kullanılarak görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b7060-173">The page is displayed using the coordinates that you specified.</span></span>

     ![eşleme-3](displaying-maps-in-an-aspnet-web-pages-site/_static/image3.png)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="b7060-175">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b7060-175">Additional Resources</span></span>

[<span data-ttu-id="b7060-176">Microsoft. Maps API başvurusu</span><span class="sxs-lookup"><span data-stu-id="b7060-176">Microsoft.Maps API Reference</span></span>](https://msdn.microsoft.com/library/gg427611.aspx)
