---
uid: web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-vb
title: SQL Server üyelik şeması oluşturma (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğretici, SqlMembershipProvider kullanmak için gerekli şemayı veritabanına ekleme tekniklerini inceleyerek başlar. Bunu izleyerek Wi...
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 112a674d-716f-41a6-99b8-4074d65a54c0
msc.legacyurl: /web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-vb
msc.type: authoredcontent
ms.openlocfilehash: 96fd72d1f368b1f7947ef0a2293161d97aaf7065
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74581008"
---
# <a name="creating-the-membership-schema-in-sql-server-vb"></a>SQL Server’da Üyelik Şeması Oluşturma (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_04_VB.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial04_MembershipSetup_vb.pdf)

> Bu öğretici, SqlMembershipProvider kullanmak için gerekli şemayı veritabanına ekleme tekniklerini inceleyerek başlar. Bunu izleyerek, şemadaki anahtar tabloları inceleyecek ve amaçlarını ve önemini tartışacağız. Bu öğretici, üyelik çerçevesinin hangi sağlayıcıya kullanması gerektiğini bir ASP.NET uygulamasına nasıl söyleyeceğinizi gösteren bir görünüm ile sonlanır.

## <a name="introduction"></a>Giriş

Web sitesi ziyaretçilerinin tanımlanması için form kimlik doğrulaması kullanılarak incelenen önceki iki öğretici. Forms kimlik doğrulama çerçevesi, geliştiricilerin bir kullanıcıyı bir Web sitesine oturum açmasını ve kimlik doğrulama biletleri aracılığıyla sayfa ziyaretlerinin tamamında hatırlamasını kolaylaştırır. `FormsAuthentication` sınıfı, Bilet oluşturma ve ziyaretçi tanımlama bilgilerine ekleme yöntemlerini içerir. `FormsAuthenticationModule` tüm gelen istekleri inceler ve geçerli bir kimlik doğrulama bileti olan kişiler için, geçerli isteğiyle bir `GenericPrincipal` ve `FormsIdentity` nesnesi oluşturur ve ilişkilendirir. Forms kimlik doğrulaması yalnızca bir ziyaretçi için oturum açarken ve sonraki isteklerde, kullanıcının kimliğini belirlemede bu bileti ayrıştırmaya yönelik bir kimlik doğrulama bileti veren bir mekanizmadır. Bir Web uygulamasının Kullanıcı hesaplarını desteklemesi için yine de bir kullanıcı deposu uygulamanız ve kimlik bilgilerini doğrulamak, yeni kullanıcıları kaydettirmek ve Kullanıcı hesabı ile ilgili diğer görevlerin sayısız ' i için işlevsellik eklemeniz gerekir.

ASP.NET 2,0 ' den önce, geliştiriciler Kullanıcı hesabı ile ilgili tüm görevleri uygulamaya yönelik kanca üzerinde vardı. Neyse ki ASP.NET ekibi bu eksiklikleri kabul ederse ve üyelik çerçevesini ASP.NET 2,0 ile kullanıma sunmuştur. Üyelik çerçevesi, ana Kullanıcı hesabı ile ilgili görevleri yerine getirmeye yönelik bir programlama arabirimi sağlayan .NET Framework bir sınıf kümesidir. Bu çerçeve, geliştiricilerin standartlaştırılmış bir API 'ye özelleştirilmiş bir uygulama takmasını sağlayan [Sağlayıcı modeli](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)oluşturulmuştur.

<a id="Tutorial1"> </a> [*Güvenlik temelleri ve ASP.NET Destek*](../introduction/security-basics-and-asp-net-support-vb.md) öğreticisinde açıklandığı gibi .NET Framework, iki yerleşik üyelik sağlayıcısıyla birlikte gelir: [`ActiveDirectoryMembershipProvider`](https://msdn.microsoft.com/library/system.web.security.activedirectorymembershipprovider.aspx) ve [`SqlMembershipProvider`](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx). Adından da anlaşılacağı gibi `SqlMembershipProvider`, kullanıcı deposu olarak bir Microsoft SQL Server veritabanı kullanır. Bu sağlayıcıyı bir uygulamada kullanabilmeniz için sağlayıcıya mağaza olarak hangi veritabanının kullanılacağını söylememiz gerekir. Imagine olabileceğiniz gibi `SqlMembershipProvider`, Kullanıcı Mağazası veritabanının belirli veritabanı tablolarının, görünümlerin ve saklı yordamların olmasını bekler. Bu beklenen şemayı seçili veritabanına eklememiz gerekiyor.

Bu öğretici, `SqlMembershipProvider`kullanmak için gerekli şemayı veritabanına ekleme tekniklerini inceleyerek başlar. Bunu izleyerek, şemadaki anahtar tabloları inceleyecek ve amaçlarını ve önemini tartışacağız. Bu öğretici, üyelik çerçevesinin hangi sağlayıcıya kullanması gerektiğini bir ASP.NET uygulamasına nasıl söyleyeceğinizi gösteren bir görünüm ile sonlanır.

Haydi başlayın!

## <a name="step-1-deciding-where-to-place-the-user-store"></a>1\. Adım: Kullanıcı mağazasının yerleştirileceği yere karar verme

Bir ASP.NET uygulamasının verileri genellikle veritabanında bir dizi tabloda depolanır. `SqlMembershipProvider` veritabanı şemasını uygularken, üyelik şemasının uygulama verileriyle aynı veritabanına mı yoksa alternatif bir veritabanında mı yerleştirileceğini karar vermelidir.

Aşağıdaki nedenlerden dolayı uygulama verileriyle aynı veritabanında üyelik şemasını bulma öneriyorum:

- Verileri bir veritabanında kapsüllenmiş bir uygulamayla, iki ayrı veritabanına **sahip bir uygulamadan** anlaşılması, bakımını yapmak ve dağıtmak daha kolay olur.
- **Ilişkisel bütünlük** uygulama tablolarıyla aynı veritabanındaki üyelikle ilişkili tabloları bularak, üyelikle ilgili tablolardaki birincil anahtarlar ve ilgili uygulama tablolarında [yabancı anahtar kısıtlamaları](http://en.wikipedia.org/wiki/Foreign_key) kurmak mümkündür.

Kullanıcı mağazalarının ve uygulama verilerinin ayrı veritabanlarına ayrılması yalnızca, her birinin ayrı veritabanları kullandığı, ancak ortak bir kullanıcı deposu paylaşması gereken birden çok uygulamanız varsa anlamlıdır.

### <a name="creating-a-database"></a>Veritabanı Oluşturma

İkinci öğreticide henüz bir veritabanına ihtiyaç duyulmadığından oluşturmakta olduğumuz uygulama. Ancak, kullanıcı deposu için şimdi bir tane gerekir. Şimdi bir tane oluşturup `SqlMembershipProvider` sağlayıcısı tarafından gereken şemayı ekleyin (bkz. 2. adım).

> [!NOTE]
> Bu öğretici serisinin tamamında uygulama tablolarımızı ve `SqlMembershipProvider` şemasını depolamak için bir [Microsoft SQL Server 2005 Express Edition](https://msdn.microsoft.com/sql/Aa336346.aspx) veritabanı kullanacağız. Bu karar, iki nedenden dolayı yapılmıştır: ilk olarak, maliyet-ücretsiz-Express sürümü, SQL Server 2005 ' in en fazla erişilebilir sürümüdür; İkinci olarak, SQL Server 2005 Express Sürüm veritabanları doğrudan Web uygulamasının `App_Data` klasörüne yerleştirilebilir, bu da veritabanını ve Web uygulamasını bir ZIP dosyasında birlikte paketleyip, özel kurulum yönergeleri veya yapılandırma seçenekleri olmadan yeniden dağıtmak için bir geçiş yapar. SQL Server Express olmayan bir sürüm sürümünü kullanarak izlemeyi tercih ediyorsanız, ücretsiz olarak kullanabilirsiniz. Adımlar neredeyse aynıdır. `SqlMembershipProvider` şeması, Microsoft SQL Server 2000 ve üzerinde herhangi bir sürümle çalışır.

Çözüm Gezgini, `App_Data` klasörüne sağ tıklayın ve yeni öğe Ekle ' yi seçin. (Projenizde bir `App_Data` klasörü görmüyorsanız, Çözüm Gezgini projede projeye sağ tıklayın, ASP.NET klasörü Ekle ' yi seçin ve `App_Data`' yı seçin.) Yeni öğe Ekle iletişim kutusundan `SecurityTutorials.mdf`adlı yeni bir SQL veritabanı eklemeyi seçin. Bu öğreticide, `SqlMembershipProvider` şemasını bu veritabanına ekleyeceğiz; sonraki öğreticilerde, uygulama verilerimizi yakalamak için ek tablolar oluşturacağız.

[![App_Data klasöre Securityöğreticileri. mdf veritabanı adlı yeni bir SQL veritabanı ekleyin](creating-the-membership-schema-in-sql-server-vb/_static/image2.png)](creating-the-membership-schema-in-sql-server-vb/_static/image1.png)

**Şekil 1**: `App_Data` klasörüne `SecurityTutorials.mdf` veritabanı adlı yenı bir SQL veritabanı ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-the-membership-schema-in-sql-server-vb/_static/image3.png))

`App_Data` klasöre bir veritabanı eklemek, Veritabanı Gezgini görünümünde otomatik olarak ekler. (Visual Studio 'nun Express sürümü olmayan sürümünde, Veritabanı Gezgini Sunucu Gezgini olarak adlandırılır.) Veritabanı Gezgini gidin ve tek eklenen `SecurityTutorials` veritabanını genişletin. Ekranda Veritabanı Gezgini görmüyorsanız, Görünüm menüsüne gidin ve Veritabanı Gezgini ' i seçin veya CTRL + ALT + S tuşlarına basın. Şekil 2 ' de gösterildiği gibi, `SecurityTutorials` veritabanı boştur; hiç tablo yok, hiçbir görünüm ve saklı yordam içermez.

[![Securityöğreticileri veritabanı şu anda boş](creating-the-membership-schema-in-sql-server-vb/_static/image5.png)](creating-the-membership-schema-in-sql-server-vb/_static/image4.png)

**Şekil 2**: `SecurityTutorials` veritabanı şu anda boş ([tam boyutlu görüntüyü görüntülemek için tıklatın](creating-the-membership-schema-in-sql-server-vb/_static/image6.png))

## <a name="step-2-adding-thesqlmembershipproviderschema-to-the-database"></a>2\. Adım: veritabanına`SqlMembershipProvider`şeması ekleme

`SqlMembershipProvider`, Kullanıcı Mağazası veritabanına yüklenecek belirli bir tablo, görünüm ve saklı yordam kümesi gerektirir. Bu önkoşul veritabanı nesneleri [`aspnet_regsql.exe` aracı](https://msdn.microsoft.com/library/ms229862.aspx)kullanılarak eklenebilir. Bu dosya `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\` klasöründe bulunur.

> [!NOTE]
> `aspnet_regsql.exe` aracı hem komut satırı işlevselliği hem de bir grafik kullanıcı arabirimi sunar. Grafik arabirimi daha kolay ve bu öğreticide inceleyeceğiz. Komut satırı arabirimi, derleme betikleri veya otomatikleştirilmiş test senaryolarında olduğu gibi `SqlMembershipProvider` şemasının eklenmesi gerektiğinde faydalıdır.

`aspnet_regsql.exe` Aracı, belirli bir SQL Server veritabanına *ASP.NET uygulama hizmetleri* eklemek veya kaldırmak için kullanılır. ASP.NET uygulama hizmetleri, diğer ASP.NET 2,0 çerçevelerinin SQL tabanlı sağlayıcılarının şemaları ile birlikte `SqlMembershipProvider` ve `SqlRoleProvider`için şemaları kapsayabilir. `aspnet_regsql.exe` aracına iki bit bilgi sağlamamız gerekir:

- Uygulama hizmetlerini eklemek mi yoksa kaldırmak mı istediğinizi ve
- Uygulama Hizmetleri şemasının ekleneceği veya kaldırılacağı veritabanı

Veritabanının kullanması istenmeden `aspnet_regsql.exe` Aracı, veritabanının bulunduğu sunucunun adını, veritabanına bağlanmak için kullanılacak güvenlik kimlik bilgilerini ve veritabanı adını sağlamamızı ister. SQL Server Express olmayan sürümünü kullanıyorsanız, bir ASP.NET Web sayfası aracılığıyla veritabanıyla çalışırken bir bağlantı dizesi aracılığıyla sağlamanız gereken bilgilerle aynı olduğundan bu bilgileri zaten bilmelisiniz. `App_Data` klasöründe SQL Server 2005 Express Sürüm veritabanı kullanılırken sunucu ve veritabanı adını belirleme, ancak bir bit daha fazla.

Aşağıdaki bölümde, `App_Data` klasöründeki bir SQL Server 2005 Express Sürüm veritabanı için sunucu ve veritabanı adını belirtmenin kolay bir yolu incelenir. SQL Server 2005 Express Sürüm kullanmıyorsanız Uygulama Hizmetleri bölümünü yüklemeye devam edebilirsiniz.

### <a name="determining-the-server-and-database-name-for-a-sql-server-2005-express-edition-database-in-theapp_datafolder"></a>`App_Data`klasöründeki bir SQL Server 2005 Express Sürüm veritabanı için sunucu ve veritabanı adı belirleniyor

`aspnet_regsql.exe` aracı 'nı kullanabilmeniz için sunucu ve veritabanı adlarını bilmemiz gerekir. Sunucu adı `localhost\InstanceName`. Büyük olasılıkla, *ınstancename* `SQLExpress`. Ancak, SQL Server 2005 Express Sürüm el ile yüklediyseniz (yani, Visual Studio 'Yu yüklerken onu otomatik olarak yüklememediyseniz), farklı bir örnek adı seçmiş olmanız mümkündür.

Veritabanı adı, tespit edilecek bir bit kankidır. `App_Data` klasöründeki veritabanları genellikle veritabanı dosyası yoluyla birlikte [genel benzersiz tanımlayıcı](http://en.wikipedia.org/wiki/Globally_Unique_Identifier) içeren bir veritabanı adına sahiptir. `aspnet_regsql.exe`aracılığıyla uygulama Hizmetleri şemasını eklemek için bu veritabanı adını belirlememiz gerekir.

Veritabanı adını belirlemek için en kolay yol SQL Server Management Studio aracılığıyla incelemektir. SQL Server Management Studio, SQL Server 2005 veritabanlarının yönetilmesine yönelik grafik bir arabirim sağlar, ancak SQL Server 2005 ' nin Express Edition ile birlikte gelmez. İyi haber, SQL Server Management Studio Ücretsiz Express sürümünü [indirebileceğiniz](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en) yerdir.

> [!NOTE]
> Masaüstünüzde SQL Server 2005 ' nin Express sürümü olmayan bir sürümüne sahipseniz, Management Studio tam sürümü büyük olasılıkla yüklüdür. Aşağıdaki, Express Edition için aşağıda özetlenen adımları izleyerek veritabanı adını tespit etmek üzere tam sürümü kullanabilirsiniz.

Veritabanı dosyasındaki Visual Studio tarafından uygulanan kilitlerin kapalı olduğundan emin olmak için Visual Studio 'Yu kapatarak başlayın. Sonra, SQL Server Management Studio başlatın ve SQL Server 2005 Express Sürüm için `localhost\InstanceName` veritabanına bağlanın. Daha önce belirtildiği gibi, örnek adı `SQLExpress`. Kimlik doğrulama seçeneği için Windows kimlik doğrulaması ' nı seçin.

[SQL Server 2005 Express Sürüm örneğine ![bağlanma](creating-the-membership-schema-in-sql-server-vb/_static/image8.png)](creating-the-membership-schema-in-sql-server-vb/_static/image7.png)

**Şekil 3**: SQL Server 2005 Express sürüm örneğine bağlanma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-the-membership-schema-in-sql-server-vb/_static/image9.png))

SQL Server 2005 Express Sürüm örneğine bağlandıktan sonra, Management Studio veritabanları, güvenlik ayarları, sunucu nesneleri vb. için klasörleri görüntüler. Veritabanları sekmesini genişletirseniz, veritabanı örneğine `SecurityTutorials.mdf` *veritabanının kaydettirilmediğini* görürsünüz. önce veritabanını iliştirmemiz gerekir.

Veritabanları klasörüne sağ tıklayın ve bağlam menüsünden Ekle ' yi seçin. Bu, veritabanları Ekle iletişim kutusunu görüntüler. Buradan, Ekle düğmesine tıklayın, `SecurityTutorials.mdf` veritabanına gidin ve Tamam ' a tıklayın. Şekil 4 ' te `SecurityTutorials.mdf` veritabanı seçildikten sonra veritabanlarını Ekle iletişim kutusu gösterilir. Şekil 5 ' te, veritabanı başarıyla eklendikten sonra Nesne Gezgini Management Studio gösterilmektedir.

[![Securityöğreticileri. mdf veritabanını ekleyin](creating-the-membership-schema-in-sql-server-vb/_static/image11.png)](creating-the-membership-schema-in-sql-server-vb/_static/image10.png)

**Şekil 4**: `SecurityTutorials.mdf` veritabanını iliştirme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-the-membership-schema-in-sql-server-vb/_static/image12.png))

