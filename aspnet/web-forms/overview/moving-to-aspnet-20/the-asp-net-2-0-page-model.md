---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: ASP.NET 2,0 sayfa modeli | Microsoft Docs
author: microsoft
description: ASP.NET 1. x içinde, geliştiriciler satır içi kod modeli ve arka plan kod modeli arasında seçim yapmış. Arka plan kodu, src özniteliği kullanılarak uygulanabilir...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: bcb71b2b5a484e8756406867e08e8aa699a9024d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78547651"
---
# <a name="the-aspnet-20-page-model"></a>ASP.NET 2,0 sayfa modeli

[Microsoft](https://github.com/microsoft) tarafından

> ASP.NET 1. x içinde, geliştiriciler satır içi kod modeli ve arka plan kod modeli arasında seçim yapmış. Arka plan kodu, @Page yönergesinin src özniteliği veya CodeBehind özniteliği kullanılarak uygulanabilir. ASP.NET 2,0 ' de, geliştiriciler hala satır içi kod ve arka plan kodu arasında seçim yapmış, ancak arka plan kod modeli için önemli iyileştirmeler yapılmıştır.

ASP.NET 1. x içinde, geliştiriciler satır içi kod modeli ve arka plan kod modeli arasında seçim yapmış. Arka plan kodu, @Page yönergesinin src özniteliği veya CodeBehind özniteliği kullanılarak uygulanabilir. ASP.NET 2,0 ' de, geliştiriciler hala satır içi kod ve arka plan kodu arasında seçim yapmış, ancak arka plan kod modeli için önemli iyileştirmeler yapılmıştır.

## <a name="improvements-in-the-code-behind-model"></a>Arka plan kod modelindeki geliştirmeler

ASP.NET 2,0 ' de arka plan kod modelindeki değişiklikleri tam olarak anlamak için, ASP.NET 1. x içinde olduğu gibi modeli hızlı bir şekilde gözden geçirmeniz en iyisidir.

## <a name="the-code-behind-model-in-aspnet-1x"></a>ASP.NET 1. x içindeki arka plan kod modeli

ASP.NET 1. x içinde, arka plan kod modeli bir ASPX dosyası (Webform) ve programlama kodunu içeren bir arka plan kod dosyası. İki dosya ASPX dosyasında @Page yönergesi kullanılarak bağlandı. ASPX sayfasındaki her denetim, arka plan kod dosyasında örnek değişkeni olarak karşılık gelen bir bildirime sahipti. Arka plan kod dosyasında olay bağlama kodu ve Visual Studio Tasarımcısı için gereken kod oluşturulmuş kod de yer alır. Bu model oldukça iyi çalıştı, ancak ASPX sayfasındaki her ASP.NET öğesi arka plan kod dosyasında karşılık gelen kodu gerektirdiğinden, kod ve içerik için doğru ayrım yoktu. Örneğin, bir tasarımcı Visual Studio IDE dışında bir ASPX dosyasına yeni bir sunucu denetimi eklendiyse, arka plan kod dosyasında bu denetim için bir bildirimin yokluğu nedeniyle uygulama kesilir.

## <a name="the-code-behind-model-in-aspnet-20"></a>ASP.NET 2,0 ' de arka plan kod modeli

ASP.NET 2,0, bu modelde büyük ölçüde gelişir. ASP.NET 2,0 ' de, arka plan kodu ASP.NET 2,0 ' de sunulan yeni *kısmi sınıflar* kullanılarak uygulanır. ASP.NET 2,0 içindeki arka plan kod sınıfı, bir kısmi sınıf olarak tanımlanır ve bu, sınıf tanımının yalnızca bir kısmını içerir. Sınıf tanımının kalan bölümü, ASP.NET 2,0 tarafından çalışma zamanında ASPX sayfası kullanılarak veya Web sitesi önceden derlenmiş olduğunda dinamik olarak oluşturulur. Arka plan kod dosyası ve ASPX sayfası arasındaki bağlantı hala @ Page yönergesi kullanılarak oluşturulmuştur. Ancak, ASP.NET 2,0, bir CodeBehind veya src özniteliği yerine şimdi CodeFile özniteliğini kullanır. Inherits özniteliği, sayfanın sınıf adını belirtmek için de kullanılır.

Tipik bir @ Page yönergesi şöyle görünebilir:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

ASP.NET 2,0 arka plan kod dosyasındaki tipik bir sınıf tanımı şöyle görünebilir:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> C#ve Visual Basic şu anda kısmi sınıfları destekleyen tek yönetilen dillerdir. Bu nedenle, J# kullanan geliştiriciler ASP.NET 2,0 ' de arka plan kod modelini kullanamaz.

Yeni model, geliştiriciler artık yalnızca oluşturdukları kodu içeren kod dosyalarına sahip olacağı için arka plan kod modelini geliştirir. Arka plan kod dosyasında örnek değişken bildirimleri olmadığından, Ayrıca kod ve içerik için doğru bir ayrım sağlar.

> [!NOTE]
> ASPX sayfasına yönelik kısmi sınıf olay bağlamanın gerçekleştiği yerdir, Visual Basic geliştiriciler, olayları bağlamak için arka plan kodundaki Handles anahtar sözcüğünü kullanarak küçük bir performans artışı sağlayabilir. C#eşdeğer anahtar sözcüğe sahip değildir.

## <a name="new--page-directive-attributes"></a>Yeni @ Page yönergesi öznitelikleri

ASP.NET 2,0, @ page yönergesine birçok yeni öznitelik ekler. Aşağıdaki öznitelikler ASP.NET 2,0 ' de yenidir.

## <a name="async"></a>Zaman Uyumsuz

Async özniteliği, sayfanın zaman uyumsuz olarak yürütülmesini yapılandırmanızı sağlar. Bu modüldeki daha sonra gelen zaman uyumsuz sayfaları iyi kapsar.

## <a name="asynctimeout"></a>AsyncTimeout

Zaman uyumsuz sayfalar için zaman aşımı belirtildi. Varsayılan değer 45 saniyedir.

## <a name="codefile"></a>CodeFile

CodeFile özniteliği, Visual Studio 2002/2003 ' deki CodeBehind özniteliğinin yerini alır.

### <a name="codefilebaseclass"></a>CodeFileBaseClass

CodeFileBaseClass özniteliği, birden çok sayfanın tek bir temel sınıftan türemesini istediğiniz durumlarda kullanılır. ASP.NET içindeki kısmi sınıfların uygulanması nedeniyle, bu öznitelik olmadan, ASP. netme derleme altyapısı sayfadaki denetimlere göre otomatik olarak yeni üyeler oluşturacak şekilde, bir ASPX sayfasında belirtilen paylaşılan ortak alanları kullanan bir temel sınıf düzgün çalışmaz. Bu nedenle, ASP.NET ' de iki veya daha fazla sayfa için ortak bir temel sınıf istiyorsanız, CodeFileBaseClass özniteliğinde temel sınıfınızı belirtmeniz ve ardından her bir sayfa sınıfını bu temel sınıftan türemeniz gerekecektir. Bu öznitelik kullanıldığında CodeFile özniteliği de gereklidir.

## <a name="compilationmode"></a>CompilationMode

Bu öznitelik ASPX sayfasının CompilationMode özelliğini ayarlamanıza olanak sağlar. CompilationMode özelliği, **her zaman**, **Otomatik**ve **hiçbir zaman**değerlerini içeren bir numaralandırmadır. Varsayılan değer **her zaman**. **Otomatik** ayar ASP.net, mümkünse sayfayı dinamik olarak derlemeye engel olur. Dinamik derlemeden sayfaların dışlanması performansı artırır. Ancak, hariç tutulan bir sayfa derlenmesi gereken kodu içeriyorsa, sayfa gözatılırken bir hata oluşur.

## <a name="enableeventvalidation"></a>EnableEventValidation

Bu öznitelik, geri gönderme ve geri çağırma olaylarının doğrulanıp doğrulanması gerekip gerekmediğini belirtir. Bu etkinleştirildiğinde, geri gönderme veya geri çağırma olaylarının bağımsız değişkenleri, ilk olarak kendilerini izleyen sunucu denetiminden kaynaklandıklarından emin olmak için denetlenir.

## <a name="enabletheming"></a>Enabletemalarını

Bu öznitelik, bir sayfada ASP.NET temalarının kullanılıp kullanılmadığını belirtir. Varsayılan değer **false**'dur. ASP.NET temaları [Modül 10](profiles-themes-and-web-parts.md)' da ele alınmıştır.

## <a name="linepragmas"></a>LinePragmas

Bu öznitelik, derleme sırasında satır pragmaları eklenip eklenmeyeceğini belirtir. Satır pragmaları, hata ayıklayıcıları tarafından kodun belirli bölümlerini işaretlemek için kullanılan seçeneklerdir.

## <a name="maintainscrollpositiononpostback"></a>MaintainScrollPositionOnPostback

Bu öznitelik, geri göndermeler arasında kaydırma konumunu korumak için JavaScript 'In sayfaya eklenip eklenmeyeceğini belirtir. Bu öznitelik varsayılan olarak **false 'tur** .

Bu öznitelik **true**olduğunda, ASP.net aşağıdaki gibi görünen geri göndermede bir &lt;betik&gt; bloğu ekler:

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

Bu betik bloğu için src 'nin WebResource. axd olduğunu unutmayın. Bu kaynak bir fiziksel yol değil. Bu betik istendiğinde, ASP.NET dinamik olarak betiği oluşturur.

### <a name="masterpagefile"></a>MasterPageFile

Bu öznitelik, geçerli sayfa için ana sayfa dosyasını belirtir. Yol göreli veya mutlak olabilir. Ana sayfalar [Modül 4](master-pages.md)' te ele alınmıştır.

## <a name="stylesheettheme"></a>StyleSheetTheme

Bu öznitelik, bir ASP.NET 2,0 teması tarafından tanımlanan Kullanıcı arabirimi görünüm özelliklerini geçersiz kılmanızı sağlar. Temalar [Modül 10](profiles-themes-and-web-parts.md)' da ele alınmıştır.

## <a name="theme"></a>Tema

Sayfa için temayı belirtir. StyleSheetTheme özniteliği için bir değer belirtilmemişse, tema özniteliği sayfadaki denetimlere uygulanan tüm stilleri geçersiz kılar.

## <a name="title"></a>Başlık

Sayfanın başlığını ayarlar. Burada belirtilen değer, işlenen sayfanın &lt;title&gt; öğesinde görüntülenir.

### <a name="viewstateencryptionmode"></a>ViewStateEncryptionMode

ViewStateEncryptionMode numaralandırması için değeri ayarlar. Kullanılabilir değerler **her zaman**, **Otomatik**ve **hiç**değildir. Varsayılan değer **Auto**' dır. Bu öznitelik **Auto**değeri olarak ayarlandığında, ViewState şifrelenir ve **RegisterRequiresViewStateEncryption** yöntemini çağırarak bir denetim ister.

## <a name="setting-public-property-values-via-the--page-directive"></a>@ Page yönergesi aracılığıyla ortak özellik değerlerini ayarlama

ASP.NET 2,0 ' deki @ Page yönergesinin yeni bir özelliği, bir temel sınıfın ortak özelliklerinin başlangıç değerini ayarlamanıza olanak sağlar. Örneğin, temel sınıfınıza **SomeText** adlı bir genel özellik olduğunu ve bir sayfa yüklendiğinde **Hello** olarak başlatılmasını istediğinizi varsayalım. Bunu, @ Page yönergesinin değerini şöyle ayarlayarak yapabilirsiniz:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

@ Page yönergesinin **SomeText** özniteliği, temel sınıftaki SomeText özelliğinin başlangıç değerini *Merhaba!* olarak ayarlar. Aşağıdaki video, @ Page yönergesini kullanarak bir temel sınıfta ortak bir özelliğin başlangıç değerini ayarlamaya yönelik bir yönergedir.

![](the-asp-net-2-0-page-model/_static/image1.png)

[Tam ekran videosunu açın](the-asp-net-2-0-page-model/_static/setprop1.wmv)

## <a name="new-public-properties-of-the-page-class"></a>Sayfa sınıfının yeni ortak özellikleri

Aşağıdaki ortak özellikler ASP.NET 2,0 ' de yenidir.

## <a name="apprelativetemplatesourcedirectory"></a>AppRelativeTemplateSourceDirectory

Sayfa veya denetimin uygulama göreli yolunu döndürür. Örneğin, http://app/folder/page.aspxbulunan bir sayfa için, özelliği ~/Folder/döndürür.

## <a name="apprelativevirtualpath"></a>AppRelativeVirtualPath

Sayfanın veya denetimin göreli sanal dizin yolunu döndürür. Örneğin, http://app/folder/page.aspxbulunan bir sayfa için, özelliği ~/Folder/Page.exe.

## <a name="asynctimeout"></a>AsyncTimeout

Zaman uyumsuz sayfa işleme için kullanılan zaman aşımını alır veya ayarlar. (Zaman uyumsuz sayfalar Bu modülün ilerleyen kısımlarında ele alınacaktır.)

## <a name="clientquerystring"></a>ClientQueryString

İstenen URL 'nin sorgu dizesi kısmını döndüren salt okunurdur bir özellik. Bu değer, URL kodlamalı. Bunu çözmek için HttpServerUtility sınıfının Urlşifre kodu yöntemini kullanabilirsiniz.

## <a name="clientscript"></a>Istemci betiği

Bu özellik, ASP 'yi yönetmek için kullanılabilecek bir ClientScriptManager nesnesi döndürür. istemci tarafı komut dosyasının ağları. (ClientScriptManager Sınıfı Bu modülün ilerleyen kısımlarında ele alınmıştır.)

## <a name="enableeventvalidation"></a>EnableEventValidation

Bu özellik, geri gönderme ve geri çağırma olayları için olay doğrulamasının etkinleştirilip etkinleştirilmediğini denetler. Etkinleştirildiğinde, geri gönderme veya geri çağırma olaylarının bağımsız değişkenleri, ilk olarak kendilerini izleyen sunucu denetiminden kaynaklarından kaynaklandıklarından emin olmak için doğrulanır.

## <a name="enabletheming"></a>Enabletemalarını

Bu özellik bir ASP.NET 2,0 temasının sayfaya uygulanıp uygulanmadığını belirten bir Boole alır veya ayarlar.

## <a name="form"></a>Form

Bu özellik ASPX sayfasındaki HTML formunu HtmlForm nesnesi olarak döndürür.

## <a name="header"></a>Üstbilgi

Bu özellik sayfa üstbilgisini içeren bir HtmlHead nesnesine bir başvuru döndürür. Döndürülen HtmlHead nesnesini, stil sayfaları, meta etiketler vb. almak/ayarlamak için kullanabilirsiniz.

## <a name="idseparator"></a>IdSeparator

Bu salt okunurdur özelliği, ASP.NET bir sayfadaki denetimler için benzersiz bir KIMLIK oluştururken denetim tanımlayıcılarını ayırmak için kullanılan karakteri alır. Doğrudan kodunuzdan kullanılmak üzere tasarlanmamıştır.

## <a name="isasync"></a>IsAsync

Bu özellik, zaman uyumsuz sayfalara izin verir. Zaman uyumsuz sayfalar Bu modülün ilerleyen kısımlarında ele alınmıştır.

## <a name="iscallback"></a>IsCallback

Bu salt okunurdur özelliği, sayfanın geri arama sonucu olması durumunda **true** değerini döndürür. Geri aramalar Bu modülün ilerleyen kısımlarında ele alınmıştır.

## <a name="iscrosspagepostback"></a>IsCrossPagePostBack

Bu salt okunurdur özelliği, sayfa çapraz sayfa geri gönderme özelliğinin parçasıysa **true** değerini döndürür. Çapraz sayfa geri göndermeler Bu modülün ilerleyen kısımlarında ele alınmıştır.

## <a name="items"></a>Öğeler

Sayfa içeriğinde depolanan tüm nesneleri içeren bir IDictionary örneğine bir başvuru döndürür. Bu IDictionary nesnesine öğe ekleyebilirsiniz ve bağlam ömrü boyunca sizin için kullanılabilir olacaktır.

## <a name="maintainscrollpositiononpostback"></a>MaintainScrollPositionOnPostBack

Bu özellik, geri gönderme gerçekleştikten sonra tarayıcıda sayfa kaydırma konumunu tutan JavaScript 'In ASP.NET olup olmadığını denetler. (Bu özelliğin ayrıntıları Bu modülün başlarında anlatılmıştır.)

## <a name="master"></a>Asıl

Bu salt okunurdur özelliği, ana sayfanın uygulandığı bir sayfa için MasterPage örneğine bir başvuru döndürür.

## <a name="masterpagefile"></a>MasterPageFile

Sayfa için ana sayfa dosya adını alır veya ayarlar. Bu özellik yalnızca PreInit yönteminde ayarlanabilir.

## <a name="maxpagestatefieldlength"></a>MaxPageStateFieldLength

Bu özellik sayfa durumunun bayt cinsinden uzunluk üst sınırını alır veya ayarlar. Özellik pozitif bir sayı olarak ayarlandıysa, sayfalar görünümü durumu, belirtilen bayt sayısını aşmayacak şekilde birden çok gizli alana ayrılır. Özellik negatif bir sayı ise, Görünüm durumu öbeklere bölünmeyecektir.

## <a name="pageadapter"></a>PageAdapter

İstenen tarayıcı için sayfayı değiştiren PageAdapter nesnesine bir başvuru döndürür.

## <a name="previouspage"></a>PreviousPage

Sunucu. aktarma veya çapraz sayfa geri gönderme durumlarında önceki sayfaya bir başvuru döndürür.

## <a name="skinid"></a>SkinID

Sayfaya uygulanacak ASP.NET 2,0 kaplamasını belirtir.

## <a name="stylesheettheme"></a>StyleSheetTheme

Bu özellik bir sayfaya uygulanan stil sayfasını alır veya ayarlar.

## <a name="templatecontrol"></a>TemplateControl

Sayfa için içeren denetime bir başvuru döndürür.

## <a name="theme"></a>Tema

Sayfaya uygulanan ASP.NET 2,0 temasının adını alır veya ayarlar. Bu değer PreInit yönteminden önce ayarlanmalıdır.

## <a name="title"></a>Başlık

Bu özellik sayfa başlığından alınan sayfanın başlığını alır veya ayarlar.

## <a name="viewstateencryptionmode"></a>ViewStateEncryptionMode

Sayfanın ViewStateEncryptionMode değerini alır veya ayarlar. Bu modülün önceki kısımlarında yer alarak bu özelliğin ayrıntılı bir tartışmasına bakın.

## <a name="new-protected-properties-of-the-page-class"></a>Sayfa sınıfının yeni korumalı özellikleri

Aşağıda, ASP.NET 2,0 ' deki sayfa sınıfının yeni korumalı özellikleri verilmiştir.

## <a name="adapter"></a>Bağdaştırıcı

İstenen cihazda sayfayı işleyen ControlAdapter öğesine bir başvuru döndürür.

## <a name="asyncmode"></a>AsyncMode

Bu özellik, sayfanın zaman uyumsuz olarak işlenip işlenmediğini belirtir. Doğrudan kodda değil, çalışma zamanı tarafından kullanılmak üzere tasarlanmıştır.

## <a name="clientidseparator"></a>Clienentidseparator

Bu özellik, denetimler için benzersiz istemci kimlikleri oluştururken ayırıcı olarak kullanılan karakteri döndürür. Doğrudan kodda değil, çalışma zamanı tarafından kullanılmak üzere tasarlanmıştır.

## <a name="pagestatepersister"></a>PageStatePersister

Bu özellik sayfa için PageStatePersister nesnesini döndürür. Bu özellik öncelikle ASP.NET denetim geliştiricileri tarafından kullanılır.

## <a name="uniquefilepathsuffix"></a>UniqueFilePathSuffix

Bu özellik, tarayıcıları önbelleğe almak için dosya yoluna eklenen benzersiz bir sonek döndürür. Varsayılan değer \_\_UPS = ve 6 basamaklı bir sayıdır.

## <a name="new-public-methods-for-the-page-class"></a>Sayfa sınıfı için yeni ortak Yöntemler

Aşağıdaki ortak Yöntemler ASP.NET 2,0 sayfa sınıfı için yenidir.

## <a name="addonprerendercompleteasync"></a>AddOnPreRenderCompleteAsync

Bu yöntem, zaman uyumsuz sayfa yürütme için olay işleyicisi temsilcilerini kaydeder. Zaman uyumsuz sayfalar Bu modülün ilerleyen kısımlarında ele alınmıştır.

## <a name="applystylesheetskin"></a>ApplyStyleSheetSkin

Sayfaların sayfa stil sayfasına özelliklerini uygular.

## <a name="executeregisteredasynctasks"></a>ExecuteRegisteredAsyncTasks

Bu yöntem, zaman uyumsuz bir görevi kullanır.

### <a name="getvalidators"></a>Getdoğrulayıcılar

Belirtilen doğrulama grubu için doğrulayıcılar koleksiyonu veya hiçbiri belirtilmemişse varsayılan doğrulama grubu döndürür.

## <a name="registerasynctask"></a>RegisterAsyncTask

Bu yöntem, yeni bir zaman uyumsuz görev kaydeder. Zaman uyumsuz sayfalar Bu modülün ilerleyen kısımlarında ele alınmıştır.

## <a name="registerrequirescontrolstate"></a>RegisterRequiresControlState

Bu yöntem, ASP.NET sayfasının denetim durumunun kalıcı olması gerektiğini söyler.

## <a name="registerrequiresviewstateencryption"></a>RegisterRequiresViewStateEncryption

Bu yöntem, ASP.NET sayfasının ViewState 'in şifreleme gerektirdiğini söyler.

## <a name="resolveclienturl"></a>ResolveClientUrl

Görüntüler için istemci istekleri için kullanılabilen göreli bir URL döndürür.

## <a name="setfocus"></a>SetFocus

Bu yöntem, odağı sayfa ilk yüklendiğinde belirtilen denetime ayarlar.

## <a name="unregisterrequirescontrolstate"></a>UnregisterRequiresControlState

Bu yöntem, artık denetim durumu kalıcılığı gerektirmeyen şekilde kendisine geçirilen denetimin kaydını siler.

## <a name="changes-to-the-page-lifecycle"></a>Sayfa yaşam döngüsünde yapılan değişiklikler

ASP.NET 2,0 ' deki sayfa yaşam döngüsü önemli ölçüde değişmemiştir, ancak farkında olmanız gereken bazı yeni yöntemler vardır. ASP.NET 2,0 sayfa yaşam döngüsü aşağıda özetlenmiştir.

## <a name="preinit-new-in-aspnet-20"></a>PreInit (2,0 ASP.NET 'de yeni)

PreInit olayı, bir geliştiricinin erişebileceği yaşam döngüsünün en erken aşamasıdır. Bu olayın eklenmesi, program aracılığıyla ASP.NET 2,0 temalarını, ana sayfaları, bir ASP.NET 2,0 profili için erişim özelliklerini, vb. değiştirmeyi mümkün kılar. Bir geri gönderme durumundaysa, ViewState 'in, yaşam döngüsünün bu noktasındaki denetimlere henüz uygulandığını fark etmeniz önemlidir. Bu nedenle, bir geliştirici bu aşamada bir denetimin özelliğini değiştirirse, büyük olasılıkla sayfa yaşam döngüsünün üzerine yazılır.

## <a name="init"></a>Init

Init olayı ASP.NET 1. x değerinden değişmemiştir. Bu, sayfanızdaki denetimlerin özelliklerini okumak veya başlatmak istediğiniz yerdir. Bu aşamada, ana sayfalar, temalar vb. sayfada zaten uygulanmış.

## <a name="initcomplete-new-in-20"></a>Inittamamlanmıştır (2,0 ' de yeni)

Inittamamlanma olayı, sayfa başlatma aşamasının sonunda çağırılır. Yaşam döngüsünün bu noktasında, sayfadaki denetimlere erişebilirsiniz, ancak durumu henüz doldurulmamıştır.

## <a name="preload-new-in-20"></a>Önyükleme (2,0 ' de yeni)

Bu olay, tüm geri gönderme verileri uygulandıktan sonra ve sayfa\_yüklemesinden hemen önce çağrılır.

## <a name="load"></a>Yükleme

Load olayı ASP.NET 1. x öğesinden değişmemiştir.

## <a name="loadcomplete-new-in-20"></a>Loadtamamlanmıştır (2,0 ' de yeni)

Loadtamamlanma olayı, sayfa yükleme aşamasındaki son olaydır. Bu aşamada, sayfaya tüm geri gönderme ve ViewState verileri uygulandı.

## <a name="prerender"></a>Işleme

Dinamik olarak sayfaya eklenen denetimler için ViewState 'in düzgün bir şekilde korunmasını istiyorsanız, PreRender olayı bunları eklemek için son fırsattır.

## <a name="prerendercomplete-new-in-20"></a>Prerendertamamlanmıştır (2,0 sürümündeki yenilikler)

Prerendertamamlanma aşamasında, sayfaya tüm denetimler eklendi ve sayfa işlenmesine hazırlanıyor. Prerendertamamlanma olayı, sayfa görünüm durumu kaydedilmeden önce oluşturulan son olaydır.

## <a name="savestatecomplete-new-in-20"></a>Savestatetamamlanmıştır (2,0 ' de yeni)

Savestatetamamlanma olayı, tüm sayfa ViewState ve denetim durumu kaydedildikten hemen sonra çağrılır. Bu, sayfa gerçekten tarayıcıya işlenmeden önce son olaydır.

## <a name="render"></a>İşleme

Render yöntemi, ASP.NET 1. x öğesinden beri değişmemiştir. Bu, HtmlTextWriter 'ın başlatıldığı ve sayfanın tarayıcıya işlendiği yerdir.

## <a name="cross-page-postback-in-aspnet-20"></a>ASP.NET 2,0 ' de çapraz sayfa geri gönderme

ASP.NET 1. x içinde, geri göndermeler aynı sayfada yer almak için gerekiyordu. Çapraz sayfaya geri göndermeler yapılmasına izin verilmedi. ASP.NET 2,0, IButtonControl arabirimi aracılığıyla farklı bir sayfaya geri gönderi özelliği ekler. Yeni IButtonControl arabirimini uygulayan tüm denetimler (üçüncü taraf özel denetimlerine ek olarak Button, LinkButton ve ImageButton), PostBackUrl özniteliği kullanılarak bu yeni işlevlerden yararlanabilir. Aşağıdaki kod, ikinci bir sayfaya geri gönderen bir düğme denetimini gösterir.

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

Sayfa geri gönderildiğinde, geri göndermeyi Başlatan sayfaya ikinci sayfadaki PreviousPage özelliği aracılığıyla erişilebilir. Bu işlevsellik, bir denetim farklı bir sayfaya geri gönderdiğinde ASP.NET 2,0 'nin sayfada oluşturduğu yeni WebForm\_DoPostBackWithOptions istemci tarafı işlevi aracılığıyla uygulanır. Bu JavaScript işlevi, bir betiği istemciye yayar yeni WebResource. axd işleyicisi tarafından sağlanır.

Aşağıdaki video, çapraz sayfa geri gönderme işlemi için izlenecek bir yönergedir.

![](the-asp-net-2-0-page-model/_static/image2.png)

[Tam ekran videosunu açın](the-asp-net-2-0-page-model/_static/xpage1.wmv)

## <a name="more-details-on-cross-page-postbacks"></a>Çapraz sayfa geri göndermeler hakkında daha fazla bilgi

### <a name="viewstate"></a>ViewState

Bir çapraz sayfa geri gönderme senaryosunda ilk sayfanın ViewState 'e ne olacağı hakkında zaten bilgi sahibi olabilirsiniz. All, IPostBackDataHandler uygulamayan tüm denetimler durumunu ViewState aracılığıyla kalıcı hale getirecektir. bu nedenle, bir çapraz sayfa geri gönderisinin ikinci sayfasında bu denetimin özelliklerine erişebilmek için, sayfanın ViewState öğesine erişiminizin olması gerekir. ASP.NET 2,0, ikinci sayfada \_\_PREVIOUSPAGE adlı yeni bir gizli alan kullanarak bu senaryoyu ele alır. İkinci sayfadaki tüm denetimlerin özelliklerine erişebilmeniz için, \_\_PREVIOUSPAGE form alanı ilk sayfanın ViewState özelliğini içerir.

### <a name="circumventing-findcontrol"></a>Bulventing FindControl

Çapraz sayfa geri göndermeye ilişkin video kılavuzsunda, ilk sayfada TextBox denetimine bir başvuru almak için FindControl metodunu kullandım. Bu yöntem bu amaçla iyi bir şekilde çalışarak, FindControl pahalıdır ve ek kod yazmayı gerektirir. Neyse ki, ASP.NET 2,0, bu amaçla birçok senaryoda çalışacak FindControl için bir alternatif sağlar. PreviousPageType yönergesi, TypeName veya VirtualPath özniteliği kullanarak önceki sayfaya kesin olarak yazılmış bir başvuruya sahip olmanızı sağlar. TypeName özniteliği, bir önceki sayfanın türünü belirtmenizi sağlar, bu, VirtualPath özniteliği bir sanal yol kullanarak önceki sayfaya başvurmanız sağlar. PreviousPageType yönergesini ayarladıktan sonra, genel özellikleri kullanarak erişime izin vermek istediğiniz denetimleri (vb.) kullanıma sunmalısınız.

## <a name="lab-1-cross-page-postback"></a>Laboratuvar 1 çapraz sayfa geri gönderme

Bu laboratuvarda, ASP.NET 2,0 ' in yeni çapraz sayfa geri gönderme işlevlerini kullanan bir uygulama oluşturacaksınız.

1. Visual Studio 2005 ' i açın ve yeni bir ASP.NET Web sitesi oluşturun.
2. Page2. aspx adlı yeni bir WebForm ekleyin.
3. Tasarım görünümü ' de default. aspx ' i açın ve bir düğme denetimi ve TextBox denetimi ekleyin. 

    1. Düğme denetimine bir **submitbutton** kimliği ve TextBox denetimini bir **Kullanıcı adı**olarak verir.
    2. Düğmenin PostBackUrl özelliğini Page2. aspx olarak ayarlayın.
4. Kaynak görünümünde Page2. aspx ' i açın.
5. Aşağıda gösterildiği gibi bir @ PreviousPageType yönergesi ekleyin:
6. Aşağıdaki kodu sayfaya ekleyin\_Page2. aspx 'in arka plan kodunu yükleyin: 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. Yapı menüsünde oluştur ' a tıklayarak projeyi derleyin.
8. Aşağıdaki kodu varsayılan. aspx için arka plan koduna ekleyin: 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. Page2. aspx içindeki\_sayfasını aşağıdaki gibi değiştirin: 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. Projeyi oluşturun.
11. Projeyi çalıştırın.
12. Metin kutusuna adınızı girin ve düğmeye tıklayın.
13. Sonuç nedir?

## <a name="asynchronous-pages-in-aspnet-20"></a>ASP.NET 2,0 ' de zaman uyumsuz sayfalar

ASP.NET ' de birçok çekişme sorunu, dış çağrıların (örneğin, Web hizmeti veya veritabanı çağrıları), dosya GÇ gecikmesi vb. gecikme süresine neden olmuştur. Bir ASP.NET uygulamasına karşı bir istek yapıldığında, ASP.NET bu isteğe hizmet vermek için çalışan iş parçacıklarından birini kullanır. Bu istek, istek tamamlanana ve yanıt gönderilene kadar o iş parçacığına sahip olur. ASP.NET 2,0, sayfaları zaman uyumsuz olarak yürütme özelliğini ekleyerek bu sorun türleriyle ilgili gecikme sorunlarını gidermek için arar. Bu, bir çalışan iş parçacığının isteği başlatabileceği ve daha sonra başka bir iş parçacığına daha fazla yürütme yaparak kullanılabilir iş parçacığı havuzuna hızla geri döndürmeyeceği anlamına gelir. GÇ, veritabanı çağrısı, vb. tamamlandığında, iş parçacığı havuzundan isteği tamamlaması için yeni bir iş parçacığı alınır.

Sayfanın zaman uyumsuz olarak yürütülmesi sırasında ilk adım, sayfa yönergesinin **zaman uyumsuz** özniteliğini şöyle ayarlayabilmenizi sağlar:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

Bu öznitelik, ASP.NET 'in sayfa için IHttpAsyncHandler uygulamasını söyler.

Sonraki adım, git 'ten önceki sayfanın yaşam döngüsünün bulunduğu bir noktada Addonprerenderilerteasync yöntemini çağırmalıdır. (Bu yöntem genellikle sayfa\_Load içinde çağrılır.) Addonprerendertamteasync yöntemi iki parametre alır; bir BeginEventHandler ve bir EndEventHandler. BeginEventHandler, daha sonra EndEventHandler parametresi olarak geçirilmiş bir IAsyncResult döndürür.

Aşağıdaki video, zaman uyumsuz bir sayfa isteğine yönelik bir yönergedir.

![](the-asp-net-2-0-page-model/_static/image3.png)

[Tam ekran videosunu açın](the-asp-net-2-0-page-model/_static/async1.wmv)

> [!NOTE]
> Zaman uyumsuz bir sayfa, EndEventHandler tamamlanana kadar tarayıcıya işlenmez. Şüpheli ancak bazı geliştiricilerin zaman uyumsuz istekleri zaman uyumsuz geri çağırmalar gibi düşündüklerini unutmayın. Bunların farkında olmak önemlidir. Zaman uyumsuz isteklere avantaj, ilk çalışan iş parçacığının yeni isteklere hizmet vermek için iş parçacığı havuzuna döndürülebilmektir ve bu sayede GÇ bağlı olması nedeniyle çekişmeyi azaltır.

## <a name="script-callbacks-in-aspnet-20"></a>ASP.NET 2,0 ' de betik geri çağırmaları

Web geliştiricileri, bir geri çağırma ile ilişkili titreşmeyi önlemenin yollarını her zaman aradı. ASP.NET 1. x içinde SmartNavigation, titreşmeyi önlemenin en yaygın yöntemidir, ancak SmartNavigation, istemci üzerindeki uygulamanın karmaşıklığı nedeniyle bazı geliştiriciler için sorunlara neden oldu. ASP.NET 2,0, bu sorunu komut dosyası geri çağırmaları ile gidermektedir. Betik geri çağırmaları Web sunucusuna JavaScript aracılığıyla istek yapmak için XMLHttp kullanır. XMLHttp isteği, daha sonra tarayıcının DOM 'ı aracılığıyla işlenebilen XML verileri döndürür. XMLHttp kodu kullanıcıdan yeni WebResource. axd işleyicisi tarafından gizlenir.

ASP.NET 2,0 ' de bir betik geri çağırması yapılandırmak için gereken birkaç adım vardır.

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a>1\. Adım: ICallbackEventHandler arabirimini uygulama

ASP.NET 'in sayfanızı bir betik geri çağırması olarak tanıması için ICallbackEventHandler arabirimini uygulamanız gerekir. Bunu, arka plan kod dosyanızda şöyle yapabilirsiniz:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

Bunu aşağıdaki gibi @ Implements yönergesini kullanarak da yapabilirsiniz:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

Satır içi ASP.NET kodu kullanırken genellikle @ Implements yönergesini kullanırsınız.

## <a name="step-2--call-getcallbackeventreference"></a>2\. Adım: GetCallbackEventReference çağırma

Daha önce belirtildiği gibi, XMLHttp çağrısı WebResource. axd işleyicisinde kapsüllenir. Sayfanız işlendiğinde ASP.NET, WebResource. axd tarafından sunulan bir istemci betiği olan WebForm\_DoCallback öğesine bir çağrı ekler. WebForm\_DoCallback işlevi, bir geri çağırma için \_\_doPostBack işlevinin yerini alır. \_\_doPostBack 'ın formu sayfada programlı bir şekilde göndermediğini unutmayın. Bir geri arama senaryosunda, geri gönderme işlemini engellemek, bu nedenle \_\_doPostBack yok.

> [!NOTE]
> \_\_doPostBack, istemci betiği geri çağırma senaryosunda sayfada hala işlenir. Ancak, geri çağırma için kullanılmaz.

WebForm\_DoCallback istemci tarafı işlevinin bağımsız değişkenleri, normalde sayfa\_Load içinde çağrılan GetCallbackEventReference sunucu tarafı işlevi aracılığıyla sağlanır. GetCallbackEventReference için tipik bir çağrı şöyle görünebilir:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> Bu durumda, cm bir ClientScriptManager örneğidir. ClientScriptManager Sınıfı Bu modülün ilerleyen kısımlarında ele alınacaktır.

Daha fazla sayıda GetCallbackEventReference sürümü vardır. Bu durumda, bağımsız değişkenler aşağıdaki gibidir:

`this`

GetCallbackEventReference çağrıldığında denetime bir başvuru. Bu durumda, sayfanın kendisi olur.

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

İstemci tarafı koddan sunucu tarafı olayına geçirilecek dize bağımsız değişkeni. Bu durumda, ddlCompany adlı bir açılan listenin değerini geçen anlık Ileti.

`ShowCompanyName`

Sunucu tarafı geri çağırma olayından döndürülen değeri (dize olarak) kabul edecek istemci tarafı işlevinin adı. Bu işlev, yalnızca sunucu tarafında geri çağırma başarılı olduğunda çağrılır. Bu nedenle, sağlamlık açısından, bir hata durumunda yürütülecek bir istemci tarafı işlevinin adını belirten ek bir dize bağımsız değişkeni alan, GetCallbackEventReference 'ın aşırı yüklenmiş sürümünün kullanılması genellikle önerilir.

`null`

Sunucuya geri aramadan önce başlattığı istemci tarafı işlevini temsil eden bir dize. Bu durumda, böyle bir betik yoktur, bu nedenle bağımsız değişken null olur.

`true`

Geri aramanın zaman uyumsuz olarak yapılıp yapılmayacağını belirten bir Boole değeri.

İstemcide WebForm\_DoCallback çağrısı bu bağımsız değişkenleri geçilecektir. Bu nedenle, Bu sayfa istemcide işlendiğinde bu kod şöyle görünür:

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

İstemcideki işlevin imzasının bir bit farklı olduğuna dikkat edin. İstemci tarafı işlevi 5 dize ve Boole değeri geçirir. Ek dize (Yukarıdaki örnekte null), sunucu tarafı geri çağrısından gelen hataları işleyecek istemci tarafı işlevini içerir.

## <a name="step-3--hook-the-client-side-control-event"></a>3\. Adım: Istemci tarafı denetim olayını bağlama

Yukarıdaki GetCallbackEventReference öğesinin dönüş değeri bir dize değişkenine atandığını unutmayın. Bu dize, geri çağırma işlemini başlatan denetim için istemci tarafı olayını bağlamak için kullanılır. Bu örnekte, geri çağırma sayfadaki bir açılan pencerede başlatılır, bu nedenle *OnChange* olayını bağlamak istiyorum.

İstemci tarafı olayını bağlamak için, istemci tarafı biçimlendirmesine aşağıdaki şekilde bir işleyici eklemeniz yeterlidir:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

GetCallbackEventReference çağrısından döndürülen değer olan *Cbref* ' i hatırlayın. Yukarıda gösterilen WebForm\_DoCallback çağrısını içerir.

## <a name="step-4--register-the-client-side-script"></a>4\. Adım: Istemci tarafı betiğini kaydetme

Sunucu tarafı geri çağırma işlemi başarılı olduğunda **Showcompanyname** adlı bir istemci tarafı betiğin çalıştırılacağını belirten GetCallbackEventReference çağrısının çalıştırılacağını unutmayın. Bu betiğin bir ClientScriptManager örneği kullanılarak sayfaya eklenmesi gerekir. (ClientScriptManager Sınıfı Bu modülün ilerleyen kısımlarında ele alınacaktır.) Bunu şöyle yapabilirsiniz:

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a>5\. Adım: ICallbackEventHandler arabiriminin yöntemlerini çağırma

ICallbackEventHandler kodunuzda uygulamanız gereken iki yöntem içerir. Bunlar **RaiseCallbackEvent** ve **Getcallbackevent**.

**RaiseCallbackEvent** bir dizeyi bağımsız değişken olarak alır ve hiçbir şey döndürmez. Dize bağımsız değişkeni, istemci tarafı WebForm\_DoCallback çağrısından geçirilir. Bu durumda bu değer, ddlCompany adlı açılan listenin *değer* özniteliğidir. Sunucu tarafı kodunuz RaiseCallbackEvent yöntemine yerleştirilmelidir. Örneğin, geri arama bir dış kaynağa karşı bir WebRequest alıyorsa, bu kod RaiseCallbackEvent 'e yerleştirilmelidir.

**Getcallbackevent** , geri aramanın istemciye döndürülmesini işlemekten sorumludur. Bağımsız değişken almaz ve bir dize döndürür. Döndürdüğü dize, istemci tarafı işlevine bağımsız değişken olarak geçirilir, bu örnekte *Showcompanyname*.

Yukarıdaki adımları tamamladıktan sonra, ASP.NET 2,0 ' de bir betik geri çağırması gerçekleştirmeye hazırlanın.

![](the-asp-net-2-0-page-model/_static/image4.png)

[Tam ekran videosunu açın](the-asp-net-2-0-page-model/_static/callback1.wmv)

ASP.NET içindeki betik geri çağırmaları, XMLHttp çağrıları yapmayı destekleyen herhangi bir tarayıcıda desteklenir. Bu, günümüzde kullanımda olan tüm modern tarayıcıları içerir. Internet Explorer XMLHttp ActiveX nesnesini kullanır, ancak diğer modern tarayıcılar (yakında çıkacak IE 7 dahil), iç bir XMLHttp nesnesi kullanır. Bir tarayıcının geri çağırmaları destekleyip desteklemediğini programlı bir şekilde anlamak için **Request. Browser. SupportCallback** özelliğini kullanabilirsiniz. İstekte bulunan istemci komut dosyası geri çağırmaları destekliyorsa bu özellik **true değerini** döndürür.

## <a name="working-with-client-script-in-aspnet-20"></a>ASP.NET 2,0 ' de Istemci betiği ile çalışma

ASP.NET 2,0 ' deki istemci betikleri ClientScriptManager sınıfının kullanımı aracılığıyla yönetilir. ClientScriptManager Sınıfı, bir tür ve bir ad kullanarak istemci betikleri izler. Bu, aynı betiğin bir sayfada birden çok kez programlı bir şekilde eklenmesini engeller.

> [!NOTE]
> Bir komut dosyası bir sayfada başarıyla kaydedildikten sonra, aynı betiği kaydetmek için sonraki tüm girişimlerde, betiğin ikinci kez kaydedilmesinin başarısız olması gerekir. Yinelenen betikler eklenmez ve özel durum oluşmaz. Gereksiz hesaplamayı önlemek için, bir betiğin birden çok kez kaydolmaya çalışmamak üzere bir betiğin zaten kayıtlı olup olmadığını tespit etmek için kullanabileceğiniz yöntemler vardır.

ClientScriptManager 'ın yöntemleri tüm geçerli ASP.NET geliştiricilerine tanıdık gelmelidir:

## <a name="registerclientscriptblock"></a>RegisterClientScriptBlock

Bu yöntem, işlenen sayfanın en üstüne bir komut dosyası ekler. Bu, istemcide açıkça çağrılacak işlevleri eklemek için yararlıdır.

Bu yöntemin iki aşırı yüklü sürümü vardır. Dört bağımsız değişkenlerden üçü arasında ortak vardır. Bunlar:

`type (string)`

***Tür*** bağımsız değişkeni betik için bir tür tanımlar. Genellikle sayfanın türünü kullanmak iyi bir fikirdir. Tür için GetType ()).

