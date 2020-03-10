---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
title: 'Visual Studio kullanarak Web dağıtımı ASP.NET: ek dosyalar dağıtma | Microsoft Docs'
author: tdykstra
description: Bu öğretici serisi, bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf bir barındırma sağlayıcısına, usin...
ms.author: riande
ms.date: 03/23/2015
ms.assetid: 1cd91055-84bc-42c6-9d80-646f41429d4d
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
msc.type: authoredcontent
ms.openlocfilehash: eaa3141c22980f0c816e2f33b5597ac9fe69c23c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78548414"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-extra-files"></a>Visual Studio kullanarak Web dağıtımı ASP.NET: ek dosya dağıtma

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Başlatıcı projesi indir](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> Bu öğretici serisi, Visual Studio 2012 veya Visual Studio 2010 kullanarak bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf barındırma sağlayıcısına dağıtmayı (yayımlamayı) gösterir. Seriler hakkında daha fazla bilgi için, [serideki ilk öğreticiye](introduction.md)bakın.

## <a name="overview"></a>Genel bakış

Bu öğreticide, dağıtım sırasında ek bir görev yapmak üzere Visual Studio Web yayımlama işlem hattının nasıl genişletileceği gösterilmektedir. Görev, proje klasöründe olmayan ek dosyaları hedef Web sitesine kopyalamadır.

Bu öğreticide, bir ek dosyayı kopyalayacaksınız: *robots. txt*. Bu dosyayı hazırlama ve üretime dağıtma amacıyla dağıtmak istiyorsunuz. [Üretime dağıtım](deploying-to-production.md) öğreticisinde, bu dosyayı projeye eklediniz ve üretim yayımlama profilini, hariç tutacak şekilde yapılandırdınız. Bu öğreticide, dağıtmak istediğiniz ancak projeye dahil etmek istemediğiniz her dosya için yararlı olacak bir tane olan bu durumu işlemek için alternatif bir yöntem görürsünüz.

## <a name="move-the-robotstxt-file"></a>Robots. txt dosyasını taşıma

Farklı bir *robots. txt*işleme yöntemi hazırlamak için öğreticinin bu bölümünde dosyayı projede bulunmayan bir klasöre taşırsınız ve *robots. txt* dosyasını hazırlama ortamından silersiniz. Dosyayı bu ortama dağıtmaya yönelik yeni yönteminizin doğru çalıştığını doğrulayabilmeniz için dosyanın hazırlanmasından silinmesi gerekir.

1. **Çözüm Gezgini**, *robots. txt* dosyasına sağ tıklayın ve **projeden Dışla**' ya tıklayın.
2. Windows Dosya Gezgini 'ni kullanarak çözüm klasöründe yeni bir klasör oluşturun ve bunu *ExtraFiles*olarak adlandırın.
3. *Contosouniversity* proje klasöründen *robots. txt* dosyasını *ExtraFiles* klasörüne taşıyın.

    ![ExtraFiles klasörü](deploying-extra-files/_static/image1.png)
4. FTP aracınızı kullanarak, hazırlama Web sitesinden *robots. txt* dosyasını silin.

    Alternatif olarak, hazırlama yayımlama profilinin **Ayarlar** sekmesinde **dosya yayımlama seçenekleri** altında **Hedefteki ek dosyaları Kaldır** ' ı ve hazırlama için yeniden Yayımla ' yı seçebilirsiniz.

## <a name="update-the-publish-profile-file"></a>Yayımlama profili dosyasını güncelleştirme

Yalnızca, hazırlama sırasında yalnızca *robots. txt* dosyasına ihtiyacınız vardır, bu nedenle onu dağıtmak için güncelleştirmeniz gereken tek yayımlama profili hazırlanıyor.

1. Visual Studio 'da, *hazırlama. pubxml*' i açın.
2. Dosyanın sonunda, kapatma `</Project>` etiketinden önce aşağıdaki biçimlendirmeyi ekleyin:

    [!code-xml[Main](deploying-extra-files/samples/sample1.xml)]

    Bu kod, dağıtılacak ek dosyaları toplayacak yeni bir *hedef* oluşturur. Hedef, belirlediğiniz koşullara göre MSBuild 'in yürütüleceği bir veya daha fazla görevden oluşur.

    `Include` özniteliği, dosyaların bulunacağı klasörün, proje klasörüyle aynı düzeyde bulunan *ExtraFiles*olduğunu belirtir. MSBuild, bu klasördeki tüm dosyaları ve herhangi bir alt klasörden özyinelemeli olarak toplar (çift yıldız özyinelemeli alt klasörleri belirtir). Bu kodla, birden çok dosya ve dosyaları *ExtraFiles* klasörünün içindeki alt klasörlere koyabilirsiniz ve tümü dağıtılır.

    `DestinationRelativePath` öğesi, klasör ve dosyaların, *ExtraFiles* klasöründe bulunan aynı dosya ve klasör yapısındaki hedef Web sitesinin kök klasörüne kopyalanması gerektiğini belirtir. *ExtraFiles* klasörünün kendisini kopyalamak isterseniz, `DestinationRelativePath` değeri *ExtraFiles\%(RecursiveDir)% (filename)% (uzantı)* olur.
3. Dosyanın sonunda, kapatma `</Project>` etiketinden önce, yeni hedefin ne zaman yürütüleceğini belirten aşağıdaki biçimlendirmeyi ekleyin.

    [!code-xml[Main](deploying-extra-files/samples/sample2.xml)]

    Bu kod, yeni `CustomCollectFiles` hedefinin, dosyaları hedef klasöre kopyalayan hedef her yürütüldüğünde yürütülmesine neden olur. Dağıtım paketi oluşturma işlemi için ayrı bir hedef vardır ve yeni hedef, yayınlama yerine bir dağıtım paketi kullanarak dağıtmaya karar vermeniz durumunda her iki hedefe da eklenir.

    *. Pubxml* dosyası artık aşağıdaki örneğe benzer şekilde görünür:

    [!code-xml[Main](deploying-extra-files/samples/sample3.xml?highlight=53-71)]
4. *Hazırlama. pubxml* dosyasını kaydedin ve kapatın.

## <a name="publish-to-staging"></a>Hazırlama için Yayımla

Tek tıklamayla Yayımla ' yı veya komut satırını kullanarak, hazırlama profilini kullanarak uygulamayı yayımlayın.

Tek tıklamayla Yayımla ' yı kullanırsanız, bir **Önizleme** penceresinde *robots. txt* ' nin kopyalanacağını doğrulayabilirsiniz. Aksi takdirde, *robots. txt* dosyasının dağıtımdan sonra Web sitesinin kök klasöründe olduğunu doğrulamak için FTP aracınızı kullanın.

## <a name="summary"></a>Özet

Bu, bir ASP.NET Web uygulamasını bir üçüncü taraf barındırma sağlayıcısına dağıtmaya yönelik bu öğretici serisini tamamlar. Bu öğreticilerde ele alınan konuların herhangi biri hakkında daha fazla bilgi için [ASP.NET dağıtım Içerik haritasına](https://go.microsoft.com/fwlink/p/?LinkId=282413)bakın.

## <a name="more-information"></a>Daha fazla bilgi

MSBuild dosyalarıyla nasıl çalışacağınızı biliyorsanız, *. pubxml* dosyaları (profile özgü görevler için) veya Project *. WPP. targets* dosyası (tüm profiller için uygulanan görevler için) için kod yazarak diğer birçok dağıtım görevini otomatikleştirebilir. *. Pubxml* ve *. WPP. targets* dosyaları hakkında daha fazla bilgi Için bkz. [nasıl yapılır: Yayımlama profili (. Pubxml) dosyalarındaki dağıtım ayarlarını düzenleme ve Visual Studio Web projelerindeki. WPP. targets dosyası](https://msdn.microsoft.com/library/ff398069). MSBuild koduna temel bir giriş için bkz. kurumsal dağıtım serisinde **bir proje dosyasının Anatomumu** [: proje dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md). Kendi senaryolarınız için görevler gerçekleştirmek üzere MSBuild dosyalarıyla nasıl çalışacağınızı öğrenmek için şu kitaba bakın: Microsoft Build Engine: Içinde,, Sayıed Ibarhehashve William Bartholomew tarafından [MSBuild ve Team Foundation derlemesini kullanma](http://msbuildbook.com) .

## <a name="acknowledgements"></a>Bildirimler

Bu öğretici serisinin içeriğine önemli bir katkı yapan kişiler için teşekkür ederiz:

- [Alberto Poblacion, MVP &amp; MCT, Ispanya](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- Jarod Ferguson, veri platformu geliştirme MVP, Birleşik Devletler
- Harsh Mittal, Microsoft
- [Jon Galloway](https://weblogs.asp.net/jgalloway) (twitter: [@jongalloway](http://twitter.com/jongalloway))
- [Kristina Olson, Microsoft](https://blogs.iis.net/krolson/default.aspx)
- [Mike Pope, Microsoft](http://www.mikepope.com/blog/DisplayBlog.aspx)
- Mohit Srivastava, Microsoft
- [Raffaele Rialdi, Italya](http://www.iamraf.net/)
- [Rick Anderson, Microsoft](https://blogs.msdn.com/b/rickandy/)
- [Sayılan diyez, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))
- [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))
- [Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))
- [Srđan Božović, Sırbistan](http://msforge.net/blogs/zmajcek/)
- [Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))

> [!div class="step-by-step"]
> [Önceki](command-line-deployment.md)
> [İleri](troubleshooting.md)
