---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-cs
title: SqlDataSource denetimiyle verileri sorgulama (C#) | Microsoft Docs
author: rick-anderson
description: Önceki öğreticilerde, veri erişim katmanından sunum katmanını tamamen ayırmak için ObjectDataSource denetimini kullandık. Bu Tutor 'dan itibaren...
ms.author: riande
ms.date: 02/20/2007
ms.assetid: 60512d6a-b572-4b7a-beb3-3e44b4d2020c
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 5bda42965f7d1db71b207c0b76e251b8fff64e31
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606187"
---
# <a name="querying-data-with-the-sqldatasource-control-c"></a>SqlDataSource Denetimi ile Veri Sorgulama (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_47_CS.exe) veya [PDF 'yi indirin](querying-data-with-the-sqldatasource-control-cs/_static/datatutorial47cs1.pdf)

> Önceki öğreticilerde, veri erişim katmanından sunum katmanını tamamen ayırmak için ObjectDataSource denetimini kullandık. Bu öğreticiden başlayarak, SqlDataSource denetiminin sunum ve veri erişimi için katı bir ayrım gerektirmeyen basit uygulamalar için nasıl kullanılabileceğini öğreniyoruz.

## <a name="introduction"></a>Giriş

Şimdiye kadar incelediğimiz tüm öğreticiler, sunum, Iş mantığı ve veri erişimi katmanlarından oluşan katmanlı bir mimari kullandık. Veri erişim katmanı (DAL) ilk öğreticide ([veri erişim katmanı oluşturma](../introduction/creating-a-data-access-layer-cs.md)) ve Ikinci bir Iş mantığı katmanının ([Iş mantığı katmanı oluşturma](../introduction/creating-a-business-logic-layer-cs.md)) oluşturulmuştur. [ObjectDataSource Ile verileri görüntüleme](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md) öğreticisiyle başlayarak, ASP.NET 2,0 s New ObjectDataSource denetimini, sunu katmanından mimariyle bildirimli arabirim olarak nasıl kullanacağınızı gördük.

Şimdiye kadar olan tüm öğreticiler, verilerle çalışmak üzere mimarinin kullanıldığı sürece, mimari atlayarak veritabanı verilerini doğrudan bir ASP.NET sayfasından erişmek, eklemek, güncelleştirmek ve silmek de mümkündür. Bunu yaptığınızda, belirli veritabanı sorguları ve iş mantığını doğrudan Web sayfasına yerleştirirsiniz. Yeterince büyük veya karmaşık uygulamalarda, katmanlı bir mimari tasarlamak, uygulamak ve kullanmak uygulamanın başarı, Güncelleştirilebilirlik ve bakım açısından önemli değildir. Ancak, daha güçlü bir mimari geliştirme, tek seferlik basit uygulamalar oluştururken gereksiz olabilir.

ASP.NET 2,0, [SqlDataSource](https://msdn.microsoft.com/library/dz12d98w%28vs.80%29.aspx), [AccessDataSource](https://msdn.microsoft.com/library/8e5545e1.aspx), [ObjectDataSource](https://msdn.microsoft.com/library/9a4kyhcx.aspx), [XmlDataSource](https://msdn.microsoft.com/library/e8d8587a%28en-US,VS.80%29.aspx)ve [SiteMapDataSource](https://msdn.microsoft.com/library/5ex9t96x%28en-US,VS.80%29.aspx)gibi beş yerleşik veri kaynağı denetimi sağlar. SqlDataSource, Microsoft SQL Server, Microsoft Access, Oracle, MySQL ve diğerleri dahil olmak üzere bir ilişkisel veritabanından doğrudan erişmek ve veri değiştirmek için kullanılabilir. Bu öğreticide ve sonraki üç adımda, SqlDataSource denetimiyle çalışmayı, veritabanı verilerinin sorgulanarak ve filtreleneceğini araştırmaya ve verileri eklemek, güncelleştirmek ve silmek için SqlDataSource 'un nasıl kullanılacağını inceleyeceğiz.

![ASP.NET 2,0, beş yerleşik veri kaynağı denetimini Içerir](querying-data-with-the-sqldatasource-control-cs/_static/image1.gif)

**Şekil 1**: ASP.NET 2,0, beş yerleşik veri kaynağı denetimini içerir

## <a name="comparing-the-objectdatasource-and-sqldatasource"></a>ObjectDataSource ve SqlDataSource karşılaştırılıyor

Kavramsal olarak, hem ObjectDataSource hem de SqlDataSource denetimleri yalnızca veri proxy 'leri olur. ObjectDataSource [Ile verileri görüntüleme konusunda](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md) anlatıldığı gibi, ObjectDataSource, verileri sağlayan nesne türünü ve temel alınan nesne türünden verileri seçmek, eklemek, güncelleştirmek ve silmek için çağrılacak yöntemleri belirten özelliklere sahiptir. ObjectDataSource 'un özellikleri yapılandırıldıktan sonra, GridView, DetailsView veya DataList gibi bir veri Web denetimi, temel mimariyle etkileşim kurmak için `Select()`, `Insert()`, `Delete()`ve `Update()` yöntemleri kullanılarak denetime bağlanabilir.

SqlDataSource aynı işlevselliği sağlar, ancak nesne kitaplığı yerine ilişkisel bir veritabanına göre çalışır. SqlDataSource ile veri ekleme, güncelleştirme, silme ve alma işlemleri için veritabanı bağlantı dizesini ve geçici SQL sorgularını veya çalıştırılacak saklı yordamları belirtmemiz gerekir. `Select()`, `Insert()`, `Update()`ve `Delete()` yöntemleri, çağrıldığında, belirtilen veritabanına bağlanır ve uygun SQL sorgusunu verebilir. Aşağıdaki diyagramda gösterildiği gibi, bu yöntemler bir veritabanına bağlanma, sorgu verme ve sonuçları döndürme için gryeniden çalışma işini yapılır.

![SqlDataSource, veritabanına bir proxy görevi görür](querying-data-with-the-sqldatasource-control-cs/_static/image2.gif)

**Şekil 2**: SqlDataSource veritabanına bir proxy görevi görür

> [!NOTE]
> Bu öğreticide, veritabanından veri almaya odaklanacağız. [SqlDataSource denetim öğreticisiyle veri ekleme, güncelleştirme ve silme](inserting-updating-and-deleting-data-with-the-sqldatasource-cs.md) konusunda, SqlDataSource 'un ekleme, güncelleştirme ve silme desteği için nasıl yapılandırılacağını inceleyeceğiz.

## <a name="the-sqldatasource-and-accessdatasource-controls"></a>SqlDataSource ve AccessDataSource denetimleri

ASP.NET 2,0, SqlDataSource denetimine ek olarak bir AccessDataSource denetimi de içerir. Bu iki farklı denetim, ASP.NET 2,0 ' ye yeni bir çok geliştirici sağlar. Bu, AccessDataSource denetiminin yalnızca Microsoft SQL Server ile çalışmak üzere tasarlanan SqlDataSource denetimiyle Microsoft Access ile özel olarak çalışacak şekilde tasarlandığından şüphelenmesine neden olur. AccessDataSource özellikle Microsoft Access ile çalışacak şekilde tasarlandığından, SqlDataSource denetimi .NET aracılığıyla erişilebilen *herhangi bir* ilişkisel veritabanıyla çalışır. Bu, çok sayıda Microsoft SQL Server, Microsoft Access, Oracle, Informix, MySQL ve PostgreSQL gibi herhangi bir OleDb veya ODBC uyumlu veri deposunu içerir.

AccessDataSource ve SqlDataSource denetimleri arasındaki tek fark, veritabanı bağlantı bilgilerinin nasıl belirtildidir. AccessDataSource denetimi yalnızca Access veritabanı dosyasının dosya yolunu gerektirir. Diğer yandan SqlDataSource, bir bağlantı dizesi gerektirir.

## <a name="step-1-creating-the-sqldatasource-web-pages"></a>1\. Adım: SqlDataSource Web sayfaları oluşturma

SqlDataSource denetimini kullanarak veritabanı verileriyle doğrudan nasıl çalışacağımız konusunda keşfetmeye başlamadan önce, Web sitesi projemizdeki Bu öğretici ve sonraki üç için gereken ASP.NET sayfalarını oluşturmak için önce bir süre sürme. `SqlDataSource`adlı yeni bir klasör ekleyerek başlayın. Ardından, aşağıdaki ASP.NET sayfalarını bu klasöre ekleyerek her bir sayfayı `Site.master` ana sayfasıyla ilişkilendirdiğinizden emin olun:

- `Default.aspx`
- `Querying.aspx`
- `ParameterizedQueries.aspx`
- `InsertUpdateDelete.aspx`
- `OptimisticConcurrency.aspx`

![SqlDataSource ile Ilgili öğreticiler için ASP.NET sayfaları ekleyin](querying-data-with-the-sqldatasource-control-cs/_static/image3.gif)

**Şekil 3**: SqlDataSource Ile ilgili öğreticiler Için ASP.NET sayfaları ekleme

Diğer klasörlerde olduğu gibi, `SqlDataSource` klasöründeki `Default.aspx` öğreticileri bölümündeki öğreticilerin listelecektir. `SectionLevelTutorialListing.ascx` Kullanıcı denetiminin bu işlevselliği sağladığını hatırlayın. Bu nedenle, bu kullanıcı denetimini Çözüm Gezgini sayfa s Tasarım görünümü üzerine sürükleyerek `Default.aspx` ekleyin.

[SectionLevelTutorialListing. ascx Kullanıcı denetimini default. aspx öğesine eklemek ![](querying-data-with-the-sqldatasource-control-cs/_static/image5.gif)](querying-data-with-the-sqldatasource-control-cs/_static/image4.gif)

**Şekil 4**: `Default.aspx` Için `SectionLevelTutorialListing.ascx` Kullanıcı denetimini ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](querying-data-with-the-sqldatasource-control-cs/_static/image6.gif))

