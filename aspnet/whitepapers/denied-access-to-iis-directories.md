---
uid: whitepapers/denied-access-to-iis-directories
title: ASP.NET IIS dizinlerine erişimi reddedildi | Microsoft Docs
author: rick-anderson
description: Bu teknik incelemede, ASP.NET uygulamanıza yönelik bir istek, "DirectoryName dizinine erişim engellendi" hatasını döndürürse ne yapmanız gerektiğini açıklar. Başarısız oldu...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 3cb27b8a-354f-4332-bfe0-232b13bbf8aa
msc.legacyurl: /whitepapers/denied-access-to-iis-directories
msc.type: content
ms.openlocfilehash: a3a53aa88abbe1bcaaea7d691406800c8f9b988b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638504"
---
# <a name="aspnet-denied-access-to-iis-directories"></a>ASP.NET IIS Dizinlerine Erişim Reddedildi

> Bu teknik incelemede, ASP.NET uygulamanıza yönelik bir istek, " *DirectoryName* dizinine erişim engellendi" hatasını döndürürse ne yapmanız gerektiğini açıklar. Dizin değişikliklerini izleme işlemi başlatılamadı. "
> 
> ASP.NET 1,0 ve ASP.NET 1,1 için geçerlidir.

ASP.NET v1 RTM artık yerel bir makinede "ASPNET" hesabı olarak kaydedilmiş daha az ayrıcalıklı bir Windows hesabı kullanarak çalışır.

Bazı kilitli sistemlerde, bu hesap varsayılan olarak bir Web sitesinin içerik dizinlerine, uygulama kök dizinine veya Web sitesi kök dizinine okuma güvenlik erişimine sahip olabilir. Bu durumda, belirli bir Web uygulamasından sayfa istenirken aşağıdaki hatayı alırsınız:

![](denied-access-to-iis-directories/_static/image1.jpg)

Bu hatayı düzeltemedi, uygun dizinlerde güvenlik izinlerini değiştirmeniz gerekir.

Özellikle, ASP.NET Web sitesi köküne yönelik ASPNET hesabı için okuma, yürütme ve listeleme erişimi gerektirir (örneğin, c:\ınetpub\wwwroot veya IIS 'de yapılandırdığınız alternatif site dizini), içerik dizini ve uygulama kök dizini yapılandırma dosyası değişikliklerini izlemek için. Uygulama kökü, IIS Yönetim Aracı 'nda (inetmgr) uygulama sanal diziniyle ilişkili klasör yoluna karşılık gelir.

Örneğin, Wwwroot klasörü altında aşağıdaki uygulama hiyerarşisini göz önünde bulundurun.

`C:\inetpub\wwwroot\myapp\default.aspx`

Bu örnekte, ASPNET hesabının hem MyApp hem de Wwwroot dizinindeki içerik için yukarıda tanımlanan okuma izinlerine ihtiyacı vardır. Kök klasördeki tek bir devralınan ACL, iç içe yerleştirilmiş olmaları durumunda her iki dizin için de isteğe bağlı olarak kullanılabilir.

Bir dizine izinler eklemek için aşağıdaki adımları uygulayın:

- Windows Gezgini 'ni kullanarak dizine gidin
- Dizin klasörüne sağ tıklayın ve "Özellikler" i seçin
- Özellik iletişim kutusunda "güvenlik" sekmesine gidin
- "Ekle" düğmesine tıklayın ve ardından ASPNET hesap adının ardından makine adını girin. Örneğin, "WebDev" adlı bir makinede, Web Dev\aspnet yazın ve "Tamam" a tıklayın.
- ASPNET hesabının "okuma &amp; yürütme", "klasör Içeriğini listeleme" ve "okuma" onay kutularının işaretli olduğundan emin olun.
- İletişim kutusunu kapatmak ve değişiklikleri kaydetmek için Tamam 'a basın.

![](denied-access-to-iis-directories/_static/image2.jpg)

İsterseniz, bu değişiklikler, Windows ile birlikte gelen betikler veya "cacls. exe" Aracı kullanılarak otomatikleştirilebilir. ASPNET hesabı hakkında daha fazla bilgi için lütfen [SSS belgesine](https://go.microsoft.com/fwlink/?LinkId=5828)bakın.

Belirli bir Web uygulamasının belirli bir klasör veya dosyaya yazma veya değiştirme izinleri varsa, bu, aynı yordam ve "yazma" ve/veya "Değiştir" onay kutularını işaretleyerek verilebilir.

Herkese veya kullanıcılar grubuna bu dizinlere okuma erişimi sağlayan makinelerde (varsayılan yapılandırma), hiçbir sorunla karşılaşılmaz ve yukarıdaki adımlar gerekli olmayacaktır.