`key (string)`

***Anahtar*** bağımsız değişkeni, komut dosyası için Kullanıcı tanımlı bir anahtardır. Bu, her komut dosyası için benzersiz olmalıdır. Zaten eklenmiş bir betikte aynı anahtara ve türe sahip bir komut dosyası eklemeye çalışırsanız, eklenmez.

`script (string)`

***Betik*** bağımsız değişkeni, eklenecek asıl betiği içeren bir dizedir. Betiği oluşturmak için bir StringBuilder kullanmanız ve ardından ***betik*** bağımsız değişkenini atamak için StringBuilder üzerinde ToString () metodunu kullanmanız önerilir.

Yalnızca üç bağımsız değişken içeren aşırı yüklenmiş RegisterClientScriptBlock kullanırsanız, betiğe betik öğelerini (&lt;betik&gt; ve &lt;/Script&gt;) eklemeniz gerekir.

RegisterClientScriptBlock 'un dördüncü bağımsız değişken alan aşırı yüklemesini kullanmayı tercih edebilirsiniz. Dördüncü bağımsız değişken, ASP.NET 'in sizin için betik öğeleri ekleyip eklememeyeceğini belirten bir Boole değeri. Bu bağımsız değişken **true**ise, betiğinizin betik öğelerini açıkça içermemesi gerekir.

