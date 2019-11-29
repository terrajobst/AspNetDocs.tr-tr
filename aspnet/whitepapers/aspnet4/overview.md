---
uid: whitepapers/aspnet4/overview
title: ASP.NET 4 ve Visual Studio 2010 Web geliştirmesine genel bakış | Microsoft Docs
author: rick-anderson
description: Bu belgede, the.NET Framework 4 ve Visual Studio 2010 ' de yer alan ASP.NET için yeni özelliklerin çoğuna genel bakış sunulmaktadır.
ms.author: riande
ms.date: 02/10/2010
ms.assetid: d7729af4-1eda-4ff2-8b61-dbbe4fc11d10
msc.legacyurl: /whitepapers/aspnet4
msc.type: content
ms.openlocfilehash: ecde48f6bd88ee5f569bfeb8b70c26a50bc869c2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74576865"
---
# <a name="aspnet-4-and-visual-studio-2010-web-development-overview"></a>ASP.NET 4 ve Visual Studio 2010 Web Geliştirmeye Genel Bakış

> Bu belgede, the.NET Framework 4 ve Visual Studio 2010 ' de yer alan ASP.NET için yeni özelliklerin çoğuna genel bakış sunulmaktadır.
> 
> [Bu teknik incelemeyi indirin](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_and_Visual_Studio_2010_Web_Development_Overview.pdf)

**İçindekiler**

