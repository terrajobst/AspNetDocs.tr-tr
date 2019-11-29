---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/debugging-stored-procedures-vb
title: Saklı yordamların hatalarını ayıklama (VB) | Microsoft Docs
author: rick-anderson
description: Visual Studio Professional ve Team System sürümleri, SQL Server içindeki saklı yordamlar için kesme noktaları ve adım adım ayarlamanıza olanak tanır...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 9ed8ccb5-5f31-4eb4-976d-cabf4b45ca09
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/debugging-stored-procedures-vb
msc.type: authoredcontent
ms.openlocfilehash: 13d213ef4baf493a4f05a82daae8d2dc3b0aa61b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74604552"
---
# <a name="debugging-stored-procedures-vb"></a>Saklı Yordamların Hatalarını Ayıklama (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_74_VB.zip) veya [PDF 'yi indirin](debugging-stored-procedures-vb/_static/datatutorial74vb1.pdf)

> Visual Studio Professional ve Team System sürümleri, SQL Server içindeki saklı yordamlar için kesme noktaları ve adım adım ayarlamanıza olanak tanır. Bu öğreticide, doğrudan veritabanı hata ayıklaması ve saklı yordamların uygulama hata ayıklaması gösterilmektedir.

## <a name="introduction"></a>Giriş

Visual Studio, zengin bir hata ayıklama deneyimi sağlar. Birkaç tuş vuruşu veya fareyi tıklamasıyla, bir programın yürütülmesini durdurmak ve durumunu ve denetim akışını incelemek için kesme noktaları kullanmak mümkündür. Visual Studio, uygulama kodu hata ayıklamayla birlikte SQL Server içinden saklı yordamları hata ayıklama desteği sunar. Tıpkı kesme noktaları, bir ASP.NET arka plan kodu sınıfı veya Iş mantığı katman sınıfının kodu içinde ayarlanabilir, bu nedenle saklı yordamların içine yerleştirilebilecek.

Bu öğreticide, Visual Studio 'daki Sunucu Gezgini saklı yordamlara adımlamayı ve saklı yordam çalışan ASP.NET uygulamasından çağrıldığında isabet kesme noktalarını ayarlamayı inceleyeceğiz.

> [!NOTE]
> Ne yazık ki, saklı yordamlar yalnızca Visual Studio 'nun Professional ve Team Systems sürümlerinde bulunabilir ve hata ayıklanamaz. Visual Web Developer veya Visual Studio 'nun standart sürümünü kullanıyorsanız, saklı yordamların hatalarını ayıklamak için gerekli olan adımlara yol gösterecek şekilde okumaya hoş geldiniz, ancak bu adımları makinenizde çoğaltabileceksiniz.

## <a name="sql-server-debugging-concepts"></a>SQL Server hata ayıklama kavramları

