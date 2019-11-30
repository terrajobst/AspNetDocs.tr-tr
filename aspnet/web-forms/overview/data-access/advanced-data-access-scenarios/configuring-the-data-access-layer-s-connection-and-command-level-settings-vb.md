---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/configuring-the-data-access-layer-s-connection-and-command-level-settings-vb
title: Veri erişim katmanının bağlantısını ve komut düzeyi ayarlarını yapılandırma (VB) | Microsoft Docs
author: rick-anderson
description: Türü belirtilmiş veri kümesi içindeki TableAdapters otomatik olarak veritabanına bağlanma, komut verme ve sonuçlarıyla bir DataTable doldurma konusunda işlem gerçekleştirir...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: d57dfa2b-d627-45cb-b5b1-abbf3159d770
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/configuring-the-data-access-layer-s-connection-and-command-level-settings-vb
msc.type: authoredcontent
ms.openlocfilehash: fa2868fc0dd8acd76f600b47d92adb984ce8d105
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74573647"
---
# <a name="configuring-the-data-access-layers-connection--and-command-level-settings-vb"></a>Veri Erişim Katmanının Bağlantısını ve Komut Düzeyi Ayarlarını Yapılandırma (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_72_VB.zip) veya [PDF 'yi indirin](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/datatutorial72vb1.pdf)

> Türü belirtilmiş veri kümesi içindeki TableAdapters otomatik olarak veritabanına bağlanma, komut verme ve sonuçlarıyla bir DataTable doldurma konusunda işlem gerçekleştirir. Ancak, bu ayrıntıların kendimize ve bu öğreticide, TableAdapter 'daki veritabanı bağlantısına ve komut düzeyi ayarlarına nasıl erişebileceğinizi öğreniyoruz.

## <a name="introduction"></a>Giriş

Eğitim Serisi boyunca, veri erişim katmanını ve katmanlı mimarimizin iş nesnelerini uygulamak için yazılan veri kümelerini kullandık. [İlk öğreticide](../introduction/creating-a-data-access-layer-vb.md)anlatıldığı gibi, yazılan veri kümesi verileri veri depoları olarak görev yapar, TableAdapters, temel alınan verileri almak ve değiştirmek üzere veritabanıyla iletişim kurmak için sarmalayıcılar olarak davranır. TableAdapters, veritabanıyla çalışma ile ilgili karmaşıklığı kapsüllendirir ve veritabanına bağlanmak, bir komut vermek veya sonuçları bir DataTable dosyasına doldurmak için kod yazmak zorunda kalmaktan kurtarır.

Bununla birlikte, TableAdapter derinliklerinde burte ve doğrudan ADO.NET nesneleriyle çalışacak kod yazmak zorunda olduğumuz durumlar vardır. [Bir işlem öğreticisindeki sarmalama veritabanı değişikliklerine](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb.md) , örneğin, ADO.net işlemlerini başlatma, kaydetme ve geri alma için TableAdapter 'a Yöntemler ekledik. Bu yöntemler, TableAdapter s `SqlCommand` nesnelerine atanan bir iç, el ile oluşturulmuş `SqlTransaction` nesnesi kullanıyordu.

Bu öğreticide, TableAdapter 'ta veritabanı bağlantısına ve komut düzeyi ayarlarına nasıl erişeöğreneceksiniz. Özellikle, temel bağlantı dizesine ve komut zaman aşımı ayarlarına erişim sağlayan `ProductsTableAdapter` işlevsellik ekleyeceğiz.

## <a name="working-with-data-using-adonet"></a>ADO.NET kullanarak verilerle çalışma

