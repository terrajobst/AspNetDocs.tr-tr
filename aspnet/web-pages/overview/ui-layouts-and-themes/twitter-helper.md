---
uid: web-pages/overview/ui-layouts-and-themes/twitter-helper
title: ASP.NET Web sayfalarıyla Twitter Yardımcısı | Microsoft Docs
author: Rick-Anderson
description: Bu konu ve uygulama, WebMatrix 3 projenize Twitter Yardımcısı eklemeyi gösterir. Twitter yardımcı kodunu içerir ve yardımcı 'nın nasıl çağrılacağını gösterir...
ms.author: riande
ms.date: 11/26/2018
ms.assetid: c1a1244e-b9c8-42e6-a00b-8456a4ec027c
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/twitter-helper
msc.type: authoredcontent
ms.openlocfilehash: 76e32b7c808467a9a87c70017dac02bdb895e1df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638560"
---
# <a name="twitter-helper-with-aspnet-web-pages"></a><span data-ttu-id="59f21-104">ASP.NET Web Sayfaları ile Twitter Yardımcısı</span><span class="sxs-lookup"><span data-stu-id="59f21-104">Twitter Helper with ASP.NET Web Pages</span></span>

<span data-ttu-id="59f21-105">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="59f21-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="59f21-106">Twitter yardımcıları artık kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="59f21-106">Twitter Helpers are obsolete.</span></span> <span data-ttu-id="59f21-107">Twitter 'ın Web siteleri için en son katılım araçları için bkz. [Web siteleri Için Twitter genel bakış](https://developer.twitter.com/en/docs/twitter-for-websites/overview).</span><span class="sxs-lookup"><span data-stu-id="59f21-107">For Twitter's latest engagement tools for websites, see [Twitter for Websites Overview](https://developer.twitter.com/en/docs/twitter-for-websites/overview).</span></span>

> <span data-ttu-id="59f21-108">Bu konu ve uygulama, WebMatrix 3 projenize Twitter Yardımcısı eklemeyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="59f21-108">This topic and application show how to add a Twitter Helper to your WebMatrix 3 project.</span></span> <span data-ttu-id="59f21-109">Twitter yardımcı kodunu içerir ve yardımcı yöntemlerin nasıl çağrılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="59f21-109">It contains the Twitter Helper code and shows how to call the helper methods.</span></span>
> 
> <span data-ttu-id="59f21-110">Twitter. cshtml dosyası için bu kod, Microsoft 'un **Tian Pan** tarafından geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="59f21-110">This code for the Twitter.cshtml file was developed by **Tian Pan** of Microsoft.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="59f21-111">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="59f21-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="59f21-112">ASP.NET Web sayfaları (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="59f21-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="59f21-113">Bu öğretici, ASP.NET Web Pages 2 ile de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="59f21-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="introduction"></a><span data-ttu-id="59f21-114">Giriş</span><span class="sxs-lookup"><span data-stu-id="59f21-114">Introduction</span></span>

