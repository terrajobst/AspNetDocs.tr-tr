---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-elmah-cs
title: ELMAH ile hata ayrıntılarını günlüğe kaydetmeC#() | Microsoft Docs
author: rick-anderson
description: Hata günlüğü modülleri ve Işleyiciler (ELMAH), bir üretim ortamında çalışma zamanı hatalarının günlüğe kaydedilmesi için başka bir yaklaşım sunar. ELMAH, ücretsiz, açık kaynaklı bir hatadır...
ms.author: riande
ms.date: 06/09/2009
ms.assetid: 11f6fe44-64ef-4a38-a3b4-35c7bb992352
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-elmah-cs
msc.type: authoredcontent
ms.openlocfilehash: 5018023eced23e7a70eab90e649f85862c548940
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74570443"
---
# <a name="logging-error-details-with-elmah-c"></a>ELMAH ile Hata Ayrıntılarını Günlüğe Kaydetme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_14_CS.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial14_ELMAH_cs.pdf)

> Hata günlüğü modülleri ve Işleyiciler (ELMAH), bir üretim ortamında çalışma zamanı hatalarının günlüğe kaydedilmesi için başka bir yaklaşım sunar. ELMAH, hata filtreleme ve bir Web sayfasından hata günlüğünü görüntüleme (RSS akışı olarak) veya virgülle ayrılmış bir dosya olarak indirme yeteneği gibi özellikleri içeren ücretsiz, açık kaynaklı bir hata günlüğü kitaplığıdır. Bu öğretici, ELMAH 'yi indirip yapılandırmayı adım adım göstermektedir.

## <a name="introduction"></a>Giriş

[Önceki ÖĞRETICI](logging-error-details-with-asp-net-health-monitoring-cs.md) ASP 'yi inceledi. NET ' in geniş bir dizi Web olayını kaydetmek için kullanıma hazır bir kitaplık sunan NET sistem durumu izleme sistemi. Birçok geliştirici işlenmemiş özel durumların ayrıntılarını günlüğe kaydetmek ve e-posta ile almak için sistem durumu izleme kullanır Ancak, bu sistemle ilgili birkaç sorun vardır. İlk ve önkoşullarına, günlüğe kaydedilen olaylar hakkında bilgi görüntülemek için herhangi bir kullanıcı arabirimi sıralaması olmamasıdır. Son 10 hata ile ilgili bir Özet görmek veya geçen hafta oluşan bir hatanın ayrıntılarını görüntülemek istiyorsanız, veritabanına göz atın, e-posta gelen kutunuza göre tarama yapın veya `aspnet_WebEvent_Events` tablosundan bilgi görüntüleyen bir Web sayfası oluşturmanız gerekir.

Durum izlemenin karmaşıklığı etrafında başka bir sorun noktası merkezi. Sistem durumu izleme farklı olayların bir plethora kaydetmek için kullanılabilir ve olayların nasıl ve ne zaman günlüğe kaydedileceğini öğrenmek için çeşitli seçenekler bulunduğundan, sistem durumu izleme sisteminin doğru şekilde yapılandırılması bir onerou görevi olabilir. Son olarak, uyumluluk sorunları vardır. Sistem durumu izleme ilk olarak sürüm 2,0 ' deki .NET Framework eklendiğinden, ASP.NET sürüm 1. x kullanılarak oluşturulan eski Web uygulamaları için kullanılamaz. Üstelik, önceki öğreticide bir veritabanına hata ayrıntılarını günlüğe kaydeden `SqlWebEventProvider` sınıfı, yalnızca Microsoft SQL Server veritabanları ile birlikte kullanılabilir. Özel bir günlük sağlayıcısı sınıfı oluşturmanız gerekir, bu da hataları bir XML dosyası veya Oracle veritabanı gibi alternatif bir veri deposuna yazmanız gerekir.