Son olarak, bu dört sayfayı `Web.sitemap` dosyasına girdi olarak ekleyin. Özellikle, DataList ve Repeater `<siteMapNode>`özel düğmeler eklendikten sonra aşağıdaki biçimlendirmeyi ekleyin:

[!code-sql[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample1.sql)]

`Web.sitemap`güncelleştirildikten sonra Öğreticiler Web sitesini bir tarayıcıdan görüntülemek için bir dakikanızı ayırın. Sol taraftaki menü artık öğreticilerin düzenlenmesine, eklemeye ve silinmesine yönelik öğeler içerir.

![Site Haritası artık SqlDataSource öğreticileri için girdiler Içeriyor](querying-data-with-the-sqldatasource-control-cs/_static/image7.gif)

**Şekil 5**: site haritasında artık SqlDataSource öğreticileri Için girişler yer almaktadır

## <a name="step-2-adding-and-configuring-the-sqldatasource-control"></a>2\. Adım: SqlDataSource denetimini ekleme ve yapılandırma

`SqlDataSource` klasöründeki `Querying.aspx` sayfasını açıp Tasarım görünümü 'e geçiş yaparak başlayın. Araç kutusundan bir SqlDataSource denetimini tasarımcı üzerine sürükleyin ve `ID` `ProductsDataSource`olarak ayarlayın. ObjectDataSource gibi, SqlDataSource işlenen herhangi bir çıktı oluşturmaz ve bu nedenle tasarım yüzeyinde gri kutu olarak görünür. SqlDataSource 'u yapılandırmak için SqlDataSource s akıllı etiketinden veri kaynağını Yapılandır bağlantısına tıklayın.

