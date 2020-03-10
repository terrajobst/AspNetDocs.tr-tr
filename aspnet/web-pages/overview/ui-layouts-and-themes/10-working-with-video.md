---
uid: web-pages/overview/ui-layouts-and-themes/10-working-with-video
title: Videoyu bir ASP.NET Web Pages (Razor) sitesinde görüntüleme | Microsoft Docs
author: Rick-Anderson
description: Bu bölümde Razor söz dizimi sayfası ile ASP.NET Web sayfalarında videonun nasıl görüntüleneceği açıklanmaktadır.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 332fb3da-e2a5-460d-bb90-dd911e1e2c95
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/10-working-with-video
msc.type: authoredcontent
ms.openlocfilehash: 516d46f38ce8910209f4207c474b0404bf012950
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628949"
---
# <a name="displaying-video-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="bf612-103">Videoyu bir ASP.NET Web Pages (Razor) sitesinde görüntüleme</span><span class="sxs-lookup"><span data-stu-id="bf612-103">Displaying Video in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="bf612-104">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="bf612-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="bf612-105">Bu makalede, kullanıcıların sitede depolanan videoları görüntülemesine izin vermek için bir ASP.NET Web Pages (Razor) Web sitesinde video (medya) yürütücüsünün nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="bf612-105">This article explains how to use a video (media) player in an ASP.NET Web Pages (Razor) website to let users view videos that are stored on the site.</span></span> <span data-ttu-id="bf612-106">Razor söz dizimi Web sayfaları ASP.NET, Flash ( *. swf*), Media Player ( *. wmv*) ve Silverlight ( *. xap*) videolarını oynamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="bf612-106">ASP.NET Web Pages with Razor syntax lets you play Flash (*.swf*), Media Player (*.wmv*), and Silverlight (*.xap*) videos.</span></span>
> 
> <span data-ttu-id="bf612-107">Öğrenecekleriniz:</span><span class="sxs-lookup"><span data-stu-id="bf612-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="bf612-108">Video oynatıcı seçme.</span><span class="sxs-lookup"><span data-stu-id="bf612-108">How to choose a video player.</span></span>
> - <span data-ttu-id="bf612-109">Bir Web sayfasına video ekleme.</span><span class="sxs-lookup"><span data-stu-id="bf612-109">How to add video to a web page.</span></span>
> - <span data-ttu-id="bf612-110">Video oynatıcı özniteliklerini ayarlama.</span><span class="sxs-lookup"><span data-stu-id="bf612-110">How to set video player attributes.</span></span>
> 
> <span data-ttu-id="bf612-111">Makalesinde sunulan ASP.NET Razor sayfaları özellikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="bf612-111">These are the ASP.NET Razor pages features introduced in the article:</span></span>
> 
> - <span data-ttu-id="bf612-112">`Video` Yardımcısı.</span><span class="sxs-lookup"><span data-stu-id="bf612-112">The `Video` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="bf612-113">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="bf612-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="bf612-114">ASP.NET Web sayfaları (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="bf612-114">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="bf612-115">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="bf612-115">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="bf612-116">Bu öğretici WebMatrix 3 ile de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bf612-116">This tutorial also works with WebMatrix 3.</span></span>

## <a name="introduction"></a><span data-ttu-id="bf612-117">Giriş</span><span class="sxs-lookup"><span data-stu-id="bf612-117">Introduction</span></span>

<span data-ttu-id="bf612-118">Sitenizde bir video göstermek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf612-118">You might want to display a video on your site.</span></span> <span data-ttu-id="bf612-119">Bunu yapmanın bir yolu, zaten video içeren bir siteye (YouTube gibi) bağlantı kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="bf612-119">One way to do that is to link to a site that already has the video, like YouTube.</span></span> <span data-ttu-id="bf612-120">Bu sitelerden bir videoyu doğrudan kendi sayfalarınıza eklemek istiyorsanız, genellikle siteden HTML biçimlendirmesi alabilir ve ardından sayfanıza kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf612-120">If you want to embed a video from these sites directly in your own pages, you can usually get HTML markup from the site and then copy it into your page.</span></span> <span data-ttu-id="bf612-121">Örneğin, aşağıdaki örnek bir YouTube videosunu nasıl katıştırabileceğinizi göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="bf612-121">For example, the following example shows how to embed a YouTube video:</span></span>

