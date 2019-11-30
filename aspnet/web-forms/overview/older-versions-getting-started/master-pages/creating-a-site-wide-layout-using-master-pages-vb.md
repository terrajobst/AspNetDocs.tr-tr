---
uid: web-forms/overview/older-versions-getting-started/master-pages/creating-a-site-wide-layout-using-master-pages-vb
title: Ana sayfaları kullanarak site genelinde bir düzen oluşturma (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, ana sayfa temelleri gösterilir. Yani, ana sayfa nedir, bir ana sayfa oluşturma, içerik yeri sahipleri nedir, bir CR...
ms.author: riande
ms.date: 05/21/2008
ms.assetid: 30945276-8ed9-4b27-8e50-4309244d3559
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/creating-a-site-wide-layout-using-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: c0ee6ed9d944b9a8ff2b2996e93706b8416de905
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74584171"
---
# <a name="creating-a-site-wide-layout-using-master-pages-vb"></a>Ana Sayfaları Kullanarak Site Geneli Bir Düzen Oluşturma (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_01_VB.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_01_VB.pdf)

> Bu öğreticide, ana sayfa temelleri gösterilir. Yani, ana sayfa nedir, bir ana sayfa oluşturma, içerik yeri sahipleri nedir, bir ana sayfa kullanan bir ASP.NET sayfası oluşturma, ana sayfanın nasıl değiştirileceği, ilişkili içerik sayfalarına otomatik olarak yansıtılmıştır ve bu şekilde devam eder.

## <a name="introduction"></a>Giriş

İyi tasarlanmış bir Web sitesinin bir özniteliği, site genelinde tutarlı bir sayfa düzenidir. Örneğin, www.asp.net Web sitesini alın. Bu yazma sırasında, her sayfada sayfanın üst ve alt kısmında aynı içerik bulunur. Şekil 1 ' de gösterildiği gibi, her sayfanın en üst kısmında Microsoft Communities listesi bulunan gri bir çubuk görüntülenir. Bu, site logosu, sitenin çevrildiği dillerin listesi ve temel bölümler: giriş, Başlarken, öğrenme, Indirmeler vs. Benzer şekilde, sayfanın en altında www.asp.net üzerinde reklam, bir telif hakkı bildirimi ve gizlilik bildirimine yönelik bir bağlantı hakkında bilgiler yer alır.

[![www.asp.net Web sitesi tüm sayfalarda tutarlı bir görünüm kullanır](creating-a-site-wide-layout-using-master-pages-vb/_static/image2.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image1.png)

<strong>Şekil 01</strong>: www.asp.NET Web sitesi tüm sayfalarda tutarlı bir görünüm kullanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-site-wide-layout-using-master-pages-vb/_static/image3.png))

İyi tasarlanmış bir sitenin başka bir özniteliği, sitenin görünümünün değiştirilebildiği kolaylığıdır. Şekil 1 Mart 2008 ' den itibaren www.asp.net giriş sayfasını gösterir, ancak şu anda ve Bu öğreticinin yayını arasında görünüm değişmiş olabilir. Büyük olasılıkla, üstteki menü öğeleri MVC çerçevesi için yeni bir bölüm içerecek şekilde genişletilir. Ya da belki de farklı renkler, yazı tipleri ve düzen içeren, daha az yeni bir tasarım yok edilecek. Tüm sitede bu tür değişiklikler uygulandığında, siteyi oluşturan binlerce web sayfasının değiştirilmesini gerektirmeyen hızlı ve basit bir süreç olmalıdır.

ASP.NET içinde site genelinde sayfa şablonu oluşturmak, *ana sayfaların*kullanımı aracılığıyla mümkündür. Bir Nutshell 'de, ana sayfa, tüm *içerik sayfaları* arasında ortak olan ve içeriğe göre içerik sayfası temelinde özelleştirilebilen olan bir ASP.NET sayfa türüdür. (İçerik sayfası, ana sayfaya bağlanan bir ASP.NET sayfasıdır.) Ana sayfanın yerleşimi veya biçimlendirmesi değiştirildiğinde, tüm içerik sayfalarının çıktısı benzer şekilde güncelleştirilir ve bu da site genelinde görünüm değişikliklerinin tek bir dosyayı güncelleştirme ve dağıtma (yani, ana sayfa) kadar kolay hale gelir.

Bu, ana sayfaları kullanarak araştıran bir öğretici serisinin ilk öğreticisidir. Bu öğretici serisinin konusu boyunca şunları yaptık:

- Ana sayfaları ve ilişkili içerik sayfalarını oluşturmayı inceleyin,
- Çeşitli ipuçları, püf noktaları ve yakalamaları tartışın
- Ortak ana sayfa tuzarını belirler ve geçici çözümleri keşfet
- Bkz. bir içerik sayfasından ana sayfaya erişme ve tam tersi,
- Çalışma zamanında bir içerik sayfasının ana sayfasını belirtmeyi öğrenin ve
- Diğer Gelişmiş Ana sayfa konuları.

