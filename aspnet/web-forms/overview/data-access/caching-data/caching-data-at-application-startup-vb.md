---
uid: web-forms/overview/data-access/caching-data/caching-data-at-application-startup-vb
title: Uygulama başlangıcında verileri önbelleğe alma (VB) | Microsoft Docs
author: rick-anderson
description: Herhangi bir Web uygulamasında, bazı veriler sık sık kullanılır ve bazı veriler seyrek kullanılır. B ASP.NET uygulamamız performansını iyileştirebiliriz...
ms.author: riande
ms.date: 05/30/2007
ms.assetid: 84afe4ac-cc53-4f2e-a867-27eaf692c2df
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-at-application-startup-vb
msc.type: authoredcontent
ms.openlocfilehash: 6c07b565329ab17496d2436f4c35bc4507694ed8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78576855"
---
# <a name="caching-data-at-application-startup-vb"></a>Uygulama Başlangıcında Verileri Önbelleğe Alma (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[PDF 'YI indir](caching-data-at-application-startup-vb/_static/datatutorial60vb1.pdf)

> Herhangi bir Web uygulamasında, bazı veriler sık sık kullanılır ve bazı veriler seyrek kullanılır. Sık kullanılan verileri, olarak bilinen bir tekniğe göre karşıya yükleyerek ASP.NET uygulamamız performansını iyileştirebiliriz. Bu öğreticide, uygulama başlangıcında önbelleğe veri yüklemek üzere bir proaktif yüklemeye yönelik bir yaklaşım gösterilmektedir.

## <a name="introduction"></a>Giriş

Önceki iki öğretici, sunudaki verileri önbelleğe alma ve önbelleğe alma katmanları hakkında bakıyor. [ObjectDataSource Ile verileri önbelleğe alma](caching-data-with-the-objectdatasource-vb.md)Işleminde, sunu katmanındaki verileri önbelleğe almak için ObjectDataSource s önbelleğe alma özelliklerini kullanmayı inceledik. [Mimarideki verileri önbelleğe](caching-data-in-the-architecture-vb.md) alma, yeni ve ayrı bir önbelleğe alma katmanında önbelleğe alınıyor. Bu öğreticilerin her ikisi de veri önbelleğiyle çalışırken *reaktif yüklemeyi* kullandı. Reaktif yükleme sayesinde, verilerin her istenilişinde sistem öncelikle önbellekte olup olmadığını denetler. Aksi takdirde, veritabanı gibi kaynak kaynaktaki verileri dönüştürür ve sonra önbellekte depolar. Reaktif yüklemenin başlıca avantajı, uygulama kolaylığıdır. Dezavantajlarından biri, istekler arasında düzensiz performanslarıdır. Ürün bilgilerini göstermek için önceki öğreticiden önbelleğe alma katmanını kullanan bir sayfa düşünün. Bu sayfa ilk kez ziyaret edildiğinde veya bellek kısıtlamaları nedeniyle önbelleğe alınan veriler çıkarıldıktan sonra ilk kez ziyaret edildiğinde veya belirtilen süre dolduktan sonra, verilerin veritabanından alınması gerekir. Bu nedenle, bu kullanıcı istekleri, önbellek tarafından sunulabilen Kullanıcı isteklerinden daha uzun sürer.

*Öngörülü yükleme* , önbellekteki verileri gerekenden önce yükleyerek isteklerin performansını yumuşönünde tutarak alternatif bir önbellek yönetimi stratejisi sağlar. Genellikle, öngörülü yükleme, temel alınan verilerde bir güncelleştirme yapıldığında düzenli olarak denetleyen veya bildirilen bir işlemi kullanır. Bu işlem daha sonra önbelleği güncel tutmak için güncelleştirir. Proaktif yükleme, özellikle temel alınan veriler yavaş bir veritabanı bağlantısı, bir Web hizmeti veya başka bir özellikle Yavaşlı veri kaynağından geliyorsa kullanışlıdır. Ancak proaktif yüklemeye yönelik bu yaklaşım, değişiklikleri denetlemek ve önbelleği güncelleştirmek için bir işlem oluşturmak, yönetmek ve dağıtmak gerektirdiğinden uygulamanız daha zordur.