Sistem durumu izleme sistemine bir alternatif, [atıf aziz](http://www.raboof.com/)tarafından oluşturulan ücretsiz, açık kaynaklı bir hata günlüğü sistemi olan hata günlüğü modülleri ve işleyiciler (ELMAH). İki sistem arasındaki en önemli fark, ELAMH 'in bir hata listesi ve bir Web sayfasından bir RSS akışı olarak belirli bir hatanın ayrıntılarını görüntüleme yeteneğidir. ELMAH, yalnızca hataları günlüğe kaydettiği için sistem durumu izlemenin daha kolay bir şekilde yapılandırılması. Ayrıca, ELMAH, ASP.NET 1. x, ASP.NET 2,0 ve ASP.NET 3,5 uygulamaları için destek içerir ve çeşitli günlük kaynağı sağlayıcılarıyla birlikte sunulur.

Bu öğreticide, bir ASP.NET uygulamasına ELMAH ekleme adımları gösterilmektedir. Haydi başlayın!

> [!NOTE]
> Sistem durumu izleme sistemi ve ELMAH 'nin her ikisi de kendi araç ve olumsuz yönleri kümelerine sahiptir. Her iki sistemi de denemenizi ve gereksinimlerinize en uygun olanı seçmeyi teşvik ediyorum.

## <a name="adding-elmah-to-an-aspnet-web-application"></a>ASP.NET Web uygulamasına ELMAH ekleme

ELMAH 'yi yeni veya mevcut bir ASP.NET uygulamasına tümleştirmek, beş dakika içinde geçen kolay ve kolay bir işlemdir. Bir Nutshell 'de, dört basit adımı içerir:

1. ELMAH 'yi indirin ve Web uygulamanıza `Elmah.dll` derlemeyi ekleyin,
2. ELMAH 'nin HTTP modüllerini ve Işleyicisini `Web.config`' de kaydedin,
3. ELMAH 'nin yapılandırma seçeneklerini belirtin ve
4. Gerekirse hata günlüğü kaynak altyapısını oluşturun.

Her seferinde bir kez olmak üzere bu dört adımın her birini inceleyelim.

### <a name="step-1-downloading-the-elmah-project-files-and-addingelmahdllto-your-web-application"></a>1\. Adım: ELMAH proje dosyalarını Indirme ve Web uygulamanıza`Elmah.dll`ekleme

ELMAH 1,0 BETA 3 (derleme 10617), yazma sırasında en son sürüm, bu öğreticide sunulan indirmeye dahil edilmiştir. Alternatif olarak, en son sürümü almak veya kaynak kodu indirmek için [ELMAH Web sitesini](https://code.google.com/p/elmah/) ziyaret edebilirsiniz. ELMAH indirme 'yi masaüstünüzdeki bir klasöre ayıklayın ve ELMAH derleme dosyasını (`Elmah.dll`) bulun.

> [!NOTE]
> `Elmah.dll` dosyası, farklı .NET Framework sürümleri ve serbest bırakma ve hata ayıklama yapıları için alt klasörlere sahip olan indirmenin `Bin` klasöründe bulunur. Uygun çerçeve sürümü için yayın derlemesini kullanın. Örneğin, bir ASP.NET 3,5 Web uygulaması oluşturuyorsanız, `Elmah.dll` dosyayı `Bin\net-3.5\Release` klasöründen kopyalayın.

Ardından, Visual Studio 'Yu açın ve Çözüm Gezgini Web sitesinin adına sağ tıklayıp bağlam menüsünden başvuru Ekle ' yi seçerek derlemeyi projenize ekleyin. Bu, başvuru Ekle iletişim kutusunu açar. Gözden geçirme sekmesine gidin ve `Elmah.dll` dosyasını seçin. Bu eylem, `Elmah.dll` dosyasını Web uygulamasının `Bin` klasörüne ekler.

> [!NOTE]
> Web uygulaması projesi (WAP) türü, Çözüm Gezgini `Bin` klasörü göstermez. Bunun yerine, bu öğeleri başvurular klasörü altında listeler.

`Elmah.dll` derlemesi ELMAH sistemi tarafından kullanılan sınıfları içerir. Bu sınıflar üç kategoriden birinde yer almalıdır:

- **Http modülleri** -http modülü, `Error` olayı gibi `HttpApplication` olaylar için olay işleyicilerini tanımlayan bir sınıftır. ELMAH, birden çok HTTP modülü içerir, en çok şu üç yanıt: 

    - `ErrorLogModule`, işlenmemiş özel durumları bir günlük kaynağına kaydeder.
    - `ErrorMailModule`-bir e-posta iletisindeki işlenmeyen bir özel durumun ayrıntılarını gönderir.
    - `ErrorFilterModule`-hangi özel durumların günlüğe kaydedileceğini ve bunların yoksayıldığını belirlemek için geliştiriciyle belirtilen filtreleri uygular.
- **Http işleyicileri** -http işleyicisi, belirli bir istek türü için biçimlendirme oluşturmaktan sorumlu bir sınıftır. ELMAH, hata ayrıntılarını bir Web sayfası olarak, RSS akışı olarak veya virgülle ayrılmış dosya (CSV) olarak işleyen HTTP Işleyicileri içerir.
- **Hata günlüğü kaynakları** -ELMAH, bir Microsoft SQL Server veritabanına, bir Microsoft Access veritabanına, bir Oracle veritabanına, bir XML dosyasına, bir SQLite veritabanına veya BIR Vista db veritabanına hataları günlüğe kaydedebilir. Sistem durumu izleme sistemi gibi, ELMAH 'nin mimarisi sağlayıcı modeli kullanılarak oluşturulmuştur; bu da, gerekirse kendi özel günlük kaynak sağlayıcınızı oluşturabileceğiniz ve sorunsuz bir şekilde tümleştirebileceğinizi belirtir.

### <a name="step-2-registering-elmahs-http-module-and-handler"></a>2\. Adım: ELMAH 'nin HTTP modülünü ve Işleyicisini kaydetme

`Elmah.dll` dosyası işlenmemiş özel durumları otomatik olarak günlüğe kaydetmek ve bir Web sayfasından hata ayrıntılarını göstermek için gereken HTTP modüllerini ve Işleyiciyi içerdiğinde, bunların Web uygulamasının yapılandırmasında açık bir şekilde kaydedilmesi gerekir. `ErrorLogModule` HTTP modülü kaydedildikten sonra `HttpApplication``Error` olayına abone olur. Bu olay her oluşturulduğunda `ErrorLogModule` özel durumun ayrıntılarını belirtilen günlük kaynağına kaydeder. "ELMAH 'yi yapılandırma" başlıklı sonraki bölümde günlük kaynak sağlayıcısını nasıl tanımlayacağınızı inceleyeceğiz. `ErrorLogPageFactory` HTTP Işleyici fabrikası, bir Web sayfasından hata günlüğü görüntülenirken biçimlendirmeyi oluşturmaktan sorumludur.

HTTP modülleri ve Işleyicileri kaydettirmek için özel sözdizimi, siteyi destekleyen Web sunucusuna bağlıdır. ASP.NET Development Server ve Microsoft 'un IIS sürüm 6,0 ve önceki sürümleri için, HTTP modülleri ve Işleyicileri `<system.web>` öğesi içinde görüntülenen `<httpModules>` ve `<httpHandlers>` bölümlerine kaydedilir. IIS 7,0 kullanıyorsanız, `<system.webServer>` öğenin `<modules>` ve `<handlers>` bölümlerinde kayıtlı olmaları gerekir. Neyse ki, kullanılan Web sunucusundan bağımsız olarak *her iki* yerde de http modülleri ve işleyicileri tanımlayabilirsiniz. Bu seçenek, kullanılan Web sunucusundan bağımsız olarak geliştirme ve üretim ortamlarında aynı yapılandırmanın kullanılmasına izin verdiği için en çok taşınabilir bir seçenektir.

`ErrorLogModule` HTTP modülünü ve `ErrorLogPageFactory` HTTP Işleyicisini, `<system.web>``<httpModules>` ve `<httpHandlers>` bölümüne kaydederek başlayın. Yapılandırmanız zaten bu iki öğeyi tanımlarsa, ELMAH 'nin HTTP modülü ve Işleyicisi için `<add>` öğesini de dahil edin.

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample1.xml)]

