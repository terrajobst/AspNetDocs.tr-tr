---
uid: web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
title: ASP.NET MVC 'de siteler arası Istek forgery (CSRF) saldırılarını önleme
author: MikeWasson
description: Siteler arası istek sahteciliğini önleme (CSRF) saldırısını ve ASP.NET Web MVC 'de Anti-CSRF ölçülerinin nasıl uygulanacağını açıklar.
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 81d46f14-8f48-4d8c-830d-cc8d594dc11b
msc.legacyurl: /web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
msc.type: authoredcontent
ms.openlocfilehash: 5fb0f8bcc9e587ba4fbbf2b857d3bf7adcaafb94
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555120"
---
# <a name="preventing-cross-site-request-forgery-csrf-attacks-in-aspnet-mvc-application"></a>ASP.NET MVC uygulamasında siteler arası Istek forgery (CSRF) saldırılarını önleme

, [Mike te son](https://github.com/MikeWasson)

Siteler arası Istek sahteciliği (CSRF), kötü niyetli bir sitenin kullanıcının şu anda oturum açtığı bir güvenlik açığı olan siteye istek gönderdiği bir saldırıya neden olur

CSRF saldırılarına bir örnek aşağıda verilmiştir:

1. Kullanıcı, Forms kimlik doğrulaması kullanarak `www.example.com` oturum açar.
2. Sunucu, kullanıcının kimliğini doğrular. Sunucudan gelen yanıt bir kimlik doğrulama tanımlama bilgisi içerir.
3. Oturum açmadan, Kullanıcı kötü amaçlı bir Web sitesi ziyaret ettiğinde. Bu kötü amaçlı site aşağıdaki HTML biçimini içerir: 

    [!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample1.html)]

    Form eyleminin kötü amaçlı siteye değil, güvenlik açığı bulunan siteye gönderdiğine dikkat edin. Bu, CSRF 'nin "siteler arası" parçasıdır.
4. Kullanıcı Gönder düğmesine tıklar. Tarayıcı, istekle kimlik doğrulama tanımlama bilgisini içerir.
5. İstek, kullanıcının kimlik doğrulama bağlamıyla sunucuda çalışır ve kimliği doğrulanmış bir kullanıcının yapmasına izin verilen her şeyi yapabilir.

Bu örnekte kullanıcının form düğmesine tıklamasa da kötü amaçlı sayfa yalnızca formu otomatik olarak gönderen bir betiği kolayca çalıştırabilir. Üstelik, SSL kullanmak CSRF saldırılarına engel değildir çünkü kötü amaçlı site "https://" isteği gönderebilir.

Genellikle, tarayıcılar tüm ilgili tanımlama bilgilerini hedef Web sitesine gönderdikleri için kimlik bilgilerini kullanan Web sitelerine karşı CSRF saldırıları mümkündür. Ancak, CSRF saldırıları, tanımlama bilgilerini kötüye ile sınırlı değildir. Örneğin, temel ve Özet kimlik doğrulaması da savunmasız olacaktır. Bir Kullanıcı temel veya Özet kimlik doğrulamasıyla oturum açtıktan sonra. tarayıcı, oturum sona erene kadar kimlik bilgilerini otomatik olarak gönderir.

## <a name="anti-forgery-tokens"></a>Korunma belirteçleri

ASP.NET MVC, CSRF saldırılarını önlemeye yardımcı olmak için, *istek doğrulama belirteçleri*olarak da adlandırılan, güvenlik yumuşatma belirteçlerini kullanır.

1. İstemci, form içeren bir HTML sayfası ister.
2. Sunucu, yanıtta iki belirteç içerir. Bir belirteç tanımlama bilgisi olarak gönderilir. Diğeri gizli form alanına yerleştirilir. Belirteçler rastgele oluşturulur, böylece bir saldırgan değerleri tahmin edemez.
3. İstemci formu gönderdiğinde, her iki belirteci sunucuya geri göndermelidir. İstemci tanımlama bilgisi belirtecini tanımlama bilgisi olarak gönderir ve form belirtecini form verileri içine gönderir. (Kullanıcı formu gönderdiğinde bir tarayıcı istemcisi bunu otomatik olarak yapar.)
4. Bir istek her iki belirteci de içermiyorsa, sunucu isteğe izin vermez.

Gizli form belirtecine sahip HTML biçimine bir örnek aşağıda verilmiştir:

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample2.html)]

Kötü amaçlı sayfa, aynı kaynak ilkeleri nedeniyle kullanıcının belirteçlerini okuyamadığı için, karşı koruma belirteçleri çalışır. ([Aynı kaynak ilkeleri](http://www.w3.org/Security/wiki/Same_Origin_Policy) iki farklı sitede barındırılan belgelerin birbirlerinin içeriğine erişmesini önler. Bu nedenle, kötü amaçlı sayfa example.com 'e istek gönderebilir, ancak yanıtı okuyamıyor.)

CSRF saldırılarını engellemek için, tarayıcının Kullanıcı oturum açtıktan sonra kimlik bilgilerini sessizce gönderdiği kimlik doğrulama protokolleriyle karşı koruma belirteçleri kullanın. Bu, Forms kimlik doğrulaması ve temel ve Özet kimlik doğrulaması gibi protokollerin yanı sıra tanımlama bilgisi tabanlı kimlik doğrulama protokollerini içerir.

Güvenli olmayan Yöntemler (POST, PUT, DELETE) için koruma yumuşatma gerekli olmalıdır. Ayrıca, güvenli yöntemlerin (GET, HEAD) hiç yan etkisi olmadığından emin olun. Üstelik, CORS veya JSONP gibi etki alanları arası desteğini etkinleştirirseniz, GET gibi güvenli yöntemler de CSRF saldırılarına açıktır ve bu da saldırganın potansiyel olarak hassas verileri okumasına olanak tanır.

## <a name="anti-forgery-tokens-in-aspnet-mvc"></a>ASP.NET MVC 'de Anti-forgery belirteçleri

Bir Razor sayfasına korsanlığa karşı koruma belirteçleri eklemek için **HtmlHelper. AntiForgeryToken** yardımcı yöntemini kullanın:

[!code-cshtml[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample3.cshtml)]

Bu yöntem gizli form alanını ekler ve tanımlama bilgisi belirtecini de ayarlar.

## <a name="anti-csrf-and-ajax"></a>Anti-CSRF ve AJAX

Bir AJAX isteği HTML form verileri değil JSON verisi gönderebildiğinden, form belirteci, AJAX istekleri için bir sorun olabilir. Tek bir çözüm, belirteçleri özel bir HTTP üst bilgisinde göndermektir. Aşağıdaki kod belirteçleri oluşturmak için Razor söz dizimi kullanır ve ardından belirteçleri bir AJAX isteğine ekler. Belirteçler, **Antiforgery. GetTokens**çağırarak sunucuda oluşturulur.

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample4.html)]

İsteği tamamladığınızda, belirteçleri istek başlığından ayıklayın. Ardından, belirteçleri doğrulamak için **Antiforgery. Validate** metodunu çağırın. Belirteçler geçerli değilse **Validate** yöntemi bir özel durum oluşturur.

[!code-csharp[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample5.cs)]