![SqlDataSource s akıllı etiketinden veri kaynağını Yapılandır bağlantısına tıklayın](querying-data-with-the-sqldatasource-control-cs/_static/image8.gif)

**Şekil 6**: SqlDataSource s akıllı etiketinden veri kaynağını Yapılandır bağlantısına tıklayın

Bu, SqlDataSource denetim s veri kaynağını yapılandırma Sihirbazı 'nı getirir. Sihirbazın adımları, ObjectDataSource denetiminden farklı olsa da, son hedef, veri kaynağı aracılığıyla veri alma, ekleme, güncelleştirme ve silme hakkındaki ayrıntıları sağlamak için aynıdır. SqlDataSource için bu, kullanılacak temel veritabanını belirtmeyi ve geçici SQL deyimlerini veya saklı yordamları sağlamayı gerektirir.

İlk sihirbaz adımı, veritabanı için bize sorar. Açılan liste, Web uygulaması `App_Data` klasöründe bulunan bu veritabanlarını ve Sunucu Gezgini veri bağlantıları düğümüne eklenmiş olanları içerir. `App_Data` klasöründeki `NORTHWIND.MDF` veritabanı için proje s `Web.config` dosyasına zaten bir bağlantı dizesi eklediğimiz için, açılan liste bu bağlantı dizesinin bir başvurusunu içerir `NORTHWINDConnectionString`. Aşağı açılan listeden bu öğeyi seçin ve Ileri ' ye tıklayın.

