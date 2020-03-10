---
uid: web-api/overview/advanced/http-cookies
title: ASP.NET Web API-ASP.NET 4. x içindeki HTTP tanımlama bilgileri
author: MikeWasson
description: ASP.NET 4. x için Web API 'de HTTP tanımlama bilgilerinin nasıl gönderileceğini ve alınacağını açıklar.
ms.author: riande
ms.date: 09/17/2012
ms.custom: seoapril2019
ms.assetid: 243db2ec-8f67-4a5e-a382-4ddcec4b4164
msc.legacyurl: /web-api/overview/advanced/http-cookies
msc.type: authoredcontent
ms.openlocfilehash: 8ca26ff6776daa13bc4f8b06c2eba61afcfefba2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557689"
---
# <a name="http-cookies-in-aspnet-web-api"></a>ASP.NET Web API’de HTTP Tanımlama Bilgileri

, [Mike te son](https://github.com/MikeWasson)

Bu konuda, Web API 'de HTTP tanımlama bilgilerinin nasıl gönderileceği ve alınacağı açıklanmaktadır.

## <a name="background-on-http-cookies"></a>HTTP tanımlama bilgilerinde arka plan

Bu bölüm, tanımlama bilgilerinin HTTP düzeyinde nasıl uygulandığı hakkında kısa bir genel bakış sunar. Ayrıntılar için bkz. [RFC 6265](http://tools.ietf.org/html/rfc6265).

Tanımlama bilgisi, bir sunucunun HTTP yanıtında gönderdiği bir veri parçasıdır. İstemci (isteğe bağlı olarak) tanımlama bilgisini depolar ve sonraki isteklere geri döndürür. Bu, istemci ve sunucunun durum paylaşmasına izin verir. Bir tanımlama bilgisi ayarlamak için, sunucu yanıtta bir set-Cookie üst bilgisi içerir. Tanımlama bilgisinin biçimi, isteğe bağlı özniteliklere sahip bir ad-değer çiftleridir. Örneğin:

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

Özniteliklere sahip bir örnek aşağıda verilmiştir:

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

Sunucuya bir tanımlama bilgisi döndürmek için, istemci sonraki isteklere bir tanımlama bilgisi üstbilgisi içerir.

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

Bir HTTP yanıtı, birden çok Set-Cookie üst bilgisi içerebilir.

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

İstemci tek bir tanımlama bilgisi üstbilgisi kullanarak birden çok tanımlama bilgisi döndürür.

[!code-console[Main](http-cookies/samples/sample5.cmd)]

Tanımlama bilgisinin kapsamı ve süresi, set-Cookie üstbilgisindeki öznitelikler tarafından denetlenir:

- **Etki alanı**: istemciye hangi etki alanının tanımlama bilgisini alacağını söyler. Örneğin, etki alanı "example.com" ise, istemci, example.com öğesinin her alt etki alanını tanımlama bilgisini döndürür. Belirtilmezse, etki alanı kaynak sunucusudur.
- **Yol**: tanımlama bilgisini, etki alanı içinde belirtilen yol ile sınırlandırır. Belirtilmemişse, istek URI 'sinin yolu kullanılır.
- **Süre sonu**: tanımlama bilgisi için bir sona erme tarihi ayarlar. İstemci, süresi dolduğu zaman tanımlama bilgisini siler.
- **Maksimum yaş**: tanımlama bilgisi için maksimum yaşı ayarlar. İstemci, en yüksek yaş sınırına ulaştığında tanımlama bilgisini siler.

Hem `Expires` hem de `Max-Age` ayarlanırsa `Max-Age` öncelik kazanır. Hiçbiri ayarlanmazsa, geçerli oturum sona erdiğinde istemci tanımlama bilgisini siler. ("Oturumun" tam anlamı Kullanıcı Aracısı tarafından belirlenir.)

Ancak, istemcilerin tanımlama bilgilerini yoksayabilir farkında olun. Örneğin, bir kullanıcı gizlilik nedenleriyle tanımlama bilgilerini devre dışı bırakabilir. İstemciler, tanımlama bilgilerini süresi dolmadan önce silebilir veya depolanan tanımlama bilgilerinin sayısını sınırlandırabilir. Gizlilik nedenleriyle, istemciler genellikle etki alanının kaynak sunucuyla eşleşmediği "üçüncü taraf" tanımlama bilgilerini reddeder. Kısacası, sunucu, ayarladığı tanımlama bilgilerini geri almaya bağlı olmamalıdır.

## <a name="cookies-in-web-api"></a>Web API 'de tanımlama bilgileri

Bir HTTP yanıtına bir tanımlama bilgisi eklemek için, tanımlama bilgisini temsil eden bir **pişirme ıeheadervalue** örneği oluşturun. Ardından, System .net. http dosyasında tanımlanan **addCookies** uzantı yöntemini çağırın **. Tanımlama bilgisini eklemek için HttpResponseHeadersExtensions** sınıfı.

Örneğin, aşağıdaki kod bir denetleyici eylemi içine bir tanımlama bilgisi ekler:

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

**AddCookies** 'in bir dizi **ıeheadervalue** örneği aldığını unutmayın.

İstemci isteğinden tanımlama bilgilerini ayıklamak için **GetCookies** metodunu çağırın:

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

Bir **pişirme ıeheadervalue** , bir **CookieState** örnekleri koleksiyonu içerir. Her bir **CookieState** bir tanımlama bilgisini temsil eder. Adlı Dizin Oluşturucu yöntemini kullanarak, gösterildiği gibi, ada göre bir **CookieState** alın.

## <a name="structured-cookie-data"></a>Yapılandırılmış tanımlama bilgisi verileri

Birçok tarayıcı, hem toplam numarayı hem de etki&#8212;alanı başına sayıyı depolayabileceği tanımlama bilgilerinin sayısını sınırlar. Bu nedenle, birden çok tanımlama bilgisi ayarlamak yerine, yapılandırılmış verileri tek bir tanımlama bilgisine yerleştirmek yararlı olabilir.

> [!NOTE]
> RFC 6265, tanımlama bilgisi verilerinin yapısını tanımlamaz.

**Pişirme ıeheadervalue** sınıfını kullanarak, tanımlama bilgisi verileri için ad-değer çiftleri listesini geçirebilirsiniz. Bu ad-değer çiftleri, set-Cookie üstbilgisinde URL kodlu form verileri olarak kodlanır:

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

Önceki kod, aşağıdaki set-Cookie üst bilgisini üretir:

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

**CookieState** sınıfı, istek iletisindeki bir tanımlama bilgisinden alt değerleri okumak için bir Dizin Oluşturucu yöntemi sağlar:

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a>Örnek: bir Ileti Işleyicisinde tanımlama bilgilerini ayarlama ve alma

Önceki örneklerde, bir Web API denetleyicisi içinden tanımlama bilgilerinin nasıl kullanılacağı gösterildi. Başka bir seçenek de [ileti işleyicilerini](http-message-handlers.md)kullanmaktır. İleti işleyicileri, ardışık düzende denetleyicilerden daha önce çağrılır. İleti işleyicisi, istek denetleyiciye ulaşmadan önce istekten tanımlama bilgilerini okuyabilir veya denetleyici yanıtı oluşturduktan sonra yanıta tanımlama bilgilerini ekleyebilir.

![](http-cookies/_static/image2.png)

Aşağıdaki kod, oturum kimlikleri oluşturmak için bir ileti işleyicisi gösterir. Oturum KIMLIĞI bir tanımlama bilgisinde depolanır. İşleyici, oturum tanımlama bilgisi isteğini denetler. İstek tanımlama bilgisini içermiyorsa, işleyici yeni bir oturum KIMLIĞI oluşturur. Her iki durumda da işleyici, oturum KIMLIĞINI **HttpRequestMessage. Properties** Özellik paketinde depolar. Ayrıca, oturum tanımlama bilgisini HTTP yanıtına ekler.

Bu uygulama, istemciden gelen oturum KIMLIĞININ sunucu tarafından gerçekten yayımlandığını doğrulamaz. Kimlik doğrulama formu olarak kullanmayın! Örneğin noktası, HTTP tanımlama bilgisi yönetimini gösterir.

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

Denetleyici, **HttpRequestMessage. Properties** Özellik çantasından oturum kimliğini alabilir.

[!code-csharp[Main](http-cookies/samples/sample12.cs)]
