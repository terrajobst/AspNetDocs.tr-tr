---
uid: web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
title: Model bağlama ve Web formları ile verileri güncelleştirme, silme ve oluşturma | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir. Model bağlama, veri etkileşimini daha düz-... hale getirir
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 602baa94-5a4f-46eb-a717-7a9e539c1db4
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
msc.type: authoredcontent
ms.openlocfilehash: 11dc52ec79ca91119b37ea60e08164eb1b1d0e2b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586648"
---
# <a name="updating-deleting-and-creating-data-with-model-binding-and-web-forms"></a>Model bağlama ve Web formları ile verileri güncelleştirme, silme ve oluşturma

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir. Model bağlama veri kaynağı nesneleriyle (örneğin, ObjectDataSource veya SqlDataSource) çok daha basit hale getirir. Bu seri giriş malzemesiyle başlar ve sonraki öğreticilerde daha gelişmiş kavramlara gider.
> 
> Bu öğreticide, model bağlama ile veri oluşturma, güncelleştirme ve silme işlemlerinin nasıl yapılacağı gösterilmektedir. Aşağıdaki özellikleri ayarlayacaksınız:
> 
> - DeleteMethod
> - InsertMethod
> - UpdateMethod
> 
> Bu özellikler, karşılık gelen işlemi işleyen yöntemin adını alır. Bu yöntemde, verilerle etkileşim kurma mantığını sağlarsınız.
> 
> Bu öğreticide, serinin ilk [bölümünde](retrieving-data.md) oluşturulan proje oluşturulur.
> 
> Tüm projeyi [](https://go.microsoft.com/fwlink/?LinkId=286116) C# veya vb 'ye indirebilirsiniz. İndirilebilir kod, Visual Studio 2012 veya Visual Studio 2013 ile birlikte kullanılabilir. Bu öğreticide gösterilen Visual Studio 2013 şablonundan biraz farklı olan Visual Studio 2012 şablonunu kullanır.

## <a name="what-youll-build"></a>Ne oluşturacağız?

Bu öğreticide şunları yapmanız gerekir:

1. Dinamik veri şablonları ekleme
2. Model bağlama yöntemleriyle verileri güncelleştirme ve silmeyi etkinleştirme
3. Veri doğrulama kurallarını uygulama-veritabanında yeni bir kayıt oluşturmayı etkinleştirin

## <a name="add-dynamic-data-templates"></a>Dinamik veri şablonları ekleme

En iyi kullanıcı deneyimini sağlamak ve kod tekrarlamayı en aza indirmek için dinamik veri şablonlarını kullanacaksınız. Önceden oluşturulmuş dinamik veri şablonlarını, bir NuGet paketi yükleyerek var olan sitenize kolayca tümleştirebilirsiniz.

**NuGet Paketlerini Yönet**' den **Dynamicdatatemplatescs**'yi yükler.

![dinamik veri şablonları](updating-deleting-and-creating-data/_static/image1.png)

Projenizin artık **DynamicData**adlı bir klasör içerdiğine dikkat edin. Bu klasörde, Web formlarınızda dinamik denetimlere otomatik olarak uygulanan şablonları bulacaksınız.

![dinamik veri klasörü](updating-deleting-and-creating-data/_static/image2.png)

## <a name="enable-updating-and-deleting"></a>Güncelleştirme ve silmeyi etkinleştir

Kullanıcıların veritabanındaki kayıtları güncelleştirmesini ve silmesini sağlamak, verileri alma sürecine çok benzer. **UpdateMethod** ve **DeleteMethod** özelliklerinde, bu işlemleri gerçekleştiren yöntemlerin adlarını belirtirsiniz. GridView denetimiyle, düzenleme ve silme düğmelerinin otomatik oluşturulmasını de belirtebilirsiniz. Aşağıdaki vurgulanan kod, GridView koduna yapılan eklemeleri gösterir.

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample1.aspx?highlight=4-5)]

Arka plan kod dosyasında, **System. Data. Entity. Infrastructure**için bir using açıklaması ekleyin.

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample2.cs)]

Ardından, aşağıdaki güncelleştirmeyi ve silme yöntemlerini ekleyin.

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample3.cs)]

**TryUpdateModel** yöntemi, Web formundan eşleşen veri bağlantılı değerleri veri öğesine uygular. Veri öğesi, ID parametresinin değerine göre alınır.

## <a name="enforce-validation-requirements"></a>Doğrulama gereksinimlerini zorla

