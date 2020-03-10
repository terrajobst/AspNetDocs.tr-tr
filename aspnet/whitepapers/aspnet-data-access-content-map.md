---
uid: whitepapers/aspnet-data-access-content-map
title: ASP.NET veri erişimi-önerilen kaynaklar | Microsoft Docs
author: rick-anderson
description: Bu konuda, birincil olarak Entity Framework ve SQL CE kullanarak ASP.NET Web uygulamalarındaki verilere erişme hakkında belge kaynaklarına yönelik bağlantılar sağlanmaktadır...
ms.author: riande
ms.date: 07/25/2013
ms.assetid: f8157be1-4ab9-469e-ad3a-0ccc80b56c00
msc.legacyurl: /whitepapers/aspnet-data-access-content-map
msc.type: content
ms.openlocfilehash: 357851f195bf233c7c34a32bd156e4408d3e1b24
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78633135"
---
# <a name="aspnet-data-access---recommended-resources"></a>ASP.NET Veri Erişimi - Önerilen Kaynaklar

> Bu konu, öncelikle Entity Framework ve SQL Server kullanarak, ASP.NET Web uygulamalarındaki verilere erişme hakkında belge kaynaklarına bağlantılar sağlar.
> 
> Harika bir blog gönderisi, [StackOverflow](http://stackoverflow.com) iş parçacığı veya yararlı olabilecek başka bir bağlantı biliyorsanız, bağlantıyı kullanarak [bize e-posta gönderin](mailto:aspnetue@microsoft.com?subject=Data Access Content Map) .
> 
> Son güncelleme 4/3/2014

Konusu aşağıdaki bölümleri içerir:

- [ASP.NET 'de veri erişimi ile çalışmaya başlama](#gettingstarted)
- [Entity Framework kullanma](#ef)

    - [Entity Framework Code First kullanma](#cf)
    - [Entity Framework Code First Migrations kullanma](#efcfmigrations)
    - [Entity Framework Database First veya Model First (EF Designer) kullanma](#efdbf)
    - [Entity Framework (yavaş yükleme, Eager yüklemesi ve açık yükleme) ile Ilgili verileri yükleme](#efrelateddata)
    - [Entity Framework performansını iyileştirme](#optimizingef)
    - [Entity Framework uygulamasında eşzamanlılık işleme](#efconcurrency)
    - [Entity Framework ilgili kitaplar](#efbooks)
    - [Ek Entity Framework kaynakları](#otherefresources)
- [ASP.NET Web Forms uygulamalarında veri bağlama](#wfdatabinding)

    - [Web Forms model bağlamayı kullanma](#wfmodelbinding)
    - [Web Forms veri kaynağı denetimleri kullanma](#wfdsc)
    - [Web Forms veriye dayalı denetimleri ve veri bağlama Ifadelerini kullanma](#wfdbc)
- [SQL Server veritabanlarıyla çalışma](#sqlserver)

    - [SQL Server Express LocalDB veritabanlarıyla çalışma](#sslocaldb)
    - [SQL Server Express veritabanlarıyla çalışma](#sse)
    - [Windows Azure SQL veritabanı ile çalışma](#ssdb)
    - [SQL Server ve Windows Azure SQL veritabanı arasında seçim yapma](#ssdbchoosing)
- [NoSQL veritabanı yönetim sistemleriyle çalışma](#nosql)
- [ASP.NET uygulamalarında LINQ sorguları kullanma](#linq)
- [Dinamik veri yapı iskelesi kullanma](#dd)
- [Veri erişiminin güvenliğini sağlama](#securing)
- [Veri erişim performansını iyileştirme](#optimizingdataaccess)
- [Veritabanı dağıtma](#deploying)
- [Web hizmeti üzerinden verilere erişme](#webservice)
- [Ek Kaynaklar](#additional)

<a id="gettingstarted"></a>

## <a name="getting-started-with-data-access-in-aspnet"></a>ASP.NET 'de veri erişimi ile çalışmaya başlama

- [Veri depolama seçenekleri (Windows Azure Ile gerçek dünya bulut uygulamaları oluşturma)](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md). Bulut için geliştirme hakkında bir e-kitap bölümü. , İlişkisel veritabanlarına alışkın birçok geliştiricinin fazla görünme eğilimi gösteren bir alternatif olarak NoSQL veritabanlarını tanıtır. İlişkisel veya NoSQL seçerken veya belirli bir platform seçerken ne düşündüğünüzü öğrenmek için yönergeler sunar.
- [ASP.NET veri erişim seçenekleri](https://msdn.microsoft.com/library/ms178359.aspx) (MSDN). ASP.NET için ilişkisel veritabanlarına yönelik veri erişim seçeneklerine giriş ve senaryonuz için uygun platformları ve erişim yöntemlerini seçme kılavuzu.
- [İlişkisel veritabanı](http://en.wikipedia.org/wiki/Relational_database). Vikipedi). İlişkisel veritabanlarıyla çalışmadıysanız, ilişkisel veritabanı terminolojisi ve kavramlarına giriş için bu sayfaya bakın. SQL Server bir giriş için, bu konunun ilerleyen kısımlarında [SQL Server veritabanlarıyla çalışma](#sqlserver) konusuna bakın.

<a id="ef"></a>

## <a name="using-the-entity-framework"></a>Entity Framework kullanma

- [Entity Framework geliştirme yaklaşımları](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf) (MSDN). Entity Framework geliştirme yaklaşımını Database First, Model First veya Code First Seçme Kılavuzu.

<a id="cf"></a>

### <a name="using-entity-framework-code-first"></a>Entity Framework Code First kullanma

Aşağıdaki öğreticiler indirilebilir örnek uygulamalar sunar:

- [MVC 5 kullanarak EF 6 Ile çalışmaya](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)başlama. Bağlantı dayanıklılığı, komut yakaalımı ve zaman uyumsuz gibi geçişler ve EF 6 özellikleri dahil olmak üzere çok sayıda Entity Framework Code First senaryosunu ele alır. Bu, [EF 5/MVC 4 serisinin](../mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)güncelleştirilmiş bir sürümüdür. Önceki seriler, yeni seriye dahil olmayan depo ve iş birimi desenlerine ilişkin bir öğretici içerir.
- [ASP.NET MVC 5 ' e giriş](../mvc/overview/getting-started/introduction/getting-started.md). Daha dar bir Entity Framework Code First senaryosu içerir, ancak MVC özelliklerini tanıtma daha kapsamlı bir işi yapar.
- [Model bağlama ve Web Forms](https://go.microsoft.com/fwlink/?LinkId=286117). Bir Web Forms uygulamasındaki Code First kullanır.
- [ASP.NET 4,5 Web Forms](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)kullanmaya başlama. Code First bir Web Forms kapsamında bir giriş. Model bağlamayı kullanır.
- [MVC müzik deposu](../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1.md). , Üyelik ve yetkilendirme uygulayan bir e-ticaret MVC 3 uygulamasındaki Code First kullanır. Burada kullanılan MVC sürümü ve ASP.NET üyeliği (kimlik doğrulama ve yetkilendirme) sistem güncel değildir; ASP.NET üyeliğiyle ilgili daha güncel bilgiler için bkz. [https://asp.net/identity](https://asp.net/identity).

Diğer kaynaklar:

- [Mevcut bir veritabanına Entity Framework Code First](https://msdn.microsoft.com/data/jj200620). MSDN. Mevcut bir veritabanıyla Code First kullanmayı gösteren video ve İzlenecek yol.
- [Veri Geliştirici Merkezi-Entity Framework](https://msdn.microsoft.com/data/ef). MSDN. Entity Framework ekibi tarafından oluşturulup korunan Entity Framework belgelerine yönelik bir kılavuz için bkz. [Başlarken](https://msdn.microsoft.com/data/ee712907) bağlantısı.

Ayrıca, bu konunun ilerleyen kısımlarında Entity Framework ve [diğer Entity Framework kaynaklarla](#otherefresources) [ilgili kitaplar](#efbooks) bölümüne bakın.

<a id="efcfmigrations"></a>

### <a name="using-entity-framework-code-first-migrations"></a>Entity Framework Code First Migrations kullanma

Yukarıda listelenen Code First öğreticilerin çoğu kapak geçişlerine göre. Ayrıca bkz. aşağıdaki kaynaklar.

- [Visual Studio kullanarak Web dağıtımı ASP.net](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md). bir veritabanını dağıtmak için Code First Migrations kullanmayı gösteren 2 parçalı öğretici serisi.
- [Üyelik, OAuth ve SQL veritabanı ile bir Microsoft Azure Web sitesine güvenli bir ASP.NET MVC 5 uygulaması dağıtın](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Microsoft Azure). Azure 'a üyelik ve uygulama verileri dağıtmak için geçişleri kullanma.
- [Visual Studio ve ASP.net Için Web dağıtımına genel bakış](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment). Code First Migrations Visual Studio Web dağıtım özellikleriyle nasıl tümleştirildiği hakkında bir açıklama için bkz. **Visual Studio 'Da veritabanı dağıtımını yapılandırma** bölümü.
- [Veri Geliştirici Merkezi-Code First Migrations](https://msdn.microsoft.com/data/jj591621) (MSDN). Entity Framework ekibin geçiş belgeleri.
- [Geçişler ekran kaydı serisi](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx). EF blogu). Code First Migrations gelişmiş konularda üç video.
- [ASP.NET Web Pages siteleriyle Code First Migrations](http://www.mikesdotnetting.com/Article/217/Code-First-Migrations-With-ASP.NET-Web-Pages-Sites). Mikesdotnetting blogu). Bir Visual Studio sınıf kitaplığı projesine veri bağlamı yerleştirerek bir ASP.NET Web Pages sitesiyle Code First geçişlerinin nasıl kullanılacağını gösterir.

<a id="efdbf"></a>

### <a name="using-entity-framework-database-first-or-model-first-the-ef-designer"></a>Entity Framework Database First veya Model First (EF Designer) kullanma

- [MVC 5 kullanarak Entity Framework 6 Database First](../mvc/overview/getting-started/database-first-development/setting-up-database.md)kullanmaya başlama. Bir veritabanı oluşturmak için Sunucu Gezgini bir komut dosyası çalıştırın ve sonra veri modelini oluşturmak için Entity Framework tasarımcısını kullanın. Basit CRUD Web sayfaları oluşturmayı gösterir ve diğer veri işleme işlevleri için, tüm EF iş akışları aynı DbContext API 'sini kullandığından Code First öğreticilerden birini izleyebilirsiniz.

Aşağıdaki kaynaklar daha eski. Entity Framework sürüm 4,0 ' i kullanmak istiyorsanız ve Web Forms uygulamasında veri bağlama için bir veri kaynağı denetimi kullanmak istiyorsanız bu faydalıdır.

- [4,0 Entity Framework kullanmaya](../web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)başlama. **EntityDataSource** denetiminin nasıl kullanılacağını gösterir.
- [Entity Framework devam](../web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)etme ( **ObjectDataSource** denetiminin nasıl kullanılacağını gösterir. Eşzamanlılık işleme, EF performansına ilişkin bir öğretici ve EF 4,0 ' deki yenilikler hakkında bir öğretici içerir.

<a id="efrelateddata"></a>

### <a name="handling-related-data-in-entity-framework-lazy-loading-eager-loading-and-explicit-loading"></a>Entity Framework (yavaş yükleme, Eager yüklemesi ve açık yükleme) içindeki ilgili verileri işleme

- [Bir ASP.NET MVC uygulamasındaki Entity Framework Ilgili verileri okuma](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md). Code First, MVC örnek uygulaması. Gösterilen Yöntemler Web Forms model bağlama ve Database First iş akışı için de geçerlidir.
- [Veri Geliştirici Merkezi-Ilgili varlıklar](https://msdn.microsoft.com/data/jj574232) (MSDN) yükleniyor. Entity Framework ekibin ilgili verileri yükleme ile ilgili belgeleri.

<a id="optimizingef"></a>

### <a name="optimizing-entity-framework-performance"></a>Entity Framework performansını iyileştirme

- [Bir ASP.NET uygulamasının gelişmiş Entity Framework senaryoları](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application.md). Kendi SQL deyimlerinizi nasıl yürütekullanacağınızı veya kendi saklı yordamlardan nasıl çağrılacağını, değişiklik algılamayı devre dışı bırakmayı ve değişiklikleri kaydederken doğrulamanın nasıl devre dışı bırakılacağını gösterir.
- [Entity Framework 5 (MSDN) Için performans konuları](https://msdn.microsoft.com/data/hh949853) .
- [Performans konuları (Entity Framework)](https://msdn.microsoft.com/library/cc853327) (MSDN).
- [Bir ASP.NET Web uygulamasındaki Entity Framework performansını](../web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)en üst düzeye çıkarın. Entity Framework 4,0 için geçerlidir.
- Bu konunun ilerleyen kısımlarında Ayrıca bkz. [ASP.NET Data Access 'ı iyileştirme](#optimizingdataaccess) .

<a id="efconcurrency"></a>

### <a name="handling-concurrency-in-an-entity-framework-application"></a>Entity Framework uygulamasında eşzamanlılık işleme

- [Bir ASP.NET MVC uygulamasındaki Entity Framework eşzamanlılık işleme](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md). Code First, DbContext API 'SI, MVC örnek uygulamasını kullanarak.
- [Veri Geliştirici Merkezi – Iyimser eşzamanlılık desenleri](https://msdn.microsoft.com/data/jj592904) (MSDN). Entity Framework ekibin eşzamanlılık belgeleri.
- [Bir ASP.NET Web uygulamasındaki Entity Framework eşzamanlılık işleme](../web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md). Entity Framework 4,0 için geçerlidir. Database First, ObjectContext API 'SI, Web Forms örnek bir uygulama kullanarak.

<a id="efrepository"></a><a id="efbooks"></a>

### <a name="books-about-the-entity-framework"></a>Entity Framework ilgili kitaplar

- [Programlama Entity Framework:](http://shop.oreilly.com/product/0636920022237.do) Julie Lerman ve Rowa Miller tarafından DbContext.
- [Programlama Entity Framework:](http://shop.oreilly.com/product/0636920022220.do) Julie Lerman ve Rowa Miller tarafından Code First.

Bu kitapların her ikisi de geçerli önerilen tekniklerle güncel değildir. Internet 'te bulunan her şeyi Entity Framework daha kapsamlı bir izlemeye daha kolay bir giriş sağlar. Diğer bir kitap olan [programlama Entity Framework](http://shop.oreilly.com/product/9780596807252.do) , Julie Lerman tarafından daha büyük ve daha kapsamlı, ancak daha eski ve kapsamakta olduğu tekniklerin çoğu, Entity Framework kullanmanın önerilen yolu değildir. Ayrıca MSDN sitesindeki [Data Developer Center-books](https://msdn.microsoft.com/data/aa937716) Entity Framework ekibi tarafından önerilen kitaplar listesine bakın.

<a id="otherefresources"></a>

### <a name="other-entity-framework-resources"></a>Diğer Entity Framework kaynakları

- [Entity Framework (ADO.net) ekip blogu](https://blogs.msdn.com/b/adonet/). Yeni geliştirmelerin en güncel bilgileri ve duyuruları için en iyi kaynaklardan biridir. EF ile ilgili diğer blogların [Entity Framework Ile çalışmaya başlama](https://msdn.microsoft.com/data/ee712907)konumundaki blogroll bölümüne bakın.
- [MSDN Dergisi](https://msdn.microsoft.com/magazine/default.aspx). Entity Framework ilgili konular hakkında sık kullanılan **veri noktaları** sütununa bakın.

<a id="wfdatabinding"></a>

## <a name="data-binding-in-aspnet-web-forms-applications"></a>ASP.NET Web Forms uygulamalarında veri bağlama

- [ASP.NET Web Forms veri erişim seçenekleri](https://msdn.microsoft.com/library/jj822927.aspx) (MSDN)<a id="wfmodelbinding"></a>.

<a id="wfmodelbinding"></a>

### <a name="using-web-forms-model-binding"></a>Web Forms model bağlamayı kullanma

- [Model bağlama ve Web Forms](https://go.microsoft.com/fwlink/?LinkId=286117). EF Code First kullanan öğretici serisi.
- [Web Forms model bağlama Bölüm 1: veri seçme](https://weblogs.asp.net/scottgu/archive/2011/09/06/web-forms-model-binding-part-1-selecting-data-asp-net-vnext-series.aspx) (Scott Guthrie 'nin blogu). Bu eski blog gönderilerinde, şu anda ItemType olarak adlandırılan Özellik ModelType olarak adlandırılmıştır, aksi halde içerdikleri bilgiler geçerlidir.
- [Web Forms model bağlama 2. Bölüm: verileri filtreleme](https://weblogs.asp.net/scottgu/archive/2011/09/12/web-forms-model-binding-part-2-filtering-data-asp-net-vnext-series.aspx) (Scott Guthrie 'nin blogu).
- [Web Forms model bağlama bölüm 3: güncelleştirme ve doğrulama](https://weblogs.asp.net/scottgu/archive/2011/10/30/web-forms-model-binding-part-3-updating-and-validation-asp-net-4-5-series.aspx) (Scott Guthrie 'nin blogu).
- [ASP.NET 4,5 Web Forms model bağlama](../web-forms/videos/aspnet-web-forms-vnext/aspnet-45-web-forms-model-binding.md). (video).
- [Model bağlama Bölüm 1-veri seçme](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-1-selecting-data.md) (video).
- [Model bağlama bölüm 2-filtreleme](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-2-filtering.md) (video).
- [ASP.NET 4,5 Web Forms Ile çalışmaya başlama-veri öğelerini ve ayrıntılarını görüntüleme](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md).

<a id="wfdsc"></a>

### <a name="using-web-forms-data-source-controls"></a>Web Forms veri kaynağı denetimleri kullanma

- [Veri kaynağı Web sunucusu denetimleri](https://msdn.microsoft.com/library/ms247258.aspx) (MSDN).
- Entity Framework 6 (Microsoft Web geliştirme blogu) [Için dinamik veri sağlayıcısı ve EntityDataSource denetimi yayını duyuruldu](https://blogs.msdn.com/b/webdev/archive/2014/02/28/announcing-the-release-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx) .

<a id="wfdbc"></a>

### <a name="using-web-forms-data-bound-controls-and-data-binding-expressions"></a>Web Forms veriye dayalı denetimleri ve veri bağlama Ifadelerini kullanma

- [Model bağlama ve Web Forms](https://go.microsoft.com/fwlink/?LinkId=286117). EF Code First kullanan öğretici serisi.
- [ASP.NET 4,5 Web Forms Ile çalışmaya başlama-veri öğelerini ve ayrıntılarını görüntüleme](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md).
- [Kesin tür belirtilmiş veri denetimleri](https://weblogs.asp.net/scottgu/archive/2011/09/02/strongly-typed-data-controls-asp-net-vnext-series.aspx) (Scott Guthrie 'nin blogu).
- [Kesin tür belirtilmiş veri denetimleri](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md) (video).
- [ASP.NET 4,5 Web Forms tanımlayıcı tür belirtilmiş veri denetimleri](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md) (video).
- [Veriye dayalı Web sunucusu denetimleri](https://msdn.microsoft.com/library/ms228214.aspx) (MSDN).
- [Veri bağlama Ifadelerine genel bakış](https://msdn.microsoft.com/library/ms178366.aspx) (MSDN). Bu sayfa yalnızca **eval** ve **bind**'yi içerir; **öğe** ve **bındıtem**dahil olmak üzere güncelleştirilmedi.

<a id="sqlserver"></a>

## <a name="working-with-sql-server-databases"></a>SQL Server veritabanlarıyla çalışma

- [SQL Server veritabanı özellikleri](https://msdn.microsoft.com/library/hh230827.aspx) (MSDN). Çok çeşitli SQL Server konularına genel bir giriş için, TOC 'deki bu girişin altındaki girişlere bakın.
- [SQL Server sürümleri](https://msdn.microsoft.com/library/ms178359.aspx#sqlserver) (MSDN). Kullanılabilir SQL Server sürümlerinin bir özeti, her biri hakkında daha fazla bilgi için bağlantılar sağlar.)
- [ASP.NET Web uygulamaları için SQL Server bağlantı dizeleri](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN).
- [ASP.NET Web uygulamaları için SQL Server Compact kullanma](https://msdn.microsoft.com/library/ms247257.aspx) (MSDN).
- [Microsoft SQL Server: veritabanı ürün örnekleri](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md). Örnek AdventureWorks veritabanları.
- [Örnek veritabanları yükleniyor](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md). Burada gösterilen yöntemlere ek olarak, Sample. mdf dosyalarından birini bir Web projesinin App\_Data klasörüne indirebilir, veritabanını LocalDB 'ye dönüştürebilir ve bir LocalDB bağlantı dizesi oluşturabilirsiniz. Bunun nasıl yapılacağı hakkında bilgi için bkz. [nasıl yapılır: LocalDB 'ye yükseltme](https://msdn.microsoft.com/library/hh873188.aspx).

Ayrıca SQL Server Express ve LocalDB ile çalışma ve SQL Server ile SQL veritabanı arasında seçim yapma hakkında aşağıdaki bölümlere bakın.

<a id="sslocaldb"></a>

### <a name="working-with-sql-server-express-localdb-databases"></a>SQL Server Express LocalDB veritabanlarıyla çalışma

- [SQL Server Express 2012 LocalDB](https://msdn.microsoft.com/library/hh510202(v=sql.110).aspx) (MSDN). LocalDB 'ye yönelik resmi MSDN tanıtımı.
- [ASP.NET Web uygulamaları için SQL Server bağlantı dizeleri](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN).
- [Nasıl yapılır: LocalDB 'ye yükseltme](https://msdn.microsoft.com/library/hh873188.aspx) (MSDN). Bir. mdf dosyasını SQL Server Express önceki bir sürümünden LocalDB 'ye geçirme. Ayrıca, [SQL Server 2012 örnek veritabanlarından](https://go.microsoft.com/fwlink/?linkid=117483)birini indirdiğinizde bu işlemi de ilerleyebilirsiniz.
- [İyileştirilmiş BIR SQL Express](https://go.microsoft.com/fwlink/?LinkId=234375) (SQL Server Express blogu) Ile LocalDB 'ye giriş. LocalDB 'nin oluşturulma nedeni MSDN 'ye dahil olan sürümünden daha fazla arka plan içerir.
- [LocalDB: Veritabanım nerede?](https://go.microsoft.com/fwlink/?LinkId=234376) (SQL Server Express blog). LocalDB veritabanı dosyalarının nerede oluşturulduğu hakkında bilgi.
- [LocalDB 'Yi tam IIS Ile kullanma, 1. Bölüm: Kullanıcı profili](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-1-user-profile.aspx) (SQL Server Express blogu). LocalDB, IIS ile çalışmak üzere tasarlanmamıştır. Bu blog gönderisi dizileri, sorunları ve bazı geçici çözümleri açıklar.

<a id="sse"></a>

### <a name="working-with-sql-server-express-databases"></a>SQL Server Express veritabanlarıyla çalışma

- [ASP.NET Web uygulamaları için SQL Server bağlantı dizeleri](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN). AttachDBFileName bağlantı dizesi ayarını SQL Server Express ile kullanırsanız, bu sayfanın özellikle Kullanıcı örneği bölümüne bakın.
- [Yerel SQL Server Express 2008 (SQL Server Express blogunuzun) sahipliğini alma](https://blogs.msdn.com/b/sqlexpress/archive/2010/02/23/how-to-take-ownership-of-your-local-sql-server-2008-express.aspx) . SQL Server Express örneğinde yönetici olmadığınızdan, yaygın bir sorun SQL Server Express veritabanlarıyla çalışamayacak. Varsayılan olarak, yalnızca SQL Server Express yükleyen kişi bir yöneticiye sahiptir. Bu blog, bilgisayarda bir yöneticiyseniz kendinize bir SQL Server Express Yöneticisi yapmayı açıklar.
- [ASP.NET Web uygulamamın üretimde SQL Server Express veritabanı kullanmasına mi?](https://msdn.microsoft.com/library/jj653753.aspx#sql_express_in_production) (MSDN).

<a id="ssdb"></a>

### <a name="working-with-windows-azure-sql-database"></a>Windows Azure SQL veritabanı ile çalışma

- [Üyelik, OAuth ve SQL veritabanı ile bir Microsoft Azure Web sitesine (Microsoft Azure sitesi) güvenli bir ASP.NET MVC uygulaması dağıtın](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data) .
- [SQL veritabanları](https://docs.microsoft.com/azure/sql-database/) (Microsoft Azure sitesi). Başlarken öğreticileri ve nasıl yapılır kılavuzlarında.
- [Microsoft Azure SQL veritabanı](https://msdn.microsoft.com/library/windowsazure/ee336279.aspx) (MSDN). MSDN 'deki SQL veritabanı için içindekiler tablosunun en üst düzey düğümü.
- [Windows Azure SQL veritabanı TechNet wiki makaleleri dizini](https://social.technet.microsoft.com/wiki/contents/articles/2267.windows-azure-sql-database-technet-wiki-articles-index-en-us.aspx) (Microsoft TechNet sitesi).
- [Geçici hata Işleme uygulama bloğu](https://msdn.microsoft.com/library/hh680934(v=PandP.50).aspx). Azaltmasından kaynaklanan geçici ağ hatalarını ve bağlantı hatalarını idare etmenizi sağlayan bir çerçeve. NuGet paketinde kullanılabilir: [Kurumsal kitaplık 5,0-geçici hata Işleme uygulama bloğu](http://nuget.org/packages/EnterpriseLibrary.WindowsAzure.TransientFaultHandling).
- [SQL veritabanı ve Entity Framework](https://msdn.microsoft.com/data/jj556244) (MSDN) ile çalışmaya başlama.
- [Windows Azure eğitim seti](https://www.microsoft.com/download/details.aspx?id=8396) (Microsoft İndirme Merkezi). SQL veritabanı için uygulamalı laboratuvarlar içerir.
- [Windows Azure SQL veritabanı topluluk Forumu](https://social.msdn.microsoft.com/Forums/ssdsgetstarted/threads).
- [Windows Azure SQL veritabanı 'na](https://msdn.microsoft.com/library/ff803375.aspx) (MSDN) taşınıyor. Microsoft düzenleri ve uygulama ekibi tarafından kapsamlı uçtan uca senaryonun bir bölümü. ' Dan SQL veritabanı 'na geçiş yapmak isteyebileceğiniz ve SQL Server neden geçirmek istediğinizi ele alır.
- [SQL Server veritabanlarını Windows Azure SQL veritabanı 'na](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx) (MSDN) geçirme.
- [SQL veritabanı geçiş Sihirbazı](http://sqlazuremw.codeplex.com/). Veritabanlarını SQL veritabanına geçirmek için açık kaynak bir araç.

<a id="ssdbchoosing"></a>

### <a name="choosing-between-sql-server-and-windows-azure-sql-database"></a>SQL Server ve Windows Azure SQL veritabanı arasında seçim yapma

- [SQL Server Windows Azure SQL veritabanı Ile karşılaştırın](https://social.technet.microsoft.com/wiki/contents/articles/996.compare-sql-server-with-windows-azure-sql-database-en-us.aspx) (Microsoft TechNet sitesi).
- [Windows Azure SQL veritabanı 'Na veri geçişi: Araçlar ve teknikler](https://msdn.microsoft.com/library/windowsazure/hh694043.aspx) (MSDN). SQL Server SQL veritabanıyla karşılaştıran ve SQL Server SQL veritabanı 'na ne zaman geçiş yapacağınız hakkında rehberlik sağlayan bölümler içerir.
- [Windows Azure SQL veritabanı teslim Kılavuzu](https://social.technet.microsoft.com/wiki/contents/articles/3398.windows-azure-sql-database-delivery-guide-en-us.aspx) (Microsoft TechNet sitesi).
- [SQL Server özellik sınırlamaları (Microsoft Azure SQL veritabanı)](https://msdn.microsoft.com/library/windowsazure/ff394115.aspx) (MSDN).
- [Windows Azure Tablo depolama ve Windows Azure SQL veritabanı-karşılaştırılan ve değişken maliyetli](https://msdn.microsoft.com/library/jj553018.aspx) (MSDN). Windows Azure 'a dağıttığınız bir uygulama için, Microsoft Azure Tablo depolama, Microsoft Azure SQL veritabanı 'na bir alternatif olabilir. Bu konu, bu alternatifler arasında karar vermenize yardımcı olur.
- [Microsoft Azure SQL veritabanı](https://msdn.microsoft.com/library/windowsazure/ee336279) (MSDN).
- [Yönergeler ve sınırlamalar (Microsoft Azure SQL veritabanı)](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)

<a id="nosql"></a>

## <a name="working-with-nosql-database-management-systems"></a>NoSQL veritabanı yönetim sistemleriyle çalışma

- [Windows Azure veri Hizmetleri](https://www.windowsazure.com/develop/net/data/) (Microsoft Azure sitesi). Sayfanın [Tablo hizmeti özellik kılavuzuna](https://docs.microsoft.com/azure/) ve **büyük veri** bölümüne bakın.
- [Depolama tabloları, kuyrukları ve Blobları (Microsoft Azure Site) kullanarak çok katmanlı uygulama ASP.net](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36) . Windows Azure Storage NoSQL tablolarını kullanan indirilebilir örnek uygulamayla uçtan uca öğretici.

<a id="linq"></a>

## <a name="using-linq-queries-in-aspnet-applications"></a>ASP.NET uygulamalarında LINQ sorguları kullanma

- [ASP.NET veri erişim seçenekleri](https://msdn.microsoft.com/library/ms178359.aspx#linq) (MSDN). LINQ 'e giriş içerir.
- [LINQ eğitim videoları](http://www.misfitgeek.com/windows-client-linq-training-videos-20/) (ali Stagner blogu).
- [Dınamık LINQ kaynaklarına yönelik bağlantılarla ASP.net Forum iş parçacığı](https://forums.asp.net/p/1961037/5601994.aspx?Please+suggest+good+books+so+that+one+can+write+and+understand+dynamic+linq).

<a id="dd"></a>

## <a name="using-dynamic-data-scaffolding"></a>Dinamik veri yapı Iskelesi kullanma

- [Dinamik veri projesi şablonları](https://msdn.microsoft.com/library/jj822927.aspx#dynamicdata) (MSDN). Dinamik veri projelerinin ne zaman kullanılacağı hakkında rehberlik.
- [ASP.NET dinamik verileri](https://msdn.microsoft.com/library/ee845452.aspx) (MSDN).

<a id="securing"></a>

## <a name="securing-data-access"></a>Veri erişiminin güvenliğini sağlama

- ASP.NET (MSDN) [' de veri erişiminin güvenliğini sağlama](https://msdn.microsoft.com/library/ms178375.aspx) .
- [Güvenlik konuları (Entity Framework)](https://msdn.microsoft.com/library/cc716760.aspx) (MSDN).
- [Nasıl yapılır: veri kaynağı denetimleri (MSDN) kullanırken bağlantı dizelerini güvenli hale getirme](https://msdn.microsoft.com/library/ms178372.aspx) .

<a id="optimizingdataaccess"></a>

## <a name="optimizing-data-access-performance"></a>Veri erişim performansını iyileştirme

- [ASP.net performansına genel bakış](https://msdn.microsoft.com/library/cc668225.aspx) (MSDN).
- [ASP.NET önbelleğe alma](https://msdn.microsoft.com/library/xsbfdd8c.aspx) (MSDN).
- [ASP.net performansını geliştirme](https://msdn.microsoft.com/library/ff647787) (MSDN). Bu sayfanın üst kısmında "kullanımdan kaldırılan Içerik" uyarısı bulunur, ancak bilgilerin çoğu hala ilgilidir ve karşılaştırılabilir güncelleştirilmiş bir kaynak yoktur.
- [SQL Server performansını artırma](https://msdn.microsoft.com/library/ff647793) (MSDN). Önceki bağlantıyla aynı açıklama.

Ayrıca bkz. bu konuda daha önce [Entity Framework performansını En Iyi duruma getirme](#optimizingef) .

<a id="deploying"></a>

## <a name="deploying-a-database"></a>Veritabanı dağıtma

- [ASP.NET Web dağıtımı-önerilen kaynaklar](aspnet-web-deployment-content-map.md) (MSDN).

<a id="webservice"></a>

## <a name="accessing-data-through-a-web-service"></a>Web hizmeti üzerinden verilere erişme

- [Web hizmeti (MSDN) üzerinden verilere erişme](https://msdn.microsoft.com/library/ms178359.aspx#webservice) . Web API ve WCF için ne zaman kullanılacağı konusunda rehberlik.
- [ASP.NET Web API 'si Ile çalışmaya](../web-api/index.md)başlama.
- [WCF veri Hizmetleri](https://msdn.microsoft.com/data/bb931106) (MSDN).

<a id="additional"></a>

## <a name="additional-resources"></a>Ek Kaynaklar

- [ASP.NET veri ERIŞIMI SSS](https://msdn.microsoft.com/library/jj653753.aspx) (MSDN).
- [ASP.NET Web Forms öğreticileri-veriler](../web-forms/overview/data-access/index.md). Bu öğreticilerin çoğu nispeten eski; senaryonuza doğru olmayan bir veri erişim yöntemine çok fazla bilgi alabilmek için, önce [ASP.NET veri erişim seçeneklerini](https://msdn.microsoft.com/library/ms178359.aspx) ve [veri depolama seçeneklerini (Windows Azure Ile gerçek hayatta bulut uygulamaları oluşturun)](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md) okuduğunuzdan emin olun.
- [ASP.NET MVC Içerik Haritası](../mvc/overview/getting-started/recommended-resources-for-mvc.md).
- [ASP.NET Web sayfaları öğreticileri-veriler](../web-pages/overview/data/index.md).
- [Visual Studio 'Da verilere erişme](https://msdn.microsoft.com/library/wzabh8c4.aspx) (MSDN). Bu içerik haritasına benzer ancak ASP.NET yerine Visual Studio üzerinde odaklanmış bir bağlantı listesi sağlar.