Microsoft .NET Framework, verilerle çalışmak için özel olarak tasarlanmış sınıfların bir plethora içerir. [`System.Data` ad alanı](https://msdn.microsoft.com/library/system.data.aspx)içinde bulunan bu sınıflar, *ADO.net* sınıfları olarak adlandırılır. ADO.NET şemsiye altındaki sınıflardan bazıları belirli bir *veri sağlayıcısına*bağlıdır. Veri sağlayıcısını, ADO.NET sınıfları ve temel alınan veri deposu arasında bilgi akışına izin veren bir iletişim kanalı olarak düşünebilirsiniz. OleDb ve ODBC gibi Genelleştirilmiş sağlayıcıların yanı sıra belirli bir veritabanı sistemi için özel olarak tasarlanan sağlayıcıları da vardır. Örneğin, OleDb sağlayıcısı kullanılarak bir Microsoft SQL Server veritabanına bağlanmak mümkün olsa da, SqlClient sağlayıcısı, SQL Server için özel olarak tasarlandığından ve iyileştirildiğinden çok daha etkilidir.

Verilere programlı olarak erişirken, aşağıdaki model yaygın olarak kullanılır:

1. Veritabanıyla bağlantı kurun.
2. Bir komut verin.
3. `SELECT` sorguları için, sonuçta elde edilen kayıtlarla çalışın.

Bu adımların her birini gerçekleştirmek için ayrı ADO.NET sınıfları vardır. Örneğin, SqlClient sağlayıcısını kullanarak bir veritabanına bağlanmak için [`SqlConnection` sınıfını](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection(VS.80).aspx)kullanın. Veritabanına `INSERT`, `UPDATE`, `DELETE`veya `SELECT` komutu vermek için [`SqlCommand` sınıfını](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.aspx)kullanın.

Işlem öğreticisindeki [sarmalama veritabanı değişiklikleri](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb.md) dışında, TableAdapters otomatik oluşturulan kod, veritabanına bağlanmak, komut vermek, veri almak ve verileri DataTable 'a doldurmak için gereken işlevleri içerdiğinden, herhangi bir alt düzey ADO.net Code kendimize yazmak zorunda kaldık. Ancak, bu alt düzey ayarların özelleştirilmesi için gereken zamanlar olabilir. Sonraki birkaç adımda, TableAdapters tarafından dahili olarak kullanılan ADO.NET nesnelerine nasıl dokunduğunuzda inceleyeceğiz.

## <a name="step-1-examining-with-the-connection-property"></a>1\. Adım: bağlantı özelliği ile Inceleme

Her TableAdapter sınıfı, veritabanı bağlantı bilgilerini belirten bir `Connection` özelliğine sahiptir. Bu özellik veri türü ve `ConnectionString` değeri, TableAdapter Yapılandırma sihirbazında yapılan seçimlere göre belirlenir. Türü belirtilmiş bir veri kümesine ilk olarak bir TableAdapter eklediğimiz durumlarda bu sihirbaz bize veritabanı kaynağını sorar (bkz. Şekil 1). Bu ilk adımdaki açılan liste, yapılandırma dosyasında belirtilen veritabanlarını ve Sunucu Gezgini s veri bağlantılarında diğer veritabanlarını içerir. Kullanmak istediğimiz veritabanı aşağı açılan listede yoksa, yeni bağlantı düğmesine tıklayıp gerekli bağlantı bilgilerini sağlayarak yeni bir veritabanı bağlantısı belirtilebilir.

[TableAdapter Yapılandırma sihirbazının Ilk adımını ![](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image2.png)](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image1.png)

**Şekil 1**: TableAdapter Yapılandırma sihirbazının ilk adımı ([tam boyutlu görüntüyü görüntülemek için tıklayın](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image3.png))

TableAdapter for `Connection` özelliği için kodu incelemeye biraz zaman atalım. [Veri erişim katmanı oluşturma](../introduction/creating-a-data-access-layer-vb.md) öğreticisinde belirtildiği gibi, otomatik olarak oluşturulan TableAdapter kodunu Sınıf Görünümü penceresine gidip, uygun sınıfa giderek ve ardından üye adına çift tıklayarak görüntüleyebiliriz.

Görünüm menüsüne gidip Sınıf Görünümü ' i seçerek (veya Ctrl + Shift + C yazarak) Sınıf Görünümü penceresine gidin. Sınıf Görünümü penceresinin üst yarısında `NorthwindTableAdapters` ad alanına gidin ve `ProductsTableAdapter` sınıfını seçin. Bu işlem, Şekil 2 ' de gösterildiği gibi `ProductsTableAdapter` s üyelerini Sınıf Görünümü alt yarısında görüntüler. Kodunu görmek için `Connection` özelliğine çift tıklayın.

![Otomatik olarak oluşturulan kodu görüntülemek için Sınıf Görünümü bağlantı özelliğine çift tıklayın](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image4.png)

**Şekil 2**: otomatik olarak oluşturulan kodu görüntülemek Için sınıf görünümü bağlantı özelliğine çift tıklayın

TableAdapter s `Connection` özelliği ve bağlantıyla ilgili diğer kod aşağıdaki gibidir:

[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample1.vb)]