Bu öğreticilerin kısa olması ve işlem boyunca görsel olarak size yol göstermek için çok sayıda ekran görüntüsü ile adım adım yönergeler sağlaması gerekir. Her öğretici, C# ve Visual Basic sürümlerde mevcuttur ve kullanılan kodun tamamını karşıdan yükleme içerir.

Bu ınaugural öğreticisi ana sayfa temelleri hakkında bir görünüm ile başlar. Ana sayfaların nasıl çalıştığını anladık, Visual Web Developer kullanarak ana sayfa ve ilişkili içerik sayfaları oluşturma konusuna bakın ve bir ana sayfadaki değişikliklerin hemen içerik sayfalarında nasıl yansıtıldığını görün. Haydi başlayın!

## <a name="understanding-how-master-pages-work"></a>Ana sayfaların nasıl çalıştığını anlama

Site genelinde tutarlı sayfa düzenine sahip bir Web sitesi oluşturmak için, her bir Web sayfasının özel içeriğine ek olarak ortak biçimlendirme işaretlemesini yaymalıdır. Örneğin, www.asp.net üzerinde her bir öğretici veya forum, kendi benzersiz içeriğine sahip olsa da, bu sayfaların her biri, üst düzey bölüm bağlantılarını görüntüleyen bir dizi ortak `<div>` öğesini de işler: giriş, Başlarken, öğrenme vb.

Tutarlı bir görünüm ile Web sayfaları oluşturmaya yönelik çeşitli teknikler vardır. Bir Naïve yaklaşımı, yaygın düzen işaretlemesini tüm Web sayfalarına kopyalayıp yapıştırmaktır, ancak bu yaklaşım bir dizi küçük tarafa sahiptir. Başlangıçlara, her yeni sayfa oluşturulduğunda, paylaşılan içeriği kopyalayıp sayfaya yapıştırmayı unutmamalısınız. Yanlışlıkla paylaşılan biçimlendirmenin yalnızca bir alt kümesini yeni bir sayfaya kopyalayabilmeniz için, bu tür kopyalama ve yapıştırma işlemleri hata için tasarlanmıştır. Ayrıca, bu yaklaşım, yeni görünümü kullanmak için sitedeki her bir sayfanın düzenlenmesi gerektiğinden, mevcut site genelinde görünümün yeni bir sorun ile değiştirilmesini sağlar.

ASP.NET sürüm 2,0 ' den önce, sayfa geliştiricileri genellikle [kullanıcı denetimlerinde](https://msdn.microsoft.com/library/y6wb1a0e.aspx) ortak biçimlendirme yerleştirir ve sonra her sayfaya ve her sayfaya bu kullanıcı denetimlerini ekledi. Bu yaklaşım, sayfa Geliştiricinin kullanıcı denetimlerini her yeni sayfaya el ile eklemeyi anımsamasını, ancak ortak biçimlendirmeyi yalnızca değiştirilmesi gereken kullanıcı denetimlerine göre güncelleştirirken daha kolay değişiklikler için izin verileceğini gerektirdi. Ne yazık ki, Visual Studio .NET 2002 ve 2003-ASP.NET 1. x uygulamaları için kullanılan Visual Studio sürümleri Tasarım görünümü gri kutular olarak. Sonuç olarak, bu yaklaşımı kullanan sayfa geliştiricileri bir WYSıWYG tasarım zamanı ortamının keyfini çıkarmadı.

Kullanıcı denetimlerini kullanmanın eksiketleri, *ana sayfaların*sunumıyla ASP.NET sürüm 2,0 ve Visual Studio 2005 ' de giderilmiştir. Ana sayfa, hem site genelinde biçimlendirmeyi hem de ilişkili *içerik sayfalarının* özel işaretlemesini tanımladığı *bölgeleri* tanımlayan özel bir tür ASP.net sayfasıdır. Adım 1 ' de göreceğiniz gibi, bu bölgeler ContentPlaceHolder denetimleri tarafından tanımlanır. ContentPlaceHolder denetimi, ana sayfanın denetim hiyerarşisinde özel içeriğin bir içerik sayfası tarafından eklenmesi için bir konum belirtir.

> [!NOTE]
> Ana sayfaların temel kavramları ve işlevleri ASP.NET sürüm 2,0 ' den beri değişmemiştir. Ancak Visual Studio 2008, Visual Studio 2005 ' de olmayan bir özellik olan iç içe yerleştirilmiş ana sayfalar için tasarım zamanı desteği sunar. Daha sonraki bir öğreticide iç içe geçmiş ana sayfaları kullanma bölümüne bakacağız.

