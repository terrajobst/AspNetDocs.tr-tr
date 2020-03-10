---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
title: ASP.NET MVC yönlendirmeye genel bakış (VB) | Microsoft Docs
author: StephenWalther
description: Bu öğreticide, Stephen Walther, ASP.NET MVC çerçevesinin Tarayıcı isteklerini denetleyici eylemlerine nasıl eşlediğini gösterir.
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 4bc8d19a-80f1-44b4-adbf-95ed22d691ca
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: ed043d76b89ce31945cf3423b0c5afca9383cc21
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601537"
---
# <a name="aspnet-mvc-routing-overview-vb"></a>ASP.NET MVC Yönlendirmesine Genel Bakış (VB)

ile [Stephen Walther](https://github.com/StephenWalther)

> Bu öğreticide, Stephen Walther, ASP.NET MVC çerçevesinin Tarayıcı isteklerini denetleyici eylemlerine nasıl eşlediğini gösterir.

Bu öğreticide, *ASP.net yönlendirme*adlı her ASP.NET MVC uygulamasının önemli bir özelliğine sunulmuştur. ASP.NET yönlendirme modülü, gelen tarayıcı isteklerini belirli MVC denetleyici eylemlerine eşlemeden sorumludur. Bu öğreticinin sonunda standart yol tablosunun istekleri denetleyici eylemlerine nasıl eşlediğini anlamış olursunuz.

## <a name="using-the-default-route-table"></a>Varsayılan yol tablosunu kullanma

Yeni bir ASP.NET MVC uygulaması oluşturduğunuzda uygulama zaten ASP.NET yönlendirme kullanmak üzere yapılandırılmıştır. ASP.NET yönlendirme iki yerde kurulumlardır.

İlk olarak, ASP.NET yönlendirme uygulamanızın Web yapılandırma dosyasında (Web. config dosyası) etkinleştirilir. Yapılandırma dosyasında yönlendirmeyle ilgili dört bölüm vardır: System. Web. httpModules bölümü, System. Web. httpHandlers bölümü, System. webserver. Modules bölümü ve System. webserver. Handlers bölümü. Bu bölüm yönlendirmenin artık çalışmadığı için, bu bölümleri silmemeye dikkat edin.

İkinci ve daha önemlisi, uygulamanın Global. asax dosyasında bir yol tablosu oluşturulur. Global. asax dosyası, ASP.NET uygulama yaşam döngüsü olayları için olay işleyicileri içeren özel bir dosyadır. Yol tablosu, uygulama başlatma olayı sırasında oluşturulur.

Listeleme 1 ' deki dosya, bir ASP.NET MVC uygulaması için varsayılan Global. asax dosyasını içerir.

**Listeleme 1-Global. asax. vb**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample1.vb)]

MVC uygulaması ilk kez başlatıldığında, uygulama\_Start () yöntemi çağrılır. Bu yöntem, sırasıyla RegisterRoutes () yöntemini çağırır. RegisterRoutes () yöntemi yol tablosu oluşturur.

Varsayılan yol tablosu, tek bir yol içerir (varsayılan olarak adlandırılır). Varsayılan yol bir URL 'nin ilk segmentini bir denetleyici adına, bir URL 'nin ikinci kesimini bir denetleyici eylemine ve üçüncü segmenti **ID**adlı bir parametreye eşler.

Web tarayıcınızın adres çubuğuna aşağıdaki URL 'YI girdiğinizi varsayın:

/Home/Index/3

Varsayılan yol bu URL 'YI aşağıdaki parametrelerle eşler:

- denetleyici = ana

- eylem = Dizin

- kimlik = 3

/Home/Index/3 URL 'sini istediğinizde, aşağıdaki kod yürütülür:

HomeController.Index(3)

Varsayılan yol, üç parametre için varsayılan değerleri içerir. Bir denetleyici belirtmezseniz, denetleyici parametresi varsayılan olarak **giriş**değerini alır. Bir eylem belirtmezseniz, eylem parametresi varsayılan değer **dizinine**göre yapılır. Son olarak, bir kimlik belirtmezseniz, ID parametresi varsayılan olarak boş bir dize olur.

Varsayılan yolun, URL 'Leri denetleyici eylemlerine nasıl eşlediğini gösteren bazı örneklere bakalım. Tarayıcınızın adres çubuğuna aşağıdaki URL 'YI girdiğinizi varsayın:

/Home

Varsayılan yol parametresi Varsayılanları nedeniyle, bu URL 'YI girmek, liste 2 ' deki HomeController sınıfının Index () yönteminin çağrılmasına neden olur.

**Listeleme 2-HomeController. vb**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample2.vb)]

Liste 2 ' de HomeController sınıfı, ID adlı tek bir parametreyi kabul eden Index () adlı bir yöntemi içerir. /Home URL 'SI, dizin () yönteminin ID parametresinin değeri olarak Nothing değeri ile çağrılmasına neden olur.

MVC çerçevesinin denetleyici eylemlerini çağırdığı şekilde,/Home URL 'SI, liste 3 ' teki HomeController sınıfının Index () yöntemiyle de eşleşir.

**Kod 3-HomeController. vb (parametre olmadan dizin eylemi)**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample3.vb)]

Listeleme 3 ' teki Index () yöntemi herhangi bir parametre kabul etmez. /Home URL 'SI, bu dizin () yönteminin çağrılmasına neden olur. /Home/Index/3 URL 'SI de bu yöntemi çağırır (kimlik yoksayıldı).

/Home URL 'SI, liste 4 ' teki HomeController sınıfının Index () yöntemiyle de eşleşir.

**4-HomeController. vb dosyasını (null yapılabilir parametresiyle Dizin eylemi) listeleme**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample4.vb)]

Liste 4 ' te, Index () yönteminde bir tamsayı parametresi vardır. Parametre null yapılabilir bir parametre olduğundan (değer Nothing olabilir), dizin () bir hata oluşturulmadan çağrılabilir.

Son olarak, kod parametresi null atanabilir bir parametre *olmadığından* , ana sayfa URL 'si olan 5. liste ile dizin () yöntemini çağırmak özel duruma neden olur. Index () yöntemini çağırmaya çalışırsanız Şekil 1 ' de hata alırsınız.

**Listeleme 5-HomeController. vb (kimlik parametresiyle Dizin eylemi)**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample5.vb)]

[bir parametre değeri bekleyen bir denetleyici eylemini çağırma ![](asp-net-mvc-routing-overview-vb/_static/image1.jpg)](asp-net-mvc-routing-overview-vb/_static/image1.png)

**Şekil 01**: parametre değeri bekleyen bir denetleyici eylemi çağırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](asp-net-mvc-routing-overview-vb/_static/image2.png))

Diğer yandan,/Home/Index/3 URL 'SI, kod 5 ' teki Dizin denetleyicisi eylemiyle sorunsuz bir şekilde çalışıyor. /Home/Index/3 isteği, dizin () yönteminin 3 değerine sahip bir kimlik parametresiyle çağrılmasına neden olur.

## <a name="summary"></a>Özet

Bu öğreticinin amacı size ASP.NET yönlendirme hakkında kısa bir giriş sunmaktır. Yeni bir ASP.NET MVC uygulamasıyla aldığınız varsayılan yol tablosunu inceledik. Varsayılan yolun URL 'Leri denetleyici eylemlerine nasıl eşlediğini öğrendiniz.

> [!div class="step-by-step"]
> [Önceki](creating-an-action-cs.md)
> [İleri](understanding-action-filters-vb.md)
