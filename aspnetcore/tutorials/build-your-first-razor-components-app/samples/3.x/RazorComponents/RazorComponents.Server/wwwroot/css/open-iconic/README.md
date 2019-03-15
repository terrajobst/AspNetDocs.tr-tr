---
ms.openlocfilehash: 3965884c8e0d7116f5d8a42e6aefb0dc5be94f1e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57078123"
---
<a name="open-iconic-v111httpuseiconiccomopen"></a>[İcon v1.1.1 açın](http://useiconic.com/open)
===========

### <a name="open-iconic-is-the-open-source-sibling-of-iconichttpuseiconiccom-it-is-a-hyper-legible-collection-of-223-icons-with-a-tiny-footprintmdashready-to-use-with-bootstrap-and-foundation-view-the-collectionhttpuseiconiccomopenicons"></a>Açık Iconic olan açık kaynak eşdüzey [Iconic](http://useiconic.com). Küçük ayak 223 simgelerle okunaklı hyper koleksiyonu olan&mdash;Bootstrap ve Foundation ile kullanıma hazır. [Koleksiyon görünümü](http://useiconic.com/open#icons)



## <a name="whats-in-open-iconic"></a>Aç'icon nedir?

* Aşağı 8 piksel okunaklı olacak şekilde tasarlanan 223 simgeleri
* Süper ışık SVG dosyaları - 61.8 tamamını için 
* SVG sprite&mdash;simgesi yazı tipleri için modern değiştirme
* Webfont (EOT, OTF, SVG, fot adı, WOFF), PNG ve WebP biçimleri
* (Önyükleme ve Foundation sürümleri dahil) Webfont stil sayfalarını CSS ya da daha az, SCSS ve ekran kalemi biçimleri
* PNG ve WebP ızgara görüntüleri 8px, 16px, 24px, 32px, 48px ve 64px.


## <a name="getting-started"></a>Başlarken

#### <a name="for-code-samples-and-everything-else-you-need-to-get-started-with-open-iconic-check-out-our-iconshttpuseiconiccomopenicons-and-referencehttpuseiconiccomopenreference-sections"></a>Kod örnekleri ve diğer her şey açık icon ile kullanmaya başlamak için ihtiyacınız için kullanıma sunduğumuz [simgeler](http://useiconic.com/open#icons) ve [başvuru](http://useiconic.com/open#reference) bölümler.

### <a name="general-usage"></a>Genel kullanım

#### <a name="using-open-iconics-svgs"></a>Açık icon 's SVGs kullanma

SVGs istiyoruz ve web üzerinde simgelerini görüntülemek için yol oldukları düşünüyoruz. Açık icon olduğundan yalnızca temel SVGs, görüntü bunları başka bir görüntü gibi öneririz (unutmayın `alt` özniteliği).

```
<img src="/open-iconic/svg/icon-name.svg" alt="icon name">
```

#### <a name="using-open-iconics-svg-sprite"></a>Açık icon 's SVG Sprite kullanma

Açık Iconic ayrıca tek bir istekle kümesindeki tüm simgeleri göstermek izin veren bir SVG sprite içinde bulunur. Bu, bir simge yazı tipi gibi bir korsan olmadan olur.

Simge bir SVG ekleme sprite için kullandığınız değerinden biraz farklıdır, ancak hala yazan bir pasta. *İpucu: Simgelerinizi kolayca stil mümkün hale getirmek için genel bir sınıfa eklemeyi önerin* `<svg>` *etiketi ve her farklı simge için bir benzersiz sınıf adı* `<use>` *etiketi.*  

```
<svg class="icon">
  <use xlink:href="open-iconic.svg#account-login" class="icon-account-login"></use>
</svg>
```

Simgeler boyutlandırma, yalnızca temel CSS gerekir. Tüm simgeleri kare biçimindedir, bu nedenle yalnızca Ayarla `<svg>` eşit genişlik ve yükseklik boyutlarla etiketi.

```
.icon {
  width: 16px;
  height: 16px;
}
```

Simgeler renklendirme daha da kolaydır. Tüm yapmanız gereken ayarlanmış `fill` üzerinde kural `<use>` etiketi.

```
.icon-account-login {
  fill: #f00;
}
```

SVG hareketli grafikler hakkında daha fazla bilgi edinmek için [Chris Coyier'ın Kılavuzu](http://css-tricks.com/svg-sprites-use-better-icon-fonts/).

#### <a name="using-open-iconics-icon-font"></a>Açık icon 's simgesi yazı tipi kullanarak...


##### <a name="with-bootstrap"></a>...ömürleri önyükleme

Bizim önyükleme stil sayfalarını bulabilirsiniz `font/css/open-iconic-bootstrap.{css, less, scss, styl}`


```
<link href="/open-iconic/font/css/open-iconic-bootstrap.css" rel="stylesheet">
```


```
<span class="oi oi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="with-foundation"></a>...ömürleri foundation

Bizim Foundation stil sayfalarını bulabilirsiniz `font/css/open-iconic-foundation.{css, less, scss, styl}`

```
<link href="/open-iconic/font/css/open-iconic-foundation.css" rel="stylesheet">
```


```
<span class="fi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="on-its-own"></a>...kutusunu işaretleyip kendi

Bizim varsayılan stil sayfalarını bulabilirsiniz `font/css/open-iconic.{css, less, scss, styl}`

```
<link href="/open-iconic/font/css/open-iconic.css" rel="stylesheet">
```

```
<span class="oi" data-glyph="icon-name" title="icon name" aria-hidden="true"></span>
```


## <a name="license"></a>Lisans

### <a name="icons"></a>Simgeler

(SVG biçimlendirme dahil) tüm kod altındadır [MIT lisansı](http://opensource.org/licenses/MIT).

### <a name="fonts"></a>Yazı Tipleri

Tüm yazı tipleri altındadır [SIL lisanslı](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web).
