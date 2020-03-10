---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
title: Önbelleğe alınmış bir sayfaya dinamik Içerik ekleme (VB) | Microsoft Docs
author: microsoft
description: Dinamik ve önbelleğe alınmış içeriği aynı sayfada nasıl karıştıracağınızı öğrenin. Önbellek sonrası değiştirme, başlık reklamları o gibi dinamik içeriği görüntülemenizi sağlar...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 68acd884-fb57-4486-a1be-aaa93e380780
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
msc.type: authoredcontent
ms.openlocfilehash: f2f4372498e5a38bbfcb96d6e9f6338b0ef4df1f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601614"
---
# <a name="adding-dynamic-content-to-a-cached-page-vb"></a>Önbelleğe Alınmış Bir Sayfaya Dinamik İçerik Ekleme (VB)

[Microsoft](https://github.com/microsoft) tarafından

> Dinamik ve önbelleğe alınmış içeriği aynı sayfada nasıl karıştıracağınızı öğrenin. Önbellek sonrası değiştirme, önbelleğe alınmış çıktı olan bir sayfada başlık reklamları veya haber öğeleri gibi dinamik içerikleri görüntülemenizi sağlar.

Çıktı önbelleğe alma özelliğinden yararlanarak, bir ASP.NET MVC uygulamasının performansını önemli ölçüde artırabilirsiniz. Her seferinde bir sayfa yeniden oluşturulması yerine, sayfa her istendiğinde, sayfa bir kez oluşturulabilir ve birden çok kullanıcı için bellekte önbelleğe alınabilir.

Ancak bir sorun var. Sayfada dinamik içerik görüntülenmesi gerekiyorsa ne olacak? Örneğin, sayfada bir başlık tanıtımı göstermek istediğinizi düşünün. Her kullanıcının çok aynı tanıtımı görmesi için başlık tanıtımlarının önbelleğe alınmasını istemezsiniz. Bu şekilde herhangi bir para yapmayın!

Neyse ki, kolay bir çözüm vardır. ASP.NET çerçevesinin, *önbellek sonrası değiştirme*adlı bir özelliğinden yararlanabilirsiniz. Önbellek sonrası değiştirme, bellekte önbelleğe alınmış bir sayfadaki dinamik içeriği yerine getirmenizi sağlar.

Normal olarak, &lt;OutputCache&gt; özniteliğini kullanarak bir sayfada çıkış yaptığınızda, sayfa hem sunucuda hem de istemcide (Web tarayıcısı) önbelleğe alınır. Önbellek sonrası değiştirme kullandığınızda, bir sayfa yalnızca sunucuda önbelleğe alınır.

#### <a name="using-post-cache-substitution"></a>Önbellek sonrası değiştirme kullanma

Önbellek sonrası değiştirme 'nin kullanılması iki adım gerektirir. İlk olarak, önbelleğe alınmış sayfada görüntülenmesini istediğiniz dinamik içeriği temsil eden bir dize döndüren bir yöntem tanımlamanız gerekir. Daha sonra, dinamik içeriği sayfaya eklemek için HttpResponse. WriteSubstitution () yöntemini çağırın.

Örneğin, farklı haber öğelerini önbelleğe alınmış bir sayfada rastgele göstermek istediğinizi düşünün. Listeleme 1 ' deki sınıf, tek bir haber öğesini rastgele olarak üç haber öğesi listesinden döndüren RenderNews () adlı tek bir yöntem sunar.

**Listeleme 1 – Models\news.exe**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample1.vb)]

Önbellek sonrası değiştirme özelliğinden yararlanmak için HttpResponse. WriteSubstitution () yöntemini çağırın. WriteSubstitution () yöntemi, önbelleğe alınmış sayfanın bir bölgesini dinamik içerikle değiştirecek şekilde kodu ayarlar. WriteSubstitution () yöntemi, liste 2 ' deki görünümde rastgele Haberler öğesini görüntülemek için kullanılır.

**Listeleme 2 – Views\home\ındex.aspx**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample2.aspx)]

RenderNews yöntemi WriteSubstitution () yöntemine geçirilir. RenderNews yönteminin çağrılmadığından emin olun. Bunun yerine, metoda yönelik bir başvuru WriteSubstitution () öğesine AddressOf işlecinin yardımıyla geçirilir.

Dizin görünümü önbelleğe alınır. Görünüm, döküm 3 ' te denetleyici tarafından döndürülür. Dizin () eyleminin, Dizin görünümünün 60 saniye boyunca önbelleğe alınmasına neden olan bir &lt;OutputCache&gt; özniteliğiyle tasarlandığına dikkat edin.

