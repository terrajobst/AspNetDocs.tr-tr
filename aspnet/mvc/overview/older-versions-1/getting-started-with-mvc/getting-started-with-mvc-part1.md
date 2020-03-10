---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: ASP.NET MVC 'ye giriş | Microsoft Docs
author: shanselman
description: Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir. Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturun.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: f8f0014776ba1313119e8c39c63a216b0fc864e7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581587"
---
# <a name="intro-to-aspnet-mvc"></a>ASP.NET MVC’ye Giriş

[Scott Hanselman](https://github.com/shanselman) tarafından

> > [!NOTE]
> > Bu öğreticiyi [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)kullanarak [burada](../../getting-started/introduction/getting-started.md) kullanılabilirse, güncelleştirilmiş bir sürüm. Yeni öğretici, bu öğreticide birçok geliştirme sağlayan ASP.NET MVC 5 ' i kullanır.
>
>
> Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir. Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturacaksınız. Diğer ASP.NET MVC öğreticileri ve örneklerini bulmak için [ASP.NET MVC öğrenme merkezini](../../../index.md) ziyaret edin.

[Visual Web Developer 2010 Express 'i](https://www.microsoft.com/express/Web/)kullanarak Ilk ASP.NET MVC web uygulamamızı yapalim. Film oluşturup listemize olanak sağlayacak küçük bir film listesi uygulaması oluşturacağız.

## <a name="what-youll-build"></a>Ne oluşturacağız?

Oluşturacağınız uygulamanın iki ekran görüntüsü aşağıda verilmiştir. Çeşitli sütunlara sahip basit bir film tablosuna sahip olursunuz.

[![film listesi-Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)

Böylece, listeye film ekleyebilmemiz için bir oluştur formu görürsünüz.

[Film oluşturmak ![-Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)

## <a name="skills-youll-learn"></a>Öğrenmeniz gereken yetenekler

Bu öğreticide, Visual Studio kullanarak bir ASP.NET MVC web uygulaması oluşturma hakkında temel bilgiler verilir. Şunları öğreneceksiniz:

- Yeni bir ASP.NET MVC projesi oluşturma
- SQL Server ile yeni bir veritabanı oluşturma
- ASP.NET MVC denetleyicileri ve görünümleri oluşturma
- Verileri alma ve görüntüleme
- Verileri düzenleme ve veri doğrulamayı etkinleştirme
- Veritabanı şemasını güncelleştirme

## <a name="get-started"></a>Başlarken

Visual Web Developer 2010 Express 'ı çalıştırarak başlayın (bunu şimdi "VWD" olarak arayarak) ve başlangıç ekranından yeni proje ' yi seçin.

Visual Web Developer, IDE veya tümleşik bir geliştirici ortamıdır. Belgeleri yazmak için Microsoft Word kullandığınızda olduğu gibi, uygulamalar oluşturmak için IDE kullanacaksınız. En üstteki, sizin için kullanabileceğiniz çeşitli seçenekleri ve ayrıca dosya seçmek için kullanabileceğiniz menüyü gösteren bir araç çubuğu bulunur | Yeni proje.

[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)

## <a name="creating-your-first-application"></a>Ilk uygulamanızı oluşturma

Visual Basic veya görsel C#kullanarak uygulamalar oluşturabilirsiniz. Şimdilik, sol taraftaki görsel C# ' i seçip "ASP.NET MVC 2 Web uygulaması" nı seçin. Projenizi "Filmler" olarak adlandırın ve Tamam ' a tıklayın.

[Yeni ![proje](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)

Sağ tarafta, uygulamanızdaki tüm dosya ve klasörler gösteriliyor Çözüm Gezgini. Ortadaki büyük pencere, kodunuzu düzenlediğiniz ve zamanınızın çoğunu geçirdiğiniz yerdir. Visual Studio, az önce oluşturduğunuz ASP.NET MVC projesi için varsayılan bir şablon kullandı, bu nedenle artık herhangi bir şey yapmadan çalışan bir uygulamaya sahipsiniz! Bu basit bir "Merhaba Dünya! Proje ve uygulamamız için başlamak iyi bir yerdir.

[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)

Araç çubuğunda "Oynat" düğmesini seçin.

![Hata Ayıklamayı Başlat](getting-started-with-mvc-part1/_static/image11.png)

Bu, programınızı derlemek ve uygulamanızı bir Web tarayıcısında başlatmak için sağ tarafta işaret eden yeşil bir oktur.

*NOTE: klavyenizde F5 tuşuna basabilir veya "hata ayıkla" menüsünden hata ayıklamayı Başlat&gt;başlatabilirsiniz.*

Bu, Visual Web Developer 'ın bir geliştirme Web sunucusu başlatmasını ve Web uygulamamızı çalıştırmasına neden olur (Bunu etkinleştirmek için yapılandırma veya el ile adım gerekmez). Daha sonra bir tarayıcı başlatır ve uygulamanın giriş sayfasına gözatmasını sağlayacak şekilde yapılandırır. Tarayıcının adres çubuğunun, example.com gibi değil, "localhost" olduğunu belirten bir bildirim aşağıda verilmiştir. Bunun nedeni, localhost 'un her zaman kendi yerel bilgisayarınızı gösterdiği ve bu durumda yeni oluşturduğumuz uygulamayı çalıştırdığı anlamına gelir.

[![giriş sayfası](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)

Bu varsayılan şablon, size iki sayfa ve temel bir oturum açma sayfası sunar. Bu uygulamanın nasıl çalıştığını değiştirelim ve işlemde ASP.NET MVC hakkında biraz bilgi edinebilirsiniz. Tarayıcınızı kapatın ve kodun değiştirilmesini sağlar.

> [!div class="step-by-step"]
> [Next](getting-started-with-mvc-part2.md)
