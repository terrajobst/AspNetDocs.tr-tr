---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
title: ASP.NET AJAX kimlik doğrulamasını ve profilini anlama Uygulama Hizmetleri | Microsoft Docs
author: scottcate
description: Kimlik doğrulama hizmeti, kullanıcıların bir kimlik doğrulama tanımlama bilgisi almak için kimlik bilgilerini sağlamasına ve özel kullanıcıya izin veren ağ geçidi hizmetine izin verir...
ms.author: riande
ms.date: 03/14/2008
ms.assetid: 6ab4efb6-aab6-45ac-ad2c-bdec5848ef9e
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
msc.type: authoredcontent
ms.openlocfilehash: cab9acb1ffd75cca87f6c575a6abdd000235828e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640534"
---
# <a name="understanding-aspnet-ajax-authentication-and-profile-application-services"></a>ASP.NET AJAX Kimlik Doğrulaması ve Profil Uygulaması Hizmetlerini Anlama

[Scott](https://github.com/scottcate) tarafından

[PDF 'YI indir](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial03_MSAjax_ASP.NET_Services_cs.pdf)

> Kimlik doğrulama hizmeti, kullanıcıların bir kimlik doğrulama tanımlama bilgisi almak için kimlik bilgilerini sağlamasına olanak sağlar ve ASP.NET tarafından sağlanmış özel kullanıcı profillerine izin veren ağ geçidi hizmetidir. ASP.NET AJAX kimlik doğrulama hizmeti, standart ASP.NET Forms kimlik doğrulamasıyla uyumludur. bu nedenle, şu anda Forms kimlik doğrulaması kullanan uygulamalar (örneğin, oturum açma denetimiyle) AJAX kimlik doğrulama hizmetine yükseltilerek kesilmeyecektir.

## <a name="introduction"></a>Giriş

.NET Framework 3,5 kapsamında, Microsoft, boyutlandırılabilir bir ortam yükseltmesi sunmakta. Yeni bir geliştirme ortamı yoktur, ancak yeni dil ile tümleşik sorgu (LINQ) özellikleri ve diğer dil geliştirmeleri de daha fazla geliyor. Ayrıca, diğer araç kümelerinin bazı tanıdık özellikleri, özellikle de ASP.NET AJAX Uzantıları, .NET Framework temel sınıf kitaplığının birinci sınıf üyeleri olarak eklenmekte. Bu uzantılar, tam sayfa yenilemesi gerektirmeden sayfaların kısmi işlenmesi, istemci betiği (ASP.NET profil oluşturma API 'SI dahil) ve kapsamlı bir istemci tarafı API 'SI aracılığıyla Web hizmetlerine erişme özelliği dahil olmak üzere birçok yeni zengin istemci özelliğini etkinleştirir ASP.NET sunucu tarafı denetim kümesinde görülen denetim düzenlerinin çoğunu yansıtmak için tasarlanmıştır.

Bu Teknik İnceleme, ASP.NET profil oluşturma ve Forms kimlik doğrulama hizmetlerinin, Microsoft ASP.NET AJAX Extensionthe Service Authentication Services tarafından kullanıma sunulduğunu ve kullanımını, (Ayrıca Profil oluşturma hizmeti) bir Web hizmeti proxy betiği aracılığıyla sunulur. AJAX Uzantıları, AuthenticationServiceManager sınıfı aracılığıyla özel kimlik doğrulamasını da destekler.

Bu Teknik İnceleme, Visual Studio 2008 ve 3,5 .NET Framework Beta 2 sürümünü temel alır. Bu Teknik İnceleme, Visual Studio 2008 Beta 2 ve Visual Web Developer Express 'i değil, Visual Studio 'nun Kullanıcı arabirimine göre izlenecek yollar sağlayacak şekilde de çalışır. Bazı kod örnekleri, Visual Web Developer Express 'te kullanılamayan proje şablonlarını kullanabilir.

## <a name="profiles-and-authentication"></a>*Profiller ve kimlik doğrulaması*

Microsoft ASP.NET profilleri ve kimlik doğrulama hizmetleri, ASP.NET Forms kimlik doğrulama sistemi tarafından sağlanır ve ASP.NET standart bileşenleridir. ASP.NET AJAX Uzantıları, istemci AJAX kitaplığının sys. Services ad alanı altındaki oldukça kolay bir model aracılığıyla betik proxy 'leri aracılığıyla bu hizmetlere betik erişimi sağlar.

Kimlik doğrulama hizmeti, kullanıcıların bir kimlik doğrulama tanımlama bilgisi almak için kimlik bilgilerini sağlamasına olanak sağlar ve ASP.NET tarafından sağlanmış özel kullanıcı profillerine izin veren ağ geçidi hizmetidir. ASP.NET AJAX kimlik doğrulama hizmeti, standart ASP.NET Forms kimlik doğrulamasıyla uyumludur. bu nedenle, şu anda Forms kimlik doğrulaması kullanan uygulamalar (örneğin, oturum açma denetimiyle) AJAX kimlik doğrulama hizmetine yükseltilerek kesilmeyecektir.

Profil hizmeti, kimlik doğrulama hizmeti tarafından sağlandığı şekilde üyelik tabanlı kullanıcı verilerinin otomatik olarak tümleştirilmesini ve depolanmasını sağlar. Depolanan veriler Web. config dosyası tarafından belirtilir ve çeşitli profil oluşturma hizmeti sağlayıcıları veri yönetimini işler. Kimlik doğrulama hizmetinde olduğu gibi, AJAX profili hizmeti standart ASP.NET Profil hizmetiyle uyumludur. böylece, şu anda ASP.NET profil hizmeti özelliklerini içeren sayfaların, AJAX desteği dahil ederek kesilmemelidir.

ASP.NET kimlik doğrulaması ve profil oluşturma hizmetlerini bir uygulamaya eklemek, bu teknik açıklamanın kapsamı dışındadır. Konu hakkında daha fazla bilgi için, [https://msdn.microsoft.com/library/tw292whz.aspx](https://msdn.microsoft.com/library/tw292whz.aspx)üyelik kullanarak kullanıcıları yönetme başlıklı MSDN Kitaplığı başvuru makalesine bakın. ASP.NET ayrıca, ASP.NET üyeliği için varsayılan kimlik doğrulama hizmeti sağlayıcısı olan SQL Server üyeliği otomatik olarak ayarlamaya yönelik bir yardımcı program içerir. Daha fazla bilgi için [https://msdn.microsoft.com/library/ms229862(vs.80).aspx](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)adresindeki ASP.NET SQL Server kayıt aracı (ASPNET\_regsql. exe) makalesine bakın.

## <a name="using-the-aspnet-ajax-authentication-service"></a>*ASP.NET AJAX kimlik doğrulama hizmeti 'ni kullanma*

ASP.NET AJAX kimlik doğrulama hizmetinin Web. config dosyasında etkinleştirilmesi gerekir:

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample1.xml)]

Kimlik doğrulama hizmeti, ASP.NET Forms kimlik doğrulamasının etkinleştirilmesini ve istemci tarayıcısında tanımlama bilgilerinin etkinleştirilmesini gerektirir (bir betik, kimlik doğrulama olmayan oturumlar URL parametreleri gerektirdiğinden bir komut dosyası tanımlama bilgisi olmayan bir oturumu etkinleştiremez).

AJAX kimlik doğrulama hizmeti etkinleştirildikten ve yapılandırıldıktan sonra, istemci betiği sys. Services. AuthenticationService nesnesinden hemen yararlanabilir. Öncelikle, istemci betiği `login` yönteminden ve `isLoggedIn` özelliğinden faydalanmak ister. Çok sayıda parametreyi kabul edebilecek oturum açma yöntemi için varsayılanlar sağlamak üzere çeşitli özellikler mevcuttur.

*Sys. Services. AuthenticationService üyeleri*

*oturum açma yöntemi:*

Login () yöntemi kullanıcının kimlik bilgilerini doğrulamak için bir istek başlatır. Bu yöntem zaman uyumsuzdur ve yürütmeyi engellemez.

*Parametrelere*

| **Parametre adı** | **Anlamı** |
| --- | --- |
| userName adı | Gerekli. Kimlik doğrulaması yapılacak Kullanıcı adı. |
| password | İsteğe bağlı (varsayılan olarak null değerini alır). Kullanıcının parolası. |
| IsPersistent | İsteğe bağlı (varsayılan olarak false olur). Kullanıcının kimlik doğrulama tanımlama bilgisinin oturumlarda kalıcı olması gerekip gerekmediğini belirtir. Yanlış ise, tarayıcı kapandığında veya oturum sona erdiğinde Kullanıcı oturumu kapatılır. |
| redirectUrl | İsteğe bağlı (varsayılan olarak null değerini alır). Başarılı kimlik doğrulamasından sonra tarayıcının yönlendirileceği URL. Bu parametre null veya boş bir dize ise, yeniden yönlendirme gerçekleşmez. |
| Custoınfo | İsteğe bağlı (varsayılan olarak null değerini alır). Bu parametre Şu anda kullanılmıyor ve gelecekte kullanılmak üzere ayrılmıştır. |
| loginCompletedCallback | İsteğe bağlı (varsayılan olarak null değerini alır). Oturum açma başarıyla tamamlandığında çağrılacak işlev. Belirtilmişse, bu parametre defaultLoginCompleted özelliğini geçersiz kılar. |
| failedCallback | İsteğe bağlı (varsayılan olarak null değerini alır). Oturum açma işlemi başarısız olduğunda çağrılacak işlev. Belirtilmişse, bu parametre defaultFailedCallback özelliğini geçersiz kılar. |
| userContext | İsteğe bağlı (varsayılan olarak null değerini alır). Geri çağırma işlevlerine geçirilmesi gereken özel kullanıcı bağlamı verileri. |

*Dönüş değeri:*

Bu işlev bir dönüş değeri içermez. Ancak, bu işleve yapılan çağrının tamamlanmasından sonra bir dizi davranış dahil edilir:

- Geçerli sayfa, `redirectUrl` parametresi null ya da boş bir dize değilse yenilenir veya değiştirilir.
- Ancak, parametre null veya boş bir dize ise, `loginCompletedCallback` parametresi veya `defaultLoginCompletedCallback` özelliği çağırılır.
- Web hizmetine yapılan çağrı başarısız olursa, `defaultFailedCallback` özelliğinin `failedCallback` parametresi çağırılır.

*oturum kapatma yöntemi:*

Logout () yöntemi, kimlik bilgilerini kaldırır ve geçerli kullanıcıyı Web uygulamasından günlüğe kaydeder.

*Parametrelere*

| **Parametre adı** | **Anlamı** |
| --- | --- |
| redirectUrl | İsteğe bağlı (varsayılan olarak null değerini alır). Başarılı kimlik doğrulamasından sonra tarayıcının yönlendirileceği URL. Bu parametre null veya boş bir dize ise, yeniden yönlendirme gerçekleşmez. |
| logoutCompletedCallback | İsteğe bağlı (varsayılan olarak null değerini alır). Oturumu kapatma başarıyla tamamlandığında çağrılacak işlev. Belirtilmişse, bu parametre defaultLogoutCompleted özelliğini geçersiz kılar. |
| failedCallback | İsteğe bağlı (varsayılan olarak null değerini alır). Oturum açma işlemi başarısız olduğunda çağrılacak işlev. Belirtilmişse, bu parametre defaultFailedCallback özelliğini geçersiz kılar. |
| userContext | İsteğe bağlı (varsayılan olarak null değerini alır). Geri çağırma işlevlerine geçirilmesi gereken özel kullanıcı bağlamı verileri. |

*Dönüş değeri:*

Bu işlev bir dönüş değeri içermez. Ancak, bu işleve yapılan çağrının tamamlanmasından sonra bir dizi davranış dahil edilir:

- Geçerli sayfa, `redirectUrl` parametresi null ya da boş bir dize değilse yenilenir veya değiştirilir.
- Ancak, parametre null veya boş bir dize ise, `logoutCompletedCallback` parametresi veya `defaultLogoutCompletedCallback` özelliği çağırılır.
- Web hizmetine yapılan çağrı başarısız olursa, `defaultFailedCallback` özelliğinin `failedCallback` parametresi çağırılır.

*defaultFailedCallback özelliği (Get, set):*

Bu özellik, Web hizmetiyle iletişim kurma hatası oluşursa, çağrılması gereken bir işlevi belirtir. Bir temsilci (veya işlev başvurusu) almalıdır.

Bu özellik tarafından belirtilen işlev başvurusu aşağıdaki imzaya sahip olmalıdır:

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample2.js)]

