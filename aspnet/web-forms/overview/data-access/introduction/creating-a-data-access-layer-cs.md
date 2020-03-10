---
uid: web-forms/overview/data-access/introduction/creating-a-data-access-layer-cs
title: Veri erişim katmanı oluşturma (C#) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, bir veritabanındaki bilgilere erişmek için çok baştan başlayıp, yazılan veri kümelerini kullanarak veri erişim katmanını (DAL) oluşturacağız.
ms.author: riande
ms.date: 04/05/2010
ms.assetid: cfe2a6a0-1e56-4dc8-9537-c8ec76ba96a4
msc.legacyurl: /web-forms/overview/data-access/introduction/creating-a-data-access-layer-cs
msc.type: authoredcontent
ms.openlocfilehash: 5aaf97dc8448dcb7b94ef2e4e23f34fd37ac4426
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78605044"
---
# <a name="creating-a-data-access-layer-c"></a>Veri Erişim Katmanını Oluşturma (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[PDF 'YI indir](creating-a-data-access-layer-cs/_static/datatutorial01cs1.pdf)

> Bu öğreticide, bir veritabanındaki bilgilere erişmek için çok baştan başlayıp, yazılan veri kümelerini kullanarak veri erişim katmanını (DAL) oluşturacağız.

## <a name="introduction"></a>Giriş

Web geliştiricileri olarak, yaşamımız verilerle çalışmaya yakın bir şekilde çalışır. Verileri depolamak için veritabanları, bu dosyayı alma ve değiştirme kodu ve toplanacak ve özetlenecek Web sayfaları oluşturacağız. Bu, ASP.NET 2,0 ' de bu ortak desenleri uygulama tekniklerini keşfedebilir, uzun bir serinin ilk öğreticisidir. Yazılan veri kümelerini kullanarak bir veri erişim katmanından (DAL) oluşan bir [yazılım mimarisi](http://en.wikipedia.org/wiki/Software_architecture) , özel iş kurallarını zorlayan bir Iş mantığı katmanı (BLL) ve ortak bir sayfa düzeni paylaşan ASP.net sayfalarından oluşan bir sunum katmanı oluşturmaya başlayacağız. Bu arka uç groundçalışma oluşturulduktan sonra, bir Web uygulamasındaki verileri görüntüleme, özetleme, toplama ve doğrulama işlemlerinin nasıl yapılacağını gösteren raporlamaya geçeceğiz. Bu öğreticilerin kısa olması ve işlem boyunca görsel olarak size yol göstermek için çok sayıda ekran görüntüsü ile adım adım yönergeler sağlaması gerekir. Her öğretici, C# ve Visual Basic sürümlerde mevcuttur ve kullanılan kodun tamamını karşıdan yükleme içerir. (Bu ilk öğretici oldukça uzun, ancak Rest çok daha fazla digestible öbekte sunulmuştur.)

Bu öğreticiler için **uygulama\_veri** dizinine yerleştirilmiş Northwind veritabanının Microsoft SQL Server 2005 Express Edition sürümünü kullanacağız. Veritabanı dosyasına ek olarak, **uygulama\_veri** klasörü, farklı bir veritabanı sürümü kullanmak istemeniz durumunda veritabanını oluşturmak için SQL komut dosyalarını da içerir. Bu betikler, tercih ediyorsanız [doğrudan Microsoft 'tan da indirilebilir](https://www.microsoft.com/downloads/details.aspx?FamilyID=06616212-0356-46a0-8da2-eebc53a68034&amp;DisplayLang=en). Northwind veritabanının farklı bir SQL Server sürümünü kullanırsanız, uygulamanın **Web. config** dosyasındaki **Kuzey wndconnectionstring** ayarını güncelleştirmeniz gerekecektir. Web uygulaması, dosya sistemi tabanlı bir Web sitesi projesi olarak Visual Studio 2005 Professional Edition kullanılarak oluşturulmuştur. Ancak, tüm öğreticiler Visual Studio 2005, [Visual Web Developer](https://msdn.microsoft.com/vstudio/express/vwd/)'ın ücretsiz sürümüyle eşit bir şekilde çalışacaktır.  
  
Bu öğreticide, en baştan başlayacağız ve veri erişim katmanını (DAL) oluşturacak ve ikinci öğreticide Iş mantığı katmanını (BLL) oluşturarak ve sayfa düzeninde ve üçüncü katmandaki gezinmede çalışmaya başlayacağız. Üçüncü bir sürüm ile sonraki öğreticiler, birinci üçünde yer alan temel üzerinde oluşturulur. Bu ilk öğreticide yer almak için çok fazla sunuyoruz ve Visual Studio 'Yu kullanmaya başlayın!

## <a name="step-1-creating-a-web-project-and-connecting-to-the-database"></a>1\. Adım: Web projesi oluşturma ve veritabanına bağlanma

Veri erişim katmanımızı (DAL) oluşturabilmeniz için önce bir Web sitesi oluşturmanız ve veritabanınızı ayarlamanız gerekir. Yeni bir dosya sistemi tabanlı ASP.NET Web sitesi oluşturarak başlayın. Bunu gerçekleştirmek için Dosya menüsüne gidin ve yeni Web sitesi ' ni seçerek yeni Web sitesi iletişim kutusunu görüntüler. ASP.NET Web sitesi şablonunu seçin, konum açılan listesini dosya sistemi olarak ayarlayın, Web sitesini yerleştirmek için bir klasör seçin ve dili olarak C#ayarlayın.

[![yeni bir dosya sistemi tabanlı Web sitesi oluşturma](creating-a-data-access-layer-cs/_static/image2.png)](creating-a-data-access-layer-cs/_static/image1.png)

**Şekil 1**: yeni bir dosya sistemi tabanlı Web sitesi oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image3.png))

Bu, **default. aspx** ASP.NET sayfası ve bir **App\_veri** klasörüyle yeni bir Web sitesi oluşturur.

Web sitesi oluşturulduğunda, sonraki adım Visual Studio 'nun Sunucu Gezgini veritabanına bir başvuru eklemektir. Sunucu Gezgini bir veritabanı ekleyerek, Visual Studio içinden tabloları, saklı yordamları, görünümleri ve benzeri işlemleri ekleyebilirsiniz. Ayrıca, Sorgu Tasarımcısı aracılığıyla tablo verilerini görüntüleyebilir veya kendi sorgularınızı oluşturabilirsiniz. Ayrıca, DAL için yazılan veri kümelerini oluşturduğumuz zaman, Visual Studio 'Nun yazılan veri kümelerinin oluşturulması gereken veritabanına işaret etmesi gerekir. Bu bağlantı bilgilerini zaman içinde sağlayabilmemiz için, Visual Studio Sunucu Gezgini zaten kayıtlı olan veritabanlarının açılan listesini otomatik olarak doldurur.

Sunucu Gezgini Northwind veritabanını ekleme adımları, **uygulama\_veri** klasöründe SQL Server 2005 Express sürüm veritabanını kullanmak istediğinize veya bunun yerine kullanmak istediğiniz Microsoft SQL Server 2000 ya da 2005 veritabanı sunucu kurulumuna sahip olup olmadığına bağlıdır.

## <a name="using-a-database-in-the-app_data-folder"></a>App\_Data klasöründeki bir veritabanını kullanma

Bağlanmak için bir SQL Server 2000 veya 2005 veritabanı sunucusu yoksa veya veritabanını bir veritabanı sunucusuna ekleme zorunluluğunu önlemek istiyorsanız, indirilen Web sitesinin **uygulama\_verileri** klasöründe bulunan Northwind veritabanının SQL Server 2005 Express sürüm sürümünü kullanabilirsiniz (**Kuzey WND. MDF**).

