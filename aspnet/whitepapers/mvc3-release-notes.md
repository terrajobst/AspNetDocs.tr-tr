---
uid: whitepapers/mvc3-release-notes
title: ASP.NET MVC 3 | Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/06/2010
ms.assetid: f44c166e-7e91-48a0-a6f8-d9285f3594e5
msc.legacyurl: /whitepapers/mvc3-release-notes
msc.type: content
ms.openlocfilehash: 504202068f5db4f8614bba02e8066ffecfd15b48
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74619235"
---
# <a name="aspnet-mvc-3"></a>ASP.NET MVC 3

- [Genel bakış](#overview)
- [Yükleme notları](#installation-notes)
- [Yazılım gereksinimleri](#software-requirements)
- [Belgeler](#documentation)
- [Support](#support)
- [ASP.NET MVC 2 projesini ASP.NET MVC 3 araç güncelleştirmesine yükseltme](#upgrading)
- [ASP.NET MVC 3 Araçlar Güncelleştirmesi (12 Nisan 2011)](#tu-changes)

    - ["Denetleyici Ekle" iletişim kutusu artık görünümler ve veri erişim kodu ile İskelesi denetleyicileri oluşturabilir](#tu-AddControllerDialog)
    - ["ASP.NET MVC 3 yeni proje" Iletişim kutusunda iyileştirmeler](#tu-ImprovementsNewDialogBox)
    - [Proje şablonları artık Modernizr 1,7 içerir](#tu-Modernizr)
    - [Proje şablonları, jQuery, jQuery UI ve jQuery doğrulamasının güncelleştirilmiş sürümlerini içerir](#tu-UpdatedJQuery)
    - [Proje şablonları artık önceden yüklenmiş bir NuGet paketi olarak ADO.NET Entity Framework 4,1 içerir](#tu-EF)
    - [Proje şablonları, JavaScript kitaplıklarını önceden yüklenmiş NuGet paketleri olarak içerir](#tu-JavaScriptLibsNuget)
    - [Bilinen Sorunlar](#tu-KI)
- [ASP.NET MVC 3 RTM (13 Ocak 2011)](#MVC3RTM)

    - [Değişiklik: jQuery Kullanıcı arabiriminin sürümü 1.8.7 olarak güncelleştirildi](#RTM-1)
    - [Değişiklik: varsayılan ModelMetadataProvider geri DataAnnotationsModelMetadataProvider olarak değiştirildi](#RTM-2)
    - [Düzeltildi: boşluk içeren bir Razor ifadesinin parçasını geri çevrilme sonucu](#RTM-3)
    - [Düzeltildi: düzenleyicide açılan bir Razor dosyasının yeniden adlandırılması, söz dizimi renklendirmesi ve IntelliSense 'i devre dışı bırakır](#RTM-4)
    - [Bilinen Sorunlar](#RTM-KI)
    - [Son değişiklikler](#RTM-BC)
- [ASP.NET MVC 3 sürüm adayı 2 (10 Aralık 2010)](#_Toc2)

    - [Proje şablonları jQuery 1.4.4, jQuery doğrulaması 1,7 ve jQuery kullanıcı arabirimi 1.8.6 y UI 1.8.6 Içerecek şekilde değiştirilmiştir](#_Toc2_1)
    - ["AdditionalMetadataAttribute" sınıfı eklendi](#_Toc2_2)
    - [Geliştirilmiş görünüm yapı Iskelesi](#_Toc2_3)
    - [HTML. RAW yöntemi eklendi](#_Toc2_3)
    - ["Controller. ViewModel" özelliği ve "View" özelliği "ViewBag" olarak yeniden adlandırıldı](#_Toc2_4)
    - ["ControllerSessionStateAttribute" sınıfı "SessionStateAttribute" olarak yeniden adlandırıldı](#_Toc2_5)
    - [RemoteAttribute "Fields" özelliği "AdditionalFields" olarak yeniden adlandırıldı](#_Toc2_6)
    - ["SkipRequestValidationAttribute", "AllowHtmlAttribute" olarak yeniden adlandırıldı](#_Toc2_7)
    - ["HTML. ValidationMessage" yöntemi, Ilk yararlı hata Iletisini görüntüleyecek şekilde değiştirildi](#_Toc2_8)
    - [Belgeye boşluk eklemek için @model bildirimi düzeltildi](#_Toc2_9)
    - [Altyapıya özgü dosya adlarını desteklemek için altyapıyı görüntülemek için "FileExtensions" özelliği eklendi](#_Toc2_10)
    - ["For" özniteliği için doğru değeri yayma için "LabelFor" Yardımcısı düzeltildi](#_Toc2_11)
    - [Model bağlama sırasında açık değerlere öncelik vermek için "RenderAction" yöntemi düzeltildi](#_Toc2_12)
    - [Son değişiklikler](#_Toc2_BC)
    - [Bilinen Sorunlar](#_Toc2_KI)
- [ASP.NET MVC 3 sürüm adayı (9 Kasım 2010)](#TOC_ASP_NET_3_RC)

    - [ASP.NET MVC 3 RC 'deki yeni özellikler](#_Toc276711785)
    - [NuGet Paket Yöneticisi](#_Toc276711786)
    - [Geliştirilmiş "yeni proje" Iletişim kutusu](#_Toc276711787)
    - [Oturumsuz denetleyiciler](#_Toc276711788)
    - [Yeni doğrulama öznitelikleri](#_Toc276711789)
    - ["LabelFor" ve "LabelForModel" yöntemleri için yeni aşırı yüklemeler](#_Toc276711790)
    - [Alt eylem çıkışı önbelleğe alma](#_Toc276711791)
    - ["Görünüm Ekle" Iletişim kutusu geliştirmeleri](#_Toc276711792)
    - [Ayrıntılı Istek doğrulaması](#_Toc276711793)
    - [Son değişiklikler](#_Toc276711794)
    - [Bilinen Sorunlar](#_Toc276711795)
- [ASP.net. MVC 3 Beta notları (6 Ekim 2010)](#TOC_ASP_NET_3_Beta)

    - [ASP.NET MVC 3 beta sürümündeki yeni özellikler](#0.1__Toc274034215)
    - [NuPack Paket Yöneticisi](#0.1__Toc274034216)
    - [Geliştirilmiş yeni proje Iletişim kutusu](#0.1__Toc274034217)
    - [Razor görünümlerinde kesin olarak belirlenmiş modeller belirtmenin Basitleştirilmiş yolu](#0.1__Toc274034218)
    - [Yeni ASP.NET Web sayfaları yardımcı yöntemleri için destek](#0.1__Toc274034219)
    - [Ek bağımlılık ekleme desteği](#0.1__Toc274034220)
    - [Unobtrusive tabanlı Ajax için yeni destek](#0.1__Toc274034221)
    - [Unobtrusive doğrulaması için yeni destek](#0.1__Toc274034222)
    - [Istemci doğrulaması ve unobtrusive JavaScript için uygulama genelinde yeni bayraklar](#0.1__Toc274034223)
    - [Görünümler çalıştırılmadan önce çalışan kod için yeni destek](#0.1__Toc274034224)
    - [VBHTML Razor sözdizimi için yeni destek](#0.1__Toc274034225)
    - [ValidateInputAttribute üzerinde daha ayrıntılı denetim](#0.1__Toc274034226)
    - [Yardımcılar, anonim nesneler kullanılarak belirtilen HTML öznitelik adları için alt çizgileri tirelere dönüştürür](#0.1__Toc274034227)
    - [Hata Düzeltmeleri](#0.1__Toc274034228)
    - [Son değişiklikler](#0.1__Toc274034229)
    - [Bilinen Sorunlar](#0.1__Toc274034230)
- [Sorumluluk reddi](#0.1__Toc274034231)

<a id="overview"></a>
## <a name="overview"></a>Genel bakış

Bu belgede, Visual Studio 2010 için ASP.NET MVC 3 RTM sürümü açıklanmaktadır. ASP.NET MVC, Model-View-Controller (MVC) modelini kullanan Web uygulamaları geliştirmeye yönelik bir çerçevedir. ASP.NET MVC 3 yükleyicisi aşağıdaki bileşenleri içerir:

- ASP.NET MVC 3 çalışma zamanı bileşenleri
- ASP.NET MVC 3 Visual Studio 2010 araçları
- ASP.NET Web sayfaları çalışma zamanı bileşenleri
- ASP.NET Web Pages Visual Studio 2010 araçları
- .NET için Microsoft Package Manager (NuGet)
- Visual Studio 2010 için Razor söz dizimi desteğini sağlayan bir güncelleştirme. (Ayrıntılar için bkz. Bilgi Bankası makalesi 2483190.)

ASP.NET MVC 3 ' ün her yayın öncesi sürümü için sürüm notlarının tam kümesi, aşağıdaki URL 'de ASP.NET Web sitesinde bulunabilir:

https://www.asp.net/learn/whitepapers/mvc3-release-notes

<a id="installation-notes"></a>
## <a name="installation-notes"></a>Yükleme notları

Web Platformu Yükleyicisi 'ni (Web PI) kullanarak ASP.NET MVC 3 RTM 'yi yüklemek için şu sayfayı ziyaret edin:

[https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3](https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3)

Alternatif olarak, Visual Studio 2010 için ASP.NET MVC 3 RTM yükleyicisini aşağıdaki sayfadan indirebilirsiniz:

https://go.microsoft.com/fwlink/?LinkID=208140

ASP.NET MVC 3 yüklenebilir ve ASP.NET MVC 2 ile yan yana çalıştırılabilir.

<a id="software-requirements"></a>
## <a name="software-requirements"></a>Yazılım Gereksinimleri

ASP.NET MVC 3 çalışma zamanı bileşenleri aşağıdaki yazılımı gerektirir:

- Sürüm 4 .NET Framework. 

    ASP.NET MVC 3 Visual Studio 2010 araçları aşağıdaki yazılımları gerektirir:
- Visual Studio 2010 veya Visual Web Developer 2010 Express.

<a id="documentation"></a>
## <a name="documentation"></a>Belgeler

ASP.NET MVC belgeleri aşağıdaki URL 'de MSDN Web sitesinde bulunabilir:

[https://go.microsoft.com/fwlink/?LinkId=205717](https://go.microsoft.com/fwlink/?LinkId=205717)

ASP.NET MVC hakkındaki öğreticiler ve diğer bilgiler, ASP.NET Web sitesinin MVC sayfasında aşağıdaki URL 'de bulunabilir:

[https://www.asp.net/mvc/](../mvc/index.md)

<a id="support"></a>
## <a name="support"></a>Destek

Bu, tam olarak desteklenen bir sürümdür. Teknik destek alma hakkında daha fazla bilgi [Microsoft desteği web sitesinde](https://support.microsoft.com/)bulunabilir.

Ayrıca, ASP.NET Community üyelerinin çok sayıda resmi olmayan destek sağlayabildiği ASP.NET MVC forumuna bu yayınla ilgili sorularınızı göndermekten çekinmeyin:

[https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)

<a id="upgrading"></a>
## <a name="upgrading-an-aspnet-mvc-2-project-to-aspnet-mvc-3-tools-update"></a>ASP.NET MVC 2 projesini ASP.NET MVC 3 araç güncelleştirmesine yükseltme

ASP.NET MVC 3, aynı bilgisayarda ASP.NET MVC 2 ile yan yana yüklenebilir ve bu da bir ASP.NET MVC 2 uygulamasının ASP.NET MVC 3 ' e ne zaman yükseltileceğini seçme esnekliği sağlar.

Mevcut bir ASP.NET MVC 2 uygulamasını sürüm 3 ' e el ile yükseltmek için aşağıdakileri yapın:

1. Bilgisayarınızda yeni bir boş ASP.NET MVC 3 projesi oluşturun. Bu proje, yükseltme için gereken bazı dosyaları içerir.
2. Aşağıdaki dosyaları ASP.NET MVC 3 projesinden ASP.NET MVC 2 projenizin karşılık gelen konumuna kopyalayın. Yeni dosya adını (jQuery-1.5.1. js) hesaba eklemek için jQuery kitaplığı başvurularını güncelleştirmeniz gerekir: 

    - /Views/Web.config
    - /packagesnconfig
    - /Scripts/\*. js
    - /Content/themes/\*.\*
3. Boş ASP.NET MVC 3 proje çözümünün kökündeki *Packages* klasörünü, çözümünüzün. sln dosyasının bulunduğu dizinde olan çözümünüzün köküne kopyalayın.
4. ASP.NET MVC 2 projeniz herhangi bir alan içeriyorsa,/Views/Web.config dosyasını her bir alanın *Görünümler* klasörüne kopyalayın.
5. ASP.NET MVC 2 projesindeki Web. config dosyalarında, genel olarak arama yapın ve ASP.NET MVC sürümünü değiştirin. Şunları bulun: 

    [!code-console[Main](mvc3-release-notes/samples/sample1.cmd)]

    Bunu aşağıdaki kodla değiştirin:

    [!code-console[Main](mvc3-release-notes/samples/sample2.cmd)]
6. Çözüm Gezgini, *System. Web. Mvc* başvurusunu silin (sürüm 2 ' den dll 'ye işaret eder) ve ardından *System. Web. Mvc* (v 3.0.0.0) öğesine bir başvuru ekleyin.
7. System. Web. Web sayfası. dll ve System. Web. yardımcılar. dll için bir başvuru ekleyin. Bu derlemeler aşağıdaki klasörlerde bulunur: 

    - % ProgramFiles% \ Microsoft ASP. NET\ASP.NET MVC 3 \ derlemeler
    - % ProgramFiles% \ Microsoft ASP. NET\ASP.NET Web Sayfa\sanal 1.0 \ derlemeler
8. Çözüm Gezgini, proje adına sağ tıklayın ve projeyi Kaldır ' ı seçin. Ardından proje adına tekrar sağ tıklayın ve *ProjectName*. csproj öğesini Düzenle ' yi seçin.
9. *Projecttypeguid* öğelerini bulun ve {F85E285D-A4E0-4152-9332-AB1D724D3325} öğesini {E53F8FEA-EAE0-44A6-8774-FFD645390401} ile değiştirin.
10. Değişiklikleri kaydedin, projeye sağ tıklayın ve ardından projeyi yeniden yükle ' yi seçin.
11. Uygulamanın kök Web. config dosyasında aşağıdaki ayarları *derlemeler* bölümüne ekleyin. 

    [!code-xml[Main](mvc3-release-notes/samples/sample3.xml)]
12. Proje, ASP.NET MVC 2 kullanılarak derlenen herhangi bir üçüncü taraf kitaplığına başvuruyorsa, *yapılandırma* bölümünün altındaki uygulama kökündeki Web. config dosyasına aşağıdaki vurgulanan *bindingRedirect* öğesini ekleyin: 

    [!code-xml[Main](mvc3-release-notes/samples/sample4.xml)]

<a id="tu-changes"></a>
## <a name="changes-in-aspnet-mvc-3-tools-update"></a>ASP.NET MVC 3 araç güncelleştirmesinde yapılan değişiklikler

Bu bölümde, ASP.NET MVC 3 RTM sürümünden bu yana ASP.NET MVC 3 Araçlar Güncelleştirme sürümünde yapılan değişiklikler açıklanmaktadır.

<a id="tu-AddControllerDialog"></a>
### <a name="add-controller-dialog-box-can-now-scaffold-controllers-with-views-and-data-access-code"></a>"Denetleyici Ekle" iletişim kutusu artık görünümler ve veri erişim kodu ile İskelesi denetleyicileri oluşturabilir

Yapı iskelesi, uygulamanız için bir denetleyiciyi ve görünümleri hızlı bir şekilde oluşturmanın bir yoludur. Kod oluşturulduktan sonra, projenizin gereksinimlerini karşılayacak şekilde düzenleyebilirsiniz.

ASP.NET MVC 3 ' te *Denetleyici Ekle* iletişim kutusunu başlatmak için *Çözüm Gezgini*' de *denetleyiciler* klasörüne sağ tıklayın, *Ekle*' ye ve ardından *Denetleyici*' ye tıklayın. İletişim kutusu ek yapı iskelesi seçenekleri sunacak şekilde geliştirilmiştir.

![](mvc3-release-notes/_static/image1.png)

Varsayılan olarak üç yapı iskelesi şablonu mevcuttur.

#### <a name="empty-controller"></a>Boş denetleyici

Bu şablon boş bir denetleyici dosyası oluşturur. Bu şablon, ASP.NET MVC 'nin önceki sürümlerindeki *oluşturma, düzenleme, ayrıntılar, silme senaryoları Için ekleme eylemlerini* denetlemede eşdeğerdir. Bunu seçerseniz, daha fazla seçenek yoktur.

#### <a name="controller-with-empty-readwrite-actions"></a>Boş okuma/yazma eylemleri olan denetleyici

Bu şablon, gerekli tüm eylem yöntemlerine sahip ancak metotlarda uygulama kodu olmayan bir denetleyici dosyası oluşturur. Bu şablon, ASP.NET MVC 'nin önceki sürümlerindeki *oluşturma, düzenleme, ayrıntılar, silme senaryoları Için ekleme eylemleri* denetimi ile eşdeğerdir. Bunu seçerseniz, daha fazla seçenek yoktur.

#### <a name="controller-with-readwrite-actions-and-views-using-entity-framework"></a>Okuma/yazma eylemleri ve görünümleri ile, Entity Framework kullanarak denetleyici

Bu şablon, çalışma veri girişi kullanıcı arabirimini hızlıca oluşturmanızı sağlar. Aşağıdakiler gibi bir dizi ortak gereksinimi ve senaryoyu işleyen bir kod üretir:

- *Veri erişimi*. Oluşturulan kod, bir veritabanındaki varlıkları okur ve yazar. Mevcut bir veri bağlamı sınıfını seçerseniz veya şablonun yeni bir *DbContext* sınıfı oluşturmasına izin verirseniz, Entity Framework Code First yaklaşımıyla birlikte kullanılır. Ayrıca, mevcut bir *ObjectContext* sınıfını seçerseniz Entity Framework Database First veya model First yaklaşımla birlikte da kullanılır.
- *Doğrulama*. Oluşturulan kod, form gönderimlerinin model sınıfınıza göre bildirildiği kurallara göre doğrulanması için ASP.NET MVC model bağlama ve meta veri özelliklerini kullanır. Bu, *gerekli* ve *StringLength* öznitelikleri ve özel doğrulama kuralları gibi yerleşik doğrulama kurallarını içerir.
- *Bire çok ilişkisi*. Model sınıflarınız arasında bire çok yabancı anahtar ilişkisi tanımlarsanız, oluşturulan kod ilgili varlıkların seçilmesi için açılan listeler oluşturur. Örneğin, Code First kuralları Entity Framework aşağıdaki model sınıflarını tanımlayabilirsiniz: 

    [!code-csharp[Main](mvc3-release-notes/samples/sample5.cs)]

    Daha sonra *ürün* sınıfı için bir denetleyiciyi dolandırdığınızda, görünümleri kullanıcıların her *ürün* örneği için bir *Kategori* nesnesi seçmesine izin verir.

    Bu şablon, *Denetleyici Ekle* iletişim kutusunda ek seçeneklere izin vermez. *Model sınıfı*için, çözümünüzde, kullanıcıların oluşturabilme veya düzenleyebileceği veri türünü belirleyen herhangi bir model sınıfını seçebilirsiniz:
- Entity Framework Code First kullanmak istiyorsanız, herhangi bir model sınıfı seçebilirsiniz.
- Entity Framework Database First veya Entity Framework Model First kullanıyorsanız, kavramsal modelinizde tanımlanmış bir varlık sınıfı seçtiğinizden emin olun.

*Veri bağlamı sınıfı*için şu seçimleri yapabilirsiniz:

- Code First kullanmak ve mevcut veri bağlamı sınıfı yoksa, * * yeni veri bağlamı * * ' nı seçin. Daha sonra sizin için bir veri bağlamı sınıfı oluşturulacaktır.
- Code First kullanmak ve var olan bir veri bağlamı sınıfına sahip olmak istiyorsanız, burada seçin. Seçtiğiniz model sınıfını kalıcı hale getirmek için güncelleştirilir.
- Database First veya Model First kullanıyorsanız, burada nesne bağlam sınıfınızı seçin.

Görünümler için, kullanmak istediğiniz görünüm altyapısını seçin ya da herhangi bir görünümü kullanmak istemiyorsanız Hiçbiri ' ni seçin.

Oluşturulan görünümler için Gelişmiş seçenek seçeneğini belirleyin. Örneğin, kullanılacak düzen veya ana sayfayı seçebilirsiniz.

<a id="tu-ImprovementsNewDialogBox"></a>
### <a name="improvements-to-the-aspnet-mvc-3-new-project-dialog-box"></a>"ASP.NET MVC 3 yeni proje" Iletişim kutusunda iyileştirmeler

Yeni ASP.NET MVC 3 projeleri oluşturmak için kullandığınız iletişim kutusu aşağıda listelendiği gibi birden çok geliştirme içerir.

![](mvc3-release-notes/_static/image2.png)

#### <a name="new-intranet-project-template"></a>Yeni "Intranet Projesi" şablonu

Proje şablonu listesi yeni bir Intranet uygulama şablonu içerir. Bu şablon, Forms kimlik doğrulaması yerine Windows kimlik doğrulaması kullanarak bir Web uygulaması oluşturmaya yönelik ayarları içerir. Bir intranet uygulaması bir proje şablonunda kapsüllenmediği bazı IIS ayarları gerektirdiğinden, şablon, proje şablonunun IIS 'de nasıl çalışacağından ilgili yönergeler içeren bir Benioku dosyası içerir. Yeni bir Intranet uygulaması şablonuna yönelik belgeler, MSDN Web sitesinde aşağıdaki URL 'de bulunabilir:

[https://msdn.microsoft.com/library/gg703322(VS.98).aspx](https://msdn.microsoft.com/library/gg703322(VS.98).aspx)

#### <a name="project-templates-are-now-html5-enabled"></a>Proje şablonları artık HTML5 özellikli

Yeni-proje iletişim kutusu artık proje şablonlarına HTML5 'e özgü özellikler ekleme seçeneği içerir. Seçeneğinin belirlenmesi, yeni HTML5 `<header>`, `<footer>`ve `<navigation>` öğelerini içeren görünümlerin oluşturulmasına neden olur.

Tarayıcıların önceki sürümlerinin HTML5 'e özgü etiketleri desteklemediğine unutmayın. HTML5 proje şablonları, bu sınırlamayı ele almak için Modernizr kitaplığına bir başvuru içerir. (Sonraki bölüme bakın.)

<a id="tu-Modernizr"></a>
### <a name="project-templates-now-include-modernizr-17"></a>Proje şablonları artık Modernizr 1,7 içerir

Modernizr, bu özellikleri henüz desteklemeyen tarayıcılarda CSS 3 ve HTML5 desteğini sağlayan bir JavaScript kitaplığıdır. Bu kitaplık, ASP.NET MVC 3 projeleri için şablonlarda önceden yüklenmiş bir NuGet paketi olarak eklenmiştir. Modernizr hakkında daha fazla bilgi için bkz. [http://www.modernizr.com/](http://www.modernizr.com/).

<a id="tu-UpdatedJQuery"></a>
### <a name="project-templates-include-updated-versions-of-jquery-jquery-ui-and-jquery-validation"></a>Proje şablonları, jQuery, jQuery UI ve jQuery doğrulamasının güncelleştirilmiş sürümlerini içerir

Proje şablonları artık jQuery betiklerinin aşağıdaki sürümlerini içerir:

- jQuery 1.5.1
- jQuery doğrulaması 1,8
- jQuery kullanıcı arabirimi 1.8.11

Bu kitaplıklar önceden yüklenmiş NuGet paketleri olarak dahil edilmiştir.

<a id="tu-EF"></a>
### <a name="project-templates-now-include-adonet-entity-framework-41-as-a-pre-installed-nuget-package"></a>Proje şablonları artık önceden yüklenmiş bir NuGet paketi olarak ADO.NET Entity Framework 4,1 içerir

ADO.NET Entity Framework 4,1 Code First özelliğini içerir. Code First, mevcut Database First ve Model First desenlerine alternatif sağlayan, ADO.NET Entity Framework için yeni bir geliştirme desendir.

Code First, Visual Basic veya C#içinde yazılmış poco sınıflarını ("düz eski CLR nesneleri") kullanarak modelinizi tanımlamaya odaklanmıştır. Bu sınıflar daha sonra var olan bir veritabanına eşlenebilir veya bir veritabanı şeması oluşturmak için kullanılabilir. Daha fazla yapılandırma *Dataek açıklama* öznitelikleri kullanılarak veya akıcı API 'ler kullanılarak sağlanabilir.

ASP.NET MVC Ile Firstcode 'u kullanmaya yönelik belgeler aşağıdaki URL 'Lerde ASP.NET Web sitesinde bulunabilir:

[https://www.asp.net/mvc/tutorials/getting-started-with-mvc3-part1-cs](../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [https://www.asp.net/entity-framework/tutorials/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)

<a id="tu-JavaScriptLibsNuget"></a>
### <a name="project-templates-include-javascript-libraries-as-pre-installed-nuget-packages"></a>Proje şablonları, JavaScript kitaplıklarını önceden yüklenmiş NuGet paketleri olarak içerir

Yeni bir ASP.NET MVC 3 projesi oluşturduğunuzda, proje, dosyaları doğrudan proje şablonundaki betikler klasörüne eklemek yerine, daha önce (örneğin, Modernizr kitaplığı) belirtilen JavaScript dosyalarını içerir. dekiler. Bu, komut dosyalarının yeni sürümleri yayımlanacaksa betikleri en son sürüme güncelleştirmek için NuGet kullanmanıza olanak sağlar.

Örneğin, Yeni jQuery sürümlerinin sıklığı verildiğinde, proje şablonuna dahil olan jQuery 'ın sürümü bir noktada güncel olmayacaktır. Bununla birlikte, jQuery yüklü bir NuGet paketi olarak eklendiğinden, jQuery 'in daha yeni sürümleri kullanılabilir olduğunda NuGet iletişim kutusunda size bildirimde bulunulacaktır.

JQuery dosya adındaki sürüm numarasını içerdiğinden, jQuery 'nin en son sürüme güncelleştirilmesi de, yeni dosya adını kullanmak için jQuery dosyasına başvuran `<script>` etiketinin güncelleştirilmesini gerektirir. Dahil edilen diğer betik kitaplıkları, en son sürümlerine daha kolay bir şekilde güncelleştiribilecekleri için, betik adındaki sürüm numarasını içermez.

<a id="tu-KI"></a>
## <a name="known-issues"></a>Bilinen Sorunlar

- Bazı durumlarda, yükleme "yükleme hata kodu ile başarısız oldu (0x80070643)" hata iletisiyle başarısız olabilir. Bu sorunu geçici olarak çözmek hakkında daha fazla bilgi için bkz. bilgi [Bankası makalesi 2531566](https://support.microsoft.com/kb/2531566).
- Denetleyici ekleme için yapı iskelesi, Entity Framework içinde varlık devralma desteğinden faydalanan varlıkları ayrıştırmaz. Örneğin, *öğrenci* sınıfı tarafından devralınan bir temel *kişi* sınıfı verildiğinde, *öğrenci* sınıfının yapı iskelesi, derlenmeyen oluşturulan koda neden olur.
- Bir çözüm klasörü içinde yeni bir ASP.NET MVC 3 projesi oluşturmak bir *NullReferenceException* hatasına neden olur. Geçici çözüm, çözümün kökünde ASP.NET MVC 3 projesini oluşturmak ve çözüm klasörüne taşımadır.
- ReSharper yüklendiğinde IntelliSense Razor söz dizimi çalışmaz. ReSharper yüklüyse ve ASP.NET MVC 3 ' teki Razor IntelliSense desteğinden yararlanmak istiyorsanız, bunları bugün birlikte kullanmanın yollarını açıklayan [Razor IntelliSense ve ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) for Hadi Hariri bloguna bakın.
- Yükleme sırasında, EULA kabulü iletişim kutusu, lisans koşullarını amaçlanan bir pencerede görüntüler.
- Bir Razor görünümünü (. cshtml veya) düzenlediğinizde. *vbhtml* dosyası), görünümler. ASP.NET MVC 3, Razor görünümleri için herhangi bir kod parçacığı içermez. ASP.NET MVC için kod parçacığını seçme aspxseçilmesi, için parçacıkları gösterir
- Visual Studio 'nun yüklü olmadığı bir bilgisayara Visual Web Developer Express için ASP.NET MVC 3 ' ü yükler ve daha sonra Visual Studio 'yu yüklerseniz, ASP.NET MVC 3 ' ü yeniden yüklemeniz gerekir. Visual Studio ve Visual Web Developer Express, ASP.NET MVC 3 yükleyicisi tarafından yükseltilen bileşenleri paylaşır. Visual Studio için ASP.NET MVC 3 ' ü Visual Web Developer Express olmayan bir bilgisayara yüklerseniz ve daha sonra Visual Web Developer Express 'i yüklüyorsanız aynı sorun geçerlidir.

<a id="MVC3RTM"></a>
## <a name="changes-in-aspnet-mvc-3-rtm"></a>ASP.NET MVC 3 RTM 'deki değişiklikler

Bu bölümde, RC2 sürümünden bu yana ASP.NET MVC 3 RTM sürümünde yapılan değişiklikler ve hata düzeltmeleri açıklanmaktadır.

<a id="RTM-1"></a>
### <a name="change-updated-the-version-of-jquery-ui-to-187"></a>Değişiklik: jQuery Kullanıcı arabiriminin sürümü 1.8.7 olarak güncelleştirildi

Visual Studio için ASP.NET MVC proje şablonları, jQuery kullanıcı arabirimi kitaplığının en son sürümünü içerecek şekilde güncelleştirildi. Şablonlar, ilişkili CSS ve görüntü dosyaları gibi jQuery kullanıcı arabirimi için gereken en düşük kaynak dosyaları kümesini de içerir.

<a id="RTM-2"></a>
### <a name="change-changed-the-default-modelmetadataprovider-back-to-dataannotationsmodelmetadataprovider"></a>Değişiklik: varsayılan ModelMetadataProvider geri DataAnnotationsModelMetadataProvider olarak değiştirildi

ASP.NET MVC 3 ' ün RC2 sürümü, var olan *DataAnnotationsModelMetadataProvider* sınıfının en üstünde bir performans geliştirmesi olarak önbelleğe almayı sağlayan bir *cacheddataannotationsmetadataprovider* sınıfı sunmuştur. Ancak, bu uygulamayla ilgili bazı hatalar raporlandı, bu nedenle değişiklik geri döndürülüyor ve [ASP.net WebStack](https://github.com/aspnet/AspNetWebStack)'TE bulunan MVC Futures projesine taşındı.

<a id="RTM-3"></a>
### <a name="fixed-pasting-part-of-a-razor-expression-that-contains-whitespace-results-in-it-being-reversed"></a>Düzeltildi: boşluk içeren bir Razor ifadesinin parçasını geri çevrilme sonucu

ASP.NET MVC 3 ' ün yayın öncesi sürümlerinde, Razor dosyasına boşluk içeren bir Razor ifadesinin parçasını yapıştırdığınızda elde edilen ifade ters çevrilir. Örneğin, aşağıdaki Razor kod bloğunu göz önünde bulundurun:

[!code-cshtml[Main](mvc3-release-notes/samples/sample6.cshtml)]

İlk yöntemde "ilk param" metnini seçip ikinci yönteme bir bağımsız değişken olarak yapıştırırsanız, sonuç aşağıdaki gibidir:

[!code-cshtml[Main](mvc3-release-notes/samples/sample7.cshtml)]

Doğru davranış, yapıştırma işleminin aşağıdakilere neden olması gerekir:

[!code-cshtml[Main](mvc3-release-notes/samples/sample8.cshtml)]

Bu sorun, yapıştırma işlemi sırasında ifadenin doğru korunması için RTM sürümünde düzeltildi.

<a id="RTM-4"></a>
### <a name="fixed-renaming-a-razor-file-that-is-opened-in-the-editor-disables-syntax-colorization-and-intellisense"></a>Düzeltildi: düzenleyicide açılan bir Razor dosyasının yeniden adlandırılması, söz dizimi renklendirmesi ve IntelliSense 'i devre dışı bırakır

Dosya düzenleyici penceresinde açıldığında Razor dosyasını Çözüm Gezgini kullanarak yeniden adlandırmak, söz dizimi vurgulamanın ve IntelliSense 'in bu dosya için çalışmayı durdurmasına neden olur. Bu, bir yeniden adlandırmadan sonra vurgulama ve IntelliSense 'in sürdürülmesi için düzeltildi.

<a id="RTM-KI"></a>
## <a name="known-issues"></a>Bilinen Sorunlar

- NuGet Paket Yöneticisi konsolu açıkken Visual Studio 2010 SP1 Beta 'yı kapatırsanız, Visual Studio kilitleniyor ve yeniden başlatılmaya çalışır. Bu, Visual Studio 2010 SP1 'in RTM sürümünde düzeltilecektir.
- ASP.NET MVC 3 yükleyicisi yalnızca NuGet paket yöneticisinin bir başlangıç sürümünü yükleyebiliyor. İlk sürümü yükledikten sonra NuGet, Visual Studio Uzantı Yöneticisi kullanılarak yüklenebilir ve güncelleştirilir. Zaten NuGet yüklüyse, NuGet 'in en son sürümüne güncelleştirmek için Visual Studio Uzantı galerisine gidin.
- Bir çözüm klasörü içinde yeni bir ASP.NET MVC 3 projesi oluşturmak bir *NullReferenceException* hatasına neden olur. Geçici çözüm, çözümün kökünde ASP.NET MVC 3 projesini oluşturmak ve çözüm klasörüne taşımadır.
- Yükleyici, ASP.NET MVC 'nin önceki sürümlerinden daha uzun sürebilir. Bunun nedeni, Visual Studio 2010 bileşenlerini güncelleştirmeleridir.
- ReSharper yüklendiğinde IntelliSense Razor söz dizimi çalışmaz. ReSharper yüklüyse ve ASP.NET MVC 3 ' teki Razor IntelliSense desteğinden yararlanmak istiyorsanız, bunları bugün birlikte kullanmanın yollarını açıklayan [Razor IntelliSense ve ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) for Hadi Hariri bloguna bakın.
- ASP.NET MVC 3 ' ün beta sürümüyle oluşturulan CCSHTML ve VBHTML görünümlerinin, proje yayımlandığında bu görünüm türlerinin atlandığından dolayı yapı eylemi doğru şekilde ayarlanmamış. Bu dosyalar için derleme eylemi değeri "Içerik" olarak ayarlanmalıdır. ASP.NET MVC 3 RTM, yeni dosyalar için bu sorunu düzeltir, ancak ön sürüm sürümleriyle oluşturulan bir proje için mevcut dosyalar için ayarı düzeltmez.
- ![](mvc3-release-notes/_static/image3.png)
- Yükleme sırasında, EULA kabulü iletişim kutusu, lisans koşullarını amaçlanan bir pencerede görüntüler.
- Bir Razor görünümü (. cshtml dosyası) düzenlenirken, Visual Studio 'daki denetleyiciye git menü öğesi kullanılamayacak ve kod parçacığı yok.
- Visual Studio 'nun yüklü olmadığı bir bilgisayara Visual Web Developer Express için ASP.NET MVC 3 ' ü yükler ve daha sonra Visual Studio 'yu yüklerseniz, ASP.NET MVC 3 ' ü yeniden yüklemeniz gerekir. Visual Studio ve Visual Web Developer Express, ASP.NET MVC 3 yükleyicisi tarafından yükseltilen bileşenleri paylaşır. Visual Studio için ASP.NET MVC 3 ' ü Visual Web Developer Express olmayan bir bilgisayara yüklerseniz ve daha sonra Visual Web Developer Express 'i yüklüyorsanız aynı sorun geçerlidir.

<a id="RTM-BC"></a>
## <a name="breaking-changes"></a>Yeni Değişiklikler

- Önceki ASP.NET MVC sürümlerinde, birkaç durum dışında istek başına eylem filtreleri oluşturulur. Bu davranış hiç garantili bir davranıştı, ancak yalnızca bir uygulama ayrıntısı ve filtrelerin sözleşmesinin durum bilgisiz durumu dikkate alınmıştı. ASP.NET MVC 3 ' te filtreler daha fazla kararlılık olarak önbelleğe alınır. Bu nedenle, örnek durumunu hatalı şekilde depolayan herhangi bir özel eylem filtresi bozuk olabilir.
- Özel durum filtreleri için yürütme sırası, aynı *sıra* değerine sahip özel durum filtreleri için değişti. ASP.NET MVC 2 ve önceki sürümlerinde, bir eylem yöntemiyle aynı *sıra* değerine sahip olan denetleyicideki özel durum filtreleri, eylem yöntemindeki özel durum filtrelerinden önce yürütülür. Bu, genellikle özel durum filtrelerinin belirtilen bir *sipariş* değeri olmadan uygulanması durumunda olur. ASP.NET MVC 3 ' te, bu sıra, en belirli özel durum işleyicisinin ilk kez çalışması için tersine çevrildi. Önceki sürümlerde olduğu gibi, *Order* özelliği açıkça belirtilmişse, filtreler belirtilen sırada çalıştırılır.
- *VirtualPathProviderViewEngine* taban sınıfına *FileExtensions* adlı yeni bir özellik eklenmiştir. ASP.NET, yola (ada göre değil) göre bir görünüm ararken, yalnızca bu yeni özellik tarafından belirtilen listede yer alan bir dosya uzantısına sahip görünümler kabul edilir. Bu, Web form görünümleri için özel bir dosya uzantısını etkinleştirmek üzere bir özel derleme sağlayıcısının kaydedildiği ve sağlayıcının bir ad yerine tam yol kullanarak bu görünümlere başvurduğu uygulamalarda önemli bir değişiklik olduğunu ortadan kaldırırsınız. Geçici çözüm, *FileExtensions* özelliğinin değerini özel dosya uzantısını içerecek şekilde değiştirmektir.
- *IControllerFactory* arabirimini doğrudan uygulayan özel denetleyici fabrikası uygulamalarının, bu sürümdeki arabirime eklenen yeni *Getcontrollersessionbehavior* yönteminin bir uygulamasını sağlaması gerekir. Genel olarak, bu arabirimi doğrudan uygulamanız ve bunun yerine *DefaultControllerFactory*'den sınıfınızı türetmeniz önerilir.

<a id="_Toc2"></a>
## <a name="changes-in-aspnet-mvc-3-rc2"></a>ASP.NET MVC 3 RC2 'deki değişiklikler

Bu bölümde, RC sürümünden bu yana ASP.NET MVC 3 RC2 sürümünde yapılan değişiklikler (yeni özellikler ve hata düzeltmeleri) açıklanmaktadır.

<a id="_Toc2_1"></a>
### <a name="project-templates-changed-to-include-jquery-144-jquery-validation-17-and-jquery-ui-186"></a>Proje şablonları jQuery 1.4.4, jQuery doğrulaması 1,7 ve jQuery kullanıcı arabirimini Içerecek şekilde değiştirilmiştir 1.8.6

ASP.NET MVC 3 için proje şablonları artık jQuery, jQuery Validation ve jQuery Kullanıcı arabiriminin en son sürümlerini içerir. jQuery kullanıcı arabirimi, proje şablonlarına yeni bir ektir ve faydalı Kullanıcı arayüzü pencere öğeleri sağlar. JQuery kullanıcı arabirimi hakkında daha fazla bilgi için, şu giriş sayfasını ziyaret edin: [http://jqueryui.com/](http://jqueryui.com/).

<a id="_Toc2_2"></a>
### <a name="added-additionalmetadataattribute-class"></a>"AdditionalMetadataAttribute" sınıfı eklendi

Bir model özelliğinin *ModelMetadata. Addivalues* sözlüğünü doldurmak Için *additionalmetadataattribute* sınıfını kullanabilirsiniz.

Örneğin, bir görünüm modelinin yalnızca bir yöneticiye gösterilmesi gereken özellikleri olduğunu varsayalım. Bu modele, aşağıdaki örnekte olduğu gibi, yalnızca anahtar olarak admin ve değer olarak true gibi yeni özniteliğiyle açıklama eklenebilir:

[!code-csharp[Main](mvc3-release-notes/samples/sample9.cs)]

Bu meta veriler, bir ürün görünümü modeli işlendiğinde herhangi bir görüntü veya düzenleyici şablonu için kullanılabilir hale getirilir. Meta veri bilgilerini yorumlamak için uygulama geliştiricisi olarak kullanılır.

<a id="_Toc2_3"></a>
### <a name="improved-view-scaffolding"></a>Geliştirilmiş görünüm yapı Iskelesi

Yapı iskelesi görünümleri için kullanılan T4 şablonları artık, örneğin, *TextBoxFor*yardımcıları yerine *editoras* gibi şablon yardımcı yöntemlerine çağrılar oluşturur. Bu değişiklik, Görünüm Ekle iletişim kutusu bir görünüm oluşturduğunda veri ek açıklaması öznitelikleri biçimindeki modeldeki meta veriler için desteği geliştirir.

Ekleme görünümü yapı iskelesi Ayrıca, kurala göre modeldeki birincil anahtar bilgilerinin gelişmiş algılamayı ve kullanımını da içerir. Örneğin, Görünüm Ekle iletişim kutusu bu bilgileri, birincil anahtar değerinin düzenlenebilir form alanı olarak dolandırıcıya katlanmadığından emin olmak için kullanır.

Varsayılan düzenleme ve oluşturma şablonları, istemci doğrulaması için gereken jQuery betiklerine yönelik başvuruları içerir.

<a id="_Toc2_4"></a>
### <a name="added-htmlraw-method"></a>HTML. RAW yöntemi eklendi

Varsayılan olarak, Razor Görünüm altyapısı HTML-tüm değerleri kodlar. Örneğin, aşağıdaki kod parçacığı, sayfada `<strong>Hello World!</strong>`olarak görüntülenmek üzere selamlama değişkeninin içindeki HTML 'yi kodluyor.

[!code-cshtml[Main](mvc3-release-notes/samples/sample10.cshtml)]

Yeni *HTML. RAW* yöntemi, içeriğin güvenli olduğu bilindiğinde, KODLANAMAYAN HTML 'yi görüntülemenin basit bir yolunu sağlar. Aşağıdaki örnek aynı dizeyi görüntüler, ancak dize biçimlendirme olarak işlenir:

[!code-cshtml[Main](mvc3-release-notes/samples/sample11.cshtml)]

<a id="_Toc2_5"></a>
### <a name="renamed-controllerviewmodel-property-and-the-view-property-to-viewbag"></a>"Controller. ViewModel" özelliği ve "View" özelliği "ViewBag" olarak yeniden adlandırıldı

Daha önce, *denetleyicinin* ViewModel özelliği bir görünümün *View* özelliğine karşılık *gelendir* . Bu özelliklerin her ikisi de, *ViewDataDictionary* nesnesinin değerlerine dinamik özellik erişimcisi sözdizimi kullanılarak erişmenin bir yolunu sağlar. Her iki özellik de karışıklık olmaması ve daha tutarlı olması için aynı olacak şekilde yeniden adlandırıldı.

<a id="_Toc2_6"></a>
### <a name="renamed-controllersessionstateattribute-class-to-sessionstateattribute"></a>"ControllerSessionStateAttribute" sınıfı "SessionStateAttribute" olarak yeniden adlandırıldı

*Controllersessionstateattribute* sınıfı, ASP.NET MVC 3 RC sürümünde sunulmuştur. Özelliği daha kısa daha fazla olacak şekilde yeniden adlandırıldı.

<a id="_Toc2_7"></a>
### <a name="renamed-remoteattribute-fields-property-to-additionalfields"></a>RemoteAttribute "Fields" özelliği "AdditionalFields" olarak yeniden adlandırıldı

*Remoteattribute* sınıfının *Fields* özelliği kullanıcılar arasında bazı karışıklıklara neden oldu. Bu özelliğin *Additionalfields* olarak yeniden adlandırılması, amacını belirler.

<a id="_Toc2_8"></a>
### <a name="renamed-skiprequestvalidationattribute-to-allowhtmlattribute"></a>"SkipRequestValidationAttribute", "AllowHtmlAttribute" olarak yeniden adlandırıldı

*Skiprequestvalidationattribute* özniteliği, amaçlanan kullanımını daha iyi temsil etmek Için *Allowwhtmlattribute* olarak yeniden adlandırıldı.

<a id="_Toc2_9"></a>
### <a name="changed-htmlvalidationmessage-method-to-display-the-first-useful-error-message"></a>"HTML. ValidationMessage" yöntemi, Ilk yararlı hata Iletisini görüntüleyecek şekilde değiştirildi

*HTML. ValidationMessage* yöntemi, yalnızca ilk hatayı görüntülemek yerine ilk yararlı hata iletisini göstermek için düzeltildi.

Model bağlama sırasında, *ModelState* sözlüğü birden çok kaynaktan, modelin kendisinden ( *IValidatableObject*uygularsa), özelliğe uygulanan doğrulama özniteliklerinden ve özellik erişildiği sırada oluşturulan özel durumlarla birlikte, bu özellik hakkındaki hata iletileriyle doldurulabilir.

*HTML. ValidationMessage* yöntemi bir doğrulama iletisi görüntülediğinde, bu durum genellikle son kullanıcıya yönelik değildir çünkü bu, bir özel durum içeren model durumu girdilerini atlar. Bunun yerine, yöntemi bir özel durumla ilişkilendirilmemiş ilk doğrulama iletisini arar ve bu iletiyi görüntüler. Böyle bir ileti bulunmazsa, varsayılan olarak ilk özel durumla ilişkili genel bir hata iletisi olur.

<a id="_Toc2_10"></a>
### <a name="fixed-model-declaration-to-not-add-whitespace-to-the-document"></a>Belgeye boşluk eklemek için @model bildirimi düzeltildi

Önceki sürümlerde, bir görünümün en üstündeki `@model` bildirimi işlenen HTML çıktısına boş bir satır ekledi. Bu, bildirimin boşluk sunmaz için düzeltildi.

<a id="_Toc2_11"></a>
### <a name="added-fileextensions-property-to-view-engines-to-support-engine-specific-file-names"></a>Altyapıya özgü dosya adlarını desteklemek için altyapıyı görüntülemek için "FileExtensions" özelliği eklendi

Bir görünüm altyapısı, aşağıdaki örnekte olduğu gibi açık bir görünüm yolunu kullanarak bir görünüm döndürebilir:

[!code-csharp[Main](mvc3-release-notes/samples/sample12.cs)]

İlk görünüm altyapısı her zaman görünümü işlemeye çalışır. Varsayılan olarak, Web Forms Görünüm altyapısı ilk görüntüleme altyapısıdır; Web Forms altyapısı bir Razor görünümünü işleyemediği için bir hata oluşur. Görüntüleme motorları artık destekledikleri dosya uzantılarını belirtmek için kullanılan bir *FileExtensions* özelliğine sahiptir. ASP.NET bir görünüm altyapısının bir dosyayı işlenip işleyemeyeceğini belirlediğinde, bu özellik denetlenir. Bu, bir son değişikliklerdir ve daha fazla ayrıntı bu belgenin [son değişiklikler](#_Toc2_BC) bölümüne dahildir.

<a id="_Toc2_12"></a>
### <a name="fixed-labelfor-helper-to-emit-the-correct-value-for-the-for-attribute"></a>"For" özniteliği için doğru değeri yayma için "LabelFor" Yardımcısı düzeltildi

Bir hata, kendi KIMLIĞI yerine *giriş* öğesinin *ad* özniteliğiyle eşleşen bir öznitelik *için* *LabelFor* metodu olarak işlendiği düzeltildi. W3C 'a göre, *for* özniteliği *giriş* öğesinin kimliğiyle eşleşmelidir.

<a id="_Toc2_13"></a>
### <a name="fixed-renderaction-method-to-give-explicit-values-precedence-during-model-binding"></a>Model bağlama sırasında açık değerlere öncelik vermek için "RenderAction" yöntemi düzeltildi

Önceki sürümlerde, *RenderAction* yöntemine geçirilen açık değerler, bir alt eylem içinde model bağlama sırasında geçerli form değerleri dikkate alınmaz. Bu çözüm, model bağlama sırasında açık değerlerin öncelikli olmasını sağlar.

<a id="_Toc2_BC"></a>
## <a name="breaking-changes"></a>Yeni Değişiklikler

- Önceki ASP.NET MVC sürümlerinde, birkaç durum dışında istek başına eylem filtreleri oluşturulmuştur. Bu davranış hiç garantili bir davranıştı, ancak yalnızca bir uygulama ayrıntısı ve filtrelerin sözleşmesinin durum bilgisiz durumu dikkate alınmıştı. ASP.NET MVC 3 ' te filtreler daha fazla kararlılık olarak önbelleğe alınır. Bu nedenle, örnek durumunu hatalı şekilde depolayan herhangi bir özel eylem filtresi bozuk olabilir.
- Özel durum filtreleri için yürütme sırası, aynı *sıra* değerine sahip özel durum filtreleri için değişti. ASP.NET MVC 2 ve önceki sürümlerinde, bir eylem yöntemiyle aynı *sıra* değerine sahip olan denetleyicideki özel durum filtreleri, eylem yöntemindeki özel durum filtrelerinden önce yürütüldü. Bu, genellikle özel durum filtrelerinin belirtilen bir *sipariş* değeri olmadan uygulanması durumunda olur. ASP.NET MVC 3 ' te, bu sıra, en belirli özel durum işleyicisinin ilk kez çalışması için tersine çevrildi. Önceki sürümlerde olduğu gibi, *Order* özelliği açıkça belirtilmişse, filtreler belirtilen sırada çalıştırılır.
- *VirtualPathProviderViewEngine* taban sınıfına *FileExtensions* adlı yeni bir özellik eklenmiştir. ASP.NET, yola (ada göre değil) göre bir görünüm ararken, yalnızca bu yeni özellik tarafından belirtilen listede yer alan bir dosya uzantısına sahip görünümler kabul edilir. Bu, Web form görünümleri için özel bir dosya uzantısını etkinleştirmek üzere bir özel derleme sağlayıcısının kaydedildiği ve sağlayıcının bir ad yerine tam yol kullanarak bu görünümlere başvurduğu uygulamalarda önemli bir değişiklik olduğunu ortadan kaldırırsınız. Geçici çözüm, *FileExtensions* özelliğinin değerini özel dosya uzantısını içerecek şekilde değiştirmektir.
- *IControllerFactory* arabirimini doğrudan uygulayan özel denetleyici fabrikası uygulamalarının, bu sürümdeki arabirime eklenen yeni *Getcontrollersessionbehavior* yönteminin bir uygulamasını sağlaması gerekir. Genel olarak, bu arabirimi doğrudan uygulamanız ve bunun yerine *DefaultControllerFactory*'den sınıfınızı türetmeniz önerilir.

<a id="_Toc2_KI"></a>
## <a name="known-issues"></a>Bilinen Sorunlar

- ASP.NET MVC 3 yükleyicisi yalnızca NuGet paket yöneticisinin bir başlangıç sürümünü yükleyebiliyor. İlk sürümü yükledikten sonra NuGet, Visual Studio Uzantı Yöneticisi kullanılarak yüklenebilir ve güncelleştirilir. Zaten NuGet yüklüyse, NuGet 'in en son sürümüne güncelleştirmek için Visual Studio Uzantı galerisine gidin.
- Bir çözüm klasörü içinde yeni bir ASP.NET MVC 3 projesi oluşturmak bir *NullReferenceException* hatasına neden olur. Geçici çözüm, çözümün kökünde ASP.NET MVC 3 projesini oluşturmak ve çözüm klasörüne taşımadır.
- Yükleyici, ASP.NET MVC 'nin önceki sürümlerinden daha uzun sürebilir. Bunun nedeni, Visual Studio 2010 bileşenlerini güncelleştirmeleridir.
- ReSharper yüklendiğinde IntelliSense Razor söz dizimi çalışmaz. ReSharper yüklüyse ve ASP.NET MVC 3 RC2 içindeki Razor IntelliSense desteğinden yararlanmak istiyorsanız, bunları bugün birlikte kullanmanın yollarını açıklayan [Razor IntelliSense ve ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) for Hadi Hariri bloguna bakın.
- ASP.NET MVC 3 ' ün beta sürümüyle oluşturulan CSHTML ve VBHTML görünümlerinin, proje yayımlandığında bu görünüm türlerinin atlandığından dolayı yapı eylemi doğru şekilde ayarlanmamış. Bu dosyalar için *derleme eylemi* değeri içerik olarak ayarlanmalıdır ". ASP.NET MVC 3 RC2, yeni dosyalar için bu sorunu düzeltir, ancak beta sürümü ile oluşturulan bir proje için mevcut dosyalar için ayarı düzeltmez.![](mvc3-release-notes/_static/image4.png)
- Yükleme sırasında, EULA kabulü iletişim kutusu, lisans koşullarını amaçlanan bir pencerede görüntüler.
- Bir Razor görünümü (. cshtml dosyası) düzenlenirken, Visual Studio 'daki denetleyiciye git menü öğesi kullanılamayacak ve kod parçacığı yok.
- Visual Studio 'nun yüklü olmadığı bir bilgisayara Visual Web Developer Express için ASP.NET MVC 3 ' ü yükler ve daha sonra Visual Studio 'yu yüklerseniz, ASP.NET MVC 3 ' ü yeniden yüklemeniz gerekir. Visual Studio ve Visual Web Developer Express, ASP.NET MVC 3 yükleyicisi tarafından yükseltilen bileşenleri paylaşır. Visual Studio için ASP.NET MVC 3 ' ü Visual Web Developer Express olmayan bir bilgisayara yüklerseniz ve daha sonra Visual Web Developer Express 'i yüklüyorsanız aynı sorun geçerlidir.
- ASP.NET MVC 3 RC 2 yüklemesi, zaten yüklüyse NuGet 'i güncelleştirmez. NuGet 'i yükseltmek için Visual Studio Uzantı Yöneticisi 'ne gidin ve kullanılabilir bir güncelleştirme olarak gösterilmesi gerekir. NuGet 'i buradan en son sürüme yükseltebilirsiniz.

<a id="TOC_ASP_NET_3_RC"></a>
## <a name="aspnet-mvc-3-release-candidate"></a>ASP.NET MVC 3 sürüm adayı

ASP.NET MVC sürüm adayı 9 Kasım 2010 ' de yayımlanmıştır.

<a id="_Toc276711785"></a>
## <a name="new-features-in-aspnet-mvc-3-rc"></a>ASP.NET MVC 3 RC 'deki yeni özellikler

Bu bölümde beta sürümünden bu yana ASP.NET MVC 3 RC sürümünde tanıtılan özellikler açıklanmaktadır.

<a id="_Toc276711786"></a>
### <a name="nuget-package-manager"></a>NuGet Paket Yöneticisi

ASP.NET MVC 3, Visual Studio projelerine kitaplık ve araç eklemeye yönelik tümleşik bir paket yönetim aracı olan NuGet Paket Yöneticisi 'Ni (eski adıyla NuPack olarak biliniyordu) içerir. Bu araç, geliştiricilerin kaynak ağacına bir kitaplık almak için bugün aldığı adımları otomatik hale getirir.

NuGet ile bir komut satırı aracı olarak, Visual Studio 2010 içinde tümleşik bir konsol penceresi olarak, Visual Studio bağlam menüsünden ve bir PowerShell cmdlet 'leri kümesi olarak çalışabilirsiniz.

NuGet hakkında daha fazla bilgi için [NuGet belgelerini](https://docs.microsoft.com/nuget/)okuyun.

<a id="_Toc276711787"></a>
### <a name="improved-new-project-dialog-box"></a>Geliştirilmiş "yeni proje" Iletişim kutusu

Yeni bir proje oluşturduğunuzda, yeni proje iletişim kutusu artık görünüm altyapısının yanı sıra bir ASP.NET MVC proje türünü belirtmenizi sağlar.

![](mvc3-release-notes/_static/image5.png)

İletişim kutusunda listelenen şablon ve görünüm altyapısının listesini değiştirme desteği bu sürüme dahildir.

Varsayılan şablonlar şunlardır:

Olmamalıdır. ASP.NET MVC projeleri için varsayılan dizin yapısı, varsayılan ASP.NET MVC stillerini içeren bir site. css dosyası ve varsayılan JavaScript dosyalarını içeren bir Scripts dizini dahil olmak üzere, bir MVC projesi için en az bir dosya kümesi içerir.

Internet uygulaması. ASP.NET MVC ile üyelik sağlayıcısı 'nın nasıl kullanılacağını gösteren örnek işlevselliği içerir.

İletişim kutusunda görüntülenen proje şablonlarının listesi Windows kayıt defterinde belirtilmiştir.

<a id="_Toc276711788"></a>
### <a name="sessionless-controllers"></a>Oturumsuz denetleyiciler

Yeni *Controllersessionstateattribute* , bir [System. Web. SessionState. SessionStateBehavior](https://msdn.microsoft.com/library/system.web.sessionstate.sessionstatebehavior.aspx) numaralandırma değeri belirterek denetleyiciler için oturum durumu davranışı üzerinde daha fazla denetim sağlar.

Aşağıdaki örnekte, bir denetleyiciye yönelik tüm istekler için oturum durumunun nasıl kapatılacağı gösterilmektedir.

[!code-csharp[Main](mvc3-release-notes/samples/sample13.cs)]

Aşağıdaki örnek, bir denetleyiciye yönelik tüm istekler için salt okuma oturum durumunun nasıl ayarlanacağını gösterir.

[!code-csharp[Main](mvc3-release-notes/samples/sample14.cs)]

<a id="_Toc276711789"></a>
### <a name="new-validation-attributes"></a>Yeni doğrulama öznitelikleri

#### <a name="compareattribute"></a>CompareAttribute

Yeni *CompareAttribute* doğrulama özniteliği, bir modelin iki farklı özelliğinin değerlerini karşılaştırmanıza imkan tanır. Aşağıdaki örnekte, *ComparePassword* özelliğinin geçerli olması için *Password* alanıyla eşleşmesi gerekir.

[!code-csharp[Main](mvc3-release-notes/samples/sample15.cs)]

#### <a name="remoteattribute"></a>RemoteAttribute

Yeni *Remoteattribute* doğrulama özniteliği, istemci tarafı doğrulamanın gerçek doğrulama mantığını gerçekleştiren sunucuda bir yöntemi çağırmasını sağlayan jQuery doğrulama eklentisinin uzak doğrulayıcısı avantajlarından yararlanır.

Aşağıdaki örnekte, *UserName* özelliğinin *remoteattribute* özelliği uygulandı. Bu özellik bir düzenleme görünümünde düzenlenirken, istemci doğrulaması bu alanı doğrulamak için *Userscontroller* sınıfında *usernameavailable* adlı bir eylem çağırır.

[!code-csharp[Main](mvc3-release-notes/samples/sample16.cs)]

Aşağıdaki örnek, ilgili denetleyiciyi gösterir.

[!code-csharp[Main](mvc3-release-notes/samples/sample17.cs)]

Varsayılan olarak, özniteliğin uygulandığı özellik adı eylem yöntemine sorgu-dize parametresi olarak gönderilir.

<a id="_Toc276711790"></a>
### <a name="new-overloads-for-labelfor-and-labelformodel-methods"></a>"LabelFor" ve "LabelForModel" yöntemleri için yeni aşırı yüklemeler

Etiket metnini belirtmenize izin veren *LabelFor* ve *LabelForModel* metotları için yeni aşırı yüklemeler eklenmiştir. Aşağıdaki örnek, bu aşırı yüklemelerin nasıl kullanılacağını göstermektedir.

[!code-cshtml[Main](mvc3-release-notes/samples/sample18.cshtml)]

<a id="_Toc276711791"></a>
### <a name="child-action-output-caching"></a>Alt eylem çıkışı önbelleğe alma

*OutputCacheAttribute* , *HTML. RenderAction* veya *HTML. Action* yardımcı yöntemleri kullanılarak çağrılan alt eylemlerin çıktı önbelleğe alınmasını destekler. Aşağıdaki örnekte, başka bir eylemi çağıran bir görünüm gösterilmektedir.

[!code-cshtml[Main](mvc3-release-notes/samples/sample19.cshtml)]

*Getdate* eylemine *OutputCacheAttribute*ile açıklama eklenir:

[!code-csharp[Main](mvc3-release-notes/samples/sample20.cs)]

Bu kod çalıştırıldığında, HTML. Action ("GetDate") çağrısının sonucu 100 saniye boyunca önbelleğe alınır.

<a id="_Toc276711792"></a>
### <a name="add-view-dialog-box-improvements"></a>"Görünüm Ekle" Iletişim kutusu geliştirmeleri

Türü kesin belirlenmiş bir görünüm eklediğinizde, Görünüm Ekle iletişim kutusu artık, çok sayıda çekirdek .NET Framework türü gibi önceki sürümlerden daha fazla uygulanamaz türü filtreler. Ayrıca, liste artık sınıf adına göre sıralanır ve tam nitelikli tür adı tarafından değil, türleri bulmayı kolaylaştırır. Örneğin, tür adı şu örnekte olduğu gibi görüntülenir:

ClassName (ad alanı)

Önceki sürümlerde, bu, aşağıdaki gibi görüntülenmiş olabilir:

Namespace. ClassName

<a id="_Toc276711793"></a>
### <a name="granular-request-validation"></a>Ayrıntılı Istek doğrulaması

*ValidateInputAttribute* 'un *exclude* özelliği artık yok. Bunun yerine, model bağlama sırasında bir modelin belirli özellikleri için istek doğrulamanın atlanmasını sağlamak üzere, New *Skiprequestvalidationattribute*' u kullanın.

Örneğin, bir blog gönderisini düzenlemek için bir eylem yönteminin kullanıldığını varsayalım:

[!code-csharp[Main](mvc3-release-notes/samples/sample21.cs)]

Aşağıdaki örnek bir blog gönderisi için görünüm modelini gösterir.

[!code-csharp[Main](mvc3-release-notes/samples/sample22.cs)]

Bir Kullanıcı Açıklama özelliği için bir biçimlendirme gönderdiğinde, istek doğrulaması nedeniyle model bağlama başarısız olur. Blog gönderisi açıklaması için model bağlama sırasında istek doğrulamayı devre dışı bırakmak için, aşağıdaki örnekte gösterildiği gibi, *SkipRequpestValidationAttribute* özelliğine uygulayın:.

[!code-csharp[Main](mvc3-release-notes/samples/sample23.cs)]

Alternatif olarak, modelin her özelliği için istek doğrulamayı devre dışı bırakmak için, eylem yöntemine *false* değeri Ile *ValidateInputAttribute* uygulayın:

[!code-csharp[Main](mvc3-release-notes/samples/sample24.cs)]

<a id="_Toc276711794"></a>
## <a name="breaking-changes"></a>Yeni Değişiklikler

- Özel durum filtreleri için yürütme sırası, aynı *sıra* değerine sahip özel durum filtreleri için değişti. ASP.NET MVC 2 ve önceki sürümlerinde, bir eylem yöntemiyle aynı *sırada* olan denetleyicideki özel durum filtreleri, eylem yöntemindeki özel durum filtrelerinden önce yürütüldü. Bu, genellikle özel durum filtrelerinin belirtilen bir *sipariş* değeri olmadan uygulanması durumunda olur. ASP.NET MVC 3 ' te, bu sıra, en belirli özel durum işleyicisinin ilk kez çalışması için tersine çevrildi. Önceki sürümlerde olduğu gibi, *Order* özelliği açıkça belirtilmişse, filtreler belirtilen sırada çalıştırılır.
- *VirtualPathProviderViewEngine* taban sınıfına *FileExtensions* adlı yeni bir özellik eklendi. Yola göre bir görünüm ararken (ada göre değil), yalnızca bu yeni özellik tarafından belirtilen listede yer alan bir dosya uzantısına sahip görünümler kabul edilir. Bu, Web form görünümleri için özel bir dosya uzantısını etkinleştirmek üzere özel bir yapı sağlayıcısı kaydeden ve bir ad yerine tam yol kullanarak bu görünümlere başvuruda bulunan bir önemli değişiklik. Geçici çözüm, *FileExtensions* özelliğinin değerini özel dosya uzantısını içerecek şekilde değiştirmektir.

<a id="_Toc276711795"></a>
## <a name="known-issues"></a>Bilinen Sorunlar

- Yükleyici, Visual Studio 2010 bileşenlerini güncelleştirdiği için ASP.NET MVC 'nin önceki sürümlerinden çok daha uzun sürebilir.
- Türü kesin belirlenmiş görünüm, salt yazılır özellikleri seçerken ekleme görünümü yapı iskelesi. Bunlar her zaman yapı iskelesi tarafından yok sayılır. Görünüm Ekle iletişim kutusu ayrıca "düzenleme" veya "Oluştur" görünümü oluştururken salt okuma özelliklerini de düzenler. Salt okuma özellikleri yalnızca görüntüleme ve liste görünümleri için scafkatmalı olmalıdır.
- ASP.NET MVC 3, zaman uyumsuz CTP ile birlikte yüklendiğinde hata ayıklama çalışmaz. ASP.NET MVC 3, zaman uyumsuz CTP ile yan yana yüklenemez. Hata ayıklamayı onarmak için zaman uyumsuz CTP 'yi kaldırın. Daha fazla ayrıntı için, ASP.NET MVC 3 RC 'nin tüm parçalarını kaldırma hakkında [Bu blog gönderisini](http://drew-prog.blogspot.com/2010/11/how-to-uninstall-microsoft-aspnet-mvc-3.html) okuyun.
- ReSharper yüklendiğinde Razor IntelliSense çalışmaz. ReSharper yüklüyse ve ASP.NET MVC 3 RC 'de Razor IntelliSense desteğinden yararlanmak istiyorsanız, lütfen [Bu blog gönderisini](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) bugün birlikte kullanmanın yollarını açıklayan JetBrains 'den okuyun.
- ASP.NET MVC 3 Beta sürümü ile oluşturulan CSHTML ve VBHTML görünümlerinin, derleme eylemi, yayımlarından yok edilecek şekilde doğru değil. Bu dosyalar için *derleme eylemi* "içerik" olarak ayarlanmalıdır. ASP.NET MVC 3 RC, yeni dosyalar için bu sorunu düzeltir, ancak beta ile oluşturulan bir proje için mevcut dosyalar için ayarı düzeltmez.
- Yükleyici, Visual Studio 2010 bileşenlerini güncelleştirdiği için ASP.NET MVC 'nin önceki sürümlerinden çok daha uzun sürebilir.
- "Düzenle" türü kesin olarak belirlenmiş görünüm yapı iskelesi, salt okuma özelliklerini seçerek ekleme görünümü oluşturma. Benzer şekilde, salt yazılır özellikler "görüntüleme" görünümleri için yapı iskelesi yapılır.
- Yükleme sırasında, EULA kabulü iletişim kutusu, lisans koşullarını amaçlanan bir pencerede görüntüler.
- Visual Studio Async CTP 'nin yüklenmesi, ASP.NET MVC 3 araç yükleme 'nin bir parçası olarak dahil edilen Razor sürümüyle çakışmaya neden olur. Hem Visual Studio Async CTP 'yi hem de Razor sürümünü aynı makineye yüklemeyi denediğinizden emin olun.
- Bir Razor görünümü (. cshtml dosyası) düzenlenirken, Visual Studio 'daki denetleyiciye git menü öğesi kullanılamayacak ve kod parçacığı yok.

<a id="TOC_ASP_NET_3_Beta"></a>
## <a name="aspnet-mvc-3-beta"></a>ASP.NET MVC 3 Beta

ASP.NET MVC 3 Beta sürümü 6 Ekim 2010 ' de yayımlanmıştır. Aşağıdaki notlar Beta sürümüne özgüdür ve yukarıdaki ASP.NET MVC 3 sürüm adayı bölümünde başvurulan tüm güncelleştirmeler veya değişikliklere tabidir.

## <a id="0.1__Toc274034215"></a>Yeni Featuresin ASP.NET MVC 3 Beta

<a id="0.1__Default_validation_system"></a>Bu bölümde ASP.NET MVC 3 Beta sürümünde tanıtılan özellikler açıklanmaktadır.

### <a id="0.1__Toc274034216"></a>NuGet Paket Yöneticisi

ASP.NET MVC 3, Visual Studio projelerine kitaplıklar ve araçlar eklemeye yönelik tümleşik bir paket yönetim aracı olan NuGet Paket Yöneticisi 'Ni içerir. Çoğu bölümde, geliştiricilerin kaynak ağacına bir kitaplık almak için bugün aldığı adımları otomatik hale getirir.

Bir komut satırı aracı olarak NuGet ile Visual Studio 2010 içinde tümleşik bir konsol penceresi olarak, Visual Studio bağlam menüsünden ve PowerShell cmdlet 'leri kümesi olarak çalışabilirsiniz.

NuGet hakkında daha fazla bilgi için [NuGet belgelerini](https://docs.microsoft.com/nuget/)okuyun.

### <a id="0.1__Toc274034217"></a>Geliştirilmiş yeni proje Iletişim kutusu

Yeni bir proje oluşturduğunuzda, yeni proje iletişim kutusu artık görünüm altyapısının yanı sıra bir ASP.NET MVC proje türünü belirtmenizi sağlar.

![](mvc3-release-notes/_static/image6.png)

İletişim kutusunda listelenen şablon ve görünüm altyapısının listesini değiştirme desteği bu yayına dahil değildir.

Varsayılan şablonlar şunlardır:

Olmamalıdır. ASP.NET MVC projeleri için varsayılan dizin yapısı, varsayılan ASP.NET MVC stillerini içeren küçük bir site. css dosyası ve varsayılan JavaScript dosyalarını içeren betikler dizini dahil olmak üzere, bir MVC projesi için en az bir dosya kümesi içerir.

Internet uygulaması. ASP.NET MVC içinde üyelik sağlayıcısının nasıl kullanılacağını gösteren örnek işlevselliği içerir.

### <a id="0.1__Toc274034218"></a>Razor görünümlerinde kesin olarak belirlenmiş modeller belirtmenin Basitleştirilmiş yolu

Türü kesin belirlenmiş Razor görünümleri için model türünü belirtmenin yolu, CSHTML görünümleri için yeni @model yönergesi ve VBHTML görünümleri için @ModelType yönergesi kullanılarak basitleştirilmiştir. ASP.NET MVC 'nin önceki sürümlerinde Razor görünümleri için kesin olarak belirlenmiş bir model bu şekilde belirtirsiniz:

[!code-cshtml[Main](mvc3-release-notes/samples/sample25.cshtml)]

Bu sürümde, aşağıdaki sözdizimini kullanabilirsiniz:

[!code-cshtml[Main](mvc3-release-notes/samples/sample26.cshtml)]

### <a id="0.1__Toc274034219"></a>Yeni ASP.NET Web sayfaları yardımcı yöntemleri için destek

Yeni ASP.NET Web sayfaları teknolojisi, görünümler ve denetleyicilere yaygın olarak kullanılan işlevleri eklemek için yararlı olan bir dizi yardımcı yöntem içerir. ASP.NET MVC 3, denetleyiciler ve görünümler içinde bu yardımcı yöntemlerin kullanılmasını destekler (uygun yerlerde). Bu yöntemler System. Web. yardımcılar derlemesinde bulunur. Aşağıdaki tabloda, ASP.NET Web sayfaları yardımcı yöntemlerinden bazıları listelenmiştir.

| **Yardımcınız** | **Açıklama** |
| --- | --- |
| Grafik | Bir görünüm içinde bir grafik oluşturur. Grafik. Towebımage, Chart. Save ve Chart. Write gibi yöntemleri içerir. |
| Ko | Doğru şekilde sallanmış ve karma hale getirilmiş parolalar oluşturmak için karma algoritmaları kullanır. |
| WebGrid | Bir nesne koleksiyonunu (genellikle bir veritabanındaki verileri) kılavuz olarak işler. Sayfalama ve sıralamayı destekler. |
| Web görüntüsü | Bir görüntü oluşturur. |
| Web postasından | Bir e-posta iletisi gönderir. |

Yardımcıları ve temel sözdizimini listeleyen bir hızlı başvuru konusu aşağıdaki URL 'de ASP.NET Razor söz dizimi belgelerinin bir parçası olarak kullanılabilir:

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-api-reference](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)

### <a id="0.1__Toc274034220"></a>Ek bağımlılık ekleme desteği

ASP.NET MVC 3 Preview 1 sürümünde derleme yaparken, geçerli sürüm iki yeni hizmet ve dört mevcut hizmet için ek destek ve bağımlılık çözümleme ve ortak hizmet bulucu desteği için geliştirilmiş destek içerir.

#### <a name="new-icontrolleractivator-interface-for-fine-grained-controller-instantiation"></a>Ayrıntılı denetleyici örneklemesi için yeni Icontrolleretkinleştirici arabirimi

Yeni Icontrolleretkinleştirici arabirimi, denetleyicilerin bağımlılık ekleme yoluyla nasıl örneklendiği konusunda daha ayrıntılı denetim sağlar. Aşağıdaki örnek, arabirimini göstermektedir:

[!code-csharp[Main](mvc3-release-notes/samples/sample27.cs)]

Bunu denetleyici fabrikası rolüne kontrast. Denetleyici fabrikası, her ikisi de bir denetleyici türü ve bu denetleyici türünün bir örneğini oluşturmak için sorumlu olan IControllerFactory arabiriminin bir uygulamasıdır.

Denetleyici Activators yalnızca bir denetleyici türü örneğinin örneğini oluşturmak için sorumludur. Denetleyici türü arama gerçekleştirmez. Uygun bir denetleyici türü bulduktan sonra denetleyici fabrikaları, denetleyicinin gerçek örneklenmesini işleyecek bir Icontrolleretkinleştirici örneğine temsilci olmalıdır.

DefaultControllerFactory sınıfının bir IControllerFactory örneğini kabul eden yeni bir Oluşturucusu vardır. Bu, denetleyici oluşturma işlemini Varsayılan denetleyici türü arama davranışını geçersiz kılmak zorunda kalmadan yönetmek için bağımlılık ekleme özelliği uygulamanıza olanak tanır.

#### <a name="iservicelocator-interface-replaced-with-idependencyresolver"></a>Ivicelocator arabirimi ıdependencyresolver ile değiştirilmiştir

Topluluk geri bildirimlerine bağlı olarak, ASP.NET MVC 3 Beta sürümü, ıstreamelocator arabiriminin kullanımını ASP.NET MVC ihtiyaçlarına özgü bir slimmed-inıdependencyresolver arabirimiyle değiştirdi. Aşağıdaki örnek, yeni arabirimi gösterir:

[!code-csharp[Main](mvc3-release-notes/samples/sample28.cs)]

Bu değişikliğin bir parçası olarak, ServiceLocator sınıfı da DependencyResolver sınıfıyla değiştirilmiştir. Bağımlılık Çözümleyicisinin kaydı, ASP.NET MVC 'nin önceki sürümlerine benzerdir:

[!code-csharp[Main](mvc3-release-notes/samples/sample29.cs)]

Bu arabirimin uygulamaları, istenen tür için kayıtlı hizmeti sağlamak üzere yalnızca temel bağımlılık ekleme kapsayıcısına temsilci atamasını sağlamalıdır.

İstenen türde kayıtlı bir hizmet olmadığında, ASP.NET MVC bu arabirimin uygulamalarının GetService 'ten null döndürmesini ve GetServices 'ten boş bir koleksiyon döndürmesini bekler.

Yeni DependencyResolver sınıfı, yeni ıdependencyresolver arabirimini ya da ortak hizmet bulucu arabirimini (ıvicelocator) uygulayan sınıfları kaydetmenizi sağlar. Ortak hizmet bulucu hakkında daha fazla bilgi için bkz. [GitHub 'Da Commonservicelocator](https://github.com/unitycontainer/commonservicelocator).

<a id="0.1__Breaking_Changes"></a>

#### <a name="new-iviewactivator-interface-for-fine-grained-view-page-instantiation"></a>Ayrıntılı görünüm sayfası örneği oluşturma için yeni ıviewetkinleştirici arabirimi

Yeni ıviewpageetkinleştirici arabirimi, görünüm sayfalarının bağımlılık ekleme yoluyla nasıl örneklendiği konusunda daha ayrıntılı denetim sağlar. Bu hem WebFormView örnekleri hem de RazorView örnekleri için geçerlidir. Aşağıdaki örnek, yeni arabirimi gösterir:

[!code-csharp[Main](mvc3-release-notes/samples/sample30.cs)]

Bu sınıflar şimdi bir ıviewpageetkinleştirici Oluşturucu bağımsız değişkeni kabul eder. Bu, ViewPage, ViewUserControl ve WebViewPage türlerinin nasıl örneklendirilçalıştığını denetlemek için bağımlılık ekleme kullanmanıza olanak sağlar.

#### <a name="new-dependency-resolver-support-for-existing-services"></a>Mevcut hizmetler için yeni bağımlılık çözümleyici desteği

Yeni sürüm aşağıdaki hizmetler için bağımlılık çözümü desteğini içerir:

- Model doğrulama sağlayıcıları. ModelValidatorProvider uygulayan sınıflar bağımlılık çözümleyici 'ye kaydedilebilir ve sistem bu istemcileri istemci ve sunucu tarafı doğrulamayı desteklemek için kullanır.
- Model meta veri sağlayıcısı. ModelMetadataProvider uygulayan tek bir sınıf bağımlılık çözümleyici 'ye kaydedilebilir ve sistem bunu şablon oluşturma ve doğrulama sistemleri için meta veriler sağlamak üzere kullanır.
- Değer sağlayıcıları. ValueProviderFactory uygulayan sınıflar bağımlılık çözümleyici 'ye kaydedilebilir ve sistem bunları, denetleyici tarafından tüketilen ve model bağlama sırasında kullanılan değer sağlayıcıları oluşturmak için kullanır.
- Model ciltleri. IModelBinderProvider uygulayan sınıflar bağımlılık çözümleyici 'ye kaydedilebilir ve sistem bunları model bağlama sistemi tarafından kullanılan model ciltleri oluşturmak için kullanır.

### <a id="0.1__Toc274034221"></a>Unobtrusive tabanlı Ajax için yeni destek

ASP.NET MVC, aşağıdakiler gibi Ajax Yardımcısı yöntemlerini içerir:

- AJAX. ActionLink
- AJAX. RouteLink
- AJAX. BeginForm
- AJAX. BeginRouteForm

Bu yöntemler, tam geri gönderme kullanmak yerine sunucuda bir eylem yöntemi çağırmak için JavaScript kullanır. Bu işlevsellik, hiçbir zaman jQuery 'ten kaçınılması açısından güncelleştirilmiştir. Satır içi istemci betikleri dahil etmek yerine, bu yardımcı yöntemler, *Data-Ajax* ÖNEKINI kullanarak HTML5 özniteliklerini yayarak, davranışı işaretlemeden ayırır. Daha sonra davranış, uygun JavaScript dosyalarına başvurarak biçimlendirmeye uygulanır. Aşağıdaki JavaScript dosyalarına başvurulduğundan emin olun:

- jQuery-1.4.1. js
- jQuery. unobtrusive. Ajax. js

Bu özellik varsayılan olarak ASP.NET MVC 3 yeni proje şablonlarındaki Web. config dosyasında etkindir, ancak mevcut projeler için varsayılan olarak devre dışıdır. Daha fazla bilgi için, bu belgenin ilerleyen kısımlarında [istemci doğrulaması için uygulama genelinde bayraklar ve unobtrusive JavaScript ekleme](#0.1_AddedApplicationWideFlagsForClientValida) bölümüne bakın.

### <a id="0.1__Toc274034222"></a>Unobtrusive doğrulaması için yeni destek

Varsayılan olarak, ASP.NET MVC 3 Beta, istemci tarafı doğrulaması gerçekleştirmek için bir unobtrusive ' de jQuery doğrulaması kullanır. Engellemeyen istemci doğrulamasını etkinleştirmek için, görünümün içinden aşağıdakiler gibi bir çağrı yapın:

[!code-csharp[Main](mvc3-release-notes/samples/sample31.cs)]

Bu, aşağıdaki çağrıyı yaparak yapabileceğiniz ViewContext. UnobtrusiveJavaScriptEnabled özelliğinin true olarak ayarlanmasını gerektirir:

[!code-csharp[Main](mvc3-release-notes/samples/sample32.cs)]

Ayrıca, aşağıdaki JavaScript dosyalarına başvurulduğundan emin olun.

- jQuery-1.4.1. js
- jQuery. Validate. js
- jQuery. Validate. unobtrusive. js

Bu özellik varsayılan olarak, ASP.NET MVC 3 yeni proje şablonlarındaki Web. config dosyasında etkindir, ancak mevcut projeler için varsayılan olarak devre dışıdır. Daha fazla bilgi için, bu belgenin ilerleyen kısımlarında [istemci doğrulaması Için yeni uygulama genelinde bayraklar ve unsctrusive JavaScript](#0.1_AddedApplicationWideFlagsForClientValida) bölümüne bakın.

<a id="0.1__Toc274034223"></a>

### <a id="0.1_AddedApplicationWideFlagsForClientValida"></a>Istemci doğrulaması ve unobtrusive JavaScript için uygulama genelinde yeni bayraklar

Aşağıdaki örnekte olduğu gibi, HtmlHelper sınıfının statik üyelerini kullanarak istemci doğrulamasını etkinleştirebilir veya devre dışı bırakabilir.

[!code-csharp[Main](mvc3-release-notes/samples/sample33.cs)]

Varsayılan proje şablonları varsayılan olarak obtrusive JavaScript 'ı etkinleştirir. Ayrıca, aşağıdaki ayarları kullanarak uygulamanızın kök Web. config dosyasında bu özellikleri etkinleştirebilir veya devre dışı bırakabilirsiniz:

[!code-xml[Main](mvc3-release-notes/samples/sample34.xml)]

Bu özellikleri varsayılan olarak etkinleştirebildiğinden, aşağıdaki örneklerde gösterildiği gibi, varsayılan ayarları geçersiz kılmanızı sağlayan HtmlHelper sınıfına yeni aşırı yüklemeler eklenmiştir:

[!code-csharp[Main](mvc3-release-notes/samples/sample35.cs)]

Geriye dönük uyumluluk için, bu özelliklerin her ikisi de varsayılan olarak devre dışıdır.

### <a id="0.1__Toc274034224"></a>Görünümler çalıştırılmadan önce çalışan kod için yeni destek

Artık, görünümler dizinine \_viewstart. cshtml (veya \_viewstart. vbhtml) adlı bir dosya yerleştirebilir ve bu dizine ve alt dizinlerinde bulunan birden çok görünüm arasında paylaşılacak kodu ekleyebilirsiniz. Örneğin, aşağıdaki kodu ~/views klasöründeki \_viewstart. cshtml sayfasına koyabilirsiniz:

[!code-cshtml[Main](mvc3-release-notes/samples/sample36.cshtml)]

Bu, görünümler klasörü içindeki her görünümün düzen sayfasını ve tüm alt klasörlerini yinelemeli olarak ayarlar. Bir görünüm işlendiğinde, \_viewstart. cshtml dosyasındaki kod, görünüm kodu çalıştırılmadan önce çalışır. \_viewstart. cshtml kodu, bu klasördeki her görünüm için geçerlidir.

Varsayılan olarak, \_viewstart. cshtml dosyasındaki kod, tüm alt klasörlerde bulunan görünümler için de geçerlidir. Ancak, her bir alt klasör \_viewstart. cshtml dosyasının kendi sürümüne sahip olabilir; Bu durumda, yerel sürüm öncelikli olur. Örneğin, HomeController için tüm görünümlerde ortak olan kodu çalıştırmak için, ~/Views/Home klasörüne bir \_viewstart. cshtml dosyası yerleştirin.

### <a id="0.1__Toc274034225"></a>VBHTML Razor sözdizimi için yeni destek

Önceki ASP.NET MVC önizlemesi, temelinde Razor söz dizimi kullanan görünümler için destek içerir C#. Bu görünümler. cshtml dosya uzantısını kullanır. ASP.NET MVC 3 Beta, Razor 'yi desteklemeye yönelik çalışmanın bir parçası olarak,. vbhtml dosya uzantısını kullanan Visual Basic Razor söz dizimi için destek sunar.

VBHTML sayfalarında Visual Basic sözdiziminin kullanılmasına giriş için aşağıdaki URL 'deki öğreticiye bakın:

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-visual-basic](../web-pages/overview/getting-started/introducing-razor-syntax-vb.md)

### <a id="0.1__Toc274034226"></a>ValidateInputAttribute üzerinde daha ayrıntılı denetim

ASP.NET MVC her zaman, gelen isteğin kötü amaçlı olabilecek bir giriş içermediğinden emin olmak için çekirdek ASP.NET isteği doğrulama altyapısını çağıran ValidateInputAttribute sınıfını içerir. Varsayılan olarak, giriş doğrulaması etkindir. Aşağıdaki örnekte olduğu gibi, ValidateInputAttribute özniteliğini kullanarak istek doğrulamasını devre dışı bırakmak mümkündür:

[!code-csharp[Main](mvc3-release-notes/samples/sample37.cs)]

Ancak, birçok Web uygulamasında HTML 'ye izin vermek gereken tek form alanları vardır, ancak kalan alanlar olmamalıdır. ValidateInputAttribute sınıfı artık istek doğrulamasına dahil olmaması gereken alanların bir listesini belirtmenizi sağlar.

Örneğin, bir blog altyapısı geliştiriyorsanız, gövde ve Özet alanlarında biçimlendirmeye izin vermek isteyebilirsiniz. Bu alanlar, her biri özellik adına ("Body" ve "Summary") karşılık gelen bir Name özniteliğiyle birlikte iki giriş öğesiyle temsil edilebilir. Yalnızca bu alanlar için istek doğrulamayı devre dışı bırakmak için, aşağıdaki örnekte gösterildiği gibi, ValidateInput sınıfının exclude özelliğindeki adları (virgülle ayrılmış) belirtin:

[!code-csharp[Main](mvc3-release-notes/samples/sample38.cs)]

### <a id="0.1__Toc274034227"></a>Yardımcılar, anonim nesneler kullanılarak belirtilen HTML öznitelik adları için alt çizgileri tirelere dönüştürür

Yardımcı yöntemler, aşağıdaki örnekte olduğu gibi, anonim bir nesne kullanarak öznitelik adı/değer çiftleri belirtmenize olanak sağlar:

[!code-csharp[Main](mvc3-release-notes/samples/sample39.cs)]

Bu yaklaşım, ASP.NET içinde özellik adı için bir tire kullanılamadığından öznitelik adında kısa çizgiler kullanmanıza izin vermez. Ancak, özel HTML5 öznitelikleri için kısa çizgiler önemlidir; Örneğin HTML5, "Data-" önekini kullanır.

Aynı zamanda, HTML 'deki öznitelik adları için alt çizgiler kullanılamaz, ancak özellik adları içinde geçerli. Bu nedenle, anonim bir nesne kullanarak öznitelikler belirtirseniz ve öznitelik adları bir alt çizgi içeriyorsa, yardımcı yöntemler alt çizgileri tirelere dönüştürür. Örneğin, aşağıdaki yardımcı sözdizimi bir alt çizgi kullanır:

[!code-csharp[Main](mvc3-release-notes/samples/sample40.cs)]

Önceki örnek, yardımcı çalıştığında aşağıdaki biçimlendirmeyi işler:

[!code-html[Main](mvc3-release-notes/samples/sample41.html)]

## <a id="0.1__Toc274034228"></a>Hata düzeltmeleri

Şablon yardımcıları için EditorFor ve Displaydefault nesne şablonu artık DisplayAttribute. Order özelliğinde belirtilen sıralamayı destekler. (Önceki sürümlerde, sipariş ayarı kullanılmıştı.)

İstemci doğrulaması artık, doğrulama öznitelikleri uygulanmış geçersiz kılınan özelliklerin doğrulanmasını desteklemektedir.

JsonValueProviderFactory artık varsayılan olarak kaydedilir.

## <a id="0.1__Toc274034229"></a>Son değişiklikler

Özel durum filtreleri için yürütme sırası, aynı sıra değerine sahip özel durum filtreleri için değişti. ASP.NET MVC 2 ve önceki sürümlerde, denetleyicideki bir eylem yöntemiyle aynı sırada olan özel durum filtreleri, eylem yöntemindeki özel durum filtrelerinden önce yürütüldü. Bu, genellikle özel durum filtrelerinin belirtilen bir sipariş değeri olmadan uygulanması durumunda olur. ASP.NET MVC 3 ' te, bu sıra, en belirli özel durum işleyicisinin ilk kez çalışması için tersine çevrildi. Önceki sürümlerde olduğu gibi, Order özelliği açıkça belirtilmişse, filtreler belirtilen sırada çalıştırılır.

## <a id="0.1__Toc274034230"></a>Bilinen sorunlar

Yükleme sırasında, EULA kabulü iletişim kutusu, lisans koşullarını amaçlanan bir pencerede görüntüler.

Razor görünümlerinde IntelliSense desteği veya sözdizimi vurgulaması yoktur. Visual Studio 'da Razor söz dizimi desteğinin, sonraki bir sürümün parçası olarak dahil edileceğini tahmin edilir.

Bir Razor görünümü (cshtml dosyası) düzenlenirken, <a id="0.1__Toc224729061"></a> <a id="0.1__Toc238051347"></a> Visual Studio 'daki denetleyiciye git menü öğesi kullanılamayacak ve kod parçacığı yok.

Türü kesin belirlenmiş bir CSHTML görünümü belirtmek için @model sözdizimini kullanırken, türler için dile özgü kısayollar tanınmıyor. Örneğin, @model int çalışmaz, ancak @model Int32 çalışır. Bu hata için geçici çözüm, model türünü belirttiğinizde gerçek tür adını kullanmaktır.

Türü kesin belirlenmiş bir CSHTML görünümünü belirtmek için @model sözdizimini kullanırken (veya kesin belirlenmiş bir VBHTML görünümü belirtmek için @ModelType), null yapılabilir türler ve dizi bildirimleri desteklenmez. Örneğin, int @model? desteklenmez. Bunun yerine `@model Nullable<Int32>` kullanın. String [] @model sözdizimi de desteklenmez; Bunun yerine `@model IList<string>`kullanın.

Bir ASP.NET MVC 2 projesini ASP.NET MVC 3 ' e yükselttiğinizde, Web. config dosyasının appSettings bölümüne aşağıdakileri eklediğinizden emin olun:

[!code-xml[Main](mvc3-release-notes/samples/sample42.xml)]

Form kimlik doğrulamasının, Web. config 'de kullanılan Forms kimlik doğrulaması ayarını yoksayarak, kimliği doğrulanmamış kullanıcıları her zaman kimliği doğrulanmamış kullanıcıları ~/Account/Login öğesine yönlendirmesine neden olan bilinen bir sorun var. Geçici çözüm aşağıdaki uygulama ayarını eklemektir.

[!code-xml[Main](mvc3-release-notes/samples/sample43.xml)]

## <a id="0.1__Toc274034231"></a>Sorumluluk reddi

© 2011 Microsoft Corporation. Tüm hakları saklıdır. Bu belge "olduğu gibi" verilmiştir. Bu belgede açıklanan bilgiler, URL ve diğer Internet Web sitesi başvuruları da dahil, önceden bildirilmeksizin değiştirilebilir. Bunların kullanım riski size aittir.

Bu belge size herhangi bir Microsoft ürününde herhangi bir fikri mülkiyet hakkı sağlamaz. Bu belgeyi kendi dahili, başvuru amaçlarınız için kopyalayabilir ve kullanabilirsiniz.