Öğrenci sınıfındaki FirstName, LastName ve Year özelliklerine uyguladığınız doğrulama öznitelikleri, veriler güncelleştirilirken otomatik olarak zorlanır. DynamicField denetimleri, doğrulama özniteliklerine göre istemci ve sunucu Doğrulayıcıları ekler. FirstName ve LastName özelliklerinin ikisi de gereklidir. FirstName uzunluğu 20 karakteri aşamaz ve LastName 40 karakteri aşamaz. Yıl, akademik Micyear numaralandırması için geçerli bir değer olmalıdır.

Kullanıcı doğrulama gereksinimlerinden birini ihlal ederse güncelleştirme devam etmez. Hata iletisini görmek için GridView 'un üzerine bir ValidationSummary denetimi ekleyin. Model bağlamasındaki doğrulama hatalarını göstermek için **ShowModelStateErrors** özelliğini **true**olarak ayarlayın. 

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample4.aspx)]

Web uygulamasını çalıştırın ve kayıtları güncelleştirin ve silin.

![verileri güncelleştirme](updating-deleting-and-creating-data/_static/image3.png)

Düzenleme modunda Year özelliğinin değeri otomatik olarak bir açılan liste olarak işlendiğine dikkat edin. Year özelliği bir sabit listesi değeridir ve bir numaralandırma değeri için dinamik veri şablonu, düzenlemenin açılan listesini belirtir. Bu şablonu, **DynamicData**/**FieldTemplates** klasöründe **numaralandırma\_. ascx** dosyasını açarak bulabilirsiniz.

Geçerli değerler sağlarsanız güncelleştirme başarıyla tamamlanır. Doğrulama gereksinimlerinden birini ihlal ederseniz, güncelleştirme devam etmez ve kılavuzun üzerinde bir hata mesajı görüntülenir.

![hata iletisi](updating-deleting-and-creating-data/_static/image4.png)

## <a name="add-new-records"></a>Yeni kayıt Ekle

GridView denetimi **InsertMethod** özelliğini içermez ve bu nedenle model bağlamaya sahip yeni bir kayıt eklemek için kullanılamaz. InsertMethod özelliğini **FormView**, **DetailsView**veya **ListView** denetimlerinde bulabilirsiniz. Bu öğreticide yeni bir kayıt eklemek için bir FormView denetimi kullanacaksınız.

İlk olarak, yeni bir kayıt eklemek için oluşturacağınız yeni sayfanın bağlantısını ekleyin. ValidationSummary üzerinde şunu ekleyin:

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample5.aspx)]

Yeni bağlantı öğrenciler sayfasının içeriğinin en üstünde görünür.

![Yeni bağlantı](updating-deleting-and-creating-data/_static/image5.png)

Ardından, ana sayfa kullanarak yeni bir Web formu ekleyin ve **Addöğrenci**olarak adlandırın. Ana sayfa olarak site. Master ' u seçin.

**DynamicEntity** denetimini kullanarak yeni bir öğrenci eklemek için alanları oluşturacaksınız. DynamicEntity denetimi, ItemType özelliğinde belirtilen sınıfta düzenlenebilir özellikleri işler. Studentitıd özelliği, **[ScaffoldColumn (false)]** özniteliğiyle işaretlendi, bu nedenle işlenmiyor. Addöğrenci sayfasının MainContent yer tutucusuna aşağıdaki kodu ekleyin.

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample6.aspx)]

Arka plan kod dosyasında (AddStudent.aspx.cs), **Contosoüniversıtymodelbinding. model** ad alanı için bir **using** açıklaması ekleyin.

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample7.cs)]

Ardından, iptal düğmesi için nasıl yeni bir kayıt ve olay işleyicisi ekleneceğini belirtmek üzere aşağıdaki yöntemleri ekleyin.

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample8.cs)]

Tüm değişiklikleri kaydedin.

Web uygulamasını çalıştırın ve yeni bir öğrenci oluşturun.

![Yeni öğrenci Ekle](updating-deleting-and-creating-data/_static/image6.png)

**Ekle** ' ye tıklayın ve yeni öğrenciye oluşturulduğuna dikkat edin.

![Yeni öğrenci görüntüle](updating-deleting-and-creating-data/_static/image7.png)

## <a name="conclusion"></a>Sonuç

Bu öğreticide, verileri güncelleştirme, silme ve oluşturma özelliği etkinleştirilmiştir. Verilerle etkileşim kurarken doğrulama kuralları uygulanır.

Bu serinin sonraki [öğreticide](sorting-paging-and-filtering-data.md) sıralama, sayfalama ve filtreleme verilerini etkinleştirecektir.

> [!div class="step-by-step"]
> [Önceki](retrieving-data.md)
> [İleri](sorting-paging-and-filtering-data.md)