**App\_veri** klasörüne yerleştirilmiş bir veritabanı Sunucu Gezgini otomatik olarak eklenir. Makinenizde SQL Server 2005 Express Sürüm yüklü olduğunu varsayarsak, kuzeydoğu adlı bir düğüm görmeniz gerekir. Sunucu Gezgini, tabloları, görünümleri, saklı yordamını ve benzerlerini genişletebileceğiniz ve keşfedebilir (bkz. Şekil 2).

**Uygulama\_veri** klasörü, Microsoft Access **. mdb** dosyalarını da barındırabilir ve bu da SQL Server karşılıkları gibi Sunucu Gezgini otomatik olarak eklenir. SQL Server seçeneklerinden birini kullanmak istemiyorsanız, her zaman [Northwind veritabanı dosyasının Microsoft Access sürümünü indirebilir](https://www.microsoft.com/downloads/details.aspx?FamilyID=C6661372-8DBE-422B-8676-C632D66C529C&amp;displaylang=EN) ve **uygulama\_veri** dizinine bırakabilirsiniz. Ancak, Access veritabanlarının SQL Server olarak Özellik zengin olmadığı ve Web sitesi senaryolarında kullanılmak üzere tasarlanmadığı göz önünde bulundurun. Ayrıca, 35 ' in birkaç öğreticimiz, erişim tarafından desteklenmeyen belirli veritabanı düzeyi özellikleri kullanır.

## <a name="connecting-to-the-database-in-a-microsoft-sql-server-2000-or-2005-database-server"></a>Microsoft SQL Server 2000 veya 2005 veritabanı sunucusunda veritabanına bağlanma

Alternatif olarak, bir veritabanı sunucusunda yüklü olan Northwind veritabanına bağlanabilirsiniz. Veritabanı sunucusunda zaten Northwind veritabanı yüklü değilse, önce Bu öğreticinin indirileceği yükleme betiğini çalıştırarak veya [Northwind ve Installation script SQL Server 2000 sürümünü](https://www.microsoft.com/downloads/details.aspx?FamilyID=06616212-0356-46a0-8da2-eebc53a68034&amp;DisplayLang=en) doğrudan Microsoft 'un web sitesinden indirerek veritabanı sunucusuna eklemeniz gerekir.

Veritabanını yükledikten sonra, Visual Studio 'daki Sunucu Gezgini gidin, veri bağlantıları düğümüne sağ tıklayın ve bağlantı Ekle ' yi seçin. Sunucu Gezgini görmüyorsanız, görünüme/Sunucu Gezgini gidin veya CTRL + ALT + S tuşlarına basın. Bu işlem, bağlanılacak sunucuyu, kimlik doğrulama bilgilerini ve veritabanı adını belirtebileceğiniz bağlantı Ekle iletişim kutusunu getirir. Veritabanı bağlantı bilgilerini başarıyla yapılandırdıktan ve Tamam düğmesine tıkladıktan sonra, veritabanı veri bağlantıları düğümünün altına bir düğüm olarak eklenecektir. Tabloları, görünümleri, saklı yordamlarını ve benzerlerini araştırmak için veritabanı düğümünü genişletebilirsiniz.

![Veritabanı sunucunuzun Northwind veritabanına bir bağlantı ekleyin](creating-a-data-access-layer-cs/_static/image4.png)

**Şekil 2**: veritabanı sunucunuzun Northwind veritabanına bağlantı ekleme

## <a name="step-2-creating-the-data-access-layer"></a>2\. Adım: veri erişim katmanını oluşturma

Verilerle çalışırken, verilere özgü mantığı doğrudan sunu katmanına (bir Web uygulamasında, ASP.NET sayfaları ise sunu katmanını yapar) katıştırmanız gerekir. Bu, ASP.NET sayfasının kod bölümünde ADO.NET kodu yazma veya biçimlendirme bölümünün SqlDataSource denetimini kullanma biçimini alabilir. Her iki durumda da bu yaklaşım, veri erişim mantığını sunum katmanıyla sıkı bir şekilde bağar. Ancak önerilen yaklaşım, veri erişim mantığını sunum katmanından ayıramaktır. Bu ayrı katmana veri erişim katmanı, kısa için DAL adı verilir ve genellikle ayrı bir sınıf kitaplığı projesi olarak uygulanır. Bu katmanlı mimarinin avantajları iyi belgelenmiştir (Bu avantajlar hakkında bilgi edinmek için Bu öğreticinin sonundaki "daha fazla okuma" bölümüne bakın) ve bu seride gerçekleştirilecek yaklaşım vardır.

Veritabanına bağlantı oluşturma, **seçme**, **ekleme**, **güncelleştirme**ve **silme** komutlarını verme gibi temel veri KAYNAĞıNA özgü tüm kod ve bu nedenle, dal içinde bulunmalıdır. Sunu katmanı, bu tür veri erişim koduna herhangi bir başvuru içermemelidir, ancak bunun yerine her türlü veri isteği için DAL çağrısı yapmamalıdır. Veri erişimi katmanları genellikle temel alınan veritabanı verilerine erişim yöntemlerini içerir. Örneğin, Northwind veritabanı, satışı için ürünleri ve ait oldukları kategorileri kaydeden **Ürünler** ve **Kategoriler** tabloları içerir. Bu şekilde, şu gibi yöntemlere sahip olduğumuz:

- Tüm Kategoriler hakkındaki bilgileri döndüren **GetCategories ()**
- Tüm ürünlerle ilgili bilgileri döndüren **GetProducts ()**
- Belirtilen kategoriye ait tüm ürünleri döndüren **Getproductsbycategoryıd (*CategoryID*)**
- **GetProductByProductID (*ProductID*)** , belirli bir ürünle ilgili bilgileri döndürecek

Çağrıldığında, bu yöntemler veritabanına bağlanır, uygun sorguyu verir ve sonuçları döndürür. Bu sonuçların nasıl döndürültiğimiz önemlidir. Bu yöntemler veritabanı sorgusu tarafından doldurulan bir veri kümesi veya DataReader döndürebilir, ancak ideal olarak *belirlenmiş nesneler*kullanılarak bu sonuçların döndürülmesi önerilir. Türü kesin belirlenmiş bir nesne, derleme zamanında rigidly tanımlanmış olan bir nesnedir, ancak gevşek olarak yazılmış bir nesne, bir şema çalışma zamanına kadar bilinmez.

Örneğin, DataReader ve veri kümesi (varsayılan olarak), şemaları doldurmak için kullanılan veritabanı sorgusunun döndürdüğü sütunlar tarafından tanımlandığından, gevşek olarak yazılmış nesnelerdir. Gevşek yazılmış bir DataTable nesnesinden belirli bir sütuna erişmek için şu sözdizimini kullanmanız gerekir:  <strong><em>DataTable</em>. Satırlar [<em>Dizin</em>] ["<em>sütunadı</em>"]</strong>. DataTable 'ın bu örnekteki gevşek olarak yazılması, bir dize veya sıralı dizin kullanarak sütun adına erişmesi gereken olgu tarafından belirlenir. Kesin türü belirtilmiş bir DataTable, diğer taraftan, sütunlarının her birini özellik olarak uygulanmış olacaktır, bu da şunun gibi görünen kod ile sonuçlanır:  <strong><em>DataTable</em>. Satırlar [<em>Dizin</em>]. *ColumnName</strong>* .

Kesin tür belirtilmiş nesneleri döndürmek için, geliştiriciler kendi özel iş nesnelerini oluşturabilir ya da türü belirlenmiş veri kümelerini kullanabilir. İş nesnesi geliştirici tarafından, özellikleri genellikle iş nesnesinin temsil ettiği temel veritabanı tablosunun sütunlarını yansıtan bir sınıf olarak uygulanır. Türü belirtilmiş veri kümesi, Visual Studio tarafından bir veritabanı şemasına göre oluşturulan ve üyeleri bu şemaya göre kesin olarak yazılan bir sınıftır. Türü belirtilmiş veri kümesi, ADO.NET DataSet, DataTable ve DataRow sınıflarını genişleten sınıflardan oluşur. Türü kesin belirlenmiş DataTable 'a ek olarak, yazılan veri kümeleri artık DataSet 'in DataTable 'ları dolduruluyor ve DataTable içindeki değişiklikleri veritabanına geri yaymaya yönelik yöntemlere sahip olan TableAdapters de içerir.

> [!NOTE]
> Türü belirtilmiş veri kümeleri ve özel iş nesneleri kullanmanın avantajları ve dezavantajları hakkında daha fazla bilgi için, [veri katmanı bileşenleri tasarlama ve katmanlar aracılığıyla veri geçirme](https://msdn.microsoft.com/library/ms978496.aspx)konusuna bakın.

Bu öğreticiler mimarisi için kesin türü belirtilmiş veri kümeleri kullanacağız. Şekil 3 ' te, yazılan veri kümelerini kullanan bir uygulamanın farklı katmanları arasındaki iş akışı gösterilmektedir.

[![tüm veri erişim kodu DAL için yeniden dağıtılır](creating-a-data-access-layer-cs/_static/image6.png)](creating-a-data-access-layer-cs/_static/image5.png)

**Şekil 3**: tüm veri ERIŞIM kodu dal için yeniden dağıtılır ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image7.png))

## <a name="creating-a-typed-dataset-and-table-adapter"></a>Türü belirtilmiş veri kümesi ve tablo bağdaştırıcısı oluşturma

DAL oluşturmaya başlamak için, projemizi belirlenmiş bir veri kümesi ekleyerek başladık. Bunu gerçekleştirmek için Çözüm Gezgini proje düğümüne sağ tıklayın ve yeni öğe Ekle ' yi seçin. Şablon listesinden veri kümesi seçeneğini belirleyin ve **Northwind. xsd**olarak adlandırın.

[![projenize yeni bir veri kümesi eklemeyi seçin](creating-a-data-access-layer-cs/_static/image9.png)](creating-a-data-access-layer-cs/_static/image8.png)

**Şekil 4**: projenize yeni bir veri kümesi eklemeyi seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image10.png))

