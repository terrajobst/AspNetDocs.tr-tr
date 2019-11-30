---
uid: web-forms/overview/older-versions-getting-started/master-pages/specifying-the-master-page-programmatically-cs
title: Ana sayfayı programlı olarak belirtme (C#) | Microsoft Docs
author: rick-anderson
description: İçerik sayfasının ana sayfasını, PreInit olay işleyicisi aracılığıyla programlı bir şekilde ayarlamaya bakar.
ms.author: riande
ms.date: 07/28/2008
ms.assetid: 7c4a3445-2440-4aee-b9fd-779c05e6abb2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/specifying-the-master-page-programmatically-cs
msc.type: authoredcontent
ms.openlocfilehash: 0db23ea05ba001c2bf9fc5330a60a767caa568a0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74590450"
---
# <a name="specifying-the-master-page-programmatically-c"></a>Ana Sayfayı Programlı Olarak Belirtme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_09_CS.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_09_CS.pdf)

> İçerik sayfasının ana sayfasını, PreInit olay işleyicisi aracılığıyla programlı bir şekilde ayarlamaya bakar.

## <a name="introduction"></a>Giriş

[*Ana sayfaları kullanarak site genelinde bir düzen oluşturma*](creating-a-site-wide-layout-using-master-pages-cs.md)bölümündeki ınaugural örneğinde, tüm içerik sayfaları, `@Page` yönergesindeki `MasterPageFile` özniteliği aracılığıyla ana sayfa bildirimli olarak başvurmuş. Örneğin, aşağıdaki `@Page` yönergesi içerik sayfasını ana sayfaya bağlar `Site.master`:

[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample1.aspx)]

`System.Web.UI` ad alanındaki [`Page` sınıfı](https://msdn.microsoft.com/library/system.web.ui.page.aspx) , içerik sayfasının ana sayfasının yolunu döndüren bir [`MasterPageFile` özelliği](https://msdn.microsoft.com/library/system.web.ui.page.masterpagefile.aspx) içerir; Bu, `@Page` yönergesi tarafından ayarlanan bu özelliktir. Bu özellik, içerik sayfasının ana sayfasını programlı bir şekilde belirtmek için de kullanılabilir. Bu yaklaşım, sayfayı ziyaret eden Kullanıcı gibi dış faktörlere bağlı olarak ana sayfayı dinamik olarak atamak istiyorsanız yararlıdır.

Bu öğreticide, Web sitemize ikinci bir ana sayfa ekler ve çalışma zamanında hangi ana sayfanın kullanılacağını dinamik olarak belirleyin.

## <a name="step-1-a-look-at-the-page-lifecycle"></a>1\. Adım: sayfa yaşam döngüsüne göz atın

Bir içerik sayfası olan bir ASP.NET sayfasının Web sunucusuna her ulaştığında, ASP.NET motoru sayfanın Içerik denetimlerini ana sayfanın karşılık gelen ContentPlaceHolder denetimlerine sigortası gerekir. Bu Fusion daha sonra tipik sayfa yaşam döngüsü boyunca geçebildiğiniz tek bir denetim hiyerarşisi oluşturur.

Şekil 1 ' de bu Fusion gösterilmektedir. Şekil 1 ' de 1. adım ilk içerik ve ana sayfa denetimi hiyerarşilerini gösterir. PreInit aşamasının kuyruk sonunda sayfadaki Içerik denetimleri, ana sayfadaki karşılık gelen Contentyertutucuları (2. adım) eklenir. Bu Fusion 'tan sonra ana sayfa, fkullanılan denetim hiyerarşisinin kökü olarak görev yapar. Bu fkullanılan denetim hiyerarşisi, son denetim hiyerarşisini oluşturmak için sayfaya eklenir (adım 3). Net sonucu, sayfanın denetim hiyerarşisinin Fuse denetim hiyerarşisini içermesi olur.

[Ana sayfa ve Içerik sayfasının denetim hiyerarşileri, PreInit aşamasında birlikte kullanılır ![](specifying-the-master-page-programmatically-cs/_static/image2.png)](specifying-the-master-page-programmatically-cs/_static/image1.png)

**Şekil 01**: Ana sayfa ve Içerik sayfasının denetim hiyerarşileri, Preinit aşaması sırasında birlikte kullanılır ([tam boyutlu görüntüyü görüntülemek için tıklayın](specifying-the-master-page-programmatically-cs/_static/image3.png))

## <a name="step-2-setting-themasterpagefileproperty-from-code"></a>2\. Adım:`MasterPageFile`özelliğini koddan ayarlama

Bu Fusion 'ta hangi ana sayfa paralalını `Page` nesnenin `MasterPageFile` özelliğinin değerine bağlıdır. `@Page` yönergesindeki `MasterPageFile` özniteliğinin ayarlanması, `Page``MasterPageFile` özelliğinin, sayfanın yaşam döngüsünün ilk aşaması olan başlangıç aşamasında atanması için net etkiye sahiptir. Alternatif olarak, bu özelliği programlı bir şekilde ayarlayabiliriz. Ancak bu özelliğin, Şekil 1 ' deki Fusion 'un gerçekleşmeden önce ayarlanması zorunludur.

PreInit aşamasının başlangıcında, `Page` nesnesi [`PreInit` olayını](https://msdn.microsoft.com/library/system.web.ui.page.preinit.aspx) oluşturur ve [`OnPreInit` yöntemini](https://msdn.microsoft.com/library/system.web.ui.page.onpreinit.aspx)çağırır. Ana sayfayı programlı olarak ayarlamak için, `PreInit` olayı için bir olay işleyicisi oluşturabilir veya `OnPreInit` yöntemini geçersiz kılabilirsiniz. Her iki yaklaşımdan de bakalım.

Sitenizin giriş sayfası için arka plan kod sınıfı dosyasını `Default.aspx.cs`açarak başlayın. Aşağıdaki kodu yazarak sayfanın `PreInit` olayına bir olay işleyicisi ekleyin:

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample2.cs)]

