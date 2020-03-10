---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-vb
title: IIS ile ASP.NET geliştirme sunucusu arasındaki temel farklılıklar (VB) | Microsoft Docs
author: rick-anderson
description: Bir ASP.NET uygulamasını yerel olarak test ederken, ASP.NET Development Web sunucusunu kullanıyor olursunuz. Ancak üretim web sitesi büyük olasılıkla çok büyük...
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 090e9205-52f3-4d72-ae31-44775b8b8421
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-vb
msc.type: authoredcontent
ms.openlocfilehash: 880bb403e671446a77d7eebccf578a1dc714d1f9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78545628"
---
# <a name="core-differences-between-iis-and-the-aspnet-development-server-vb"></a>IIS ile ASP.NET Geliştirme Sunucusu Arasındaki Temel Farklılıklar (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_06_VB.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial06_WebServerDiff_vb.pdf)

> Bir ASP.NET uygulamasını yerel olarak test ederken, ASP.NET Development Web sunucusunu kullanıyor olursunuz. Ancak üretim web sitesi, büyük olasılıkla desteklenen IIS 'dir. Bu Web sunucularının istekleri nasıl işleydiğiyle arasında bazı farklılıklar vardır ve bu farklılıklar önemli sonuçlara sahip olabilir. Bu öğreticide, daha fazla gere farkı incelenmektedir.

## <a name="introduction"></a>Giriş