Ekle ' ye tıkladıktan sonra, veri kümesini **uygulama\_kodu** klasörüne eklemek isteyip Istemediğiniz sorulduğunda Evet ' i seçin. Daha sonra, yazılan veri kümesine ilişkin tasarımcı görüntülenir ve TableAdapter Yapılandırma Sihirbazı başlatılır ve bu işlem, türü belirtilmiş veri kümesine ilk TableAdapter eklemenizi sağlar.

Türü belirtilmiş veri kümesi, kesin türü belirtilmiş bir veri koleksiyonu işlevi görür. her biri türü kesin belirlenmiş DataRow örneklerinden oluşan kesin türü belirtilmiş DataTable örneklerinden oluşur. Bu öğreticiler serisinde birlikte çalışması gereken temel alınan veritabanı tablolarının her biri için kesin olarak yazılmış bir DataTable oluşturacağız. **Products** tablosu Için bir DataTable oluşturmaya başlayalım.

Türü kesin belirlenmiş DataTable 'ın, temel alınan veritabanı tablosundan verilere erişme hakkında herhangi bir bilgi içermediği göz önünde bulundurun. DataTable 'ı doldurmak üzere verileri almak için veri erişim katmanımız olarak işlev gören bir TableAdapter sınıfı kullanırız. **Ürünlerimiz** DataTable 'larımız için TableAdapter, sunum katmanından çağıracağımız **GetProducts ()** , **GetProductByCategoryID (*CategoryID*)** ve bu yöntemleri içerir. DataTable 'ın rolü, katmanlar arasında veri geçirmek için kullanılan türü kesin belirlenmiş nesneler olarak kullanılır.

TableAdapter Yapılandırma Sihirbazı, hangi veritabanının birlikte çalışabileceği seçmenizi isteyerek başlar. Açılan listede bu veritabanları Sunucu Gezgini gösterilmektedir. Northwind veritabanını Sunucu Gezgini eklememediyseniz, şu anda yeni bağlantı düğmesine tıklayabilirsiniz.

[![, açılan listeden Northwind veritabanını seçin](creating-a-data-access-layer-cs/_static/image12.png)](creating-a-data-access-layer-cs/_static/image11.png)

**Şekil 5**: açılan listeden Northwind veritabanını seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image13.png))

Veritabanını seçip Ileri ' ye tıkladıktan sonra, bağlantı dizesini **Web. config** dosyasına kaydetmek isteyip istemediğiniz sorulur. Bağlantı dizesini kaydederek, daha sonra bağlantı dizesi bilgileri değişirse, TableAdapter sınıflarında sabit kodlanmış olmasını önleyin. Bağlantı dizesini yapılandırma dosyasına kaydetmeyi tercih ediyorsanız, gelişmiş güvenlik için [isteğe bağlı olarak şifrelenen](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx) veya daha sonra Yöneticiler için daha Ideal olan IIS GUI yönetici aracında yeni ASP.NET 2,0 özellik sayfası aracılığıyla değiştirilen **&lt;connectionStrings&gt;** bölümüne yerleştirilir.

[![bağlantı dizesini Web. config dosyasına kaydet](creating-a-data-access-layer-cs/_static/image15.png)](creating-a-data-access-layer-cs/_static/image14.png)

**Şekil 6**: bağlantı dizesini **Web. config** dosyasına kaydedin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image16.png))

Daha sonra, kesin olarak belirlenmiş ilk DataTable için şemayı tanımlamanız ve TableAdapter 'ızın kesin türü belirtilmiş veri kümesini doldururken kullanacağı ilk yöntemi sağlaması gerekir. Bu iki adım aynı anda DataTable 'umuza yansıtıldığımız tablodaki sütunları döndüren bir sorgu oluşturularak gerçekleştirilir. Sihirbazın sonunda bu sorguya bir yöntem adı vereceğiz. Bu yöntem alındıktan sonra sunum katmanınızdan çağrılabilir. Yöntemi, tanımlı sorguyu yürütür ve türü kesin belirlenmiş bir DataTable olarak doldurur.

SQL sorgusunu tanımlamaya başlamak için önce TableAdapter 'ın sorguyu nasıl vermesini istediğinizi belirtmemiz gerekir. Geçici bir SQL ifadesini kullanabilir, yeni bir saklı yordam oluşturabilir veya var olan bir saklı yordamı kullanabilirsiniz. Bu öğreticiler için geçici SQL deyimlerini kullanacağız. Bkz. [Brian Noyes](http://briannoyes.net/)'in makalesi, saklı yordamları kullanma örneği Için [Visual Studio 2005 veri kümesi Tasarımcısı Ile veri erişim katmanı oluşturma](http://www.theserverside.net/articles/showarticle.tss?id=DataSetDesigner) .

[![geçici bir SQL Ifadesini kullanarak verileri sorgulama](creating-a-data-access-layer-cs/_static/image18.png)](creating-a-data-access-layer-cs/_static/image17.png)

**Şekil 7**: GEÇICI bir SQL Ifadesini kullanarak verileri sorgulama ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image19.png))

