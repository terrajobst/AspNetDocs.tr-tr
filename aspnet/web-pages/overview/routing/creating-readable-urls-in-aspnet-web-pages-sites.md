---
uid: web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
title: ASP.NET Web Pages (Razor) sitelerinde okunabilir URL 'Ler oluşturma | Microsoft Docs
author: Rick-Anderson
description: Bu makalede, ASP.NET Web Pages (Razor) Web sitesinde yönlendirmeyi ve bu, SEO için daha okunaklı ve daha iyi bir URL 'yi nasıl kullanabileceğinizi açıklar. Yapabilecekleriniz...
ms.author: riande
ms.date: 02/17/2014
ms.assetid: a8aac1ac-89de-4415-afe0-97a41c6423d2
msc.legacyurl: /web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: 832db8e144cab730f16c78f67c12feb9b7c92c7c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628396"
---
# <a name="creating-readable-urls-in-aspnet-web-pages-razor-sites"></a>ASP.NET Web Pages (Razor) sitelerinde okunabilir URL 'Ler oluşturma

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede, ASP.NET Web Pages (Razor) Web sitesinde yönlendirmeyi ve bu, SEO için daha okunaklı ve daha iyi bir URL 'yi nasıl kullanabileceğinizi açıklar.
> 
> Öğrenecekleriniz:
> 
> - ASP.NET daha okunabilir ve aranabilir URL 'Ler kullanmanıza imkan sağlamak için yönlendirmeyi nasıl kullanır.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 3
>   
> 
> Bu öğretici, ASP.NET Web Pages 2 ile de kullanılabilir.

## <a name="about-routing"></a>Yönlendirme hakkında

Sitenizdeki sayfaların URL 'Leri, sitenin ne kadar iyi çalıştığıyla ilgili bir etkiye sahip olabilir. &quot;kolay&quot; bir URL, kişilerin siteyi kullanmasını kolaylaştırabilir. Ayrıca, site için arama motoru iyileştirmesi (SEO) konusunda da yardımcı olabilir. ASP.NET Web siteleri, kolay URL 'Leri otomatik olarak kullanma özelliği içerir.

ASP.NET, yalnızca sunucusundaki bir dosyaya işaret etmek yerine kullanıcı eylemlerini tanımlayan anlamlı URL 'Ler oluşturmanızı sağlar. Kurgusal bir blog için bu URL 'Leri göz önünde bulundurun:

- `http://www.contoso.com/Blog/blog.cshtml?categories=hardware`
- `http://www.contoso.com//Blog/blog.cshtml?startdate=2009-11-01&enddate=2009-11-30`

Bu URL 'Leri aşağıdaki olanlarla karşılaştırın:

- `http://www.contoso.com/Blog/categories/hardware/`
- `http://www.contoso.com/Blog/2009/November`

İlk çifte, kullanıcının blog *. cshtml* sayfasını kullanarak Web blogunuzun görüntülendiğini ve ardından doğru kategoriyi veya tarih aralığını alan bir sorgu dizesi oluşturacağını bilmeleri gerekir. İkinci örnek kümesi, anlarsınız ve oluşturmak için çok daha kolaydır.

İlk örnek URL 'Leri de doğrudan belirli bir dosyaya işaret eden (*blog. cshtml*). Herhangi bir nedenle blog sunucudaki başka bir klasöre taşınırsa veya blog farklı bir sayfa kullanmak üzere yeniden yazıldı, bağlantılar yanlış olur. İkinci URL kümesi belirli bir sayfaya işaret etmez, bu nedenle blog uygulamasının veya konumunun değişse bile URL 'Ler hala geçerli olur.

ASP.NET Web sayfalarında, Yukarıdaki örneklerde olduğu gibi, daha kolay URL 'Ler oluşturabilirsiniz çünkü ASP.NET *yönlendirme*kullanır. Yönlendirme bir URL 'den, isteği yerine getirebilecek bir sayfaya (veya sayfalara) mantıksal eşleme oluşturur. Eşleme mantıksal (belirli bir dosyaya fiziksel değil) olduğundan, yönlendirme sitenizin URL 'Lerini nasıl tanımladığınız konusunda harika bir esneklik sağlar.

## <a name="how-routing-works"></a>Yönlendirmenin nasıl çalıştığı

ASP.NET bir isteği işlediğinde, nasıl yönlendirileceğini anlamak için URL 'YI okur. ASP.NET, soldan sağa doğru bir şekilde URL 'nin bağımsız segmentlerini disk üzerindeki dosyalarla eşleştirmeye çalışır. Bir eşleşme varsa, URL 'de kalan herhangi bir şey *yol bilgisi*olarak sayfaya geçirilir.

Birisinin bu URL 'YI kullanarak bir istek yaptığı hakkında düşünün:

`http://www.contoso.com/a/b/c`

Arama şöyle gider:

1. */A/b/c.exe*yolunu ve adını içeren bir dosya var mı? Bu durumda, bu sayfayı çalıştırın ve bu sayfaya bilgi geçirin. Aksi taktirde...
2. */A/b/cshtml*yolu ve adı olan bir dosya var mı? Bu durumda, bu sayfayı çalıştırın ve `c` değeri geçirin. Aksi takdirde...
3. */A.exe*yolu ve adı ile bir dosya var mı? Bu durumda, bu sayfayı çalıştırın ve `b/c` değeri geçirin.

Arama, belirtilen klasörlerinde *. cshtml* dosyaları için tam eşleşme bulmazsa, ASP.NET bu dosyaları sırayla aramaya devam eder:

1. */a/b/c/default.exe* (yol bilgisi yok).
2. */a/b/c/Index.cshtml* (yol bilgisi yok).

> [!NOTE]
> Açık olması için, belirli sayfalara yönelik istekler (yani, *. cshtml* dosya adı uzantısını içeren istekler) yalnızca bekleyeceğiniz gibi çalışır. `http://www.contoso.com/a/b.cshtml` gibi bir istek, *b. cshtml* sayfasını sorunsuz bir şekilde çalıştıracaktır.

Bir sayfa içinde, sayfanın `UrlData` özelliği aracılığıyla yol bilgilerini alabilir, bu bir sözlük. *Viewcustomers. cshtml* adlı bir dosyanız olduğunu ve sitenizin bu isteği aldığından emin olmak için:

`http://mysite.com/myWebSite/ViewCustomers/1000`

Yukarıdaki kurallarda açıklandığı gibi, istek sayfanıza gidecektir. Sayfanın içinde, yol bilgilerini almak ve göstermek için aşağıdaki gibi bir kod kullanabilirsiniz (Bu durumda &quot;1000&quot;):

[!code-html[Main](creating-readable-urls-in-aspnet-web-pages-sites/samples/sample1.html)]

> [!NOTE]
> Yönlendirme tam dosya adlarını içermediğinden, aynı ada ancak farklı dosya adı uzantılarına sahip sayfalarınız varsa (örneğin, *MyPage. cshtml* ve *MyPage. html*), belirsizlik olabilir. Yönlendirme ile ilgili sorunlardan kaçınmak için, sitenizde adları yalnızca kendi uzantısında farklı olan sayfalarınız olmadığından emin olmak en iyisidir.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

[WebMatrix-URL 'ler, UrlData ve SEO Için yönlendirme](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO). Mike Brind tarafından bu blog girdisi, ASP.NET Web sayfalarında yönlendirmenin nasıl çalıştığı hakkında bazı ek ayrıntılar sağlar.
