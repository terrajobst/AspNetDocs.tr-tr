---
uid: web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
title: Mobil cihazlar için ASP.NET Web Pages (Razor) sitelerini işleme | Microsoft Docs
author: Rick-Anderson
description: 'Bu makalede, mobil cihazlarda uygun şekilde işlenecek bir ASP.NET Web Pages (Razor) sitesinde sayfaların nasıl oluşturulacağı açıklanır. Ne öğreneceksiniz: nasıl yapılır...'
ms.author: riande
ms.date: 02/17/2014
ms.assetid: f15ab392-c05e-4269-83bf-7c6d2b8c8ec8
msc.legacyurl: /web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
msc.type: authoredcontent
ms.openlocfilehash: c012348d65e48a275cb0e4808fef2a7f31e5fb33
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563569"
---
# <a name="rendering-aspnet-web-pages-razor-sites-for-mobile-devices"></a>Mobil cihazlar için ASP.NET Web Pages (Razor) sitelerini işleme

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede, mobil cihazlarda uygun şekilde işlenecek bir ASP.NET Web Pages (Razor) sitesinde sayfaların nasıl oluşturulacağı açıklanır.
> 
> Öğrenecekleriniz:
> 
> - Bir sayfanın özellikle mobil cihazlarda tasarlanmasını belirtmek için adlandırma kuralı kullanma.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 3
>   
> 
> Bu öğretici, ASP.NET Web Pages 2 ile de kullanılabilir.

ASP.NET Web sayfaları, mobil veya diğer cihazlarda içerik işlemeye yönelik özel ekranlar oluşturmanızı sağlar.

Bir ASP.NET Web sayfaları sitesinde cihaza özgü sayfa oluşturmanın en kolay yolu, şöyle bir dosya adlandırma deseninin kullanılması: *filename. Mobile. cshtml*. Bir sayfanın iki sürümünü (örneğin, *Dosyam. cshtml* adlı bir tane ve *Dosyam. Mobile. cshtml*adlı bir tane) oluşturabilirsiniz. Çalışma zamanında, bir mobil cihaz *Dosyam. cshtml*istediğinde, ASP.net *Dosyam. Mobile. cshtml*içindeki içeriği işler. Aksi takdirde, *Dosyam. cshtml* işlenir.

Aşağıdaki örnekte, mobil cihazlar için bir içerik sayfası ekleyerek mobil işlemenin nasıl etkinleştirileceği gösterilmektedir. *Sayfa1. cshtml* içerik ve bir gezinti kenar çubuğu içerir. *Sayfa1. Mobile. cshtml* aynı içeriği içerir, ancak kenar çubuğunu atlar.

1. Bir ASP.NET Web Pages sitesinde, *Sayfa1. cshtml* adlı bir dosya oluşturun ve geçerli içeriği aşağıdaki biçimlendirme ile değiştirin.

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample1.html)]
2. *Sayfa1. Mobile. cshtml* adlı bir dosya oluşturun ve var olan içeriği aşağıdaki biçimlendirme ile değiştirin. Sayfanın mobil sürümünün, daha küçük bir ekran üzerinde daha iyi işleme için gezinti bölümünü atladığına dikkat edin.

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample2.html)]
3. Bir masaüstü tarayıcısı çalıştırın ve *Sayfa1. cshtml*'ye gidin. mobilesites ![-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)
4. Bir mobil tarayıcı (veya bir mobil cihaz öykünücüsü) çalıştırın ve *Sayfa1. cshtml*'ye gidin. ( *. Mobile eklemeyin.* URL 'nin bir parçası olarak.) İstek *Sayfa1. cshtml*'ye olsa da ASP.net, *Sayfa1. Mobile. cshtml*işler.

    ![mobilesites-2](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image2.png)

> [!NOTE]
> Mobil sayfaları test etmek için masaüstü bilgisayarda çalışan bir mobil cihaz simülatörü kullanabilirsiniz. Bu araç, Web sayfalarını mobil cihazlara (genellikle çok daha küçük bir görüntüleme alanı ile) baktıkları gibi test etmenizi sağlar. Bir Benzetici örneği, Mozilla Firefox için [Kullanıcı Aracısı değiştirici eklentisinin](http://addons.mozilla.org/firefox/addon/user-agent-switcher/) , çeşitli mobil tarayıcıları Firefox Masaüstü sürümünden öykünmenizi sağlayan bir örnektir.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

[Windows Phone öykünücü](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)