Bu noktada, SQL sorgusunu el ile yazabilirsiniz. TableAdapter içinde ilk yöntemi oluştururken, genellikle sorgunun karşılık gelen DataTable 'da ifade edilmesi gereken sütunları döndürmesini istersiniz. Bunu, **Products** tablosundan tüm sütunları ve tüm satırları döndüren bir sorgu oluşturarak gerçekleştirebiliriz:

[![metin kutusuna SQL sorgusunu girin](creating-a-data-access-layer-cs/_static/image21.png)](creating-a-data-access-layer-cs/_static/image20.png)

**Şekil 8**: metın kutusuna SQL sorgusunu girin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image22.png))

Alternatif olarak, Şekil 9 ' da gösterildiği gibi Sorgu Tasarımcısı kullanın ve sorguyu grafik olarak oluşturun.

[sorgu Düzenleyicisi aracılığıyla sorguyu grafik olarak oluşturma ![](creating-a-data-access-layer-cs/_static/image24.png)](creating-a-data-access-layer-cs/_static/image23.png)

**Şekil 9**: sorgu Düzenleyicisi aracılığıyla sorgu grafiksel olarak oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image25.png))

Sorguyu oluşturduktan sonra, bir sonraki ekrana geçmeden önce Gelişmiş Seçenekler düğmesine tıklayın. Web sitesi projelerinde, "INSERT, Update ve delete deyimlerini oluştur" seçeneği varsayılan olarak seçilen tek gelişmiş seçenektir; Bu Sihirbazı bir sınıf kitaplığından veya bir Windows projesinden çalıştırırsanız, "iyimser eşzamanlılık kullan" seçeneği de işaretlenir. Şimdilik "iyimser eşzamanlılık kullan" seçeneğini işaretsiz bırakın. Gelecekteki öğreticilerde iyimser eşzamanlılık inceleyeceğiz.

[![yalnızca INSERT, Update ve delete deyimlerini oluştur seçeneğini belirleyin](creating-a-data-access-layer-cs/_static/image27.png)](creating-a-data-access-layer-cs/_static/image26.png)

**Şekil 10**: yalnızca INSERT, Update ve delete deyimlerini oluştur seçeneğini belirleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image28.png))

Gelişmiş seçenekleri doğruladıktan sonra, son ekrana ilerlemek için Ileri ' ye tıklayın. Buraya, TableAdapter 'a eklenecek yöntemleri seçmemiz istenir. Veri doldurulmaya yönelik iki desen vardır:

- **DataTable** 'ı bu yaklaşım ile doldur bir yöntem, bir DataTable içinde parametre olarak alan ve sorgunun sonuçlarına göre doldurulur. Örneğin, ADO.NET DataAdapter sınıfı, bu kalıbı **Fill ()** yöntemiyle uygular.
- Bu yaklaşımla **bir DataTable döndürün** yöntemi, DataTable 'ı sizin için oluşturur ve doldurur ve yöntem dönüş değeri olarak döndürür.

TableAdapter 'ın Bu desenlerden birini veya her ikisini birden uygulayabilmeniz gerekir. Burada sunulan yöntemleri de yeniden adlandırabilirsiniz. Her iki onay kutusu da yalnızca bu öğreticiler boyunca yalnızca ikinci kalıbı kullanacağız. Ayrıca, bunun yerine **GetProducts**olarak tercih edilecek genel **GetData** yöntemini yeniden adlandıralım.

İşaretliyse, son onay kutusu "GenerateDBDirectMethods", TableAdapter için **Insert ()** , **Update ()** ve **Delete ()** yöntemlerini oluşturur. Bu seçeneği işaretlenmemiş olarak bırakırsanız, tüm güncelleştirmelerin, türü belirtilmiş veri kümesini, bir DataTable 'ı, tek bir DataRow 'ı veya bir DataRow dizisini alan TableAdapter 'ın tek **Update ()** yöntemi aracılığıyla yapılması gerekir. (Şekil 9 ' da Gelişmiş özelliklerde "INSERT, Update ve delete deyimlerini üret" seçeneğini işaretlemezseniz, bu onay kutusunun ayarı hiçbir etkiye sahip olmayacaktır.) Bu onay kutusunu seçili bırakalım.

[![yöntem adını GetData öğesinden GetProducts olarak değiştirin](creating-a-data-access-layer-cs/_static/image30.png)](creating-a-data-access-layer-cs/_static/image29.png)

**Şekil 11**: **GetData** olan yöntem adını **GetProducts** olarak değiştirin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image31.png))

Son ' a tıklayarak Sihirbazı doldurun. Sihirbaz kapandıktan sonra, yeni oluşturduğumuz DataTable 'ı gösteren veri kümesi tasarımcısına döndürülür. **Ürünler** DataTable 'Daki (**ProductID**, **ProductName**, vb.) sütunların listesini ve **productsTableAdapter** (**Fill ()** ve **GetProducts ()** ) yöntemlerini görebilirsiniz.

[DataTable ve ProductsTableAdapter ürünlerini ![yazılan veri kümesine eklenmiştir](creating-a-data-access-layer-cs/_static/image33.png)](creating-a-data-access-layer-cs/_static/image32.png)

**Şekil 12**: **ürün** tablosu ve **productsTableAdapter** , yazılan veri kümesine eklenmiştir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image34.png))

Bu noktada, bir **GetProducts ()** yöntemiyle tek bir DataTable (**Northwind. Products**) ve kesin türü belirtilmiş bir DataAdapter sınıfı (**NorthwindTableAdapters. productsTableAdapter**) içeren bir veri kümesi var. Bu nesneler, aşağıdaki koddan tüm ürünlerin listesine erişmek için kullanılabilir:

[!code-html[Main](creating-a-data-access-layer-cs/samples/sample1.html)]

Bu kod, bir bit veri erişimine özgü kod yazmamızı gerektirmez. Herhangi bir ADO.NET sınıfını örnekliyoruz, herhangi bir bağlantı dizesine, SQL sorgusuna veya saklı yordamlara başvurmamalıdır. Bunun yerine TableAdapter, bizim için alt düzey veri erişim kodunu sağlar.

Bu örnekte kullanılan her nesne Ayrıca kesin olarak belirlenmiş, Visual Studio 'Nun IntelliSense ve derleme zamanı tür denetimi sağlamasına izin verir. TableAdapter tarafından döndürülen tüm DataTable, GridView, DetailsView, DropDownList, CheckBoxList gibi ASP.NET Data Web denetimlerine bağlanabilir. Aşağıdaki örnek, **GetProducts ()** yöntemi tarafından döndürülen DataTable 'ın, **sayfa\_Load** olay işleyicisi içinde yalnızca scant üç satır kodu içindeki GridView 'a bağlamasını gösterir.

AllProducts.aspx

[!code-aspx[Main](creating-a-data-access-layer-cs/samples/sample2.aspx)]

AllProducts.aspx.cs

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample3.cs)]

[![ürünlerin listesi bir GridView içinde görüntülenir](creating-a-data-access-layer-cs/_static/image36.png)](creating-a-data-access-layer-cs/_static/image35.png)

**Şekil 13**: ürünlerin listesi bir GridView 'da görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image37.png))

Bu örnek, ASP.NET sayfası **sayfa\_yükleme** olay işleyicimize üç satır kod yazmanızı gerektirirken, gelecekteki öğreticilerde, verileri dal içinden bildirimli olarak almak için ObjectDataSource 'un nasıl kullanılacağını inceleyeceğiz. ObjectDataSource ile herhangi bir kod yazmak zorunda olmayacaktır ve sayfalama ve sıralama desteğini de alacak!