Microsoft SQL Server 2005, tüm .NET derlemeleri tarafından kullanılan çalışma zamanı olan [ortak dil çalışma zamanı (CLR)](https://msdn.microsoft.com/netframework/aa497266.aspx)ile tümleştirme sağlamak üzere tasarlanmıştır. Sonuç olarak, SQL Server 2005 yönetilen veritabanı nesnelerini destekler. Diğer bir deyişle, bir Visual Basic sınıfında yöntemler olarak saklı yordamlar ve Kullanıcı tanımlı Işlevler (UDF 'ler) gibi veritabanı nesneleri oluşturabilirsiniz. Bu, bu saklı yordamların ve UDF 'ların .NET Framework ve kendi özel sınıflarınızda işlevselliği kullanmasına olanak sağlar. Elbette SQL Server 2005, T-SQL veritabanı nesneleri için de destek sağlar.

SQL Server 2005, T-SQL ve yönetilen veritabanı nesneleri için hata ayıklama desteği sunar. Ancak, bu nesnelere yalnızca Visual Studio 2005 Professional ve Team Systems sürümlerinde hata ayıklanabilir. Bu öğreticide, hata ayıklama T-SQL veritabanı nesneleri anlatılmaktadır. Sonraki öğretici, yönetilen veritabanı nesnelerinde hata ayıklama işlemini inceler.

[SQL Server 2005 CLR Integration ekibinin](https://blogs.msdn.com/sqlclr/default.aspx) [SQL Server 2005 blog GIRIŞINDE T-SQL ve clr hata ayıklamasına genel bakış](https://blogs.msdn.com/sqlclr/archive/2006/06/29/651644.aspx) , Visual Studio 'dan SQL Server 2005 nesnelerinde hata ayıklamanın üç yolunu vurgular:

- **Doğrudan veritabanı hata ayıklaması (DDD)** -Sunucu Gezgini, saklı yordamlar ve UDF 'ler gibi herhangi bir T-SQL veritabanı nesnesine ilerliyoruz. Adım 1 ' de DDD ' i inceleyeceğiz.
- **Uygulama hata ayıklaması** -bir veritabanı nesnesi içinde kesme noktaları ayarlayabiliyoruz ve sonra ASP.net uygulamamızı çalıştırabiliriz. Veritabanı nesnesi yürütüldüğünde, kesme noktasına isabet edilir ve denetim hata ayıklayıcıya açılır. Uygulama hata ayıklaması ile uygulama kodundan bir veritabanı nesnesine ilerliyoruz. Hata ayıklayıcının durdurulmasını istediğimiz, bu saklı yordamlarda veya UDF 'de açıkça kesme noktaları ayarlamanız gerekir. Uygulama hata ayıklaması adım 2 ' den başlayarak incelenir.
- **SQL Server projeden hata ayıklama** -Visual Studio Professional ve ekip sistemleri sürümleri, yönetilen veritabanı nesneleri oluşturmak için yaygın olarak kullanılan bir SQL Server proje türü içerir. SQL Server projelerini kullanarak bir sonraki öğreticide içeriklerinin hatalarını ayıklacağız.

Visual Studio, yerel ve uzak SQL Server örneklerinde saklı yordamların hatalarını ayıklayabilir. Yerel bir SQL Server örneği, Visual Studio ile aynı makineye yüklenmiş biridir. Kullanmakta olduğunuz SQL Server veritabanı geliştirme makinenizde bulunmuyorsa, uzak bir örnek olarak kabul edilir. Bu öğreticiler için yerel SQL Server örnekleri kullandık. Uzak bir SQL Server örneğinde saklı yordamların hata ayıklaması, yerel bir örnekteki saklı yordamların hata ayıklamasının dışında daha fazla yapılandırma adımı gerektirir.

Yerel bir SQL Server örneği kullanıyorsanız, 1. adımla başlayabilir ve bu öğreticiden sonuna kadar çalışabilirsiniz. Ancak uzak bir SQL Server örneği kullanıyorsanız, ilk olarak hata ayıklama sırasında, uzak örnekte SQL Server bir oturum açmaya sahip bir Windows kullanıcı hesabıyla geliştirme makinenize oturum açtığınızı doğrulayın. Üstelik, çalışan ASP.NET uygulamasından veritabanına bağlanmak için kullanılan bu veritabanı oturum açma ve veritabanı oturum açmanın `sysadmin` rolün üyesi olması gerekir. Visual Studio 'Yu yapılandırma hakkında daha fazla bilgi için ve uzak bir örnekte hata ayıklamak üzere SQL Server, Bu öğreticinin sonundaki uzak örneklerdeki hata ayıklama T-SQL veritabanı nesneleri bölümüne bakın.

Son olarak, T-SQL veritabanı nesneleri için hata ayıklama desteğinin, .NET uygulamaları için hata ayıklama desteği olarak zengin özellik olarak olduğunu anlayın. Örneğin, kesme noktası koşulları ve filtreleri desteklenmez, yalnızca hata ayıklama pencerelerinin bir alt kümesi kullanılabilir; Düzenle ve devam et kullanamazsınız, acil pencere kullanılamaz ve bu şekilde işlenir. Daha fazla bilgi için bkz. [hata ayıklayıcı komutlarında ve özelliklerinde sınırlamalar](https://msdn.microsoft.com/library/ms165035(VS.80).aspx) .

## <a name="step-1-directly-stepping-into-a-stored-procedure"></a>1\. Adım: doğrudan bir saklı yordama adımla

Visual Studio, bir veritabanı nesnesinin doğrudan hata ayıklamasını kolaylaştırır. Northwind veritabanında `Products_SelectByCategoryID` saklı yordamın içine geçmek için doğrudan veritabanı hata ayıklama (DDD) özelliğinin nasıl kullanılacağına göz atalım. Adından da anlaşılacağı gibi, `Products_SelectByCategoryID` belirli bir kategori için ürün bilgilerini döndürür; [yazılan veri kümesi s TableAdapters öğreticisi Için mevcut saklı yordamlar kullanılarak](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) oluşturulmuştur. Sunucu Gezgini giderek başlayın ve Northwind veritabanı düğümünü genişletin. Ardından, saklı yordamlar klasörünün detayına gidin, `Products_SelectByCategoryID` saklı yordamına sağ tıklayın ve bağlam menüsünde saklı yordam seçeneğine adımla seçeneğini belirleyin. Bu işlem hata ayıklayıcıyı başlatır.

`Products_SelectByCategoryID` saklı yordamı bir `@CategoryID` giriş parametresi beklediği için, bu değeri sağlamamız istenir. İçecek hakkında bilgi döndüren 1 yazın.

![@CategoryID parametresi için 1 değerini kullanın](debugging-stored-procedures-vb/_static/image1.png)

**Şekil 1**: `@CategoryID` parametresi Için 1 değerini kullanın

`@CategoryID` parametresi için değer verdikten sonra, saklı yordam yürütülür. , Ancak tamamlanmayı çalıştırmak yerine, hata ayıklayıcı ilk ifadede yürütmeyi halden çıkarır. Kenar boşluğunda, saklı yordamdaki geçerli konumu belirten Sarı oka göz önünde bulundurma. İzleme penceresi veya saklı yordamdaki parametre adının üzerine gelerek parametre değerlerini görüntüleyebilir ve düzenleyebilirsiniz.

[Hata ayıklayıcının, saklı yordamın Ilk Ifadesinde durdurdu ![](debugging-stored-procedures-vb/_static/image3.png)](debugging-stored-procedures-vb/_static/image2.png)

**Şekil 2**: hata ayıklayıcı saklı yordamın Ilk ifadesinde durdu ([tam boyutlu görüntüyü görüntülemek için tıklayın](debugging-stored-procedures-vb/_static/image4.png))

Saklı yordamı tek seferde bir deyime göre ilerlemek için, araç çubuğundaki adımla düğmesine tıklayın veya F10 tuşuna basın. `Products_SelectByCategoryID` saklı yordamı tek bir `SELECT` ifadesini içerir, bu nedenle F10 'e vurarak tek deyimin üzerinde adım adım olur ve saklı yordamın yürütülmesi tamamlanır. Saklı yordam tamamlandıktan sonra çıktısı çıkış penceresinde görünür ve hata ayıklayıcı sonlandırılır.

> [!NOTE]
> T-SQL hata ayıklama, ifade düzeyinde oluşur; `SELECT` ifadeye ilerlenemez.

## <a name="step-2-configuring-the-website-for-application-debugging"></a>2\. Adım: uygulama hata ayıklaması için Web sitesini yapılandırma

Saklı yordamda doğrudan Sunucu Gezgini hata ayıklaması yaparken, ASP.NET uygulamamızda çağrıldığında, saklı yordamda hata ayıklamayla ilgili birçok senaryoda daha fazla senaryo olması yararlı olur. Visual Studio içinden bir saklı yordama kesme noktaları ekleyebiliriz ve sonra ASP.NET uygulamasında hata ayıklamaya başlayabilirsiniz. Uygulamadan kesme noktaları olan bir saklı yordam çağrıldığında, yürütme kesme noktasında durabilir ve 1. adımda yaptığımız gibi, saklı yordamın parametre değerlerini görüntüleyip değiştirebiliyoruz ve deyimlerini adım adım izleyebilirsiniz.

Uygulamadan çağrılan saklı yordamları hata ayıklamaya başlayabilmemiz için, ASP.NET Web uygulamasına SQL Server hata ayıklayıcı ile tümleştirileceğini söylemek istiyoruz. Çözüm Gezgini (`ASPNET_Data_Tutorial_74_VB`) Web sitesinin adına sağ tıklayıp başlatın. Bağlam menüsünden Özellik sayfaları seçeneğini belirleyin, sol taraftaki başlangıç seçenekleri öğesini seçin ve hata ayıklayıcıları bölümündeki SQL Server onay kutusunu işaretleyin (bkz. Şekil 3).

[Uygulama ![özellik sayfalarındaki SQL Server onay kutusunu Işaretleyin](debugging-stored-procedures-vb/_static/image6.png)](debugging-stored-procedures-vb/_static/image5.png)

**Şekil 3**: uygulama öğeleri özellik sayfalarındaki SQL Server onay kutusunu işaretleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](debugging-stored-procedures-vb/_static/image7.png))

Ayrıca, bağlantı havuzunun devre dışı bırakılması için uygulama tarafından kullanılan veritabanı bağlantı dizesini güncelleştirmemiz gerekir. Bir veritabanına bağlantı kapatıldığında, karşılık gelen `SqlConnection` nesnesi kullanılabilir bir bağlantı havuzuna yerleştirilir. Bir veritabanına bağlantı kurarken, yeni bir bağlantı oluşturmak ve kurmak zorunda kalmak yerine, kullanılabilir bir bağlantı nesnesi bu havuzdan alınabilir. Bu bağlantı nesneleri havuzu bir performans geliştirmedir ve varsayılan olarak etkindir. Ancak, hata ayıklarken hata ayıklama altyapısı havuzdan alınan bir bağlantıyla çalışırken doğru şekilde yeniden kurulmadığı için bağlantı havuzunu kapatmak istiyoruz.

Bağlantı kuyruğunu devre dışı bırakmak için, `Web.config` `NORTHWNDConnectionString` `Pooling=false` ayarını içerecek şekilde güncelleştirin.

[!code-xml[Main](debugging-stored-procedures-vb/samples/sample1.xml)]

> [!NOTE]
> ASP.NET uygulaması aracılığıyla SQL Server hata ayıklamayı tamamladıktan sonra, `Pooling` ayarını bağlantı dizesinden kaldırarak (veya `Pooling=true` olarak ayarlayarak) bağlantı havuzunu yeniden devreye sokduğunuzdan emin olun.

Bu noktada, ASP.NET uygulaması, Web uygulaması aracılığıyla çağrıldığında, Visual Studio 'Nun SQL Server veritabanı nesnelerinde hata ayıklamasına izin verecek şekilde yapılandırılmıştır. Artık kalan işlemler, saklı yordama bir kesme noktası eklemek ve hata ayıklamayı başlatacak!

## <a name="step-3-adding-a-breakpoint-and-debugging"></a>3\. Adım: kesme noktası ve hata ayıklama ekleme

`Products_SelectByCategoryID` saklı yordamını açın ve uygun yerdeki kenar boşluğuna tıklayarak ya da imlecinizi `SELECT` deyimin başlangıcında yerleştirip F9 tuşuna basarak `SELECT` deyimin başlangıcında bir kesme noktası ayarlayın. Şekil 4 ' te gösterildiği gibi, kesme noktası kenar boşluğunda kırmızı bir daire olarak görünür.

[Products_SelectByCategoryID saklı yordamında bir kesme noktası ayarlamak ![](debugging-stored-procedures-vb/_static/image9.png)](debugging-stored-procedures-vb/_static/image8.png)

**Şekil 4**: `Products_SelectByCategoryID` saklı yordamında bir kesme noktası ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](debugging-stored-procedures-vb/_static/image10.png))