[!code-html[Main](10-working-with-video/samples/sample1.html?highlight=10-14)]

<span data-ttu-id="bf612-122">Kendi web sitenizde (genel video paylaşım sitesinde değil) bir video oynatmak istiyorsanız, buna benzer katıştırılmış biçimlendirme kullanarak doğrudan buna bağlayamazsınız.</span><span class="sxs-lookup"><span data-stu-id="bf612-122">If you want to play a video that's on your own website (not on a public video-sharing site), you can't directly link to it using embedded markup like this.</span></span> <span data-ttu-id="bf612-123">Ancak, bir Medya yürütücüyü doğrudan bir sayfada işleyen `Video` Yardımcısı 'nı kullanarak sitenizdeki videoları oynatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf612-123">However, you can play videos from your site by using the `Video` helper, which renders a media player directly in a page.</span></span>

<a id="Choosing_a_Video_Player"></a>
## <a name="choosing-a-video-player"></a><span data-ttu-id="bf612-124">Video oynatıcı seçme</span><span class="sxs-lookup"><span data-stu-id="bf612-124">Choosing a Video Player</span></span>

<span data-ttu-id="bf612-125">Video dosyaları için çok sayıda biçim vardır ve her biçim genellikle Player 'ı yapılandırmak için farklı bir oyuncu ve farklı bir yol gerektirir.</span><span class="sxs-lookup"><span data-stu-id="bf612-125">There are lots of formats for video files, and each format typically requires a different player and a different way to configure the player.</span></span> <span data-ttu-id="bf612-126">ASP.NET Razor sayfalarında, `Video` Yardımcısı 'nı kullanarak bir Web sayfasında video oynatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf612-126">In ASP.NET Razor pages, you can play a video in a web page using the `Video` helper.</span></span> <span data-ttu-id="bf612-127">`Video` Yardımcısı, bir Web sayfasına video ekleme işlemini basitleştirir, çünkü bu, sayfaya video eklemek için normalde kullanılan `object` ve `embed` HTML öğelerini otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bf612-127">The `Video` helper simplifies the process of embedding videos in a web page because it automatically generates the `object` and `embed` HTML elements that are normally used to add video to the page.</span></span>

<span data-ttu-id="bf612-128">`Video` Yardımcısı aşağıdaki medya oyuncularını destekler:</span><span class="sxs-lookup"><span data-stu-id="bf612-128">The `Video` helper supports the following media players:</span></span>

- <span data-ttu-id="bf612-129">Adobe Flash</span><span class="sxs-lookup"><span data-stu-id="bf612-129">Adobe Flash</span></span>
- <span data-ttu-id="bf612-130">Windows MediaPlayer</span><span class="sxs-lookup"><span data-stu-id="bf612-130">Windows MediaPlayer</span></span>
- <span data-ttu-id="bf612-131">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="bf612-131">Microsoft Silverlight</span></span>

### <a name="the-flash-player"></a><span data-ttu-id="bf612-132">Flash Player</span><span class="sxs-lookup"><span data-stu-id="bf612-132">The Flash Player</span></span>

<span data-ttu-id="bf612-133">`Video` Yardımcısı 'nın `Flash` oynatıcı, Flash videolarını ( *. swf* dosyaları) bir Web sayfasında oynaetmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="bf612-133">The `Flash` player of the `Video` helper let you play Flash videos (*.swf* files) in a web page.</span></span> <span data-ttu-id="bf612-134">En azından, video dosyasının yolunu sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bf612-134">At a minimum, you have to provide a path to the video file.</span></span> <span data-ttu-id="bf612-135">Hiçbir şey belirtmezseniz, Player geçerli Flash sürümü tarafından ayarlanan varsayılan değerleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="bf612-135">If you specify nothing but the path, the player uses default values that are set by the current version of Flash.</span></span> <span data-ttu-id="bf612-136">Tipik varsayılan ayarlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="bf612-136">Typical default settings are:</span></span>