Başka bir öngörülü yükleme özelliği ve bu öğreticide keşfetmeye başlayacağımız tür, uygulamanın başlangıcında verileri önbelleğe yüklüyor. Bu yaklaşım özellikle veritabanı arama tablolarındaki kayıtlar gibi statik verileri önbelleğe almak için yararlıdır.

> [!NOTE]
> Öngörülü ve reaktif yükleme arasındaki farklılıklara, diğer taraf listelerine, dezavantajlara ve uygulama önerlerine yönelik daha ayrıntılı bir bakış için, [.NET Framework uygulamalar Için önbelleğe alma mimarisi kılavuzunun](https://msdn.microsoft.com/library/ms978498.aspx) [önbellek içeriğini yönetme](https://msdn.microsoft.com/library/ms978503.aspx) bölümüne bakın.

## <a name="step-1-determining-what-data-to-cache-at-application-startup"></a>1\. Adım: uygulama başlangıcında hangi verilerin önbelleğe yerleştirileceğini belirleme

Önceki iki öğreticinin inceduğumuz reaktif yüklemeyi kullanan önbelleğe alma örnekleri, düzenli aralıklarla değişen ve exorbitantly uzun sürme sürelerine uygun verilerle iyi çalışır. Ancak önbelleğe alınan veriler hiç değişmediğinde, reaktif yükleme tarafından kullanılan süre sonu gereksiz olur. Benzer şekilde, önbelleğe alınan verilerin oluşturulabilmesi uzun süre sürüyorsa, bu durumda, istekleri önbellekte bulunan kullanıcıların, temel alınan veriler alınırken uzun bir bekleme süresine sahip olması gerekir. Uygulama başlangıcında oluşturmak için çok uzun süre alan statik verileri ve verileri önbelleğe almayı düşünün.

Veritabanlarında çok sayıda dinamik, sık değişen değer olduğunda, çoğu da büyük miktarda statik veriye sahiptir. Örneğin, neredeyse tüm veri modellerinde sabit bir seçenek kümesinden belirli bir değer içeren bir veya daha fazla sütun bulunur. Bir `Patients` veritabanı tablosu, bir `PrimaryLanguage` sütununa sahip olabilir; bu değer kümesi Ingilizce, Ispanyolca, Fransızca, Rusça, Japonca gibi olabilir. Oftentimes, bu tür sütunlar *arama tabloları*kullanılarak uygulanır. `Patients` tablosunda Ingilizce veya Fransızca dizesini depolamak yerine, genellikle iki sütunlu, benzersiz bir tanımlayıcı ve dize açıklaması olan her olası değer için bir kayıt içeren ikinci bir tablo oluşturulur. `Patients` tablosundaki `PrimaryLanguage` sütunu, arama tablosunda karşılık gelen benzersiz tanımlayıcıyı depolar. Şekil 1 ' de hasta John tikan birincil dili Ingilizce, ancak Ed Johnson s ise Rusça.

![Diller tablosu, hastalar tablosu tarafından kullanılan bir arama tablosudur](caching-data-at-application-startup-vb/_static/image1.png)

**Şekil 1**: `Languages` tablo, `Patients` tablo tarafından kullanılan bir arama tablosudur

Yeni bir hasta düzenlemesi veya oluşturulması için Kullanıcı arabirimi, `Languages` tablosundaki kayıtlar tarafından doldurulan izin verilen dillerin açılan listesini içerir. Önbelleğe alma olmadan, bu arabirim her ziyaret edildiğinde sistem `Languages` tablosunu sorgulmalıdır. Bu, arama tablosu değerleri çok seyrek değişiklik yaptığından, bu, neredeyse gereksizdir ve gereksiz olur.

Önceki öğreticilerde incelenen aynı reaktif yükleme tekniklerini kullanarak `Languages` verilerini önbelleğe göndereceğiz. Ancak reaktif yükleme, statik arama tablosu verileri için gerekli olmayan, zaman tabanlı süre sonu kullanır. Reaktif yükleme kullanılarak önbelleğe alma işlemi, hiç önbelleğe alma olmadan daha iyi olacaktır, ancak en iyi yaklaşım, arama tablosu verilerini uygulama başlangıcında önbelleğe önceden yüklemek olacaktır.

Bu öğreticide, arama tablosu verilerini ve diğer statik bilgileri önbelleğe alma bölümüne bakacağız.

## <a name="step-2-examining-the-different-ways-to-cache-data"></a>2\. Adım: verileri önbelleğe almanın farklı yollarını Inceleme

Bilgiler, çeşitli yaklaşımlar kullanılarak program aracılığıyla bir ASP.NET uygulamasında önbelleğe alınabilir. Önceki öğreticilerde veri önbelleğinin nasıl kullanıldığını zaten gördük. Alternatif olarak, nesneler *statik Üyeler* veya *uygulama durumu*kullanılarak programlı bir şekilde önbelleğe alınabilir.

Bir sınıfla çalışırken, genellikle sınıfın üyelerine erişilebilmesi için önce sınıfın oluşturulması gerekir. Örneğin, Iş mantığı katmanımızda sınıflardan birindeki bir yöntemi çağırmak için öncelikle sınıfının bir örneğini oluşturmanız gerekir:

[!code-vb[Main](caching-data-at-application-startup-vb/samples/sample1.vb)]

*SomeMethod* 'u çağırabilmemiz veya *SomeProperty*ile çalışmadan önce, önce `New` anahtar sözcüğünü kullanarak sınıfın bir örneğini oluşturmanız gerekir. *SomeMethod* ve *SomeProperty* belirli bir örnekle ilişkilendirilir. Bu üyelerin ömrü, ilişkili nesnesinin kullanım ömrüne bağlıdır. Diğer yandan *statik Üyeler*, sınıfının *Tüm* örnekleri arasında paylaşılan değişkenler, Özellikler ve yöntemlerdir ve sonuç olarak, bu, sınıfının süresi kadar olan bir yaşam süresine sahiptir. Statik Üyeler anahtar sözcük `Shared`gösterilir.

Statik üyelere ek olarak, veriler uygulama durumu kullanılarak önbelleğe alınabilir. Her bir ASP.NET uygulaması, uygulamanın tüm kullanıcıları ve sayfaları genelinde paylaşılan bir ad/değer koleksiyonu tutar. Bu koleksiyona [`HttpContext` Class](https://msdn.microsoft.com/library/system.web.httpcontext.aspx) s [`Application` özelliği](https://msdn.microsoft.com/library/system.web.httpcontext.application.aspx)kullanılarak erişilebilir ve bunun gibi bir ASP.net Page s arka plan kod sınıfından de kullanılabilir:

[!code-vb[Main](caching-data-at-application-startup-vb/samples/sample2.vb)]

Veri önbelleği, verileri önbelleğe almak için daha zengin bir API sağlar ve zaman ve bağımlılık tabanlı expiries, önbellek öğesi öncelikleri ve benzeri mekanizmalar sağlar. Statik üyeler ve uygulama durumuyla, bu tür özelliklerin sayfa geliştiricisi tarafından el ile eklenmesi gerekir. Uygulamanın kullanım ömrü boyunca uygulama başlangıcında verileri önbelleğe alırken, veri önbelleğinin avantajları moot ' dir. Bu öğreticide statik verileri önbelleğe almak için üç tekniği kullanan koda bakacağız.

## <a name="step-3-caching-thesupplierstable-data"></a>3\. Adım:`Suppliers`tablo verilerini önbelleğe alma

Bugüne yaptığımız Northwind veritabanı tabloları herhangi bir geleneksel arama tablosu içermez. Bu dört DataTable, değerleri statik olmayan tüm model tabloları olan DAL ' de uygulanır. DAL için yeni bir DataTable eklemek ve ardından BLL 'e yeni bir sınıf ve yöntemler eklemek yerine, bu öğretici için `Suppliers` tablo s verilerinin statik olduğunu yalnızca önceden kabul edelim. Bu nedenle, bu verileri uygulama başlangıcında önbelleğe göndereceğiz.

Başlamak için `CL` klasöründe `StaticCache.cs` adlı yeni bir sınıf oluşturun.

![CL klasöründe StaticCache. vb sınıfını oluşturma](caching-data-at-application-startup-vb/_static/image2.png)

**Şekil 2**: `CL` klasöründe `StaticCache.vb` sınıfını oluşturma

Başlangıçtaki verileri uygun önbellek deposuna ve bu önbellekten veri döndüren yöntemlere yükleyen bir yöntem eklememiz gerekiyor.

[!code-vb[Main](caching-data-at-application-startup-vb/samples/sample3.vb)]

Yukarıdaki kod, `LoadStaticCache()` yönteminden çağrılan `SuppliersBLL` sınıf s `GetSuppliers()` yönteminden sonuçları tutmak için `suppliers`statik bir üye değişkenini kullanır. `LoadStaticCache()` yöntemi, uygulamanın başlatılması sırasında çağrılır. Bu veriler uygulama başlangıcında yüklendikten sonra, tedarikçi verileriyle çalışması gereken herhangi bir sayfa `StaticCache` sınıf s `GetSuppliers()` metodunu çağırabilir. Bu nedenle, tedarikçilere ulaşmak için veritabanına yapılan çağrı, uygulamanın başlangıcında yalnızca bir kez gerçekleşir.

Önbellek deposu olarak bir statik üye değişkeni kullanmak yerine, başka bir uygulama durumu veya veri önbelleği kullandık. Aşağıdaki kod, uygulama durumunu kullanmak için sınıfını gösterir:

[!code-vb[Main](caching-data-at-application-startup-vb/samples/sample4.vb)]

`LoadStaticCache()`, tedarikçinin bilgileri uygulama değişkeni *anahtarında*depolanır. Bu, `GetSuppliers()`uygun tür (`Northwind.SuppliersDataTable`) olarak döndürüldü. Uygulama durumuna `Application("key")`kullanarak ASP.NET sayfaların arka plan kod sınıflarında erişilebilir olsa da, mimaride geçerli `HttpContext`alabilmek için `HttpContext.Current.Application("key")` kullanılmalıdır.

Benzer şekilde, aşağıdaki kodda gösterildiği gibi, veri önbelleği bir önbellek deposu olarak kullanılabilir:

[!code-vb[Main](caching-data-at-application-startup-vb/samples/sample5.vb)]

Veri önbelleğine zaman tabanlı süre sonu olmadan bir öğe eklemek için, `System.Web.Caching.Cache.NoAbsoluteExpiration` ve `System.Web.Caching.Cache.NoSlidingExpiration` değerlerini giriş parametresi olarak kullanın. Veri önbelleği s `Insert` yönteminin bu belirli aşırı yüklemesi, önbellek öğesinin *önceliğini* belirleyebilmemiz için seçilmiştir. Kullanılabilir bellek az çalıştığında önbellekten hangi öğelerin atmak gerektiğini belirlemek için öncelik kullanılır. Burada, bu önbellek öğesinin atılmamasını sağlayan öncelik `NotRemovable`kullanırız.

> [!NOTE]
> Bu öğreticide indirme, statik üye değişkeni yaklaşımını kullanarak `StaticCache` sınıfını uygular. Uygulama durumu ve veri önbelleği teknikleri kodu, sınıf dosyasındaki açıklamalarda kullanılabilir.

## <a name="step-4-executing-code-at-application-startup"></a>4\. Adım: uygulama başlangıcında kodu yürütme

Bir Web uygulaması ilk kez başladığında kodu yürütmek için `Global.asax`adlı özel bir dosya oluşturmanız gerekir. Bu dosya, uygulama, oturum ve istek düzeyindeki olaylar için olay işleyicileri içerebilir ve uygulama her başlatıldığında yürütülecek kodu ekleyebilmemiz burada yer alabilir.

Visual Studio s Çözüm Gezgini Web sitesi proje adına sağ tıklayıp yeni öğe Ekle ' yi seçerek `Global.asax` dosyasını Web uygulamanızın kök dizinine ekleyin. Yeni öğe Ekle iletişim kutusunda, genel uygulama sınıfı öğe türünü seçin ve ardından Ekle düğmesine tıklayın.

> [!NOTE]
> Projenizde zaten bir `Global.asax` dosyanız varsa, genel uygulama sınıfı öğe türü yeni öğe Ekle iletişim kutusunda listelenmez.

[![Global. asax dosyasını Web uygulamanızın kök dizinine ekleyin](caching-data-at-application-startup-vb/_static/image4.png)](caching-data-at-application-startup-vb/_static/image3.png)

**Şekil 3**: `Global.asax` dosyasını Web uygulamanızın kök dizinine ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](caching-data-at-application-startup-vb/_static/image5.png))

