---
uid: web-forms/overview/older-versions-getting-started/master-pages/nested-master-pages-vb
title: İç içe yerleştirilmiş ana sayfalar (VB) | Microsoft Docs
author: rick-anderson
description: Bir ana sayfanın bir diğerinin içine nasıl ekleneceğini gösterir.
ms.author: riande
ms.date: 07/28/2008
ms.assetid: 14d9aa1b-4dca-43a0-aa9d-a6e891fee019
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/nested-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 9bb39712855c37f5cbcbb447f7691e9451b8dc92
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78571850"
---
# <a name="nested-master-pages-vb"></a>İç İçe Geçmiş Ana Sayfalar (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_10_VB.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_10_VB.pdf)

> Bir ana sayfanın bir diğerinin içine nasıl ekleneceğini gösterir.

## <a name="introduction"></a>Giriş

Son dokuz öğreticinin kursunda, ana sayfalarla site genelinde bir düzeni nasıl uygulayacağınızı gördük. Bir Nutshell 'de, ana sayfalar, ana sayfada bir içerik sayfası sayfa temelinde özelleştirilebilecek belirli bölgelerle birlikte ana sayfada ortak biçimlendirme tanımlamasına olanak tanır. Ana sayfadaki ContentPlaceHolder denetimleri özelleştirilebilir bölgeleri belirtir; ContentPlaceHolder denetimleri için özelleştirilmiş biçimlendirme içerik sayfasında Içerik denetimleri aracılığıyla tanımlanır.

Şimdiye kadar araştırdığımız ana sayfa teknikleri, tüm sitede tek bir düzen varsa harika. Ancak, birçok büyük web sitesinin çeşitli bölümler genelinde özelleştirilmiş bir site düzeni vardır. Örneğin, hastane personeli tarafından hasta bilgilerini, etkinliklerini ve faturalandırmayı yönetmek için kullanılan bir sistem durumu bakım uygulaması düşünün. Bu uygulamada üç tür Web sayfası olabilir:

- Personel üyelerinin kullanılabilirliği güncelleştirebileceği, zamanlamaları görüntüleyebileceği veya tatil süresi isteyebildiği personele üyeye özgü sayfalar.
- Personel üyelerinin belirli bir hasta için bilgileri görüntülemesi veya düzenlemesi gereken hasta 'e özgü sayfalar.
- Muhasebeciler geçerli talep durumlarını ve finansal raporları incelemesinin faturalandırmaya özgü sayfalar.

Her sayfa, üstteki bir menü ve alt taraftaki sık kullanılan bağlantılar dizisi gibi ortak bir düzen paylaşabilir. Ancak personel, hasta ve faturalandırmaya özgü sayfaların bu genel düzeni özelleştirmesi gerekebilir. Örneğin, personele özgü tüm sayfalar, şu anda oturum açmış olan kullanıcının kullanılabilirliğini ve günlük zamanlamayı gösteren bir takvim ve görev listesi içermelidir. Hasta 'e özgü tüm sayfaların, bilgileri düzenlenmekte olan hasta için ad, adres ve sigorta bilgilerini göstermesi gerekir.

*İç içe yerleştirilmiş ana sayfalar*kullanılarak bu tür özelleştirilmiş düzenler oluşturmak mümkündür. Yukarıdaki senaryoyu uygulamak için, özelleştirilebilir bölgeleri tanımlayan Contentyertutucuları olan site genelinde düzeni, menü ve alt bilgi içeriğini tanımlayan bir ana sayfa oluşturarak başlayacağız. Daha sonra her Web sayfası türü için bir tane olmak üzere üç iç içe ana sayfa oluşturacağız. İç içe yerleştirilmiş her ana sayfa, ana sayfayı kullanan içerik sayfalarının türü arasındaki içeriği tanımlar. Diğer bir deyişle, hasta 'e özgü içerik sayfaları için iç içe geçmiş ana sayfa, düzenlenmekte olan hasta hakkındaki bilgileri görüntülemek için biçimlendirme ve programlama mantığını içerir. Hasta 'e özgü yeni bir sayfa oluştururken onu bu iç içe geçmiş ana sayfaya bağlayacağız.

Bu öğretici, iç içe yerleştirilmiş ana sayfaların avantajlarını vurgulayarak başlar. Ardından, iç içe geçmiş ana sayfaların nasıl oluşturulacağını ve kullanılacağını gösterir.

