---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-cs
title: Çıktı önbelleğe alma ile performansı iyileştirmeC#() | Microsoft Docs
author: microsoft
description: Bu öğreticide, çıkış önbelleğe alma özelliğinden yararlanarak ASP.NET MVC web uygulamalarınızın performansını ciddi ölçüde iyileştirebileceğinizi öğreneceksiniz. Siz...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 521c9117-81cd-4d8d-9d96-0256dc7bf50f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-cs
msc.type: authoredcontent
ms.openlocfilehash: 548c5bea2e9cf26e0574e72d2c0ea204dbd90f9c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601271"
---
# <a name="improving-performance-with-output-caching-c"></a>Çıktı Önbelleğe Alma ile Performansı İyileştirme (C#)

[Microsoft](https://github.com/microsoft) tarafından

> Bu öğreticide, çıkış önbelleğe alma özelliğinden yararlanarak ASP.NET MVC web uygulamalarınızın performansını ciddi ölçüde iyileştirebileceğinizi öğreneceksiniz. Bir denetleyici eyleminden döndürülen sonucun nasıl önbelleğe alınacağını öğrenirsiniz, böylece her yeni kullanıcı eylemi her çağırdığında aynı içeriğin her bir oluşturulması gerekmez.

Bu öğreticinin amacı, çıkış önbelleğinden yararlanarak bir ASP.NET MVC uygulamasının performansını ciddi ölçüde iyileştirebileceğinizi açıklamaktır. Çıktı önbelleği, bir denetleyici eylemi tarafından döndürülen içeriği önbelleğe almanıza olanak sağlar. Bu şekilde, aynı denetleyici eylemi her çağrıldığında aynı içeriğin her biri ve her seferinde oluşturulması gerekmez.

Örneğin, ASP.NET MVC uygulamanızın dizin adlı bir görünümdeki veritabanı kayıtlarının listesini görüntülediğini düşünün. Normalde, her biri ve bir Kullanıcı dizin görünümünü döndüren denetleyici eylemini her çağırdığında, veritabanı kayıtlarının bir veritabanı sorgusu yürütülerek veritabanından alınması gerekir.

Diğer taraftan, çıkış önbelleğinden faydalanabilirsiniz, her kullanıcı aynı denetleyici eylemini her çağırdığında bir veritabanı sorgusunun yürütülmesinden kaçınabilirsiniz. Görünüm, denetleyici eyleminden yeniden oluşturulması yerine önbellekten alınabilir. Önbelleğe alma, sunucuda yedekli iş gerçekleştirmenizi önlemenize olanak sağlar.

## <a name="enabling-output-caching"></a>Çıktı önbelleğe alma etkinleştiriliyor

Tek bir denetleyici eylemine veya bir denetleyici sınıfına [OutputCache] özniteliği ekleyerek çıkış önbelleğe almayı etkinleştirirsiniz. Örneğin, liste 1 ' deki denetleyici dizin () adlı bir eylem gösterir. Dizin () eyleminin çıkışı 10 saniye için önbelleğe alınır.

**Listeleme 1 – Controllers\HomeController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample1.cs)]

ASP.NET MVC 'nin Beta sürümlerinde, çıkış önbelleği [http://www.MySite.com/](http://www.mysite.com/)gıbı bir URL için çalışmaz. Bunun yerine, [http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index)gıbı bir URL girmeniz gerekir. 

Liste 1 ' de, dizin () eyleminin çıkışı 10 saniye için önbelleğe alınır. İsterseniz, daha uzun bir önbellek süresi belirtebilirsiniz. Örneğin, bir gün için bir denetleyici eyleminin çıkışını önbelleğe almak istiyorsanız, 86400 saniyelik bir önbellek süresi (60 saniye \* 60 dakika \* 24 saat) belirtebilirsiniz.

Belirlediğiniz zaman miktarı için içeriğin önbelleğe alınacağını garanti etmez. Bellek kaynakları azaldığında, önbellek içeriği otomatik olarak çıkarma başlar.