Bir Kullanıcı bir ASP.NET uygulamasını ziyaret ettiğinde, tarayıcı web sitesine bir istek gönderir. Bu istek Web sunucusu yazılımı tarafından çekilir ve bu, istenen kaynağın içeriğini oluşturmak ve döndürmek için ASP.NET çalışma zamanına göre eşgüdümünü sağlar. [**İ** nternet **i** nm **S** Ervıces (IIS)](http://en.wikipedia.org/wiki/Internet_Information_Services) , Windows sunucuları için ortak Internet tabanlı işlevselliği sağlayan bir hizmet paketidir. IIS, üretim ortamlarında ASP.NET uygulamaları için en yaygın olarak kullanılan Web sunucusudur; Web barındırma sağlayıcınız tarafından ASP.NET uygulamanızı karşılamak için kullanılan Web sunucusu yazılımı en büyük olasılıktır. IIS, geliştirme ortamında Web sunucusu yazılımı olarak da kullanılabilir, ancak bu, IIS yüklemeyi ve düzgün şekilde yapılandırmayı gerektirir.

ASP.NET geliştirme sunucusu, geliştirme ortamı için alternatif bir Web sunucusu seçeneğidir; ile birlikte gönderilir ve Visual Studio ile tümleşiktir. Web uygulaması IIS kullanmak üzere yapılandırılmamışsa, Visual Studio içinden bir Web sayfasını ilk kez ziyaret ettiğinizde ASP.NET geliştirme sunucusu otomatik olarak başlatılır ve Web sunucusu olarak kullanılır. [*Hangi dosyaların dağıtılması gerektiğini belirleme*](determining-what-files-need-to-be-deployed-vb.md) öğreticisinde oluşturduğumuz tanıtım Web UYGULAMALARı, IIS kullanmak üzere yapılandırılmamış dosya sistemi tabanlı web uygulamamız. Bu nedenle, Visual Studio içinden bu Web sitelerinden birini ziyaret ederken ASP.NET Development Server kullanılır.

Mükemmel bir dünyada geliştirme ve üretim ortamları aynı olacaktır. Ancak, önceki öğreticide anlatıldığı gibi, ortamlar farklı yapılandırma ayarlarına sahip olmak için yaygın olmayan bir durumdur. Ortamlarda farklı Web sunucusu yazılımlarının kullanılması, bir uygulama dağıtıldığında dikkate alınması gereken başka bir değişken ekliyor. Bu öğreticide, IIS ve ASP.NET geliştirme sunucusu arasındaki temel farklılıklar ele alınmaktadır. Bu farklılıklar nedeniyle, geliştirme ortamında sorunsuz şekilde çalışan kodun bir özel durum oluşturduğunda veya üretimde yürütüldüğünde farklı davrandığı senaryolar vardır.

## <a name="security-context-differences"></a>Güvenlik bağlamı farklılıkları

Web sunucusu yazılımı gelen bir isteği işlediğinde, bu isteği belirli bir güvenlik bağlamı ile ilişkilendirir. Bu güvenlik bağlamı bilgileri, istek tarafından hangi eylemlerin izin verilen olduğunu belirlemek için işletim sistemi tarafından kullanılır. Örneğin, bir ASP.NET sayfası, bazı iletileri diskteki bir dosyaya kaydeden kodu içerebilir. Bu ASP.NET sayfasının hata olmadan yürütülmesi için, güvenlik bağlamının uygun dosya sistemi düzeyi izinlerine sahip olması gerekir ve bu dosya üzerinde yazma izinleri vardır.

ASP.NET Development Server, gelen istekleri, oturum açmış olan kullanıcının güvenlik içeriğiyle ilişkilendirir. Masaüstünüzde yönetici olarak oturum açtıysanız, ASP.NET Development Server tarafından sunulan ASP.NET sayfaları, yönetici ile aynı erişim haklarına sahip olur. Ancak, IIS tarafından işlenen ASP.NET istekleri belirli bir makine hesabıyla ilişkilendirilir. Varsayılan olarak, Web ana bilgisayar sağlayıcınız her müşteri için benzersiz bir hesap yapılandırmış olsa da, ağ hizmeti makine hesabı 6 ve 7 IIS sürümleri tarafından kullanılır. Ne kadar çok, Web ana bilgisayar sağlayıcınız bu makine hesabına sınırlı izinleri vermiş olabilir. Net sonuç, geliştirme ortamında hatasız şekilde yürütülen web sayfalarınız olabilir, ancak üretim ortamında barındırılırken yetkilendirmeyle ilgili özel durumlar oluşturabilirsiniz.

Bu tür bir hata türünü görüntülemek için kitap Incelemeleri Web sitesinde bir sayfada bir dosya oluşturan en son tarihi ve saati veren bir dosyayı, *24 saat içinde ASP.NET 3,5* inceleyin. Bu arada izlemek için `~/Tech/TYASP35.aspx` sayfasını açın ve aşağıdaki kodu `Page_Load` olay işleyicisine ekleyin:

[!code-vb[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample1.vb)]

> [!NOTE]
> [`File.WriteAllText` yöntemi](https://msdn.microsoft.com/library/system.io.file.writealltext.aspx) yoksa yeni bir dosya oluşturur ve belirtilen içeriği buna yazar. Dosya zaten varsa, var olan içeriğin üzerine yazılır.

Daha sonra, ASP.NET geliştirme sunucusunu kullanarak geliştirme ortamında *kendinizi 24 saat içinde ASP.NET 3,5* inceleme sayfasına gidin. Bilgisayarınızda, Web uygulamasının kök dizininde bir metin dosyası oluşturmak ve değiştirmek için yeterli izinlere sahip bir hesapla oturum açtığınızı varsayarsak, kitap incelemesi daha önce olduğu gibi görünür, ancak sayfa tarih ve saati ziyaret edildiğinde ve kullanıcının IP adresi `LastTYASP35Access.txt` dosyasında depolanır. Tarayıcınızı bu dosyaya işaret edin; Şekil 1 ' de gösterilenle benzer bir ileti görmeniz gerekir.

[![metin dosyası, kitap Incelemesinin ziyaret ettiği son tarihi ve saati Içerir&lt;](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image2.png)](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image1.png)

**Şekil 1**: metin dosyası, kitap Incelemesinin ziyaret edilme son tarihi ve saati içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image3.png))

Web uygulamasını üretime dağıtın ve ardından barındırılan *öğretme ASP.NET 3,5 ' i 24 saat içinde* inceleyin. Bu noktada kitap incelemesi sayfasını normal veya şekil 2 ' de gösterilen hata iletisi olarak görmeniz gerekir. Bazı Web ana bilgisayar sağlayıcıları anonim ASP.NET makine hesabına yazma izinleri verir ve bu durumda sayfa hatasız çalışacaktır. Ancak, Web ana bilgisayar sağlayıcınız anonim hesap için yazma erişimini yasakladığından, `TYASP35.aspx` sayfası `LastTYASP35Access.txt` dosyasına geçerli tarih ve saati yazmaya çalıştığında [`UnauthorizedAccessException` bir özel durum](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) oluşur.

[![IIS tarafından kullanılan varsayılan makine hesabının dosya sistemine yazma Izni yok](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image5.png)](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image4.png)

**Şekil 2**: IIS tarafından kullanılan varsayılan makine hesabının dosya sistemine yazma izni yok ([tam boyutlu görüntüyü görüntülemek için tıklatın](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image6.png))