> [!NOTE]
> .NET Framework sürüm 2,0 ' den beri iç içe yerleştirilmiş ana sayfalar mümkün. Ancak, Visual Studio 2005, iç içe geçmiş ana sayfalar için tasarım zamanı desteği içermiyordu. İyi haber, Visual Studio 2008 iç içe geçmiş ana sayfalar için zengin bir tasarım zamanı deneyimi sunuyor. İç içe geçmiş ana sayfalar kullanmak istiyorsanız, ancak hala Visual Studio 2005 kullanıyorsanız [Scott Guthrie](https://weblogs.asp.net/scottgu/)'nin blog girişine göz ATıN ve [vs 2005 tasarım zamanında Iç Içe geçmiş ana sayfalar için ipuçları](https://weblogs.asp.net/scottgu/archive/2005/11/11/430382.aspx)bulabilirsiniz.

## <a name="the-benefits-of-nested-master-pages"></a>Iç Içe yerleştirilmiş ana sayfaların avantajları

Birçok Web sitesinin Ayrıca, belirli sayfa türlerine özgü daha özelleştirilmiş tasarımlar ve çok sayıda site tasarımı vardır. Örneğin, tanıtım Web uygulamamızda bir ilkel yönetim bölümü (`~/Admin` klasöründeki sayfalar) oluşturduk. Şu anda `~/Admin` klasöründeki Web sayfaları, Yönetim bölümünde bulunmayan sayfalarla aynı ana sayfayı kullanır (yani, `Site.master` veya `Alternate.master`kullanıcının seçimine bağlı olarak).

> [!NOTE]
> Şimdilik, sitemizin yalnızca bir ana sayfa `Site.master`. Bu öğreticinin ilerleyen kısımlarında "yönetim bölümü için Iç Içe yerleştirilmiş ana sayfa kullanma" ile başlayan iç içe yerleştirilmiş ana sayfaları kullanarak iki (veya daha fazla) Ana sayfa kullanın.

Yönetim sayfalarının yerleşimini, diğer sayfalarda bulunmayan ek bilgileri veya bağlantıları içerecek şekilde özelleştirmenin sorulduğu hakkında düşünün. Bu gereksinimi uygulamak için dört teknik vardır:

1. `~/Admin` klasöründeki her içerik sayfasına yönetime özgü bilgileri ve bağlantıları el ile ekleyin.
2. `Site.master` ana sayfasını, Yönetim bölümüne özgü bilgileri ve bağlantıları içerecek şekilde güncelleştirin ve sonra yönetim sayfalarından birinin ziyaret edilip edilmeyeceğini temel alarak bu bölümleri göstermek veya gizlemek için ana sayfaya kod ekleyin.
3. Özellikle Yönetim bölümünde yeni bir ana sayfa oluşturun, `Site.master`biçimlendirmesini kopyalayın, Yönetim bölümüne özgü bilgileri ve bağlantıları ekleyin ve ardından bu yeni ana sayfayı kullanmak için `~/Admin` klasöründeki içerik sayfalarını güncelleştirin.
4. `Site.master` bağlanan ve `~/Admin` klasördeki içerik sayfalarının bu yeni iç içe geçmiş ana sayfayı kullanmasını sağlayan bir iç içe ana sayfa oluşturun. Bu iç içe yerleştirilmiş ana sayfa yalnızca yönetim sayfalarına özgü ek bilgileri ve bağlantıları içerir ve `Site.master`zaten tanımlı biçimlendirmeyi tekrarlamanız gerekmez.

İlk seçenek en az bir kez Damadır tablosudur. Ana sayfaları kullanmanın tam noktası, ortak biçimlendirmeyi el ile kopyalayıp yeni ASP.NET sayfalarına yapıştırmaya kadar uzaklaşmaktır. İkinci seçenek kabul edilebilir, ancak uygulamanın ana sayfaları yalnızca bir zaman içinde görüntülenen işaretlerle kullandığından daha az bakım yapılmasını sağlar ve ana sayfayı düzenleyen geliştiricilerin bu biçimlendirme etrafında çalışmasını ve ne zaman hatırlamasını istiyorsanız, tam olarak, belirli bir biçimlendirme gizlenirse buna karşı görüntülenir. Bu yaklaşım, bu tek ana sayfa tarafından sağlanmak için daha fazla ve daha fazla Web sayfası türünden özelleştirmeler için daha az kullanılabilir.

Üçüncü seçenek ikinci seçenekle ortaya çıkan dağınıklığı ve karmaşıklık sorunlarını ortadan kaldırır. Ancak, üç ana dezavantajı seçeneği, `Site.master` ' den ortak düzeni kopyalayıp yeni yönetim bölümüne özgü ana sayfaya yapıştırmamızı gerektirmesidir. Daha sonra site genelinde düzeni değiştirme kararı verirse, bunu iki yerde değiştirmeyi hatırladık.

Dördüncü seçenek olan iç içe yerleştirilmiş ana sayfalar bize ikinci ve üçüncü seçeneklerden en iyi şekilde erişmenizi sağlar. Site genelinde düzen bilgileri bir dosyada tutulur-üst düzey ana sayfa-belirli bölgelere özgü içerik farklı dosyalara ayrılır.

Bu öğretici basit bir iç içe geçmiş ana sayfa oluşturma ve kullanma konusunda bir görünüm ile başlar. Yeni bir en üst düzey ana sayfa, iç içe geçmiş iki ana sayfa ve iki içerik sayfası oluşturacağız. "Yönetim bölümünde Iç Içe yerleştirilmiş ana sayfa kullanma" ile başlayarak, iç içe yerleştirilmiş ana sayfaların kullanımını dahil etmek için mevcut ana sayfa mimarimizi güncelleştirme bölümüne baktık. Özellikle, iç içe geçmiş ana sayfa oluşturur ve bu sayfayı, `~/Admin` klasöründeki içerik sayfaları için ek özel içerik içerecek şekilde kullanır.

## <a name="step-1-creating-a-simple-top-level-master-page"></a>1\. Adım: basit bir üst düzey ana sayfa oluşturma

Var olan ana sayfalardan birini temel alan iç içe bir ana sayfa oluşturma ve var olan içerik sayfası, üst düzey ana sayfa yerine bu yeni iç içe ana sayfanın kullanılması bazı karmaşıklıklar sağlar çünkü var olan içerik sayfaları zaten beklenirken Üst düzey ana sayfada tanımlanan ContentPlaceHolder denetimleri. Bu nedenle, iç içe yerleştirilmiş ana sayfa aynı ada sahip aynı ContentPlaceHolder denetimlerini de içermelidir. Ayrıca, belirli tanıtım uygulamamız, Bu karmaşıklığa daha fazla eklenen bir kullanıcının tercihlerine bağlı olarak bir içerik sayfasına dinamik olarak atanan iki ana sayfaya (`Site.master` ve `Alternate.master`) sahiptir. Mevcut uygulamayı, bu öğreticide daha sonra iç içe geçmiş ana sayfaları kullanacak şekilde güncelleştirmeye bakacağız, ancak ilk olarak bir basit iç içe ana sayfa örneğine odaklanalım.

`NestedMasterPages` adlı yeni bir klasör oluşturun ve ardından `Simple.master`adlı klasöre yeni bir ana sayfa dosyası ekleyin. (Bu klasör ve dosya eklendikten sonra Çözüm Gezgini ekran görüntüsü için Şekil 1 ' i inceleyin.) `AlternateStyles.css` stil sayfası dosyasını Çözüm Gezgini tasarımcı üzerine sürükleyin. Bu, ana sayfanın `<head>` öğe biçimlendirmesinin şöyle görünmesi için `<head>` öğesindeki stil sayfası dosyasına bir `<link>` öğesi ekler:

[!code-aspx[Main](nested-master-pages-vb/samples/sample1.aspx)]

Sonra, aşağıdaki biçimlendirmeyi `Simple.master`Web biçiminde ekleyin:

[!code-aspx[Main](nested-master-pages-vb/samples/sample2.aspx)]

Bu biçimlendirme, sayfanın en üstünde yer alan "Iç Içe yerleştirilmiş ana sayfalar (basit)" adlı bir bağlantı görüntüleyerek bir Navy arka planında büyük bir beyaz yazı tipidir. Bunun altında, `MainContent` ContentPlaceHolder. Şekil 1, Visual Studio tasarımcısında yüklendiğinde `Simple.master` ana sayfasını gösterir.

[Iç Içe ana sayfa ![, yönetim bölümündeki sayfalara özgü Içeriği tanımlar](nested-master-pages-vb/_static/image2.png)](nested-master-pages-vb/_static/image1.png)

**Şekil 01**: Iç Içe yerleştirilmiş ana sayfa, yönetim bölümündeki sayfalara özgü içeriği tanımlar ([tam boyutlu görüntüyü görüntülemek için tıklayın](nested-master-pages-vb/_static/image3.png))

## <a name="step-2-creating-a-simple-nested-master-page"></a>2\. Adım: basit bir Iç Içe ana sayfa oluşturma

`Simple.master` iki ContentPlaceHolder denetimi içerir: Web formu içine eklenen ve `<head>` öğesinde bulunan `head` ContentPlaceHolder ile birlikte `MainContent` ContentPlaceHolder. Bir içerik sayfası oluşturmak ve bunu `Simple.master` bağlamanız durumunda, içerik sayfasında iki Contentbir yer tutucuyu başvuruda bulunan iki Içerik denetimi olacaktır. Benzer şekilde, iç içe geçmiş ana sayfa oluşturup `Simple.master`, iç içe yerleştirilmiş ana sayfanın iki Içerik denetimi olacaktır.

`SimpleNested.master`adlı `NestedMasterPages` klasöre yeni bir iç içe ana sayfa ekleyelim. `NestedMasterPages` klasöre sağ tıklayın ve yeni öğe Ekle ' yi seçin. Bu, Şekil 2 ' de gösterilen yeni öğe Ekle iletişim kutusunu açar. Ana sayfa şablonu türünü seçin ve yeni ana sayfanın adını yazın. Yeni ana sayfanın iç içe yerleştirilmiş bir ana sayfa olması gerektiğini göstermek için "Ana sayfa seç" onay kutusunu işaretleyin.

Sonra Ekle düğmesine tıklayın. Bu, bir içerik sayfasını ana sayfaya bağlarken gördüğünüz ana sayfa Seç iletişim kutusunu görüntüler (bkz. Şekil 3). `NestedMasterPages` klasöründe `Simple.master` ana sayfasını seçin ve Tamam ' a tıklayın.

> [!NOTE]
> Web sitesi proje modeli yerine Web uygulaması proje modelini kullanarak ASP.NET Web sitenizi oluşturduysanız Şekil 2 ' de gösterilen yeni öğe Ekle iletişim kutusunda "Ana sayfa seç" onay kutusunu görmezsiniz. Web uygulaması proje modelini kullanırken iç içe yerleştirilmiş bir ana sayfa oluşturmak için, Iç sayfa şablonunu (Ana sayfa şablonu yerine) seçmeniz gerekir. Iç Içe geçmiş ana sayfa şablonunu seçtikten sonra Ekle ' ye tıkladığınızda, Şekil 3 ' te gösterilen aynı ana sayfa Seç iletişim kutusu görüntülenir.

[Iç Içe geçmiş ana sayfa eklemek için &quot;ana sayfa seçin&quot; onay kutusunu ![işaretleyin](nested-master-pages-vb/_static/image5.png)](nested-master-pages-vb/_static/image4.png)

**Şekil 02**: Iç Içe geçmiş ana sayfa eklemek için "Ana sayfa seç" onay kutusunu işaretleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](nested-master-pages-vb/_static/image6.png))

