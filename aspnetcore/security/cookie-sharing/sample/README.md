---
ms.openlocfilehash: c3b00951d2f9e22a1c677a88261a36238d2b12fc
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57077127"
---
# <a name="cookie-sharing-sample-app"></a>Tanımlama bilgisi örnek uygulama paylaşımı

Örnek paylaşımı tanımlama bilgisi kimlik doğrulamasını kullanan üç uygulamalar arasında tanımlama bilgisi gösterilmektedir:

| Project                             | Açıklama |
| ----------------------------------- | ----------- |
| CookieAuth.Core                     | ASP.NET Core Razor sayfalar uygulamasını kullanarak ASP.NET Core kimliği olmadan |
| CookieAuthWithIdentity.Core         | ASP.NET Core kimliği ile ASP.NET Core MVC uygulaması |
| CookieAuthWithIdentity.NETFramework | ASP.NET Identity ile ASP.NET Framework MVC uygulaması |

Yönergeler:

1. CookieAuth.Core uygulamayı çalıştırın. Bir kullanıcı kaydı. Kullanıcı kaydedildiğinde uygulamayı kullanıcının kimliğini doğrular. Kullanıcı oturumu kapatın.
1. Aynı tarayıcı oturumunda CookieAuthWithIdentity.Core uygulamayı çalıştırın. Aynı kullanıcı olarak kullanılan Core uygulaması ile kaydedin. Kullanıcı kaydedildiğinde uygulamayı kullanıcının kimliğini doğrular. Kullanıcı oturumu kapatın.
1. Aynı tarayıcı oturumunda CookieAuthWithIdentity.NETFramework uygulamayı çalıştırın. Kullanılan diğer uygulamalarla aynı kullanıcı kaydedin. Kullanıcı kaydedildiğinde uygulamayı kullanıcının kimliğini doğrular. Kullanıcı oturumu kapatın.
1. Üç uygulamalardan herhangi birini için kullanıcının oturum açmasını. Kimlik doğrulama tanımlama, uygulamalar arasında paylaşılır. Kullanıcı diğer iki uygulamalara otomatik olarak işaretli olduğunu unutmayın.
1. Uygulamaların herhangi birinin kullanıcının oturum açın. Kullanıcı diğer iki uygulama dışında otomatik olarak işaretli olduğunu unutmayın.

Bu örnek, açıklanan özellikleri gösterir. [uygulamalar arasında tanımlama bilgilerini paylaşma](https://docs.microsoft.com/aspnet/core/security/cookie-sharing) konu.
