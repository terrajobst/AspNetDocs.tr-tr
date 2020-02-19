---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
title: ASP.NET MVC 3 ' e girişC#() | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici, Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 86a80b35-88bd-4b7c-bd58-f6e7997197d4
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: e71275c93558c0b6ca087a145786e8c846b69721
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457550"
---
# <a name="intro-to-aspnet-mvc-3-c"></a>ASP.NET MVC 3 Sürümüne Giriş (C#)

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> > [!NOTE]
> > [Burada](../../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur. Daha güvenlidir, daha kolay hale gelir ve daha fazla özellik gösterir.
> 
> 
> Bu öğretici, Microsoft Visual Studio ücretsiz bir sürümü olan Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir. Başlamadan önce, aşağıda listelenen önkoşulları yüklediğinizden emin olun. Şu bağlantıya tıklayarak hepsini yükleyebilirsiniz: [Web Platformu Yükleyicisi](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Alternatif olarak, aşağıdaki bağlantıları kullanarak önkoşulları ayrı ayrı yükleyebilirsiniz:
> 
> - [Visual Studio Web Developer Express SP1 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 Araçlar güncelleştirmesi](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(çalışma zamanı + araçlar desteği)
> 
> Visual Web Developer 2010 yerine Visual Studio 2010 kullanıyorsanız, aşağıdaki bağlantıya tıklayarak önkoşulları yükleyebilirsiniz: [Visual studio 2010 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Kaynak koduna sahip bir Visual Web C# Developer projesi, bu konuyla birlikte kullanılabilecek. [Sürümü C# indirin](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Visual Basic tercih ediyorsanız, Bu öğreticinin [Visual Basic sürümüne](../vb/intro-to-aspnet-mvc-3.md) geçin.

## <a name="what-youll-build"></a>Ne oluşturacağız?

Bir veritabanından film oluşturmayı, düzenlemenizi ve listelemeyi destekleyen basit bir film listeleme uygulaması uygulayacaksınız. Aşağıda, oluşturacağınız uygulamanın iki ekran görüntüsü verilmiştir. Bu, bir veritabanının bir filmin listesini görüntüleyen bir sayfa içerir:

![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image1.png)

Uygulama ayrıca film eklemenize, düzenlemenize ve silmenize olanak sağlar ve bireysel kişilerle ilgili ayrıntıları görebilir. Tüm veri girişi senaryoları, veritabanında depolanan verilerin doğru olduğundan emin olmak için doğrulama içerir.

![](intro-to-aspnet-mvc-3/_static/image2.png)

## <a name="skills-youll-learn"></a>Öğrenmeniz gereken yetenekler

Öğrenirsiniz:

- Yeni bir ASP.NET MVC projesi oluşturma.
- ASP.NET MVC denetleyicileri ve görünümleri oluşturma.
- Entity Framework Code First paradigması kullanarak yeni bir veritabanı oluşturma.
- Verileri alma ve görüntüleme.
- Verileri düzenleme ve veri doğrulamayı etkinleştirme.

## <a name="getting-started"></a>Başlarken

Visual Web Developer 2010 Express (kısa için "Visual Web Developer") çalıştırarak başlayın ve **Başlangıç** sayfasından **Yeni proje** ' yi seçin.

Visual Web Developer, IDE veya tümleşik bir geliştirme ortamıdır. Belgeleri yazmak için Microsoft Word kullandığınızda olduğu gibi, uygulamalar oluşturmak için IDE kullanacaksınız. Visual Web Developer 'da, sizin için kullanabileceğiniz çeşitli seçenekleri gösteren bir araç çubuğu vardır. Ayrıca, IDE 'de görevler gerçekleştirmek için başka bir yol sağlayan bir menü de vardır. (Örneğin, **Başlangıç** sayfasından **Yeni proje** ' yi seçmek yerine, menüsünü kullanabilir ve **Dosya** **Yeni proje**&gt; ' ni seçebilirsiniz.)

[![](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)

## <a name="creating-your-first-application"></a>Ilk uygulamanızı oluşturma

Programlama dili olarak Visual Basic veya görseli C# kullanarak uygulamalar oluşturabilirsiniz. Sol taraftaki C# görsel ' i seçin ve ardından **ASP.NET MVC 3 Web uygulaması**' nı seçin. Projenizi "MvcMovie" olarak adlandırın ve ardından **Tamam**' a tıklayın. (Visual Basic tercih ediyorsanız, Bu öğreticinin [Visual Basic sürümüne](../vb/intro-to-aspnet-mvc-3.md) geçin.)

![](intro-to-aspnet-mvc-3/_static/image5.png)

**Yeni ASP.NET MVC 3 projesi** Iletişim kutusunda **Internet uygulaması**' nı seçin. **HTML5 Işaretlemesini kullan** ' a bakın ve varsayılan görünüm altyapısı olarak **Razor** ' i bırakın.

![](intro-to-aspnet-mvc-3/_static/image6.png)

**Tamam**'a tıklayın. Visual Web Developer, az önce oluşturduğunuz ASP.NET MVC projesi için varsayılan bir şablon kullandı, bu nedenle artık herhangi bir şey yapmadan çalışan bir uygulamanız var! Bu basit bir "Merhaba Dünya!" Project ve uygulamanızı başlatmak için iyi bir yerdir.

[![](intro-to-aspnet-mvc-3/_static/image8.png)](intro-to-aspnet-mvc-3/_static/image7.png)

**Hata Ayıkla** menüsünden **hata ayıklamayı Başlat**' ı seçin.

![](intro-to-aspnet-mvc-3/_static/image9.png)

Hata ayıklamayı başlatmak için klavye kısayolunun F5 olduğuna dikkat edin.

F5, Visual Web Developer 'ın bir geliştirme Web sunucusu başlatmasına ve Web uygulamanızı çalıştırmasına neden olur. Daha sonra Visual Web Developer bir tarayıcı başlatır ve uygulamanın giriş sayfasını açar. Tarayıcının adres çubuğunun `example.com`gibi `localhost` söydiğine dikkat edin. Bunun nedeni `localhost` her zaman kendi yerel bilgisayarınıza işaret ettiğinden, bu durumda yeni oluşturduğunuz uygulamayı çalıştırıyor olur. Visual Web Developer bir Web projesi çalıştırdığında, Web sunucusu için rastgele bir bağlantı noktası kullanılır. Aşağıdaki görüntüde rastgele bağlantı noktası numarası 43246 ' dir. Uygulamayı çalıştırdığınızda, muhtemelen farklı bir bağlantı noktası numarası görürsünüz.

![](intro-to-aspnet-mvc-3/_static/image10.png)

Bu varsayılan şablon, size iki sayfa ve temel bir oturum açma sayfası sunar. Sonraki adım, bu uygulamanın nasıl çalıştığını değiştirmek ve işlemde ASP.NET MVC hakkında biraz bilgi sağlamaktır. Tarayıcınızı kapatın ve bazı kodları değiştirelim.

> [!div class="step-by-step"]
> [Next](adding-a-controller.md)
