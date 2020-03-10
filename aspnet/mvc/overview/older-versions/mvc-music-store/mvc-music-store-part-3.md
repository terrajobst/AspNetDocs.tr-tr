---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
title: '3\. kısım: görünümler ve Viewmodeller | Microsoft Docs'
author: jongalloway
description: Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. Bölüm 3, görünümleri ve ViewModel içerir.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 94297aa0-1f2d-4d72-bbcb-63f64653e0c0
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
msc.type: authoredcontent
ms.openlocfilehash: 3fcfc816cde22c697a78bab2c9ea7ace1bf68501
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559810"
---
# <a name="part-3-views-and-viewmodels"></a>3\. Bölüm: Görünümler ve ViewModel’lar

[Jon Galloway](https://github.com/jongalloway) tarafından

> MVC müzik deposu, Web geliştirme için ASP.NET MVC ve Visual Studio 'nun nasıl kullanılacağını anlatan bir öğretici uygulamadır.  
>   
> MVC müzik deposu, çevrimiçi olarak müzik albümlerini satan ve temel site yönetimi, Kullanıcı oturum açma ve alışveriş sepeti işlevlerini uygulayan basit bir örnek depolama uygulamasıdır.  
>   
> Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. Bölüm 3, görünümleri ve ViewModel içerir.

Şu ana kadar yalnızca denetleyici eylemlerinden dizeler döndürdük. Bu, denetleyicilerin nasıl çalıştığı konusunda fikir sahibi olmak için iyi bir yoldur, ancak gerçek bir Web uygulaması oluşturmak istemekten değildir. Sitemizi ziyaret eden tarayıcılarımıza geri HTML oluşturmak için daha iyi bir yol isteyeceksiniz. Bu, şablon dosyalarını yalnızca bir HTML içeriğini geri gönder ' i daha kolay özelleştirmek için kullanabilirsiniz. Tam olarak bu görünümler vardır.

## <a name="adding-a-view-template"></a>Görünüm şablonu ekleme

Bir görünüm şablonu kullanmak için, HomeController Dizin yöntemini bir ActionResult döndürecek şekilde değiştirecek ve aşağıdaki gibi bir görünüm () döndürüyor.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample1.cs)]

Yukarıdaki değişiklik, bir dize döndürmesinin yerine, bir sonuç oluşturmak için bir "Görünüm" kullanmak istediğinin olduğunu gösterir.

Şimdi projemizi uygun bir görünüm şablonu ekleyeceğiz. Bunu yapmak için, metin imlecini Dizin eylemi yöntemine konumlandırır, sonra sağ tıklayıp "Görünüm Ekle" seçeneğini belirleyin. Bu işlem, Görünüm Ekle iletişim kutusunu getirir:

![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)

"Görünüm Ekle" iletişim kutusu, görünüm şablonu dosyalarını hızlı ve kolay bir şekilde üretmemize olanak sağlar. Varsayılan olarak, "Görünüm Ekle" iletişim kutusu, oluşturulacak eylem yöntemiyle eşleşecek şekilde oluşturmak için görünüm şablonunun adını önceden doldurur. HomeController 'ın Index () eylem yöntemi içinde "Görünüm Ekle" bağlam menüsünü kullandığımız için, yukarıdaki "Görünüm Ekle" iletişim kutusunda varsayılan olarak önceden doldurulan görünüm adı olarak "Dizin" bulunur. Bu iletişim kutusundaki seçeneklerden herhangi birini değiştirmemiz gerekmez, bu nedenle Ekle düğmesine tıklayın.

Ekle düğmesine tıkladığımızda, Visual Web Developer, daha önce yoksa klasörü oluşturmak için \Views\Home dizininde yeni bir Index. cshtml görünüm şablonu oluşturacaktır.

![](mvc-music-store-part-3/_static/image2.png)

"Index. cshtml" dosyasının adı ve klasör konumu önemlidir ve varsayılan ASP.NET MVC adlandırma kurallarını izler. \Views\Home dizin adı, HomeController adlı denetleyiciyle eşleşir. Görünüm şablonu adı, dizin, görünümü görüntüleyen denetleyici eylemi yöntemiyle eşleşir.

