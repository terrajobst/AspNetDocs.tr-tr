---
uid: whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application
title: 'Nasıl yapılır: ASP.NET Web Forms/MVC uygulamanıza mobil sayfa ekleme | Microsoft Docs'
author: rick-anderson
description: Bu, ASP.NET Web Forms/MVC uygulamanızdan mobil cihazlar için en iyi duruma getirilmiş sayfaları kullanmanın çeşitli yollarını açıklar ve mimari ve...
ms.author: riande
ms.date: 01/20/2011
ms.assetid: 3124f28e-cc32-418a-afe3-519fa56f4c36
msc.legacyurl: /whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application
msc.type: content
ms.openlocfilehash: 63c555358d06a9506bb5c8c993800c3307108192
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78572739"
---
# <a name="how-to-add-mobile-pages-to-your-aspnet-web-forms--mvc-application"></a>Nasıl Yapılır: ASP.NET Web Forms/MVC Uygulamanıza Mobil Sayfalar Ekleme

> **Uygulama hedefi**
> 
> - ASP.NET Web Forms 4,0 sürümü
> - ASP.NET MVC sürüm 3,0
> 
> **Özet**
> 
> Bu, mobil cihazlar için en iyi duruma getirilmiş sayfaları ASP.NET Web Forms/MVC uygulamanızdan sunmanın çeşitli yollarını açıklar ve çok sayıda cihazı hedeflerken göz önünde bulundurmanız gereken mimari ve tasarım sorunları sunar. Bu belgede, ASP.NET 2,0 ' den 3,5 ' ye ASP.NET Mobile denetimlerinin neden artık kullanılmıyor olduğunu ve bazı modern alternatifleri ele alınmaktadır.

## <a name="contents"></a>İçindekiler

- Genel bakış
- Mimari seçenekleri
- Tarayıcı ve cihaz algılama
- ASP.NET Web Forms uygulamalar, mobil 'e özgü sayfaları nasıl sunabilir?
- ASP.NET MVC uygulamalarının mobil 'e özgü sayfaları nasıl sunabilir
- Ek kaynaklar

Bu teknik incelemeyi hem ASP.NET Web Forms hem de MVC 'nin tekniklerini gösteren indirilebilir kod örnekleri için, bkz. [ASP.NET ile Mobile Apps & siteleri](https://docs.microsoft.com/aspnet/mobile/overview).

## <a name="overview"></a>Genel bakış

Mobil cihazlar – akıllı telefonlar, özellik telefonları ve tabletler: Web 'e erişmek için bir yol olarak popülerliği büyümeye devam edin. Birçok web geliştiricisi ve Web odaklı işletme için, bu cihazları kullanan ziyaretçiler için harika bir tarama deneyimi sağlamak daha fazla önemli olduğu anlamına gelir.

### <a name="how-earlier-versions-of-aspnet-supported-mobile-browsers"></a>ASP.NET desteklenen mobil tarayıcıların önceki sürümleri

ASP.NET 2,0 sürümleri 3,5 dahil *ASP.NET mobil denetimleri*: *System. Web. Mobile. dll* derlemesinde ve *System. Web. UI. MobileControls* ad alanındaki mobil cihazlar için bir dizi sunucu denetimi. Derleme ASP.NET 4 ' te hala dahil edilmiştir, ancak kullanım dışıdır. Geliştiricilerin, bu kağıda açıklananlar gibi daha modern yaklaşımlara geçirilmesi önerilir.

ASP.NET Mobile denetimlerinin kullanım dışı olarak işaretlenmesinin nedeni, tasarımının 2005 ve önceki sürümlerde ortak olan cep telefonlarına yönlendirilmesine neden olur. Denetimler, genellikle bu çağın WAP tarayıcılarında WML veya cHTML işaretlemesini (normal HTML yerine) işlemek için tasarlanmıştır. Ancak WAP, WML ve cHTML artık çoğu proje için uygun değildir, çünkü HTML artık mobil ve masaüstü tarayıcıları için ubititous biçimlendirme diline benzer.

### <a name="the-challenges-of-supporting-mobile-devices-today"></a>Mobil cihazları bugün destekleme sorunları

Mobil tarayıcılar artık HTML 'yi neredeyse evrensel olarak desteklese de harika mobil gözatma deneyimleri oluşturmak için çok fazla zorluk gösterirsiniz:

- ***Ekran boyutu*** -mobil cihazlar, formda önemli ölçüde farklılık gösterir ve ekranlar genellikle masaüstü izleyicilerinden çok daha küçüktür. Bu nedenle, bunlar için tamamen farklı sayfa düzenleri tasarlamanız gerekebilir.
- ***Giriş yöntemleri*** – bazı cihazlarda anahtar reklamları vardır, bazıları stilize bir, diğerleri de Touch kullanır. Birden çok gezinti mekanizmasını ve veri giriş yöntemlerini dikkate almanız gerekebilir.
- ***Standartlar uyumluluğu*** : birçok mobil tarayıcı, en son HTML, CSS veya JavaScript standartlarını desteklemez.
- ***Bant genişliği*** – hücresel veri ağı performansı yayana farklılık gösterir ve bazı son kullanıcılar megabayt ile ücretlendirerek tariffs üzerinde yer alır.

Tek boyuta uyan bir çözüm yoktur; Uygulamanızın ona erişen cihaza göre farklı şekilde görünmesi ve davranması gerekecektir. İstediğiniz mobil destek düzeyine bağlı olarak, bu, Web geliştiricileri için "tarayıcı çatışmaları" olan herhangi bir zaman daha büyük bir zorluk olabilir.

