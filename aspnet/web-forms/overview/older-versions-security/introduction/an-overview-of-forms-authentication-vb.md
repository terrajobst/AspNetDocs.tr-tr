---
uid: web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-vb
title: Forms kimlik doğrulamasına genel bakış (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, boyutundaydı tartışmadan uygulamaya ekleyeceğiz; Özellikle, form kimlik doğrulamasını uygulama bölümüne bakacağız. Web uygulaması w...
ms.author: riande
ms.date: 01/14/2008
ms.assetid: 83267f7d-64d9-41ee-82cf-da91b1bf534d
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: d8ceb6b5290300992e52199caa9314c573de1942
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74626295"
---
# <a name="an-overview-of-forms-authentication-vb"></a>Forms kimlik doğrulamasına genel bakış (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/ASPNET_Security_Tutorial_02_VB.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial02_FormsAuth_vb.pdf)

> Bu öğreticide, boyutundaydı tartışmadan uygulamaya ekleyeceğiz; Özellikle, form kimlik doğrulamasını uygulama bölümüne bakacağız. Bu öğreticide oluşturacağız başlatdığımız Web uygulaması, basit form kimlik doğrulamasından üyelik ve rollere geçtiğimiz için sonraki öğreticilerde derlenmeye devam edecektir.
> 
> Bu konu hakkında daha fazla bilgi için bkz. [ASP.net Içinde temel form kimlik doğrulaması kullanma](../../../videos/authentication/using-basic-forms-authentication-in-aspnet.md).

## <a name="introduction"></a>Giriş

[Önceki öğreticide](security-basics-and-asp-net-support-vb.md) , ASP.NET tarafından sunulan çeşitli kimlik doğrulama, yetkilendirme ve Kullanıcı hesabı seçeneklerini tartıştık. Bu öğreticide, boyutundaydı tartışmadan uygulamaya ekleyeceğiz; Özellikle, form kimlik doğrulamasını uygulama bölümüne bakacağız. Bu öğreticide oluşturacağız başlatdığımız Web uygulaması, basit form kimlik doğrulamasından üyelik ve rollere geçtiğimiz için sonraki öğreticilerde derlenmeye devam edecektir.

Bu öğreticide, önceki öğreticide dokunduğumuz bir konu, Forms kimlik doğrulaması iş akışında ayrıntılı bir bakış ile başlar. Bunu izleyerek, form kimlik doğrulaması kavramlarını tanıtıtacak bir ASP.NET Web sitesi oluşturacağız. Daha sonra, siteyi Forms kimlik doğrulamasını kullanacak şekilde yapılandıracağız, basit bir oturum açma sayfası oluşturacak ve bir kullanıcının kimlik doğrulamasının yapılıp yapılmayacağını ve bu durumda oturum açtıkları Kullanıcı adının nasıl belirleneceğini öğreneceksiniz.

Form kimlik doğrulaması iş akışını anlamak, bir Web uygulamasında etkinleştirmek ve oturum açma ve oturum kapatma sayfalarının oluşturulması, Kullanıcı hesaplarını destekleyen bir ASP.NET uygulaması oluşturma ve bir Web sayfası aracılığıyla kullanıcıların kimliğini doğrulama konusunda önemli adımlardır. Bu nedenle ve bu öğreticiler bir diğeri üzerine inşa edildiğinden, geçmiş projelerde form kimlik doğrulamasını yapılandırma konusunda deneyim almış olsanız bile, Bu öğreticiye geçmeden önce Bu öğreticide geçiş yapmak için size tam olarak çalışmanız önerilir.

## <a name="understanding-the-forms-authentication-workflow"></a>Forms kimlik doğrulaması Iş akışını anlama

ASP.NET çalışma zamanı, bir ASP.NET sayfası veya ASP.NET Web hizmeti gibi bir ASP.NET kaynağı için isteği işlediğinde, istek yaşam döngüsü boyunca birkaç olay oluşturur. İsteğin çok başında ve çok sonunda oluşturulan, isteğin kimlik doğrulaması yapıldığında ve yetkilendirildiğinde, işlenmemiş bir özel durum durumunda oluşturulan bir olay ve bu şekilde gerçekleştirilen olaylar vardır. Olayların tüm listesini görmek için [HttpApplication nesnesinin olaylarına](https://msdn.microsoft.com/library/system.web.httpapplication_events.aspx)bakın.

*Http modülleri* , kodu istek yaşam döngüsünde belirli bir olaya yanıt olarak yürütülen yönetilen sınıflardır. ASP.NET, arka planda önemli görevleri gerçekleştiren bir dizi HTTP modülleriyle birlikte gelir. Özellikle Tartışmayla ilgili olan iki yerleşik HTTP modülü şunlardır:

- **[FormsAuthenticationModule](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)** -kullanıcının tanımlama bilgisi koleksiyonuna dahil edilen Forms kimlik doğrulama biletini inceleyerek Kullanıcı kimliğini doğrular. Hiçbir form kimlik doğrulama bileti yoksa, kullanıcı anonimdir.
- **[UrlAuthorizationModule](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)** -geçerli kullanıcının istenen URL 'ye erişim yetkisi olup olmadığını belirler. Bu modül, uygulamanın yapılandırma dosyalarında belirtilen yetkilendirme kurallarına danışarak yetkiyi belirler. ASP.NET, istenen dosya (ler) ACL 'Lerine danışarak yetkiyi belirleyen [FileAuthorizationModule 'ü](https://msdn.microsoft.com/library/system.web.security.fileauthorizationmodule.aspx) de içerir.

FormsAuthenticationModule, UrlAuthorizationModule (ve FileAuthorizationModule) çalıştırılmadan önce kullanıcının kimliğini doğrulamaya çalışır. İsteği yapan kullanıcının istenen kaynağa erişim yetkisi yoksa, yetkilendirme modülü isteği sonlandırır ve [HTTP 401 Yetkisiz](http://www.checkupdown.com/status/E401.html) durumunu döndürür. Windows kimlik doğrulama senaryolarında HTTP 401 durumu tarayıcıya döndürülür. Bu durum kodu tarayıcının, kullanıcının kimlik bilgilerini bir kalıcı iletişim kutusu aracılığıyla sormasını sağlar. Ancak, Forms kimlik doğrulaması ile, FormsAuthenticationModule bu durumu algıladığı ve kullanıcıyı bunun yerine oturum açma sayfasına ( [HTTP 302 yeniden yönlendirme](http://www.checkupdown.com/status/E302.html) durumu aracılığıyla) yeniden yönlendirmek üzere DEĞIŞTIRDIĞI için http 401 Yetkisiz durumu hiçbir şekilde tarayıcıya gönderilmez.

Oturum açma sayfasının sorumluluğu, kullanıcının kimlik bilgilerinin geçerli olup olmadığını ve bu durumda bir form kimlik doğrulama bileti oluşturup kullanıcıyı ziyaret edilmeye çalıştıkları sayfaya yeniden yönlendirmeyi belirlemektir. Kimlik doğrulama anahtarı, Web sitesindeki sayfalara sonraki isteklere dahil edilir ve bu da FormsAuthenticationModule Kullanıcı tanımlamak için kullanır.

[Forms kimlik doğrulaması Iş akışını ![](an-overview-of-forms-authentication-vb/_static/image2.png)](an-overview-of-forms-authentication-vb/_static/image1.png)

**Şekil 01**: Forms kimlik doğrulama iş akışı ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-forms-authentication-vb/_static/image3.png))

### <a name="remembering-the-authentication-ticket-across-page-visits"></a>Sayfa ziyaretlerinin tamamında kimlik doğrulama biletini anımsama

Oturum açtıktan sonra, kullanıcının siteye gözatarken oturum açmasını sağlamak için form kimlik doğrulama anahtarının her bir istekteki Web sunucusuna geri gönderilmesi gerekir. Bu, genellikle kimlik doğrulama bileti kullanıcının tanımlama bilgileri koleksiyonuna yerleştirilerek gerçekleştirilir. [Tanımlama bilgileri](http://en.wikipedia.org/wiki/HTTP_cookie) , kullanıcının bilgisayarında yer alan küçük metin dosyalarıdır ve tanımlama bilgisini oluşturan Web sitesine her Istek için http üstbilgilerinde iletilir. Bu nedenle, formlar kimlik doğrulama bileti oluşturulup tarayıcının tanımlama bilgilerinde depolandıktan sonra, bu siteye yapılan her bir sonraki ziyaret, kimlik doğrulama biletini istekle birlikte gönderir ve bu sayede kullanıcıyı tanımlar.

> [!NOTE]
> Her öğreticide kullanılan tanıtım Web uygulaması bir indirme olarak sunulmaktadır. Bu indirilebilir uygulama, .NET Framework sürüm 3,5 için hedeflenen Visual Web Developer 2008 ile oluşturulmuştur. Uygulama .NET 3,5 için hedeflendiğinden, Web. config dosyası, 3,5 'e özgü ek yapılandırma öğeleri içerir. Uzun hikaye kısa, henüz bilgisayarınıza .NET 3,5 ' i yüklemeniz gerekiyorsa indirilebilir web uygulaması önce, Web. config dosyasından 3,5 özel biçimlendirmeyi kaldırmadan çalışmaz.

Tanımlama bilgilerinin bir yönü, tarayıcının tanımlama bilgisini atma tarihi ve saati olan tarih ve saat olan süre sonu sayısıdır. Form kimlik doğrulaması tanımlama bilgisinin süresi dolmuşsa, kullanıcının kimliği artık doğrulanmaz ve bu nedenle anonim hale gelir. Bir Kullanıcı bir genel terminalden ziyaret edildiğinde, kendi tarayıcısını kapattıklarında kimlik doğrulama biletinin zaman dolmasını istiyoruz. Ancak evden ziyaret edildiğinde, aynı kullanıcı, her siteyi ziyaret ettiklerinde her seferinde oturum açmasını gerektirmeyen kimlik doğrulama biletinin tarayıcı yeniden başlatmaları arasında hatırlanmasını isteyebilir. Bu karar, oturum açma sayfasındaki Kullanıcı tarafından genellikle beni anımsa onay kutusu biçiminde yapılır. Adım 3 ' te oturum açma sayfasında beni anımsa onay kutusunu nasıl uygulayacağınızı inceleyeceğiz. Aşağıdaki öğreticide, kimlik doğrulama anahtarı zaman aşımı ayarları ayrıntılı olarak ele alınmaktadır.

> [!NOTE]
> Web sitesinde oturum açmak için kullanılan Kullanıcı aracısının tanımlama bilgilerini desteklememesi olasıdır. Böyle bir durumda ASP.NET, tanımlama bilgisi olmayan form kimlik doğrulama biletlerini kullanabilir. Bu modda, kimlik doğrulama anahtarı URL olarak kodlanır. Tanımlama bilgisi olmayan kimlik doğrulama biletlerinin ne zaman kullanıldığını ve sonraki öğreticide nasıl oluşturulup yönetileceğini inceleyeceğiz.

### <a name="the-scope-of-forms-authentication"></a>Form kimlik doğrulaması kapsamı

FormsAuthenticationModule, ASP.NET çalışma zamanının bir parçası olan yönetilen koddur. Microsoft 'un [Internet Information Services (IIS)](https://www.iis.net/) Web sunucusu sürüm 7 ' den önce, IIS 'nin http işlem hattı ve ASP.NET çalışma zamanının işlem hattı arasında ayrı bir engel vardı. Kısacası, IIS 6 ve önceki sürümlerde FormsAuthenticationModule yalnızca IIS 'den ASP.NET çalışma zamanına bir istek atandığında yürütülür. Varsayılan olarak IIS, statik içeriğin kendisini, HTML sayfaları ve CSS ve resim dosyaları gibi işler ve yalnızca. aspx,. asmx veya. ashx uzantılı bir sayfa istendiğinde ASP.NET çalışma zamanına yönelik istekleri devre dışı bırakır.

Ancak IIS 7, tümleşik IIS ve ASP.NET işlem hatları sağlar. Birkaç yapılandırma ayarı ile, IIS 7 ' yi *Tüm* Istekler için FormsAuthenticationModule çağırmak üzere ayarlayabilirsiniz. Ayrıca, IIS 7 ile herhangi bir türdeki dosyalar için URL Yetkilendirme kuralları tanımlayabilirsiniz. Daha fazla bilgi için [IIS6 ve IIS7 güvenliği](https://www.iis.net/learn/get-started/whats-new-in-iis-7/changes-in-security-between-iis-60-and-iis-7-and-above), [Web platformu GÜVENLIK](https://www.iis.net/learn/get-started/whats-new-in-iis-7/iis7-and-above-security-improvements)ve [IIS7 URL yetkilendirmesini anlama](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)arasındaki değişikliklere bakın.

Uzun hikaye kısaltması, IIS 7 ' den önceki sürümlerde yalnızca ASP.NET çalışma zamanı tarafından işlenen kaynakları korumak için form kimlik doğrulamasını kullanabilirsiniz. Benzer şekilde, URL Yetkilendirme kuralları yalnızca ASP.NET çalışma zamanı tarafından işlenen kaynaklara uygulanır. Ancak, IIS 7 ' de, FormsAuthenticationModule ve UrlAuthorizationModule ' yi IIS 'nin HTTP işlem hattına entegre etmek mümkündür. bu nedenle bu işlevselliği tüm isteklere genişleterek.

## <a name="step-1-creating-an-aspnet-website-for-this-tutorial-series"></a>1\. Adım: Bu öğretici serisi için bir ASP.NET Web sitesi oluşturma

Mümkün olan en geniş kitleye ulaşmak için, bu serinin tamamında oluşturulacak ASP.NET Web sitesi Microsoft 'un ücretsiz Visual Studio 2008, [Visual Web Developer 2008](https://www.microsoft.com/express/vwd/)sürümü ile oluşturulacaktır. SqlMembershipProvider kullanıcı mağazasını [Microsoft SQL Server 2005 Express Edition](https://msdn.microsoft.com/sql/Aa336346.aspx) veritabanında uygulayacağız. Visual Studio 2005 veya Visual Studio 2008 ' nin farklı bir sürümünü kullanıyorsanız veya SQL Server, endişelenmeyin, adımlar neredeyse aynı olur ve önemsiz olmayan tüm farklılıklar gösterilir.

Forms kimlik doğrulamasını yapılandırmadan önce, önce bir ASP.NET Web sitesine ihtiyacımız var. Yeni bir dosya sistemi tabanlı ASP.NET Web sitesi oluşturarak başlayın. Bunu gerçekleştirmek için, Visual Web Developer ' ı başlatın ve ardından Dosya menüsüne gidin ve yeni Web sitesi ' ni seçerek yeni Web sitesi iletişim kutusunu görüntüler. ASP.NET Web sitesi şablonunu seçin, konum açılan listesini dosya sistemi olarak ayarlayın, Web sitesini yerleştirmek için bir klasör seçin ve dili VB olarak ayarlayın. Bu, default. aspx ASP.NET sayfası, bir uygulama\_veri klasörü ve Web. config dosyası ile yeni bir Web sitesi oluşturur.

> [!NOTE]
> Visual Studio, iki proje yönetimi modunu destekler: Web sitesi projeleri ve Web uygulaması projeleri. Web sitesi projelerinin proje dosyası olmadığından, Web uygulaması projeleri Visual Studio .NET 2002/2003 'deki proje mimarisini taklit ederken, proje dosyası içerirler ve projenin kaynak kodunu,/bin klasörüne yerleştirilmiş tek bir derlemede derler. Visual Studio 2005 başlangıçta yalnızca desteklenen Web sitesi projeleri, ancak Web uygulaması proje modeli Service Pack 1 ile yeniden kullanılmaya başlandı; Visual Studio 2008, her iki proje modelini de sunmaktadır. Ancak, Visual Web Developer 2005 ve 2008 sürümleri yalnızca Web sitesi projelerini destekler. Web sitesi proje modelini kullanıyorum. Express olmayan bir sürüm kullanıyorsanız ve bunun yerine [Web uygulaması proje modelini](https://msdn.microsoft.com/library/aa730880(vs.80).aspx) kullanmak istiyorsanız, ekranınızda gördüklerinizle ilgili bazı tutarsızlıklar olabileceğini ve bu öğreticilerde sunulan ekran görüntülerini ve yönergeleri izlemeniz gereken adımları aklınızda bulundurun.

[![yeni bir dosya sistemi tabanlı Web sitesi oluşturma](an-overview-of-forms-authentication-vb/_static/image5.png)](an-overview-of-forms-authentication-vb/_static/image4.png)

**Şekil 02**: yeni bir dosya sistemi tabanlı Web sitesi oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-forms-authentication-vb/_static/image6.png))

### <a name="adding-a-master-page"></a>Ana sayfa ekleme

Ardından, site. Master adlı kök dizinde siteye yeni bir ana sayfa ekleyin. [Ana sayfalar](https://msdn.microsoft.com/library/wtxbf3hh.aspx) , sayfa geliştiricisinin ASP.NET sayfalarına uygulanabilecek site genelinde bir şablon tanımlamasına olanak tanır. Ana sayfaların başlıca avantajı, sitenin genel görünümünün tek bir konumda tanımlanıp tanımlanabileceği ve bu sayede sitenin düzeninin güncelleştirilmesini veya ince ayar olmasını kolaylaştırmaktır.

[Web sitesine site. Master adlı bir ana sayfa eklemek ![](an-overview-of-forms-authentication-vb/_static/image8.png)](an-overview-of-forms-authentication-vb/_static/image7.png)

**Şekil 03**: Web sitesine site. Master adlı bir ana sayfa ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-forms-authentication-vb/_static/image9.png))