Şekil 2 www.asp.net için ana sayfanın nasıl görünebileceğini gösterir. Ana sayfanın, her bir Web sayfası için benzersiz içeriklerin bulunduğu her sayfanın üst, alt ve sağ tarafında, her sayfanın en üstünde, altında ve sağında yer alan biçimlendirme ve sol tarafta bulunan bir ContentPlaceHolder tanımladığına unutmayın.

![Bir ana sayfa, içerik sayfası sayfa temelinde, site genelinde düzen ve düzenlenebilir bölgeleri tanımlar](creating-a-site-wide-layout-using-master-pages-vb/_static/image4.png)

**Şekil 02**: bir ana sayfa, Içerik sayfası sayfa temelinde, site genelinde düzen ve düzenlenebilir bölgeleri tanımlar

Ana sayfa tanımlandıktan sonra, bir onay kutusu ile yeni ASP.NET sayfalarına bağlanabilir. Bu ASP.NET sayfaları-adlandırılan içerik sayfaları-ana sayfanın ContentPlaceHolder denetimlerinin her biri için bir Içerik denetimi ekleyin. İçerik sayfası bir tarayıcı aracılığıyla ziyaret edildiğinde, ASP.NET altyapısı ana sayfanın denetim hiyerarşisini oluşturur ve içerik sayfasının denetim hiyerarşisini uygun yerlere çıkartır. Bu Birleşik denetim hiyerarşisi işlenir ve sonuçta elde edilen HTML, son kullanıcının tarayıcısına döndürülür. Sonuç olarak, içerik sayfası, kendi ana sayfasında tanımlanmış olan ve kendi Içerik denetimlerinde tanımlanan sayfaya özgü biçimlendirmenin bulunduğu ortak biçimlendirmeyi yayar. Şekil 3 ' te bu kavram gösterilmektedir.

[Istenen sayfanın biçimlendirmesinin ana sayfada Fkullanılma ![](creating-a-site-wide-layout-using-master-pages-vb/_static/image6.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image5.png)

**Şekil 03**: Istenen sayfanın biçimlendirmesi ana sayfada fkullanılma yapılır ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-site-wide-layout-using-master-pages-vb/_static/image7.png))

Ana sayfaların nasıl çalıştığını tartıştığımız için, Visual Web Developer kullanarak bir ana sayfa ve ilişkili içerik sayfaları oluşturmaya göz atalım.

> [!NOTE]
> Mümkün olan en geniş kitleye ulaşmak için, bu öğretici serisi boyunca derduğumuz ASP.NET Web sitesi Microsoft 'un ücretsiz Visual Studio 2008, [Visual Web Developer 2008](https://www.microsoft.com/express/vwd/)sürümü ile ASP.NET 3,5 kullanılarak oluşturulacaktır. Henüz ASP.NET 3,5 sürümüne yükseltmezseniz, bu öğreticilerde ele alınan kavramlar ASP.NET 2,0 ve Visual Studio 2005 ile aynı şekilde çalışır. Ancak bazı tanıtım uygulamaları, .NET Framework sürüm 3,5 ' deki yeni özellikleri kullanabilir; 3,5 'e özgü özellikler kullanıldığında, sürüm 2,0 ' de benzer işlevselliği nasıl uygulayacağınızı ele alan bir notim dahil ediyorum. Her öğreticiden indirileceği tanıtım uygulamalarının, 3,5 özel yapılandırma öğelerini içeren bir `Web.config` dosyası ile sonuçlanan .NET Framework sürüm 3,5 ' i hedeflemesini aklınızda bulundurun. Uzun hikaye kısa, henüz bilgisayarınıza .NET 3,5 ' i yüklemeniz gerekiyorsa indirilebilir web uygulaması, `Web.config`' den önce 3,5 özel biçimlendirmeyi kaldırmadan çalışmaz. Bu konuyla ilgili daha fazla bilgi için bkz. [ASP.NET sürüm 3.5 'in `Web.config` dosyası](http://www.4guysfromrolla.com/articles/121207-1.aspx) .

## <a name="step-1-creating-a-master-page"></a>1\. Adım: Ana sayfa oluşturma

Ana ve içerik sayfalarını oluşturmak ve kullanmak için önce bir ASP.NET Web sitesine ihtiyacımız var. Yeni bir dosya sistemi tabanlı ASP.NET Web sitesi oluşturarak başlayın. Bunu gerçekleştirmek için, Visual Web Developer 'ı başlatın ve ardından Dosya menüsüne gidin ve yeni Web sitesi ' ni seçin, yeni Web sitesi iletişim kutusunu (bkz. Şekil 4) görüntüleyin. ASP.NET Web sitesi şablonunu seçin, Konum açılır listesini dosya sistemi olarak ayarlayın, Web sitesini yerleştirmek için bir klasör seçin ve dili Visual Basic olarak ayarlayın. Bu, bir `Default.aspx` ASP.NET sayfası, bir `App_Data` klasörü ve bir `Web.config` dosyası ile yeni bir Web sitesi oluşturur.

> [!NOTE]
> Visual Studio, iki proje yönetimi modunu destekler: Web sitesi projeleri ve Web uygulaması projeleri. Web sitesi projelerinin proje dosyası olmadığından, Web uygulaması projeleri Visual Studio .NET 2002/2003 'deki proje mimarisini taklit ederken, proje dosyası içerirler ve projenin kaynak kodunu `/bin` klasörüne yerleştirilmiş tek bir derlemede derler. Visual Studio 2005 başlangıçta yalnızca desteklenen Web sitesi projeleri, ancak Web uygulaması proje modeli Service Pack 1 ile yeniden kullanılmaya başlandı; Visual Studio 2008, her iki proje modelini de sunmaktadır. Ancak, Visual Web Developer 2005 ve 2008 sürümleri yalnızca Web sitesi projelerini destekler. Bu öğretici serisinde tanıtımlar için Web sitesi proje modelini kullanıyorum. Express olmayan bir sürüm kullanıyorsanız ve bunun yerine [Web uygulaması proje modelini](https://msdn.microsoft.com/library/aa730880(vs.80).aspx) kullanmak istiyorsanız, ekranınızda gördüklerinizle ilgili bazı tutarsızlıklar olabileceğini ve bu öğreticilerde sunulan ekran görüntülerini ve yönergeleri izlemeniz gereken adımları aklınızda bulundurun.

[![yeni bir dosya sistemi tabanlı Web sitesi oluşturma](creating-a-site-wide-layout-using-master-pages-vb/_static/image9.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image8.png)

**Şekil 04**: yeni bir dosya sistemi tabanlı Web sitesi oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-site-wide-layout-using-master-pages-vb/_static/image10.png))