Bir betiğin zaten kayıtlı olup olmadığını anlamak için IsClientScriptBlockRegistered metodunu kullanın. Bu, zaten kayıtlı olan bir betiği yeniden kaydetme denemesinden kaçınmanızı sağlar.

### <a name="registerclientscriptinclude-new-in-20"></a>RegisterClientScriptInclude (2,0 sürümündeki yenilikler)

RegisterClientScriptInclude etiketi, bir dış betik dosyasına bağlanan bir betik bloğu oluşturur. İki aşırı yüklemesi vardır. Bir anahtar ve URL alır. İkincisi, türü belirten üçüncü bir bağımsız değişken ekler.

Örneğin, aşağıdaki kod, uygulamanın betikler klasörünün kökündeki jsfunctions. js öğesine bağlanan bir betik bloğu oluşturur:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

Bu kod, işlenen sayfada aşağıdaki kodu üretir:

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> Betik bloğu sayfanın alt kısmında işlenir.

Bir betiğin zaten kayıtlı olup olmadığını anlamak için Isclientscriptıncluınregistered metodunu kullanın. Bu, bir betiği yeniden kaydetme denemesinden kaçınmanızı sağlar.

## <a name="registerstartupscript"></a>RegisterStartupScript

RegisterStartupScript yöntemi RegisterClientScriptBlock yöntemiyle aynı bağımsız değişkenleri alır. RegisterStartupScript ile kaydedilen bir betik, sayfa yüklendikten sonra, ancak OnLoad istemci tarafı olayından önce yürütülür. 1\. X içinde, RegisterStartupScript ile kaydedilen betikler, açılan &lt;formu&gt; etiketinden hemen sonra yerleştirirken, RegisterClientScriptBlock ile kaydedilen betikler hemen&gt; &lt;öncesine yerleştirildi. ASP.NET 2,0 ' de, her ikisi de kapatma &lt;form&gt; etiketinden hemen önce yerleştirilir.