**[Çekirdek hizmetler](#0.2__Toc253429238 "_Toc253429238")**  
[Web. config dosyasını yeniden düzenleme](#0.2__Toc253429239 "_Toc253429239")  
[Genişletilebilir çıktı önbelleği](#0.2__Toc253429240 "_Toc253429240")  
[Web uygulamalarını otomatik olarak Başlat](#0.2__Toc253429241 "_Toc253429241")  
[Sayfayı kalıcı olarak yeniden yönlendirme](#0.2__Toc253429242 "_Toc253429242")  
[Oturum durumunu küçültme](#0.2__Toc253429243 "_Toc253429243")  
[Izin verilen URL 'Lerin aralığı genişletiliyor](#0.2__Toc253429244 "_Toc253429244")  
[Genişletilebilir Istek doğrulaması](#0.2__Toc253429245 "_Toc253429245")  
[Nesne önbelleğe alma ve nesne önbelleğe alma genişletilebilirliği](#0.2__Toc253429246 "_Toc253429246")  
[Genişletilebilir HTML, URL ve HTTP üst bilgi kodlaması](#0.2__Toc253429247 "_Toc253429247")  
[Tek bir çalışan Işlemindeki ayrı uygulamalar için performans Izleme](#0.2__Toc253429248 "_Toc253429248")  
[Çoklu hedefleme](#0.2__Toc253429249 "_Toc253429249")

**[Ajax](#0.2__Toc253429250 "_Toc253429250")**  
[Web Forms ve MVC ile birlikte bulunan jQuery](#0.2__Toc253429251 "_Toc253429251")  
[Content Delivery Network desteği](#0.2__Toc253429252 "_Toc253429252")  
[ScriptManager açık betikler](#0.2__Toc253429253 "_Toc253429253")

**[Web Forms](#0.2__Toc253429256 "_Toc253429256")**  
[Meta etiketler Page. MetaKeywords ve Page. MetaDescription özellikleriyle ayarlanıyor](#0.2__Toc253429257 "_Toc253429257")  
[Bireysel denetimler için görünüm durumunu etkinleştirme](#0.2__Toc253429258 "_Toc253429258")  
[Tarayıcı özelliklerine yapılan değişiklikler](#0.2__Toc253429259 "_Toc253429259")  
[ASP.NET 4 ' te yönlendirme](#0.2__Toc253429260 "_Toc253429260")  
[Istemci kimliklerini ayarlama](#0.2__Toc253429261 "_Toc253429261")  
[Veri denetimlerinde kalıcı satır seçimi](#0.2__Toc253429262 "_Toc253429262")  
[ASP.NET grafik denetimi](#0.2__Toc253429263 "_Toc253429263")  
[Querygenişletici denetimiyle verileri filtreleme](#0.2__Toc253429264 "_Toc253429264")  
[HTML kodlu kod Ifadeleri](#0.2__Toc253429265 "_Toc253429265")  
[Proje şablonu değişiklikleri](#0.2__Toc253429266 "_Toc253429266")  
[CSS geliştirmeleri](#0.2__Toc253429267 "_Toc253429267")  
[Gizli alanlar etrafında div öğelerini gizleme](#0.2__Toc253429268 "_Toc253429268")  
[Şablonlu denetimler için bir dış tablo işleme](#0.2__Toc253429269 "_Toc253429269")  
[ListView denetimi geliştirmeleri](#0.2__Toc253429270 "_Toc253429270")  
[CheckBoxList ve RadioButtonList denetimi geliştirmeleri](#0.2__Toc253429271 "_Toc253429271")  
[Menü denetimi geliştirmeleri](#0.2__Toc253429272 "_Toc253429272")  
[Sihirbaz ve CreateUserWizard denetimleri 56](#0.2__Toc253429273 "_Toc253429273")

**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**  
[Alan desteği](#0.2__Toc253429275 "_Toc253429275")  
[Veri ek açıklama öznitelik doğrulama desteği](#0.2__Toc253429276 "_Toc253429276")  
[Şablonlu yardımcılar](#0.2__Toc253429277 "_Toc253429277")

**[Dinamik veriler](#0.2__Toc253429278 "_Toc253429278")**  
[Mevcut projeler için dinamik verileri etkinleştirme](#0.2__Toc253429279 "_Toc253429279")  
[Bildirime dayalı DynamicDataManager denetimi sözdizimi](#0.2__Toc253429280 "_Toc253429280")  
[Varlık şablonları](#0.2__Toc253429281 "_Toc253429281")  
[URL 'Ler ve e-posta adresleri için yeni alan şablonları](#0.2__Toc253429282 "_Toc253429282")  
[DynamicHyperLink denetimiyle bağlantılar oluşturma](#0.2__Toc253429283 "_Toc253429283")  
[Veri modelinde devralma desteği](#0.2__Toc253429284 "_Toc253429284")  
[Çoktan çoğa Ilişkiler için destek (yalnızca Entity Framework)](#0.2__Toc253429285 "_Toc253429285")  
[Görüntüleme ve destek numaralandırmaları denetlemek için yeni öznitelikler](#0.2__Toc253429286 "_Toc253429286")  
[Filtreler için gelişmiş destek](#0.2__Toc253429287 "_Toc253429287")

**[Visual Studio 2010 Web geliştirme Iyileştirmeleri](#0.2__Toc253429288 "_Toc253429288")**  
[Gelişmiş CSS uyumluluğu](#0.2__Toc253429289 "_Toc253429289")  
[HTML ve JavaScript kod parçacıkları](#0.2__Toc253429290 "_Toc253429290")  
[JavaScript IntelliSense geliştirmeleri](#0.2__Toc253429291 "_Toc253429291")

**[Visual Studio 2010 ile Web uygulaması dağıtımı](#0.2__Toc253429292 "_Toc253429292")**  
[Web paketleme](#0.2__Toc253429293 "_Toc253429293")  
[Web. config dönüşümü](#0.2__Toc253429294 "_Toc253429294")  
[Veritabanı dağıtımı](#0.2__Toc253429295 "_Toc253429295")  
[Web uygulamaları için tek tıklamayla yayımlama](#0.2__Toc253429296 "_Toc253429296")  
[Kaynaklar](#0.2__Toc253429297 "_Toc253429297")

**[Sorumluluk reddi](#0.2__Toc253429298 "_Toc253429298")**

<a id="0.2__Toc224729018"></a><a id="0.2__Toc253429238"></a><a id="0.2__Toc243304612"></a>

## <a name="core-services"></a>Çekirdek hizmetler

ASP.NET 4, çıktı önbelleği ve oturum durumu depolaması gibi çekirdek ASP.NET hizmetlerini geliştiren bir dizi özellik sunar.

<a id="0.2__Toc243304613"></a><a id="0.2__Toc253429239"></a><a id="0.2__Toc224729019"></a>

### <a name="webconfig-file-refactoring"></a>Web. config dosyasını yeniden düzenleme

Bir Web uygulaması için yapılandırmayı içeren `Web.config` dosyası, Ajax, Yönlendirme ve IIS 7 ile tümleştirme gibi yeni özellikler eklendiğinden, .NET Framework son birkaç sürümüne çok fazla büyümüştür. Bunun yapılması, Visual Studio gibi bir araç olmadan yeni Web uygulamaları yapılandırmayı veya başlatmayı zorlaştırır. . NET Framework 4 ' te, ana yapılandırma öğeleri `machine.config` dosyasına taşınmıştır ve uygulamalar artık bu ayarları devralmasını sağlar. Bu, ASP.NET 4 uygulamalarındaki `Web.config` dosyasının boş olmasına ya da yalnızca Visual Studio 'nun uygulamanın hedeflediği Framework sürümünü belirten aşağıdaki satırları içermesine izin verir:

[!code-xml[Main](overview/samples/sample1.xml)]

<a id="0.2__Toc253429240"></a><a id="0.2__Toc243304614"></a>

### <a name="extensible-output-caching"></a>Genişletilebilir çıktı önbelleği

ASP.NET 1,0 ' nin yayımlandığı zaman, çıkış önbelleği geliştiricilerin oluşturulan sayfaların, denetimlerin ve HTTP yanıtlarının üretilen çıkışını bellekte depolamasını etkinleştirdi. Sonraki Web isteklerinde, ASP.NET çıkışı sıfırdan yeniden oluşturma yerine bellekten oluşturulan çıktıyı alarak daha hızlı bir şekilde içerik sunabilir. Ancak, bu yaklaşımın bir sınırlaması vardır: oluşturulan içerik her zaman bellekte depolanması gerekir ve ağır trafik yaşayan sunucularda, çıktı önbelleği tarafından tüketilen bellek, bir Web uygulamasının diğer bölümlerinden bellek taleplerine rekabet edebilir.

ASP.NET 4, bir veya daha fazla özel çıkış önbellek sağlayıcısını yapılandırmanızı sağlayan çıkış önbelleğe almaya bir genişletilebilirlik noktası ekler. Çıktı önbelleği sağlayıcıları, HTML içeriğini kalıcı hale getirmek için herhangi bir depolama mekanizmasını kullanabilir. Bu, yerel veya uzak diskler, bulut depolama ve dağıtılmış önbellek altyapılarını içerebilen farklı Kalıcılık mekanizmaları için özel çıkış önbelleği sağlayıcıları oluşturmayı mümkün kılar.

Yeni *System. Web. Caching. OutputCacheProvider* türünden türeten bir sınıf olarak özel çıkış önbelleği sağlayıcısı oluşturursunuz. Daha sonra, aşağıdaki örnekte gösterildiği gibi *OutputCache* öğesinin yeni *sağlayıcılar* alt bölümünü kullanarak `Web.config` dosyasında sağlayıcıyı yapılandırabilirsiniz:

[!code-xml[Main](overview/samples/sample2.xml)]

Varsayılan olarak, ASP.NET 4 ' te, tüm HTTP yanıtları, işlenmiş sayfalar ve denetimler, önceki örnekte gösterildiği gibi, *defaultProvider* özniteliği aspnetınterprovider olarak ayarlandığı gibi bellek içi çıkış önbelleğini kullanır. *DefaultProvider*için farklı bir sağlayıcı adı belirterek, bir Web uygulaması için kullanılan varsayılan çıkış önbelleği sağlayıcısını değiştirebilirsiniz.

Ayrıca, denetim başına ve istek başına farklı çıkış önbelleği sağlayıcıları seçebilirsiniz. Farklı Web Kullanıcı denetimleri için farklı çıkış önbelleği sağlayıcısı seçmek için en kolay yol, aşağıdaki örnekte gösterildiği gibi, bir denetim yönergesinde yeni *ProviderName* özniteliğini kullanarak bunu bildirimli olarak kullanmaktır:

[!code-aspx[Main](overview/samples/sample3.aspx)]

Bir HTTP isteği için farklı bir çıkış önbelleği sağlayıcısı belirtilmesi biraz daha fazla iş gerektirir. Sağlayıcıyı bildirimli olarak belirtmek yerine, belirli bir istek için hangi sağlayıcıyı kullanacağınızı programlı bir şekilde belirtmek üzere `Global.asax` dosyasındaki yeni *Getouputcacheprovidername* yöntemini geçersiz kılarsınız. Aşağıdaki örnek bunun nasıl yapılacağını göstermektedir.

[!code-csharp[Main](overview/samples/sample4.cs)]

Çıkış önbelleği sağlayıcısı genişletilebilirliği ASP.NET 4 ' e ek olarak, Web siteleriniz için daha fazla ısrarlı ve daha akıllı çıkış önbelleği stratejileri de bulabilirsiniz. Örneğin, artık bellekte bir sitenin "En Iyi 10" sayfalarını önbelleğe almak mümkündür ve diskte daha düşük trafik alan sayfalar önbelleğe alınır. Alternatif olarak, işlenmiş bir sayfa için her değişiklik yapılan birleşimi önbelleğe alabilir, ancak bir dağıtılmış önbellek kullanarak bellek tüketiminin ön uç Web sunucularından boşaltılmasını sağlayabilirsiniz.

<a id="0.2__Toc224729020"></a><a id="0.2__Toc253429241"></a><a id="0.2__Toc243304615"></a>

### <a name="auto-start-web-applications"></a>Web uygulamalarını otomatik olarak Başlat

Bazı Web uygulamalarının, ilk isteği sunmadan önce büyük miktarlarda veri yüklemesi veya pahalı başlatma işlemesi gerçekleştirmesi gerekir. Önceki ASP.NET sürümlerinde, bu durumlar için özel yaklaşımlara "bir ASP.NET uygulamasını uyandırma" ve sonra da `Global.asax` dosyasında *uygulama\_yük* yöntemi sırasında başlatma kodunu çalıştırmak zorunda kaldık.

ASP.NET 4, Windows Server 2008 R2 üzerinde IIS 7,5 çalıştırıyorsa, bu senaryoya doğrudan adreslendirilen *otomatik başlatma* adlı yeni bir ölçeklenebilirlik özelliği kullanılabilir. Otomatik başlatma özelliği, bir uygulama havuzu başlatmak, bir ASP.NET uygulaması başlatmak ve ardından HTTP isteklerini kabul etmek için denetimli bir yaklaşım sağlar.

> [!NOTE] 
> 
> IIS 7,5 için IIS uygulaması ısınma modülü
> 
> IIS ekibi, IIS 7,5 için uygulama ısınma modülünün ilk beta test sürümünü serbest bıraktı. Bu, daha önce açıklankıyasla uygulamalarınızın daha da kolay olmasını sağlar. Özel kod yazmak yerine, Web uygulaması ağdan gelen istekleri kabul etmeden önce yürütülecek kaynakların URL 'Lerini belirtirsiniz. Bu ısınma, IIS hizmetinin başlatılması sırasında (IIS uygulama havuzunu *AlwaysRunning*olarak yapılandırdıysanız) ve bir IIS çalışan işlemi geri dönüştürüldüğünde oluşur. Geri dönüşüm sırasında eski IIS çalışan işlemi, yeni oluşturulan çalışan işlem tamamen çarpılana kadar istekleri yürütmeye devam eder, böylece uygulamalar, birincil olmayan önbellekler nedeniyle kesintiler veya başka sorunlar yaşar. Bu modülün sürüm 2,0 ' den başlayarak herhangi bir ASP.NET sürümüyle çalışıp çalışmadığını unutmayın.
> 
> Daha fazla bilgi için bkz. IIS.net Web sitesinde [uygulama ısınma](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net) . Isınma özelliğinin nasıl kullanılacağını gösteren bir anlatım için, IIS.net Web sitesinde [ııs 7,5 uygulama ısınma modülünü](https://www.iis.net/learn/manage) kullanmaya başlama bölümüne bakın.

Otomatik başlatma özelliğini kullanmak için, IIS Yöneticisi, `applicationHost.config` dosyasında aşağıdaki yapılandırma kullanılarak otomatik olarak başlatılacak şekilde IIS 7,5 ' de bir uygulama havuzu ayarlar:

[!code-xml[Main](overview/samples/sample5.xml)]

Tek bir uygulama havuzu birden çok uygulama içerebildiğinden, `applicationHost.config` dosyasında aşağıdaki yapılandırma kullanılarak otomatik olarak başlatılacak ayrı uygulamalar belirtirsiniz:

[!code-xml[Main](overview/samples/sample6.xml)]

IIS 7,5 sunucusu soğuk başlatıldığında veya ayrı bir uygulama havuzu geri dönüştürüldüğünde, IIS 7,5 hangi Web uygulamalarının otomatik olarak başlatılması gerektiğini belirleyen `applicationHost.config` dosyadaki bilgileri kullanır. Otomatik başlatma için işaretlenen her uygulama için, IIS 7.5, uygulamayı uygulamanın geçici olarak HTTP isteklerini kabul etmediğinden bir durumda başlatmak için ASP.NET 4 ' e bir istek gönderir. Bu durumda ASP.NET, *Serviceautomatic Startprovider* özniteliği tarafından tanımlanan türü (önceki örnekte gösterildiği gibi) oluşturur ve ortak giriş noktasına çağırır.

Aşağıdaki örnekte gösterildiği gibi, *IProcessHostPreloadClient* arabirimini uygulayarak gerekli giriş noktasıyla yönetilen bir otomatik başlatma türü oluşturursunuz:

[!code-csharp[Main](overview/samples/sample7.cs)]

Başlatma kodunuz, *preload* yönteminde çalıştıktan sonra ve yöntemi dönerse, ASP.NET uygulaması istekleri işlemeye hazırız.

IIS 5 ve ASP.NET 4 ' e otomatik başlatma eklemesi sayesinde, ilk HTTP isteğini işlemeden önce pahalı uygulama başlatma işlemi gerçekleştirmek için iyi tanımlanmış bir yaklaşım vardır. Örneğin, yeni otomatik başlatma özelliğini kullanarak bir uygulamayı başlatabilir ve sonra uygulamanın başlatıldığı ve HTTP trafiğini kabul etmeye hazır bir yük dengeleyiciye işaret edebilirsiniz.

<a id="0.2__Toc224729021"></a><a id="0.2__Toc253429242"></a><a id="0.2__Toc243304616"></a>

### <a name="permanently-redirecting-a-page"></a>Sayfayı kalıcı olarak yeniden yönlendirme

Web uygulamalarında sayfaları ve diğer içerikleri zamana göre taşımak için sık kullanılan bir uygulamadır. Bu, arama altyapılarındaki eski bağlantıların birikmesine yol açabilir. ASP.NET ' de, geliştiriciler, isteği yeni URL 'ye iletmek için *Response. Redirect* metodunu kullanarak kullanarak eski URL 'lere istekleri ister. Ancak, *yeniden yönlendirme* YÖNTEMI bir http 302 bulundu (geçici yeniden yönlendirme) yanıtı verir ve bu, kullanıcılar eski URL 'lere erişmeyi denediklerinde fazladan bir http gidiş yolculuğuna neden olur.

ASP.NET 4, aşağıdaki örnekte olduğu gibi HTTP 301 taşınan kalıcı yanıtlarını kolayca vermesini kolaylaştıran yeni bir *Redirectkalıcı* yardımcı yöntemi ekler:

[!code-csharp[Main](overview/samples/sample8.cs)]

Kalıcı yeniden yönlendirmeleri tanıyan arama motorları ve diğer kullanıcı aracıları, içerik ile ilişkili yeni URL 'YI depolar ve bu da geçici yeniden yönlendirmeler için tarayıcının yaptığı gereksiz gidiş dönüş gereksinimini ortadan kaldırır.

<a id="0.2__Toc224729022"></a><a id="0.2__Toc253429243"></a><a id="0.2__Toc243304617"></a>

### <a name="shrinking-session-state"></a>Oturum durumunu küçültme

ASP.NET, oturum durumunu bir Web grubu genelinde depolamak için iki varsayılan seçenek sunar: işlem dışı oturum durumu sunucusunu çağıran bir oturum durumu sağlayıcısı ve verileri Microsoft SQL Server veritabanında depolayan bir oturum durumu sağlayıcısı. Her iki seçenek de durum bilgilerini bir Web uygulamasının çalışan işlemi dışında depoladığını içerdiğinden, oturum durumunun uzak depolamaya gönderilmeden önce serileştirilmesi gerekir. Bir geliştiricinin oturum durumunda ne kadar bilgi kaydetdiğine bağlı olarak, serileştirilmiş verilerin boyutu çok büyük büyüyebilir.

ASP.NET 4, işlem dışı oturum durumu sağlayıcılarının her iki türü için yeni bir sıkıştırma seçeneği sunar. Aşağıdaki örnekte gösterilen *CompressionEnabled* yapılandırma seçeneği *true*olarak ayarlandığında ASP.net, .NET Framework *System. IO. Compression. GZipStream* sınıfını kullanarak serileştirilmiş oturum durumunu sıkıştırır (ve sıkıştırmasını açılır).

[!code-xml[Main](overview/samples/sample9.xml)]

Yeni özniteliğin `Web.config` dosyasına basit bir şekilde eklenmesi sayesinde, Web sunucuları üzerinde yedek CPU döngülerine sahip uygulamalar, serileştirilmiş oturum durumu verilerinin boyutunda önemli ölçüde indirimleri fark edebilir.

<a id="0.2__Toc253429244"></a><a id="0.2__Toc243304618"></a>

### <a name="expanding-the-range-of-allowable-urls"></a>Izin verilen URL 'Lerin aralığı genişletiliyor

ASP.NET 4, uygulama URL 'Lerinin boyutunu genişletmeye yönelik yeni seçenekler sunar. ASP.NET 'in önceki sürümleri, NTFS dosya yolu sınırına göre 260 karakter uzunluğunda bir biçimde kısıtlanmış URL yol uzunluklarına sahiptir. ASP.NET 4 ' te, iki yeni *httpRuntime* yapılandırma özniteliği kullanarak bu sınırı uygulamalarınıza uygun şekilde artırma (veya azaltma) seçeneğiniz vardır. Aşağıdaki örnek bu yeni öznitelikleri gösterir.

[!code-xml[Main](overview/samples/sample10.xml)]

Daha uzun veya daha kısa yollara izin vermek için (URL 'nin protokol, sunucu adı ve sorgu dizesi içermeyen bölümü), *[MaxUrlLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)* özniteliğini değiştirin. Daha uzun veya daha kısa sorgu dizelerine izin vermek için *[MaxQueryStringLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)* özniteliğinin değerini değiştirin.

ASP.NET 4, URL karakter denetimi tarafından kullanılan karakterleri yapılandırmanıza de olanak sağlar. ASP.NET bir URL 'nin yol bölümünde geçersiz bir karakter bulduğunda, isteği reddeder ve HTTP 400 hatası verir. Önceki ASP.NET sürümlerinde, URL karakter denetimleri sabit bir karakter kümesiyle sınırlandırılmıştır. ASP.NET 4 ' te, aşağıdaki örnekte gösterildiği gibi, *httpRuntime* yapılandırma öğesinin yeni *RequestPathInvalidCharacters* özniteliğini kullanarak geçerli karakterler kümesini özelleştirebilirsiniz:

[!code-xml[Main](overview/samples/sample11.xml)]

Varsayılan olarak, *RequestPathInvalidCharacters* özniteliği sekiz karakteri geçersiz olarak tanımlar. (Varsayılan olarak *RequestPathInvalidCharacters* 'e atanan dizede, `Web.config` dosyası bir XML dosyası olduğundan, küçüktür (&lt;), büyüktür (&gt;) ve ampersan (&amp;) karakterleri kodlanır.) Gerektiğinde geçersiz karakter kümesini özelleştirebilirsiniz.

> [!NOTE]
> Note ASP.NET 4, IETF 'nin ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt)) RFC 2396 ' de tanımlanan geçersiz URL karakterleri olduğundan, her zaman 0x00-0x1F ASCII aralığındaki KARAKTERLERI içeren URL yollarını reddeder. IIS 6 veya üstünü çalıştıran Windows Server sürümlerinde, http. sys protokol cihazı sürücüsü bu karakterlerle URL 'Leri otomatik olarak reddeder.

<a id="0.2__Toc253429245"></a><a id="0.2__Toc243304619"></a>

### <a name="extensible-request-validation"></a>Genişletilebilir Istek doğrulaması

ASP.NET istek doğrulaması, siteler arası komut dosyası (XSS) saldırılarına karşı yaygın olarak kullanılan dizeler için gelen HTTP istek verilerini arar. Olası XSS dizeleri bulunursa, istek doğrulama bayrakları şüpheli dizeyi ve bir hata döndürür. Yerleşik istek doğrulaması yalnızca XSS saldırılarına karşı kullanılan en yaygın dizeleri bulduğunda bir hata döndürür. XSS doğrulamasını daha fazla agresif hale getirmeye yönelik önceki girişimler çok fazla hatalı pozitif sonuç ile sonuçlandı. Ancak, müşteriler daha agresif veya buna karşılık gelen istek doğrulaması için belirli sayfalar veya belirli istek türleri için denetim yapmak isteyebilir.

ASP.NET 4 ' te, özel istek doğrulama mantığını kullanabilmeniz için istek doğrulama özelliği Genişletilebilir hale getirilir. İstek doğrulamayı genişletmek için, yeni *System. Web. util. RequestValidator* türünden türeten bir sınıf oluşturur ve uygulamayı (`Web.config` dosyasının *httpRuntime* bölümünde) özel türü kullanacak şekilde yapılandırırsınız. Aşağıdaki örnek, bir özel istek doğrulama sınıfının nasıl yapılandırılacağını göstermektedir:

[!code-xml[Main](overview/samples/sample12.xml)]

Yeni *RequestValidationType* özniteliği, özel istek doğrulaması sağlayan sınıfı belirten standart bir .NET Framework tür tanımlayıcı dizesi gerektirir. Her istek için ASP.NET, gelen HTTP istek verilerinin her parçasını işlemek üzere özel türü çağırır. Gelen URL, tüm HTTP üst bilgileri (hem tanımlama bilgileri hem de özel üstbilgiler) ve varlık gövdesi, aşağıdaki örnekte gösterildiği gibi özel bir istek doğrulama sınıfı tarafından denetim için kullanılabilir:

[!code-csharp[Main](overview/samples/sample13.cs)]

Gelen HTTP verilerinin bir parçasını incelemek istemediğiniz durumlarda, istek doğrulama sınıfı ASP.NET varsayılan istek doğrulamasının yalnızca temel çağırarak çalışmasına izin vermek üzere geri dönebilir *. IsValidRequestString.*

<a id="0.2__Toc253429246"></a><a id="0.2__Toc243304620"></a>

### <a name="object-caching-and-object-caching-extensibility"></a>Nesne önbelleğe alma ve nesne önbelleğe alma genişletilebilirliği

İlk sürümü olan ASP.NET, güçlü bir bellek içi nesne önbelleği (*System. Web. Caching. Cache*) içeriyordu. Önbellek uygulaması, Web 'e ait olmayan uygulamalarda kullanılma yaygındır. Ancak, ASP.NET nesne önbelleğini kullanabilmek için bir Windows Forms veya WPF uygulamasının `System.Web.dll` bir başvuru içermesi gerekir.

Önbelleğe alma işlemini tüm uygulamalarda kullanılabilir hale getirmek için, .NET Framework 4 yeni bir derleme, yeni bir ad alanı, bazı temel türler ve somut bir önbelleğe alma uygulaması sağlar. Yeni `System.Runtime.Caching.dll` derlemesi *System. Runtime. Caching* ad alanında yeni bir önbelleğe alma API 'si içerir. Ad alanı iki temel sınıf kümesi içerir:

- Herhangi bir tür özel önbellek uygulamasını oluşturmak için temel sağlayan soyut türler.
- Somut bellek içi nesne önbelleği uygulama ( *System. Runtime. Caching. MemoryCache* sınıfı).

Yeni *MemoryCache* sınıfı, ASP.net önbelleğine yakından modellenir ve ASP.NET ile iç önbellek altyapısı mantığının çoğunu paylaşır. *System. Runtime. Caching* içindeki genel önbelleğe alma API 'leri özel önbelleklerin geliştirilmesini destekleyecek şekilde güncelleştirildiğinden, ASP.net *Cache* nesnesini kullandıysanız, yeni API 'lerde tanıdık kavramlar bulacaksınız.

Yeni *MemoryCache* sınıfı ve destekleyici temel API 'lerin derinlemesine bir tartışması tüm belgeyi gerektirecektir. Ancak aşağıdaki örnek, yeni Önbellek API 'sinin nasıl çalıştığına ilişkin bir fikir verir. Örnek, `System.Web.dll`bağımlılığı olmadan Windows Forms bir uygulama için yazılmıştır.

[!code-csharp[Main](overview/samples/sample14.cs)]

<a id="0.2__Toc253429247"></a><a id="0.2__Toc243304621"></a>

### <a name="extensible-html-url-and-http-header-encoding"></a>Genişletilebilir HTML, URL ve HTTP üst bilgi kodlaması

ASP.NET 4 ' te, aşağıdaki ortak metin kodlama görevleri için özel kodlama yordamları oluşturabilirsiniz:

- HTML kodlaması.
- URL kodlaması.
- HTML öznitelik kodlaması.
- Giden HTTP üst bilgilerini kodlama.

Yeni *System. Web. util. HttpEncoder* türünden türeterek özel bir kodlayıcı oluşturabilir ve sonra aşağıdaki örnekte gösterildiği gibi `Web.config` dosyanın *httpRuntime* bölümünde özel türü kullanmak için ASP.net yapılandırabilirsiniz:

[!code-xml[Main](overview/samples/sample15.xml)]

Özel bir kodlayıcı yapılandırıldıktan sonra, *System. Web. HttpUtility* veya *System. Web. HttpServerUtility* sınıflarının ortak kodlama yöntemleri her çağrıldığında ASP.NET otomatik olarak özel kodlama uygulamasını çağırır. Bu, Web geliştirme ekibinin bir kısmının agresif karakter kodlaması uygulayan özel bir kodlayıcı oluşturmasına izin verir, ancak Web geliştirme ekibinin geri kalanı ortak ASP.NET Encoding API 'Lerini kullanmaya devam eder. *HttpRuntime* öğesinde bir özel kodlayıcı merkezi olarak yapılandırarak, genel ASP.net Encoding API 'lerinde bulunan tüm metin kodlama çağrılarının özel kodlayıcı aracılığıyla yönlendirildiği garanti edilir.

<a id="0.2__Toc253429248"></a><a id="0.2__Toc243304622"></a>

### <a name="performance-monitoring-for-individual-applications-in-a-single-worker-process"></a>Tek bir çalışan Işlemindeki ayrı uygulamalar için performans Izleme

Tek bir sunucuda barındırılabilecek Web sitelerinin sayısını artırmak için birçok barındırıcıların tek bir çalışan işleminde birden çok ASP.NET uygulaması çalıştırır. Ancak, birden çok uygulama tek bir paylaşılan çalışan işlemi kullanıyorsa, sunucu yöneticilerinin sorun yaşayan tek bir uygulamayı tanımlaması zordur.

ASP.NET 4, CLR tarafından sunulan yeni kaynak izleme işlevlerinden yararlanır. Bu işlevi etkinleştirmek için aşağıdaki XML yapılandırma kod parçacığını `aspnet.config` yapılandırma dosyasına ekleyebilirsiniz.

[!code-xml[Main](overview/samples/sample16.xml)]

> [!NOTE]
> `aspnet.config` dosyanın .NET Framework yüklendiği dizinde olduğunu aklınızda edin. `Web.config` dosyası değil.

*Appdomainresourcemonitoring* özelliği etkinleştirildiğinde, "ASP.net Applications" performans kategorisinde iki yeni performans sayacı bulunur: *% yönetilen Işlemci zamanı* ve *yönetilen bellek kullanıldı*. Bu performans sayaçlarından her ikisi de, tek tek ASP.NET uygulamalarının tahmini CPU süresini ve yönetilen bellek kullanımını izlemek için yeni CLR Application-Domain kaynak yönetimi özelliğini kullanır. Sonuç olarak, ASP.NET 4 ile yöneticiler artık tek bir çalışan işlemde çalışan tek tek uygulamaların kaynak tüketimine daha ayrıntılı bir görünüm elde ediyor.

<a id="0.2__Toc253429249"></a><a id="0.2__Toc243304623"></a>

### <a name="multi-targeting"></a>Çoklu Sürüm Desteği

.NET Framework belirli bir sürümünü hedefleyen bir uygulama oluşturabilirsiniz. ASP.NET 4 ' te, `Web.config` dosyanın *derleme* öğesindeki yeni bir öznitelik, .NET Framework 4 ve üstünü hedeflemenizi sağlar. .NET Framework 4 ' ü açıkça hedefliyorsanız ve `Web.config` dosyasına *System. CodeDom*girişleri gibi isteğe bağlı öğeler eklerseniz, bu öğelerin .NET Framework 4 için doğru olması gerekir. (.NET Framework 4 ' ü açık bir şekilde Hedeflemeyin, hedef Framework, `Web.config` dosyasındaki bir girdinin olmamasından itibaren algılanır.)

Aşağıdaki örnek, `Web.config` dosyasının *derleme* öğesinde *TargetFramework* özniteliğinin kullanımını gösterir.

[!code-xml[Main](overview/samples/sample17.xml)]

.NET Framework belirli bir sürümünü hedeflemek hakkında aşağıdakilere göz önünde kalın:

- .NET Framework 4 uygulama havuzunda, `Web.config` dosyasında *TargetFramework* özniteliği yoksa veya `Web.config` dosyası eksikse, ASP.NET derleme sistemi bir hedef olarak .NET Framework 4 ' ü varsayar. (.NET Framework 4 ' ün altında çalışmasını sağlamak için uygulamanızda kodlama değişiklikleri yapmanız gerekebilir.)
- *TargetFramework* özniteliğini dahil ederseniz ve *System. CodeDom* öğesi `Web.config` dosyasında tanımlanmışsa, bu dosya .NET Framework 4 için doğru girdileri içermelidir.
- Uygulamanızı önceden derlemek için *aspnet\_derleyici* komutunu (örneğin, bir derleme ortamında) kullanıyorsanız, hedef çerçeve için *ASPNET\_derleyicisi* komutunun doğru sürümünü kullanmanız gerekir. .NET Framework 3,5 ve önceki sürümleri için derlemek üzere .NET Framework 2,0 (%WINDIR%\Microsoft.NET\Framework\v2.0.50727) ile birlikte gelen derleyicisini kullanın. Bu Framework kullanılarak oluşturulan uygulamaları derlemek veya sonraki sürümleri kullanmak için .NET Framework 4 ile birlikte gelen derleyicisini kullanın.
- Çalışma zamanında derleyici, bilgisayarda yüklü olan en son çerçeve derlemelerini (ve bu nedenle GAC 'de) kullanır. Bir güncelleştirme daha sonra çerçeveye yapılırsa (örneğin, kuramsal bir sürüm 4,1 yüklüyse), *TargetFramework* özniteliği daha düşük bir sürümü (örneğin, 4,0) hedeflese bile, Framework 'ün yeni sürümündeki özellikleri kullanabilirsiniz. (Ancak, Visual Studio 2010 ' de tasarım zamanında veya *aspnet\_derleyici* komutunu kullandığınızda, Framework 'ün daha yeni özellikleri kullanmak derleyici hatalarına neden olur).

<a id="0.2__Toc224729023"></a><a id="0.2__Toc253429250"></a><a id="0.2__Toc243304624"></a>

## <a name="ajax"></a>Ajax

<a id="0.2__Toc253429251"></a><a id="0.2__Toc243304625"></a>

### <a name="jquery-included-with-web-forms-and-mvc"></a>Web Forms ve MVC ile birlikte bulunan jQuery

Hem Web Forms hem de MVC için Visual Studio şablonları, açık kaynak jQuery kitaplığını içerir. Yeni bir Web sitesi veya proje oluşturduğunuzda, aşağıdaki 3 dosyayı içeren betikler klasörü oluşturulur:

- jQuery-1.4.1. js – jQuery kitaplığının insan tarafından okunabilen, küçültülmüş olmayan sürümüdür.
- jQuery-14,1. min. js – jQuery kitaplığının küçültülmüş sürümü.
- jQuery-1.4.1-vsdoc. js – jQuery kitaplığı için IntelliSense belge dosyası.

Uygulama geliştirirken jQuery 'in küçültülmüş sürümünü dahil edin. Üretim uygulamaları için jQuery 'in küçültülmüş sürümünü dahil edin.

Örneğin, aşağıdaki Web Forms sayfasında, odak olduğunda ASP.NET TextBox denetimlerinin arka plan rengini değiştirmek için jQuery nasıl kullanabileceğiniz gösterilmektedir.

[!code-aspx[Main](overview/samples/sample18.aspx)]

<a id="0.2__Toc253429252"></a><a id="0.2__Toc243304626"></a>

### <a name="content-delivery-network-support"></a>Content Delivery Network desteği

Microsoft Ajax Content Delivery Network (CDN), Web uygulamalarınıza kolayca ASP.NET AJAX ve jQuery betikleri eklemenizi sağlar. Örneğin, sayfanıza aşağıdaki gibi Ajax.microsoft.com işaret eden bir `<script>` etiketi ekleyerek jQuery kitaplığını kullanmaya başlayabilirsiniz:

[!code-html[Main](overview/samples/sample19.html)]

Microsoft Ajax CDN 'nin avantajlarından yararlanarak, Ajax uygulamalarınızın performansını önemli ölçüde artırabilirsiniz. Microsoft Ajax CDN içerikleri dünyanın dört bir yanındaki sunucularda önbelleğe alınır. Ayrıca, Microsoft Ajax CDN, tarayıcıların farklı etki alanlarında bulunan Web siteleri için önbelleğe alınmış JavaScript dosyalarını yeniden kullanmasına olanak sağlar.

Microsoft Ajax Content Delivery Network, Güvenli Yuva Katmanı kullanarak bir Web sayfasına ihtiyacınız olması durumunda SSL 'yi (HTTPS) destekler.

CDN kullanılamadığında geri dönüş uygulayın. Geri dönüşü test edin.

Microsoft Ajax CDN hakkında daha fazla bilgi edinmek için aşağıdaki Web sitesini ziyaret edin:

[https://www.asp.net/ajaxlibrary/CDN.ashx](../../ajax/cdn/overview.md)

ASP.NET ScriptManager, Microsoft Ajax CDN 'yi destekler. Yalnızca bir özelliği, EnableCdn özelliğini ayarlayarak CDN 'den tüm ASP.NET Framework JavaScript dosyalarını alabilirsiniz:

[!code-aspx[Main](overview/samples/sample20.aspx)]

EnableCdn özelliğini true değerine ayarladıktan sonra, ASP.NET Framework, doğrulama ve UpdatePanel için kullanılan tüm JavaScript dosyaları dahil olmak üzere CDN 'den tüm ASP.NET Framework JavaScript dosyalarını alır. Bu bir özelliğin ayarlanması, Web uygulamanızın performansı üzerinde önemli bir etkiye sahip olabilir.

WebResource özniteliğini kullanarak kendi JavaScript dosyalarınız için CDN yolunu ayarlayabilirsiniz. Yeni CdnPath özelliği, EnableCdn özelliğini true değerine ayarladığınızda kullanılan CDN 'nin yolunu belirtir:

[!code-csharp[Main](overview/samples/sample21.cs)]

<a id="0.2__Toc253429253"></a><a id="0.2__Toc243304627"></a>

### <a name="scriptmanager-explicit-scripts"></a>ScriptManager açık betikler

Geçmişte, ASP.NET ScriptManager ' ı kullandıysanız, tüm monoparçalı ASP.NET Ajax Kitaplığı 'nı yüklemeniz gerekiyordu. Yeni ScriptManager. AjaxFrameworkMode özelliğinden yararlanarak, ASP.NET Ajax Kitaplığı 'nın hangi bileşenlerinin yüklendiğini ve yalnızca ihtiyacınız olan ASP.NET Ajax Kitaplığı bileşenlerini yükleyebileceğini denetleyebilirsiniz.

ScriptManager. AjaxFrameworkMode özelliği aşağıdaki değerlere ayarlanabilir:

- Etkin--ScriptManager denetiminin her çekirdek çerçeve betiğinin (eski davranış) birleştirilmiş bir betik dosyası olan MicrosoftAjax. js betik dosyasını otomatik olarak içerdiğini belirtir.
- Devre dışı--tüm Microsoft Ajax betiği özelliklerinin devre dışı bırakıldığını ve ScriptManager denetiminin hiçbir komut dosyasına otomatik olarak başvurmadığından emin olarak belirtir.
- Açık--Sayfanızın gerektirdiği tek bir Framework Çekirdek betik dosyasına betik başvurularını açıkça dahil edileceğini ve her bir betik dosyasının gerektirdiği bağımlılıklara başvuruları dahil edileceğini belirtir.

Örneğin, AjaxFrameworkMode özelliğini açık değerine ayarlarsanız, ihtiyacınız olan belirli ASP.NET AJAX bileşen betikleri belirtebilirsiniz:

[!code-aspx[Main](overview/samples/sample22.aspx)]

<a id="0.2__The_DataView_Control"></a><a id="0.2__The_DataContext_and"></a><a id="0.2__Refactoring_the_Microsoft"></a><a id="0.2__Toc224729032"></a><a id="0.2__Toc253429256"></a><a id="0.2__Toc243304630"></a>

## <a name="web-forms"></a>Web Forms

Web Forms, ASP.NET 1,0 ' nin yayımlanmasından bu yana ASP.NET içinde çekirdek bir özelliktir. Bu alanda, aşağıdakiler dahil olmak üzere ASP.NET 4 için pek çok geliştirme yapılmıştır:

- *Meta* Etiketleri ayarlama yeteneği.
- Görünüm durumu üzerinde daha fazla denetim.
- Tarayıcı özellikleri ile çalışmanın daha kolay yolları.
- Web Forms ile ASP.NET yönlendirme kullanma desteği.
- Oluşturulan kimlikler üzerinde daha fazla denetim.
- Veri denetimlerinde seçili satırları kalıcı hale getirme özelliği.
- *FormView* ve *LISTVIEW* denetimlerinde işlenmiş html üzerinde daha fazla denetim.
- Veri kaynağı denetimleri için filtreleme desteği.

<a id="0.2__Toc224729033"></a><a id="0.2__Toc253429257"></a><a id="0.2__Toc243304631"></a>

### <a name="setting-meta-tags-with-the-pagemetakeywords-and-pagemetadescription-properties"></a>Meta etiketler Page. MetaKeywords ve Page. MetaDescription özellikleriyle ayarlanıyor

ASP.NET 4, *sayfa* sınıfına, *MetaKeywords* ve *MetaDescription*'a iki özellik ekler. Bu iki özellik, aşağıdaki örnekte gösterildiği gibi sayfanızda karşılık gelen *meta* etiketleri temsil eder:

[!code-aspx[Main](overview/samples/sample23.aspx)]

Bu iki özellik, sayfanın *title* özelliğiyle aynı şekilde çalışır. Bunlar şu kurallara uyar:

1. *Baş* öğede Özellik adlarıyla eşleşen hiçbir *meta* etiketi yoksa (sayfa. MetaDescription için Name = "Keywords *" ve* *Page. MetaDescription*için Name = "Description", bu özelliklerin ayarlanmayan anlamına gelir), bu özellik, işlendiğinde, *meta* etiketleri sayfaya eklenir.
2. Bu adlarla zaten *meta* Etiketler varsa, bu özellikler mevcut etiketlerin içeriği için Get ve set yöntemleri olarak davranır.

Bu özellikleri çalışma zamanında ayarlayabilirsiniz, bu da bir veritabanından veya başka bir kaynaktan içerik almanızı sağlar ve bu sayede belirli bir sayfanın ne için olduğunu açıklayan etiketleri dinamik olarak ayarlamanıza olanak tanır.

Ayrıca, aşağıdaki örnekte olduğu gibi, Web Forms sayfa biçimlendirmesinin en üstündeki *@ Page* yönergesinin *anahtar sözcüklerini* ve *Açıklama* özelliklerini de ayarlayabilirsiniz:

[!code-aspx[Main](overview/samples/sample24.aspx)]

Bu, sayfada zaten belirtilen *meta* etiketi içeriğini (varsa) geçersiz kılar.

Açıklama *meta* etiketinin Içeriği, Google 'daki arama listesi önizlemelerini iyileştirmek için kullanılır. (Ayrıntılar için bkz. Google Web merkezi blogundan [meta açıklama makeon ile kod parçacıklarını geliştirme](https://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html) .) Google ve Windows Live Search, hiçbir şey için anahtar sözcüklerin içeriğini kullanmaz, ancak diğer arama motorları da oluşabilir. Daha fazla bilgi için bkz. arama motoru Kılavuzu Web sitesinde [meta anahtar sözcükleri önerisi](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php) .

Bu yeni özellikler basit bir özelliktir, ancak bunları el ile eklemek veya *meta* Etiketler oluşturmak için kendi kodunuzu yazmak için gerekli adımları kaydeder.

<a id="0.2__Toc224729034"></a><a id="0.2__Toc253429258"></a><a id="0.2__Toc243304632"></a>

### <a name="enabling-view-state-for-individual-controls"></a>Bireysel denetimler için görünüm durumunu etkinleştirme

Varsayılan olarak, sayfa için Görünüm durumu etkindir ve bu, sayfadaki her bir denetimin, uygulama için gerekli olmasa bile görünüm durumunu depolayabileceği sonucudur. Görünüm durumu verileri bir sayfanın oluşturduğu biçimlendirmeye dahildir ve istemciye bir sayfa göndermek için geçen süreyi artırır ve geri gönderin. Gerekenden daha fazla görünüm durumu depolanması, önemli performans düşüşüne neden olabilir. ASP.NET 'in önceki sürümlerinde, geliştiriciler sayfa boyutunu azaltmak için tek tek denetimler için görünüm durumunu devre dışı bırakabilir, ancak tek tek denetimler için bunu açıkça yapmak zorunda kalmıştı. ASP.NET 4 ' te, Web sunucusu denetimleri, varsayılan olarak görünüm durumunu devre dışı bırakmanızı ve yalnızca sayfada bunu gerektiren denetimler için etkinleştirmenizi sağlayan bir *ViewStateMode* özelliği içerir.

*ViewStateMode* özelliği, üç değere sahip bir sabit listesi alır: *etkin*, *devre dışı*ve *Devralma*. *Etkin* , bu denetim Için ve *Devralma* olarak ayarlanan veya hiçbir şey ayarlanmamış olan tüm alt denetimler için görünüm durumunu sağlar. *Disabled* görünüm durumunu devre dışı bırakır ve *Devralma* , denetimin, üst denetimden *ViewStateMode* ayarını kullandığını belirtir.

Aşağıdaki örnek, *ViewStateMode* özelliğinin nasıl çalıştığını gösterir. Aşağıdaki sayfadaki denetimlerle ilgili biçimlendirme ve kod, *ViewStateMode* özelliği için değerler içerir:

[!code-aspx[Main](overview/samples/sample25.aspx)]

Görebileceğiniz gibi, kod PlaceHolder1 denetimi için görünüm durumunu devre dışı bırakır. Alt Label1 denetimi bu özellik değerini devralır (*Inherit* , denetimler Için *ViewStateMode* için varsayılan değerdir.) ve bu nedenle hiçbir görünüm durumu kaydeder. PlaceHolder2 denetiminde, *ViewStateMode* *etkin*olarak ayarlanır, bu nedenle etiket 2 Bu özelliği devralır ve görünüm durumunu kaydeder. Sayfa ilk yüklendiğinde, her iki *etiket* denetiminin *Text* özelliği "[dynamicvalue]" dizesine ayarlanır.

Bu ayarların etkisi, sayfa ilk kez yüklendiğinde aşağıdaki Çıktının tarayıcıda görüntülenmesiyle ilgili olacaktır:

Devre dışı `: [DynamicValue]`

Etkin:`[DynamicValue]`

Ancak geri gönderme sonrasında aşağıdaki çıktı görüntülenir:

Devre dışı `: [DeclaredValue]`

Etkin:`[DynamicValue]`

Label1 denetimi ( *ViewStateMode* değeri *devre dışı*olarak ayarlanan), kod içinde olarak ayarlandığı değeri korunmaz. Ancak, etiket 2 denetimi ( *ViewStateMode* değeri *Enabled*olarak ayarlanmıştır), durumunu saklandı.

Ayrıca, aşağıdaki örnekte olduğu gibi,, *@ Page* yönergesinde *ViewStateMode* öğesini de ayarlayabilirsiniz:

[!code-aspx[Main](overview/samples/sample26.aspx)]

*Sayfa* sınıfı yalnızca başka bir denetimdir; sayfadaki tüm diğer denetimler için üst denetim görevi görür. *ViewStateMode* varsayılan değeri *sayfa*örnekleri için *etkinleştirilmiştir* . Denetimleri varsayılan olarak *devralması*için, sayfa veya Denetim düzeyinde *ViewStateMode* 'U ayarlamadığınız müddetçe denetimler *etkin* özellik değerini alır.

*ViewStateMode* özelliğinin değeri, yalnızca *EnableViewState* özelliği *true*olarak ayarlandığında görünüm durumunun tutulup tutulamayacağını belirler. *EnableViewState* özelliği *false*olarak ayarlandıysa, *ViewStateMode* *etkin*olarak ayarlanmış olsa bile görünüm durumu korunmaz.

Bu özellik için iyi bir kullanım, ana sayfalarda, *ViewStateMode* 'u ana sayfa Için *devre dışı* olarak ayarlayabileceğiniz ve sonra da görünüm durumu gerektiren denetimleri içeren *ContentPlaceHolder* denetimleri için tek tek etkinleştirebileceğiniz *ContentPlaceHolder* denetimleridir.

<a id="0.2__Toc224729035"></a><a id="0.2__Toc253429259"></a><a id="0.2__Toc243304633"></a>

### <a name="changes-to-browser-capabilities"></a>Tarayıcı özelliklerine yapılan değişiklikler

ASP.NET *tarayıcı özellikleri*adlı bir özellik kullanarak sitenize taramak için kullanıcının kullandığı tarayıcının yeteneklerini belirler. Tarayıcı Özellikleri, *HttpBrowserCapabilities* nesnesiyle temsil edilir ( *istek. Browser* özelliği tarafından gösterilir). Örneğin, geçerli tarayıcının türünün ve sürümünün JavaScript 'in belirli bir sürümünü destekleyip desteklemediğini anlamak için *HttpBrowserCapabilities* nesnesini kullanabilirsiniz. Ya da, isteğin bir mobil cihazdan kaynaklanıp kaynaklanmadığını öğrenmek için *HttpBrowserCapabilities* nesnesini de kullanabilirsiniz.

*HttpBrowserCapabilities* nesnesi, bir dizi tarayıcı tanım dosyası tarafından çalıştırılır. Bu dosyalar, belirli tarayıcıların özellikleri hakkında bilgiler içerir. ASP.NET 4 ' te bu tarayıcı tanımı dosyaları, son kullanılan tarayıcılar ve Google Chrome, Motion BlackBerry smartphone 'lar ve Apple iPhone gibi en son sunulan tarayıcılar ve cihazlar hakkında bilgi içerecek şekilde güncelleştirilmiştir.

Aşağıdaki listede yeni tarayıcı tanım dosyaları gösterilmektedir:

- *BlackBerry. Browser*
- *Chrome. Browser*
- *Varsayılan. Browser*
- *Firefox. Browser*
- *Gateway. Browser*
- *Genel. Browser*
- *IE. Browser*
- *Iemobile. Browser*
- *iPhone. Browser*
- *Opera. Browser*
- *Safari. Browser*

#### <a name="using-browser-capabilities-providers"></a>Tarayıcı özellikleri sağlayıcılarını kullanma

ASP.NET sürüm 3,5 hizmet paketi 1 ' de, bir tarayıcının aşağıdaki yollarla sahip olduğu özellikleri tanımlayabilirsiniz:

- Bilgisayar düzeyinde, aşağıdaki klasörde bir `.browser` XML dosyası oluşturur veya güncelleştirin:

- [!code-console[Main](overview/samples/sample27.cmd)]

- Tarayıcı yeteneklerini tanımladıktan sonra, tarayıcı yetenekleri derlemesini yeniden derlemek ve GAC 'ye eklemek için Visual Studio komut Isteminden aşağıdaki komutu çalıştırın:

- [!code-console[Main](overview/samples/sample28.cmd)]

- Tek bir uygulama için, uygulamanın `App_Browsers` klasöründe bir `.browser` dosyası oluşturursunuz.

Bu yaklaşımlar, XML dosyalarını değiştirmenizi gerektirir ve bilgisayar düzeyinde değişiklikler için, ASPNET\_regbrowsers. exe işlemini çalıştırdıktan sonra uygulamayı yeniden başlatmanız gerekir.

ASP.NET 4, *tarayıcı özellikleri sağlayıcıları*olarak adlandırılan bir özelliği içerir. Adından da anlaşılacağı gibi, bu, tarayıcı yeteneklerini tespit etmek için kendi kodunuzu kullanmanıza olanak sağlayan bir sağlayıcı oluşturmanızı sağlar.

Pratikte geliştiriciler genellikle özel tarayıcı özellikleri tanımlamaz. Tarayıcı dosyalarının güncelleştirilmesi zor, bunları güncelleştirme süreci oldukça karmaşıktır ve `.browser` dosyaları için XML sözdiziminin kullanılması ve tanımlanması karmaşık olabilir. Ortak bir tarayıcı tanımı söz dizimi veya güncel tarayıcı tanımları içeren bir veritabanı ya da böyle bir veritabanı için Web hizmeti olan bu işlemi çok daha kolay hale getirir. Yeni tarayıcı özellikleri sağlayıcıları özelliği, üçüncü taraf geliştiriciler için bu senaryoları mümkün kılar ve pratik hale getirir.

Yeni ASP.NET 4 tarayıcı özellikleri sağlayıcısı özelliğini kullanmak için iki ana yaklaşım vardır: ASP.NET Browser özellikleri tanım işlevselliğini genişletme veya tamamen değiştirme. Aşağıdaki bölümlerde, işlevin nasıl değiştirileceği ve sonra nasıl genişletileceği açıklanır.

#### <a name="replacing-the-aspnet-browser-capabilities-functionality"></a>ASP.NET Browser özellikleri Işlevini değiştirme

ASP.NET Browser özellikleri tanım işlevini tamamen değiştirmek için şu adımları izleyin:

1. Aşağıdaki örnekte olduğu gibi *Httpcapabilitiessağlayıcısından* türetilen ve *GetBrowserCapabilities* yöntemini geçersiz kılan bir sağlayıcı sınıfı oluşturun: 

    [!code-csharp[Main](overview/samples/sample29.cs)]

    Bu örnekteki kod, yalnızca Browser adlı özelliği belirterek ve MyCustomBrowser özelliğini ayarlayarak yeni bir *HttpBrowserCapabilities* nesnesi oluşturur.
2. Sağlayıcıyı uygulamayla kaydedin. 

    Bir sağlayıcıyı uygulamayla birlikte kullanmak için, `Web.config` veya `Machine.config` dosyalarındaki *browserCaps* bölümüne *provider* özniteliğini eklemeniz gerekir. (Ayrıca, belirli bir mobil cihazın bir klasörü gibi, uygulamadaki belirli dizinler için bir *konum* öğesinde sağlayıcı özniteliklerini de tanımlayabilirsiniz.) Aşağıdaki örnekte, bir yapılandırma dosyasında *sağlayıcı* özniteliğinin nasıl ayarlanacağı gösterilmektedir:

    [!code-xml[Main](overview/samples/sample30.xml)]

    Yeni tarayıcı yetenek tanımı 'nı kaydetmek için başka bir yöntem de aşağıdaki örnekte gösterildiği gibi kod kullanmaktır:

    [!code-csharp[Main](overview/samples/sample31.cs)]

    Bu kodun, `Global.asax` dosyasının *uygulama\_başlangıç* olayında çalışması gerekir. Uygulamanın çözümlenmiş *HttpCapabilitiesBase* nesnesi için geçerli bir durumda kaldığından emin olmak Için, *BrowserCapabilitiesProvider* sınıfında yapılan herhangi bir değişiklik, uygulamadaki herhangi bir kod üzerinde gerçekleşmelidir.

#### <a name="caching-the-httpbrowsercapabilities-object"></a>HttpBrowserCapabilities nesnesini önbelleğe alma

Yukarıdaki örnekte bir sorun vardır. Bu, kodun, *HttpBrowserCapabilities* nesnesini almak için özel sağlayıcının her çağrılışında çalışmasına neden olur. Bu, her istek sırasında birden çok kez gerçekleşebilir. Örnekte, sağlayıcının kodu çok daha yapmaz. Ancak, özel sağlayıcıdaki kod *HttpBrowserCapabilities* nesnesini almak için önemli iş gerçekleştiriyorsa, bu performansı etkileyebilir. Bunun oluşmasını engellemek için *HttpBrowserCapabilities* nesnesini önbelleğe alabilirsiniz. Aşağıdaki adımları uygulayın:

1. Aşağıdaki örnekte olduğu gibi *HttpCapabilitiesProvider*'dan türeten bir sınıf oluşturun: 

    [!code-csharp[Main](overview/samples/sample32.cs)]

    Örnekte, kod özel bir BuildCacheKey yöntemi çağırarak bir önbellek anahtarı oluşturur ve özel bir GetCacheTime yöntemi çağırarak önbelleğe alma süresi uzunluğunu alır. Kod daha sonra çözümlenen *HttpBrowserCapabilities* nesnesini önbelleğe ekler. Nesne önbellekten alınabilir ve özel sağlayıcıyı kullanan sonraki isteklerde yeniden kullanılabilir.
2. Önceki yordamda açıklandığı gibi sağlayıcıyı uygulamayla kaydedin.

#### <a name="extending-aspnet-browser-capabilities-functionality"></a>ASP.NET Browser özellikleri Işlevlerini genişletme

Önceki bölümde, ASP.NET 4 ' te yeni bir *HttpBrowserCapabilities* nesnesinin nasıl oluşturulacağı açıklanmaktadır. Ayrıca, daha önce ASP.NET içinde olan bir yeni tarayıcı özellikleri tanımları ekleyerek ASP.NET Browser özellikleri işlevini genişletebilirsiniz. Bunu XML tarayıcı tanımlarını kullanmadan yapabilirsiniz. Aşağıdaki yordamda nasıl yapılacağı gösterilmektedir.

1. Aşağıdaki örnekte gösterildiği gibi, *HttpCapabilitiesEvaluator* öğesinden türetilen ve *GetBrowserCapabilities* metodunu geçersiz kılan bir sınıf oluşturun: 

    [!code-csharp[Main](overview/samples/sample33.cs)]

    Bu kod, tarayıcıyı belirlemeyi denemek için önce ASP.NET Browser özellikleri işlevini kullanır. Ancak, istekte tanımlanan bilgiler temel alınarak hiçbir tarayıcı tanımlanmamışsa (yani, *HttpBrowserCapabilities* nesnesinin *Browser* özelliği "bilinmiyor" dizeyse), kod tarayıcıyı tanımlamak Için özel sağlayıcıyı (MyBrowserCapabilitiesEvaluator) çağırır.
2. Önceki örnekte açıklandığı gibi sağlayıcıyı uygulamayla kaydedin.

#### <a name="extending-browser-capabilities-functionality-by-adding-new-capabilities-to-existing-capabilities-definitions"></a>Mevcut yetenek tanımlarına yeni yetenekler ekleyerek tarayıcı özellikleri Işlevselliğini genişletme

Özel bir tarayıcı tanımı sağlayıcısı oluşturmaya ve dinamik olarak yeni tarayıcı tanımları oluşturmaya ek olarak, var olan tarayıcı tanımlarını ek yetenekler ile genişletebilirsiniz. Bu, istediğiniz kadar yakın olan ancak yalnızca birkaç özelliği olmayan bir tanım kullanmanıza olanak sağlar. Bunu yapmak için aşağıdaki adımları kullanın.

1. Aşağıdaki örnekte gösterildiği gibi, *HttpCapabilitiesEvaluator* öğesinden türetilen ve *GetBrowserCapabilities* metodunu geçersiz kılan bir sınıf oluşturun: 

    [!code-csharp[Main](overview/samples/sample34.cs)]

    Örnek kod, var olan ASP.NET *HttpCapabilitiesEvaluator* sınıfını genişletir ve aşağıdaki kodu kullanarak geçerli istek tanımıyla eşleşen *HttpBrowserCapabilities* nesnesini alır:

    [!code-csharp[Main](overview/samples/sample35.cs)]

    Kod daha sonra bu tarayıcı için bir özellik ekleyebilir veya değiştirebilir. Yeni bir tarayıcı özelliği belirlemek için iki yol vardır:

    - *HttpCapabilitiesBase* nesnesinin *Capabilities* özelliği tarafından açığa çıkarılan *IDictionary* nesnesine bir anahtar/değer çifti ekleyin. Önceki örnekte, kod, *true*değerine sahip multitouch adlı bir özellik ekler.
    - *HttpCapabilitiesBase* nesnesinin varolan özelliklerini ayarlayın. Önceki örnekte, kod *çerçeveler* özelliğini *true*olarak ayarlar. Bu özellik yalnızca yetenekler özelliği tarafından sunulan *IDictionary* nesnesine yönelik bir erişimciye *sahiptir* . 

        > [!NOTE]
        > Bu model, denetim bağdaştırıcıları dahil olmak üzere *HttpBrowserCapabilities*'ın herhangi bir özelliği için geçerlidir.
2. Sağlayıcıyı, önceki yordamda açıklandığı gibi uygulamayla kaydedin.

<a id="0.2__Toc224729036"></a><a id="0.2__Toc253429260"></a><a id="0.2__Toc243304634"></a>

### <a name="routing-in-aspnet-4"></a>ASP.NET 4 ' te yönlendirme

ASP.NET 4, Web Forms ile yönlendirmeyi kullanmak için yerleşik destek ekler. Yönlendirme, bir uygulamayı fiziksel dosyalarla eşlenmez istek URL 'Lerini kabul edecek şekilde yapılandırmanızı sağlar. Bunun yerine, kullanıcılar için anlamlı olan ve uygulamanıza yönelik arama motoru iyileştirmesi (SEO) konusunda yardımcı olabilecek URL 'Leri tanımlamak için yönlendirmeyi kullanabilirsiniz. Örneğin, mevcut bir uygulamadaki ürün kategorilerini görüntüleyen bir sayfanın URL 'SI aşağıdaki örneğe benzeyebilir:

[!code-console[Main](overview/samples/sample36.cmd)]

Yönlendirmeyi kullanarak, uygulamayı aynı bilgileri işlemek için aşağıdaki URL 'YI kabul edecek şekilde yapılandırabilirsiniz:

[!code-console[Main](overview/samples/sample37.cmd)]

Yönlendirme, ASP.NET 3,5 SP1 ile başlayarak kullanılabilir. (ASP.NET 3,5 SP1 'de yönlendirmenin nasıl kullanılacağına ilişkin bir örnek için, Phil Haack 'in blogu 'nda [WebForms Ile yönlendirme kullanma adlı](http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "Bu girdinin başlığı.") girişe bakın.) Ancak, ASP.NET 4, yönlendirmeyi daha kolay hale getirmek için aşağıdakiler dahil bazı özellikler içerir:

- Yolları tanımlarken kullandığınız basit bir HTTP işleyicisi olan *PageRouteHandler* sınıfı. Sınıfı, isteğin yönlendirildiği sayfaya verileri geçirir.
- Yeni Özellikler *HttpRequest. RequestContext* ve *Page. RouteData* ( *HttpRequest. RequestContext. RouteData* nesnesi için bir ara sunucu). Bu özellikler, rotadan geçirilen bilgilere erişmeyi kolaylaştırır.
- *System. Web. Compilation. RouteUrlExpressionBuilder* ve *System. Web. Compilation. RouteValueExpressionBuilder*içinde tanımlanan aşağıdaki yeni ifade oluşturucuları:
- Bir ASP.NET sunucu denetimindeki yol URL 'sine karşılık gelen bir URL oluşturmak için basit bir yol sağlayan *RouteUrl*.
- *Routecontext* nesnesinden bilgi ayıklamaya yönelik basit bir yol sağlayan *RouteValue*.
- Bir *Routecontext* nesnesinde yer alan verileri bir veri kaynağı denetimi sorgusuna ( [*FormParameter*](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)gibi) geçirmeye daha kolay hale getiren *RouteParameter* sınıfı.

#### <a name="routing-for-web-forms-pages"></a>Web Forms sayfaları için yönlendirme

Aşağıdaki örnek, *yol* sınıfının yeni *MapPageRoute* yöntemi kullanılarak bir Web Forms yolunun nasıl tanımlanacağını göstermektedir:

[!code-csharp[Main](overview/samples/sample38.cs)]

ASP.NET 4, *MapPageRoute* metodunu tanıtır. Aşağıdaki örnek, önceki örnekte gösterilen SearchRoute tanımına eşdeğerdir, ancak *PageRouteHandler* sınıfını kullanır.

[!code-csharp[Main](overview/samples/sample39.cs)]

Örnekteki kod, yolu fiziksel bir sayfayla eşler (ilk yolda, `~/search.aspx`için). İlk yol tanımı Ayrıca, SearchTerm adlı parametrenin URL 'den ayıklanıp sayfaya geçirilmeyeceğini belirtir.

*MapPageRoute* yöntemi, aşağıdaki yöntem yüklerini destekler:

- *MapPageRoute (dize routeName, String routeUrl, dize physicalFile, bool checkPhysicalUrlAccess)*
- *MapPageRoute (dize routeName, String routeUrl, dize physicalFile, bool checkPhysicalUrlAccess, Routevaluedıfredefaults)*
- *MapPageRoute (dize routeName, String routeUrl, dize physicalFile, bool checkPhysicalUrlAccess, Routevaluedıfresel varsayılanlar, Routevaluedıfredensel kısıtlamalar)*

*CheckPhysicalUrlAccess* parametresi, yolun yönlendirilmekte olan fiziksel sayfanın güvenlik izinlerini denetleyip denetmeyeceğini belirtir (Bu durumda, Search. aspx) ve gelen URL üzerindeki izinler (Bu durumda arama/{SearchTerm}). *CheckPhysicalUrlAccess* değeri *false*Ise, yalnızca gelen URL 'nin izinleri denetlenir. Bu izinler, `Web.config` dosyasında aşağıdakiler gibi ayarlar kullanılarak tanımlanmıştır:

[!code-xml[Main](overview/samples/sample40.xml)]

Örnek yapılandırmada, yönetici rolünde olmayanlar hariç tüm kullanıcılar için fiziksel sayfa `search.aspx` erişim engellenir. *CheckPhysicalUrlAccess* parametresi *true* olarak ayarlandığında (varsayılan değer olan), fiziksel sayfa arama. aspx Bu roldeki kullanıcılarla kısıtlandığından yalnızca yönetici kullanıcıların/search/{searchterm} url 'sine erişmesine izin verilir. *CheckPhysicalUrlAccess* *yanlış* olarak ayarlanırsa ve site önceki örnekte gösterildiği gibi yapılandırılmışsa, tüm kimliği doğrulanmış kullanıcıların/search/{searchterm}url 'sine erişmesine izin verilir.

#### <a name="reading-routing-information-in-a-web-forms-page"></a>Web Forms sayfasında yönlendirme bilgilerini okuma

Web Forms fiziksel sayfasının kodunda, yönlendirmenin ayıklandığı bilgilere (veya başka bir nesnenin *RouteData* nesnesine eklediği diğer bilgilere) iki yeni özellik kullanarak erişebilirsiniz: *HttpRequest. RequestContext* ve *Page. RouteData*. (*Page. RouteData* , *HttpRequest. RequestContext. RouteData*öğesini sarmalanmış.) Aşağıdaki örnek, *Page. RouteData*'ın nasıl kullanılacağını gösterir.

[!code-csharp[Main](overview/samples/sample41.cs)]

Kod, daha önce örnek rotasında tanımlanan şekilde SearchTerm parametresi için geçirilen değeri ayıklar. Aşağıdaki istek URL 'sini göz önünde bulundurun:

[!code-console[Main](overview/samples/sample42.cmd)]

Bu istek yapıldığında, "Scott" sözcüğü `search.aspx` sayfasında işlenir.

#### <a name="accessing-routing-information-in-markup"></a>Işaretlemede yönlendirme bilgilerine erişme

Önceki bölümde açıklanan yöntemi, Web Forms bir sayfada kodda rota verilerinin nasıl alınacağını gösterir. Ayrıca, biçimlendirmede aynı bilgilere erişim sağlayan ifadeler de kullanabilirsiniz. İfade oluşturucular, bildirim temelli kodla çalışmanın güçlü ve zarif bir yoludur. (Daha fazla bilgi için bkz. PHIL Haack 'in blogu üzerinde [özel Ifade oluşturucuları Ile kendinize giriş hızlı](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx) .)

ASP.NET 4 Web Forms yönlendirme için iki yeni ifade oluşturucular içerir. Aşağıdaki örnek nasıl kullanılacağını göstermektedir.

[!code-aspx[Main](overview/samples/sample43.aspx)]

Örnekte, *RouteUrl* ifadesi bir yönlendirme parametresine dayalı bir URL 'yi tanımlamak için kullanılır. Bu, tam URL 'yi biçimlendirmeye sabit kodlamanızı ve bu bağlantıda herhangi bir değişiklik yapmanıza gerek kalmadan URL yapısını daha sonra değiştirmenize olanak sağlar.

Daha önce tanımlanan yola bağlı olarak, bu biçimlendirme aşağıdaki URL 'YI oluşturur:

[!code-console[Main](overview/samples/sample44.cmd)]

ASP.NET, giriş parametrelerine göre doğru yolu otomatik olarak (yani, doğru URL 'yi oluşturur) verir. Ayrıca, ifadeye bir yol belirtmenize olanak sağlayan bir yol adı ekleyebilirsiniz.

Aşağıdaki örnek, *RouteValue* ifadesinin nasıl kullanılacağını göstermektedir.

[!code-aspx[Main](overview/samples/sample45.aspx)]

Bu denetimi içeren sayfa çalıştığında, etikette "Scott" değeri görüntülenir.

*RouteValue* ifadesi, biçimlendirme verilerini biçimlendirmeyi basit hale getirir ve biçimlendirme sırasında daha karmaşık sayfa. RouteData ["x"] sözdizimiyle çalışmak zorunda kalmaktan kaçınır.

#### <a name="using-route-data-for-data-source-control-parameters"></a>Veri kaynağı denetim parametreleri için rota verilerini kullanma

*RouteParameter* sınıfı, veri kaynağı denetimindeki sorgular için bir parametre değeri olarak rota verileri belirtmenize olanak tanır. Aşağıdaki örnekte gösterildiği gibi, sınıfı [gibi oldukça işe yarar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx) :

[!code-aspx[Main](overview/samples/sample46.aspx)]

Bu durumda, *Select* deyimindeki @companyname parametresi için SearchTerm yol parametresinin değeri kullanılacaktır.

<a id="0.2__Toc224729037"></a><a id="0.2__Toc253429261"></a><a id="0.2__Toc243304635"></a>

### <a name="setting-client-ids"></a>Istemci kimliklerini ayarlama

Yeni *Clienentidmode* özelliği, ASP.NET içinde uzun süreli bir sorunu ele alarak denetimlerin, oluşturdukları öğeler için *ID* özniteliği nasıl oluşturtığına sahiptir. Uygulamanız bu öğelere başvuran istemci betiği içeriyorsa, işlenen öğelerin *ID* özniteliğinin bilinmesi önemlidir.

Web sunucusu denetimleri için işlenen HTML içindeki *ID* özniteliği, denetimin *ClientID* özelliğine göre oluşturulur. ASP.NET 4 ' e kadar, *ClientID* özelliğinden *ID* ÖZNITELIĞI oluşturma algoritması, kimliğe sahip (varsa) adlandırma kapsayıcısını ve yinelenen denetimler söz konusu olduğunda (veri denetimlerinde olduğu gibi) bir ön ek ve sıralı sayı eklemek için. Bu, sayfadaki denetimlerin kimliklerinin benzersiz olduğunu garanti ederken, algoritma tahmin edilemez olan denetim kimliklerini sonuçlanmış ve bu nedenle istemci betiğine başvurulmaya zordu.

Yeni *Clienentidmode* özelliği, istemci kimliğinin denetimler için nasıl oluşturulduğunu daha kesin olarak belirtmenizi sağlar. Sayfa için de dahil olmak üzere herhangi bir denetim için *Clienentidmode* özelliğini ayarlayabilirsiniz. Olası ayarlar şunlardır:

- *AutoID* : Bu, önceki ASP.net sürümlerinde kullanılan *ClientID* özellik değerlerini oluşturmaya yönelik algoritmaya eşdeğerdir.
- *Static* – bu, *ClientID* değerinin, üst ADLANDıRMA kapsayıcıları kimliklerini birleştirirken kimlik ile aynı olacağını belirtir. Bu, Web kullanıcı denetimlerinde yararlı olabilir. Web Kullanıcı denetimi farklı sayfalarda ve farklı kapsayıcı denetimlerinde konumlandırabileceğinden, KIMLIK değerlerinin ne olacağı tahmin edemeyeceği için, *oto kimliği* algoritmasını kullanan denetimler için istemci betiği yazmak zor olabilir.
- *Öngörülebilir* – Bu seçenek öncelikle yinelenen şablonlar kullanan veri denetimlerinde kullanım içindir. Denetimin adlandırma kapsayıcılarının ID özelliklerini birleştirir, ancak oluşturulan *ClientID* değerleri "ctlxxx" gibi dizeler içermez. Bu ayar, denetimin *Clienentidrowsuffix* özelliği ile birlikte kullanılır. *Clienentidrowsuffix* özelliğini bir veri alanı adına ayarlarsınız ve bu alanın değeri oluşturulan *ClientID* değeri için sonek olarak kullanılır. Genellikle, bir veri kaydının birincil anahtarını *Clienentidrowsuffix* değeri olarak kullanacaksınız.
- *Devralma* – Bu ayar denetimler için varsayılan davranıştır; bir denetimin KIMLIK üretimi üst öğesiyle aynı olduğunu belirtir.

*Clienentidmode* özelliğini sayfa düzeyinde ayarlayabilirsiniz. Bu, geçerli sayfadaki tüm denetimler için varsayılan *Clienentidmode* değerini tanımlar.

Sayfa düzeyindeki varsayılan *Clienentidmode* değeri, *oto kimliğidir*ve denetim düzeyindeki varsayılan *Clienentidmode* değeri *devralınır*. Sonuç olarak, bu özelliği kodunuzda herhangi bir yere ayarlamayın, tüm denetimler varsayılan olarak *oto kimliği* algoritmasıdır.

Aşağıdaki örnekte gösterildiği gibi, *@ Page* yönergesinde sayfa düzeyi değerini ayarlarsınız:

[!code-aspx[Main](overview/samples/sample47.aspx)]

Yapılandırma dosyasında, bilgisayar (makine) düzeyinde veya uygulama düzeyinde *Clienentidmode* değerini de ayarlayabilirsiniz. Bu, uygulamadaki tüm sayfalardaki tüm denetimler için varsayılan *Clienentidmode* ayarını tanımlar. Değeri bilgisayar düzeyinde ayarlarsanız, bu bilgisayardaki tüm Web siteleri için varsayılan *Clienentidmode* ayarını tanımlar. Aşağıdaki örnek yapılandırma dosyasında *Clienentidmode* ayarını göstermektedir:

[!code-xml[Main](overview/samples/sample48.xml)]

Daha önce belirtildiği gibi, *ClientID* özelliğinin değeri bir denetimin üst öğesi için adlandırma kapsayıcısından türetilir. Ana sayfaları kullanırken olduğu gibi bazı senaryolarda, denetimler aşağıdaki işlenmiş HTML 'de olduğu gibi kimlikler ile bitebilirler:

[!code-html[Main](overview/samples/sample49.html)]

İşaretlemede gösterilen *giriş* öğesi (bir *TextBox* denetiminden) sayfada yalnızca iki adlandırma kapsayıcısı olsa da (iç içe yerleştirilmiş *ContentPlaceholder* denetimleri), ana sayfaların işlendiği şekilde, son sonuç aşağıdaki gibi bir denetim kimliğidir:

[!code-console[Main](overview/samples/sample50.cmd)]

Bu KIMLIğIN sayfada benzersiz olması garantilenir, ancak çoğu amaçla gereksiz bir süredir. İşlenmiş KIMLIğIN uzunluğunu azaltmak istediğinizi ve KIMLIğIN oluşturulma şekli üzerinde daha fazla denetime sahip olduğunu düşünün. (Örneğin, "ctlxxx" öneklerini ortadan kaldırmak istiyorsunuz.) Bunu başarmanın en kolay yolu, aşağıdaki örnekte gösterildiği gibi *Clienentidmode* özelliğini ayarlamadır:

[!code-aspx[Main](overview/samples/sample51.aspx)]

Bu örnekte, *Clienentidmode* özelliği, en dıştaki *Namingpanel* öğesi için *static* olarak ayarlanır ve Inner *namingcontrol* öğesi için *tahmin edilebilir* olarak ayarlanır. Bu ayarlar, aşağıdaki biçimlendirmeye neden olur (sayfanın geri kalanı ve ana sayfanın önceki örnekteki gibi olduğu varsayılır):

[!code-html[Main](overview/samples/sample52.html)]

*Statik* ayar, en dıştaki *namingpanel* öğesi içindeki denetimlerin adlandırma hiyerarşisini SıFıRLAMANıN ve oluşturulan kimliğin *ContentPlaceHolder* ve *MasterPage* kimliklerini ortadan kaldıran etkiye sahiptir. (İşlenen öğelerin *ad* özniteliği etkilenmemiştir, bu nedenle normal ASP.NET işlevselliği olaylar için korunur, durumu görüntüle vb.) Adlandırma hiyerarşisinin sıfırlanmasının yan etkisi, *Namingpanel* öğelerinin işaretlemesini farklı bir *ContentPlaceholder* denetimine taşısanız bile, işlenen istemci kimlikleri aynı kalır.

> [!NOTE]
> Bu, işlenen Denetim kimliklerinin benzersiz olduğundan emin olmak için size dikkat edin. Aksi takdirde, istemci *belgesi. getElementById* işlevi gıbı ayrı HTML öğeleri Için benzersiz kimlikler gerektiren tüm işlevleri bozabilir.

#### <a name="creating-predictable-client-ids-in-data-bound-controls"></a>Veri bağlantılı denetimlerde öngörülebilir Istemci kimlikleri oluşturma

Eski algoritmaya göre veri bağlantılı liste denetimindeki denetimler için oluşturulan *ClientID* değerleri uzun olabilir ve gerçekten tahmin edilebilir değildir. *Clienentidmode* işlevselliği, bu kimliklerin nasıl oluşturulduğu konusunda daha fazla denetime sahip olmanıza yardımcı olabilir.

Aşağıdaki örnekteki biçimlendirme bir *ListView* denetimi içerir:

[!code-aspx[Main](overview/samples/sample53.aspx)]

Önceki örnekte, *Clienentidmode* ve *Rowclientidrowsuffix* özellikleri biçimlendirme olarak ayarlanır. *Clienentidrowsuffix* özelliği yalnızca veriye bağlı denetimlerde kullanılabilir ve davranışı kullandığınız denetime göre farklılık gösterir. Farklar şunlardır:

- *GridView* denetimi — veri kaynağındaki bir veya daha fazla sütunun adını belirtebilir ve bu, istemci kimliklerini oluşturmak için çalışma zamanında birleştirilir. Örneğin, *Rowclientidrowsonekini* "ProductName, ProductID" olarak ayarlarsanız, işlenen öğelerin Denetim kimlikleri aşağıdaki gibi bir biçime sahip olur:

- [!code-console[Main](overview/samples/sample54.cmd)]

- *ListView* denetimi — veri KAYNAĞıNDA istemci kimliğine eklenen tek bir sütun belirtebilirsiniz. Örneğin, *Clienentidrowsuffix* öğesini "ProductName" olarak ayarlarsanız, Işlenen Denetim kimlikleri aşağıdaki gibi bir biçime sahip olur:

- [!code-console[Main](overview/samples/sample55.cmd)]

- Bu durumda, sondaki 1 geçerli veri öğesinin ürün KIMLIĞINDEN türetilir.

- *Yineleyici* denetimi — bu denetim *Clienentidrowsuffix* özelliğini desteklemez. *Yineleyici* denetiminde, geçerli satırın dizini kullanılır. Bir *Yineleyici* denetimiyle Clienentidmode = "öngörülebilir" kullandığınızda, istemci kimlikleri aşağıdaki biçimde oluşturulur:

- [!code-console[Main](overview/samples/sample56.cmd)]

- Sondaki 0 geçerli satırın dizinidir.

*FormView* ve *DetailsView* denetimleri birden çok satır göstermez, bu nedenle *clienentidrowsuffix* özelliğini desteklemezler.

<a id="0.2__Toc224729038"></a><a id="0.2__Toc253429262"></a><a id="0.2__Toc243304636"></a>

### <a name="persisting-row-selection-in-data-controls"></a>Veri denetimlerinde kalıcı satır seçimi

*GridView* ve *ListView* denetimleri kullanıcıların bir satır seçmesini sağlayabilir. Önceki ASP.NET sürümlerinde seçim, sayfadaki satır dizinini temel alır. Örneğin, sayfa 1 ' de üçüncü öğeyi seçip Sayfa 2 ' ye taşırsanız, bu sayfadaki üçüncü öğe seçilir.

Kalıcı seçim başlangıçta yalnızca .NET Framework 3,5 SP1 'deki dinamik veri projelerinde desteklendi. Bu özellik etkinleştirildiğinde, seçilen geçerli öğe, öğenin veri anahtarını temel alır. Bu, sayfa 1 ' de üçüncü satırı seçip Sayfa 2 ' ye taşıdığınızda, sayfa 2 ' de hiçbir şey seçilmediği anlamına gelir. Sayfa 1 ' e geri döndüğünüzde, üçüncü satır hala seçilidir. Kalıcı seçim artık, aşağıdaki örnekte gösterildiği gibi, *EnablePersistedSelection* özelliğini kullanarak tüm projelerdeki *GridView* ve *ListView* denetimleri için desteklenir:

[!code-aspx[Main](overview/samples/sample57.aspx)]

<a id="0.2__Toc253429263"></a><a id="0.2__Toc243304637"></a>

### <a name="aspnet-chart-control"></a>ASP.NET grafik denetimi

ASP.NET *grafik* denetimi .NET Framework veri görselleştirme tekliflerini genişletir. *Grafik* denetimini kullanarak, karmaşık istatistiksel veya finansal analizler için sezgisel ve görsel açıdan etkileyici grafikler içeren ASP.NET sayfaları oluşturabilirsiniz. ASP.NET *grafik* denetimi, .NET Framework sürüm 3,5 SP1 sürümüne bir eklenti olarak sunulmuştur ve .NET Framework 4 sürümünün bir parçası.

Denetim aşağıdaki özellikleri içerir:

- 35 ayrı grafik türü.
- Sınırsız sayıda grafik alanı, başlık, açıklama ve ek açıklama.
- Tüm grafik öğeleri için çok çeşitli görünüm ayarları.
- Çoğu grafik türü için 3-b destek.
- Veri noktalarına otomatik olarak uyaabilecek akıllı veri etiketleri.
- Şerit çizgileri, ölçek sonları ve Logaritmik ölçekleme.
- Veri çözümleme ve dönüştürme için 50 ' den fazla finansal ve istatistiksel formül.
- Grafik verilerini basit bağlama ve düzenleme.
- Tarih, saat ve para birimi gibi ortak veri biçimleri için destek.
- İstemci tıklama olayları için AJAX kullanarak etkileşimli ve olay odaklı özelleştirme desteği.
- Durum yönetimi.
- İkili akış.

Aşağıdaki rakamlar, ASP.NET grafik denetimi tarafından üretilen finansal grafiklerin örneklerini göstermektedir.

<a id="0.2_graphic17"></a>![](overview/_static/image1.png)

Şekil 2: ASP.NET grafik denetimi örnekleri

ASP.NET grafik denetimini kullanma hakkında daha fazla örnek için, MSDN Web sitesindeki [Microsoft Grafik denetimleri Için örnekler ortamında](https://go.microsoft.com/fwlink/?LinkId=128300) örnek kodu indirin. [Grafik denetimi forumundan](https://go.microsoft.com/fwlink/?LinkId=128713)topluluk içeriğine daha fazla örnek bulabilirsiniz.

#### <a name="adding-the-chart-control-to-an-aspnet-page"></a>Grafik denetimini bir ASP.NET sayfasına ekleme

Aşağıdaki örnek, biçimlendirme kullanarak bir ASP.NET sayfasına nasıl *grafik* denetimi ekleneceğini gösterir. Örnekte, *grafik* denetimi statik veri noktaları için bir sütun grafik oluşturur.

[!code-aspx[Main](overview/samples/sample58.aspx)]

#### <a name="using-3-d-charts"></a>3-b grafikleri kullanma

*Grafik* denetimi, grafik alanlarının özelliklerini tanımlayan *ChartArea* nesneleri Içerebilen bir *ChartArea* koleksiyonu içerir. Örneğin, bir grafik alanı için 3-b kullanmak için, *Area3DStyle* özelliğini aşağıdaki örnekte olduğu gibi kullanın:

[!code-aspx[Main](overview/samples/sample59.aspx)]

Aşağıdaki şekilde, *çubuk* grafik türünde dört serisi olan 3-b grafik gösterilmektedir.

<a id="0.2_graphic18"></a>![](overview/_static/image2.png)

Şekil 3:3-D çubuk grafik

#### <a name="using-scale-breaks-and-logarithmic-scales"></a>Ölçek sonlarını ve Logaritmik ölçeği kullanma

Ölçek sonları ve Logaritmik ölçekler, grafiğe gelişmiş algoritmaların mümkündür eklemenin iki farklı yolu vardır. Bu özellikler bir grafik alanındaki her eksene özeldir. Örneğin, bu özellikleri bir grafik alanının birincil Y ekseninde kullanmak için, *ChartArea* nesnesindeki *Axyönünde. ıslogaritmik* ve *ScaleBreakStyle* özelliklerini kullanın. Aşağıdaki kod parçacığında, birincil Y ekseninde ölçek sonlarının nasıl kullanılacağı gösterilmektedir.

[!code-aspx[Main](overview/samples/sample60.aspx)]

Aşağıdaki şekilde ölçek sonlarının etkinleştirildiği Y ekseni gösterilmektedir.

<a id="0.2_graphic19"></a>![](overview/_static/image3.png)

Şekil 4: ölçek sonları

<a id="0.2__QueryExtender"></a><a id="0.2__Toc224729041"></a><a id="0.2__Toc253429264"></a><a id="0.2__Toc243304638"></a>

### <a name="filtering-data-with-the-queryextender-control"></a>Querygenişletici denetimiyle verileri filtreleme

Veri tabanlı Web sayfaları oluşturan geliştiriciler için çok yaygın bir görev, verileri filtremaktır. Bu, geleneksel olarak veri kaynağı denetimlerinde *WHERE* yan tümceleri oluşturarak gerçekleştirildi. Bu yaklaşım karmaşık olabilir ve bazı *durumlarda söz konusu sözdizimi, temel* alınan veritabanının tüm işlevselliğinden yararlanabilmenizi sağlar.

Filtrelemenin daha kolay olması için, ASP.NET 4 ' e yeni bir *Querygenişletici* denetimi eklenmiştir. Bu denetim, bu denetimlerin döndürdüğü verileri filtrelemek için *EntityDataSource* veya *LinqDataSource* denetimlerine eklenebilir. *Querygenişletici* denetimi LINQ 'ı kullandığından, veriler sayfaya gönderilmeden önce filtre veritabanı sunucusuna uygulanır, bu da çok verimli işlemlere neden olur.

*Querygenişletici* denetimi, çeşitli filtre seçeneklerini destekler. Aşağıdaki bölümlerde bu seçenekler açıklanır ve bunların nasıl kullanılacağına ilişkin örnekler sağlanır.

#### <a name="search"></a>Ara

Arama seçeneği için, *Querygenişletici* denetimi belirtilen alanlarda bir arama gerçekleştirir. Aşağıdaki örnekte, denetim, TextBoxSearch denetimine girilen metni kullanır ve `ProductName` ve *LinqDataSource* denetiminden döndürülen verilerdeki `Supplier.CompanyName` sütunlarında içeriğini arar.

[!code-aspx[Main](overview/samples/sample61.aspx)]

#### <a name="range"></a>Aralık

Aralık seçeneği arama seçeneğine benzerdir, ancak aralığı tanımlamak için bir çift değer belirtir. Aşağıdaki örnekte, *Querygenişletici* denetimi, *LinqDataSource* denetiminden döndürülen verilerdeki `UnitPrice` sütununu arar. Aralık, sayfadaki TextBoxFrom ve TextBoxTo denetimlerinden okunmalıdır.

[!code-aspx[Main](overview/samples/sample62.aspx)]

#### <a name="propertyexpression"></a>PropertyExpression koleksiyonda

Özellik ifadesi seçeneği, bir özellik değeriyle karşılaştırma tanımlamanıza olanak sağlar. İfade *true*olarak değerlendirilirse, incelenmekte olan veriler döndürülür. Aşağıdaki örnekte, *Querygenişletici* denetimi verileri `Discontinued` sütunundaki verileri, sayfadaki checkboxdiscontinued denetimindeki değerle karşılaştırarak filtreler.

[!code-aspx[Main](overview/samples/sample63.aspx)]

#### <a name="customexpression"></a>CustomExpression

Son olarak, *Querygenişletici* denetimiyle kullanmak için özel bir ifade belirtebilirsiniz. Bu seçenek, sayfada özel filtre mantığını tanımlayan bir işlevi çağırmanızı sağlar. Aşağıdaki örnek, *Querygenişletici* denetiminde özel bir ifadenin bildirimli olarak nasıl belirtilme şeklini gösterir.

[!code-aspx[Main](overview/samples/sample64.aspx)]

Aşağıdaki örnek, *Querygenişletici* denetimi tarafından çağrılan özel işlevi gösterir. Bu durumda, *WHERE* yan tümcesini içeren bir veritabanı sorgusu kullanmak yerine, kod verileri filtrelemek IÇIN bir LINQ sorgusu kullanır.

[!code-csharp[Main](overview/samples/sample65.cs)]

Bu örnekler, tek seferde *Querygenişletici* denetiminde kullanılan yalnızca bir ifadeyi gösterir. Ancak, *Querygenişletici* denetiminin içine birden çok ifade ekleyebilirsiniz.

<a id="0.2__Toc253429265"></a><a id="0.2__Toc243304639"></a>

### <a name="html-encoded-code-expressions"></a>HTML kodlu kod Ifadeleri

Bazı ASP.NET siteleri (özellikle ASP.NET MVC ile), yanıta bazı metinler yazmak için `<%`= `expression %>` söz dizimini (genellikle "Code nugal" olarak adlandırılır) kullanır. Kod ifadelerini kullandığınızda, metnin HTML kodlanması kolaydır, metin Kullanıcı girişinden geliyorsa sayfaları XSS (siteler arası komut dosyası oluşturma) saldırısına açık bırakabilir.

ASP.NET 4, kod ifadeleri için aşağıdaki yeni sözdizimini tanıtır:

[!code-aspx[Main](overview/samples/sample66.aspx)]

Bu sözdizimi, yanıta yazarken varsayılan olarak HTML kodlaması kullanır. Bu yeni ifade etkin bir şekilde aşağıdaki gibi çeviri yapar:

[!code-aspx[Main](overview/samples/sample67.aspx)]

Örneğin,% &lt;: Request ["Userınput"]%&gt; *["userınput"] isteğinin*değerinde HTML kodlaması gerçekleştiriyor.

Bu özelliğin amacı, bir bütün olarak kullanılacak olan her adıma karar vermeye zorlanmadan, eski sözdiziminin tüm örneklerinin yeni sözdizimiyle değiştirilmesini olanaklı hale getirir. Ancak, çıktının bulunduğu metnin HTML olması veya zaten kodlandığı durumlar vardır; bu durumda, bu, Çift kodlamaya neden olabilir.

Bu gibi durumlarda, ASP.NET 4 yeni bir arabirim, *IHtmlString*ve somut bir uygulamayla birlikte *HtmlString*'i tanıtır. Bu türlerin örnekleri, dönüş değerinin HTML olarak görüntülenmek üzere zaten doğru şekilde kodlandığını (veya başka bir şekilde inceledi) belirtebilmesine ve bu nedenle değerin HTML kodlu bir kez yeniden kodlanmamalıdır. Örneğin, aşağıdakiler (ve değil) HTML kodlamalı olmalıdır:

[!code-aspx[Main](overview/samples/sample68.aspx)]

ASP.NET MVC 2 yardımcı yöntemleri, bu yeni söz dizimi ile çalışacak şekilde güncelleştirilerek, ancak yalnızca ASP.NET 4 ' i çalıştırıyorsanız, Double olarak kodlanmamalıdır. Bu yeni sözdizimi, ASP.NET 3,5 SP1 kullanarak bir uygulamayı çalıştırdığınızda çalışmaz.

Bunun, XSS saldırılarına karşı koruma garantisi vermediğini unutmayın. Örneğin, tırnak işaretleri içinde olmayan öznitelik değerlerini kullanan HTML, hala açıktır olan kullanıcı girişini içerebilir. ASP.NET denetimlerinin ve ASP.NET MVC yardımcılarının çıktısının her zaman, önerilen yaklaşım olan tırnak işaretleri içinde öznitelik değerleri içerdiğini unutmayın.

Benzer şekilde, bu sözdizimi, kullanıcı girişine dayalı bir JavaScript dizesi oluştururken olduğu gibi JavaScript kodlaması gerçekleştirmez.

<a id="0.2__Toc253429266"></a><a id="0.2__Toc243304640"></a>

### <a name="project-template-changes"></a>Proje şablonu değişiklikleri

Önceki ASP.NET sürümlerinde, Visual Studio 'Yu kullanarak yeni bir Web sitesi projesi veya Web uygulaması projesi oluşturduğunuzda, sonuçta elde edilen projeler yalnızca varsayılan bir. aspx sayfası, varsayılan bir `Web.config` dosyası ve `App_Data` klasörünü aşağıdaki çizimde gösterildiği gibi içerir:

<a id="0.2_graphic1A"></a>![](overview/_static/image4.png)

Visual Studio, aşağıdaki şekilde gösterildiği gibi, hiçbir dosya içermeyen boş bir Web sitesi proje türünü de destekler:

<a id="0.2_graphic1B"></a>![](overview/_static/image5.png)

Sonuç, başlangıç için bir üretim Web uygulaması oluşturma konusunda çok az kılavuzluk sağlar. Bu nedenle, ASP.NET 4, biri boş bir Web uygulaması projesi ve bir Web uygulaması ve Web sitesi projesi için olmak üzere üç yeni şablon tanıtır.

#### <a name="empty-web-application-template"></a>Boş Web uygulaması şablonu

Adından da anlaşılacağı gibi, boş Web uygulaması şablonu bir aşağı açılan Web uygulaması projem olur. Aşağıdaki şekilde gösterildiği gibi, Visual Studio yeni proje iletişim kutusundan bu proje şablonunu seçersiniz:

[![](overview/_static/image7.png)](overview/_static/image6.png)

([Tam boyutlu görüntüyü görüntülemek Için tıklayın](overview/_static/image8.png))

Boş bir ASP.NET Web uygulaması oluşturduğunuzda, Visual Studio aşağıdaki klasör mizanpajını oluşturur:

<a id="0.2_graphic1D"></a>![](overview/_static/image9.png)

Bu, ASP.NET 'in önceki sürümlerindeki boş Web sitesi düzenine benzer ve tek bir özel durumla benzerdir. Visual Studio 2010 ' de boş Web uygulaması ve boş Web sitesi projeleri, Visual Studio tarafından projenin hedeflediği çerçeveyi belirlemek için kullanılan bilgileri içeren aşağıdaki en küçük `Web.config` dosya içerir:

<a id="0.2_graphic1E"></a>![](overview/_static/image10.png)

Bu *TargetFramework* özelliği olmadan, Visual Studio, eski uygulamaları açarken uyumluluğu korumak için .NET Framework 2,0 ' i hedefleyecek şekilde varsayılan değer.

#### <a name="web-application-and-web-site-project-templates"></a>Web uygulaması ve Web sitesi proje şablonları

Visual Studio 2010 ile birlikte gelen diğer iki yeni proje şablonu büyük değişiklikler içerir. Aşağıdaki şekilde, yeni bir Web uygulaması projesi oluşturduğunuzda oluşturulan proje düzeni gösterilmektedir. (Bir Web sitesi projesinin düzeni neredeyse aynıdır.)

- <a id="0.2_graphic1F"></a>![](overview/_static/image11.png)

Proje, önceki sürümlerde oluşturulmamış bir dizi dosya içerir. Ayrıca, yeni Web uygulaması projesi temel üyelik işlevselliğiyle yapılandırılır, bu da yeni uygulamaya erişimi güvenli hale getirmenin hızlı bir şekilde başlamanızı sağlar. Bu içerme nedeniyle, yeni proje için `Web.config` dosyası üyelik, roller ve profilleri yapılandırmak için kullanılan girdileri içerir. Aşağıdaki örnek, yeni bir Web uygulaması projesi için `Web.config` dosyasını gösterir. (Bu durumda, *roleManager* devre dışıdır.)

[![](overview/_static/image13.png)](overview/_static/image12.png)

([Tam boyutlu görüntüyü görüntülemek Için tıklayın](overview/_static/image14.png))

Proje, `Account` dizininde ikinci bir `Web.config` dosyası da içerir. İkinci yapılandırma dosyası, oturum açmamış kullanıcılar için ChangePassword. aspx sayfasına erişimin güvenliğini sağlamak için bir yol sağlar. Aşağıdaki örnek, ikinci `Web.config` dosyanın içeriğini gösterir.

![](overview/_static/image15.png)

Yeni proje şablonlarında varsayılan olarak oluşturulan sayfalar, önceki sürümlerden daha fazla içerik de içerir. Proje varsayılan bir ana sayfa ve CSS dosyası içerir ve varsayılan sayfa (default. aspx) varsayılan olarak ana sayfayı kullanacak şekilde yapılandırılmıştır. Sonuç olarak, Web uygulamasını veya Web sitesini ilk kez çalıştırdığınızda varsayılan (giriş) sayfası zaten çalışır durumdadır. Aslında, yeni bir MVC uygulaması başlattığınızda gördüğünüz varsayılan sayfaya benzer.

[![](overview/_static/image17.png)](overview/_static/image16.png)

([Tam boyutlu görüntüyü görüntülemek Için tıklayın](overview/_static/image18.png))

Proje şablonlarındaki bu değişikliklerin amacı, yeni bir Web uygulaması oluşturmaya nasıl başlayabileceğine ilişkin rehberlik sağlamaktır. Anlamsal olarak doğru, katı XHTML 1,0 uyumlu biçimlendirme ve CSS kullanılarak belirtilen düzen ile, şablonlardaki sayfalar ASP.NET 4 Web uygulamaları oluşturmak için en iyi yöntemleri temsil eder. Varsayılan sayfaların de kolayca özelleştirebileceğiniz iki sütunlu bir düzeni vardır.

Örneğin, yeni bir Web uygulaması için bazı renklerden bazılarını değiştirmek istediğinizi ve şirket logonuzu My ASP.NET Application logosunun yerine yerleştirmenizi düşünün. Bunu yapmak için logo görüntünüzü depolamak üzere `Content` altında yeni bir dizin oluşturursunuz:

<a id="0.2_graphic23"></a>![](overview/_static/image19.png)

Görüntüyü sayfaya eklemek için `Site.Master` dosyasını açın, ASP.NET uygulama metnimin nerede tanımlandığını bulur ve bunu aşağıdaki örnekte olduğu gibi *src* özniteliği yeni logo resmine ayarlanmış bir *görüntü* öğesiyle değiştirirsiniz:

[![](overview/_static/image21.png)](overview/_static/image20.png)

([Tam boyutlu görüntüyü görüntülemek Için tıklayın](overview/_static/image22.png))

Daha sonra, sayfanın arka plan rengini ve üst bilgisinin yanı sıra, site. css dosyasına gidebilir ve CSS sınıf tanımlarını değiştirebilirsiniz.

Bu değişikliklerin sonucunda, çok az çabayla özelleştirilmiş bir giriş sayfası görüntüleyebilirsiniz:

[![](overview/_static/image24.png)](overview/_static/image23.png)

([Tam boyutlu görüntüyü görüntülemek Için tıklayın](overview/_static/image25.png))

<a id="0.2__Toc253429267"></a><a id="0.2__Toc243304641"></a>

### <a name="css-improvements"></a>CSS geliştirmeleri

ASP.NET 4 ' te çalışmanın ana alanlarından biri, en son HTML standartlarıyla uyumlu HTML 'i işlemeye yardımcı olmak için tasarlanmıştır. Bu, ASP.NET Web sunucusu denetimlerinin CSS stillerini nasıl kullandığını gösteren değişiklikleri içerir.

#### <a name="compatibility-setting-for-rendering"></a>Işleme için uyumluluk ayarı

Varsayılan olarak, bir Web uygulaması veya Web sitesi .NET Framework 4 ' ü hedefliyorsa, *Pages* öğesinin *controlRenderingCompatibilityVersion* özniteliği "4,0" olarak ayarlanır. Bu öğe makine düzeyinde `Web.config` dosyasında tanımlanmıştır ve varsayılan olarak tüm ASP.NET 4 uygulamalarına uygulanır:

[!code-xml[Main](overview/samples/sample69.xml)]

*Controlrenderingcompatibility* değeri, gelecek sürümlerde olası yeni sürüm tanımlarına izin veren bir dizedir. Geçerli sürümde, bu özellik için aşağıdaki değerler desteklenir:

- "3,5". Bu ayar, eski işleme ve işaretlemeyi gösterir. Denetimler tarafından işlenen biçimlendirme %100 geriye dönük olarak uyumludur ve *Xhtmluyum* özelliğinin ayarı kabul edilir.
- "4,0". Özelliğin bu ayarı varsa, ASP.NET Web sunucusu denetimleri şunları yapın:
- *Xhtmluygunluğu* özelliği her zaman "katı" olarak değerlendirilir. Sonuç olarak, denetim XHTML 1,0 katı biçimlendirmeyi işler.
- Giriş olmayan denetimleri devre dışı bırakmak artık geçersiz stilleri oluşturmayacağını.
- gizli alanlar etrafındaki *div* öğeleri, Kullanıcı tarafından oluşturulan CSS kurallarıyla karışabilmeleri için artık stilleniyor.
- Menü, anlam açısından doğru ve erişilebilirlik kılavuzlarından uyumlu olan işleme işaretlemesini denetler.
- Doğrulama denetimleri satır içi stilleri işlemez.
- Önceden işlenmiş Border = "0" (ASP.NET *Table* denetiminden türetilen denetimler ve ASP.net *Image* Control) artık bu özniteliği işlemez.

#### <a name="disabling-controls"></a>Denetimleri devre dışı bırakma

ASP.NET 3,5 SP1 ve önceki sürümlerinde Framework, *Enabled* özelliği *false*olarak ayarlanan HERHANGI bir denetim için HTML biçimlendirmesinde *devre dışı bırakılmış* özniteliği işler. Ancak, HTML 4,01 belirtimine göre yalnızca *giriş* öğelerinde bu öznitelik olmalıdır.

ASP.NET 4 ' te, aşağıdaki örnekte olduğu gibi *controlRenderingCompatibilityVersion* özelliğini "3,5" olarak ayarlayabilirsiniz:

[!code-xml[Main](overview/samples/sample70.xml)]

Aşağıdaki gibi bir *etiket* denetimi için biçimlendirme oluşturabilirsiniz, bu da denetimi devre dışı bırakır:

[!code-aspx[Main](overview/samples/sample71.aspx)]

*Etiket* denetımı aşağıdaki HTML 'yi işleyebilir:

[!code-html[Main](overview/samples/sample72.html)]

ASP.NET 4 ' te *controlRenderingCompatibilityVersion* 'ı "4,0" olarak ayarlayabilirsiniz. Bu durumda, denetimin *etkin* özelliği *false*olarak ayarlandığında yalnızca işlem *girişi* öğelerini işleyen denetim *devre dışı bırakılmış* bir özniteliği işleyecek olur. Bunun yerine HTML *giriş* öğelerini işlemeyin denetimler, denetim için devre dışı bırakılmış bir görünüm tanımlamak için KULLANABILECEĞINIZ bir CSS sınıfına başvuran bir *sınıf* özniteliği işler. Örneğin, önceki örnekte gösterilen *etiket* denetimi aşağıdaki biçimlendirmeyi oluşturur:

[!code-html[Main](overview/samples/sample73.html)]

Bu denetim için belirtilen sınıfın varsayılan değeri "aspNetDisabled" dır. Ancak, *WebControl* sınıfının statik *DisabledCssClass* static özelliğini ayarlayarak bu varsayılan değeri değiştirebilirsiniz. Denetim geliştiricileri için, belirli bir denetim için kullanılacak davranış, *SupportsDisabledAttribute* özelliği kullanılarak da tanımlanabilir.

<a id="0.2__Toc253429268"></a><a id="0.2__Toc243304642"></a>

### <a name="hiding-div-elements-around-hidden-fields"></a>Gizli alanlar etrafında div öğelerini gizleme

ASP.NET 2,0 ve sonraki sürümler, XHTML standardına uymak için, sistem 'e özgü gizli alanları (görünüm durumu bilgilerini depolamak için kullanılan *gizli* öğe gibi) *div* öğesinin içinde işler. Ancak, bir CSS kuralı sayfadaki *DIV* öğelerini etkiliyorsa, bu soruna neden olabilir. Örneğin, gizli *div* öğelerinin etrafındaki sayfada tek piksellik bir çizgi görünmesine neden olabilir. ASP.NET 4 ' te, ASP.NET tarafından oluşturulan gizli alanları kapsayan *div* öğeleri aşağıdaki örnekte gösterildiği gıbı bir CSS sınıfı başvurusu ekleyin:

[!code-html[Main](overview/samples/sample74.html)]

Ardından, aşağıdaki örnekte olduğu gibi, yalnızca ASP.NET tarafından oluşturulan *gizli* öğeler için geçerli olan bir CSS sınıfı tanımlayabilirsiniz:

[!code-css[Main](overview/samples/sample75.css)]

<a id="0.2__Toc253429269"></a><a id="0.2__Toc243304643"></a>

### <a name="rendering-an-outer-table-for-templated-controls"></a>Şablonlu denetimler için bir dış tablo işleme

Varsayılan olarak, aşağıdaki ASP.NET Web sunucusu, destek şablonlarının satır içi stilleri uygulamak için kullanılan bir dış tabloya otomatik olarak sarılacağını denetler:

- *FormView*
- *LOGIN*
- *PasswordRecovery*
- *Parola*
- *Ekleme*
- *CreateUserWizard*

Bu denetimlere, *RenderOuterTable* adlı yeni bir özellik eklenmiş ve dış tablonun biçimlendirmeden kaldırılmasına izin veren. Örneğin, bir *FormView* denetiminin aşağıdaki örneğini göz önünde bulundurun:

[!code-aspx[Main](overview/samples/sample76.aspx)]

Bu biçimlendirme, bir HTML tablosu içeren sayfada aşağıdaki çıktıyı işler:

[!code-html[Main](overview/samples/sample77.html)]

Tablonun işlenmesini engellemek için, aşağıdaki örnekte olduğu gibi *FormView* denetiminin *RenderOuterTable* özelliğini ayarlayabilirsiniz:

[!code-aspx[Main](overview/samples/sample78.aspx)]

Önceki örnek *Table*, *tr*ve *TD* öğeleri olmadan aşağıdaki çıktıyı oluşturur:

> İçerik

Bu geliştirme, denetim tarafından beklenmeyen Etiketler işlenmediğinden, denetimin içeriğini CSS ile stilleyerek daha kolay hale getirebilirsiniz.

> [!NOTE]
> Bu değişiklik, otomatik biçim seçeneği tarafından oluşturulan stil özniteliklerini barındırabildiğinden artık *tablo* öğesi olmadığından, Visual Studio 2010 tasarımcısında otomatik biçim işlevine yönelik desteği devre dışı bırakır.

<a id="0.2__Toc253429270"></a><a id="0.2__Toc243304644"></a>

### <a name="listview-control-enhancements"></a>ListView denetimi geliştirmeleri

*ListView* denetimi, ASP.NET 4 ' te kullanımı daha kolay yapılmıştır. Denetimin önceki sürümü, bilinen bir KIMLIĞE sahip sunucu denetimi içeren bir düzen şablonu belirtmenizi gerektirir. Aşağıdaki biçimlendirmede, ASP.NET 3,5 ' de *ListView* denetiminin nasıl kullanılacağına ilişkin tipik bir örnek gösterilmektedir.

[!code-aspx[Main](overview/samples/sample79.aspx)]

ASP.NET 4 ' te, *ListView* denetimi bir düzen şablonu gerektirmez. Önceki örnekte gösterilen biçimlendirme aşağıdaki biçimlendirme ile değiştirilebilir:

[!code-aspx[Main](overview/samples/sample80.aspx)]

<a id="0.2__Toc253429271"></a><a id="0.2__Toc243304645"></a>

### <a name="checkboxlist-and-radiobuttonlist-control-enhancements"></a>CheckBoxList ve RadioButtonList denetimi geliştirmeleri

ASP.NET 3,5 ' de, *CheckBoxList* ve *RadioButtonList* için aşağıdaki iki ayarı kullanarak düzen belirtebilirsiniz:

- *Flow*. Denetim, içeriğini içerecek şekilde *span* öğelerini işler.
- *Tablo*. Denetim, içeriğini içeren bir *tablo* öğesi işler.

Aşağıdaki örnekte bu denetimlerin her biri için biçimlendirme gösterilmektedir.

[!code-aspx[Main](overview/samples/sample81.aspx)]

Varsayılan olarak, denetimler işleme HTML 'yi aşağıdakine benzer şekilde işler:

[!code-html[Main](overview/samples/sample82.html)]

Bu denetimler öğe listeleri içerdiğinden, anlamsal olarak doğru HTML 'yi işlemek için, HTML listesi (*li*) öğelerini kullanarak içeriklerini işlemelidir. Bu, yardımcı teknolojiyi kullanarak Web sayfalarını okuyan kullanıcıların daha kolay olmasını sağlar ve bu denetimleri CSS kullanarak stili daha kolay hale getirir.

ASP.NET 4 ' te, *CheckBoxList* ve *RadioButtonList* denetimleri, *RepeatLayout* özelliği için aşağıdaki yeni değerleri destekler:

- *OrderedList* : içerik bir *ol* öğesi içinde *li* öğeler olarak işlenir.
- *UnorderedList* : içerik bir *ul* öğesi içinde *li* öğeler olarak işlenir.

Aşağıdaki örnek, bu yeni değerlerin nasıl kullanılacağını göstermektedir.

[!code-aspx[Main](overview/samples/sample83.aspx)]

Yukarıdaki biçimlendirme aşağıdaki HTML 'yi oluşturur:

[!code-html[Main](overview/samples/sample84.html)]

> [!NOTE]
> *Notsenlayout* öğesini *OrderedList* veya *UnorderedList*olarak ayarlarsanız, *RepeatDirection* özelliği artık kullanılamaz ve bu özellik, biçimlendirme veya kodunuz içinde ayarlandıysa çalışma zamanında bir özel durum oluşturur. Bu denetimlerin görsel düzeni bunun yerine CSS kullanılarak tanımlandığından özelliğin değeri olmamalıdır.

<a id="0.2__Toc253429272"></a><a id="0.2__Toc243304646"></a>

### <a name="menu-control-improvements"></a>Menü denetimi geliştirmeleri

ASP.NET 4 öncesinde, *menü* denetimi BIR dizi HTML tablosu işlendi. Bu, satır içi Özellikler ayarının dışında CSS stillerinin uygulanmasını daha zor hale yaptı ve aynı zamanda erişilebilirlik standartları ile uyumlu değil.

ASP.NET 4 ' te, denetim artık sıralanmamış bir liste ve liste öğelerinden oluşan semantik biçimlendirmeyi kullanarak HTML 'yi işler. Aşağıdaki örnekte, *menü* denetimi için bir ASP.NET sayfasında biçimlendirme gösterilmektedir.

[!code-aspx[Main](overview/samples/sample85.aspx)]

Sayfa oluşturulduğunda, Denetim aşağıdaki HTML 'yi üretir ( *OnClick* kodu açıklık için atlandı):

[!code-html[Main](overview/samples/sample86.html)]

İşleme iyileştirmelerine ek olarak, menünün klavye gezintisi odak Yönetimi kullanılarak geliştirilmiştir. *Menü* denetimi odağı aldığında, öğelerin gezinmek için ok tuşlarını kullanabilirsiniz. *Menü* denetimi ayrıca[,](http://www.w3.org/TR/wai-aria-practices/#menu "Menü ARıA yönergeleri")Gelişmiş erişilebilirlik için de erişilebilir zengin internet uygulamaları (Aria) rollerini ve özniteliklerini de ekler.

Menü denetimi stilleri, oluşturulan HTML öğeleriyle satır yerine sayfanın üst kısmındaki stil bloğunda işlenir. Denetimin stili üzerinde tam denetim almak istiyorsanız, yeni *ıncludestyleblock* özelliğini *false*olarak ayarlayabilirsiniz, bu durumda stil bloğu yayılmaz. Bu özelliği kullanmanın bir yolu, Visual Studio tasarımcısında otomatik biçim özelliğini kullanarak menünün görünümünü ayarlamanıza olanak sağlar. Daha sonra sayfayı çalıştırabilir, sayfa kaynağını açabilir ve ardından işlenmiş stil bloğunu bir dış CSS dosyasına kopyalayabilirsiniz. Visual Studio 'da, stili geri alın ve *ıncludestyleblock* öğesini *false*olarak ayarlayın. Sonuç olarak, menü görünümü bir dış stil sayfasında stiller kullanılarak tanımlanır.

<a id="0.2__Toc253429273"></a><a id="0.2__Toc243304647"></a>

### <a name="wizard-and-createuserwizard-controls"></a>Sihirbaz ve CreateUserWizard denetimleri

ASP.NET *Sihirbazı* ve *CreateUserWizard* denetimleri, oluşturdukları HTML 'yi tanımlamanıza olanak sağlayan şablonları destekler. (*CreateUserWizard* , *sihirbazdan*türetilir.) Aşağıdaki örnekte, tam şablonlu bir *CreateUserWizard* denetimi için biçimlendirme gösterilmektedir:

[!code-aspx[Main](overview/samples/sample87.aspx)]

Denetim, HTML 'yi aşağıdakine benzer şekilde işler:

[!code-html[Main](overview/samples/sample88.html)]

ASP.NET 3,5 SP1 'de, şablon içeriğini değiştirebilmenize karşın, *sihirbaz* denetiminin çıktısı üzerinde hala sınırlı denetim sahibi olursunuz. ASP.NET 4 ' te, *Sihirbaz denetiminin* nasıl işleneceğini belirtmek Için bir *LayoutTemplate* şablonu oluşturabilir ve *yer tutucu* denetimleri (ayrılmış adlar kullanarak) ekleyebilirsiniz. Aşağıdaki örnek şunu gösterir:

[!code-aspx[Main](overview/samples/sample89.aspx)]

Örnek, *LayoutTemplate* öğesinde aşağıdaki adlandırılmış yer tutucuları içerir:

- *headerPlaceHolder* – çalışma zamanında, bu, *HeaderTemplate* öğesinin içeriğiyle değiştirilmiştir.
- *sideBarPlaceHolder* – çalışma zamanında, bu, *SideBarTemplate* öğesinin içeriğiyle değiştirilmiştir.
- *WizardStepPlaceHolder* – çalışma zamanında, bu, *wizardsteptemplate* öğesinin içeriğiyle değiştirilmiştir.
- *navigationPlaceHolder* – çalışma zamanında, bu, tanımladığınız tüm gezinti şablonlarıyla değiştirilmiştir.

Örnek yer tutucuları kullanan örnekteki biçimlendirme aşağıdaki HTML 'yi (şablonlarda gerçekten tanımlanmış içerik olmadan) oluşturur:

[!code-html[Main](overview/samples/sample90.html)]

Artık Kullanıcı tanımlı olmayan tek HTML, *span* öğesidir. (Gelecek sürümlerde, *span* öğesi oluşturulmayacak şekilde tahmin ederiz.) Bu artık, *sihirbaz* denetimi tarafından oluşturulan tüm içerikler üzerinde tam denetim elde etmenizi sağlar.

<a id="0.2_dyndata"></a><a id="0.2__Toc253429274"></a><a id="0.2__Toc243304648"></a><a id="0.2__Toc224729042"></a>

## <a name="aspnet-mvc"></a>ASP.NET MVC

ASP.NET MVC, ASP.NET 3,5 SP1 'e Mart 2009 ' de eklenti çerçevesi olarak sunulmuştur. Visual Studio 2010, yeni özellikler ve yetenekler içeren ASP.NET MVC 2 içerir.

<a id="0.2__Toc253429275"></a>

### <a name="areas-support"></a>Alan desteği

Alanları, diğer bölümlerden göreli yalıtımlarda, denetleyicileri ve görünümleri büyük bir uygulamanın bölümlerine gruplandırmenizi sağlar. Her alan, ana uygulama tarafından başvurulabilen ayrı bir ASP.NET MVC projesi olarak uygulanabilir. Bu, büyük bir uygulama oluşturduğunuzda karmaşıklığın yönetilmesine yardımcı olur ve birden çok ekibin tek bir uygulamada birlikte çalışmasını kolaylaştırır.

<a id="0.2__Toc253429276"></a>

### <a name="data-annotation-attribute-validation-support"></a>Veri ek açıklama öznitelik doğrulama desteği

*Dataaçıklamaların* öznitelikleri, meta veri özniteliklerini kullanarak bir modele doğrulama mantığı eklemenize olanak sağlar. ASP.NET dinamik verilerinde ASP.NET 3,5 SP1 'de *Dataaçıklamaların* öznitelikleri tanıtılmıştı. Bu öznitelikler varsayılan model Bağlayıcısı ile tümleşiktir ve Kullanıcı girişini doğrulamak için meta veri odaklı bir yol sağlar.

<a id="0.2__Toc253429277"></a>

### <a name="templated-helpers"></a>Şablonlu yardımcılar

Şablonlu yardımcılar, düzenleme ve görüntüleme şablonlarını veri türleriyle otomatik olarak ilişkilendirmenize olanak tanır. Örneğin, bir *System. DateTime* değeri için bir TARIH seçici UI öğesinin otomatik olarak işleneceğini belirtmek için şablon yardımcısını kullanabilirsiniz. Bu, ASP.NET dinamik verilerinde alan şablonlarına benzerdir.

*HTML. EditorFor* ve *HTML. DisplayFor* Helper yöntemleri, standart veri türlerini ve birden çok özelliği olan karmaşık nesneleri işlemek için yerleşik desteğe sahiptir. Ayrıca, *ViewModel* nesnesine *DisplayName* ve *ScaffoldColumn* gibi veri ek açıklama öznitelikleri uygulamanıza izin vererek işlemeyi özelleştirir.

Genellikle, Kullanıcı arabirimi yardımcılarından çıkışı daha da özelleştirmek ve üretilme üzerinde tamamen denetim sağlamak istersiniz. *HTML. EditorFor* ve *HTML. DisplayFor* Helper yöntemleri bunu, işlenmiş çıktıyı geçersiz kılabilen ve denetleyebilen harici şablonlar tanımlamanıza olanak tanıyan bir şablon oluşturma mekanizması kullanarak destekler. Şablonlar bir sınıf için tek tek oluşturulabilir.

<a id="0.2__Toc253429278"></a><a id="0.2__Toc243304649"></a>

## <a name="dynamic-data"></a>Dinamik veriler

Dinamik veriler, orta 2008 ' de .NET Framework 3,5 SP1 sürümünde tanıtılmıştır. Bu özellik, aşağıdakiler de dahil olmak üzere veri odaklı uygulamalar oluşturmaya yönelik birçok geliştirme sağlar:

- Veri odaklı bir Web sitesini hızlı bir şekilde oluşturmak için bir RAD deneyimi.
- Veri modelinde tanımlanan kısıtlamalara dayalı otomatik doğrulama.
- *GridView* 'daki alanlar için oluşturulan biçimlendirmeyi kolayca değiştirebilme ve *DetailsView* , dinamik veri projenizin parçası olan alan şablonlarını kullanarak.

> [!NOTE]
> Göz atın hakkında daha fazla bilgi Için MSDN Kitaplığı 'ndaki [dinamik veri belgelerine](https://msdn.microsoft.com/library/cc488545.aspx) bakın.

ASP.NET 4 için dinamik veriler, geliştiricilere veri odaklı web sitelerini hızlıca oluşturmak için daha fazla güç sağlayacak şekilde geliştirilmiştir.

<a id="0.2__Toc253429279"></a><a id="0.2__Toc243304650"></a>

### <a name="enabling-dynamic-data-for-existing-projects"></a>Mevcut projeler için dinamik verileri etkinleştirme

.NET Framework 3,5 SP1 'e gönderilen dinamik veri özellikleri, aşağıdakiler gibi yeni özellikler getirdi:

- Alan şablonları: Bunlar veriye bağlı denetimler için veri türü tabanlı şablonlar sağlar. Alan şablonları, veri denetimlerinin görünümünü özelleştirmek için, her bir alan için şablon alanlarını kullanmaktan daha basit bir yol sağlar.
- Doğrulama – dinamik veriler, gerekli alanlar, Aralık denetimi, tür denetimi, normal ifadeleri kullanarak model eşleştirme ve özel doğrulama gibi yaygın senaryolar için doğrulama belirtmek üzere veri sınıflarında öznitelikleri kullanmanıza olanak sağlar. Doğrulama, veri denetimleri tarafından zorlanır.

Ancak, bu özellikler aşağıdaki gereksinimlere sahiptir:

- Veri erişim katmanının Entity Framework veya LINQ to SQL temel alan olması gerekiyordu.
- Bu özellikler için desteklenen tek veri kaynağı denetimleri *EntityDataSource* veya *LinqDataSource* denetimleridir.
- Özellikler, özelliği desteklemek için gerekli olan tüm dosyaları sağlamak için dinamik veriler veya dinamik veri varlıkları şablonları kullanılarak oluşturulmuş bir Web projesi gerektirir.

ASP.NET 4 ' te dinamik veri desteğinin önemli bir amacı, herhangi bir ASP.NET uygulaması için dinamik verilerin yeni işlevlerini etkinleştirmektir. Aşağıdaki örnek, var olan bir sayfada dinamik veri işlevselliğinden yararlanabilen denetimlerin işaretlemesini gösterir.

[!code-aspx[Main](overview/samples/sample91.aspx)]

Sayfanın kodunda, bu denetimler için dinamik veri desteğini etkinleştirmek üzere aşağıdaki kodun eklenmesi gerekir:

[!code-csharp[Main](overview/samples/sample92.cs)]

*GridView* denetimi düzenleme modundayken, dinamik veriler girilen verilerin doğru biçimde olduğunu otomatik olarak doğrular. Aksi takdirde bir hata iletisi görüntülenir.

Bu işlevsellik, ekleme modu için varsayılan değerleri belirtme gibi diğer avantajları da sağlar. Dinamik veriler olmadan, bir alan için varsayılan bir değer uygulamak üzere bir olaya iliştirmeli, denetimin ( *FindControl*kullanılarak) bulunması ve değerini ayarlamanız gerekir. ASP.NET 4 ' te, *EnableDynamicData* çağrısı, bu örnekte gösterildiği gibi, nesne üzerinde herhangi bir alan için varsayılan değerleri iletmenizi sağlayan ikinci bir parametreyi destekler:

[!code-csharp[Main](overview/samples/sample93.cs)]

<a id="0.2__Toc224729043"></a><a id="0.2__Toc253429280"></a><a id="0.2__Toc243304651"></a>

### <a name="declarative-dynamicdatamanager-control-syntax"></a>Bildirime dayalı DynamicDataManager denetimi sözdizimi

*DynamicDataManager* denetimi, tek yapmanız gereken şekilde, yalnızca kod içinde değil, ASP.net ' de en çok denetim ile yapılandırmak için geliştirilmiştir. *DynamicDataManager* denetimi için biçimlendirme aşağıdaki örneğe benzer şekilde görünür:

[!code-aspx[Main](overview/samples/sample94.aspx)]

Bu biçimlendirme, *DynamicDataManager* denetiminin *DataControls* bölümünde başvurulan GridView1 denetimi için dinamik veri davranışına izin vermez.

<a id="0.2__Toc224729044"></a><a id="0.2__Toc253429281"></a><a id="0.2__Toc243304652"></a>

### <a name="entity-templates"></a>Varlık şablonları

Varlık şablonları, özel bir sayfa oluşturmanıza gerek kalmadan verilerin yerleşimini özelleştirmenin yeni bir yolunu sunar. Sayfa *şablonları, (* dinamik verilerin önceki sürümlerindeki sayfa şablonlarında kullanılan *DetailsView* denetimi yerine) ve varlık şablonlarını işlemek için *DynamicEntity* denetimini kullanır. Bu, dinamik veriler tarafından işlenen biçimlendirme üzerinde daha fazla denetim sağlar.

Aşağıdaki liste, varlık şablonlarını içeren yeni proje dizin yerleşimini gösterir:

[!code-console[Main](overview/samples/sample95.cmd)]

`EntityTemplate` Dizin, veri modeli nesnelerinin nasıl görüntüleneceği hakkında şablonlar içerir. Varsayılan olarak, nesneleri, ASP.NET 3,5 SP1 'de dinamik veriler tarafından kullanılan, *DetailsView* denetimi tarafından oluşturulan biçimlendirme gibi görünen biçimlendirme sağlayan `Default.ascx` şablonu kullanılarak işlenir. Aşağıdaki örnekte `Default.ascx` denetimi için biçimlendirme gösterilmektedir:

[!code-aspx[Main](overview/samples/sample96.aspx)]

Varsayılan Şablonlar, tüm sitenin görünümünü değiştirmek için düzenlenebilir. Görüntüleme, düzenleme ve ekleme işlemlerine yönelik şablonlar vardır. Yalnızca bir nesne türünün görünümünü değiştirmek için veri nesnesinin adına göre yeni şablonlar eklenebilir. Örneğin, aşağıdaki şablonu ekleyebilirsiniz:

[!code-console[Main](overview/samples/sample97.cmd)]

Şablon aşağıdaki biçimlendirmeyi içerebilir:

[!code-aspx[Main](overview/samples/sample98.aspx)]

Yeni varlık şablonları, yeni *DynamicEntity* denetimi kullanılarak bir sayfada görüntülenir. Çalışma zamanında bu denetim, varlık şablonunun içeriğiyle değiştirilmiştir. Aşağıdaki biçimlendirmede, varlık şablonunu kullanan `Detail.aspx` sayfa şablonunda bulunan *FormView* denetimi gösterilmektedir. İşaretlemede *DynamicEntity* öğesine dikkat edin.

[!code-aspx[Main](overview/samples/sample99.aspx)]

<a id="0.2__Toc224729045"></a><a id="0.2__Toc253429282"></a><a id="0.2__Toc243304653"></a>

### <a name="new-field-templates-for-urls-and-email-addresses"></a>URL 'Ler ve e-posta adresleri için yeni alan şablonları

ASP.NET 4, `EmailAddress.ascx` ve `Url.ascx`iki yeni yerleşik alan şablonu sunar. Bu şablonlar, *Emadresi* veya *DataType* özniteliğiyle *URL* olarak işaretlenen alanlar için kullanılır. *Emadresi* nesneleri için, alan *mailto:* Protocol kullanılarak oluşturulan bir köprü olarak görüntülenir. Kullanıcılar bağlantıya tıkladığında kullanıcının e-posta istemcisini açar ve bir iskelet iletisi oluşturur. *URL* olarak yazılan nesneler sıradan köprüler olarak görüntülenir.

Aşağıdaki örnek, alanların nasıl işaretleneceğini gösterir.

[!code-csharp[Main](overview/samples/sample100.cs)]

<a id="0.2__Toc224729046"></a><a id="0.2__Toc253429283"></a><a id="0.2__Toc243304654"></a>

### <a name="creating-links-with-the-dynamichyperlink-control"></a>DynamicHyperLink denetimiyle bağlantılar oluşturma

Dinamik veriler, son kullanıcıların Web sitesine erişirken göreceği URL 'Leri denetlemek için .NET Framework 3,5 SP1 'e eklenen yeni yönlendirme özelliğini kullanır. Yeni *DynamicHyperLink* denetimi, dinamik bir veri sitesindeki sayfalara bağlantılar oluşturmayı kolaylaştırır. Aşağıdaki örnek, *DynamicHyperLink* denetiminin nasıl kullanılacağını gösterir:

[!code-aspx[Main](overview/samples/sample101.aspx)]

Bu biçimlendirme, `Global.asax` dosyasında tanımlanan yollara göre `Products` tablo için liste sayfasına işaret eden bir bağlantı oluşturur. Denetim otomatik olarak dinamik veri sayfasının temel aldığı varsayılan tablo adını kullanır.

<a id="0.2__Toc224729047"></a><a id="0.2__Toc253429284"></a><a id="0.2__Toc243304655"></a>

### <a name="support-for-inheritance-in-the-data-model"></a>Veri modelinde devralma desteği

Hem Entity Framework hem de LINQ to SQL veri modellerinde devralmayı destekler. Buna bir örnek `InsurancePolicy` tablo olan bir veritabanı olabilir. Ayrıca, `InsurancePolicy` ile aynı alanlara sahip `CarPolicy` ve `HousePolicy` tabloları içerebilir ve daha fazla alan ekleyebilirler. Dinamik veriler, veri modelindeki devralınan nesneleri anlamak ve devralınan tablolar için yapı iskelesi desteklemek üzere değiştirilmiştir.

<a id="0.2__Toc224729048"></a><a id="0.2__Toc253429285"></a><a id="0.2__Toc243304656"></a>

### <a name="support-for-many-to-many-relationships-entity-framework-only"></a>Çoktan çoğa Ilişkiler için destek (yalnızca Entity Framework)

Entity Framework, tablolar arasındaki çoktan çoğa ilişkiler için zengin desteğe sahiptir ve bu, ilişkiyi bir *varlık* nesnesi üzerinde bir koleksiyon olarak ortaya çıkaran şekilde uygulanır. Çoktan çoğa ilişkilerde yer alan verileri görüntüleme ve düzenlemeyle ilgili destek sağlamak için yeni `ManyToMany.ascx` ve `ManyToMany_Edit.ascx` alanı şablonları eklenmiştir.

<a id="0.2__Toc224729049"></a><a id="0.2__Toc253429286"></a><a id="0.2__Toc243304657"></a>

### <a name="new-attributes-to-control-display-and-support-enumerations"></a>Görüntüleme ve destek numaralandırmaları denetlemek için yeni öznitelikler

*DisplayAttribute* , alanların nasıl görüntülendiğine ilişkin ek denetim sağlamak için eklenmiştir. Dinamik verilerin önceki sürümlerindeki *DisplayName* özniteliği, bir alan için bir başlık olarak kullanılan adı değiştirmenize izin verilir. Yeni *DisplayAttribute* sınıfı, bir alanın görüntüleneceği sıra ve bir alanın filtre olarak kullanılıp kullanılmayacağını gösteren bir alanı görüntülemek için daha fazla seçenek belirlemenizi sağlar. Özniteliği aynı zamanda bir *GridView* denetimindeki Etiketler için kullanılan adın bağımsız denetimini, bir *DetailsView* denetiminde kullanılan adı, alan için yardım metnini ve alan için kullanılan filigranı (alan metin girişi kabul ederse) de sağlar.

*EnumDataTypeAttribute* sınıfı, alanları numaralandırmalar ile eşlemenizi sağlamak için eklenmiştir. Bu özniteliği bir alana uyguladığınızda, bir sabit listesi türü belirtirsiniz. Dinamik veriler, numaralandırma değerlerini görüntüleme ve düzenlemeyle ilgili Kullanıcı arabirimi oluşturmak için yeni `Enumeration.ascx` alanı şablonunu kullanır. Şablon, veritabanındaki değerleri, Numaralandırmadaki adlarla eşler.

<a id="0.2__Toc224729050"></a><a id="0.2__Toc253429287"></a><a id="0.2__Toc243304658"></a>

### <a name="enhanced-support-for-filters"></a>Filtreler için gelişmiş destek

Dinamik veriler 1,0, Boole sütunları ve yabancı anahtar sütunları için yerleşik filtrelerle birlikte gönderilir. Filtreler, görüntülenip görüntülenmediğini veya görüntülendikleri sırayı belirtmenize izin vermedi. Yeni *DisplayAttribute* özniteliği, bir sütunun bir filtre olarak görüntülenip görüntülenmeyeceğini ve görüntüleneceği sırayı kontrol ederek bu sorunlardan her ikisini de ele verir.

Ek bir geliştirme, filtreleme desteğinin Web Forms[yeni özelliği kullanmak için yeniden yazılmasından](#0.2__QueryExtender "_QueryExtender") oluşur. Bu, filtrelerin birlikte kullanılacağı veri kaynağı denetimi bilgisine gerek duymadan filtre oluşturmanıza olanak sağlar. Bu uzantılarla birlikte filtreler, yeni yenilerini eklemenize olanak sağlayan şablon denetimlerine de eklenmiştir. Son olarak, daha önce bahsedilen *DisplayAttribute* sınıfı varsayılan filtrenin geçersiz kılınmasına izin verir, *uiHint* , bir sütunun varsayılan alan şablonunun geçersiz kılınmasına izin verir.

<a id="0.2__Toc224729051"></a><a id="0.2__Toc253429288"></a><a id="0.2__Toc243304659"></a>

## <a name="visual-studio-2010-web-development-improvements"></a>Visual Studio 2010 Web geliştirme Iyileştirmeleri

Visual Studio 2010 ' de Web geliştirme, daha fazla CSS uyumluluğu, HTML ve ASP.NET biçimlendirme parçacıkları ve yeni dinamik IntelliSense JavaScript üzerinden daha fazla verimlilik için geliştirilmiştir.

<a id="0.2__Toc224729052"></a><a id="0.2__Toc253429289"></a><a id="0.2__Toc243304660"></a>

### <a name="improved-css-compatibility"></a>Gelişmiş CSS uyumluluğu

Visual Studio 2010 ' deki Visual Web Developer Designer, CSS 2,1 standartları uyumluluğunu artıracak şekilde güncelleştirilmiştir. Tasarımcı, HTML kaynağının bütünlüğünü daha iyi korur ve Visual Studio 'nun önceki sürümlerinden daha sağlamdır. Aynı zamanda, işleme, düzen ve bakım için gelecekteki geliştirmelerin daha iyi bir şekilde etkinleştirilmesi için mimari iyileştirmeler yapılmıştır.

<a id="0.2__Toc224729053"></a><a id="0.2__Toc253429290"></a><a id="0.2__Toc243304661"></a>

### <a name="html-and-javascript-snippets"></a>HTML ve JavaScript kod parçacıkları

HTML düzenleyicisinde, IntelliSense etiket adlarını otomatik olarak tamamlar. IntelliSense parçacıkları özelliği etiketlerin tamamını ve daha fazlasını otomatik olarak tamamlar. Visual Studio 2010 ' de IntelliSense kod parçaları, Visual Studio 'nun önceki C# sürümlerinde desteklenen ve Visual Basic birlikte JavaScript için desteklenir.

Visual Studio 2010, gerekli öznitelikler (runat = "Server" gibi) ve bir etikete özgü ortak öznitelikler ( *ID*, *DataSourceID*, *ControlToValidate*ve *Text*gıbı) dahil olmak üzere ortak ASP.net ve HTML etiketlerini otomatik olarak tamamlamanıza yardımcı olan 200 ' den fazla kod parçacığı içerir.

Daha fazla kod parçacığı indirebilir veya sizin veya takımınızın ortak görevler için kullandığı biçimlendirme bloklarını kapsülleyen kendi kod parçacıklarınızı yazabilirsiniz.

<a id="0.2__Toc224729054"></a><a id="0.2__Toc253429291"></a><a id="0.2__Toc243304662"></a>

### <a name="javascript-intellisense-enhancements"></a>JavaScript IntelliSense geliştirmeleri

Visual 2010 ' de JavaScript IntelliSense, daha zengin bir düzen deneyimi sunacak şekilde yeniden tasarlanmıştır. IntelliSense artık *registerNamespace* gibi yöntemler ve diğer JavaScript çerçeveleri tarafından kullanılan benzer teknikler tarafından dinamik olarak oluşturulan nesneleri tanır. Büyük yazı kitaplıklarını analiz etmek ve IntelliSense 'i çok az veya hiç işlem gecikmeyle göstermek için performans geliştirilmiştir. Uyumluluk, neredeyse tüm üçüncü taraf kitaplıklarını desteklemek ve farklı kodlama stillerini desteklemek için önemli ölçüde artmıştır. Belge açıklamaları artık siz yazarken ayrıştırılır ve IntelliSense tarafından hemen yararlanılabilir.

<a id="0.2__Toc224729055"></a><a id="0.2__Toc253429292"></a><a id="0.2__Toc243304663"></a>

## <a name="web-application-deployment-with-visual-studio-2010"></a>Visual Studio 2010 ile Web uygulaması dağıtımı

ASP.NET geliştiricileri bir Web uygulaması dağıttıklarında, genellikle aşağıdakiler gibi sorunlarla karşılaştıkları sorunları bullar:

- Paylaşılan bir barındırma sitesine dağıtım, yavaş olabilecek FTP gibi teknolojiler gerektirir. Ayrıca, bir veritabanını yapılandırmak için SQL betikleri çalıştırmak gibi görevleri el ile gerçekleştirmeniz ve bir sanal dizin klasörünü uygulama olarak yapılandırmak gibi IIS ayarlarını değiştirmeniz gerekir.
- Kurumsal bir ortamda, Web uygulaması dosyalarını dağıtmanın yanı sıra Yöneticiler, genellikle ASP.NET yapılandırma dosyalarını ve IIS ayarlarını değiştirmeli. Veritabanı yöneticilerinin, çalışan uygulama veritabanını almak için bir dizi SQL betiğini çalıştırması gerekir. Bu tür yüklemeler işgücü yoğun bir işlemdir, genellikle tamamlanması gereken saatleri alır ve dikkatle belgelenmelidir.

Visual Studio 2010, bu sorunları gideren ve Web uygulamalarını sorunsuz bir şekilde dağıtmanıza olanak tanıyan teknolojiler içerir. Bu teknolojilerden biri IIS Web Dağıtım aracıdır (MsDeploy. exe).

Visual Studio 2010 ' deki Web Dağıtım özellikleri aşağıdaki ana bölgeleri içerir:

- Web paketleme
- Web. config dönüşümü
- Veritabanı dağıtımı
- Web uygulamaları için tek tıklamayla yayımlama

Aşağıdaki bölümler, bu özelliklerle ilgili ayrıntıları sağlar.

<a id="0.2__Toc224729056"></a><a id="0.2__Toc253429293"></a><a id="0.2__Toc243304664"></a>

### <a name="web-packaging"></a>Web paketleme

Visual Studio 2010, uygulamanız için bir *Web paketi*olarak adlandırılan bir sıkıştırılmış (. zip) dosya oluşturmak için MSDeploy aracını kullanır. Paket dosyası, uygulamanız hakkındaki meta verileri ve aşağıdaki içeriği içerir:

- Uygulama havuzu ayarlarını, hata sayfası ayarlarını ve benzerlerini içeren IIS ayarları.
- Web sayfaları, Kullanıcı denetimleri, statik içerik (görüntüler ve HTML dosyaları) gibi gerçek Web içeriği.
- Veritabanı şemaları ve verileri SQL Server.
- Güvenlik sertifikaları, GAC 'de yüklenecek bileşenler, kayıt defteri ayarları vb.

Bir Web paketi herhangi bir sunucuya kopyalanabilir ve ardından IIS Yöneticisi kullanılarak el ile yüklenebilir. Alternatif olarak, otomatik dağıtım için paket komut satırı komutları kullanılarak veya dağıtım API 'Leri kullanılarak yüklenebilir.

Visual Studio 2010, Web paketleri oluşturmak için yerleşik MSBuild görevleri ve hedefleri sağlar. Daha fazla bilgi için bkz. [ASP.NET Web uygulaması proje dağıtımına genel bakış](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx) MSDN Web sitesi ve 10 + 20 nedeni, Vishal Joshi 'in bloguna [bir Web paketi oluşturmanız gerektiğine](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html) yönelik.

<a id="0.2__Toc224729057"></a><a id="0.2__Toc253429294"></a><a id="0.2__Toc243304665"></a>

### <a name="webconfig-transformation"></a>Web. config dönüşümü

Web uygulaması dağıtımı için, Visual Studio 2010, `Web.config` bir dosyayı geliştirme ayarlarından üretim ayarlarına dönüştürmenizi sağlayan bir özellik olan [XML belge dönüşümünü (XDT)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)tanıtır. Dönüştürme ayarları `web.debug.config`, `web.release.config`vb. adlı dönüştürme dosyalarında belirtilir. (Bu dosyaların adları MSBuild yapılandırmalarına uymuyor.) Bir dönüşüm dosyası, yalnızca dağıtılan bir `Web.config` dosyasında yapmanız gereken değişiklikleri içerir. Basit sözdizimi kullanarak değişiklikleri belirlersiniz.

Aşağıdaki örnek, yayın yapılandırmanızın dağıtılması için üretilebilen bir `web.release.config` dosyasının bir bölümünü gösterir. Örnekteki Replace anahtar sözcüğü, dağıtım sırasında `Web.config` dosyasındaki *ConnectionString* düğümünün, örnekte listelenen değerlerle değiştirileceğini belirtir.

[!code-xml[Main](overview/samples/sample102.xml)]

Daha fazla bilgi için, MSDN <a id="0.2_a"></a> Web sitesindeki Web [uygulaması proje dağıtımı için Web. config dönüştürme sözdizimi](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx) ve Vishal Joshi[Web dağıtımı: Web. config dönüşümünde](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) bkz.

<a id="0.2__Toc224729058"></a><a id="0.2__Toc253429295"></a><a id="0.2__Toc243304666"></a>

### <a name="database-deployment"></a>Veritabanı dağıtımı

Visual Studio 2010 dağıtım paketi, SQL Server veritabanlarına bağımlılıklar içerebilir. Paket tanımının bir parçası olarak, kaynak veritabanınızın bağlantı dizesini sağlarsınız. Web paketini oluştururken, Visual Studio 2010, veritabanı şeması ve isteğe bağlı olarak veriler için SQL betikleri oluşturur ve ardından bunları pakete ekler. Ayrıca özel SQL betikleri sağlayabilir ve sunucuda çalıştırmaları gereken sırayı belirtebilirsiniz. Dağıtım zamanında, hedef sunucuya uygun bir bağlantı dizesi sağlarsınız; daha sonra dağıtım işlemi, veritabanı şemasını oluşturan ve verileri ekleyen betikleri çalıştırmak için bu bağlantı dizesini kullanır.

Ayrıca, tek tıklamayla yayımlama kullanarak, uygulama uzak bir paylaşılan barındırma sitesine yayımlandığında veritabanını doğrudan yayımlamak için dağıtımı yapılandırabilirsiniz. Daha fazla bilgi için, bkz. [nasıl yapılır: msdn Web sitesinde Web uygulaması projesiyle bir veritabanı dağıtma](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx) ve Vishal Joshi 'in blogu üzerinde [vs 2010 ile veritabanı dağıtımı](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) .

<a id="0.2__Toc224729059"></a><a id="0.2__Toc253429296"></a><a id="0.2__Toc243304667"></a>

### <a name="one-click-publish-for-web-applications"></a>Web uygulamaları için tek tıklamayla yayımlama

Visual Studio 2010, bir Web uygulamasını uzak bir sunucuda yayımlamak için IIS Uzaktan Yönetim hizmetini de kullanmanıza imkan tanır. Barındırma hesabınız için veya sunucuları ya da hazırlama sunucularını test etmek için bir yayımlama profili oluşturabilirsiniz. Her profil, uygun kimlik bilgilerini güvenli bir şekilde kaydedebilir. Daha sonra, Web tek tıklamayla Yayımla araç çubuğunu kullanarak hedef sunuculardan birine tek bir tıklama ile dağıtım yapabilirsiniz. Visual Studio 2010 ile, MSBuild komut satırını kullanarak da yayımlayabilirsiniz. Bu, ekip derleme ortamınızı sürekli tümleştirme modeline yayımlamayı içerecek şekilde yapılandırmanıza olanak tanır.

Daha fazla bilgi için, bkz. [nasıl yapılır: bir Web uygulaması projesini, MSDN Web sitesinde tek tıklamayla Yayımla ve Web dağıtımı kullanarak dağıtma](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx) ve Web 1-Vishal Joshi BLOGUNA [vs 2010 ile Yayımla ' ya tıklayın](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html) . Visual Studio 2010 ' de Web uygulaması dağıtımıyla ilgili video sunularını görüntülemek için, Vishal Joshi ' deki [Web geliştirici önizlemeleri Için VS 2010](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html) bölümüne bakın.

<a id="0.2__Toc224729060"></a><a id="0.2__Toc253429297"></a><a id="0.2__Toc243304668"></a>

### <a name="resources"></a>Kaynaklar

Aşağıdaki Web siteleri, ASP.NET 4 ve Visual Studio 2010 hakkında ek bilgiler sağlar.

- [ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) — MSDN Web sitesinde ASP.NET 4 için resmi belgeler.
- [https://www.asp.net/](https://www.asp.net/) — ASP.net ekibinin kendi web sitesi.
- [https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx) ve [ASP.NET dinamik veri içeriği Haritası](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx) — ASP.NET ekip sitesindeki çevrimiçi kaynaklar ve ASP.NET dinamik veriler için resmi belgelerde.
- [https://www.asp.net/ajax/](../../ajax/index.md) — ASP.NET AJAX geliştirmesi Için ana Web kaynağı.
- [https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/) — visual Studio 2010 özellikleri hakkında bilgi Içeren Visual Web Developer ekip blogu.
- [ASP.net WebStack](https://github.com/aspnet/AspNetWebStack) — ASP.net 'in önizleme sürümleri Için ana web kaynağıdır.

<a id="0.2__Toc224729061"></a><a id="0.2__Toc253429298"></a><a id="0.2__Toc243304669"></a>

## <a name="disclaimer"></a>Sorumluluk reddi

Bu bir ön belgedir ve burada açıklanan yazılımın son ticari sürümünden önce önemli ölçüde değiştirilebilir.

Bu belgede yer alan bilgiler, Yayın tarihi itibariyle ele alınan sorunlar hakkında Microsoft Corporation 'ın geçerli görünümünü temsil eder. Microsoft 'un değişen piyasa koşullarını yanıtlaması gerektiğinden, Microsoft 'un kapsamında bir taahhüt olarak yorumlanmamalıdır ve Microsoft 'un, yayın tarihinden sonra sunulan bilgilerin doğruluğunu garanti edemez.

Bu teknik Inceleme yalnızca bilgilendirme amaçlıdır. MICROSOFT, BU BELGEDEKI BILGILERE GÖRE HIÇBIR GARANTI VERMEZ, ÖRTÜLÜ VEYA YASAL DEĞILDIR.

Tüm geçerli telif hakkı yasaları ile uyumlu olması, kullanıcının sorumluluğundadır. Telif hakkı kapsamındaki hakları sınırlandırmadan, bu belgenin hiçbir bölümü çoğaltılamaz, bir alma sisteminde depolanabilir veya bir alma sisteminde bulunabilir ya da herhangi bir biçimde ya da herhangi bir amaçla (elektronik, mekanik, Fotokopi, kayıt veya diğer yollarla) veya herhangi bir amaçla iletilebilir Microsoft Corporation 'ın Express yazılı izni olmadan.

Microsoft 'un bu belgede ilgili konuyu kapsayan patentler, patent uygulamaları, ticari markalar, telif hakları veya diğer fikri mülkiyet hakları olabilir. Microsoft 'un herhangi bir yazılı lisans sözleşmesinde açık bir şekilde sağlanmasının dışında, bu belgenin bu patentinin bir lisansını, ticari markalara, telif haklarına veya diğer fikri mülkiyet için herhangi bir lisansa vermez.

Aksi belirtilmedikçe, burada adı geçen örnek şirketler, kuruluşlar, ürünler, etki alanı adları, e-posta adresleri, logolar, kişiler, konumlar ve olaylar kurgusaldır ve gerçek şirket, kuruluş, ürün, etki alanı adı, e-posta ile hiçbir ilişki yoktur Adres, logo, kişi, yer veya olay amaçlıdır veya çıkarsanmalıdır.

© 2009 Microsoft Corporation. Tüm hakları saklıdır.

Microsoft ve Windows, Microsoft Corporation 'ın Birleşik Devletler ve/veya diğer ülkelerde kayıtlı ticari markaları veya ticari markalarıdır.

Burada bahsedilen gerçek şirketlerin ve ürünlerin adları, ilgili sahiplerinin ticari markaları olabilir.