*Parametrelere*

| **Parametre adı** | **Anlamı** |
| --- | --- |
| error | Hata bilgilerini belirtir. |
| userContext | Login veya Logout işlevi çağrıldığında belirtilen kullanıcı bağlamı bilgilerini belirtir. |
| MethodName | Çağıran yöntemin adı. |

*defaultLoginCompletedCallback özelliği (Get, set):*

Bu özellik, oturum açma Web hizmeti çağrısı tamamlandığında çağrılması gereken bir işlevi belirtir. Bir temsilci (veya işlev başvurusu) almalıdır.

Bu özellik tarafından belirtilen işlev başvurusu aşağıdaki imzaya sahip olmalıdır:

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample3.js)]

*Parametrelere*

| **Parametre adı** | **Anlamı** |
| --- | --- |
| validCredentials | Kullanıcının geçerli kimlik bilgileri sağlamadığını belirtir. Kullanıcı başarıyla oturum açtıysa `true`; Aksi takdirde `false`. |
| userContext | Oturum açma işlevi çağrıldığında verilen kullanıcı bağlamı bilgilerini belirtir. |
| MethodName | Çağıran yöntemin adı. |

*defaultLogoutCompletedCallback özelliği (Get, set):*

Bu özellik, Logout Web hizmeti çağrısı tamamlandığında çağrılması gereken bir işlevi belirtir. Bir temsilci (veya işlev başvurusu) almalıdır.