![Açılan listeden NORTHWINDConnectionString öğesini seçin](querying-data-with-the-sqldatasource-control-cs/_static/image9.gif)

**Şekil 7**: açılan listeden `NORTHWINDConnectionString` seçin

Veritabanı seçildikten sonra sihirbaz, sorgunun veri döndürmesini ister. Döndürülecek veya özel bir SQL ifadesini girebileceğiniz ya da bir saklı yordam belirtebileceğiniz bir tablonun veya görünümün sütunlarını belirttik. Özel bir SQL ifadesini veya saklı yordamı belirleme ve tablo veya görünüm radyo düğmelerini kullanarak bu seçim arasında geçiş yapabilirsiniz.

> [!NOTE]
> Bu ilk örnek için, bir tablo veya görünüm seçeneğinde sütunları belirt ' i kullanalım. Bu öğreticide daha sonra sihirbaza geri döneceğiz ve özel bir SQL ifadesini veya saklı yordamı belirtme seçeneğini keşfetmeye başlayacağız.

Şekil 8 ' de bir tablodan sütun belirt veya bir görünüm radyo düğmesi seçildiğinde Select Ifadesini Yapılandır ekranı görüntülenir. Aşağı açılan listede, aşağıdaki onay kutusu listesinde bulunan seçili tablo veya görünüm sütunları ile Northwind veritabanındaki tablo ve görünüm kümesi bulunur. Bu örnekte, s `ProductID`, `ProductName`ve `UnitPrice` sütunlarını `Products` tablosundan döndürmesini sağlar. Şekil 8 ' de gösterildiği gibi, bu seçimleri yaptıktan sonra sihirbaz, sonuçta elde edilen SQL ifadesini `SELECT [ProductID], [ProductName], [UnitPrice] FROM [Products]`gösterir.

![Products tablosundan veri döndürme](querying-data-with-the-sqldatasource-control-cs/_static/image10.gif)

**Şekil 8**: `Products` tablosundan veri döndürme

Sihirbazı `Products` tablosundan `ProductID`, `ProductName`ve `UnitPrice` sütunları döndürecek şekilde yapılandırdıktan sonra Ileri düğmesine tıklayın. Bu son ekran, önceki adımdan yapılandırılan sorgunun sonuçlarını incelemek için bir fırsat sağlar. Sorguyu Sına düğmesine tıklamak yapılandırılmış `SELECT` ifadesini yürütür ve sonuçları bir kılavuzda görüntüler.

![Seçme sorgunuzu gözden geçirmek için sorguyu Sına düğmesine tıklayın](querying-data-with-the-sqldatasource-control-cs/_static/image11.gif)

**Şekil 9**: `SELECT` sorgunuzu gözden geçirmek Için sorguyu Sına düğmesine tıklayın

Sihirbazı tamamladığınızda son ' a tıklayın.

ObjectDataSource gibi, SqlDataSource s Sihirbazı yalnızca denetim s özelliklerine değerler atar, bu da [`ConnectionString`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.connectionstring.aspx) ve [`SelectCommand`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.selectcommand.aspx) özelliklerdir. Sihirbazı tamamladıktan sonra, SqlDataSource denetim bildirim temelli işaretlerinizin aşağıdakine benzer şekilde görünmesi gerekir:

[!code-aspx[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample2.aspx)]