Mobil tarayıcı desteği 'ne ilk kez yaklaştığı geliştiriciler genellikle en son ve en karmaşık akıllı telefonu (ör. Windows Phone 7, iPhone veya Android) desteklemeye yöneliktir, ancak geliştiriciler genellikle kişisel olarak cihazlarınız. Ancak, kimaper telefonlar son derece popüler olur ve sahipleri, özellikle de mobil telefonların bir geniş bant bağlantısından daha kolay olduğu ülkelerde Web 'e gözatabilmeleri için bunları kullanır. İşletmenizin, olası müşterileri göz önünde bulundurarak hangi cihaz yelpazesini destekleyeceği gerektiğine karar vermeniz gerekir. Bir merkezlerini sistem durumu Spa için çevrimiçi bir broşür oluşturuyorsanız, yalnızca gelişmiş akıllı telefonların hedeflemesini sağlamak için bir iş kararı verebilir, ancak bir Cinema için bir bilet kayıt sistemi oluşturuyorsanız, muhtemelen daha az güçlü özelliği olan ziyaretçiler için hesap yapmanız gerekir telefonlarının.

## <a name="architectural-options"></a>Mimari seçenekleri

ASP.NET Web Forms veya MVC 'nin belirli teknik ayrıntılarına geçmeden önce, genel olarak Web geliştiricilerinin mobil tarayıcıları desteklemeye yönelik üç ana olası seçeneği olduğunu unutmayın:

1. ***Hiçbir şey yapmayın –*** Tek yapmanız gereken standart, masaüstü yönelimli bir Web uygulaması oluşturabilir ve mobil tarayıcılarına güvenebilirsiniz. 

    - **Avantaj**: ek bir iş olmaması ve bakımını yapmak için en ucuz seçenektir
    - **Dezavantajı**: en kötü Son Kullanıcı deneyimini sağlar: 

        - En son smartphone 'lar, HTML 'nizin yanı sıra bir masaüstü tarayıcısı da oluşturabilir, ancak kullanıcılarınız, içeriğinizi küçük bir ekran üzerinde kullanmak için yatay ve dikey olarak yakınlaştırmak ve kaydırmak için zorlanacak. Bu en iyi.
        - Daha eski cihazlar ve özellik telefonları, işaretlemelerinizi tatmin edici bir şekilde işleyemeyebilir.
        - En son Tablet cihazlarında bile (ekranlar dizüstü bilgisayar ekranları kadar büyük olabilir), farklı etkileşim kuralları uygulanır. Dokunma tabanlı giriş en iyi, daha büyük düğmeler ve bağlantılarla birlikte daha fazla kullanılabilir ve bir fare imlecini bir anlık menü üzerine gelme yolu yoktur.
