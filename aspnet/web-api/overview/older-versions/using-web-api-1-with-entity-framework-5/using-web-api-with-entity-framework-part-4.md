---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
title: '4\. Bölüm: yönetici görünümü ekleme | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 792f4513-a508-4d14-a0dd-1a2fe282c7bb
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
msc.type: authoredcontent
ms.openlocfilehash: 664aeb33031e933322886a6d6bdd989277e9fda2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600008"
---
# <a name="part-4-adding-an-admin-view"></a>4\. Bölüm: yönetici görünümü ekleme

, [Mike te son](https://github.com/MikeWasson)

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-view"></a>Yönetici görünümü ekleme

Şimdi istemci tarafına ve yönetici denetleyicisinden veri kullanabilen bir sayfa ekleyecek. Bu sayfa, kullanıcıların denetleyiciye AJAX istekleri göndererek ürün oluşturmalarına, düzenlemesine veya silmesine izin verir.

Çözüm Gezgini, denetleyiciler klasörünü genişletin ve HomeController.cs adlı dosyayı açın. Bu dosya bir MVC denetleyicisi içeriyor. `Admin`adlı bir yöntem ekleyin:

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample1.cs)]

**Httprouteurl** yöntemi, Web API 'sine URI 'yi oluşturur ve bunu daha sonra Görünüm çantasında depoluyoruz.

Sonra, metin imlecini `Admin` Action yönteminin içinde konumlandırın, sonra sağ tıklayıp **Görünüm Ekle**' yi seçin. Bu işlem, **Görünüm Ekle** iletişim kutusunu getirir.

![](using-web-api-with-entity-framework-part-4/_static/image1.png)

**Görünüm Ekle** iletişim kutusunda "Yönetici" görünümünü adlandırın. **Kesin olarak belirlenmiş görünüm oluştur**etiketli onay kutusunu seçin. **Model sınıfı**altında "Product (productstore. modeller)" öğesini seçin. Diğer tüm seçenekleri varsayılan değerler olarak bırakın.

![](using-web-api-with-entity-framework-part-4/_static/image2.png)

**Ekle** ' ye tıklamak, görünümler/giriş bölümünde admin. cshtml adlı bir dosya ekler. Bu dosyayı açın ve aşağıdaki HTML 'yi ekleyin. Bu HTML sayfanın yapısını tanımlar, ancak henüz hiçbir işlev kablolu değildir.

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample2.cshtml)]

## <a name="create-a-link-to-the-admin-page"></a>Yönetici sayfasına bağlantı oluştur

Çözüm Gezgini, görünümler klasörünü genişletin ve ardından paylaşılan klasörü genişletin. \_Layout. cshtml adlı dosyayı açın. ID = "Menu" olan **ul** öğesini ve yönetici görünümü için bir eylem bağlantısını bulun:

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample3.cshtml)]

> [!NOTE]
> Örnek projede, "logonuzu buraya" yazmanız gibi birkaç başka yüzeysel değişikliği yaptık. Bunlar, uygulamanın işlevselliğini etkilemez. Projeyi indirebilir ve dosyaları karşılaştırabilirsiniz.

Uygulamayı çalıştırın ve giriş sayfasının en üstünde görünen "Yönetici" bağlantısına tıklayın. Yönetici sayfası aşağıdaki gibi görünmelidir:

![](using-web-api-with-entity-framework-part-4/_static/image3.png)

Şu anda sayfa hiçbir şey yapmaz. Bir sonraki bölümde, dinamik bir kullanıcı arabirimi oluşturmak için altını gizleme. js ' yi kullanacağız.

## <a name="add-authorization"></a>Yetkilendirme Ekle

Yönetici sayfasına şu anda siteyi ziyaret eden herkes erişebilir. Bunu, yöneticilere izinleri kısıtlamak için değiştirelim.

Bir "Yönetici" rolü ve bir yönetici kullanıcı ekleyerek başlayın. Çözüm Gezgini, filtreler klasörünü genişletin ve InitializeSimpleMembershipAttribute.cs adlı dosyayı açın. `SimpleMembershipInitializer` oluşturucusunu bulun. **WebSecurity. InitializeDatabaseConnection**çağrısından sonra aşağıdaki kodu ekleyin:

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample4.cs)]

Bu, "Yönetici" rolünü eklemenin ve rol için bir kullanıcı oluşturmanın hızlı ve kirli bir yoludur.

Çözüm Gezgini, denetleyiciler klasörünü genişletin ve HomeController.cs dosyasını açın. `Admin` metoduna **Yetkilendir** özniteliğini ekleyin.

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample5.cs)]

AdminController.cs dosyasını açın ve tüm `AdminController` sınıfına **Yetkilendir** özniteliğini ekleyin.

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample6.cs)]

> [!NOTE]
> MVC ve Web API 'SI, farklı ad alanlarında **Yetkilendirme** özniteliklerini tanımlar. MVC, **System. Web. Mvc. AuthorizeAttribute**kullanır, Web API 'si **System. Web. http. AuthorizeAttribute**kullanır.

Artık yönetici sayfasını yalnızca yöneticiler görüntüleyebilir. Ayrıca, yönetici denetleyicisine bir HTTP isteği gönderirseniz, istek bir kimlik doğrulama tanımlama bilgisi içermelidir. Aksi takdirde, sunucu bir HTTP 401 (yetkisiz) yanıtı gönderir. Bunu, `http://localhost:*port*/api/admin`için bir GET isteği göndererek Fiddler 'da görebilirsiniz.

> [!div class="step-by-step"]
> [Önceki](using-web-api-with-entity-framework-part-3.md)
> [İleri](using-web-api-with-entity-framework-part-5.md)