Varsayılan `Global.asax` dosya şablonu, sunucu tarafı `<script>` etiketi içinde beş yöntem içerir:

- Web uygulaması ilk kez başladığında **`Application_Start`** yürütülür
- Uygulama kapatılırken **`Application_End`** çalışır
- Her işlenmeyen bir özel durum uygulamaya ulaştığında **`Application_Error`** yürütülür
- Yeni bir oturum oluşturulduğunda **`Session_Start`** yürütülür
- **`Session_End`** , bir oturumun süre dolduğunda veya terk edildiğinde çalıştırılır

`Application_Start` olay işleyicisi, bir uygulama yaşam döngüsü sırasında yalnızca bir kez çağrılır. Uygulama, uygulama yeniden başlatılana kadar bir ASP.NET kaynağı istendiğinde çalışmaya başlar ve `/Bin` klasörünün içeriğini değiştirerek, `Global.asax`değiştirerek, `App_Code` klasöründeki içerikleri değiştirerek veya `Web.config` dosyasını başka nedenler arasında değiştirerek ortaya çıkabilir. Uygulama yaşam döngüsü hakkında daha ayrıntılı bir tartışma için [ASP.NET uygulama yaşam döngüsüne genel bakış](https://msdn.microsoft.com/library/ms178473.aspx) bölümüne bakın.

Bu öğreticiler için yalnızca `Application_Start` yöntemine kod eklememiz gerekiyor, bu nedenle diğerlerini kaldırmayı ücretsiz olarak hissettik. `Application_Start`' de, üretici bilgilerini yükleyecek ve önbelleğe alacak `StaticCache` sınıf s `LoadStaticCache()` metodunu çağırmanız yeterlidir:

[!code-aspx[Main](caching-data-at-application-startup-vb/samples/sample6.aspx)]

İşte bu kadar! Uygulama başlangıcında `LoadStaticCache()` yöntemi BLL 'den Tedarikçi bilgilerini alacak ve statik bir üye değişkeninde (ya da `StaticCache` sınıfında kullanarak sonlandırmış olan herhangi bir önbellek deposu) depolayacaktır. Bu davranışı doğrulamak için `Application_Start` yönteminde bir kesme noktası ayarlayın ve uygulamanızı çalıştırın. Kesme noktasının uygulamanın başladığı üzerine isabet dığına göz önünde varın. Ancak, sonraki istekler `Application_Start` yönteminin yürütülmesine neden olmaz.

[Application_Start olay Işleyicisinin yürütüldüğünü doğrulamak için bir kesme noktası kullanın ![](caching-data-at-application-startup-vb/_static/image7.png)](caching-data-at-application-startup-vb/_static/image6.png)

**Şekil 4**: `Application_Start` olay Işleyicisinin yürütüldüğünü doğrulamak Için bir kesme noktası kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](caching-data-at-application-startup-vb/_static/image8.png))