Site genelinde sayfa mizanpajını ana sayfada tanımlayın. Tasarım görünümü kullanabilir ve gereken düzen veya Web denetimlerini ekleyebilir ya da biçimlendirmeyi el ile kaynak görünümüne ekleyebilirsiniz. Ana sayfamın düzeninden, *[ASP.NET 2,0 öğretici serisinde bulunan verilerle çalışmamda](../../data-access/index.md)* kullanılan düzeni taklit etmek için yapılandırılmış mıyım (bkz. Şekil 4). Ana sayfa, dosya stilinde (Bu öğreticinin ilişkili İndirilme dahil) tanımlanmış CSS ayarlarına sahip konumlandırma ve stiller için [geçişli stil sayfaları](http://www.w3schools.com/css/default.asp) kullanır. Aşağıda gösterilen biçimlendirmeden söylemeirken, CSS kuralları, gezinti &lt;div&gt;içeriğinin solunda görünmesi için mutlak olarak konumlandırılıp 200 piksellik sabit genişliğe sahip olacak şekilde tanımlanır.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample1.aspx)]

Ana sayfa, hem statik sayfa mizanpajını hem de ana sayfayı kullanan ASP.NET sayfaları tarafından düzenlenebilecek bölgeleri tanımlar. Bu içerik düzenlenebilir bölgeler, içerik &lt;div&gt;içinde görünebilen ContentPlaceHolder denetimiyle belirtilir. Ana sayfamız tek bir ContentPlaceHolder (MainContent) özelliğine sahiptir, ancak ana sayfanın birden çok Contentyertutucusu olabilir.

Yukarıda girilen biçimlendirme ile, Tasarım görünümü geçiş ana sayfanın yerleşimini gösterir. Bu ana sayfayı kullanan tüm ASP.NET sayfaları, MainContent bölgesi için biçimlendirmeyi belirtme özelliği ile bu Tekdüzen düzenine sahip olacaktır.

[Tasarım görünümü Ile görüntülenirken ana sayfayı ![](an-overview-of-forms-authentication-vb/_static/image11.png)](an-overview-of-forms-authentication-vb/_static/image10.png)

**Şekil 04**: Tasarım görünümü Ile görüntülenirken ana sayfa ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-forms-authentication-vb/_static/image12.png))