Bir SQL veritabanı nesnesinin hata ayıklaması için bir istemci uygulama aracılığıyla ayıklanmak üzere, veritabanının uygulama hata ayıklamasını destekleyecek şekilde yapılandırılması zorunludur. İlk olarak bir kesme noktası ayarladığınızda, bu ayarın otomatik olarak ayarlanması gerekir, ancak bu ayar, iki kez denetim altına alınmıştır. Sunucu Gezgini `NORTHWND.MDF` düğümüne sağ tıklayın. Bağlam menüsü, uygulama hata ayıklaması adlı işaretli bir menü öğesi içermelidir.

![Uygulama hata ayıklama seçeneğinin etkinleştirildiğinden emin olun](debugging-stored-procedures-vb/_static/image11.png)

**Şekil 5**: uygulama hata ayıklama seçeneğinin etkinleştirildiğinden emin olun

Kesme noktası kümesi ve uygulama hata ayıklama seçeneği etkinken, ASP.NET uygulamasından çağrıldığında saklı yordamda hata ayıklamaya hazırız. Hata ayıklama menüsüne gidip hata ayıklamayı Başlat ' ı seçerek, F5 tuşuna basarak veya araç çubuğundaki yeşil yürütme simgesine tıklayarak hata ayıklayıcıyı başlatın. Bu işlem hata ayıklayıcıyı başlatacak ve Web sitesini başlatacaktır.