**Listeleme 3 – Controllers\homecontroller.exe**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample3.vb)]

Dizin görünümü önbelleğe alınmış olsa bile, Dizin sayfasını istediğinizde farklı rastgele haber öğeleri görüntülenir. Dizin sayfasını istediğinizde, sayfa tarafından Görüntülenme zamanı 60 saniye boyunca değişmez (bkz. Şekil 1). Zaman, sayfanın önbelleğe alındığı kanıtlar olarak değişmez. Ancak, WriteSubstitution () yöntemi tarafından eklenen içerik – rastgele Haberler öğesi – her istekle birlikte değişir.

**Şekil 1 – önbelleğe alınmış bir sayfada dinamik haber öğelerini ekleme**

![clip_image002](adding-dynamic-content-to-a-cached-page-vb/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a>Yardım yöntemlerinde önbellek sonrası değiştirme kullanma

Önbellek sonrası değiştirme özelliğinden faydalanmak için daha kolay bir yöntem, WriteSubstitution () yöntemine yapılan çağrıyı özel bir yardımcı yöntem içinde kapsülmaktır. Bu yaklaşım, liste 4 ' teki yardımcı yönteme göre gösterilmiştir.

**Listeleme 4 – Helpers\adhelper.exe**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample4.vb)]

4\. liste, iki yöntemi ortaya çıkaran Visual Basic modülünü içerir: RenderBanner () ve RenderBannerInternal (). RenderBanner () yöntemi gerçek yardımcı yöntemi temsil eder. Bu yöntem, standart ASP.NET MVC HtmlHelper sınıfını genişleterek tıpkı diğer yardımcı yöntemler gibi bir görünümde HTML. RenderBanner () çağırabilmenizi sağlayabilir.

RenderBanner () yöntemi, RenderBannerInternal () yöntemini WriteSubstitution () yöntemine geçirerek HttpResponse. WriteSubstitution () yöntemini çağırır.

RenderBannerInternal () yöntemi özel bir yöntemdir. Bu yöntem bir yardımcı yöntem olarak sunulmayacaktır. RenderBannerInternal () yöntemi, üç başlık reklam görüntüsü listesinden rastgele bir başlık reklam görüntüsü döndürür.

5\. listede değiştirilen dizin görünümü RenderBanner () yardımcı yöntemini nasıl kullanabileceğinizi gösterir. MvcApplication1. yardımcılar ad alanını içeri aktarmak için görünümün en üstüne bir ek &lt;% @ Import%&gt; yönergesi eklendiğinden emin olun. Bu ad alanını içeri aktarmayı düşünüyorsanız, RenderBanner () yöntemi HTML özelliğinde bir yöntem olarak görünmez.

**Listeleme 5 – Views\home\ındex.aspx (RenderBanner () yöntemiyle)**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample5.aspx)]

Liste 5 ' te görünüm tarafından oluşturulan sayfayı istediğinizde, her istekle birlikte farklı bir başlık tanıtımı görüntülenir (bkz. Şekil 2). Sayfa önbelleğe alınır, ancak başlık tanıtımı RenderBanner () yardımcı yöntemiyle dinamik olarak eklenir.

**Şekil 2 – rastgele bir başlık tanıtımı görüntüleyen dizin görünümü**

![clip_image004](adding-dynamic-content-to-a-cached-page-vb/_static/image2.jpg)

#### <a name="summary"></a>Özet

Bu öğreticide, önbelleğe alınmış bir sayfada içeriği dinamik olarak nasıl güncelleştirebilmeniz açıklanmaktadır. Önbelleğe alınmış bir sayfaya dinamik içerik eklenmesi için HttpResponse. WriteSubstitution () yönteminin nasıl kullanılacağını öğrendiniz. Ayrıca, bir HTML Yardımcısı yöntemi içinde WriteSubstitution () yöntemine yapılan çağrıyı kapsüllemek için de öğrenirsiniz.

Mümkün olduğunda önbelleğe alma özelliğinden yararlanın; Web uygulamalarınızın performansı üzerinde önemli bir etkiye sahip olabilir. Bu öğreticide açıklandığı gibi, sayfalarınızda dinamik içerik görüntülenmesi gerektiğinde bile önbelleğe almanın avantajlarından yararlanabilirsiniz.

> [!div class="step-by-step"]
> [Önceki](improving-performance-with-output-caching-vb.md)
> [İleri](creating-a-controller-vb.md)
