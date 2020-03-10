---
uid: web-api/overview/security/enabling-cross-origin-requests-in-web-api
title: ASP.NET Web API 2 ' de çapraz kaynak Isteklerini etkinleştirme | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API 'sinde, çıkış noktaları arası kaynak paylaşımı 'nı (CORS) nasıl desteklemenin gösterir.
ms.author: riande
ms.date: 01/29/2019
ms.assetid: 9b265a5a-6a70-4a82-adce-2d7c56ae8bdd
msc.legacyurl: /web-api/overview/security/enabling-cross-origin-requests-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 9d3016d98fa6c3a55359c6dab0737407b29925f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555708"
---
# <a name="enable-cross-origin-requests-in-aspnet-web-api-2"></a>ASP.NET Web API 2 ' de çapraz kaynak isteklerini etkinleştirme

, [Mike te son](https://github.com/MikeWasson)

> Tarayıcı güvenliği, bir web sitesinin başka bir etki alanına AJAX istekleri göndermesini engeller. Bu kısıtlamaya *aynı-Origin ilkesi*adı verilir ve kötü amaçlı bir sitenin başka bir siteden hassas verileri okumasını önler. Ancak, bazen diğer sitelerin Web API 'nizi çağırmasını sağlamak isteyebilirsiniz.
>
> [Çapraz kaynak kaynak paylaşımı](http://www.w3.org/TR/cors/) (CORS), bir sunucunun aynı kaynak ilkeyi rahat bir şekilde sağlamasına olanak tanıyan bir W3C standardıdır. CORS kullanarak, bir sunucu bazı çapraz kaynak isteklerine, diğerlerini reddetirken açık bir şekilde izin verebilir. CORS, [JSONP](http://en.wikipedia.org/wiki/JSONP)gibi önceki tekniklerin daha güvenli ve daha esnektir. Bu öğreticide, Web API uygulamanızda CORS 'nin nasıl etkinleştirileceği gösterilmektedir.
>
> ## <a name="software-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım
>
> - [Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - Web API 2,2

## <a name="introduction"></a>Giriş

Bu öğreticide, ASP.NET Web API 'sinde CORS desteği gösterilmektedir. Bir Web API denetleyicisi barındıran "WebService" adlı, diğeri de WebService 'yi çağıran "WebClient" adlı iki ASP.NET projesi oluşturarak başlayacağız. İki uygulama farklı etki alanlarında barındırıldığından, WebClient 'dan WebService 'a yönelik bir AJAX isteği bir çapraz kaynak isteği olur.

![](enabling-cross-origin-requests-in-web-api/_static/image1.png)

### <a name="what-is-same-origin"></a>"Aynı kaynak" nedir?

Aynı şemalara, konaklara ve bağlantı noktalarına sahip olmaları durumunda iki URL aynı kaynağa sahiptir. ([RFC 6454](http://tools.ietf.org/html/rfc6454))

Bu iki URL aynı kaynağa sahiptir:

- `http://example.com/foo.html`
- `http://example.com/bar.html`

Bu URL 'Ler, önceki iki değerden farklı kaynaklardan farklıdır:

- `http://example.net`-farklı etki alanı
- `http://example.com:9000/foo.html`-farklı bağlantı noktası
- `https://example.com/foo.html`-farklı düzen
- `http://www.example.com/foo.html`-farklı alt etki alanı

> [!NOTE]
> Internet Explorer, kaynakları karşılaştırırken bağlantı noktasını dikkate almaz.

## <a name="create-the-webservice-project"></a>WebService projesi oluşturma

> [!NOTE]
> Bu bölümde, Web API projeleri oluşturmayı bildiğiniz varsayılmaktadır. Aksi takdirde, bkz. [ASP.NET Web API 'si Ile çalışmaya](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)başlama.

1. Visual Studio 'Yu başlatın ve yeni bir **ASP.NET Web uygulaması (.NET Framework)** projesi oluşturun.
2. **Yeni ASP.NET Web uygulaması** Iletişim kutusunda **boş** proje şablonunu seçin. **Klasör ve temel başvuru Ekle**' nin altında **Web API** onay kutusunu seçin.

   ![Visual Studio 'da yeni ASP.NET Project iletişim kutusu](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog.png)

3. Aşağıdaki kodla `TestController` adlı bir Web API denetleyicisi ekleyin:

   [!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample1.cs)]

4. Uygulamayı yerel olarak çalıştırabilir veya Azure 'a dağıtabilirsiniz. (Bu öğreticideki ekran görüntüleri için, uygulama Azure App Service Web Apps dağıtılır.) Web API 'sinin çalıştığını doğrulamak için, *ana bilgisayar adının* uygulamayı dağıttığınız etki alanı olduğu `http://hostname/api/test/`' a gidin. &quot;al: test Iletisi&quot;yanıt metnini görmeniz gerekir.

   ![Sınama iletisini gösteren Web tarayıcısı](enabling-cross-origin-requests-in-web-api/_static/image4.png)

## <a name="create-the-webclient-project"></a>WebClient projesi oluşturma

1. Başka bir **ASP.NET Web uygulaması (.NET Framework)** projesi oluşturun ve **MVC** proje şablonunu seçin. İsteğe bağlı olarak **, kimlik doğrulaması > ** **kimlik doğrulamasını Değiştir** ' i seçin Bu öğretici için kimlik doğrulamaya gerek yoktur.

   ![Visual Studio 'da yeni ASP.NET proje iletişim kutusunda MVC şablonu](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog-mvc.png)

2. **Çözüm Gezgini**' de, *Görünümler/Home/Index. cshtml*dosyasını açın. Bu dosyadaki kodu aşağıdaki kodla değiştirin:

   [!code-cshtml[Main](enabling-cross-origin-requests-in-web-api/samples/sample2.cshtml?highlight=13)]

   *ServiceUrl* değişkeni için WEBSERVICE uygulamasının URI 'sini kullanın.

3. WebClient uygulamasını yerel olarak çalıştırın veya başka bir Web sitesinde yayımlayın.

"Dene" düğmesine tıkladığınızda, Web hizmeti uygulamasına açılan kutuda listelenen HTTP yöntemi kullanılarak bir AJAX isteği gönderilir (GET, POST veya PUT). Bu, farklı çapraz kaynak isteklerini incelemenizi sağlar. Şu anda, Web hizmeti uygulaması CORS 'yi desteklemez, bu nedenle düğmeye tıkladığınızda bir hata alırsınız.

![Tarayıcıda ' deneyin ' hatası](enabling-cross-origin-requests-in-web-api/_static/image7.png)

> [!NOTE]
> HTTP trafiğini [Fiddler](https://www.telerik.com/fiddler)gibi bir araçta izleyebilirsiniz, tarayıcının get isteğini göndereceğini ve isteğin başarılı olduğunu, ancak Ajax çağrısının bir hata döndürdüğünü görürsünüz. Aynı kaynak ilkenin tarayıcının isteği *göndermesini* önleyemediğinden emin olmak önemlidir. Bunun yerine, uygulamanın *yanıtı*görmesini önler.

![Web isteklerini gösteren Fiddler Web hata ayıklayıcısı](enabling-cross-origin-requests-in-web-api/_static/image8.png)

## <a name="enable-cors"></a>CORS'yi etkinleştirme

Şimdi WebService uygulamasında CORS 'yi etkinleştirelim. İlk olarak CORS NuGet paketini ekleyin. Visual Studio 'da, **Araçlar** menüsünden **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin. Paket Yöneticisi konsolu penceresinde aşağıdaki komutu yazın:

[!code-powershell[Main](enabling-cross-origin-requests-in-web-api/samples/sample3.ps1)]

Bu komut, en son paketi yüklenir ve çekirdek Web API kitaplıkları da dahil olmak üzere tüm bağımlılıkları günceller. Belirli bir sürümü hedeflemek için `-Version` bayrağını kullanın. CORS paketi için Web API 2,0 veya üzeri gerekir.

*Start/WebApiConfig. cs\_dosya uygulamasını*açın. **WebApiConfig. Register** yöntemine aşağıdaki kodu ekleyin:

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample4.cs?highlight=9)]

Sonra, `TestController` sınıfına **[Enablecors]** özniteliğini ekleyin:

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample5.cs?highlight=3,7)]

*Kaynakları* parametresi Için, WebClient UYGULAMASıNı dağıttığınız URI 'yi kullanın. Bu, aynı zamanda diğer tüm etki alanları arası isteklere izin verdiğinden WebClient kaynaklı çapraz kaynak isteklerine izin verir. Daha sonra, **[Enablecors]** parametrelerini daha ayrıntılı olarak açıklayacağım.

*Çıkış* URL 'sinin sonuna eğik çizgi eklemeyin.

Güncelleştirilmiş Web hizmeti uygulamasını yeniden dağıtın. WebClient 'ı güncelleştirmeniz gerekmez. Şimdi WebClient 'daki AJAX isteği başarılı olmalıdır. GET, PUT ve POST yöntemlerine izin verilir.

![Başarılı sınama iletisini gösteren Web tarayıcısı](enabling-cross-origin-requests-in-web-api/_static/image9.png)

## <a name="how-cors-works"></a>CORS nasıl kullanılır?

Bu bölümde, HTTP iletileri düzeyinde bir CORS isteğinde ne olacağı açıklanmaktadır. CORS 'nin nasıl çalıştığını anlamak önemlidir. böylece, **[Enablecors]** özniteliğini doğru şekilde yapılandırabilir ve her şeyin beklendiği gibi çalışmadığına sorun giderebilirsiniz.

CORS belirtimi, çıkış noktaları arası istekleri etkinleştiren birkaç yeni HTTP üst bilgisi sunar. Bir tarayıcı CORS 'yi destekliyorsa, bu üst bilgileri, çıkış noktaları arası istekler için otomatik olarak ayarlar; JavaScript kodunuzda özel bir şey yapmanız gerekmez.

Bir çapraz kaynak isteğine bir örnek aşağıda verilmiştir. "Origin" üstbilgisi, isteği yapan sitenin etki alanını verir.

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample6.cmd?highlight=5)]

Sunucu isteğe izin veriyorsa, erişim-denetim-Izin-kaynak üst bilgisini ayarlar. Bu üstbilginin değeri, kaynak üstbilgisiyle eşleşir veya "\*" joker değeri, yani herhangi bir kaynağa izin verilir.

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample7.cmd?highlight=5)]