Bu özellik tarafından belirtilen işlev başvurusu aşağıdaki imzaya sahip olmalıdır:

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample4.js)]

*Parametrelere*

| **Parametre adı** | **Anlamı** |
| --- | --- |
| Sonuç | Bu parametre her zaman `null`olacaktır; gelecekte kullanılmak üzere ayrılmıştır. |
| userContext | Oturum açma işlevi çağrıldığında verilen kullanıcı bağlamı bilgilerini belirtir. |
| MethodName | Çağıran yöntemin adı. |

*IsLoggedIn özelliği (Get):*

Bu özellik kullanıcının geçerli kimlik doğrulama durumunu alır; sayfa isteği sırasında ScriptManager nesnesi tarafından ayarlanır.

Kullanıcı oturum açmışsa, bu özellik `true` döndürür; Aksi takdirde, `false`döndürür.

*Path Özelliği (Get, set):*

Bu özellik, kimlik doğrulama Web hizmetinin konumunu programlı bir şekilde belirler. Varsayılan kimlik doğrulama sağlayıcısını geçersiz kılmak için ve ScriptManager denetiminin AuthenticationService alt düğümünün Path özelliğinde bildirimli olarak bir küme oluşturulabilir (daha fazla bilgi için bkz. özel kimlik doğrulama hizmeti sağlayıcısı kullanma Konu başlığı altında).

