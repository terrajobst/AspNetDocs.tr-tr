---
uid: web-pages/overview/ui-layouts-and-themes/installing-helpers
title: Bir ASP.NET Web Pages (Razor) sitesinde yardımcı yükleme | Microsoft Docs
author: Rick-Anderson
description: Bu makalede, bir ASP.NET Web Pages (Razor) Web sitesinde yardımcı 'nın nasıl yükleneceği açıklanır. Yardımcı, başına kod ve biçimlendirme içeren yeniden kullanılabilir bir bileşendir...
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 5e968ead-906a-45ea-ac2a-c70e57e1a9b1
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/installing-helpers
msc.type: authoredcontent
ms.openlocfilehash: 41e33c04a53a6ad257c3937cdadcec767e9217c8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638588"
---
# <a name="installing-a-helper-in-an-aspnet-web-pages-razor-site"></a>Bir ASP.NET Web Pages (Razor) sitesinde yardımcı yükleme

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede, bir ASP.NET Web Pages (Razor) Web sitesinde yardımcı 'nın nasıl yükleneceği açıklanır. *Yardımcı* , sıkıcı veya karmaşık olabilecek bir görevi gerçekleştirmek için kod ve biçimlendirme içeren yeniden kullanılabilir bir bileşendir.
> 
> Öğrenecekleriniz:
> 
> - WebMatrix 3 kullanılarak oluşturulan bir Web sitesine yardımcı nasıl yüklenir.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - WebMatrix 3

## <a name="overview-of-helpers"></a>Yardımcıların Özeti

Kullanıcıların genellikle Web sayfalarında yapmak istedikleri bazı görevler çok fazla kod gerektirir veya ek bilgi gerektirir. Veriler için bir grafik görüntülemeyi örnek olarak içerir. sayfaya Twitter "Izle" düğmesi koyma; Web siteinizden e-posta gönderme; görüntüleri kırpma veya yeniden boyutlandırma; siteniz için PayPal 'yi kullanma. Bu tür şeyleri daha kolay hale getirmek için ASP.NET Web sayfaları, *yardımcıları*kullanmanıza olanak sağlar. Yardımcılar, bir site için yüklediğiniz ve yalnızca bir satır veya iki Razor kodu kullanarak tipik görevleri gerçekleştirmenize olanak sağlayan bileşenlerdir.

ASP.NET Web sayfalarının içinde yerleşik olarak bulunan birkaç yardımcıları vardır. Ancak, NuGet Paket Yöneticisi kullanılarak sağlanan paketlerde (eklentiler) birçok yardımcı vardır. NuGet, yüklenecek bir paket seçmenizi sağlar ve yükleme ayrıntılarının tamamını ele alır.

## <a name="installing-a-helper-in-webmatrix-3"></a>WebMatrix 3 ' te yardımcı yükleme

1. WebMatrix 3 ' te **NuGet** düğmesine tıklayın.

    ![WebMatrix 'te NuGet Galerisi iletişim kutusu](installing-helpers/_static/image1.png)
2. Bu, NuGet paket yöneticisini başlatır ve kullanılabilir paketleri görüntüler. Arama kutusuna, yüklemek istediğiniz yardımcı için bir anahtar sözcük girin.

    ![WebMatrix 'te NuGet Galerisi iletişim kutusu](installing-helpers/_static/image2.png)
3. Paketi seçin ve ardından **yükler**' e tıklayın. Paketi yüklemek isteyip istemediğiniz sorulduğunda **Evet** ' e tıklayın ve koşulları kabul etmiş olursunuz.

     İlk kez bir yardımcı yüklüyorsanız NuGet, yardımcı 'yı oluşturan kod için Web sitenizde klasörler oluşturur.
4. Bir yardımcıyı kaldırmak için, **Galeri** düğmesine tıklayın, **yüklü** sekmesine tıklayın ve kaldırmak istediğiniz paketi seçin.

## <a name="installing-the-twitter-helper"></a>Twitter yardımcısını yükleme

Twitter API 'sinin en son sürümü, NuGet aracılığıyla yüklediğiniz Twitter Yardımcısı ile uyumlu değildir. Bunun yerine, projenizde Twitter yardımcısını ayarlama hakkında bilgi edinmek için [WebMatrix Ile Twitter Yardımcısı](twitter-helper.md) konusuna bakın.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

[ASP.NET Web sayfalarına giriş 2-Programlama Temelleri](../getting-started/introducing-razor-syntax-c.md)

[WebMatrix ile Twitter Yardımcısı](twitter-helper.md)