Yanıt, erişim-denetim-Izin verme-kaynak üst bilgisini içermiyorsa, AJAX isteği başarısız olur. Özellikle, tarayıcı isteğe izin vermez. Sunucu başarılı bir yanıt döndürse bile tarayıcı, yanıtı istemci uygulaması için kullanılabilir hale getirmez.

**Ön kontrol Istekleri**

Bazı CORS istekleri için, tarayıcı kaynağın gerçek isteğini göndermeden önce "ön kontrol isteği" olarak adlandırılan ek bir istek gönderir.

Aşağıdaki koşullar doğruysa tarayıcı, ön kontrol isteğini atlayabilir:

- İstek yöntemi al, HEAD veya POST, *ve*
- Uygulama, kabul etme, kabul etme dili, Içerik-dil, Içerik türü veya son olay KIMLIĞI dışında bir istek üst bilgisi ayarlanmamış *ve*
- Content-Type üst bilgisi (ayarlandıysa) aşağıdakilerden biridir:

    - Application/x-www-form-urlencoded
    - multipart/form-Data
    - metin/düz

İstek üstbilgileri hakkındaki kural, uygulamanın **setRequestHeader** **XMLHttpRequest** nesnesine çağırarak ayarladığı üst bilgiler için geçerlidir. (CORS belirtimi bu "yazar istek üstbilgilerini" çağırır.) Kural, *tarayıcı* tarafından ayarlanan Kullanıcı Aracısı, ana bilgisayar veya içerik uzunluğu gibi üstbilgilere uygulanmaz.

