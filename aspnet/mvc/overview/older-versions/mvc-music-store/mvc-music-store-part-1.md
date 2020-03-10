---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
title: '1\. Bölüm: genel bakış ve Dosya-> Yeni proje | Microsoft Docs'
author: jongalloway
description: Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 1\. bölüm, genel bakış ve Dosya > Yeni proje içerir.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: bd356ca3-5bdb-4067-9dac-c9e9923a86e8
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
msc.type: authoredcontent
ms.openlocfilehash: 48428ff4ab5888253ed93ac41e79006eec823ad2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559985"
---
# <a name="part-1-overview-and-file-new-project"></a>1\. Bölüm: Genel Bakış ve Dosya->Yeni Proje

[Jon Galloway](https://github.com/jongalloway) tarafından

> MVC müzik deposu, Web geliştirme için ASP.NET MVC ve Visual Studio 'nun nasıl kullanılacağını anlatan bir öğretici uygulamadır.  
>   
> MVC müzik deposu, çevrimiçi olarak müzik albümlerini satan ve temel site yönetimi, Kullanıcı oturum açma ve alışveriş sepeti işlevlerini uygulayan basit bir örnek depolama uygulamasıdır.  
>   
> Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 1\. bölüm, genel bakış ve dosya&gt;yeni proje içerir.

## <a name="overview"></a>Genel bakış

MVC müzik deposu, Web geliştirme için ASP.NET MVC ve Visual Web Developer 'ın nasıl kullanılacağı hakkında ayrıntılı bilgiler sunan bir öğretici uygulamadır. Yavaş başlayacağız, bu nedenle başlangıç düzeyi Web geliştirme deneyimi sorunsuz.

Oluşturmakta olduğumuz uygulama basit bir müzik deposudur. Uygulamanın üç ana bölümü vardır: alışveriş, kullanıma alma ve yönetim.

![](mvc-music-store-part-1/_static/image1.jpg)

Ziyaretçiler, tarza göre albümlere gözatabilir:

![](mvc-music-store-part-1/_static/image2.jpg)

Tek bir albümü görüntüleyebilir ve bu kişinin sepetine eklemesini sağlayabilirsiniz:

![](mvc-music-store-part-1/_static/image3.jpg)

Sepetlerinde, artık istedikleri öğeleri kaldırarak kendi sepetini gözden geçirebilir:

![](mvc-music-store-part-1/_static/image4.jpg)

Kullanıma almaya devam etmek, bir kullanıcı hesabı için oturum açmasını veya kaydolmasını ister.

![](mvc-music-store-part-1/_static/image1.png)

![](mvc-music-store-part-1/_static/image2.png)

Hesap oluşturduktan sonra, Sevkiyat ve ödeme bilgilerini doldurarak siparişi tamamlayabilirler. Şeyleri basit tutmak için harika bir yükseltme çalıştırıyoruz: promosyon kodu "ÜCRETSIZ" olarak girerseniz her şey ücretsizdir!

![](mvc-music-store-part-1/_static/image5.jpg)

Sipariş ettikten sonra basit bir onay ekranı görürler:

![](mvc-music-store-part-1/_static/image6.jpg)

Müşterilere yönelik sayfalara ek olarak, yöneticilerin albüm, düzenleme ve silme yapabileceği Albümler listesini gösteren bir yönetici bölümü de oluşturacağız:

![](mvc-music-store-part-1/_static/image7.jpg)

## <a name="1-file--gt-new-project"></a>1. dosya-&gt; yeni proje

### <a name="installing-the-software"></a>Yazılımı yükleme

Bu öğretici, ücretsiz Visual Web Developer 2010 Express (ücretsiz) kullanarak yeni bir ASP.NET MVC 3 projesi oluşturarak başlayacak ve ardından tamamen çalışan bir uygulama oluşturmak için artımlı olarak Özellikler ekleyeceğiz. Bu şekilde, veritabanı erişimi, form gönderme senaryoları, veri doğrulama, tutarlı sayfa düzeni için ana sayfaları kullanma, sayfa güncelleştirmeleri ve doğrulama, Kullanıcı oturumu açma ve daha fazlası için AJAX kullanma gibi bilgileri ele alacağız.

Adımları adım adım takip edebilir veya tamamlanan uygulamayı [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store)' dan indirebilirsiniz.

Uygulamayı derlemek için Visual Studio 2010 SP1 veya Visual Web Developer 2010 Express SP1 (Visual Studio 2010 ' in ücretsiz sürümü) kullanabilirsiniz. Veritabanını barındırmak için SQL Server Compact (de ücretsiz) kullanacağız. Başlamadan önce, aşağıda listelenen önkoşulları yüklediğinizden emin olun.

- [Visual Studio Web Developer Express SP1 önkoşulları]
- [ASP.NET MVC 3 araç güncelleştirmesi]
- [SQL Server Compact 4,0]-çalışma zamanı ve araçlar desteği dahil

### <a name="creating-a-new-aspnet-mvc-3-project"></a>Yeni bir ASP.NET MVC 3 projesi oluşturma

Visual Web Developer 'daki Dosya menüsünden "yeni proje" seçeneğini belirleyerek başlayacağız. Bu, yeni proje iletişim kutusunu getirir.

![](mvc-music-store-part-1/_static/image5.png)

Sol taraftaki görsel C#&gt; Web şablonları grubunu seçeceğiz ve ardından Orta sütundaki "ASP.NET MVC 3 Web uygulaması" şablonunu seçersiniz. Projenizi MvcMusicStore olarak adlandırın ve Tamam düğmesine basın.

![](mvc-music-store-part-1/_static/image8.jpg)

Bu, projemiz için bazı MVC 'ye özel ayarlar yapmamızı sağlayan bir ikincil iletişim kutusu görüntüler. Aşağıdakileri seçin:

Proje şablonu-boş seçin

Görünüm altyapısı-Razor seçme

HTML5 anlam işaretlemesi-işaretli kullan

Ayarlarınızın aşağıda gösterildiği gibi olduğunu doğrulayıp Tamam düğmesine basın.

![](mvc-music-store-part-1/_static/image9.jpg)

Bu, projemizi oluşturacaktır. Aşağıda, uygulamamıza eklenen klasörlere, sağ taraftaki Çözüm Gezgini göz atalım.

![](mvc-music-store-part-1/_static/image10.jpg)

Boş MVC 3 şablonu tamamen boş değil; temel bir klasör yapısı ekler:

![](mvc-music-store-part-1/_static/image6.png)

ASP.NET MVC, klasör adları için bazı temel adlandırma kurallarını kullanır:

| **Klasör** | **Amaç** |
| --- | --- |
| **/Controllers** | Denetleyiciler tarayıcıdan girişe yanıt verir, onunla ne yapacağınıza karar verir ve kullanıcıya yanıt döndürür. |
| **/Views** | UI şablonlarımızı tutan görünümler |
| **/Modeller** | Modeller verileri tutar ve işleyebilir |
| **/Content** | Bu klasör görüntülerimizi, CSS 'yi ve diğer tüm statik içerikleri barındırır |
| **/Scripts** | Bu klasör JavaScript dosyalarımı barındırır |

ASP.NET MVC çerçevesi varsayılan olarak "yapılandırma üzerinden kural" yaklaşımı kullandığından ve klasör adlandırma kurallarına göre bazı varsayılan varsayımlar yaptığından, bu klasörler boş bir ASP.NET MVC uygulamasında bile bulunur. Örneğin, denetleyicilerde açıkça bunu belirtmek zorunda kalmadan, denetleyiciler görünümler klasöründeki görünümleri varsayılan olarak arar. Varsayılan kurallara uyma, yazmanız gereken kod miktarını azaltır ve diğer geliştiricilerin projenizi anlamasına daha da kolay hale gelir. Uygulamamızı oluşturduğumuzdan bu kuralları daha anlatacağız.

> [!div class="step-by-step"]
> [Next](mvc-music-store-part-2.md)