2. ***İstemci üzerindeki sorunu çözün***  ; CSS ve [aşamalı geliştirmelerden](http://en.wikipedia.org/wiki/Progressive_enhancement) dikkatli bir şekilde kullanılması, hangi tarayıcıya sahip olduğunu uyarlayacak biçimlendirme, stiller ve betikler oluşturabilirsiniz. Örneğin, [CSS 3 medya sorgularıyla](http://www.w3.org/TR/2010/CR-css3-mediaqueries-20100727/), ekranları seçili eşikten daha dar olan cihazlarda tek bir sütun düzenine dönüşen çok sütunlu bir düzen oluşturabilirsiniz. 

    - **Avantaj**: sahip oldukları ekran ve giriş özelliklerine göre bilinmeyen gelecekteki cihazlarda bile, kullanımda olan belirli bir cihaz için işlemeyi iyileştirir
    - **Avantaj**: tüm cihaz türlerinde sunucu tarafı mantığını kolayca paylaşmanızı sağlar; kod veya çaba için en az çoğaltma
    - **Dezavantajı**: mobil cihazlar, mobil sayfalarınızın masaüstü sayfalarınızda tamamen farklı olmasını isteyebileceğiniz ve farklı bilgileri gösteren masaüstü cihazlarından farklıdır. Bu tür Çeşitlemeler, özellikle CSS aracılığıyla robustly ulaşmak için verimsiz veya imkansız olabilir, özellikle de ne kadar eski cihazların CSS kurallarını yorumlamasını sağlar. Bu, özellikle CSS 3 özniteliklerinin bir kısmını doğrudur.
    - **Dezavantajı**: farklı cihazlarda sunucu tarafı mantığı ve iş akışları için destek sağlamaz. Örneğin, mobil kullanıcılara yönelik basitleştirilmiş bir alışveriş sepeti kullanıma alma iş akışını yalnızca CSS aracılığıyla uygulayabilirsiniz.
    - **Dezavantajı**: verimsiz bant genişliği kullanımı. Hedef cihaz yalnızca bu bilgilerin bir alt kümesini kullanmasına rağmen, sunucu tüm olası cihazlara uygulanan biçimlendirme ve stilleri iletmede olabilir.
3. ***Sorunu sunucuda çözün* –** Sunucunuz, cihaza hangi cihazın eriştiğini veya ekran boyutu ve giriş yöntemi gibi en azından bu aygıtın özelliklerine ve bir mobil cihaz olup olmadığına biliyorsa, farklı mantık çalıştırabilir ve farklı HTML işaretlemesi gerçekleştirebilir. 

    - **Avantajı:** En yüksek esneklik. Kaydettiğinde için sunucu tarafı mantığınızı ne kadar farklılık gösterebileceğinizi veya istediğiniz cihaza özgü düzen için biçiminizi en üst düzeye çıkarmanıza izin yoktur.
    - **Avantajı:** Verimli bant genişliği kullanımı. Yalnızca hedef cihazın kullanacağı biçimlendirme ve stil bilgilerini iletmede ihtiyacınız vardır.
    - **Dezavantajı:** Bazen çabaların veya kodun tekrarlanmasını zorlar (örn., Web Forms sayfalarınızın veya MVC görünümlerinizin benzer ancak biraz farklı kopyalarını oluşturmanızı sağlar). Mümkün olduğunda, ortak mantığı temel bir katman veya hizmette çarpanlara katyacaksınız, ancak yine de Kullanıcı arabirimi kodunuzun veya biçimlendirmesinin bazı bölümlerinin tekrarlanmış olması ve paralel olarak tutulması gerekebilir.
    - **Dezavantajı:** Cihaz Algılama önemsiz bir değer değil. Bilinen cihaz türlerinin bir listesini veya veritabanını ve bunların özelliklerini (her zaman tam olarak güncel olmayabilir) gerektirir ve gelen tüm istekleri doğru bir şekilde eşleştirmek için garanti edilmez. Bu belgede daha sonra bazı seçenekler ve bunların sınırları açıklanmaktadır.

En iyi sonuçları elde etmek için çoğu geliştirici, (2) ve (3) seçeneklerini birleştirmeleri gerektiğini bulur. Küçük biçimsel farklılıklar, CSS veya hatta JavaScript kullanan istemcide en iyi şekilde veri, iş akışı veya biçimlendirme üzerinde önemli farklılıklar sunucu tarafı kodunda en etkili şekilde uygulanır.

### <a name="this-paper-focuses-on-server-side-techniques"></a>Bu sayfa, sunucu tarafı tekniklerine odaklanır

ASP.NET Web Forms ve MVC birincil olarak sunucu tarafı teknolojilerinde olduğundan, bu Teknik İnceleme, mobil tarayıcılar için farklı biçimlendirme ve mantık üretmenize olanak tanıyan sunucu tarafı tekniklerine odaklanacaktır. Kuşkusuz, bunu herhangi bir istemci tarafı tekniğinden (örneğin, CSS 3 medya sorguları, aşamalı geliştirme JavaScript 'i) birleştirebilir, ancak bu çok daha fazla web tasarımı ASP.NET geliştirmeye göre daha fazla olabilir.

## <a name="browser-and-device-detection"></a>Tarayıcı ve cihaz algılama

Mobil cihazları desteklemek için tüm sunucu tarafı teknikleri için temel önkoşul, ziyaretçinizin hangi cihazla kullandığını bilmektedir. Aslında, söz konusu Cihazın üretici ve model numarasını bilmenin, cihazın *özelliklerini* öğrendiğinden de daha iyi bir seçenektir. Özellikler şunlar olabilir:

- Bu bir mobil cihaz mi?
- Input yöntemi (fare/klavye, dokunmatik, tuş takımı, oyun çubuğu,...)
- Ekran boyutu (fiziksel ve piksel olarak)
- Desteklenen medya ve veri biçimleri
- Etc.

Daha sonra gelecekteki cihazları işlemek için daha iyi bir şekilde donatılmış olacak şekilde, kararları model numarasına göre özelliklere göre yapmak daha iyidir.

### <a name="using-aspnets-built-in-browser-detection-support"></a>ASP. NET 'in yerleşik tarayıcı algılama desteği

ASP.NET Web Forms ve MVC geliştiricileri, *istek. Browser* nesnesinin özelliklerini inceleyerek, ziyaret eden bir tarayıcının önemli özelliklerini hemen bulabilir. Örneğin, bkz.

- Request.Browser.IsMobileDevice
- İstek. Browser. MobileDeviceManufacturer, Request. Browser. MobileDeviceModel
- Request. Browser. Screenpixelyüzdth
- Request.Browser.SupportsXmlHttp
- ...ve diğer birçok

Arka planda ASP.NET platformu, bir tarayıcı tanımı XML dosyaları kümesindeki normal ifadelerle gelen *Kullanıcı Aracısı* (UA) http üstbilgisiyle eşleşir. Varsayılan olarak, platform birçok yaygın mobil cihaz için tanımlar içerir ve tanımak istediğiniz diğerleri için özel tarayıcı tanım dosyaları ekleyebilirsiniz. Daha ayrıntılı bilgi için bkz. MSDN sayfası [ASP.NET Web sunucusu denetimleri ve tarayıcı özellikleri](https://msdn.microsoft.com/library/x3k2ssx2.aspx).

### <a name="using-the-wurfl-device-database-via-51degreesmobi-foundation"></a>51Degrees.mobi Foundation aracılığıyla WURFL cihaz veritabanını kullanma

ASP. NET 'in yerleşik tarayıcı algılama desteği birçok uygulama için yeterli olacaktır, bu, yeterince önemli olmayan iki ana durum olabilir:

- ***En son cihazları***(bunlar Için tarayıcı tanım dosyalarını el ile oluşturmadan) tanımak istiyorsunuz. .NET 4 ' ün tarayıcı tanımı dosyalarının Windows Phone 7, Android telefonlar, Opera mobil tarayıcıları veya Apple iPads tanıması için yeterince güncel olmadığına unutmayın.
- ***Cihaz özellikleri hakkında daha ayrıntılı bilgi almanız gerekir***. Bir cihazın giriş yöntemi (örneğin, dokunma-tuş takımı) veya tarayıcının desteklediği ses biçimlerini bilmeniz gerekebilir. Bu bilgiler standart tarayıcı tanım dosyalarında kullanılamaz.

[ *Kablosuz Evrensel kaynak dosyası* (WURFL) projesi](http://wurfl.sourceforge.net/) , günümüzde kullanımda olan mobil cihazlarla ilgili çok daha güncel ve ayrıntılı bilgiler sağlar.

.NET geliştiricileri için harika haberler, ASP. NET ' in tarayıcı algılama özelliği Genişletilebilir, bu nedenle bu sorunları aşmak için geliştirmek mümkündür. Örneğin, açık kaynak [*51Degrees.mobi Foundation*](https://github.com/51Degrees/dotNET-Device-Detection) kitaplığını projenize ekleyebilirsiniz. Bu, ASP.NET IHttpModule veya tarayıcı yetenekleri sağlayıcısıdır (hem Web Forms hem de MVC uygulamalarında kullanılabilir), böylece doğrudan WURFL verilerini okur ve ASP 'ye takar. NET 'in yerleşik tarayıcı algılama mekanizması. Modülünü yükledikten sonra, *istek. Browser* daha önce çok daha doğru ve ayrıntılı bilgiler içerir: daha önce bahsedilen cihazların çoğunu doğru bir şekilde algılar ve yeteneklerini (giriş yöntemi gibi ek yetenekler dahil) listeler. Daha fazla ayrıntı için projenin belgelerine bakın.

## <a name="how-web-forms-applications-can-present-mobile-specific-pages"></a>Web Forms uygulamalar, mobil 'e özgü sayfalar sunabilir

Varsayılan olarak, yepyeni bir Web Forms uygulamasının yaygın mobil cihazlarda nasıl görüntüleyeceği aşağıda verilmiştir:

![](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/_static/image1.png)

Açıkça, düzen çok mobil kullanımı kolay görünmüyor – Bu sayfa, küçük ve dikey yönelimli bir ekran için değil, büyük, yatay yönelimli bir izleyici için tasarlanmıştır. Böylece ne yapabilirsiniz?

Bu yazıda daha önce anlatıldığı gibi, sayfalarınızı mobil cihazlara uyarlamak için birçok yol vardır. Bazı teknikler sunucu tabanlıdır, diğerleri ise istemci üzerinde çalışır.

### <a name="creating-a-mobile-specific-master-page"></a>Mobil olarak özel ana sayfa oluşturma

Gereksinimlerinize bağlı olarak, tüm ziyaretçiler için aynı Web Forms kullanabilir, ancak biri masaüstü ziyaretçileri için bir diğeri de mobil ziyaretçiler için bir tane olabilir. Bu, herhangi bir sayfa mantığını çoğaltmadan, CSS stil sayfasını veya en üst düzey HTML biçimlerinizi mobil cihazlara uyacak şekilde değiştirme esnekliği sağlar.

Bu kolay bir işlemdir. Örneğin, bir Web formuna aşağıdaki gibi bir PreInit işleyicisi ekleyebilirsiniz:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample1.cs)]

Şimdi, uygulamanızın en üst düzey klasöründe Mobile. Master adlı bir ana sayfa oluşturun ve bir mobil cihaz algılandığında kullanılacaktır. Mobil ana sayfanız, gerekirse, mobil 'e özgü CSS stil sayfasına başvurabilir. Masaüstü ziyaretçileri, mobil olanı değil varsayılan ana sayfanızı görmeye devam eder.

### <a name="creating-independent-mobile-specific-web-forms"></a>Bağımsız mobil özel Web Forms oluşturma

En yüksek esneklik için, farklı cihaz türleri için ayrı ana sayfalar kullanmaktan çok daha fazla gidebilirsiniz. İki *ayrı Web Forms sayfa* kümesi uygulayabilirsiniz: masaüstü tarayıcıları için bir küme, farklı bir Mobiles kümesi. Mobil ziyaretçilere çok farklı bilgiler veya iş akışları sunmak istiyorsanız bu en iyi sonucu verir. Bu bölümün geri kalanında bu yaklaşım ayrıntılı olarak açıklanmaktadır.

Masaüstü tarayıcıları için tasarlanan bir Web Forms uygulamasına zaten sahip olduğunuz varsayılarak, devam etmenin en kolay yolu projeniz içinde "mobil" adlı bir alt klasör oluşturmak ve mobil sayfalarınızı burada oluşturmaktır. Tüm alt siteleri, kendi ana sayfaları, stil sayfaları ve sayfalarla, diğer tüm Web Forms uygulamaları için kullandığınız tekniklerin aynısını kullanarak oluşturabilirsiniz. Masaüstü sitenizdeki *her* sayfa için bir mobil eşdeğer oluşturmanız gerekmez; Hangi işlev alt kümesinin mobil ziyaretçiler için anlamlı olduğunu seçebilirsiniz.

Mobil sayfalarınız, isterseniz normal sayfalarınızın ortak statik kaynaklarını (görüntüler, JavaScript veya CSS dosyaları gibi) paylaşabilir. "Mobil" klasörünüz, IIS 'de barındırılırken ayrı bir uygulama olarak *işaretlenmeyecektir (* Web Forms sayfaların yalnızca basit bir alt klasörü), aynı yapılandırmayı, oturum verilerini ve diğer altyapıyı masaüstü sayfalarınız olarak da paylaşır.

> [!NOTE]
> Bu yaklaşım genellikle kodun tekrarlanmasını içerdiğinden (mobil sayfaların masaüstü sayfalarıyla bazı benzerlikler paylaştığı için), ortak iş mantığını veya veri erişim kodunu paylaşılan bir temel katman veya hizmete katmamak önemlidir. Aksi takdirde, uygulamanızı oluşturma ve sürdürme çabasıyla karşılaşırsınız.

#### <a name="redirecting-mobile-visitors-to-your-mobile-pages"></a>Mobil ziyaretçileri mobil sayfalarınıza yönlendirme

Mobil ziyaretçileri, yalnızca gözatma oturumundaki *ilk* istek üzerine (ve oturumunda her istekte değil) yalnızca mobil sayfalara yönlendirmek kullanışlıdır, çünkü:

- Daha sonra, mobil ziyaretçilerin masaüstü sayfalarınıza kolayca erişmelerini isterseniz, Ana sayfanıza "masaüstü sürümü" ye giden bir bağlantı koyabilirsiniz. Ziyaretçi, artık oturumunda ilk istek olmadığı için bir mobil sayfaya geri yönlendirilmeyecektir.
- Sitenizin masaüstü ve mobil bölümleri arasında paylaşılan Dinamik kaynaklar için isteklerle müdahale olma riskini ortadan kaldırır (örn., sitenin hem masaüstü hem de mobil bölümlerinin IFRAME 'de veya belirli Ajax işleyicilerde görüntüleyeceği ortak bir Web formunuz varsa)

Bunu yapmak için, yönlendirme mantığınızı bir **oturum\_başlangıç** yöntemine yerleştirebilirsiniz. Örneğin, Global.asax.cs dosyanıza aşağıdaki yöntemi ekleyin:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample2.cs)]

#### <a name="configuring-forms-authentication-to-respect-your-mobile-pages"></a>Mobil sayfalarınıza göre form kimlik doğrulamasını yapılandırma

Form kimlik doğrulamasının, kimlik doğrulama işleminden sonra ve sonrasında ziyaretçilerin yeniden yönlendirilebileceği belirli varsayımlar olduğunu unutmayın:

- Bir kullanıcının kimlik doğrulaması yapması gerektiğinde, Forms kimlik doğrulaması, masaüstü veya mobil kullanıcı olup olmadıkları (yalnızca *bir oturum açma URL 'si kavramı* olduğu için) ne olursa olsun onları masaüstü oturum açma sayfanıza yönlendirecektir. Mobil oturum açma sayfanıza farklı şekilde stil eklemek istediğiniz varsayılarak, mobil kullanıcıları ayrı bir mobil oturum açma sayfasına yönlendirmeleri için masaüstü oturum açma sayfanızı geliştirmenin olması gerekir. Örneğin, aşağıdaki kodu **Masaüstü** oturum açma sayfanızın arka plan koduna ekleyin: 

    [!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample3.cs)]
- Kullanıcı başarıyla oturum açtıktan sonra, Forms kimlik doğrulaması varsayılan olarak bunları Masaüstü giriş sayfanıza yönlendirir (yalnızca *bir* varsayılan sayfa kavramı olduğundan). Başarılı bir oturum açma işleminden sonra mobil giriş sayfasına yeniden yönlendirmeleri için mobil oturum açma sayfanızı geliştirdiğinizden emin olmanız gerekir. Örneğin, aşağıdaki kodu **Mobil** oturum açma sayfanızın arka plan koduna ekleyin: 

    [!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample4.cs)]
  
  Bu kod, sayfanızın varsayılan proje şablonunda olduğu gibi, LoginUser adlı bir oturum açma sunucusu denetimine sahip olduğunu varsayar.

