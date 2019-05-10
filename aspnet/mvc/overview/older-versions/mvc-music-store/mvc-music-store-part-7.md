---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
title: 'Bölüm 7: Üyelik ve yetkilendirme | Microsoft Docs'
author: jongalloway
description: Bu öğretici serisinde ASP.NET MVC müzik Store örnek uygulamayı oluşturmak için gerçekleştirilen tüm adımları ayrıntılı olarak açıklanmaktadır. 7. bölüm, üyelik ve yetkilendirme kapsar.
ms.author: riande
ms.date: 10/13/2010
ms.assetid: c8511ebe-68bc-4240-87c3-d5ced84a3f37
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
msc.type: authoredcontent
ms.openlocfilehash: a6a1a936e0ea29ea36721ba78f35845401f74c01
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65112462"
---
# <a name="part-7-membership-and-authorization"></a>Bölüm 7: Üyelik ve Yetkilendirme

tarafından [Jon Galloway](https://github.com/jongalloway)

> MVC müzik Store tanıtır ve ASP.NET MVC ve Visual Studio web geliştirme için nasıl kullanılacağını adım adım anlatan bir öğretici uygulamasıdır.  
>   
> MVC müzik Store müzik albümleri çevrimiçi sattığı ve temel site yönetimi, kullanıcı oturum açma ve alışveriş sepeti işlevselliğini uygulayan bir Basit örnek deposu uygulamasıdır.  
>   
> Bu öğretici serisinde ASP.NET MVC müzik Store örnek uygulamayı oluşturmak için gerçekleştirilen tüm adımları ayrıntılı olarak açıklanmaktadır. 7. bölüm, üyelik ve yetkilendirme kapsar.

Store Yöneticisi denetleyicimizin sitemizi ziyaret eden herkes için şu anda erişilebilir. Bu site yöneticileri erişimi kısıtlamak için değiştirelim.

## <a name="adding-the-accountcontroller-and-views"></a>AccountController ve görünümleri ekleme

ASP.NET MVC 3 boş Web uygulaması şablonu tam ASP.NET MVC 3, Web uygulaması şablonu arasındaki tek fark, boş şablonu bir hesap denetleyicisi içermez ' dir. Tam bir ASP.NET MVC 3, Web uygulaması şablondan oluşturulan yeni bir ASP.NET MVC uygulamasında birkaç dosya kopyalayarak bir hesap denetleyicisi ekleyeceğiz.

Tam ASP.NET MVC 3, Web uygulaması şablonunu kullanarak yeni bir ASP.NET MVC uygulaması oluşturun ve aynı dizinlerde Projemizin aşağıdaki dosyaları kopyalayın:

1. AccountController.cs denetleyicileri dizine kopyalayın.
2. AccountModels modelleri dizine kopyalayın.
3. Görünümler dizini içinde bir hesap dizin oluşturma ve dört tüm görünümlerde kopyalayın

Bunlar MvcMusicStore ile başlar bu nedenle denetleyici ve Model sınıfları için ad alanı değiştirin. AccountController sınıfı MvcMusicStore.Controllers ad uzayını kullanmalı ve AccountModels sınıfı MvcMusicStore.Models ad uzayını kullanmalı.

*Not: Bu dosyalar, biz öğreticinin başında bizim site tasarımı dosyaları kopyalanan MvcMusicStore Assets.zip indirme mevcuttur. Üyelik dosyaları kod dizininde bulunur.*

Güncel çözümü aşağıdaki gibi görünmelidir:

![](mvc-music-store-part-7/_static/image1.png)

## <a name="adding-an-administrative-user-with-the-aspnet-configuration-site"></a>ASP.NET yapılandırma sitesi olan bir yönetici kullanıcı ekleme

Yetkilendirme Web sitemizi kılarız önce biz erişimi olan bir kullanıcı oluşturma gerekir. Bir kullanıcı oluşturmak için en kolay yolu, yerleşik ASP.NET yapılandırma Web sitesini kullanmaktır.

ASP.NET yapılandırması Web sitesi, Çözüm Gezgini'nde simgesini izleyen'ı tıklatarak başlatın.

![](mvc-music-store-part-7/_static/image2.png)

Bu, bir yapılandırma Web sitesini çalıştırır. Ana Ekran Güvenlik sekmesine tıklayın ve ardından ekranın ortasında "rollerini etkinleştir" bağlantısına tıklayın.

![](mvc-music-store-part-7/_static/image3.png)

"Rolleri oluşturma ve yönetme" bağlantısına tıklayın.

![](mvc-music-store-part-7/_static/image4.png)

Rol adı olarak "Yönetici" girin ve Rol Ekle düğmesine basın.

![](mvc-music-store-part-7/_static/image5.png)

Geri düğmesine tıklayın ve ardından sol taraftaki oluşturma kullanıcı bağlantısına tıklayın.

![](mvc-music-store-part-7/_static/image6.png)

Aşağıdaki bilgileri kullanarak soldaki kullanıcı bilgileri alanları doldurun:

| **Alan** | **Değer** |
| --- | --- |
| **Kullanıcı adı** | Yönetici |
| **Parola** | / password123! |
| **Parolayı onaylayın** | / password123! |
| **E-posta** | (herhangi bir e-posta adresi çalışır) |
| **Güvenlik sorusu** | (istediğiniz gibi) |
| **Güvenlik yanıtı** | (istediğiniz gibi) |

*Not: Elbette, istediğiniz herhangi bir parola da kullanabilirsiniz. Varsayılan parola güvenlik ayarlarını 7 karakterden daha uzun ve bir tane alfasayısal olmayan karakter içeren bir parola gerektirir.*

Bu kullanıcı için Yönetici rolü seçin ve kullanıcı Oluştur düğmesine tıklayın.

![](mvc-music-store-part-7/_static/image7.png)

Bu noktada, kullanıcının başarıyla oluşturulduğunu belirten bir ileti görürsünüz.

![](mvc-music-store-part-7/_static/image8.png)

Artık tarayıcı penceresini kapatabilirsiniz.

## <a name="role-based-authorization"></a>Rol tabanlı yetkilendirme

Şimdi biz sınıftaki herhangi bir denetleyici eylemi erişmek için yönetici rolündeki kullanıcı olmalıdır belirtme [Authorize] özniteliği kullanılarak StoreManagerController erişimi kısıtlayabilirsiniz.

[!code-csharp[Main](mvc-music-store-part-7/samples/sample1.cs)]

*Not: Hem denetleyici sınıf düzeyinde hem de özel eylem yöntemleri [Authorize] özniteliği yerleştirilebilir.*

Artık /StoreManager için gözatma, bir oturum açma iletişim kutusunu açar:

![](mvc-music-store-part-7/_static/image9.png)

Sunduğumuz yeni bir yönetici hesabıyla oturum açtıktan sonra önce albümü düzenle ekranı Git sunabiliyoruz.

> [!div class="step-by-step"]
> [Önceki](mvc-music-store-part-6.md)
> [İleri](mvc-music-store-part-8.md)
