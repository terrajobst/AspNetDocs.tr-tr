---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: Yeni bir ASP.NET MVC projesi oluştur | Microsoft Docs
author: microsoft
description: 1\. adım temel Nerdakşam yemeği uygulama yapısını yerinde nasıl koyabileceğiniz gösterilmektedir.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 189ddc187fc83db14106b2da199ba12a70a32b45
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580936"
---
# <a name="create-a-new-aspnet-mvc-project"></a>Yeni ASP.NET MVC Projesi Oluşturma

[Microsoft](https://github.com/microsoft) tarafından

[PDF 'YI indir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu, ASP.NET MVC 1 kullanarak küçük, ancak tam bir Web uygulamasının nasıl oluşturulacağını gösteren ücretsiz bir ["Nerdakşam yemeği" uygulama öğreticisinin](introducing-the-nerddinner-tutorial.md) 1. adımından oluşur.
> 
> 1\. adım temel Nerdakşam yemeği uygulama yapısını yerinde nasıl koyabileceğiniz gösterilmektedir.
> 
> ASP.NET MVC 3 kullanıyorsanız, [MVC 3 Ile çalışmaya başlama](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC müzik mağazası](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) öğreticilerini izlemeniz önerilir.

## <a name="nerddinner-step-1-file-gtnew-project"></a>Nerdakşam yemeği adım 1: dosya-&gt;yeni proje

Visual Studio 2008 veya ücretsiz Visual Web Developer 2008 Express içinde **dosya&gt;yeni proje** menü öğesini seçerek Nerdakşam yemeği uygulamamıza başlayacağız.

Bu, "yeni proje" iletişim kutusunu getirir. Yeni bir ASP.NET MVC uygulaması oluşturmak için, iletişim kutusunun sol tarafındaki "Web" düğümünü seçip sağdaki "ASP.NET MVC web uygulaması" proje şablonunu seçeceğiz:

![](create-a-new-aspnet-mvc-project/_static/image1.png)

*Önemli: ASP.NET MVC 'yi indirdiğinizden ve yüklediğinizden emin olun; Aksi takdirde yeni proje iletişim kutusunda gösterilmez. Henüz yüklemediyseniz [Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx) v2 'yi kullanabilirsiniz (ASP.NET MVC, "Web platformu-&gt;çerçeveleri ve çalışma zamanları" bölümünde bulunur).*

"Nerdakşam yemeği" oluşturacağımız yeni projeyi adlandırın ve ardından oluşturmak için "Tamam" düğmesine tıklayın.

"Tamam" seçeneğine tıkladığımızda, Visual Studio, isteğe bağlı olarak yeni uygulama için bir birim testi projesi oluşturmamızı isteyen ek bir iletişim kutusu getirir. Bu birim testi projesi, uygulamamızın işlevlerini ve davranışını doğrulayan otomatikleştirilmiş testler oluşturmamızı sağlar (Bu öğreticide daha sonra yapılacak nasıl yapılacağını ele alacağız).

![](create-a-new-aspnet-mvc-project/_static/image2.png)

Yukarıdaki iletişim kutusundaki "test çerçevesi" açılan menüsü, makinede yüklü olan tüm ASP.NET MVC birim test projesi şablonları ile doldurulur. Sürümler NUnit, MBUnit ve XUnit için indirilebilir. Yerleşik Visual Studio birim test çerçevesi de desteklenir.

*Note: Visual Studio birim testi çerçevesi yalnızca Visual Studio 2008 Professional ve daha yeni sürümlerde kullanılabilir. VS 2008 Standard Edition veya Visual Web Developer 2008 Express kullanıyorsanız, bu iletişim kutusunun gösterilmesi için NUnit, MBUnit veya XUnit uzantıları ASP.NET MVC için indirmeniz ve yüklemeniz gerekir. Yüklü herhangi bir test çerçevesi yoksa iletişim kutusu görüntülenmez.*

Oluşturduğumuz test projesi için varsayılan "Nerdakşam yemeği. Tests" adını kullanacağız ve "Visual Studio birim testi" çerçeve seçeneğini kullanırız. "Tamam" düğmesine tıkladığımızda, Visual Studio, web uygulamamız ve birim testlerimiz için bir tane olmak üzere iki proje ile bizim için bir çözüm oluşturacak:

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a>Nerdakşam yemeği dizin yapısını İnceleme

Visual Studio ile yeni bir ASP.NET MVC uygulaması oluşturduğunuzda, projeye otomatik olarak bir dizi dosya ve dizin ekler:

![](create-a-new-aspnet-mvc-project/_static/image4.png)

ASP.NET MVC projeleri varsayılan olarak altı üst düzey dizine sahiptir:

| **Dizinden** | **Amaç** |
| --- | --- |
| **/Controllers** | URL isteklerini işleyen denetleyici sınıflarını yerleştirdiğiniz yer |
| **/Modeller** | Verileri temsil eden ve işleyen sınıfları yerleştirdiğiniz yer |
| **/Views** | Çıktı işlemeden sorumlu Kullanıcı Arabirimi şablon dosyalarını yerleştirdiğiniz yerdir |
| **/Scripts** | JavaScript kitaplığı dosyalarını ve komut dosyalarını (. js) yerleştirdiğiniz yer |
| **/Content** | CSS ve resim dosyalarını ve dinamik olmayan/JavaScript olmayan diğer içeriği yerleştirdiğiniz yer |
| **/App\_verileri** | Okumak/yazmak istediğiniz veri dosyalarını depoladığınız yerdir. |

ASP.NET MVC bu yapıyı gerektirmez. Aslında, büyük uygulamalar üzerinde çalışan geliştiriciler genellikle uygulamayı daha yönetilebilir hale getirmek için birden fazla proje genelinde bölümleyebilir (örneğin: veri modeli sınıfları, genellikle Web uygulamasından ayrı bir sınıf kitaplığı projesine gider). Bununla birlikte, varsayılan proje yapısı, uygulama kaygılarını temiz tutmak için kullanabilmemiz için iyi bir varsayılan dizin kuralı sağlar.

/Controllers dizinini genişlettiğimiz zaman, Visual Studio 'Nun iki denetleyici sınıfı (varsayılan olarak, giriş denetleyicisi ve AccountController) eklediğini bulacağız:

![](create-a-new-aspnet-mvc-project/_static/image5.png)

/Views dizinini genişlettiğimiz sırada üç alt dizin bulunur:/Home,/Account ve/Shared – Ayrıca, içindeki çeşitli şablon dosyaları da projeye varsayılan olarak eklenmiştir:

![](create-a-new-aspnet-mvc-project/_static/image6.png)

/Content ve/Scripts dizinlerini genişlettiğimiz zaman, sitedeki tüm HTML 'yi (Ayrıca, uygulamada ASP.NET AJAX ve jQuery desteğini etkinleştirebileceği JavaScript kitaplıklarını) bir site. css dosyası bulacağız:

![](create-a-new-aspnet-mvc-project/_static/image7.png)

Nerdakşam yemeği. Tests projesini genişlettiğimiz zaman denetleyici sınıflarımız için birim testlerini içeren iki sınıf bulacaksınız:

![](create-a-new-aspnet-mvc-project/_static/image8.png)

Visual Studio tarafından eklenen bu varsayılan dosyalar bize, çalışan bir uygulama için temel bir yapı ve giriş sayfası, sayfa, hesap oturumu açma/kayıt sayfaları ve işlenmemiş bir hata sayfası (tüm kablolu ve kutudan çıkar) sağlar.

### <a name="running-the-nerddinner-application"></a>Nerdakşam yemeği uygulamasını çalıştırma

Hata **Ayıkla-&gt;Başlat** veya **hata ayıkla-&gt;** hata ayıklama menü öğelerinden birini seçerek projeyi çalıştırabiliriz:

![](create-a-new-aspnet-mvc-project/_static/image9.png)

Bu işlem, Visual Studio ile birlikte gelen yerleşik ASP.NET Web sunucusunu başlatır ve uygulamamızı çalıştırır:

![](create-a-new-aspnet-mvc-project/_static/image10.png)

Yeni Projemiz için giriş sayfası (URL: "/") çalışırken aşağıda verilmiştir:

![](create-a-new-aspnet-mvc-project/_static/image11.png)

"Hakkında" sekmesine tıklanması hakkında bir sayfa (URL: "/Home/About") görüntülenir:

![](create-a-new-aspnet-mvc-project/_static/image12.png)

Sağ üst taraftaki "oturum aç" bağlantısına tıkladığınızda bir oturum açma sayfası (URL: "/Account/LogOn")

![](create-a-new-aspnet-mvc-project/_static/image13.png)

Bir oturum açma hesabınız yoksa, oluşturmak için kayıt bağlantısına tıklayeceğiz (URL: "/Account/Register"):

![](create-a-new-aspnet-mvc-project/_static/image14.png)

Yeni projemizi oluşturduğumuzda, yukarıdaki giriş, hakkında ve oturum kapatma/kaydetme işlevlerini uygulamak için kod varsayılan olarak eklenmiştir. Bunu uygulamamız başlangıç noktası olarak kullanacağız.

### <a name="testing-the-nerddinner-application"></a>Nerdakşam yemeği uygulamasını test etme

Visual Studio 2008 ' nin Professional sürümünü veya daha yüksek bir sürümünü kullandığımızda, Visual Studio içinde yerleşik birim testi IDE desteğini kullanarak projeyi test edebilirsiniz:

![](create-a-new-aspnet-mvc-project/_static/image15.png)

Yukarıdaki seçeneklerden birini seçmek, IDE 'nin içindeki "Test Sonuçları" bölmesini açar ve yeni projemizdeki yerleşik işlevselliği kapsayan 27 birim testlerinde Pass/Fail durumu sağlar:

![](create-a-new-aspnet-mvc-project/_static/image16.png)

Bu öğreticide daha sonra otomatikleştirilmiş test hakkında daha fazla konuşacak ve uyguladığımız uygulama işlevselliğini kapsayan ek birim testleri ekleyeceğiz.

### <a name="next-step"></a>Sonraki adım

Artık temel bir uygulama yapısı sunuyoruz. Şimdi [uygulama Verilerimizi depolamak için bir veritabanı oluşturalım](create-a-database.md).

> [!div class="step-by-step"]
> [Önceki](introducing-the-nerddinner-tutorial.md)
> [İleri](create-a-database.md)