Daha sonra, proje adına sağ tıklayıp, yeni öğe Ekle ' yi seçip ana sayfa şablonunu seçerek kök dizindeki siteye bir ana sayfa ekleyin. Ana sayfaların uzantı `.master`bitiş olduğunu unutmayın. Bu yeni ana sayfayı `Site.master` adlandırın ve Ekle ' ye tıklayın.

[Web sitesine site. Master adlı bir ana sayfa eklemek ![](creating-a-site-wide-layout-using-master-pages-vb/_static/image12.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image11.png)

**Şekil 05**: web sitesine `Site.master` adlı ana sayfa ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-site-wide-layout-using-master-pages-vb/_static/image13.png))

Visual Web Developer aracılığıyla yeni bir ana sayfa dosyası eklemek, aşağıdaki bildirim temelli işaretlerle bir ana sayfa oluşturur:

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample1.aspx)]

Bildirim temelli biçimlendirmenin ilk satırı [`@Master` yönergedir](https://msdn.microsoft.com/library/ms228176.aspx). `@Master` yönergesi, ASP.NET sayfalarında görünen [`@Page` yönergesine](https://msdn.microsoft.com/library/ydy4x04a.aspx) benzerdir. Sunucu tarafı dili (VB) ve ana sayfanın arka plan kod sınıfının konumu ve devralması hakkındaki bilgileri tanımlar.

`DOCTYPE` ve sayfanın bildirim temelli biçimlendirme `@Master` yönergesinin altında görünür. Sayfa, dört sunucu tarafı denetimi ile birlikte statik HTML içerir:

- **Bir Web formu (`<form runat="server">`)** -tüm ASP.NET sayfalarında genellikle bir Web formu olduğundan ve ana sayfa bir Web formu içinde görünmesi gereken Web denetimlerini Içerebildiğinden, Web formunu ana sayfanıza eklediğinizden emin olun (her bir Içerik sayfasına Web formu eklemek yerine).
- **`ContentPlaceHolder1`adlı bir ContentPlaceHolder denetimi** Web formu içinde görünür ve içerik sayfasının Kullanıcı arabirimi için bölge görevi görür.
- **Sunucu tarafı `<head>` öğesi** -`<head>` öğesi `runat="server"` özniteliğe sahiptir ve sunucu tarafı kodu aracılığıyla erişilebilir hale getirir. `<head>` öğesi bu şekilde uygulanır, böylece sayfa başlığı ve diğer `<head>`ilgili biçimlendirme programlı bir şekilde eklenebilir veya ayarlanabilir. Örneğin, bir ASP.NET sayfasının `Title` özelliği ayarlandığında `<head>` sunucu denetimi tarafından oluşturulan `<title>` öğesi değişir.
- **`head`adlı ContentPlaceHolder denetimi** , `<head>` sunucu denetimi içinde görünür ve `<head>` öğesine bildirimli olarak içerik eklemek için kullanılabilir.

Bu varsayılan ana sayfa bildirim temelli biçimlendirme, kendi ana sayfalarınızı tasarlamak için bir başlangıç noktası olarak görev yapar. Ana sayfaya daha fazla Web denetimi veya Contentyertutucuları eklemek için veya HTML 'yi düzenleyebilirsiniz.

> [!NOTE]
> Ana sayfa tasarlarken, ana sayfanın bir Web formu içerdiğinden ve en az bir ContentPlaceHolder denetiminin bu Web formu içinde göründüğünden emin olun.

### <a name="creating-a-simple-site-layout"></a>Basit bir site düzeni oluşturma

Tüm sayfaların paylaştığı bir site düzeni oluşturmak için `Site.master`varsayılan bildirim temelli işaretlemesini genişletelim: ortak üst bilgi; Gezinti, Haberler ve diğer site genelinde içeriğe sahip bir sol sütun; ve "Microsoft ASP.NET ile güçlendirilmiştir" simgesini görüntüleyen bir altbilgi. Şekil 6, içerik sayfalarından biri tarayıcı aracılığıyla görüntülenirken ana sayfanın nihai sonucunu gösterir. Şekil 6 ' daki kırmızı daire içinde, ziyaret edilen sayfaya özgü (`Default.aspx`); diğer içerik ana sayfada tanımlanmıştır ve bu nedenle tüm içerik sayfalarında tutarlıdır.

[Ana sayfa ![üst, sol ve alt bölümleri için biçimlendirmeyi tanımlar](creating-a-site-wide-layout-using-master-pages-vb/_static/image15.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image14.png)

**Şekil 06**: Ana sayfa üst, sol ve alt bölümlerin işaretlemesini tanımlar ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-site-wide-layout-using-master-pages-vb/_static/image16.png))