### <a name="working-with-output-caching"></a>Çıktı önbelleği ile çalışma

Çıktı önbelleği kullanıyorsanız, varsayılan olarak, bir masaüstü kullanıcının belirli bir URL 'yi ziyaret etmesini (çıktısının önbelleğe alınmasına neden olur) ve ardından önbelleğe alınmış masaüstü çıkışını alan bir mobil kullanıcı tarafından daha sonra bu şekilde olduğunu unutmayın. Bu uyarı, ana sayfanızı cihaz türüne göre mi yoksa ya da cihaz türü başına tamamen ayrı Web Forms uygulama gibi bir şekilde uygular.

Sorunu önlemek için, ziyaretçilerin bir mobil cihaz kullanıp kullanmadığını göre önbellek girdisini değiştirmek için ASP.NET bildirebilirsiniz. Sayfanızın OutputCache bildirimine aşağıdaki şekilde bir VaryByCustom parametresi ekleyin:

[!code-aspx[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample5.aspx)]

Sonra, Global.asax.cs dosyanıza aşağıdaki yöntemi geçersiz kılmayı ekleyerek *IsMobileDevice* 'ı özel bir önbellek parametresi olarak tanımlayın:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample6.cs)]

Bu, sayfada bulunan mobil ziyaretçilerin bir masaüstü ziyaretçisi tarafından daha önce önbelleğe yerleştirmemesini sağlar.