`Products_SelectByCategoryID` saklı yordamı, [yazılan veri kümesi s TableAdapters öğreticisi Için mevcut saklı yordamlar kullanılarak](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) oluşturulmuştur. Karşılık gelen Web sayfası (`~/AdvancedDAL/ExistingSprocs.aspx`), bu saklı yordam tarafından döndürülen sonuçları görüntüleyen bir GridView içerir. Tarayıcı aracılığıyla bu sayfayı ziyaret edin. Sayfaya ulaştıktan sonra, `Products_SelectByCategoryID` saklı yordamdaki kesme noktasına isabet edilir ve bu denetim Visual Studio 'ya döndürülür. 1\. adımda olduğu gibi, saklı yordam deyimlerini kullanarak, parametre değerlerini görüntüleyebilir ve değiştirebilirsiniz.

[ExistingSprocs. aspx sayfasında Ilk olarak Içecek görüntülenir ![](debugging-stored-procedures-vb/_static/image13.png)](debugging-stored-procedures-vb/_static/image12.png)

**Şekil 6**: `ExistingSprocs.aspx` sayfası başlangıçta alkolu görüntüler ([tam boyutlu görüntüyü görüntülemek için tıklayın](debugging-stored-procedures-vb/_static/image14.png))

[![saklı yordam kesme noktasına ulaşıldı](debugging-stored-procedures-vb/_static/image16.png)](debugging-stored-procedures-vb/_static/image15.png)

