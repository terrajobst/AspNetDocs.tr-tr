---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: NerdDinner Öğreticisine giriş | Microsoft Docs
author: shanselman
description: Yeni bir çerçeve öğrenmenin en iyi yolu olan bir şey oluşturmaktır. Bu öğreticide ASP.NE kullanarak küçük ancak tam bir uygulama oluşturma hakkında bilgi vermektedir...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: 154cfe6694cf723c0a1f8e33bfdb42c97594518f
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65122316"
---
# <a name="introducing-the-nerddinner-tutorial"></a>NerdDinner Öğreticisine Giriş

tarafından [Scott Hanselman](https://github.com/shanselman)

[PDF'yi indirin](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Yeni bir çerçeve öğrenmenin en iyi yolu olan bir şey oluşturmaktır. Bu öğretici, küçük bir derleme, ancak tamamlamak, ASP.NET MVC 1'i kullanarak uygulama hakkında bilgi vermektedir ve bazı ardındaki temel kavramları tanıtır.
> 
> ASP.NET MVC 3 kullanıyorsanız, takip ettiğiniz öneririz [MVC 3 ile çalışmaya başlama](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC müzik Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) öğreticiler.

## <a name="nerddinner-tutorial"></a>NerdDinner Öğreticisine

Yeni bir çerçeve öğrenmenin en iyi yolu olan bir şey oluşturmaktır. Bu öğretici, küçük bir derleme, ancak tamamlamak, ASP.NET MVC kullanarak uygulama hakkında bilgi vermektedir ve bazı ardındaki temel kavramları tanıtır.

Uygulama oluşturmak için kullanacağız "NerdDinner" adı verilir. NerdDinner çevrimiçi azalma bulun ve bu kişiler için kolay bir yol sağlar:

![](introducing-the-nerddinner-tutorial/_static/image1.png)

NerdDinner kayıtlı kullanıcıların oluşturma, düzenleme ve silme azalma sağlar. Uygulamanın tamamında tutarlı özellik kümesi doğrulama ve iş kuralları zorunlu kılar:

![](introducing-the-nerddinner-tutorial/_static/image2.png)

Ziyaretçiler, bunları tutulmakta yaklaşan azalma aramak için bir AJAX tabanlı eşleme kullanabilirsiniz:

![](introducing-the-nerddinner-tutorial/_static/image3.png)

Bir Akşam Yemeği tıklayarak bunları ayrıntıları sayfasına nereden öğrenebilir hakkında daha fazla sürer:

![](introducing-the-nerddinner-tutorial/_static/image4.png)

Bunlar dinner katılan içinde ilgileniyorsanız oturum açma veya sitesine kaydolun:

![](introducing-the-nerddinner-tutorial/_static/image5.png)

Bunlar, ardından etkinliğine katılın için bir AJAX tabanlı RSVP bağlantısına tıklayabilirsiniz:

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a>NerdDinner uygulama

Dosya - kullanarak NerdDinner uygulamamız başlamak kullanacağız&gt;yepyeni bir ASP.NET MVC projesi oluşturmak için Visual Studio'da yeni proje komutu. Ardından artımlı olarak işlevleri ve özellikleri ekleyeceğiz. Süreç boyunca şu konulara değineceğiz:

1. [Yeni bir ASP.NET MVC projesi oluşturma](create-a-new-aspnet-mvc-project.md)
2. [Bir veritabanı oluşturma](create-a-database.md)
3. [Nasıl iş kuralı doğrulamaları ile model oluşturma](build-a-model-with-business-rule-validations.md)
4. [Denetleyicileri ve görünümleri listeleme/Ayrıntılar kullanıcı Arabirimi uygulamak için kullanma](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [Nasıl CRUD (oluşturma, okuma, güncelleştirme ve silme) veri formu giriş desteği](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [ViewData kullanma ve ViewModel sınıfları uygulama](use-viewdata-and-implement-viewmodel-classes.md)
7. [Ana sayfaları ve kısmi bölümleri kullanarak kullanıcı arabirimini yeniden kullanma](re-use-ui-using-master-pages-and-partials.md)
8. [Verimli veri sayfalama uygulama](implement-efficient-data-paging.md)
9. [Kimlik doğrulama ve yetkilendirme kullanarak uygulamaların güvenliğini sağlama](secure-applications-using-authentication-and-authorization.md)
10. [AJAX dinamik güncelleştirmeler sunma konusunda](use-ajax-to-deliver-dynamic-updates.md)
11. [AJAX kullanarak eşleme senaryoları gerçekleştirmeyi öğrenin](use-ajax-to-implement-mapping-scenarios.md)
12. [Otomatik birim testi etkinleştirme](enable-automated-unit-testing.md)

NerdDinner kopyasına oluşturabileceğinizi her tamamlayarak sıfırdan adım Biz bu bölümdeki gözden geçirme. Alternatif olarak, kaynak kodu buraya tamamlanmış bir sürümünü indirebilirsiniz: [GitHub üzerinde NerdDinner](https://github.com/AspNetMVPSamples/NerdDinner). Ayrıca isteğe bağlı olarak ayrıca [Bu öğretici ücretsiz bir PDF sürümünü indirin](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) öğretici çevrimdışı okumak istiyorsanız.

Uygulamayı oluşturmak için Visual Studio 2008 ya da ücretsiz Visual Web Developer 2008 Express kullanabilirsiniz. Veritabanı için SQL Server veya ücretsiz SQL Server Express kullanabilirsiniz.

ASP.NET MVC, Visual Web Developer 2008 Express ve SQL Server'ın V2 kullanarak Express (tüm ücretsiz) yükleyebilirsiniz [Microsoft Web Platformu yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)

### <a name="now-lets-get-started"></a>Şimdi başlayalım...

NerdDinner nedir ele aldığımız, şimdi bizim kollarınızı sıvayın ve biraz kod yazalım.

Şu dosya - kullanarak başlarsınız&gt;NerdDinner uygulama oluşturmak için Visual Studio'da yeni proje.

> [!div class="step-by-step"]
> [Next](create-a-new-aspnet-mvc-project.md)