<span data-ttu-id="59f21-115">Bu konuda, uygulamanıza Twitter Yardımcısı ekleme ve yardımcı yöntemleri çağırmak için Razor söz dizimi kullanma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="59f21-115">This topic demonstrates how to add a Twitter Helper to your application and use Razor syntax to call the helper methods.</span></span> <span data-ttu-id="59f21-116">Twitter Yardımcısı, uygulamanızdaki Twitter düğmelerini ve pencere öğelerini eklemenizi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="59f21-116">The Twitter Helper makes it easy to incorporate Twitter buttons and widgets in your application.</span></span> <span data-ttu-id="59f21-117">Kullanıcının zaman çizelgesi veya bir diyez etiketi için arama sonuçları gibi bir Twitter pencere öğesini kullanmak için, önce [Twitter 'da pencere öğesini](https://twitter.com/settings/widgets)oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="59f21-117">To use a Twitter widget, such as a user's timeline or the search results for a hashtag, you must first create the [widget on Twitter](https://twitter.com/settings/widgets).</span></span> <span data-ttu-id="59f21-118">Pencere öğesini oluşturduktan sonra bir pencere öğesi kimliği alacaksınız. Pencere öğesini gösteren yardımcı yöntemler çağrılırken bu pencere öğesi kimliğini bir parametre olarak geçirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59f21-118">After creating your widget, you will receive a widget id. You pass this widget id as a parameter when calling the helper methods that show widget.</span></span>

<span data-ttu-id="59f21-119">Bu konu, Twitter API 'sinin 1,1 sürümü için yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="59f21-119">This topic was written for version 1.1 of the Twitter API.</span></span> <span data-ttu-id="59f21-120">Twitter yardımcı kodunu projenize doğrudan ekleyerek Twitter API 'SI değişirse yardımcı kodunu güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59f21-120">By directly adding the Twitter Helper code to your project, you can update the helper code if the Twitter API changes.</span></span>

<span data-ttu-id="59f21-121">WebMatrix 'i yükleme hakkında daha fazla bilgi için bkz. [ASP.NET Web Pages 2-](../getting-started/introducing-aspnet-web-pages-2/getting-started.md)Başlarken.</span><span class="sxs-lookup"><span data-stu-id="59f21-121">For information about installing WebMatrix, see [Introducing ASP.NET Web Pages 2 - Getting Started](../getting-started/introducing-aspnet-web-pages-2/getting-started.md).</span></span>

## <a name="add-twitter-helper-to-your-project"></a><span data-ttu-id="59f21-122">Projenize Twitter Yardımcısı ekleyin</span><span class="sxs-lookup"><span data-stu-id="59f21-122">Add Twitter Helper to your project</span></span>

<span data-ttu-id="59f21-123">Twitter yardımcısını eklemek için, önce projenize **App\_kodu** adlı bir klasör ekleyin.</span><span class="sxs-lookup"><span data-stu-id="59f21-123">To add the Twitter Helper, first, add a folder named **App\_Code** to your project.</span></span> <span data-ttu-id="59f21-124">Daha sonra **Twitter. cshtml**adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="59f21-124">Then, create a file named **Twitter.cshtml**.</span></span>

![App_Code klasörü](twitter-helper/_static/image1.png)

<span data-ttu-id="59f21-126">Twitter. cshtml içindeki varsayılan kodu aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="59f21-126">Replace the default code in Twitter.cshtml with the following code.</span></span>

[!code-cshtml[Main](twitter-helper/samples/sample1.cshtml)]

## <a name="call-twitter-methods-from-your-web-pages"></a><span data-ttu-id="59f21-127">Web sayfalarınıza Twitter yöntemlerini çağırma</span><span class="sxs-lookup"><span data-stu-id="59f21-127">Call Twitter methods from your web pages</span></span>

<span data-ttu-id="59f21-128">Aşağıdaki örnek, projenizdeki bir sayfadan Twitter yardımcı yöntemlerinin nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="59f21-128">The following example shows how to use the Twitter Helper methods from a page in your project.</span></span> <span data-ttu-id="59f21-129">Projenizde, parametre değerlerini gereksinimlerinize uygun değerlerle değiştirmek isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="59f21-129">In your project, you will want to replace the parameter values with values that are relevant to your needs.</span></span> <span data-ttu-id="59f21-130">Yöntemlerin nasıl çalıştığını araştırmak için, belirtilen pencere öğesi kimliklerini kullanabilirsiniz, ancak projeniz için kendi pencere öğelerinizi oluşturmak isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="59f21-130">You can use the provided widget ids to explore how the methods work, but you will want to generate your own widgets for your project.</span></span>

<span data-ttu-id="59f21-131">Aşağıda gösterilen parametrelerin hepsi gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="59f21-131">Not all of the parameters shown below are required.</span></span> <span data-ttu-id="59f21-132">Düğme veya pencere öğesinin nasıl görüntülendiğini özelleştirmek için isteğe bağlı parametreler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="59f21-132">The optional parameters are used to customize how the button or widget is displayed.</span></span> <span data-ttu-id="59f21-133">Örneğin, Izle düğmesi yalnızca Kullanıcı adının izlemesini gerektirir, ancak örnek, izleme sayısının nasıl ekleneceğini ve düğmenin boyutunu ve dilini nasıl belirtdiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="59f21-133">For example, the Follow Button only requires the user name to follow, but the example shows how to include the number of followers, and how specify the size of the button and the language.</span></span>

[!code-html[Main](twitter-helper/samples/sample2.html)]

## <a name="see-the-results"></a><span data-ttu-id="59f21-134">Sonuçları görme</span><span class="sxs-lookup"><span data-stu-id="59f21-134">See the results</span></span>

<span data-ttu-id="59f21-135">Yukarıdaki kod, aşağıdaki düğmeleri ve pencere öğelerini üretir.</span><span class="sxs-lookup"><span data-stu-id="59f21-135">The above code produces the following buttons and widgets.</span></span> <span data-ttu-id="59f21-136">Bu düğmeler ve pencere öğeleri, ekran görüntüleri değil tam işlevseldir.</span><span class="sxs-lookup"><span data-stu-id="59f21-136">These buttons and widgets are fully-functional, not screenshots.</span></span> <span data-ttu-id="59f21-137">Dil parametresi **es**olarak ayarlandığı Için Izle düğmesi İspanyolca olarak görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="59f21-137">The Follow Button is displayed in Spanish because the language parameter was set to **es**.</span></span>

### <a name="follow-button"></a><span data-ttu-id="59f21-138">Takip et düğmesi</span><span class="sxs-lookup"><span data-stu-id="59f21-138">Follow Button</span></span>

<span data-ttu-id="59f21-139">[@aspnetizleyin)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span><span class="sxs-lookup"><span data-stu-id="59f21-139">[Follow @aspnet)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span></span>

### <a name="tweet-button"></a><span data-ttu-id="59f21-140">Tweet düğmesi</span><span class="sxs-lookup"><span data-stu-id="59f21-140">Tweet Button</span></span>

<span data-ttu-id="59f21-141">[Tweet](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span><span class="sxs-lookup"><span data-stu-id="59f21-141">[Tweet](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span></span>

### <a name="user-timeline-profile"></a><span data-ttu-id="59f21-142">Kullanıcı zaman çizelgesi (profil)</span><span class="sxs-lookup"><span data-stu-id="59f21-142">User Timeline (Profile)</span></span>

<span data-ttu-id="59f21-143">[@aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="59f21-143">[Tweets by @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="favorites"></a><span data-ttu-id="59f21-144">Sık Kullanılanlar</span><span class="sxs-lookup"><span data-stu-id="59f21-144">Favorites</span></span>

<span data-ttu-id="59f21-145">[Sık kullanılan @Microsoft](https://twitter.com/Microsoft/favorites)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="59f21-145">[Favorite Tweets by @Microsoft](https://twitter.com/Microsoft/favorites)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="list"></a><span data-ttu-id="59f21-146">List</span><span class="sxs-lookup"><span data-stu-id="59f21-146">List</span></span>

<span data-ttu-id="59f21-147">[@Microsoft/MS\_tüketicisi\_bantların arası şeritler](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="59f21-147">[Tweets from @Microsoft/MS\_Consumer\_Bands](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="search"></a><span data-ttu-id="59f21-148">Ara</span><span class="sxs-lookup"><span data-stu-id="59f21-148">Search</span></span>

<span data-ttu-id="59f21-149">[&quot;#asp .net`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`&quot;hakkında](https://twitter.com/search?q=%23asp.net) daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="59f21-149">[Tweets about &quot;#asp.net&quot;](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>