### <a name="creating-content-pages"></a>Içerik sayfaları oluşturma

Bu noktada, Web sitemizden bir default. aspx sayfası vardır, ancak yeni oluşturduğumuz ana sayfayı kullanmaz. Bir Web sayfasının bildirim temelli işaretlemesini bir ana sayfa kullanmak üzere işlemek mümkün olsa da, sayfada herhangi bir içerik yoksa sayfayı silmek ve bunu projeye yeniden eklemek daha kolay olur ve kullanılacak ana sayfayı belirterek. Bu nedenle, varsayılan. aspx öğesini projeden silerek başlayın.

Sonra, Çözüm Gezgini proje adına sağ tıklayın ve default. aspx adlı yeni bir Web formu eklemeyi seçin. Bu kez, ana sayfa seç onay kutusunu işaretleyin ve listeden site. Master ana sayfasını seçin.

[![yeni bir default. aspx sayfası eklemek için bir ana sayfa seçmeyi seçin](an-overview-of-forms-authentication-vb/_static/image14.png)](an-overview-of-forms-authentication-vb/_static/image13.png)

**Şekil 05**: bir ana sayfa seçerek yeni bir default. aspx sayfası ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-forms-authentication-vb/_static/image15.png))

[![site. Master ana sayfasını kullanın](an-overview-of-forms-authentication-vb/_static/image17.png)](an-overview-of-forms-authentication-vb/_static/image16.png)

**Şekil 06**: site. Master ana sayfasını kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-forms-authentication-vb/_static/image18.png))

> [!NOTE]
> Web uygulaması proje modeli kullanıyorsanız yeni öğe Ekle iletişim kutusunda bir ana sayfa seç onay kutusu yoktur. Bunun yerine, Web Içerik formu türünde bir öğe eklemeniz gerekir. Web Içerik formu seçeneğini belirledikten ve Ekle ' ye tıkladığınızda, Visual Studio, Şekil 6 ' da gösterilen aynı ana öğe seç iletişim kutusunu görüntüler.

Yeni default. aspx sayfasının bildirim temelli biçimlendirmesi, ana sayfa dosyasının yolunu ve ana sayfanın MainContent ContentPlaceHolder için bir Içerik denetimini belirten yalnızca bir @Page yönergesini içerir.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample2.aspx)]

Şimdilik default. aspx ' i boş bırakın. İçerik eklemek için Bu öğreticinin ilerleyen kısımlarında buna geri döneceksiniz.

> [!NOTE]
> Ana sayfamız, bir menü ya da başka bir gezinti arabirimine ilişkin bir bölüm içerir. Daha sonraki bir öğreticide böyle bir arabirim oluşturacağız.

## <a name="step-2-enabling-forms-authentication"></a>2\. Adım: form kimlik doğrulamasını etkinleştirme

ASP.NET Web sitesi oluşturulduğunda, bir sonraki göreviniz form kimlik doğrulamasını etkinleştirmektir. Uygulamanın kimlik doğrulama yapılandırması, Web. config dosyasındaki [&lt;authentication&gt; öğesi](https://msdn.microsoft.com/library/532aee0e.aspx) aracılığıyla belirtilir. &lt;Authentication&gt; öğesi, uygulama tarafından kullanılan kimlik doğrulama modelini belirten Mode adlı tek bir öznitelik içerir. Bu öznitelik aşağıdaki dört değerden birine sahip olabilir:

- **Windows** -önceki öğreticide açıklandığı gibi, bir uygulama Windows kimlik doğrulaması kullandığında, ziyaretçi kimlik doğrulaması için Web sunucusunun sorumluluğundadır ve bu genellikle temel, Özet veya tümleşik Windows kimlik doğrulaması aracılığıyla yapılır.
- **Formlar**-kullanıcıların kimliği bir Web sayfasındaki form aracılığıyla doğrulanır.
- **Passport**-kullanıcıların kimliği, Microsoft 'un Passport ağı kullanılarak doğrulanır.
- **Hiçbiri**-kimlik doğrulama modeli kullanılmıyor; Tüm ziyaretçiler anonimdir.

Varsayılan olarak, ASP.NET uygulamaları Windows kimlik doğrulamasını kullanır. Kimlik doğrulama türünü Forms kimlik doğrulaması olarak değiştirmek için, &lt;kimlik doğrulaması&gt; öğesinin mode özniteliğini Forms olarak değiştirmemiz gerekir.

Projeniz henüz bir Web. config dosyası içermiyorsa, Çözüm Gezgini proje adına sağ tıklayıp yeni öğe Ekle ' yi seçip bir Web yapılandırma dosyası ekleyerek bir tane ekleyin.

[![projeniz henüz Web. config Içermiyorsa, şimdi ekleyin](an-overview-of-forms-authentication-vb/_static/image20.png)](an-overview-of-forms-authentication-vb/_static/image19.png)

**Şekil 07**: projeniz henüz Web. config Içermiyorsa, şimdi ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-forms-authentication-vb/_static/image21.png))

Sonra, &lt;kimlik doğrulaması&gt; öğesini bulun ve Forms kimlik doğrulamasını kullanmak için güncelleştirin. Bu değişiklikten sonra, Web. config dosyanızın biçimlendirmesi şuna benzer olmalıdır:

[!code-xml[Main](an-overview-of-forms-authentication-vb/samples/sample3.xml)]

> [!NOTE]
> Web. config bir XML dosyası olduğundan, büyük/küçük harf önemli olur. Mode özniteliğini, büyük bir F ile formlar olarak ayarladığınızdan emin olun. Formlar gibi farklı bir büyük harf kullanırsanız, siteyi bir tarayıcı aracılığıyla ziyaret ederken bir yapılandırma hatası alırsınız.

&lt;Authentication&gt; öğesi, isteğe bağlı olarak, form kimlik doğrulamasına özgü ayarları içeren bir &lt;Forms&gt; alt öğe içerebilir. Şimdilik yalnızca varsayılan form kimlik doğrulama ayarlarını kullanalım. Bir sonraki öğreticide,&gt; alt öğe &lt;formları daha ayrıntılı bir şekilde araştıracağız.

## <a name="step-3-building-the-login-page"></a>3\. Adım: oturum açma sayfası oluşturma