Şekil 6 ' da gösterilen site düzenine ulaşmak için `Site.master` ana sayfasını aşağıdaki bildirim temelli biçimlendirmeyi içerecek şekilde güncelleştirerek başlayın:

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample2.aspx)]

Ana sayfanın düzeni bir dizi `<div>` HTML öğesi kullanılarak tanımlanır. `topContent` `<div>`, her sayfanın üst kısmında görüntülenen biçimlendirmeyi içerir, ancak `mainContent`, `leftContent`ve `footerContent` `<div>`, sırasıyla sayfanın içeriğini, sol sütununu ve "Microsoft ASP.NET ile destekleniyor" simgesini göstermek için kullanılır. Bu `<div>` öğelerini eklemenin yanı sıra, birincil ContentPlaceHolder denetiminin `ID` özelliğini `MainContent``ContentPlaceHolder1` olarak yeniden adlandırdım.

Bu assıralanmış `<div>` öğelerinin biçimlendirme ve düzen kuralları, ana sayfanın `<head>` öğesindeki bir `<link>` öğesi aracılığıyla belirtilen [basamaklı stil sayfası (CSS)](http://en.wikipedia.org/wiki/Cascading_Style_Sheets) dosyasında `Styles.css`. Bu çeşitli kurallar, yukarıda belirtilen her bir `<div>` öğesinin görünümünü tanımlar. Örneğin, "Ana sayfa öğreticilerini" metin ve bağlantıyı gösteren `topContent` `<div>` öğesi, aşağıdaki şekilde `Styles.css` belirtilen biçimlendirme kurallarına sahiptir:

[!code-css[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample3.css)]

Bilgisayarınızda ve ' yi takip ediyorsanız, Bu öğreticinin eşlik eden kodunu indirmeniz ve `Styles.css` dosyasını projenize eklemeniz gerekir. Benzer şekilde, `Images` adlı bir klasör oluşturmanız ve indirilen tanıtım Web sitesinden projenize "Microsoft ASP.NET ile güçlendirilmiştir" simgesini kopyalamanız gerekir.

> [!NOTE]
> CSS ve Web sayfası biçimlendirmesindeki bir tartışma, bu makalenin kapsamı dışındadır. CSS hakkında daha fazla bilgi için [w3schools.com](http://www.w3schools.com/)adresindeki [CSS öğreticilerine](http://www.w3schools.com/css/default.asp) göz atın. Ayrıca, farklı biçimlendirme kurallarının etkilerini görmek için Bu öğreticinin eşlik eden kodunu indirip `Styles.css` CSS ayarlarıyla oynamanızı da teşvik ediyorum.

### <a name="creating-a-master-page-using-an-existing-design-template"></a>Mevcut bir tasarım şablonunu kullanarak ana sayfa oluşturma

Küçük ve orta ölçekli şirketler için çok sayıda ASP.NET Web uygulaması derlendim. İstemcilerimin bazılarında kullanmak istedikleri mevcut bir site düzeni vardı; Diğerleri bir uzmanlık grafik tasarımcısını işe yarsın. Web sitesi yerleşimini tasarlamaktan birkaç güvenilir. Şekil 6 ' ya göre söylebilirken, bir Web sitesinin yerleşimini tasarlayabilmeniz için bir programcı genellikle sizin için bir programcinizin vergi, vergilerinizi yaparken açık kalp olma oranı gerçekleştirmesini sağlar.

Neyse ki, ücretsiz HTML tasarım şablonları sunan çok sayıda Web sitesi vardır. Google, "Ücretsiz Web sitesi şablonları" arama terimi için 6.000.000 'den fazla sonuç döndürdü. En sevdiğiniz olanlardan biri [OpenDesigns.org](http://opendesigns.org/). İstediğiniz bir Web sitesi şablonunu bulduktan sonra, Web sitesi projenize CSS dosyalarını ve görüntülerini ekleyin ve şablonun HTML 'sini ana sayfanız ile tümleştirin.

> [!NOTE]
> Microsoft ayrıca, Visual Studio 'daki yeni Web sitesi iletişim kutusuyla tümleştirilen çeşitli [ücretsiz ASP.net tasarım başlatma seti şablonları](https://msdn.microsoft.com/asp.net/aa336613.aspx) sunmaktadır.

## <a name="step-2-creating-associated-content-pages"></a>2\. Adım: Ilişkili Içerik sayfaları oluşturma

Ana sayfa oluşturulduğunda, ana sayfaya bağlanan ASP.NET sayfaları oluşturmaya başlamaya hazırız. Bu tür sayfalar *içerik sayfaları*olarak adlandırılır.

Projeye yeni bir ASP.NET sayfası ekleyelim ve `Site.master` ana sayfasına bağlayalim. Çözüm Gezgini ' de proje adına sağ tıklayın ve yeni öğe Ekle seçeneğini belirleyin. Web formu şablonunu seçin, `About.aspx`adı girin ve ardından şekil 7 ' de gösterildiği gibi "ana sayfayı seçin" onay kutusunu işaretleyin. Bunu yapmak, ana sayfa Seç iletişim kutusunu (bkz. Şekil 8), kullanılacak ana sayfayı seçebileceğiniz yerden gösterir.

> [!NOTE]
> Web sitesi proje modeli yerine Web uygulaması proje modelini kullanarak ASP.NET Web sitenizi oluşturduysanız, Şekil 7 ' de gösterilen yeni öğe Ekle iletişim kutusunda "Ana sayfa seç" onay kutusunu görmezsiniz. Web uygulaması proje modelini kullanırken bir içerik sayfası oluşturmak için Web formu şablonu yerine Web Içerik formu şablonunu seçmeniz gerekir. Web Içerik formu şablonunu seçtikten sonra Ekle ' ye tıkladığınızda, Şekil 8 ' de gösterilen aynı ana sayfa Seç iletişim kutusu görüntülenir.

[Yeni Içerik sayfası eklemek ![](creating-a-site-wide-layout-using-master-pages-vb/_static/image18.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image17.png)

**Şekil 07**: yeni içerik sayfası ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-site-wide-layout-using-master-pages-vb/_static/image19.png))

[![site. Master ana sayfasını seçin](creating-a-site-wide-layout-using-master-pages-vb/_static/image21.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image20.png)

**Şekil 08**: `Site.master` ana sayfasını seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-site-wide-layout-using-master-pages-vb/_static/image22.png))