### <a name="a-working-example"></a>Çalışan bir örnek

Bu teknikleri bu şekilde görmek için [Bu teknik incelemeye ait kod örneklerini](https://docs.microsoft.com/aspnet/mobile/overview)indirin. Web Forms örnek uygulama, mobil kullanıcıları mobil adlı bir alt klasördeki mobil olarak belirli bir sayfaya otomatik olarak yönlendirir. Aşağıdaki ekran görüntüleriyle görebileceğiniz gibi, bu sayfaların biçimlendirmesi ve stili, mobil tarayıcılar için daha iyi iyileştirilmiştir:

![](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/_static/image2.png)

Mobil tarayıcılar için biçimlendirme ve CSS 'nizi iyileştirme hakkında daha fazla ipucu için, bu belgenin devamındaki "mobil tarayıcılar için mobil sayfaları stillendirme" bölümüne bakın.

## <a name="how-aspnet-mvc-applications-can-present-mobile-specific-pages"></a>ASP.NET MVC uygulamalarının mobil 'e özgü sayfaları nasıl sunabilir

Model-Görünüm-denetleyici modeli, uygulama mantığını (görünümlerde) sunum mantığından (görünümlerde) ayırdığından, sunucu tarafı kodundaki mobil desteği işlemek için aşağıdaki yaklaşımlardan herhangi birini seçebilirsiniz:

1. ***hem masaüstü hem de mobil tarayıcılar için aynı denetleyicileri ve görünümleri kullanın, ancak bu görünümleri cihaz türüne bağlı olarak farklı Razor düzenlerine göre işlenir.** Bu seçenek, tüm cihazlarda özdeş veriler görüntülüyorsanız, ancak yalnızca farklı CSS stil sayfaları sağlamak veya Mobiles için birkaç üst düzey HTML öğesini değiştirmek istiyorsanız en iyi şekilde geçerlidir.
2. ***Hem masaüstü hem de mobil tarayıcılar için aynı denetleyicileri kullanın, ancak cihaz türüne bağlı olarak farklı görünümler işleyebilirsiniz***. Bu seçenek, kabaca aynı verileri görüntülerken ve son kullanıcılar için aynı iş akışlarını sağladıysanız en iyi şekilde kullanılır, ancak kullanılan cihaza uyacak şekilde çok farklı HTML biçimlendirmesi işlemek isteyebilir.
3. **Masaüstü ve mobil tarayıcılar için, her bir * için bağımsız denetleyiciler ve görünümler uygulayarak ayrı alanları oluşturun *.** Bu seçenek, farklı bilgiler içeren ve Kullanıcı cihaz türleri için iyileştirilmiş farklı iş akışlarıyla önde gelen çok farklı ekranlar görüntülüyorsanız en iyi şekilde geçerlidir. Kod yinelemesi anlamına gelebilir, ancak bunu temel bir katman veya hizmette ortak mantığı düzenleme göre küçültebilirsiniz.

**İlk** seçeneği alıp cihaz türü başına yalnızca Razor düzenine göre değişiklik yapmak istiyorsanız bu çok kolaydır. \_ViewStart. cshtml dosyanızı aşağıdaki gibi değiştirmeniz yeterlidir:

[!code-cshtml[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample7.cshtml)]

Artık, mobil cihazlar için iyileştirilmiş bir sayfa yapısı ve CSS kuralları ile \_LayoutMobile. cshtml adlı bir mobil özel düzen oluşturabilirsiniz.

**İkinci** seçeneği ziyaretçinin cihaz türüne göre tamamen farklı görünümler işlemek istiyorsanız, bkz. [Scott Hanselman 'ın blog gönderisi](http://www.hanselman.com/blog/ABetterASPNETMVCMobileDeviceCapabilitiesViewEngine.aspx).

Bu kağıdın geri kalanı, mobil cihazlar için ayrı denetleyiciler *ve* görünümler oluşturma başlıklı **üçüncü** seçeneğe odaklanmaktadır. böylece, mobil ziyaretçiler için işlevselliğin hangi alt kümesinin önerilmekte olduğunu kontrol edebilirsiniz.

### <a name="setting-up-a-mobile-area-within-your-aspnet-mvc-application"></a>ASP.NET MVC Uygulamanızda bir mobil alan ayarlama

Var olan bir ASP.NET MVC uygulamasına "mobil" adlı bir alanı normal şekilde ekleyebilirsiniz: Çözüm Gezgini içindeki proje adına sağ tıklayın ve ardından à alanı Ekle ' yi seçin. Daha sonra, ASP.NET MVC uygulamasındaki diğer tüm alanlar için yaptığınız gibi denetleyicileri ve görünümleri ekleyebilirsiniz. Örneğin, mobil ziyaretçilere bir giriş sayfası görevi gören yeni bir denetleyiciyi mobil bölgeye ekleyin.

### <a name="ensuring-the-url-mobile-reaches-the-mobile-homepage"></a>/Mobile URL 'sinin mobil giriş sayfasına ulaşmasını sağlama

/Mobile URL 'sinin mobil bölgenizdeki HomeController üzerindeki Dizin eylemine ulaşmasını istiyorsanız, yönlendirme yapılandırmanızda iki küçük değişiklik yapmanız gerekir. İlk olarak, aşağıdaki kodda gösterildiği gibi, HomeController 'ın mobil bölgenizdeki varsayılan denetleyici olması için MobileAreaRegistration sınıfınızı güncelleştirin:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample8.cs)]