## <a name="step-3-adding-parameterized-methods-to-the-data-access-layer"></a>3\. Adım: veri erişim katmanına parametreli Yöntemler Ekleme

Bu noktada, **productsTableAdapter** sınıfımızda, veritabanındaki ürünlerin tümünü döndüren **GetProducts ()** yöntemi vardır. Tüm ürünlerle çalışabilmeniz mümkün olsa da, belirli bir ürün veya belirli bir kategoriye ait olan tüm ürünler hakkında bilgi almak istediğimiz durumlar vardır. Veri erişim katmanımız gibi işlevselliği eklemek için TableAdapter 'a parametreli Yöntemler ekleyebiliriz.

**Getproductsbycategoryıd (*CategoryID*)** yöntemini ekleyelim. DAL 'e yeni bir yöntem eklemek için veri kümesi Tasarımcısına dönün, **productsTableAdapter** bölümüne sağ tıklayın ve sorgu Ekle ' yi seçin.

![TableAdapter 'a sağ tıklayın ve sorgu Ekle ' yi seçin.](creating-a-data-access-layer-cs/_static/image38.png)

**Şekil 14**: TableAdapter 'A sağ tıklayın ve sorgu Ekle ' yi seçin.

İlk olarak, veritabanına geçici bir SQL ifadesini veya yeni veya mevcut bir saklı yordamı kullanarak erişmek isteyip istemediğimiz sorulur. Geçici bir SQL ifadesini yeniden kullanmayı seçelim. Ardından, kullanmak istediğimiz SQL sorgusu türü sorulur. Belirtilen bir kategoriye ait tüm ürünleri döndürmek istediğimize göre, satırları döndüren bir **Select** ifadesini yazmak istiyoruz.

[![satırları döndüren bir SELECT Ifadesinin oluşturulmasını seçin](creating-a-data-access-layer-cs/_static/image40.png)](creating-a-data-access-layer-cs/_static/image39.png)

**Şekil 15**: satırları döndüren bir **Select** ifadesinin oluşturulmasını seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image41.png))

Sonraki adım, verilere erişmek için kullanılan SQL sorgusunu tanımlamaktır. Yalnızca belirli bir kategoriye ait olan ürünleri döndürmek istediğimiz için <strong>GetProducts ()</strong>öğesinden aynı <strong>Select</strong> ifadesini kullanıyorum, ancak şu <strong>WHERE</strong> yan tümcesini ekleyeceğiz: <strong>WHERE CategoryID = @CategoryID</strong>. <strong>@CategoryID</strong> parametresi, bir TableAdapter sihirbazına, oluşturmakta olduğumuz yöntemin ilgili türde (yani, null atanabilir bir tamsayı) bir giriş parametresi gerektirdiğini gösterir.

[![yalnızca belirtilen bir kategorideki ürünlerin döndürülmesi için bir sorgu girin](creating-a-data-access-layer-cs/_static/image43.png)](creating-a-data-access-layer-cs/_static/image42.png)

**Şekil 16**: yalnızca belirtilen bir kategorideki ürünleri döndürmek Için bir sorgu girin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image44.png))

Son adımda, hangi veri erişimi desenlerini kullanacağınızı ve oluşturulan yöntemlerin adlarını özelleştirmenizi seçebiliriz. Fill deseninin adını <strong>Fillbycategoryıd</strong> olarak değiştirelim ve bir DataTable Return deseninin ( <strong>Get*X</strong>*  yöntemleri) döndürdüğü için <strong>getproductsbycategoryıd</strong>kullanalım.

[TableAdapter yöntemlerinin adlarını seçin ![](creating-a-data-access-layer-cs/_static/image46.png)](creating-a-data-access-layer-cs/_static/image45.png)

**Şekil 17**: TableAdapter metotları için adları seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image47.png))

Sihirbazı tamamladıktan sonra, veri kümesi Tasarımcısı yeni TableAdapter yöntemlerini içerir.

![Ürünler artık kategori ile sorgulanabilecek](creating-a-data-access-layer-cs/_static/image48.png)

**Şekil 18**: ürünler artık kategori ile sorgulanabilecek

Aynı tekniği kullanarak bir **GetProductByProductID (*ProductID*)** yöntemi eklemek için bir dakikanızı ayırın.

Bu parametreli sorgular doğrudan veri kümesi tasarımcısından test edilebilir. TableAdapter ' ta yönteme sağ tıklayın ve verileri Önizle ' yi seçin. Ardından, parametreler için kullanılacak değerleri girin ve Önizleme ' ye tıklayın.

[Alkolların kategorisine ait olan ürünler ![gösterilir](creating-a-data-access-layer-cs/_static/image50.png)](creating-a-data-access-layer-cs/_static/image49.png)

**Şekil 19**: Içecek kategorisine ait olan ürünler gösterilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image51.png))

Bu DAL içindeki **Getproductsbycategoryıd (*CategoryID*)** yöntemiyle artık yalnızca belirtilen bir kategorideki ürünleri görüntüleyen bir ASP.NET sayfası oluşturuyoruz. Aşağıdaki örnek, bir **CategoryID** 'si 1 olan alkolın kategorisindeki tüm ürünleri gösterir.

İçecek. asp

[!code-aspx[Main](creating-a-data-access-layer-cs/samples/sample4.aspx)]

Beverages.aspx.cs

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample5.cs)]

[Içecek kategorisindeki Bu ürünler ![görüntülenir](creating-a-data-access-layer-cs/_static/image53.png)](creating-a-data-access-layer-cs/_static/image52.png)

**Şekil 20**: alkoller kategorisindeki Ürünler görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image54.png))

## <a name="step-4-inserting-updating-and-deleting-data"></a>4\. Adım: verileri ekleme, güncelleştirme ve silme

Verileri eklemek, güncelleştirmek ve silmek için yaygın olarak kullanılan iki desen vardır. Veritabanı doğrudan modelini çağıracağımız ilk model, çağrıldığında, tek bir veritabanı kaydında çalışan veritabanında bir **Insert**, **Update**veya **Delete** komutu veren Yöntemler oluşturmayı içerir. Bu tür yöntemler genellikle INSERT, Update veya delete değerlerine karşılık gelen bir dizi skalar değer (tamsayılar, dizeler, Boolean, DateTimes, vb.) dizisine geçirilir. Örneğin, **Products** tablosu için bu düzende, Delete yöntemi, silinecek kaydın **ProductID** 'sini belirten bir Integer parametresi Içinde, Insert yöntemi **ProductName**için bir dize, **UnitPrice**için bir tamsayı, **unitsonstock**için bir tamsayı ve bu şekilde devam eder.

[Her ekleme, güncelleştirme ve silme Isteği veritabanına hemen gönderilir ![](creating-a-data-access-layer-cs/_static/image56.png)](creating-a-data-access-layer-cs/_static/image55.png)

**Şekil 21**: her ekleme, güncelleştirme ve silme Isteği veritabanına hemen gönderilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](creating-a-data-access-layer-cs/_static/image57.png))

Toplu güncelleştirme düzeninde başvurabileceğiniz diğer bir model, bir yöntem çağrısında tüm veri kümesini, DataTable 'ı veya DataRow koleksiyonunu güncelleştirmek olacaktır. Bu düzende bir geliştirici DataTable içindeki DataRow 'ı siler, ekler ve değiştirir ve ardından bu DataRow veya DataTable 'ı bir Update metoduna geçirir. Bu yöntem daha sonra geçirilen DataRow öğesini numaralandırır, değiştirilip değiştirilmediğini, eklendiğini veya silindiğini (DataRow 'ın [RowState özelliği](https://msdn.microsoft.com/library/system.data.datarow.rowstate.aspx) değeri aracılığıyla) belirler ve her kayıt için uygun veritabanı isteğini yayınlar.

[![güncelleştirme yöntemi çağrıldığında tüm değişiklikler veritabanıyla eşitlenir](creating-a-data-access-layer-cs/_static/image59.png)](creating-a-data-access-layer-cs/_static/image58.png)

**Şekil 22**: güncelleştirme yöntemi çağrıldığında tüm değişiklikler veritabanıyla eşitlenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image60.png))