- <span data-ttu-id="bf612-137">Video, varsayılan genişliği ve yüksekliği kullanılarak ve bir arka plan rengi olmadan görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="bf612-137">The video is displayed using its default width and height and without a background color.</span></span>
- <span data-ttu-id="bf612-138">Sayfa yüklendiğinde video otomatik olarak oynatılır.</span><span class="sxs-lookup"><span data-stu-id="bf612-138">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="bf612-139">Video, açıkça durduruluncaya kadar sürekli olarak döngü olur.</span><span class="sxs-lookup"><span data-stu-id="bf612-139">The video loops continuously until it's explicitly stopped.</span></span>
- <span data-ttu-id="bf612-140">Video, belirli bir boyuta sığacak şekilde videoyu kırpmak yerine videonun tamamını gösterecek şekilde ölçeklendirilir.</span><span class="sxs-lookup"><span data-stu-id="bf612-140">The video is scaled to show all of the video, rather than cropping the video to fit a specific size.</span></span>
- <span data-ttu-id="bf612-141">Video bir pencerede oynatılır.</span><span class="sxs-lookup"><span data-stu-id="bf612-141">The video plays in a window.</span></span>

### <a name="the-mediaplayer-player"></a><span data-ttu-id="bf612-142">MediaPlayer yürütücüsü</span><span class="sxs-lookup"><span data-stu-id="bf612-142">The MediaPlayer Player</span></span>

<span data-ttu-id="bf612-143">`Video` yardımcı 'nın `MediaPlayer` oynatıcı, bir Web sayfasında Windows Media videolarını ( *. wmv* dosyaları), Windows Media Audio ( *. wma* dosyaları) ve MP3 ( *. mp3* dosyaları) oynamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="bf612-143">The `MediaPlayer` player of the `Video` helper lets you play Windows Media videos (*.wmv* files), Windows Media audio (*.wma* files), and MP3 (*.mp3* files) in a web page.</span></span> <span data-ttu-id="bf612-144">Yürütülecek medya dosyasının yolunu dahil etmeniz gerekir; diğer tüm parametreler isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="bf612-144">You must include path of the media file to play; all other parameters are optional.</span></span> <span data-ttu-id="bf612-145">Yalnızca bir yol belirtirseniz, oynatıcı şu şekilde geçerli MediaPlayer sürümü tarafından ayarlanan varsayılan ayarları kullanır:</span><span class="sxs-lookup"><span data-stu-id="bf612-145">If you specify only a path, the player uses default settings set by the current version of MediaPlayer, such as:</span></span>