[![Securityöğreticileri. mdf veritabanı veritabanları klasöründe görüntülenir](creating-the-membership-schema-in-sql-server-vb/_static/image14.png)](creating-the-membership-schema-in-sql-server-vb/_static/image13.png)

**Şekil 5**: `SecurityTutorials.mdf` veritabanı veritabanları klasöründe görünür ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-the-membership-schema-in-sql-server-vb/_static/image15.png))

Şekil 5 ' i gösterdiği gibi, `SecurityTutorials.mdf` veritabanı bunun yerine abstruse adına sahiptir. Bunu daha kolay bir şekilde (ve yazmak daha kolay) değiştirelim. Veritabanına sağ tıklayın, bağlam menüsünden Yeniden Adlandır ' ı seçin ve `SecurityTutorialsDatabase`yeniden adlandırın. Bu dosya adını değiştirmez, yalnızca veritabanının kendisini SQL Server için tanımlamak üzere kullandığı adı.

[Veritabanını SecurityTutorialsDatabase olarak yeniden adlandırma ![](creating-the-membership-schema-in-sql-server-vb/_static/image17.png)](creating-the-membership-schema-in-sql-server-vb/_static/image16.png)

**Şekil 6**: veritabanını `SecurityTutorialsDatabase`olarak yeniden adlandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-the-membership-schema-in-sql-server-vb/_static/image18.png))

