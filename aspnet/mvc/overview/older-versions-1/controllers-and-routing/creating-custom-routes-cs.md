---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: Özel yollar oluşturma (C#) | Microsoft Docs
author: microsoft
description: Özel yolların bir ASP.NET MVC uygulamasına nasıl ekleneceğini öğrenin. Bu öğreticide, Global. asax dosyasındaki varsayılan yol tablosunu değiştirme hakkında bilgi edineceksiniz.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: 58f72e390f0053d136ef00ddbda0b071ba225d98
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601334"
---
# <a name="creating-custom-routes-c"></a>Özel Rotalar Oluşturma (C#)

[Microsoft](https://github.com/microsoft) tarafından

> Özel yolların bir ASP.NET MVC uygulamasına nasıl ekleneceğini öğrenin. Bu öğreticide, Global. asax dosyasındaki varsayılan yol tablosunu değiştirme hakkında bilgi edineceksiniz.

Bu öğreticide, bir ASP.NET MVC uygulamasına özel bir yol eklemeyi öğreneceksiniz. Global. asax dosyasındaki varsayılan yol tablosunu özel bir yol ile nasıl değiştireceğinizi öğrenirsiniz.

Birçok basit ASP.NET MVC uygulaması için, varsayılan yol tablosu yalnızca iyi çalışacaktır. Ancak, özel yönlendirme gereksinimleriniz olduğunu fark edebilirsiniz. Bu durumda, özel bir yol oluşturabilirsiniz.

Örneğin, bir blog uygulaması oluşturduğunuzu düşünün. Şuna benzeyen gelen istekleri işlemek isteyebilirsiniz:

/Archive/12-25-2009

Bir Kullanıcı bu isteği girdiğinde, 12/25/2009 tarihine karşılık gelen blog girişini döndürmek istersiniz. Bu tür bir isteği işlemek için özel bir yol oluşturmanız gerekir.

Liste 1 ' deki Global. asax dosyası,/Archive/*Giriş tarihi*gibi görünen Istekleri işleyen blog adlı yeni bir özel yol içerir.

**Listeleme 1-Global. asax (özel rota ile)**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

Yol tablosuna eklediğiniz yolların sırası önemlidir. Yeni özel Blog Rotamız var olan varsayılan yolun önüne eklenir. Siparişi tersine aldıysanız, varsayılan yol özel yol yerine her zaman çağrılır.

Özel blog yolu,/Archive/. ile başlayan tüm istekler ile eşleşir Bu nedenle, aşağıdaki URL 'Lerin tümüyle eşleşir:

- /Archive/12-25-2009

- /Archive/10-6-2004

- /Archive/apple

Özel yol, gelen isteği arşiv adlı bir denetleyiciye eşler ve giriş () eylemini çağırır. Entry () yöntemi çağrıldığında, giriş tarihi entryDate adlı bir parametre olarak geçirilir.

Blog özel yolunu, döküm 2 ' de denetleyicisiyle birlikte kullanabilirsiniz.

**Listeleme 2-ArchiveController.cs**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

Liste 2 ' deki entry () yönteminin DateTime türünde bir parametreyi kabul ettiğini unutmayın. MVC çerçevesi, giriş tarihini URL 'den otomatik olarak bir tarih saat değerine dönüştürecek kadar akıllıdır. URL 'deki giriş tarihi parametresi bir tarih saat değerine dönüştürülemiyorsa bir hata oluşur (bkz. Şekil 1).

**Şekil 1-parametre dönüştürülürken hata oluştu**

[Yeni proje iletişim kutusunu ![](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)

**Şekil 01**: parametre dönüştürülürken hata ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-custom-routes-cs/_static/image2.png))

## <a name="summary"></a>Özet

Bu öğreticinin amacı, nasıl özel bir rota oluşturacağınızı göstermektir. Web günlüğü girdilerini temsil eden Global. asax dosyasındaki yol tablosuna nasıl özel bir yol ekleneceğini öğrendiniz. Blog girdilerine yönelik isteklerin ArchiveController adlı bir denetleyiciye ve girdi () adlı bir denetleyici eylemine nasıl eşleneceğini tartıştık.

> [!div class="step-by-step"]
> [Önceki](aspnet-mvc-controllers-overview-cs.md)
> [İleri](creating-a-route-constraint-cs.md)
