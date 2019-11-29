---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-the-production-web-application-to-use-the-production-database-cs
title: Üretim Web uygulamasını üretim veritabanını (C#) kullanacak şekilde yapılandırma | Microsoft Docs
author: rick-anderson
description: Daha önceki öğreticilerde ele alındığı gibi, yapılandırma bilgilerinin geliştirme ve üretim ortamları arasında farklı olması yaygın olmayan bir durumdur. Bu es...
ms.author: riande
ms.date: 04/23/2009
ms.assetid: 0177dabd-d888-449f-91b2-24190cf5e842
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-the-production-web-application-to-use-the-production-database-cs
msc.type: authoredcontent
ms.openlocfilehash: 89941bb6db52316a259ad5f5577721e36f19bd84
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74635867"
---
# <a name="configuring-the-production-web-application-to-use-the-production-database-c"></a>Üretim Web Uygulamasını Üretim Veritabanını Kullanacak Şekilde Yapılandırma (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_08_CS.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial08_DBConfig_cs.pdf)

> Daha önceki öğreticilerde ele alındığı gibi, yapılandırma bilgilerinin geliştirme ve üretim ortamları arasında farklı olması yaygın olmayan bir durumdur. Veritabanı bağlantı dizeleri geliştirme ve üretim ortamları arasında farklılık gösterdiğinden, bu durum özellikle veri odaklı web uygulamaları için geçerlidir. Bu öğreticide, üretim ortamını, uygun bağlantı dizesini daha ayrıntılı olarak dahil etmek için yapılandırma yolları ele alır.

## <a name="introduction"></a>Giriş

Veri odaklı web uygulamaları, genellikle üretimde olduğu gibi geliştirmelerde farklı bir veritabanı kullanır. Bir Web ana makinesi tarafından barındırılan ve yerel olarak geliştirilen uygulamalar için, geliştirme veritabanı genellikle geliştirici s bilgisayarında bulunur, üretim veritabanı, Şirket içindeki Web barındırma tesisinde bir veritabanı sunucusunda barındırılır. Veri odaklı bir Web uygulamasının dağıtımı, geliştirme veritabanını üretim veritabanı sunucusuna kopyalamayı gerektirir. Önceki öğreticide, bu adımı gerçekleştirmenin yollarını inceledik.

Web uygulaması, veritabanıyla bağlantı kurmak için bir *bağlantı dizesindeki* bilgileri kullanır. Genellikle `Web.config`depolanan bağlantı dizesi, veritabanı sunucusu adını, veritabanının adını, güvenlik bağlamını ve diğer bilgileri belirtir. Web uygulaması tarafından kullanılan veritabanı, Web uygulamasının geliştirme veya üretim ortamlarında çalışıyor olmasına bağlı olduğundan, bağlantı dizelerinin iki ortam arasında farklı olması gerekir.

Yapılandırma bilgilerinin geliştirme ve üretim ortamları arasında farklı olması yaygın olmayan bir durumdur. *Geliştirme ve üretim öğreticisiyle Ilgili yaygın yapılandırma farkları* , bu iki ortam arasında ayrı yapılandırma bilgilerinin yanı sıra veritabanı bağlantı dizeleriyle ilgili kısa bir tartışma sağlayan teknikleri ele alır. Bu öğreticide, üretim ortamını, uygun bağlantı dizesini daha ayrıntılı olarak dahil etmek için yapılandırma yolları ele alır.

## <a name="examining-the-connection-string-information"></a>Bağlantı dizesi bilgilerini İnceleme

Kitap Incelemeleri Web uygulaması tarafından kullanılan bağlantı dizesi, `Web.config`uygulama yapılandırma dosyasında depolanır. `Web.config`, bağlantı dizelerini depolamak için [&lt;connectionStrings&gt;](https://msdn.microsoft.com/library/bf7sd233.aspx)adlı özel bir bölüm içerir. Book Incelemeleri Web sitesinin `Web.config` dosyasında, bu bölümde `ReviewsConnectionString`adında bir bağlantı dizesi tanımlanmış:

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-cs/samples/sample1.xml)]