**Şekil 7**: saklı yordam kesme noktasına ulaşıldı ([tam boyutlu görüntüyü görüntülemek için tıklayın](debugging-stored-procedures-vb/_static/image17.png))

Şekil 7 ' deki izleme penceresi gösterdiği gibi, `@CategoryID` parametresinin değeri 1 ' dir. Bunun nedeni, `ExistingSprocs.aspx` sayfanın başlangıçta `CategoryID` değeri 1 olan içecek kategorisindeki ürünleri görüntülemektedir. Açılan listeden farklı bir kategori seçin. Bunun yapılması geri göndermeye neden olur ve `Products_SelectByCategoryID` saklı yordamını yeniden yürütür. Kesme noktası bir kez daha, ancak bu kez `@CategoryID` parametresi değeri seçili aşağı açılan liste öğesi s `CategoryID`yansıtır.

[![aşağı açılan listeden farklı bir kategori seçin](debugging-stored-procedures-vb/_static/image19.png)](debugging-stored-procedures-vb/_static/image18.png)

**Şekil 8**: açılan listeden farklı bir kategori seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](debugging-stored-procedures-vb/_static/image20.png))

[![@CategoryID parametresi, Web sayfasından Seçilen kategoriyi yansıtır](debugging-stored-procedures-vb/_static/image22.png)](debugging-stored-procedures-vb/_static/image21.png)