Buradan `MasterPageFile` özelliğini ayarlayabiliriz. Kodu, `MasterPageFile` özelliğine "~/site.exe" değerini atayan şekilde güncelleştirin.

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample3.cs)]

Bir kesme noktası ayarlar ve hata ayıklaması ile başlatırsanız, `Default.aspx` sayfa ziyaret edildiğinde veya bu sayfaya her geri gönderme yapıldığında, `Page_PreInit` olay işleyicisi çalıştırılır ve `MasterPageFile` özelliği "~/site.exe" olarak atanır.

Alternatif olarak, `Page` sınıfının `OnPreInit` yöntemini geçersiz kılabilir ve `MasterPageFile` özelliğini bu şekilde ayarlayabilirsiniz. Bu örnek için, ana sayfayı `BasePage`değil, belirli bir sayfada ayarlayalım. [*Ana sayfa öğreticisindeki başlık, meta etiketler ve DIĞER HTML üst bilgilerini belirterek*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) özel bir temel sayfa sınıfı (`BasePage`) oluşturduğumuz geri çekin. Şu anda `BasePage` `Page` sınıfının `OnLoadComplete` yöntemini geçersiz kılar, burada sayfanın `Title` özelliği site haritası verilerine göre ayarlanır. Ayrıca, ana sayfayı programlı olarak belirtmek için `OnPreInit` metodunu da geçersiz kılmak için `BasePage` güncelleştirelim.

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample4.cs)]

Tüm içerik sayfalarımız `BasePage`türetilmediği için, bunların hepsi ana sayfası programlı olarak atanmıştır. Bu noktada, `Default.aspx.cs` `PreInit` olay işleyicisi gereksiz; Bunu kaldırmayı ücretsiz hale gelmekten çekinmeyin.

### <a name="what-about-thepagedirective"></a>`@Page`yönergesi hakkında ne olacak?

Ne kadar karmaşık olabilecek, içerik sayfalarının ' `MasterPageFile` özelliklerinin artık iki yerde belirtilme yöntemidir: program aracılığıyla `BasePage` sınıfının `OnPreInit` yönteminde ve her bir içerik sayfasının `@Page` yönergesinde `MasterPageFile` özniteliği.

