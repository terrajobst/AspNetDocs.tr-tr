---
ms.openlocfilehash: 3965884c8e0d7116f5d8a42e6aefb0dc5be94f1e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57078123"
---
<a name="open-iconic-v111httpuseiconiccomopen"></a>[<span data-ttu-id="f3ba4-101">İcon v1.1.1 açın</span><span class="sxs-lookup"><span data-stu-id="f3ba4-101">Open Iconic v1.1.1</span></span>](http://useiconic.com/open)
===========

### <a name="open-iconic-is-the-open-source-sibling-of-iconichttpuseiconiccom-it-is-a-hyper-legible-collection-of-223-icons-with-a-tiny-footprintmdashready-to-use-with-bootstrap-and-foundation-view-the-collectionhttpuseiconiccomopenicons"></a><span data-ttu-id="f3ba4-102">Açık Iconic olan açık kaynak eşdüzey [Iconic](http://useiconic.com).</span><span class="sxs-lookup"><span data-stu-id="f3ba4-102">Open Iconic is the open source sibling of [Iconic](http://useiconic.com).</span></span> <span data-ttu-id="f3ba4-103">Küçük ayak 223 simgelerle okunaklı hyper koleksiyonu olan&mdash;Bootstrap ve Foundation ile kullanıma hazır.</span><span class="sxs-lookup"><span data-stu-id="f3ba4-103">It is a hyper-legible collection of 223 icons with a tiny footprint&mdash;ready to use with Bootstrap and Foundation.</span></span> [<span data-ttu-id="f3ba4-104">Koleksiyon görünümü</span><span class="sxs-lookup"><span data-stu-id="f3ba4-104">View the collection</span></span>](http://useiconic.com/open#icons)



## <a name="whats-in-open-iconic"></a><span data-ttu-id="f3ba4-105">Aç'icon nedir?</span><span class="sxs-lookup"><span data-stu-id="f3ba4-105">What's in Open Iconic?</span></span>

* <span data-ttu-id="f3ba4-106">Aşağı 8 piksel okunaklı olacak şekilde tasarlanan 223 simgeleri</span><span class="sxs-lookup"><span data-stu-id="f3ba4-106">223 icons designed to be legible down to 8 pixels</span></span>
* <span data-ttu-id="f3ba4-107">Süper ışık SVG dosyaları - 61.8 tamamını için</span><span class="sxs-lookup"><span data-stu-id="f3ba4-107">Super-light SVG files - 61.8 for the entire set</span></span> 
* <span data-ttu-id="f3ba4-108">SVG sprite&mdash;simgesi yazı tipleri için modern değiştirme</span><span class="sxs-lookup"><span data-stu-id="f3ba4-108">SVG sprite&mdash;the modern replacement for icon fonts</span></span>
* <span data-ttu-id="f3ba4-109">Webfont (EOT, OTF, SVG, fot adı, WOFF), PNG ve WebP biçimleri</span><span class="sxs-lookup"><span data-stu-id="f3ba4-109">Webfont (EOT, OTF, SVG, TTF, WOFF), PNG and WebP formats</span></span>
* <span data-ttu-id="f3ba4-110">(Önyükleme ve Foundation sürümleri dahil) Webfont stil sayfalarını CSS ya da daha az, SCSS ve ekran kalemi biçimleri</span><span class="sxs-lookup"><span data-stu-id="f3ba4-110">Webfont stylesheets (including versions for Bootstrap and Foundation) in CSS, LESS, SCSS and Stylus formats</span></span>
* <span data-ttu-id="f3ba4-111">PNG ve WebP ızgara görüntüleri 8px, 16px, 24px, 32px, 48px ve 64px.</span><span class="sxs-lookup"><span data-stu-id="f3ba4-111">PNG and WebP raster images in 8px, 16px, 24px, 32px, 48px and 64px.</span></span>


## <a name="getting-started"></a><span data-ttu-id="f3ba4-112">Başlarken</span><span class="sxs-lookup"><span data-stu-id="f3ba4-112">Getting Started</span></span>

#### <a name="for-code-samples-and-everything-else-you-need-to-get-started-with-open-iconic-check-out-our-iconshttpuseiconiccomopenicons-and-referencehttpuseiconiccomopenreference-sections"></a><span data-ttu-id="f3ba4-113">Kod örnekleri ve diğer her şey açık icon ile kullanmaya başlamak için ihtiyacınız için kullanıma sunduğumuz [simgeler](http://useiconic.com/open#icons) ve [başvuru](http://useiconic.com/open#reference) bölümler.</span><span class="sxs-lookup"><span data-stu-id="f3ba4-113">For code samples and everything else you need to get started with Open Iconic, check out our [Icons](http://useiconic.com/open#icons) and [Reference](http://useiconic.com/open#reference) sections.</span></span>

### <a name="general-usage"></a><span data-ttu-id="f3ba4-114">Genel kullanım</span><span class="sxs-lookup"><span data-stu-id="f3ba4-114">General Usage</span></span>

#### <a name="using-open-iconics-svgs"></a><span data-ttu-id="f3ba4-115">Açık icon 's SVGs kullanma</span><span class="sxs-lookup"><span data-stu-id="f3ba4-115">Using Open Iconic's SVGs</span></span>

<span data-ttu-id="f3ba4-116">SVGs istiyoruz ve web üzerinde simgelerini görüntülemek için yol oldukları düşünüyoruz.</span><span class="sxs-lookup"><span data-stu-id="f3ba4-116">We like SVGs and we think they're the way to display icons on the web.</span></span> <span data-ttu-id="f3ba4-117">Açık icon olduğundan yalnızca temel SVGs, görüntü bunları başka bir görüntü gibi öneririz (unutmayın `alt` özniteliği).</span><span class="sxs-lookup"><span data-stu-id="f3ba4-117">Since Open Iconic are just basic SVGs, we suggest you display them like you would any other image (don't forget the `alt` attribute).</span></span>