Bu noktada, `SecurityTutorials.mdf` veritabanı dosyası için sunucu ve veritabanı adlarını biliyoruz: sırasıyla `localhost\InstanceName` ve `SecurityTutorialsDatabase`. Artık `aspnet_regsql.exe` aracı aracılığıyla uygulama hizmetlerini yüklemeye hazırsınız.

### <a name="installing-the-application-services"></a>Uygulama Hizmetleri yükleme

`aspnet_regsql.exe` aracını başlatmak için Başlat menüsüne gidin ve Çalıştır ' ı seçin. Metin kutusuna `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\aspnet_regsql.exe` girin ve Tamam ' a tıklayın. Alternatif olarak, uygun klasöre gitmek için Windows Gezgini 'ni kullanabilir ve `aspnet_regsql.exe` dosyasına çift tıklayabilirsiniz. Her iki yaklaşım da aynı sonuçlara neden olur.

`aspnet_regsql.exe` aracını komut satırı bağımsız değişkenleri olmadan çalıştırmak, ASP.NET SQL Server Kurulum Sihirbazı grafik kullanıcı arabirimini başlatır. Sihirbaz, ASP.NET uygulama hizmetlerinin belirtilen bir veritabanına eklenmesini veya kaldırılmasını kolaylaştırır. Sihirbazın ilk ekranı, Şekil 7 ' de gösterildiği gibi, aracın amacını açıklamaktadır.

[![ASP.NET SQL Server Kurulum Sihirbazı üyelik şemasını eklemek için kullanılır](creating-the-membership-schema-in-sql-server-vb/_static/image20.png)](creating-the-membership-schema-in-sql-server-vb/_static/image19.png)

**Şekil 7**: ASP.NET SQL Server Kurulum Sihirbazı üyelik şemasını eklemek için kullanılır ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-the-membership-schema-in-sql-server-vb/_static/image21.png))

Sihirbazdaki ikinci adım, uygulama hizmetlerini eklemek mi yoksa kaldırmak mı istediğinizi sorar. `SqlMembershipProvider`için gereken tabloları, görünümleri ve saklı yordamları eklemek istediğimiz için, uygulama hizmetleri için SQL Server Yapılandır seçeneğini belirleyin. Daha sonra, bu şemayı veritabanınızdan kaldırmak istiyorsanız, bu Sihirbazı yeniden çalıştırın, bunun yerine var olan bir veritabanından uygulama hizmetleri bilgilerini Kaldır seçeneğini belirleyin.

[![Uygulama Hizmetleri için SQL Server Yapılandır seçeneğini belirleyin](creating-the-membership-schema-in-sql-server-vb/_static/image23.png)](creating-the-membership-schema-in-sql-server-vb/_static/image22.png)

