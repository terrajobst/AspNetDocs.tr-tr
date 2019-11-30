---
uid: mvc/mvc3
title: ASP.NET MVC 3
author: rick-anderson
description: (Nisan 2011 Araçlar güncelleştirmesi dahildir) ASP.NET MVC 3, iyi belirlenen tasarım modelini kullanarak ölçeklenebilir, standartlara dayalı Web uygulamaları oluşturmaya yönelik bir çerçevedir...
ms.author: riande
ms.date: 10/05/2010
ms.assetid: dddc8812-a0bc-49f9-aafb-caf2064c2b8c
msc.legacyurl: /mvc/mvc3
msc.type: content
ms.openlocfilehash: 421a06c89d4dbcb05d4080033813cc6558b7c698
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74586746"
---
# <a name="aspnet-mvc-3"></a>ASP.NET MVC 3

> *(Nisan 2011 Araçlar güncelleştirmesi dahildir)*
> 
> ASP.NET MVC 3, iyi kurulan tasarım düzenlerini ve ASP.NET ve .NET Framework gücünü kullanarak ölçeklenebilir, standartlara dayalı Web uygulamaları oluşturmaya yönelik bir çerçevedir.
> 
> ASP.NET MVC 2 ile yan yana yüklenir, bu nedenle hemen kullanmaya başlayın!
> 
> [Yükleyiciyi buraya](https://go.microsoft.com/fwlink/?LinkID=208140) indirin

## <a name="top-features"></a>Popüler Özellikler

- NuGet üzerinden Genişletilebilir tümleşik yapı Iskelesi sistemi
- HTML 5 etkin proje şablonları
- Yeni Razor Görünüm altyapısı dahil ifade eden görünümler
- Bağımlılık ekleme ve genel eylem filtreleriyle güçlü kancalar
- Unobtrusive JavaScript, jQuery doğrulaması ve JSON bağlamasıyla zengin JavaScript desteği
- *[Aşağıdaki](#overview) tam özellik listesini okuyun*

## <a name="top-links"></a>Üst bağlantılar

ASP.NET MVC 3 sürümündeki yenilikler

- PHIL Haack: [ASP.NET MVC 3 Yayınlandı](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)
- Scott Hanselman: [ASP.net mvc3, WebMatrix, NuGet, IIS Express ve Orchard yayımlandı-bağlamdaki Microsoft Ocak Web yayını](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)
- Scott Guthrie: [ASP.NET MVC 3, IIS Express, SQL CE 4, Web grubu çerçevesi, Orchard, WebMatrix 'In duyurusu](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)
- [ASP.NET MVC 3 için sürüm notları](../whitepapers/mvc3-release-notes.md)

Yükleme ve yardım

- Web platformu yükleyicisini kullanarak ASP.NET MVC 3 ' ü yükleme [(önerilir)](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)
- [Yükleyici yürütülebilirini](https://go.microsoft.com/fwlink/?LinkID=208140) kullanarak ASP.NET MVC 3 ' ü yükleme
- [Visual Studio 11 Geliştirici Önizlemesi için ASP.NET MVC 3](https://go.microsoft.com/fwlink/?LinkID=208140) ' ü yükler
- [ASP.NET MVC 3 öğreticisine giriş](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) okuyun
- [Forumlarda](https://forums.asp.net/1146.aspx) yardım alın ve ASP.NET MVC 3 ' ü tartışın

<a id="overview"></a>
## <a name="aspnet-mvc-3-overview"></a>ASP.NET MVC 3 genel bakış

ASP.NET MVC 3, kodunuzu basitleştirecek ve daha derin genişletilebilirlik sağlayan harika özellikler ekleyerek ASP.NET MVC 1 ve 2 üzerinde derlemeler. Bu konuda, bu yayında yer alan yeni özelliklerin birçoğu aşağıdaki bölümlere göre düzenlenmiş bir genel bakış sunulmaktadır:

- [MvcScaffold tümleştirmesiyle Genişletilebilir yapı Iskelesi](#BM_MvcScaffolding)
- [HTML 5 etkin proje şablonları](#BM_HTML5)
- [Razor Görünüm altyapısı](#BM_TheRazorViewEngine)
- [Birden çok görünüm altyapısı desteği](#BM_Support_for_Multiple_View_Engines)
- [Denetleyici geliştirmeleri](#BM_Controller_Improvements)
- [JavaScript ve Ajax](#BM_JavaScript_and_Ajax_Improvements)
- [Model doğrulama geliştirmeleri](#BM_Model_Validation_Improvements)
- [Bağımlılık ekleme geliştirmeleri](#BM_Dependency_Injection_Improvements)
- [Diğer yeni özellikler](#BM_Other_New_Features)

<a id="BM_MvcScaffolding"></a>

## <a name="extensible-scaffolding-with-mvcscaffold-integration"></a>MvcScaffold tümleştirmesiyle Genişletilebilir yapı Iskelesi

Yeni yapı Iskelesi sistemi, çerçeveye tamamen yeni başladıysanız ve ne yaptığınızı biliyorsanız ortak geliştirme görevlerini otomatikleştirmek için, üretken bir şekilde kullanmayı ve başlatmayı kolaylaştırır.

Bu, **Mvcscafkatlama**adlı yeni NuGet *scafkatlama* paketi tarafından desteklenir. "Scafkatlama" terimi birçok yazılım teknolojisi tarafından, "sizin düzenleyebileceğiniz ve özelleştirebileceğiniz, yazılımınızın temel bir ana hattını hızla oluşturmak" amacıyla kullanılır. ASP.NET MVC için oluşturmakta olduğumuz yapı iskelesi, çeşitli senaryolarda önemli ölçüde faydalıdır:

- **ASP.NET MVC 'yi ilk kez öğreniyor olmanız**nedeniyle, daha sonra gereksinimlerinize göre düzenleyip uyarlayabileceğiniz bazı yararlı, çalışan kodlar elde etmenizi sağlayan bir daha hızlı bir yol sağlar. Bu, size boş bir sayfaya bakmaktan ve nereden başlayabileceğiniz konusunda fikir sahibi olmanın bir bölümünü kaydeder!
- **ASP.NET MVC 'nin iyi olduğunu biliyorsanız ve** bir nesne ilişkisel Eşleyici, bir görünüm altyapısı, bir test kitaplığı vb. gibi yeni eklenti teknolojisinden de keşfetmeye çalışıyorsanız, bu teknolojinin Oluşturucusu kendisi için de bir yapı iskelesi paketi de oluşturmuş olabilir.
- Çalışmanız, test armatürleri, dağıtım betikleri veya ihtiyacınız olan herhangi bir başka şey için çıkış yapan özel platformları oluşturabileceğiniz için, **benzer sınıfları veya bazı bir sıralama dosyasını sürekli olarak oluşturma işlemi**içeriyorsa. Takımınızdaki herkes, özel scaffolders da kullanabilir.

Mvcscafkatlama içindeki diğer özellikler şunlardır:

- Ve VB C# projeleri için destek
- Razor ve ASPX görünüm motorları için destek
- ASP.NET MVC alanlarında yapı iskelesi destekler ve özel görünüm düzenlerini/asıllarını kullanarak
- T4 şablonlarını düzenleyerek çıktıyı kolay bir şekilde özelleştirebilirsiniz
- Özel PowerShell mantığını ve özel T4 şablonlarını kullanarak tamamen yeni platformları ekleyebilirsiniz. Bunlar (ve verdiğiniz özel parametreler) konsol sekmesi tamamlama listesinde otomatik olarak görünür.
- Farklı teknolojiler için ek platformları içeren NuGet paketleri alabilirsiniz (örneğin, şimdilik LINQ to SQL bir kavram kanıtı vardır) ve bunları birlikte karıştırarak ve onlarla eşleştirebilirsiniz

ASP.NET MVC 3 araçları güncelleştirmesi, bu yapı iskelesi sistemi için harika Visual Studio desteği içerir, örneğin:

- Denetleyici Ekle Iletişim kutusu artık oluşturma, okuma, güncelleştirme ve silme denetleyicisi eylemlerinin ve ilgili görünümlerin tam otomatik yapı iskelesi desteklemektedir. Varsayılan olarak, bu yapı Code First EF kullanarak veri erişim kodunu yasaklıyor.
- Denetleyici Ekle Iletişim kutusu, *Mvcscafkatlama*gibi NuGet paketleri aracılığıyla *Genişletilebilir yapı iskelesi* destekler. Bu, özel dolandırıcıların iletişim kutusuna takmayı sağlar ve bu sayede Nhazırda bekleme veya hatta JET gibi diğer veri erişimi teknolojileri için daha fazla

ASP.NET MVC 3 ' teki yapı Iskelesi hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- Steve Sanderson 'in aşağıdakiler de dahil olmak üzere post serisi: 

    1. [Giriş: Mvcscafkatlama paketiyle ASP.NET MVC 3 projenizi dolandırın](http://blog.stevensanderson.com/2011/01/13/scaffold-your-aspnet-mvc-3-project-with-the-mvcscaffolding-package/)
    2. [Standart kullanım: tipik kullanım örnekleri ve seçenekleri](http://blog.stevensanderson.com/2011/01/13/mvcscaffolding-standard-usage/)
    3. [Bire çok Ilişkileri](http://blog.stevensanderson.com/2011/01/28/mvcscaffolding-one-to-many-relationships/)
    4. [Yapı iskelesi eylemleri ve birim testleri](http://blog.stevensanderson.com/2011/03/28/scaffolding-actions-and-unit-tests-with-mvcscaffolding/)
    5. [T4 şablonlarını geçersiz kılma](http://blog.stevensanderson.com/2011/04/06/mvcscaffolding-overriding-the-t4-templates/)
    6. [Bu Gönderi: özel platformları oluşturma](http://blog.stevensanderson.com/2011/04/07/mvcscaffolding-creating-custom-scaffolders/)
- Scott Hanselman 'ın PDC 2010 oturumundan gönderisini [Microsoft "adlandırılmamış Web sevgi paketi" ile bir blog oluşturma](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)
- [MVC 3 sürüm notları](../whitepapers/mvc3-release-notes.md)

<a id="BM_HTML5"></a>

## <a name="html-5-project-templates"></a>HTML 5 proje şablonları

Yeni proje iletişim kutusu, proje şablonlarının HTML 5 sürümlerini etkinleştir onay kutusunu içerir. Bu şablonlar, alt düzey tarayıcılarda HTML 5 ve CSS 3 için uyumluluk desteği sağlamak üzere Modernizr 1,7 ' den faydalanır.

<a id="BM_TheRazorViewEngine"></a>

## <a name="the-razor-view-engine"></a>Razor Görünüm altyapısı

ASP.NET MVC 3, aşağıdaki avantajları sunan Razor adlı yeni bir görünüm altyapısıyla birlikte gelir:

- Razor söz dizimi, en az sayıda tuş vuruşu gerektiren temiz ve kısa bir sayıdır.
- Razor, ve Visual Basic gibi C# var olan dillere bağlı olduğundan, kısmen öğrenilmesi kolaydır.
- Visual Studio, Razor söz dizimi için IntelliSense ve kod renklendirme içerir.
- Razor görünümleri, uygulamayı çalıştırmanız veya bir Web sunucusu başlatmanız gerekmeden birim test edilebilir.

Bazı yeni Razor özellikleri şunları içerir:

- görünüme geçirmekte olan türü belirtmek için `@model` sözdizimi.
- `@* *@` açıklama sözdizimi.
- Tüm site için varsayılan değerleri (örneğin `layoutpage`) belirtme özelliği.
- HTML kodlaması olmadan metin görüntülemek için `Html.Raw` yöntemi.
- Birden çok görünüm arasında kod paylaşma desteği ( *\_viewstart. cshtml* veya *\_viewstart. vbhtml* dosyaları).

Razor, aşağıdakiler gibi yeni HTML Yardımcıları da içerir:

- `Chart`. ASP.NET 4 ' te grafik denetimiyle aynı özellikleri sunan bir grafik oluşturur.
- `WebGrid`. Sayfalama ve sıralama işlevselliğiyle birlikte bir veri kılavuzunu işler.
- `Crypto`. Doğru şekilde sallanmış ve karma hale getirilmiş parolalar oluşturmak için karma algoritmaları kullanır.
- `WebImage`. Bir görüntü oluşturur.
- `WebMail`. Bir e-posta iletisi gönderir.

Razor hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Scott Guthrie 'nin blog gönderisi Razor tanıtımı](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)
- [Scott Guthrie 'nin blog gönderisi @model anahtar sözcüğünü tanıtma](https://weblogs.asp.net/scottgu/archive/2010/10/19/asp-net-mvc-3-new-model-directive-support-in-razor.aspx)
- [Scott Guthrie 'nin, Razor düzenlerini tanıtma blog gönderisi](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)
- [Razor API hızlı başvurusu](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)
- [MVC 3 sürüm notları](../whitepapers/mvc3-release-notes.md)

<a id="BM_Support_for_Multiple_View_Engines"></a>

## <a name="support-for-multiple-view-engines"></a>Birden çok görünüm altyapısı desteği

ASP.NET MVC 3 ' teki **Görünüm Ekle** iletişim kutusu, birlikte çalışmak istediğiniz görünüm altyapısını seçmenizi sağlar ve **Yeni proje** iletişim kutusu, bir proje için varsayılan görünüm altyapısını belirtmenize olanak tanır. Web Forms View Engine (ASPX), Razor veya [Spark](http://sparkviewengine.com/), [NHaml](https://code.google.com/p/nhaml/)veya [ndocgo](http://ndjango.org/)gibi bir açık kaynaklı görünüm altyapısını seçebilirsiniz.

<a id="BM_Controller_Improvements"></a>

## <a name="controller-improvements"></a>Denetleyici geliştirmeleri

### <a name="global-action-filters"></a>Genel eylem filtreleri

Bazen bir eylem yöntemi çalıştırılmadan önce ya da bir eylem yöntemi çalıştıktan sonra mantığı gerçekleştirmek isteyebilirsiniz. Bunu desteklemek için, ASP.NET MVC 2 tarafından sunulan eylem filtrelerini izleyin. Eylem filtreleri, belirli denetleyici eylem yöntemlerine eylem öncesi ve eylem sonrası davranışı eklemek için bildirime dayalı bir yol sağlayan özel özniteliklerdir. Ancak bazı durumlarda, tüm eylem yöntemleri için geçerli olan eylem öncesi veya eylem sonrası davranışı belirtmek isteyebilirsiniz. MVC 3, genel filtreleri `GlobalFilters` koleksiyonuna ekleyerek belirtmenize olanak tanır. Genel eylem filtreleri hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Scott Guthrie 'nin Web günlüğü MVC 3 Preview](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)
- [ASP.NET MVC 'de filtreleme](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)

### <a name="new-viewbag-property"></a>Yeni "ViewBag" özelliği

MVC 2 denetleyicileri, verileri bir görünüm şablonuna, geç bağlanan bir sözlük API 'SI kullanarak geçirmenize olanak sağlayan bir `ViewData` özelliğini destekler. MVC 3 ' te, aynı amaca ulaşmak için `ViewBag` özelliği ile biraz daha basit bir sözdizimi de kullanabilirsiniz. Örneğin, `ViewData["Message"]="text"`yazmak yerine `ViewBag.Message="text"`yazabilirsiniz. `ViewBag` özelliğini kullanmak için kesin olarak belirlenmiş bir sınıf tanımlamanız gerekmez. Dinamik bir özellik olduğundan, bunun yerine yalnızca özellikleri alabilir veya ayarlayabilirsiniz ve çalışma zamanında dinamik olarak çözümlenir. Dahili olarak, `ViewBag` Özellikler `ViewData` sözlüğünde ad/değer çiftleri olarak depolanır. (Note: MVC 3 ' ün çoğu yayın öncesi sürümünde, `ViewBag` özelliği `ViewModel` özelliği olarak adlandırılmıştı.)

### <a name="new-actionresult-types"></a>Yeni "ActionResult" türleri

Aşağıdaki `ActionResult` türleri ve ilgili yardımcı yöntemler MVC 3 ' te yenidir veya geliştirilmiştir:

- [Httpnotfoundresult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx). İstemciye bir 404 HTTP durum kodu döndürür.
- [RedirectResult](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx). Boole parametresine bağlı olarak geçici yeniden yönlendirme (HTTP 302 durum kodu) veya kalıcı yeniden yönlendirme (HTTP 301 durum kodu) döndürür. Bu değişiklik ile birlikte, [Denetleyici](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx) sınıfı artık kalıcı yeniden yönlendirmeler gerçekleştirmek için üç yönteme sahiptir: `RedirectPermanent`, `RedirectToRoutePermanent`ve `RedirectToActionPermanent`. Bu yöntemler, `Permanent` özelliği `true`olarak ayarlanan bir `RedirectResult` örneğini döndürür.
- [Httpstatuscoderesult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx). Kullanıcı tarafından belirtilen HTTP durum kodunu döndürür.

<a id="BM_JavaScript_and_Ajax_Improvements"></a>

## <a name="javascript-and-ajax-improvements"></a>JavaScript ve Ajax geliştirmeleri

Varsayılan olarak, MVC 3 ' teki Ajax ve doğrulama yardımcıları unobtrusive JavaScript yaklaşımını kullanır. Unobtrusive JavaScript, ekleme satır içi JavaScript 'ı HTML olarak önler. Bu, HTML 'nizi daha küçük ve daha az karışık hale getirir ve JavaScript kitaplıklarını değiştirmeyi veya özelleştirmeyi kolaylaştırır. MVC 3 ' teki doğrulama yardımcıları, varsayılan olarak `jQueryValidate` eklentisini de kullanır. MVC 2 davranışını istiyorsanız, *Web. config* dosya ayarını kullanarak unobtrusive JavaScript 'i devre dışı bırakabilirsiniz. JavaScript ve Ajax iyileştirmeleri hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Vimüpit sitede JavaScript 'i kaldırmak için temel giriş](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript)
- [Atacan Solson 's unobtrusive JavaScript gönderisi](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-ajax.html)
- [Atacan Solson 'un unobtrusive JavaScript doğrulama gönderisi](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)
- [Razor ve unobtrusive JavaScript Ile MVC 3 uygulaması oluşturma](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md) (ASP.net sitesinde öğretici)
- [MVC 3 sürüm notları](../whitepapers/mvc3-release-notes.md)

### <a name="client-side-validation-enabled-by-default"></a>Varsayılan olarak etkin istemci tarafı doğrulaması

MVC 'nin önceki sürümlerinde, istemci tarafı doğrulamayı etkinleştirmek için bir görünümden `Html.EnableClientValidation` yöntemi açıkça çağırmanız gerekir. MVC 3 ' te, istemci tarafı doğrulaması varsayılan olarak etkinleştirildiğinden bu artık gerekli değildir. ( *Web. config* dosyasındaki bir ayarı kullanarak bunu devre dışı bırakabilirsiniz.)

İstemci tarafı doğrulamanın çalışması için, sitenizde uygun jQuery ve jQuery doğrulama kitaplıklarına başvurmanız gerekir. Bu kitaplıkları kendi sunucunuzda barındırabilir veya Microsoft veya Google 'dan CDNs gibi bir Content Delivery Network (CDN) ile başvurabilirsiniz.

### <a name="remote-validator"></a>Uzak Doğrulayıcı

ASP.NET MVC 3, jQuery doğrulama eklentisinin uzak Doğrulayıcı desteğinden yararlanmanızı sağlayan yeni [Remoteattribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx) sınıfını destekler. Bu, istemci tarafı doğrulama kitaplığının yalnızca sunucu tarafında yapılabilen doğrulama mantığını gerçekleştirmek üzere sunucuda tanımladığınız özel bir yöntemi otomatik olarak çağırmasını sağlar.

Aşağıdaki örnekte `Remote` özniteliği, istemci doğrulamasının `UserName` alanını doğrulamak için `UsersController` sınıfında `UserNameAvailable` adlı bir eylemi çağıracağını belirtir.

[!code-csharp[Main](mvc3/samples/sample1.cs)]

Aşağıdaki örnek, ilgili denetleyiciyi gösterir.

[!code-csharp[Main](mvc3/samples/sample2.cs)]

`Remote` özniteliğini kullanma hakkında daha fazla bilgi için, MSDN Kitaplığı 'nda [nasıl yapılır: ASP.NET MVC 'de uzaktan doğrulamayı uygulama](https://msdn.microsoft.com/library/gg508808(VS.98).aspx) bölümüne bakın.

### <a name="json-binding-support"></a>JSON bağlama desteği

ASP.NET MVC 3, eylem yöntemlerinin JSON kodlu verileri almasına ve model olarak bunu eylem-yöntem parametrelerine bağlamasını sağlayan yerleşik JSON bağlama desteğini içerir. Bu özellik, istemci şablonları ve veri bağlama dahil olmak üzere senaryolar için yararlıdır. (İstemci şablonları, istemci üzerinde yürütülen şablonları kullanarak tek bir veri öğesini veya veri öğeleri kümesini biçimlendirebilir ve görüntülemenizi sağlar.) MVC 3, JSON verilerini gönderen ve alan sunucudaki eylem yöntemleriyle istemci şablonlarına kolayca bağlanmanızı sağlar. JSON bağlama desteği hakkında daha fazla bilgi için [Scott Guthrie 'nın MVC 3 Preview blog gönderisinin](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx) **JavaScript ve Ajax iyileştirmeleri** bölümüne bakın.

<a id="BM_Model_Validation_Improvements"></a>

## <a name="model-validation-improvements"></a>Model doğrulama geliştirmeleri

### <a name="dataannotations-metadata-attributes"></a>"Dataaçıklamalarda" meta veri öznitelikleri

ASP.NET MVC 3, `DisplayAttribute`gibi `DataAnnotations` meta veri özniteliklerini destekler.

### <a name="validationattribute-class"></a>"ValidationAttribute" sınıfı

`ValidationAttribute` sınıfı, geçerli doğrulama bağlamı hakkında, hangi nesnenin Doğrulanmakta olduğu gibi daha fazla bilgi sağlayan yeni bir `IsValid` aşırı yüklemesini desteklemek için .NET Framework 4 ' te geliştirilmiştir. Bu, geçerli değeri modelin başka bir özelliğine göre doğrulayabileceğiniz daha zengin senaryolara izin vermez. Örneğin, yeni `CompareAttribute` özniteliği bir modelin iki özelliğinin değerlerini karşılaştırmanıza imkan tanır. Aşağıdaki örnekte, `ComparePassword` özelliğinin geçerli olması için `Password` alanla eşleşmesi gerekir.

[!code-csharp[Main](mvc3/samples/sample3.cs)]

### <a name="validation-interfaces"></a>Doğrulama arabirimleri

[IValidatableObject](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx) arabirimi model düzeyinde doğrulama gerçekleştirmenize olanak sağlar ve genel modelin durumuna özgü veya modeldeki iki özellik arasında doğrulama hata iletileri sağlamanıza olanak sağlar. MVC 3 artık model bağlama sırasında `IValidatableObject` arabiriminden hata alıyor ve yerleşik HTML form yardımcıları kullanarak bir görünüm içindeki etkilenen alanları otomatik olarak işaretler veya vurgular.

[Ilientvalidatable](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx) arabirimi, doğrulayıcının istemci doğrulaması için desteğe sahip olup olmadığına BAKıLMAKSıZıN ASP.NET MVC 'nin çalışma zamanında bulmasını sağlar. Bu arabirim, çeşitli doğrulama çerçeveleri ile tümleştirilebilecek şekilde tasarlanmıştır.

Doğrulama arabirimleri hakkında daha fazla bilgi için [Scott Guthrie 'nın MVC 3 Preview blog gönderisinin](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx) **model doğrulama iyileştirmeleri** bölümüne bakın. (Ancak, blogdaki "ıvalidateobject" başvurusunun "IValidatableObject" olması gerektiğini unutmayın.)

<a id="BM_Dependency_Injection_Improvements"></a>

## <a name="dependency-injection-improvements"></a>Bağımlılık ekleme geliştirmeleri

ASP.NET MVC 3, bağımlılık ekleme (dı) uygulamak ve bağımlılık ekleme veya denetim (ıOC) kapsayıcıları ile tümleştirme için daha iyi destek sağlar. Şu alanlara dı desteği eklenmiştir:

- Denetleyiciler (kayıt ve ekleme Controller Factory, ekleme denetleyicileri).
- Görünümler (kayıt ve ekleme görünüm motorları, ekleme bağımlılıklar görüntüleme sayfalarına).
- Eylem filtreleri (bulma ve ekleme filtreleri).
- Model ciltleri (kayıt ve ekleme).
- Model doğrulama sağlayıcıları (kayıt ve ekleme).
- Model meta veri sağlayıcıları (kayıt ve ekleme).
- Değer sağlayıcıları (kayıt ve ekleme).

MVC 3, [ortak hizmet bulucu](https://github.com/unitycontainer/commonservicelocator) kitaplığını ve bu kitaplığın `IServiceLocator` arabirimini destekleyen tüm dı kapsayıcısını destekler. Ayrıca, dı çerçevelerini tümleştirmeyi kolaylaştıran yeni bir `IDependencyResolver` arabirimini destekler.

MVC 3 ' teki DI hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Atacan Solson 'ın hizmet konumundaki blog gönderilerinin serisi](http://bradwilson.typepad.com/blog/2010/07/service-location-pt1-introduction.html)
- [MVC 3 sürüm notları](../whitepapers/mvc3-release-notes.md)

<a id="BM_Other_New_Features"></a>

## <a name="other-new-features"></a>Diğer yeni özellikler

### <a name="nuget-integration"></a>NuGet tümleştirmesi

ASP.NET MVC 3, kurulumunun bir parçası olarak NuGet 'yi otomatik olarak yükleyip etkinleştirmektedir. NuGet, projelerinizde .NET kitaplıklarını ve araçları bulmayı, yüklemeyi ve kullanmayı kolaylaştıran ücretsiz bir açık kaynaklı paket yöneticisidir. Tüm Visual Studio proje türleriyle (ASP.NET Web Forms ve ASP.NET MVC dahil) birlikte çalışmaktadır.

NuGet, açık kaynak projeleri (örneğin, moq, Nhazırda beklet, Neklemesine, StructureMap, NUnit, WINR, Rhinomokıs ve ELMAH gibi projeler) kullanan geliştiricilere, kitaplıklarını paketlemek ve çevrimiçi bir galeride kaydetmek için olanak sağlar. Daha sonra, paketi bulmak ve üzerinde çalıştıkları projelere yüklemek için bu kitaplıkların birini kullanmak isteyen .NET geliştiricileri daha kolay olur.

ASP.NET 3 Araçlar güncelleştirmesi sayesinde proje şablonları, önceden yüklenmiş olan JavaScript kitaplıklarını, NuGet aracılığıyla güncelleştirilebilir. Entity Framework Code First, bir NuGet paketi olarak da önceden yüklenir.

NuGet hakkında daha fazla bilgi için bkz. [NuGet belgeleri](https://docs.microsoft.com/nuget/).

### <a name="partial-page-output-caching"></a>Kısmi sayfa çıkışı önbelleğe alma

ASP.NET MVC, sürüm 1 ' den bu yana tam sayfa yanıtlarının çıkış önbelleğini destekliyordu. MVC 3 Ayrıca, bir yanıtın bölgelerini veya parçalarını kolayca önbelleğe almanıza olanak tanıyan kısmi sayfa çıkışı önbelleğe almayı da destekler. Önbelleğe alma hakkında daha fazla bilgi için [MVC 3 sürüm adayındaki Scott Guthrie 'nin blog gönderisine](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx) ve [MVC 3 sürüm notlarındaki](../whitepapers/mvc3-release-notes.md) **alt eylem çıktısı önbelleğe alma** **bölümüne bakın** .

### <a name="granular-control-over-request-validation"></a>Istek doğrulaması üzerinde ayrıntılı denetim

ASP.NET MVC, XSS ve HTML ekleme saldırılarına karşı korumaya otomatik olarak yardımcı olan yerleşik istek doğrulamaya sahiptir. Ancak bazen, kullanıcıların HTML içeriği (örneğin, blog girişlerinde veya CMS içeriğinde) göndermenize izin vermek gibi istek doğrulamasını açıkça devre dışı bırakmak isteyebilirsiniz. Artık model bağlama sırasında özellik başına temelinde istek doğrulamayı devre dışı bırakmak için modellere veya modellerdeki bir [Allowwhtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx) özniteliği ekleyebilirsiniz. İstek doğrulama hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Scott Guthrie 'nın MVC 3 sürüm Candidate 'teki blog gönderisine ait](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx) **unobtrusive JavaScript ve doğrulama** bölümü.
- [MVC 3 sürüm notları](../whitepapers/mvc3-release-notes.md)

### <a name="extensible-new-project-dialog-box"></a>Genişletilebilir "yeni proje" Iletişim kutusu

ASP.NET MVC 3 ' te, **Yeni proje** iletişim kutusuna proje şablonları, görünüm motorları ve birim testi proje çerçeveleri ekleyebilirsiniz.

### <a name="template-scaffolding-improvements"></a>Şablon yapı Iskelesi Iyileştirmeleri

ASP.NET MVC 3 yapı iskelesi şablonları, modellerdeki birincil anahtar özellikleri tanımlamayı ve bunları daha önceki MVC sürümleriyle uygun şekilde işlemeyi daha iyi bir şekilde işler. (Örneğin, yapı iskelesi şablonları artık birincil anahtarın düzenlenebilir form alanı olarak scaklesi olmadığından emin olur.)

Varsayılan olarak, oluşturma ve düzenleme yapı ve düzenleme artık `Html.TextBoxFor` Yardımcısı yerine `Html.EditorFor` Yardımcısı 'nı kullanır. Bu, **Görünüm Ekle** iletişim kutusu bir görünüm oluşturduğunda veri ek açıklaması öznitelikleri biçimindeki modeldeki meta veriler için desteği geliştirir.

### <a name="new-overloads-for-htmllabelfor-and-htmllabelformodel"></a>"HTML. LabelFor" ve "HTML. LabelForModel" için yeni aşırı yüklemeler

`LabelFor` ve `LabelForModel` yardımcı yöntemleri için yeni yöntem aşırı yüklemeleri eklendi. Yeni aşırı yüklemeler etiket metnini belirtmenize veya geçersiz kılmanızı sağlar.

### <a name="sessionless-controller-support"></a>Oturumsuz denetleyici desteği

ASP.NET MVC 3 ' te, bir denetleyici sınıfının oturum durumunu kullanmasını isteyip istemediğinizi belirtebilir ve gerekiyorsa, oturum durumunun okuma/yazma veya salt okuma olması gerekip gerekmediğini belirtebilirsiniz. Oturumsuz denetleyici desteği hakkında daha fazla bilgi için bkz. [MVC 3 sürüm notları](../whitepapers/mvc3-release-notes.md).

### <a name="new-additionalmetadataattribute-class"></a>Yeni "AdditionalMetadataAttribute" sınıfı

Bir model özelliği için `ModelMetadata.AdditionalValues` sözlüğünü doldurmak üzere [AdditionalMetadata](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx) özniteliğini kullanabilirsiniz. Örneğin, bir görünüm modelinin yalnızca bir yöneticiye gösterilmesi gereken bir özelliği varsa, aşağıdaki örnekte gösterildiği gibi bu özelliğe açıklama ekleyebilirsiniz:

[!code-csharp[Main](mvc3/samples/sample4.cs)]

Bu meta veriler, bir ürün görünümü modeli işlendiğinde herhangi bir görüntü veya düzenleyici şablonu için kullanılabilir hale getirilir. Meta veri bilgilerini yorumlamak en iyisidir.

### <a name="accountcontroller-improvements"></a>AccountController geliştirmeleri

Internet Proje şablonundaki AccountController önemli ölçüde geliştirildi.

### <a name="new-intranet-project-template"></a>Yeni Intranet proje şablonu

Windows kimlik doğrulamasına izin veren ve AccountController 'ı kaldıran yeni bir Intranet proje şablonu dahildir.