```
<img src="/open-iconic/svg/icon-name.svg" alt="icon name">
```

#### <a name="using-open-iconics-svg-sprite"></a><span data-ttu-id="f3ba4-118">Açık icon 's SVG Sprite kullanma</span><span class="sxs-lookup"><span data-stu-id="f3ba4-118">Using Open Iconic's SVG Sprite</span></span>

<span data-ttu-id="f3ba4-119">Açık Iconic ayrıca tek bir istekle kümesindeki tüm simgeleri göstermek izin veren bir SVG sprite içinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="f3ba4-119">Open Iconic also comes in a SVG sprite which allows you to display all the icons in the set with a single request.</span></span> <span data-ttu-id="f3ba4-120">Bu, bir simge yazı tipi gibi bir korsan olmadan olur.</span><span class="sxs-lookup"><span data-stu-id="f3ba4-120">It's like an icon font, without being a hack.</span></span>

<span data-ttu-id="f3ba4-121">Simge bir SVG ekleme sprite için kullandığınız değerinden biraz farklıdır, ancak hala yazan bir pasta.</span><span class="sxs-lookup"><span data-stu-id="f3ba4-121">Adding an icon from an SVG sprite is a little different than what you're used to, but it's still a piece of cake.</span></span> <span data-ttu-id="f3ba4-122">*İpucu: Simgelerinizi kolayca stil mümkün hale getirmek için genel bir sınıfa eklemeyi önerin* `<svg>` *etiketi ve her farklı simge için bir benzersiz sınıf adı* `<use>` *etiketi.*</span><span class="sxs-lookup"><span data-stu-id="f3ba4-122">*Tip: To make your icons easily style able, we suggest adding a general class to the* `<svg>` *tag and a unique class name for each different icon in the* `<use>` *tag.*</span></span>  

```
<svg class="icon">
  <use xlink:href="open-iconic.svg#account-login" class="icon-account-login"></use>
</svg>
```

<span data-ttu-id="f3ba4-123">Simgeler boyutlandırma, yalnızca temel CSS gerekir.</span><span class="sxs-lookup"><span data-stu-id="f3ba4-123">Sizing icons only needs basic CSS.</span></span> <span data-ttu-id="f3ba4-124">Tüm simgeleri kare biçimindedir, bu nedenle yalnızca Ayarla `<svg>` eşit genişlik ve yükseklik boyutlarla etiketi.</span><span class="sxs-lookup"><span data-stu-id="f3ba4-124">All the icons are in a square format, so just set the `<svg>` tag with equal width and height dimensions.</span></span>

```
.icon {
  width: 16px;
  height: 16px;
}
```

<span data-ttu-id="f3ba4-125">Simgeler renklendirme daha da kolaydır.</span><span class="sxs-lookup"><span data-stu-id="f3ba4-125">Coloring icons is even easier.</span></span> <span data-ttu-id="f3ba4-126">Tüm yapmanız gereken ayarlanmış `fill` üzerinde kural `<use>` etiketi.</span><span class="sxs-lookup"><span data-stu-id="f3ba4-126">All you need to do is set the `fill` rule on the `<use>` tag.</span></span>