Varsayılan kimlik doğrulama hizmeti konumunun değişmediğini unutmayın. Ancak, ASP.NET AJAX, ASP.NET AJAX kimlik doğrulama hizmeti proxy 'si ile aynı sınıf arabirimini sağlayan bir Web hizmetinin konumunu belirtmenize olanak tanır.

Ayrıca, bu özelliğin komut dosyası isteğini geçerli sitede yönlendiren bir değere ayarlanmamış olması gerektiğini unutmayın. Geçerli uygulama kimlik doğrulama kimlik bilgilerini almadığı için, bu işe yaramaz; Ayrıca, temel alınan AJAX, siteler arası istekleri nakletmemelidir ve istemci tarayıcısında bir güvenlik özel durumu oluşturabilir.

Bu özellik, kimlik doğrulama Web hizmetinin yolunu temsil eden bir `String` nesnesidir.

*Timeout Özelliği (Get, set):*

Bu özellik, oturum açma isteği başarısız olmadan önce kimlik doğrulama hizmeti için beklenecek sürenin uzunluğunu belirler. Çağrının tamamlanması beklenirken zaman aşımı süresi dolarsa, istek başarısız geri arama çağrılır ve çağrı tamamlanmaz.

Bu özellik, kimlik doğrulama hizmetinden sonuçların bekleyeceği milisaniye sayısını temsil eden bir `Number` nesnesidir.

*Kod örneği: kimlik doğrulama hizmetinde oturum açma*