ASP.NET MVC, bir görünüm döndürmek için bu adlandırma kuralını kullanırken bir görünüm şablonunun adını veya konumunu açık bir şekilde belirtmemizi önlemenize olanak tanır. Bu, varsayılan olarak \Views\home\ındex.cshtml görünüm şablonunu izleyerek HomeController içinde aşağıdaki gibi kod yazdığımızda işlenir:

[!code-csharp[Main](mvc-music-store-part-3/samples/sample2.cs)]

"Görünüm Ekle" iletişim kutusunda "Ekle" düğmesine tıkladıktan sonra Visual Web Developer "Index. cshtml" görünüm şablonunu oluşturup açtı. Index. cshtml 'nin içerikleri aşağıda gösterilmiştir.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample3.cshtml)]

Bu görünüm, ASP.NET Web Forms ve önceki ASP.NET MVC sürümlerinde kullanılan Web Forms görünüm altyapısından daha kısa olan Razor söz dizimi kullanıyor. Web Forms View Engine, ASP.NET MVC 3 ' te hala kullanılabilir, ancak birçok geliştirici Razor görünüm altyapısının ASP.NET MVC geliştirme sürecinde uygun olduğunu bulur.

İlk üç satır, ViewBag. title kullanarak sayfa başlığını ayarlar. Bunun kısa süre içinde nasıl çalıştığını inceleyeceğiz, ancak ilk olarak metin başlık metnini güncelleştirip sayfayı görüntüleyelim. &lt;H2&gt; etiketini aşağıda gösterildiği gibi "Bu giriş sayfasıdır" olarak güncelleştirin.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample4.cshtml)]

Uygulamanın çalıştırılması, yeni metnimizin giriş sayfasında görünür olduğunu gösterir.

![](mvc-music-store-part-3/_static/image3.png)

## <a name="using-a-layout-for-common-site-elements"></a>Ortak site öğeleri için Düzen kullanma

Çoğu Web sitesinin birçok sayfa arasında paylaşılan içeriği vardır: gezinme, altbilgiler, logo görüntüleri, stil sayfası başvuruları, vb. Razor Görünüm altyapısı, bu işlemi otomatik olarak/Views/Shared klasöründe oluşturulan \_Layout. cshtml adlı bir sayfa kullanarak yönetmeyi kolaylaştırır.

![](mvc-music-store-part-3/_static/image4.png)

Aşağıda gösterilen içerikleri görüntülemek için bu klasöre çift tıklayın.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample5.cshtml)]

Bireysel görünümlerimizin içeriği, @RenderBody() komutuyla ve bunun dışında görünmesini istediğimiz tüm ortak içerikler, \_Layout. cshtml biçimlendirmesine eklenebilir. MVC müzik mağazamız, sitedeki tüm sayfalarda giriş sayfası ve depolama alanı bağlantılarıyla ortak bir üst bilgiye sahip olmasını istiyoruz, bu nedenle bu @RenderBody() deyimin hemen üstüne bu şablonu ekleyeceğiz.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample6.cshtml)]

## <a name="updating-the-stylesheet"></a>Stil sayfasını güncelleştirme

Boş proje şablonu, yalnızca doğrulama iletilerini göstermek için kullanılan stilleri içeren çok kolaylaştırılmış bir CSS dosyası içerir. Tasarımcı, sitemizin görünümünü tanımlamak için bazı ek CSS ve görüntüler sağladı, bu nedenle bunları şimdi ekleyeceğiz.

Güncelleştirilmiş CSS dosyası ve görüntüleri, [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store)' da bulunan MvcMusicStore-assets. zip ' in içerik dizinine dahildir. Bunları Windows Gezgini 'nde her ikisini de seçeceğiz ve Visual Web Developer 'daki çözümünüzün Içerik klasörüne aşağıda gösterildiği gibi bırakmalısınız:

![](mvc-music-store-part-3/_static/image5.png)