Bu, mobil giriş sayfasının artık, Mobil sayfalar için örtük olarak varsayılan denetleyici adı olduğu için, "Home", artık varsayılan olarak/Mobile/Home yerine/Mobile konumunda yer alır.

Ardından, uygulamanıza ikinci bir HomeController ekleyerek (yani, mobil bir bilgisayar var olan masaüstüne ek olarak), normal masaüstü giriş sayfanız kopmuş olursunuz. "*Giriş ' adlı denetleyiciyle eşleşen birden çok tür bulundu*" hatasıyla başarısız olur. Bu sorunu çözmek için, en üst düzey yönlendirme yapılandırmanızı güncelleştirin (Global.asax.cs ' de), belirsizlik olduğunda Masaüstü HomeController 'ın öncelikli olması gerektiğini belirtmek için:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample9.cs)]

Artık hata bırakılır ve http: \/\/URL 'SI, *site*/Masaüstü giriş sayfasına ulaşmak için http: *\/\/.*

### <a name="redirecting-mobile-visitors-to-your-mobile-area"></a>Mobil ziyaretçileri mobil alanına yönlendirme

ASP.NET MVC 'de birçok farklı genişletilebilirlik noktası bulunur, bu nedenle yeniden yönlendirme mantığını eklemek için birçok olası yol vardır. Bir düzenlidir seçeneği, aşağıdaki koşullar karşılandığında bir yeniden yönlendirme gerçekleştiren [redirectmobiledevicestomobilearea] filtre özniteliği oluşturmaktır:

1. Kullanıcının oturumunda ilk istek (yani, Session. ınewsession, true eşittir)
2. İstek bir mobil tarayıcıdan geliyor (yani, Request. Browser. ımobiledevice true değerine eşittir)
3. Kullanıcı zaten mobil alanda bir kaynak isteğinde bulunmuyor (yani, URL 'nin *yol* bölümü/Mobile ile başlamıyor)

Bu teknik incelemeye eklenen indirilebilir örnek, bu mantığın bir uygulamasını içerir. Bu, bir yetkilendirme filtresi olarak uygulanır, bu, çıkış önbelleği kullanıyor olsanız bile düzgün bir şekilde çalışabileceği anlamına gelir. Aksi halde, bir masaüstü ziyaretçisi belirli bir URL 'ye eriştiğinde, masaüstü çıkışı önbelleğe alınıp şu şekilde hizmet verebilir sonraki mobil ziyaretçiler).

Filtre olduğundan, belirli denetleyicilere ve eylemlere uygulanmasını seçebilirsiniz, örneğin,

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample10.cs)]

… Alternatif olarak, Global.asax.cs dosyanıza MVC 3 *genel filtresi* olarak tüm denetleyicilere ve eylemlere uygulayabilirsiniz:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample11.cs)]

İndirilebilir örnek ayrıca, bu özniteliğin mobil bölgenizdeki belirli konumlara yönlendiren alt sınıflarının nasıl oluşturulacağını gösterir. Yani, örneğin şunları yapabilirsiniz:

- Mobil ziyaretçileri varsayılan olarak mobil giriş sayfasına gönderen yukarıda gösterildiği gibi genel bir filtre kaydedin.
- Ayrıca, mobil ziyaretçileri istedikleri ürün sayfasının mobil sürümüne götüren bir "ürünü görüntüle" eylemine özel bir [RedirectMobileDevicesToMobileProductPage] filtresi uygulayın.
- Ayrıca, belirli eylemlere filtrenin diğer özel alt sınıflarını da uygular ve mobil ziyaretçileri eşdeğer mobil sayfaya yeniden yönlendirebilir

### <a name="configuring-forms-authentication-to-respect-your-mobile-pages"></a>Mobil sayfalarınıza göre form kimlik doğrulamasını yapılandırma

Forms kimlik doğrulaması kullanıyorsanız, bir kullanıcının oturum açması gerektiğinde kullanıcıyı otomatik olarak tek bir "oturum açma" URL 'sine yeniden yönlendirdiğini ve varsayılan olarak **/Account/Logon**olduğunu unutmayın. Bu, mobil kullanıcıların masaüstünüze "oturum aç" eylemine yönlendirilebileceği anlamına gelir.

Bu sorundan kaçınmak için, mobil kullanıcıları mobil bir "oturum açma" eylemine yeniden yönlendirmeleri için masaüstünüze "oturum aç" eylemine mantık ekleyin. Varsayılan ASP.NET MVC uygulama şablonunu kullanıyorsanız, AccountController 'ın oturum açma eylemini aşağıdaki şekilde güncelleştirin:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample12.cs)]

… ve ardından mobil bölgenizdeki AccountController adlı bir denetleyicide, uygun bir mobil 'e özgü "oturum açma" eylemi uygulayın.

### <a name="working-with-output-caching"></a>Çıktı önbelleği ile çalışma

[OutputCache] filtresini kullanıyorsanız, önbellek girişini cihaz türüne göre değişiklik yapmak üzere zorlamanız gerekir. Örneğin şunu yazın:

[!code-javascript[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample13.js)]

Ardından, Global.asax.cs dosyanıza aşağıdaki yöntemi ekleyin:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample14.cs)]

Bu, sayfada bulunan mobil ziyaretçilerin bir masaüstü ziyaretçisi tarafından daha önce önbelleğe yerleştirmemesini sağlar.

### <a name="a-working-example"></a>Çalışan bir örnek

Bu teknikleri eylemde görmek için [Bu teknik incelemeye ait kod ile ilgili örnekleri](https://docs.microsoft.com/aspnet/mobile/overview)indirin. Örnek, yukarıda açıklanan yöntemleri kullanarak mobil cihazları desteklemek için geliştirilmiş bir ASP.NET MVC 3 (Release Candidate) uygulaması içerir.

## <a name="further-guidance-and-suggestions"></a>Daha fazla rehberlik ve öneri

Aşağıdaki tartışma, bu belgede ele alınan teknikleri kullanan Web Forms ve MVC geliştiricileri için geçerlidir.

### <a name="enhancing-your-redirection-logic-using-51degreesmobi-foundation"></a>51Degrees.mobi Foundation kullanarak yeniden yönlendirme mantığınızı geliştirme

Bu belgede gösterilen yeniden yönlendirme mantığı, uygulamanız için yeterince kusursuz olabilir, ancak oturumları devre dışı bırakmanız gerekiyorsa veya tanımlama bilgilerini (bu oturumlara sahip olamaz) engelleyen mobil tarayıcılarla, belirli bir isteğin olup olmadığını bilmez Bu ziyaretçiden ilki.

Açık kaynak 51Degrees.mobi Foundation 'ın ASP 'nin doğruluğunu nasıl iyileştirebileceğinizi zaten öğrendiniz. NET ' in tarayıcı algılaması. Ayrıca, mobil ziyaretçileri Web. config 'de yapılandırılmış belirli konumlara yeniden yönlendirebilme özelliği de vardır. Ziyaretçi ' HTTP üst bilgileri ve IP adresi karmalarını günlüğe kaydederek ASP.NET oturumlarına (ve bu nedenle tanımlama bilgileri) bağlı olmadan çalışabilir, bu nedenle her isteğin belirli bir vizör tarafından ilk kez olup olmadığını bilir.

Web. config dosyasının on beşinci Tyone bölümüne eklenen aşağıdaki öğe, algılanan bir mobil cihazdaki ilk isteği ~/Mobile/default.aspxpage sayfasına yönlendirir. Mobil klasör altındaki sayfalara yapılan tüm istekler, cihaz türünden bağımsız olarak yeniden *yönlendirilmeyecektir.* Mobil cihaz 20 dakikalık bir süre için etkin değilse veya daha fazla işlem yeniden yönlendirme amacıyla, sonraki istekler yeni olanlar olarak kabul edilir.

[!code-xml[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample15.xml)]

Daha ayrıntılı bilgi için bkz. [51Degrees.mobi Foundation belgeleri](https://github.com/51Degrees/dotNET-Device-Detection).

> [!NOTE]
> 51Degrees.mobi Foundation 'ın yeniden yönlendirme özelliğini ASP.NET MVC *uygulamalarında kullanabilirsiniz,* ancak yeniden yönlendirme yapılandırmanızı yönlendirme parametreleri açısından değil, düz URL 'ler olarak tanımlamanız gerekir, ancak eylemler üzerine MVC filtreleri koyarak. Bunun nedeni, (yazma sırasında) 51Degrees.mobi Foundation 'ın filtreleri veya yönlendirmeyi tanımaz.

### <a name="disabling-transcoders-and-proxy-servers"></a>Dönüştürme ve proxy sunucularını devre dışı bırakma

Mobil ağ operatörleri, mobil internet 'e yaklaşımda iki geniş hedefe sahiptir:

1. Mümkün olduğunca çok ilgili içerik sağlayın
2. Sınırlı radyo ağı bant genişliğini paylaşabilen müşterilerin sayısını en üst düzeye çıkarın

Çoğu Web sayfası, büyük masaüstü boyutunda ekranlar ve hızlı sabit çizgili geniş bant bağlantıları için tasarlandığından, birçok işleç, Web içeriğini dinamik olarak değiştiren *kodlayıcılarımızdan* veya *proxy sunucuları* kullanır. HTML biçimlerinizi veya CSS 'yi daha küçük ekranlara uyacak şekilde değiştirebilir (özellikle de karmaşık düzenleri işlemek için işlem gücü olmayan "özellik telefonları" için) ve sayfa teslim hızlarını geliştirmek için görüntülerinizi yeniden sıkıştırabilir (kalitesini önemli ölçüde azaltabilirsiniz).

Ancak sitenizin mobil olarak iyileştirilmiş bir sürümünü üretme çabasıyla karşılaşırsanız, ağ operatörünün daha fazlasını kesintiye uğramasını istemezsiniz. Aşağıdaki satırı, herhangi bir ASP.NET Web formundaki\_Load olayına ekleyebilirsiniz:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample16.cs)]