TableAdapter varsayılan olarak Batch güncelleştirme modelini kullanır, ancak VERITABANı doğrudan modelini de destekler. TableAdapter 'umuzu oluştururken gelişmiş özelliklerden "INSERT, Update ve delete deyimlerini üret" seçeneğini belirlediğimiz için, **productsTableAdapter** Batch Update modelini uygulayan bir **Update ()** yöntemi içerir. Özellikle TableAdapter, türü belirtilmiş veri kümesini, türü kesin belirlenmiş bir DataTable 'ı veya bir ya da daha fazla DataRow 'ı geçirilebilecek bir **Update ()** yöntemi içerir. TableAdapter oluştururken "GenerateDBDirectMethods" onay kutusunu işaretlediğinizde, VERITABANı doğrudan deseninin de **Insert ()** , **Update ()** ve **Delete ()** yöntemleri aracılığıyla uygulanması gerekir.

Veri değişikliği desenlerinin her ikisi de, veritabanına **Insert**, **Update**ve **Delete** komutlarını vermek için TableAdapter **InsertCommand**, **UpdateCommand**ve **DeleteCommand** özelliklerini kullanır. Veri kümesi Tasarımcısı ' nda TableAdapter ' a tıklayıp Özellikler penceresi giderek **InsertCommand**, **UpdateCommand**ve **DeleteCommand** özelliklerini inceleyebilir ve değiştirebilirsiniz. (TableAdapter ' ı seçtiğinizden emin olun ve Özellikler penceresi **productsTableAdapter** nesnesinin, açılan listede seçili olduğunu doğrulayın.)

[TableAdapter 'ın InsertCommand, UpdateCommand ve DeleteCommand özelliklerine sahip ![](creating-a-data-access-layer-cs/_static/image62.png)](creating-a-data-access-layer-cs/_static/image61.png)

**Şekil 23**: TableAdapter, **InsertCommand**, **UpdateCommand**ve **DeleteCommand** özelliklerine sahiptir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image63.png))

Bu veritabanı komut özelliklerinden herhangi birini incelemek veya değiştirmek için, Sorgu Tasarımcısı ' yi getirecek **CommandText** alt özelliğine tıklayın.

[Sorgu Tasarımcısı INSERT, UPDATE ve DELETE deyimlerini yapılandırma ![](creating-a-data-access-layer-cs/_static/image65.png)](creating-a-data-access-layer-cs/_static/image64.png)

**Şekil 24**: Sorgu Tasarımcısı **Insert**, **Update**ve **Delete** deyimlerini yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image66.png))

Aşağıdaki kod örneği, toplu güncelleştirme düzeninin, son olmayan ve stokta 25 birime sahip olan tüm ürünlerin fiyatını iki katına eklemek için nasıl kullanılacağını gösterir:

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample6.cs)]

Aşağıdaki kod, belirli bir ürünü programlı olarak silmek, sonra güncelleştirmek ve yeni bir ürün eklemek için DB doğrudan deseninin nasıl kullanılacağını göstermektedir:

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample7.cs)]

## <a name="creating-custom-insert-update-and-delete-methods"></a>Özel ekleme, güncelleştirme ve silme yöntemleri oluşturma

VERITABANı doğrudan yöntemi tarafından oluşturulan **Insert ()** , **Update (** ) ve **Delete (** ) yöntemleri, özellikle birçok sütun içeren tablolar için bir bit, biraz kısası olabilir. Önceki kod örneğine bakıyor, IntelliSense 'in yardımı olmadan, **Update ()** ve **Insert ()** yöntemlerine her giriş parametresine hangi **ürün** tablosu sütununun eşlendiğini özellikle temizlemez. Yalnızca tek bir sütunu veya ikisini de güncelleştirmek istediğimiz veya bir özelleştirilmiş **Insert ()** yöntemi (Belki de yeni eklenen kaydın **kimlik** (otomatik artış) alanının değerini döndürecek şekilde tercih ettiğimiz zamanlar olabilir.

Böyle bir özel yöntem oluşturmak için veri kümesi Tasarımcısına dönün. TableAdapter 'a sağ tıklayın ve TableAdapter sihirbazına dönerek sorgu Ekle ' yi seçin. İkinci ekranda, oluşturulacak sorgunun türünü belirtebiliriz. Yeni bir ürün ekleyen ve sonra yeni eklenen kaydın **ProductID**değerini döndüren bir yöntem oluşturalım. Bu nedenle, bir **Insert** sorgusu oluşturmayı tercih edin.

[![Products tablosuna yeni bir satır eklemek için bir yöntem oluşturma](creating-a-data-access-layer-cs/_static/image68.png)](creating-a-data-access-layer-cs/_static/image67.png)

**Şekil 25**: **Ürünler** tablosuna yeni bir satır eklemek için bir yöntem oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image69.png))

Sonraki ekranda, **InsertCommand**'ın **CommandText** 'i görüntülenir. Sorgunun sonuna **Select SCOPE\_Identity ()** ekleyerek bu sorguyu, aynı kapsamdaki bir **kimlik** sütununa eklenen son kimlik değerini döndürecek şekilde belirleyin. ( **Kapsam\_kimliği ()** hakkında daha fazla bilgi için [teknik belgelere](https://msdn.microsoft.com/library/ms190315.aspx) ve neden büyük OLASıLıKLA [@@IDENTITYyerine kapsam\_kimliği () kullanmak ](http://weblogs.sqlteam.com/travisl/archive/2003/10/29/405.aspx)istediğimize bakın.) **Select** ifadesini eklemeden önce **Insert** ifadesini noktalı virgül ile sonlandırdığınızdan emin olun.

[![SCOPE_IDENTITY () değerini döndürecek şekilde sorguyu artırmak](creating-a-data-access-layer-cs/_static/image71.png)](creating-a-data-access-layer-cs/_static/image70.png)

**Şekil 26**: **kapsam\_Identity ()** değerini döndürecek şekilde sorguyu artırmak ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image72.png))

Son olarak, yeni yöntem **InsertProduct**olarak adlandırın.

[Yeni yöntem adını InsertProduct olarak ayarlamak ![](creating-a-data-access-layer-cs/_static/image74.png)](creating-a-data-access-layer-cs/_static/image73.png)

**Şekil 27**: yeni yöntem adını **InsertProduct** olarak ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image75.png))

Veri kümesi tasarımcısına geri döndüğünüzde, **productsTableAdapter** 'ın **InsertProduct**yeni bir yöntemi içerdiğini görürsünüz. Bu yeni yöntemin **Products** tablosundaki her sütun için bir parametresi yoksa, **Insert** ifadesini noktalı virgül ile sonlandırmayı unutmanız gerekir. **InsertProduct** yöntemini yapılandırın ve **Insert** ve **Select** deyimlerini sınırlayan noktalı virgülle ayırın.

Varsayılan olarak, ekleme yöntemleri sorgu dışı Yöntemler vererek etkilenen satırların sayısını döndürtikleri anlamına gelir. Ancak, **InsertProduct** yönteminin, etkilenen satır sayısı değil, sorgu tarafından döndürülen değeri döndürmesini istiyoruz. Bunu gerçekleştirmek için, **InsertProduct** yönteminin **Executemode** özelliğini **skaler**olarak ayarlayın.