En iyi haber, Web ana bilgisayar sağlayıcılarının, Web sitenizde dosya sistemi izinleri belirtmenize izin veren bir dizi izin aracına sahip olduğu yerdir. Anonymous ASP.NET hesabına kök dizinine yazma erişimi verin ve ardından kitap incelemesi sayfasını ziyaret edin. (Gerekirse, varsayılan ASP.NET hesabına yazma izinleri verme hakkında yardım almak için Web ana bilgisayar sağlayıcınızla iletişim kurun.) Bu zaman sayfa hata olmadan yüklenir ve `LastTYASP35Access.txt` dosya başarıyla oluşturulmalıdır.

Burada ele alma, ASP.NET geliştirme sunucusu IIS 'den farklı bir güvenlik bağlamı altında çalıştığı için, dosya sistemine okuma veya yazma, Windows olay günlüğünü okuma veya yazma veya Windows olay günlüğü 'ne okuma veya yazma gibi ASP.NET sayfalarınız olabilir.  kayıt defteri, geliştirme sırasında beklendiği gibi çalışacaktır ancak üretimde özel durum oluşturur. Paylaşılan bir Web barındırma ortamına dağıtılacak bir Web uygulaması oluştururken, olay günlüğünü veya Windows kayıt defteri 'ni okuma veya yazma. Ayrıca, üretim ortamındaki uygun klasörlerde okuma ve yazma ayrıcalıkları vermeniz gerekebilmeniz için dosya sisteminden okuma veya yazma ayrıcalıklarına sahip tüm ASP.NET sayfalarını da göz önünde bulabilirsiniz.

## <a name="differences-on-serving-static-content"></a>Statik Içerik sunma farkları

IIS ile ASP.NET geliştirme sunucusu arasındaki diğer temel fark, statik içerik isteklerini nasıl işleyseler. ASP.NET geliştirme sunucusuna gelen her istek, bir ASP.NET sayfası, bir resim veya bir JavaScript dosyası için ASP.NET çalışma zamanı tarafından işlenir. Varsayılan olarak, IIS yalnızca bir ASP.NET kaynağı için bir istek geldiğinde, bir ASP.NET Web sayfası, bir Web hizmeti gibi ASP.NET çalışma zamanını çağırır. Statik içerik-görüntü, CSS dosyaları, JavaScript dosyaları, PDF dosyaları, ZIP dosyaları ve LIKE-ASP.NET çalışma zamanının katılımı olmadan IIS tarafından alınan istekler. (Daha fazla bilgi için, IIS 'nin ASP.NET çalışma zamanı ile çalışmasını söylemek mümkündür. daha fazla bilgi için, bu öğreticideki "IIS 7 ile statik dosyalarda Forms tabanlı kimlik doğrulaması ve URL kimlik doğrulaması gerçekleştirme" bölümüne bakın.)

ASP.NET çalışma zamanı, kimlik doğrulama (istek sahibi belirleme) ve yetkilendirme (istek sahibinin istenen içeriği görüntüleme iznine sahip olup olmadığını belirleme) dahil olmak üzere istenen içeriği oluşturmak için birkaç adım gerçekleştirir. Popüler bir kimlik doğrulama biçimi, bir kullanıcının kimlik bilgilerini (genellikle bir Web sayfasındaki Kullanıcı adı ve parola) girerek tanımladığı *form tabanlı kimlik doğrulamasıdır*. Kimlik bilgileri doğrulandıktan sonra, Web sitesi kullanıcının tarayıcısına bir *kimlik doğrulama bileti* tanımlama bilgisi depolar ve bu, Web sitesine yapılan her sonraki istekle birlikte gönderilir ve kullanıcının kimliğini doğrulamak için kullanılır. Ayrıca, kullanıcıların belirli bir klasöre ne yapabileceğini veya erişebileceklerini dikte eden *URL yetkilendirme* kuralları belirtilebilir. Birçok ASP.NET Web sitesi, Kullanıcı hesaplarını desteklemek için form tabanlı kimlik doğrulaması ve URL yetkilendirmesi kullanır ve site yalnızca kimliği doğrulanmış kullanıcılar veya belirli bir role ait olan kullanıcılar tarafından erişilebilen bölümleri tanımlar.

> [!NOTE]
> Tam bir ASP incelemesi için. NET ' in form tabanlı kimlik doğrulaması, URL yetkilendirmesi ve Kullanıcı hesabı ile ilgili diğer özellikler, [Web sitesi güvenlik öğreticilerimi](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)göz önüne aldığınızdan emin olun.

Form tabanlı yetkilendirme kullanan kullanıcı hesaplarını destekleyen bir Web sitesi düşünün ve URL yetkilendirmesi kullanan bir klasör, yalnızca kimliği doğrulanmış kullanıcılara izin verecek şekilde yapılandırılır. Bu klasörün ASP.NET sayfaları ve PDF dosyaları içerdiğini ve bu PDF dosyalarını yalnızca kimliği doğrulanmış kullanıcıların görüntüleyebileceklerini belirten bir düşünün.

Ziyaretçi, URL 'YI tarayıcının adres çubuğuna doğrudan girerek bu PDF dosyalarından birini görüntülemeyi denerse ne olur? Daha fazla bilgi edinmek için, kitap Incelemeleri sitesinde yeni bir klasör oluşturalım, bazı PDF dosyaları ekleme ve siteyi anonim kullanıcıların bu klasörü ziyaret etmesini önlemek için URL yetkilendirmesi kullanacak şekilde yapılandırma. Demo uygulamasını indirdiğinizde, `PrivateDocs` adlı bir klasör oluşturdum ve [Web sitemin güvenlik öğreticilerimin](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md) (nasıl sığdırma!) bir PDF eklendiğini görürsünüz. `PrivateDocs` klasörü, anonim kullanıcıları reddetmek için URL yetkilendirme kurallarını belirten bir `Web.config` dosyası da içerir:

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample2.xml)]