Form kimlik doğrulamasını desteklemek için, Web sitemiz bir oturum açma sayfasına ihtiyaç duyuyor. Forms kimlik doğrulaması Iş akışını anlama bölümünde anlatıldığı gibi, FormsAuthenticationModule, görüntüleme yetkisine sahip olmadıkları bir sayfaya erişmeyi denediklerinde kullanıcıyı otomatik olarak oturum açma sayfasına yönlendirecektir. Anonim kullanıcılara oturum açma sayfası bağlantısını görüntüleyen ASP.NET Web denetimleri de vardır. Bu, soru, oturum açma sayfasının URL 'SI nedir?

Varsayılan olarak, Forms kimlik doğrulama sistemi, oturum açma sayfasının Login. aspx olarak adlandırılması ve Web uygulamasının kök dizinine yerleştirilmesi bekler. Farklı bir oturum açma sayfası URL 'SI kullanmak istiyorsanız, bunu Web. config içinde belirterek yapabilirsiniz. Bunu sonraki öğreticide nasıl yapacağız.

Oturum açma sayfası üç sorumluluklara sahiptir:

1. Ziyaretçilerin kimlik bilgilerini girmesini sağlayan bir arabirim sağlayın.
2. Gönderilen kimlik bilgilerinin geçerli olup olmadığını belirleme.
3. Form kimlik doğrulama bileti oluşturarak Kullanıcı oturumunu açın.

### <a name="creating-the-login-pages-user-interface"></a>Oturum açma sayfasının Kullanıcı arabirimini oluşturma

İlk görevi kullanmaya başlayalım. Sitenin Login. aspx adlı kök dizinine yeni bir ASP.NET sayfası ekleyin ve bunu site. Master ana sayfası ile ilişkilendirin.

[![Login. aspx adlı yeni bir ASP.NET sayfası ekleyin](an-overview-of-forms-authentication-vb/_static/image23.png)](an-overview-of-forms-authentication-vb/_static/image22.png)

**Şekil 08**: login. aspx adlı yeni bir ASP.NET sayfası ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-forms-authentication-vb/_static/image24.png))

Tipik oturum açma sayfası arabirimi, biri Kullanıcı adı, biri parola için ve formu göndermek için bir düğme olmak üzere iki metin kutularının oluşur. İşaretliyse Web siteleri, denetlenen bir beni hatırla onay kutusunu, işaretlenirse, tarayıcı yeniden başlatmalarının elde ettiği sonuç kimlik doğrulama biletini içerir.

Login. aspx öğesine iki metin kutuları ekleyin ve KIMLIK özelliklerini sırasıyla Kullanıcı adı ve parola olarak ayarlayın. Parolanın TextMode özelliğini de Password olarak ayarlayın. Sonra, bir CheckBox denetimi ekleyin, ID özelliğini RememberMe olarak ve Text özelliğini ise beni anımsa olarak ayarlar. Bundan sonra Text özelliği Login olarak ayarlanmış olan LoginButton adlı bir düğme ekleyin. Son olarak, bir etiket Web denetimi ekleyip ID özelliğini ınvalidcredentialsmessage olarak ayarlarsanız, Text özelliği kullanıcı adınızla veya parolanızla geçersiz olur. Lütfen yeniden deneyin., ForeColor özelliği Red ve Visible özelliği false olarak ayarlandı.

Bu noktada ekranınızın, Şekil 9 ' da ekran görüntüsüne benzer olması gerekir ve Sayfanızın bildirime dayalı sözdizimi aşağıdaki gibi görünmelidir:

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample4.aspx)]

[Oturum açma sayfası ![Iki metin kutusu, bir onay kutusu, düğme ve etiket Içerir](an-overview-of-forms-authentication-vb/_static/image26.png)](an-overview-of-forms-authentication-vb/_static/image25.png)

**Şekil 09**: oturum açma sayfası Iki metin kutusu, bir onay kutusu, düğme ve bir etiket içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-forms-authentication-vb/_static/image27.png))

Son olarak, LoginButton 'ın Click olayı için bir olay işleyicisi oluşturun. Tasarımcıda Bu olay işleyicisini oluşturmak için düğme denetimini çift tıklayın.

### <a name="determining-if-the-supplied-credentials-are-valid"></a>Sağlanan kimlik bilgilerinin geçerli olup olmadığı belirleniyor

Şimdi düğmenin Click olay işleyicisine görev 2 ' yi uygulamanız gerekir. sağlanan kimlik bilgilerinin geçerli olup olmadığını belirleme. Bunu yapmak için, belirtilen kimlik bilgilerinin bilinen kimlik bilgileriyle eşleşip eşleşmediğine belirleyebilmemiz için tüm kullanıcıların kimlik bilgilerini tutan bir kullanıcı deposu olması gerekir.

ASP.NET 2,0 ' den önce, geliştiriciler hem kendi Kullanıcı mağazalarını uygulamaktan hem de kodu yazarken, belirtilen kimlik bilgilerini depoya göre doğrulamaya sorumludur. Çoğu geliştirici Kullanıcı mağazasını bir veritabanında uygular, Kullanıcı adı, parola, e-posta, LastLoginDate vb. gibi sütunlara sahip kullanıcılar adlı bir tablo oluşturur. Bu tabloda, Kullanıcı hesabı başına bir kayıt olur. Kullanıcının sağladığı kimlik bilgilerinin doğrulanması, eşleşen bir Kullanıcı adı için veritabanını sorgulamayı ve sonra veritabanındaki parolanın sağlanan parolaya uygun olduğundan emin olmayı içerir.

ASP.NET 2,0 ile, geliştiriciler Kullanıcı mağazasını yönetmek için üyelik sağlayıcılarından birini kullanmalıdır. Bu öğretici serisinde, kullanıcı deposu için bir SQL Server veritabanı kullanan SqlMembershipProvider 'ı kullanacağız. SqlMembershipProvider kullanırken, sağlayıcı tarafından beklenen tabloları, görünümleri ve saklı yordamları içeren belirli bir veritabanı şeması uygulamamız gerekir. SQL Server öğreticide *[Üyelik şeması oluşturma](../membership/creating-the-membership-schema-in-sql-server-vb.md)* bölümünde bu şemayı nasıl uygulayacağınızı inceleyeceğiz. Üyelik sağlayıcısı varken, kullanıcının kimlik bilgilerini doğrulamak, Kullanıcı *adı* ve *parola* birleşiminin geçerliliğini belirten bir Boole değeri döndüren [Üyelik sınıfının](https://msdn.microsoft.com/library/system.web.security.membership.aspx) [ValidateUser (*Kullanıcı adı*, *parola*) yöntemini](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx)çağırmak kadar basittir. Zaten SqlMembershipProvider 'ın Kullanıcı deposunu uygulamadığımızda, üyelik sınıfının ValidateUser metodunu şu anda kullanmıyoruz.

Kendi özel kullanıcılar veritabanı tabloımızı oluşturma süresi yerine (SqlMembershipProvider uygulandıktan sonra kullanımdan kalktı), bunun yerine oturum açma sayfasının içinde geçerli kimlik bilgilerini sabit olarak kodlayalım. LoginButton ' ın Click olay işleyicisine aşağıdaki kodu ekleyin:

[!code-vb[Main](an-overview-of-forms-authentication-vb/samples/sample5.vb)]

Gördüğünüz gibi, üç geçerli kullanıcı hesabı vardır: Scott, Jisun ve Sam; üçü de aynı parolaya sahiptir (parola). Kod, geçerli bir Kullanıcı adı ve parola eşleşmesi bulmak için Kullanıcı ve parola dizileri boyunca döngü yapılır. Kullanıcı adı ve parola geçerliyse, kullanıcıyı oturum açıp uygun sayfaya yönlendirmemiz gerekir. Kimlik bilgileri geçersizse, ınvalidcredentialsmessage etiketini görüntüleriz.

Kullanıcı geçerli kimlik bilgileri girdiğinde ilgili sayfaya yönlendirildiğine bahsetmiştim. Ne olmasa da uygun sayfa nedir? Kullanıcı, görüntüleme yetkisine sahip olmayan bir sayfayı ziyaret ettiğinde, FormsAuthenticationModule otomatik olarak oturum açma sayfasına yönlendirir. Bunu yaparken, istenen URL 'yi ReturnUrl parametresi aracılığıyla QueryString içinde içerir. Diğer bir deyişle, bir Kullanıcı ProtectedPage. aspx ' i ziyaret etmeyi denediğinde ve bunu yapmak için yetkilendirilmeyen FormsAuthenticationModule, bunları şu şekilde yönlendirecektir:

Login. aspx? ReturnUrl = ProtectedPage. aspx

Başarıyla oturum açtıktan sonra, Kullanıcı ProtectedPage. aspx 'e yeniden yönlendirilmelidir. Alternatif olarak, kullanıcılar kendi oyları üzerinde oturum açma sayfasını ziyaret edebilir. Bu durumda, kullanıcıya oturum açtıktan sonra, kök klasörün default. aspx sayfasına gönderilmesi gerekir.