Mevcut site. css dosyasının üzerine yazmak isteyip istemediğinizi onaylamanız istenecektir. Evet’e tıklayın.

![](mvc-music-store-part-3/_static/image6.png)

Uygulamanızın Içerik klasörü şu şekilde görünür:

![](mvc-music-store-part-3/_static/image7.png)

Şimdi uygulamayı çalıştıralım ve değişikliklerin giriş sayfasında nasıl görünemizi görelim.

![](mvc-music-store-part-3/_static/image8.png)

- Nelerin değiştiğini gözden geçirelim: HomeController 'ın Dizin eylemi yöntemi, "Return View ()" olarak adlandırılsa da, "dönüş görünümü ()" olarak adlandırılsa da, "döndürülen görünüm ()" olarak adlandırılsa da, izleme şablonunuz standart adlandırma kuralına uyduğundan, \ views\home\ındex
- Giriş sayfası, \Views\home\ındex.cshtml görünüm şablonu içinde tanımlanan basit bir hoş geldiniz iletisi görüntülüyor.
- Giriş sayfası \_Layout. cshtml şablonumuzu kullanıyor ve bu nedenle hoş geldiniz iletisi standart site HTML düzeni içinde yer alıyor.

## <a name="using-a-model-to-pass-information-to-our-view"></a>Görünümümüze bilgi geçirmek için bir model kullanma

Yalnızca sabit kodlanmış HTML 'yi görüntüleyen bir görünüm şablonu, çok ilgi çekici bir Web sitesi yapamıyor. Dinamik bir Web sitesi oluşturmak için, denetleyici eylemlerimizden görünüm Şablonlarımıza bilgi geçirmek istiyoruz.

Model-View-Controller düzeninde model terimi, uygulamadaki verileri temsil eden nesneleri ifade eder. Genellikle, model nesneleri veritabanınızdaki tablolara karşılık gelir, ancak bunlara gerek kalmaz.

Bir ActionResult döndüren denetleyici eylemi metotları bir model nesnesini görünüme geçirebilir. Bu, bir denetleyicinin yanıt oluşturmak için gereken tüm bilgileri düzgün bir şekilde paketleyip bu bilgileri uygun HTML yanıtını oluşturmak için kullanılacak bir görünüm şablonuna iletmesini sağlar. Bu işlemin anlaşılması en kolay yöntemdir. bu nedenle kullanmaya başlayın.

İlk olarak, mağazamız içindeki tarzları ve albümleri temsil eden bazı model sınıfları oluşturacağız. Bir tarz sınıfı oluşturarak başlayalım. Projenizin içindeki "modeller" klasörüne sağ tıklayın, "Sınıf Ekle" seçeneğini belirleyin ve "Genre.cs" dosyasını adlandırın.

![](mvc-music-store-part-3/_static/image2.jpg)

![](mvc-music-store-part-3/_static/image9.png)

Ardından oluşturulan sınıfa ortak bir dize adı özelliği ekleyin:

[!code-csharp[Main](mvc-music-store-part-3/samples/sample7.cs)]

*Note: merak ediyorsanız, {get; set;} gösterimi, otomatik olarak C#uygulanan özellikler özelliğinin kullanımını yapıyor. Bu, bir destek alanı bildirmek zorunda kalmadan bir özelliğin avantajlarından yararlanmanızı sağlar.*

Ardından, bir başlık ve bir tarz özelliği olan bir albüm sınıfı (Album.cs adlı) oluşturmak için aynı adımları izleyin:

[!code-csharp[Main](mvc-music-store-part-3/samples/sample8.cs)]

Artık, modelinizdeki dinamik bilgileri görüntüleyen görünümleri kullanmak için StoreController 'ı değiştirebiliriz. Daha önce tanıtım amaçlı olarak, istek KIMLIĞINE göre albümlerimizi adlandırdık, bu bilgileri aşağıdaki görünümde olduğu gibi görüntüleyebiliriz.

![](mvc-music-store-part-3/_static/image10.png)

