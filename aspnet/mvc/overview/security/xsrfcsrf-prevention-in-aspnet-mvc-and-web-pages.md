---
uid: mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages
title: ASP.NET MVC ve Web sayfalarında XSRF/CSRF önleme | Microsoft Docs
author: Rick-Anderson
description: Siteler arası istek sahteciliği (XSRF veya CSRF olarak da bilinir), kötü amaçlı bir Web sitesinin ınteracti 'yi etkileyebilecek Web 'de barındırılan uygulamalara karşı bir saldırıya karşı bir saldırıdır...
ms.author: riande
ms.date: 03/14/2013
ms.assetid: aadc5fa4-8215-4fc7-afd5-bcd2ef879728
msc.legacyurl: /mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages
msc.type: authoredcontent
ms.openlocfilehash: 1965063a9b613d0e2857cddcc2165f5fda64ec0c
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455535"
---
# <a name="xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages"></a>ASP.NET MVC ve Web Sayfalarında XSRF/CSRF Önleme

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> Siteler arası istek sahteciliği (XSRF veya CSRF olarak da bilinir), kötü amaçlı bir Web sitesinin bir istemci tarayıcısı ile bu tarayıcı tarafından güvenilen bir Web sitesi arasındaki etkileşimi etkileyebilecek Web 'de barındırılan uygulamalara karşı bir saldırıya karşı bir saldırıdır. Web tarayıcıları her bir Web sitesi isteğiyle otomatik olarak kimlik doğrulama belirteçleri gönderebileceğinden, bu saldırılar mümkün hale getirilir. Kurallı örnek, ASP gibi bir kimlik doğrulama tanımlama bilgisidir. NET ' in Forms kimlik doğrulama bileti. Ancak, herhangi bir kalıcı kimlik doğrulama mekanizması (örneğin, Windows kimlik doğrulaması, temel vb.) kullanan Web siteleri bu saldırılar tarafından hedeflenebilir.
> 
> Bir XSRF saldırısı, kimlik avı saldırısından farklıdır. Sızdırma saldırıları, kurban 'ten etkileşim gerektirir. Bir sızdırma saldırısında, kötü amaçlı bir Web sitesi hedef Web sitesini taklit eder ve kurban, saldırgana duyarlı bilgiler sağlamaya çalışır. Bir XSRF saldırısında, genellikle kurban için gereken bir etkileşim yoktur. Bunun yerine saldırgan, tüm ilgili tanımlama bilgilerini hedef Web sitesine otomatik olarak göndererek tarayıcıya bağlı olur.
> 
> Daha fazla bilgi için [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page)(OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))bölümüne bakın.

## <a name="anatomy-of-an-attack"></a>Bir saldırının anatomumu

Bir XSRF saldırısında gezinmek için, bazı çevrimiçi bankacılık işlemlerini gerçekleştirmek isteyen bir kullanıcıyı göz önünde bulundurun. Bu Kullanıcı, içindeki WoodgroveBank.com ve günlükleri ilk kez ziyaret eder; bu noktada yanıt üst bilgisi kimlik doğrulama tanımlama bilgisini içerir:

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample1.cmd)]

Kimlik doğrulama tanımlama bilgisi bir oturum tanımlama bilgisi olduğundan, tarayıcı işlemi çıktığında tarayıcı tarafından otomatik olarak temizlenir. Ancak, bu zamana kadar tarayıcı otomatik olarak her bir WoodgroveBank.com isteğine sahip tanımlama bilgisini dahil eder. Kullanıcı şimdi başka bir hesaba $1000 aktarmak istiyor, bu nedenle bankacılık sitesinde bir form doldurmuş ve tarayıcı bu isteği sunucuya getiriyor:

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample2.cmd)]

Bu işlemin bir yan etkisi olduğundan (parasal bir işlem başlatır), bu işlemi başlatmak için bankacılık sitesi bir HTTP POST gerektirmesini seçti. Sunucu, istekten kimlik doğrulama belirtecini okur, geçerli kullanıcının hesap numarasını arar, yeterli fon olduğunu doğrular ve ardından işlemi hedef hesaba başlatır.