Liste 1 ' deki giriş denetleyicisi, liste 2 ' de dizin görünümünü döndürür. Bu görünüm hakkında özel bir şey yok. Dizin görünümü yalnızca geçerli saati görüntüler (bkz. Şekil 1).

**Listeleme 2 – Views\home\ındex.aspx**

[!code-aspx[Main](improving-performance-with-output-caching-cs/samples/sample2.aspx)]

**Şekil 1 – önbelleğe alınmış dizin görünümü**

![clip_image002](improving-performance-with-output-caching-cs/_static/image1.jpg)

Tarayıcınızın adres çubuğuna/Home/Index URL 'sini girerek dizin () eylemini birden çok kez çağırırsanız ve tarayıcınızdaki Yenile/yeniden yükle düğmesine sürekli olarak geçiş yaparsanız, dizin görünümü tarafından Görüntülenme zamanı 10 saniye değişmez. Aynı zaman görüntülenir, çünkü görünüm önbelleğe alınır.

Uygulamanızı ziyaret eden herkes için aynı görünümün önbelleğe alındığını anlamak önemlidir. Dizin () eylemini çağıran herkes, Dizin görünümünün önbelleğe alınmış sürümünü alır. Bu, Web sunucusunun dizin görünümüne hizmeti sağlamak için gerçekleştirmesi gereken iş miktarının önemli ölçüde azaltıldığı anlamına gelir.

Liste 2 ' deki görünüm aslında basit bir şekilde yapılıyor. Görünüm yalnızca geçerli saati görüntüler. Ancak, bir dizi veritabanı kaydını görüntüleyen bir görünümü kolayca önbelleğe alabilirsiniz. Bu durumda, veritabanı kayıtlarının her biri veritabanından alınması gerekmez ve bu da görünümü döndüren denetleyici eylemi çağrılır. Önbelleğe alma, hem Web sunucunuzun hem de veritabanı sunucunuzun gerçekleştirmesi gereken iş miktarını azaltabilir.

MVC görünümünde% @ OutputCache%&gt; yönergesini &lt;sayfasını kullanmayın. Bu yönerge Web Forms dünyadan erişilebilir ve bir ASP.NET MVC uygulamasında kullanılmamalıdır.

## <a name="where-content-is-cached"></a>Içeriğin önbelleğe alındığı yer

Varsayılan olarak, [OutputCache] özniteliğini kullandığınızda içerik üç konumda önbelleğe alınır: Web sunucusu, tüm proxy sunucular ve Web tarayıcısı. [OutputCache] özniteliğinin Location özelliğini değiştirerek içeriğin önbelleğe alındığını tam olarak denetleyebilirsiniz.

Location özelliğini aşağıdaki değerlerden herhangi birine ayarlayabilirsiniz:

> · Kaydedilmemiş
> 
> · İstemcilerinin
> 
> · Akış
> 
> · Server
> 
> · Seçim
> 
> · Sunucuandclient

Varsayılan olarak, Location özelliği herhangi bir değere sahiptir. Ancak, yalnızca tarayıcıda veya yalnızca sunucuda önbelleğe almak isteyebileceğiniz durumlar vardır. Örneğin, her kullanıcı için kişiselleştirilmiş bilgileri önbelleğe alırsanız, bu bilgileri sunucuda önbelleğe almalısınız. Farklı kullanıcılara farklı bilgiler görüntülüyorsanız, bu bilgileri yalnızca istemcide önbelleğe almalısınız.

Örneğin, Listeleme 3 ' teki denetleyici, geçerli kullanıcı adını döndüren GetName () adlı bir eylem gösterir. Jak Web sitesinde oturum açar ve GetName () eylemini çağırsa, eylem "Hi jak" dizesini döndürür. Daha sonra, Jill Web sitesinde oturum açar ve GetName () eylemini çağırsa, "Hi jak" dizesini de alır. Bu dize, jak ilk olarak denetleyici eylemini çağırdıktan sonra tüm kullanıcılar için Web sunucusunda önbelleğe alınır.