Aşağıdaki biçimlendirme, AuthenticationService sınıfının oturum açma ve oturum kapatma yöntemlerine basit bir betik çağrısıyla örnek bir ASP.NET sayfasıdır.

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample5.aspx)]

## <a name="accessing-aspnet-profiling-data-via-ajax"></a>AJAX aracılığıyla ASP.NET profil oluşturma verilerine erişme

ASP.NET profil oluşturma hizmeti Ayrıca ASP.NET AJAX uzantıları aracılığıyla da sunulur. ASP.NET profil oluşturma hizmeti, Kullanıcı verilerini depolamak ve almak için zengin ve ayrıntılı bir API sağladığından, bu harika bir üretkenlik aracı olabilir.

Profil hizmetinin Web. config dosyasında etkinleştirilmesi gerekir; Varsayılan olarak değildir. Bunu yapmak için, `profileService` alt öğesinin etkinleştirildiğinden emin olun = Web. config dosyasında belirtilen ve hangi özelliklerin okunabilmesi veya yazılamayacağını belirtdiğinizden emin olun:

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample6.xml)]

Profil hizmetinin de yapılandırılması gerekir. Profil oluşturma hizmeti yapılandırması bu teknik incelemeye ait kapsamın dışında olsa da, profil yapılandırma ayarları ' nda tanımlanan gruplar grup adının alt özellikleri olarak erişilebilecektir. Örneğin, aşağıdaki profil bölümü belirtildi:

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample7.xml)]

İstemci betiği ad, adres. Satır1, Address. Satır2, Address. City, Address. State, Address. zip ve BackgroundColor ' i ProfileService sınıfının Özellikler alanının özellikleri olarak erişebilecek.

AJAX profil oluşturma hizmeti yapılandırıldıktan sonra, sayfada hemen kullanılabilir olur; Ancak, kullanılmadan önce bir kez yüklenmesi gerekir.

*Sys. Services. ProfileService üyeleri*

*Özellikler alanı:*

Özellikler alanı, tüm yapılandırılmış profil verilerini, nokta operatörü ad kuralı tarafından başvurulabilen alt özellikler olarak kullanıma sunar. Özellik gruplarının alt öğeleri olan özellikler GroupName. PropertyName olarak adlandırılır. Yukarıda sunulan örnek profil yapılandırmasında, kullanıcının durumunu almak için aşağıdaki tanımlayıcıyı kullanabilirsiniz:

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample8.cs)]

*yükleme yöntemi:*

Sunucudan seçilen bir listeyi veya tüm özellikleri yükler.

*Parametrelere*

| **Parametre adı** | **Anlamı** |
| --- | --- |
| propertyNames | İsteğe bağlı (varsayılan olarak null değerini alır). Sunucudan yüklenecek Özellikler. |
| loadCompletedCallback | İsteğe bağlı (varsayılan olarak null değerini alır). Yükleme tamamlandığında çağrılacak işlev. |
| failedCallback | İsteğe bağlı (varsayılan olarak null değerini alır). Bir hata oluşursa çağrılacak işlev. |
| userContext | İsteğe bağlı (varsayılan olarak null değerini alır). Geri çağırma işlevine geçirilecek bağlam bilgileri. |

Load işlevinin dönüş değeri yok. Çağrı başarıyla tamamlanırsa, `loadCompletedCallback` parametresi ya da `defaultLoadCompletedCallback` özelliğini çağırır. Çağrı başarısız olursa ya da zaman aşımı süresi dolmuşsa, `failedCallback` parametresi veya `defaultFailedCallback` özelliği çağrılacaktır.

`propertyNames` parametresi sağlanmazsa, tüm okuma yapılandırılmış özellikler sunucudan alınır.

*yöntemi Kaydet:*

Save () yöntemi, belirtilen özellik listesini (veya tüm özellikleri) kullanıcının ASP.NET profiline kaydeder.

*Parametrelere*

| **Parametre adı** | **Anlamı** |
| --- | --- |
| propertyNames | İsteğe bağlı (varsayılan olarak null değerini alır). Sunucuya kaydedilecek Özellikler. |
| saveCompletedCallback | İsteğe bağlı (varsayılan olarak null değerini alır). Kaydetme tamamlandığında çağrılacak işlev. |
| failedCallback | İsteğe bağlı (varsayılan olarak null değerini alır). Bir hata oluşursa çağrılacak işlev. |
| userContext | İsteğe bağlı (varsayılan olarak null değerini alır). Geri çağırma işlevine geçirilecek bağlam bilgileri. |