Sonra, `<system.webServer>` öğesinde ELMAH 'un HTTP modülünü ve Işleyicisini kaydettirin. Daha önce olduğu gibi, bu öğe zaten yapılandırmanızda yoksa ekleyin.

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample2.xml)]

Varsayılan olarak, HTTP modülleri ve Işleyicileri `<system.web>` bölümünde kayıtlıysa IIS 7 şikayet edilir. `<validation>` öğesindeki `validateIntegratedModeConfiguration` özniteliği, IIS 7 ' nin bu tür hata iletilerini gizmesini sağlar.

`ErrorLogPageFactory` HTTP Işleyicisini kaydetme sözdiziminin `elmah.axd`olarak ayarlanan bir `path` özniteliği içerdiğini unutmayın. Bu öznitelik, `elmah.axd` adlı bir sayfaya istek geldiğinde Web uygulamasına, isteğin `ErrorLogPageFactory` HTTP Işleyicisi tarafından işlenmesi gerektiğini bildirir. `ErrorLogPageFactory` HTTP Işleyicisini Bu öğreticinin ilerleyen kısımlarında göreceğiz.

### <a name="step-3-configuring-elmah"></a>3\. Adım: ELMAH 'yi yapılandırma

ELMAH, `<elmah>`adlı özel bir yapılandırma bölümünde Web sitesinin `Web.config` dosyasındaki yapılandırma seçeneklerini arar. `Web.config` ' de bir özel bölüm kullanabilmek için öncelikle `<configSections>` öğesinde tanımlanması gerekir. `Web.config` dosyasını açın ve aşağıdaki biçimlendirmeyi `<configSections>`ekleyin:

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample3.xml)]

