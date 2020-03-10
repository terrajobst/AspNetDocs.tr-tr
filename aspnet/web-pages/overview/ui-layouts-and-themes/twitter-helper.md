---
uid: web-pages/overview/ui-layouts-and-themes/twitter-helper
title: ASP.NET Web sayfalarıyla Twitter Yardımcısı | Microsoft Docs
author: Rick-Anderson
description: Bu konu ve uygulama, WebMatrix 3 projenize Twitter Yardımcısı eklemeyi gösterir. Twitter yardımcı kodunu içerir ve yardımcı 'nın nasıl çağrılacağını gösterir...
ms.author: riande
ms.date: 11/26/2018
ms.assetid: c1a1244e-b9c8-42e6-a00b-8456a4ec027c
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/twitter-helper
msc.type: authoredcontent
ms.openlocfilehash: 76e32b7c808467a9a87c70017dac02bdb895e1df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638560"
---
# <a name="twitter-helper-with-aspnet-web-pages"></a>ASP.NET Web Sayfaları ile Twitter Yardımcısı

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> [!IMPORTANT]
> Twitter yardımcıları artık kullanılmıyor. Twitter 'ın Web siteleri için en son katılım araçları için bkz. [Web siteleri Için Twitter genel bakış](https://developer.twitter.com/en/docs/twitter-for-websites/overview).

> Bu konu ve uygulama, WebMatrix 3 projenize Twitter Yardımcısı eklemeyi gösterir. Twitter yardımcı kodunu içerir ve yardımcı yöntemlerin nasıl çağrılacağını gösterir.
> 
> Twitter. cshtml dosyası için bu kod, Microsoft 'un **Tian Pan** tarafından geliştirilmiştir.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 3
>   
> 
> Bu öğretici, ASP.NET Web Pages 2 ile de kullanılabilir.

## <a name="introduction"></a>Giriş

Bu konuda, uygulamanıza Twitter Yardımcısı ekleme ve yardımcı yöntemleri çağırmak için Razor söz dizimi kullanma gösterilmektedir. Twitter Yardımcısı, uygulamanızdaki Twitter düğmelerini ve pencere öğelerini eklemenizi kolaylaştırır. Kullanıcının zaman çizelgesi veya bir diyez etiketi için arama sonuçları gibi bir Twitter pencere öğesini kullanmak için, önce [Twitter 'da pencere öğesini](https://twitter.com/settings/widgets)oluşturmanız gerekir. Pencere öğesini oluşturduktan sonra bir pencere öğesi kimliği alacaksınız. Pencere öğesini gösteren yardımcı yöntemler çağrılırken bu pencere öğesi kimliğini bir parametre olarak geçirirsiniz.

Bu konu, Twitter API 'sinin 1,1 sürümü için yazılmıştır. Twitter yardımcı kodunu projenize doğrudan ekleyerek Twitter API 'SI değişirse yardımcı kodunu güncelleştirebilirsiniz.

WebMatrix 'i yükleme hakkında daha fazla bilgi için bkz. [ASP.NET Web Pages 2-](../getting-started/introducing-aspnet-web-pages-2/getting-started.md)Başlarken.

## <a name="add-twitter-helper-to-your-project"></a>Projenize Twitter Yardımcısı ekleyin

Twitter yardımcısını eklemek için, önce projenize **App\_kodu** adlı bir klasör ekleyin. Daha sonra **Twitter. cshtml**adlı bir dosya oluşturun.

![App_Code klasörü](twitter-helper/_static/image1.png)

Twitter. cshtml içindeki varsayılan kodu aşağıdaki kodla değiştirin.

[!code-cshtml[Main](twitter-helper/samples/sample1.cshtml)]

## <a name="call-twitter-methods-from-your-web-pages"></a>Web sayfalarınıza Twitter yöntemlerini çağırma

Aşağıdaki örnek, projenizdeki bir sayfadan Twitter yardımcı yöntemlerinin nasıl kullanılacağını gösterir. Projenizde, parametre değerlerini gereksinimlerinize uygun değerlerle değiştirmek isteyeceksiniz. Yöntemlerin nasıl çalıştığını araştırmak için, belirtilen pencere öğesi kimliklerini kullanabilirsiniz, ancak projeniz için kendi pencere öğelerinizi oluşturmak isteyeceksiniz.

Aşağıda gösterilen parametrelerin hepsi gerekli değildir. Düğme veya pencere öğesinin nasıl görüntülendiğini özelleştirmek için isteğe bağlı parametreler kullanılır. Örneğin, Izle düğmesi yalnızca Kullanıcı adının izlemesini gerektirir, ancak örnek, izleme sayısının nasıl ekleneceğini ve düğmenin boyutunu ve dilini nasıl belirtdiğini gösterir.

[!code-html[Main](twitter-helper/samples/sample2.html)]

## <a name="see-the-results"></a>Sonuçları görme

Yukarıdaki kod, aşağıdaki düğmeleri ve pencere öğelerini üretir. Bu düğmeler ve pencere öğeleri, ekran görüntüleri değil tam işlevseldir. Dil parametresi **es**olarak ayarlandığı Için Izle düğmesi İspanyolca olarak görüntülenir.

### <a name="follow-button"></a>Takip et düğmesi

[@aspnetizleyin)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`

### <a name="tweet-button"></a>Tweet düğmesi

[Tweet](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`

### <a name="user-timeline-profile"></a>Kullanıcı zaman çizelgesi (profil)

[@aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

### <a name="favorites"></a>Sık Kullanılanlar

[Sık kullanılan @Microsoft](https://twitter.com/Microsoft/favorites)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

### <a name="list"></a>List

[@Microsoft/MS\_tüketicisi\_bantların arası şeritler](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

### <a name="search"></a>Ara

[&quot;#asp .net`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`&quot;hakkında](https://twitter.com/search?q=%23asp.net) daha fazla bilgi
