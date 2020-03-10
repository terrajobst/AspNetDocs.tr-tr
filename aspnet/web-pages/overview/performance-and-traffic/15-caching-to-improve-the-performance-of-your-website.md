---
uid: web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
title: Daha Iyi performans için bir ASP.NET Web sayfaları (Razor) sitesinde verileri önbelleğe alma | Microsoft Docs
author: Rick-Anderson
description: Web sitenizi, depolama alanı, önbelleğe alma ve genellikle bir işlem almak veya işlemek için uzun zaman alan veri sonuçları gibi bir şekilde hızlandırabilecek şekilde hızlandırabilirsiniz...
ms.author: riande
ms.date: 02/14/2014
ms.assetid: 961e525b-7700-469e-8a68-d7010b6fb68c
msc.legacyurl: /web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
msc.type: authoredcontent
ms.openlocfilehash: 01796d3ca699a6af5d9162b22a926551435c2040
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641521"
---
# <a name="caching-data-in-an-aspnet-web-pages-razor-site-for-better-performance"></a>Daha Iyi performans için bir ASP.NET Web sayfaları (Razor) sitesinde verileri önbelleğe alma

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede, bir ASP.NET Web Pages (Razor) Web sitesinde daha hızlı performans için bilgileri önbelleğe almak üzere bir yardımcı 'nın nasıl kullanılacağı açıklanmaktadır. Web sitenizi, bir depolama &#8212; alanına sahip olacak şekilde artırabilir, &#8212; bu da genellikle veri alma veya işleme için önemli ölçüde zaman alabilir ve sık değişmemelidir.
> 
> **Şunları öğreneceksiniz:** 
> 
> - Web sitenizin yanıt hızını artırmak için önbelleğe alma özelliğini kullanma.
> 
> Makalesinde sunulan ASP.NET özellikleri şunlardır:
> 
> - `WebCache` Yardımcısı.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 3
>   
> 
> Bu öğretici, ASP.NET Web Pages 2 ile de kullanılabilir.

Sitenizdeki her bir sayfa istediğinde, Web sunucusunun isteği yerine getirmek için bazı işler yapması gerekir. Sayfalarınızın bir kısmı için, bir veritabanından veri alma gibi bir çok uzun süre (karşılaştırmalı) alan görevleri gerçekleştirmek için sunucu gerekebilir. Bu görevler mutlak koşullarda uzun sürmese bile, siteniz çok sayıda trafik yaşıyorsa, Web sunucusunun karmaşık veya yavaş görevi gerçekleştirmesini sağlayan bir dizi tek isteğin tamamı çok fazla iş ekleyebilirler. Bu, sonunda sitenin performansını etkileyebilir.

Bu gibi durumlarda Web sitenizin performansını artırmanın bir yolu, verileri önbelleğe alma yöntemidir. Siteniz aynı bilgiler için yinelenen istekler alıyorsa ve bilgilerin her bir kişi için değiştirilmesi gerekmiyorsa ve zamana duyarlı değilse, yeniden almak veya yeniden hesaplanması yerine, verileri bir kez getirip sonuçları kaydedebilirsiniz. Bu bilgiler için bir sonraki istek geldiğinde, bunu yalnızca önbellekten alırsınız.

Genel olarak, sık değişmeyen bilgileri önbelleğe alırsınız. Bilgileri önbelleğe koyduğunuzda, Web sunucusunda bellekte depolanır. Saniye ile günlere ne kadar süre önbellekte tutulacağını belirtebilirsiniz. Önbelleğe alma döneminin süresi dolarsa, bilgiler önbellekten otomatik olarak kaldırılır.

> [!NOTE]
> Önbellekteki girişler, bunların süre doldukları nedenlerle kaldırılabilir. Örneğin, Web sunucusunun belleği geçici olarak azalmış olabilir ve belleği geri kazanmak için bir yol, girişlerin önbellekten çıkarılmasından kaynaklanabilir. Gördüğünüz gibi, önbelleğe bilgi yerleştirseniz bile, yine de ihtiyacınız olduğunda emin olmak için kontrol etmeniz gerekir.

Web sitenizin geçerli sıcaklık ve hava durumu tahminini görüntüleyen bir sayfa olduğunu düşünün. Bu tür bilgileri almak için bir dış hizmete bir istek gönderebilirsiniz. Bu bilgiler çok fazla değişmediğinden (örneğin, iki saatlik bir zaman diliminde) ve dış çağrılar zaman ve bant genişliği gerektirdiğinden, önbelleğe alma işlemi için iyi bir adaydır.