### <a name="logging-in-the-user"></a>Kullanıcı oturumu açma

Sağlanan kimlik bilgilerinin geçerli olduğu varsayıldığında, bir form kimlik doğrulama bileti oluşturmanız ve bu nedenle kullanıcıya sitede oturum açmanız gerekir. [System. Web. Security ad alanındaki](https://msdn.microsoft.com/library/system.web.security.aspx) [FormsAuthentication sınıfı](https://msdn.microsoft.com/library/system.web.security.formsauthentication.aspx) , kullanıcıların oturum açmasını ve Forms kimlik doğrulama sistemi aracılığıyla oturum açmasını sağlayan assıralanan yöntemler sağlar. FormsAuthentication sınıfında çeşitli yöntemler olsa da, bu kavşakta 'te ilgilendiğiniz üç yöntem şunlardır:

- [GetAuthCookie (*Kullanıcı*adı, *persistcookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.getauthcookie.aspx) -sağlanan ad *Kullanıcı*adı için bir form kimlik doğrulama bileti oluşturur. Ardından, bu yöntem kimlik doğrulama anahtarının içeriğini tutan bir HttpCookie nesnesi oluşturur ve döndürür. *Persistcookie* değeri true ise kalıcı tanımlama bilgisi oluşturulur.
- [SetAuthCookie (*Kullanıcı adı*, *persistcookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) -form kimlik doğrulama tanımlama bilgisini oluşturmak için GetAuthCookie (*UserName*, *persistcookie*) yöntemini çağırır. Bu yöntem daha sonra GetAuthCookie tarafından döndürülen tanımlama bilgisini Cookies koleksiyonuna ekler (tanımlama bilgileri tabanlı formlar kimlik doğrulamasının kullanıldığı varsayılarak), aksi takdirde, bu yöntem, tanımlama bilgisi olmayan bilet mantığını işleyen bir iç sınıf çağırır).
- [RedirectFromLoginPage (*Kullanıcı adı*, *persistcookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.redirectfromloginpage.aspx) -bu yöntem, SetAuthCookie (*UserName*, *persistcookie*) öğesini çağırır ve ardından kullanıcıyı uygun sayfaya yönlendirir.

Tanımlama bilgisini tanımlama bilgisi koleksiyonuna yazmadan önce kimlik doğrulama biletini değiştirmeniz gerektiğinde GetAuthCookie yararlı olur. , Forms kimlik doğrulama bileti oluşturmak ve tanımlama bilgileri koleksiyonuna eklemek istiyorsanız SetAuthCookie yararlı olur, ancak kullanıcıyı uygun sayfaya yönlendirmek istemezsiniz. Belki de oturum açma sayfasında tutmak veya farklı bir sayfaya göndermek isteyebilirsiniz.

Kullanıcıya oturum açıp uygun sayfaya yönlendirdiğinizden, RedirectFromLoginPage ' i kullanalım. İki açıklamalı TODO satırını aşağıdaki kod satırıyla değiştirerek LoginButton 'ın Click olay işleyicisini güncelleştirin:

FormsAuthentication. RedirectFromLoginPage (Kullanıcı adı. metin, RememberMe. Checked)

Form kimlik doğrulama bileti oluştururken, form kimlik doğrulaması bileti *Kullanıcı adı* parametresi Için Kullanıcı adı metin kutusu Text özelliğini ve *Persistcookie* parametresi için RememberMe onay kutusunun denetlenen durumunu kullanırız.

Oturum açma sayfasını test etmek için bir tarayıcıda ziyaret edin. Nope 'nin Kullanıcı adı ve yanlış parolası gibi geçersiz kimlik bilgilerini girerek başlayın. Oturum açma düğmesine tıklandıktan sonra bir geri gönderme gerçekleşir ve ınvalidcredentialsmessage etiketi görüntülenecektir.

[Geçersiz kimlik bilgileri girilirken ınvalidcredentialsmessage etiketi ![görüntülenir](an-overview-of-forms-authentication-vb/_static/image29.png)](an-overview-of-forms-authentication-vb/_static/image28.png)

**Şekil 10**: geçersiz kimlik bilgileri girilirken ınvalidcredentialsmessage etiketi görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-forms-authentication-vb/_static/image30.png))

Sonra, geçerli kimlik bilgileri girin ve oturum aç düğmesine tıklayın. Bu kez geri gönderme işlemi bir form kimlik doğrulama bileti oluşturulduğunda ve otomatik olarak varsayılan. aspx 'e yeniden yönlendiriliyorsunuz. Bu noktada, Web sitesinde oturum açmış olursunuz, ancak şu anda oturum açtığınızı belirten hiçbir görsel ipucu yok. Adım 4 ' te, bir kullanıcının oturum açıp açmayıp belirlememe ve sayfayı ziyaret eden kullanıcıyı nasıl tanımlayabileceği hakkında bilgi vereceğiz.

5\. adım, bir kullanıcıyı Web sitesinden günlüğe kaydetme tekniklerini inceler.

### <a name="securing-the-login-page"></a>Oturum açma sayfasının güvenliğini sağlama

Kullanıcı kimlik bilgilerini girdiğinde ve oturum açma sayfası formunu gönderdiğinde, parola dahil olmak üzere kimlik bilgileri, *düz metin*olarak Internet üzerinden Web sunucusuna iletilir. Bu, tüm korsanlarının ağ trafiğinin Kullanıcı adını ve parolayı göremeyeceğini gösterir. Bunu engellemek için [Güvenli Yuva katmanları (SSL)](http://en.wikipedia.org/wiki/Secure_Sockets_Layer)kullanarak ağ trafiğini şifrelemek gereklidir. Bu, kimlik bilgilerinin (Ayrıca tüm sayfanın HTML işaretlemesi) Web sunucusu tarafından alınana kadar tarayıcıdan ayrıldıklarından emin olur.

Web siteniz hassas bilgiler içermiyorsa, oturum açma sayfasında ve kullanıcının parolasının düz metin olarak kablo üzerinden gönderilebileceği diğer sayfalarda SSL kullanmanız gerekir. Form kimlik doğrulama biletini güvenli hale getirmeniz gerekmez, çünkü varsayılan olarak hem şifreli hem de dijital olarak imzalanır (değişiklik yapılmasını engellemek için). Aşağıdaki öğreticide, Forms kimlik doğrulama bileti güvenliği hakkında daha kapsamlı bir tartışma sunulmaktadır.

> [!NOTE]
> Birçok finansal ve tıp web sitesi, kimliği doğrulanmış kullanıcıların erişebileceği *Tüm* sayfalarda SSL kullanmak üzere yapılandırılmıştır. Böyle bir Web sitesi oluşturuyorsanız Forms kimlik doğrulama sisteminin yalnızca güvenli bir bağlantı üzerinden iletilmesi için Forms kimlik doğrulama sistemini yapılandırabilirsiniz. Sonraki öğreticide, *[Forms kimlik doğrulaması yapılandırması ve gelişmiş konular](../membership/creating-the-membership-schema-in-sql-server-vb.md)* 'daki çeşitli form kimlik doğrulama yapılandırma seçeneklerine bakacağız.

## <a name="step-4-detecting-authenticated-visitors-and-determining-their-identity"></a>4\. Adım: kimliği doğrulanmış ziyaretçileri algılama ve kimliklerini belirleme

Bu noktada, form kimlik doğrulamasını etkinleştirdik ve bir ilkel oturum açma sayfası oluşturdunuz, ancak kullanıcının kimlik doğrulamasının yapılıp yapılmayacağını veya anonim olduğunu nasıl belirleyebiliriz. Belirli senaryolarda, kimliği doğrulanmış veya anonim bir kullanıcının sayfayı ziyaret edip etmediğine bağlı olarak farklı verileri veya bilgileri göstermek isteyebilirsiniz. Üstelik, kimliği doğrulanmış kullanıcının kimliğini bilmemiz gerekir.

Bu teknikleri göstermek için mevcut default. aspx sayfasını artalım. Default. aspx ' de iki panel denetimi ekleyin, bir tane bir kimlik doğrulayan Tedmessagepanel ve başka bir AnonymousMessagePanel adı. İlk panelde WelcomeBackMessage adlı bir etiket denetimi ekleyin. İkinci panelde bir köprü denetimi ekleyin, Text özelliğini oturum aç ve NavigateUrl özelliğini ~/Login.exe olarak ayarlayın. Bu noktada, default. aspx için bildirim temelli biçimlendirme aşağıdakine benzer olmalıdır:

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample6.aspx)]

Şu anda tahmin ettiğiniz için buradaki fikir, yalnızca kimliği doğrulanmış ziyaretçilere ve yalnızca AnonymousMessagePanel 'e anonim ziyaretçilere olan kimlik doğrulamalı Tedmessagepanel 'i görüntülemektir. Bunu gerçekleştirmek için, kullanıcının oturum açmış olmasına bağlı olarak bu panellerin görünür özelliklerini ayarlaması gerekir.