Aşağıdaki bildirim temelli işaretlerde gösterildiği gibi yeni bir içerik sayfası, ana sayfasına ve ana sayfanın ContentPlaceHolder denetimlerinin her biri için bir Içerik denetimine işaret eden bir `@Page` yönergesi içerir.

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample4.aspx)]

> [!NOTE]
> Adım 1 ' deki "basit site düzeni oluşturma" bölümünde `ContentPlaceHolder1` `MainContent`olarak yeniden adlandırdım. Bu ContentPlaceHolder denetiminin `ID` aynı şekilde yeniden adlandırmazsanız, içerik sayfanızın bildirim temelli biçimlendirmesi yukarıda gösterilen biçimlendirmeden biraz farklı olacaktır. Yani, ikinci Içerik denetimi `ContentPlaceHolderID` ana sayfanızda ilgili ContentPlaceHolder denetiminin `ID` yansıtır.

Bir içerik sayfasını işlerken, ASP.NET altyapısı sayfanın Içerik denetimlerini ana sayfanın ContentPlaceHolder denetimleriyle sigortası gerekir. ASP.NET motoru, içerik sayfasının ana sayfasını `@Page` yönergesinin `MasterPageFile` özniteliğinden belirler. Yukarıdaki biçimlendirme gösterildiği gibi, bu içerik sayfası `~/Site.master`bağımlıdır.

Ana sayfada iki ContentPlaceHolder denetimi olduğu için-`head` ve `MainContent`-Visual Web Developer iki Içerik denetimi oluşturdu. Her Içerik denetimi `ContentPlaceHolderID` özelliği aracılığıyla belirli bir ContentPlaceHolder öğesine başvurur.