> [!NOTE]
> Bir ASP.NET 1. x uygulaması için ELMAH yapılandırıyorsanız, `requirePermission="false"` özniteliğini yukarıdaki `<section>` öğelerinden kaldırın.

Yukarıdaki sözdizimi, özel `<elmah>` bölümü ve alt bölümleri kaydeder: `<security>`, `<errorLog>`, `<errorMail>`ve `<errorFilter>`.

Sonra, `Web.config``<elmah>` bölümünü ekleyin. Bu bölüm `<system.web>` öğesiyle aynı düzeyde görünmelidir. `<elmah>` bölümü içinde, `<security>` ve `<errorLog>` bölümlerini şu şekilde ekleyin:

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample4.xml)]

`<security>` bölümün `allowRemoteAccess` özniteliği, uzaktan erişime izin verilip verilmeyeceğini belirtir. Bu değer 0 olarak ayarlanırsa, hata günlüğü Web sayfası yalnızca yerel olarak görüntülenebilir. Bu öznitelik 1 olarak ayarlandıysa, uzak ve yerel ziyaretçiler için hata günlüğü Web sayfası etkinleştirilir. Şimdilik, uzak ziyaretçilerin hata günlüğü Web sayfasını devre dışı bırakalim. Bunu yapmanın güvenlik konusundaki kaygılarını tartıştığımız daha sonra uzaktan erişime izin vereceğiz.

`<errorLog>` bölümü, hata ayrıntılarının nerede kaydedileceğini belirleyen hata günlüğü kaynağını tanımlar; sistem durumu izleme sistemindeki `<providers>` bölümüne benzer. Yukarıdaki sözdizimi, hataları `connectionStringName` öznitelik değeri tarafından belirtilen bir Microsoft SQL Server veritabanına kaydeden hata günlüğü kaynağı olarak `SqlErrorLog` sınıfını belirtir.

> [!NOTE]
> ELMAH, hataları bir XML dosyasına, bir Microsoft Access veritabanına, Oracle veritabanına ve diğer veri depolarına kaydetmek için kullanılabilecek ek hata günlüğü sağlayıcılarıyla birlikte gönderilir. Bu alternatif hata günlüğü sağlayıcılarının nasıl kullanılacağı hakkında bilgi için, ELMAH indirme ile birlikte gelen örnek `Web.config` dosyasına bakın.

### <a name="step-4-creating-the-error-log-source-infrastructure"></a>4\. Adım: hata günlüğü kaynak altyapısını oluşturma

ELMAH `SqlErrorLog` sağlayıcısı, belirtilen Microsoft SQL Server veritabanına hata ayrıntılarını günlüğe kaydeder. `SqlErrorLog` sağlayıcı bu veritabanının `ELMAH_Error` ve üç saklı yordam adlı bir tabloya sahip olmasını bekler: `ELMAH_GetErrorsXml`, `ELMAH_GetErrorXml`ve `ELMAH_LogError`. ELMAH indirmesi, bu tabloyu ve bu saklı yordamları oluşturmak için T-SQL ' y i içeren `db` klasöründe `SQLServer.sql` adlı bir dosya içerir. `SqlErrorLog` sağlayıcıyı kullanmak için bu deyimleri veritabanınızda çalıştırmanız gerekir.

**Şekil 1** ve **2** `SqlErrorLog` sağlayıcısı için gereken veritabanı nesneleri eklendikten sonra Visual Studio 'da veritabanı Gezgini görüntüleyin.

[![](logging-error-details-with-elmah-cs/_static/image2.png)](logging-error-details-with-elmah-cs/_static/image1.png)

**Şekil 1**: `SqlErrorLog` sağlayıcı hataları `ELMAH_Error` tablosuna kaydeder

[![](logging-error-details-with-elmah-cs/_static/image4.png)](logging-error-details-with-elmah-cs/_static/image3.png)

**Şekil 2**: `SqlErrorLog` sağlayıcı üç saklı yordam kullanır

## <a name="elmah-in-action"></a>ELMAH, eylemde

