---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
title: Dosyaları ve klasörleri dağıtımdan dışlama | Microsoft Docs
author: jrjlee
description: Bu konuda, bir Web uygulaması projesi oluşturup paketlemeyi yaptığınızda bir Web dağıtım paketinden dosya ve klasörleri nasıl dışarıda bırakabileceğinizi açıklanmaktadır.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f4cc2d40-6a78-429b-b06f-07d000d4caad
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
msc.type: authoredcontent
ms.openlocfilehash: a262ce43d7199fb1015d54d0b7c213857c360946
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544977"
---
# <a name="excluding-files-and-folders-from-deployment"></a>Dosya ve Klasörleri Dağıtımdan Dışlama

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konuda, bir Web uygulaması projesi oluşturup paketlemeyi yaptığınızda bir Web dağıtım paketinden dosya ve klasörleri nasıl dışarıda bırakabileceğinizi açıklanmaktadır.

Bu konu, Fabrikam, Inc adlı kurgusal bir şirketin Kurumsal Dağıtım gereksinimlerini temel alarak bir öğretici serisinin bir parçasını oluşturur. Bu öğretici serisi, bir ASP.NET MVC&#x2014;3 uygulaması, Windows Communication Foundation (WCF) hizmeti ve bir veritabanı projesi dahil, gerçekçi bir karmaşıklık düzeyine sahip bir Web uygulamasını temsil etmek üzere bir örnek çözüm olan [Contact Manager çözümünü](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;kullanır.

Bu öğreticilerin temelini oluşturan dağıtım yöntemi, derleme işleminin her hedef ortam için uygulanan derleme yönergelerini içeren ve ortama özel yapı ve dağıtım ayarlarını içeren iki proje&#x2014;dosyası tarafından kontrol edilen proje [dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md)bölümünde açıklanan bölünmüş proje dosyası yaklaşımını temel alır. Derleme zamanında, ortama özgü proje dosyası, derleme yönergelerinin tam bir kümesini oluşturmak için ortam agtik proje dosyası ile birleştirilir.

## <a name="overview"></a>Genel bakış

Visual Studio 2010 ' de bir Web uygulaması projesi oluşturduğunuzda, Web yayımlama işlem hattı (WPP), derlenmiş Web uygulamanızı dağıtılabilir bir Web paketine paketleyerek bu yapı sürecini genişletmenizi sağlar. Daha sonra bu Web paketini uzak bir IIS Web sunucusuna dağıtmak veya Web paketini IIS Yöneticisi aracılığıyla el ile içeri aktarmak için Internet Information Services (IIS) Web Dağıtım aracı 'nı (Web Dağıtımı) kullanabilirsiniz. Bu paketleme işlemi, [Web uygulaması projelerini oluşturma ve paketleme](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)bölümünde açıklanmaktadır.

Peki Web paketinize nelerin dahil edildiğini nasıl denetlersiniz? Visual Studio 'daki proje ayarları temel alınan proje dosyası aracılığıyla çok sayıda senaryo için yeterli denetim sağlar. Ancak bazı durumlarda, Web paketinizin içeriğini belirli hedef ortamlara uyarlamak isteyebilirsiniz. Örneğin, uygulamanızı bir test ortamına dağıtırken ve uygulamayı bir hazırlık veya üretim ortamına dağıtırken klasörü dışladığınızda, günlük dosyaları için bir klasör dahil etmek isteyebilirsiniz. Bu konu, bunu nasıl yapılacağını gösterir.

## <a name="what-gets-included-by-default"></a>Varsayılan olarak neler dahildir?

Web uygulaması proje özelliklerinizi Visual Studio 'da yapılandırdığınızda, dağıtım **/Web yayımlama** sayfasında **dağıtılacak öğeler** listesi, Web Dağıtım paketinize neleri eklemek istediğinizi belirtmenize olanak tanır. Bu, varsayılan olarak **yalnızca bu uygulamayı çalıştırmak için gereken dosyalara**ayarlanmıştır.

![](excluding-files-and-folders-from-deployment/_static/image1.png)

**Yalnızca bu uygulamayı çalıştırmak için gereken dosyaları**SEÇTIĞINIZDE, WPP, Web paketine hangi dosyaların ekleneceğini belirlemek için çalışacaktır. Şunları içerir:

