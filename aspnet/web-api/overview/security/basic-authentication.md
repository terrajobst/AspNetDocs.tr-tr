---
uid: web-api/overview/security/basic-authentication
title: ASP.NET Web API 'sinde temel kimlik doğrulaması | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API 'sinde temel kimlik doğrulamasının kullanılmasını açıklar.
ms.author: riande
ms.date: 10/02/2014
ms.assetid: 41423767-0021-47c3-9e53-0021b457c39f
msc.legacyurl: /web-api/overview/security/basic-authentication
msc.type: authoredcontent
ms.openlocfilehash: 1470bd4b5abd5199b9a5105973b053812d643351
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555729"
---
# <a name="basic-authentication-in-aspnet-web-api"></a>ASP.NET Web API 'sinde temel kimlik doğrulaması

, [Mike te son](https://github.com/MikeWasson)

Temel kimlik doğrulaması [RFC 2617, http kimlik doğrulaması: temel ve Özet erişimi kimlik doğrulaması](http://www.ietf.org/rfc/rfc2617.txt)içinde tanımlanmıştır.

Dezavantajlar

- Kullanıcı kimlik bilgileri istekte gönderilir.
- Kimlik bilgileri düz metin olarak gönderilir.
- Kimlik bilgileri her istekle birlikte gönderilir.
- Tarayıcı oturumunun sonlandırılacağından hariç, oturum açma yöntemi yoktur.
- Siteler arası istek için güvenlik açığı (CSRF); Anti-CSRF ölçüleri gerektirir.

Yararları

- Internet standart.
- Tüm büyük tarayıcılar tarafından desteklenir.
- Görece basit protokol.

Temel kimlik doğrulaması aşağıdaki gibi çalışmaktadır:

1. Bir istek kimlik doğrulaması gerektiriyorsa, sunucu 401 (yetkisiz) döndürür. Yanıt, sunucunun temel kimlik doğrulamasını desteklediğini belirten bir WWW-Authenticate üst bilgisi içerir.
2. İstemci, yetkilendirme üstbilgisinde istemci kimlik bilgileriyle başka bir istek gönderir. Kimlik bilgileri "ad: parola", Base64 kodlamalı dize olarak biçimlendirilir. Kimlik bilgileri şifrelenmedi.

Temel kimlik doğrulaması, "bölge" bağlamında gerçekleştirilir. Sunucu, WWW-Authenticate üstbilgisindeki bölge adını içerir. Kullanıcının kimlik bilgileri bu bölge içinde geçerli. Bir bölgenin tam kapsamı sunucu tarafından tanımlanır. Örneğin, kaynakları bölümlemek için birkaç bölge tanımlayabilirsiniz.

![](basic-authentication/_static/image1.png)

Kimlik Bilgileri şifrelenmemiş olarak gönderildiğinden, temel kimlik doğrulaması yalnızca HTTPS üzerinden güvenlidir. Bkz. [Web API 'de SSL Ile çalışma](working-with-ssl-in-web-api.md).

Temel kimlik doğrulaması da CSRF saldırılarına karşı savunmasızdır. Kullanıcı kimlik bilgilerini girdikten sonra, tarayıcı otomatik olarak onları oturum süresince aynı etki alanına, sonraki isteklere gönderir. Bu, AJAX isteklerini içerir. Bkz. [siteler arası Istek forgery (CSRF) saldırılarını önleme](preventing-cross-site-request-forgery-csrf-attacks.md).

## <a name="basic-authentication-with-iis"></a>IIS ile temel kimlik doğrulaması

IIS temel kimlik doğrulamasını destekler, ancak bir desteklenmediği uyarısıyla vardır: kullanıcının kimliği Windows kimlik bilgileriyle doğrulanır. Bu, kullanıcının sunucunun etki alanında bir hesabı olması gerektiği anlamına gelir. Herkese açık bir Web sitesi için genellikle bir ASP.NET üyelik sağlayıcısına göre kimlik doğrulaması yapmak istersiniz.

IIS kullanarak temel kimlik doğrulamasını etkinleştirmek için, ASP.NET projenizin Web. config dosyasında kimlik doğrulama modunu "Windows" olarak ayarlayın:

[!code-xml[Main](basic-authentication/samples/sample1.xml)]

Bu modda IIS, kimlik doğrulaması için Windows kimlik bilgilerini kullanır. Ayrıca, IIS 'de temel kimlik doğrulamasını etkinleştirmeniz gerekir. IIS Yöneticisi 'nde Özellikler Görünümü ' ne gidin, kimlik doğrulaması ' nı seçin ve temel kimlik doğrulamasını etkinleştirin.

![](basic-authentication/_static/image2.png)

Web API projenizde, kimlik doğrulaması gerektiren herhangi bir denetleyici eylemi için `[Authorize]` özniteliğini ekleyin.

İstemci, istekteki yetkilendirme üst bilgisini ayarlayarak kimliğini doğrular. Tarayıcı istemcileri bu adımı otomatik olarak gerçekleştirir. Tarayıcı olmayan istemcilerin üstbilgiyi ayarlaması gerekir.

## <a name="basic-authentication-with-custom-membership"></a>Özel üyelikle temel kimlik doğrulaması

Belirtildiği gibi, IIS 'de yerleşik olarak bulunan temel kimlik doğrulaması Windows kimlik bilgilerini kullanır. Bu, barındırma sunucusunda kullanıcılarınız için hesap oluşturmanız gerektiği anlamına gelir. Ancak, bir Internet uygulaması için Kullanıcı hesapları genellikle bir dış veritabanında depolanır.

Aşağıdaki kod, temel kimlik doğrulaması gerçekleştiren bir HTTP modülünü kullanır. Bu örnekte sözde bir yöntem olan `CheckPassword` yöntemini değiştirerek, bir ASP.NET üyelik sağlayıcısını kolayca takabilirsiniz.

Web API 2 ' de, bir HTTP modülü yerine bir [kimlik doğrulama filtresi](authentication-filters.md) veya [owın ara yazılımı](../../../aspnet/overview/owin-and-katana/index.md)yazmayı düşünmelisiniz.

[!code-csharp[Main](basic-authentication/samples/sample2.cs)]

HTTP modülünü etkinleştirmek için, **System. webserver** bölümündeki Web. config dosyanıza aşağıdakileri ekleyin:

[!code-xml[Main](basic-authentication/samples/sample3.xml?highlight=4)]

"YourAssemblyName" öğesini derlemenin adıyla değiştirin ("dll" uzantısını dahil değil).

Formlar veya Windows kimlik doğrulaması gibi diğer kimlik doğrulama düzenlerini devre dışı bırakmanız gerekir.
