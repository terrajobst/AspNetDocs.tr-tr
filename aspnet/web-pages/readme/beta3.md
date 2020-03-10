---
uid: web-pages/readme/beta3
title: Web Matrix ve ASP.NET Web Pages (Razor) Beta 3 yayın Benioku | Microsoft Docs
author: rick-anderson
description: WebMatrix ve ASP.NET Web Sayfaları (Razor) Beta 3 Yayını Benioku Dosyası
ms.author: riande
ms.date: 01/10/2011
ms.assetid: ffa3d5c9-91e5-4da3-b409-560b0c7fbbf0
msc.legacyurl: /web-pages/readme/beta3
msc.type: content
ms.openlocfilehash: dc1d9237c04a7fcdbf4db6ccc8c36d255f6de003
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628900"
---
# <a name="web-matrix-and-aspnet-web-pages-razor-beta-3-release-readme"></a>WebMatrix ve ASP.NET Web Sayfaları (Razor) Beta 3 Yayını Benioku Dosyası

> WebMatrix ve ASP.NET Web Sayfaları (Razor) Beta 3 Yayını Benioku Dosyası

9 Kasım 2010

## <a name="contents"></a>İçindekiler

- [Genel bakış](#Overview)
- [Yükleme](#Installation_Notes)
- [Beta 3 sürümündeki yeni özellikler, değişiklikler ve bilinen sorunlar](#Known_Issues)

    - [WebMatrix yükleme sorunları](#Known_Issues_Installation)
    - [ASP.NET Web Sayfaları](#Known_Issues_ASPNET)
    - [SQL Server Compact](#Known_Issues_SQL_Server_Compact)
    - [Uygulamaları yükleme](#Known_Issues_Installing_Applications)
    - [Uygulamaları yayımlama](#Known_Issues_Publishing_Applications)
    - [Diğer Sorunlar](#Known_Issues_Other_Issues)
- [Daha fazla bilgi için](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a>Genel bakış

> Microsoft WebMatrix Beta, dakikalar içinde yüklenen ücretsiz bir Web geliştirme yığınıdır. Tek ve tümleşik bir deneyim oluşturmak için veritabanı ve programlama çerçeveleri ile bir Web sunucusunu tümleştirir. WebMatrix Beta 'yı kullanarak kendi ASP.NET veya PHP Web sitenizi kodlamanıza, test etmeniz ve yayımlamanıza olanak sağlayabilir veya DotNetNuke, dönen Raco, WordPress veya Joomla gibi popüler açık kaynaklı uygulamaları kullanarak yeni bir Web sitesi başlatmak için WebMatrix Beta 'yı kullanabilirsiniz. WebMatrix Beta, geliştirmeden üretime sorunsuz ve sorunsuz bir şekilde geçiş yapan web sitenizi Internet üzerinde çalıştıracak olan güçlü Web sunucusu, veritabanı altyapısı ve çerçeveler ortamını kullanır.

<a id="Installation_Notes"></a>

## <a name="installation"></a>Yükleme

> WebMatrix Beta 3 ' ü yüklemek için [Microsoft Web Platformu Yükleyicisi 3,0](https://go.microsoft.com/fwlink/?LinkID=194638)' i kullanırsınız. Web Platformu Yükleyicisi 'ni yükledikten sonra, WebMatrix Beta 3 ' ü yüklemek için kullanabilirsiniz.
> 
> Yükleme sırasında sorunlarla karşılaşırsanız [Microsoft Web Platformu Yükleyicisi sorun giderme sorunları](https://go.microsoft.com/fwlink/?LinkId=196212)bölümüne bakın.

<a id="Installation_Notes0"></a>

## <a name="instructions-for-publishing-applications"></a>Uygulama yayımlama yönergeleri

> Bkz. [uygulamaları yayımlamak Için adım adım yönergeler](https://go.microsoft.com/fwlink/?LinkID=196149)

<a id="Known_Issues"></a>

## <a name="new-features-changes-andknown-issues"></a>Yeni özellikler, değişiklikler ve bilinen sorunlar

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-beta-3-installation"></a>WebMatrix Beta 3 yüklemesi

#### <a name="issue-webmatrix-beta-3-is-only-available-on-platforms-that-support-microsoft-net-framework-4"></a>Sorun: WebMatrix Beta 3 yalnızca Microsoft .NET Framework 4 ' ü destekleyen platformlarda kullanılabilir

> WebMatrix Beta için .NET Framework sürüm 4 gereklidir. Bazı durumlarda, WebMatrix Beta yükleyicisi, desteklenen yapılandırma kümesinin parçası olmayan bir platforma yükleme denemenize imkan tanır. Özellikle, SP1 güncelleştirmesi olmayan Windows Vista, WebMatrix Beta yüklemesine başlamanızı sağlar, ancak .NET Framework 4 bileşeni başarısız olur ve yüklemenizi engeller.
> 
> **Geçici çözüm**  
> Aşağıdakileri içeren desteklenen bir platforma yükler:
> 
> - Windows 7
> - Windows Server 2008
> - Windows Server 2008 R2
> - Windows Vista SP1 veya sonraki sürümü
> - Windows XP SP3
> - Windows Server 2003 SP2

#### <a name="issue-cannot-install-webmatrix-beta-3-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a>Sorun: Microsoft Visual Studio 2008 SP1 olmadan Microsoft Visual Studio 2008 yüklenirse WebMatrix Beta 3 yüklenemiyor

> **Geçici çözüm**  
> [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) 'ı Microsoft İndirme Merkezi ' nden yükleyin.

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a>Sorun: SQL Server Compact 4,0 için bazı derlemeler GAC 'de yüklü değil

> SQL Server Compact 4,0 için yönetilen derlemeler, SQL Server Compact 4,0 ' i bir 64 bit bilgisayara yüklediğinizde ve bilgisayarda yalnızca .NET Framework 3,5 SP1 Istemci profili yüklü olduğunda genel derleme önbelleği 'ne (GAC) yerleştirilmez. GAC 'de yüklü olmayan yönetilen derlemeler şunlardır:
> 
> - *System. Data. SqlServerCe. dll* (ADO.NET sağlayıcısı)
> - *System. Data. SqlServerCe. Entity. dll* (ADO.NET Entity Framework)
> 
> **Geçici çözüm**  
> SQL Server Compact 4,0 'yi kaldırın. Aşağıdaki konumdan .NET Framework 3,5 SP1 'in tam sürümünü indirip yükleyin:  
>   
> [Microsoft .NET Framework 3,5 Service Pack 1 (tam paket)](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> SQL Server Compact 4,0 yeniden yükleyin.

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a>Sorun: komut satırı kullanılarak SQL Server Compact kaldırılamıyor

> Komut satırı seçeneklerini kullanarak SQL Server Compact kaldırılması bu sürümde çalışmaz.
> 
> **Geçici çözüm**  
> 4,0 Microsoft SQL Server Compact kaldırmak için Windows Denetim Masası 'ndaki *Programlar ve Özellikler ' i* kullanın.

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a>ASP.NET Web Sayfaları

Belgenin bu bölümünde, Razor söz dizimi ile ASP.NET Web sayfalarının Beta 3 sürümündeki yeni özellikler, değişiklikler ve bilinen sorunlar açıklanmaktadır.

- [Yeni özellikler](#NewFeatures)
- [Değişikliklerine](#Changes)
- [Sorunlar](#Issues)

<a id="NewFeatures"></a>

#### <a name="new-features-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a>Razor sözdizimi olan ASP.NET Web sayfaları için Beta 3 ' teki yeni özellikler

#### <a name="new-htmlraw-method-renders-unencoded-markup"></a>Yeni: "HTML. RAW" yöntemi, kodlanmamış biçimlendirmeyi işler

> Yeni `Html.Raw` yöntemi, HTML işaretlemesini kodlanmış çıktıyı işlemek yerine biçimlendirme olarak işlemenize olanak sağlar. (Varsayılan olarak, ASP.NET Razor dizeleri işlemeden önce kodlar.) Sözdizimi şöyledir:
> 
> `Html.Raw(value)`
> 
> Aşağıdaki örnek `Html.Raw`nasıl kullanacağınızı gösterir:
> 
> [!code-cshtml[Main](beta3/samples/sample1.cshtml)]

<a id="Changes"></a>

#### <a name="changes-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a>Razor sözdizimi olan ASP.NET Web sayfaları için Beta 3 değişiklikleri

#### <a name="change-hrefattribute-method-removed"></a>Değişiklik: "HrefAttribute" yöntemi kaldırıldı

> `WebPage` sınıfının `HrefAttribute` yöntemi kaldırıldı. Bu yardımcı, URL 'lerde güvenli olmayan karakterleri kodlamak için kullanıldı. ASP.NET Razor dizeleri otomatik olarak kodlarsa artık gerekli değildir. (Kodlanmış dizeleri işlemek için yeni `Html.Raw` yöntemini kullanın.)

#### <a name="change-syntax-for-declarative-helper-helpers-changed"></a>Değişiklik: bildirime dayalı "@helper" yardımcıları için sözdizimi değişti

> Beta 3 sürümünde, ASP.NET `@helper` söz dizimi kullanılarak oluşturulan yardımcıları nasıl ayrıştırdığı de değişir. Temelde `@helper` sözdizimi, kod içerebilen bir biçimlendirme bloğu yerine bir kod bloğu olarak ayrıştırılır. Bu nedenle, yardım içindeki kodun `@{ }` blokları içine alınması gerekmez. Buna karşılık, yardımın içindeki biçimlendirmenin HTML öğelerine veya ASP.NET Razor `<text></text>` etiketlerine açık bir şekilde eklenmesi gerekir.
> 
> Örneğin, aşağıdaki `@helper` sözdizimi Beta 3 sürümünde çalışmaktadır:
> 
> [!code-cshtml[Main](beta3/samples/sample2.cshtml)]
> 
> Beta 3 sürümünde, bu yardımcının aşağıdaki örnekteki gibi görünmesi için değiştirilmesi gerekir:
> 
> [!code-cshtml[Main](beta3/samples/sample3.cshtml)]
> 
> Yardımdaki ilk kod etrafında `@{ }` karakterlerin artık kullanılmadığını unutmayın. Bunun nedeni, yardımcılar içeriğinin varsayılan olarak bir kod bloğu olarak kabul edilmesidir. Yardımcısı, açma `<a>` etiketiyle başlayan biçimlendirmeyi işler. Yardımcının bir kapanış etiketi içermeyen düz metin veya etiketleri işlemesi gerekiyorsa (örneğin, `<meta>` etiketleri), işlenecek içerik `<text></text>` etiketlerinde olmalıdır.

#### <a name="change-webpagecontexthttpcontext-removed"></a>Değişiklik: "WebPageContext. HttpContext" kaldırıldı

> `WebPageContext.HttpContext` özelliği kaldırılmıştır. Bunun yerine `HttpContext.Current` kullanın. (`WebPageContext.HttpContext` özelliği bunu sarmalanmış.)

#### <a name="change-facebook-helper-moved-to-new-package"></a>Değişiklik: "Facebook" Yardımcısı yeni pakete taşındı

> `Facebook` Yardımcısı, `Facebook` Yardımcısı ve ek işlevler içeren *Facebook. Helper* kitaplığına taşınmıştır. Bu kitaplığı, [ASP.net Pages Ile çalışmaya](https://go.microsoft.com/fwlink/?LinkId=202889)başlama öğreticisindeki "Paket Yöneticisi Ile yükleme yardımcıları" bölümünde açıklandığı gibi ayrı bir paket olarak yüklemeniz gerekir.

#### <a name="change-membership-role-and-security-types-moves-to-new-assembly"></a>Değişiklik: üyelik, rol ve güvenlik türleri yeni derlemeye gider

> Aşağıdaki türler `WebMatrix.WebData` derlemesine taşındı:
> 
> - `ExtendedMembershipProvider`
> - `SimpleMembershipProvider`
> - `SimpleRoleProvider`
> - `WebSecurity`

#### <a name="change-tagbuilder-class-moved-to-systemwebwebpagesdll-assembly"></a>Değişiklik: "TagBuilder" sınıfı System. Web. Web sayfası. dll derlemesine taşındı

> `TagBuilde` r sınıfı System. Web. Web sayfası. dll derlemesine taşınmıştır. Daha önce bu, ASP.NET MVC 'nin bir parçası olan bir derlemedir. Bu değişiklik, `TagBuilder` sınıfını kullanabilmeniz için ASP.NET MVC 'yi yüklemek zorunda değilsiniz anlamına gelir.
> 
> Ancak, sınıfı hala `System.Web.Mvc` ad alanında bulunur. `TagBuilder` sınıfını kullanmak için (örneğin, özel bir ASP.NET Razor Yardımcısı), ad alanına başvurmanız gerekir (örneğin, kodunuza `@using System.Web.Mvc` ekleyerek).

#### <a name="change-request-validation-syntax-changed-validation-class-removed"></a>Değişiklik: Istek doğrulama sözdizimi değişti; "Doğrulama" sınıfı kaldırıldı

> Beta 3 sürümünde, tek bir alan veya alan kümesi için doğrulamayı devre dışı bırakmak üzere, doğrulamanın dışında tutulacak alanların adını veya adlarını geçirerek `Validation.Exclude` yöntemini çağırabilirsiniz. Beta 3 sürümünde doğrulamayı atlamak için yeni bir sözdizimi mevcuttur. Beta 3 ' te kullanılan `Validation` yöntemi kaldırılmıştır.
> 
> > [!NOTE]
> > İstek doğrulamasını devre dışı bırakırsanız, kullanıcılar HTML işaretlemesini karşıya yüklemeye çalışır (örneğin, bir sayfada zengin metin düzenleyicisi kullanarak), Web sitesi potansiyel olarak tehlikeli bir Istek gibi bir hata bildirir *. Istemciden form değeri algılandı* ve Kullanıcı girişi kabul edilmedi. İstek doğrulamayı devre dışı bırakırsanız, [Microsoft Anti-Cross site betik kitaplığı v 4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651)gibi bir şey kullanarak potansiyel olarak tehlikeli biçimlendirme veya betik içermediğinden emin olmak için Kullanıcı girişini el ile denetlemeniz gerekir.
> 
> 
> Otomatik istek doğrulamayı devre dışı bırakmak için `Request.Unvalidated` yöntemini çağırın, bu, alanı veya için istek doğrulamayı atlamak istediğiniz başka bir post nesnesinin adını geçirerek. `Form`, `QueryString`, `Cookies`ve `ServerVariables` koleksiyonlarındaki öğelerin doğrulanmasını atlamak için bu yöntemi kullanabilirsiniz. Aşağıdaki örneklerde `Unvalidated` yönteminin nasıl kullanılacağı gösterilmektedir:
> 
> [!code-csharp[Main](beta3/samples/sample4.cs)]

<a id="Issues"></a>

#### <a name="known-issues-for-aspnet-web-pages-with-razor-syntax"></a>Razor sözdizimi ile ASP.NET Web sayfaları için bilinen sorunlar

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a>Sorun: üyelik için özel bir kullanıcı tablosu kullanılırken beklenmeyen davranış

> Bir ASP.NET Razor Web sitesinin üyelik sağlayıcısını başlatmak için `WebSecurity.InitializeDatabaseConnection` yöntemini çağırın. (WebMatrix 'te, başlatıcı site şablonu *\_AppStart. cshtml* dosyasında Bu metoda bir çağrı içerir.) Bu yöntemin `autoCreateTables` parametresi true olarak ayarlanmışsa (varsayılan olarak, başlatıcı site şablonunda true olarak ayarlanır) ve tanınmayan bir tablo adı yönteme (ikinci parametre) geçirilirse Yöntem bir hata oluşturmaz. Bunun yerine, tabloyu otomatik olarak oluşturur.
> 
> Bu, üyelik için özel bir kullanıcı tablosu kullanmayı amaçlıyorsanız ancak yanlış tablo adını `WebSecurity.InitializeDatabaseConnection` yöntemine geçirirseniz bir sorun olabilir. Yöntemi varsayılan olarak, belirttiğiniz tablo yoksa ve bunun yerine yeni bir tablo oluşturduğunda bir hata oluşturmaz, uygulama çalışıyor olarak görünebilir. Ancak, Özel Kullanıcı tablonuza (ve içindeki alanlarda) bağlı olan uygulama kodu sonunda beklenmedik hatalarla başarısız olabilir.
> 
> **Geçici çözüm**  
> `InitializeDatabaseConnection` yönteminde geçirilen adın, üyelik veritabanındaki kullanıcı profili tablosuyla eşleştiğinden emin olun veya `autoCreateTables` parametresinin false olarak ayarlandığından emin olun.

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a>Sorun: "SQL Server bir kullanıcı örneği oluşturulamadı" hatası

> Bir WebMatrix Web uygulaması SQL Server Express kullanıyorsa ve Windows 7 veya Windows Server 2008 R2 üzerinde IIS 7,5 çalıştırıyorsa, SQL Server kullanıcının yerel uygulama yolunu çalışma zamanında alamadığını belirten bir hata görebilirsiniz.
> 
> **Geçici çözüm** Uygulamanın altında çalıştığı Windows hesabının (genellikle ağ HIZMETI) uygulamanın kök klasörleri ve *App\_verileri*gibi alt klasörler için okuma/yazma izinlerine sahip olduğundan emin olun. [SQL Server Express Kullanıcı örneği oluşturma ve ASP.NET Web uygulaması projeleriyle](https://support.microsoft.com/kb/2002980)Ilgili Bilgi Bankası makalesi sorunlarını daha ayrıntılı olarak bulabilirsiniz.

#### <a name="issue-in-visual-studio-namespaces-for-custom-assemblies-dlls-are-not-imported-automatically"></a>Sorun: Visual Studio 'Da özel derlemeler (dll 'Ler) için ad alanları otomatik olarak içeri aktarılmaz

> Visual Studio 'da bir projede özel derlemeler kullanıyorsanız, bu derlemelerde belirtilen ad alanları tasarım zamanında otomatik olarak içeri aktarılmaz. Sonuç olarak, özel türlere yapılan başvurular tasarım zamanında tanınmayabilir ve Visual Studio 'da tanınmıyor olarak işaretlenir ("dalgalı çizgi" kullanılarak). Bu sorun yalnızca Visual Studio 'da tasarım zamanında oluşur; uygulamanın kendisi düzgün şekilde çalışır.
> 
> **Geçici çözüm**  
> Tasarım zamanında tanınmayan varlıklara başvuran bir `using` deyimin (Visual Basic`imports`) dahil edin.

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a>Sorun: Visual Studio IntelliSense ve proje şablonları yalnızca ASP.NET MVC sürüm 3 ' te kullanılabilir

> ASP.NET Web sayfalarının yüklenmesi, Visual Studio için IntelliSense ve ASP.NET Web sayfaları uygulamalarına yönelik proje şablonları gibi araçları da yüklemez.
> 
> **Geçici çözüm** Visual Studio 'da ASP.NET Web Pages uygulamaları için IntelliSense ve proje şablonları kullanmak üzere, Web Platformu Yükleyicisi veya [tek başına yükleyici](https://go.microsoft.com/fwlink/?LinkID=191797)aracılığıyla ASP.NET MVC 3 RC 'yi yükleme.

#### <a name="issue-lthelpergt-class-cannot-be-found-error"></a>Sorun: "&lt;yardımcı&gt; sınıfı bulunamıyor" hatası

> Beta 3 ' e yükselttikten sonra bir yardımcı sınıfın (örneğin, `Facebook` sınıfı) bulunamadığını belirten bir hata görebilirsiniz. Beta 2 ' den itibaren ve Beta 3 ' te devam eden yardımcılar, açıkça yüklenmesi gereken paketlere taşınmıştır. Mevcut siteler bu paketleri içerecek şekilde yükseltilmemiştir; Bu, *\Belgelerim\iisexpress* veya *\Belgelerim\web siteleri* klasörlerindeki siteleri içerir. Özellikle, *sitemdeki* (websitesi1) varsayılan siteyi kullanıyorsanız, `Twitter` Yardımcısı 'na bir başvuru içeren bu hatayı görürsünüz.
> 
> **Geçici çözüm**  
> Sitedeki herhangi bir yardımcıya yönelik çağrıları açıklama olarak *\_yönetici* sayfasını çalıştırın ve kullanmak istediğiniz yardımcıları içeren paketi veya paketleri yükleyebilirsiniz. Paketi yükledikten sonra, yardımcılar 'a başvuru yapan satırların açıklamasını kaldırabilirsiniz.

#### <a name="issue-deploying-beta-3-aspnet-razor-assemblies-to-the-bin-folder-might-not-work-on-hosting-sites"></a>Sorun: Beta 3 ASP.NET Razor derlemelerini bin klasörüne dağıtmak barındırma sitelerinde çalışmayabilir

> Bir barındırma sitesine ASP.NET Web sayfaları Web sitesini dağıtırsanız ve ASP.NET Razor Beta 3 derlemelerini sitenin *bin* klasörüne dağıtırsanız, aşağıdakiler de dahil olmak üzere hatalarla karşılaşabilirsiniz:
> 
> `Could not load type 'Microsoft.Web.Infrastructure.DynamicModuleHelper.DynamicModuleUtility' from assembly 'Microsoft.Web.Infrastructure, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`
> 
> Barındırma sağlayıcısı, ASP.NET Web sayfaları Beta 1 derlemelerini sunucunun genel uygulama önbelleğine (GAC) yüklemişse bu durum oluşabilir. GAC içindeki derlemeler, *bin* klasöründe yerel olarak yüklenen derlemelerin üzerine önceliğe sahip olur.
> 
> **Geçici çözüm** Gördüğünüz hataların sağlayıcının derlemelerin sürümleri ve sizinkilerle ilgili olduğunu doğrulamak için barındırma sağlayıcınızla iletişim kurun. Bu durumda, barındırma sağlayıcısının derlemeleri sunucunun GAC 'de güncelleştirmesini isteyin.

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a>Sorun: bir ara sunucu aracılığıyla akışları veya diğer dış verileri okuma

> Siteyi çalıştıran sunucu bir proxy sunucusunun arkasındaysa, sitenizin dışından gelen bilgileri okuyabilmeniz için *Web. config* dosyasındaki proxy bilgilerini yapılandırmanız gerekebilir. Örneğin, `ReCaptcha` yardımcısını kullanıyorsanız, yardımcı, reCAPTCHA hizmeti ile iletişim kurar, ancak proxy sunucunuz tarafından engelleniyor olabilir. Benzer şekilde, ASP.NET Web sayfalarında kullanılan ve paket yöneticisi tarafından kullanılan akış gibi akışlar ara sunucu yapılandırması gerektirebilir.
> 
> Bir dış hizmetle çalışırken veya paket akışı ile çalışırken sorunlarla karşılaşırsanız, aşağıdaki öğeleri uygulamanızın kök *Web. config* dosyasına yerleştirin:
> 
> [!code-xml[Main](beta3/samples/sample5.xml)]
> 
> Proxy sunucu yapılandırma hakkında daha fazla bilgi için, MSDN Web sitesindeki [&lt;proxy&gt; öğesi (ağ ayarları)](https://msdn.microsoft.com/library/sa91de1e.aspx) bölümüne bakın.

#### <a name="issue-microsoftwebinfrastructuredll-cannot-be-loaded-error"></a>Sorun: "Microsoft. Web. Infrastructure. dll yüklenemiyor" hatası

> Daha önce ASP.NET Web sayfalarının Beta 1 sürümünü Razor söz dizimi ve ardından Beta 3 sürümünü yüklerseniz, tüm uygun derlemeler *Microsoft. Web. Infrastructure. dll*hariç GAC 'ye yüklenir. Sonuç olarak, ASP.NET Razor sayfaları çalıştırdığınızda, *Microsoft. Web. Infrastructure. dll ' nin* yüklenemediğini belirten bir hata görürsünüz.
> 
> Beta 3 sürümünü temiz bir bilgisayara yüklediyseniz bu sorun oluşmaz.
> 
> **Geçici çözüm**  
> Denetim Masası 'nda ASP.NET Web sayfalarını kaldırın. Ardından Beta 3 sürümünü yeniden yükleyin.

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a>Sorun: .NET Framework sürüm 4 ' ü kaldırmak, Razor sözdizimi ile ASP.NET Web sayfalarını devre dışı bırakır

> .NET Framework sürüm 4 ' ü kaldırıp yeniden yüklerseniz, Razor söz dizimi Web sayfaları devre dışı bırakılır. *. Cshtml* uzantılı sayfalar düzgün çalışmaz. ASP.NET Web sayfaları, bir derlemeyi makine kök *Web. config* dosyasına kaydeder ve .NET Framework kaldırıldığında bu dosya kaldırılır. .NET Framework yeniden yüklemek, yapılandırma dosyasının yeni bir sürümünü yüklüyor, ancak ASP.NET Web Pages derlemesinin başvurusunu eklemez.
> 
> **Geçici çözüm** .NET Framework yeniden yükledikten sonra, ASP.NET Web sayfalarını Razor söz dizimi yeniden yükleyin. Bu, genellikle aşağıdaki konumda olan makine kökündeki *Web. config* dosyasına aşağıdaki öğeyi ekler:  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> 
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](beta3/samples/sample6.xml)]

#### <a name="issue-applications-previously-deployed-with-aspnet-assemblies-in-the-bin-folder-experience-errors"></a>Sorun: bin klasör deneyimi hatalarında daha önce ASP.NET Derlemeleriyle dağıtılan uygulamalar

> Dağıtım sırasında, ASP.NET Web sayfaları derlemelerinin (örneğin, *Microsoft. Web sayfaları. dll*), sunucudaki Web sitesinin *bin* klasörüne kopyaları. (Dağıtım sırasında veya geliştirici derlemeleri açıkça kopyalandığı için bu durum otomatik olarak oluşmuş olabilir.) Ancak, Beta 3 sürümü yüklendiğinde, belirli türlerin hataları gibi hatalar oluşur. Bu durum, Beta 3 sürümü için bir dizi ASP.NET Web sayfası türünün farklı ad alanlarına taşındığı için oluşur.
> 
> **Geçici çözüm**   
> Dağıtılan uygulamanın *bin* klasörünü temizleyin, yeni derlemeleri klasöre kopyalayın (veya uygulamayı yeniden dağıtın) ve uygulamayı yeniden başlatın.

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a>Sorun: Extensionless URL 'Leri IIS 7 veya IIS 7,5 üzerinde. cshtml/. vbhtml dosyalarını bulamıyor

> IIS 7 veya IIS 7,5 ' de, aşağıdakine benzer bir URL 'ye sahip istekler *. cshtml* veya *. vbhtml* uzantısına sahip sayfaları bulamaz:  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> Bu sorun ortaya çıkar çünkü URL yeniden yazma özelliği IIS 7 veya IIS 7,5 için varsayılan olarak etkinleştirilmemiştir. Likeliest senaryosu, IIS Express kullanarak yerel olarak test ederken sorunu görmemelidir, ancak Web sitenizi bir barındırma web sitesine dağıttığınızda bu sorunla karşılaşırsınız.
> 
> **Geçici çözüm**
> 
> - Sunucu bilgisayar üzerinde denetiminiz varsa, sunucu bilgisayarda, [belırlı ııs 7,0 veya ııs 7,5 işleyicilerinin, URL 'lerin noktayla bitmeyen istekleri işlemesini sağlayan bir güncelleştirmede](https://support.microsoft.com/kb/980368)açıklanan güncelleştirmeyi yükleyebilirsiniz.
> - Sunucu bilgisayarı üzerinde denetiminiz yoksa (örneğin, bir barındırma web sitesine dağıtıyorsanız), aşağıdakileri Web sitesinin *Web. config* dosyasına ekleyin:
> 
> 
> [!code-xml[Main](beta3/samples/sample7.xml)]

#### <a name="issue-using-web-application-project-or-aspnet-mvc-and-aspnet-web-pages-in-the-same-application"></a>Sorun: Web uygulaması projesi veya ASP.NET MVC ve ASP.NET Web sayfalarını aynı uygulamada kullanma

> Web uygulaması projesinde veya ASP.NET MVC uygulamasında ASP.NET Web sayfaları kullanıyorsanız, *Webpagehttpapplication* 'un bulunamadığını belirten bir hata görebilirsiniz.
> 
> **Geçici çözüm**  
> Bu hatayı alırsanız, uygulamanın türettiği temel sınıfı değiştirin. *Global. asax* dosyasında aşağıdaki satırı değiştirin:
> 
> [!code-csharp[Main](beta3/samples/sample8.cs)]
> 
> Bunun için:
> 
> [!code-csharp[Main](beta3/samples/sample9.cs)]
> 
> Bu efekt, Razor söz dizimi ile ASP.NET Web sayfalarının Beta 1 sürümü için tanıtılan bir değişikliği tersine çevirir.

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a>Sorun: SQL Server Compact yüklü olmayan bir bilgisayara uygulama dağıtma

> SQL Server Compact veritabanlarını içeren uygulamalar, SQL Server Compact yüklü olmayan bir bilgisayarda çalıştırılabilir. Microsoft WebMatrix Beta 3, bu ikili dosyaları sizin için otomatik olarak kopyalar ve uygun *Web. config* dosyası dönüşümlerini gerçekleştirir.
> 
> **Geçici çözüm** Bu dosyaları kopyalamanız ve *Web. config* dosyasının el ile değişiklikleri yapmanız gerekiyorsa, şunları yapın:
> 
> 1. Veritabanı altyapısı derlemelerini hedef bilgisayardaki uygulamanın *bin* klasörüne (ve alt klasörlerine) kopyalayın: 
> 
>     - *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **'i** *\Bin* 'e Kopyala
>     - *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* *  **'i** *\bin\x86* ' ya kopyalayın
>     - *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\* *  **'i** *\bin\amd64* dizinine kopyalayın
> 2. Web sitesinin kök klasöründe bir *Web. config* dosyası oluşturun veya açın. (WebMatrix Beta 3 ' te, **dosya türü seç** Iletişim kutusunda **Tümü** ' ne tıkladığınızda bu dosya türü kullanılabilir.)
> 3. Aşağıdaki öğeyi **&lt;configuration&gt;** öğesinin bir alt öğesi olarak ekleyin ( **&lt;system. Web&gt;** öğesinin içinde değil):
> 
> 
> [!code-xml[Main](beta3/samples/sample10.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a>Sorun: veritabanı ve WebGrid yardımcıları Visual Basic sürümünde Orta güvende çalışmıyor

> Visual Basic kullanıyorsanız ( *. vbhtml* dosyaları oluşturma), uygulama orta güveni kullanmak üzere ayarlandıysa `Database` ve `WebGrid` yardımcıları çalışmaz.
> 
> **Geçici çözüm**  
> Uygulamayı tam güven kullanacak şekilde geçici olarak ayarlayın.

<a id="Known_Issues_SQL_Server_Compact"></a>
### <a name="sql-server-compact"></a>SQL Server Compact

#### <a name="issue-encrypt-property-is-not-recognized"></a>Sorun: "Encrypt" özelliği tanınmıyor

> SQL Server Compact 4,0, `SqlCeConnection` sınıfının `Encrypt` özelliğini tanımıyor. Veritabanı dosyalarını şifrelemek için bu özelliği kullanmamalısınız. `Encrypt` özelliği SQL Server Compact 3,5 sürümünde kullanımdan kaldırılmıştır ve yalnızca geriye dönük uyumluluk için korunur. 
> 
> **Geçici çözüm**  
> SQL Server Compact 4,0 veritabanı dosyalarını şifrelemek için `SqlCeConnection` sınıfının `Encryption Mode` özelliğini kullanın. Aşağıdaki örnek, `Encryption Mode` özelliğini kullanarak nasıl şifreli SQL Server Compact 4,0 veritabanı oluşturulacağını gösterir:
> 
> [!code-csharp[Main](beta3/samples/sample11.cs)]
> 
> [!code-vb[Main](beta3/samples/sample12.vb)]
> 
> Mevcut bir SQL Server Compact 4,0 veritabanının şifreleme modunu değiştirmek için aşağıdakileri yapın:
> 
> [!code-csharp[Main](beta3/samples/sample13.cs)]
> 
> [!code-vb[Main](beta3/samples/sample14.vb)]
> 
> Şifrelenmemiş bir SQL Server Compact 4,0 veritabanını şifrelemek için aşağıdakileri yapın:
> 
> [!code-csharp[Main](beta3/samples/sample15.cs)]
> 
> [!code-vb[Main](beta3/samples/sample16.vb)]

#### <a name="issue-microsoft-visual-c-2008-runtime-libraries-are-required"></a>Sorun: Microsoft Visual C++ 2008 çalışma zamanı kitaplıkları gereklidir

> SQL Server Compact 4,0 ' in yerel dll 'Leri Microsoft Visual C++ 2008 çalışma zamanı kitaplıklarını (x86, IA64 ve x64), hizmet paketi 1 ' i gerektirir.
> 
> **Geçici çözüm**  
> .NET Framework 3,5 SP1 'i yükler. Bu, Visual C++ 2008 çalışma zamanı kitaplıkları SP1 de yüklenir. Kitaplıkları aşağıdaki konumdan indirebilirsiniz:   
>   
> [Microsoft Visual C++ 2008 Service Pack 1 yeniden DAĞITILABILIR paket ATL güvenlik güncelleştirmesi](https://go.microsoft.com/fwlink/?LinkId=194827)
> 
> [!NOTE]
> 2,0, 3,0 veya 4 *.NET Framework yükleme Visual* C++ 2008 çalışma zamanı kitaplıkları SP1 'i yüklemediğini unutmayın.

#### <a name="issue-if-sql-server-compact-is-installed-prior-to-installing-net-framework-on-the-computer-its-provider-invariant-name-is-not-registered-in-the-net-framework-machineconfig-file"></a>Sorun: bilgisayara .NET Framework yüklemeden önce SQL Server Compact yüklüyse, sağlayıcının sabit adı .NET Framework Machine. config dosyasında kayıtlı değil

> SQL Server Compact, SQL Server Compact .NET Framework gerektirdiğinden .NET Framework yüklü olmayan bir makineye yüklenebilir. SQL Server Compact yüklemeden önce .NET Framework sürüm 3,5 veya 4 yüklü değilse SQL Server Compact kurulum, *Machine. config* dosyasına sağlayıcının sabit adını kaydetmez. *Machine. config* dosyasında SQL Server Compact girişi kullanan herhangi bir uygulama başarısız olur. *Machine. config* dosyasındaki sabit ad kayıt girdisi aşağıdaki örneğe benzer şekilde görünür:
> 
> [!code-xml[Main](beta3/samples/sample17.xml)]
> 
> **Geçici çözüm**  
> SQL Server Compact 4,0 CTP1 'yi kaldırın. Aşağıdaki konumdan .NET Framework tam sürümlerini indirip yükleyin:
> 
> [Microsoft .NET Framework 3,5 Service Pack 1 (tam paket)](https://go.microsoft.com/fwlink/?LinkId=194828)  
> [Microsoft .NET Framework 4,0 sürümü (tam paket)](https://www.microsoft.com/downloads/details.aspx?FamilyID=9cfb2d51-5ff4-4491-b0e5-b386f32c0992&amp;displaylang=en)
> 
> [SQL Server Compact 4,0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en)yeniden yükleyin.

<a id="Known_Issues_Installing_Applications"></a>

### <a name="installing-applications"></a>Uygulamaları yükleme

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a>Sorun: kullanıcının Belgelerim klasörü bir ağ paylaşımında yeniden yönlendiriliyorsa, uygulamanın yüklenmesi uzun zaman alabilir

> **Geçici çözüm**  
> Yok. Uygulamanın yüklenmesi biraz zaman alabilir, ancak doğru şekilde yüklenir.

<a id="Known_Issues_Publishing_Applications"></a>

### <a name="publishing-applications"></a>Uygulamaları yayımlama

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a>Sorun: "hedef URL" alanı http://veya https://ön eki değilse, site yayımlamadan sonra çalışmayabilir

> **Yayımlama ayarları** iletişim kutusunda, hedef URL `http://` veya `https://`ile başlamadıysanız, site dağıtımdan sonra çalışmayabilir.
> 
> **Geçici çözüm**  
> Bir siteyi yayımlamadan önce, **yayınlama ayarları** iletişim KUTUSUNDAKI hedef URL 'nin `http://` veya `https://`ile başlayacağını doğrulayın.

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a>Sorun: bir MySQL veritabanının yayımlanması "veritabanı yayımlanamadı. Uzak veritabanı betiği çalıştıramadığı takdirde bu durum oluşabilir. "

> Hata çeşitli nedenlerden kaynaklanabilir. Bu hatayı görebileceğiniz bir nedeni, veritabanı betiğinin tek tırnak karakteri (') içermesi ve hedef MySQL veritabanının varsayılan karakter kümesinin UTF-8 ' e olmaması olabilir.
> 
> **Geçici çözüm**  
> Uzak MySQL veritabanı için varsayılan karakter kümesini UTF-8 olarak ayarlayın.

<a id="Known_Issues_Other_Issues"></a>

### <a name="other-issues"></a>Diğer Sorunlar

#### <a name="issue-searchfilter-does-not-work-in-reports-for-group-by-issue-type"></a>Sorun: arama/filtreleme, gruplandırma ölçütü: sorun türü raporlarında çalışmıyor

> Bir site için rapor çalıştırdığınızda, *URL 'ye göre filtrele* kutusuna metin girip *Ara*' yı tıklatırsanız, hiçbir şey olmaz. Bunun nedeni, raporun eyalet *ölçütü* , varsayılan değer olan durum *türü*olarak ayarlandığı sürece bu denetim işlevsel değildir.
> 
> **Geçici çözüm** Şerit 'in *Gruplandırma ölçütü* sekmesinde, GIRDILERI kaynak URL 'lerine göre gruplandırmak için *URL* ' ye tıklayın. Bu durumda, girdileri filtrelemek için metin kutusu ve düğme işlevseldir.

#### <a name="issue-wcf-applications-fail-to-run-with-iis-express"></a>Sorun: WCF uygulamaları IIS Express ile çalıştırılamaz

> Bir WCF uygulamasına göz atmak aşağıdakine benzer bir hata ile sonuçlanır:
> 
> *Dosya veya derleme ' Microsoft. Web. Administration, version = 7.0.0.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35 ' veya bağımlılıklarından biri yüklenemedi. Sistem belirtilen dosyayı bulamıyor.*
> 
> Bu durum IIS Express beta sürümü varsayılan olarak WCF 'yi desteklemediğinden oluşur.
> 
> **Geçici çözüm** Aşağıdaki geçici çözümlerden birini kullanın (geçici çözüm #2 Microsoft Windows Vista veya üstünü gerektirir):
> 
> 
> 1. WebMatrix yükleme konumundan *Microsoft. Web. dll* ve *Microsoft. Web. Administration. dll* derlemelerini WCF uygulamasının *bin* dizinine kopyalayın. Varsayılan olarak, WebMatrix, sistemin *Program Files* klasörü altındaki *Microsoft WebMatrix* alt klasörüne yüklenir.
> 2. Microsoft Windows Vista veya üzeri sürümlerde, *bin* dizinindeki derlemeler için aşağıdaki komutları kullanarak bir oluşturmaksızın oluşturun. (Bu yaklaşım, derlemelerin bir kopyasını oluşturmadığından faydalanır.)
> 
>     [!code-console[Main](beta3/samples/sample18.cmd)]
> 3. GAC 'de iki derlemeyi yükler. Yükseltilmiş bir komut isteminden aşağıdaki komutları çalıştırın:
> 
>     [!code-console[Main](beta3/samples/sample19.cmd)]

#### <a name="issue-webmatrix-beta-3-is-unable-to-perform-certain-tasks-that-require-elevation"></a>Sorun: WebMatrix Beta 3, yükseltme gerektiren belirli görevleri gerçekleştiremiyor

> WebMatrix Beta 3, aşağıdaki durumlarda ek bileşenler yükleme gibi yükseltme gerektiren belirli görevleri gerçekleştiremiyor:
> 
> - Windows Vista veya Windows 7 ' de, yönetici ayrıcalıklarına sahip olmayan bir hesapla oturum açarsınız ve Kullanıcı hesabı denetimi (UAC) devre dışı bırakılır.
> - Microsoft Windows XP veya Microsoft Windows Server 2003 kullanıyorsunuz.
> 
> **Geçici çözüm**  
> WebMatrix Beta 3 ' teki çoğu görev yönetici izni gerektirmez. Bu işlemler için, işlemi yönetici olarak gerçekleştirebilir veya aşağıdaki adımları izleyebilirsiniz:
> 
> - Windows Vista veya Windows 7 ' de UAC 'yi etkinleştirin.
> - Windows XP 'de, kullanıcıyı Administrators güvenlik grubuna ekleyin.

#### <a name="issue-site-from-web-gallery-is-disabled"></a>Sorun: "Web galerisinden site" devre dışı

> Web Platformu Yükleyicisi 3,0 yüklü değilse, **Web galerisinden site** seçeneği devre dışıdır.
> 
> **Geçici çözüm**  
> [3,0 Microsoft Web Platformu Yükleyicisi](https://go.microsoft.com/fwlink/?LinkID=194638)'yi yükler.

#### <a name="issue-on-windows-server-2003-iis-express-does-not-start-for-a-non-administrative-user"></a>Sorun: Windows Server 2003 ' de IIS Express yönetici olmayan bir kullanıcı için başlamıyor

> Windows Server 2003 ' de, bir sayfa başlattığınızda veya IIS Express başlattığınızda IIS Express başlamaz. Web sayfaları için, uygulamanın yönetici olmayan bir kullanıcı tarafından başlatıldığını belirten bir hata görüntülenir.
> 
> **Geçici çözüm**  
> WebMatrix Beta 3 ' ü Yönetici Kullanıcı olarak başlatın. Daha fazla ayrıntı için aşağıdaki Bilgi Bankası makalesine bakın:  
>   
> [Yönetici olmayan bir kullanıcı tarafından başlatılan bir uygulama, uygulamanın Windows Vista, Windows Server 2003 veya Windows XP 'de çalıştığı bilgisayarın HTTP trafiğini dinleyemeyen bir uygulamadır.](https://support.microsoft.com/kb/939786)

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a>Sorun: Google Chrome bir çalıştır seçeneği olarak kullanılamıyor

> Google Chrome, **giriş** sekmesinde **Çalıştır** altında bulunan tarayıcılar listesinde gösterilmez.
> 
> **Geçici çözüm**  
> Google Chrome 'un bazı sürümleri, Windows 'daki varsayılan programlar özelliği ile kendilerini doğru bir şekilde kaydetmez. Geçici bir çözüm olarak, Google Chrome 'u başlatın, *Google Chrome ' ı Özelleştir ve denetle* menüsüne tıklayın, *Seçenekler*' e ve ardından *Google Chrome varsayılan tarayıcımı oluştur*' a tıklayın.

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a>Sorun: "yabancı anahtar" iletişim kutusu birincil anahtar girmeye izin vermiyor

> **Yabancı anahtar** iletişim kutusu birincil anahtar tablosundan birincil anahtar adını girmenize izin vermez.
> 
> **Geçici çözüm**  
> Bu bilerek yapılır. Birincil anahtar tablosundan birincil anahtar adını girmeniz gerekmez.

#### <a name="issue-the-relationships-button-is-disabled"></a>Sorun: "Ilişkiler" düğmesi devre dışı

> **Veritabanları** çalışma alanındaki **tablo** sekmesinin altındaki **ilişkiler** düğmesi SQL Server Compact veritabanları için devre dışıdır.
> 
> **Geçici çözüm**  
> Yok. SQL Server Compact, tablolar arasındaki ilişkileri desteklemez.

#### <a name="issue-parameterized-sql-queries-throw-exceptions"></a>Sorun: parametreli SQL sorguları özel durumlar oluşturur

> SQL Server Compact 4,0 ' de, parametreli sorgularda parametreler için `SqlDbType` veya `DbType` gibi bir veri türü belirtmezseniz, sorgu çalıştırıldığında bir özel durum oluşturulur.
> 
> **Geçici çözüm**  
> `SqlDbType` veya `DbType`gibi parametreler için veri türünü açık olarak ayarlayın. BLOB veri türleri (`image` ve `ntext`) söz konusu olduğunda bu kritik öneme sahiptir. Aşağıdaki gibi bir kod kullanın:
> 
> [!code-sql[Main](beta3/samples/sample20.sql)]
> 
> [!code-vb[Main](beta3/samples/sample21.vb)]

<a id="More_Info"></a>

## <a name="for-more-information"></a>Daha Fazla Bilgi İçin

WebMatrix Beta 3 hakkında daha fazla bilgi için, aşağıdaki Web sitelerine bakın:

- [IIS.net](http://iis.net/)
- [ASP.NET](https://asp.net/webmatrix)
- [Microsoft.com/web](https://www.microsoft.com/web)

---

© 2010 Microsoft Corporation. Tüm hakları saklıdır. [Kullanım koşulları](https://msdn.microsoft.cos/cc300389.aspx).
