---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
title: ASP.NET MVC 4 ' e giriş | Microsoft Docs
author: Rick-Anderson
description: Bu öğreticiyi Visual Studio 2013 kullanarak burada kullanılabilirse, güncelleştirilmiş bir sürüm. Yeni öğretici, t üzerinde birçok geliştirme sağlayan ASP.NET MVC 5 ' i kullanır...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: ed66530a-04d5-49eb-b76a-85be1f57c437
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 51709a9c6ddb39b8fcd1cd94cd08d530a595825a
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455548"
---
# <a name="intro-to-aspnet-mvc-4"></a>ASP.NET MVC 4’e Giriş

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> Bu öğreticiyi [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)kullanarak [burada](../../getting-started/introduction/getting-started.md) kullanılabilirse, güncelleştirilmiş bir sürüm. Yeni öğretici, bu öğreticide birçok geliştirme sağlayan ASP.NET MVC 5 ' i kullanır.
>
> Bu öğretici, Microsoft [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) veya Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak BIR ASP.NET MVC 4 Web uygulaması oluşturmaya ilişkin temel bilgileri öğretir. Visual Studio 2012 önerilir, öğreticiyi tamamlayabilmeniz için herhangi bir şey yüklemeniz gerekmez. Visual Studio 2010 kullanıyorsanız aşağıdaki bileşenleri yüklemelisiniz. Aşağıdaki bağlantılara tıklayarak hepsini yükleyebilirsiniz:
>
> - [Visual Studio Web Developer Express SP1 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 4 için WPı yükleyicisi](https://go.microsoft.com/fwlink/?LinkId=243392)
> - [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)
> - [SSDT](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx)
>
> Visual Web Developer 2010 yerine Visual Studio 2010 kullanıyorsanız, [ASP.NET MVC 4 Için WPI yükleyicisini](https://go.microsoft.com/fwlink/?LinkId=243392) ve: [Visual Studio 2010 önkoşullarını](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack) yükleme
>
> Kaynak koduna sahip bir Visual Web C# Developer projesi, bu konuyla birlikte kullanılabilecek. [Sürümü C# indirin](https://code.msdn.microsoft.com/Intro-to-ASPNET-MVC-4-61d0219d/file/114480/1/MvcMovie.zip).
>
> Öğreticide, uygulamayı Visual Studio 'da çalıştırırsınız. Ayrıca, uygulamayı bir barındırma sağlayıcısına dağıtarak Internet üzerinden kullanılabilir hale getirebilirsiniz. Microsoft, [ücretsiz bir Windows Azure deneme hesabında](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)en fazla 10 Web sitesi için ücretsiz web barındırma hizmeti sunar. Bir Visual Studio Web projesinin bir Windows Azure Web sitesine nasıl dağıtılacağı hakkında bilgi için bkz. [Visual Studio ile ASP.NET Web sitesi ve SQL veritabanı oluşturma ve dağıtma](https://docs.microsoft.com/dotnet/azure/). Bu öğretici Ayrıca, SQL Server veritabanınızı Windows Azure SQL veritabanı 'na (eskiden SQL Azure) dağıtmak için Entity Framework Code First Migrations nasıl kullanacağınızı gösterir.
>
> Bu öğretici, Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ) tarafından yazılmıştır.

## <a name="what-youll-build"></a>Ne oluşturacağız?

> [!NOTE]
> Bu öğreticiyi [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)kullanarak [burada](../../getting-started/introduction/getting-started.md) kullanılabilirse, güncelleştirilmiş bir sürüm. Yeni öğretici, bu öğreticide birçok geliştirme sağlayan ASP.NET MVC 5 ' i kullanır.

Bir veritabanından film oluşturmayı, düzenlemenizi, aramayı ve listelemeyi destekleyen basit bir film listeleme uygulaması uygulayacaksınız. Aşağıda, oluşturacağınız uygulamanın iki ekran görüntüsü verilmiştir. Bu, bir veritabanının bir filmin listesini görüntüleyen bir sayfa içerir:

![](intro-to-aspnet-mvc-4/_static/image1.png)

Uygulama ayrıca film eklemenize, düzenlemenize ve silmenize olanak sağlar ve bireysel kişilerle ilgili ayrıntıları görebilir. Tüm veri girişi senaryoları, veritabanında depolanan verilerin doğru olduğundan emin olmak için doğrulama içerir.

![](intro-to-aspnet-mvc-4/_static/image2.png)

## <a name="getting-started"></a>Başlarken

Visual Studio Express 2012 veya Visual Web Developer 2010 Express çalıştırarak başlayın. Bu serideki ekran görüntülerini çoğu 2012 Visual Studio Express kullanır, ancak Visual Studio 2010/SP1, Visual Studio 2012, Visual Studio Express 2012 veya Visual Web Developer 2010 Express ile bu öğreticiyi tamamlayabilirsiniz. **Başlangıç** sayfasından **Yeni proje** ' yi seçin.

Visual Studio, IDE veya tümleşik bir geliştirme ortamıdır. Belgeleri yazmak için Microsoft Word kullandığınızda olduğu gibi, uygulamalar oluşturmak için IDE kullanacaksınız. Visual Studio 'da, sizin için kullanabileceğiniz çeşitli seçenekleri gösteren bir araç çubuğu vardır. Ayrıca, IDE 'de görevler gerçekleştirmek için başka bir yol sağlayan bir menü de vardır. (Örneğin, **Başlangıç** sayfasından **Yeni proje** ' yi seçmek yerine, menüsünü kullanabilir ve **Dosya** **Yeni proje**&gt; ' ni seçebilirsiniz.)

![](intro-to-aspnet-mvc-4/_static/image3.png)

## <a name="creating-your-first-application"></a>Ilk uygulamanızı oluşturma

Programlama dili olarak Visual Basic veya görseli C# kullanarak uygulamalar oluşturabilirsiniz. Sol taraftaki C# görsel ' i seçin ve ardından **ASP.NET MVC 4 Web uygulaması**' nı seçin. Projenizin &quot;MvcMovie&quot; olarak adlandırın ve ardından **Tamam**' a tıklayın.

![](intro-to-aspnet-mvc-4/_static/image4.png)

**Yeni ASP.NET MVC 4 projesi** Iletişim kutusunda **Internet uygulaması**' nı seçin. **Razor** 'yi varsayılan görünüm altyapısı olarak bırakın.

![](intro-to-aspnet-mvc-4/_static/image5.png)

**Tamam**'a tıklayın. Visual Studio, az önce oluşturduğunuz ASP.NET MVC projesi için varsayılan bir şablon kullandı, bu nedenle artık herhangi bir şey yapmadan çalışan bir uygulamaya sahipsiniz! Bu basit bir &quot;Merhaba Dünya!&quot; Project, uygulamanızı başlatmak için iyi bir yerdir.

![](intro-to-aspnet-mvc-4/_static/image6.png)

**Hata Ayıkla** menüsünden **hata ayıklamayı Başlat**' ı seçin.

![](intro-to-aspnet-mvc-4/_static/image7.png)

Hata ayıklamayı başlatmak için klavye kısayolunun F5 olduğuna dikkat edin.

F5, Visual Studio 'Nun IIS Express başlatmasına ve Web uygulamanızı çalıştırmasına neden olur. Daha sonra Visual Studio bir tarayıcı başlatır ve uygulamanın giriş sayfasını açar. Tarayıcının adres çubuğunun `example.com`gibi `localhost` söydiğine dikkat edin. Bunun nedeni `localhost` her zaman kendi yerel bilgisayarınıza işaret ettiğinden, bu durumda yeni oluşturduğunuz uygulamayı çalıştırıyor olur. Visual Studio bir Web projesi çalıştırdığında, Web sunucusu için rastgele bir bağlantı noktası kullanılır. Aşağıdaki görüntüde, bağlantı noktası numarası 41788 ' dir. Uygulamayı çalıştırdığınızda, muhtemelen farklı bir bağlantı noktası numarası görürsünüz.

![](intro-to-aspnet-mvc-4/_static/image8.png)

Bu varsayılan şablon, giriş, Iletişim ve sayfalarla Ilgili sayfalar sağlar. Ayrıca, kaydolmak ve oturum açmak ve Facebook ve Twitter bağlantıları için destek sağlar. Sonraki adım, bu uygulamanın nasıl çalıştığını değiştirmek ve ASP.NET MVC hakkında biraz bilgi sağlamaktır. Tarayıcınızı kapatın ve bazı kodları değiştirelim.

> [!div class="step-by-step"]
> [Next](adding-a-controller.md)