> [!NOTE]
> Hata ayıklamayı ilk kez başlattığınızda `Application_Start` kesme noktasına ulaşırsanız, uygulamanızın zaten başlatılmış olması gerekir. `Global.asax` veya `Web.config` dosyalarını değiştirerek uygulamayı yeniden başlamaya zorlayın ve sonra yeniden deneyin. Uygulamayı hızlı bir şekilde yeniden başlatmak için bu dosyalardan birinin sonuna boş bir satır ekleyebilir (veya kaldırabilirsiniz).

## <a name="step-5-displaying-the-cached-data"></a>5\. Adım: önbelleğe alınan verileri görüntüleme

Bu noktada `StaticCache` sınıfı, uygulama başlangıcında önbelleğe alınan ve `GetSuppliers()` yöntemi aracılığıyla erişilebilen Tedarikçi verilerinin bir sürümüne sahiptir. Sunu katmanından bu verilerle çalışmak için bir ObjectDataSource kullanabilir veya bir ASP.NET sayfa arka plan kod sınıfından `StaticCache` sınıf s `GetSuppliers()` metodunu program aracılığıyla çağırabilirsiniz. Önbelleğe alınan Tedarikçi bilgilerini göstermek için ObjectDataSource ve GridView denetimlerini kullanmaya bakalım.