Ana sayfalar önceki site genelinde şablon tekniklerinden daha fazla görünse de tasarım zamanı desteğiyle birlikte bulunur. Şekil 9 ' da, Visual Web Developer Tasarım görünümü ile görüntülenirken `About.aspx` içerik sayfası gösterilmektedir. Ana sayfa içeriği görünür olsa da gri renkte olduğunu ve değiştirilemeyeceğini unutmayın. Ana sayfanın Contentyertutucuları ile ilgili Içerik denetimleri ancak düzenlenebilir. Diğer tüm ASP.NET sayfaları ile tıpkı, kaynak veya tasarım görünümleri aracılığıyla Web denetimleri ekleyerek içerik sayfasının arabirimini de oluşturabilirsiniz.

[Içerik sayfasının Tasarım görünümünde, sayfaya özgü ve ana sayfa Içeriğini görüntüleyen ![](creating-a-site-wide-layout-using-master-pages-vb/_static/image24.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image23.png)

**Şekil 09**: Içerik sayfasının Tasarım görünümü hem sayfaya özgü hem de ana sayfa içeriğini görüntüler ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-site-wide-layout-using-master-pages-vb/_static/image25.png))

### <a name="adding-markup-and-web-controls-to-the-content-page"></a>Içerik sayfasına Işaretleme ve Web denetimleri ekleme

`About.aspx` sayfa için bir içerik oluşturmak için biraz zaman ayırın. Şekil 10 ' da görebileceğiniz gibi, "yazar hakkında" başlığına ve birkaç metin paragrafını girdim, ancak Web denetimleri eklemeyi de ücretsiz olarak kullanabilirsiniz. Bu arabirimi oluşturduktan sonra tarayıcıda `About.aspx` sayfasını ziyaret edin.

[![Browser aracılığıyla about. aspx sayfasını ziyaret edin](creating-a-site-wide-layout-using-master-pages-vb/_static/image27.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image26.png)

**Şekil 10**: tarayıcı aracılığıyla `About.aspx` sayfasını ziyaret edin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-site-wide-layout-using-master-pages-vb/_static/image28.png))

İstenen içerik sayfasının ve onunla ilişkili ana sayfanın tamamen Web sunucusunda tamamen kullanıldığını ve tam olarak işleneceğini anlamak önemlidir. Son kullanıcının tarayıcısı, sonuçta elde edilen ve kullanılmayan HTML 'yi göndermiştir. Bunu doğrulamak için, Görünüm menüsüne gidip kaynak ' ı seçerek tarayıcı tarafından alınan HTML 'yi görüntüleyin. Tek bir pencerede iki farklı Web sayfasını görüntülemek için herhangi bir çerçeve veya başka bir özel teknik olmadığına göz önünde unutmayın.

### <a name="binding-a-master-page-to-an-existing-aspnet-page"></a>Ana sayfayı var olan bir ASP.NET sayfasına bağlama

Bu adımda gördüğümüz gibi, bir ASP.NET Web uygulamasına yeni bir içerik sayfası eklemek, "Ana sayfa seç" onay kutusunu işaretleyerek ve ana sayfanın seçilmesi kadar kolaydır. Ne yazık ki, var olan bir ASP.NET sayfasını ana sayfaya dönüştürmek çok kolay değildir.

Ana sayfayı var olan bir ASP.NET sayfasına bağlamak için aşağıdaki adımları gerçekleştirmeniz gerekir:

1. `MasterPageFile` özniteliğini ASP.NET sayfasının `@Page` yönergesine ekleyerek uygun ana sayfaya işaret edin.
2. Ana sayfadaki her bir Contenttutucuların için Içerik denetimleri ekleyin.
3. ASP.NET sayfasının mevcut içeriğini uygun Içerik denetimlerine seçmeli olarak kesip yapıştırın. ASP.NET sayfası büyük olasılıkla ana sayfa tarafından zaten ifade edilen `DOCTYPE`, `<html>` öğesi ve Web formu gibi biçimlendirme içerdiğinden, burada "seçmeli" söyledim.

