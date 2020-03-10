---
uid: webhooks/index
title: ASP.NET Web kancalarına genel bakış | Microsoft Docs
author: rick-anderson
description: ASP.NET Web kancalarına giriş.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: 1e21c92e950893c0ff87c63f03f4710a158441fd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637293"
---
# <a name="aspnet-webhooks-overview"></a>ASP.NET Web kancalarına genel bakış

Web kancaları, Web API 'Leri ve SaaS hizmetlerini birbirine bağlama için basit bir yayın/alt model sağlayan hafif bir HTTP modelidir. Bir hizmette bir olay gerçekleştiğinde, kayıtlı abonelere HTTP POST isteği biçiminde bir bildirim gönderilir. POST isteği, alıcının uygun şekilde davranmasına olanak sağlayan olayla ilgili bilgiler içerir.

Web kancaları kolaylık nedeniyle [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [bolluk](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/)ve çok daha fazlasını içeren çok sayıda hizmet tarafından zaten kullanıma sunuldu. Örneğin, bir Web kancası bir dosyanın [Dropbox](http://dropbox.com/)'ta değiştiğini veya bir kod değişikliğinin GitHub 'da kaydedilmiş olduğunu veya bir ödemenin [PayPal](http://www.paypal.com/)'de başlatıldığını ya da [Trello](http://www.trello.com/)'da bir kartın oluşturulduğunu gösterebilir. Olanaklar sınırsızdır!

Web kancaları Microsoft ASP.NET, Web kancalarını ASP.NET uygulamanızın bir parçası olarak hem gönderilmesini hem de almanızı kolaylaştırır:

* Alma tarafında, Web kancalarını herhangi bir sayıda Web kancası sağlayıcısından almak ve işlemek için ortak bir model sağlar. [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [iletici](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [bolluk](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) ve [Zendesk](https://www.zendesk.com/) desteğiyle birlikte daha fazla destek eklemek çok daha kolay.

* Gönderme tarafında, aboneliklerin yönetilmesi ve depolanması ve doğru abone kümesine olay bildirimleri gönderilmesi için destek sağlar. Bu, abonelerin abone olabileceği kendi olay kümesini tanımlamanızı ve şeyler gerçekleştiğinde bunları bilgilendirmesini sağlar.

İki bölüm, senaryonuza bağlı olarak veya ayrı bir şekilde kullanılabilir. Yalnızca diğer hizmetlerden Web kancaları almanız gerekiyorsa yalnızca alıcı parçasını kullanabilirsiniz; yalnızca başkalarının kullanması için Web kancaları sunmak istiyorsanız, bunu yapabilirsiniz.

Kod, ASP.NET Web API 2 ve ASP.NET MVC 5 ' i hedefler ve [GitHub 'Da OSS](https://github.com/aspnet/WebHooks)olarak kullanılabilir.

## <a name="webhooks-overview"></a>Web kancalarına genel bakış

Web kancaları, hizmetten hizmete nasıl kullanıldığını, ancak temel fikrin aynı olduğunu gösterdiği anlamına gelen bir modeldir. Web kancalarını, bir kullanıcının başka bir yerde yer aldığı olaylara abone olabileceği basit bir yayın/alt model olarak düşünebilirsiniz. Olay bildirimleri olay kendisiyle ilgili bilgiler içeren HTTP POST istekleri olarak dağıtılır.

Genellikle HTTP POST isteği, Web kancası göndericisi tarafından belirlenen ve Web kancasının tetiklenmesine neden olan olay hakkında bilgi içeren bir JSON nesnesi veya HTML form verileri içerir. Örneğin, [GitHub](https://www.github.com/) 'Dan bir Web kancası gönderi isteği gövdesi, belirli bir depoda açılmakta olan yeni bir sorun nedeniyle şöyle görünür:

```json
{
  "action": "opened",
  "issue": {
      "url": "https://api.github.com/repos/octocat/Hello-World/issues/1347",
      "number": 1347,
      ...
  },
  "repository": {
      "id": 1296269,
      "full_name": "octocat/Hello-World",
      "owner": {
          "login": "octocat",
          "id": 1
          ...
      },
      ...
  },
  "sender": {
      "login": "octocat",
      "id": 1,
      ...
  }
}
```

Web kancasının amaçlanan gönderenden gerçekten olduğundan emin olmak için POST isteğinin bir şekilde güvenli hale getirilmesi ve sonra alıcı tarafından doğrulanması gerekir. Örneğin, [GitHub Web kancaları](https://developer.github.com/webhooks/) , alıcı uygulama tarafından denetlenen istek gövdesinin karmasını Içeren bir *X-hub-Signature* http üst bilgisi içerir, böylece endişelenmenize gerek kalmaz.

Web kancası akışı genellikle şuna benzer bir şekilde geçer:

* Web kancası göndericisi, bir istemcinin abone olabileceği olayları kullanıma sunar. Olaylar, sistemdeki observable değişikliklerini, örneğin yeni bir veri öğesinin eklendiği, bir işlemin tamamlandığını veya başka bir şey olduğunu anlatmaktadır.

* Web kancası alıcısı dört şeyi içeren bir Web kancası kaydederek abone olur:

     1. Olay bildiriminin HTTP POST isteği biçiminde nakledilmesi gereken bir URI;

     2. Web kancasının tetiklenme gereken belirli olayları açıklayan bir filtre kümesi;

     3. HTTP POST isteğini imzalamak için kullanılan gizli anahtar;

     4. HTTP POST isteğine dahil edilecek ek veriler. Bu örnek, HTTP POST istek gövdesine eklenen ek HTTP üst bilgi alanları veya özellikleri olabilir.

* Bir olay gerçekleştiğinde, eşleşen Web kancası kayıtları bulunur ve HTTP POST istekleri gönderilir. Genellikle, HTTP POST isteklerinin oluşturulması bazı nedenlerle alıcının yanıt vermemesi veya HTTP POST isteğinin bir hata yanıtına neden olması halinde birkaç kez yeniden denenir.

## <a name="webhooks-processing-pipeline"></a>Web kancaları Işleme Işlem hattı

Gelen Web kancaları için Microsoft ASP.NET Web kancaları işleme işlem hattı şuna benzer:

![ASP.NET Web kancaları Işleme Işlem hattı](_static/WebHookReceivers.png)

*Alıcılar* ve *işleyiciler*burada bulunan iki temel kavramlardır:

* *Alıcılar* belirli bir gönderenden gelen Web kancası türünü işlemekten ve Web kancası isteğinin gerçekten amaçlanan gönderenden olduğundan emin olmak için güvenlik denetimlerinin zorlanmasından sorumludur.

* *İşleyiciler* genellikle kullanıcı kodunun belirli Web kancasını işleme çalıştırdığı yerdir.

Aşağıdaki düğümlerde, bu kavramlar daha ayrıntılı olarak açıklanmıştır.