[Request. IsAuthenticated özelliği](https://msdn.microsoft.com/library/system.web.httprequest.isauthenticated.aspx) , isteğin doğrulanıp doğrulanmadığını gösteren bir Boole değeri döndürür. Aşağıdaki kodu sayfa\_Load olay işleyicisi kodu olarak girin:

[!code-vb[Main](an-overview-of-forms-authentication-vb/samples/sample7.vb)]

Bu kodla birlikte, bir tarayıcıdan default. aspx adresini ziyaret edin. Henüz oturum açmanız gerektiğini varsayarsak, oturum açma sayfasına bir bağlantı görürsünüz (bkz. Şekil 11). Bu bağlantıya tıklayın ve sitede oturum açın. Adım 3 ' te gördüğünüz gibi, kimlik bilgilerinizi girdikten sonra default. aspx ' e geri dönersiniz, ancak bu kez sayfada hoş geldiniz geri alınacaktır! ileti (bkz. Şekil 12).

[Anonim olarak ziyaret edildiğinde ![bağlantıda bir oturum görüntülenir](an-overview-of-forms-authentication-vb/_static/image32.png)](an-overview-of-forms-authentication-vb/_static/image31.png)

**Şekil 11**: anonim olarak ziyaret edildiğinde bir oturum açma bağlantısı görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-forms-authentication-vb/_static/image33.png))

[![kimliği doğrulanmış kullanıcılara hoş geldiniz geri ödeme gösteriliyor! İleti](an-overview-of-forms-authentication-vb/_static/image35.png)](an-overview-of-forms-authentication-vb/_static/image34.png)

**Şekil 12**: kimliği doğrulanmış kullanıcılar, hoş geldiniz geri görüntülenir! İleti ([tam boyutlu görüntüyü görüntülemek Için tıklayın](an-overview-of-forms-authentication-vb/_static/image36.png))

Şu anda oturum açmış olan kullanıcının kimliğini [HttpContext nesnesinin](https://msdn.microsoft.com/library/system.web.httpcontext.aspx) [User özelliği](https://msdn.microsoft.com/library/system.web.httpcontext.user.aspx)aracılığıyla belirleyebiliriz. HttpContext nesnesi, geçerli istek hakkındaki bilgileri temsil eder ve diğer yaygın ASP.NET nesneleri için yanıt, Istek ve oturum olarak diğerleri arasında giriş olur. User özelliği, geçerli HTTP isteğinin güvenlik bağlamını temsil eder ve [IPrincipal arabirimini](https://msdn.microsoft.com/library/system.security.principal.iprincipal.aspx)uygular.

Kullanıcı özelliği FormsAuthenticationModule tarafından ayarlanır. Özellikle, FormsAuthenticationModule gelen istekte bir Forms kimlik doğrulama bileti bulduğunda, yeni bir GenericPrincipal nesnesi oluşturur ve bunu Kullanıcı özelliğine atar.

Principal nesneleri (GenericPrincipal gibi), kullanıcının kimliği ve ait oldukları roller hakkında bilgi sağlar. IPrincipal arabirimi iki üyeyi tanımlar:

- [Idirole (*roleName*)](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole.aspx) -asıl değerin belirtilen role ait olup olmadığını gösteren bir Boole değeri döndüren bir yöntem.
- [Identity](https://msdn.microsoft.com/library/system.security.principal.iprincipal.identity.aspx) - [IIdentity arabirimini](https://msdn.microsoft.com/library/system.security.principal.iidentity.aspx)uygulayan bir nesne döndüren özellik. IIdentity arabirimi üç özelliği tanımlar: [AuthenticationType](https://msdn.microsoft.com/library/system.security.principal.iidentity.authenticationtype.aspx), [IsAuthenticated](https://msdn.microsoft.com/library/system.security.principal.iidentity.isauthenticated.aspx)ve [Name](https://msdn.microsoft.com/library/system.security.principal.iidentity.name.aspx).

Aşağıdaki kodu kullanarak geçerli ziyaretçi adını belirleyebiliriz:

Dim currentUsersName as String = User.Identity.Name

Form kimlik doğrulaması kullanılırken, GenericPrincipal 'ın Identity özelliği için bir [FormsIdentity nesnesi](https://msdn.microsoft.com/library/system.web.security.formsidentity.aspx) oluşturulur. FormsIdentity sınıfı her zaman, AuthenticationType özelliği için dize formlarını ve IsAuthenticated özelliği için true değerini döndürür. Name özelliği, Forms kimlik doğrulama bileti oluşturulurken belirtilen kullanıcı adını döndürür. Bu üç özelliğe ek olarak, FormsIdentity, [anahtar özelliği](https://msdn.microsoft.com/library/system.web.security.formsidentity.ticket.aspx)aracılığıyla temel alınan kimlik doğrulama biletlerine erişimi içerir. Bilet özelliği, [FormsAuthenticationTicket](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.aspx)türünde bir nesne döndürür, bu, Expiration, IsPersistent, IssueDate, ad vb. gibi özelliklere sahiptir.

Burada ele almanız gereken önemli nokta, FormsAuthentication. GetAuthCookie (*UserName*, *Persistcookie*), FormsAuthentication. SetAuthCookie tanımlama*bilgisinde (username*, *Persistcookie*) ve FormsAuthentication. redirecuthloginpage (*username*, *persistcookie*) yöntemlerinde belirtilen değer olan User.Identity.Name tarafından döndürülen değere sahip. Ayrıca, bu yöntemler tarafından oluşturulan kimlik doğrulama bileti, User. Identity bir FormsIdentity nesnesine ve ardından bilet özelliğine erişerek kullanılabilir:

Dim IIdentity as FormsIdentity = CType (User. Identity, FormsIdentity)

Dim authTicket as FormsAuthenticationTicket = IBU. Ticket

Default. aspx dosyasında daha kişiselleştirilmiş bir ileti sağlayabiliriz. \_, olay işleyicisini Yükle ' yi, WelcomeBackMessage etiketinin Text özelliğinin String 'e hoş geldiniz geri geldin, *UserName*! olarak atanabilmesi için güncelleştirin.

WelcomeBackMessage. Text = "hoş geldiniz", "&amp; User.Identity.Name &amp;"! "

Şekil 13, bu değişikliğin etkisini gösterir (Kullanıcı Scott olarak oturum açarken).

[Hoş geldiniz Iletisi ![Şu anda oturum açmış olan kullanıcının adını Içerir](an-overview-of-forms-authentication-vb/_static/image38.png)](an-overview-of-forms-authentication-vb/_static/image37.png)

**Şekil 13**: hoş geldiniz Iletisi Şu anda oturum açmış olan kullanıcının adını içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-forms-authentication-vb/_static/image39.png))

### <a name="using-the-loginview-and-loginname-controls"></a>LoginView ve LoginName denetimlerini kullanma

Kimliği doğrulanmış ve anonim kullanıcılara farklı içerik görüntüleme yaygın bir gereksinimdir; Bu nedenle, şu anda oturum açmış olan kullanıcının adını görüntülüyor. Bu nedenle ASP.NET, Şekil 13 ' te gösterilen işlevselliği, ancak tek bir kod satırı yazmak zorunda kalmadan sağlayan iki Web denetimi içerir.

[LoginView denetimi](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx) , kimliği doğrulanmış ve anonim kullanıcılara farklı verilerin görüntülenmesini kolaylaştıran şablon tabanlı bir Web denetimidir. LoginView, önceden tanımlanmış iki şablonu içerir:

- AnonymousTemplate-bu şablona eklenen tüm biçimlendirmeler yalnızca anonim ziyaretçilere görüntülenir.
- LoggedInTemplate-bu şablonun biçimlendirmesi yalnızca kimliği doğrulanmış kullanıcılar için gösteriliyor.

Şimdi sitenizin ana sayfasına, site. Master öğesine LoginView denetimi ekleyelim. Yalnızca LoginView denetimi eklemek yerine, hem yeni bir ContentPlaceHolder denetimi ekleyelim hem de LoginView denetimini bu yeni ContentPlaceHolder içine koyalım. Bu karar için daha kısa bir süre içinde görünür hale gelir.

> [!NOTE]
> AnonymousTemplate ve LoggedInTemplate 'e ek olarak, LoginView denetimi role özgü Şablonlar içerebilir. Role özgü şablonlar yalnızca belirtilen role ait olan kullanıcılar için biçimlendirme gösterir. Sonraki bir öğreticide, LoginView denetiminin rol tabanlı özelliklerini inceleyeceğiz.

Gezinti &lt;div&gt; öğesi içindeki ana sayfaya bir ContentPlaceHolder adlı bir ContentPlaceHolder ekleyerek başlayın. Araç kutusu ' ndan bir ContentPlaceHolder denetimini kaynak görünümüne sürükleyebilirsiniz ve elde edilen biçimlendirmeyi TODO: Menü ' ye doğru yerleştirebilirsiniz.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample8.aspx)]

