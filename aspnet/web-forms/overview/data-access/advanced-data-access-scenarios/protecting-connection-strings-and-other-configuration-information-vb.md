---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/protecting-connection-strings-and-other-configuration-information-vb
title: Bağlantı dizelerini ve diğer yapılandırma bilgilerini koruma (VB) | Microsoft Docs
author: rick-anderson
description: Bir ASP.NET uygulaması genellikle yapılandırma bilgilerini bir Web. config dosyasında depolar. Bu bilgilerden bazıları hassas ve belirli bir koruma. Def öğesine göre...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: cd17dbe1-c5e1-4be8-ad3d-57233d52cef1
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/protecting-connection-strings-and-other-configuration-information-vb
msc.type: authoredcontent
ms.openlocfilehash: 070e1dccb80ef9af21ea621357c5b23e2ada6f9f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78524656"
---
# <a name="protecting-connection-strings-and-other-configuration-information-vb"></a>Bağlantı Dizelerini ve Diğer Yapılandırma Bilgilerini Koruma (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_73_VB.zip) veya [PDF 'yi indirin](protecting-connection-strings-and-other-configuration-information-vb/_static/datatutorial73vb1.pdf)

> Bir ASP.NET uygulaması genellikle yapılandırma bilgilerini bir Web. config dosyasında depolar. Bu bilgilerden bazıları hassas ve belirli bir koruma. Varsayılan olarak, bu dosya bir Web sitesi ziyaretçisine sunulmayacak, ancak bir yönetici veya korsan Web sunucusunun dosya sistemine erişim elde edebilir ve dosyanın içeriğini görüntüleyebilir. Bu öğreticide, ASP.NET 2,0 ' nin, Web. config dosyasının bölümlerini şifreleyerek hassas bilgileri korumamıza izin verdiğini öğreniyoruz.

## <a name="introduction"></a>Giriş

ASP.NET uygulamaları için yapılandırma bilgileri genellikle `Web.config`adlı bir XML dosyasında depolanır. Bu öğreticilerin kursunda `Web.config` çok kez güncelleştirdik. [İlk öğreticide](../introduction/creating-a-data-access-layer-vb.md)`Northwind` türü belirtilmiş veri kümesini oluştururken, örneğin, bağlantı dizesi bilgileri `<connectionStrings>` bölümünde `Web.config` otomatik olarak eklenmiştir. Daha sonra, [ana sayfalarda ve site gezinti](../introduction/master-pages-and-site-navigation-vb.md) öğreticisinde `Web.config`el ile güncelleştirdik, bu, projemizdeki tüm ASP.NET sayfalarının `DataWebControls` temasını kullanması gerektiğini belirten bir `<pages>` öğesi ekliyor.

`Web.config` bağlantı dizeleri gibi hassas veriler içerebildiği için, `Web.config` içeriğinin güvenli tutulması ve yetkisiz görüntüleyicilerden gizlenmesi önemlidir. Varsayılan olarak, `.config` uzantılı bir dosyaya yapılan HTTP istekleri, Şekil 1 ' de gösterilen *Bu sayfa türünü* döndüren ASP.NET altyapısı tarafından işlenir. Bu, ziyaretçilerin `Web.config` dosya içeriğinizi yalnızca tarayıcının adres çubuğuna http://www.YourServer.com/Web.config girerek görüntüleyemeyeceği anlamına gelir.