`Caching` klasöründeki `AtApplicationStartup.aspx` sayfasını açarak başlayın. Araç kutusundan Tasarımcı üzerine bir GridView sürükleyip `ID` özelliğini `Suppliers`olarak ayarlayarak. Sonra, GridView s akıllı etiketinden `SuppliersCachedDataSource`adlı yeni bir ObjectDataSource oluşturmayı seçin. `StaticCache` sınıf s `GetSuppliers()` metodunu kullanmak için ObjectDataSource 'ı yapılandırın.

[![, ObjectDataSource 'ı StaticCache sınıfını kullanacak şekilde yapılandırma](caching-data-at-application-startup-vb/_static/image10.png)](caching-data-at-application-startup-vb/_static/image9.png)

**Şekil 5**: ObjectDataSource 'ı `StaticCache` sınıfını kullanacak şekilde yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](caching-data-at-application-startup-vb/_static/image11.png))

[![, önbelleğe alınmış Tedarikçi verilerini almak için GetSuppliers () yöntemini kullanın](caching-data-at-application-startup-vb/_static/image13.png)](caching-data-at-application-startup-vb/_static/image12.png)

**Şekil 6**: önbelleğe alınan üretici verilerini almak Için `GetSuppliers()` yöntemini kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](caching-data-at-application-startup-vb/_static/image14.png))

