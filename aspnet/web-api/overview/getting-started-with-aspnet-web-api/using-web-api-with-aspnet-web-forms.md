---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: ASP.NET Web Forms-ASP.NET 4. x ile Web API 'sini kullanma
author: MikeWasson
description: ASP.NET 4. x için ASP.NET Forms uygulamasına Web API 'SI eklemek üzere kod adım adım ile öğretici
ms.author: riande
ms.date: 04/03/2012
ms.custom: seoapril2019
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: ae553b62998fefd128e12711cbde958ea42d8c63
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556779"
---
# <a name="using-web-api-with-aspnet-web-forms"></a>ASP.NET Web Forms ile Web API Kullanma

, [Mike te son](https://github.com/MikeWasson)

Bu öğretici, ASP.NET 4. x içindeki geleneksel bir ASP.NET Web Forms uygulamasına Web API 'SI ekleme adımlarında size yol gösterir. 

## <a name="overview"></a>Genel bakış

ASP.NET Web API 'SI ASP.NET MVC ile paketlense de, Web API 'sini geleneksel bir ASP.NET Web Forms uygulamasına eklemek kolaydır.

Web API 'sini bir Web Forms uygulamasında kullanmak için iki ana adım vardır:

- **Apicontroller** sınıfından türetilen BIR Web API denetleyicisi ekleyin.
- **Uygulama\_start** yöntemine bir yol tablosu ekleyin.

## <a name="create-a-web-forms-project"></a>Web Forms projesi oluşturma

Visual Studio 'Yu başlatın ve **Başlangıç** sayfasından **Yeni proje** ' yi seçin. Ya da **Dosya** menüsünde **Yeni** ' yi ve ardından **Proje**' yi seçin.

**Şablonlar** bölmesinde, **yüklü şablonlar** ' ı seçin ve **görsel C#**  düğümünü genişletin. **Görsel C#** bölümünde **Web**' i seçin. Proje şablonları listesinde **ASP.NET Web Forms uygulama**' yı seçin. Proje için bir ad girin ve **Tamam**' a tıklayın.

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a>Modeli ve denetleyiciyi oluşturma

Bu [öğretici, başlangıç öğreticisiyle](tutorial-your-first-web-api.md) aynı model ve denetleyici sınıflarını kullanır.

İlk olarak, bir model sınıfı ekleyin. **Çözüm Gezgini**, projeye sağ tıklayın ve **Sınıf Ekle**' yi seçin. Sınıf ürününü adlandırın ve aşağıdaki uygulamayı ekleyin:

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

Sonra, projeye bir Web API denetleyicisi ekleyin. bir *Denetleyici* , Web API 'SI için http isteklerini işleyen nesnedir.

**Çözüm Gezgini**, projeye sağ tıklayın. **Yeni öğe Ekle**' yi seçin.

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

**Yüklü şablonlar**altında, **görsel C#**  ' i genişletin ve **Web**' i seçin. Ardından, şablonlar listesinden **Web API denetleyici sınıfı**' nı seçin. Denetleyiciyi "ProductsController" olarak adlandırın ve **Ekle**' ye tıklayın.

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

**Yeni öğe ekleme** sihirbazı, ProductsController.cs adlı bir dosya oluşturur. Sihirbazın dahil olduğu yöntemleri silin ve aşağıdaki yöntemleri ekleyin:

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

Bu denetleyicideki kod hakkında daha fazla bilgi için bkz. [Başlangıç](tutorial-your-first-web-api.md) öğreticisi.

## <a name="add-routing-information"></a>Yönlendirme bilgilerini ekle

Daha sonra, &quot;/api/Products/&quot; formundaki URI 'Lerin denetleyiciye yönlendirilmesi için bir URI yolu ekleyeceğiz.

**Çözüm Gezgini**' de, Global. asax dosyasına çift tıklayarak Global.asax.cs dosya arkasındaki kodu açın. Aşağıdaki **using** ifadesini ekleyin.

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

Ardından aşağıdaki kodu **uygulama\_başlangıç** yöntemine ekleyin:

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

Yönlendirme tabloları hakkında daha fazla bilgi için bkz. [ASP.NET Web API 'de yönlendirme](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).

## <a name="add-client-side-ajax"></a>Istemci tarafı AJAX ekleme

Bu, istemcilerin erişebileceği bir Web API 'SI oluşturmanız için yeterlidir. Şimdi de API 'YI çağırmak için jQuery kullanan bir HTML sayfası ekleyelim.

Ana sayfanızın (örneğin, *site. Master*) `ID="HeadContent"`bir `ContentPlaceHolder` içerdiğinden emin olun:

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

Default. aspx dosyasını açın. Ana İçerik bölümündeki ortak metni gösterildiği gibi değiştirin:

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

Sonra, `HeaderContent` bölümünde jQuery kaynak dosyasına bir başvuru ekleyin:

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

Note: dosya **Çözüm Gezgini** ' den kod Düzenleyicisi penceresine sürükleyip bırakarak betik başvurusunu kolayca ekleyebilirsiniz.

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

JQuery betiği etiketinin altında aşağıdaki betik bloğunu ekleyin:

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

Belge yüklendiğinde, bu betik API/ürün&quot;&quot;bir AJAX isteği yapar. İstek JSON biçimindeki ürünlerin bir listesini döndürür. Betik, ürün bilgilerini HTML tablosuna ekler.

Uygulamayı çalıştırdığınızda, şöyle görünmelidir:

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