```
.icon-account-login {
  fill: #f00;
}
```

<span data-ttu-id="f3ba4-127">SVG hareketli grafikler hakkında daha fazla bilgi edinmek için [Chris Coyier'ın Kılavuzu](http://css-tricks.com/svg-sprites-use-better-icon-fonts/).</span><span class="sxs-lookup"><span data-stu-id="f3ba4-127">To learn more about SVG Sprites, read [Chris Coyier's guide](http://css-tricks.com/svg-sprites-use-better-icon-fonts/).</span></span>

#### <a name="using-open-iconics-icon-font"></a><span data-ttu-id="f3ba4-128">Açık icon 's simgesi yazı tipi kullanarak...</span><span class="sxs-lookup"><span data-stu-id="f3ba4-128">Using Open Iconic's Icon Font...</span></span>


##### <a name="with-bootstrap"></a><span data-ttu-id="f3ba4-129">...ömürleri önyükleme</span><span class="sxs-lookup"><span data-stu-id="f3ba4-129">…with Bootstrap</span></span>

<span data-ttu-id="f3ba4-130">Bizim önyükleme stil sayfalarını bulabilirsiniz `font/css/open-iconic-bootstrap.{css, less, scss, styl}`</span><span class="sxs-lookup"><span data-stu-id="f3ba4-130">You can find our Bootstrap stylesheets in `font/css/open-iconic-bootstrap.{css, less, scss, styl}`</span></span>


```
<link href="/open-iconic/font/css/open-iconic-bootstrap.css" rel="stylesheet">
```


```
<span class="oi oi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="with-foundation"></a><span data-ttu-id="f3ba4-131">...ömürleri foundation</span><span class="sxs-lookup"><span data-stu-id="f3ba4-131">…with Foundation</span></span>

<span data-ttu-id="f3ba4-132">Bizim Foundation stil sayfalarını bulabilirsiniz `font/css/open-iconic-foundation.{css, less, scss, styl}`</span><span class="sxs-lookup"><span data-stu-id="f3ba4-132">You can find our Foundation stylesheets in `font/css/open-iconic-foundation.{css, less, scss, styl}`</span></span>

```
<link href="/open-iconic/font/css/open-iconic-foundation.css" rel="stylesheet">
```


```
<span class="fi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="on-its-own"></a><span data-ttu-id="f3ba4-133">...kutusunu işaretleyip kendi</span><span class="sxs-lookup"><span data-stu-id="f3ba4-133">…on its own</span></span>

<span data-ttu-id="f3ba4-134">Bizim varsayılan stil sayfalarını bulabilirsiniz `font/css/open-iconic.{css, less, scss, styl}`</span><span class="sxs-lookup"><span data-stu-id="f3ba4-134">You can find our default stylesheets in `font/css/open-iconic.{css, less, scss, styl}`</span></span>

```
<link href="/open-iconic/font/css/open-iconic.css" rel="stylesheet">
```

```
<span class="oi" data-glyph="icon-name" title="icon name" aria-hidden="true"></span>
```


## <a name="license"></a><span data-ttu-id="f3ba4-135">Lisans</span><span class="sxs-lookup"><span data-stu-id="f3ba4-135">License</span></span>

### <a name="icons"></a><span data-ttu-id="f3ba4-136">Simgeler</span><span class="sxs-lookup"><span data-stu-id="f3ba4-136">Icons</span></span>

<span data-ttu-id="f3ba4-137">(SVG biçimlendirme dahil) tüm kod altındadır [MIT lisansı](http://opensource.org/licenses/MIT).</span><span class="sxs-lookup"><span data-stu-id="f3ba4-137">All code (including SVG markup) is under the [MIT License](http://opensource.org/licenses/MIT).</span></span>

### <a name="fonts"></a><span data-ttu-id="f3ba4-138">Yazı Tipleri</span><span class="sxs-lookup"><span data-stu-id="f3ba4-138">Fonts</span></span>

<span data-ttu-id="f3ba4-139">Tüm yazı tipleri altındadır [SIL lisanslı](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web).</span><span class="sxs-lookup"><span data-stu-id="f3ba4-139">All fonts are under the [SIL Licensed](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web).</span></span>