Sihirbazı tamamladıktan sonra, Visual Studio `SuppliersDataTable`içindeki her veri alanı için otomatik olarak BoundFields ekler. GridView ve ObjectDataSource 'lar için bildirim temelli biçimlendirme aşağıdakine benzer olmalıdır:

[!code-aspx[Main](caching-data-at-application-startup-vb/samples/sample7.aspx)]

Şekil 7 ' de bir tarayıcıdan görüntülendikleri sayfa gösterilir. Çıktı, BLL s `SuppliersBLL` sınıfından verileri çektik, ancak `StaticCache` sınıfının kullanılması, uygulama başlangıcında önbelleğe alınmış olarak tedarikçinin verilerini geri döndürüyor. Bu davranışı doğrulamak için `StaticCache` sınıf s `GetSuppliers()` yönteminde kesme noktaları ayarlayabilirsiniz.

[![önbelleğe alınmış tedarikçinin verileri bir GridView içinde görüntülenir](caching-data-at-application-startup-vb/_static/image16.png)](caching-data-at-application-startup-vb/_static/image15.png)

**Şekil 7**: önbelleğe alınan Tedarikçi verileri bir GridView içinde görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](caching-data-at-application-startup-vb/_static/image17.png))

## <a name="summary"></a>Özet

Her veri modelinin çoğu, genellikle arama tabloları biçiminde uygulanan, büyük miktarda statik veri içerir. Bu bilgiler statik olduğundan, bu bilgilerin gösterilmesi her zaman veritabanına sürekli olarak erişmeye yönelik bir neden yoktur. Ayrıca, statik doğası nedeniyle verileri önbelleğe alırken süre sonu için gerekli değildir. Bu öğreticide, bu tür verileri nasıl kullanacağınızı ve veri önbelleğinde, uygulama durumunda ve statik bir üye değişkeniyle nasıl önbelleğe alınacağını gördük. Bu bilgiler uygulama başlangıcında önbelleğe alınır ve uygulama ömrü boyunca önbellekte kalır.

Bu öğreticide ve geçmişteki iki adımda, uygulamanın yaşam süresi boyunca verileri önbelleğe alma ve zaman tabanlı expiries kullanma konusunda baktık. Veritabanı verilerini önbelleğe alırken, zaman tabanlı süre sonu ideal olabilir. Önbelleği düzenli aralıklarla reçeteye göre, yalnızca temeldeki veritabanı verileri değiştirildiğinde önbelleğe alınmış öğeyi çıkarmak en iyi hale gelir. Bu ideal değer, bir sonraki öğreticimizde inceleyeceğiz. SQL önbellek bağımlılıklarının kullanımı aracılığıyla yapılabilir.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler, bir Murphy ve Zack Jones olarak değiştirildi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](caching-data-in-the-architecture-vb.md)
> [İleri](using-sql-cache-dependencies-vb.md)
