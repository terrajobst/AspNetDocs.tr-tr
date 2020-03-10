---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
title: Denetleyici oluşturma (C#) | Microsoft Docs
author: StephenWalther
description: Bu öğreticide, Stephen Walther bir ASP.NET MVC uygulamasına nasıl denetleyici ekleyebileceğiniz gösterilmektedir.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 719d50d4-2305-454c-98b4-bae64937c48f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
msc.type: authoredcontent
ms.openlocfilehash: 6e3d0bae7f07410637c2b06c500d94a02c821f5c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544081"
---
# <a name="creating-a-controller-c"></a>Denetleyici Oluşturma (C#)

ile [Stephen Walther](https://github.com/StephenWalther)

> Bu öğreticide, Stephen Walther bir ASP.NET MVC uygulamasına nasıl denetleyici ekleyebileceğiniz gösterilmektedir.

Bu öğreticinin amacı, yeni ASP.NET MVC denetleyicilerini nasıl oluşturabileceğiniz açıklanmaktadır. Visual Studio denetleyici Ekle menü seçeneğini kullanarak ve el ile bir sınıf dosyası oluşturarak denetleyiciler oluşturmayı öğreneceksiniz.

### <a name="using-the-add-controller-menu-option"></a>Denetleyici Ekle menü seçeneğini kullanma

Yeni bir denetleyici oluşturmanın en kolay yolu, Visual Studio Çözüm Gezgini penceresinde Controllers klasörüne sağ tıklayıp **Ekle, denetleyici** menü seçeneğini (bkz. Şekil 1) seçer. Bu menü seçeneği belirlendiğinde, **Denetleyici Ekle** iletişim kutusu açılır (bkz. Şekil 2).

[Yeni proje iletişim kutusunu ![](creating-a-controller-cs/_static/image1.jpg)](creating-a-controller-cs/_static/image1.png)

**Şekil 01**: yeni bir denetleyici ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-controller-cs/_static/image2.png))

[Yeni proje iletişim kutusunu ![](creating-a-controller-cs/_static/image2.jpg)](creating-a-controller-cs/_static/image3.png)

**Şekil 02**: denetleyici Ekle iletişim kutusu ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-controller-cs/_static/image4.png))

Denetleyici adının ilk bölümünün **Denetleyici Ekle** iletişim kutusunda vurgulandığına dikkat edin. Her denetleyici adının son ek *denetleyicisiyle*bitmesi gerekir. Örneğin, *ProductController* adlı bir denetleyici oluşturabilirsiniz, ancak *ürün*adında bir denetleyici oluşturamazsınız.

*Denetleyici* son eki eksik olan bir denetleyici oluşturursanız, denetleyiciyi çağıramazsınız. Bunu yapma-bu hata yapıldıktan sonra hayata daha az saat harcandım.

**Listeleme 1-Controllers\ProductController.cs**

[!code-csharp[Main](creating-a-controller-cs/samples/sample1.cs)]

Denetleyiciler klasöründe her zaman denetleyici oluşturmanız gerekir. Aksi takdirde, ASP.NET MVC 'nin kurallarını ihlal edersiniz ve diğer geliştiriciler uygulamanızı daha zor bir zamana göre anlayacaktır.

### <a name="scaffolding-action-methods"></a>Yapı iskelesi eylem yöntemleri

Bir denetleyici oluşturduğunuzda, otomatik olarak Create, Update ve details eylem yöntemleri oluşturma seçeneğiniz vardır (bkz. Şekil 3). Bu seçeneği belirlerseniz, liste 2 ' deki denetleyici sınıfı oluşturulur.

[eylem yöntemlerini otomatik olarak oluşturma ![](creating-a-controller-cs/_static/image3.jpg)](creating-a-controller-cs/_static/image5.png)

**Şekil 03**: otomatik olarak eylem yöntemleri oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-controller-cs/_static/image6.png))

**Listeleme 2-Controllers\CustomerController.cs**

[!code-csharp[Main](creating-a-controller-cs/samples/sample2.cs)]

Bu oluşturulan Yöntemler saplama yöntemleridir. Müşterinin ayrıntılarını oluşturmak, güncelleştirmek ve göstermek için gerçek mantığı eklemeniz gerekir. Ancak, saplama yöntemleri size iyi bir başlangıç noktası sağlar.

### <a name="creating-a-controller-class"></a>Denetleyici sınıfı oluşturma

ASP.NET MVC denetleyicisi yalnızca bir sınıftır. İsterseniz, uygun bir Visual Studio denetleyicisi yapı iskelesi yoksayabilirsiniz ve el ile bir denetleyici sınıfı oluşturabilirsiniz. Aşağıdaki adımları uygulayın:

1. Denetleyiciler klasörüne sağ tıklayın ve **Ekle, yeni öğe** menü seçeneğini belirleyin ve **sınıf** şablonunu seçin (bkz. Şekil 4).
2. Yeni sınıfı PersonController.cs olarak adlandırın ve **Ekle** düğmesine tıklayın.
3. Elde edilen sınıf dosyasını, sınıfın temel System. Web. Mvc. Controller sınıfından devrayor şekilde değiştirin (bkz. Listeleme 3).

[Yeni bir sınıf oluşturma ![](creating-a-controller-cs/_static/image4.jpg)](creating-a-controller-cs/_static/image7.png)

**Şekil 04**: yeni bir sınıf oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-controller-cs/_static/image8.png))

**Listeleme 3-Controllers\PersonController.cs**

[!code-csharp[Main](creating-a-controller-cs/samples/sample3.cs)]

Listeleme 3 ' teki denetleyici, "Merhaba Dünya!" dizesini döndüren Index () adlı bir eylem gösterir. Uygulamanızı çalıştırarak ve aşağıdakine benzer bir URL isteğinde bulunarak bu denetleyici eylemini çağırabilirsiniz:

`http://localhost:40071/Person`

> [!NOTE]
> 
> ASP.NET geliştirme sunucusu rastgele bir bağlantı noktası numarası kullanır (örneğin, 40071). Denetleyiciyi çağırmak için bir URL girerken, doğru bağlantı noktası numarasını sağlamanız gerekir. Farenizi Windows bildirim alanındaki (ekranınızın sağ alt tarafındaki) ASP.NET geliştirme sunucusu simgesinin üzerine getirerek bağlantı noktası numarasını belirleyebilirsiniz.
> 
> [!div class="step-by-step"]
> [Önceki](adding-dynamic-content-to-a-cached-page-cs.md)
> [İleri](creating-an-action-cs.md)
