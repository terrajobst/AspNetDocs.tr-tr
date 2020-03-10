---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: Dinamik güncelleştirmeleri sunmak için AJAX kullanma | Microsoft Docs
author: microsoft
description: 10. adım, oturum açan kullanıcıların, akşam yemeği ayrıntısı dahilinde tümleşik bir Ajax tabanlı yaklaşım kullanarak bir akşam yemeği ile ilgilendikleri konusunda bilgi almak için destek uygular...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 3edc02fec546609505b5e085440fa684abe7acd0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600851"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a>AJAX Kullanarak Dinamik Güncelleştirmeler Sunma

[Microsoft](https://github.com/microsoft) tarafından

[PDF 'YI indir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu, ASP.NET MVC 1 kullanarak küçük, ancak tam bir Web uygulamasının nasıl oluşturulacağını gösteren ücretsiz bir ["Nerdakşam yemeği" uygulama öğreticisinin](introducing-the-nerddinner-tutorial.md) adım 10 ' dur.
> 
> 10. adım, oturum açan kullanıcıların, akşam yemeği ayrıntıları sayfasında tümleştirilmiş Ajax tabanlı bir yaklaşım kullanarak bir akşam yemeği ile ilgilenmek için destek sağlar.
> 
> ASP.NET MVC 3 kullanıyorsanız, [MVC 3 Ile çalışmaya başlama](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC müzik mağazası](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) öğreticilerini izlemeniz önerilir.

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a>Nerdakşam yemeği adım 10: AJAX etkinleştirme RSVPs kabul eder

Şimdi, oturum açan kullanıcılar için bir akşam yemeği ile ilgilendikleri için destek uygulayalim. Bunu, akşam yemeği ayrıntıları sayfasında tümleştirilmiş bir AJAX tabanlı yaklaşım kullanarak etkinleştireceğiz.

### <a name="indicating-whether-the-user-is-rsvpd"></a>Kullanıcının RSVP olup olmadığını belirtir

Kullanıcılar, belirli bir akşam yemeği hakkındaki ayrıntıları görmek için */Dinners/details/[ID*] URL 'sini ziyaret edebilir:

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

Ayrıntılar () eylem yöntemi şöyle uygulanır:

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

RSVP desteğini uygulamaya yönelik ilk adımımız, akşam yemeği nesnemiz için bir "ıkullanıcıkayıtlı (Kullanıcı adı)" yardımcı yöntemi eklemektir (daha önce oluşturduğumuz Dinner.cs kısmi sınıfı içinde). Bu yardımcı yöntem, kullanıcının akşam yemeği için geçerli olup olmadığına bağlı olarak true veya false değerini döndürür:

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

Daha sonra, kullanıcının kaydedilip edilmeyeceğini belirten uygun bir ileti görüntülemek için details. aspx görünüm şablonumuza aşağıdaki kodu ekleyebiliriz:

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

Şimdi de bir Kullanıcı akşam yemeği ziyaret ettiğinde şu iletiyi görür:

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

Bir akşam yemeği ziyaret ettiğinde, bu kişiler için kayıtlı değildir ve şu iletiyi görürsünüz:

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a>Register ACTION metodunu uygulama

Şimdi, Ayrıntılar sayfasından kullanıcıların bir akşam yemeği için RSVP 'e yanıt vermek üzere gerekli işlevselliği ekleyelim.

Bunu uygulamak için, \Controllers dizinine sağ tıklayıp add-&gt;Controller menü komutunu seçerek yeni bir "RSVPController" sınıfı oluşturacağız.

Bağımsız değişken olarak akşam yemeği için bir kimlik alan yeni RSVPController sınıfında bir "Register" eylem yöntemi uygulayacağız, uygun akşam yemeği nesnesini alır, oturum açan kullanıcının o anda kendisi için Kaydolmakta olup olmadığını denetler ve Bunlar için bir RSVP nesnesi eklememez:

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

Eylem yönteminin çıktısı olarak nasıl basit bir dize döndüyoruz hakkında bildirim. Bu iletiyi bir görünüm şablonu içinde katıştırıyoruz, ancak bu nedenle küçük olduğundan, denetleyici temel sınıfında Content () yardımcı yöntemini kullanacağız ve yukarıdaki gibi bir dize iletisi döndürdük.

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a>AJAX kullanarak RSVPForEvent eylem yöntemini çağırma

AJAX ' i, Ayrıntılar görünümümüzde kaydetme eylemi yöntemini çağırmak için kullanacağız. Bunu uygulamak oldukça kolaydır. İlk olarak iki betik kitaplığı başvurusu ekleyeceğiz:

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

İlk kitaplık, çekirdek ASP.NET AJAX istemci tarafı komut dosyası kitaplığına başvurur. Bu dosya yaklaşık 24k boyutunda (sıkıştırılmış) ve çekirdek istemci tarafı AJAX işlevleri içerir. İkinci kitaplık, ASP.NET MVC 'nin yerleşik AJAX Yardımcısı yöntemleriyle (kısa süre içinde kullanacağız) tümleştirilen yardımcı program işlevlerini içerir.

Daha sonra, daha önce eklediğimiz görünüm şablonu kodunu, "Bu olay için kaydolmadıysanız" iletisini almak yerine daha sonra güncelleştirebiliriz. bunun yerine, gönderildiğinde, RSVP denetleyicimizde RSVPForEvent eylem yöntemini çağıran bir AJAX çağrısı gerçekleştirdiğinde bir bağlantı oluşturuyoruz RSVPs ve Kullanıcı:

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

Yukarıda kullanılan Ajax. ActionLink () yardımcı yöntemi yerleşik ASP.NET MVC 'dir ve HTML. ActionLink () yardımcı yöntemine benzer ve standart bir gezinti gerçekleştirmek yerine, bağlantı tıklandığında eylem yöntemine bir AJAX çağrısı yapar. Yukarıdaki "RSVP" denetleyicisindeki "Register" eylem yöntemini çağırıyoruz ve DinnerID ' i "ID" parametresi olarak geçiririz. Geçirdiğimiz son AjaxOptions parametresi, eylem yönteminden döndürülen içeriği almak ve kimliği "rsvpmsg" olan sayfada HTML &lt;div&gt; öğesini güncelleştirmek istediğimiz olduğunu gösterir.

Şimdi de bir Kullanıcı bir akşam yemeği 'ye gözattığında, bunun için bir RSVP bağlantısı görürsünüz:

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

"Bu olaya yönelik RSVP" bağlantısını tıkladıklarında, RSVP denetleyicisindeki kayıt eylemi yöntemine bir AJAX çağrısı yapar ve tamamlandığında aşağıdaki gibi güncelleştirilmiş bir ileti görür:

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

Bu AJAX çağrısını yapmak için kullanılan ağ bant genişliği ve trafik gerçekten hafif. Kullanıcı "Bu olaya yönelik RSVP" bağlantısı üzerine tıkladığında, */Dinners/Register/1* URL 'sine şu şekilde BIR küçük http post ağı isteği yapılır:

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

Kayıt eylemi yönteminizin yanıtı yalnızca şu şekilde yapılır:

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

Bu hafif çağrı hızlıdır ve yavaş bir ağ üzerinden bile çalışacaktır.

### <a name="adding-a-jquery-animation"></a>JQuery animasyonu ekleme

Uyguladığımız AJAX işlevleri iyi ve hızlı bir şekilde çalışmaktadır. Bazen hızlı bir şekilde gerçekleşebilir, ancak Kullanıcı RSVP bağlantısının yeni metinle değiştirildiğini fark edemeyebilir. Sonucu daha belirgin hale getirmek için, güncelleştirme iletisine dikkat çekmek üzere basit bir animasyon ekleyebiliriz.

Varsayılan ASP.NET MVC proje şablonu, Microsoft tarafından da desteklenen jQuery: mükemmel (ve çok popüler) açık kaynaklı JavaScript kitaplığı içerir. jQuery, iyi bir HTML DOM seçimi ve efektler kitaplığı dahil olmak üzere çeşitli özellikler sağlar.

JQuery kullanmak için önce buna bir betik başvurusu ekleyeceğiz. Sitemizdeki çeşitli konumlarda jQuery kullanacağınızı öğrendiğimiz için, tüm sayfaların onu kullanabilmesi için, site. Master ana sayfa dosyası içinde betik başvurusunu ekleyeceğiz.

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

*İpucu: JavaScript dosyaları için daha zengin IntelliSense desteğini sağlayan VS 2008 SP1 için JavaScript IntelliSense düzeltmesini (jQuery dahil) yüklediğinizden emin olun. Buradan indirebilirsiniz: http://tinyurl.com/vs2008javascripthotfix*

JQuery kullanılarak yazılan kod genellikle CSS seçiciyi kullanarak bir veya daha fazla HTML öğesi alan Global "$ ()" JavaScript yöntemini kullanır. Örneğin, *$ ("#rsvpmsg")* , rsvpmsg kimliğine sahip HERHANGI bir HTML öğesini seçer, ancak *$ (". bir")* , "bir" CSS sınıfı adı olan tüm öğeleri seçer. Ayrıca, "işaretlenmiş radyo düğmelerinin tümünü Döndür" gibi daha gelişmiş sorgular da yazabilirsiniz: *$ ("input [@type= Radio] [@checked]")* .

Öğeleri seçtikten sonra, bunları gizleme gibi eyleme geçmek için yöntemler çağırabilirsiniz: *$ ("#rsvpmsg"). Hide ();*

RSVP senaryomız için, "rsvpmsg" &lt;div&gt; seçen ve metin içeriğinin boyutunu canlandırmış olan "AnimateRSVPMessage" adlı basit bir JavaScript işlevi tanımlayacağız. Aşağıdaki kod, metni küçük ve 400 milisaniyelik zaman diliminde artmasına neden olur:

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

Daha sonra bu JavaScript işlevinin adı Ajax. ActionLink () yardımcı yöntemimize (AjaxOptions "OnSuccess" olay özelliği aracılığıyla) başarılı bir şekilde tamamlandıktan sonra, AJAX çağrımız başarıyla tamamlandıktan sonra çağrılabilir:

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

Artık "Bu olaya yönelik RSVP" bağlantısı tıklandığında ve AJAX çağrımız başarıyla tamamlanırsa, geri gönderilen içerik iletisi animasyon uygular ve büyük büyüyülecektir:

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

"OnSuccess" olayı sağlamaya ek olarak, AjaxOptions nesnesi, işleyebileceğiniz Onbegın, OnFailure ve Ontamamlanmış olayları (diğer özellikler ve yararlı seçeneklerle birlikte) kullanıma sunar.

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a>Temizleme-bir RSVP kısmi görünümünü yeniden düzenleme

Ayrıntılar görünümü şablonu biraz uzun sürer, bu da fazla mesainin anlaşılması biraz daha zor hale gelir. Kod okunabilirliğini artırmaya yardımcı olmak için, Ayrıntılar sayfamız için tüm RSVP görünüm kodunu kapsülleyen kısmi bir görünüm – RSVPStatus. ascx ' i oluşturarak bitelim.

Bunu, \Views\dıntik klasörüne sağ tıklayıp ardından Ekle-&gt;görünümü menü komutunu seçerek yapabiliriz. Bir akşam yemeği nesnesini kesin belirlenmiş ViewModel olarak ele alacağız. Bundan sonra, details. aspx görünümümüzden gelir içeriğini kopyalayabilir/yapıştırabilir.

Bunu yaptıktan sonra, Düzenle ve Sil bağlantı görünümü kodumuzu kapsülleyen bir kısmi görünüm – EditAndDeleteLinks. ascx ' i de oluşturalım. Ayrıca, bunu kesin belirlenmiş ViewModel olarak bir akşam yemeği nesnesi alacak ve details. aspx görünümümüzde düzenleme ve silme mantığını kopyalayacak/yapıştırıyoruz.

Ayrıntılar görünümü şablonu, en alta yalnızca iki HTML. RenderPartial () yöntem çağrısı içerebilir:

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

Bu, kod temizleyiciyi okumayı ve bakımını yapmayı sağlar.

### <a name="next-step"></a>Sonraki adım

Artık AJAX 'ı daha da nasıl kullanabileceğimizi ve uygulamamıza etkileşimli eşleme desteği eklemenizi inceleyelim.

> [!div class="step-by-step"]
> [Önceki](secure-applications-using-authentication-and-authorization.md)
> [İleri](use-ajax-to-implement-mapping-scenarios.md)
