---
uid: web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
title: Model bağlama ve Web formlarıyla verileri filtrelemek için sorgu dizesi değerlerini kullanma | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir. Model bağlama, veri etkileşimini daha düz-... hale getirir
ms.author: riande
ms.date: 02/27/2014
ms.assetid: b90978bd-795d-4871-9ade-1671caff5730
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
msc.type: authoredcontent
ms.openlocfilehash: 143ddcb40b576a3129e659b90bfc8321c061a547
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639099"
---
# <a name="using-query-string-values-to-filter-data-with-model-binding-and-web-forms"></a>Model bağlama ve Web formlarıyla verileri filtrelemek için sorgu dizesi değerlerini kullanma

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir. Model bağlama veri kaynağı nesneleriyle (örneğin, ObjectDataSource veya SqlDataSource) çok daha basit hale getirir. Bu seri giriş malzemesiyle başlar ve sonraki öğreticilerde daha gelişmiş kavramlara gider.
> 
> Bu öğreticide, sorgu dizesinde bir değerin nasıl geçirileceğini ve model bağlama yoluyla verileri almak için bu değerin nasıl kullanılacağı gösterilmektedir.
> 
> Bu öğreticide, serinin [önceki](retrieving-data.md) bölümlerinde oluşturulan projede derleme yapılır.
> 
> Tüm projeyi [](https://go.microsoft.com/fwlink/?LinkId=286116) C# veya vb 'ye indirebilirsiniz. İndirilebilir kod, Visual Studio 2012 veya Visual Studio 2013 ile birlikte kullanılabilir. Bu öğreticide gösterilen Visual Studio 2013 şablonundan biraz farklı olan Visual Studio 2012 şablonunu kullanır.

## <a name="what-youll-build"></a>Ne oluşturacağız?

Bu öğreticide şunları yapmanız gerekir:

1. Bir öğrenciye yönelik kayıtlı kursları göstermek için yeni bir sayfa ekleyin
2. Sorgu dizesindeki bir değere göre seçili öğrenci için kayıtlı kursları alın
3. Kılavuz görünümünden yeni sayfaya sorgu dizesi değeri olan bir köprü ekleyin

Bu öğreticideki adımlar, bir açılan listede Kullanıcı seçimine bağlı olarak görüntülenen öğrencileri filtrelemek için daha önceki [öğreticide](sorting-paging-and-filtering-data.md) yaptığınız şekilde oldukça benzerdir. Bu öğreticide, parametre değerinin bir denetimden geldiğini belirtmek için Select yöntemindeki **Denetim** özniteliğini kullandınız. Bu öğreticide, parametre değerinin sorgu dizesinden geldiğini belirtmek için Select yönteminde **QueryString** özniteliğini kullanacaksınız.

## <a name="add-new-page-for-displaying-a-students-courses"></a>Öğrencinin kurslarını görüntülemek için yeni sayfa ekle

Site. Master ana sayfasını kullanan yeni bir Web formu ekleyin ve sayfa **kurslarını**adlandırın.

**Kurslar. aspx** dosyasında seçili öğrenci için kursları görüntülemek üzere bir kılavuz görünümü ekleyin.

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample1.aspx)]

## <a name="define-the-select-method"></a>Select metodunu tanımlama

**Courses.aspx.cs**' de, Select yöntemini Grid görünümünün **SelectMethod** özelliğinde belirttiğiniz adla eklersiniz. Bu yöntemde, öğrencinin kurslarını almak için sorgu tanımlayacaksınız ve parametrenin parametreyle aynı ada sahip bir sorgu dizesi değerinden geldiğini belirtmeniz gerekir.

İlk olarak, aşağıdaki **using** deyimlerini eklemeniz gerekir.

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample2.cs)]

Ardından, aşağıdaki kodu Courses.aspx.cs öğesine ekleyin:

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample3.cs)]

QueryString özniteliği, bu yöntemdeki parametreye otomatik olarak Studentitıd adlı bir sorgu dizesi atanır.

## <a name="add-hyperlink-with-query-string-value"></a>Sorgu dizesi değeri olan köprü ekleme

Öğrenciler. aspx üzerinde kılavuz görünümünde, yeni kurslar sayfanıza bağlanan bir köprü alanı ekleyeceksiniz. Köprü, öğrencinin kimliğiyle bir sorgu dizesi değeri içerecektir.

Öğrenciler. aspx ' te, toplam krediler için alanın hemen altındaki kılavuz görünümü sütunlarına aşağıdaki alanı ekleyin.

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample4.aspx?highlight=7-8)]

Uygulamayı çalıştırın ve kılavuz görünümünün şimdi kurslar bağlantısını içerdiğine dikkat edin.

![Köprü Ekle](using-query-string-values-to-retrieve-data/_static/image1.png)

Bağlantılardan birine tıkladığınızda, öğrencinin kayıtlı kurslarını görürsünüz.

![kursları göster](using-query-string-values-to-retrieve-data/_static/image2.png)

## <a name="conclusion"></a>Sonuç

Bu öğreticide, sorgu dizesi değeri olan bir bağlantı eklediniz. Select yöntemindeki parametre değeri için bu sorgu dizesi değerini kullandınız.

Sonraki [öğreticide](adding-business-logic-layer.md), kodu arka plan kod dosyalarından iş mantığı katmanına ve veri erişim katmanına taşıyacaksınız.

> [!div class="step-by-step"]
> [Önceki](integrating-jquery-ui.md)
> [İleri](adding-business-logic-layer.md)
