---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
title: ASP.NET MVC uygulamaları için birim testleri oluşturma (C#) | Microsoft Docs
author: StephenWalther
description: Denetleyici eylemleri için birim testleri oluşturmayı öğrenin. Bu öğreticide, bir denetleyici eyleminin bir parti döndürüp döndürmediğini test etmek için Stephen Walther gösterilmektedir...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: d3a270b9-d7b1-47f2-8775-fc3beb518b5c
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
msc.type: authoredcontent
ms.openlocfilehash: 35fd0d85c63e5bd196394ce11b851c822a6405d9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623944"
---
# <a name="creating-unit-tests-for-aspnet-mvc-applications-c"></a>ASP.NET MVC Uygulamaları için Birim Testleri Oluşturma (C#)

ile [Stephen Walther](https://github.com/StephenWalther)

[PDF 'YI indir](https://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_CS.pdf)

> Denetleyici eylemleri için birim testleri oluşturmayı öğrenin. Bu öğreticide, bir denetleyici eyleminin belirli bir görünümü döndürüp döndürmediğini test etme, belirli bir veri kümesini geri alma veya farklı türde bir eylem sonucu döndürür.

Bu öğreticinin amacı, ASP.NET MVC uygulamalarınızda denetleyiciler için birim testlerini nasıl yazabileceğinizi göstermek içindir. Üç farklı türde birim testi oluşturmayı tartıştık. Bir denetleyici eylemi tarafından döndürülen görünümü test etme, bir denetleyici eylemi tarafından döndürülen Görünüm verilerini test etme ve bir denetleyici eyleminin, sizi ikinci bir denetleyiciye yeniden yönlendirip yönlendirmediğini test etme hakkında bilgi edinebilirsiniz.

## <a name="creating-the-controller-under-test"></a>Test altında denetleyici oluşturma

Sınamayı planladığımız denetleyiciyi oluşturalım. `ProductController`adlı denetleyici, liste 1 ' de yer alır.

**Listeleme 1 – `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample1.cs)]

`ProductController`, `Index()` ve `Details()`adında iki eylem yöntemi içerir. Her iki eylem yöntemi de bir görünüm döndürür. `Details()` eyleminin ID adlı bir parametreyi kabul ettiğini unutmayın.

## <a name="testing-the-view-returned-by-a-controller"></a>Denetleyicinin döndürdüğü görünümü test etme

`ProductController` doğru görünümü döndürüp döndürmediğini test etmek istediğimiz düşünün. `ProductController.Details()` eylemi çağrıldığında, Ayrıntılar görünümünün döndürüldüğünden emin olmak istiyoruz. Liste 2 ' deki test sınıfı, `ProductController.Details()` eylemi tarafından döndürülen görünümü test etmek için bir birim testi içerir.

**Listeleme 2 – `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample2.cs)]

Liste 2 ' deki sınıf, `TestDetailsView()`adlı bir test yöntemi içerir. Bu yöntem üç satır kod içerir. Kodun ilk satırı `ProductController` sınıfının yeni bir örneğini oluşturur. Kodun ikinci satırı denetleyicinin `Details()` Action yöntemini çağırır. Son olarak, kodun son satırı `Details()` eylemi tarafından döndürülen görünümün Ayrıntılar görünümü olup olmadığını denetler.

`ViewResult.ViewName` özelliği, bir denetleyicinin döndürdüğü görünümün adını temsil eder. Bu özelliği test etmek için büyük bir uyarı. Denetleyicinin bir görünümü döndürebilmenin iki yolu vardır. Bir denetleyici şu şekilde açıkça bir görünüm döndürebilir:

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample3.cs)]

Alternatif olarak, görünümün adı aşağıdaki gibi, denetleyici eyleminin adından de görünebilir:

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample4.cs)]

Bu denetleyici eylemi, `Details`adlı bir görünüm de döndürür. Ancak, görünümün adı eylem adından algılanır. Görünüm adını test etmek isterseniz, denetleyici eyleminden görünüm adını açıkça geri döndürmanız gerekir.

**CTRL-R, A** ya da **tüm testleri çözümle Çalıştır** düğmesine tıklayarak (bkz. Şekil 1), liste 2 ' de birim testini çalıştırabilirsiniz. Test geçerse Şekil 2 ' de Test Sonuçları penceresini görürsünüz.

[Çözümdeki tüm testleri çalıştırmak ![](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)

**Şekil 01**: Çözümdeki tüm Testleri Çalıştır ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))

[Başarılı ![!](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)

**Şekil 02**: başarılı! ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))