Çevrimiçi bankacılık tamamlanmıştır, Kullanıcı bankacılık sitesinden uzaklaştırabilir ve Web 'deki diğer konumları ziyaret ettiğinde. Bu sitelerden biri – fabrikam.com – &lt;iframe&gt;eklenmiş bir sayfada aşağıdaki biçimlendirmeyi içerir:

[!code-html[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample3.html)]

Böylece tarayıcının bu isteği yapmasına neden olur:

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample4.cmd)]

Saldırgan, kullanıcının hedef Web sitesi için geçerli bir kimlik doğrulama belirtecine sahip olabileceği ve tarayıcının hedef siteye otomatik olarak bir HTTP POST işlemi yapmasını sağlamak için küçük bir JavaScript kod parçacığı kullanmakta olduğundan emin olmaya başlamıştır. Kimlik doğrulama belirteci hala geçerliyse, bankacılık sitesi, saldırganın tercih ettiği hesaba $250 aktarımını başlatır.

### <a name="ineffective-mitigations"></a>Etkisiz azaltmaları

Yukarıdaki senaryoda, WoodgroveBank.com 'in SSL aracılığıyla erişildiği ve saldırı için yalnızca bir SSL kimlik doğrulama tanımlama bilgisinin yetersiz olduğunu düşündüğüne dikkat edin. Saldırgan, &lt;form&gt; öğesinde [URI şeması](http://en.wikipedia.org/wiki/URI_scheme) (https) belirtebilir ve bu tanımlama bilgileri amaçlanan hedefin URI şeması ile tutarlı olduğu sürece tarayıcı, geçerliliği olmayan tanımlama bilgilerini hedef siteye göndermeye devam edecektir.

Yalnızca güvenilen siteleri ziyaret etmek, güvenli çevrimiçi olmaya yardımcı olduğundan, Kullanıcı yalnızca güvenilmeyen siteleri ziyaret etmemelidir. Bunun için bazı gerçeği vardır, ancak bu öneri her zaman pratik değildir. Belki de Kullanıcı, yerel haber sitesi ConsolidatedMessenger "güvenir". ConsolidatedMessenger.com ve bunun yerine bu siteyi ziyaret edin, ancak bu sitede, bir saldırganın fabrikam.com üzerinde çalışan aynı kod parçacığını eklemesine izin veren bir XSS Güvenlik açığı vardır.