- Projenin tüm derleme çıkışları.
- **İçerik**oluşturma eylemiyle işaretlenmiş tüm dosyalar.

> [!NOTE]
> Hangi dosyaların ekleneceğini belirleyen mantık bu dosyada yer alır:   
> *%PROGRAMFILES%\MSBuild\Microsoft\VisualStudio\v10.0\Web\ Microsoft. Web. Publishing. OnlyFilesToRunTheApp. targets*

## <a name="excluding-specific-files-and-folders"></a>Belirli dosya ve klasörleri dışlama

Bazı durumlarda, hangi dosya ve klasörlerin dağıtıldığı üzerinde daha ayrıntılı denetim isteyeceksiniz. Hangi dosyaları zaman içinde dışarıda bırakmak istediğinizi biliyorsanız ve dışlama tüm hedef ortamlara geçerliyse, her dosyanın **derleme eylemini** **none**olarak ayarlayabilirsiniz.

**Belirli dosyaları dağıtımdan dışlamak için**

1. **Çözüm Gezgini** penceresinde, dosyaya sağ tıklayın ve ardından **Özellikler**' e tıklayın.
2. **Özellikler** penceresinde, **derleme eylemi** satırında **hiçbiri**' ni seçin.

Ancak, bu yaklaşım her zaman uygun değildir. Örneğin, hedef ortamınıza göre hangi dosya ve klasörlerin ekleneceğini ve Visual Studio 'Nun dışından değişiklik yapmak isteyebilirsiniz. Örneğin, Contact Manager örnek çözümünde ContactManager. Mvc projesinin içeriğine göz atın:

![](excluding-files-and-folders-from-deployment/_static/image2.png)

- Iç klasör, geliştiricinin geliştirme amacıyla yerel veritabanlarını oluşturmak, bırakmak ve doldurmak için kullandığı bazı SQL betikleri içerir. Bu klasördeki hiçbir şey bir hazırlık veya üretim ortamına dağıtılmalıdır.
- Betikler klasörü çeşitli JavaScript dosyaları içerir. Bu dosyaların çoğu, yalnızca hata ayıklamayı desteklemek ya da Visual Studio 'da IntelliSense sağlamak için eklenmiştir. Bu dosyalardan bazıları hazırlama veya üretim ortamlarına dağıtılmamalıdır. Ancak, sorun gidermeyi kolaylaştırmak için bunları bir geliştirici sınama ortamına dağıtmak isteyebilirsiniz.

Proje dosyalarınızı belirli dosya ve klasörleri dışarıda bırakacak şekilde işleyebilseniz de, daha kolay bir yol vardır. WPP, **Excludefrompackagefolders** ve **Excludefrompackagefiles**adlı öğe listeleri oluşturarak dosya ve klasörleri hariç tutmak için bir mekanizma içerir. Kendi öğelerinizi bu listelere ekleyerek bu mekanizmayı genişletebilirsiniz. Bunu yapmak için, aşağıdaki üst düzey adımları gerçekleştirmeniz gerekir:

1. Proje dosyanız ile aynı klasörde *[proje adı]. WPP. targets* adlı özel bir proje dosyası oluşturun.

    > [!NOTE]
    > *. WPP. targets* dosyasının, derleme ve dağıtım işlemini denetlemek için kullandığınız özel proje dosyalarıyla aynı klasörde değil&#x2014; *,* &#x2014;Web uygulaması proje dosyası ile aynı klasöre gitmesi gerekir.
2. *. WPP. targets* dosyasında bir **ItemGroup** öğesi ekleyin.
3. **ItemGroup** öğesinde, belirli dosya ve klasörleri gerektiği şekilde dışlamak Için **Excludefrompackagefolders** ve **Excludefrompackagefiles** öğelerini ekleyin.

Bu, bu *. WPP. targets* dosyasının temel yapısıdır:

[!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample1.xml)]

Her öğenin **Fromtarget**adlı bir öğe meta veri öğesi içerdiğini unutmayın. Bu, yapı işlemini etkilemeyen isteğe bağlı bir değerdir; yalnızca bir kişi, Derleme günlüklerini gözden geçirirse belirli dosya veya klasörlerin neden atlandığını belirtmek için kullanılır.