Sayfa yaşam döngüsünün ilk aşaması başlatma aşamasıdır. Bu aşamada `Page` nesnesinin `MasterPageFile` özelliği, `@Page` yönergesinde `MasterPageFile` özniteliğinin değeri olarak atanır (sağlanmışsa). PreInit aşaması, başlatma aşamasını izler ve `Page` nesnenin `MasterPageFile` özelliğini programlı bir şekilde ayarlamış olduğumuz ve böylece `@Page` yönergesinin atandığı değerin üzerine yazılmasına neden olur. `Page` nesnesinin `MasterPageFile` özelliğini program aracılığıyla ayarlamamız nedeniyle, son kullanıcının deneyimini etkilemeden `@Page` yönergesinin `MasterPageFile` özniteliğini kaldırabiliriz. Bunu ikna etmek için, devam edin ve `Default.aspx` ' deki `@Page` yönergesinden `MasterPageFile` özniteliğini kaldırın ve ardından sayfayı bir tarayıcıdan ziyaret edin. Beklendiğinde, çıkış öznitelik kaldırılmadan önceki ile aynı olur.

`MasterPageFile` özelliğinin `@Page` yönergesi aracılığıyla ayarlanmış olup olmadığı veya program aracılığıyla son kullanıcının deneyimine ne kadar önemsizdir. Ancak, `@Page` yönergesindeki `MasterPageFile` özniteliği, tasarımcıda WYSıWYG görünümü oluşturmak için tasarım zamanı sırasında Visual Studio tarafından kullanılır. Visual Studio 'da `Default.aspx` geri dönüp tasarımcıya gittiğinizde, "Ana sayfa hatası: sayfada bir ana sayfa başvurusu gerektiren denetimler var, ancak hiçbiri belirtilmemiş" iletisini görürsünüz (bkz. Şekil 2).

Kısacası, Visual Studio 'da zengin tasarım zamanı deneyiminin tadını çıkarmak için `@Page` yönergesindeki `MasterPageFile` özniteliğini bırakmanız gerekir.

[![Visual Studio, Tasarım görünümünü Işlemek için @Page yönergesinin MasterPageFile özniteliğini kullanır](specifying-the-master-page-programmatically-cs/_static/image5.png)](specifying-the-master-page-programmatically-cs/_static/image4.png)

**Şekil 02**: Visual Studio, Tasarım görünümünü işlemek Için `@Page` yönergesinin `MasterPageFile` özniteliğini kullanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](specifying-the-master-page-programmatically-cs/_static/image6.png))

## <a name="step-3-creating-an-alternative-master-page"></a>3\. Adım: alternatif ana sayfa oluşturma

Bir içerik sayfasının ana sayfası çalışma zamanında programlama yoluyla ayarlanabileceğinden, belirli bir ana sayfayı bazı dış ölçütlere göre dinamik olarak yüklemek mümkündür. Bu işlevsellik, site düzeninin kullanıcıya göre değişmesi gereken durumlarda yararlı olabilir. Örneğin, bir blog motoru Web uygulaması, kullanıcıların bloguna ait bir düzen seçmesine izin verebilir, her düzen farklı bir ana sayfayla ilişkilendirilir. Çalışma zamanında, bir ziyaretçi kullanıcının blogunu görüntülerken, Web uygulamasının blogunuzun yerleşimini belirlemesi ve ilgili ana sayfayı içerik sayfasıyla dinamik olarak ilişkilendirmeniz gerekir.

Bir ana sayfayı bazı dış ölçütlere göre çalışma zamanında dinamik olarak yüklemeyi inceleyelim. Web sitemiz şu anda yalnızca bir ana sayfa içeriyor (`Site.master`). Çalışma zamanında ana sayfa seçmeyi göstermek için başka bir ana sayfa gerekiyor. Bu adım, yeni ana sayfanın oluşturulmasına ve yapılandırılmasına odaklanmaktadır. 4\. adım, çalışma zamanında hangi ana sayfanın kullanılacağını belirlemede size bakar.

`Alternate.master`adlı kök klasörde yeni bir ana sayfa oluşturun. Ayrıca, `AlternateStyles.css`adlı Web sitesine yeni bir stil sayfası da ekleyin.

[![Web sitesine başka bir ana sayfa ve CSS dosyası ekleyin](specifying-the-master-page-programmatically-cs/_static/image8.png)](specifying-the-master-page-programmatically-cs/_static/image7.png)