[Iç Içe yerleştirilmiş ana sayfayı basit. Master ana sayfasına bağlama ![](nested-master-pages-vb/_static/image8.png)](nested-master-pages-vb/_static/image7.png)

**Şekil 03**: Iç Içe ana sayfayı `Simple.master` ana sayfasına bağlama ([tam boyutlu görüntüyü görüntülemek için tıklayın](nested-master-pages-vb/_static/image9.png))

Aşağıda gösterilen iç içe ana sayfanın bildirime dayalı biçimlendirmesi, üst düzey ana sayfanın iki ContentPlaceHolder denetimine başvuran iki Içerik denetimini içerir.

[!code-aspx[Main](nested-master-pages-vb/samples/sample3.aspx)]

`<%@ Master %>` yönergesi dışında, iç içe geçmiş ana sayfanın ilk bildirim temelli biçimlendirme biçimlendirmesi, bir içerik sayfasını aynı üst düzey ana sayfaya bağlarken başlangıçta oluşturulan biçimlendirmeyle aynıdır. Bir içerik sayfasının `<%@ Page %>` yönergesine benzer şekilde, `<%@ Master %>` yönergesi, iç içe yerleştirilmiş ana sayfanın üst ana sayfasını belirten bir `MasterPageFile` özniteliği içerir. İç içe yerleştirilmiş ana sayfa ile aynı üst düzey ana sayfaya bağlanan bir içerik sayfası arasındaki temel fark, iç içe yerleştirilmiş ana sayfanın ContentPlaceHolder denetimlerini içeremeyeceği bir içeriktir. İç içe yerleştirilmiş ana sayfanın ContentPlaceHolder denetimleri, içerik sayfalarının biçimlendirmeyi özelleştirebileceği bölgeleri tanımlar.

Bu iç içe geçmiş ana sayfayı, "Merhaba, SimpleNested! öğesinden" metin görüntüleyecek şekilde güncelleştirin Içerik denetiminde `MainContent` ContentPlaceHolder denetimine karşılık gelir.

[!code-aspx[Main](nested-master-pages-vb/samples/sample4.aspx)]

Bu eklemeyi yaptıktan sonra, iç içe geçmiş ana sayfayı kaydedin ve sonra `Default.aspx`adlı `NestedMasterPages` klasöre yeni bir içerik sayfası ekleyin ve `SimpleNested.master` ana sayfasına bağlayın. Bu sayfayı ekledikten sonra hiç Içerik denetimi içerdiğini görmek için şaşırmış olabilirsiniz (bkz. Şekil 4)! İçerik sayfası, yalnızca *üst* ana sayfanın içerik yertutucuları ile erişebilir. `SimpleNested.master` ContentPlaceHolder denetimi içermez; Bu nedenle, bu ana sayfaya bağlantılı tüm içerik sayfaları Içerik denetimleri içeremez.