TableAdapter sınıfı örneği oluşturulduğunda `_connection` üye değişkeni `Nothing`eşittir. `Connection` özelliğine erişildiğinde, önce `_connection` üye değişkeninin örneği oluşturulmuş olup olmadığını kontrol eder. Bu yoksa `InitConnection` yöntemi çağrılır, bu, `_connection` örnekleyen ve `ConnectionString` özelliğini TableAdapter Yapılandırma Sihirbazı s ilk adımından belirtilen bağlantı dizesi değerine ayarlıyor.

`Connection` özelliği bir `SqlConnection` nesnesine de atanabilir. Bunun yapılması, yeni `SqlConnection` nesnesini tek bir TableAdapter s `SqlCommand` nesneleri ile ilişkilendirir.

## <a name="step-2-exposing-connection-level-settings"></a>2\. Adım: bağlantı düzeyi ayarlarını gösterme

Bağlantı bilgileri TableAdapter içinde kapsüllenmelidir ve uygulama mimarisinde diğer katmanlara erişemez. Ancak, TableAdapter bağlantı düzeyi bilgilerinin bir sorgu, Kullanıcı veya ASP.NET sayfası için erişilebilir veya özelleştirilebilir olması gerektiğinde senaryolar olabilir.

`Northwind` veri kümesindeki `ProductsTableAdapter`, TableAdapter tarafından kullanılan bağlantı dizesini okumak veya değiştirmek için Iş mantığı katmanı tarafından kullanılabilecek bir `ConnectionString` özelliği içerecek şekilde genişletmenize olanak tanır.

> [!NOTE]
> *Bağlantı dizesi* , kullanılacak sağlayıcı, veritabanının konumu, kimlik doğrulama bilgileri ve veritabanıyla ilgili diğer ayarlar gibi veritabanı bağlantı bilgilerini belirten bir dizedir. Çeşitli veri depoları ve sağlayıcılar tarafından kullanılan bağlantı dizesi desenlerinin listesi için bkz. [connectionStrings.com](http://www.connectionstrings.com/).

[Veri erişim katmanı oluşturma](../introduction/creating-a-data-access-layer-vb.md) öğreticisinde açıklandığı gibi, yazılan veri kümesinin otomatik olarak oluşturulan sınıfları kısmi sınıfların kullanımı aracılığıyla Genişletilebilir. İlk olarak, `~/App_Code/DAL` klasörünün altında `ConnectionAndCommandSettings` adlı projede yeni bir alt klasör oluşturun.

![ConnectionAndCommandSettings adında bir alt klasör ekleyin](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image5.png)

**Şekil 3**: `ConnectionAndCommandSettings` adlı bir alt klasör ekleme

`ProductsTableAdapter.ConnectionAndCommandSettings.vb` adlı yeni bir sınıf dosyası ekleyin ve aşağıdaki kodu girin:

[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample2.vb)]

Bu kısmi sınıf `ProductsTableAdapter` sınıfına `ConnectionString` adlı `Public` özelliği ekler. Bu, herhangi bir katmanın, ilişkili olan bağlantı dizesini okumasına veya güncelleştirmesine izin verir.

Bu kısmi sınıf oluşturulur (ve kaydedildiğinde), `ProductsBLL` sınıfını açın. Mevcut yöntemlerden birine gidin ve `Adapter` yazın ve ardından IntelliSense 'i getirmek için period tuşuna basın. IntelliSense 'de yeni `ConnectionString` özelliğini görmeniz gerekir, yani bu değeri BLL 'den programlama yoluyla okuyabilmeniz veya ayarlayabilmelisiniz.

## <a name="exposing-the-entire-connection-object"></a>Tüm bağlantı nesnesi gösteriliyor

Bu kısmi sınıf, temel alınan bağlantı nesnesinin yalnızca bir özelliğini kullanıma sunar: `ConnectionString`. Tüm bağlantı nesnesini TableAdapter 'ın sınırlarının ötesinde kullanılabilir hale getirmek istiyorsanız, `Connection` özellik s koruma düzeyini değiştirebilirsiniz. Adım 1 ' de incelenen otomatik oluşturulan kod, TableAdapter s `Connection` özelliğinin `Friend`olarak işaretlendiğinden, yani yalnızca aynı derlemede bulunan sınıflar tarafından erişilebileceği anlamına geliyor. Bununla birlikte, TableAdapter s `ConnectionModifier` özelliği aracılığıyla bu değiştirilebilir.