**Şekil 03**: başka bir ana sayfa ve CSS dosyasını Web sitesine ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](specifying-the-master-page-programmatically-cs/_static/image9.png))

`Alternate.master` ana sayfasını, sayfanın üst kısmında, ortalanmış ve bir Navy arka planında görüntülenecek şekilde tasarlıyorum. Sol sütundan ayrıldım ve bu içeriği artık sayfanın genişliğinin tamamına yayılan `MainContent` ContentPlaceHolder denetiminin altına taşıdım. Ayrıca, sıralanmamış dersler listesini de `MainContent`yukarıdaki yatay bir listeyle değiştirdim. Ayrıca Ana sayfa tarafından kullanılan yazı tiplerini ve renkleri (ve uzantıya göre, içerik sayfalarını) güncelleştirdim. Şekil 4 ' te, `Alternate.master` ana sayfası kullanılırken `Default.aspx` gösterilmektedir.

> [!NOTE]
> ASP.NET, *temaları*tanımlama olanağını içerir. Tema, çalışma zamanında bir sayfaya uygulanabilen bir görüntü, CSS dosyası ve stille ilgili Web denetimi özelliği ayarları koleksiyonudur. Bu Temalar, sitenizin düzenlerinizin yalnızca görüntülenen görüntülerde ve CSS kuralları tarafından farklı olması durumunda gideceizin yoludur. Mizanpajlar, farklı Web denetimleri kullanma veya daha fazla farklı bir düzene sahip gibi önemli ölçüde farklıysa, ayrı ana sayfalar kullanmanız gerekir. Temalar hakkında daha fazla bilgi için Bu öğreticinin sonundaki daha fazla okuma bölümüne başvurun.

[Içerik sayfalarımız ![artık yeni bir görünüm kullanabilir](specifying-the-master-page-programmatically-cs/_static/image11.png)](specifying-the-master-page-programmatically-cs/_static/image10.png)

**Şekil 04**: içerik sayfalarımız artık yeni bir görünüm kullanabilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](specifying-the-master-page-programmatically-cs/_static/image12.png))

Ana ve içerik sayfalarının biçimlendirmesi FI kullanılırken `MasterPage` sınıfı, içerik sayfasındaki her Içerik denetiminin ana sayfada bir ContentPlaceHolder öğesine başvurduğundan emin olmak için kontrol eder. Var olmayan bir ContentPlaceHolder öğesine başvuran bir Içerik denetimi bulunursa bir özel durum oluşur. Diğer bir deyişle, içerik sayfasına atanan ana sayfanın içerik sayfasında her Içerik denetimi için bir ContentPlaceHolder 'a sahip olması zorunludur.

`Site.master` ana sayfası dört ContentPlaceHolder denetimi içerir:

- `head`
- `MainContent`
- `QuickLoginUI`
- `LeftColumnContent`

Web sitemizdeki bazı içerik sayfaları yalnızca bir veya iki Içerik denetimi içeriyor; diğer bir deyişle, kullanılabilir her bir Contenttutucuların Içerik denetimini içerir. Yeni ana sayfamız (`Alternate.master`) `Site.master` içindeki tüm Contentyertutucuları için Içerik denetimlerine sahip olan bu içerik sayfalarına atanabileceği için, `Alternate.master` aynı ContentPlaceHolder denetimlerinin de `Site.master`da dahil olması önemlidir.

`Alternate.master` ana sayfanızı mayın (bkz. Şekil 4), `AlternateStyles.css` stil sayfasında ana sayfanın stillerini tanımlayarak başlatın. Aşağıdaki kuralları `AlternateStyles.css`ekleyin:

[!code-css[Main](specifying-the-master-page-programmatically-cs/samples/sample5.css)]

Sonra, `Alternate.master`için aşağıdaki bildirime dayalı biçimlendirmeyi ekleyin. Gördüğünüz gibi `Alternate.master`, `Site.master`içindeki ContentPlaceHolder denetimleriyle aynı `ID` değerleri içeren dört ContentPlaceHolder denetimi içerir. Üstelik, ASP.NET AJAX çerçevesini kullanan Web sitemizdeki sayfalar için gerekli olan bir ScriptManager denetimini içerir.

