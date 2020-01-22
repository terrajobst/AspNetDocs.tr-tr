---
uid: web-api/overview/security/authentication-filters
title: ASP.NET Web API 2 ' deki kimlik doğrulama filtreleri | Microsoft Docs
author: MikeWasson
description: Bir kimlik doğrulama filtresi, HTTP isteğinin kimliğini doğrulayan bir bileşendir. Web API 2 ve MVC 5 her ikisi de kimlik doğrulama filtrelerini destekler, ancak biraz farklı...
ms.author: riande
ms.date: 09/25/2014
ms.assetid: b9882e53-b3ca-4def-89b0-322846973ccb
msc.legacyurl: /web-api/overview/security/authentication-filters
msc.type: authoredcontent
ms.openlocfilehash: b6815baf05303d5f47a14ee5fe0fdfc2836c1868
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519381"
---
# <a name="authentication-filters-in-aspnet-web-api-2"></a>ASP.NET Web API 2 ' deki kimlik doğrulama filtreleri

, [Mike te son](https://github.com/MikeWasson)

> Bir kimlik doğrulama filtresi, HTTP isteğinin kimliğini doğrulayan bir bileşendir. Web API 2 ve MVC 5 her ikisi de kimlik doğrulama filtrelerini destekler, ancak çoğunlukla filtre arabirimine ilişkin adlandırma kurallarına göre biraz farklılık gösterir. Bu konu, Web API kimlik doğrulama filtrelerini açıklamaktadır.

Kimlik doğrulama filtreleri, bireysel denetleyiciler veya eylemler için bir kimlik doğrulama düzeni ayarlamanıza olanak sağlar. Bu şekilde, uygulamanız farklı HTTP kaynakları için farklı kimlik doğrulama mekanizmalarını destekleyebilir.

Bu makalede, [https://github.com/aspnet/samples](https://github.com/aspnet/samples) [temel kimlik doğrulama](http://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication) örneğinden kod göstereceğim. Örnek, HTTP temel erişim kimlik doğrulama şemasını (RFC 2617) uygulayan bir kimlik doğrulama filtresi gösterir. Filtre, `IdentityBasicAuthenticationAttribute`adlı bir sınıfta uygulanır. Örnekten yalnızca bir kimlik doğrulama filtresinin nasıl yazılacağını gösteren parçalar olan kodun tümünü göstermiyorum.

## <a name="setting-an-authentication-filter"></a>Kimlik doğrulama filtresi ayarlama

Diğer filtreler gibi, kimlik doğrulama filtreleri denetleyici başına, eyleme göre veya genel olarak tüm Web API denetleyicilerine uygulanabilir.

Bir denetleyiciye kimlik doğrulama filtresi uygulamak için, denetleyici sınıfını filtre özniteliğiyle süsleyerek. Aşağıdaki kod, denetleyicinin tüm eylemleri için temel kimlik doğrulamaya izin veren bir Controller sınıfında `[IdentityBasicAuthentication]` filtresini ayarlar.

[!code-csharp[Main](authentication-filters/samples/sample1.cs)]

Filtreyi bir eyleme uygulamak için eylemi filtreyle süsleyerek. Aşağıdaki kod denetleyicinin `Post` yönteminde `[IdentityBasicAuthentication]` filtresini ayarlar.

[!code-csharp[Main](authentication-filters/samples/sample2.cs)]

Filtreyi tüm Web API denetleyicilerine uygulamak için **Globalconfiguration. Filters**öğesine ekleyin.

[!code-csharp[Main](authentication-filters/samples/sample3.cs)]

## <a name="implementing-a-web-api-authentication-filter"></a>Web API kimlik doğrulama filtresi uygulama

Web API 'sinde, kimlik doğrulama filtreleri [System. Web. http. Filters. ıauthenticationfilter](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx) arabirimini uygular. Ayrıca, öznitelikler olarak uygulanması için **System. Attribute**'tan de devralması gerekir.

**Iauthenticationfilter** arabiriminin iki yöntemi vardır:

- Kimlik **doğrulayan ekip eşitleme** , istekte kimlik bilgilerini doğrulayarak isteğin kimliğini doğrular.
- Yanıt, gerekirse HTTP yanıtına bir kimlik doğrulama **sınaması ekler.**

Bu yöntemler, [rfc 2612](http://tools.ietf.org/html/rfc2616) ve [RFC 2617](http://tools.ietf.org/html/rfc2617)' de tanımlanan kimlik doğrulama akışına karşılık gelir:

1. İstemci kimlik bilgilerini yetkilendirme üst bilgisinde gönderir. Bu durum genellikle istemci sunucudan 401 (yetkisiz) yanıt aldıktan sonra oluşur. Ancak, bir istemci yalnızca 401 aldıktan sonra değil, herhangi bir istek ile kimlik bilgilerini gönderebilir.
2. Sunucu kimlik bilgilerini kabul etmezse, 401 (yetkisiz) yanıtını döndürür. Yanıt, bir veya daha fazla zorluk içeren bir WWW-Authenticate üst bilgisi içerir. Her zorluk, sunucu tarafından tanınan bir kimlik doğrulama şemasını belirtir.

Sunucu, anonim bir istekten 401 de döndürebilir. Aslında, genellikle kimlik doğrulama işlemi nasıl başlatılmıştı:

1. İstemci anonim bir istek gönderir.
2. Sunucu 401 döndürür.
3. İstemciler isteği kimlik bilgileriyle yeniden sonlandırır.

Bu akış hem *kimlik doğrulama* hem de *Yetkilendirme* adımlarını içerir.

- Kimlik doğrulama, istemcinin kimliğini kanıtlar.
- Yetkilendirme, istemcinin belirli bir kaynağa erişip erişemeyeceğini belirler.

Web API 'de, kimlik doğrulama filtreleri kimlik doğrulamasını işler, ancak yetkilendirmeyi işlemez. Yetkilendirme, yetkilendirme filtresi veya denetleyici eylemi içinde yapılmalıdır.

Web API 2 ardışık düzeninde akış aşağıda verilmiştir:

1. Bir eylemi çağırmadan önce Web API 'SI, bu eyleme yönelik kimlik doğrulama filtrelerinin bir listesini oluşturur. Buna eylem kapsamı, denetleyici kapsamı ve genel kapsama sahip filtreler dahildir.
2. Web API 'SI, listedeki her filtrede **kimlik doğrulayan ekip eşitlemesini** çağırır. Her filtre istekteki kimlik bilgilerini doğrulayabilir. Herhangi bir filtre kimlik bilgilerini başarıyla doğrularırsa, filtre bir **IPrincipal** oluşturur ve bunu isteğe ekler. Bu noktada bir filtre de bir hata tetiklenebilir. Öyleyse, ardışık düzen geri kalanı çalışmaz.
3. Bir hata olmadığı varsayılarak, istek işlem hattının geri kalanı üzerinden akar.
4. Son olarak, Web API her kimlik doğrulama filtresinin her ne **zaman uyumsuz** yöntemini çağırır. Filtreler, gerekirse yanıta bir sınama eklemek için bu yöntemi kullanır. Genellikle bir 401 hatasına yanıt olarak gerçekleştirilecek olan (her zaman değil).

Aşağıdaki diyagramlarda iki olası durum gösterilmektedir. İlk olarak, kimlik doğrulama filtresi isteğin kimliğini başarıyla doğrular, bir yetkilendirme filtresi isteği yetkilendirir ve denetleyici eylemi 200 döndürür (Tamam).

![](authentication-filters/_static/image1.png)

İkinci örnekte, kimlik doğrulama filtresi isteğin kimliğini doğrular, ancak yetkilendirme filtresi 401 (yetkisiz) değerini döndürür. Bu durumda, denetleyici eylemi çağrılmaz. Kimlik doğrulama filtresi, yanıta bir WWW-Authenticate üst bilgisi ekler.

![](authentication-filters/_static/image2.png)

Diğer birleşimler olasıdır&mdash;Örneğin, denetleyici eylemi anonim isteklere izin veriyorsa, bir kimlik doğrulama filtreniz olabilir ancak yetkilendirmenize sahip olabilirsiniz.

## <a name="implementing-the-authenticateasync-method"></a>Kimlik doğrulayan Teasync metodunu uygulama

**Kimlik doğrulayan Teasync** yöntemi isteğin kimliğini doğrulamaya çalışır. Yöntem imzası şöyledir:

[!code-csharp[Main](authentication-filters/samples/sample4.cs)]

**Kimlik doğrulayan Teasync** yöntemi aşağıdakilerden birini yapmanız gerekir:

1. Nothing (Hayır-op).
2. Bir **IPrincipal** oluşturun ve istekte ayarlayın.
3. Bir hata sonucu ayarlayın.

(1) seçeneği, isteğin, filtrenin anladığı kimlik bilgilerine sahip olmadığı anlamına gelir. (2) seçeneği, filtrenin isteği başarıyla doğruladığını gösterir. (3) seçeneği, isteğin geçersiz kimlik bilgilerine sahip olduğu anlamına gelir (yanlış parola gibi) ve bu da hata yanıtı tetikler.

**Kimlik doğrulayan ekip eşitlemesini**uygulamak için genel bir ana hat aşağıda verilmiştir.

1. İstekteki kimlik bilgilerini arayın.
2. Kimlik bilgileri yoksa, hiçbir şey yapmayın ve döndürün (Hayır-op).
3. Kimlik bilgileri varsa ancak filtre kimlik doğrulama düzenini algılamazsa hiçbir şey yapmayın ve döndürün (Hayır-op). İşlem hattındaki başka bir filtre düzeni anlayabilir.
4. Filtrenin anladığı kimlik bilgileri varsa, kimlik doğrulaması yapmayı deneyin.
5. Kimlik bilgileri bozuksa, `context.ErrorResult`ayarlayarak 401 döndürün.
6. Kimlik bilgileri geçerliyse, bir **IPrincipal** oluşturun ve `context.Principal`ayarlayın.

Takip kodu, [temel kimlik doğrulama](http://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication) örneğinden **kimlik doğrulayan teasync** yöntemini gösterir. Açıklamalar her adımı gösterir. Kod birçok hata türünü gösterir: kimlik bilgileri olmayan bir yetkilendirme üstbilgisi, hatalı biçimlendirilmiş kimlik bilgileri ve hatalı Kullanıcı adı/parola.

[!code-csharp[Main](authentication-filters/samples/sample5.cs)]

## <a name="setting-an-error-result"></a>Hata sonucunu ayarlama

Kimlik bilgileri geçersizse, filtrenin bir hata yanıtı oluşturan **ıhttpactionresult** `context.ErrorResult` ayarlaması gerekir. **Ihttpactionresult**hakkında daha fazla bilgi için bkz. [Web API 2 ' de eylem sonuçları](../getting-started-with-aspnet-web-api/action-results.md).

Temel kimlik doğrulama örneği, bu amaçla uygun bir `AuthenticationFailureResult` sınıfını içerir.

[!code-csharp[Main](authentication-filters/samples/sample6.cs)]

## <a name="implementing-challengeasync"></a>Requesgeasync uygulama

Yanıt **verme yönteminin amacı, gerekirse** yanıta kimlik doğrulama güçlükleri eklemektir. Yöntem imzası şöyledir:

[!code-csharp[Main](authentication-filters/samples/sample7.cs)]

Yöntemi, istek ardışık düzeninde her kimlik doğrulama filtresinde çağrılır.

HTTP yanıtı oluşturulmadan *önce* , Istene **zaman uyumsuz** olarak çağrıldığını ve denetleyici eyleminin çalıştırılmasından önce bile, yanıt verme işlemini anlamak önemlidir. Yanıt **verme isteği çağrıldığında `context.Result`** , daha sonra http yanıtı oluşturmak için kullanılan bir **ıhttpactionresult**içerir. Bu nedenle, yanıt verme **isteği ÇAĞRıLDıĞıNDA http** yanıtıyla ilgili hiçbir şeyi henüz bilemezsiniz. Bu **, `context.Result`** özgün değerini yeni bir **ıhttpactionresult**ile değiştirin. Bu **ıhttpactionresult** , özgün `context.Result`sarmalıdır.

![](authentication-filters/_static/image3.png)

Özgün **ıhttpactionresult** *iç sonucu*çağıracağım ve yeni **ıhttpactionresult** , *dıştaki sonucu*. Dış sonuç şunları sağlamalıdır:

1. HTTP yanıtını oluşturmak için iç sonucu çağırın.
2. Yanıtı inceleyin.
3. Gerekirse yanıta bir kimlik doğrulama sınaması ekleyin.

Aşağıdaki örnek, temel kimlik doğrulama örneğinden alınmıştır. Dış sonuç için bir **ıhttpactionresult** tanımlar.

[!code-csharp[Main](authentication-filters/samples/sample8.cs)]

`InnerResult` özelliği, iç **ıhttpactionresult**öğesini içerir. `Challenge` özelliği bir www-Authentication üst bilgisini temsil eder. **ExecuteAsync** , HTTP yanıtını oluşturmak için ilk `InnerResult.ExecuteAsync` çağırır ve gerekirse zorluğu ekler.

Sınamayı eklemeden önce yanıt kodunu kontrol edin. Çoğu kimlik doğrulama düzeni, burada gösterildiği gibi yalnızca yanıt 401 ise bir zorluk ekler. Ancak, bazı kimlik doğrulama şemaları başarı yanıtına bir zorluk ekler. Örneğin bkz. [Negotiate](http://tools.ietf.org/html/rfc4559#section-5) (RFC 4559).

`AddChallengeOnUnauthorizedResult` sınıfı verildiğinde,, bu, fiili kodu, bu, **zaman uyumsuz** ' de basittir. Yalnızca sonucu oluşturup `context.Result`iliştirebilirsiniz.

[!code-csharp[Main](authentication-filters/samples/sample9.cs)]

Note: temel kimlik doğrulama örneği bu mantığı bir genişletme yöntemine yerleştirerek bir bit soyutlar.

## <a name="combining-authentication-filters-with-host-level-authentication"></a>Kimlik doğrulama filtrelerini ana bilgisayar düzeyinde kimlik doğrulama ile birleştirme

"Ana bilgisayar düzeyinde kimlik doğrulaması", istek Web API çerçevesine ulaşmadan önce konak tarafından (IIS gibi) gerçekleştirilen kimlik doğrulamadır.

Genellikle uygulamanızın geri kalanı için ana bilgisayar düzeyinde kimlik doğrulamasını etkinleştirmek isteyebilir, ancak Web API denetleyicileriniz için devre dışı bırakabilirsiniz. Örneğin, tipik bir senaryo, form kimlik doğrulamasını konak düzeyinde etkinleştirmektir, ancak Web API için belirteç tabanlı kimlik doğrulaması kullanır.

Web API ardışık düzeninde ana bilgisayar düzeyinde kimlik doğrulamasını devre dışı bırakmak için, yapılandırmanızda `config.SuppressHostPrincipal()` çağırın. Bu, Web API 'sinin, Web API ardışık düzenine giren herhangi bir istekten **IPrincipal** 'ı kaldırmasına neden olur. Bu, isteği&quot; &quot;kimliğini doğrular.

[!code-csharp[Main](authentication-filters/samples/sample10.cs)]

## <a name="additional-resources"></a>Ek Kaynaklar

[ASP.NET Web API 'Si güvenlik filtreleri](https://msdn.microsoft.com/magazine/dn781361.aspx) (MSDN Magazine)