Bağlantı dizesi-veri kaynağı = .\SQLEXPRESS; AttachDbFilename = | DataDirectory | \Edilecek S.mdf; Integrated Security = true; Kullanıcı örneği = true-noktalı virgülle ayrılmış seçenek/değer çiftleri ve bir eşittir işaretiyle ayrılmış her bir seçenek ve değer içeren bir dizi seçenekten ve değerden oluşur. Bu bağlantı dizesinde kullanılan dört seçenek şunlardır:

- `Data Source`-veritabanı sunucusunun konumunu ve veritabanı sunucu örneği adını (varsa) belirtir. `.\SQLEXPRESS`değeri, bir veritabanı sunucusu ve örnek adı olan bir örnektir. Bu süre, veritabanı sunucusunun uygulamayla aynı bilgisayarda olduğunu belirtir; örnek adı `SQLEXPRESS`.
- `AttachDbFilename`-veritabanı dosyasının konumunu belirtir. Değer, çalışma zamanında uygulama s `App_Data` klasörünün tam yoluna çözümlenen `|DataDirectory|`yer tutucu içerir.
- `Integrated Security`-veritabanına bağlanırken belirtilen bir kullanıcı adının/parolanın kullanılıp kullanılmayacağını belirten bir Boole değeri (false) veya geçerli Windows hesabı kimlik bilgileri (true).
- `User Instance`-yerel bilgisayarda yönetici olmayan kullanıcıların bir SQL Server Express sürümü veritabanına eklenip bağlanamayacağını belirten SQL Server Express sürümlerine özgü bir yapılandırma seçeneği. Bu ayar hakkında daha fazla bilgi için bkz. [SQL Server Express Kullanıcı örnekleri](https://msdn.microsoft.com/library/ms254504.aspx) .

İzin verilen bağlantı dizesi seçenekleri, bağlandığınız veritabanına ve kullanılmakta olan ADO.NET veritabanı sağlayıcısına bağlıdır. Örneğin, bir Microsoft SQL Server veritabanına bağlanmak için bağlantı dizesi, Oracle veritabanına bağlanmak için kullanılan öğesinden farklıdır. Benzer şekilde, SqlClient sağlayıcısı kullanılarak bir Microsoft SQL Server veritabanına bağlanmak, OLE-DB sağlayıcısını kullanırken farklı bir bağlantı dizesi kullanır.

Veritabanı bağlantı dizesini, [connectionStrings.com](http://www.connectionstrings.com/) gibi bir site olarak kullanılabilir seçenekler için bir kaynak olarak kullanarak el ile oluşturabilirsiniz. Ancak, daha kolay bir yaklaşım, veritabanını Visual Studio 'daki Sunucu Gezgini eklemek ve ardından Özellikler penceresi bağlantı dizesini almak için kullanılır. Bu ikinci tekniği, bağlantı dizesini üretim veritabanı sunucusuna oluşturmak için kullanın.

Visual Studio 'Yu açın ve Sunucu Gezgini penceresine gidin (Visual Web Developer 'da bu pencere Veritabanı Gezgini olarak adlandırılır). Veri bağlantıları seçeneğine sağ tıklayın ve bağlam menüsünde Bağlantı Ekle seçeneğini belirleyin. Bu, Şekil 1 ' de gösterilen Sihirbazı getirir. Uygun veri kaynağını seçin ve devam ' a tıklayın.

[![Sunucu Gezgini yeni bir veritabanı eklemeyi seçin](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image2.jpg)](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image1.jpg) 

**Şekil 1**: Sunucu Gezgini yeni bir veritabanı eklemeyi seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image3.jpg))

Ardından, çeşitli veritabanı bağlantı bilgilerini belirtin (bkz. Şekil 2). Web barındırma şirketiniz ile kaydolduğunuzda, veritabanına bağlanma hakkında bilgi (veritabanı sunucusu adı, veritabanı adı, veritabanına bağlanmak için kullanılacak Kullanıcı adı ve parola vb.) ile ilgili bilgiler verilmelidir. Bu bilgileri girdikten sonra, bu Sihirbazı tamamlayıp veritabanını Sunucu Gezgini eklemek için Tamam ' a tıklayın.