## <a name="adding-caching-to-a-page"></a>Bir sayfaya önbelleğe alma ekleme

ASP.NET, sitenize önbellek eklemenizi ve önbelleğe veri eklemenizi kolaylaştıran bir `WebCache` Yardımcısı içerir. Bu yordamda, geçerli saati önbelleğe alan bir sayfa oluşturacaksınız. Bu gerçek bir örnek değildir, çünkü geçerli zaman sık değişme ve hesaplanmasının karmaşık olmadığı bir şeydir. Ancak, önbelleğe alma işlemini çalışırken göstermek için iyi bir yoldur.

1. Web sitesine *webcache. cshtml* adlı yeni bir sayfa ekleyin.
2. Aşağıdaki kodu ve biçimlendirmeyi sayfaya ekleyin:

    [!code-cshtml[Main](15-caching-to-improve-the-performance-of-your-website/samples/sample1.cshtml)]

    Verileri önbelleğe aldığınızda, bu Web sitesi genelinde benzersiz bir ad kullanarak önbelleğe koyabilirsiniz. Bu durumda, `CachedTime`adlı bir önbellek girişi kullanacaksınız. Bu, kod örneğinde gösterilen `cacheItemKey`.

    Kod ilk olarak `CachedTime` önbellek girdisini okur. Değer döndürülürse (yani, önbellek girdisi null değilse), kod yalnızca zaman değişkeninin değerini önbellek verilerine ayarlar.

    Ancak, önbellek girdisi yoksa (yani null ise), kod saat değerini ayarlar, önbelleğe ekler ve bir süre sonu değerini bir dakika olarak ayarlar. Bir dakika sonra, önbellek girdisi atılır. (Önbellekteki bir öğe için varsayılan süre sonu değeri 20 dakikadır.) Komut `WebCache.Set(cacheItemKey, time, 1, false)`, geçerli saat değerinin önbelleğe nasıl ekleneceğini ve süresinin 1 dakika olarak ayarlanacağını gösterir. *SlidingExpiration* parametresinin `false` olarak ayarlanması, sona erme zamanının istendiği her seferinde yenilenmediği anlamına gelir. İlk olarak önbelleğe eklendikten sonra 1 dakikalık süre dolacak. Bu değeri `true` olarak ayarlarsanız, değerin önbellekten her istenilişinde 1 dakikalık sona erme saati sıfırlanır.

    Bu kod, verileri önbelleğe alırken her zaman kullanmanız gereken kalıbı gösterir. Önbellekten bir şey yapmadan önce, `WebCache.Get` yönteminin null döndürmediğini her zaman denetleyin. Önbellek girişinin dolduğunu veya başka bir nedenle kaldırılmış olabileceğini unutmayın. bu nedenle, belirli bir girdinin önbellekte olması hiçbir zaman garanti edilmez.
3. *Web Cache. cshtml* dosyasını bir tarayıcıda çalıştırın. (Çalıştırmadan önce sayfanın **dosyalar** çalışma alanında seçili olduğundan emin olun.) Sayfayı ilk kez istediğinizde, zaman verileri önbellekte değildir ve kodun zaman değerini önbelleğe eklemesi gerekir.

    ![Önbellek-1](15-caching-to-improve-the-performance-of-your-website/_static/image1.jpg)
4. Tarayıcıda *webcache. cshtml* dosyasını yenileyin. Bu kez, zaman verileri önbellekte olur. Sayfayı son görüntülediğiniz zamandan bu yana zaman değişmediğinden emin olun.

    ![önbellek-2](15-caching-to-improve-the-performance-of-your-website/_static/image2.jpg)
5. Önbelleğin boşaltılması için bir dakika bekleyin ve sonra sayfayı yenileyin. Sayfa, zaman verilerinin önbellekte bulunamadığını ve güncelleştirilmiş saatin önbelleğe eklendiğini gösterir.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

- [Verileri Bir Grafikte Görüntüleme](https://go.microsoft.com/fwlink/?LinkId=202895)
- [WebCache API başvurusu](https://msdn.microsoft.com/library/system.web.helpers.webcache(v=vs.99).aspx) (MSDN)