Bir ön kontrol isteğine bir örnek aşağıda verilmiştir:

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample8.cmd?highlight=4-5)]

Uçuş öncesi isteği HTTP SEÇENEKLERI yöntemini kullanır. İki özel üst bilgi içerir:

- Access-Control-Request-Method: gerçek istek için kullanılacak HTTP yöntemi.
- Erişim-denetim-Istek-üstbilgiler: *uygulamanın* gerçek istekte ayarlandığı istek üst bilgilerinin bir listesi. (Yine, bu, tarayıcının ayarladığı üst bilgileri içermez.)

Sunucunun isteğe izin verdiğini kabul eden örnek bir yanıt aşağıda verilmiştir:

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample9.cmd?highlight=6-7)]

Yanıt, izin verilen yöntemleri ve isteğe bağlı olarak izin verilen üst bilgileri listeleyen bir erişim-denetimi-Izin-üstbilgiler başlığını listeleyen bir Access-Control-Allow-Methods üst bilgisi içerir. Ön kontrol isteği başarılı olursa, tarayıcı, daha önce açıklandığı gibi gerçek isteği gönderir.

Sık kullanılan araçlar, ön uç noktalarını (örneğin, [Fiddler](https://www.telerik.com/fiddler) ve [Postman](https://www.getpostman.com/)), varsayılan olarak gerekli seçenek üstbilgilerini göndermez. `Access-Control-Request-Method` ve `Access-Control-Request-Headers` üst bilgilerinin istekle birlikte gönderildiğini ve seçenekler başlıklarının IIS aracılığıyla uygulamaya ulaşmasını onaylayın.

IIS 'yi bir ASP.NET uygulamasının seçenek isteklerini almasına ve işlemesine izin verecek şekilde yapılandırmak için, aşağıdaki yapılandırmayı `<system.webServer><handlers>` bölümünde uygulamanın *Web. config* dosyasına ekleyin:

```xml
<system.webServer>
  <handlers>
    <remove name="ExtensionlessUrlHandler-Integrated-4.0" />
    <remove name="OPTIONSVerbHandler" />
    <add name="ExtensionlessUrlHandler-Integrated-4.0" path="*." verb="*" type="System.Web.Handlers.TransferRequestHandler" preCondition="integratedMode,runtimeVersionv4.0" />
  </handlers>
</system.webServer>
```

`OPTIONSVerbHandler` kaldırılması, IIS 'nin seçenek isteklerini işlemesini engeller. Varsayılan modül kaydı yalnızca uzantısız URL 'Ler ile alma, baş, POST ve hata ayıklama isteklerine izin verdiğinden, `ExtensionlessUrlHandler-Integrated-4.0` değişimi, SEÇENEKLERE ulaşmak için izin verir.

## <a name="scope-rules-for-enablecors"></a>[EnableCors] için kapsam kuralları

Uygulamanızdaki tüm Web API denetleyicileri için işlem başına CORS 'yi, denetleyici başına veya genel olarak etkinleştirebilirsiniz.

**Eylem başına**

CORS 'yi tek bir eylem için etkinleştirmek üzere, eylem yönteminde **[Enablecors]** özniteliğini ayarlayın. Aşağıdaki örnek, CORS 'yi yalnızca `GetItem` yöntemi için etkinleştirilir.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample10.cs)]