**Listeleme 3 – Controllers\BadUserController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample3.cs)]

Büyük olasılıkla, Listeleme 3 ' teki denetleyici istediğiniz şekilde çalışmaz. "Hi jak" iletisini Jill 'e göstermek istemezsiniz.

Kişiselleştirilmiş içeriği hiçbir şekilde sunucu önbelleğinde önbelleğe almalısınız. Ancak, performansı artırmak için tarayıcı önbelleğindeki kişiselleştirilmiş içeriği önbelleğe almak isteyebilirsiniz. İçeriği tarayıcıda önbelleğe alırsanız ve bir kullanıcı aynı denetleyici eylemini birden çok kez çağırdıysanız, içerik sunucu yerine tarayıcı önbelleğinden alınabilir.

4\. listede değiştirilen denetleyici, GetName () eyleminin çıkışını önbelleğe alır. Ancak, içerik sunucuda değil yalnızca tarayıcıda önbelleğe alınır. Bu şekilde, birden çok Kullanıcı GetName () yöntemini çağırdığında, her kişi başka birinin Kullanıcı adını değil kendi kullanıcı adlarını alır.

**Listeleme 4 – Controllers\UserController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample4.cs)]

Kod 4 ' teki [OutputCache] özniteliğinin OutputCacheLocation. Client değerine ayarlanmış bir Location özelliği içerdiğine dikkat edin. [OutputCache] özniteliği bir NoStore özelliği de içerir. NoStore özelliği, proxy sunuculara ve tarayıcıya önbelleğe alınmış içeriğin kalıcı bir kopyasını saklamamasını sağlamak için kullanılır.

## <a name="varying-the-output-cache"></a>Çıktı önbelleğini değiştirme

Bazı durumlarda, aynı içeriğin farklı önbelleğe alınmış sürümlerini isteyebilirsiniz. Örneğin, ana/ayrıntı sayfası oluşturduğunuzu düşünün. Ana sayfa, film başlıklarının bir listesini görüntüler. Bir başlığa tıkladığınızda, seçili filmin ayrıntılarını alırsınız.

Ayrıntılar sayfasını önbelleğe alırsanız, aynı filmin ayrıntıları hangi filmi tıkladıysanız olsun görüntülenir. İlk Kullanıcı tarafından seçilen ilk film, gelecekteki tüm kullanıcılara görüntülenecektir.

[OutputCache] özniteliğinin VaryByParam özelliğinden yararlanarak bu sorunu çözebilirsiniz. Bu özellik, bir form parametresi veya sorgu dizesi parametresi değiştiğinde çok aynı içeriğin önbelleğe alınmış farklı sürümlerini oluşturmanızı sağlar.

Örneğin, Listeleme 5 ' teki denetleyici ana () ve ayrıntılar () adlı iki eylemi ortaya koyar. Master () eylemi bir film başlıkları listesi döndürür ve ayrıntılar () eylemi seçili filmin ayrıntılarını döndürür.

**Listeleme 5 – Controllers\MoviesController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample5.cs)]

Master () eylemi, "none" değerine sahip bir VaryByParam özelliği içerir. Master () eylemi çağrıldığında, ana görünümün aynı önbelleğe alınmış sürümü döndürülür. Herhangi bir form parametresi veya sorgu dizesi parametresi yok sayılır (bkz. Şekil 2).

**Şekil 2 –/Movies/Master görünümü**

![clip_image004](improving-performance-with-output-caching-cs/_static/image2.jpg)

**Şekil 3 –/Movies/Details görünümü**

![clip_image006](improving-performance-with-output-caching-cs/_static/image3.jpg)

Details () eylemi, "ID" değerine sahip bir VaryByParam özelliği içerir. Kimlik parametresinin farklı değerleri denetleyici eylemine geçirildiğinde, Ayrıntılar görünümünün farklı önbelleğe alınmış sürümleri oluşturulur.

