---
uid: web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
title: Model bağlama ve Web formlarıyla verileri sıralama, sayfalama ve filtreleme | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir. Model bağlama, veri etkileşimini daha düz-... hale getirir
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 266e7866-e327-4687-b29d-627a0925e87d
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
msc.type: authoredcontent
ms.openlocfilehash: f8e64392af6110f36c6af98c4e4e9481c94a0d82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78548064"
---
# <a name="sorting-paging-and-filtering-data-with-model-binding-and-web-forms"></a>Model bağlama ve Web formlarıyla verileri sıralama, sayfalama ve filtreleme

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir. Model bağlama veri kaynağı nesneleriyle (örneğin, ObjectDataSource veya SqlDataSource) çok daha basit hale getirir. Bu seri giriş malzemesiyle başlar ve sonraki öğreticilerde daha gelişmiş kavramlara gider.
> 
> Bu öğretici, model bağlama aracılığıyla verilerin nasıl sıralanması, sayfalama ve filtrelemesinin ekleneceğini gösterir.
> 
> Bu öğreticide, serinin ilk [bölümünde](retrieving-data.md) oluşturulan proje oluşturulur.
> 
> Tüm projeyi [](https://go.microsoft.com/fwlink/?LinkId=286116) C# veya vb 'ye indirebilirsiniz. İndirilebilir kod, Visual Studio 2012 veya Visual Studio 2013 ile birlikte kullanılabilir. Bu öğreticide gösterilen Visual Studio 2013 şablonundan biraz farklı olan Visual Studio 2012 şablonunu kullanır.

## <a name="what-youll-build"></a>Ne oluşturacağız?

Bu öğreticide şunları yapmanız gerekir:

1. Verilerin sıralanmasını ve Sayfalamayı Etkinleştir
2. Kullanıcı tarafından seçime bağlı olarak verilerin filtrelenmesini etkinleştir

## <a name="add-sorting"></a>Sıralama Ekle

GridView 'da sıralamayı etkinleştirmek çok kolaydır. Öğrenci. aspx dosyasında, GridView 'da **Allowsıralamayı** **true** olarak ayarlamanız yeterlidir. DataField 'in otomatik olarak kullanıldığı için her sütun için bir **SortExpression** değeri ayarlamanız gerekmez. GridView, verileri seçili değere göre sıralamayı dahil etmek için sorguyu değiştirir. Aşağıdaki vurgulanan kod, sıralamayı etkinleştirmek için yapmanız gereken ek eki gösterir.

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample1.aspx?highlight=5)]

Web uygulamasını çalıştırın ve farklı sütunlardaki değerlere göre öğrenci kayıtlarını sıralamayı test edin.

![öğrencileri Sırala](sorting-paging-and-filtering-data/_static/image2.png)

## <a name="add-paging"></a>Sayfalama Ekle

Sayfalama özelliğinin etkinleştirilmesi de çok kolaydır. GridView 'da, **AllowPaging** özelliğini **true** olarak ayarlayın ve **PageSize** özelliğini her sayfada görüntülenmesini istediğiniz kayıt sayısı olarak ayarlayın. Bu öğreticide, 4 olarak ayarlayabilirsiniz.

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample2.aspx?highlight=5)]

Web uygulamasını çalıştırın ve şimdi kayıtların tek bir sayfada 4 ' ten fazla kayıt görüntülenmeksizin birden çok sayfanın üzerine bölündiğine dikkat edin.

![Sayfalama Ekle](sorting-paging-and-filtering-data/_static/image4.png)

Ertelenmiş sorgu yürütme, uygulama verimliliğini geliştirir. GridView, tüm veri kümesini almak yerine yalnızca geçerli sayfanın kayıtlarını almak için sorguyu değiştirir.

## <a name="filter-records-by-user-selection"></a>Kayıtları Kullanıcı seçimine göre filtrele

Model bağlama, bir model bağlama yönteminde bir parametre için değer ayarlamayı tanımlamanızı sağlayan birkaç öznitelik ekler. Bu öznitelikler **System. Web. ModelBinding** ad alanıdır. Bunlara aşağıdakiler dahildir:

- Denetim
- Tanımlama Bilgisi
- Form
- Profil
- QueryString
- RouteData
- Oturum
- UserProfile
- ViewState

Bu öğreticide, GridView 'da görüntülenecek kayıtları filtrelemek için bir denetimin değerini kullanacaksınız. Daha önce oluşturduğunuz sorgu yöntemine **Denetim** özniteliğini ekleyeceksiniz. [Sonraki](using-query-string-values-to-retrieve-data.md) bir öğreticide, parametre değerinin bir sorgu dizesi değerinden geldiğini belirtmek için **QueryString** özniteliğini bir parametreye uygulayacaksınız.

İlk olarak, ValidationSummary 'nin üzerinde gösterilen öğrencileri filtrelemek için bir açılır liste ekleyin.

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample3.aspx?highlight=3-11)]

Arka plan kod dosyasında, select metodunu, denetimden bir değer alacak şekilde değiştirin ve parametrenin adını değeri sağlayan denetimin adı olarak ayarlayın.

Denetim özniteliğini çözümlemek için **System. Web. ModelBinding** ad alanı için bir **using** ifadesini eklemeniz gerekir.

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample4.cs)]

Aşağıdaki kod, döndürülen verileri açılan liste değerine göre filtrelemek için Select yöntemini yeniden çalıştı ' ı gösterir. Bir parametre önüne bir denetim özniteliği eklemek, bu parametrenin değerinin aynı ada sahip bir denetimden geldiğini belirtir.

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample5.cs)]

Öğrenciler listesini filtrelemek için Web uygulamasını çalıştırın ve açılan listeden farklı değerler seçin.

![öğrencileri filtrele](sorting-paging-and-filtering-data/_static/image6.png)

## <a name="conclusion"></a>Sonuç

Bu öğreticide, verileri sıralamayı ve sayfalama 'yi etkinleştirdiniz. Ayrıca, verileri bir denetimin değerine göre filtrelemeyi de etkinleştirmiş olursunuz.

Sonraki [öğreticide](integrating-jquery-ui.md) , jQuery UI pencere öğesini dinamik veri şablonuyla TÜMLEŞTIREREK Kullanıcı arabirimini geliştirebilirsiniz.

> [!div class="step-by-step"]
> [Önceki](updating-deleting-and-creating-data.md)
> [İleri](integrating-jquery-ui.md)