Bu noktada, Web uygulamasına ELMAH ekledik, `ErrorLogModule` HTTP modülünü ve `ErrorLogPageFactory` HTTP `Web.config`Işleyicisini kaydettiniz ve `SqlErrorLog` hata günlüğü sağlayıcısı için gerekli veritabanı nesnelerini ekledik. Şimdi de ELMAH 'yi görmek için hazırsınız! Book Incelemeleri Web sitesini ziyaret edin ve `Genre.aspx?ID=foo`gibi bir çalışma zamanı hatası oluşturan bir sayfayı veya `NoSuchPage.aspx`gibi mevcut olmayan bir sayfayı ziyaret edin. Bu sayfaları ziyaret ederken gördükleriniz `<customErrors>` yapılandırmaya bağlıdır ve yerel olarak veya uzaktan ziyaret edilip edilmeyeceğini belirtir. (Bu konudaki Yenileyici için [ *özel hata sayfası* öğreticisine](displaying-a-custom-error-page-cs.md) geri bakın.)

ELMAH, işlenmeyen bir özel durum oluştuğunda kullanıcıya hangi içeriğin gösterildiğini etkilemez; yalnızca ayrıntılarını günlüğe kaydeder. Bu hata günlüğüne Web sayfasından `elmah.axd`, `http://localhost/BookReviews/elmah.axd`gibi Web sitenizin kökünden erişilebilir. (Bu dosya projenizde fiziksel olarak mevcut değil, ancak `elmah.axd` için bir istek geldiğinde, çalışma zamanı, tarayıcıya geri gönderilen biçimlendirmeyi oluşturan `ErrorLogPageFactory` HTTP Işleyicisine dağıtır.)

> [!NOTE]
> Ayrıca, bir sınama hatası oluşturmak üzere ELMAH 'e yönlendirmek için `elmah.axd` sayfasını kullanabilirsiniz. `elmah.axd/test` ziyaret eden (`http://localhost/BookReviews/elmah.axd/test`), ELMAH 'in, hata iletisine sahip `Elmah.TestException`türünde bir özel durum oluşturmasına neden olur: "Bu, güvenle yoksayılabilir bir test istisnadır."

**Şekil 3** ' te, geliştirme ortamından `elmah.axd` ziyaret edildiğinde hata günlüğü gösterilmektedir.

[![](logging-error-details-with-elmah-cs/_static/image6.png)](logging-error-details-with-elmah-cs/_static/image5.png)

**Şekil 3**: `Elmah.axd` bir Web sayfasından hata günlüğünü görüntüler  
([Tam boyutlu görüntüyü görüntülemek Için tıklayın](logging-error-details-with-elmah-cs/_static/image7.png))

**Şekil 3** ' te hata günlüğü altı hata girişi içerir. Her giriş HTTP durum kodunu (404 veya 500, bu hatalar için), türü, açıklamayı, hata oluştuğunda oturum açan kullanıcının adını ve Tarih ve saati içerir. Ayrıntılar bağlantısına tıkladığınızda hata ayrıntıları sarı ekran hatası (bkz. **Şekil 4**) ve hata sırasında sunucu değişkenlerinin değerleriyle birlikte gösterilen aynı hata iletisini içeren bir sayfa görüntülenir (bkz. **Şekil 5**). Ayrıca, HTTP POST üstbilgisindeki değerler gibi ek bilgiler içeren hata ayrıntılarının kaydedildiği ham XML 'i görüntüleyebilirsiniz.

[![](logging-error-details-with-elmah-cs/_static/image9.png)](logging-error-details-with-elmah-cs/_static/image8.png)

**Şekil 4**: hata ayrıntılarını görüntüleme YSOD  
([Tam boyutlu görüntüyü görüntülemek Için tıklayın](logging-error-details-with-elmah-cs/_static/image10.png))

[![](logging-error-details-with-elmah-cs/_static/image12.png)](logging-error-details-with-elmah-cs/_static/image11.png)

**Şekil 5**: hata sırasında sunucu değişkenleri koleksiyonunun değerlerini keşfet  
([Tam boyutlu görüntüyü görüntülemek Için tıklayın](logging-error-details-with-elmah-cs/_static/image13.png))

ELMAH 'yi üretim Web sitesine dağıtmak şunları kapsar:

- `Elmah.dll` dosyasını üretimde `Bin` klasörüne kopyalama,
- ELMAH 'e özgü yapılandırma ayarlarını üretimde kullanılan `Web.config` dosyasına kopyalama ve
- Hata günlüğü kaynak altyapısı üretim veritabanına ekleniyor.