Mağaza ayrıntıları eylemini değiştirerek başlayacağız, bu nedenle tek bir albümün bilgilerini gösterir. MvcMusicStore. model ad alanını dahil etmek için **Storecontrollers** sınıfının en üstüne bir "Using" ifadesini ekleyin. bu nedenle, albüm sınıfını kullanmak istediğimiz her seferinde MvcMusicStore. modeller. albümünü yazmanız gerekmez. Bu sınıfın "kullanımlar" bölümü şimdi aşağıda gösterildiği gibi görünmelidir.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample9.cs)]

Daha sonra, HomeController 'ın Dizin yöntemiyle yaptığımız gibi, bir dize yerine bir ActionResult döndüren Ayrıntılar denetleyicisi eylemini güncelleştireceğiz.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample10.cs)]

Şimdi görünüme bir albüm nesnesi döndürecek mantığı değiştirebiliriz. Bu öğreticide daha sonra verileri bir veritabanından alacak, ancak şu anda başlamak için "kukla verileri" kullanacağız.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample11.cs)]

*Note: hakkında bilginiz varsa C#, bunu kullanarak, albüm değişkenimizin geç bağlantılı olduğu anlamına gelebilir. Bu doğru değildir: C# derleyici, albümün albüm türünde olduğunu belirlemek ve yerel albüm değişkenini bir albüm türü olarak derlemek için değişkene neleri atadığımızda tür çıkarımı kullanıyor, bu nedenle derleme zamanı denetimi ve Visual Studio kod Düzenleyicisi desteği sunuyoruz.*

Şimdi de HTML yanıtı oluşturmak için albümümüzü kullanan bir görünüm şablonu oluşturalım. Bunu yapmadan önce, görünümü Ekle iletişim kutusu yeni oluşturulan albüm sınıfınızı hakkında bilgi sahibi olacak şekilde projeyi derliyoruz. Projeyi, hata ayıkla ⇨ Build MvcMusicStore menü öğesini seçerek oluşturabilirsiniz (ek kredi için, projeyi derlemek için Ctrl-Shift-B kısayolunu kullanabilirsiniz).

![](mvc-music-store-part-3/_static/image11.png)

Artık destekleyici sınıflarınızı ayarladığımıza göre, görünüm şablonumuzu oluşturmaya hazır olduğumuz. Ayrıntılar yöntemine sağ tıklayın ve "Görünüm Ekle..." öğesini seçin. bağlam menüsünden.

![](mvc-music-store-part-3/_static/image12.png)

HomeController 'tan önce yaptığımız gibi yeni bir görünüm şablonu oluşturacağız. Bunu StoreController 'dan oluşturduğumuz için varsayılan olarak \Views\store\ındex.cshtml dosyasında oluşturulacaktır.

Daha önce olduğu gibi, "kesin olarak belirlenmiş bir" görünümü oluşturma onay kutusunu denetleyeceğiz. Daha sonra "veri sınıfı görüntüle" aşağı açılan listesinde "albüm" sınıfınızı seçeceğiz. Bu, "Görünüm Ekle" iletişim kutusunun bir albüm nesnesinin kullanmak üzere geçirilmesini bekleyen bir görünüm şablonu oluşturmasına neden olur.

![](mvc-music-store-part-3/_static/image13.png)

\Views\Store\Details.cshtml görünüm şablonumuz "Ekle" düğmesine tıkladığımızda, aşağıdaki kodu içeren oluşturulacak.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample12.cshtml)]

Bu görünümün, albüm sınıfımızda kesin olarak yazılmış olduğunu gösteren ilk satıra dikkat edin. Razor görünümü altyapısı, bir albüm nesnesi geçtiğini anladığından, model özelliklerine kolayca erişebilmemiz ve hatta Visual Web Developer Editor 'da IntelliSense 'in avantajlarından yararlanabiliyoruz.

&lt;H2&gt; etiketini, bu satırı aşağıdaki gibi görünecek şekilde değiştirerek albümün title özelliğini görüntüleyecek şekilde güncelleştirin.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample13.cshtml)]