Ardından, LoginContent ContentPlaceHolder içinde bir LoginView denetimi ekleyin. Ana sayfanın ContentPlaceHolder denetimlerine yerleştirilmiş içerikler, ContentPlaceHolder için *varsayılan içerik* olarak değerlendirilir. Diğer bir deyişle, bu ana sayfayı kullanan ASP.NET sayfaları her bir ContentPlaceHolder için kendi içeriğini belirtebilir veya ana sayfanın varsayılan içeriğini kullanabilir.

LoginView ve oturum açmayla ilgili diğer denetimler, araç kutusunun oturum açma sekmesinde bulunur.

[Araç kutusundaki LoginView denetimini ![](an-overview-of-forms-authentication-vb/_static/image41.png)](an-overview-of-forms-authentication-vb/_static/image40.png)

**Şekil 14**: araç kutusundaki LoginView denetimi ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-forms-authentication-vb/_static/image42.png))

Sonra, LoginView denetiminden hemen sonra, ancak ContentPlaceHolder içinde iki &lt;br/&gt; öğesi ekleyin. Bu noktada, gezinti &lt;div&gt; öğesinin biçimlendirmesi aşağıdaki gibi görünmelidir:

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample9.aspx)]

LoginView şablonları tasarımcıdan veya bildirime dayalı biçimlendirmeden tanımlanabilir. Visual Studio tasarımcısında, bir açılan listede yapılandırılmış şablonları listeleyen LoginView ' ın akıllı etiketini genişletin. Merhaba metin yazarak, AnonymousTemplate 'e yabancıyazın; sonra, bir köprü denetimi ekleyin ve Text ve NavigateUrl özelliklerini sırasıyla oturum açıp ~/Login.aspx olarak ayarlayın.

AnonymousTemplate 'i yapılandırdıktan sonra LoggedInTemplate 'e geçin ve "hoş geldiniz" metnini girin. Ardından araç kutusundan bir LoginName denetimini LoggedInTemplate öğesine sürükleyerek "hoş geldiniz" metninin hemen sonrasına yerleştirebilirsiniz. [LoginName denetimi](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginname.aspx), adının gösterdiği gibi, o anda oturum açmış kullanıcının adını görüntüler. Dahili olarak, LoginName denetimi yalnızca User.Identity.Name özelliğini verir

Bu eklemeleri LoginView şablonlarına yaptıktan sonra, biçimlendirme aşağıdakine benzer olmalıdır:

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample10.aspx)]

Site. Master ana sayfasına bu ekleme ile, Web sitemizden her sayfa, kullanıcının kimliğinin doğrulanmadığına bağlı olarak farklı bir ileti görüntüler. Şekil 15, Kullanıcı Jisun tarafından bir tarayıcı aracılığıyla ziyaret edildiğinde varsayılan. aspx sayfasını gösterir. Geri hoş geldiniz, Jisun iletisi iki kez yinelenir: sol taraftaki ana sayfanın gezinti bölümünde (yeni eklediğimiz LoginView denetimi aracılığıyla) ve bir kez default. aspx içerik alanında (panel denetimleri ve programlama mantığı aracılığıyla).

[![LoginView denetimi, hoş geldiniz 'i, Jisun 'yi görüntüler.](an-overview-of-forms-authentication-vb/_static/image44.png)](an-overview-of-forms-authentication-vb/_static/image43.png)

**Şekil 15**: LoginView denetimi, hoş geldiniz geri, Jisun 'yi görüntüler. ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](an-overview-of-forms-authentication-vb/_static/image45.png))

LoginView öğesini ana sayfaya eklediğimiz için, sitemizdeki her sayfada görünebilir. Ancak, bu iletiyi göstermek istemediğimiz Web sayfaları olabilir. Bu tür bir sayfa, oturum açma sayfasına bir bağlantı olmadığı için oturum açma sayfasıdır. LoginView denetimini ana sayfada ContentPlaceHolder öğesine yerleştirdiğimiz için içerik sayfamızda bu varsayılan biçimlendirmeyi geçersiz kılarız. Login. aspx ' i açın ve tasarımcıya gidin. Ana sayfada bulunan LoginContent için login. aspx içinde açıkça bir Içerik denetimi tanımlamadık, oturum açma sayfası bu ContentPlaceHolder için ana sayfanın varsayılan işaretlemesini gösterir. Bunu tasarımcı aracılığıyla görebilirsiniz-LoginContent ContentPlaceHolder varsayılan biçimlendirmeyi gösterir (LoginView denetimi).

[Oturum açma sayfası ![ana sayfanın LoginContent ContentPlaceHolder öğesinin varsayılan Içeriğini gösterir](an-overview-of-forms-authentication-vb/_static/image47.png)](an-overview-of-forms-authentication-vb/_static/image46.png)

**Şekil 16**: oturum açma sayfası, ana sayfanın Logincontent ContentPlaceHolder öğesinin varsayılan içeriğini gösterir ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-forms-authentication-vb/_static/image48.png))

LoginContent ContentPlaceHolder için varsayılan biçimlendirmeyi geçersiz kılmak için, tasarımcıda bölgeye sağ tıklayıp bağlam menüsünden Özel Içerik oluştur seçeneğini belirlemeniz yeterlidir. (Visual Studio 2008 kullanırken ContentPlaceHolder, seçildiğinde aynı seçeneği sunan akıllı bir etiket içerir.) Bu, sayfanın biçimlendirmesine yeni bir Içerik denetimi ekler ve bu sayede Bu sayfa için özel içerik tanımlamamıza izin verir. Buraya bir özel ileti ekleyebilirsiniz, örneğin, lütfen oturum açın, ancak bunu boş bırakalım.

> [!NOTE]
> Visual Studio 2005 ' de, özel içerik oluşturmak ASP.NET sayfasında boş bir Içerik denetimi oluşturur. Ancak Visual Studio 2008 ' de, özel içerik oluşturma ana sayfanın varsayılan içeriğini yeni oluşturulan Içerik denetimine kopyalar. Visual Studio 2008 kullanıyorsanız, yeni Içerik denetimini oluşturduktan sonra ana sayfadan kopyalanmış içeriği temizlediğinizden emin olun.

Şekil 17, bu değişikliği yaptıktan sonra bir tarayıcıdan ziyaret edildiğinde Login. aspx sayfasını gösterir. Varsayılan. aspx ' i ziyaret edildiğinde olduğu gibi, sol gezinti &lt;div&gt; bir Hello, Stranger veya hoş geldiniz yok, *Kullanıcı adı* iletisi yok.