**Denetleyici başına**

Denetleyici sınıfında **[Enablecors]** ayarlarsanız, denetleyici üzerindeki tüm eylemler için geçerli olur. Bir eylemde CORS 'yi devre dışı bırakmak için, eyleme **[Disablecors]** özniteliğini ekleyin. Aşağıdaki örnek, `PutItem`hariç her yöntemde CORS 'yi mümkün.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample11.cs)]

**Görünüm**

Uygulamanızdaki tüm Web API denetleyicileri için CORS 'yi etkinleştirmek üzere **Enablecorsattribute** örneğini **enablecors** yöntemine geçirin:

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample12.cs)]

Özniteliği birden fazla kapsamda ayarlarsanız, öncelik sırası şu şekilde olur:

1. Eylem
2. Denetleyici
3. Global

## <a name="set-the-allowed-origins"></a>İzin verilen kaynakları ayarla

**[Enablecors]** özniteliğinin *kaynaklar parametresi,* kaynağa hangi kaynakların erişmelerine izin verildiğini belirtir. Değer, izin verilen çıkış noktaları için virgülle ayrılmış bir listesidir.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample13.cs)]

Tüm kaynaklardan gelen isteklere izin vermek için "\*" joker değerini de kullanabilirsiniz.

Herhangi bir kaynaktan isteklere izin vermeden önce dikkatlice düşünün. Bu, tam olarak herhangi bir Web sitesinin Web API 'niz için AJAX çağrıları yapabileceği anlamına gelir.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample14.cs)]

