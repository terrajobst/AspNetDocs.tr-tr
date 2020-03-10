---
uid: mvc/overview/older-versions-1/controllers-and-routing/aspnet-mvc-controllers-overview-cs
title: ASP.NET MVC denetleyicisine genel bakışC#() | Microsoft Docs
author: StephenWalther
description: Bu öğreticide, Stephen Walther sizi ASP.NET MVC denetleyicilerini tanıtır. Yeni denetleyiciler oluşturmayı ve farklı eylem türlerini geri döndürmeyi öğrenirsiniz...
ms.author: riande
ms.date: 02/16/2008
ms.assetid: b985c49a-3668-455c-a366-f85f6bc64b12
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/aspnet-mvc-controllers-overview-cs
msc.type: authoredcontent
ms.openlocfilehash: 1a287b37742400a17c2ed53cfd00bfb053b4f3d2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544116"
---
# <a name="aspnet-mvc-controller-overview-c"></a>ASP.NET MVC Denetleyicisine Genel Bakış (C#)

ile [Stephen Walther](https://github.com/StephenWalther)

> Bu öğreticide, Stephen Walther sizi ASP.NET MVC denetleyicilerini tanıtır. Yeni denetleyiciler oluşturmayı ve farklı türlerde eylem sonuçları döndürmeyi öğrenirsiniz.

Bu öğretici, ASP.NET MVC denetleyicileri, denetleyici eylemleri ve eylem sonuçlarının konusunu araştırır. Bu Öğreticiyi tamamladıktan sonra, bir ziyaretçinin bir ASP.NET MVC web sitesiyle etkileşim kurma şeklini denetlemek için denetleyicilerin nasıl kullanıldığını anlamış olursunuz.

## <a name="understanding-controllers"></a>Denetleyicileri anlama

MVC denetleyicileri bir ASP.NET MVC web sitesinde yapılan isteklere yanıt vermekten sorumludur. Her tarayıcı isteği belirli bir denetleyiciye eşlenir. Örneğin, tarayıcınızın adres çubuğuna aşağıdaki URL 'YI girdiğinizi varsayın:

`http://localhost/Product/Index/3`

Bu durumda, ProductController adlı bir denetleyici çağrılır. ProductController, tarayıcı isteğine yanıt oluşturmaktan sorumludur. Örneğin, denetleyici tarayıcıya geri döndürülen belirli bir görünümü döndürebilir veya denetleyici kullanıcıyı başka bir denetleyiciye yönlendirebilir.

Listeleme 1, ProductController adlı basit bir denetleyici içerir.

**Listing1-Controllers\ProductController.cs**

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample1.cs)]

Liste 1 ' den görebileceğiniz gibi, bir denetleyici yalnızca bir sınıf (Visual Basic .NET veya C# sınıf) olur. Denetleyici, temel System. Web. Mvc. Controller sınıfından türetilen bir sınıftır. Bir denetleyici bu temel sınıftan devraldığı için, denetleyici birkaç yararlı yöntemi ücretsiz olarak devralır (Bu yöntemleri bir süre içinde tartıştık).

## <a name="understanding-controller-actions"></a>Denetleyici eylemlerini anlama

Denetleyici, denetleyici eylemlerini kullanıma sunar. Eylem, tarayıcı adres çubuğuna belirli bir URL girerken çağrılan bir denetleyicide bir yöntemdir. Örneğin, aşağıdaki URL için bir istek oluşturduğunuzu düşünün:

`http://localhost/Product/Index/3`

Bu durumda, Index () yöntemi ProductController sınıfında çağrılır. Index () yöntemi, bir denetleyici eyleminin bir örneğidir.

Denetleyici eyleminin bir denetleyici sınıfının ortak bir yöntemi olması gerekir. C#Yöntemler, varsayılan olarak özel yöntemlerdir. Bir denetleyici sınıfına eklediğiniz herhangi bir genel yöntemin otomatik olarak bir denetleyici eylemi olarak sunulduğunu unutmayın (bir denetleyici eylemi, bir tarayıcı adres çubuğuna doğru URL 'yi yazarak, Universe ' deki herkes tarafından çağrılabilir.

Bir denetleyici eylemi tarafından karşılanması gereken bazı ek gereksinimler vardır. Denetleyici eylemi olarak kullanılan bir yöntem aşırı yüklenemez. Ayrıca, bir denetleyici eylemi statik bir yöntem olamaz. Bundan farklı olarak, yalnızca bir denetleyici eylemi olarak istediğiniz yöntemi kullanabilirsiniz.

## <a name="understanding-action-results"></a>Eylem sonuçlarını anlama

Bir denetleyici eylemi, *eylem sonucu*olarak adlandırılan bir şeyi döndürür. Bir eylem sonucu, bir tarayıcı isteğine yanıt olarak bir denetleyici eyleminin döndürdüğü şeydir.

ASP.NET MVC çerçevesi aşağıdakiler dahil olmak üzere birkaç tür eylem sonucunu destekler:

1. ViewResult-HTML ve biçimlendirmeyi temsil eder.
2. EmptyResult-sonuç olmadığını gösterir.
3. RedirectResult-yeni bir URL 'ye yeniden yönlendirmeyi temsil eder.
4. JsonResult-bir AJAX uygulamasında kullanılabilecek JavaScript Nesne Gösterimi sonucunu temsil eder.
5. JavaScriptResult-bir JavaScript betiğini temsil eder.
6. ContentResult-bir metin sonucunu temsil eder.
7. FileContentResult-indirilebilir bir dosyayı temsil eder (ikili içerikle birlikte).
8. FilePathResult-indirilebilir bir dosyayı (bir yol ile) temsil eder.
9. FileStreamResult-indirilebilir bir dosyayı (dosya akışı ile) temsil eder.

Bu eylem sonuçlarının hepsi temel ActionResult sınıfından devralınır.

Çoğu durumda, bir denetleyici eylemi bir ViewResult döndürür. Örneğin, liste 2 ' deki Dizin denetleyicisi eyleminde bir ViewResult döndürülür.

**Listeleme 2-Controllers\BookController.cs**

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample2.cs)]

Bir eylem bir ViewResult döndürdüğünde, HTML tarayıcıya döndürülür. Liste 2 ' deki Index () yöntemi, tarayıcıya dizin adlı bir görünüm döndürür.

Liste 2 ' deki Index () eyleminin ViewResult () döndürmediğine dikkat edin. Bunun yerine, denetleyici temel sınıfının View () yöntemi çağrılır. Normalde, bir eylem sonucunu doğrudan döndürmeyin. Bunun yerine, Controller temel sınıfının aşağıdaki yöntemlerinden birini çağırın:

1. Görüntüle-ViewResult eylem sonucunu döndürür.
2. Yeniden yönlendir-bir RedirectResult eylem sonucunu döndürür.
3. RedirectToAction-RedirectToRouteResult eylem sonucunu döndürür.
4. RedirectToRoute-RedirectToRouteResult eylem sonucunu döndürür.
5. JSON-bir JsonResult eylem sonucunu döndürür.
6. JavaScriptResult-bir JavaScriptResult döndürür.
7. İçerik-bir ContentResult eylem sonucunu döndürür.
8. Dosya-metoda geçirilen parametrelere bağlı olarak bir FileContentResult, FilePathResult veya FileStreamResult döndürür.

Bu nedenle, tarayıcıya bir görünüm döndürmek istiyorsanız, View () yöntemini çağırın. Kullanıcıyı bir denetleyici eyleminden diğerine yönlendirmek istiyorsanız RedirectToAction () yöntemini çağırın. Örneğin, liste 3 ' teki ayrıntılar () eylemi, kimlik parametresinin bir değere sahip olup olmadığına bağlı olarak bir görünüm görüntüler veya kullanıcıyı dizin () eylemine yeniden yönlendirir.

**Listeleme 3-CustomerController.cs**

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample3.cs)]

ContentResult eylem sonucu özeldir. Bir eylem sonucunu düz metin olarak döndürmek için ContentResult eylem sonucunu kullanabilirsiniz. Örneğin, liste 4 ' teki Index () yöntemi bir iletiyi düz metin olarak HTML olarak değil bir ileti döndürür.

**Listeleme 4-Controllers\StatusController.cs**

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample4.cs)]

StatusController. Index () eylemi çağrıldığında bir görünüm döndürülmez. Bunun yerine, "Merhaba Dünya!" RAW metni tarayıcıya döndürülür.

Bir denetleyici eylemi bir eylem sonucu olmayan bir sonuç döndürürse (örneğin, bir tarih veya tamsayı), sonuç otomatik olarak bir ContentResult öğesine kaydırılır. Örneğin, Listeleme 5 ' teki WorkController dizini () eylemi çağrıldığında, tarih otomatik olarak bir ContentResult olarak döndürülür.

**Listeleme 5-WorkController.cs**

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample5.cs)]

Listeleme 5 ' teki Index () eylemi bir DateTime nesnesi döndürür. ASP.NET MVC Framework, DateTime nesnesini bir dizeye dönüştürür ve bir ContentResult içindeki DateTime değerini otomatik olarak kaydırır. Tarayıcı Tarih ve saati düz metin olarak alır.

## <a name="summary"></a>Özet

Bu öğreticinin amacı, sizi ASP.NET MVC denetleyicileri, denetleyici eylemleri ve denetleyici eylem sonuçlarının kavramlarını tanıtmaktadır. İlk bölümde, bir ASP.NET MVC projesine yeni denetleyiciler eklemeyi öğrendiniz. Daha sonra, bir denetleyicinin genel yöntemlerinin Universe as Controller eylemlerine nasıl sunuleceğini öğrendiniz. Son olarak, bir denetleyici eyleminden döndürülebilecek farklı eylem sonuçları türlerini tartıştık. Özellikle, bir denetleyici eyleminden bir ViewResult, RedirectToActionResult ve ContentResult döndürme hakkında anlatıldık.

> [!div class="step-by-step"]
> [Önceki](creating-an-action-vb.md)
> [İleri](creating-custom-routes-cs.md)
