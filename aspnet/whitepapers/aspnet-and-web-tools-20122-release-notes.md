---
uid: whitepapers/aspnet-and-web-tools-20122-release-notes
title: ASP.NET and Web Tools 2012,2 sürüm notları | Microsoft Docs
author: rick-anderson
description: ASP.NET and Web Tools 2012,2 için sürüm notları.
ms.author: riande
ms.date: 02/14/2013
ms.assetid: bdb18d02-9f61-4676-836d-6fdea94f9282
msc.legacyurl: /whitepapers/aspnet-and-web-tools-20122-release-notes
msc.type: content
ms.openlocfilehash: a4ea1d7c146309e1d5e8be944d496e9fd87bca3e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78523781"
---
# <a name="aspnet-and-web-tools-20122-release-notes"></a>ASP.NET and Web Tools 2012.2 Sürüm Notları

> Bu belgede ASP.NET and Web Tools 2012,2 sürümü açıklanmaktadır. Visual Studio Web araçları ve ASP.NET güncelleştirmesidir.

- [Yükleme notları](#_Installation)
- [Belgeler](#_Documentation)
- [Destek](#_Support)
- [Yazılım gereksinimleri](#_Software_Requirements)
- [ASP.NET and Web Tools 2012,2 ' deki yeni özellikler](#_New_Features_in)

    - [Araçları](#_Tooling)
    - [Web yayımlaması](#_Web_Publishing)
    - [ASP.NET MVC şablonları](#_Templates)
    - [ASP.NET Web API](#_ASP.NET_Web_API)

    - [ASP.NET SignalR](#_ASP.NET_SignalR)
    - [ASP.NET kolay URL 'Ler](#_ASP.NET_Friendly_URLs)
- [Bilinen sorunlar ve son değişiklikler](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a>Yükleme notları

Visual Studio 2012 için ASP.NET and Web Tools 2012,2, [Web Platformu Yükleyicisi](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)kullanılarak yüklenebilir. Bu, Visual Studio 2012 veya Web için Visual Studio Express 2012 ' e yönelik bir güncelleştirmedir ve bu gereklidir. Visual Studio yüklü değilse, Web için Visual Studio Express 2012 yüklenir.

ASP.NET and Web Tools 2012,2 'yi el ile de yükleyebilirsiniz. Web için Visual Studio 2012 veya Visual Studio Express 2012 yüklü olmalıdır. Ardından aşağıdaki yönergeleri kullanın: 

1. [ASP.net ve Web çerçeveleri 2012,2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) yükleyicisini indirme merkezinden indirin.
2. İstendiğinde Çalıştır ' a tıklayın. Dosyayı daha sonra çalıştırmak için de kaydedebilirsiniz.
3. Güncelleştirilecek Visual Studio sürümünü doğrulayın. Bunu, güncelleştirmek istediğiniz Visual Studio 'Yu başlatarak yapabilirsiniz. Yardım menüsü öğesine tıklayın.   
    ![](aspnet-and-web-tools-20122-release-notes/_static/image1.jpg)
4. Web&quot; için Microsoft Visual Studio 2012 &quot;menü öğesini görürseniz Web [Için web Geliştirici Araçları 2012,2-Visual Studio Express 2012](https://go.microsoft.com/fwlink/?LinkID=282228)' i indirin. Aksi halde [Web Geliştirici Araçları 2012,2-Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228)indirin.
5. İstendiğinde Çalıştır ' a tıklayın. Dosyayı daha sonra çalıştırmak için de kaydedebilirsiniz.

> [!NOTE]
> ASP.NET and Web Tools 2012,2 sürümü SQL Server Veri Araçları içermez. SQL Server ve Windows Azure SQL veritabanları, çevrimdışı proje destekli geliştirme, şema karşılaştırma ve gelişmiş veritabanı dağıtım özellikleri dahil olmak üzere daha zengin bir veritabanı araçları kümesi sağlar. Daha fazla bilgi veya SQL Server Veri Araçları yüklemek için [https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127)ziyaret edin.

<a id="_Documentation"></a>
## <a name="documentation"></a>Belgeler

ASP.NET and Web Tools 2012,2 hakkındaki öğreticiler ve diğer bilgiler ASP.NET Web sitesinden edinilebilir (https://www.asp.net).

<a id="_Support"></a>
## <a name="support"></a>Destek

ASP.NET and Web Tools 2012,2 resmi olarak serbest bırakılır ve desteklenir. Normal destek kanalınızı kullanabilirsiniz. Ayrıca, ASP.NET Community üyelerinin çok sayıda resmi olmayan destek sağlayabildiği ASP.NET forumlarına ([https://forums.asp.net/](https://forums.asp.net/)) sorular da gönderebilirsiniz.

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a>Yazılım Gereksinimleri

2012,2 ASP.NET and Web Tools web için Visual Studio 2012 veya Visual Studio Express 2012 gerektirir.

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a>ASP.NET and Web Tools 2012,2 ' deki yeni özellikler

Bu bölümde ASP.NET and Web Tools 2012,2 sürümünde tanıtılan özellikler açıklanmaktadır.

<a id="_Tooling"></a>
### <a name="tooling"></a>Araçlar

- Sayfa Denetçisi 

    - Sayfa denetçisi 'ne, sayfaya karşılık gelen JavaScript koduna geri eklenen öğeleri eşlemeye izin veren JavaScript seçim eşlemesini destekler.
    - CSS güncelleştirmelerini gerçek zamanlı olarak görme özelliği.
    - Daha fazla bilgi için, [sayfa denetçisinde CSS otomatik eşitleme ve JavaScript seçim eşlemesini](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx)okuyun.
- Düzenleyici 

    - CoffeeScript, Mustache, Handleçubuklar ve JsRender için sözdizimi vurgulamasını destekler.
    - HTML Düzenleyicisi, altını gizleme bağlamaları için IntelliSense sağlar.
    - DAHA az kullanarak dinamik CSS oluşturmayı etkinleştirmek için daha az düzen ve derleyici desteği.
    - JSON 'ı bir .NET sınıfı olarak yapıştırın. JSON 'ı bir C# veya vb.NET kod dosyasına yapıştırmak Için bu özel yapıştırma komutunu kullanma ve Visual Studio OTOMATIK olarak JSON 'dan çıkarılan .NET sınıfları oluşturur.
- Mobil öykünücü desteği, üçüncü taraf öykünücülerin VSıX olarak yüklenebilmesi için genişletilebilirlik kancaları ekler. Geliştiricilerin Web sitelerini çeşitli mobil cihazlarda önizleme yapabilmesi için, F5 açılan menüsünde yüklü Öykünücüler görünür. [Visual Studio ile yeni BrowserStack tümleştirmesinde](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx)Scott Hanselman 'ın blog girişinde bu özellik hakkında daha fazla bilgi edinin.

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a>Web yayımlaması

- Web sitesi projeleri artık Microsoft Azure Web siteleri 'ne yayımlama dahil Web uygulaması projeleriyle aynı yayımlama deneyimine sahiptir.
- Bir veya &#8211; daha fazla dosya için seçmeli yayımlama aşağıdaki eylemleri gerçekleştirebilir (bir Web dağıtımı uç noktasına yayımladıktan sonra): 

    - Seçili dosyaları Yayımla.
    - Yerel bir dosya ile uzak dosya arasındaki farka bakın.
    - Yerel dosyayı uzak dosyayla güncelleştirin veya uzak dosyayı yerel dosyayla güncelleştirin.

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a>ASP.NET MVC şablonları

- Yeni Facebook Uygulama şablonu, Facebook Canvas uygulamalarını yazmayı kolaylaştırır. Birkaç basit adımda, oturum açmış bir kullanıcıdan veri alan ve arkadaşlarıyla entegre olan bir Facebook uygulaması oluşturabilirsiniz. Şablon; kimlik doğrulama, izinler, Facebook verilerine erişme ve daha fazlası gibi Facebook uygulaması oluşturmaya ilişkin tüm ayarlamaları halletmeniz için yeni bir kitaplık içerir. Facebook uygulama şablonunu kullanma hakkında daha fazla bilgi için bkz. [https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921).
- Tek Sayfalı Uygulama MVC şablonu; geliştiricilerin HTML 5, CSS 3, ve popüler Knockout ve jQuery JavaScript kitaplıklarını kullanarak ASP.NET Web API üstünde etkileşimli istemci tarafı web uygulamaları oluşturmalarına imkan verir. Şablon, bir daha iyi sunucu API 'SI kullanan bir JavaScript HTML5 uygulaması oluşturmak için ortak uygulamaları gösteren bir "Todo" liste uygulaması içerir. [https://www.asp.net/single-page-application](../single-page-application/index.md)daha fazla bilgi edinebilirsiniz.
- Artık ASP.NET MVC yeni proje iletişim kutusuna yeni şablonlar ekleyen bir VSıX oluşturabilirsiniz. Nasıl yapıldığını öğrenin: [https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)
- FixedDisplayModes Package &#8211; MVC proje ŞABLONLARı, MVC 4 ' teki bir hata için geçici çözüm içeren yeni ' Fixeddisplaymodes ' NuGet paketini içerecek şekilde güncelleştirilmiştir. Pakette bulunan düzeltmeyle ilgili daha fazla bilgi için, MVC ekibinden bu blog gönderisine ([https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)) bakın.

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET Web API 'SI, birkaç yeni özellik ile geliştirilmiştir:

- ASP.NET Web API OData
- ASP.NET Web API 'SI Izleme
- ASP.NET Web API Yardım sayfası

#### <a name="aspnet-web-api-odata"></a>ASP.NET Web API OData

ASP.NET Web API OData, tüm veri kaynakları üzerinde zengin iş mantığı ile OData uç noktaları oluşturmak için gereken esnekliği sağlar. ASP.NET Web API OData ile, göstermek istediğiniz OData semantiğinin miktarını kontrol edersiniz. ASP.NET Web API OData, ASP.NET MVC 4 proje şablonlarına dahildir ve NuGet ([http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)) ' de de kullanılabilir.

ASP.NET Web API 'SI OData Şu anda aşağıdaki özellikleri desteklemektedir:

- [Queryable] özniteliğini uygulayarak OData sorgu semantiğini etkinleştirin.
- OData sorgularını kolayca doğrulayın ve desteklenen sorgu seçenekleri, işleçler ve işlevler kümesini kısıtlayın.
- Parametresi, daha sonra doğrulanabilir ve bir IQueryable veya IEnumerable öğesine uygulanabilen sorgunun bir soyut sözdizimi ağacı gösterimini almak için doğrudan ODataQueryOptions öğesine bağlanır.
- [Queryable] özniteliğinde sonuç sınırlarını belirterek hizmet odaklı sayfalama ve sonraki sayfa bağlantısı oluşturmayı etkinleştirin.
- $İnlinecount kullanarak toplam eşleşen kaynak sayısının satır içi sayısını isteyin.
- Null yaymayı denetleyin.
- $Filter tüm/tüm işleçler.
- Bir varlık veri modelini kurala göre çıkarın veya bir modeli Entity Framework koduna benzer şekilde açıkça özelleştirin.
- Varlık kümelerini EntitySetController 'dan türeterek kullanıma sunun.
- Gezinti özelliklerini ortaya çıkarmak, bağlantıları işlemek ve OData eylemlerini uygulamak için basit, özelleştirilebilir kurallar.
- MapODataRoute genişletme yöntemi kullanılarak Basitleştirilmiş yönlendirme.
- Birden çok EDM modeli açığa çıkarmak için sürüm oluşturma desteği.
- Web API 'niz için istemcileri (.NET, Windows Phone, Windows Mağazası vb.) oluşturabilmeniz için hizmet belgesi ve $metadata kullanıma sunun.
- OData atom, JSON ve JSON ayrıntılı biçimleri için destek.
- Oluşturma, güncelleştirme, kısmen güncelleştirme (Düzeltme Eki) ve varlıkları silme.
- Varlıklar arasındaki ilişkileri sorgulama ve değiştirme.
- Rotalarınızda bağlantı sağlayan ilişki bağlantıları oluşturun.
- Karmaşık türler.
- Varlık türü devralma.
- Koleksiyon özellikleri.
- Maların.
- OData eylemleri.
- WCF Veri Hizmetleri ile aynı temel üzerine kurulmuştur, yani ODataLib ([http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)).

ASP.NET Web API OData hakkında daha fazla bilgi için bkz. [https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141).

#### <a name="aspnet-web-api-tracing"></a>ASP.NET Web API 'SI Izleme

ASP.NET Web API Izleme, .NET Izleme ile Web API 'lerinizin izleme verilerini tümleştirir. Artık varsayılan olarak Web API proje şablonunda etkindir. Web API 'leriniz için izleme verileri çıkış penceresine gönderilir ve IntelliTrace aracılığıyla kullanılabilir hale getirilir. ASP.NET Web API 'SI Izleme, Windows [Azure tanılama](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx)ile tümleştirme aracılığıyla Windows Azure 'da barındırılırken Web API 'niz hakkındaki bilgileri izlemenizi sağlar. Ayrıca, ASP.NET Web API Izleme NuGet paketini ([http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)) kullanarak herhangi bir uygulamada ASP.NET Web API izlemeyi yükleyebilir ve etkinleştirebilirsiniz.

ASP.NET Web API Izlemeyi yapılandırma ve kullanma hakkında daha fazla bilgi için bkz. [https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874).

#### <a name="aspnet-web-api-help-page"></a>ASP.NET Web API Yardım sayfası

ASP.NET Web API 'SI yardım sayfası artık varsayılan olarak Web API proje şablonunda bulunur. ASP.NET Web API Yardım sayfası, HTTP uç noktaları, desteklenen HTTP yöntemleri, parametreler ve örnek istek ve yanıt iletisi yükleri dahil Web API 'Leri için otomatik olarak belgeler oluşturur. Belgeler kodunuzdaki açıklamalardan otomatik olarak çekilir. Ayrıca, ASP.NET Web API Yardım sayfası NuGet paketini ([http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)) kullanarak herhangi bir uygulamaya ASP.NET Web API 'Si yardım sayfasını ekleyebilirsiniz.

ASP.NET Web API 'SI yardım sayfasını ayarlama ve özelleştirme hakkında daha fazla bilgi için bkz. [https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140).

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a>ASP.NET SignalR

ASP.NET SignalR, kullanılabilir olduğunda WebSockets kullanarak ve olmadığında otomatik olarak diğer tekniklerin geri düşmesini sağlayan ASP.NET uygulamanıza gerçek zamanlı web özellikleri eklemenizi kolaylaştırır.

ASP.NET SignalR kullanma hakkında daha fazla bilgi için bkz. [https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271).

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a>ASP.NET Kolay URL'leri

ASP.NET Elyurls, Web Forms geliştiricilerinin temizleyici URL 'Leri (. aspx uzantısı olmadan) üretmesini çok kolay hale getirir. Daha az yapılandırma gerektirmez ve mevcut ASP.NET v 4.0 uygulamalarıyla birlikte kullanılabilir. Kolay URL 'ler özelliği ayrıca, masaüstü ve mobil görünümler arasında geçiş yapmayı destekleyerek geliştiricilerin uygulamalarına mobil destek eklemesini kolaylaştırır.

ASP.NET kullanımı kolay URL 'Leri yükleme ve kullanma hakkında daha fazla bilgi için [http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)bakın.

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a>Bilinen sorunlar ve son değişiklikler

Bu bölümde ASP.NET and Web Tools 2012,2 sürümündeki bilinen sorunlar ve son değişiklikler açıklanmaktadır.

### <a name="installation-issues"></a>Yükleme Sorunları

#### <a name="out-of-order-installs-of-visual-studio-2012"></a>Visual Studio 2012 'nin sıra dışı yüklemeleri

ASP.NET and Web Tools 2012,2 ' i yükledikten sonra ek bir Visual Studio 2012 SKU 'SU yüklemek bir onarım işlemi gerektirir. Aşağıdaki sırayı göz önünde bulundurun:

1. Web için Visual Studio 2012 Express 'ı yükler
2. ASP.NET and Web Tools 2012,2 'yi yükler
3. Visual Studio 2012 Professional, Premium veya Ultimate 'ı yükler

2\. adım yalnızca Web için Express güncelleştirmelerini yüklemeye neden olur. 3\. adım sırasında yüklenen ek SKU 'nun güncelleştirmeyi içerdiğinden emin olmak için, yüklenen son SKU için güncelleştirmeleri yüklemek üzere 2012,2 ASP.NET and Web Tools onarmanız gerekir. Bu Ayrıca, 1 ve 3. adımdaki SKU 'Lar tersine çevrilirse da geçerlidir.

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a>Visual Studio açık olduğunda Microsoft ASP.NET and Web Tools 2012,2 yükleniyor

VS Microsoft ASP.NET and Web Tools 2012,2 yüklemesi sırasında açıksa, Visual Studio hatalı bir durumda bitebilirler. Kullanıcıların yüklemeye devam etmeden önce tüm Visual Studio örneklerini kapatması önerilir.

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a>Yükleme işleminin ortasında ASP.NET and Web Tools 2012,2 kurulumu iptal ediliyor

Yüklemenin ortasında ASP.NET and Web Tools 2012,2 kurulumu iptal edildiğinde, Visual Studio hatalı bir durumda bırakılır. Bu sorunu gidermek için şu adımları izleyin: 

- Program Ekle Kaldır 'a git
- Varsa Microsoft ASP.NET and Web Tools 2012,2 'yi kaldırın.
- Microsoft ASP.NET and Web Tools yeniden yükleyin 2012,2

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a>ASP.NET and Web Tools kaldırıldıktan sonra 2012,2 ASP.NET MVC 4 şablonları ve Razor V2 Web sitesi şablonları eksik

ASP.NET and Web Tools 2012,2 kaldırıldığında, Visual Studio 2012 ' den tüm ASP.NET MVC 4 ve Razor V2 Web sitesi şablonları da kaldırılır.

Geçici çözüm, ASP.NET MVC 4 ve Razor V2 Web sitesi şablonlarını yeniden yüklemek için Visual Studio 2012 yüklemenizin onarılmasına yönelik bir çözümdür.

### <a name="tooling-issues"></a>Araç sorunları

#### <a name="nuget-error-reported-during-project-creation"></a>Proje oluşturma sırasında NuGet hatası bildirildi

ASP.NET and Web Tools 2012,2 yükledikten sonra, MVC 4 projesi oluştururken aşağıdaki hatayı görebilirsiniz

![](aspnet-and-web-tools-20122-release-notes/_static/image1.png)

2012,2 ASP.NET and Web Tools NuGet 2,1 ' i sevk eder ve Visual Studio 2012 ' de uzantıyı yükseltir. Bazı durumlarda, VSıX yükleyicisi VSıX 'i doğru bir şekilde güncelleştiremeyecektir. Aşağıdaki adımlar bu sorunu ele almak için size olanak sağlayacak:

1. Visual Studio 2012 ' i yönetici olarak Başlat
2. Araçlar-&gt;Uzantılar ve güncelleştirmeler 'e gidin ve NuGet 'i kaldırın.
3. Visual Studio’yu kapatın
4. ASP.NET and Web Tools 2012,2 yükleme klasörüne gidin:

    1. Visual Studio 2012 için: **Program FILES\MICROSOFT ASP. NET\ASP.NET Web Stack\adim $2012**
    2. Web için Visual Studio 2012 Express için: **Program FILES\MICROSOFT ASP. NET\ASP.NET Web Stack\adim Web Için Visual Studio express 2012**
5. NuGet 'i yeniden yüklemek için NuGet. Tools. vsix öğesine çift tıklayın

### <a name="web-api-issues"></a>Web API sorunları

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a>$filter ve DateTime değişmez değerlerinde ayrıştırma sorunları

OData URI ayrıştırıcısı kısmi DateTime sabit değerlerini doğru bir şekilde ayrıştıramaz. Örneğin, $filter = start EQ DateTime ' 2012-12-31T12:00 ' düzgün ayrıştırılamaz. Geçici bir çözüm, $filter = start EQ DateTime ' 2012-12-31T12:00:00 ' olan tam sabit değeri kullanmaktır.

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a>OData, büyük/küçük harfe duyarsız özellik adlarını desteklemez.

OData, OData sorgularında ve OData yolunda büyük/küçük harfe duyarsız özellik adlarını desteklemez. Bkz. WorkItems:

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

Kullanıcıların JavaScript istemci tarafında ve sunucu tarafında farklı bir büyük harfe sahip olması halinde bu sorunla karşılaşacaktır. Bu sorun OData protokolünde tasarıma göre yapılır. Ancak, birçok kullanıcı bu sorunu raporlar. Bu soruna geçici bir çözüm bulmak için, kullanıcıların bu durumlarını URL 'de düzeltmesine sahip olması gerekir.

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a>Varsayılan OData yönlendirme kuralları, gezinti özelliğinde gönderi/PUT işlemini desteklemez.

Varsayılan OData yönlendirme kuralları, gezinti özelliğinde gönderi/PUT işlemini desteklemez. Bkz. WorkItem [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366). Varsayılan kurallar bölümünde yaygın olarak kullanılan bu kuralı kaçırdık.

Bu soruna geçici bir çözüm olarak, kullanıcıların bunu desteklemesi için yeni yönlendirme kuralını genişletmesi gerekir.

### <a name="facebook-template-issues"></a>Facebook şablonu sorunları

#### <a name="facebook-application-template-only-works-using-net-45"></a>Facebook uygulama şablonu yalnızca .NET 4,5 kullanılarak çalışmaktadır

ASP.NET MVC 4 ' te Facebook uygulama şablonunu görmek için yeni proje iletişim kutusundaki çerçeve açılan listesinde .NET 4,5 ' i seçmeniz gerekir.

#### <a name="real-time-update-controller"></a>Gerçek zamanlı güncelleştirme denetleyicisi

Facebook uygulama şablonu, kullanıcının Facebook 'tan gerçek zamanlı güncelleştirmeleri işlemek için kolayca bir Web API denetleyicisi oluşturmalarına olanak tanır. Geliştirme makineniz NAT 'nin arkasındaysa, denetleyicinizde daha fazla ağ yapılandırması yapılmadan çalışmayabilir. Ayrıntılar için buraya bakın: [http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a>Sorgu dizesi değerleri Facebook OAuth parametreleriyle çakışıyor

Aşağıdaki alanlar Facebook OAuth iletişim kutusunun geri arama URL 'SI ile çakışıyor. Kendi sorgu dizesi değerlerinizi şu adlarla eklemeyin: kod, hata, hata\_açıklama, hata\_neden.

#### <a name="using-page-inspector-with-facebook-template"></a>Facebook şablonuyla sayfa denetçisini kullanma

Facebook uygulamanızda hata ayıklarken Visual Studio 2012 ' deki sayfa denetçisi özelliğini kullanamazsınız. Sayfa denetçisi Şu anda iframe 'leri desteklemiyor.

### <a name="single-page-application-template-issues"></a>Tek sayfalı uygulama şablonu sorunları

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a>JQuery 1.9/altını gizleme 2.2.1 güncelleştirmesi ile, varsayılan MVC SPA projesi çalıştırılırken yeni Todo öğesi düzenleme ENTER odak olayı düzgün işlenmez.

JQuery 1.9/altını gizleme 2.2.1 güncelleştirmesi ile, varsayılan MVC SPA projesi çalıştırılırken yeni Todo öğesi düzenleme girişi artık yeni Todo öğesi yapılacaklar listesine girildikten sonra yeni Todo öğesi düzenleme kutusuna geri odaklanmayacaktır.

[http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html)geçici çözüm başvurusu ve aşağıdaki örnek koda benzer bir onarım yapın:

Dosya Todo. model. js  
 Function ToDoList (veri), aşağıdakileri ekleyin:  
 **Self. IsSelected = ko. Observable (false);**

Function todoList. prototype. addTodo, aşağıdaki Blacked metnini ekleyin:  
 **Self. IsSelected (true);**  
 Self. newTodoTitle (&quot;&quot;);

Dosya index. cshtml, aşağıdaki Blacked metnini ekleyin:  
 &lt;form verileri-bind =&quot;gönderme: addTodo&quot;&gt;  
 &lt;Input Class =&quot;addTodo&quot; Type =&quot;Text&quot; Data-bind =&quot;değer: newTodoTitle, PlaceHolder: ' eklemek için buraya yazın ', blurOnEnter: true, **HasFocus: IsSelected**, Event: {bulanıklığı: addtodo}&quot; /&gt;  
 &lt;form&gt;