Ya da bir ASP.NET MVC denetleyicisi için, bu denetleyicideki tüm eylemler için geçerli olacak şekilde aşağıdaki yöntemi geçersiz kılmayı ekleyebilirsiniz:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample17.cs)]

Elde edilen HTTP iletisi W3C uyumlu dönüştürme ve proxy 'leri içerik değiştirmeyecektir. Tabii ki, mobil ağ işleçlerinin bu iletiye uymayacak bir garanti yoktur.

### <a name="styling-mobile-pages-for-mobile-browsers"></a>Mobil tarayıcılar için mobil sayfaları Stillendirme

Bu belgenin kapsamı, ne tür bir HTML biçimlendirmesinin doğru çalıştığını veya hangi web tasarımı tekniklerinin belirli cihazlarda kullanılabilirliği en üst düzeye çıkardığından ayrıntılı bilgiler sağlar. Güvenilir olmayan HTML veya CSS konumlandırma püf noktaları kullanmadan, mobil boyutlu bir ekran için optimize edilmiş, yeterince basit bir düzen bulmanız en iyisidir. Bununla birlikte, önemli bir teknik ifade, *Görünüm penceresi meta etiketidir*.

Belirli modern mobil tarayıcılarda, masaüstü izleyicilerine yönelik bir çaba görüntüleme Web sayfalarında, sayfayı "Görünüm penceresi" olarak da adlandırılan bir sanal tuvalde (örneğin, sanal görünüm, iPhone üzerinde 980 piksel genişliğinde ve varsayılan olarak Opera Mobile 'da 850 piksel genişliğinde) işle sonucu ekranın fiziksel pikseline sığacak şekilde ölçeklendirin. Kullanıcı daha sonra bu görünüm penceresini yakınlaştırmak ve kaydırmak için kullanılabilir. Bu, tarayıcının sayfayı amaçlanan düzeninde görüntülemesine izin veren avantajına sahiptir, ancak kullanıcı için uygun olmayan yakınlaştırma ve kaydırma işlemini zorladığı dezavantajı de vardır. Mobil için tasarlandıysanız, yakınlaştırma veya yatay kaydırma gerekli olmayacak şekilde dar bir ekran tasarlamak daha iyidir.

Mobil tarayıcıya *, standart olmayan görünüm penceresinin* ne kadar geniş olduğunu anlatmak için bir yol. Örneğin, sayfanın baş bölümüne aşağıdakileri eklerseniz,

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample18.html)]

… daha sonra akıllı telefon tarayıcıları, sayfayı 480 piksel geniş bir sanal tuvalde oluşturacak şekilde düzenleyin. Bu, HTML öğeleriniz genişliğini yüzde cinsinden tanımladıysanız, yüzdeleri varsayılan görünüm penceresinin genişliği değil bu 480 piksel genişliğine göre yorumlanacak anlamına gelir. Sonuç olarak, Kullanıcı yatay olarak yakınlaştırmak ve kaydırmak zorunda kalmaz ve mobil gözatma deneyimini önemli ölçüde geliştirir.

Görünüm penceresinin genişliğini cihazın fiziksel pikselleriyle eşleşecek şekilde istiyorsanız aşağıdakileri belirtebilirsiniz:

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample19.html)]

Bunun düzgün çalışması için, öğeleri bu genişliği aşmaya (örneğin, bir *Width* ÖZNITELIĞI veya CSS özelliği kullanarak) açıkça zorlamayabilir, aksi takdirde tarayıcı daha büyük bir görünüm penceresinin ne olursa olsun kullanılmasına zorlanır. Ayrıca bkz: [Standart olmayan görünüm kutusu etiketi hakkında daha fazla ayrıntı](https://developer.apple.com/library/safari/#documentation/AppleApplications/Reference/SafariHTMLRef/Articles/MetaTags.html).

Birçok modern akıllı telefon, *çift yönlendirmeyi*destekler: dikey veya yatay modda tutulabilir. Bu nedenle, ekran genişliği hakkında varsayımlar yapmak önemlidir. Ayrıca ekran genişliğinin düzeltilmediği varsayımda değildir, çünkü Kullanıcı sayfanızda olduklarında cihazlarını yeniden yönlendirebilirler.

Eski Windows Mobile ve BlackBerry cihazları, içerik Mobil için iyileştirildiğini bilgilendirmek için sayfa üst bilgisinde aşağıdaki meta etiketleri de kabul edebilir ve bu nedenle dönüştürülmemelidir.

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample20.html)]

## <a name="additional-resources"></a>Ek Kaynaklar

Mobil ASP.NET Web uygulamanızı test etmek için kullanabileceğiniz mobil cihaz öykünücüleri ve simülatörleri listesi için, bkz. [test için popüler mobil cihazların benzetimini](../mobile/device-simulators.md)yapma sayfası.

## <a name="credits"></a>Krediler

- Birincil Yazar: Steven Sanderson
- Gözden geçirenler/ek içerik yazarları: James Rosewell, MIKAEL Söderström, Scott Hanselman, Scott Hunter