**Şekil 9**: `@CategoryID` parametresi, Web sayfasından Seçilen kategoriyi yansıtır ([tam boyutlu görüntüyü görüntülemek için tıklayın](debugging-stored-procedures-vb/_static/image23.png))

> [!NOTE]
> `ExistingSprocs.aspx` sayfasını ziyaret ederken `Products_SelectByCategoryID` saklı yordamdaki kesme noktası isabet ettirilmediğinde, SQL Server onay kutusunun ASP.NET uygulama özellikleri sayfasının hata ayıklayıcıları bölümünde işaretli olduğundan emin olun, bu bağlantı havuzu oluşturma devre dışı bırakıldı ve veritabanı uygulama hata ayıklama seçeneğinin etkin olduğundan emin olun. Hala sorun yaşıyorsanız, Visual Studio 'Yu yeniden başlatıp tekrar deneyin.

## <a name="debugging-t-sql-database-objects-on-remote-instances"></a>Uzak örneklerde T-SQL veritabanı nesnelerinde hata ayıklama

SQL Server veritabanı örneği Visual Studio ile aynı makineli olduğunda, Visual Studio aracılığıyla veritabanı nesnelerinin hatalarını ayıklama oldukça basittir. Ancak, SQL Server ve Visual Studio farklı makinelerde bulunuyorsa, her şeyin düzgün şekilde çalışmasını sağlamak için bazı dikkatli bir yapılandırma gerekir. Karşılaştığı iki temel görev vardır:

- ADO.NET aracılığıyla veritabanına bağlanmak için kullanılan oturumun `sysadmin` rolüne ait olduğundan emin olun.
- Geliştirme makinesinde Visual Studio tarafından kullanılan Windows Kullanıcı hesabının, `sysadmin` rolüne ait geçerli bir SQL Server oturum açma hesabı olduğundan emin olun.

İlk adım nispeten basittir. İlk olarak, ASP.NET uygulamasından veritabanına bağlanmak için kullanılan Kullanıcı hesabını belirleyip SQL Server Management Studio ' den bu oturum açma hesabını `sysadmin` rolüne ekleyin.

İkinci görev, uygulamanın hatalarını ayıklamak için kullandığınız Windows Kullanıcı hesabının uzak veritabanında geçerli bir oturum açma olması gerekir. Ancak, iş istasyonunuzda oturum açtığınız Windows hesabı, SQL Server üzerinde geçerli bir oturum değil. SQL Server için belirli bir oturum açma hesabınızı eklemek yerine, bazı Windows Kullanıcı hesaplarını SQL Server hata ayıklama hesabı olarak belirlemek daha iyi bir seçimdir. Ardından, uzak bir SQL Server örneğinin veritabanı nesnelerinde hata ayıklaması yapmak için, Windows oturum açma hesabı s kimlik bilgilerini kullanarak Visual Studio 'Yu çalıştırırsınız.

Bir örnek, şeyleri açıklığa kavuşturmasına yardımcı olmalıdır. Windows etki alanı içinde `SQLDebug` adlı bir Windows hesabı olduğunu düşünün. Bu hesabın, uzak SQL Server örneğine geçerli bir oturum açma ve `sysadmin` rolünün bir üyesi olarak eklenmesi gerekir. Daha sonra Visual Studio 'da uzak SQL Server örneğinde hata ayıklamak için, Visual Studio 'Yu `SQLDebug` Kullanıcı olarak çalıştırmanız gerekir. Bu işlem iş istasyonumuzu günlüğe kaydederek, `SQLDebug`olarak yeniden oturum açarak ve sonra Visual Studio 'yu başlatarak, iş istasyonumuzdan kendi kimlik bilgilerinizle oturum açıp `SQLDebug` Kullanıcı olarak Visual Studio 'Yu başlatmak için `runas.exe` kullanmaktan daha basit bir yaklaşım olabilir. `runas.exe`, belirli bir uygulamanın farklı bir kullanıcı hesabının GUISE altında yürütülmesini sağlar. Visual Studio 'Yu `SQLDebug`olarak başlatmak için komut satırına aşağıdaki ifadeyi girebilirsiniz:

[!code-console[Main](debugging-stored-procedures-vb/samples/sample2.cmd)]

Bu işlemle ilgili daha ayrıntılı bir açıklama için, bkz. [William R. Vaughn](http://betav.com/BLOG/billva/) s *Hitchhiker s Guide for Visual Studio ve SQL Server, yedinci sürüm ve* [hata ayıklama için SQL Server izinleri ayarlama](https://msdn.microsoft.com/library/w1bhybwz(VS.80).aspx).

> [!NOTE]
> Geliştirme makineniz Windows XP Service Pack 2 çalıştırıyorsa, Internet bağlantısı güvenlik duvarını uzaktan hata ayıklamaya izin verecek şekilde yapılandırmanız gerekir. [Nasıl yapılır: etkinleştirme SQL Server 2005 hata ayıklama](https://msdn.microsoft.com/library/s0fk6z6e(VS.80).aspx) makalesinde, Visual Studio konak makinesinde iki adım vardır: (a), özel durumlar listesine `Devenv.exe` eklemenız ve TCP 135 bağlantı noktasını açmanız gerekir. ve (b) uzak (SQL) makinede, TCP 135 bağlantı noktasını açmanız ve özel durumlar listesine `sqlservr.exe` eklemeniz gerekir. Etki alanı ilkeniz IPSec üzerinden ağ iletişimi yapılmasını gerektiriyorsa, UDP 4500 ve UDP 500 bağlantı noktalarını açmanız gerekir.

## <a name="summary"></a>Özet

Visual Studio, .NET uygulama kodu için hata ayıklama desteği sağlamaya ek olarak SQL Server 2005 için çeşitli hata ayıklama seçenekleri de sağlar. Bu öğreticide, bu seçeneklerden ikisini de inceledik: doğrudan veritabanı hata ayıklaması ve uygulama hata ayıklaması. T-SQL veritabanı nesnesinde doğrudan hata ayıklamak için, Sunucu Gezgini nesneyi bulun, sonra sağ tıklayıp adımla ' yı seçin. Bu, hata ayıklayıcıyı ve veritabanı nesnesindeki ilk deyimde halleri başlatır. bu noktada, nesne s deyimlerinde adım adım ve parametre değerlerini görüntüleyebilir ve değiştirebilirsiniz. Adım 1 ' de bu yaklaşımı `Products_SelectByCategoryID` saklı yordamının içine adımla kullandık.

Uygulama hata ayıklaması, kesme noktalarının doğrudan veritabanı nesneleri içinde ayarlamaya izin verir. Kesme noktaları olan bir veritabanı nesnesi bir istemci uygulamasından çağrıldığında (örneğin, bir ASP.NET Web uygulaması), program hata ayıklayıcı üzerinde sürer. Uygulama hata ayıklaması, belirli bir veritabanı nesnesinin çağrılmasına neden olan uygulama eylemini daha açık bir şekilde gösterdiği için yararlıdır. Ancak, doğrudan veritabanı hata ayıklamadan biraz daha fazla yapılandırma ve kurulum gerektirir.

Veritabanı nesneleri SQL Server projeler aracılığıyla da hata ayıklanabilir. SQL Server projelerini ve bir sonraki öğreticide yönetilen veritabanı nesneleri oluşturmak ve hatalarını ayıklamak için bunları nasıl kullanacağınızı inceleyeceğiz.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

> [!div class="step-by-step"]
> [Önceki](protecting-connection-strings-and-other-configuration-information-vb.md)
> [İleri](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb.md)