[Web. config dosyasını bir tarayıcı aracılığıyla ziyaret ![, bu tür bir sayfada sunulmayan bir Ileti döndürür](protecting-connection-strings-and-other-configuration-information-vb/_static/image2.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image1.png)

**Şekil 1**: tarayıcı aracılığıyla `Web.config` ziyaret etmek, bu tür bir sayfada sunulmayan bir ileti döndürüyor ([tam boyutlu görüntüyü görüntülemek için tıklayın](protecting-connection-strings-and-other-configuration-information-vb/_static/image3.png))

Ancak bir saldırgan, `Web.config` dosya içeriklerini görüntülemesine izin veren başka bir yararlanma işlemi de bulabiliyor mu? Bu bilgilerle bir saldırgan ne yapabilir ve `Web.config`içindeki hassas bilgileri korumak için hangi adımlar alınabilir? Neyse ki `Web.config` çoğu bölüm hassas bilgiler içermez. ASP.NET sayfalarınız tarafından kullanılan varsayılan temanın adını bildiklerinde saldırganlar ne kadar zararlı olabilir?

Ancak, bazı `Web.config` bölümler, bağlantı dizeleri, Kullanıcı adları, parolalar, sunucu adları, şifreleme anahtarları ve benzeri olabilecek gizli bilgiler içerir. Bu bilgiler genellikle aşağıdaki `Web.config` bölümlerinde bulunur:

- `<appSettings>`
- `<connectionStrings>`
- `<identity>`
- `<sessionState>`

Bu öğreticide, bu tür hassas yapılandırma bilgilerini koruma tekniklerini inceleyeceğiz. .NET Framework sürüm 2,0, seçilen yapılandırma bölümlerinin bir Breeze olarak şifrelenmesini ve şifresini çözmesini sağlayan bir korumalı yapılandırmalar sistemi içerir.

> [!NOTE]
> Bu öğretici, bir ASP.NET uygulamasından bir veritabanına bağlanmak için Microsoft s önerilerine göz atın. Bağlantı dizelerinizi şifrelemeye ek olarak, veritabanına güvenli bir biçimde bağlanmanızı sağlayarak sisteminizin sağlamlaştırılmasına yardımcı olabilirsiniz.

## <a name="step-1-exploring-aspnet-20-s-protected-configuration-options"></a>1\. Adım: ASP.NET 2,0 s korumalı yapılandırma seçeneklerini keşfetme

ASP.NET 2,0, yapılandırma bilgilerini şifrelemek ve şifrelerini çözmek için korunan bir yapılandırma sistemi içerir. Bu, yapılandırma bilgilerini programlı bir şekilde şifrelemek veya şifrelerini çözmek için kullanılabilen .NET Framework yöntemleri içerir. Korunan yapılandırma sistemi, geliştiricilerin hangi şifreleme uygulamalarının kullanıldığını seçmesini sağlayan [sağlayıcı modelini](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)kullanır.

.NET Framework, iki korumalı yapılandırma sağlayıcısıyla birlikte gelir:

- [`RSAProtectedConfigurationProvider`](https://msdn.microsoft.com/library/system.configuration.rsaprotectedconfigurationprovider.aspx) -şifreleme ve şifre çözme Için asimetrik [RSA algoritmasını](http://en.wikipedia.org/wiki/Rsa) kullanır.
- [`DPAPIProtectedConfigurationProvider`](https://msdn.microsoft.com/system.configuration.dpapiprotectedconfigurationprovider.aspx) -şifreleme ve şifre çözme Için Windows [Data Protection API 'yi (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx) kullanır.

Korunan yapılandırma sistemi sağlayıcı tasarım modelini gerçekleştirdiğinden, kendi korumalı yapılandırma sağlayıcınızı oluşturup uygulamanıza takabilirsiniz. Bu işlem hakkında daha fazla bilgi için bkz. [korumalı yapılandırma sağlayıcısı uygulama](https://msdn.microsoft.com/library/wfc2t3az(VS.80).aspx) .

RSA ve DPAPI sağlayıcıları şifreleme ve şifre çözme yordamları için anahtarlar kullanır ve bu anahtarlar makine veya Kullanıcı düzeyinde depolanabilir. Makine düzeyi anahtarlar, Web uygulamasının kendi adanmış sunucusunda çalıştığı senaryolar için veya şifreli bilgileri paylaşması gereken bir sunucuda birden çok uygulama varsa idealdir. Kullanıcı düzeyi anahtarlar, paylaşılan barındırma ortamlarında, aynı sunucudaki diğer uygulamaların uygulama korumalı yapılandırma bölümlerinin şifresini çözemediğinden daha güvenli bir seçenektir.

Bu öğreticide, örneklerimizde DPAPI sağlayıcısı ve makine düzeyindeki anahtarlar kullanılacaktır. Özellikle, korunan yapılandırma sistemi herhangi bir `Web.config` bölümünü şifrelemek için kullanılabilir olsa da, `Web.config``<connectionStrings>` bölümünü şifrelemeyi inceleyeceğiz. Kullanıcı düzeyi anahtarları kullanma veya RSA sağlayıcısını kullanma hakkında bilgi için, Bu öğreticinin sonundaki diğer okumalar bölümünde yer alan kaynaklara bakın.

> [!NOTE]
> `RSAProtectedConfigurationProvider` ve `DPAPIProtectedConfigurationProvider` sağlayıcılar `machine.config` dosyasında, sırasıyla sağlayıcı adları `RsaProtectedConfigurationProvider` ve `DataProtectionConfigurationProvider`ile kaydedilir. Yapılandırma bilgilerini şifrelerken veya şifresini çözerken gerçek tür adı (`RSAProtectedConfigurationProvider` ve `DPAPIProtectedConfigurationProvider`) yerine uygun sağlayıcı adını (`RsaProtectedConfigurationProvider` veya `DataProtectionConfigurationProvider`) sağlamaları gerekir. `machine.config` dosyasını `$WINDOWS$\Microsoft.NET\Framework\version\CONFIG` klasöründe bulabilirsiniz.

## <a name="step-2-programmatically-encrypting-and-decrypting-configuration-sections"></a>2\. Adım: program aracılığıyla yapılandırma bölümlerinin şifresini çözme ve şifrelerini çözme

Belirli bir sağlayıcıyı kullanarak belirli bir yapılandırma bölümünü şifreleyebilir veya şifrelerini çözebiliriz. Kod, kısa süre içinde, uygun yapılandırma bölümüne programlı bir şekilde başvurulması, `ProtectSection` veya `UnprotectSection` metodunu çağırmanız ve sonra değişiklikleri kalıcı hale getirmek için `Save` metodunu çağırmaktır. Ayrıca .NET Framework, yapılandırma bilgilerini şifreleyebilmeyen ve şifresini çözebilecekler yararlı bir komut satırı yardımcı programı içerir. Bu komut satırı yardımcı programını adım 3 ' te keşfedecektir.

Yapılandırma bilgilerini programlı bir şekilde korumayı göstermek için, s `Web.config``<connectionStrings>` bölümünü şifrelemek ve şifrelerini çözmek için düğmeler içeren bir ASP.NET sayfası oluşturalım.

`AdvancedDAL` klasöründeki `EncryptingConfigSections.aspx` sayfasını açarak başlayın. Araç kutusundan Tasarımcı üzerine bir TextBox denetimi sürükleyip `ID` özelliğini `WebConfigContents`, `TextMode` özelliğini `MultiLine`ve `Width` ve `Rows` özelliklerini sırasıyla %95 ve 15 olarak ayarlayarak. Bu TextBox denetimi, içeriğin şifrelenip şifrelenmediğini hızlı bir şekilde görmemize izin veren `Web.config` içeriğini görüntüler. Kuşkusuz, gerçek bir uygulamada `Web.config`içeriğini göstermek istemezsiniz.

Metin kutusunun altına `EncryptConnStrings` ve `DecryptConnStrings`adlı iki düğme denetimi ekleyin. Bağlantı dizelerini şifrelemek ve bağlantı dizelerinin şifresini çözmek için metin özelliklerini ayarlayın.

Bu noktada, ekranınızda Şekil 2 ' ye benzer görünmelidir.

[Sayfaya bir TextBox ve Iki düğme web denetimi eklemek ![](protecting-connection-strings-and-other-configuration-information-vb/_static/image5.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image4.png)

**Şekil 2**: sayfaya metin kutusu ve Iki düğme web denetimi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](protecting-connection-strings-and-other-configuration-information-vb/_static/image6.png))

Daha sonra, sayfa ilk yüklendiğinde `WebConfigContents` metin kutusuna `Web.config` içeriğini yükleyen ve görüntüleyen bir kod yazdık. Aşağıdaki kodu Page s arka plan kod sınıfına ekleyin. Bu kod, `DisplayWebConfig` adlı bir yöntemi ekler ve `Page.IsPostBack` `False`olduğunda `Page_Load` olay işleyicisinden çağırır:

[!code-vb[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample1.vb)]

`DisplayWebConfig` yöntemi, uygulama s `Web.config` dosyasını açmak için [`File` sınıfını](https://msdn.microsoft.com/library/system.io.file.aspx) , içeriğini bir dizeye okumak için [`StreamReader` sınıfını](https://msdn.microsoft.com/library/system.io.streamreader.aspx) ve`Path` dosyası fiziksel yolunu oluşturmak için [`Web.config` sınıfını](https://msdn.microsoft.com/library/system.io.path.aspx) kullanır. Bu üç sınıfın hepsi [`System.IO` ad alanında](https://msdn.microsoft.com/library/system.io.aspx)bulunur. Sonuç olarak, arka plan kod sınıfının üst kısmına bir `Imports``System.IO` deyim eklemeniz ya da alternatif olarak, bu sınıf adlarını `System.IO.` önekiyle birlikte uygulamanız gerekecektir

Daha sonra, iki düğme denetimine `Click` olay işleyicileri eklememiz ve DPAPI sağlayıcısı ile makine düzeyindeki bir anahtar kullanarak `<connectionStrings>` bölümünü şifrelemek ve şifresini çözmek için gerekli kodu eklemeniz gerekir. Tasarımcıdan, arka plan kod sınıfında `Click` olay işleyicisi eklemek için düğmelerin her birine çift tıklayın ve ardından aşağıdaki kodu ekleyin:

[!code-vb[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample2.vb)]

İki olay işleyicilerinde kullanılan kod neredeyse aynıdır. Her ikisi de, [`WebConfigurationManager` sınıf](https://msdn.microsoft.com/library/system.web.configuration.webconfigurationmanager.aspx) s [`OpenWebConfiguration` yöntemi](https://msdn.microsoft.com/library/system.web.configuration.webconfigurationmanager.openwebconfiguration.aspx)aracılığıyla geçerli uygulama s `Web.config` dosyası hakkında bilgi almaya başlar. Bu yöntem, belirtilen sanal yol için Web yapılandırma dosyasını döndürür. Sonra, `Web.config` File s `<connectionStrings>` bölümüne, [`ConfigurationSection`](https://msdn.microsoft.com/library/system.configuration.configurationsection.aspx) nesnesi döndüren [`Configuration` Class](https://msdn.microsoft.com/library/system.configuration.configuration.aspx) s [`GetSection(sectionName)` yöntemi](https://msdn.microsoft.com/library/system.configuration.configuration.getsection.aspx)aracılığıyla erişilir.

`ConfigurationSection` nesnesi, yapılandırma bölümüyle ilgili ek bilgi ve işlevsellik sağlayan bir [`SectionInformation` özelliği](https://msdn.microsoft.com/library/system.configuration.configurationsection.sectioninformation.aspx) içerir. Yukarıdaki kodda gösterildiği gibi, yapılandırma bölümünün `SectionInformation` özellik s `IsProtected` özelliğini denetleyerek şifrelenip şifrelenmeyeceğini belirleyebiliriz. Üstelik, Bölüm `SectionInformation` özellik s `ProtectSection(provider)` ve `UnprotectSection` yöntemleri aracılığıyla şifrelenebilir veya şifresi çözülür.

`ProtectSection(provider)` yöntemi, şifreleme sırasında kullanılacak korumalı yapılandırma sağlayıcısının adını belirten bir dize girişi kabul eder. `EncryptConnString` Button s olay işleyicisinde, DPAPI sağlayıcısının kullanılması için DataProtectionConfigurationProvider 'ı `ProtectSection(provider)` yöntemine geçirdik. `UnprotectSection` yöntemi, yapılandırma bölümünü şifrelemek için kullanılan sağlayıcıyı belirleyebilir ve bu nedenle herhangi bir giriş parametresi gerektirmez.

`ProtectSection(provider)` veya `UnprotectSection` yöntemini çağırdıktan sonra, değişiklikleri kalıcı hale getirmek için `Configuration` nesne s [`Save` yöntemini](https://msdn.microsoft.com/library/system.configuration.configuration.save.aspx) çağırmanız gerekir. Yapılandırma bilgileri şifrelendikten veya şifresi çözüldükten ve değişiklikler kaydedildikten sonra, güncelleştirilmiş `Web.config` içeriğini TextBox denetimine yüklemek için `DisplayWebConfig` çağırdık.

Yukarıdaki kodu girdikten sonra, `EncryptingConfigSections.aspx` sayfasını bir tarayıcıda ziyaret ederek test edin. Başlangıçta düz metin olarak görüntülenen `<connectionStrings>` bölümü ile `Web.config` içeriğini listeleyen bir sayfa görmeniz gerekir (bkz. Şekil 3).

[Sayfaya bir TextBox ve Iki düğme web denetimi eklemek ![](protecting-connection-strings-and-other-configuration-information-vb/_static/image8.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image7.png)

**Şekil 3**: sayfaya metin kutusu ve Iki düğme web denetimi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](protecting-connection-strings-and-other-configuration-information-vb/_static/image9.png))

Şimdi bağlantı dizelerini şifreleyin düğmesine tıklayın. İstek doğrulaması etkinleştirilirse `WebConfigContents` metin kutusundan geri gönderilen biçimlendirme, istemcide tehlikeli olabilecek bir `Request.Form` değeri algılanan bir `HttpRequestValidationException`oluşturur. ASP.NET 2,0 ' de varsayılan olarak etkinleştirilen istek doğrulaması, kodlanmamış HTML içeren geri göndermeler yasaklar ve betik ekleme saldırılarını önlemeye yardımcı olmak için tasarlanmıştır. Bu denetim, sayfa veya uygulama düzeyinde devre dışı bırakılabilir. Bu sayfada devre dışı bırakmak için `ValidateRequest` ayarını `@Page` yönergesinde `False` olarak ayarlayın. `@Page` yönergesi sayfa bildirim temelli biçimlendirmenin en üstünde bulunur.

[!code-aspx[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample3.aspx)]

İstek doğrulama hakkında daha fazla bilgi, amacı, sayfa ve uygulama düzeyinde devre dışı bırakma ve HTML kodlama biçimlendirme hakkında daha fazla bilgi için bkz. [Istek doğrulama-betik saldırılarını önler](../../../../whitepapers/request-validation.md).

Sayfa için istek doğrulamayı devre dışı bıraktıktan sonra, bağlantı dizelerini şifreleyin düğmesine tekrar tıklayın. Geri göndermede, yapılandırma dosyasına erişilir ve `<connectionStrings>` bölümü DPAPI sağlayıcısı kullanılarak şifrelenir. Metin kutusu daha sonra yeni `Web.config` içeriğini görüntüleyecek şekilde güncelleştirilir. Şekil 4 ' ün gösterdiği gibi `<connectionStrings>` bilgiler artık şifrelenir.

[Bağlantı dizelerini şifreleyin düğmesine tıklamak ![&lt;connectionString&gt; bölümünü şifreler](protecting-connection-strings-and-other-configuration-information-vb/_static/image11.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image10.png)

**Şekil 4**: bağlantı dizelerini şifreleyin düğmesine tıklamak `<connectionString>` bölümünü şifreler ([tam boyutlu görüntüyü görüntülemek için tıklayın](protecting-connection-strings-and-other-configuration-information-vb/_static/image12.png))

Bilgisayarımda oluşturulan şifreli `<connectionStrings>` bölümü, `<CipherData>` öğesinin bazı içerikleri breçekimi için kaldırılmış olsa da aşağıdaki gibidir:

[!code-xml[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample4.xml)]

> [!NOTE]
> `<connectionStrings>` öğesi, şifrelemeyi gerçekleştirmek için kullanılan sağlayıcıyı belirtir (`DataProtectionConfigurationProvider`). Bu bilgiler, bağlantı dizelerini çöz düğmesine tıklandığında `UnprotectSection` yöntemi tarafından kullanılır.

Yazdığımız kodla, bir SqlDataSource denetiminden veya otomatik olarak oluşturulan koddan `Web.config` bağlantı dizesi bilgisine erişildiğinde, otomatik olarak şifresi çözülür. Kısaca şifreli `<connectionString>` bölümünün şifresini çözmek için ek kod veya mantık eklememiz gerekmez. Bunu göstermek için, bu anda, temel raporlama bölümündeki (`~/BasicReporting/SimpleDisplay.aspx`) basit görüntüleme öğreticisi gibi önceki öğreticilerden birini ziyaret edin. Şekil 5 ' i gösterdiği gibi, öğretici tam olarak beklendiği gibi çalışarak, şifrelenmiş bağlantı dizesi bilgilerinin ASP.NET sayfası tarafından otomatik olarak şifresinin çözülmediğini belirtir.

[![veri erişim katmanı, bağlantı dizesi bilgilerinin şifresini otomatik olarak çözer](protecting-connection-strings-and-other-configuration-information-vb/_static/image14.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image13.png)

**Şekil 5**: veri erişim katmanı, bağlantı dizesi bilgilerinin otomatik olarak şifresini çözer ([tam boyutlu görüntüyü görüntülemek için tıklayın](protecting-connection-strings-and-other-configuration-information-vb/_static/image15.png))

`<connectionStrings>` bölümünü düz metin gösterimine geri dönmek için bağlantı dizelerini çöz düğmesine tıklayın. Geri göndermede, bağlantı dizelerini düz metin olarak `Web.config` görmeniz gerekir. Bu noktada, ekranınızda Bu sayfa ilk kez ziyaret edildiğinde olduğu gibi görünmelidir (Şekil 3 ' te bakın).

## <a name="step-3-encrypting-configuration-sections-usingaspnet_regiisexe"></a>3\. Adım:`aspnet_regiis.exe` kullanarak yapılandırma bölümlerini şifreleme

.NET Framework, `$WINDOWS$\Microsoft.NET\Framework\version\` klasöründeki çeşitli komut satırı araçlarını içerir. [SQL önbellek bağımlılıklarını kullanma](../caching-data/using-sql-cache-dependencies-vb.md) öğreticisinde, ÖRNEĞIN, SQL önbellek bağımlılıkları için gereken altyapıyı eklemek için `aspnet_regsql.exe` komut satırı aracını kullanma hakkında baktık. Bu klasördeki başka bir yararlı komut satırı aracı, [ASP.NET IIS kayıt aracıdır (`aspnet_regiis.exe`)](https://msdn.microsoft.com/library/k6h9cz8h(VS.80).aspx). Adından da anlaşılacağı gibi, ASP.NET IIS kayıt aracı öncelikle Microsoft s Professional-sınıf Web sunucusu, IIS ile bir ASP.NET 2,0 uygulaması kaydetmek için kullanılır. IIS ile ilgili özelliklerin yanı sıra, ASP.NET IIS kayıt aracı da `Web.config`belirtilen yapılandırma bölümlerini şifrelemek veya şifresini çözmek için de kullanılabilir.

Aşağıdaki bildirimde, `aspnet_regiis.exe` komut satırı aracı ile bir yapılandırma bölümünü şifrelemek için kullanılan genel sözdizimi gösterilmektedir:

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample5.cmd)]

*bölüm* , şifrelemek için yapılandırma bölümüdür (connectionStrings gibi), *fiziksel\_Dizin* , Web uygulaması kök dizininin tam, fiziksel yoludur ve *sağlayıcı* , kullanılacak korumalı yapılandırma sağlayıcısının adıdır (örneğin, DataProtectionConfigurationProvider). Alternatif olarak, Web uygulaması IIS 'de kayıtlıysa, aşağıdaki sözdizimini kullanarak fiziksel yol yerine sanal yolu girebilirsiniz:

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample6.cmd)]

Aşağıdaki `aspnet_regiis.exe` örnek, bir makine düzeyindeki anahtarla DPAPI sağlayıcısını kullanarak `<connectionStrings>` bölümünü şifreler:

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample7.cmd)]

Benzer şekilde, `aspnet_regiis.exe` komut satırı aracı yapılandırma bölümlerinin şifresini çözmek için de kullanılabilir. `-pef` anahtarını kullanmak yerine `-pdf` kullanın (veya `-pe`yerine `-pd`kullanın). Ayrıca, şifre çözme sırasında sağlayıcı adının gerekli olmadığına de unutmayın.

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample8.cmd)]

> [!NOTE]
> Bilgisayara özel anahtarlar kullanan DPAPI sağlayıcısını kullandığımızdan, Web sayfalarının sunulduğu makineden `aspnet_regiis.exe` çalıştırmanız gerekir. Örneğin, bu komut satırı programını yerel geliştirme makinenizden çalıştırırsanız ve sonra şifrelenmiş Web. config dosyasını üretim sunucusuna yüklerseniz, üretim sunucusu şifrelendikten sonra bağlantı dizesi bilgilerinin şifresini çözemeyecektir geliştirme makinenize özel anahtarlar kullanma. RSA anahtarı başka bir makineye dışarı aktarmak mümkün olduğu için RSA sağlayıcısı bu sınırlamaya sahip değildir.

## <a name="understanding-database-authentication-options"></a>Veritabanı kimlik doğrulama seçeneklerini anlama

Herhangi bir uygulama, bir Microsoft SQL Server veritabanına `SELECT`, `INSERT`, `UPDATE`veya `DELETE` sorguları yayınlamamasından önce, önce veritabanının istek sahibine tanımlaması gerekir. Bu işlem *kimlik doğrulama* olarak bilinir ve SQL Server iki kimlik doğrulama yöntemi sağlar:

- **Windows kimlik doğrulaması** -uygulamanın üzerinde çalıştığı işlem veritabanıyla iletişim kurmak için kullanılır. Visual Studio 2005 s ASP.NET Development Server aracılığıyla bir ASP.NET uygulaması çalıştırırken, ASP.NET uygulaması şu anda oturum açmış kullanıcının kimliğini varsayar. Microsoft Internet Information Server (IIS) üzerinde ASP.NET uygulamaları için ASP.NET uygulamaları genellikle `domainName``\MachineName` veya `domainName``\NETWORK SERVICE`kimliğini varsayar, ancak bu özelleştirilebilir.
- **SQL kimlik doğrulaması** -kimlik doğrulaması için kimlik bilgileri olarak BIR kullanıcı kimliği ve parola değerleri sağlanır. SQL kimlik doğrulaması ile, Kullanıcı KIMLIĞI ve parola bağlantı dizesinde sağlanır.

Daha güvenli olduğundan, Windows kimlik doğrulaması SQL kimlik doğrulaması üzerinden tercih edilir. Windows kimlik doğrulaması ile bağlantı dizesi bir Kullanıcı adı ve paroladan ücretsizdir ve Web sunucusu ve veritabanı sunucusu iki farklı makinede bulunuyorsa, kimlik bilgileri düz metin olarak ağ üzerinden gönderilmez. Ancak, SQL kimlik doğrulaması ile bağlantı dizesinde kimlik doğrulama kimlik bilgileri sabit olarak kodlanmıştır ve Web sunucusundan düz metin olarak veritabanı sunucusuna iletilir.

Bu öğreticiler Windows kimlik doğrulamasını kullandı. Bağlantı dizesini inceleyerek hangi kimlik doğrulama modunun kullanıldığını söyleyebilirsiniz. Öğreticilerimiz için `Web.config` bağlantı dizesi:

`Data Source=.\SQLEXPRESS; AttachDbFilename=|DataDirectory|\NORTHWND.MDF; Integrated Security=True; User Instance=True`

Tümleşik güvenlik = doğru ve Kullanıcı adının ve parolanın olmaması Windows kimlik doğrulamasının kullanıldığını belirtir. Bazı bağlantı dizelerine, güvenilen bağlantı = Evet veya tümleşik güvenlik = SSPI terimi tümleşik güvenlik = true yerine kullanılır, ancak üçü de Windows kimlik doğrulamasının kullanımını gösterir.

Aşağıdaki örnek, SQL kimlik doğrulaması kullanan bir bağlantı dizesini gösterir. Bağlantı dizesi içine gömülü kimlik bilgilerini aklınızda edin:

`Server=serverName; Database=Northwind; uid=userID; pwd=password`

Bir saldırganın uygulama `Web.config` dosyanızı görüntüleyebileceklerini düşünün. Internet üzerinden erişilebilen bir veritabanına bağlanmak için SQL kimlik doğrulaması kullanıyorsanız, saldırgan bu bağlantı dizesini kullanarak SQL Management Studio aracılığıyla veritabanınıza veya kendi web sitelerindeki ASP.NET sayfalarından bağlantı oluşturabilir. Bu tehdidi azaltmaya yardımcı olmak için korunan yapılandırma sistemini kullanarak `Web.config` bağlantı dizesi bilgilerini şifreleyin.

> [!NOTE]
> SQL Server kullanılabilir farklı kimlik doğrulama türleri hakkında daha fazla bilgi için bkz. [secure ASP.NET uygulamaları oluşturma: kimlik doğrulama, yetkilendirme ve güvenli iletişim](https://msdn.microsoft.com/library/aa302392.aspx). Windows ve SQL kimlik doğrulama sözdizimi arasındaki farkları gösteren daha fazla bağlantı dizesi örnekleri için [connectionStrings.com](http://www.connectionstrings.com/)adresine bakın.

## <a name="summary"></a>Özet

Varsayılan olarak, bir ASP.NET uygulamasındaki `.config` uzantısına sahip dosyalara bir tarayıcıdan erişilemez. Bu dosya türleri, veritabanı bağlantı dizeleri, Kullanıcı adları ve parolalar gibi hassas bilgileri içerebileceğinden döndürülmez. .NET 2,0 ' deki korumalı yapılandırma sistemi, belirtilen yapılandırma bölümlerinin şifrelenmesini sağlayarak hassas bilgilerin korunmasını sağlar. İki yerleşik korumalı yapılandırma sağlayıcısı vardır: RSA algoritmasını kullanan bir ve Windows Data Protection API (DPAPI) kullanan bir tane.

Bu öğreticide, DPAPI sağlayıcısını kullanarak yapılandırma ayarlarının nasıl şifreleneceğini ve şifresinin çözülmesini inceledik. Bu, adım 2 ' de gördüğünüz ve adım 3 ' te ele alınan `aspnet_regiis.exe` komut satırı aracının yanı sıra programlama yoluyla da gerçekleştirilebilir. Kullanıcı düzeyi anahtarları kullanma veya bunun yerine RSA sağlayıcısını kullanma hakkında daha fazla bilgi için daha fazla okuma bölümündeki kaynaklara bakın.

Programlamanın kutlu olsun!

## <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Güvenli ASP.NET uygulaması oluşturma: kimlik doğrulama, yetkilendirme ve güvenli Iletişim](https://msdn.microsoft.com/library/aa302392.aspx)
- [ASP.NET 2,0 uygulamalarında yapılandırma bilgilerini şifreleme](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx)
- [ASP.NET 2,0 'de şifreleme `Web.config` değerleri](https://weblogs.asp.net/scottgu/archive/2006/01/09/434893.aspx)
- [Nasıl yapılır: DPAPI kullanarak ASP.NET 2,0 'de yapılandırma bölümlerini şifreleme](https://msdn.microsoft.com/library/ms998280.aspx)
- [Nasıl yapılır: ASP.NET 2,0 ' de yapılandırma bölümlerini RSA kullanarak şifreleme](https://msdn.microsoft.com/library/ms998283.aspx)
- [.NET 2,0 ' de Yapılandırma API 'SI](http://www.odetocode.com/Articles/418.aspx)
- [Windows veri koruması](https://msdn.microsoft.com/library/ms995355.aspx)

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler, bir Murphy ve Randy SCHMIDT olarak değiştirildi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb.md)
> [İleri](debugging-stored-procedures-vb.md)
