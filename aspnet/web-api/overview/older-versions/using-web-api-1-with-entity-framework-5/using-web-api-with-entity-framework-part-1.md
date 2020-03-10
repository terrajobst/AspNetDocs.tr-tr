---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
title: '1\. Bölüm: projeyi genel bakış ve oluşturma | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: 94421d86-68c4-4471-bf5f-82d654a17252
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
msc.type: authoredcontent
ms.openlocfilehash: a76a18f2bd95969358452085ef342fdca8a386e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556079"
---
# <a name="part-1-overview-and-creating-the-project"></a>1\. Bölüm: projeyi genel bakış ve oluşturma

, [Mike te son](https://github.com/MikeWasson)

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

Entity Framework bir nesne/ilişkisel eşleme çerçevesidir. Kodunuzda bulunan etki alanı nesnelerini bir ilişkisel veritabanındaki varlıklara eşler. En çok bölüm için, Entity Framework veritabanı katmanı hakkında endişelenmenize gerek kalmaz. Kodunuz nesneleri yönetir ve değişiklikler bir veritabanında kalıcı hale getirilir.

## <a name="about-the-tutorial"></a>Öğretici hakkında

Bu öğreticide, basit bir mağaza uygulaması oluşturacaksınız. Uygulamanın iki ana bölümü vardır. Normal kullanıcılar ürünleri görüntüleyebilir ve sipariş oluşturabilir:

![](using-web-api-with-entity-framework-part-1/_static/image1.png)

Yöneticiler ürünleri oluşturabilir, silebilir veya düzenleyebilir:

![](using-web-api-with-entity-framework-part-1/_static/image2.png)

## <a name="skills-youll-learn"></a>Öğrenmeniz gereken yetenekler

Öğrenirsiniz:

- ASP.NET Web API 'SI ile Entity Framework nasıl kullanılır.
- Dinamik istemci kullanıcı arabirimi oluşturmak için altını gizleme. js kullanma.
- Kullanıcıların kimliğini doğrulamak için Web API 'siyle Forms kimlik doğrulaması kullanma.

Bu öğretici kendine dahil olsa da, önce aşağıdaki öğreticileri okumak isteyebilirsiniz:

- [Ilk ASP.NET Web API 'niz](../../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)
- [CRUD Işlemlerini destekleyen bir Web API 'SI oluşturma](../creating-a-web-api-that-supports-crud-operations.md)

[ASP.NET MVC](../../../../mvc/index.md) 'nin bazı bilgileri de yararlıdır.

## <a name="overview"></a>Genel bakış

Yüksek düzeyde, uygulamanın mimarisi aşağıda verilmiştir:

- ASP.NET MVC, istemci için HTML sayfalarını oluşturur.
- ASP.NET Web API 'SI, veriler üzerinde CRUD işlemleri gösterir (ürünler ve siparişler).
- Entity Framework Web API C# 'si tarafından kullanılan modelleri veritabanı varlıklarına çevirir.

![](using-web-api-with-entity-framework-part-1/_static/image3.png)

Aşağıdaki diyagramda, etki alanı nesnelerinin uygulamanın çeşitli katmanlarında nasıl temsil edildiği gösterilmektedir: veritabanı katmanı, nesne modeli ve son olarak HTTP aracılığıyla istemciye veri aktarmak için kullanılan Tel biçimi.

![](using-web-api-with-entity-framework-part-1/_static/image4.png)

## <a name="create-the-visual-studio-project"></a>Visual Studio projesi oluşturma

Visual Web Developer Express ya da Visual Studio 'nun tam sürümünü kullanarak öğretici projesi oluşturabilirsiniz.

**Başlangıç** sayfasından **Yeni proje**' ye tıklayın.

**Şablonlar** bölmesinde, **yüklü şablonlar** ' ı seçin ve **görsel C#**  düğümünü genişletin. **Görsel C#** bölümünde **Web**' i seçin. Proje şablonları listesinde **ASP.NET MVC 4 Web uygulaması**' nı seçin. Projeyi "ProductStore" olarak adlandırın ve **Tamam**' a tıklayın.

![](using-web-api-with-entity-framework-part-1/_static/image5.png)

**Yeni ASP.NET MVC 4 proje** Iletişim kutusunda **Internet uygulaması** ' nı seçin ve **Tamam**' ı tıklatın.

![](using-web-api-with-entity-framework-part-1/_static/image6.png)

"Internet uygulaması" şablonu, Forms kimlik doğrulamasını destekleyen bir ASP.NET MVC uygulaması oluşturur. Uygulamayı şimdi çalıştırırsanız, zaten bazı özellikler vardır:

- Yeni kullanıcılar, sağ üst köşedeki "Kaydet" bağlantısına tıklayarak kayıt yapabilir.
- Kayıtlı kullanıcılar "oturum aç" bağlantısına tıklayarak oturum açabilirler.

Üyelik bilgileri otomatik olarak oluşturulan bir veritabanında kalıcı hale getirilir. ASP.NET MVC 'de Forms kimlik doğrulaması hakkında daha fazla bilgi için bkz. [Izlenecek yol: ASP.NET MVC 'de form kimlik doğrulamasını kullanma](https://msdn.microsoft.com/library/ff398049(VS.98).aspx).

## <a name="update-the-css-file"></a>CSS dosyasını güncelleştirme

Bu adım yüzeysel 'dir, ancak sayfaların önceki ekran görüntüleri gibi işlemesini sağlayacak.

Çözüm Gezgini, Içerik klasörünü genişletin ve site. css adlı dosyayı açın. Aşağıdaki CSS stillerini ekleyin:

[!code-css[Main](using-web-api-with-entity-framework-part-1/samples/sample1.css)]

> [!div class="step-by-step"]
> [Next](using-web-api-with-entity-framework-part-2.md)