[![ExecuteMode özelliğini skaler olarak değiştirme](creating-a-data-access-layer-cs/_static/image77.png)](creating-a-data-access-layer-cs/_static/image76.png)

**Şekil 28**: **Executemode** özelliğini **skaler** olarak değiştirin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image78.png))

Aşağıdaki kod bu yeni **InsertProduct** metodunu eylemde gösterir:

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample8.cs)]

## <a name="step-5-completing-the-data-access-layer"></a>5\. Adım: veri erişim katmanını tamamlama

**ProductsTableAdapters** sınıfının, **Products** tablosundan **KategoriNo** ve **TedarikçiNo** değerlerini döndürdüğünü, ancak bunlar büyük olasılıkla ürün bilgilerini gösterirken bu sütunların görüntülenmesini Istiyoruz. Bunlar muhtemelen, tedarikçiler tablosundan **CategoryName** sütununu veya **Suppliers** tablosundan **CompanyName** sütununu bulundurmadığını unutmayın. Bu yeni **sütunları da içerecek** şekilde, tam olarak yazılmış DataTable ' ı güncelleştirecek olan TableAdapter ve **CompanyName** sütun değerlerini dahil etmek için TableAdapter 'ın ilk yöntemini **()** kullanabilirsiniz.

Bu, bir sorun oluşturabilir, ancak TableAdapter 'ın veri ekleme, güncelleştirme ve silme yöntemleri bu başlangıç yöntemine göre yapılır. Neyse ki, ekleme, güncelleştirme ve silme için otomatik olarak oluşturulan Yöntemler **Select** yan tümcesindeki alt sorgularda etkilenmez. Sorguları **kategorilere** ve **tedarikçilere** , **birleştirmek** yerine alt sorgular olarak eklemek için bu yöntemleri veri değiştirme yöntemlerine engel olmamız gerekir. **ProductsTableAdapter** Içindeki **GetProducts ()** yöntemine sağ tıklayın ve Yapılandır ' ı seçin. Sonra, **Select** yan tümcesini şöyle olacak şekilde ayarlayın:

[!code-sql[Main](creating-a-data-access-layer-cs/samples/sample9.sql)]

[GetProducts () yöntemi için SELECT Ifadesini güncelleştirme ![](creating-a-data-access-layer-cs/_static/image80.png)](creating-a-data-access-layer-cs/_static/image79.png)

**Şekil 29**: **GetProducts ()** yöntemi için **Select** ifadesini güncelleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image81.png))

Bu yeni sorguyu kullanmak için **GetProducts ()** yöntemini güncelleştirdikten sonra DataTable iki yeni sütun Içerir: **CategoryName** ve **SupplierName**.

![Products DataTable 'ın Iki yeni sütunu vardır](creating-a-data-access-layer-cs/_static/image82.png)

**Şekil 30**: **Products** DataTable 'ın iki yeni sütunu vardır

**Getproductsbycategoryıd (*CategoryID*)** yönteminde **Select** yan tümcesini de güncellemek için bir dakikanızı ayırın.

**GetProducts ()** öğesini güncelleştirirseniz **ekleme sözdizimini kullanma** **seçeneğini belirlerseniz** veri kümesi Tasarımcısı, veritabanı verilerini ekleme, güncelleştirme ve silme yöntemlerini DB doğrudan düzeniyle otomatik olarak oluşturamayacak. Bunun yerine, bu öğreticide daha önce **InsertProduct** yöntemiyle yaptığımız gibi bunları el ile oluşturmanız gerekir. Ayrıca, Batch güncelleştirme modelini kullanmak istiyorsanız **InsertCommand**, **UpdateCommand**ve **DeleteCommand** özellik değerlerini el ile sağlamanız gerekir.

## <a name="adding-the-remaining-tableadapters"></a>Kalan TableAdapters ekleme

Şimdi tek bir veritabanı tablosu için tek bir TableAdapter ile çalışmaya bakıyoruz. Bununla birlikte, Northwind veritabanı Web uygulamamızda ile birlikte çalışmak için gereken birkaç ilgili tablo içerir. Türü belirtilmiş bir veri kümesi birden çok, ilgili DataTable içerebilir. Bu nedenle, DAL olarak bu öğreticilerde kullanacağımız diğer tablolar için DataTable eklememiz gerekiyor. Türü belirtilmiş bir veri kümesine yeni bir TableAdapter eklemek için veri kümesi tasarımcısını açın, tasarımcıya sağ tıklayın ve Ekle/TableAdapter ' ı seçin. Bu, yeni bir DataTable ve TableAdapter oluşturur ve bu öğreticide daha önce incelendiğimiz sihirbazda size kılavuzluk eder.

Aşağıdaki sorguları kullanarak aşağıdaki TableAdapters ve yöntemleri oluşturmak için birkaç dakikanızı alın. **ProductsTableAdapter** içindeki sorguların her bir ürünün kategori ve Tedarikçi adlarını almak için alt sorguları içerdiğine unutmayın. Bunlara ek olarak, aşağıdaki gibi, **productsTableAdapter** sınıfının **GetProducts ()** ve **Getproductsbycategoryıd (*CategoryID*)** yöntemlerini zaten eklemiş oldunuz.

- **ProductsTableAdapter**

  - **GetProducts**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample10.sql)]
  - **Getproductsbycategoryıd**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample11.sql)]
  - **Getproductsbysupplierıd**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample12.sql)]
  - **GetProductByProductID**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample13.sql)]
- **CategoriesTableAdapter**

  - **GetCategories**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample14.sql)]
  - **Getcategorybycategoryıd**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample15.sql)]
- **SuppliersTableAdapter**

  - **Getsuppliers**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample16.sql)]
  - **GetSuppliersByCountry**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample17.sql)]
  - **Getsupplierbysupplierıd**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample18.sql)]
- **EmployeesTableAdapter**

  - **GetEmployees**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample19.sql)]
  - **GetEmployeesByManager**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample20.sql)]
  - **GetEmployeeByEmployeeID**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample21.sql)]

[Dört TableAdapters eklendikten sonra veri kümesi tasarımcısını ![](creating-a-data-access-layer-cs/_static/image84.png)](creating-a-data-access-layer-cs/_static/image83.png)

**Şekil 31**: dört TableAdapters sonra veri kümesi Tasarımcısı ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image85.png))

## <a name="adding-custom-code-to-the-dal"></a>DAL için özel kod ekleme

Türü belirtilmiş veri kümesine eklenen TableAdapters ve DataTable, bir XML şema tanımı dosyası (**Northwind. xsd**) olarak ifade edilir. Bu şema bilgilerini, Çözüm Gezgini **Northwind. xsd** dosyasına sağ tıklayıp kodu görüntüle ' yi seçerek görüntüleyebilirsiniz.

[Northwintürü belirtilmiş veri kümesinin XML şema tanımı (XSD) dosyası ![](creating-a-data-access-layer-cs/_static/image87.png)](creating-a-data-access-layer-cs/_static/image86.png)

**Şekil 32**: Northwinds türünde VERI kümesinin XML şema tanımı (xsd) dosyası ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image88.png))