[![veritabanı bağlantı bilgilerini belirtin](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image5.jpg)](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image4.jpg) 

**Şekil 2**: veritabanı bağlantı bilgilerini belirtin ([tam boyutlu görüntüyü görüntülemek için tıklayın](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image6.jpg))

Üretim ortamı veritabanının artık Sunucu Gezgini listelenmesi gerekir. Sunucu Gezgini veritabanını seçin ve Özellikler penceresi gidin. Veritabanı s bağlantı dizesiyle bağlantı dizesi adlı bir özellik bulacaksınız. Üretimde ve SqlClient sağlayıcısında bir Microsoft SQL Server veritabanı kullandığınızı varsayarsak, bağlantı dizeniz aşağıdakine benzer olmalıdır:

<strong>Veri kaynağı =<em>ServerName</em>; İlk Katalog =<em>DatabaseName</em>; Kalıcı güvenlik bilgisi = doğru; Kullanıcı KIMLIĞI = Kullanıcı<em>adı</em>; Password =*parola</strong>*

Burada *ServerName*, *DatabaseName*, *UserName*ve *Password* , veritabanı sunucu adı, veritabanı adı ve Web ana bilgisayar şirketiniz tarafından size sağlanan Kullanıcı adı ve parola değerleri ile aynıdır.

## <a name="deploying-the-book-reviews-web-application"></a>Kitap Incelemeleri Web uygulamasını dağıtma

Önceki öğreticide geliştirme veritabanını üretim ortamına kopyalamayı ve veri odaklı uygulamanın dağıtılmasını araştırmadık. Bu noktada, üretim ortamı veritabanını içerir, ancak statik İncelemeleri olan kitap Incelemeleri uygulamasının sürümünü kullanıyor. Yeni, veri odaklı uygulamayı, güncelleştirilmiş yapılandırma bilgileriyle birlikte üretim sunucusuna dağıtmamız gerekir.

Veri odaklı uygulamanın geliştirme ortamından üretime dağıtılması için bir dakikanızı ayırın. Bu işlem, önceki öğreticilerde ayrıntılı olarak ele alınmıştır. Bir yenileyici gerekiyorsa, bir *FTP Istemcisi kullanarak Web sitenizi dağıtma* veya *Visual Studio öğreticileri kullanarak Web sitenizi dağıtma* bölümüne bakın. Üretim veritabanı bağlantı dizesinin üretim ortamında kullanılan bir tane olduğundan emin olmanız gerekir. Bu, alternatif bir `Web.config` dosyası dağıtılması gerektiği anlamına gelir. Özellikle, bu `Web.config` dosya `<connectionStrings>` öğesinin, üretim veritabanı bağlantı dizesini içermesi gerekir ve şuna benzer olmalıdır:

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-cs/samples/sample2.xml)]

`<connectionStrings>` öğesindeki bağlantı dizesinin aynı (`ReviewsConnectionString`) olarak adlandırdığına, ancak şimdi geliştirme veritabanı bağlantı dizesi yerine üretim veritabanı bağlantı dizesini içerdiğini unutmayın.

Daha fazla şekillendirilmiş bir dağıtım iş akışınız yoksa, dağıtım işleminin bir parçası olarak üretim ortamına yüklenen üretim ortamı yapılandırma bilgileri ile ayrı bir `Web.config` dosyasını (daha sonra geliştirme veritabanı bağlantı dizesi kullanmaya geri almak için hatırlama) kullanmak üzere `Web.config` dosyasını el ile değiştirin.

> [!NOTE]
> Geliştirme veritabanı bağlantı dizesini içeren bir `Web.config` dosyasını yanlışlıkla dağıtırsanız, üretimde uygulama veritabanına bağlanmaya çalıştığında bir hata olur. Bu hata, sunucu bulunamadığını bildiren veya erişilemeyen bir ileti ile `SqlException` olarak bildirimler.

