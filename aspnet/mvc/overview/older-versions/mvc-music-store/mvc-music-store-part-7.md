---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
title: '7\. Bölüm: Üyelik ve yetkilendirme | Microsoft Docs'
author: jongalloway
description: Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. Bölüm 7 ' de üyelik ve yetkilendirme ele alınmaktadır.
ms.author: riande
ms.date: 10/13/2010
ms.assetid: c8511ebe-68bc-4240-87c3-d5ced84a3f37
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
msc.type: authoredcontent
ms.openlocfilehash: a6a1a936e0ea29ea36721ba78f35845401f74c01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539202"
---
# <a name="part-7-membership-and-authorization"></a>7\. Bölüm: Üyelik ve Yetkilendirme

[Jon Galloway](https://github.com/jongalloway) tarafından

> MVC müzik deposu, Web geliştirme için ASP.NET MVC ve Visual Studio 'nun nasıl kullanılacağını anlatan bir öğretici uygulamadır.  
>   
> MVC müzik deposu, çevrimiçi olarak müzik albümlerini satan ve temel site yönetimi, Kullanıcı oturum açma ve alışveriş sepeti işlevlerini uygulayan basit bir örnek depolama uygulamasıdır.  
>   
> Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. Bölüm 7 ' de üyelik ve yetkilendirme ele alınmaktadır.

Depolama Yöneticisi denetleyicimiz Şu anda sitemizi ziyaret eden herkes tarafından erişilebilir durumda. Site yöneticileri iznini kısıtlamak için bunu değiştirelim.

## <a name="adding-the-accountcontroller-and-views"></a>AccountController ve görünümleri ekleme

Tam ASP.NET MVC 3 Web uygulaması şablonu ve ASP.NET MVC 3 boş Web uygulaması şablonu arasındaki bir fark, boş şablonun bir hesap denetleyicisi içermediğinden emin değildir. Tam ASP.NET MVC 3 Web uygulaması şablonundan oluşturulan yeni bir ASP.NET MVC uygulamasından birkaç dosya kopyalayarak bir hesap denetleyicisi ekleyeceğiz.

Full ASP.NET MVC 3 Web uygulaması şablonunu kullanarak yeni bir ASP.NET MVC uygulaması oluşturun ve aşağıdaki dosyaları projemizdeki dizinlere kopyalayın:

1. AccountController.cs 'i denetleyiciler dizininde Kopyala
2. Accountmodellerini modeller dizininde kopyalama
3. Görünümler dizini içinde bir hesap dizini oluşturun ve tüm dört görünümü ' de kopyalayın

Denetleyici ve model sınıflarının ad alanını MvcMusicStore ile başlayacak şekilde değiştirin. AccountController sınıfı, MvcMusicStore. Controllers ad alanını kullanmalı ve Accountmodeller sınıfı MvcMusicStore. model ad alanını kullanmalıdır.

*Note: Bu dosyalar, öğreticinin başlangıcında site tasarım dosyalarımı kopyaladığımız MvcMusicStore-Assets. zip indirimde da mevcuttur. Üyelik dosyaları kod dizininde bulunur.*

Güncelleştirilmiş çözüm aşağıdaki gibi görünmelidir:

![](mvc-music-store-part-7/_static/image1.png)

## <a name="adding-an-administrative-user-with-the-aspnet-configuration-site"></a>ASP.NET yapılandırma sitesiyle Yönetici Kullanıcı ekleme

Web sitemizden yetkilendirme gerektirmeden önce, erişimi olan bir kullanıcı oluşturmanız gerekir. Bir kullanıcı oluşturmanın en kolay yolu yerleşik ASP.NET yapılandırması Web sitesini kullanmaktır.

Çözüm Gezgini simgesini izleyerek ASP.NET Configuration Web sitesini başlatın.

![](mvc-music-store-part-7/_static/image2.png)

Bu, bir yapılandırma Web sitesi başlatır. Giriş ekranındaki Güvenlik sekmesine tıklayın ve ardından ekranın ortasında "rolleri etkinleştir" bağlantısına tıklayın.

![](mvc-music-store-part-7/_static/image3.png)

"Rol oluşturma veya yönetme" bağlantısına tıklayın.

![](mvc-music-store-part-7/_static/image4.png)

Rol adı olarak "Yönetici" yazın ve rol Ekle düğmesine basın.

![](mvc-music-store-part-7/_static/image5.png)

Geri düğmesine tıklayın ve ardından sol taraftaki kullanıcı oluştur bağlantısına tıklayın.

![](mvc-music-store-part-7/_static/image6.png)

Aşağıdaki bilgileri kullanarak sol taraftaki Kullanıcı bilgileri alanlarını girin:

| **Alan** | **Değer** |
| --- | --- |
| **Kullanıcı adı** | Yönetici |
| **Parola** | password123! |
| **Parolayı Onayla** | password123! |
| **Postadaki** | (herhangi bir e-posta adresi çalışacaktır) |
| **Güvenlik sorusu** | (beğendiğiniz şey) |
| **Güvenlik yanıtı** | (beğendiğiniz şey) |

*Note: Elbette istediğiniz parolayı kullanabilirsiniz. Varsayılan parola güvenlik ayarları 7 karakter uzunluğunda ve alfasayısal olmayan bir karakter içeren bir parola gerektirir.*

Bu Kullanıcı için yönetici rolünü seçin ve Kullanıcı Oluştur düğmesine tıklayın.

![](mvc-music-store-part-7/_static/image7.png)

Bu noktada, kullanıcının başarıyla oluşturulduğunu belirten bir ileti görmeniz gerekir.

![](mvc-music-store-part-7/_static/image8.png)

Artık tarayıcı penceresini kapatabilirsiniz.

## <a name="role-based-authorization"></a>Rol tabanlı yetkilendirme

Artık, [Yetkilendir] özniteliğini kullanarak StoreManagerController erişimini kısıtlayabiliriz. Bu, kullanıcının sınıftaki herhangi bir denetleyiciye erişmek için yönetici rolünde olması gerektiğini belirten bir işlemdir.

[!code-csharp[Main](mvc-music-store-part-7/samples/sample1.cs)]

*Note: [Yetkilendir] özniteliği belirli eylem yöntemlerine ve denetleyici sınıf düzeyinde yer alabilir.*

Şimdi/StoreManager 'a göz atma bir oturum açma iletişim kutusunu açar:

![](mvc-music-store-part-7/_static/image9.png)

Yeni yönetici hesabımızda oturum açtıktan sonra, albüm düzenleme ekranına daha önce olduğu gibi gidebilirsiniz.

> [!div class="step-by-step"]
> [Önceki](mvc-music-store-part-6.md)
> [İleri](mvc-music-store-part-8.md)