## <a name="set-the-allowed-http-methods"></a>İzin verilen HTTP yöntemlerini ayarlama

**[Enablecors]** özniteliğinin *Methods* parametresi, hangi http yöntemlerinin kaynağa erişmelerine izin verileceğini belirtir. Tüm yöntemlere izin vermek için "\*" joker karakter değerini kullanın. Aşağıdaki örnek yalnızca GET ve POST isteklerine izin verir.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample15.cs)]

## <a name="set-the-allowed-request-headers"></a>İzin verilen istek üst bilgilerini ayarlama

Bu makalede, bir ön kontrol isteğinin, uygulama tarafından ayarlanan HTTP üstbilgilerini (yani, "yazar istek üstbilgileri") listeleyerek bir erişim denetimi-Istek-üstbilgiler üst bilgisi nasıl dahil olabileceği açıklanmaktadır. **[Enablecors]** özniteliğinin *Headers* parametresi hangi yazar istek üst bilgilerine izin verileceğini belirtir. Tüm üstbilgilere izin vermek için *üst bilgileri* "\*" olarak ayarlayın. Belirli üstbilgileri beyaz listelemek için *üst bilgileri* izin verilen üst bilgilerin virgülle ayrılmış listesine ayarlayın:

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample16.cs)]

Ancak, tarayıcılar erişim-denetim-Istek üst bilgilerini ayarlama konusunda tamamen tutarlı değildir. Örneğin, Chrome şu anda "Origin" i içerir. FireFox, uygulama bunları betikte ayarlarsa bile, "kabul et" gibi standart üstbilgileri içermez.

*Üst bilgileri* "\*" dışında bir şeye ayarlarsanız, en az "kabul", "içerik türü" ve "kaynak" ve ayrıca desteklemek istediğiniz tüm özel üstbilgileri dahil etmelisiniz.

## <a name="set-the-allowed-response-headers"></a>İzin verilen yanıt üst bilgilerini ayarlama

Varsayılan olarak tarayıcı, tüm yanıt üst bilgilerini uygulamaya sunmaz. Varsayılan olarak kullanılabilen yanıt üstbilgileri şunlardır:

- Cache-Control
- İçerik-dil
- İçerik Türü
- Süresi Dolacak
- Son değiştirme
- Prag

CORS belirtimi bu [basit yanıt üstbilgilerini](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header)çağırır. Diğer üst bilgileri uygulama için kullanılabilir hale getirmek için, **[Enablecors]** *exposedHeaders* parametresini ayarlayın.

