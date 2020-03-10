---
uid: whitepapers/mvc4-release-notes
title: ASP.NET MVC 4 | Microsoft Docs
author: rick-anderson
description: Bu belgede ASP.NET MVC 4 sürümü açıklanmaktadır.
ms.author: riande
ms.date: 09/09/2011
ms.assetid: f014524f-25c0-4094-b8e1-886d99536f00
msc.legacyurl: /whitepapers/mvc4-release-notes
msc.type: content
ms.openlocfilehash: b57480bd0274fbb76c600dfb0dd09037bdcbf1e7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563429"
---
# <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

> Bu belgede ASP.NET MVC 4 sürümü açıklanmaktadır.

- [Yükleme notları](#_Toc303253802)
- [Belgeler](#_Toc303253803)
- [Destek](#_Toc303253804)
- [Yazılım gereksinimleri](#_Toc303253805)
- [ASP.NET MVC 4 sürümündeki yeni özellikler](#_Toc303253807)

    - [ASP.NET Web API](#_Toc317096197)
    - [Varsayılan proje şablonlarına yönelik geliştirmeler](#_Toc303253808)
    - [Mobil proje şablonu](#_Toc303253809)
    - [Görüntüleme modları](#_Toc303253810)
    - [jQuery Mobile, görünüm değiştirici ve tarayıcı geçersiz kılma](#_Toc303253811)
    - [Zaman uyumsuz denetleyiciler için görev desteği](#_Toc303253813)
    - [Azure SDK](#_Toc303253814)
    - [Veritabanı geçişleri](#_Toc303253818)
    - [Boş proje şablonu](#_Toc303253819)
    - [Denetleyiciyi herhangi bir proje klasörüne ekleyin](#_Toc303253820)
    - [Paketleme ve Küçültme](#_Toc303253821)
    - [OAuth ve OpenID kullanan Facebook ve diğer sitelerden oturum açma Işlemlerini etkinleştirme](#_Toc303253822)
- [ASP.NET MVC 3 projesini ASP.NET MVC 4 ' e yükseltme](#_Toc303253806)
- [ASP.NET MVC 4 sürüm adayından değişiklikler](#_Toc303253817)
- [Bilinen sorunlar ve son değişiklikler](#_Toc303253815)

<a id="_Toc303253802"></a>
## <a name="installation-notes"></a>Yükleme notları

Visual Studio 2010 için ASP.NET MVC 4, Web Platformu Yükleyicisi kullanılarak [ASP.NET MVC 4 ana sayfasından](../mvc/mvc4.md) yüklenebilir.

ASP.NET MVC 4 ' ü yüklemeden önce ASP.NET MVC 4 ' ün önceden yüklenmiş tüm önizlemelerini kaldırmanızı öneririz. ASP.NET MVC 4 Beta sürümünü ve sürüm adayını kaldırma işlemini yapmadan ASP.NET MVC 4 ' e yükseltebilirsiniz.

Bu sürüm, .NET Framework 4,5 ' nin tüm önizleme sürümleri ile uyumlu değildir. ASP.NET MVC 4 ' ü yüklemeden önce .NET Framework 4,5 ' nin yüklü tüm önizleme sürümlerini son sürüme ayrı olarak yükseltmeniz gerekir.

ASP.NET MVC 4, ASP.NET MVC 3 ile birlikte yüklenebilir ve yan yana çalıştırılabilir.

<a id="_Toc303253803"></a>
## <a name="documentation"></a>Belgeler

ASP.NET MVC belgeleri aşağıdaki URL 'de MSDN Web sitesinde bulunabilir:

[https://go.microsoft.com/fwlink/?LinkID=243043](https://go.microsoft.com/fwlink/?LinkID=243043)

ASP.NET MVC hakkında öğreticiler ve diğer bilgiler ASP.NET Web sitesinin MVC 4 sayfasında ([https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)) bulunabilir.

<a id="_Toc303253804"></a>
## <a name="support"></a>Destek

ASP.NET MVC 4 tam olarak desteklenmektedir. Bu sürümle çalışma hakkında sorularınız varsa, ASP.NET MVC forumuna ([https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)) da gönderebilirsiniz. burada, ASP.net topluluğunun üyeleri çok sayıda resmi olmayan destek sağlayabilecektir.

<a id="_Toc303253805"></a>
## <a name="software-requirements"></a>Yazılım Gereksinimleri

Visual Studio için ASP.NET MVC 4 bileşenleri, PowerShell 2,0 ve Service Pack 1 ile Visual Studio 2010 ya da Service Pack 1 Visual Web Developer Express 2010 gerektirir.

<a id="_Toc303253807"></a>
## <a name="new-features-in-aspnet-mvc-4"></a>ASP.NET MVC 4 sürümündeki yeni özellikler

Bu bölümde ASP.NET MVC 4 sürümünde tanıtılan özellikler açıklanmaktadır.

<a id="_Toc317096197"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET MVC 4, tarayıcılar ve mobil cihazlar dahil olmak üzere çok çeşitli istemcilere ulaşan HTTP Hizmetleri oluşturmaya yönelik yeni bir çerçeve olan ASP.NET Web API 'sini içerir. ASP.NET Web API 'SI Ayrıca, yeniden oluşan hizmetler oluşturmak için ideal bir platformdur.

ASP.NET Web API 'SI aşağıdaki özellikler için destek içerir:

- **Modern http programlama modeli:** Yeni ve kesin tür belirtilmiş bir HTTP nesne modeli kullanarak Web API 'inizdeki HTTP isteklerini ve yanıtlarını doğrudan erişin ve değiştirin. Aynı programlama modeli ve HTTP işlem hattı, istemci üzerinde yeni *HttpClient* türü aracılığıyla simetrik olarak kullanıma sunulmuştur.
- **Yollar Için tam destek:** ASP.NET Web API 'SI, rota parametreleri ve kısıtlamaları da dahil olmak üzere ASP.NET yönlendirme 'nin tüm yönlendirme özelliklerini destekler. Ayrıca, eylemleri HTTP yöntemlerine eşlemek için basit kuralları kullanın.
- **İçerik anlaşması:** İstemci ve sunucu, bir Web API 'sinden döndürülen verilerin doğru biçimini belirlemede birlikte çalışabilir. ASP.NET Web API 'si, XML, JSON ve form URL kodlamalı biçimleri için varsayılan destek sağlar ve kendi biçimlerinizi ekleyerek veya varsayılan içerik anlaşması stratejisini değiştirerek bu desteği genişletebilirsiniz.
- **Model bağlama ve doğrulama:** Model ciltler, bir HTTP isteğinin çeşitli parçalarından veri ayıklamanın kolay bir yolunu sağlar ve bu ileti parçalarını Web API 'SI eylemleri tarafından kullanılabilecek .NET nesnelerine dönüştürür. Doğrulama, veri ek açıklamalarını temel alan eylem parametreleri üzerinde de gerçekleştirilir.
- **Filtreler:** ASP.NET Web API 'SI, *[Yetkilendir]* özniteliği gibi iyi bilinen filtreler dahil olmak üzere filtreleri destekler. Eylemler, yetkilendirme ve özel durum işleme için kendi filtrelerinizi yazabilir ve takabilirsiniz.
- **Sorgu kompozisyonu:** OData sorgu kuralları aracılığıyla Web API 'nizi sorgulama desteğini etkinleştirmek için *IQueryable* döndüren bir eylemde *[Queryable]* Filter özniteliğini kullanın.
- **İyileştirilmiş test edilebilirlik:** Statik bağlam nesnelerinde HTTP ayrıntılarını ayarlamak yerine, Web API eylemleri *HttpRequestMessage* ve *HttpResponseMessage*örnekleri ile çalışır. Web API işlevselliğine yönelik birim testlerini hızlıca yazmaya başlamak için Web API projenizle birlikte bir birim test projesi oluşturun.
- **Kod tabanlı yapılandırma:** ASP.NET Web API 'SI yapılandırması, yalnızca kod aracılığıyla gerçekleştirilir ve yapılandırma dosyalarınızın temiz kalmasını önler. Genişletilebilirlik noktalarını yapılandırmak için, sunulan hizmet bulucu modelini kullanın.
- **Denetim (IOC) kapsayıcıları Için gelişmiş destek:** ASP.NET Web API 'SI, geliştirilmiş bir bağımlılık Çözümleyicisi soyutlaması aracılığıyla IOC kapsayıcıları için harika destek sağlar
- **Self-Host:** Web API 'Leri, yolların tam gücünden ve Web API 'sinin diğer özelliklerinin hala kullanılması sırasında IIS 'e ek olarak kendi işleminizde barındırılabilir.
- **Özel yardım ve test sayfaları oluşturun:** Web API 'lerinizin tamamen çalışma zamanı açıklaması almak için yeni *IApiExplorer* hizmetini kullanarak Web API 'leriniz için kolayca özel yardım ve test sayfaları oluşturabilirsiniz.
- **İzleme ve Tanılama:** ASP.NET Web API 'SI artık, System. Diagnostics, ETW ve üçüncü taraf günlük çerçeveleri gibi mevcut günlük çözümleri ile tümleştirmeyi kolaylaştıran hafif bir izleme altyapısı sağlıyor. Bir *ıstracewriter* uygulamasını sağlayarak izlemeyi etkinleştirebilir ve onu Web API yapılandırmanıza ekleyebilirsiniz.
- **Bağlantı oluşturma:** Aynı uygulamadaki ilgili kaynakların bağlantılarını oluşturmak için ASP.NET Web API *UrlHelper* ' i kullanın.
- **Web API 'si proje şablonu:** Yeni Web API projesi formunu seçerek, ASP.NET Web API 'SI ile hızlıca çalışmaya başlayın.
- **Yapı iskelesi:** Bir Web API denetleyiciyi Entity Framework tabanlı bir model türüne göre hızlıca kullanmak için **Denetleyici Ekle** iletişim kutusunu kullanın.

ASP.NET Web API 'SI hakkında daha fazla bilgi için lütfen [https://www.asp.net/web-api](../web-api/index.md)ziyaret edin.

<a id="_Toc303253808"></a>
### <a name="enhancements-to-default-project-templates"></a>Varsayılan proje şablonlarına yönelik geliştirmeler

Yeni ASP.NET MVC 4 projeleri oluşturmak için kullanılan şablon daha modern görünümlü bir Web sitesi oluşturmak üzere güncelleştirilmiştir:

![](mvc4-release-notes/_static/image1.png)

Yüzeysel geliştirmeleri 'nin yanı sıra, yeni şablonda de geliştirilmiş işlevsellik vardır. Şablon, hiçbir özelleştirme olmadan hem masaüstü tarayıcılarında hem de mobil tarayıcılarda iyi bakmak için uyarlamalı işleme adlı bir teknik kullanır.

![](mvc4-release-notes/_static/image2.png)

Uyarlamalı işleme eylemini görmek için bir mobil öykünücü kullanabilir veya masaüstü tarayıcı penceresini daha küçük olacak şekilde yeniden boyutlandırmayı deneyebilirsiniz. Tarayıcı penceresi yeterince az olduğunda, sayfanın düzeni değişecektir.

<a id="_Toc303253809"></a>
### <a name="mobile-project-template"></a>Mobil proje şablonu

Yeni bir proje başlatıyorsanız ve özellikle mobil ve tablet tarayıcıları için bir site oluşturmak istiyorsanız, yeni mobil uygulama projesi şablonunu kullanabilirsiniz. Bu, dokunarak iyileştirilmiş UI oluşturmaya yönelik açık kaynaklı bir kitaplık olan jQuery Mobile 'a dayalıdır:

![](mvc4-release-notes/_static/image3.png)

Bu şablon, Internet uygulaması şablonuyla aynı uygulama yapısını içerir (ve denetleyici kodu neredeyse aynıdır), ancak daha iyi bakmak için jQuery Mobile kullanılarak stillendirilmiş ve dokunmatik tabanlı mobil cihazlarda iyi davranacağız. Mobil Kullanıcı arabirimine yönelik yapı ve stil oluşturma hakkında daha fazla bilgi edinmek için [jQuery Mobile Project Web sitesine](http://jquerymobile.com/)bakın.

Mobil olarak iyileştirilmiş görünümler eklemek istediğiniz masaüstü yönelimli bir siteniz zaten varsa veya masaüstü ve mobil tarayıcılara farklı biçimlendirilmiş görünümler sunan tek bir site oluşturmak istiyorsanız, yeni görüntüleme modları özelliğini kullanabilirsiniz. (Sonraki bölüme bakın.)

<a id="_Toc303253810"></a>
### <a name="display-modes"></a>Görüntüleme modları

Yeni görüntü modları özelliği, bir uygulamanın, isteği yapan tarayıcıya bağlı olarak görünüm seçmesini sağlar. Örneğin, bir masaüstü tarayıcısı giriş sayfasını isterse, uygulama Views\home\ındex.cshtml şablonunu kullanabilir. Bir mobil tarayıcı giriş sayfasını isterse, uygulama Views\Home\Index.mobile.cshtml şablonunu döndürebilir.

Ayrıca, belirli tarayıcı türleri için düzenler ve partileri geçersiz kılınabilir. Örneğin:

- Views\Shared klasörünüzde hem \_Layout. cshtml hem de \_Layout. Mobile. cshtml şablonları varsa, uygulama varsayılan olarak mobil tarayıcıların istekleri sırasında \_Layout. Mobile. cshtml ve diğer istekler sırasında \_Layout. cshtml kullanır.
- Bir klasör hem \_MyPartial. cshtml hem de \_MyPartial. Mobile. cshtml içeriyorsa, yönerge @Html.Partial("\_MyPartial"), mobil tarayıcıların istekleri sırasında MyPartial. Mobile. cshtml 'yi ve diğer istekler sırasında MyPartial. cshtml dosyasını \_.\_

Diğer cihazlar için daha özel görünümler, düzenler veya kısmi görünümler oluşturmak istiyorsanız, bir istek belirli koşullara uysa aranacak adı belirtmek için yeni bir *Defaultdisplaymode* örneği kaydedebilirsiniz. Örneğin, "iPhone" dizesini, Apple iPhone tarayıcısı bir istek yaptığında geçerli bir görüntüleme modu olarak kaydetmek için, Global. asax dosyasındaki *Application\_start* yöntemine aşağıdaki kodu ekleyebilirsiniz:

[!code-csharp[Main](mvc4-release-notes/samples/sample1.cs)]

Bu kod çalıştıktan sonra, bir Apple iPhone tarayıcısı istek yaptığında, uygulamanız Views\Shared\\_Layout. iPhone. cshtml düzeni (varsa) kullanır. Görüntü modu hakkında daha fazla bilgi için bkz. [ASP.NET MVC 4 mobil özellikleri](../mvc/overview/older-versions/aspnet-mvc-4-mobile-features.md). DisplayModeProvider kullanan uygulamalar, [sabit DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) NuGet paketini yüklemelidir. [ASP.net Fall 2012 güncelleştirmesi](https://go.microsoft.com/fwlink/?LinkID=271322) , yeni proje şablonlarında [düzeltilen DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) NuGet paketini içerir. Düzeltme hakkındaki ayrıntılar için bkz. [ASP.NET MVC 4 Mobile Caching hata Fixedd](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) .

<a id="_Toc303253811"></a>
### <a name="jquery-mobile-and-mobile-features"></a>jQuery Mobile ve mobil özellikleri

JQuery Mobile kullanarak ASP.NET MVC 4 ile mobil uygulamalar oluşturma hakkında daha fazla bilgi için, bkz. [MVC 4 mobil özellikleri](../mvc/overview/older-versions/aspnet-mvc-4-mobile-features.md).

<a id="_Toc303253813"></a>
### <a name="task-support-for-asynchronous-controllers"></a>Zaman uyumsuz denetleyiciler için görev desteği

Artık zaman uyumsuz eylem yöntemlerini, *Task* veya *Task&lt;ActionResult&gt;* türünde bir nesne döndüren tek yöntemler olarak yazabilirsiniz.

 Daha fazla bilgi için bkz. [ASP.NET MVC 4 Içinde zaman uyumsuz yöntemler kullanma](../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).

<a id="_Toc303253814"></a>
### <a name="azure-sdk"></a>Azure SDK

ASP.NET MVC 4, Windows Azure SDK 'sının 1,6 ve sonraki sürümlerini destekler.

<a id="_Toc303253818"></a>
### <a name="database-migrations"></a>Veritabanı geçişleri

ASP.NET MVC 4 projeleri artık Entity Framework 5 ' i içerir. Entity Framework 5 ' teki harika özelliklerden biri veritabanı geçişleri için desteğe yöneliktir. Bu özellik, veritabanındaki verileri korurken, kod odaklı bir geçiş kullanarak veritabanı şemanızı kolayca gerçekleştirmenizi sağlar. Veritabanı geçişleri hakkında daha fazla bilgi için bkz. [ASP.NET MVC 4 öğreticisinde](../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) [Film modeli ve tablosuna yeni alan ekleme](../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table.md) .

<a id="_Toc303253819"></a>
### <a name="empty-project-template"></a>Boş proje şablonu

Tamamen temiz bir tablet 'den başlayabilmeniz için MVC boş proje şablonu artık gerçekten boştur. Boş proje şablonunun önceki sürümü temel olarak yeniden adlandırıldı.

<a id="_Toc303253820"></a>
### <a name="add-controller-to-any-project-folder"></a>Denetleyiciyi herhangi bir proje klasörüne ekleyin

Artık sağ tıklayıp MVC projenizdeki herhangi bir klasörden **Denetleyici Ekle** ' yi seçebilirsiniz. Bu sayede, MVC ve Web API denetleyicilerinizi ayrı klasörler halinde tutmak da dahil olmak üzere denetleyicilerinizi düzenleme konusunda daha fazla esneklik elde edersiniz.

<a id="_Toc303253821"></a>
### <a name="bundling-and-minification"></a>Paketleme ve Küçültme

Paketleme ve minbirleştirime çerçevesi, tek tek dosyaları betikler ve CSS için tek ve paketlenmiş bir dosyaya birleştirerek bir Web sayfasının yapması gereken HTTP isteklerinin sayısını azaltmanıza olanak sağlar. Daha sonra paketin içeriğini azaltarak bu isteklerin genel boyutunu azaltabilir. Minifying, değişken adlarını kısaltma altına almak için boşluğu ortadan kaldıran, anlamlarına göre CSS seçicileri bile daraltma gibi etkinlikleri içerebilir. Paketlemeler kodda tanımlanır ve yapılandırılır ve bir pakete tek bir bağlantı oluşturabileceğiniz ya da hata ayıklarken, her bir paket için birden çok bağlantı oluşturabileceğiniz yardımcı yöntemler aracılığıyla görünümlerde kolayca başvuruluyor. Daha fazla bilgi için bkz. [paketleme ve küçültmeye](../mvc/overview/performance/bundling-and-minification.md)yönelik.

<a id="_Toc303253822"></a>
### <a name="enabling-logins-from-facebook-and-other-sites-using-oauth-and-openid"></a>OAuth ve OpenID kullanan Facebook ve diğer sitelerden oturum açma Işlemlerini etkinleştirme

ASP.NET MVC 4 Internet Proje şablonundaki varsayılan şablonlar artık DotNetOpenAuth kitaplığı kullanılarak OAuth ve OpenID oturum açma desteğini içerir. OAuth veya OpenID sağlayıcısı yapılandırma hakkında daha fazla bilgi için bkz. ASP.NET Web Pages içindeki [WebForms, MVC ve Web sayfaları](https://blogs.msdn.com/b/webdev/archive/2012/08/15/oauth-openid-support-for-webforms-mvc-and-webpages.aspx) ve [OAuth ve OpenID Özellik belgeleri](../web-pages/overview/releases/top-features-in-web-pages-2.md#oauthsetup)Için OAuth/OpenID desteği.

<a id="_Toc303253806"></a>
## <a name="upgrading-an-aspnet-mvc-3-project-to-aspnet-mvc-4"></a>ASP.NET MVC 3 projesini ASP.NET MVC 4 ' e yükseltme

ASP.NET MVC 4, aynı bilgisayarda ASP.NET MVC 3 ile yan yana yüklenebilir ve bu da bir ASP.NET MVC 3 uygulamasının ASP.NET MVC 4 ' e ne zaman yükseltileceğini seçme esnekliği sağlar.

Yükseltmenin en kolay yolu, yeni bir ASP.NET MVC 4 projesi oluşturmaktır ve var olan MVC 3 projesinden tüm görünümleri, denetleyicileri, kodu ve içerik dosyalarını yeni projeye kopyalayacak ve ardından yeni projedeki derleme başvurularını, ' deki MVC olmayan herhangi bir şablonla eşleşecek şekilde güncelleştirecek şekilde güncelleştirmesidir. kullandığınız Assembiles kümediniz. MVC 3 projesinde Web. config dosyasında değişiklik yaptıysanız, bu değişiklikleri MVC 4 projesindeki Web. config dosyasında da birleştirmeniz gerekir.

Mevcut bir ASP.NET MVC 3 uygulamasını sürüm 4 ' e el ile yükseltmek için aşağıdakileri yapın:

1. Projedeki tüm Web. config dosyalarında (projenin kökünde, görünümler klasöründe, diğeri de projenizdeki her bir alana ilişkin Görünümler klasöründe), aşağıdaki metnin her örneğini değiştirin (Not: System. Web. Web sayfaları, Version = 1.0.0.0, içinde bulunamadı) Visual Studio 2012 ile oluşturulan projeler): 

    [!code-console[Main](mvc4-release-notes/samples/sample2.cmd)]

    aşağıdaki metinle birlikte:

    [!code-console[Main](mvc4-release-notes/samples/sample3.cmd)]
2. Kök Web. config dosyasında, Web *sayfaları: sürüm* öğesini "2.0.0.0" olarak güncelleştirin ve "true" değerine sahip yeni bir *Preserveloginurl* anahtarı ekleyin: 

    [!code-xml[Main](mvc4-release-notes/samples/sample4.xml)]
3. Çözüm Gezgini, başvurular ' a sağ tıklayın ve NuGet Paketlerini Yönet ' i seçin. Sol bölmede **Online\nual resmi paket kaynağı**' nı seçin ve ardından aşağıdakileri güncelleştirin:

    - ASP.NET MVC 4
    - (İsteğe bağlı) jQuery, jQuery doğrulaması ve jQuery kullanıcı arabirimi
    - Seçim Entity Framework
    - (Opton) Modernize
4. Çözüm Gezgini, proje adına sağ tıklayın ve ardından projeyi Kaldır ' ı seçin. Sonra adı tekrar sağ tıklayın ve *ProjectName*. csproj öğesini Düzenle ' yi seçin.
5. *Projecttypeguid* öğelerini bulun ve {E53F8FEA-EAE0-44A6-8774-FFD645390401} öğesini {E3E379DF-F4C6-4180-9B81-6769533ABE47} ile değiştirin.
6. Değişiklikleri kaydedin, düzenlemekte olduğunuz proje (. csproj) dosyasını kapatın, projeye sağ tıklayın ve ardından projeyi yeniden yükle ' yi seçin.
7. Proje ASP.NET MVC 'nin önceki sürümleri kullanılarak derlenen herhangi bir üçüncü taraf kitaplığına başvuruyorsa, kök Web. config dosyasını açın ve *yapılandırma* bölümünün altına aşağıdaki üç *bindingRedirect* öğesini ekleyin: 

    [!code-xml[Main](mvc4-release-notes/samples/sample5.xml)]

<a id="_Toc303253817"></a>
## <a name="changes-from-aspnet-mvc-4-release-candidate"></a>ASP.NET MVC 4 sürüm adayından değişiklikler

ASP.NET MVC 4 sürüm adayı sürüm notları şurada bulunabilir:

Bu sürümdeki ASP.NET MVC 4 sürüm adayından önemli değişiklikler aşağıda özetlenmiştir:

- **Denetleyici başına yapılandırma:** ASP.NET Web API 'SI denetleyicileri kendi formatlarını, eylem seçiciyi ve parametre ciltleri ayarlamak için *Icontrollerconfiguration* uygulayan özel bir öznitelikle ilişkilendirilebilirler. *Httpcontrollerconfigurationattribute* kaldırılmıştır.
- **Yol ileti Işleyicileri başına:** Artık belirli bir rota için istek zincirinde son ileti işleyicisini belirtebilirsiniz. Bu, kendi (*ıhttpcontroller*) uç noktalarına dağıtım yapmak için yönlendirmeyi kullanmak üzere, urde ve çerçeveler için destek sağlar.
- **İlerleme bildirimleri:** *ProgressMessageHandler* , yüklenen hem istek varlıklarının hem de indirilen yanıt varlıklarının ilerleme durumunu oluşturur. Bu işleyiciyi kullanarak, bir istek gövdesini karşıya yüklemeyi veya bir yanıt gövdesini karşıdan yüklemeyi takip etmek mümkündür.
- **Içeriği gönder:** *Pushstreamcontent* sınıfı, bir veri üreticisi bir akış kullanarak doğrudan istek veya yanıta (zaman uyumlu veya zaman uyumsuz) yazmak istediği senaryolara olanak sağlar. *Pushstreamcontent* , çıkış akışıyla bir eylem temsilcisine çağrı yaptığı verileri kabul etmeye hazır olduğunda. Geliştirici daha sonra akışa gereken sürece yazabilir ve yazma tamamlandığında akışı kapatabilir. *Pushstreamcontent* , akışın kapanışını algılar ve içeriği yazmak için temeldeki zaman uyumsuz *görevi* tamamlar.
- **Hata yanıtları oluşturma:** Diğer bir deyişle, *ıncludeerrordetailpolicy*özelliğini kullanırken doğrulama hataları ve özel durumlar gibi hata bilgilerini sürekli olarak göstermek Için *HttpError* türünü kullanın. İçerik olarak *HttpError* ile hata yanıtlarını kolayca oluşturmak Için yeni *createerrorresponse* genişletme yöntemlerini kullanın. *HttpError* içeriği, tam olarak anlaşılan içeriktir.
- **MediaRangeMapping kaldırıldı:** Medya türü aralıkları artık varsayılan içerik Negotiator tarafından işlenir.
- **Basit tür parametreleri Için varsayılan parametre bağlaması artık [FromUri]:** Önceki ASP.NET Web API sürümlerinde, basit tür parametreleri için varsayılan parametre bağlama model bağlama kullanır. Basit tür parametreleri için varsayılan parametre bağlaması artık *[Fromuri]* .
- **Eylem seçimi gereken parametreleri** kabul eder: ASP.NET Web API 'sindeki eylem seçimi artık yalnızca URI 'den gelen tüm gerekli parametreler sağlandıysa bir eylem seçer. Bir parametre, eylem yöntemi imzasında bağımsız değişken için varsayılan bir değer sağlayarak isteğe bağlı olarak belirtilebilir.
- **Http parametre bağlamalarını Özelleştir:** Belirli bir eylem parametresi için parametre bağlamayı özelleştirmek üzere *ParameterBindingAttribute* kullanın veya parametre bağlamalarını daha büyük ölçüde özelleştirmek Için *HttpConfiguration* üzerinde *parameterbindingrules* kullanın.
- **MediaTypeFormatter geliştirmeleri:** Biçimlendiriciler artık tam *HttpContent* örneğine erişebilir.
- **Ana bilgisayar arabelleğe alma ilkesi seçimi:** ASP.NET Web API 'sinde *ıhostbufferpolicyselector* hizmetini uygulayıp yapılandırıp, ana bilgisayarların, arabelleğe alma işleminin kullanılacağı ilkeyi belirlemesine olanak sağlar.
- **İstemci sertifikalarına bir ana bilgisayar bağımsız olarak erişim:** İstek iletisinden sağlanan istemci sertifikasını almak için *GetClientCertificate* Extension metodunu kullanın.
- **İçerik anlaşması genişletilebilirliği:** *Defaultcontentnegotiator* öğesinden türeterek ve istediğiniz içerik görüşmesinin tüm yönlerini geçersiz kılarak içerik anlaşmasını özelleştirin.
- **406 döndürme desteği kabul edilebilir yanıt yok:** Artık, *Excludematchontypeonly* parametresi *true*olarak ayarlanmış bir *defaultcontentnegotiator* oluşturarak uygun bir biçimlendirici bulunamadığında ASP.NET Web apı 'sinde kabul edilebilir olmayan yanıtlar 406 döndürebilirsiniz.
- **Form verilerini NameValueCollection veya JToken olarak oku:** Form verilerini URI sorgu dizesinde veya istek gövdesinde, sırasıyla *ParseQueryString* ve *Readasformdataasync* uzantı yöntemlerini kullanarak bir *NameValueCollection* olarak okuyabilirsiniz. Benzer şekilde, bir şekilde, bir URI sorgu dizesinde veya istek gövdesinde, sırasıyla *Tryreadqueryasjson* ve *readasasync*&lt;t&gt; genişletme yöntemlerini kullanarak bir *jtoken* olarak form verilerini okuyabilirsiniz.
- **Çok parçalı iyileştirmeler:** Artık okuyamadığı MIME çok parçalı verilerinin türüne tamamen uyarlanmış ve sonucu kullanıcıya en uygun şekilde sunan *MultipartStreamProvider* yazmak mümkündür. Ayrıca *MultipartStreamProvider* üzerinde, uygulamanın MIME çok parçalı gövde bölümlerinde istediği herhangi bir post işlemini yapmasına olanak tanıyan bir post işleme adımı da bağlayabilirsiniz. Örneğin, *Multipartformdatastreamprovider* uygulamasının HTML form veri parçalarını okur ve bunları çağırandan almak kolay olacak şekilde bir *NameValueCollection* öğesine ekler.
- **Bağlantı oluşturma geliştirmeleri:** *UrlHelper* artık *HttpControllerContext*'e bağlı değil. Artık *HttpRequestMessage* kullanılabilir olan herhangi bir Içerikten *UrlHelper* 'a erişebilirsiniz.
- **İleti işleyici yürütme sırası değişikliği:** İleti işleyicileri artık, ters sırada değil, yapılandırıldıkları sırada yürütülür.
- **İleti işleyicilerinin yedeklenme Yardımcısı:** *DelegatingHandlers* 'e bağlanabilir ve istenen işlem hattına başlamaya yönelik bir *HttpClient* oluşturup bu yeni *httpclientfactory* . Ayrıca, diğer iç işleyicilerle (varsayılan olarak, *HttpClientHandler*) ve en üst düzey olarak *HttpClient* yerine de *HttpMessageInvoker* veya başka bir *DelegatingHandler* kullanırken kablolama için işlevsellik sağlar.
- **ASP.NET Web iyileştirmesi Için CDNs desteği:** ASP.NET Web Iyileştirmesi artık, her bir paket için bir içerik teslim ağında aynı kaynağa işaret eden ek bir URL 'YI belirtmenizi sağlayan CDN alternatif yolları için destek sağlar. CDNs 'yi desteklemek, betiğinizi ve stil paketlerinizi Web uygulamalarınızın son tüketicilerine coğrafi olarak daha yakından almanızı sağlar. CDN kullanılamadığında üretim uygulamaları bir geri dönüş uygulamalıdır. Geri dönüşü test edin.
- **ASP.NET Web API yönlendirmeleri ve yapılandırması *WebApiConfig.* test kodunda yeniden kullanılabilecek statik yöntemi kaydedin.** Daha önce ASP.NET Web API yönlendirmeleri, standart MVC yollarıyla birlikte *Routeconfig. RegisterRoutes* içine eklenmiştir. Varsayılan ASP.NET Web API yolları ve yapılandırması artık, testi kolaylaştırmak için ayrı bir *WebApiConfig. Register* yönteminde işlenir.

<a id="_Toc303253815"></a>
## <a name="known-issues-and-breaking-changes"></a>Bilinen sorunlar ve son değişiklikler

- **ASP.NET MVC 4 ' ün RC ve RTM sürümü, mobil görünümler döndürüldüğünde hatalı önbelleğe alınmış masaüstü görünümlerini geri döndürdü.**

    - Düzeltme hakkındaki ayrıntılar için bkz. [ASP.NET MVC 4 mobil önbelleğe alma hatası düzeltildi](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) . Düzeltme, [sabit DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) NuGet paketinden yüklenebilir.
- **Razor görünüm altyapısında son değişiklikler**. *System. Web. Mvc. Razor*'den şu türler kaldırılmıştır: 

    - *ModelSpan*
    - *MvcVBRazorCodeGenerator*
    - *MvcCSharpRazorCodeGenerator*
    - *MvcVBRazorCodeParser*

  Aşağıdaki yöntemler de kaldırılmıştır: 

    - *MvcCSharpRazorCodeParser. Parseınhersdeyim(System. Web. Razor. Parser. Codeblockınfo)*
    - *MvcWebPageRazorHost. Dekoratecodegenerator (System. Web. Razor. Generator. RazorCodeGenerator)*
    - *MvcVBRazorCodeParser. Parseınhersdeyim(System. Web. Razor. Parser. Codeblockınfo)*
- **WebMatrix. WebData. dll, ASP.NET MVC 4 uygulamalarının/bin dizinine dahil edildiğinde, form kimlik doğrulamasının URL 'sini devralır.** , WebMatrix. WebData. dll derlemesini uygulamanıza ekleme (örneğin, "dağıtılabilir bağımlılıklar Ekle iletişim kutusu kullanıldığında" Razor sözdizimi ile ASP.NET Web sayfaları "nı seçerek), varsayılan ASP.NET MVC hesap denetleyicisi tarafından beklendiği gibi/Account/Login yerine/account/Logon için kimlik doğrulama oturumu açmayı geçersiz kılar. Bu davranışı engellemek ve Web. config 'in kimlik doğrulama bölümünde belirtilen URL 'YI kullanmak için PreserveLoginUrl adlı bir appSetting ekleyebilir ve bunu true olarak ayarlayabilirsiniz: 

    [!code-xml[Main](mvc4-release-notes/samples/sample6.xml)]
- **NuGet Paket Yöneticisi, Visual Studio 2010 ve Visual Web Developer 2010 ' nin yan yana yüklemeleri için ASP.NET MVC 4 ' ü yüklemeye çalışırken yükleme işlemi başarısız olur.** Visual Studio 2010 ve Visual Web Developer 2010 ' i ASP.NET MVC 4 ile yan yana çalıştırmak için Visual Studio 'nun her iki sürümü de yüklendikten sonra ASP.NET MVC 4 ' ü yüklemelisiniz.
- **Önkoşullar zaten kaldırılmışsa, ASP.NET MVC 4 ' ün kaldırılması başarısız olur.** ASP.NET MVC 4'i temiz bir şekilde kaldırmak için Visual Studio 'Yu kaldırmadan önce ASP.NET MVC 4 ' ü kaldırmanız gerekir.
- **ASP.NET MVC 4 kesmeler ASP.NET MVC 3 RTM uygulamaları yükleniyor.** ASP.NET MVC 3 RTM sürümüyle oluşturulmuş uygulamalar ( [ASP.NET MVC 3 Araçlar Güncelleştirme](https://www.microsoft.com/download/details.aspx?id=1491) sürümü ile değil), ASP.NET MVC 4 ile yan yana çalışmak için aşağıdaki değişiklikleri gerektirir. Projeyi bu güncelleştirmeleri yapmadan oluşturmak derleme hatalarıyla sonuçlanır. 

    **Gerekli güncelleştirmeler**

  1. Kök Web. config dosyasında, anahtar *Web sayfaları: sürümü* ve *1.0.0.0*değeri Ile yeni bir *&lt;appSettings&gt;* girişi ekleyin. 

      [!code-xml[Main](mvc4-release-notes/samples/sample7.xml)]
  2. Çözüm Gezgini, proje adına sağ tıklayın ve ardından projeyi Kaldır ' ı seçin. Sonra adı tekrar sağ tıklayın ve *ProjectName*. csproj öğesini Düzenle ' yi seçin.
  3. Aşağıdaki derleme başvurularını bulun: 

      [!code-xml[Main](mvc4-release-notes/samples/sample8.xml)]

      Bunları aşağıdaki kodla değiştirin:

      [!code-xml[Main](mvc4-release-notes/samples/sample9.xml)]
  4. Değişiklikleri kaydedin, düzenlemekte olduğunuz proje (. csproj) dosyasını kapatın ve ardından projeye sağ tıklayıp yeniden yükle ' yi seçin.

- **ASP.NET MVC 4 projesini 4,5 ' den target 4,0 ' e değiştirmek EntityFramework derleme başvurusunu güncelleştirmez:** ASP.NET MVC 4 projesini, taralıma 4,5 sonrasında 4,0 hedef olarak değiştirirseniz, EntityFramework derlemesine yönelik başvuru yine de 4,5 sürümüne işaret eder. Bu sorunu onarmak için EntityFramework NuGet paketini kaldırın ve yeniden yükleyin.
- **403 ' 4,5 den hedef 4,0 ' e değiştirildikten sonra Azure 'da bir ASP.NET MVC 4 uygulaması çalıştırırken yasak:** ASP.NET MVC 4 projesini, 4,5 'e ve ardından Azure 'a dağıttıktan sonra 4,0 hedef olarak değiştirirseniz, çalışma zamanında bir 403 Yasak hatası görebilirsiniz. Bu soruna geçici bir çözüm olarak, Web. config dosyasına aşağıdakini ekleyin: `<modules runAllManagedModulesForAllRequests="true" />`
- **Razor dosyasındaki bir dize sabit değerinde bir '\' yazdığınızda Visual Studio 2012 çöküyor.** Sorunu geçici olarak çözmek için önce dize sabit değerinin kapatma teklifini girin.
- <strong>Internet şablonunda &quot;hesaba göz atma/yönetme&quot;, CHS, DIM ve CHT dilleri için bir çalışma zamanı hatasına neden olur.</strong> Sorunu onarmak için sayfayı, <em>&lt;güçlü&gt;</em> etiketi içindeki tek içerik olarak yerleştirerek <em>@User.Identity.Name</em> ayırmak üzere değiştirin.
- **Azure Web siteleri 'nde Google ve LinkedIn sağlayıcıları desteklenmez.** Azure Web sitelerine dağıtım yaparken alternatif kimlik doğrulama sağlayıcılarını kullanın.
- **IIS 8 Express/IIS ile Urıpathextensionmapping kullanırken, uzantıyı kullanmaya çalıştığınızda 404 bulunamadı hatası alırsınız.** Statik dosya işleyicisi, *Urıpathextensionmappings*kullanan Web API 'lerine yönelik istekleri kesintiye uğratacaktır. Sorunu geçici olarak çözmek için Web. config dosyasında *runAllManagedModulesForAllRequests = true* olarak ayarlayın.
- **Controller. Execute metodu artık çağrılmayacak.** Tüm MVC denetleyicileri artık zaman uyumsuz olarak yürütülür.