VaryByParam özelliğini kullanarak daha fazla önbelleğe alma ve daha az bilgi elde edilmesi gerektiğini anlamak önemlidir. Her farklı kimlik parametresinin sürümü için Ayrıntılar görünümünün farklı bir önbelleğe alınmış sürümü oluşturulur.

VaryByParam özelliğini aşağıdaki değerlere ayarlayabilirsiniz:

> \* = bir form veya sorgu dizesi parametresi değiştiğinde farklı bir önbelleğe alınmış sürüm oluşturun.
> 
> hiçbiri = hiçbir şekilde farklı önbelleğe alınmış sürümler oluşturma
> 
> Parametrelerin noktalı virgül listesi = bir form veya sorgu dizesi parametrelerinden herhangi biri değiştiğinde farklı önbelleğe alınmış sürümler oluştur

## <a name="creating-a-cache-profile"></a>Önbellek profili oluşturma

[OutputCache] özniteliğinin özelliklerini değiştirerek çıktı önbelleği özelliklerini yapılandırmaya alternatif olarak, Web yapılandırma (Web. config) dosyasında bir önbellek profili oluşturabilirsiniz. Web yapılandırma dosyasında bir önbellek profili oluşturmak birkaç önemli avantaj sunar.

İlk olarak, Web yapılandırma dosyasında çıktı önbelleği yapılandırarak, denetleyici eylemlerinin içeriği tek bir merkezi konumda nasıl önbelleğe kullandığını denetleyebilirsiniz. Tek bir önbellek profili oluşturabilir ve profili çeşitli denetleyicilere veya denetleyici eylemlerine uygulayabilirsiniz.

İkincisi, uygulamanızı yeniden derlemeden Web yapılandırma dosyasını değiştirebilirsiniz. Üretime zaten dağıtılan bir uygulama için önbelleğe almayı devre dışı bırakmanız gerekirse, Web yapılandırma dosyasında tanımlanan önbellek profillerini de değiştirebilirsiniz. Web yapılandırma dosyasında yapılan tüm değişiklikler otomatik olarak algılanır ve uygulanır.

Örneğin &lt;, liste 6 ' daki önbelleğe alma&gt; Web yapılandırması bölümü, Cache1Hour adlı bir önbellek profilini tanımlar. &lt;önbelleğe alma&gt; bölümü, bir Web yapılandırma dosyasının &lt;System. Web&gt; bölümü içinde yer almalıdır.

**Listeleme 6 – Web. config için önbelleğe alma bölümü**

[!code-xml[Main](improving-performance-with-output-caching-cs/samples/sample6.xml)]

7 dökümdeki denetleyici, Cache1Hour profilini [OutputCache] özniteliğiyle bir denetleyici eylemine nasıl uygulayacağınızı gösterir.

**Listeleme 7 – Controllers\ProfileController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample7.cs)]

Döküm 7 ' de denetleyicinin açığa çıkarılan dizin () eylemini çağırırsanız, 1 saat boyunca aynı süre döndürülür.

## <a name="summary"></a>Özet

Çıktı önbelleği, ASP.NET MVC uygulamalarınızın performansını önemli ölçüde iyileştirmeye yönelik çok kolay bir yöntem sağlar. Bu öğreticide, denetleyici eylemlerinin çıkışını önbelleğe almak için [OutputCache] özniteliğini nasıl kullanacağınızı öğrendiniz. Ayrıca, içeriğin nasıl önbelleğe alınacağını değiştirmek için Duration ve VaryByParam özellikleri gibi [OutputCache] özniteliğinin özelliklerinin nasıl değiştirileceğini öğrenirsiniz. Son olarak, Web yapılandırma dosyasında önbellek profillerinin nasıl tanımlanacağını öğrendiniz.

> [!div class="step-by-step"]
> [Önceki](understanding-action-filters-cs.md)
> [İleri](adding-dynamic-content-to-a-cached-page-cs.md)