Aşağıdaki örnekte, denetleyicinin `Get` yöntemi ' X-Custom-Header ' adlı bir özel üst bilgi ayarlıyor. Varsayılan olarak tarayıcı, bu üst bilgiyi bir çapraz kaynak isteğinde kullanıma sunmaz. Üstbilgiyi kullanılabilir hale getirmek için, *exposedHeaders*Içine ' X-Custom-Header ' ekleyin.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample17.cs)]

## <a name="pass-credentials-in-cross-origin-requests"></a>Kimlik bilgilerini, çıkış noktaları arası isteklere geçirme

Kimlik bilgileri CORS isteğinde özel işleme gerektirir. Varsayılan olarak tarayıcı, bir çapraz kaynak isteğiyle kimlik bilgileri göndermez. Kimlik bilgileri, HTTP kimlik doğrulama düzenlerini de içerir. Bir çapraz kaynak isteğiyle kimlik bilgilerini göndermek için, istemcinin **XMLHttpRequest. withcredentials** öğesini true olarak ayarlaması gerekir.

Doğrudan **XMLHttpRequest** kullanma:

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample18.cs)]

JQuery içinde:

[!code-javascript[Main](enabling-cross-origin-requests-in-web-api/samples/sample19.js)]

Ayrıca, sunucu kimlik bilgilerine izin vermelidir. Web API 'sinde, çıkış noktaları arası kimlik bilgilerine izin vermek için, **[Enablecors]** özniteliğinde **SupportsCredentials** özelliğini true olarak ayarlayın:

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample20.cs)]

Bu özellik true ise, HTTP yanıtı bir erişim-denetim-Izin-kimlik bilgileri üst bilgisi içerecektir. Bu üst bilgi, tarayıcıya sunucunun bir çapraz kaynak isteği için kimlik bilgilerini verdiğini söyler.

Tarayıcı kimlik bilgilerini gönderirse, ancak yanıt geçerli bir erişim-denetim-Izin-kimlik bilgileri üst bilgisi içermiyorsa, tarayıcı uygulamaya yanıtı kullanıma sunmaz ve AJAX isteği başarısız olur.

**SupportsCredentials** değeri true olarak ayarlanırken, başka bir etki alanındaki bir Web sitesinin kullanıcı adına Kullanıcı adına, oturum açmış bir kullanıcının kimlik bilgilerini, Kullanıcı tarafından farkında olmadan BIR Web API 'nize gönderebildiğinden emin olun. CORS belirtimi Ayrıca, **SupportsCredentials** true ise &quot;\*&quot; için *Çıkış* ayarının geçersiz olduğunu belirtir.

## <a name="custom-cors-policy-providers"></a>Özel CORS ilke sağlayıcıları

**[Enablecors]** özniteliği **ıcorspolicyprovider** arabirimini uygular. **Özniteliğinden** türetilen ve **ıcorspolicyprovider**uygulayan bir sınıf oluşturarak kendi uygulamanızı sağlayabilirsiniz.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample21.cs)]

Artık özniteliği, **[Enablecors]** yerine koyabileceğiniz herhangi bir yerde uygulayabilirsiniz.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample22.cs)]

Örneğin, özel bir CORS ilke sağlayıcısı yapılandırma dosyasından ayarları okuyabilir.

Öznitelikleri kullanmanın bir alternatifi olarak **ıcorspolicyprovider** nesneleri oluşturan bir **ıcorspolicyproviderfactory** nesnesini kaydedebilirsiniz.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample23.cs)]

**Icorspolicyproviderfactory**ayarlamak için, başlangıç sırasında **setcorspolicyproviderfactory** genişletme yöntemini aşağıdaki gibi çağırın:

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample24.cs)]

## <a name="browser-support"></a>Tarayıcı desteği

Web API CORS paketi, sunucu tarafı teknolojisidir. Kullanıcının tarayıcısının de CORS 'yi desteklemesi gerekir. Neyse ki, tüm büyük tarayıcıların geçerli sürümleri [cors desteği](http://caniuse.com/cors)içerir.