Bu şema bilgileri C# , derleme zamanında derlendiğinde veya çalışma zamanında (gerekliyse) kodu Visual Basic dönüştürülür. bu noktada, hata ayıklayıcıyla adım adım ilerlenebilir. Otomatik olarak oluşturulan bu kodu görüntülemek için Sınıf Görünümü gidin ve TableAdapter veya Typed DataSet sınıflarının detayına gidin. Ekranınızda Sınıf Görünümü görmüyorsanız, Görünüm menüsüne gidin ve buradan seçin ya da CTRL + SHIFT + C tuşlarına basın. Sınıf Görünümü, yazılan veri kümesinin ve TableAdapter sınıflarının özelliklerini, yöntemlerini ve olaylarını görebilirsiniz. Belirli bir yöntemin kodunu görüntülemek için Sınıf Görünümü Yöntem adına çift tıklayın veya sağ tıklayın ve tanıma git ' i seçin.

![Sınıf Görünümü tanıma git ' i seçerek otomatik oluşturulan kodu inceleyin](creating-a-data-access-layer-cs/_static/image89.png)

**Şekil 33**: sınıf görünümü tanıma git ' i seçerek otomatik oluşturulan kodu inceleyin

Otomatik olarak oluşturulan kod harika bir zaman koruyucu olabilir, ancak kod genellikle çok geneldir ve uygulamanın benzersiz ihtiyaçlarını karşılamak için özelleştirilmelidir. Ancak otomatik olarak oluşturulan kodu genişletme riski, kodu oluşturan aracın, "yeniden oluşturma" ve özelleştirmelerinizin üzerine yazma zamanına karar vermesine neden olabilir. .NET 2.0 'ın yeni kısmi sınıf kavramıyla, bir sınıfı birden çok Dosya arasında ayırmak kolaydır. Bu, kendi yöntemlerimizi, özellikleri ve olayları, özelleştirmelerimizin üzerine yazarak Visual Studio hakkında endişelenmenize gerek kalmadan otomatik oluşturulan sınıflara eklememize olanak sağlar.

DAL özelleştirmeyi göstermek için **SuppliersRow** sınıfına bir **GetProducts ()** yöntemi ekleyelim. **SuppliersRow** sınıfı, **Suppliers** tablosundaki tek bir kaydı temsil eder; her tedarikçi, her bir tedarikçiden çok ürüne kadar, bu nedenle **GetProducts ()** belirtilen tedarikçinin ürünlerini döndürmeyecektir. Bunu gerçekleştirmek için, **SuppliersRow.cs** adlı **uygulama\_kod** klasöründe yeni bir sınıf dosyası oluşturun ve aşağıdaki kodu ekleyin:

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample22.cs)]

Bu kısmi sınıf, daha önce tanımladığımız **GetProducts ()** yöntemini dahil etmek için **Northwind. SuppliersRow** sınıfını oluştururken derleyiciye bildirir. Projenizi derleyip Sınıf Görünümü geri dönerseniz, şimdi **Northwind. SuppliersRow**yöntemi olarak listelenen **GetProducts ()** görürsünüz.

![GetProducts () yöntemi artık Northwind. SuppliersRow sınıfının bir parçasıdır](creating-a-data-access-layer-cs/_static/image90.png)

**Şekil 34**: **GetProducts ()** yöntemi artık **Northwind. SuppliersRow** sınıfının bir parçasıdır

**GetProducts ()** yöntemi artık, aşağıdaki kodda gösterildiği gibi belirli bir tedarikçinin ürün kümesini numaralandırmak için kullanılabilir:

[!code-html[Main](creating-a-data-access-layer-cs/samples/sample23.html)]

Bu veriler aynı zamanda ASP ' de görüntülenebilir. NET 'in veri Web denetimleri. Aşağıdaki sayfada iki alan içeren bir GridView denetimi kullanılmıştır:

- Her tedarikçinin adını görüntüleyen bir BoundField ve
- Her tedarikçi için **GetProducts ()** yöntemi tarafından döndürülen sonuçlara bağlanan bir BulletedList denetimi Içeren bir TemplateField.

Bu tür ana ayrıntı raporlarının gelecekteki öğreticilerde nasıl görüntüleneceğini inceleyeceğiz. Şimdilik, bu örnek **Northwind. SuppliersRow** sınıfına eklenen özel yöntemin kullanımını göstermek için tasarlanmıştır.

SuppliersAndProducts.aspx

[!code-aspx[Main](creating-a-data-access-layer-cs/samples/sample24.aspx)]

SuppliersAndProducts.aspx.cs

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample25.cs)]

[![, tedarikçinin şirket adı sol sütunda, sağ taraftaki ürünlerle listelenir](creating-a-data-access-layer-cs/_static/image92.png)](creating-a-data-access-layer-cs/_static/image91.png)

**Şekil 35**: tedarikçinin şirket adı sol sütunda, sağ taraftaki ürünlerde listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-data-access-layer-cs/_static/image93.png))

## <a name="summary"></a>Özet

Bir Web uygulaması oluşturulurken DAL oluşturma, sunum katmanınızı oluşturmaya başlamadan önce ortaya çıkan ilk adımlardan biri olmalıdır. Visual Studio ile, türü belirtilmiş veri kümelerine dayalı bir DAL oluşturmak, kod satırı yazmadan 10-15 dakika içinde gerçekleştirilebilen bir görevdir. İleriye doğru ilerleyen öğreticiler bu DAL üzerine oluşturulacak. Bir [sonraki öğreticide](creating-a-business-logic-layer-cs.md) , bir dizi iş kuralı tanımlayacağız ve bunları ayrı bir Iş mantığı katmanında nasıl uygulayacağınızı görürsünüz.

Programlamanın kutlu olsun!

## <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [VS 2005 ve ASP.NET 2,0 ' de kesin türü belirtilmiş TableAdapters ve DataTable kullanarak DAL oluşturma](https://weblogs.asp.net/scottgu/435498)
- [Veri katmanı bileşenlerini tasarlama ve katmanlar aracılığıyla veri geçirme](https://msdn.microsoft.com/library/ms978496.aspx)
- [Visual Studio 2005 DataSet Designer ile veri erişim katmanı oluşturma](http://www.theserverside.net/articles/showarticle.tss?id=DataSetDesigner)
- [ASP.NET 2,0 uygulamalarında yapılandırma bilgilerini şifreleme](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx)
- [TableAdapter Genel Bakış](https://msdn.microsoft.com/library/bz9tthwx.aspx)
- [Türü belirtilmiş bir veri kümesiyle çalışma](https://msdn.microsoft.com/library/esbykkzb.aspx)
- [Visual Studio 2005 ve ASP.NET 2,0 ' de kesin türü belirtilmiş veri erişimini kullanma](http://aspnet.4guysfromrolla.com/articles/020806-1.aspx)
- [TableAdapter yöntemlerini genişletme](https://blogs.msdn.com/vbteam/archive/2005/05/04/ExtendingTableAdapters.aspx)
- [Saklı yordamdan skalar verileri alma](http://aspnet.4guysfromrolla.com/articles/062905-1.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>Bu öğreticide bulunan konularda video eğitimi

- [ASP.NET Uygulamalarında Veri Erişim Katmanları](../../../videos/data-access/adonet-data-services/data-access-layers-in-aspnet-applications.md)
- [Bir veri kümesini DataGrid 'e El Ile bağlama](../../../videos/data-access/adonet-data-services/how-to-manually-bind-a-dataset-to-a-datagrid.md)
- [Bir ASP uygulamasından veri kümeleri ve filtrelerle çalışma](../../../videos/data-access/adonet-data-services/how-to-work-with-datasets-and-filters-from-an-asp-application.md)

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticiye ilişkin müşteri adayı gözden geçirenler, deniz yeşili, Tepton Giesenow, dennıs Patterson, Liz Shulok, Abel Gomez ve Carlos Santos. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Next](creating-a-business-logic-layer-cs.md)