`Northwind` veri kümesini açın, tasarımcıda `ProductsTableAdapter` tıklayın ve Özellikler penceresi gidin. `ConnectionModifier`, `Assembly`varsayılan değerine ayarlandığını görürsünüz. `Connection` özelliğini, türü belirtilmiş DataSet s derlemesinin dışında kullanılabilir hale getirmek için, `ConnectionModifier` özelliğini `Public`olarak değiştirin.

[Bağlantı özelliği s erişilebilirlik düzeyi ![ConnectionModifier özelliği aracılığıyla yapılandırılabilir](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image7.png)](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image6.png)

**Şekil 4**: `Connection` Property s erişilebilirlik düzeyi `ConnectionModifier` özelliği aracılığıyla yapılandırılabilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image8.png))

Veri kümesini kaydedin ve sonra `ProductsBLL` sınıfına geri dönün. Daha önce olduğu gibi, mevcut yöntemlerden birine gidin ve `Adapter` yazın ve ardından IntelliSense 'i getirmek için period tuşuna basın. Liste, artık BLL 'den herhangi bir bağlantı düzeyindeki ayarı program aracılığıyla okuyabilmeniz veya atayabilmeniz için bir `Connection` özelliği içermelidir.

## <a name="step-3-examining-the-command-related-properties"></a>3\. Adım: komutla Ilgili özellikleri Inceleme

TableAdapter, varsayılan olarak otomatik olarak oluşturulan `INSERT`, `UPDATE`ve `DELETE` deyimlerini içeren bir ana sorgudan oluşur. Bu ana sorgu s `INSERT`, `UPDATE`ve `DELETE` deyimleri, `Adapter` özelliği aracılığıyla TableAdapter s kodunda bir ADO.NET veri bağdaştırıcısı nesnesi olarak uygulanır. `Connection` özelliği ile benzer şekilde, `Adapter` özellik s veri türü kullanılan veri sağlayıcısı tarafından belirlenir. Bu öğreticiler SqlClient sağlayıcısını kullandığından `Adapter` özelliği [`SqlDataAdapter`](https://msdn.microsoft.com/library/system.data.sqlclient.sqldataadapter(VS.80).aspx)türündedir.

TableAdapter s `Adapter` özelliği, `SqlCommand` türünde `INSERT`, `UPDATE`ve `DELETE` deyimlerini vermek için kullandığı üç özelliğe sahiptir:

- `InsertCommand`
- `UpdateCommand`
- `DeleteCommand`

`SqlCommand` nesnesi, veritabanına belirli bir sorgu göndermekten sorumludur ve şu şekilde özelliklere sahiptir: [`CommandText`](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.commandtext.aspx), örneğin, geçici SQL ifadesini veya yürütülecek saklı yordamı içeren. ve bir `SqlParameter` nesneleri koleksiyonu olan [`Parameters`](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.parameters.aspx). [Veri erişim katmanı oluşturma](../introduction/creating-a-data-access-layer-vb.md) öğreticisinde geri döndüğünüzde, bu komut nesneleri Özellikler penceresi aracılığıyla özelleştirilebilir.

TableAdapter, ana sorgusuna ek olarak, çağrıldığında, belirtilen bir komutu veritabanına gönderse, bir değişken sayıda yöntem içerebilir. Ana sorgu s komut nesnesi ve tüm ek yöntemler için komut nesneleri TableAdapter s `CommandCollection` özelliğinde depolanır.

Bu iki özellik ve destekleyici üye değişkenleri ve yardımcı yöntemleri için `Northwind` veri kümesindeki `ProductsTableAdapter` tarafından oluşturulan koda bakmak için bir süre bekleyin:

[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample3.vb)]

`Adapter` ve `CommandCollection` özelliklerinin kodu `Connection` özelliğini yakından taklit eder. Özellikler tarafından kullanılan nesneleri tutan üye değişkenleri vardır. Özellikler `Get` erişimcileri, ilgili üye değişkeninin `Nothing`olup olmadığını denetleyerek başlar. Bu durumda, üye değişkeninin bir örneğini oluşturan ve komutla ilgili temel özellikleri atayan bir başlatma yöntemi çağırılır.