[Yeni Içerik sayfası, Içerik denetimi içermiyor ![](nested-master-pages-vb/_static/image11.png)](nested-master-pages-vb/_static/image10.png)

**Şekil 04**: yeni Içerik sayfası içerik denetimi içermiyor ([tam boyutlu görüntüyü görüntülemek için tıklayın](nested-master-pages-vb/_static/image12.png))

Yapmanız gerekenler, iç içe yerleştirilmiş ana sayfayı (`SimpleNested.master`) ContentPlaceHolder denetimlerini içerecek şekilde güncelleştiririz. Genellikle, iç içe yerleştirilmiş ana sayfalarınızın üst ana sayfası tarafından tanımlanan her bir ContentPlaceHolder için bir ContentPlaceHolder içermesini, böylece alt ana sayfa veya içerik sayfasının üst düzey ana sayfanın ContentPlaceHolder ile çalışmasına izin vermesini isteyeceksiniz kontrollerini.

`SimpleNested.master` ana sayfasını, iki Içerik denetimine bir ContentPlaceHolder içerecek şekilde güncelleştirin. ContentPlaceHolder denetimlerine, Içerik denetiminin başvurduğu ContentPlaceHolder denetimiyle aynı adı verin. Diğer bir deyişle, `Simple.master`içindeki `MainContent` ContentPlaceHolder öğesine başvuran `SimpleNested.master` Içerik denetimine `MainContent` adlı bir ContentPlaceHolder denetimi ekleyin. Içerik denetimindeki `head` ContentPlaceHolder öğesine başvuran aynı şeyi yapın.

> [!NOTE]
> İç içe ana sayfadaki ContentPlaceHolder denetimlerinin, üst düzey ana sayfadaki Contentyertutucuları ile aynı şekilde adlandırılması önerdiğimde, bu adlandırma simetriyi gerekli değildir. İç içe yerleştirilmiş ana sayfanızda ContentPlaceHolder denetimlerine dilediğiniz adı verebilirsiniz. Bununla birlikte, en üst düzey ana sayfam ve iç içe yerleştirilmiş ana sayfalar aynı adları kullanıyorsa, sayfanın hangi bölgelerine karşılık geldiğini unutmayı daha kolay buldum.

Bu eklemeleri yaptıktan sonra `SimpleNested.master` ana sayfanızın bildirim temelli biçimlendirmesinin aşağıdakine benzer şekilde görünmesi gerekir:

[!code-aspx[Main](nested-master-pages-vb/samples/sample5.aspx)]

Yeni oluşturduğumuz `Default.aspx` içerik sayfasını silin ve sonra yeniden ekleyin ve `SimpleNested.master` ana sayfasına bağlamanız gerekir. Bu kez, Visual Studio `Default.aspx`, artık `SimpleNested.master` tanımlanmış olan Contentyertutucuları ile başvurulan iki Içerik denetimini ekler (bkz. Şekil 6). "Hello, default. aspx!" metnini ekleyin `MainContent`başvurulan Içerik denetiminde.

Şekil 5 ' te yer alan üç varlık (`Simple.master`, `SimpleNested.master`ve `Default.aspx`, birbirleriyle birbirleriyle nasıl ilişkili olduğu gösterilmektedir. Diyagramda gösterildiği gibi, iç içe yerleştirilmiş ana sayfa üst öğesinin ContentPlaceHolder için Içerik denetimleri uygular. Bu bölgelerin içerik sayfasında erişilebilir olması gerekiyorsa, iç içe yerleştirilmiş ana sayfanın Içerik denetimlerine kendi Contentyertutucuları eklemesi gerekir.

[Üst düzey ve Iç Içe yerleştirilmiş ana sayfaların ![, Içerik sayfasının yerleşimini dikte](nested-master-pages-vb/_static/image14.png)](nested-master-pages-vb/_static/image13.png)

**Şekil 05**: en üst düzey ve Iç Içe yerleştirilmiş ana sayfalar Içerik sayfasının yerleşimini ([tam boyutlu görüntüyü görüntülemek için tıklatın](nested-master-pages-vb/_static/image15.png))

Bu davranış, bir içerik sayfası veya ana sayfanın yalnızca üst ana sayfasının bilmi olduğunu gösterir. Bu davranış, Visual Studio Tasarımcısı tarafından da belirtilir. Şekil 6 `Default.aspx`için tasarımcıyı gösterir. Tasarımcı içerik sayfasından hangi bölgelerin düzenlenebilir olduğunu ve bunların ne tür olduğunu açıkça gösterirken, düzenlenemeyen bölgelerin iç içe yerleştirilmiş ana sayfadan ve en üst düzey ana sayfadan hangi bölgelerde olduğunu belirsizliğini engellemez.

[Içerik sayfası ![artık Iç Içe yerleştirilmiş ana sayfanın Contentyertutucuları için Içerik denetimleri Içeriyor](nested-master-pages-vb/_static/image17.png)](nested-master-pages-vb/_static/image16.png)

**Şekil 06**: Içerik sayfası artık Iç Içe yerleştirilmiş ana sayfanın contentyertutucuları Için Içerik denetimleri içeriyor ([tam boyutlu görüntüyü görüntülemek için tıklayın](nested-master-pages-vb/_static/image18.png))

## <a name="step-3-adding-a-second-simple-nested-master-page"></a>3\. Adım: Ikinci bir basit Iç Içe geçmiş ana sayfa ekleme

Birden çok iç içe yerleştirilmiş ana sayfa olduğunda, iç içe yerleştirilmiş ana sayfaların avantajı daha fazla belirlenir. Bu avantajı göstermek için `NestedMasterPages` klasöründe başka bir iç içe ana sayfa oluşturun; Bu yeni iç içe geçmiş ana sayfayı `SimpleNestedAlternate.master` adlandırın ve `Simple.master` ana sayfasına bağlayın. İç içe yerleştirilmiş ana sayfanın ikinci Içerik denetimlerine 2. adım yaptığımız gibi ContentPlaceHolder denetimleri ekleyin. Ayrıca "Merhaba, SimpleNestedAlternate!" metnini ekleyin üst düzey ana sayfanın `MainContent` ContentPlaceHolder öğesine karşılık gelen Içerik denetiminde. Bu değişiklikleri yaptıktan sonra, yeni iç içe ana sayfanın bildirim temelli biçimlendirmesinin aşağıdakine benzer şekilde görünmesi gerekir:

[!code-aspx[Main](nested-master-pages-vb/samples/sample6.aspx)]

`NestedMasterPages` klasöründe `Alternate.aspx` adlı bir içerik sayfası oluşturun ve `SimpleNestedAlternate.master` iç içe ana sayfaya bağlayın. "Merhaba, diğer!" metnini ekleyin `MainContent`karşılık gelen Içerik denetiminde. Şekil 7 ' de, Visual Studio Tasarımcısı aracılığıyla görüntülendiğinde `Alternate.aspx` gösterilmektedir.

[![alternatif. aspx, SimpleNestedAlternate. Master ana sayfasına bağlanır](nested-master-pages-vb/_static/image20.png)](nested-master-pages-vb/_static/image19.png)

**Şekil 07**: `Alternate.aspx` `SimpleNestedAlternate.master` ana sayfasına bağlanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](nested-master-pages-vb/_static/image21.png))

Şekil 7 ' deki tasarımcıyı Şekil 6 ' da tasarımcı ile karşılaştırın. Her iki içerik sayfası da üst düzey ana sayfada (`Simple.master`) tanımlanan düzeni paylaşır, yani "Iç Içe geçmiş ana sayfalar öğreticisi (basit)" başlığı. Ancak her ikisi de üst ana sayfalarında tanımlı farklı içeriğe sahiptir-"Hello, SimpleNested öğesinden" metni " Şekil 6 ' da ve "Merhaba, SimpleNestedAlternate!" Şekil 7 ' de. Bu farklar önemsiz, ancak daha anlamlı farklılıklar içermesi için bu örnek genişletebilirsiniz. Örneğin, `SimpleNested.master` sayfasında içerik sayfalarına özgü seçeneklere sahip bir menü bulunabilir, ancak `SimpleNestedAlternate.master`, bu sayfaya bağlanan içerik sayfaları ile ilgili bilgiler içerebilir.

Şimdi, site düzeninde daha fazla değişiklik yapmak için gerekdiğimiz hakkında düşünün. Örneğin, tüm içerik sayfalarına ortak bağlantıların bir listesini eklemek istediğimizde düşünün. Bunu gerçekleştirmek için üst düzey ana sayfayı güncelleştireceğiz `Simple.master`. Tüm değişiklikler, iç içe geçmiş ana sayfalarına ve uzantıya göre içerik sayfalarına hemen yansıtılır.

Kapsamlı site yerleşimini değiştirediğimiz kolaylığınızı göstermek için `Simple.master` ana sayfasını açın ve `topContent` ve `mainContent` `<div>` öğeleri arasında aşağıdaki biçimlendirmeyi ekleyin:

[!code-aspx[Main](nested-master-pages-vb/samples/sample7.aspx)]

Bu, `Simple.master`, `SimpleNested.master`veya `SimpleNestedAlternate.master`bağlanan her sayfanın üst kısmına iki bağlantı ekler; Bu değişiklikler, iç içe geçmiş ana sayfalara ve bunların içerik sayfalarına hemen uygulanır. Şekil 8 ' de bir tarayıcıdan görüntülendiklerinde `Alternate.aspx` gösterilmektedir. Sayfanın üst kısmındaki bağlantıların eklenmesine (Şekil 7 ' ye kıyasla) göz önünde.

[En üst düzey ana sayfa olarak değiştirilen ![, Iç Içe yerleştirilmiş ana sayfalara ve bunların Içerik sayfalarına hemen yansıtılır](nested-master-pages-vb/_static/image23.png)](nested-master-pages-vb/_static/image22.png)

**Şekil 08**: en üst düzey ana sayfa olarak değiştirme, Iç Içe geçmiş ana sayfalarında ve bunların Içerik sayfalarında hemen yansıtılır ([tam boyutlu görüntüyü görüntülemek için tıklayın](nested-master-pages-vb/_static/image24.png))

## <a name="using-a-nested-master-page-for-the-administration-section"></a>Yönetim bölümü için Iç Içe geçmiş ana sayfa kullanma

Bu noktada, iç içe geçmiş ana sayfaların avantajlarını inceledik ve bunları nasıl oluşturup bir ASP.NET uygulamasında kullanacağınızı gördünüz. 1, 2 ve 3. adımlarda, bununla birlikte yeni bir üst düzey ana sayfa, yeni iç içe ana sayfa ve yeni içerik sayfaları oluşturma dahil olmak üzere örnekler. Var olan üst düzey ana sayfa ve içerik sayfalarıyla bir Web sitesine yeni bir iç içe ana sayfa ekleme hakkında ne olacak?

İç içe yerleştirilmiş ana sayfayı var olan bir Web sitesiyle tümleştirme ve var olan içerik sayfalarıyla ilişkilendirme, sıfırdan başlayarak biraz daha fazla çaba gerektirir. 4, 5, 6 ve 7. adım, yönetim yönergelerini içeren `AdminNested.master` adlı yeni bir iç içe ana sayfa eklemek için tanıtım uygulamamızı geliştirdik ve `~/Admin` klasöründeki ASP.NET sayfaları tarafından kullanılır.

İç içe yerleştirilmiş ana sayfayı tanıtım uygulamamızda tümleştirmek aşağıdaki acecüleri tanıtır:

- `~/Admin` klasöründeki mevcut içerik sayfaları, ana sayfalarından belirli beklentiler. Başlangıçlar için bazı ContentPlaceHolder denetimlerinin mevcut olmasını bekler. Ayrıca, `~/Admin/AddProduct.aspx` ve `~/Admin/Products.aspx` sayfaları ana sayfanın ortak `RefreshRecentProductsGrid` yöntemini çağırır, `GridMessageText` özelliğini ayarlar veya `PricesDoubled` olayı için bir olay işleyicisine sahiptir. Sonuç olarak, iç içe geçmiş ana sayfamız aynı Contentyertutucuları ve ortak üyeleri sağlamalıdır.
- Önceki öğreticide, bir oturum değişkenine göre `Page` nesnesinin `MasterPageFile` özelliğini dinamik olarak ayarlamak için `BasePage` sınıfını geliştirdik. İç içe geçmiş ana sayfalar kullanılırken dinamik ana sayfaları destekliyoruz?

