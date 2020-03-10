---
uid: mvc/overview/getting-started/database-first-development/customizing-a-view
title: 'Öğretici: ASP.NET MVC uygulamasıyla EF Database First için görünümü özelleştirme'
description: Bu öğretici, sunuyu iyileştirmek için otomatik olarak oluşturulan görünümlerin değiştirilmesine odaklanmaktadır.
author: Rick-Anderson
ms.author: riande
ms.date: 01/24/2019
ms.topic: tutorial
ms.assetid: 269380ff-d7e1-4035-8ad1-fe1316a25f76
msc.legacyurl: /mvc/overview/getting-started/database-first-development/customizing-a-view
msc.type: authoredcontent
ms.openlocfilehash: 89b8a0eb84b6e287c45bc141c68a2c76e63b0e41
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583596"
---
# <a name="tutorial-customize-view-for-ef-database-first-with-aspnet-mvc-app"></a>Öğretici: ASP.NET MVC uygulamasıyla EF Database First için görünümü özelleştirme

MVC, Entity Framework ve ASP.NET Scafkatı kullanarak var olan bir veritabanına arabirim sağlayan bir Web uygulaması oluşturabilirsiniz. Bu öğretici serisinde, kullanıcıların bir veritabanı tablosunda yer alan verileri görüntülemesini, düzenlemesini, oluşturmasını ve silmesini sağlayan nasıl otomatik olarak kod üretileyeceğiniz gösterilmektedir. Oluşturulan kod, veritabanı tablosundaki sütunlara karşılık gelir.

Bu öğretici, sunuyu iyileştirmek için otomatik olarak oluşturulan görünümlerin değiştirilmesine odaklanmaktadır.

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Öğrenci ayrıntısı sayfasına kurslar ekleme
> * Kurslar sayfasına eklendiğini onaylayın

## <a name="prerequisites"></a>Önkoşullar

* [Veritabanını değiştirme](changing-the-database.md)

## <a name="add-courses-to-student-detail"></a>Öğrenci ayrıntılarına kurslar ekleyin

Oluşturulan kod, uygulamanız için iyi bir başlangıç noktası sağlar, ancak uygulamanızda ihtiyaç duyduğunuz tüm işlevleri sağlamaz. Kodu uygulamanızın belirli gereksinimlerini karşılayacak şekilde özelleştirebilirsiniz. Şu anda, uygulamanız seçili öğrenci için kayıtlı kursları görüntülemez. Bu bölümde, her öğrencinin kayıtlı kurslarını öğrenciye ait **Ayrıntılar** görünümüne ekleyeceksiniz.

**Görünümler** > **öğrenciler** > *details. cshtml*dosyasını açın. Son &lt;/DL&gt; etiketinin altında, ancak kapanış &lt;/div&gt; etiketiyle önce aşağıdaki kodu ekleyin.

[!code-cshtml[Main](customizing-a-view/samples/sample1.cshtml)]

Bu kod, seçili öğrenci için kayıt tablosundaki her bir kayıt için bir satır görüntüleyen bir tablo oluşturur. **Görüntüleme** yöntemi, ifadeyi temsil eden nesne (Modelıdıtem) için HTML 'i işler. Değerin türüne ve bu türün şablonuna göre doğru biçimlendirildiğinden emin olmak için, görüntüleme yöntemini (kodda özellik değerini katıştırmak yerine) kullanın. Bu örnekte, her bir ifade döngüdeki geçerli kayıttan tek bir özellik döndürür ve değerler metin olarak işlenen ilkel türlerdir.

## <a name="confirm-courses-are-added"></a>Kurslar eklendiğini Onayla

Çözümü çalıştırın. **Öğrenciler listesi** ' ne tıklayın ve öğrencilerden biri için **Ayrıntılar** ' ı seçin. Kayıtlı kurslar görünüme dahil edildiğini görürsünüz.

![kayıt ile öğrenci](customizing-a-view/_static/image1.png)

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Öğrenci ayrıntısı sayfasına kurslar eklendi
> * Kurslar sayfasına eklendiğine onaylandı

Doğrulama gereksinimlerini belirtmek ve biçimlendirmeyi göstermek için veri ek açıklamaları ekleme hakkında bilgi edinmek için sonraki öğreticiye ilerleyin.
> [!div class="nextstepaction"]
> [Veri doğrulamayı geliştirme](enhancing-data-validation.md)