## <a name="step-4-exposing-command-level-settings"></a>4\. Adım: komut düzeyi ayarları gösterme

İdeal olarak, komut düzeyi bilgileri veri erişim katmanında kapsüllenmelidir. Bu bilgilerin mimarinin diğer katmanlarında olması gerekir, ancak tıpkı bağlantı düzeyi ayarları gibi kısmi bir sınıf aracılığıyla sunulabilir.

TableAdapter yalnızca tek bir `Connection` özelliğine sahip olduğundan, bağlantı düzeyi ayarlarını gösterme kodu oldukça basittir. TableAdapter, bir `InsertCommand`, `UpdateCommand`ve `DeleteCommand`, `CommandCollection` özelliğindeki çeşitli komut nesneleriyle birlikte birden çok komut nesnesine sahip olabileceğinden, komut düzeyi ayarları değiştirirken bu işlemler biraz daha karmaşıktır. Komut düzeyi ayarları güncelleştirilirken, bu ayarların tüm komut nesnelerine yayılmalıdır.

Örneğin, TableAdapter 'ta yürütülmesi için olağandışı uzun süre geçen belirli sorgular olduğunu düşünün. Bu sorgulardan birini yürütmek için TableAdapter kullanılırken, komut nesne s [`CommandTimeout` özelliğini](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.commandtimeout.aspx)artırmak isteyebilirsiniz. Bu özellik, komutun yürütülmesi için bekleyeceği saniye sayısını ve varsayılan olarak 30 değerini belirtir.

`CommandTimeout` özelliğinin BLL tarafından ayarlanmasına izin vermek için, adım 2 ' de oluşturulan kısmi sınıf dosyasını kullanarak `ProductsDataTable` aşağıdaki `Public` yöntemini ekleyin (`ProductsTableAdapter.ConnectionAndCommandSettings.vb`):

[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample4.vb)]

Bu yöntem, Bu TableAdapter örneği tarafından tüm komut sorunları için komut zaman aşımını ayarlamak üzere BLL veya Presentation katmanından çağrılabilir.

> [!NOTE]
> `Adapter` ve `CommandCollection` özellikleri `Private`olarak işaretlenir, yani yalnızca TableAdapter içindeki koddan erişilebilir. `Connection` özelliğinden farklı olarak, bu erişim değiştiricileri yapılandırılamaz. Bu nedenle, komut düzeyi özellikleri mimarideki diğer katmanlara kullanıma sunmaya ihtiyacınız varsa, `Private` komut nesnelerini okuyan veya yazan bir `Public` metodu veya özelliği sağlamak için yukarıda açıklanan kısmi sınıf yaklaşımını kullanmanız gerekir.

## <a name="summary"></a>Özet

Türü belirtilmiş veri kümesi içindeki TableAdapters veri erişimi ayrıntılarını ve karmaşıklığını kapsüllemek için işlev yapar. TableAdapters kullanarak, veritabanına bağlanmak, bir komut vermek veya sonuçları bir DataTable dosyasına doldurmak için ADO.NET kodu yazma konusunda endişelenmenize gerek yoktur. Hepsi sizin için otomatik olarak işlenir.

Ancak, bağlantı dizesini veya varsayılan bağlantıyı veya komut zaman aşımı değerlerini değiştirme gibi alt düzey ADO.NET özelliklerini özelleştirmek için gereken durumlar olabilir. TableAdapter otomatik olarak oluşturulan `Connection`, `Adapter`ve `CommandCollection` özelliklerine sahiptir, ancak bunlar varsayılan olarak `Friend` veya `Private`. Bu iç bilgiler, `Public` Yöntemler veya özellikler dahil olmak üzere kısmi sınıflar kullanılarak TableAdapter genişleterek ortaya çıkabilir. Alternatif olarak, TableAdapter s `Connection` özellik erişim değiştiricisi TableAdapter s `ConnectionModifier` özelliği aracılığıyla yapılandırılabilir.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler Burnadette Leigh, S Ren Jacob Lauritsen, Teresa Murphy ve Tepton Geisenow. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](working-with-computed-columns-vb.md)
> [İleri](protecting-connection-strings-and-other-configuration-information-vb.md)