Son olarak, Web uygulamasını kök dizindeki Web. config dosyasını güncelleştirerek form tabanlı kimlik doğrulaması kullanacak şekilde yapılandırdım, şunu değiştirin:

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample3.xml)]

Yerine konan:

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample4.xml)]

ASP.NET geliştirme sunucusunu kullanarak, siteyi ziyaret edin ve tarayıcınızın adres çubuğundaki PDF dosyalarından birine doğrudan URL 'yi girin. Bu öğreticiyle ilişkili Web sitesini indirdiyseniz URL şöyle görünmelidir: `http://localhost:portNumber/PrivateDocs/aspnet_tutorial01_Basics_vb.pdf`

Bu URL 'YI adres çubuğuna girmek tarayıcının dosya için ASP.NET geliştirme sunucusuna bir istek göndermesini sağlar. ASP.NET Development Server, işleme için ASP.NET çalışma zamanına isteği kapatır. Henüz oturum açmadığımız ve `PrivateDocs` klasöründeki `Web.config` anonim erişimi reddedecek şekilde yapılandırıldığı için, ASP.NET çalışma zamanı otomatik olarak ABD 'yi oturum açma sayfasına `Login.aspx` (bkz. Şekil 3). Kullanıcıyı, oturum açma sayfasında yeniden yönlendirirken, ASP.NET bir `ReturnUrl` QueryString parametresi içerir ve kullanıcının görüntülemeye çalıştığınız sayfayı gösterir. Kullanıcı başarıyla günlüğe kaydedildikten sonra bu sayfaya geri dönebilirler.

[Yetkisiz kullanıcılar ![oturum açma sayfasına otomatik olarak yönlendirilir](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image8.png)](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image7.png)

**Şekil 3**: yetkisiz kullanıcılar otomatik olarak oturum açma sayfasına yönlendirilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image9.png))

Şimdi bunun üretimde nasıl davranacağını görelim. Uygulamanızı dağıtın ve üretimde `PrivateDocs` klasöründeki PDF 'Lerden birine doğrudan URL 'YI girin. Bu, tarayıcınızı dosya için bir istek IIS göndermesini ister. Statik bir dosya istentiğinden, IIS ASP.NET çalışma zamanını çağırmadan dosyayı alır ve döndürür. Sonuç olarak, URL yetkilendirme denetimi gerçekleştirilmedi; gizli olmayan özel PDF 'nin içeriğine dosyanın doğrudan URL 'sini bilen herkes erişebilir.

[![anonim kullanıcılar, dosyaya doğrudan URL girerek özel PDF dosyalarını Indirebilir](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image11.png)](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image10.png)

**Şekil 4**: anonim kullanıcılar DOSYANıN doğrudan URL 'Sini gırerek özel PDF dosyalarını indirebilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image12.png))

### <a name="performing-forms-based-authentication-and-url-authentication-on-static-files-with-iis-7"></a>IIS 7 ile statik dosyalarda form tabanlı kimlik doğrulaması ve URL kimlik doğrulaması gerçekleştirme