**Şekil 8**: Uygulama Hizmetleri Için SQL Server Yapılandır seçeneğini belirleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-the-membership-schema-in-sql-server-vb/_static/image24.png))

Üçüncü adım veritabanı bilgilerini ister: sunucu adı, kimlik doğrulama bilgileri ve veritabanı adı. Bu öğreticiyle birlikte takip ediyorsanız ve `SecurityTutorials.mdf` veritabanını `App_Data`eklediyseniz `localhost\InstanceName`iliştirdiniz ve `SecurityTutorialsDatabase`olarak yeniden adlandırdıysanız, ardından aşağıdaki değerleri kullanın:

- Sunucu: `localhost\InstanceName`
- Windows kimlik doğrulama
- Veritabanı: `SecurityTutorialsDatabase`

[![veritabanı bilgilerini girin](creating-the-membership-schema-in-sql-server-vb/_static/image26.png)](creating-the-membership-schema-in-sql-server-vb/_static/image25.png)

**Şekil 9**: veritabanı bilgilerini girin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-the-membership-schema-in-sql-server-vb/_static/image27.png))

Veritabanı bilgilerini girdikten sonra Ileri ' ye tıklayın. Son adım, gerçekleştirilecek adımları özetler. Uygulama hizmetlerini yüklemek için Ileri ' ye tıklayın ve Sihirbazı tamamladıktan sonra işlemi doldurun.

> [!NOTE]
> Veritabanını iliştirmek ve veritabanı dosyasını yeniden adlandırmak için Management Studio kullandıysanız, Visual Studio 'Yu yeniden açmadan önce veritabanını kullanımdan çıkarmayı ve Management Studio kapatmayı unutmayın. `SecurityTutorialsDatabase` veritabanını ayırmak için veritabanı adına sağ tıklayın ve görevler menüsünde Ayır ' ı seçin.

Sihirbaz tamamlandıktan sonra Visual Studio 'ya dönün ve Veritabanı Gezgini gidin. Tablolar klasörünü genişletin. Adları `aspnet_`önekiyle başlayan bir tablo dizisi görmeniz gerekir. Benzer şekilde, görünümler ve saklı yordamlar klasörlerinin çeşitli görünümleri ve saklı yordamları bulabilirsiniz. Bu veritabanı nesneleri uygulama Hizmetleri şemasını yapar. 3\. adımda üyelik ve role özgü veritabanı nesnelerini inceleyeceğiz.

[Veritabanına çeşitli tablolar, görünümler ve saklı yordamlar ![eklenmiştir](creating-the-membership-schema-in-sql-server-vb/_static/image29.png)](creating-the-membership-schema-in-sql-server-vb/_static/image28.png)

**Şekil 10**: veritabanına çeşitli tablolar, görünümler ve saklı yordamlar eklendi ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-the-membership-schema-in-sql-server-vb/_static/image30.png))

> [!NOTE]
> `aspnet_regsql.exe` aracın grafik kullanıcı arabirimi, tüm uygulama Hizmetleri şemasını kurar. Ancak, komut satırından `aspnet_regsql.exe` yürütürken, hangi uygulama Hizmetleri bileşenlerinin yükleneceğini (veya kaldırabileceklerini) belirtebilirsiniz. Bu nedenle, yalnızca `SqlMembershipProvider` ve `SqlRoleProvider` sağlayıcıları için gereken tabloları, görünümleri ve saklı yordamları eklemek istiyorsanız, komut satırından `aspnet_regsql.exe` çalıştırın. Alternatif olarak, `aspnet_regsql.exe`tarafından kullanılan T-SQL oluşturma betikleri 'nin uygun alt kümesini el ile çalıştırabilirsiniz. Bu betikler, `InstallCommon.sql`, `InstallMembership.sql`, `InstallRoles.sql`, `InstallProfile.sql`, `InstallSqlState.sql`gibi adlara sahip `WINDIR%\Microsoft.Net\Framework\v2.0.50727\` klasöründe bulunur.

Bu noktada, `SqlMembershipProvider`gereken veritabanı nesnelerini oluşturduk. Ancak, üyelik çerçevesine hala `SqlMembershipProvider` (yani, `ActiveDirectoryMembershipProvider`) kullanması gerektiğini ve `SqlMembershipProvider` `SecurityTutorials` veritabanını kullanması gerektiğini söylememiz gerekir. Hangi sağlayıcının kullanılacağını ve 4. adımda seçilen sağlayıcının ayarlarını nasıl özelleştireceğinizi inceleyeceğiz. Ancak ilk olarak, yeni oluşturulan veritabanı nesnelerine daha derin bir göz atalım.

## <a name="step-3-a-look-at-the-schemas-core-tables"></a>3\. Adım: şemanın temel tablolarına bakış

Bir ASP.NET uygulamasında üyelik ve rol çerçeveleri ile çalışırken, uygulama ayrıntıları sağlayıcı tarafından kapsüllenir. Gelecek öğreticilerde, bu çerçeveleri .NET Framework `Membership` ve `Roles` sınıfları aracılığıyla arayüzle göndereceğiz. Bu üst düzey API 'Leri kullanırken, hangi sorguların yürütüldüğü veya `SqlMembershipProvider` ve `SqlRoleProvider`tarafından hangi tabloların değiştirildiği gibi alt düzey ayrıntılarla kendimize ilgilenmenize gerek yoktur.

Bu şekilde, 1. adımda oluşturulan veritabanı şemasını araştırmadan üyelik ve rol çerçevelerini güvenle kullanabiliriz. Ancak, uygulama verilerini depolamak için tablolar oluştururken, kullanıcılar veya rollerle ilgili varlıklar oluşturmanız gerekebilir. Uygulama veri tabloları ve adım 2 ' de oluşturulan tablolar arasında yabancı anahtar kısıtlamaları oluştururken `SqlMembershipProvider` ve `SqlRoleProvider` şemaları hakkında bir benzerlik sağlanmasına yardımcı olur. Üstelik, bazı nadir durumlarda, Kullanıcı ve rol depolarıyla doğrudan veritabanı düzeyinde Arabirim (`Membership` veya `Roles` sınıfları yerine) arayüzlü olması gerekebilir.

### <a name="partitioning-the-user-store-into-applications"></a>Kullanıcı mağazasını uygulamalara bölümleme

Üyelik ve rol çerçeveleri, tek bir Kullanıcı ve rol mağazasının birçok farklı uygulama arasında paylaşılabilmesi için tasarlanmıştır. Üyeliği veya rolleri kullanan bir ASP.NET uygulamasının kullanılacak uygulama bölümünü belirtmesi gerekir. Kısacası, birden çok Web uygulaması aynı kullanıcı ve rol mağazalarını kullanabilir. Şekil 11 ' de üç uygulamada bölümlenen Kullanıcı ve rol depoları gösterilmektedir: HRSite, CustomerSite ve SalesSite. Bu üç Web uygulamasının kendine ait benzersiz kullanıcıları ve rolleri vardır, ancak bunların hepsi, Kullanıcı hesabını ve rol bilgilerini aynı veritabanı tablolarında fiziksel olarak depolar.

