---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: Nerdakşam yemeği öğreticisine giriş | Microsoft Docs
author: shanselman
description: Yeni bir çerçeve öğrenmenin en iyi yolu, onunla bir şey oluşturmak. Bu öğreticide, ASP.NE kullanarak küçük, ancak tamamlanmış bir uygulama oluşturma işlemi gösterilmektedir...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: 154cfe6694cf723c0a1f8e33bfdb42c97594518f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580579"
---
# <a name="introducing-the-nerddinner-tutorial"></a>NerdDinner Öğreticisine Giriş

[Scott Hanselman](https://github.com/shanselman) tarafından

[PDF 'YI indir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Yeni bir çerçeve öğrenmenin en iyi yolu, onunla bir şey oluşturmak. Bu öğreticide, ASP.NET MVC 1 kullanarak küçük, ancak tamamlanmış bir uygulamanın nasıl oluşturulacağı ve bunun arkasındaki temel kavramlardan bazıları tanıtılmaktadır.
> 
> ASP.NET MVC 3 kullanıyorsanız, [MVC 3 Ile çalışmaya başlama](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC müzik mağazası](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) öğreticilerini izlemeniz önerilir.

## <a name="nerddinner-tutorial"></a>Nerdakşam yemeği öğreticisi

Yeni bir çerçeve öğrenmenin en iyi yolu, onunla bir şey oluşturmak. Bu öğreticide, ASP.NET MVC kullanarak küçük, ancak tamamlanmış bir uygulama oluşturma ve bunun arkasındaki temel kavramlardan bazıları tanıtılmaktadır.

Derleyeceğiz uygulama "Nerdakşam yemeği" olarak adlandırılır. Nerdakşam yemeği, kullanıcıların dinleleri çevrimiçi bulma ve düzenleme konusunda kolay bir yol sunar:

![](introducing-the-nerddinner-tutorial/_static/image1.png)

Nerdakşam yemeği, kayıtlı kullanıcıların dinlayıcıları oluşturmalarına, düzenlemesine ve silmesine olanak sağlar. Uygulama genelinde tutarlı bir doğrulama ve iş kuralları kümesi uygular:

![](introducing-the-nerddinner-tutorial/_static/image2.png)

Ziyaretçiler, yaklaşan ön anlar için arama yapmak üzere AJAX tabanlı bir eşleme kullanabilir:

![](introducing-the-nerddinner-tutorial/_static/image3.png)

Bir akşam yemeği 'ya tıkladığınızda, bu kişiler hakkında daha fazla bilgi sağlayabilecekleri bir ayrıntı sayfasına götürür:

![](introducing-the-nerddinner-tutorial/_static/image4.png)

Dinner 'e katılmakla ilgileniyorsanız, sitede oturum açabilir veya kaydolarlar:

![](introducing-the-nerddinner-tutorial/_static/image5.png)

Daha sonra olaya katılmak için AJAX tabanlı bir RSVP bağlantısına tıklabilirler:

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a>Nerdakşam yemeği uygulama

Yeni bir ASP.NET MVC projesi oluşturmak için Visual Studio içindeki File-&gt;New Project komutunu kullanarak Nerdakşam yemeği uygulamamıza başlayacağız. Daha sonra özellik ve özellik artımlı olarak ekleyeceğiz. Şu şekilde ele alacağız:

1. [Yeni bir ASP.NET MVC projesi oluşturma](create-a-new-aspnet-mvc-project.md)
2. [Veritabanı oluşturma](create-a-database.md)
3. [İş kuralı doğrulamaları ile model oluşturma](build-a-model-with-business-rule-validations.md)
4. [Bir listeleme/Ayrıntılar Kullanıcı arabirimi uygulamak için denetleyicileri ve görünümleri kullanma](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [CRUD (oluşturma, okuma, güncelleştirme, silme) veri formu girişi desteği sağlama](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [ViewData kullanma ve ViewModel sınıfları uygulama](use-viewdata-and-implement-viewmodel-classes.md)
7. [Ana sayfaları ve partileri kullanarak Kullanıcı arabirimini yeniden kullanma](re-use-ui-using-master-pages-and-partials.md)
8. [Verimli veri sayfalamayı uygulama](implement-efficient-data-paging.md)
9. [Kimlik doğrulama ve yetkilendirme kullanarak uygulamaları güvenli hale getirme](secure-applications-using-authentication-and-authorization.md)
10. [Dinamik güncelleştirmeleri sunmak için AJAX kullanma](use-ajax-to-deliver-dynamic-updates.md)
11. [Eşleme senaryolarını uygulamak için AJAX kullanma](use-ajax-to-implement-mapping-scenarios.md)
12. [Otomatik birim testini etkinleştirme](enable-automated-unit-testing.md)

Bu bölümde anlatıyoruz her adımı tamamlayarak Nerdakşam yemeği 'nin kendi kopyasını sıfırdan oluşturabilirsiniz. Alternatif olarak, kaynak kodun tamamlanmış bir sürümünü buradan indirebilirsiniz: [GitHub 'Da Nerdakşam yemeği](https://github.com/AspNetMVPSamples/NerdDinner). Ayrıca, öğreticiyi çevrimdışı olarak okumak istiyorsanız [Bu öğreticinin ÜCRETSIZ PDF sürümünü de indirebilirsiniz](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) .

Uygulamayı derlemek için Visual Studio 2008 veya ücretsiz Visual Web Developer 2008 Express kullanabilirsiniz. Veritabanı için SQL Server ya da ücretsiz SQL Server Express kullanabilirsiniz.

ASP.NET MVC, Visual Web Developer 2008 Express ve SQL Server Express (tümü ücretsiz) sürümünü kullanarak [Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx) v2 yükleyebilirsiniz

### <a name="now-lets-get-started"></a>Şimdi başlayalım....

Nerdakşam yemeği 'nin ne olduğunu eklediğimiz için, sıvayıp sitemizi oluşturalım ve kod yazalım.

Nerdakşam yemeği uygulamasını oluşturmak için Visual Studio içinde dosya&gt;yeni proje 'yi kullanarak başlayacağız.

> [!div class="step-by-step"]
> [Next](create-a-new-aspnet-mvc-project.md)
