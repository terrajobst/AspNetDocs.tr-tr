---
uid: web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
title: Model bağlama ve Web formları kullanan bir projeye iş mantığı katmanı ekleme | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir. Model bağlama, veri etkileşimini daha düz-... hale getirir
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 7ef664b3-1cc8-4cbf-bb18-9f0f3a3ada2b
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
msc.type: authoredcontent
ms.openlocfilehash: a824d06d3781e11706f2a48d44ea3ad89bdb7c8b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634836"
---
# <a name="adding-business-logic-layer-to-a-project-that-uses-model-binding-and-web-forms"></a>Model bağlama ve Web formları kullanan bir projeye iş mantığı katmanı ekleme

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir. Model bağlama veri kaynağı nesneleriyle (örneğin, ObjectDataSource veya SqlDataSource) çok daha basit hale getirir. Bu seri giriş malzemesiyle başlar ve sonraki öğreticilerde daha gelişmiş kavramlara gider.
> 
> Bu öğreticide, model bağlamanın bir iş mantığı katmanıyla nasıl kullanılacağı gösterilmektedir. Veri yöntemlerini çağırmak için geçerli sayfa dışında bir nesnenin kullanıldığını belirtmek için OnCallingDataMethods üyesini ayarlayacaksınız.
> 
> Bu öğreticide, serinin [önceki](retrieving-data.md) bölümlerinde oluşturulan projede derleme yapılır.
> 
> Tüm projeyi [](https://go.microsoft.com/fwlink/?LinkId=286116) C# veya vb 'ye indirebilirsiniz. İndirilebilir kod, Visual Studio 2012 veya Visual Studio 2013 ile birlikte kullanılabilir. Bu öğreticide gösterilen Visual Studio 2013 şablonundan biraz farklı olan Visual Studio 2012 şablonunu kullanır.

## <a name="what-youll-build"></a>Ne oluşturacağız?

Model bağlama, veri etkileşimi kodunuzu bir Web sayfası için arka plan kod dosyasına veya ayrı bir iş mantığı sınıfına yerleştirmenizi sağlar. Önceki öğreticilerde, veri etkileşimi kodu için arka plan kod dosyalarının nasıl kullanılacağı gösterilmekte. Bu yaklaşım küçük siteler için geçerlidir, ancak büyük bir site korunurken kod tekrarı ve daha zorluk ortaya çıkmasına neden olabilir. Özet katman olmadığından, kod arkasında bulunan kodu programlama yoluyla test etmek de çok zor olabilir.

Veri etkileşim kodunu merkezileştirmek için verilerle etkileşimde bulunmak üzere tüm mantığı içeren bir iş mantığı katmanı oluşturabilirsiniz. Daha sonra Web sayfalarınızdaki iş mantığı katmanını çağırabilirsiniz. Bu öğreticide, önceki öğreticilerde yazdığınız kodun tümünü bir iş mantığı katmanına taşıma ve sonra bu kodu sayfalardan kullanma işlemlerinin nasıl yapılacağı gösterilmektedir.

Bu öğreticide şunları yapmanız gerekir:

1. Kodu arka plan kod dosyalarından iş mantığı katmanına taşıma
2. Veri bağlantılı denetimlerinizi iş mantığı katmanındaki yöntemleri çağırmak için değiştirin

## <a name="create-business-logic-layer"></a>İş mantığı katmanı oluşturma

Şimdi, Web sayfalarından çağrılan sınıfını oluşturacaksınız. Bu sınıftaki Yöntemler, önceki öğreticilerde kullandığınız yöntemlere benzer ve değer sağlayıcısı özniteliklerini içerir.

İlk olarak **BLL**adlı yeni bir klasör ekleyin.

![Klasör Ekle](adding-business-logic-layer/_static/image1.png)

BLL klasöründe, **SchoolBL.cs**adlı yeni bir sınıf oluşturun. Bu, başlangıçta arka plan kod dosyalarında yer alan tüm veri işlemlerini içerir. Yöntemler, arka plan kod dosyasındaki yöntemlerle neredeyse aynıdır, ancak bazı değişiklikler içerir.

Dikkat edilmesi gereken en önemli değişiklik, artık kodu **Page** sınıfının bir örneği içinden yürütmemenin bir örneğidir. Sayfa sınıfı, **TryUpdateModel** yöntemini ve **ModelState** özelliğini içerir. Bu kod bir iş mantığı katmanına taşındığında, artık bu üyeleri çağırmak için Page sınıfının bir örneğine sahip olmayacaktır. Bu sorunu çözmek için, TryUpdateModel veya ModelState 'e erişen herhangi bir yönteme **ModelMethodContext** parametresini eklemeniz gerekir. Bu ModelMethodContext parametresini TryUpdateModel ' i çağırmak veya ModelState almak için kullanırsınız. Bu yeni parametre için Web sayfasındaki herhangi bir şeyi hesaba çevirmek zorunda değilsiniz.

SchoolBL.cs içindeki kodu aşağıdaki kodla değiştirin.

[!code-csharp[Main](adding-business-logic-layer/samples/sample1.cs)]

## <a name="revise-existing-pages-to-retrieve-data-from-business-logic-layer"></a>Mevcut sayfaları, iş mantığı katmanından veri almak için gözden geçirin

Son olarak, iş mantığı katmanını kullanarak öğrenciler. aspx, Addöğrenci. aspx ve kurslar. aspx sayfalarını arka plan kod dosyasındaki sorguları kullanarak dönüştürmeniz gerekir.

Öğrenciler, Addöğrenci ve kurslar için arka plan kod dosyalarında aşağıdaki sorgu yöntemlerini silin veya not edin:

- studentsGrid\_GetData
- studentsGrid\_UpdateItem
- studentsGrid\_DeleteItem
- addStudentForm\_InsertItem
- coursesGrid\_GetData

Artık, veri işlemleriyle ilgili arka plan kod dosyasında kod içermemelidir.

**Oncallingdatamethods** olay işleyicisi, veri yöntemleri için kullanılacak bir nesne belirtmenize olanak sağlar. Öğrenciler. aspx ' te, bu olay işleyicisi için bir değer ekleyin ve veri yöntemlerinin adlarını iş mantığı sınıfındaki yöntemlerin adlarıyla değiştirin.

[!code-aspx[Main](adding-business-logic-layer/samples/sample2.aspx?highlight=3-4,8)]

Öğrenciler. aspx için arka plan kod dosyasında, CallingDataMethods olayının olay işleyicisini tanımlayın. Bu olay işleyicisinde, veri işlemleri için iş mantığı sınıfını belirtirsiniz.

[!code-csharp[Main](adding-business-logic-layer/samples/sample3.cs)]

AddStudent. aspx dosyasında benzer değişiklikler yapın.

[!code-aspx[Main](adding-business-logic-layer/samples/sample4.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample5.cs)]

Kurslar. aspx ' te benzer değişiklikler yapın.

[!code-aspx[Main](adding-business-logic-layer/samples/sample6.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample7.cs)]

Uygulamayı çalıştırın ve sayfaların tümünün daha önce olduğu gibi işlev görür. Doğrulama mantığı da doğru şekilde çalışmaktadır.

## <a name="conclusion"></a>Sonuç

Bu öğreticide, bir veri erişim katmanını ve iş mantığı katmanını kullanmak için uygulamanızı yeniden yapılandırılmıştır. Veri denetimlerinin veri işlemleri için geçerli sayfa olmayan bir nesne kullanmasını belirttiniz.

> [!div class="step-by-step"]
> [Öncekini](using-query-string-values-to-retrieve-data.md)