> [!NOTE]
> RegisterStartupScript ile bir işlev kaydettiğinizde, bu işlev, istemci tarafı kodunda açıkça çağrılana kadar yürütülmez.

Bir betiğin zaten kayıtlı olup olmadığını ve bir betiği yeniden kaydetme denemesinden kaçının olduğunu anlamak için IsStartupScriptRegistered yöntemini kullanın.

## <a name="other-clientscriptmanager-methods"></a>Diğer ClientScriptManager yöntemleri

ClientScriptManager sınıfının diğer yararlı yöntemlerinden bazıları aşağıda verilmiştir.

|  <strong>GetCallbackEventReference</strong>   |                                                 Bu modüldeki önceki betikle geri çağırmaları inceleyin.                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <strong>GetPostBackClientHyperlink</strong>  |                İstemci tarafı olayından geri göndermek için kullanılabilen bir JavaScript başvurusu (JavaScript:&lt;Call&gt;) alır.                 |
|  <strong>GetPostBackEventReference</strong>   |                                   İstemciden geri gönderi başlatmak için kullanılabilecek bir dize alır.                                    |
|      <strong>GetWebResourceUrl 'Si</strong>       | Bir derlemeye gömülü bir kaynağın URL 'sini döndürür. <strong>RegisterClientScriptResource</strong>ile birlikte kullanılmalıdır. |
| <strong>RegisterClientScriptResource</strong> |     Sayfaya bir Web kaynağı kaydeder. Bunlar, bir derlemeye katıştırılmış ve yeni WebResource. axd işleyicisi tarafından işlenen kaynaklardır.      |
|     <strong>RegisterHiddenField</strong>      |                                                 Gizli form alanını sayfasıyla kaydeder.                                                 |
|  <strong>Registeronsubmitdeyimin</strong>   |                                  HTML formu gönderildiğinde yürütülen istemci tarafı kodunu kaydeder.                                   |
