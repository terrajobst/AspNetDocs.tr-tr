---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
title: Eylem filtrelerini anlama (C#) | Microsoft Docs
author: microsoft
description: Bu öğreticinin amacı, eylem filtrelerini açıklamaktır. Eylem filtresi, bir denetleyici eylemine veya bir denetleyicinin tamamına uygulayabileceğiniz bir özniteliktir...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: a94e4e81-40c1-47b7-8613-126a1a6cc93d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
msc.type: authoredcontent
ms.openlocfilehash: d1c72c2355c6122f851351a8c1e8f04fa63ae04e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581825"
---
# <a name="understanding-action-filters-c"></a>Eylem Filtrelerini Anlama (C#)

[Microsoft](https://github.com/microsoft) tarafından

[PDF 'YI indir](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_CS.pdf)

> Bu öğreticinin amacı, eylem filtrelerini açıklamaktır. Eylem filtresi, bir denetleyici eylemi için uygulayabileceğiniz bir özniteliktir veya bir denetleyicinin tamamına, eylemin yürütülme biçimini değiştirir.

## <a name="understanding-action-filters"></a>Eylem filtrelerini anlama

Bu öğreticinin amacı, eylem filtrelerini açıklamaktır. Eylem filtresi, bir denetleyici eylemi için uygulayabileceğiniz bir özniteliktir veya bir denetleyicinin tamamına, eylemin yürütülme biçimini değiştirir. ASP.NET MVC çerçevesi birkaç eylem filtresi içerir:

- OutputCache – bu eylem filtresi, belirli bir süre boyunca bir denetleyici eyleminin çıkışını önbelleğe alır.
- HandleError: Bu eylem filtresi, bir denetleyici eylemi yürütüldüğünde oluşan hataları işler.
- Yetkilendir – bu eylem filtresi, belirli bir kullanıcı veya role erişimi kısıtlamanıza olanak sağlar.

Kendi özel eylem filtrelerinizi de oluşturabilirsiniz. Örneğin, özel bir kimlik doğrulama sistemi uygulamak için özel bir eylem filtresi oluşturmak isteyebilirsiniz. Ya da, bir denetleyici eylemi tarafından döndürülen Görünüm verilerini değiştiren bir eylem filtresi oluşturmak isteyebilirsiniz.

Bu öğreticide, baştan sona bir eylem filtresi oluşturmayı öğreneceksiniz. Bir eylemin, Visual Studio çıktı penceresine işlenmesinin farklı aşamalarını günlüğe kaydeden bir günlük eylemi filtresi oluşturacağız.

### <a name="using-an-action-filter"></a>Eylem filtresi kullanma

Eylem filtresi bir özniteliktir. Birçok eylem filtresini tek bir denetleyici eylemine veya bir denetleyicinin tamamına uygulayabilirsiniz.

Örneğin, liste 1 ' deki veri denetleyicisi, geçerli saati döndüren `Index()` adlı bir eylem gösterir. Bu eylem `OutputCache` eylem filtresiyle birlikte tasarlanmıştır. Bu filtre, eylem tarafından döndürülen değerin 10 saniye önbellekte önbelleğe alınmasına neden olur.

**Listeleme 1 – `Controllers\DataController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample1.cs)]

Tarayıcınızın adres çubuğuna/Data/Index URL 'sini girerek `Index()` eylemini tekrar çağırdığınızda ve Yenile düğmesine birden çok kez ulaşarak, 10 saniye boyunca aynı zamanı görürsünüz. `Index()` eyleminin çıkışı 10 saniye için önbelleğe alınır (bkz. Şekil 1).

[![önbelleğe alınmış zaman](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)

**Şekil 01**: önbelleğe alınan süre ([tam boyutlu görüntüyü görüntülemek için tıklayın](understanding-action-filters-cs/_static/image3.png))

Liste 1 ' de, tek bir eylem filtresi – `OutputCache` Action filtresi – `Index()` yöntemine uygulanır. Gerekirse, aynı eyleme birden çok eylem filtresi uygulayabilirsiniz. Örneğin, hem `OutputCache` hem de `HandleError` eylem filtrelerini aynı eyleme uygulamak isteyebilirsiniz.

Liste 1 ' de `OutputCache` eylem filtresi `Index()` eylemine uygulanır. Ayrıca, bu özniteliği `DataController` sınıfının kendisi için de uygulayabilirsiniz. Bu durumda, denetleyici tarafından sunulan herhangi bir eylem tarafından döndürülen sonuç 10 saniye için önbelleğe alınır.

### <a name="the-different-types-of-filters"></a>Farklı filtre türleri

ASP.NET MVC çerçevesi dört farklı filtre türünü destekler:

1. Yetkilendirme filtreleri – `IAuthorizationFilter` özniteliğini uygular.
2. Eylem filtreleri – `IActionFilter` özniteliğini uygular.
3. Sonuç filtreleri – `IResultFilter` özniteliğini uygular.
4. Özel durum filtreleri – `IExceptionFilter` özniteliğini uygular.

Filtreler yukarıda listelenen sırayla yürütülür. Örneğin, Yetkilendirme filtreleri her zaman eylem filtreleri ve özel durum filtreleri her zaman diğer filtre türlerinin ardından yürütülene kadar yürütülür.

Yetkilendirme filtreleri, denetleyici eylemlerine yönelik kimlik doğrulama ve yetkilendirme uygulamak için kullanılır. Örneğin, yetkilendirme filtresi, yetkilendirme filtresine bir örnektir.

Eylem filtreleri, bir denetleyici eylemi yürütmeden önce ve sonra yürütülen mantığı içerir. Bir denetleyici eyleminin döndürdüğü verileri değiştirmek için bir eylem filtresi (örneğin,) kullanabilirsiniz.

Sonuç filtreleri, bir görünüm sonucu yürütülmeden önce ve sonra yürütülen mantığı içerir. Örneğin, görünüm tarayıcıya işlenmeden önce bir görünüm sonucunu değiştirmek isteyebilirsiniz.

Özel durum filtreleri, çalıştırılacak filtrenin son türüdür. Denetleyici eylemleriniz veya denetleyici eylem sonuçlarınız tarafından oluşturulan hataları işlemek için bir özel durum filtresi kullanabilirsiniz. Hataları günlüğe kaydetmek için özel durum filtreleri de kullanabilirsiniz.

Her farklı filtre türü belirli bir sırada yürütülür. Aynı türdeki filtrelerin yürütüldüğü sırayı denetlemek isterseniz, bir filtrenin Order özelliğini ayarlayabilirsiniz.

Tüm eylem filtrelerinin temel sınıfı `System.Web.Mvc.FilterAttribute` sınıfıdır. Belirli bir tür filtre uygulamak istiyorsanız, temel filtre sınıfından devralan bir sınıf oluşturmanız ve bir veya daha fazla `IAuthorizationFilter`, `IActionFilter`, `IResultFilter`veya `IExceptionFilter` arabirimi uygulamanız gerekir.

### <a name="the-base-actionfilterattribute-class"></a>Temel ActionFilterAttribute sınıfı

Özel bir eylem filtresi uygulamanızı kolaylaştırmak için, ASP.NET MVC çerçevesi bir temel `ActionFilterAttribute` sınıfı içerir. Bu sınıf hem `IActionFilter` hem de `IResultFilter` arabirimlerini uygular ve `Filter` sınıfından devralır.

Buradaki terminoloji tamamen tutarlı değildir. Teknik olarak, ActionFilterAttribute sınıfından devralan bir sınıf hem eylem filtresi hem de sonuç filtresidir. Ancak, gevşek anlamda Word eylem filtresi, ASP.NET MVC çerçevesindeki herhangi bir filtre türüne başvurmak için kullanılır.

Temel `ActionFilterAttribute` sınıfı, geçersiz kılabileceğiniz aşağıdaki yöntemlere sahiptir:

- OnActionExecuting – bu yöntem, bir denetleyici eylemi yürütülmeden önce çağrılır.
- Onactionyürütüldü – bu yöntem bir denetleyici eylemi yürütüldükten sonra çağrılır.
- OnResultExecuting – bu yöntem, bir denetleyici eylem sonucu yürütülmeden önce çağrılır.
- OnResultExecuted – bu yöntem bir denetleyici eylemi sonucu yürütüldükten sonra çağrılır.

Sonraki bölümde, bu farklı yöntemlerin her birini nasıl uygulayabileceğinizi görüyoruz.

### <a name="creating-a-log-action-filter"></a>Günlük eylemi filtresi oluşturma

Özel bir eylem filtresi oluşturmayı göstermek için, bir denetleyici eylemini işleme aşamalarını, Visual Studio çıktı penceresine kaydeden bir özel eylem filtresi oluşturacağız. `LogActionFilter`, liste 2 ' de yer alır.

**Listeleme 2 – `ActionFilters\LogActionFilter.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample2.cs)]

Liste 2 ' de, `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`ve `OnResultExecuted()` yöntemlerinin hepsi, `Log()` yöntemini çağırır. Yöntemin adı ve geçerli yol verileri `Log()` yöntemine geçirilir. `Log()` yöntemi, Visual Studio çıktı penceresine bir ileti yazar (bkz. Şekil 2).

[Visual Studio çıktı penceresine ![yazma](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)

**Şekil 02**: Visual Studio çıktı penceresine yazma ([tam boyutlu görüntüyü görüntülemek için tıklayın](understanding-action-filters-cs/_static/image6.png))

Listeleme 3 ' teki giriş denetleyicisi, tüm denetleyici sınıfına günlük eylemi filtresini nasıl uygulayacağınızı gösterir. Giriş denetleyicisi tarafından kullanıma sunulan eylemlerden herhangi biri çağrıldığında `Index()` yöntemi veya `About()` yöntemi – eylemi işleme aşamaları Visual Studio çıktı penceresine kaydedilir.

**Listeleme 3 – `Controllers\HomeController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample3.cs)]

### <a name="summary"></a>Özet

Bu öğreticide, ASP.NET MVC eylem filtreleri ' ne sunulmuştur. Dört farklı filtre türü hakkında bilgi edindiniz: Yetkilendirme filtreleri, eylem filtreleri, sonuç filtreleri ve özel durum filtreleri. Temel `ActionFilterAttribute` sınıfı hakkında da bilgi edindiniz.

Son olarak, basit bir eylem filtresinin nasıl uygulanacağını öğrendiniz. Bir denetleyici eylemini işleme aşamalarını, Visual Studio çıktı penceresine kaydeden bir günlük eylemi filtresi oluşturduk.

> [!div class="step-by-step"]
> [Önceki](asp-net-mvc-routing-overview-cs.md)
> [İleri](improving-performance-with-output-caching-cs.md)