Save işlevinin dönüş değeri yok. Çağrı başarıyla tamamlanırsa, `saveCompletedCallback` parametresi ya da `defaultSaveCompletedCallback` özelliğini çağırır. Çağrı başarısız olursa ya da zaman aşımı süresi dolmuşsa, `failedCallback` veya `defaultFailedCallback` özelliği çağrılacaktır.

`propertyNames` parametresi null ise, tüm profil özellikleri sunucuya gönderilir ve sunucu hangi özelliklerin kaydedileceğine ve bu işlem gerçekleştirilemez.

*defaultFailedCallback özelliği (Get, set):*

Bu özellik, Web hizmetiyle iletişim kurma hatası oluşursa, çağrılması gereken bir işlevi belirtir. Bir temsilci (veya işlev başvurusu) almalıdır.

Bu özellik tarafından belirtilen işlev başvurusu aşağıdaki imzaya sahip olmalıdır:

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample9.js)]

*Parametrelere*

| **Parametre adı** | **Anlamı** |
| --- | --- |
| Hata | Hata bilgilerini belirtir. |
| userContext | Load veya Save işlevi çağrıldığında verilen kullanıcı bağlamı bilgilerini belirtir. |
| MethodName | Çağıran yöntemin adı. |

*defaultSaveCompleted özelliği (Get, set):*

Bu özellik, kullanıcının profil verilerini kaydetme işleminin tamamlanmasından sonra çağrılması gereken bir işlevi belirtir. Bir temsilci (veya işlev başvurusu) almalıdır.

Bu özellik tarafından belirtilen işlev başvurusu aşağıdaki imzaya sahip olmalıdır:

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample10.js)]

*Parametrelere*

| **Parametre adı** | **Anlamı** |
| --- | --- |
| numPropsSaved | Kaydedilen özelliklerin sayısını belirtir. |
| userContext | Load veya Save işlevi çağrıldığında verilen kullanıcı bağlamı bilgilerini belirtir. |
| MethodName | Çağıran yöntemin adı. |

*defaultLoadCompleted özelliği (Get, set):*

Bu özellik, kullanıcının profil verilerinin yüklenmesi tamamlandıktan sonra çağrılması gereken bir işlevi belirtir. Bir temsilci (veya işlev başvurusu) almalıdır.

Bu özellik tarafından belirtilen işlev başvurusu aşağıdaki imzaya sahip olmalıdır:

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample11.js)]

*Parametrelere*

| **Parametre adı** | **Anlamı** |
| --- | --- |
| numPropsLoaded | Yüklenen özelliklerin sayısını belirtir. |
| userContext | Load veya Save işlevi çağrıldığında verilen kullanıcı bağlamı bilgilerini belirtir. |
| MethodName | Çağıran yöntemin adı. |

*Path Özelliği (Get, set):*

Bu özellik program aracılığıyla profil Web hizmetinin konumunu belirler. Varsayılan profil hizmeti sağlayıcısını geçersiz kılmak için ve ScriptManager denetiminin ProfileService alt düğümünün Path özelliğinde bildirimli olarak bir küme oluşturulabilir.

Varsayılan profil hizmeti konumunun değişmediğini unutmayın. Ancak, ASP.NET AJAX, ASP.NET AJAX kimlik doğrulama hizmeti proxy 'si ile aynı sınıf arabirimini sağlayan bir Web hizmetinin konumunu belirtmenize olanak tanır.

Ayrıca, bu özelliğin komut dosyası isteğini geçerli sitede yönlendiren bir değere ayarlanmamış olması gerektiğini unutmayın. Teknoloji temelindeki AJAX, siteler arası istekleri nakletmemelidir ve istemci tarayıcısında bir güvenlik özel durumu oluşturabilir.

Bu özellik, profil Web hizmetinin yolunu temsil eden bir `String` nesnesidir.

*Timeout Özelliği (Get, set):*