`ConnectionString` özelliği, veritabanına bağlanma hakkında bilgi sağlar. Bu özelliğe, tam, sabit kodlanmış bir bağlantı dizesi değeri atanabilir veya `Web.config`içindeki bir bağlantı dizesine işaret edebilir. Web. config dosyasındaki bir bağlantı dizesi değerine başvurmak için `<%$ expressionPrefix:expressionValue %>`söz dizimini kullanın. Genellikle, *ExpressionPrefix* ConnectionString ve *expressionvalue* , `Web.config` [`<connectionStrings>` bölümündeki](https://msdn.microsoft.com/library/bf7sd233.aspx)bağlantı dizesinin adıdır. Ancak söz dizimi, kaynak dosyalarından `<appSettings>` öğelerine veya içeriğe başvurmak için kullanılabilir. Bu söz dizimi hakkında daha fazla bilgi için bkz. [ASP.net Ifadeleri Overview](https://msdn.microsoft.com/library/d5bd1tad.aspx) .

`SelectCommand` özelliği, verileri döndürmek için yürütülecek geçici SQL ifadesini veya saklı yordamı belirtir.

## <a name="step-3-adding-a-data-web-control-and-binding-it-to-the-sqldatasource"></a>3\. Adım: veri Web denetimi ekleme ve SqlDataSource 'a bağlama

SqlDataSource yapılandırıldıktan sonra, GridView veya DetailsView gibi bir veri Web denetimine bağlanabilir. Bu öğreticide, verileri bir GridView 'da görüntüler. Araç kutusundan bir GridView öğesini sayfaya sürükleyin ve GridView s akıllı etiketindeki açılan listeden veri kaynağını seçerek `ProductsDataSource` SqlDataSource 'a bağlayın.

[GridView ekleme ve SqlDataSource denetimine bağlama ![](querying-data-with-the-sqldatasource-control-cs/_static/image13.gif)](querying-data-with-the-sqldatasource-control-cs/_static/image12.gif)

**Şekil 10**: GridView ekleme ve SqlDataSource denetimine bağlama ([tam boyutlu görüntüyü görüntülemek için tıklayın](querying-data-with-the-sqldatasource-control-cs/_static/image14.gif))

GridView s akıllı etiketindeki aşağı açılan listeden SqlDataSource denetimini seçtikten sonra, Visual Studio veri kaynağı denetimi tarafından döndürülen her sütun için GridView 'a otomatik olarak bir BoundField veya CheckBoxField ekler. SqlDataSource `ProductID`, `ProductName`ve `UnitPrice` üç veritabanı sütunu döndürdüğünden, GridView 'da üç alan vardır.

GridView s üç BoundFields 'i yapılandırmak için bir dakikanızı ayırın. `ProductName` alan s `HeaderText` özelliğini ürün adı ve `UnitPrice` alanı için fiyat olarak değiştirin. Ayrıca `UnitPrice` alanını para birimi olarak biçimlendirin. Bu değişiklikleri yaptıktan sonra, GridView s bildirim temelli işaretlerinizin aşağıdakine benzer şekilde görünmesi gerekir:

[!code-aspx[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample3.aspx)]

Bu sayfayı bir tarayıcı aracılığıyla ziyaret edin. Şekil 11 ' de gösterildiği gibi, GridView her bir ürün `ProductID`, `ProductName`ve `UnitPrice` değerlerini listeler.

[GridView ![her ürün ProductID, ProductName ve BirimFiyat değerlerini görüntüler](querying-data-with-the-sqldatasource-control-cs/_static/image16.gif)](querying-data-with-the-sqldatasource-control-cs/_static/image15.gif)

**Şekil 11**: GridView her bir ürün için `ProductID`, `ProductName`ve `UnitPrice` değerleri görüntüler ([tam boyutlu görüntüyü görüntülemek için tıklayın](querying-data-with-the-sqldatasource-control-cs/_static/image17.gif))

Sayfa ziyaret edildiğinde GridView, veri kaynağı denetim s `Select()` yöntemini çağırır. ObjectDataSource denetimini kullanırken, bu `ProductsBLL` sınıf s `GetProducts()` metodunu çağırdı. Ancak, SqlDataSource ile `Select()` yöntemi belirtilen veritabanıyla bir bağlantı kurar ve `SelectCommand` (`SELECT [ProductID], [ProductName], [UnitPrice] FROM [Products]`, bu örnekte) yayınlar. SqlDataSource, GridView 'un, döndürülen her veritabanı kaydı için GridView 'da bir satır oluşturan sonuçlarını getirir.

## <a name="the-built-in-data-web-control-features-and-the-sqldatasource-control"></a>Yerleşik veri Web denetimi özellikleri ve SqlDataSource denetimi

Genel olarak, veri Web 'e ait özellikler, sayfalama, sıralama, Düzenle, silme, ekleme, vb. veri Web denetimine özgüdür ve kullanılan veri kaynağı denetimine bağlı değildir. Diğer bir deyişle, GridView, yerleşik sayfalama, sıralama, düzen ve silmeyi bir ObjectDataSource veya SqlDataSource 'a bağlanıp bağlanmadığını kullanabilir. Ancak, belirli veri Web denetimi özellikleri kullanılan veri kaynağı denetimiyle veya veri kaynağı denetimi s yapılandırmasına duyarlıdır.

Örneğin, [büyük miktarlarda veri öğreticisi aracılığıyla verimli bir şekilde sayfalamakta](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs.md) , varsayılan olarak, veri Web denetimlerine ait sayfalama mantığı, temel alınan veri kaynağından *Tüm* kayıtları döndürmektedir ve ardından yalnızca geçerli sayfa dizini ve sayfa başına görüntülenecek kayıt sayısı için uygun kayıt alt kümesini görüntüler. Bu model yeterince büyük sonuç kümeleriyle sayfalama yaparken oldukça verimsiz olur. Neyse ki, ObjectDataSource, yalnızca görüntülenecek kayıtların kesin alt kümesini döndüren özel sayfalama 'yı destekleyecek şekilde yapılandırılabilir. Ancak, SqlDataSource denetimi özel sayfalama uygulamaya yönelik özellikler eksiktir.

SqlDataSource ile sayfalama ve sıralama ile başka bir alt ttity. Varsayılan olarak, bir SqlDataSource 'tan döndürülen veriler disk belleğine alınabilir veya GridView aracılığıyla sıralanabilir. Bunu göstermek için, `Querying.aspx` ' deki GridView s akıllı etiketinde sayfalama etkinleştir ve sıralama seçeneklerini etkinleştir ' i işaretleyin ve bunun beklendiği gibi çalıştığını doğrulayın.

Sıralama ve sayfalama, SqlDataSource veritabanı verilerini gevşek yazılmış bir veri kümesine alcağından kullanılır. Sorgu tarafından döndürülen kayıtların toplam sayısı, veri kümesinden bunun olabilir. Ayrıca, DataSet s sonuçları bir DataView aracılığıyla sıralanabilir. Bu yetenekler, GridView tarafından disk belleğine veya sıralanmış verileri istediğinde SqlDataSource tarafından otomatik olarak kullanılır.

SqlDataSource, [`DataSourceMode` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.datasourcemode.aspx) `DataSet` (varsayılan) `DataReader`olarak değiştirerek veri kümesi yerine bir DataReader döndürecek şekilde yapılandırılabilir. Bir DataReader kullanmak, SqlDataSource 'un sonuçları bir DataReader bekleyen mevcut koda geçirirken durumlarda tercih edilebilir. Ayrıca, DataReaders, veri kümelerinden önemli ölçüde daha basit nesneler olduğundan, daha iyi performans sunar. Ancak bu değişikliği yaparsanız, SqlDataSource, sorgu tarafından kaç kayıt yapıldığını belirlemediğinden veya DataReader döndürülen verileri sıralamak için herhangi bir teknik sunduğundan, veri Web denetimi ne sıralama ne de sayfa değildir.

## <a name="step-4-using-a-custom-sql-statement-or-stored-procedure"></a>4\. Adım: özel bir SQL Ifadesini veya saklı yordamı kullanma

SqlDataSource denetimini yapılandırırken, verileri döndürmek için kullanılan sorgu, özel bir SQL ifadesiyle veya saklı yordamda ya da varolan bir tablo ya da görünümden sütunlar olarak iki yaklaşımdan birinde belirtilebilir. 2\. adımda `Products` tablosundan sütunları seçmeyi inceledik. Özel bir SQL ifadesini kullanarak bakalım.

`Querying.aspx` sayfasına başka bir GridView denetimi ekleyin ve akıllı etiketteki açılan listeden yeni bir veri kaynağı oluşturmayı seçin. Sonra, verilerin bir veritabanından çekileceğini, bu yeni bir SqlDataSource denetimi oluşturulacağını gösterir. Denetim `ProductsWithCategoryInfoDataSource`adlandırın.

![Productswithcategorınfodatasource adlı yeni bir SqlDataSource denetimi oluşturun](querying-data-with-the-sqldatasource-control-cs/_static/image18.gif)

**Şekil 12**: `ProductsWithCategoryInfoDataSource` adlı yeni bir SqlDataSource denetimi oluşturma

Sonraki ekranda veritabanını belirtmemizi ister. Şekil 7 ' ye geri döndüğünüzde, açılan listeden `NORTHWINDConnectionString` seçin ve Ileri ' ye tıklayın. Select Ifadesini Yapılandır ekranında, özel bir SQL ifadesini veya saklı yordamı belirtin radyo düğmesini seçin ve Ileri ' ye tıklayın. Bu, SELECT, UPDATE, INSERT ve DELETE etiketli sekmeler sunan özel deyimler veya saklı yordamlar tanımla ekranını getirir. Her sekmede, metin kutusuna özel bir SQL ifadesini girebilir veya açılan listeden bir saklı yordam seçebilirsiniz. Bu öğreticide, özel bir SQL bildirisini girmeye bakacağız; sonraki öğreticide, saklı yordam kullanan bir örnek yer alır.

![Özel bir SQL Ifadesini girin veya saklı yordam seçin](querying-data-with-the-sqldatasource-control-cs/_static/image19.gif)

**Şekil 13**: özel bir SQL ifadesini girin veya saklı yordam seçin

Özel SQL deyimleri metin kutusuna el ile girilebilir veya Sorgu Tasarımcısı düğmesine tıklanarak grafiksel olarak oluşturulabilir. Sorgu Tasarımcısı veya metin kutusundan, `JOIN` tablosundan ürün s `CategoryName` almak için `Categories` kullanarak `Products` tablosundan `ProductID` ve `ProductName` alanları döndürmek için aşağıdaki sorguyu kullanın:

[!code-sql[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample4.sql)]

![Sorgu Tasarımcısı kullanarak sorguyu grafiksel olarak oluşturabilirsiniz](querying-data-with-the-sqldatasource-control-cs/_static/image20.gif)

**Şekil 14**: Sorgu Tasarımcısı kullanarak sorguyu grafik olarak oluşturabilirsiniz

Sorguyu belirttikten sonra, test sorgu ekranına ilerlemek için Ileri ' ye tıklayın. SqlDataSource sihirbazını gerçekleştirmek için son ' a tıklayın.

Sihirbazı tamamladıktan sonra GridView 'un, sorgudan döndürülen `ProductID`, `ProductName`ve `CategoryName` sütunları görüntüleyerek üç BoundFields eklenir ve aşağıdaki bildirime dayalı biçimlendirme elde edilir:

[!code-aspx[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample5.aspx)]

[GridView ![her ürün KIMLIĞI, adı ve Ilişkili kategori adını gösterir](querying-data-with-the-sqldatasource-control-cs/_static/image22.gif)](querying-data-with-the-sqldatasource-control-cs/_static/image21.gif)

**Şekil 15**: GridView her ürün kimliği, adı ve Ilişkili kategori adını gösterir ([tam boyutlu görüntüyü görüntülemek için tıklayın](querying-data-with-the-sqldatasource-control-cs/_static/image23.gif))

## <a name="summary"></a>Özet

Bu öğreticide, SqlDataSource denetimini kullanarak verileri sorgulama ve görüntüleme hakkında gördük. ObjectDataSource gibi, SqlDataSource bir proxy görevi görür ve verilere erişmek için bildirim temelli bir yaklaşım sağlar. Özellikleri bağlanılacak veritabanını ve yürütülecek SQL `SELECT` sorgusunu belirtir; Özellikler penceresi veya veri kaynağı Yapılandırma Sihirbazı kullanılarak belirtilebilir.

Bu öğreticide incelenen `SELECT` sorgu örnekleri, belirtilen sorgudaki tüm kayıtları döndürdü. Ancak, SqlDataSource denetimi, değerleri programlı olarak atanan veya belirtilen bir kaynaktan otomatik olarak çekilen parametrelere sahip bir `WHERE` yan tümcesi içerebilir. Sonraki öğreticide parametreli sorgular oluşturmayı ve kullanmayı inceleyeceğiz!

Programlamanın kutlu olsun!

## <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Ilişkisel veritabanı verilerine erişme](http://aspnet.4guysfromrolla.com/articles/022206-1.aspx)
- [SqlDataSource denetimine genel bakış](https://msdn.microsoft.com/library/dz12d98w.aspx)
- [ASP.NET hızlı başlangıç öğreticileri: SqlDataSource denetimi](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/data/sqldatasource.aspx)
- [Web. config `<connectionStrings>` öğesi](https://msdn.microsoft.com/library/bf7sd233.aspx)
- [Veritabanı bağlantı dizesi başvurusu](http://www.connectionstrings.com/)

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide müşteri adayı gözden geçirenler, Çiğdem Connery, Bernadette Leigh ve David suru. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Next](using-parameterized-queries-with-the-sqldatasource-cs.md)