Dosyaları geliştirmede önceki öğreticilerde kopyalamaya yönelik teknikleri araştırdık. Üretim veritabanında hata günlüğü kaynak altyapısını almanın en kolay yolu, üretim veritabanına bağlanmak ve ardından gerekli tablo ve saklı yordamları oluşturacak `SqlServer.sql` betik dosyasını yürütmek için SQL Server Management Studio kullanmaktır.

### <a name="viewing-the-error-details-page-on-production"></a>Üretimde hata ayrıntıları sayfasını görüntüleme

Sitenizi üretime dağıttıktan sonra üretim Web sitesini ziyaret edin ve işlenmeyen bir özel durum oluşturun. Geliştirme ortamında olduğu gibi, işlenmeyen bir özel durum oluştuğunda, ELMAH hata sayfasında görünen bir etkisi yoktur; Bunun yerine, yalnızca hatayı günlüğe kaydeder. Üretim ortamından hata günlüğü sayfasını (`elmah.axd`) ziyaret etmeye çalışırsanız, **Şekil 6**' da gösterilen yasak sayfayla dolanacaktır.

[![](logging-error-details-with-elmah-cs/_static/image15.png)](logging-error-details-with-elmah-cs/_static/image14.png)

**Şekil 6**: varsayılan olarak uzak ziyaretçiler hata günlüğü Web sayfasını görüntüleyemez  
([Tam boyutlu görüntüyü görüntülemek Için tıklayın](logging-error-details-with-elmah-cs/_static/image16.png))

ELMAH yapılandırmasının `<security>` bölümünde, uzak kullanıcıların hata günlüğünü görüntülemesini önleyen `allowRemoteAccess` özniteliğini 0 olarak ayarlayacağız. Hata ayrıntıları güvenlik açıklarını veya diğer hassas bilgileri açığa çıkardığından, anonim ziyaretçilerin hata günlüğünü görüntülemesini önlemek önemlidir. Bu özniteliği 1 olarak ayarlamaya karar verirseniz ve hata günlüğüne uzaktan erişimi etkinleştirmek istiyorsanız, yalnızca yetkili ziyaretçilerin erişebilmesi için `elmah.axd` yolunu kilitlemek önemlidir. Bu, `Web.config` dosyasına bir `<location>` öğesi eklenerek elde edilebilir.

Aşağıdaki yapılandırma yalnızca yönetici rolündeki kullanıcıların hata günlüğü Web sayfasına erişmesine izin verir:

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample5.xml)]

> [!NOTE]
> Yönetici rolü ve System-Scott, Jisun ve Gamze içindeki üç Kullanıcı, [ *uygulama hizmetleri öğreticisini kullanan bir Web sitesini yapılandırma* ](configuring-a-website-that-uses-application-services-cs.md)konusuna eklenmiştir. Scott ve Jisun kullanıcıları yönetici rolünün üyeleridir. Kimlik doğrulama ve yetkilendirme hakkında daha fazla bilgi için Web sitemin [güvenlik öğreticilerime](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)bakın.

Üretim ortamındaki hata günlüğü artık uzak kullanıcılar tarafından görüntülenebilir; hata günlüğü Web sayfasının ekran görüntüleri için **Şekil 3**, **4**ve **5** ' e geri bakın. Ancak, anonim veya yönetici olmayan bir kullanıcı hata günlüğü sayfasını görüntülemeyi denerse, **Şekil 7** ' de gösterildiği gibi otomatik olarak oturum açma sayfasına (`Login.aspx`) yönlendirilir.

[![](logging-error-details-with-elmah-cs/_static/image18.png)](logging-error-details-with-elmah-cs/_static/image17.png)

**Şekil 7**: yetkisiz kullanıcılar otomatik olarak oturum açma sayfasına yönlendirilir  
([Tam boyutlu görüntüyü görüntülemek Için tıklayın](logging-error-details-with-elmah-cs/_static/image19.png))

### <a name="programmatically-logging-errors"></a>Programlı olarak günlüğe kaydetme hataları