[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample6.aspx)]

### <a name="testing-the-new-master-page"></a>Yeni Ana sayfa sınanıyor

Bu yeni ana sayfayı sınamak için, `MasterPageFile` özelliğine "~/Alternate.exe ana" değeri atanacak şekilde `BasePage` sınıfının `OnPreInit` metodunu güncelleştirin ve ardından Web sitesini ziyaret edin. Her sayfanın iki hariç hata olmadan çalışması gerekir: `~/Admin/AddProduct.aspx` ve `~/Admin/Products.aspx`. `~/Admin/AddProduct.aspx` ' de DetailsView 'a bir ürün eklemek, ana sayfanın `GridMessageText` özelliğini ayarlamaya çalıştığı kod satırından bir `NullReferenceException` sonuçlanır. `~/Admin/Products.aspx` ziyaret edildiğinde, sayfa yüklenirken "ASP. alternatif\_Master ' türündeki nesne ' ASP. site\_Master ' türüne atılamamak üzere bir `InvalidCastException` oluşturulur."

Bu hatalar, `Site.master` arka plan kod sınıfı, `Alternate.master`tanımlı olmayan ortak olayları, özellikleri ve yöntemleri içerdiğinden oluşur. Bu iki sayfanın biçimlendirme bölümünün `Site.master` ana sayfasına başvuran bir `@MasterType` yönergesi vardır.

[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample7.aspx)]

Ayrıca, DetailsView 'un `~/Admin/AddProduct.aspx` `ItemInserted` olay işleyicisi, gevşek olarak yazılmış `Page.Master` özelliğini `Site`türündeki bir nesneye veren kodu içerir. `@MasterType` yönergesi (Bu şekilde kullanılır) ve `ItemInserted` olay işleyicisindeki atama `~/Admin/AddProduct.aspx` ve `~/Admin/Products.aspx` sayfalarını `Site.master` ana sayfasına sıkı şekilde bağar.

Bu sıkı kuponu bölmek için `Site.master` ve `Alternate.master` ortak üyelerin tanımlarını içeren ortak bir temel sınıftan türeyebiliriz. Bunu izleyerek, bu ortak temel türe başvurmak için `@MasterType` yönergesini güncelleştirebiliriz.

### <a name="creating-a-custom-base-master-page-class"></a>Özel bir temel Ana sayfa sınıfı oluşturma

`BaseMasterPage.cs` adlı `App_Code` klasöre yeni bir sınıf dosyası ekleyin ve `System.Web.UI.MasterPage`türetebilirsiniz. `BaseMasterPage`' de `RefreshRecentProductsGrid` yöntemini ve `GridMessageText` özelliğini belirlememiz gerekir, ancak bu Üyeler `Site.master` ana sayfasına (`RecentProducts` GridView ve `GridMessage` etiketi) özgü Web denetimleriyle çalıştıkları için bu öğeleri `Site.master` buraya taşıyamıyoruz.

Yapmanız gerekenler, bu üyelerin burada tanımlanması, ancak gerçekten `BaseMasterPage`türetilmiş sınıflar (`Site.master` ve `Alternate.master`) tarafından uygulandığı şekilde `BaseMasterPage` yapılandırmaktır. Bu tür kalıtımı, sınıfı ve üyelerini `abstract`olarak işaretleyerek mümkündür. Kısacası, bu iki üyeye `abstract` anahtar sözcüğünü eklemek, `BaseMasterPage` `RefreshRecentProductsGrid` ve `GridMessageText`uygulamadığını, ancak türetilen sınıfların olacağını duyuruyor.

Ayrıca, `BaseMasterPage` `PricesDoubled` olayını tanımlamanız ve olayı yükseltmek için türetilmiş sınıflar tarafından bir yol sağlamanız gerekir. Bu davranışı kolaylaştırmak için .NET Framework kullanılan desenler, temel sınıfta ortak bir olay oluşturmak ve `OnEventName`adlı korumalı bir `virtual` yöntemi eklemektir. Türetilmiş sınıflar daha sonra olayı yükseltmek için bu yöntemi çağırabilir veya olay oluşturulmadan hemen önce veya sonra kodu yürütmek için geçersiz kılabilir.