Site üretime dağıtıldıktan sonra, tarayıcınız üzerinden üretim sitesini ziyaret edin. Veri odaklı uygulamayı yerel olarak çalıştırırken aynı kullanıcı deneyiminin aynısını görmeniz ve keyfini çıkarmanız gerekir. Üretim aşamasında Web sitesini ziyaret ettiğinizde, site üretim veritabanı sunucusu tarafından desteklenir, ancak geliştirme ortamındaki Web sitesini ziyaret etmek geliştirme aşamasında veritabanını kullanır. Şekil 3 ' te, üretim ortamındaki Web sitesindeki (tarayıcının adres çubuğundaki URL 'YI aklınızda bulunan) *24 saat Içinde kendinizi ASP.NET 3,5* inceleyin.

[![veri odaklı uygulama artık üretimde kullanılabilir!](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image8.jpg)](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image7.jpg) 

**Şekil 3**: veri odaklı uygulama artık üretimde kullanılabilir! ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image9.jpg))

### <a name="storing-connection-strings-in-a-separate-configuration-file"></a>Bağlantı dizelerini ayrı bir yapılandırma dosyasında depolama

Geliştirme ve üretim ortamlarında ayrı yapılandırma bilgilerinin korunmasında kullanılan yaygın bir teknik, `Web.config`bir geliştirme ortamı ve bir üretim için olmak üzere iki sürümüne sahiptir: Dağıtım zamanında uygun `Web.config` sürümü üretim ortamına kopyalanabilir. İdeal olarak, bu işlem dağıtım iş akışının bir parçası olarak otomatikleştirilebilir.

İki ayrı `Web.config` dosyasını sürdürmek yerine, isteğe bağlı olarak daha ayrıntılı farklılıklar sağlayabilirsiniz. `Web.config` dosyasını oluşturan öğeler, daha sonra `Web.config` dosyasında başvurulan bir dış yapılandırma dosyalarında tanımlanabilir. Bir kısaca 'de, her iki ortam için bir `Web.config` dosyanız olabilir. Bu, uygulama tarafından kullanılan bağlantı dizelerini içerir ve her ortam için benzersiz olacaktır. Farklı yapılandırma bilgilerini ayrı dosyalara ayıran tidier ve daha basit bir `Web.config` dosyası sağlar ve geliştirme ve üretim ortamları arasındaki yapılandırma farklarını daha net bir şekilde özetler.

Bu tekniği kullanmak için, `ConfigSections`adlı Web uygulamasında yeni bir klasör oluşturarak başlayın. Sonra, bu yeni klasöre databaseConnectionStrings. dev. config ve databaseConnectionStrings. Production. config adlı iki dosya ekleyin. Sonra, `Web.config` `<connectionStrings>` öğesini databaseConnectionStrings. dev. config ve databaseConnectionStrings. Production. config dosyalarına kopyalayın ve ardından databaseConnectionStrings. Production. config dosyasındaki bağlantı dizesini üretim veritabanı bağlantı dizesini belirten şekilde değiştirin. Örneğin, databaseConnectionStrings. dev. config dosyası yalnızca geliştirme veritabanına başvuran bir bağlantı dizesiyle `<connectionStrings>` öğesini içermelidir:

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-cs/samples/sample3.xml)]

Benzer şekilde, databaseConnectionStrings. Production. config dosyası yalnızca bir `<connectionStrings>` öğesi içermeli, ancak üretim veritabanı bağlantı dizesine sahip bir tane.

DatabaseConnectionStrings. dev. config dosyasının bir kopyasını oluşturun ve databaseConnectionStrings. config olarak adlandırın.