Yetkisiz kullanıcılardan statik içeriği korumak için kullanabileceğiniz birkaç teknik vardır. IIS 7, ASP.NET çalışma zamanının iş akışı ile birlikte IIS 'nin iş akışını marrıes ile *Tümleşik*işlem hattını sunmuştur. Bir Nutshell 'de, IIS 'nin ASP.NET çalışma zamanının kimlik doğrulama ve yetkilendirme modüllerini tüm gelen istekleri (PDF dosyaları gibi statik içerik dahil) çağırabilmesini söyleyebilirsiniz. Web sitenizin tümleşik işlem hattını kullanmak üzere nasıl yapılandırılacağını öğrenmek için Web barındırma sağlayıcınızla iletişim kurun.

IIS Tümleşik işlem hattını kullanacak şekilde yapılandırıldıktan sonra aşağıdaki biçimlendirmeyi kök dizindeki `Web.config` dosyasına ekleyin:

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample5.xml)]

Bu biçimlendirme, IIS 7 ' nin ASP.NET tabanlı kimlik doğrulama ve yetkilendirme modüllerini kullanmasını söyler. Uygulamanızı yeniden dağıtın ve ardından PDF dosyasını yeniden ziyaret edin. Bu kez, IIS isteği işlediğinde, isteği incelemeye yönelik bir fırsat olan ASP.NET çalışma zamanının kimlik doğrulama ve yetkilendirme mantığını verir. Yalnızca kimliği doğrulanmış kullanıcılar `PrivateDocs` klasöründeki içeriği görüntüleme yetkisine sahip olduğundan, anonim ziyaretçi otomatik olarak oturum açma sayfasına yönlendirilir (Şekil 3 ' e geri bakın).

> [!NOTE]
> Web ana bilgisayar sağlayıcınız hala IIS 6 kullanıyorsa, tümleşik işlem hattı özelliğini kullanamazsınız. Tek bir geçici çözüm, özel belgelerinizi HTTP erişimini yasaklamış bir klasöre (örneğin, `App_Data`) koymaya ve sonra bu belgeleri sunacak bir sayfa oluşturmaya yönelik bir çözümdür. Bu sayfa `GetPDF.aspx`olarak adlandırılır ve bir QueryString parametresi aracılığıyla PDF 'nin adını geçti. `GetPDF.aspx` sayfası öncelikle kullanıcının dosyayı görüntüleme iznine sahip olduğunu doğrular ve bu durumda, istenen PDF dosyasının içeriğini istekte bulunan istemciye geri göndermek için [`Response.WriteFile(filePath)`](https://msdn.microsoft.com/library/system.web.httpresponse.writefile.aspx) yöntemini kullanır. Bu teknik, tümleşik ardışık düzeni etkinleştirmek istemiyorsanız IIS 7 için de çalışır.

## <a name="summary"></a>Özet

Bir üretim ortamındaki Web uygulamaları Microsoft 'un IIS Web sunucusu yazılımı kullanılarak barındırılır. Ancak geliştirme ortamında, uygulama IIS veya ASP.NET Development Server kullanılarak barındırılıyor olabilir. İdeal olarak, farklı yazılımlar kullanmak karışımta başka bir değişken eklediğinden, aynı Web sunucusu yazılımı her iki ortamda da kullanılmalıdır. Ancak, ASP.NET Development Server 'ın kullanım kolaylığı, geliştirme ortamında etkileyici bir seçenek sunar. İyi haber, IIS ve ASP.NET geliştirme sunucusu arasında yalnızca birkaç temel farklılık olmakla kalmaz ve bu farklılıkları biliyorsanız, uygulamanın çalıştığından ve ' den bağımsız olarak aynı şekilde çalıştığından emin olmanıza yardımcı olmak için adımları izleyebilirsiniz. ortamınızın.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [IIS 7,0 ile ASP.NET tümleştirmesi](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)
- [IIS 7 ' de tüm Içerik türleriyle ASP.net forumları kimlik doğrulamasını kullanma](https://blogs.iis.net/bills/archive/2007/05/19/using-asp-net-forms-authentication-with-all-types-of-content-with-iis7-video.aspx) (video)
- [Visual Web Developer 'da Web sunucuları](https://msdn.microsoft.com/library/58wxa9w5.aspx)

> [!div class="step-by-step"]
> [Önceki](common-configuration-differences-between-development-and-production-vb.md)
> [İleri](deploying-a-database-vb.md)