`BaseMasterPage` sınıfınızı aşağıdaki kodu içerecek şekilde güncelleştirin:

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample8.cs)]

Sonra, `Site.master` arka plan kod sınıfına gidin ve `BaseMasterPage`türetebilirsiniz. `BaseMasterPage` `abstract` bu `abstract` üyelerini `Site.master`' de geçersiz kılmalıdır. Yöntem ve özellik tanımlarına `override` anahtar sözcüğünü ekleyin. Ayrıca, `DoublePrice` düğmesinin `Click` olay işleyicisindeki `PricesDoubled` olayı temel sınıfın `OnPricesDoubled` yöntemine yapılan bir çağrıyla oluşturan kodu güncelleştirin.

Bu değişiklikler sonrasında `Site.master` arka plan kod sınıfı aşağıdaki kodu içermelidir:

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample9.cs)]

Ayrıca, `BaseMasterPage` türetmek ve iki `abstract` üyesini geçersiz kılmak için `Alternate.master`arka plan kod sınıfını güncelleştirmemiz gerekir. Ancak `Alternate.master`, en son ürünleri veya veritabanına yeni bir ürün eklendikten sonra bir ileti görüntüleyen bir etiketi içeren bir GridView içermediğinden, bu yöntemlerin hiçbir şey yapması gerekmez.

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample10.cs)]

### <a name="referencing-the-base-master-page-class"></a>Temel Ana sayfa sınıfına başvurma

Artık `BaseMasterPage` sınıfını tamamladığımıza ve iki ana sayfamızı genişlettireceğimize göre, son adımınız bu ortak türe başvurmak için `~/Admin/AddProduct.aspx` ve `~/Admin/Products.aspx` sayfalarını güncelleştiririz. Her iki sayfada de `@MasterType` yönergesini değiştirerek başlayın:

[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample11.aspx)]

Kime:

[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample12.aspx)]

Bir dosya yoluna başvurmak yerine `@MasterType` özelliği artık temel türe (`BaseMasterPage`) başvurur. Sonuç olarak, her iki sayfada da arka plan kod sınıflarında kullanılan kesin türü belirtilmiş `Master` özelliği artık `BaseMasterPage` türündedir (`Site`türü yerine). Bu değişiklik yerinde yeniden ziyaret `~/Admin/Products.aspx`. Daha önce, sayfa `Alternate.master` ana sayfasını kullanacak şekilde yapılandırıldığı, ancak `@MasterType` yönergesi `Site.master` dosyasına başvurduğu için bu bir atama hatası ile sonuçlandı. Ancak artık sayfa hatasız olarak işlenir. Bunun nedeni, `Alternate.master` ana sayfanın `BaseMasterPage` türünde bir nesneye (genişlettiğinden) yayınlanabileceğinden.

`~/Admin/AddProduct.aspx`' de yapılması gereken bir küçük değişiklik vardır. DetailsView denetiminin `ItemInserted` olay işleyicisi hem kesin türü belirtilmiş `Master` özelliğini hem de gevşek olarak yazılmış `Page.Master` özelliğini kullanır. `@MasterType` yönergesini güncelleştirdiğimiz halde kesin tür belirtilmiş başvuruyu düzelttik, ancak yine de gevşek yazılmış başvuruyu güncelleştirmemiz gerekiyor. Aşağıdaki kod satırını değiştirin:

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample13.cs)]

Aşağıdaki ile `Page.Master` temel türe yayınlar:

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample14.cs)]

## <a name="step-4-determining-what-master-page-to-bind-to-the-content-pages"></a>4\. Adım: Içerik sayfalarına hangi ana sayfanın bağlanacağını belirleme

`BasePage` sınıfınız Şu anda tüm içerik sayfaları ' `MasterPageFile` özelliklerini sayfa yaşam döngüsünün PreInit aşamasında sabit kodlanmış bir değere ayarlıyor. Bu kodu, ana sayfayı bir dış faktörde temel alarak güncelleştirebiliriz. Belki de yüklenecek ana sayfa, oturum açmış olan kullanıcının tercihlerine bağlıdır. Bu durumda, şu anda ziyaret edilen kullanıcının ana sayfa tercihlerini gösteren `BasePage` `OnPreInit` yönteminde kod yazmamız gerekir.