@Model anahtar sözcüğünden sonra, albüm sınıfının desteklediği özellikleri ve yöntemleri göstererek, IntelliSense 'in tetiklendiğine dikkat edin.

Şimdi projemizi yeniden çalıştırıp/Store/Details/5 URL 'sini ziyaret edin. Aşağıdaki gibi bir albümün ayrıntılarını görebiliriz.

![](mvc-music-store-part-3/_static/image14.png)

Şimdi mağaza tarama eylemi yöntemine benzer bir güncelleştirme yapacağız. Yöntemi bir ActionResult döndüren şekilde güncelleştirin ve yöntem mantığını yeni bir tarz nesnesi oluşturacak ve görünüme döndüren şekilde değiştirin.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample14.cs)]

Tarayıcı yöntemine sağ tıklayın ve "Görünüm Ekle..." seçeneğini belirleyin. bağlam menüsünden, türü kesin belirlenmiş bir görünüm ekleyin ve tarz sınıfına kesin bir tür ekleyin.

![](mvc-music-store-part-3/_static/image15.png)

Görünüm kodundaki &lt;H2&gt; öğesini (/Views/Store/Browse.cshtml 'de), tarz bilgilerini görüntülemek için güncelleştirin.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample15.cshtml)]

Şimdi, projemizi yeniden çalıştırıp/Store/zat mı gözatalim? Tarz = disco URL 'SI. Aşağıda gösterildiği gibi, gözden geçirme sayfasını görüyoruz.

![](mvc-music-store-part-3/_static/image16.png)

Son olarak, **Depolama dizini** eylem yöntemine biraz daha karmaşık bir güncelleştirme yapalim ve mağazamızda tüm tarzın bir listesini görüntülemek için görünümü. Yalnızca tek bir tarz yerine model nesnemiz olarak bir tarzın listesini kullanarak bunu yapacağız.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample16.cs)]

Depolama dizini eylem yöntemine sağ tıklayın ve Görünüm Ekle ' yi seçin, model sınıfı olarak tarz ' ı seçin ve Ekle düğmesine basın.

![](mvc-music-store-part-3/_static/image17.png)

İlk olarak, görünümün yalnızca bir tane yerine birkaç tarz nesne isteyeceğini göstermek için @model bildirimini değiştireceksiniz. /Store/Index.cshtml adlı ilk satırı aşağıdaki gibi okunacak şekilde değiştirin:

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample17.cshtml)]

Bu, Razor görünüm altyapısına, çeşitli tarz nesneleri tutabilecek bir model nesnesiyle çalışmayacağını söyler. Daha genel olduğundan, model türümüzü daha sonra IEnumerable arabirimini destekleyen herhangi bir nesne türüne değiştirebilmemiz için, bir liste&lt;tarzı&gt; yerine IEnumerable&lt;tarz&gt; kullanıyoruz.

Daha sonra, aşağıdaki tamamlanan görünüm kodunda gösterildiği gibi modeldeki tarz nesneleri arasında döngü göndereceğiz.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample18.cshtml)]

"@Model" yazdığımızda, bu kodu girdiğimiz için tam IntelliSense desteğine sahip olduğumuz hakkında dikkat edin. tür tarzı IEnumerable tarafından desteklenen tüm yöntemleri ve özellikleri görüyoruz.

![](mvc-music-store-part-3/_static/image18.png)

"Foreach" döngümiz dahilinde, Visual Web Developer her öğenin tarz türünde olduğunu bilir, bu nedenle her tarz türü için IntelliSense 'i görüyoruz.

![](mvc-music-store-part-3/_static/image19.png)

Daha sonra, yapı iskelesi özelliği tarz nesnesini inceledi ve her birinin bir Name özelliğine sahip olduğunu tespit eder, bu nedenle aralarında geçiş yapın ve yazar. Ayrıca, her bir öğe için düzenleme, Ayrıntılar ve silme bağlantıları da oluşturur. Daha sonra Store Manager 'da bundan sonra faydalanıyoruz, ancak şimdilik basit bir liste kullanmak istiyoruz.