Bu iki zorluk, iç içe geçmiş ana sayfa oluşturduğumuzdan ve var olan içerik sayfalarımızdan kullanıldığı sürece yüzeyidir. Bu sorunları ortaya çıktığında araştırıp bağlayacağız.

## <a name="step-4-creating-the-nested-master-page"></a>4\. Adım: Iç Içe geçmiş ana sayfa oluşturma

İlk göreviniz, yönetim bölümündeki sayfalar tarafından kullanılacak iç içe yerleştirilmiş ana sayfayı oluşturmaktır. 2\. adımda gördüğümüz gibi, iç içe yerleştirilmiş ana sayfanın üst ana sayfasını belirtmemiz gereken yeni bir iç içe ana sayfa eklenirken. Ancak en üst düzey iki ana sayfanız vardır: `Site.master` ve `Alternate.master`. Önceki öğreticide `Alternate.master` oluşturduğumuz ve `BasePage` sınıfında, çalışma zamanında `Page` nesnesinin `MasterPageFile` özelliğini `Site.master` oturum değişkeninin değerine bağlı olarak `Alternate.master` veya `MyMasterPage` olarak belirten kodu yazdığımızda geri çekin.

İç içe geçmiş ana sayfamızı, uygun üst düzey ana sayfayı kullanacak şekilde nasıl yapılandıracağız? İki seçeneğiniz vardır:

- İki iç içe geçmiş ana sayfa oluşturun, `AdminNestedSite.master` ve `AdminNestedAlternate.master`ve bunları sırasıyla en üst düzey ana sayfalara `Site.master` ve `Alternate.master`bağlayın. `BasePage`, `Page` nesnesinin `MasterPageFile` uygun iç içe ana sayfaya ayarlayacağız.
- Tek bir iç içe geçmiş ana sayfa oluşturun ve içerik sayfalarında bu özel ana sayfayı kullanın. Sonra, çalışma zamanında, iç içe yerleştirilmiş ana sayfanın `MasterPageFile` özelliğini çalışma zamanında uygun en üst düzey ana sayfaya ayarlamanız gerekir. (Şu anda iletişime, ana sayfaların da bir `MasterPageFile` özelliği vardır.)

İkinci seçeneği kullanalım. `AdminNested.master`adlı `~/Admin` klasöründe tek bir iç içe geçmiş ana sayfa dosyası oluşturun. Hem `Site.master` hem de `Alternate.master` aynı ContentPlaceHolder denetim kümesine sahip olduğundan, bu, hangi ana sayfayı bağladıkınızın önemi yoktur, ancak bunu tutarlılığın sake için `Site.master` bağlamanız önerilir.

[~/Admin klasörüne Iç Içe geçmiş ana sayfa eklemek ![.](nested-master-pages-vb/_static/image26.png)](nested-master-pages-vb/_static/image25.png)

**Şekil 09**: `~/Admin` klasöre Iç Içe geçmiş ana sayfa ekleyin. ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](nested-master-pages-vb/_static/image27.png))

İç içe yerleştirilmiş ana sayfa dört ContentPlaceHolder denetimine sahip bir ana sayfaya bağlandığı için, Visual Studio yeni iç içe ana sayfa dosyasının ilk biçimlendirmesine dört Içerik denetimi ekler. 2 ve 3. adımlarda yaptığımız gibi, her Içerik denetimine bir ContentPlaceHolder denetimi ekleyerek üst düzey ana sayfanın ContentPlaceHolder denetimiyle aynı adı vermiş olursunuz. Ayrıca, `MainContent` ContentPlaceHolder öğesine karşılık gelen Içerik denetimine aşağıdaki biçimlendirmeyi ekleyin:

[!code-html[Main](nested-master-pages-vb/samples/sample8.html)]

Sonra, `Styles.css` ve `AlternateStyles.css` CSS dosyalarında `instructions` CSS sınıfını tanımlayın. Aşağıdaki CSS kuralları, açık sarı arka plan rengi ve siyah, düz kenarlık ile görüntülenmek üzere `instructions` sınıfıyla biçimlendirilmiş HTML öğelerine neden olur:

[!code-css[Main](nested-master-pages-vb/samples/sample9.css)]

Bu işaretleme, iç içe yerleştirilmiş ana sayfaya eklendiğinden, yalnızca bu iç içe ana sayfayı kullanan sayfalarda görünür (yani, yönetim bölümündeki sayfalar).

İç içe geçmiş ana sayfanıza Bu eklemeleri yaptıktan sonra, bildirim temelli biçimlendirme aşağıdakine benzer olmalıdır:

[!code-aspx[Main](nested-master-pages-vb/samples/sample10.aspx)]

Her Içerik denetiminin bir ContentPlaceHolder denetimine sahip olduğunu ve ContentPlaceHolder denetimlerinin ' `ID` özelliklerinin en üst düzey ana sayfadaki ilgili ContentPlaceHolder denetimleriyle aynı değerleri atandığını unutmayın. Üstelik, Yönetim bölümüne özgü biçimlendirme `MainContent` ContentPlaceHolder ' da görünür.

Şekil 10 ' da, Visual Studio 'nun Tasarımcısı aracılığıyla görüntülendiğinde iç içe geçmiş ana sayfa `AdminNested.master` gösterilmektedir. Yönergeleri `MainContent` Içerik denetiminin en üstündeki sarı kutuda görebilirsiniz.

[Iç Içe geçmiş ana sayfa ![, yönetici için yönergeler Içerecek şekilde üst düzey ana sayfayı genişletir.](nested-master-pages-vb/_static/image29.png)](nested-master-pages-vb/_static/image28.png)

**Şekil 10**: Iç Içe yerleştirilmiş ana sayfa, yönetici Için yönergeler Içerecek şekilde üst düzey ana sayfayı genişletir. ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](nested-master-pages-vb/_static/image30.png))

## <a name="step-5-updating-the-existing-content-pages-to-use-the-new-nested-master-page"></a>5\. Adım: var olan Içerik sayfalarını yeni Iç Içe geçmiş ana sayfayı kullanmak üzere güncelleştirme