Gelen isteklerin, etki alanına başvuran bir [Referer üst bilgisine](http://www.w3.org/Protocols/HTTP/HTRQ_Headers.html#z14) sahip olduğunu doğrulayabilirsiniz. Bu, bir üçüncü taraf etki alanından gönderilen isteklerin farkında olarak durdurulur. Bununla birlikte, bazı kullanıcılar tarayıcının Referer üst bilgisini gizlilik nedenleriyle devre dışı bırakır ve kurban bazı güvenli olmayan yazılımların yüklü olduğu durumlarda saldırganlar bu üstbilgiyi taklit edebilir. [Başvuru üst bilgisinin](http://www.w3.org/Protocols/HTTP/HTRQ_Headers.html#z14) DOĞRULANMASı, XSRF saldırılarını önlemek için güvenli bir yaklaşım olarak kabul edilmez.

## <a name="web-stack-runtime-xsrf-mitigations"></a>Web yığını çalışma zamanı XSRF azaltmaları

ASP.NET Web Stack çalışma zamanı, XSRF saldırılarına karşı savunmak için [Eşitleyici belirteç deseninin](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html#synchronizer-token-pattern) bir türevini kullanır. Eşitleyici belirteç deseninin genel formu, her HTTP gönderimiyle (kimlik doğrulama belirtecine ek olarak) sunucuya iki anti-XSRF belirtecinin gönderilmesinin yanı sıra, tanımlama bilgisi olarak bir belirteç ve diğeri de bir form değeri olarak oluşturulur. ASP.NET çalışma zamanı tarafından oluşturulan belirteç değerleri, bir saldırgan tarafından belirleyici veya öngörülebilir değildir. Belirteçler gönderildiğinde sunucu, isteğin yalnızca her iki belirteç de bir karşılaştırma denetimi iletmesine izin verir.

XSRF isteği doğrulama *oturum belirteci* bir http tanımlama bilgisi olarak depolanır ve şu anda yükünde şu bilgileri içerir:

- Rastgele bir 128 bit tanımlayıcısından oluşan bir güvenlik belirteci.   
 Aşağıdaki görüntüde, Internet Explorer F12 geliştirici araçları ile gösterilen XSRF isteği doğrulama oturum belirteci gösterilmektedir: (Bu, geçerli uygulama ve büyük olasılıkla, değişebilir, yani değiştirilebilir.)

![](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/_static/image1.png)

*Alan belirteci* bir `<input type="hidden" />` olarak depolanır ve yükünde aşağıdaki bilgileri içerir:

- Oturum açmış kullanıcının Kullanıcı adı (kimliği doğrulanmışsa).
- [Iantiforgeryadditionaldataprovider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx)tarafından sunulan ek veriler.

Anti-XSRF belirteçleri 'nin yükleri şifrelenir ve imzalanır, bu nedenle belirteçleri incelemek için araçları kullanırken kullanıcı adını görüntüleyemezsiniz. Web uygulaması ASP.NET 4,0 ' i hedeflerken, Şifreleme Hizmetleri [machineKey. Encode](https://msdn.microsoft.com/library/system.web.security.machinekey.encode.aspx) yordamı tarafından sağlanır. Web uygulaması ASP.NET 4,5 veya üstünü hedeflerken, şifreleme hizmetleri, daha iyi performans, genişletilebilirlik ve güvenlik sunan [machineKey. Protect](https://msdn.microsoft.com/library/system.web.security.machinekey.protect(v=vs.110)) yordamı tarafından sağlanır. Daha fazla ayrıntı için aşağıdaki blog gönderilerine bakın:

- [ASP.NET 4,5, pt. 1 ' de şifreleme geliştirmeleri](https://blogs.msdn.com/b/webdev/archive/2012/10/22/cryptographic-improvements-in-asp-net-4-5-pt-1.aspx)
- [ASP.NET 4,5, pt. 2 ' de şifreleme geliştirmeleri](https://blogs.msdn.com/b/webdev/archive/2012/10/23/cryptographic-improvements-in-asp-net-4-5-pt-2.aspx)
- [ASP.NET 4,5, pt. 3 ' te şifreleme geliştirmeleri](https://blogs.msdn.com/b/webdev/archive/2012/10/24/cryptographic-improvements-in-asp-net-4-5-pt-3.aspx)

## <a name="generating-the-tokens"></a>Belirteçleri oluşturma

Anti-XSRF belirteçlerini oluşturmak için bir MVC görünümünden [@Html.AntiForgeryToken](https://msdn.microsoft.com/library/dd470175.aspx) yöntemini veya Razor sayfasından @AntiForgery.GetHtml() çağırın. Çalışma zamanı daha sonra aşağıdaki adımları gerçekleştirir:

1. Geçerli HTTP isteği zaten bir anti-xsrf oturum belirteci içeriyorsa (\_Requestdoğrulamaları Icationtoken \_Anti-XSRF Cookie), güvenlik belirteci bundan ayıklanır. HTTP isteği bir anti-XSRF oturum belirteci içermiyorsa veya güvenlik belirtecinin ayıklanması başarısız olursa, yeni bir rastgele Anti-XSRF belirteci oluşturulur.
2. Bir anti-XSRF alan belirteci, yukarıdaki adım (1) ve oturum açmış geçerli kullanıcının kimliği kullanılarak oluşturulur. (Kullanıcı kimliğini belirleme hakkında daha fazla bilgi için aşağıdaki **[özel desteğe sahip senaryolar](#_Scenarios_with_special)** bölümüne bakın.) Ek olarak, bir [ıantiforgeryadditionaldataprovider](https://msdn.microsoft.com/library/jj158328(v=vs.111).aspx) yapılandırıldıysa, çalışma zamanı, [Getaddıtionaldata](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider.getadditionaldata(v=vs.111).aspx) metodunu çağırır ve döndürülen dizeyi alan belirtecine dahil eder. (Daha fazla bilgi için **[yapılandırma ve genişletilebilirlik](#_Configuration_and_extensibility)** bölümüne bakın.)
3. Adımda (1) yeni bir anti-XSRF belirteci oluşturulduysa, bunu içerecek yeni bir oturum belirteci oluşturulur ve giden HTTP tanımlama bilgileri koleksiyonuna eklenecektir. Adımdaki alan belirteci (2) bir `<input type="hidden" />` öğesinde Sarmalanacak ve bu HTML biçimlendirmesi `Html.AntiForgeryToken()` veya `AntiForgery.GetHtml()`dönüş değeri olacaktır.

## <a name="validating-the-tokens"></a>Belirteçleri doğrulama

Geliştirici, gelen Anti-XSRF belirteçlerini doğrulamak için, MVC eyleminde veya denetleyicisinde bir [Validateantiforgeri belirteci](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(VS.108).aspx) özniteliği içerir ya da Razor sayfasından `@AntiForgery.Validate()` çağırır. Çalışma zamanı aşağıdaki adımları gerçekleştirir:

1. Gelen oturum belirteci ve alan belirteci okunurdur ve her birinden ayıklanan Anti-XSRF belirteci bulunur. Oluşturma yordamında, Anti-XSRF belirteçleri, adım (2) başına aynı olmalıdır.
2. Geçerli kullanıcının kimliği doğrulanırsa, Kullanıcı adı, alan belirtecinde depolanan Kullanıcı adı ile karşılaştırılır. Kullanıcı adları eşleşmelidir.
3. Bir [ıantiforgeryadditionaldataprovider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) yapılandırılmışsa, çalışma zamanı *validateadditionaldata* yöntemini çağırır. Yöntem, *true*Boole değerini döndürmelidir.

Doğrulama başarılı olursa, isteğin devam etmesini izin verilir. Doğrulama başarısız olursa, Framework bir *Httpantiforgero özel durumu*oluşturur.

## <a name="failure-conditions"></a>Hata koşulları

ASP.NET Web Stack Runtime v2 ile başlayarak, doğrulama sırasında oluşturulan tüm *Httpantiforgeri özel durumu* , neyin yanlış gittiğini belirten ayrıntılı bilgiler içerir. Şu anda tanımlı hata koşulları şunlardır:

- İstekte oturum belirteci veya form belirteci yok.
- Oturum belirteci veya form belirteci okunamaz durumda. Bunun en olası nedeni, ASP.NET Web Stack çalışma zamanının eşleşmeyen sürümlerini çalıştıran bir grup veya Web. config dosyasındaki &lt;machineKey&gt; öğesinin makineler arasında farklılık gösterir. Bu özel durumu, Anti-XSRF belirteci ile izinsiz değişiklik yaparak zorlamak için Fiddler gibi bir araç kullanabilirsiniz.
- Oturum belirteci ve alan belirteci takas edildi.
- Oturum belirteci ve alan belirteci eşleşmeyen güvenlik belirteçleri içeriyor.
- Alan belirteci içine katıştırılmış Kullanıcı adı, oturum açmış olan kullanıcının kullanıcı adıyla eşleşmiyor.
- *[Iantiforgeryadditionaldataprovider. ValidateAdditionalData](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider.validateadditionaldata(v=vs.111).aspx)* yöntemi *false*döndürdü.

Anti-XSRF tesisler, belirtecin oluşturulması veya doğrulanması sırasında de ek denetim gerçekleştirebilir ve bu denetimler sırasında oluşan başarısızlıklar özel durumlar oluşturulmasına neden olabilir. Daha fazla bilgi için bkz. [WIF/ACS/talepler tabanlı kimlik doğrulaması](#_WIF_ACS) ve **[yapılandırma ve genişletilebilirlik](#_Configuration_and_extensibility)** bölümleri.

<a id="_Scenarios_with_special"></a>

## <a name="scenarios-with-special-support"></a>Özel desteğe sahip senaryolar

### <a name="anonymous-authentication"></a>Anonim kimlik doğrulama

Anti-XSRF sistemi, anonim kullanıcılar için özel destek içerir. burada "anonim", *IIdentity. IsAuthenticated* özelliğinin *false*döndüğü bir kullanıcı olarak tanımlanmıştır. Senaryolar, oturum açma sayfasında (kullanıcının kimlik doğrulamasından önce) XSRF koruması sağlamayı ve uygulamanın kullanıcıları tanımlamak için *IIdentity* dışında bir mekanizma kullandığı özel kimlik doğrulama düzenlerini içerir.

Bu senaryoları desteklemek için, oturum ve alan belirteçlerinin 128 bitlik bir rastgele oluşturulmuş donuk tanımlayıcı olan bir güvenlik belirteci ile katıldığını geri çekin. Bu güvenlik belirteci, siteyi gezindiği için tek bir kullanıcının oturumunu izlemek üzere kullanılır, bu nedenle anonim bir tanımlayıcının amacını etkin bir şekilde sunar. Yukarıda açıklanan oluşturma ve doğrulama yordamlarının Kullanıcı adının yerine boş bir dize kullanılır.

<a id="_WIF_ACS"></a>

### <a name="wif--acs--claims-based-authentication"></a>WıF/ACS/talep tabanlı kimlik doğrulaması

Normal olarak, .NET Framework yerleşik olarak bulunan *IIdentity* sınıfları, belirli bir uygulama içinde belirli bir kullanıcıyı benzersiz şekilde tanımlamak için *IIdentity.Name* özelliği vardır. Örneğin, *FormsIdentity.Name* , üyelik veritabanında depolanan kullanıcı adını döndürür (bu veritabanına bağlı olarak tüm uygulamalar için benzersizdir), *WindowsIdentity.Name* kullanıcının etki alanı nitelikli kimliğini döndürür ve bu şekilde devam eder. Bu sistemler yalnızca kimlik doğrulaması sağlamaz; kullanıcılar da bir uygulamaya kullanıcıları *belirler* .

Diğer yandan talep tabanlı kimlik doğrulaması, belirli bir kullanıcıyı tanımlamayı gerektirmez. Bunun yerine, *ClaimsPrincipal* ve *ClaimsIdentity* türleri bir *talep* örnekleri kümesiyle ilişkilendirilir, burada ayrı talepler "18 + yıllık kullanım" veya "yönetici ise" olabilir. Kullanıcı tanımlı olmadığından, çalışma zamanı bu belirli kullanıcı için benzersiz bir tanımlayıcı olarak *ClaimsIdentity.Name* özelliğini kullanamaz. Takım, *ClaimsIdentity.Name* ' nin *null*döndüğü, kolay (görünen) bir ad döndürdüğü veya başka bir şekilde Kullanıcı için benzersiz bir tanımlayıcı olarak kullanılması uygun olmayan bir dize döndüren gerçek dünyada örnekleri gördünüz.

Talep tabanlı kimlik doğrulaması kullanan birçok dağıtım, belirli bir şekilde [Azure Access Control Service](https://msdn.microsoft.com/library/windowsazure/gg429786.aspx) (ACS) kullanıyor. ACS, geliştiricilerin tek tek *kimlik sağlayıcılarını* (ADFS, Microsoft hesap sağlayıcısı, Yahoo! gibi OpenID sağlayıcıları, vb.) yapılandırmasına izin verir ve kimlik sağlayıcıları *ad tanımlayıcılarını*döndürür. Bu ad tanımlayıcıları, e-posta adresi gibi kişisel olarak tanımlanabilir bilgiler (PII) içerebilir veya özel bir kişisel tanımlayıcı (PPıD) gibi anonim olabilir. Ne olursa olsun, kayıt düzeni (kimlik sağlayıcısı, ad tanımlayıcısı), siteye göz atarken belirli bir kullanıcı için uygun bir izleme belirteci görevi görirken, ASP.NET Web Stack çalışma zamanı, oluştururken Kullanıcı adının yerine kayıt kümesini kullanabilir ve Anti-XSRF alan belirteçleri doğrulanıyor. Kimlik sağlayıcısı ve ad tanımlayıcısı için belirli URI 'Ler şunlardır:

- `https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider`
- `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`

(daha fazla bilgi için bu [ACS belgesi sayfasına](https://msdn.microsoft.com/library/windowsazure/gg185971.aspx) bakın.)

Bir belirteci oluştururken veya doğrularken, ASP.NET Web Stack çalışma zamanı çalışma zamanında bu türlere bağlamayı dener:

- `Microsoft.IdentityModel.Claims.IClaimsIdentity, Microsoft.IdentityModel, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35` (WıF SDK Için).
- `System.Security.Claims.ClaimsIdentity` (.NET 4,5 Için).

Bu türler varsa ve geçerli kullanıcının *Iiiıdentity* bu türlerden birini uygularsa veya alt sınıflara alıyorsa, ANTI-XSRF tesisi belirteçleri oluştururken ve doğrularken Kullanıcı adının yerine (kimlik sağlayıcısı, ad tanımlayıcısı) kayıt düzeni kullanır. Böyle bir tanımlama grubu yoksa, istek, geliştirici ile ilgili belirli kimlik doğrulama mekanizmasını anlamak için anti-XSRF sisteminin nasıl yapılandırılacağı hakkında hata vererek başarısız olur. Daha fazla bilgi için **[yapılandırma ve genişletilebilirlik](#_Configuration_and_extensibility)** bölümüne bakın.

### <a name="oauth--openid-authentication"></a>OAuth/OpenID kimlik doğrulaması

Son olarak, Anti-XSRF özelliği OAuth veya OpenID kimlik doğrulaması kullanan uygulamalar için özel desteğe sahiptir. Bu destek buluşsal-tabanlıdır: geçerli *IIdentity.Name* http://veya https://ile başlıyorsa, Kullanıcı adı karşılaştırmaları varsayılan OrdinalIgnoreCase karşılaştırıcısı yerine bir sıra karşılaştırıcısı kullanılarak yapılır.

<a id="_Configuration_and_extensibility"></a>

## <a name="configuration-and-extensibility"></a>Yapılandırma ve genişletilebilirlik

Bazen, geliştiriciler Anti-XSRF oluşturma ve doğrulama davranışları üzerinde sıkı bir denetim isteyebilir. Örneğin, MVC ve Web sayfaları yardımcılarının yanıta HTTP tanımlama bilgilerini otomatik olarak eklemenin varsayılan davranışı istenmeyen bir durum değildir ve geliştirici belirteçleri başka bir yerde kalıcı hale getirmek isteyebilir. Bunun için yardımcı olacak iki API var:

`AntiForgery.GetTokens(string oldCookieToken, out string newCookieToken, out string formToken);`  
`AntiForgery.Validate(string cookieToken, string formToken);`

*GetTokens* metodu, mevcut bir xsrf isteği doğrulama oturum belirtecini (null olabilir) giriş olarak alır ve yenı bir xsrf isteği doğrulama oturumu belirteci ve alan belirteci olarak üretilir. Belirteçler, dekorasyonu olmadan yalnızca opak dizelerdir; *form belirteci* değeri, örnek bir &lt;girişi&gt; etiketine kaydırılmayacak. *Newbir ıetoken* değeri null olabilir; Bu durumda, *Oldpişirme ıetoken* değeri hala geçerlidir ve yeni yanıt tanımlama bilgisinin ayarlanması gerekmez. *GetToken* çağıranı, gerekli yanıt tanımlama bilgilerini kalıcı hale getirmekten veya gerekli biçimlendirme oluşturmaktan sorumludur; *GetTokens* metodu, bir yan etkisi olarak yanıtı değiştirmez. *Validate* yöntemi, gelen oturum ve alan belirteçlerini alır ve kendileri üzerinde belirtilen doğrulama mantığını çalıştırır.

### <a name="antiforgeryconfig"></a>AntiForgeryConfig

Geliştirici, uygulama\_Başlat ' dan Anti-XSRF sistemini yapılandırabilir. Yapılandırma programlı. Statik *Antiforgeryıconfig* türünün özellikleri aşağıda açıklanmıştır. Talepler kullanan çoğu kullanıcı, UniqueClaimTypeIdentifier özelliğini ayarlamak ister.

| **Özellik** | **Açıklama** |
| --- | --- |
| **AdditionalDataProvider** | Belirteç oluşturma sırasında ek veriler sağlayan ve belirteç doğrulama sırasında ek veriler tüketen bir [ıantiforgeryadditionaldataprovider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) . Varsayılan değer *null*. Daha fazla bilgi için, bkz. [ıantiforgeryadditionaldataprovider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) bölümü. |
| **Tanımlama bilgisi adı** | Anti-XSRF oturum belirtecini depolamak için kullanılan HTTP tanımlama bilgisinin adını sağlayan bir dize. Bu değer ayarlanmamışsa, uygulamanın dağıtılan sanal yoluna göre otomatik olarak bir ad oluşturulur. Varsayılan değer *null*. |
| **RequireSsl** | Anti-XSRF belirteçlerinin SSL ile güvenli bir kanaldan gönderilmesi gerekip gerekmediğini belirleyen bir Boole değeri. Bu değer *true*ise, otomatik olarak oluşturulan herhangi bir tanımlama bilgisi "güvenli" bayrak kümesine sahip olur ve SSL aracılığıyla gönderilmemiş bir istek içinden çağrılırsa, ANTI-XSRF API 'leri oluşturulur. Varsayılan değer *false*'dur. |
| **SuppressIdentityHeuristicChecks** | Anti-XSRF sisteminin, talep tabanlı kimlikler için desteğini devre dışı bırakıp bırakmayacağını belirleyen bir Boole değeri. Bu değer *true*ise sistem, *IIdentity.Name* 'in benzersiz bir Kullanıcı başına tanımlayıcı olarak kullanım için uygun olduğunu varsayar ve [WIF/ACS/talepler tabanlı kimlik doğrulama](#_WIF_ACS) bölümünde açıklandığı gibi özel durum *ıımsıdentity* veya *clclaimsıdentity* ' yi denemeyecektir. Varsayılan değer: `false`. |
| **UniqueClaimTypeIdentifier** | Hangi talep türünün benzersiz kullanıcı başına tanımlayıcı olarak kullanım için uygun olduğunu gösteren bir dize. Bu değer ayarlandıysa ve geçerli *ıidentity* , talepler tabanlıysa, sistem *UniqueClaimTypeIdentifier*tarafından belirtilen türden bir talebi ayıklamayı dener ve alan belirtecini oluştururken kullanıcının Kullanıcı adı yerine ilgili değer kullanılır. Talep türü bulunamazsa, sistem isteği başarısız olur. Varsayılan değer, sistemin Kullanıcı Kullanıcı adının yerine daha önce açıklanan (kimlik sağlayıcısı, ad tanımlayıcısı) kayıt kümesini kullanması gerektiğini belirten *null*değeridir. |

<a id="_IAntiForgeryAdditionalDataProvider"></a>

### <a name="iantiforgeryadditionaldataprovider"></a>IAntiForgeryAdditionalDataProvider

*[Iantiforgeryadditionaldataprovider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx)* türü, geliştiricilerin, her bir belirteçte ek verilere gidiş dönüşü yaparak ANTI-XSRF sisteminin davranışını genişletmesini sağlar. *Getaddıtionaldata* yöntemi, bir alan belirtecinin oluşturulduğu her seferinde çağrılır ve döndürülen değer oluşturulan belirtecin içine gömülür. Bir uygulayıcının Bu yöntemden bir zaman damgası, nonce veya başka bir değer döndürmesi olabilir.

Benzer şekilde, *Validateadditionaldata* yöntemi, bir alan belirteci doğrulandığında her seferinde çağrılır ve belirtece gömülü olan "ek veriler" dizesi yöntemine geçirilir. Doğrulama yordamı, bir zaman aşımı (belirteç oluşturulduğu sırada saklanan zamana karşı geçerli zamanı denetleyerek), bir kerelik bir denetim yordamı veya istediğiniz diğer herhangi bir mantığı uygulayabilir.

## <a name="design-decisions-and-security-considerations"></a>Tasarım kararları ve güvenlik konuları

Oturumu ve alan belirteçlerini bağlayan güvenlik belirteci Teknik olarak yalnızca anonim/kimliği doğrulanmamış kullanıcıları XSRF saldırılarına karşı korumaya çalışırken gereklidir. Kullanıcının kimliği doğrulandığında, kimlik doğrulama belirtecinin kendisi (bir tanımlama bilgisi biçiminde), Eşitleyici belirteç çiftinin bir yarısı olarak kullanılabilir. Ancak, kimliği doğrulanmamış kullanıcılar tarafından gerçekleştirilen oturum açma sayfalarının korunması için geçerli senaryolar vardır ve güvenlik belirtecini kimliği doğrulanmış kullanıcılar için bile her zaman oluşturup doğrulayarak, Anti-XSRF mantığı daha basit hale getirilir. Ayrıca, bir alan belirtecinin bir saldırgan tarafından ele geçirilmediği konusunda, oturum belirtecinin ayarlanması veya tahmin edilmemesini sağlamak için başka bir sorumlu olması durumunda da bazı ek koruma sağlar.

Geliştiriciler, birden çok uygulama tek bir etki alanında barındırıldığı zaman dikkatli kullanılmalıdır. Örneğin, *example1.cloudapp.net* ve *example2.cloudapp.net* farklı konaklar olsa da, *\*. cloudapp.net* etki alanındaki tüm konaklar arasında örtük bir güven ilişkisi vardır. Bu örtük güven ilişkisi, [Güvenilmeyen ana bilgisayarların birbirlerinin tanımlama bilgilerini etkilemesini sağlar](http://stackoverflow.com/questions/9636857/how-can-asp-net-or-asp-net-mvc-be-protected-from-related-domain-cookie-attacks) (AJAX isteklerini yöneten aynı kaynak ilkeleri http tanımlama bilgilerine uygulanmaz). ASP.NET Web Stack çalışma zamanı, Kullanıcı adının alan belirtecine katıştırılması açısından bazı hafifletme sağlar, bu nedenle kötü amaçlı bir alt etki alanı bir oturum belirtecinin üzerine yazabileceğinden bile, Kullanıcı için geçerli bir alan belirteci oluşturamayacak. Bununla birlikte, böyle bir ortamda barındırıldığı zaman, yerleşik anti-XSRF yordamları, oturum ele geçirme veya oturum açma XSRF için de savunamaz.

Anti-XSRF yordamları Şu anda [tıklama mercesine](https://www.owasp.org/index.php/Clickjacking)karşı koruma sağlamaz. Kendilerini etkileşimli bir şekilde korumak isteyen uygulamalar, bir X-Frame-Options: SAMEORIGIN üst bilgisini her Yanıtla göndererek kolayca bunu yapabilirsiniz. Bu üst bilgi, tüm son tarayıcılar tarafından desteklenir. Daha fazla bilgi için bkz. [IE blogu](https://blogs.msdn.com/b/ieinternals/archive/2010/03/30/combating-clickjacking-with-x-frame-options.aspx), [SDL blogu](https://blogs.msdn.com/b/sdl/archive/2009/02/05/clickjacking-defense-in-ie8.aspx)ve [OWASP](https://www.owasp.org/index.php/Clickjacking). ASP.NET Web Stack çalışma zamanı bazı gelecek sürümlerde olabilir. MVC ve Web sayfaları Anti-XSRF yardımcıları, uygulamaların bu saldırıya karşı otomatik olarak korunması için bu üstbilgiyi otomatik olarak ayarlar.

Web geliştiricileri, sitelerinin XSS saldırılarına karşı savunmasız olmadığından emin olmaya devam etmelidir. XSS saldırıları çok güçlüdür ve başarılı bir yararlanma işlemi, XSRF saldırılarına karşı ASP.NET Web yığını çalışma zamanı savunmasının de kesintiye uğramasıdır.

## <a name="acknowledgment"></a>Olumlu

[@LeviBroderick](https://twitter.com/LeviBroderick), bu bilgilerin toplu ASP.NET güvenlik kodunun çoğunu yazdı.