## <a name="testing-the-view-data-returned-by-a-controller"></a>Bir denetleyici tarafından döndürülen Görünüm verilerini test etme

MVC denetleyicisi *`View Data`* adlı bir şeyi kullanarak verileri bir görünüme geçirir. Örneğin, `ProductController Details()` eylemini çağırdığınızda belirli bir ürünün ayrıntılarını göstermek istediğinizi düşünün. Bu durumda, `Product` sınıfının bir örneğini oluşturabilir (modelinizde tanımlanmıştır) ve `View Data`avantajlarından yararlanarak örneği `Details` görünümüne geçirebilirsiniz.

Kod 3 ' teki değiştirilen `ProductController`, bir ürün döndüren güncelleştirilmiş bir `Details()` eylemi içerir.

**Listeleme 3 – `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample5.cs)]

İlk olarak `Details()` eylem, bir dizüstü bilgisayarı temsil eden `Product` sınıfının yeni bir örneğini oluşturur. Sonra, `Product` sınıfının örneği `View()` yöntemine ikinci parametre olarak geçirilir.

Beklenen verilerin görünüm verilerinde içerilip içerilmediğini test etmek için birim testleri yazabilirsiniz. Listeleme 4 ' teki birim testi, `ProductController Details()` eylem yöntemini çağırdığınızda bir dizüstü bilgisayarı temsil eden bir ürünün döndürülüp döndürülmediğini sınar.

**Listeleme 4 – `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample6.cs)]

Liste 4 ' te `TestDetailsView()` yöntemi, `Details()` yöntemini çağırarak döndürülen Görünüm verilerini sınar. `ViewData`, `Details()` yöntemini çağırarak döndürülen `ViewResult` bir özellik olarak sunulur. `ViewData.Model` özelliği, görünüme geçirilen ürünü içerir. Test, görünüm verilerinde içerilen ürünün dizüstü bilgisayar adına sahip olduğunu doğrular.

## <a name="testing-the-action-result-returned-by-a-controller"></a>Bir denetleyici tarafından döndürülen eylem sonucunu sınama

Daha karmaşık bir denetleyici eylemi, denetleyici eylemine geçirilen parametrelerin değerlerine bağlı olarak farklı türlerde eylem sonuçları döndürebilir. Bir denetleyici eylemi, `ViewResult`, `RedirectToRouteResult`veya `JsonResult`dahil olmak üzere çeşitli türlerde eylem sonuçları döndürebilir.

Örneğin, kod 5 ' teki değiştirilen `Details()` eylemi, eyleme geçerli bir ürün kimliği geçirdiğinizde `Details` görünümü döndürür. Geçersiz bir ürün kimliği geçirirseniz (1 ' den küçük bir değere sahip bir kimlik), `Index()` eyleme yönlendirilirsiniz.

**Listeleme 5 – `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample7.cs)]

`Details()` eyleminin davranışını, liste 6 ' da birim testiyle test edebilirsiniz. Liste 6 ' daki birim testi, `Details()` yöntemine-1 değeri ile bir kimlik geçirildiğinde `Index` görünümüne yönlendirildiğini doğrular.

**Listeleme 6 – `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample8.cs)]

Bir denetleyici eyleminde `RedirectToAction()` yöntemini çağırdığınızda, denetleyici eylemi bir `RedirectToRouteResult`döndürür. Test, `RedirectToRouteResult` kullanıcıyı `Index`adlı bir denetleyici eylemine yönlendirip yönlendirmeyeceğini denetler.

## <a name="summary"></a>Özet

Bu öğreticide, MVC denetleyici eylemleri için birim testleri oluşturmayı öğrendiniz. İlk olarak, doğru görünümün bir denetleyici eylemi tarafından döndürülüp döndürülmediğini nasıl doğrulayabildiğinizi öğrendiniz. Bir görünümün adını doğrulamak için `ViewResult.ViewName` özelliğini kullanmayı öğrendiniz.

Sonra, `View Data`içeriğini nasıl test kullanabileceğinizi inceledik. Bir denetleyici eylemi çağrıldıktan sonra doğru ürünün `View Data` döndürülüp döndürülmediğini nasıl denetleceğini öğrendiniz.

Son olarak, bir denetleyici eyleminden farklı türlerde eylem sonuçları döndürülüp döndürülmeyeceğini nasıl test ettireceğiz anlatılmıştır. Denetleyicinin bir `ViewResult` veya `RedirectToRouteResult`döndürüp döndürmediğini nasıl test etmeyeceğinizi öğrendiniz.

> [!div class="step-by-step"]
> [Next](creating-unit-tests-for-asp-net-mvc-applications-vb.md)
