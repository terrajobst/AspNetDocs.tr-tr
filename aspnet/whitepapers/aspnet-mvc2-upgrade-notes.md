---
uid: whitepapers/aspnet-mvc2-upgrade-notes
title: ASP.NET MVC 1,0 uygulamasını ASP.NET MVC 2 ' ye yükseltme | Microsoft Docs
author: rick-anderson
description: Bu belgede hem el ile yükseltme hem de bir sihirbaz ile ASP.NET MVC 1,0 uygulaması ile ASP.NET MVC 2 açıklanır. Bu belge d... için de kullanılabilir.
ms.author: riande
ms.date: 04/08/2010
ms.assetid: f1a01759-d251-4b09-8835-e112e336c6dd
msc.legacyurl: /whitepapers/aspnet-mvc2-upgrade-notes
msc.type: content
ms.openlocfilehash: 27589f1b1c9d5038118e5ff0cc2e7cecae17d5ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637020"
---
# <a name="upgrading-an-aspnet-mvc-10-application-to-aspnet-mvc-2"></a>Bir ASP.NET MVC 1.0 Uygulamasını ASP.NET MVC 2 Sürümüne Yükseltme

> Bu belgede hem el ile yükseltme hem de bir sihirbaz ile ASP.NET MVC 1,0 uygulaması ile ASP.NET MVC 2 açıklanır. Bu belge [Indirileceği](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/MVC2-Upgrade-Notes.pdf) için de kullanılabilir

## <a name="introduction"></a>Giriş

ASP.NET MVC 2 aynı sunucuda ASP.NET MVC 1,0 ile yan yana yüklenebilir. Bu, ASP.NET MVC 1,0 uygulamasının ASP.NET MVC 2 ' ye ne zaman yükseltileceğini seçerken uygulama geliştiricileri esnekliği sağlar.

Visual Studio 2010, Visual Studio 2008 ile oluşturulan mevcut ASP.NET MVC 1,0 projelerini ASP.NET MVC 2 ' ye yükselten bir sihirbaz içerir. Yükseltme Sihirbazı, Visual Studio 2010 ' de bir ASP.NET MVC 1,0 projesi açılarak başlatılır.

## <a name="upgrade-wizard-for-aspnet-mvc-10-on-visual-studio-2008-sp1"></a>Visual Studio 2008 SP1 üzerinde ASP.NET MVC 1,0 için Yükseltme Sihirbazı

ASP.NET MVC 1,0 uygulamasını Visual Studio 2008 SP1 'de ASP.NET MVC 2 ' ye yükseltmek için (desteklenmeyen) MvcAppConverter uygulamasını kullanın. Bu uygulamayı Şu URL 'den indirebilirsiniz:

[https://go.microsoft.com/fwlink/?LinkID=185351](https://go.microsoft.com/fwlink/?LinkID=185351)

## <a name="manually-upgrading-an-aspnet-mvc-10-project"></a>ASP.NET MVC 1,0 projesini el ile yükseltme

Mevcut bir ASP.NET MVC 1,0 uygulamasını sürüm 2 ' ye el ile yükseltmek için aşağıdaki adımları izleyin:

1. Mevcut projenin yedeğini alın.
2. Bir metin düzenleyicisinde, proje dosyasını (. csproj veya. vbproj dosyası uzantılı dosya) açın ve ProjectTypeGuid öğesini bulun. Bu öğenin değeri olarak, {603c0e0b-db56-11dc-be95-000d561079b0} DEĞERINI {F85E285D-A4E0-4152-9332-AB1D724D3325} ile değiştirin. İşiniz bittiğinde, bu öğenin değeri şu şekilde olmalıdır: 

    `{F85E285D-A4E0-4152-9332-AB1D724D3325};{349c5851-65df-11da-9384-00065b846f21};{fae04ec0-301f-11d3-bf4b-00c04f79efbc}`
3. Web uygulaması kök klasöründe, Web. config dosyasını düzenleyin. System. Web. Mvc, Version = 1.0.0.0 araması yapın ve tüm örnekleri System. Web. Mvc, Version = 2.0.0.0 ile değiştirin.
4. Görünümler klasöründe bulunan Web. config dosyası için önceki adımı yineleyin.
5. Visual Studio 'Yu kullanarak projeyi açın ve **Çözüm Gezgini**' de **Başvurular** düğümünü genişletin. System. Web. Mvc başvurusunu silin (sürüm 1,0 derlemesini işaret eder). System. Web. Mvc (v 2.0.0.0) öğesine bir başvuru ekleyin.
6. Aşağıdaki bindingRedirect öğesini yapılandırma bölümünün altındaki uygulama kökündeki Web. config dosyasına ekleyin:   

    [!code-xml[Main](aspnet-mvc2-upgrade-notes/samples/sample1.xml)]
7. Yeni boş bir ASP.NET MVC 2 uygulaması oluşturun. Dosyaları yeni uygulamanın betikler klasöründen mevcut uygulamanın betikler klasörüne kopyalayın.
8. Mevcut applicationâ €™ s CSS dosyasını, site. CSS dosyasındaki CSS stili tanımlarıyla güncelleştirin.
9. Uygulamayı derleyin ve çalıştırın. Herhangi bir hata oluşursa, [ASP.NET MVC 2 ' deki](https://go.microsoft.com/fwlink/?LinkID=185038) yenilikler sayfasındaki son değişiklikler bölümüne bakın.