> [!NOTE]
> Yapılandırma dosyasını, `connectionStrings.config` veya `dbInfo.config`gibi d beğenmezseniz databaseConnectionStrings. config dışında bir şekilde adlandırın. Ancak, ASP.NET altyapısı tarafından sunulmayan, varsayılan olarak, `.config` dosyaları `.config` uzantılı dosyayı adlandırın. Dosyayı başka bir şey olarak adlandırırsanız `connectionStrings.txt`gibi bir Kullanıcı, tarayıcıyı [www.yoursite.com/configsettings/connectionStrings.txt](http://www.yoursite.com/ConfigSettings/connectionStrings.txt) 'ye işaret edip dosyanın içeriğini görüntüleyebilir!

Bu noktada `ConfigSections` klasörü üç dosya içermelidir (bkz. Şekil 4). DatabaseConnectionStrings. dev. config ve databaseConnectionStrings. Production. config dosyaları sırasıyla geliştirme ve üretim ortamları için bağlantı dizelerini içerir. DatabaseConnectionStrings. config dosyası, çalışma zamanında Web uygulaması tarafından kullanılacak olan bağlantı dizesi bilgilerini içerir. Sonuç olarak, databaseconnectionstrings. config dosyası geliştirme ortamındaki databaseConnectionStrings. dev. config dosyası ile aynı olmalıdır, ancak üretimde databaseConnectionStrings. config dosyası ile özdeş olmalıdır databaseConnectionStrings. Production. config.

[![ConfigSections](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image11.jpg)](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image10.jpg) 

**Şekil 4**: configSections ([tam boyutlu görüntüyü görüntülemek için tıklayın](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image12.jpg))

Artık `Web.config`, bağlantı dizesi deposu için databaseConnectionStrings. config dosyasını kullanmak üzere talimat veriyoruz. `Web.config` açın ve var olan `<connectionStrings>` öğesini aşağıdaki kodla değiştirin:

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-cs/samples/sample4.xml)]

`configSource` özniteliği, `Web.config` dosyasına göre fiziksel bir yol belirtir. Dış `.config` dosyası `Web.config` aynı dizinde ise, bu özniteliği `.config` dosyanın dosya adına ayarlayın. Bu bir alt dizinde bulunuyorsa databaseConnectionStrings. config dosyasında olduğu gibi, klasör ve dosya adlarını sınırlandırmak için ConfigSections\databaseConnectionStrings.config. gibi bir ters eğik çizgi kullanarak alt klasörü belirtin

Bu değişiklik ile, geliştirme ve üretim ortamları aynı `Web.config` dosyasını içerir. Artık tek fark databaseConnectionStrings. config dosyasıdır. DatabaseConnectionStrings. Production. config dosyasını üretime kopyalayın ve databaseConnectionStrings. config olarak yeniden adlandırın. Gelecekte, üretim veritabanı bağlantı dizesinde değişiklikler varsa, bunları databaseConnectionStrings. Production. config dosyasında yapmanız ve ardından dosyayı üretime yüklemeniz, databaseConnectionStrings. config dosyasını yeniden adlandırmanız gerekir.

> [!NOTE]
> Her bir `Web.config` öğesi için bilgileri ayrı bir dosyada belirtebilir ve `configSource` özniteliğini kullanarak bu dosyaya `Web.config`içinden başvurabilirsiniz.

## <a name="summary"></a>Özet

Veri odaklı uygulamalar genellikle geliştirme ve üretim ortamlarında farklı veritabanlarını kullanır. Sonuç olarak, Web uygulaması yapılandırmasında depolanan veritabanı bağlantı dizelerinin her ortam için benzersiz olması gerekir. Bu öğreticide, üretim veritabanı bağlantı dizesinin nasıl belirleneceğini ve iki ortamda benzersiz bağlantı dizesi bilgilerini nasıl koruyabilmenin yollarını inceledik.

Programlamanın kutlu olsun!

#### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Bağlantı Dizeleri ve Yapılandırma Dosyaları](https://msdn.microsoft.com/library/ms254494.aspx)
- [Veritabanı yapılandırma dizeleri bilgileri @ ConnectionStrings.com](http://www.connectionstrings.com/)
- [Ayarları Web. config dosyasının dışına taşı](http://www.asp101.com/tips/index.asp?id=154)
- [&lt;connectionStrings&gt; öğesi için teknik belgeler](https://msdn.microsoft.com/library/bf7sd233.aspx)

> [!div class="step-by-step"]
> [Önceki](deploying-a-database-cs.md)
> [İleri](configuring-a-website-that-uses-application-services-cs.md)
