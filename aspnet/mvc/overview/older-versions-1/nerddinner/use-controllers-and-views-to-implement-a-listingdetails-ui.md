---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: Bir listeleme/Ayrıntılar Kullanıcı arabirimi uygulamak için denetleyicileri ve görünümleri kullanma | Microsoft Docs
author: microsoft
description: 4\. adım, kullanıcılara veri listeleme/Ayrıntılar gezinti deneyimi sağlamak için modelimizin avantajlarından yararlanan uygulamaya nasıl bir denetleyici ekleneceğini gösterir...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 74319fe5ea4c79b50140834349e2fdf86420cfbb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600746"
---
# <a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a>Denetleyicileri ve Görünümleri Kullanarak Listeleme/Ayrıntılar Kullanıcı Arabirimi Uygulama

[Microsoft](https://github.com/microsoft) tarafından

[PDF 'YI indir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu, ASP.NET MVC 1 kullanarak küçük, ancak tam bir Web uygulamasının nasıl oluşturulacağını gösteren ücretsiz bir ["Nerdakşam yemeği" uygulama öğreticisinin](introducing-the-nerddinner-tutorial.md) 4. adımından oluşur.
> 
> 4\. adım, kullanıcılara, Nerdakşam yemeği sitemizdeki dinlimler için veri listeleme/Ayrıntılar gezinti deneyimi sağlamak amacıyla, bir uygulamanın, modelimizin avantajlarından yararlanan bir denetleyicinin nasıl ekleneceğini gösterir.
> 
> ASP.NET MVC 3 kullanıyorsanız, [MVC 3 Ile çalışmaya başlama](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC müzik mağazası](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) öğreticilerini izlemeniz önerilir.

## <a name="nerddinner-step-4-controllers-and-views"></a>Nerdakşam yemeği 4. Adım: denetleyiciler ve görünümler

Geleneksel Web çerçeveleri (klasik ASP, PHP, ASP.NET Web Forms vb.) ile gelen URL 'Ler genellikle disk üzerindeki dosyalarla eşleştirilir. Örneğin: "/Products.aspx" veya "/Products.php" gibi bir URL isteği bir "Products. aspx" veya "Products. php" dosyası tarafından işlenebilir.

Web tabanlı MVC çerçeveleri, URL 'Leri sunucu koduna biraz farklı bir şekilde eşler. Gelen URL 'Leri dosyalara eşlemek yerine, URL 'Leri sınıfların yöntemlerine eşleyin. Bu sınıflar "denetleyiciler" olarak adlandırılır ve gelen HTTP isteklerini işlemekten, Kullanıcı girişi işleme, verileri alma ve kaydetme ve istemciye geri gönderme yanıtını belirleme (HTML görüntüleme, bir dosyayı indirme, farklı bir şekilde yeniden yönlendirme) URL, vb.).

Nerdakşam yemeği uygulamamız için temel bir model oluşturduğumuzdan, bir sonraki adımınız, kullanıcılara sitemizin için bir veri listeleme/Ayrıntılar gezintisi deneyimi sağlamak üzere uygulamanın avantajlarından yararlanan bir denetleyici eklemektir.

### <a name="adding-a-dinnerscontroller-controller"></a>DinnersController denetleyicisi ekleme

Web projemizdeki "denetleyiciler" klasörüne sağ tıklayıp ardından **Add-&gt;Controller** menü komutunu seçin (Ctrl-M, CTRL-C yazarak da bu komutu çalıştırabilirsiniz):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

Bu, "denetleyici Ekle" iletişim kutusunu getirir:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

"DinnersController" adlı yeni denetleyiciyi ve "Ekle" düğmesine tıklayacağız. Visual Studio, \Controllers dizinimizin altına bir DinnersController.cs dosyası ekler:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

Ayrıca, kod Düzenleyicisi içinde yeni DinnersController sınıfını açar.

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a>DinnersController sınıfına dizin () ve ayrıntılar () eylem yöntemleri ekleme

Uygulamamızı kullanarak, yaklaşan içgörülerin listesine gözatmasını ve ilgili belirli ayrıntıları görmek için listedeki herhangi bir akşam 'ye tıklamalarını sağlamak istiyoruz. Bunu uygulamamızda aşağıdaki URL 'Leri yayımlayarak yapacağız:

| **URL** | **Amaç** |
| --- | --- |
| */Dinners/* | Yaklaşan dinlerlerin HTML listesini görüntüleme |
| */Dinners/Details/[kimlik]* | URL içinde gömülü bir "ID" parametresi tarafından belirtilen belirli bir akşam yemeği hakkındaki ayrıntıları, veritabanındaki akşam yemeği 'nin DinnerID eşleşecek şekilde görüntüler. Örneğin:/Dinners/Details/2, DinnerID değeri 2 olan akşam yemeği hakkındaki ayrıntıları içeren bir HTML sayfası görüntüler. |

Aşağıdaki gibi DinnersController sınıfımız iki genel "Action yöntemi" ekleyerek bu URL 'lerin ilk uygulamalarını yayımlayacağız:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

Daha sonra Nerdakşam yemeği uygulamasını çalıştıracağız ve bunları çağırmak için tarayıcımızı kullanacağız. *"/Dinners/"* URL 'Sini yazmak *Dizin ()* yönteminizin çalışmasına neden olur ve aşağıdaki yanıtı geri gönderir:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

*"/Dinners/details/2"* URL 'sini yazmak, *Details ()* yönteminin çalışmasına neden olur ve aşağıdaki yanıtı geri gönderir:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

DinnersController sınıfınızı nasıl oluşturmak ve bu yöntemleri çağırmak için ASP.NET MVC 'nin nasıl çalıştığını merak ediyor olabilirsiniz mi? Bunu anlamak için yönlendirmenin nasıl çalıştığına göz atalım.

### <a name="understanding-aspnet-mvc-routing"></a>ASP.NET MVC yönlendirmesini anlama

ASP.NET MVC, URL 'Lerin denetleyici sınıflarıyla nasıl eşlenildiğini denetlemek için çok sayıda esneklik sağlayan güçlü bir URL yönlendirme altyapısı içerir. ASP.NET MVC 'nin hangi denetleyici sınıfının oluşturulacağını, hangi yöntem üzerinde çağrılacak yöntemi seçmemizi ve değişkenlerin URL/QueryString 'den otomatik olarak ayrıştırılabileceği ve yönteme parametre bağımsız değişkenleri olarak geçirildiği farklı yollar yapılandırabilmesini sağlar. Bir uygulamayı bir SEO (arama motoru iyileştirmesi) için en iyi duruma getirme esnekliği sağlar ve bir uygulamadan istediğiniz URL yapısını yayımlayın.

Varsayılan olarak, yeni ASP.NET MVC projeleri önceden kaydedilmiş bir URL yönlendirme kuralları kümesi ile gelir. Bu, açıkça bir şey yapılandırmak zorunda kalmadan bir uygulamaya kolayca başlayabilmenizi sağlar. Varsayılan yönlendirme kuralı kayıtları, projelerimizin "uygulama" sınıfında bulunabilir. Bu, proje kökündeki "Global. asax" dosyasına çift tıklayarak açabiliyoruz:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

Varsayılan ASP.NET MVC yönlendirme kuralları bu sınıfın "RegisterRoutes" metodu içinde kaydedilir:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

"Yollar. Yukarıdaki MapRoute () "yöntem çağrısı, gelen URL 'Leri denetleyici sınıflarına eşleyen bir varsayılan yönlendirme kuralını Şu URL biçimi kullanarak kaydeder:"/{Controller}/{id} "–" denetleyici "örneklendirilecek denetleyici sınıfının adıdır," eylem ", üzerinde çağrılacak bir ortak yöntemin adıdır ve" kimlik ", bir bağımsız değişken olarak metoduna geçirilen URL içinde gömülü isteğe bağlı bir parametredir. "MapRoute ()" yöntem çağrısına geçirilen üçüncü parametre, (denetleyici = "giriş", eylem = "Dizin", kimlik = "") olayda denetleyici/eylem/kimlik değerleri için kullanılacak varsayılan değerler kümesidir.

Aşağıda, çeşitli URL 'Lerin varsayılan "<em>/{Controllers}/{Action}/{ID}"</em>yol kuralını kullanarak nasıl eşlendiğini gösteren bir tablo verilmiştir:

| **URL** | **Denetleyici sınıfı** | **Action yöntemi** | **Geçirilen parametreler** |
| --- | --- | --- | --- |
| */Dinners/Details/2* | DinnersController | Ayrıntılar (kimlik) | kimlik = 2 |
| */Dinners/Edit/5* | DinnersController | Düzenle (kimlik) | kimlik = 5 |
| */Dinners/Create* | DinnersController | Oluştur () | Yok |
| */Dinanlar* | DinnersController | Dizin () | Yok |
| */Home* | HomeController | Dizin () | Yok |
| */* | HomeController | Dizin () | Yok |

Son üç satır, kullanılan varsayılan değerleri (denetleyici = Home, Action = Dizin, ID = "") gösterir. "Dizin" yöntemi belirtilmemişse varsayılan eylem adı olarak kaydedildiğinden, "/Dınanlar" ve "/Home" URL 'Leri, denetleyici sınıflarında dizin () eylem yönteminin çağrılmasına neden olur. "Giriş" denetleyicisi belirtilmemişse varsayılan denetleyici olarak kaydedildiğinden, "/" URL 'SI HomeController 'ın oluşturulmasına ve üzerinde dizin () eylem yöntemine neden olur.

Bu varsayılan URL yönlendirme kurallarını beğenmezseniz, iyi haber, daha kolay bir şekilde değiştirilebilir. Bunlar, yukarıdaki RegisterRoutes yöntemi içinde düzenlenmelidir. Nerdakşam yemeği uygulamamız için, varsayılan URL yönlendirme kurallarından herhangi birini değiştiremedik, bunun yerine bunları olduğu gibi kullanacağız.

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a>DinnersController 'umuza DinnerRepository kullanma

Şimdi, DinnersController 'in dizin () ve details () eylem yöntemlerinin geçerli uygulamamızı, modelimizi kullanan uygulamalarla değiştirecek.

Daha önce oluşturduğumuz DinnerRepository sınıfını, davranışı uygulamak için kullanacağız. "Nerdakşam yemeği. modeller" ad alanına başvuruda bulunan bir "Using" ifadesini ekleyerek başlayacağız ve ardından DinnerRepository bir örnek olarak DinnerController sınıfımızda bir alan olarak bildireceğiz.

Bu bölümde daha sonra, "bağımlılık ekleme" kavramının tanıtılmasına ve Denetleyicilerimizin daha iyi birim testi sağlayan bir DinnerRepository başvurusu alması için başka bir yol göstermemiz gerekir, ancak şu anda yalnızca DinnerRepository bir örneğini oluşturacağız aşağıdaki gibi satır içi.

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

Şimdi, alınan veri modeli nesnelerimizi kullanarak bir HTML yanıtı oluşturmaya hazır hale getiriyoruz.

### <a name="using-views-with-our-controller"></a>Denetleyicimiz ile görünümleri kullanma

HTML 'i birleştirmek ve ardından *Response. Write ()* yardımcı yöntemini kullanarak, HTML 'yi birleştirme ve sonra istemciye geri göndermek için eylem yöntemlerimiz dahilinde kod yazmak mümkün olsa da, bu yaklaşım oldukça hızlı hale gelir. Çok daha iyi bir yaklaşım, DinnersController eylem yöntemlerimiz içinde yalnızca uygulama ve veri mantığı gerçekleştirmekten ve sonra HTML yanıtını HTML gösteriminin çıktısını almak için gereken ayrı bir "Görünüm" şablonuna geçirmesi için gereken verileri iletmektir. . Bir süre içinde göreceğiniz gibi, bir "Görünüm" şablonu, genellikle HTML biçimlendirme ve katıştırılmış işleme kodu birleşimini içeren bir metin dosyasıdır.

Denetleyici mantığımızı görüntüleme işlemızdan ayırarak birçok büyük avantaj elde edin. Özellikle uygulama kodu ve Kullanıcı arabirimi biçimlendirme/işleme kodu arasında açık bir "kaygıları ayrımı" uygulanmasını sağlar. Bu işlem, birim testi uygulama mantığını UI işleme mantığının yalıtımına çok daha kolay hale getirir. Uygulama kodu değişikliği yapmak zorunda kalmadan, daha sonra UI işleme şablonlarının değiştirilmesini kolaylaştırır. Ayrıca, geliştiricilerin ve tasarımcıların projelerde birlikte işbirliği yapmasını kolaylaştırır.

DinnersController sınıfınızı, bir HTML UI yanıtı göndermek için bir görünüm şablonu kullanmak istediğimizin, "void" dönüş türü yerine "ActionResult" dönüş türüne sahip olması gerektiğini gösterecek şekilde güncelleyebiliriz. Daha sonra, aşağıdaki gibi bir "ViewResult" nesnesi geri dönmek için denetleyici temel sınıfında *View ()* yardımcı yöntemini çağırabiliriz:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

Yukarıda kullandığımız *View ()* yardımcı yönteminin imzası aşağıdaki gibi görünür:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

*View ()* yardımcı yönteminin ilk PARAMETRESI, HTML yanıtını işlemek için kullanmak istediğimiz görünüm şablonu dosyasının adıdır. İkinci parametre, görünüm şablonunun HTML yanıtını işlemek için ihtiyacı olan verileri içeren bir model nesnesidir.

Dizin () eylem yöntemimizde, *View ()* yardımcı yöntemini arıyoruz ve bir "Dizin" görünümü şablonu kullanarak dinetler 'in HTML listesini işlemek istediğimizi gösterir. Listeyi oluşturmak için görünüm şablonuna bir akşam yemeği nesne sırası geçiriyoruz:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

Ayrıntılarımızda () eylem yönteminde, URL içinde sunulan kimliği kullanarak bir akşam yemeği nesnesini almayı denedik. Geçerli bir akşam yemeği bulunursa, alınan akşam yemeği nesnesini işlemek için "Ayrıntılar" görünüm şablonunu kullanmak istediğimiz olan *View ()* yardımcı yöntemini çağırdık. Geçersiz bir akşam yemeği isteniyorsa, akşam yemeği 'nin "NotFound" görünüm şablonunu (ve yalnızca şablon adını alan *Görünüm ()* yardımcı yönteminin aşırı yüklenmiş bir sürümünü kullanarak var olmadığını belirten faydalı bir hata iletisi oluşturacağız:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

Şimdi "NotFound", "details" ve "Dizin" görünüm şablonlarını uygulayalim.

### <a name="implementing-the-notfound-view-template"></a>"NotFound" görünüm şablonunu uygulama

İstenen akşam yemeği bulunamadığını belirten kolay bir hata iletisi görüntüleyen "NotFound" görünüm şablonunu uygulayarak başlayacağız.

Metin imlecinizi bir denetleyici eylemi yöntemi içinde konumlandırarak yeni bir görünüm şablonu oluşturacağız ve sağ tıklayıp "Görünüm Ekle" menü komutunu seçtiğinizde (Bu komutu ayrıca Ctrl-u, CTRL-V yazarak de yürütebiliriz):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

Bu, aşağıdaki gibi bir "Görünüm Ekle" iletişim kutusu getirir. Varsayılan olarak, iletişim kutusu başlatıldığında (Bu durumda "Ayrıntılar") imlecin bulunduğu eylem yönteminin adıyla eşleşecek şekilde, oluşturmak için görünümün adının önceden doldurulması gerekir. Önce "NotFound" şablonunu uygulamak istiyoruz, bu görünüm adını geçersiz kılacağız ve bunun yerine "NotFound" olarak ayarlayacağız:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

"Ekle" düğmesine tıkladığımızda, Visual Studio "\Views\dıntik" dizininde bizimle ilgili yeni bir "NotFound. aspx" görünüm şablonu oluşturacak (Dizin zaten yoksa, bu da bu da oluşturulur):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

Ayrıca, kod Düzenleyicisi içinde yeni "NotFound. aspx" görünüm şablonunu açar:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

Şablonları varsayılan olarak görüntüle, içerik ve kod ekleyebilmemiz için iki "içerik bölgesi" vardır. Birincisi, geri gönderilen HTML sayfasının "başlığını" özelleştirmenizi sağlar. İkincisi, geri gönderilen HTML sayfasının "ana içeriğini" özelleştirmenizi sağlar.

"NotFound" görünüm şablonunuzu uygulamak için bazı temel içerikleri ekleyeceğiz:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

Daha sonra bunu tarayıcıdan deneyebilirsiniz. Bunu yapmak için *"/Dinners/details/9999"* URL 'sini isteelim. Bu, şu anda veritabanında mevcut olmayan bir akşam yemeği 'ye başvuracaktır ve DinnersController. Details () eylem yönteminin "NotFound" görünüm şablonunu işlemesine neden olur:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

Yukarıdaki ekran görüntüsünde fark ettiğiniz bir şey, temel görünüm şablonumuzın ekrandaki ana içeriği çevreleyen bir veya daha fazla HTML devraldığından emin olun. Bunun nedeni, görünüm şablonumuz sitedeki tüm görünümlerde tutarlı bir düzen uygulamamızı sağlayan bir "Ana sayfa" şablonu kullanıyor. Bu öğreticinin sonraki kısımlarında ana sayfaların daha fazla çalışma şeklini inceleyeceğiz.

### <a name="implementing-the-details-view-template"></a>"Ayrıntılar" görünüm şablonunu uygulama

Şimdi, tek bir akşam yemeği modeli için HTML oluşturacak "Ayrıntılar" görünüm şablonunu uygulayalim.

Bunu, metin imlecinizi Ayrıntılar eylem yöntemi içinde konumlandırarak ve ardından sağ tıklayıp "Görünüm Ekle" menü komutunu seçerek yapacağız (veya CTRL-e, CTRL-V tuşlarına basın):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

Bu işlem "Görünüm Ekle" iletişim kutusunu getirir. Varsayılan görünüm adını ("Ayrıntılar") tutacağız. Ayrıca, iletişim kutusunda "kesin türü belirtilmiş bir görünüm oluştur" onay kutusunu seçeceğiz ve denetleyiciden görünüme geçirdiğimiz model türünün adını (ComboBox açılan menüsünü kullanarak) seçin. Bu görünüm için bir akşam yemeği nesnesi geçiriyoruz (Bu tür için tam ad: "Nerdakşam. modeller. akşam"):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

Önceki şablondan farklı olarak, "boş görünüm" oluşturmayı seçtik, bu kez "Ayrıntılar" şablonunu kullanarak görünümü otomatik olarak "scafkatmayı" tercih ediyoruz. Yukarıdaki iletişim kutusunda "içeriği görüntüle" açılan kutusunu değiştirerek bunu belirtebiliriz.

"Scafkatlama", geçirdiğimiz akşam yemeği nesnesine göre ayrıntı görünümü şablonumuzdan bir başlangıç uygulamasını oluşturacaktır. Bu, görünüm şablonu uygulamamıza hızlı bir şekilde başlamamız için kolay bir yol sağlar.

"Ekle" düğmesine tıkladığımızda, Visual Studio "\Views\dıntik" dizininiz dahilinde bize yönelik yeni bir "details. aspx" görünüm şablonu dosyası oluşturacak:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

Ayrıca, kod Düzenleyicisi içindeki yeni "details. aspx" görünüm şablonunu açar. Bir akşam yemeği modeline dayalı olarak bir ayrıntılar görünümünün ilk yapı iskelesi uygulamasını içerir. Yapı iskelesi altyapısı, geçirilen sınıf üzerinde sunulan ortak özelliklere bakmak için .NET Reflection kullanır ve bulduğu her türe göre uygun içeriği ekler:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

"Ayrıntılar" yapı iskelesi uygulamasının tarayıcıda nasıl göründüğünü görmek için *"/Dinners/details/1"* URL 'sini isteyebiliriz. Bu URL 'YI kullanmak, ilk oluşturduğumuzda veritabanınıza el ile eklediğimiz dinetleri gösterir:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

Bu, hızlı bir şekilde çalışmaya başlamanızı sağlar ve bize ayrıntılar. aspx görünümümüzü ilk uygulamayla birlikte verir. Daha sonra, Kullanıcı arabirimini memnuniyet duyuyoruz olarak özelleştirmek için ince ayar ve bu uygulamayı kullanabilirsiniz.

Details. aspx şablonuna daha yakından baktığımızda, gömülü işleme kodunun yanı sıra statik HTML de içerdiğini fark ediyoruz. &lt;%%&gt; Code nugbu, görünüm şablonu işlerken kodu yürütür ve &lt;% =%&gt; kodu nugın içinde yer alan kodu yürütür ve sonucu, şablonun çıkış akışına işler.

Görünümümüzden kesin olarak belirlenmiş "model" özelliği kullanılarak geçirilen "akşam yemeği" model nesnesine erişen görünümümüzde kod yazalım. Visual Studio, düzenleyici içindeki bu "model" özelliğine erişirken tam koda sahip bize IntelliSense sağlar:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

Son Ayrıntılar görünümü şablonumuza ait kaynağın aşağıdaki gibi görünmesini sağlamak için bazı temks oluşturalım:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

*"/Dinners/details/1"* URL 'sine yeniden eriştiğinizde, artık aşağıdaki gibi işleme alınır:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a>"Dizin" görünüm şablonunu uygulama

Şimdi "Dizin" görünüm şablonunu uygulayalim. Bu, yaklaşan Dinverlerin bir listesini oluşturur. Bunu yapmak için, metin imlecinizi Dizin eylemi yöntemi içinde konumlandırması ve sonra sağ tıklayıp "Görünüm Ekle" menü komutunu seçmesi (veya CTRL-e, CTRL-V tuşlarına basmanız) gerekir.

"Görünüm Ekle" iletişim kutusunda "Dizin" adlı görünüm şablonunu tutacağız ve "kesin türü belirtilmiş bir görünüm oluştur" onay kutusunu seçmelisiniz. Bu süre otomatik olarak bir "liste" görünümü şablonu oluşturmayı tercih edeceğiz ve görünüme geçilen model türü olarak "Nerdakşam. modeller. akşam" yi seçin (bir "liste" oluşturduğumuz Denetleyicimizde bir akşam yemeği nesneleri dizisini görünüme geçirme):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

"Ekle" düğmesine tıkladığımızda, Visual Studio "\Views\dıntik" dizininiz dahilinde bize yönelik yeni bir "Index. aspx" görünüm şablonu dosyası oluşturacaktır. Bu, görünümü geçirdiğimiz Dinetleri içeren bir HTML tablo listesi sağlayan bir ilk uygulama olan "scafkatmayı" kullanacaktır.

Uygulamayı çalıştırıp *"/Dinners/"* URL 'sine eriştiğinizde, şunun gibi dinetleri listemizi işleyecek:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

Yukarıdaki tablo çözümü bize akşam yemeği verilerimizin kılavuza benzer bir yerleşimini sağlar. Bu, tüketiciye yönelik akşam yemeği listemize yönelik olarak istiyoruz. Index. aspx görünüm şablonunu güncelleştirebiliriz ve daha az veri sütunu listelemek için bunu değiştirebilir ve aşağıdaki kodu kullanarak bir tablo yerine onları işlemek için &lt;ul&gt; öğesi kullanabilirsiniz:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

Modelimizde her akşam yemeği için döngü yaptığımız için yukarıdaki foreach ifadesi içinde "var" anahtar sözcüğünü kullanıyoruz. 3,0 ile C# bilmediğiniz bu kişiler, "var" kullanmanın, akşam yemeği nesnesinin geç bağlantılı olduğunu düşünebilir. Bunun yerine, derleyicinin tür çıkarımı kesin belirlenmiş "model" özelliği ("IEnumerable&lt;akşam&gt;" türü) ve yerel "akşam yemeği" değişkenini bir akşam yemeği türü olarak derlerken, bu da kod blokları içinde tam IntelliSense ve derleme zamanı denetimi yaptığımız anlamına gelir:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

Tarayıcımızda bulunan */dinlerimizin* URL 'si üzerinde yenileme isabet ettiğimiz zaman şu anda şu şekilde görünür:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

Bu, daha iyi bir şekilde gezinerek henüz tamamen orada değildir. Son adımımız, son kullanıcıların listedeki her bir kez tıklamasını ve bunlarla ilgili ayrıntıları görmesini olanaklı hale sunmamız. Bunu uygulamamız için DinnersController adresindeki Ayrıntılar eylem yöntemine bağlanan HTML köprü öğelerini işlenerek uygulayacağız.

Bu köprüleri, Dizin görünümümüzde iki şekilde oluşturabilirsiniz. İlk olarak,&gt; bir &lt;HTML öğesi&gt; &lt;%&gt; bloklarını katıştıracağız aşağıda olduğu gibi bir öğelerini el ile oluşturmak &lt;:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

Kullanabileceğiniz alternatif bir yaklaşım, ASP.NET MVC içindeki yerleşik "HTML. ActionLink ()" yardımcı yönteminden yararlanarak, bir denetleyicideki başka bir eylem yöntemine bağlanan bir&gt; öğesi olan bir HTML &lt;programlı bir şekilde HTML oluşturmayı destekler:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

HTML için ilk parametre. ActionLink () yardımcı yöntemi görüntülenecek olan bağlantı metinleridir (Bu durumda akşam yemeği 'nın başlığı), ikinci parametre bağlantı oluşturmak istediğimiz denetleyici eylemi adıdır (Bu durumda, Ayrıntılar yöntemi) ve üçüncü parametre eyleme gönderilmek üzere bir parametre kümesidir (özellik adı/değerleri olan anonim bir tür olarak uygulanır). Bu durumda, bağlanmak istediğimiz akşam yemeği 'nin "kimlik" parametresini belirttik ve ASP.NET MVC 'deki varsayılan URL yönlendirme kuralı "{Controller}/{Action}/{ID}", HTML. ActionLink () yardımcı yöntemi aşağıdaki çıktıyı oluşturacak:

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

Index. aspx görünümümüzde HTML. ActionLink () yardımcı yöntem yaklaşımını kullanacağız ve her bir akşam yemeği için ilgili ayrıntılar URL 'sine sahip olursunuz:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

Şimdi de akşam yemeği listemizin *URL 'sini* ziyaret ettiğimiz zaman şu şekilde görünür:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

Listede yer aldığı bazı yemekleri tıkladığımızda, ilgili ayrıntıları görmek için gezineceğiz:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a>Kural tabanlı adlandırma ve \Views dizin yapısı

ASP.NET MVC uygulamaları varsayılan olarak Görünüm şablonları çözümlenirken kural tabanlı dizin adlandırma yapısını kullanır. Bu, geliştiricilerin bir denetleyici sınıfından görünümleri başvururken bir konum yolunu tamamen nitelemek zorunda kalmalarına olanak sağlar. Varsayılan olarak, ASP.NET MVC, uygulamanın altındaki * \Views\[ControllerName]\* dizininde bulunan görünüm şablonu dosyasını arayacaktır.

Örneğin, DinnersController sınıfı üzerinde çalıştık: "Index", "details" ve "NotFound". ASP.NET MVC, varsayılan olarak, uygulama kök dizinimizin altındaki *\Views\ınk\dizininde* bulunan bu görünümleri arayacaktır:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

Şu anda proje içinde üç denetleyici sınıfının (DinnersController, HomeController ve AccountController) nasıl kullanıldığına dikkat edin: son iki, proje oluşturduğumuz varsayılan olarak eklenmiştir ve üç alt dizin (her biri için bir tane) vardır. denetleyicisi) \Views dizininde.

Giriş ve hesap denetleyicilerinden başvurulan görünümler, kendi görünüm şablonlarını ilgili *\Views\home* ve *\Views\account* dizinlerinden otomatik olarak çözümler. *\Views\shared* alt dizini, uygulamanın içindeki birden çok denetleyicilerde yeniden kullanılan görünüm şablonlarını depolamanın bir yolunu sağlar. ASP.NET MVC bir görünüm şablonunu çözümlemeye çalıştığında, ilk olarak *\views\[Controller]* özel dizinini iade eder ve *\Views\shared* dizininde görünecektir.

Tek tek görünüm şablonlarının adlandırılması gerektiğinde, görüntüleme şablonunun işleme neden olan eylem yöntemiyle aynı adı paylaşması önerilir. Örneğin, "Dizin" eylemi yöntemi, görünüm sonucunu işlemek için "Dizin" görünümünü kullanıyor ve "Ayrıntılar" eylem yöntemi sonuçları işlemek için "Ayrıntılar" görünümünü kullanıyor. Bu, hangi şablonun her eylemle ilişkili olduğunu hızlıca görmeyi kolaylaştırır.

Görünüm şablonu denetleyicide çağrılan eylem yöntemiyle aynı ada sahip olduğunda, geliştiricilerin görünüm şablonu adını açıkça belirtmelerine gerek yoktur. Bunun yerine, model nesnesini "View ()" yardımcı yöntemine (görünüm adını belirtmeden) geçirebiliriz ve ASP.NET MVC onu işlemek için diskte *\Views\[ControllerName]\[ActionName]* görünüm şablonunu kullanmak istediğimizden otomatik olarak çıkarması gerekir.

Bu, denetleyici kodumuzu biraz temizleyelim ve kodumuzdaki adı iki kez çoğaltmamızı sağlar:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

Yukarıdaki kod, siteye yönelik iyi bir akşam yemeği listeleme/ayrıntıları deneyimi uygulamak için gereklidir.

#### <a name="next-step"></a>Sonraki adım

Artık derlenmiş iyi bir akşam yemeği göz atma deneyimi sunuyoruz.

Şimdi CRUD (oluşturma, okuma, güncelleştirme, silme) veri formu Düzenle desteğini etkinleştirelim.

> [!div class="step-by-step"]
> [Önceki](build-a-model-with-business-rule-validations.md)
> [İleri](provide-crud-create-read-update-delete-data-form-entry-support.md)