ELMAH `ErrorLogModule` HTTP modülü, işlenmeyen özel durumları belirtilen günlük kaynağına otomatik olarak günlüğe kaydeder. Alternatif olarak, `ErrorSignal` sınıfını ve `Raise` yöntemini kullanarak işlenmeyen bir özel durum oluşturmadan bir hatayı günlüğe kaydedebilirsiniz. `Raise` yöntemine `Exception` bir nesne geçirilir ve bu özel durum oluşturulsa ve ASP.NET çalışma zamanına ulaşılmadan ulaşmış gibi günlüğe kaydedilir. Ancak, bunun farkı, `Raise` yöntemi çağrıldıktan sonra isteğin normal şekilde yürütülmeye devam etmesine neden olur, ancak bu, işlenmemiş bir özel durum isteğin normal yürütmesini keser ve ASP.NET çalışma zamanının yapılandırılan hata sayfasını görüntülemesine neden olur.

`ErrorSignal` sınıfı, başarısız olabilecek bazı eylemler olduğu durumlarda faydalıdır, ancak hata sorunu gerçekleştirilen genel işleme karşı çok önemli değildir. Örneğin, bir Web sitesi kullanıcının girişini alan bir form içerebilir, onu bir veritabanında depolar ve sonra kullanıcılara bilgilerin işlendiğini bildiren bir e-posta gönderir. Bilgiler veritabanına başarıyla kaydedilirse, ancak e-posta iletisi gönderilirken bir hata var mı? Bir seçenek, bir özel durum oluşturmak ve kullanıcıyı hata sayfasına göndermek olacaktır. Bununla birlikte, bu durum kullanıcıyı, girdikleri bilgilerin kaydedilmediğinden emin olmak için şaşırtır. Başka bir yaklaşım da e-posta ile ilgili hatayı günlüğe kaydetmek, ancak kullanıcının deneyimini herhangi bir şekilde değiştirmemelidir. Burada `ErrorSignal` sınıfı yararlı olur.

[!code-csharp[Main](logging-error-details-with-elmah-cs/samples/sample6.cs)]

## <a name="error-notification-via-email"></a>E-posta Ile hata bildirimi

ELMAH, hataları bir veritabanına kaydetmeye ve ayrıca belirli bir alıcıya hata ayrıntılarını e-posta olarak da yapılandırılabilir. Bu işlevsellik `ErrorMailModule` HTTP modülü tarafından sağlanır; Bu nedenle, hata ayrıntılarını e-posta ile göndermek için `Web.config` bu HTTP modülünü kaydetmeniz gerekir.

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample7.xml)]

Sonra, e-postanın göndereni ve alıcısını, konusunu ve e-postanın zaman uyumsuz olarak gönderilip gönderilmediğini belirten `<elmah>` öğenin `<errorMail>` bölümündeki hata e-postası hakkında bilgi belirtin.

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample8.xml)]

Yukarıdaki ayarlarla birlikte, bir çalışma zamanı hatası oluştuğunda ELMAH, hata ayrıntılarına sahip support@example.com bir e-posta gönderir. ELMAH 'un hata e-postası, hata ayrıntıları Web sayfasında gösterilen bilgileri, hata iletisi, yığın izlemesi ve sunucu değişkenleri ( **Şekil 4** ve **5**' e geri başvuru) içerir. Hata e-postası Ayrıca bir ek (`YSOD.html`) olarak ölüm dışı içeriğin özel durum ayrıntıları sarı ekranını da içerir.

**Şekil 8** ' de `Genre.aspx?ID=foo`ziyaret ederek, ELMAH 'nin hata e-postası gösterilmektedir. **Şekil 8** yalnızca hata iletisini ve yığın izlemesini gösterirken, sunucu değişkenleri e-postanın gövdesinde daha aşağı dahil edilir.

[![](logging-error-details-with-elmah-cs/_static/image21.png)](logging-error-details-with-elmah-cs/_static/image20.png)

**Şekil 8**: ELMAH 'Yi, e-posta Ile hata ayrıntılarını gönderecek şekilde yapılandırabilirsiniz  
([Tam boyutlu görüntüyü görüntülemek Için tıklayın](logging-error-details-with-elmah-cs/_static/image22.png))

## <a name="only-logging-errors-of-interest"></a>Yalnızca Ilgilendiğiniz hataları günlüğe kaydetme

Varsayılan olarak, ELMAH, 404 ve diğer HTTP hataları da dahil olmak üzere işlenmemiş her özel durumun ayrıntılarını günlüğe kaydeder. Aynı hata filtrelemesini kullanarak bu veya diğer hata türlerini yok saymaya yönelik ELMAH söyleyebilirsiniz. Filtreleme mantığı ELMAH 'nin `ErrorFilterModule` HTTP modülü tarafından gerçekleştirilir, bu da filtreleme mantığını kullanmak için `Web.config` kaydetmeniz gerekir. Filtreleme kuralları `<errorFilter>` bölümünde belirtilmiştir.