Uygulamayı çalıştırıp/Store 'a gözattığınızda, her iki tür için de sayım listesinin görüntülendiğini görüyoruz.

![](mvc-music-store-part-3/_static/image20.png)

## <a name="adding-links-between-pages"></a>Sayfalar arasında bağlantı ekleme

Tarzımızı listeleyen/Store URL 'SI Şu anda yalnızca düz metin olarak tarz adlarını listelemektedir. Bunu, düz metin yerine uygun/Store/gözam URL 'sine sahip olacak şekilde değiştirelim. böylece, "Disco" gibi bir müzik tarzında tıklatmak/Store/gözatmaya mi? tarzı = disco URL 'sine gidecektir. Aşağıdaki kodu kullanarak bu bağlantıları çıkarmak için \Views\store\ındex.cshtml görünüm şablonumuzu güncelleştirebiliriz **(bunun üzerinde iyileştireceğiz)** :

[!code-html[Main](mvc-music-store-part-3/samples/sample19.html)]

Bu, daha sonra, sorunsuz kodlanmış bir dizeye dayandığından sorun oluşmasına neden olabilir. Örneğin, denetleyiciyi yeniden adlandırmak istiyoruz, güncelleştirilebilmemiz gereken bağlantıları arayan kodunuzda arama yapmanız gerekir.

Bir alternatif yaklaşım, bir HTML yardımcı yönteminden faydalanabilir. ASP.NET MVC, görüntüleme şablonu kodumuzda olduğu gibi çeşitli yaygın görevleri gerçekleştirmek için kullanılabilen HTML Yardımcısı yöntemlerini içerir. HTML. ActionLink () yardımcı yöntemi özellikle yararlıdır ve HTML &lt;&gt; bağlantıları oluşturmayı kolaylaştırır ve URL yollarının düzgün şekilde URL kodlamalı olduğundan emin olmak için bu ayrıntıları ele alır.

HTML. ActionLink (), bağlantılarınız için ihtiyaç duyduğunuz kadar çok bilgi belirtilmesine izin veren birkaç farklı aşırı yüklemeye sahiptir. En basit durumda, köprünün istemcide tıklandığı zaman gitmek için yalnızca bağlantı metnini ve eylem yöntemini sağlarsınız. Örneğin, mağaza ayrıntıları sayfasındaki "/Store/" dizinine bağlantı metni "Store dizinine git" bağlantısını, aşağıdaki çağrıyı kullanarak bağlayabiliriz:

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample20.cshtml)]

*Note: Bu durumda, yalnızca geçerli görünümü işleyen Denetleyici içindeki başka bir eyleme bağlanmakta olduğumuz için denetleyici adını belirtmemiz gerekmiyordu.*

Tarama sayfasına yönelik bağlantılarımız bir parametre geçirmemiz gerekir, ancak üç parametre alan HTML. ActionLink yönteminin başka bir aşırı yüklemesini kullanacağız:

- 1. Bağlantı metni, bu tarz adı görüntülenecektir
- 2. Denetleyici eylem adı (tarama)
- 3. Ad (tarz) ve değer (tarzı adı) belirterek rota parametre değerleri

Bunu bir araya getirmek, bu bağlantıları mağaza dizini görünümüne yazdığımızda şöyle olacaktır:

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample21.cshtml)]

Şimdi projemizi yeniden çalıştırıp/Store/URL 'ye eriştiğinizde, tarzın bir listesini görürsünüz. Her bir tarz bir köprüdür. tıklandıklarında, bu bir köprü,/Store/gözatmaya mi? tarzı = *[tarz]* URL 'imize götürür.

![](mvc-music-store-part-3/_static/image3.jpg)

Tarz listesinin HTML 'si şöyle görünür:

[!code-html[Main](mvc-music-store-part-3/samples/sample22.html)]

> [!div class="step-by-step"]
> [Önceki](mvc-music-store-part-2.md)
> [İleri](mvc-music-store-part-4.md)