- <span data-ttu-id="bf612-146">Video varsayılan genişliği ve yüksekliği kullanılarak görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="bf612-146">The video is displayed using its default width and height.</span></span>
- <span data-ttu-id="bf612-147">Sayfa yüklendiğinde video otomatik olarak oynatılır.</span><span class="sxs-lookup"><span data-stu-id="bf612-147">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="bf612-148">Video bir kez oynatılır (döngüye almaz).</span><span class="sxs-lookup"><span data-stu-id="bf612-148">The video plays once (it doesn't loop).</span></span>
- <span data-ttu-id="bf612-149">Oynatıcı, Kullanıcı arabirimindeki denetimlerin tam kümesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="bf612-149">The player displays the full set of controls in the user interface.</span></span>
- <span data-ttu-id="bf612-150">Video bir pencerede oynatılır.</span><span class="sxs-lookup"><span data-stu-id="bf612-150">The video plays in a window.</span></span>

### <a name="the-silverlight-player"></a><span data-ttu-id="bf612-151">Silverlight oynatıcı</span><span class="sxs-lookup"><span data-stu-id="bf612-151">The Silverlight Player</span></span>

<span data-ttu-id="bf612-152">`Video` Yardımcısı 'nın `Silverlight` oynatıcı, Windows Media videosunu ( *. wmv* dosyaları), Windows Media Audio ( *. wma* dosyaları) ve MP3 ( *. mp3* dosyaları) oynamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="bf612-152">The `Silverlight` player of the `Video` helper lets you play Windows Media Video (*.wmv* files), Windows Media Audio (*.wma* files), and MP3 (*.mp3* files).</span></span> <span data-ttu-id="bf612-153">Yol parametresini, Silverlight tabanlı bir uygulama paketine ( *. xap* dosyası) işaret etmek üzere ayarlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="bf612-153">You must set the path parameter to point to a Silverlight-based application package (*.xap* file).</span></span> <span data-ttu-id="bf612-154">Genişlik ve yükseklik parametrelerini de ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bf612-154">You also must set the width and height parameters.</span></span> <span data-ttu-id="bf612-155">Diğer tüm parametreler isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="bf612-155">All other parameters are optional.</span></span> <span data-ttu-id="bf612-156">Video için Silverlight Player 'ı kullandığınızda, yalnızca gerekli parametreleri ayarlarsanız, Silverlight Player Videoyu arka plan rengi olmadan görüntüler.</span><span class="sxs-lookup"><span data-stu-id="bf612-156">When you use the Silverlight player for video, if you set only the required parameters, the Silverlight player displays the video without a background color.</span></span>

> [!NOTE]
> <span data-ttu-id="bf612-157">Silverlight 'ı henüz bilmiyorsanız: *. xap* dosyası, bir *. xaml* dosyasındaki düzen yönergelerini, derlemelerde yönetilen kodu ve isteğe bağlı kaynakları içeren sıkıştırılmış bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="bf612-157">In case you don't already know Silverlight: the *.xap* file is a compressed file that contains layout instructions in a *.xaml* file, managed code in assemblies, and optional resources.</span></span> <span data-ttu-id="bf612-158">Visual Studio 'da bir *. xap* dosyasını Silverlight uygulama projesi olarak oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf612-158">You can create a *.xap* file in Visual Studio as a Silverlight application project.</span></span>

<span data-ttu-id="bf612-159">`Silverlight` video oynatıcı, oynatıcı için sağladığınız ayarları ve *. xap* dosyasında belirtilen ayarları kullanır.</span><span class="sxs-lookup"><span data-stu-id="bf612-159">The `Silverlight` video player uses both the settings that you provide for the player and the settings that are provided in the *.xap* file.</span></span>

> [!TIP] 
> 
> <a id="SB_MimeTypes"></a>
> ### <a name="mime-types"></a><span data-ttu-id="bf612-160">MIME türleri</span><span class="sxs-lookup"><span data-stu-id="bf612-160">MIME Types</span></span>
> 
> <span data-ttu-id="bf612-161">Tarayıcı bir dosyayı indirdiğinde, tarayıcı dosya türünün işlenen belge için belirtilen MIME türüyle eşleştiğinden emin olur.</span><span class="sxs-lookup"><span data-stu-id="bf612-161">When a browser downloads a file, the browser makes sure that the file type matches the MIME type that's specified for the document that's being rendered.</span></span> <span data-ttu-id="bf612-162">MIME türü, bir dosyanın içerik türü veya ortam türüdür.</span><span class="sxs-lookup"><span data-stu-id="bf612-162">The MIME type is the content type or media type of a file.</span></span> <span data-ttu-id="bf612-163">`Video` Yardımcısı aşağıdaki MIME türlerini kullanır:</span><span class="sxs-lookup"><span data-stu-id="bf612-163">The `Video` helper uses the following MIME types:</span></span>
> 
> - `application/x-shockwave-flash`
> - `application/x-mplayer2`
> - `application/x-silverlight-2`

<a id="Playing_Flash"></a>
## <a name="playing-flash-swf-videos"></a><span data-ttu-id="bf612-164">Flash (. swf) videoları oynama</span><span class="sxs-lookup"><span data-stu-id="bf612-164">Playing Flash (.swf) Videos</span></span>

<span data-ttu-id="bf612-165">Bu yordam, *Sample. swf*adlı bir Flash videonun nasıl çalındığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="bf612-165">This procedure shows you how to play a Flash video named *sample.swf*.</span></span> <span data-ttu-id="bf612-166">Yordamda, sitenizde *medya* adlı bir klasör olduğunu ve *. swf* dosyasının bu klasörde olduğunu varsaymış olursunuz.</span><span class="sxs-lookup"><span data-stu-id="bf612-166">The procedure assumes that you've got a folder named *Media* on your site and that the *.swf* file is in that folder.</span></span>

1. <span data-ttu-id="bf612-167">ASP.NET Web yardımcıları kitaplığını, daha önce eklemediyseniz [bir ASP.NET Web sayfaları sitesine yardımcılar yükleme](https://go.microsoft.com/fwlink/?LinkId=252372)başlığı altında açıklandığı gibi Web sitenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bf612-167">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="bf612-168">Web sitesinde bir sayfa ekleyin ve bunu *FlashVideo. cshtml*olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="bf612-168">In the website, add a page and name it *FlashVideo.cshtml*.</span></span>
3. <span data-ttu-id="bf612-169">Aşağıdaki biçimlendirmeyi sayfaya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bf612-169">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample2.cshtml)]
4. <span data-ttu-id="bf612-170">Sayfayı bir tarayıcıda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bf612-170">Run the page in a browser.</span></span> <span data-ttu-id="bf612-171">(Çalıştırmadan önce sayfanın **dosyalar** çalışma alanında seçili olduğundan emin olun.) Sayfa görüntülenir ve video otomatik olarak oynatılır.</span><span class="sxs-lookup"><span data-stu-id="bf612-171">(Make sure the page is selected in the **Files** workspace before you run it.) The page is displayed and the video plays automatically.</span></span> 

    <span data-ttu-id="bf612-172">![görüntüyle](10-working-with-video/_static/image1.jpg "ch08_video -1. jpg")</span><span class="sxs-lookup"><span data-stu-id="bf612-172">![[image]](10-working-with-video/_static/image1.jpg "ch08_video-1.jpg")</span></span>

<span data-ttu-id="bf612-173">Bir Flash videonun `quality` parametresini `low`, `autolow`, `autohigh`, `medium`, `high`ve `best`olarak ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bf612-173">You can set the `quality` parameter for a Flash video to `low`, `autolow`, `autohigh`, `medium`, `high`, and `best`:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample3.cshtml)]

<span data-ttu-id="bf612-174">Aşağıdaki şekilde ayarlayabileceğiniz `scale` parametresini kullanarak, Flash videosunu belirli bir boyutta yürütmeye dönüştürebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bf612-174">You can change the Flash video to play at a specific size using the `scale` parameter, which you can set to the following:</span></span>

- <span data-ttu-id="bf612-175">`showall`.</span><span class="sxs-lookup"><span data-stu-id="bf612-175">`showall`.</span></span> <span data-ttu-id="bf612-176">Bu, orijinal en boy oranını koruyarak videonun tamamının görünmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="bf612-176">This makes the entire video visible while maintaining the original aspect ratio.</span></span> <span data-ttu-id="bf612-177">Bununla birlikte, her bir taraftaki kenarlıkların üzerine çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="bf612-177">However, you might end up with borders on each side.</span></span>
- <span data-ttu-id="bf612-178">`noorder`.</span><span class="sxs-lookup"><span data-stu-id="bf612-178">`noorder`.</span></span> <span data-ttu-id="bf612-179">Bu, özgün en boy oranını koruyarak videoyu ölçeklendirir, ancak kırpılmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="bf612-179">This scales the video while maintaining the original aspect ratio, but it might be cropped.</span></span>
- <span data-ttu-id="bf612-180">`exactfit`.</span><span class="sxs-lookup"><span data-stu-id="bf612-180">`exactfit`.</span></span> <span data-ttu-id="bf612-181">Bu, özgün en boy oranını korumadan videonun tamamını görünür hale getirir, ancak deformasyon meydana gelebilir.</span><span class="sxs-lookup"><span data-stu-id="bf612-181">This makes the entire video visible without preserving the original aspect ratio, but distortion may occur.</span></span>

<span data-ttu-id="bf612-182">Bir `scale` parametresi belirtmezseniz, videonun tamamı görünür olur ve özgün en boy oranı herhangi bir kırpma olmadan korunur.</span><span class="sxs-lookup"><span data-stu-id="bf612-182">If you don't specify a `scale` parameter, the entire video will be visible and the original aspect ratio will be maintained without any cropping.</span></span> <span data-ttu-id="bf612-183">Aşağıdaki örnek `scale` parametrenin nasıl kullanılacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="bf612-183">The following example shows how to use the `scale` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample4.cshtml)]

<span data-ttu-id="bf612-184">Flash Player, `windowMode`adlı bir video modu ayarını destekler.</span><span class="sxs-lookup"><span data-stu-id="bf612-184">The Flash player supports a video mode setting named `windowMode`.</span></span> <span data-ttu-id="bf612-185">Bunu `window`, `opaque`ve `transparent`olarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf612-185">You can set this to `window`, `opaque`, and `transparent`.</span></span> <span data-ttu-id="bf612-186">Varsayılan olarak `windowMode`, videoyu web sayfasındaki ayrı bir pencerede görüntüleyen `window`olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="bf612-186">By default, the `windowMode` is set to `window`, which displays the video in a separate window on the web page.</span></span> <span data-ttu-id="bf612-187">`opaque` ayarı, Web sayfasındaki videonun arkasındaki her şeyi gizler.</span><span class="sxs-lookup"><span data-stu-id="bf612-187">The `opaque` setting hides everything behind the video on the web page.</span></span> <span data-ttu-id="bf612-188">`transparent` ayarı, Web sayfasının arka planının videoda görünmesini sağlar ve videonun herhangi bir kısmının saydam olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="bf612-188">The `transparent` setting lets the background of the web page show through the video, assuming any part of the video is transparent.</span></span>

<a id="Playing_MediaPlayer"></a>
## <a name="playing-mediaplayer-wmv-videos"></a><span data-ttu-id="bf612-189">MediaPlayer ( *. wmv*) videoları oynama</span><span class="sxs-lookup"><span data-stu-id="bf612-189">Playing MediaPlayer (*.wmv*) Videos</span></span>

<span data-ttu-id="bf612-190">Aşağıdaki yordamda, *Media* klasöründe *örnek. wmv* adlı bir pencere medya videosunu nasıl oynatacak gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="bf612-190">The following procedure shows you how to play a Window Media video named *sample.wmv* that's in the *Media* folder.</span></span>

1. <span data-ttu-id="bf612-191">Henüz yapmadıysanız, [bir ASP.NET Web sayfaları sitesine yardımcılar yükleme](https://go.microsoft.com/fwlink/?LinkId=252372)bölümünde açıklandığı gibi, ASP.NET Web yardımcıları kitaplığı 'nı Web sitenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bf612-191">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="bf612-192">*MediaPlayerVideo. cshtml*adlı yeni bir sayfa oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bf612-192">Create a new page named *MediaPlayerVideo.cshtml*.</span></span>
3. <span data-ttu-id="bf612-193">Aşağıdaki biçimlendirmeyi sayfaya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bf612-193">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample5.cshtml)]
4. <span data-ttu-id="bf612-194">Sayfayı bir tarayıcıda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bf612-194">Run the page in a browser.</span></span> <span data-ttu-id="bf612-195">Video otomatik olarak yüklenir ve oynatılır.</span><span class="sxs-lookup"><span data-stu-id="bf612-195">The video loads and plays automatically.</span></span> 

    <span data-ttu-id="bf612-196">![görüntüyle](10-working-with-video/_static/image2.jpg "ch08_video -2. jpg")</span><span class="sxs-lookup"><span data-stu-id="bf612-196">![[image]](10-working-with-video/_static/image2.jpg "ch08_video-2.jpg")</span></span>

<span data-ttu-id="bf612-197">Videonun otomatik olarak kaç kez çalındığını belirten bir tamsayıya `playCount` ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bf612-197">You can set `playCount` to an integer that indicates how many times to play the video automatically:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample6.cshtml)]

<span data-ttu-id="bf612-198">`uiMode` parametresi, Kullanıcı arabiriminde hangi denetimlerin gösterileceğini belirtmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="bf612-198">The `uiMode` parameter lets you specify which controls show up in the user interface.</span></span> <span data-ttu-id="bf612-199">`uiMode` `invisible`, `none`, `mini`veya `full`olarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf612-199">You can set `uiMode` to `invisible`, `none`, `mini`, or `full`.</span></span> <span data-ttu-id="bf612-200">Bir `uiMode` parametresi belirtmezseniz, video, ekran penceresine ek olarak durum penceresi, arama çubuğu, denetim düğmeleri ve ses denetimleriyle birlikte görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="bf612-200">If you don't specify a `uiMode` parameter, the video will be displayed with the status window, seek bar, control buttons, and volume controls in addition to the video window.</span></span> <span data-ttu-id="bf612-201">Bu denetimler, Player 'ı bir ses dosyası çalmak için kullanıyorsanız de görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="bf612-201">These controls will also be displayed if you use the player to play an audio file.</span></span> <span data-ttu-id="bf612-202">`uiMode` parametresinin nasıl kullanılacağına ilişkin bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="bf612-202">Here's an example of how to use the `uiMode` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample7.cshtml)]

<span data-ttu-id="bf612-203">Varsayılan olarak, video oynatılırken ses açık olur.</span><span class="sxs-lookup"><span data-stu-id="bf612-203">By default, audio is on when the video plays.</span></span> <span data-ttu-id="bf612-204">`mute` parametresini true olarak ayarlayarak sesin sesini kapatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bf612-204">You can mute the audio by setting the `mute` parameter to true:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample8.cshtml)]

<span data-ttu-id="bf612-205">`volume` parametresini 0 ile 100 arasında bir değere ayarlayarak MediaPlayer videosunun ses düzeyini kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf612-205">You can control the audio level of the MediaPlayer video by setting the `volume` parameter to a value between 0 and 100.</span></span> <span data-ttu-id="bf612-206">Varsayılan değer 50 ' dir.</span><span class="sxs-lookup"><span data-stu-id="bf612-206">The default value is 50.</span></span> <span data-ttu-id="bf612-207">Örnek buradadır:</span><span class="sxs-lookup"><span data-stu-id="bf612-207">Here's an example:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample9.cshtml)]

<a id="Playing_Silverlight"></a>
## <a name="playing-silverlight-videos"></a><span data-ttu-id="bf612-208">Silverlight videoları oynama</span><span class="sxs-lookup"><span data-stu-id="bf612-208">Playing Silverlight Videos</span></span>

<span data-ttu-id="bf612-209">Bu yordam, *medya*adlı bir klasörde bulunan Silverlight *. xap* sayfasında bulunan videonun nasıl çalındığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="bf612-209">This procedure shows you how to play video contained in a Silverlight *.xap* page that's in a folder named *Media*.</span></span>

1. <span data-ttu-id="bf612-210">Henüz yapmadıysanız, [bir ASP.NET Web sayfaları sitesine yardımcılar yükleme](https://go.microsoft.com/fwlink/?LinkId=252372)bölümünde açıklandığı gibi, ASP.NET Web yardımcıları kitaplığı 'nı Web sitenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bf612-210">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already .</span></span>
2. <span data-ttu-id="bf612-211">*SilverlightVideo. cshtml*adlı yeni bir sayfa oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bf612-211">Create a new page named *SilverlightVideo.cshtml*.</span></span>
3. <span data-ttu-id="bf612-212">Aşağıdaki biçimlendirmeyi sayfaya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bf612-212">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample10.cshtml)]
4. <span data-ttu-id="bf612-213">Sayfayı bir tarayıcıda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bf612-213">Run the page in a browser.</span></span> 

    <span data-ttu-id="bf612-214">![görüntüyle](10-working-with-video/_static/image3.jpg "ch08_video -3. jpg")</span><span class="sxs-lookup"><span data-stu-id="bf612-214">![[image]](10-working-with-video/_static/image3.jpg "ch08_video-3.jpg")</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="bf612-215">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="bf612-215">Additional Resources</span></span>

<span data-ttu-id="bf612-216">[Silverlight genel bakış](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)</span><span class="sxs-lookup"><span data-stu-id="bf612-216">[Silverlight Overview](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)</span></span>

[<span data-ttu-id="bf612-217">Flash NESNESI ve ekleme etiketi öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="bf612-217">Flash OBJECT and EMBED tag attributes</span></span>](http://kb2.adobe.com/cps/127/tn_12701.html)

<span data-ttu-id="bf612-218">[Windows Media Player 11 SDK PARAM etiketleri](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="bf612-218">[Windows Media Player 11 SDK PARAM Tags](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)</span></span>