[![Kullanıcı hesapları birden çok uygulama arasında bölümlenmiş olabilir](creating-the-membership-schema-in-sql-server-vb/_static/image32.png)](creating-the-membership-schema-in-sql-server-vb/_static/image31.png)

**Şekil 11**: Kullanıcı hesapları birden çok uygulama arasında bölümlenebilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](creating-the-membership-schema-in-sql-server-vb/_static/image33.png))

`aspnet_Applications` tablosu bu bölümleri tanımlar. Kullanıcı hesabı bilgilerini depolamak için veritabanını kullanan her uygulama, bu tablodaki bir satırla temsil edilir. `aspnet_Applications` tabloda dört sütun vardır: `ApplicationId`, `ApplicationName`, `LoweredApplicationName`ve `Description`.`ApplicationId` [`uniqueidentifier`](https://msdn.microsoft.com/library/ms187942.aspx) türündedir ve tablonun birincil anahtarıdır; `ApplicationName` her uygulama için benzersiz bir insan dostu ad sağlar.

Diğer üyelik ve rolle ilgili tablolar `aspnet_Applications``ApplicationId` alanına geri bağlanır. Örneğin, her kullanıcı hesabı için bir kayıt içeren `aspnet_Users` tablosu, bir `ApplicationId` yabancı anahtar alanına sahiptir; `aspnet_Roles` tablosu için Ditto. Bu tablolardaki `ApplicationId` alanı, Kullanıcı hesabının veya rolün ait olduğu uygulama bölümünü belirtir.

### <a name="storing-user-account-information"></a>Kullanıcı hesabı bilgilerini depolama

Kullanıcı hesabı bilgileri iki tabloda barındırılabilir: `aspnet_Users` ve `aspnet_Membership`. `aspnet_Users` tablosu, temel kullanıcı hesabı bilgilerini tutan alanları içerir. En önemli üç sütun şunlardır:

- `UserId`
- `UserName`
- `ApplicationId`

`UserId` birincil anahtardır (ve `uniqueidentifier`türü). `UserName` `nvarchar(256)` türüdür ve parolanın yanı sıra kullanıcının kimlik bilgilerini oluşturur. (Bir kullanıcının parolası `aspnet_Membership` tablosunda depolanır.) `ApplicationId`, Kullanıcı hesabını `aspnet_Applications`belirli bir uygulamaya bağlar. `UserName` ve `ApplicationId` sütunlarda bir bileşik [`UNIQUE` kısıtlaması](https://msdn.microsoft.com/library/ms191166.aspx) vardır. Bu, belirli bir uygulamada her kullanıcı adının benzersiz olmasını sağlar, ancak aynı `UserName` farklı uygulamalarda kullanılmasına izin verir.

`aspnet_Membership` tablosu kullanıcının parolası, e-posta adresi, son oturum açma tarihi ve saati gibi ek kullanıcı hesabı bilgilerini içerir. `aspnet_Users` ve `aspnet_Membership` tablolarındaki kayıtlar arasında bire bir yazışmalar vardır. Bu ilişki, tablonun birincil anahtarı olarak hizmet veren `aspnet_Membership``UserId` alanı tarafından belirlenir. `aspnet_Users` tablosu gibi `aspnet_Membership`, bu bilgileri belirli bir uygulama bölümüne bağlayan bir `ApplicationId` alanı içerir.

### <a name="securing-passwords"></a>Parolaların güvenliğini sağlama

Parola bilgileri `aspnet_Membership` tablosunda depolanır. `SqlMembershipProvider`, aşağıdaki üç teknikten biri kullanılarak parolaların veritabanında depolanmasını sağlar:

- **Temizle** -parola veritabanında düz metin olarak depolanır. Bu seçeneği kullanmayı kesinlikle önleyin. Veritabanı tehlikeye atılırsa, veritabanı erişimi olan bir arka kapı veya disgruntled çalışanı bulan bir bilgisayar korsanının olması-her tek kullanıcının kimlik bilgileri almak için orada bulunur.
- **Karma hale getirilmiş** parolalar tek yönlü bir karma algoritması ve rastgele oluşturulmuş bir anahtar değeri kullanılarak karma hale getirilir. Bu karma değer (güvenlik ile birlikte) veritabanında depolanır.
- **Şifrelenmiş** -parolanın şifrelenmiş bir sürümü veritabanında depolanır.

Kullanılan parola depolama tekniği, `Web.config`belirtilen `SqlMembershipProvider` ayarlarına bağlıdır. 4\. adımdaki `SqlMembershipProvider` ayarlarını özelleştirmeye bakacağız. Varsayılan davranış parolanın karmasını deposıdır.

Parolanın depolanmasından sorumlu sütunlar `Password`, `PasswordFormat`ve `PasswordSalt`. `PasswordFormat`, değeri, parolayı depolamak için kullanılan tekniği belirten `int` türünde bir alandır: Clear için 0; Karma için 1; 2 şifreli. `PasswordSalt`, kullanılan parola depolama tekniğinden bağımsız olarak rastgele oluşturulmuş bir dizeye atanır; `PasswordSalt` değeri yalnızca parolanın karması hesaplanırken kullanılır. Son olarak, `Password` sütunu gerçek parola verilerini içerir, düz metin parolası, Parola karması veya şifrelenmiş parola olur.

Tablo 1, parolayı saklarken çeşitli depolama teknikleri için bu üç sütunun nasıl görünebileceğini gösterir! .

| **Depolama tekniği&lt;\_o3a\_p/&gt;** | **Parola&lt;\_o3a\_p/&gt;** | **PasswordFormat&lt;\_o3a\_p/&gt;** | **Passwordanahtar&lt;\_o3a\_p/&gt;** |
| --- | --- | --- | --- |
| Lediğiniz | MySecret! | 0 | tTnkPlesqissc2y2SMEygA = = |
| Haline | 2oXm6sZHWbTHFgjgkGQsc2Ec9ZM = | 1\. | wFgjUfhdUFOCKQiI61vtiQ = = |
| Şifreli | 62RZgDvhxykkqsMchZ0Yly7HS6onhpaoCYaRxV8g0F4CW56OXUU3e7Inza9j9BKp | 2 | LSRzhGS/AA/oqAXGLHJNBw = = |

**Tablo 1**: parolayı saklarken parola Ile ilgili alanlar Için örnek değerler MySecret!

> [!NOTE]
> `SqlMembershipProvider` tarafından kullanılan özel şifreleme veya karma algoritma `<machineKey>` öğesindeki ayarlar tarafından belirlenir. Bu yapılandırma öğesi, <a id="Tutorial3"> </a> [*Forms kimlik doğrulaması yapılandırması ve gelişmiş konular*](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md) öğreticisinin 3. adımında anlatıldık.

### <a name="storing-roles-and-role-associations"></a>Rolleri ve rol Ilişkilendirmelerini depolama

Rol çerçevesi, geliştiricilerin bir rol kümesi tanımlamasına ve hangi kullanıcıların hangi rollere ait olduğunu belirlemesine izin verir. Bu bilgiler veritabanında iki tablo aracılığıyla yakalanır: `aspnet_Roles` ve `aspnet_UsersInRoles`. `aspnet_Roles` tablosundaki her kayıt, belirli bir uygulama için bir rolü temsil eder. `aspnet_Users` tablosuna benzer şekilde, `aspnet_Roles` tablosunda tartışmamızı belirten üç sütun vardır:

- `RoleId`
- `RoleName`
- `ApplicationId`

`RoleId` birincil anahtardır (ve `uniqueidentifier`türü). `RoleName` `nvarchar(256)`türüdür. Ve `ApplicationId` Kullanıcı hesabını `aspnet_Applications`belirli bir uygulamaya bağlar. `RoleName` ve `ApplicationId` sütunlarında bir bileşik `UNIQUE` kısıtlaması vardır. Bu, belirli bir uygulamada her bir rol adının benzersiz olmasını sağlar.

`aspnet_UsersInRoles` tablo, kullanıcılar ve roller arasında bir eşleme görevi görür. Yalnızca iki sütun vardır-`UserId` ve `RoleId` ve birlikte bir bileşik birincil anahtar oluşturun.

## <a name="step-4-specifying-the-provider-and-customizing-its-settings"></a>4\. Adım: sağlayıcıyı belirtme ve ayarlarını özelleştirme

Üyelik ve rol çerçeveleri gibi sağlayıcı modelini destekleyen tüm çerçeveler-uygulama ayrıntılarının olmaması ve bunun yerine bu sorumluluğu bir sağlayıcı sınıfına devretmek. Üyelik çerçevesi söz konusu olduğunda, `Membership` sınıfı kullanıcı hesaplarını yönetmek için API 'yi tanımlar, ancak herhangi bir Kullanıcı deposuyla doğrudan etkileşime almaz. Bunun yerine, `Membership` sınıfının yöntemleri, yapılandırılan sağlayıcıya yönelik isteği devre dışı bırakır. `SqlMembershipProvider`kullanacağız. `Membership` sınıfındaki yöntemlerden birini çağırdığımızda, üyelik çerçevesinin `SqlMembershipProvider`çağrıyı devretmek nasıl bildiği hakkında bilgi sahibi misiniz?

`Membership` sınıfı, üyelik çerçevesi tarafından kullanılabilecek tüm kayıtlı sağlayıcı sınıflarının başvurusunu içeren bir [`Providers` özelliğine](https://msdn.microsoft.com/library/system.web.security.membership.providers.aspx) sahiptir. Kayıtlı her sağlayıcının ilişkili bir adı ve türü vardır. Ad, `Providers` koleksiyonundaki belirli bir sağlayıcıya başvurmak için kolay bir yol sunar, tür sağlayıcı sınıfını tanımlar. Üstelik, her kayıtlı sağlayıcı yapılandırma ayarlarını içerebilir. Üyelik çerçevesinin yapılandırma ayarları, çok sayıda `PasswordFormat` ve `requiresUniqueEmail`içerir. `SqlMembershipProvider`tarafından kullanılan yapılandırma ayarlarının tüm listesi için bkz. Tablo 2.

`Providers` özelliğinin içeriği, Web uygulamasının yapılandırma ayarları aracılığıyla belirtilir. Varsayılan olarak, tüm Web uygulamalarının `SqlMembershipProvider`türünde `AspNetSqlMembershipProvider` adlı bir sağlayıcısı vardır. Bu varsayılan üyelik sağlayıcısı `machine.config` kaydedilir (`%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG`konumunda bulunur):

[!code-xml[Main](creating-the-membership-schema-in-sql-server-vb/samples/sample1.xml)]

Yukarıdaki biçimlendirme gösterildiği gibi, [`<membership>` öğesi](https://msdn.microsoft.com/library/1b9hw62f.aspx) , üyelik çerçevesinin yapılandırma ayarlarını tanımlar, [`<providers>` alt öğesi](https://msdn.microsoft.com/library/6d4936ht.aspx) kayıtlı sağlayıcıları belirtir. Sağlayıcılar [`<add>`](https://msdn.microsoft.com/library/whae3t94.aspx) veya [`<remove>`](https://msdn.microsoft.com/library/aykw9a6d.aspx) öğeleri kullanılarak eklenebilir veya kaldırılabilir; Şu anda kayıtlı olan tüm sağlayıcıları kaldırmak için [`<clear>`](https://msdn.microsoft.com/library/t062y6yc.aspx) öğesini kullanın. Yukarıdaki biçimlendirme gösterildiği gibi, `machine.config` `SqlMembershipProvider`türünde `AspNetSqlMembershipProvider` adlı bir sağlayıcı ekler.

`name` ve `type` özniteliklerine ek olarak `<add>` öğesi, çeşitli yapılandırma ayarlarının değerlerini tanımlayan öznitelikler içerir. Tablo 2, kullanılabilir `SqlMembershipProvider`özgü yapılandırma ayarlarını, her birinin açıklamasıyla birlikte listeler.

> [!NOTE]
> Tablo 2 ' de belirtilen varsayılan değerler `SqlMembershipProvider` sınıfında tanımlanan varsayılan değerlere başvurur. `AspNetSqlMembershipProvider` içindeki yapılandırma ayarlarının hepsi `SqlMembershipProvider` sınıfının varsayılan değerlerine karşılık geldiğini unutmayın. Örneğin, bir üyelik sağlayıcısında belirtilmemişse, `requiresUniqueEmail` ayarı varsayılan olarak true olur. Ancak `AspNetSqlMembershipProvider`, açıkça bir `false`değeri belirterek bu varsayılan değeri geçersiz kılar.

| **&lt;\_o3a\_p/&gt; ayarlama** | **Açıklama&lt;\_o3a\_p/&gt;** |
| --- | --- |
| `ApplicationName` | Üyelik çerçevesinin, tek bir Kullanıcı deposunun birden çok uygulama arasında bölümlenmesi için izin verdiğini hatırlayın. Bu ayar, üyelik sağlayıcısı tarafından kullanılan uygulama bölümünün adını gösterir. Bu değer açıkça belirtilmemişse, çalışma zamanında, uygulamanın sanal kök yolu değerine ayarlanır. |
| `commandTimeout` | SQL komut zaman aşımı değerini (saniye cinsinden) belirtir. Varsayılan değer 30 ' dur. |
| `connectionStringName` | Kullanıcı deposu veritabanına bağlanmak için kullanılacak `<connectionStrings>` öğesindeki bağlantı dizesinin adı. Bu değer gereklidir. |
| `description` | Kayıtlı sağlayıcının insanın kolay bir açıklamasını sağlar. |
| `enablePasswordRetrieval` | Kullanıcıların unutulan parolalarını alıp almamadığını belirtir. Varsayılan değer `false` şeklindedir. |
| `enablePasswordReset` | Kullanıcıların parolalarını sıfırlamasına izin verilip verilmeyeceğini belirtir. `true` değerini varsayılan olarak alır. |
| `maxInvalidPasswordAttempts` | Kullanıcı kilitlenmesinden önce belirtilen `passwordAttemptWindow` sırasında belirli bir kullanıcı için gerçekleşebileceğini en fazla başarısız oturum açma girişimi sayısı. Varsayılan değer 5 ' tir. |
| `minRequiredNonalphanumericCharacters` | Kullanıcı parolada görünmesi gereken en az alfasayısal olmayan karakter sayısı. Bu değer 0 ile 128 arasında olmalıdır; Varsayılan değer 1 ' dir. |
| `minRequiredPasswordLength` | Bir parolada gereken en az karakter sayısı. Bu değer 0 ile 128 arasında olmalıdır; Varsayılan değer 7 ' dir. |
| `name` | Kayıtlı sağlayıcının adı. Bu değer gereklidir. |
| `passwordAttemptWindow` | Başarısız oturum açma girişimlerinin izlendiği dakika sayısı. Bir Kullanıcı belirtilen bu pencere içinde `maxInvalidPasswordAttempts` zaman geçersiz oturum açma kimlik bilgileri sağlarsa, bunlar kilitlenir. Varsayılan değer 10 ' dur. |
| `PasswordFormat` | Parola depolama biçimi: `Clear`, `Hashed`veya `Encrypted`. Varsayılan, `Hashed` değeridir. |
| `passwordStrengthRegularExpression` | Sağlanmışsa, bu normal ifade, yeni bir hesap oluştururken veya parolalarını değiştirirken kullanıcının seçili parolasının gücünü değerlendirmek için kullanılır. Varsayılan değer boş bir dizedir. |
| `requiresQuestionAndAnswer` | Kullanıcının parolasını alırken veya sıfırlarken güvenlik sorusuna yanıt vermesi gerekip gerekmediğini belirtir. Varsayılan değer `true` şeklindedir. |
| `requiresUniqueEmail` | Belirli bir uygulama bölümündeki tüm Kullanıcı hesaplarının benzersiz bir e-posta adresine sahip olup olmadığını gösterir. Varsayılan değer `true` şeklindedir. |
| `type` | Sağlayıcının türünü belirtir. Bu değer gereklidir. |

**Tablo 2**: üyelik ve `SqlMembershipProvider` yapılandırma ayarları

`AspNetSqlMembershipProvider`ek olarak, diğer üyelik sağlayıcıları, `Web.config` dosyasına benzer biçimlendirme eklenerek uygulama temelinde bir uygulamayla kaydedilebilir.

> [!NOTE]
> Rol çerçevesi çok aynı şekilde çalışıyor: `machine.config` ' de varsayılan bir kayıtlı rol sağlayıcısı vardır ve kayıtlı sağlayıcılar `Web.config`içinde uygulama temelinde özelleştirilebilir. Daha sonraki bir öğreticide, roller çerçevesini ve yapılandırma işaretlemesini ayrıntılı olarak inceleyeceğiz.

### <a name="customizing-thesqlmembershipprovidersettings"></a>`SqlMembershipProvider`ayarlarını özelleştirme

Varsayılan `SqlMembershipProvider` (`AspNetSqlMembershipProvider`) `connectionStringName` özniteliği `LocalSqlServer`olarak ayarlanmıştır. `AspNetSqlMembershipProvider` sağlayıcısı gibi `LocalSqlServer` bağlantı dizesi adı `machine.config`tanımlanmıştır.

[!code-xml[Main](creating-the-membership-schema-in-sql-server-vb/samples/sample2.xml)]

Görebileceğiniz gibi, bu bağlantı dizesi | konumunda bulunan bir SQL 2005 Express Edition veritabanını tanımlar. DataDirectory | aspnetdb. mdf. Dize | Veri dizini | çalışma zamanında, `~/App_Data/` dizinine işaret etmek için çevrilir, bu nedenle veritabanı yolu | DataDirectory | aspnetdb. mdf `~/App_Data`/`aspnet.mdf`dönüştürür.

Uygulamanın `Web.config` dosyasında herhangi bir üyelik sağlayıcısı bilgisi belirtmediyseniz, uygulama varsayılan kayıtlı üyelik sağlayıcısını kullanır, `AspNetSqlMembershipProvider`. `~/App_Data/aspnet.mdf` veritabanı yoksa, ASP.NET çalışma zamanı otomatik olarak oluşturur ve uygulama Hizmetleri şemasını ekler. Ancak, `aspnet.mdf` veritabanını kullanmak istemiyorum; Bunun yerine, adım 2 ' de oluşturduğumuz `SecurityTutorials.mdf` veritabanını kullanmak istiyoruz. Bu değişiklik, iki şekilde gerçekleştirilebilir:

- <strong>`Web.config`</strong><strong>`LocalSqlServer`</strong> <strong>bağlantı dizesi adı</strong> <strong>için bir değer belirtin</strong> <strong>.</strong> `Web.config``LocalSqlServer` bağlantı dizesi adı değerinin üzerine yazarak, varsayılan kayıtlı üyelik sağlayıcısını (`AspNetSqlMembershipProvider`) kullanabilir ve `SecurityTutorials.mdf` veritabanıyla doğru bir şekilde çalışabilir. Bu yaklaşım, `AspNetSqlMembershipProvider`tarafından belirtilen yapılandırma ayarlarıyla içeriğiniz varsa uygundur. Bu teknik hakkında daha fazla bilgi için bkz. [Scott Guthrie](https://weblogs.asp.net/scottgu/)'nin blog gönderisi, [SQL Server 2000 veya SQL Server 2005 kullanmak için ASP.NET 2,0 uygulama hizmetleri yapılandırma](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx).
- <strong>`SqlMembershipProvider`türünde yeni bir kayıtlı sağlayıcı ekleyin</strong> <strong>ve</strong> <strong>`connectionStringName`</strong>ayarını<strong>`SecurityTutorials.mdf`</strong> <strong>veritabanına</strong> <strong>işaret etmek üzere</strong> yapılandırın. Bu yaklaşım, veritabanı bağlantı dizesine ek olarak diğer yapılandırma özelliklerini özelleştirmek istediğiniz senaryolarda yararlıdır. Kendi projelerimde bu yaklaşımı esneklik ve okunabilirlik nedeniyle her zaman kullandım.

`SecurityTutorials.mdf` veritabanına başvuran yeni bir kayıtlı sağlayıcı ekleyebilmek için önce `Web.config``<connectionStrings>` bölümünde uygun bir bağlantı dizesi değeri eklememiz gerekir. Aşağıdaki biçimlendirme `App_Data` klasöründeki SQL Server 2005 Express Sürüm `SecurityTutorials.mdf` veritabanına başvuran `SecurityTutorialsConnectionString` adlı yeni bir bağlantı dizesi ekler.

[!code-xml[Main](creating-the-membership-schema-in-sql-server-vb/samples/sample3.xml)]

> [!NOTE]
> Alternatif bir veritabanı dosyası kullanıyorsanız, bağlantı dizesini gerektiği şekilde güncelleştirin. Doğru bağlantı dizesinin nasıl oluşabileceği hakkında daha fazla bilgi için bkz. [connectionStrings.com](http://www.connectionstrings.com/).

Sonra, `Web.config` dosyasına aşağıdaki Üyelik yapılandırma işaretlemesini ekleyin. Bu biçimlendirme `SecurityTutorialsSqlMembershipProvider`adlı yeni bir sağlayıcı kaydeder.

[!code-xml[Main](creating-the-membership-schema-in-sql-server-vb/samples/sample4.xml)]

`SecurityTutorialsSqlMembershipProvider` sağlayıcıyı kaydetmenin yanı sıra, yukarıdaki biçimlendirme `SecurityTutorialsSqlMembershipProvider` varsayılan sağlayıcı olarak tanımlar (`<membership>` öğesindeki `defaultProvider` özniteliği aracılığıyla). Üyelik çerçevesinin birden çok kayıtlı sağlayıcısı olabilir. `AspNetSqlMembershipProvider`, `machine.config`ilk sağlayıcı olarak kaydedildiğinden, aksini belirtmediğiniz sürece varsayılan sağlayıcı olarak görev yapar.

Şu anda uygulamamız iki kayıtlı sağlayıcıya sahiptir: `AspNetSqlMembershipProvider` ve `SecurityTutorialsSqlMembershipProvider`. Ancak, `SecurityTutorialsSqlMembershipProvider` sağlayıcıyı kaydetmeden önce, `<add>` öğesinden hemen önce [`<clear />` bir öğe](https://msdn.microsoft.com/library/t062y6yc.aspx) ekleyerek önceden kaydedilmiş tüm sağlayıcıları temizlemiş olabilir. Bu, kayıtlı sağlayıcılar listesinden `AspNetSqlMembershipProvider` temizleyebilir, yani `SecurityTutorialsSqlMembershipProvider` yalnızca kayıtlı üyelik sağlayıcısı olacaktır. Bu yaklaşımı kullandığımızda, tek kayıtlı üyelik sağlayıcısı olduğundan, `SecurityTutorialsSqlMembershipProvider` varsayılan sağlayıcı olarak işaretlemenize gerek kalmaz. `<clear />`kullanma hakkında daha fazla bilgi için bkz. [sağlayıcılar eklenirken `<clear />` kullanma](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx).

`SecurityTutorialsSqlMembershipProvider``connectionStringName` ayarının, tam eklenen `SecurityTutorialsConnectionString` bağlantı dizesi adına başvurdığına ve `applicationName` ayarının Securityöğreticiler değeri olarak ayarlandığını unutmayın. Ayrıca, `requiresUniqueEmail` ayarı `true`olarak ayarlanmıştır. Diğer tüm yapılandırma seçenekleri, `AspNetSqlMembershipProvider`değerleriyle aynıdır. İsterseniz, burada herhangi bir yapılandırma değişikliği yapabilirsiniz. Örneğin, bir tane yerine iki alfasayısal olmayan karakter gerektirerek veya parola uzunluğunu yedi yerine sekiz karakter ile artırarak parola gücünü güçleyerek artırabilirsiniz.

> [!NOTE]
> Üyelik çerçevesinin, tek bir Kullanıcı deposunun birden çok uygulama arasında bölümlenmesi için izin verdiğini hatırlayın. Üyelik sağlayıcısının `applicationName` ayarı, sağlayıcının kullanıcı deposuyla çalışırken hangi uygulamayı kullanacağını gösterir. `applicationName` yapılandırma ayarı için açıkça bir değer ayarlamanız önemlidir çünkü `applicationName` açıkça ayarlanmamışsa, çalışma zamanında Web uygulamasının sanal kök yoluna atanır. Uygulamanın sanal kök yolu değişmediğinden bu işlem sorunsuz çalışır, ancak uygulamayı farklı bir yola taşırsanız `applicationName` ayarı da aynı şekilde değişir. Bu durumda, üyelik sağlayıcısı daha önce kullanılandan farklı bir uygulama bölümüyle çalışmaya başlayacaktır. Taşıma işleminden önce oluşturulan kullanıcı hesapları farklı bir uygulama bölümünde kalacak ve bu kullanıcılar artık sitede oturum açamaz. Bu konuyla ilgili daha ayrıntılı bir tartışma için, bkz. [ASP.NET 2,0 üyeliğini ve diğer sağlayıcıları yapılandırırken her zaman `applicationName` özelliğini ayarlama](https://weblogs.asp.net/scottgu/443634).

## <a name="summary"></a>Özet

Bu noktada, yapılandırılmış uygulama hizmetleri (`SecurityTutorials.mdf`) ile bir veritabanı vardır ve üyelik çerçevesinin yeni Kaydolduğumuz `SecurityTutorialsSqlMembershipProvider` sağlayıcıyı kullanması için Web uygulamamızı yapılandırmış olmanız gerekir. Bu kayıtlı sağlayıcı `SqlMembershipProvider` türündedir ve `connectionStringName` uygun bağlantı dizesine (`SecurityTutorialsConnectionString`) ve `applicationName` değeri açıkça ayarlanmış olarak ayarlanmıştır.

Artık uygulamamızda üyelik çerçevesini kullanmaya hazırsınız. Sonraki öğreticide, Yeni Kullanıcı hesapları oluşturmayı inceleyeceğiz. Aşağıdaki, Kullanıcı tabanlı yetkilendirme gerçekleştirerek ve Kullanıcı ile ilgili ek bilgileri veritabanında depolarız.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ASP.NET 2,0 üyeliğini ve diğer sağlayıcıları yapılandırırken her zaman `applicationName` özelliğini ayarlayın](https://weblogs.asp.net/scottgu/443634)
- [SQL Server 2000 veya SQL Server 2005 kullanmak için ASP.NET 2,0 Uygulama Hizmetleri yapılandırma](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)
- [SQL Server Management Studio Express Edition 'ı indirin](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)
- [ASP.NET 2,0 s üyeliğini, rollerini ve profilini İnceleme](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [Üyelik sağlayıcıları için `<add>` öğesi](https://msdn.microsoft.com/library/whae3t94.aspx)
- [`<membership>` öğesi](https://msdn.microsoft.com/library/1b9hw62f.aspx)
- [Üyelik için `<providers>` öğesi](https://msdn.microsoft.com/library/6d4936ht.aspx)
- [Sağlayıcılar eklenirken `<clear />` kullanma](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx)
- [`SqlMembershipProvider` ile doğrudan çalışma](http://aspnet.4guysfromrolla.com/articles/091207-1.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>Bu öğreticide bulunan konularda video eğitimi

- [ASP.NET Üyeliklerini Anlama](../../../videos/authentication/understanding-aspnet-memberships.md)
- [SQL’yi Üyelik Şemalarıyla Çalışacak Biçimde Yapılandırma](../../../videos/authentication/configuring-sql-to-work-with-membership-schemas.md)
- [Varsayılan Üyelik Şemasında Üyelik Ayarlarını Değiştirme](../../../videos/authentication/changing-membership-settings-in-the-default-membership-schema.md)

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı Scott Mitchell, 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, *[24 saat içinde ASP.NET 2,0 kendi kendinize eğitim](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ister. Scott 'a [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) veya blogundan [http://ScottOnWriting.NET](http://scottonwriting.net/)üzerinden erişilebilir.

### <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için lider gözden geçiren Alicja Maziarz. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, beni [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)bir satır bırakın.

> [!div class="step-by-step"]
> [Önceki](storing-additional-user-information-cs.md)
> [İleri](creating-user-accounts-vb.md)