Bu özellik, yükleme veya kaydetme isteğinin başarısız olduğunu varsaymadan önce profil hizmeti için beklenecek sürenin uzunluğunu belirler. Çağrının tamamlanması beklenirken zaman aşımı süresi dolarsa, istek başarısız geri arama çağrılır ve çağrı tamamlanmaz.

Bu özellik, profil hizmetinden sonuçların bekleyeceği milisaniye sayısını temsil eden bir `Number` nesnesidir.

*Kod örneği: sayfa yüklemesinde profil verileri yükleme*

Aşağıdaki kod, bir kullanıcının kimlik doğrulamasının yapılıp yapılmayacağını ve bu durumda kullanıcının tercih edilen arka plan rengini sayfa olarak yükleyip yükleyemeyeceğini denetler.

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample12.js)]

## <a name="using-a-custom-authentication-service-provider"></a>*Özel bir kimlik doğrulama hizmeti sağlayıcısı kullanma*

ASP.NET AJAX Uzantıları, özel bir Web hizmeti aracılığıyla işlevselliklerinizi açığa çıkarmak için özel bir betik kimlik doğrulama hizmet sağlayıcısı oluşturmanıza olanak sağlar. Web hizmetiniz, kullanılmak üzere iki yöntemi kullanıma sunmalıdır, `Login` ve `Logout`; Bu yöntemlerin varsayılan ASP.NET AJAX kimlik doğrulama Web hizmeti ile aynı yöntem imzaları ile belirtilmesi gerekir.

Özel Web hizmetini oluşturduktan sonra, bu yolun yolunu, kod içinde program aracılığıyla ya da istemci betiği aracılığıyla sayfanızda bildirimli olarak belirtmeniz gerekir.

*Yolu bildirimli olarak ayarlamak için:*

Yolu bildirimli olarak ayarlamak için, ASP.NET sayfanıza ScriptManager nesnesinin AuthenticationService alt öğesini ekleyin:

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample13.aspx)]

*Koddaki yolu ayarlamak için:*

Yolu programlı olarak ayarlamak için, komut dosyası yöneticinizin örneği aracılığıyla yolu belirtin:

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample14.cs)]

*Komut dosyasında yolu ayarlamak için:*

Komut dosyasında program aracılığıyla yolu ayarlamak için AuthenticationService sınıfının `path` özelliğini kullanın:

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample15.js)]

*Özel kimlik doğrulaması için örnek Web hizmeti*

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample16.aspx)]

## <a name="summary"></a>Özet

ASP.NET Services-özellikle profil oluşturma, üyelik ve kimlik doğrulama hizmetleri, istemci tarayıcısında JavaScript 'e kolayca sunulur. Bu, geliştiricilerin, yoğun kaldırma işlemini yapmak için UpdatePanel gibi denetimlere bağlı kalmadan, istemci tarafı kodlarını kimlik doğrulama mekanizmasıyla sorunsuz bir şekilde tümleştirmelerini sağlar. Profil verileri, Web yapılandırma ayarları kullanılarak istemciden da korunabilir; Varsayılan olarak kullanılabilir veri yoktur ve geliştiricilerin profil özelliklerini kabul etmelidir.

Ayrıca, benzer yöntem imzaları ile basitleştirilmiş Web hizmeti uygulamaları oluşturarak, geliştiriciler bu iç ASP.NET Hizmetleri için özel betik sağlayıcıları oluşturabilir. Bu teknikler için destek, zengin istemci uygulamalarının geliştirilmesini basitleştirir ve geliştiricilere belirli ihtiyaçları karşılamak için çok çeşitli esneklik sağlar.

## <a name="bio"></a>*Biyografisi*

Scott, 1997 tarihinden itibaren Microsoft Web teknolojileriyle çalışmaktadır ve Bilgi Bankası yazılım çözümlerine odaklanmış ASP.NET tabanlı uygulamalar yazma konusunda uzmanımız myKB.com ([www.myKB.com](http://www.myKB.com)) Başkan Yardımcısı. Scott 'da e-posta ile [scott.cate@myKB.com](mailto:scott.cate@myKB.com) veya blogundan [ScottCate.com](http://ScottCate.com) adresinden iletişim kurulabilirler

> [!div class="step-by-step"]
> [Önceki](understanding-asp-net-ajax-updatepanel-triggers.md)
> [İleri](understanding-asp-net-ajax-localization.md)