Kullanıcının hangi ana sayfanın kullanılacağını seçebilmesine izin veren bir Web sayfası oluşturalım `Site.master` veya `Alternate.master` ve bu seçimi bir oturum değişkenine kaydeder. `ChooseMasterPage.aspx`adlı kök dizinde yeni bir Web sayfası oluşturarak başlayın. Bu sayfayı (veya başka bir içerik sayfası) oluştururken, ana sayfa `BasePage`programlı olarak ayarlandığı için onu ana sayfaya bağlamanız gerekmez. Bununla birlikte, yeni sayfayı bir ana sayfaya bağlamayın, yeni sayfanın varsayılan bildirime dayalı biçimlendirmesi, ana sayfa tarafından sağlanan bir Web formu ve diğer içerikleri içerir. Bu biçimlendirmeyi uygun Içerik denetimleriyle el ile değiştirmeniz gerekir. Bu nedenle, yeni ASP.NET sayfasını bir ana sayfaya bağlamayı daha kolay buldum.

> [!NOTE]
> `Site.master` ve `Alternate.master` aynı ContentPlaceHolder denetimleri kümesine sahip olduğundan, yeni içerik sayfasını oluştururken hangi ana sayfanın tercih ettiğinize bağımsız değildir. Tutarlılık için `Site.master`kullanmayı öneriyorum.

[Web sitesine yeni bir Içerik sayfası eklemek ![](specifying-the-master-page-programmatically-cs/_static/image14.png)](specifying-the-master-page-programmatically-cs/_static/image13.png)

**Şekil 05**: Web sitesine yeni içerik sayfası ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](specifying-the-master-page-programmatically-cs/_static/image15.png))

`Web.sitemap` dosyasını bu ders için bir giriş içerecek şekilde güncelleştirin. Ana sayfalar ve ASP.NET AJAX dersi için `<siteMapNode>` altına aşağıdaki biçimlendirmeyi ekleyin:

[!code-xml[Main](specifying-the-master-page-programmatically-cs/samples/sample15.xml)]

`ChooseMasterPage.aspx` sayfasına herhangi bir içerik eklemeden önce, sayfanın arka plan kod sınıfını (`System.Web.UI.Page`yerine) `BasePage` türeten önce güncellemek için bir dakikanızı ayırın. Sonra, sayfaya bir DropDownList denetimi ekleyin, `ID` özelliğini `MasterPageChoice`olarak ayarlayın ve "~/site. Master" ve "~/Alternate.exe" `Text` değerleriyle iki ListItems ekleyin.

Sayfaya bir düğme web denetimi ekleyin ve `ID` ve `Text` özelliklerini sırasıyla `SaveLayout` ve "düzen seçimini Kaydet" olarak ayarlayın. Bu noktada sayfanızın bildirime dayalı biçimlendirmesi aşağıdakine benzer görünmelidir:

[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample16.aspx)]

Sayfa ilk kez ziyaret edildiğinde, kullanıcının şu anda seçili olan ana sayfa seçimini görüntülemesi gerekir. `Page_Load` olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample17.cs)]

Yukarıdaki kod yalnızca ilk sayfada (sonraki geri göndermeler için değil) ziyaret çalıştırılır. Önce oturum değişkeninin `MyMasterPage` olup olmadığını kontrol eder. Varsa, `MasterPageChoice` DropDownList 'de eşleşen ListItem bulmayı dener. Eşleşen bir ListItem bulunursa, `Selected` özelliği `true`olarak ayarlanır.

Ayrıca, kullanıcının seçimini `MyMasterPage` oturum değişkenine kaydeden koda de ihtiyacımız var. `SaveLayout` düğmenin `Click` olayı için bir olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample18.cs)]

> [!NOTE]
> `Click` olay işleyicisi geri gönderme sırasında yürütüldüğünde, ana sayfa zaten seçilmiş demektir. Bu nedenle, bir sonraki sayfa ziyaret edilene kadar kullanıcının açılan liste seçimi geçerli olmayacaktır. `Response.Redirect` tarayıcıyı `ChooseMasterPage.aspx`yeniden isteyecek şekilde zorlar.