Yönetim bölümüne yeni bir içerik sayfası eklediğimiz her zaman, onu yeni oluşturduğumuz `AdminNested.master` ana sayfaya bağlamanız gerekir. Ancak var olan içerik sayfaları ne kadar? Şu anda sitedeki tüm içerik sayfaları, çalışma zamanında içerik sayfasının ana sayfasını programlı bir şekilde ayarlayan `BasePage` sınıfından türetilir. Bu, yönetim bölümündeki içerik sayfaları için istediğimiz davranış değildir. Bunun yerine, bu içerik sayfalarının `AdminNested.master` sayfasını her zaman kullanmasını istiyoruz. Çalışma zamanında sağ üst düzey içerik sayfasını seçmek için iç içe yerleştirilmiş ana sayfanın sorumluluğu olacaktır.

Bu istenen davranışı elde etmenin en iyi yolu, `BasePage` sınıfını genişleten `AdminBasePage` adlı yeni bir özel taban sayfa sınıfı oluşturmaktır. `AdminBasePage` daha sonra `SetMasterPageFile` geçersiz kılabilir ve `Page` nesnesinin `MasterPageFile` "~/Admin/AdminNested.master" sabit kodlanmış değerine ayarlayabilir. Bu şekilde, `AdminBasePage` türetilen tüm sayfalar `AdminNested.master`kullanacaktır, ancak `MasterPageFile` `BasePage` türetilen herhangi bir sayfa `MyMasterPage` oturum değişkeninin değerine bağlı olarak "~/site.exe ana" veya "~/Alternate.exe ana" olarak ayarlanır.

`AdminBasePage.vb`adlı `App_Code` klasöre yeni bir sınıf dosyası ekleyerek başlayın. `BasePage` genişletecek `AdminBasePage` ve ardından `SetMasterPageFile` yöntemini geçersiz kılarsınız. Bu yöntemde, "~/Admin/AdminNested.master" değerini `MasterPageFile` atayın. Bu değişiklikleri yaptıktan sonra sınıf dosyanız aşağıdakine benzer şekilde görünmelidir:

[!code-vb[Main](nested-master-pages-vb/samples/sample11.vb)]

Artık, Yönetim bölümünde bulunan içerik sayfalarının `BasePage`yerine `AdminBasePage` türetmemiz gerekir. `~/Admin` klasöründeki her içerik sayfası için arka plan kod dosyasına gidin ve bu değişikliği yapın. Örneğin `~/Admin/Default.aspx` ' de, arka plan kod sınıfı bildirimini öğesinden değiştirirsiniz:

[!code-vb[Main](nested-master-pages-vb/samples/sample12.vb)]

Hedef:

[!code-vb[Main](nested-master-pages-vb/samples/sample13.vb)]

Şekil 11 üst düzey ana sayfanın (`Site.master` veya `Alternate.master`), iç içe geçmiş ana sayfanın (`AdminNested.master`) ve yönetim bölümü içerik sayfalarının birbiriyle ilişkisini gösterir.

[Iç Içe ana sayfa ![, yönetim bölümündeki sayfalara özgü Içeriği tanımlar](nested-master-pages-vb/_static/image32.png)](nested-master-pages-vb/_static/image31.png)

**Şekil 11**: Iç Içe yerleştirilmiş ana sayfa, yönetim bölümündeki sayfalara özgü içeriği tanımlar ([tam boyutlu görüntüyü görüntülemek için tıklayın](nested-master-pages-vb/_static/image33.png))

## <a name="step-6-mirroring-the-master-pages-public-methods-and-properties"></a>6\. Adım: ana sayfanın ortak yöntemlerini ve özelliklerini yansıtma

`~/Admin/AddProduct.aspx` ve `~/Admin/Products.aspx` sayfalarının ana sayfayla programlı olarak etkileşimde bulunduğunu hatırlayın: `~/Admin/AddProduct.aspx` ana sayfanın ortak `RefreshRecentProductsGrid` yöntemini çağırır ve onun `GridMessageText` özelliğini ayarlıyor; `~/Admin/Products.aspx`, `PricesDoubled` olayı için bir olay işleyicisine sahiptir. Önceki öğreticide, bu genel üyeleri tanımlayan bir `MustInherit` `BaseMasterPage` sınıfı oluşturduk.

`~/Admin/AddProduct.aspx` ve `~/Admin/Products.aspx` sayfaları, ana sayfalarının `BaseMasterPage` sınıfından türediği varsayılır. Ancak `AdminNested.master` sayfası şu anda `System.Web.UI.MasterPage` sınıfını genişletiyor. Sonuç olarak, `~/Admin/Products.aspx` ziyaret edildiğinde `InvalidCastException` şu iletiyle oluşturulur: "' ASP. admin\_adminnested\_Master ' türündeki nesne ' BaseMasterPage ' türüne yayınlanamıyor."

Bu hatayı düzeltireceğiz, `AdminNested.master` arka plan kod sınıfı `BaseMasterPage`genişletmemiz gerekir. İç içe yerleştirilmiş ana sayfanın arka plan kod sınıfı bildirimini şuradan güncelleştirin:

[!code-vb[Main](nested-master-pages-vb/samples/sample14.vb)]

Hedef:

[!code-vb[Main](nested-master-pages-vb/samples/sample15.vb)]

Henüz bitmedi. `MustOverride`olarak işaretlenmiş üyeleri geçersiz kıldık, yani `RefreshRecentProductsGrid` ve `GridMessageText`. Bu Üyeler kullanıcı arabirimlerini güncelleştirmek için üst düzey ana sayfalar tarafından kullanılır. (Aslında yalnızca `Site.master` ana sayfası bu yöntemleri kullanır, ancak her iki üst düzey ana sayfa da `BaseMasterPage`genişlediğinden bu yöntemleri uygular.)

Bu üyeleri `AdminNested.master`uygulamamız gerekir, ancak tüm bu uygulamalar, iç içe yerleştirilmiş ana sayfa tarafından kullanılan en üst düzey ana sayfada yalnızca aynı üyeyi çağırmalıdır. Örneğin, yönetim bölümündeki bir içerik sayfası, iç içe yerleştirilmiş ana sayfanın `RefreshRecentProductsGrid` yöntemini çağırdığında, iç içe geçmiş ana sayfanın tek yapması gerekir, sırasıyla `Site.master` veya `Alternate.master``RefreshRecentProductsGrid` yöntemini çağırır.

Bunu başarmak için, `AdminNested.master`en üstüne aşağıdaki `@MasterType` yönergesini ekleyerek başlayın:

[!code-aspx[Main](nested-master-pages-vb/samples/sample16.aspx)]

`@MasterType` yönergesinin, `Master`adlı arka plan kod sınıfına kesin olarak yazılmış bir özellik ekleyeceğini hatırlayın. Sonra `RefreshRecentProductsGrid` ve `GridMessageText` üyelerini geçersiz kılın ve çağrıyı `Master`karşılık gelen yönteme devretmek yeterlidir:

[!code-vb[Main](nested-master-pages-vb/samples/sample17.vb)]

Bu kodla birlikte, yönetim bölümündeki içerik sayfalarını ziyaret edebilir ve kullanabilirsiniz. Şekil 12 ' de bir tarayıcıdan görüntülendiklerinde `~/Admin/Products.aspx` sayfası gösterilmektedir. Gördüğünüz gibi sayfa, iç içe ana sayfada tanımlanan yönetim yönergeleri kutusunu içerir.

[Yönetim bölümündeki Içerik sayfalarını ![her sayfanın üst kısmındaki yönergeleri Içerir](nested-master-pages-vb/_static/image35.png)](nested-master-pages-vb/_static/image34.png)

**Şekil 12**: yönetim bölümündeki içerik sayfaları, her sayfanın üst kısmındaki yönergeleri içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](nested-master-pages-vb/_static/image36.png))

## <a name="step-7-using-the-appropriate-top-level-master-page-at-runtime"></a>7\. Adım: çalışma zamanında uygun en üst düzey ana sayfayı kullanma

Yönetim bölümündeki tüm içerik sayfaları tamamen işlevsel olsa da, hepsi aynı üst düzey ana sayfayı kullanır ve `ChooseMasterPage.aspx`üzerinde kullanıcı tarafından seçilen ana sayfayı yoksayar. Bu davranış, iç içe yerleştirilmiş ana sayfanın `MasterPageFile` özelliği statik olarak `<%@ Master %>` yönergesinde `Site.master` olarak ayarlanmış olması nedeniyle olur.

Son Kullanıcı tarafından seçilen en üst düzey ana sayfayı kullanmak için, `AdminNested.master``MasterPageFile` özelliğini `MyMasterPage` oturum değişkenindeki değere ayarlamanız gerekir. `BasePage`' `MasterPageFile` içerik sayfalarının özelliklerini ayarlamamız nedeniyle, iç içe yerleştirilmiş ana sayfanın `MasterPageFile` özelliğini `BaseMasterPage` veya `AdminNested.master`arka plan kod sınıfında ayarlayabileceğimizi düşünebilirsiniz. Ancak, `MasterPageFile` özelliğini PreInit aşamasının sonuna kadar ayarlamış olmaları gerektiğinden, bu çalışmaz. Ana sayfadan sayfa yaşam döngüsüne programlı bir şekilde dokunduğumuz en kısa süre, Init aşamasıdır (ön Init aşamasından sonra gerçekleşir).

Bu nedenle, iç içe yerleştirilmiş ana sayfanın `MasterPageFile` özelliğini içerik sayfalarından ayarlamanız gerekir. `AdminNested.master` ana sayfasını kullanan tek içerik sayfaları `AdminBasePage`türetilir. Bu nedenle bu mantığı buraya koyabiliriz. 5\. adımda, sayfa nesnesinin `MasterPageFile` özelliğini "~/Admin/AdminNested.master" olarak ayarlayarak `SetMasterPageFile` yöntemi de çok fazla. `SetMasterPageFile`, ana sayfanın `MasterPageFile` özelliğini oturum içinde depolanan sonuca ayarlamak için de güncelleştirin:

[!code-vb[Main](nested-master-pages-vb/samples/sample18.vb)]

Önceki öğreticideki `BasePage` sınıfına eklediğimiz `GetMasterPageFileFromSession` yöntemi, oturum değişkeni değerine göre uygun ana sayfa dosya yolunu döndürür.

Bu değişiklik söz konusu olduğunda, kullanıcının ana sayfa seçimi yönetim bölümünün üzerinde geçiş yapar. Şekil 13, Şekil 12 ile aynı sayfayı gösterir, ancak Kullanıcı Ana sayfa seçimini `Alternate.master`olarak değiştirdikten sonra.

[Iç Içe geçmiş Yönetim sayfasında Kullanıcı tarafından seçilen en üst düzey ana sayfayı kullanan ![](nested-master-pages-vb/_static/image38.png)](nested-master-pages-vb/_static/image37.png)

**Şekil 13**: Iç Içe yönetim sayfası, Kullanıcı tarafından seçilen en üst düzey ana sayfayı kullanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](nested-master-pages-vb/_static/image39.png))

## <a name="summary"></a>Özet

İçerik sayfalarının ana sayfaya nasıl bağlanılmasından çok benzer şekilde, bir üst ana sayfaya bağlı bir alt ana sayfa oluşturarak iç içe yerleştirilmiş ana sayfalar oluşturmak mümkündür. Alt ana sayfa, üst öğesinin Contenttutucuların her biri için Içerik denetimleri tanımlayabilir; daha sonra bu Içerik denetimlerine kendi ContentPlaceHolder denetimlerini (Ayrıca diğer biçimlendirmeleri de) ekleyebilirler. İç içe yerleştirilmiş ana sayfalar, tüm sayfaların çok sayıda görünümü paylaştığı, ancak sitenin belirli bölümlerinin benzersiz özelleştirmeler gerektirmesine neden olan büyük Web uygulamalarında oldukça kullanışlıdır.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [İç içe ASP.NET ana sayfaları](https://msdn.microsoft.com/library/x2b3ktt7.aspx)
- [Iç Içe geçmiş ana sayfalar ve VS 2005 tasarım zamanı ipuçları](https://weblogs.asp.net/scottgu/archive/2005/11/11/430382.aspx)
- [VS 2008 Iç Içe ana sayfa desteği](https://weblogs.asp.net/scottgu/archive/2007/07/09/vs-2008-nested-master-page-support.aspx)

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 3,5 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)ister. Scott 'a [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) veya blogundan [http://ScottOnWriting.NET](http://scottonwriting.net/)üzerinden erişilebilir.

### <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, beni [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) bir satır bırakın

> [!div class="step-by-step"]
> [Öncekini](specifying-the-master-page-programmatically-vb.md)