Bu süreç hakkında, ekran görüntüleriyle birlikte adım adım yönergeler için, [ana sayfaları ve site gezinti](http://webproject.scottgu.com/VisualBasic/MasterPages/MasterPages.aspx) öğreticisini kullanarak [Scott Guthrie](https://weblogs.asp.net/scottgu/)' ye göz atın. "Güncelleştirme `Default.aspx` ve ana sayfayı kullanmak için `DataSample.aspx`" bölümünde bu adımlar ayrıntılı olarak yer.

Varolan ASP.NET sayfalarını içerik sayfalarına dönüştürmek yerine yeni içerik sayfaları oluşturmak çok daha kolay olduğundan, siteye bir ana sayfa eklemek için yeni bir ASP.NET Web sitesi oluşturduğunuz her seferinde bu önerilir. Tüm yeni ASP.NET sayfalarını bu ana sayfaya bağlayın. İlk ana sayfa çok basit veya düz ise endişelenmeyin; Ana sayfayı daha sonra güncelleştirebilirsiniz.

> [!NOTE]
> Yeni bir ASP.NET uygulaması oluştururken, Visual Web Developer ana sayfaya bağlanmayan bir `Default.aspx` sayfası ekler. Varolan bir ASP.NET sayfasını bir içerik sayfasına dönüştürmek istiyorsanız, devam edin ve `Default.aspx`. Alternatif olarak, `Default.aspx` silip yeniden ekleyebilirsiniz, ancak bu kez "Ana sayfa seç" onay kutusunu işaretleyebilirsiniz.

## <a name="step-3-updating-the-master-pages-markup"></a>3\. Adım: ana sayfanın Işaretlemesini güncelleştirme

Ana sayfaların başlıca avantajlarından biri, sitedeki çok sayıda sayfanın genel yerleşimini tanımlamak için tek bir ana sayfanın kullanılabileceği bir ana sayfa olabilir. Bu nedenle, sitenin görünüm ve yapısını güncelleştirmek için tek bir dosyanın güncelleştirilmesi gerekir-ana sayfa.

Bu davranışı göstermek için ana sayfamızı, sol sütunun en üstünde bulunan geçerli tarihi içerecek şekilde güncelleştirelim. `leftContent` `<div>``DateDisplay` adlı bir etiket ekleyin.

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample5.aspx)]

Ardından, ana sayfa için `Page_Load` bir olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-vb[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample6.vb)]

Yukarıdaki kod etiketin `Text` özelliğini, haftanın günü, ayın adı ve iki rakamlı gün olarak biçimlendirilen geçerli tarih ve saate ayarlar (bkz. Şekil 11). Bu değişiklik ile içerik sayfalarınızın birini yeniden ziyaret edin. Şekil 11 ' de gösterildiği gibi, sonuçta elde edilen biçimlendirme, ana sayfaya yapılan değişikliği içerecek şekilde hemen güncelleştirilir.

[![ana sayfadaki değişiklikler, Içerik sayfası görüntülenirken yansıtılır](creating-a-site-wide-layout-using-master-pages-vb/_static/image30.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image29.png)

**Şekil 11**: Ana sayfadaki değişiklikler bir Içerik sayfası görüntülenirken yansıtılır ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-site-wide-layout-using-master-pages-vb/_static/image31.png))

> [!NOTE]
> Bu örnekte gösterildiği gibi, ana sayfalar sunucu tarafı Web denetimleri, kod ve olay işleyicileri içerebilir.

## <a name="summary"></a>Özet

Ana sayfalar, ASP.NET geliştiricilerin kolayca güncelleştirilebilir olan tutarlı bir site genelinde düzen tasarlamasını sağlar. Visual Web Developer zengin tasarım zamanı desteği sağladığından, ana sayfaların ve ilişkili içerik sayfalarının oluşturulması, standart ASP.NET sayfaları oluşturma kadar basittir.

Bu öğreticide oluşturduğumuz ana sayfa örneği, iki ContentPlaceHolder denetimine, baş ve ana Içeriğe sahipti. Ancak içerik sayfamızda MainContent ContentPlaceHolder denetimi için yalnızca biçimlendirme belirledik. Bir sonraki öğreticide, içerik sayfasında birden çok Içerik denetimi kullanmayı inceleyeceğiz. Ana sayfada Içerik denetimleri için varsayılan biçimlendirmeyi nasıl tanımlayacağınızı ve ana sayfada tanımlanan varsayılan biçimlendirmeyi kullanma ve içerik sayfasından özel biçimlendirme sağlama arasında da görüyoruz.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Tasarımcılar için ASP.NET: Web standartları kullanarak ASP.NET Web siteleri oluşturma hakkında ücretsiz tasarım şablonları ve yönergeler](https://msdn.microsoft.com/asp.net/aa336602.aspx)
- [ASP.NET ana sayfalarına genel bakış](https://msdn.microsoft.com/library/wtxbf3hh.aspx)
- [Basamaklı stil sayfaları (CSS) öğreticileri](http://www.w3schools.com/css/default.asp)
- [Sayfanın başlığını dinamik olarak ayarlama](http://aspnet.4guysfromrolla.com/articles/051006-1.aspx)
- [ASP.NET 'deki ana sayfalar](http://www.odetocode.com/articles/419.aspx)
- [Ana sayfalar hızlı başlangıç öğreticileri](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/masterpages/default.aspx)

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 3,5 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. Scott 'a [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) veya blogundan [http://ScottOnWriting.NET](http://scottonwriting.net/)üzerinden erişilebilir.

### <a name="special-thanks-to"></a>Özel olarak teşekkürler

Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, beni [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)bir satır bırakın.

> [!div class="step-by-step"]
> [Önceki](nested-master-pages-cs.md)
> [İleri](multiple-contentplaceholders-and-default-content-vb.md)