[Oturum açma sayfası ![varsayılan LoginContent ContentPlaceHolder 'ın Işaretlemesini gizler](an-overview-of-forms-authentication-vb/_static/image50.png)](an-overview-of-forms-authentication-vb/_static/image49.png)

**Şekil 17**: oturum açma sayfası varsayılan Logincontent ContentPlaceHolder 'ın işaretlemesini gizler ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-forms-authentication-vb/_static/image51.png))

## <a name="step-5-logging-out"></a>5\. Adım: oturumu kapatma

Adım 3 ' te, bir kullanıcının siteye oturum açmasını sağlamak için bir oturum açma sayfası oluşturma konusuna baktık, ancak henüz bir kullanıcıyı nasıl günlüğe kaydettireceğiz. ' De bir Kullanıcı kaydetme yöntemlerine ek olarak, FormsAuthentication sınıfı da bir [SignOut yöntemi](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx)sağlar. SignOut yöntemi, form kimlik doğrulama anahtarını yok eder, böylece kullanıcı siteden dışarı günlüğe kaydediliyor.

Bir oturum çıkış bağlantısı sunumu, ASP.NET 'in bir kullanıcıyı günlüğe kaydetmek için özel olarak tasarlanmış bir denetim içermesi gibi yaygın bir özelliktir. [LoginStatus denetimi](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginstatus.aspx) , kullanıcının kimlik doğrulama durumuna bağlı olarak bir Login LinkButton veya Logout LinkButton görüntüler. Anonim kullanıcılar için bir oturum açma LinkButton, kimliği doğrulanmış kullanıcılara bir Logout LinkButton gösterilirken işlenir. Login ve Logout LinkButtons için metin, LoginStatus 'un LoginText ve LogoutText özellikleri aracılığıyla yapılandırılabilir.

Login LinkButton öğesine tıkladığınızda, oturum açma sayfasına yeniden yönlendirme verilen bir geri göndermeye neden olur. Logout LinkButton düğmesine tıklamak, LoginStatus denetiminin FormsAuthentication. SignOff metodunu çağırmasına ve sonra kullanıcıyı bir sayfaya yönlendirmesine neden olur. Oturum açmış kullanıcının yeniden yönlendirildiği sayfa, aşağıdaki üç değerden birine atanabilecek LogoutAction özelliğine bağlıdır:

- Yenile-varsayılan; kullanıcıyı yeni ziyaret ettikleri sayfaya yönlendirir. Yeni ziyaret ettikleri sayfa anonim kullanıcılara izin vermediğinden, FormsAuthenticationModule otomatik olarak Kullanıcı oturum açma sayfasına yönlendirir.

Burada yeniden yönlendirmenin neden gerçekleştirildiğinden merak ediyor olabilirsiniz. Kullanıcı aynı sayfada kalmak isterse, neden açık yeniden yönlendirme gereksinimim gerekir? Bunun nedeni, oturum kapatma bağlantısı düğmesine tıklandığında kullanıcının, Forms kimlik doğrulama biletini tanımlama bilgileri koleksiyonunda hala vardır. Sonuç olarak, geri gönderme isteği, kimliği doğrulanmış bir istek olur. LoginStatus denetimi SignOut yöntemini çağırır, ancak FormsAuthenticationModule Kullanıcı kimliğini doğruladıktan sonra olur. Bu nedenle, açık bir yeniden yönlendirme tarayıcının sayfayı yeniden istemesine neden olur. Tarayıcının sayfayı yeniden istediği zaman, Forms kimlik doğrulama bileti kaldırılmıştır ve bu nedenle gelen istek anonimdir.

- Yeniden yönlendirme-Kullanıcı, LoginStatus 'un LogoutPageUrl özelliği tarafından belirtilen URL 'ye yeniden yönlendirilir.
- RedirectToLoginPage-Kullanıcı oturum açma sayfasına yönlendirilir.

Ana sayfaya bir LoginStatus denetimi ekleyelim ve kullanıcıyı, imzalandığını onaylayan bir ileti görüntüleyen bir sayfaya göndermek için yeniden yönlendirme seçeneğini kullanacak şekilde yapılandıralim. Logout. aspx adlı kök dizinde bir sayfa oluşturarak başlayın. Bu sayfayı site. Master ana sayfasıyla ilişkilendirmeyi unutmayın. Ardından, kullanıcının oturum açtıkları Kullanıcı tarafından kullanılan biçimlendirmesinde bir ileti girin.

Ardından, site. Master ana sayfasına dönün ve LoginContent ContentPlaceHolder içindeki LoginView altına bir LoginStatus denetimi ekleyin. LoginStatus denetiminin LogoutAction özelliğini, Redirect ve LogoutPageUrl özelliğini ~/Logout.aspx olarak ayarlayın.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample11.aspx)]

LoginStatus, LoginView denetimi dışında olduğundan, hem anonim hem de kimliği doğrulanmış kullanıcılar için görünür, ancak LoginStatus bir oturum açma veya oturum kapatma LinkButton 'ı doğru bir şekilde görüntülemesi için bu işlem tamam. LoginStatus denetimi eklendiğinde, AnonymousTemplate içindeki günlük Köprüsü gereksiz olduğundan, bunu kaldırın.

Şekil 18, Jisun ziyaret edildiğinde default. aspx ' i gösterir. Sol sütunda iletiyi görüntülediğini, geri hoş geldiniz 'in yanı sıra oturum kapatma bağlantısı ile ilgili olduğunu unutmayın. Günlüğe kaydet LinkButton düğmesine tıklamak geri göndermeye neden olur, sistemin oturumunu kapatır ve sonra da oturumu kapat. aspx öğesine yönlendirir. Şekil 19 ' u gösterdiği gibi, Jisun Logout 'e ulaşmaz. aspx zaten kaydolmuş ve bu nedenle anonimdir. Sonuç olarak, sol sütunda hoş geldiniz, yabanger ve oturum açma sayfasına yönelik bir bağlantı gösterilir.

[![default. aspx, bir Logout LinkButton ile birlikte hoş geldiniz 'i geri, Jisun gösterir](an-overview-of-forms-authentication-vb/_static/image53.png)](an-overview-of-forms-authentication-vb/_static/image52.png)

**Şekil 18**: default. aspx, bir Logout LinkButton ([tam boyutlu görüntüyü görüntülemek için tıklatın](an-overview-of-forms-authentication-vb/_static/image54.png)) ile birlikte hoş geldiniz 'i gösterir.

[![Logout. aspx, bir Login LinkButton ile birlikte hoş geldiniz, yabanger gösterir](an-overview-of-forms-authentication-vb/_static/image56.png)](an-overview-of-forms-authentication-vb/_static/image55.png)

**Şekil 19**: logout. aspx, bir Login LinkButton Ile birlikte Welcome, Stranger gösterir ([tam boyutlu görüntüyü görüntülemek için tıklayın](an-overview-of-forms-authentication-vb/_static/image57.png))

> [!NOTE]
> Ana sayfanın LoginContent ContentPlaceHolder 'ı (adım 4 ' te Login. aspx yaptığımız gibi) gizlemek için Logout. aspx sayfasını özelleştirmenizi öneririz. Bunun nedeni, LoginStatus denetimi tarafından işlenen oturum açma LinkButton 'ın (Hello, Stranger), kullanıcının geçerli URL 'yi ReturnUrl QueryString parametresinde geçen oturum açma sayfasına göndermesi nedeniyle oluşur. Kısacası, oturum açmış bir Kullanıcı bu LoginStatus oturum açma bilgileri düğmesine tıklamıştır ve sonra oturum açar. Bu, kullanıcıyı kolayca karıştırabilen Logout. aspx ' e yönlendirilir.

## <a name="summary"></a>Özet

Bu öğreticide, Forms kimlik doğrulaması iş akışını inceliyoruz ve sonra bir ASP.NET uygulamasında form kimlik doğrulaması uygulamayı etkinleştirdik. Form kimlik doğrulaması, iki sorumluluğu olan FormsAuthenticationModule tarafından desteklenir: kullanıcıları Forms kimlik doğrulama biletini temel alarak tanımlama ve yetkisiz kullanıcıları oturum açma sayfasına yönlendirme.

.NET Framework FormsAuthentication sınıfı, form kimlik doğrulama biletlerini oluşturma, İnceleme ve kaldırma yöntemlerini içerir. Istek. IsAuthenticated özelliği ve Kullanıcı nesnesi, bir isteğin kimlik doğrulamasının yapılıp yapılmayacağını ve kullanıcının kimliğiyle ilgili bilgilerin belirlenmesi için ek programlama desteği sağlar. Ayrıca, geliştiricilere birçok yaygın oturum açma görevi gerçekleştirmeye yönelik hızlı ve kod içermeyen bir yol veren LoginView, LoginStatus ve LoginName Web denetimleri de vardır. Bu ve diğer oturum açma ile ilgili Web denetimlerini sonraki öğreticilerde daha ayrıntılı bir şekilde inceleyeceğiz.

Bu öğreticide, Forms kimlik doğrulamasına yönelik bir Amna hatlarıyla genel bakış sunulmaktadır. Assıralanan yapılandırma seçeneklerini inceleyemedi, tanımlama bilgisi olmayan formların kimlik doğrulama biletlerinin nasıl çalıştığını inceleyin veya form kimlik doğrulama anahtarının içeriğini nasıl koruduğunu araştırın ASP.NET. [Sonraki öğreticide](forms-authentication-configuration-and-advanced-topics-vb.md)bu konuları ve daha fazlasını tartışacağız.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [IıS6 ve ııS7 güvenliği arasındaki değişiklikler](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/Changes-between-IIS6-and-IIS7-Security)
- [Login ASP.NET denetimleri](https://msdn.microsoft.com/library/d51ttbhx.aspx)
- [Professional ASP.NET 2,0 güvenlik, üyelik ve rol yönetimi](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html) (ısbn: 978-0-7645-9698-8)
- [&lt;Authentication&gt; öğesi](https://msdn.microsoft.com/library/532aee0e.aspx)
- [&lt;Forms &lt;kimlik doğrulaması için&gt; öğesi&gt;](https://msdn.microsoft.com/library/1d3t3c61.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>Bu öğreticide bulunan konularda video eğitimi

- [ASP.NET’te Temel Forms Kimlik Doğrulaması Kullanma](../../../videos/authentication/using-basic-forms-authentication-in-aspnet.md)

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı Scott Mitchell, 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, *[24 saat içinde ASP.NET 2,0 kendi kendinize eğitim](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ister. Scott 'a [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) veya blogundan [http://ScottOnWriting.NET](http://scottonwriting.net/)üzerinden erişilebilir.

### <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler, Alicja Maziarz, John suru ve Teresa Murphy ' i içerir. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, beni [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)bir satır bırakın.

> [!div class="step-by-step"]
> [Önceki](security-basics-and-asp-net-support-vb.md)
> [İleri](forms-authentication-configuration-and-advanced-topics-vb.md)