`ChooseMasterPage.aspx` sayfası tamamlandıktan sonra son görevimiz, `MyMasterPage` Session değişkeninin değerine göre `MasterPageFile` özelliğini `BasePage` atayacaktır. Oturum değişkeni ayarlanmamışsa `Site.master``BasePage` varsayılan değeri yoktur.

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample19.cs)]

> [!NOTE]
> `Page` nesnesinin `MasterPageFile` özelliğini `OnPreInit` olay işleyicisine ve iki ayrı yönteme atayan kodu taşıdım. Bu ilk yöntem `SetMasterPageFile`, `GetMasterPageFileFromSession`ikinci yöntem tarafından döndürülen değere `MasterPageFile` özelliğini atar. `SetMasterPageFile` yöntemi `virtual`, bu `BasePage` genişleten gelecekteki sınıfların isteğe bağlı olarak özel mantık uygulamak üzere geçersiz kılmasını sağlayabilirsiniz. Bir sonraki öğreticide `BasePage``SetMasterPageFile` özelliğini geçersiz kılma örneği görüyoruz.

Bu kodla birlikte `ChooseMasterPage.aspx` sayfasını ziyaret edin. Başlangıçta ana sayfa `Site.master` seçilidir (bkz. Şekil 6), ancak Kullanıcı açılan listeden farklı bir ana sayfa seçebilir.

[![Içerik sayfaları site. Master ana sayfası kullanılarak görüntülenir](specifying-the-master-page-programmatically-cs/_static/image17.png)](specifying-the-master-page-programmatically-cs/_static/image16.png)

**Şekil 06**: içerik sayfaları `Site.master` ana sayfa kullanılarak görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](specifying-the-master-page-programmatically-cs/_static/image18.png))

[![Içerik sayfaları artık alternatif. Master ana sayfası kullanılarak gösteriliyor](specifying-the-master-page-programmatically-cs/_static/image20.png)](specifying-the-master-page-programmatically-cs/_static/image19.png)

**Şekil 07**: Içerik sayfaları artık `Alternate.master` ana sayfası kullanılarak görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](specifying-the-master-page-programmatically-cs/_static/image21.png))

## <a name="summary"></a>Özet

İçerik sayfası ziyaret edildiğinde, Içerik denetimleri ana sayfanın ContentPlaceHolder denetimleriyle birlikte kullanılır. İçerik sayfasının ana sayfası, başlatma aşamasında `@Page` yönergesinin `MasterPageFile` özniteliğine atanan `Page` sınıfın `MasterPageFile` özelliği tarafından gösterilir. Bu öğreticide, Önınıt aşamasının sonundan önce yaptığımız sürece `MasterPageFile` özelliğine bir değer atayabiliriz. Ana sayfayı programlı bir şekilde belirleyebilmek, dış faktörlere bağlı olarak bir içerik sayfasını dinamik olarak ana sayfaya bağlama gibi daha gelişmiş senaryolar için kapıyı açar.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ASP.NET sayfası yaşam döngüsü diyagramı](http://emanish.googlepages.com/Asp.Net2.0Lifecycle.PNG)
- [ASP.NET sayfa yaşam döngüsüne genel bakış](https://msdn.microsoft.com/library/ms178472.aspx)
- [ASP.NET Temalar ve kaplamalar genel bakış](https://msdn.microsoft.com/library/ykzx33wh.aspx)
- [Ana sayfalar: Ipuçları, püf noktaları ve tuzaklar](http://www.odetocode.com/articles/450.aspx)
- [ASP.NET 'deki Temalar](http://www.odetocode.com/articles/423.aspx)

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 3,5 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)ister. Scott 'a [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) veya blogundan [http://ScottOnWriting.NET](http://scottonwriting.net/)üzerinden erişilebilir.

### <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için lider gözden geçiren Suçi Banerjee idi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, beni [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) bir satır bırakın

> [!div class="step-by-step"]
> [Önceki](master-pages-and-asp-net-ajax-cs.md)
> [İleri](nested-master-pages-cs.md)