## <a name="excluding-files-and-folders-from-a-web-package"></a>Dosya ve klasörleri bir Web paketinden dışlama

Sonraki yordamda, bir Web uygulaması projesine *. WPP. targets* dosyasını nasıl ekleyeceğiniz ve projenizi oluştururken Web paketinden belirli dosya ve klasörleri dışlamak için dosyanın nasıl kullanılacağı gösterilmektedir.

**Dosya ve klasörleri bir Web dağıtım paketinden dışlamak için**

1. Çözümünüzü Visual Studio 2010 ' de açın.
2. **Çözüm Gezgini** penceresinde, Web uygulaması proje düğümünüz (örneğin, **ContactManager. Mvc**) sağ tıklayın, **Ekle**' nin üzerine gelin ve ardından **Yeni öğe**' ye tıklayın.
3. **Yeni öğe Ekle** iletişim kutusunda, **XML dosya** şablonunu seçin.
4. **Ad** kutusuna *[proje adı] * * *. WPP. targets** yazın (örneğin, **ContactManager. Mvc. WPP. targets**) ve ardından **Ekle**' ye tıklayın.

    ![](excluding-files-and-folders-from-deployment/_static/image3.png)

    > [!NOTE]
    > Projenin kök düğümüne yeni bir öğe eklerseniz, dosya proje dosyası ile aynı klasörde oluşturulur. Bunu, Windows Gezgini 'nde klasörünü açarak doğrulayabilirsiniz.
5. Dosyasında bir **Proje** öğesi ve bir **ItemGroup** öğesi ekleyin:

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample2.xml)]
6. Klasörleri Web paketinden dışlamak istiyorsanız, **ItemGroup** öğesine bir **Excludefrompackagefolders** öğesi ekleyin:

   1. **Include** özniteliğinde, dışlamak istediğiniz klasörlerin noktalı virgülle ayrılmış bir listesini sağlayın.
   2. **Fromtarget** meta veri öğesinde, *. WPP. targets* dosyasının adı gibi klasörlerin Neden dışlandığını belirten anlamlı bir değer sağlayın.

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample3.xml)]
7. Dosyaları Web paketinden dışlamak istiyorsanız, **ItemGroup** öğesine bir **Excludefrompackagefiles** öğesi ekleyin:

   1. **Include** özniteliğinde, dışlamak istediğiniz dosyaların noktalı virgülle ayrılmış bir listesini sağlayın.
   2. **Fromtarget** meta verileri öğesinde, dosyaların neden dışlandığını belirten, *. WPP. targets* dosyasının adı gibi anlamlı bir değer sağlayın.

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample4.xml)]
8. *[Proje adı]. WPP. targets* dosyası artık şuna benzemelidir:

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample5.xml)]
9. *[Proje adı]. WPP. targets* dosyasını kaydedin ve kapatın.

Web uygulaması projenizi bir sonraki derleme ve paketleme sırasında, WPP *. WPP. targets* dosyasını otomatik olarak algılar. Belirttiğiniz tüm dosyalar ve klasörler Web paketine dahil edilmez.

## <a name="conclusion"></a>Sonuç

Bu konu, Web paketi oluştururken, Web uygulaması proje dosyanız ile aynı klasörde özel bir *. WPP. targets* dosyası oluşturarak belirli dosya ve klasörlerin nasıl hariç tutulacağı açıklanmaktadır.

## <a name="further-reading"></a>Daha Fazla Bilgi

Dağıtım işlemini denetlemek için özel Microsoft Build Engine (MSBuild) proje dosyalarını kullanma hakkında daha fazla bilgi için bkz. [Proje dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md) ve [derleme sürecini anlama](../web-deployment-in-the-enterprise/understanding-the-build-process.md). Paketleme ve dağıtım işlemi hakkında daha fazla bilgi için bkz. [Web uygulaması projelerini oluşturma ve paketleme](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md), [Web paketi dağıtımı için parametreleri yapılandırma](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md)ve [Web paketleri dağıtma](../web-deployment-in-the-enterprise/deploying-web-packages.md).

> [!div class="step-by-step"]
> [Önceki](deploying-membership-databases-to-enterprise-environments.md)
> [İleri](taking-web-applications-offline-with-web-deploy.md)