Aşağıdaki biçimlendirme ELMAH 'e 404 hatalarını günlüğe kaydetme talimatını verir.

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample9.xml)]

> [!NOTE]
> Unutmayın, hata filtrelemesini kullanmak için `ErrorFilterModule` HTTP modülünü kaydetmeniz gerekir.

`<test>` bölümünün içindeki `<equal>` öğesi bir onaylama olarak adlandırılır. Onaylama doğru olarak değerlendirilirse, hata ELMAH 'nin günlüğünden filtrelenir. `<greater>`, `<greater-or-equal>`, `<not-equal>`, `<lesser>`, `<lesser-or-equal>`vb. gibi başka onaylar mevcuttur. Ayrıca, `<and>` ve `<or>` Boole işleçlerini kullanarak onayları birleştirebilirsiniz. Üstelik, bir onaylama olarak basit bir JavaScript ifadesi de içerebilir veya kendi onaylarınızı C# veya Visual Basic yazabilirsiniz.

ELMAH 'un hata filtreleme özellikleri hakkında daha fazla bilgi için, [ELMAH wiki](https://code.google.com/p/elmah/w/list)'Deki [hata filtreleme bölümüne](https://code.google.com/p/elmah/wiki/ErrorFiltering) bakın.

## <a name="summary"></a>Özet

ELMAH, bir ASP.NET Web uygulamasında hataları günlüğe kaydetmek için basit, ancak güçlü bir mekanizma sağlar. Aynı Microsoft 'un sistem durumu izleme sistemi gibi, ELMAH hataları bir veritabanına kaydedebilir ve hata ayrıntılarını e-posta yoluyla bir geliştiriciye gönderebilir. Sistem durumu izleme sisteminin aksine ELMAH, Microsoft SQL Server, Microsoft Access, Oracle, XML dosyaları ve diğer birçok hata günlüğü veri deposu için kullanıma hazır destek içerir. Üstelik, ELMAH, hata günlüğünü ve bir Web sayfasından belirli bir hata hakkındaki ayrıntıları görüntülemek için yerleşik bir mekanizma sunar `elmah.axd`. `elmah.axd` sayfası, hata bilgilerini bir RSS akışı olarak veya Microsoft Excel kullanarak okuyabilmeniz için virgülle ayrılmış bir değer dosyası (CSV) olarak da işleyebilir. Ayrıca, bildirim temelli veya programlı onaylar kullanarak günlükteki hataları filtrelemeye da yol açabilir. Ve ELMAH, ASP.NET sürüm 1. x uygulamalarıyla birlikte kullanılabilir.

Dağıtılan her uygulamanın, işlenmemiş özel durumları otomatik olarak günlüğe kaydetmek ve geliştirme ekibine bildirim göndermek için bir mekanizmaya sahip olması gerekir. Bu durum, sistem durumu izleme kullanılarak mı yoksa ELMAH 'in mi ikincildir? Diğer bir deyişle, sistem durumu izleme veya ELMAH kullanma konusunda büyük bir önemi yoktur. Her iki sistemi de değerlendirin ve gereksinimlerinize en uygun olanı seçin. Temel olarak önemli olan özellikler, bazı mekanizmanın üretim ortamında işlenmemiş özel durumları günlüğe kaydetmek için yerleştirilme örneğidir.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ELMAH-hata günlüğü modülleri ve Işleyiciler](http://dotnetslackers.com/articles/aspnet/ErrorLoggingModulesAndHandlers.aspx)
- [ELMAH proje sayfası](https://code.google.com/p/elmah/) (kaynak kodu, örnekler, wiki)
- [Işlenmemiş özel durumları yakalamak için bir Web uygulamasına ELMAH 'Yi takma](http://screencastaday.com/ScreenCasts/43_Plugging_Elmah_into_Web_Application_to_Catch_Unhandled_Exceptions.aspx) (video)
- [Güvenlik hata günlüğü sayfaları](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)
- [Takılabilir ASP.NET bileşenleri oluşturmak için HTTP modülleri ve Işleyicileri kullanma](https://msdn.microsoft.com/library/aa479332.aspx)
- [Web sitesi güvenlik öğreticileri](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)

> [!div class="step-by-step"]
> [Önceki](logging-error-details-with-asp-net-health-monitoring-cs.md)
> [İleri](precompiling-your-website-cs.md)
