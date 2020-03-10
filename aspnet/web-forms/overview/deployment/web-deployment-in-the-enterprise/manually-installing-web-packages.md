---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
title: Web paketlerini el ile yükleme | Microsoft Docs
author: jrjlee
description: Bu konu, bir Web dağıtım paketini Internet Information Services (IIS) içine el ile nasıl içeri aktarabileceğinizi açıklamaktadır. Web uygulaması oluşturma ve paketleme konusu...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f11d22a7-5d32-4ad0-8a9b-276460a61c06
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
msc.type: authoredcontent
ms.openlocfilehash: f778549d3e26989a2e71ef21171adec521842729
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634206"
---
# <a name="manually-installing-web-packages"></a>Web Paketlerini El ile Yükleme

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konu, bir Web dağıtım paketini Internet Information Services (IIS) içine el ile nasıl içeri aktarabileceğinizi açıklamaktadır.
> 
> [Web uygulaması projelerini oluşturma ve paketleme](building-and-packaging-web-application-projects.md) konusunda, IIS Web Dağıtım aracı 'nın (Web dağıtımı), Microsoft Build Engine (MSBuild) ve Web yayımlama işlem hattı (WPP) ile birlikte, Web uygulaması projelerinizi tek bir zip dosyasına paketlemenize olanak tanır. Genellikle bir Web dağıtım paketi (veya yalnızca bir dağıtım paketi) olarak bilinen bu dosya, Web uygulamanızı bir Web sunucusunda yeniden oluşturmak için IIS 'nin ihtiyaç duyacağı tüm içerik ve yapılandırma bilgilerini içerir.
> 
> Bir Web dağıtım paketi oluşturduktan sonra, bunu çeşitli yollarla bir IIS sunucusunda yayımlayabilirsiniz. Birçok senaryoda, MSBuild, WPP ve Web Dağıtımı arasındaki tümleştirme noktalarından yararlanarak otomatik veya tek adımlı derleme ve dağıtım sürecinin bir parçası olarak Uzaktan Web paketleri oluşturup yükleyebilirsiniz. Bu işlem [Web paketlerinin dağıtılmasında](deploying-web-packages.md)açıklanmıştır. Ancak, bu her zaman mümkün değildir. Bir Web uygulamasını Internet 'e yönelik bir üretim ortamına dağıtmak istediğinizi varsayalım. Güvenlik nedenleriyle, bir üretim ortamı, derleme sunucusundan (DMZ, sivil bölge ve denetimli alt ağ olarak da bilinir) ayrı bir alt ağda bir güvenlik duvarının arkasında olma olasılığı yüksektir. Birçok durumda, üretim ortamı ayrı bir etki alanında veya fiziksel olarak yalıtılmış bir ağda olacaktır.
> 
> Bu senaryolarda, tek seçeneğiniz Web paketinin hedef sunucuya bağlantı noktası haline gelebilir ve el ile IIS 'ye içeri aktarabilirsiniz. Bu yaklaşım otomatik dağıtıma neden olsa da, bir Web uygulaması&#x2014;yayımlamak için oldukça etkili bir tekniktir, Web sunucunuza tek bir ZIP dosyasını kopyalamanız ve içeri aktarma işleminde size rehberlik etmek için bir sihirbaz kullanmanız yeterlidir.

Bu konu, Fabrikam, Inc adlı kurgusal bir şirketin Kurumsal Dağıtım gereksinimlerini temel alarak bir öğretici serisinin bir parçasını oluşturur. Bu öğretici serisi, bir ASP.NET MVC&#x2014;3 uygulaması, Windows Communication Foundation (WCF) hizmeti ve bir veritabanı projesi dahil, gerçekçi bir karmaşıklık düzeyine sahip bir Web uygulamasını temsil etmek üzere bir örnek çözüm olan [Contact Manager çözümünü](the-contact-manager-solution.md)&#x2014;kullanır.

## <a name="task-overview"></a>Göreve genel bakış

Web dağıtım paketini IIS 'e aktarmak için bu üst düzey görevleri gerçekleştirmeniz gerekir:

- MSBuild komut satırı, takım derlemesi veya Visual Studio 2010 kullanarak bir Web dağıtım paketi oluşturun.
- Web paketini hedef Web sunucusuna kopyalayın.
- Web paketini yüklemek ve bağlantı dizeleri ve hizmet uç noktaları gibi değişkenler için değerler sağlamak üzere IIS Yöneticisi 'ndeki uygulama paketini Içeri aktarma Sihirbazı 'Nı kullanın.

Bu konu başlığı altında, bu yordamların nasıl gerçekleştirileceği gösterilmektedir. Bu konudaki görevler ve izlenecek yollar, Web paketleri, Web Dağıtımı ve WPP 'nin arkasındaki kavramları zaten öğrenolduğunuzu varsayar. Daha fazla bilgi için bkz. [Web uygulaması projelerini oluşturma ve paketleme](building-and-packaging-web-application-projects.md).

> [!NOTE]
> Bu konu, [bir Web sunucusunu Web dağıtımı yayımlama Için yapılandırma (çevrimdışı dağıtım)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)ile birlikte en iyi şekilde kullanılmak üzere, gerekli bileşenlerin nasıl yükleneceğini ve paket içeri aktarma IÇIN bir IIS Web sitesi nasıl hazırlanacağını açıklar.

## <a name="create-a-web-deployment-package"></a>Web dağıtım paketi oluşturma

İlk görev, dağıtmak istediğiniz Web uygulaması projesi için bir Web dağıtım paketi oluşturmaktır. Web paketlerini çeşitli yollarla oluşturabilirsiniz.

**Yaklaşım 1: Visual Studio ile derleme sürecinin bir parçası olarak paket oluşturma**

Web uygulaması projenizi, her derlemeden sonra bir Web dağıtım paketi oluşturacak şekilde yapılandırabilir ve proje özellik sayfalarındaki **Web 'ı Yayımla** sekmesini kullanarak. Bu işlem, [Web uygulaması projelerini oluşturma ve paketleme](building-and-packaging-web-application-projects.md)konularında açıklanmaktadır.

**2. yaklaşım: MSBuild ile derleme işleminin bir parçası olarak bir paket oluşturma**

Özel bir MSBuild proje dosyası ya da komut satırından doğrudan MSBuild 'i kullanarak Web uygulaması projenizi derliyorsanız, komutunuz **Deployonbuild = true** ve **Deploytarget = Package** özelliklerini ekleyerek yapı işleminin bir parçası olarak bir Web dağıtım paketi oluşturabilirsiniz. Bu işlem [, yapı sürecini anlama](understanding-the-build-process.md)bölümünde açıklanmaktadır.

**Yaklaşım 3: Visual Studio 'da isteğe bağlı bir paket oluşturma**

Web uygulaması projesi için, Visual Studio 2010 ' de dilediğiniz zaman Web dağıtım paketi oluşturabilirsiniz. Bunu yapmak için, **Çözüm Gezgini** penceresinde, Web uygulaması projenize sağ tıklayın ve ardından **dağıtım paketi oluştur**' a tıklayın.

![](manually-installing-web-packages/_static/image1.png)

**Yaklaşım 4: komut satırından isteğe bağlı bir paket oluşturma**

MSBuild kullanarak Web uygulaması projenizdeki **paket** hedefini çağırarak komut satırından bir Web dağıtım paketi oluşturabilirsiniz. Komut şuna benzemelidir:

[!code-console[Main](manually-installing-web-packages/samples/sample1.cmd)]

Hangi yaklaşımı kullanırsanız kullanın, nihai sonuç aynıdır. WPP, Web uygulaması projenizin çıktı klasöründe çeşitli destekleyici kaynaklarla birlikte bir Web dağıtım paketini ZIP dosyası olarak oluşturur.

![](manually-installing-web-packages/_static/image2.png)

Web paketini el ile aktarmayı planlarken, yalnızca ZIP dosyası gerekir. Bu dosyayı hedef Web sunucunuza kopyalayın ve içeri aktarma işlemini başlatabilirsiniz.

## <a name="import-a-web-package-into-iis"></a>Web paketini IIS 'e aktarma

Bir Web dağıtım paketini yerel dosya sisteminden bir IIS Web sitesine aktarmak için bir sonraki yordamı kullanabilirsiniz. Bu yordamı gerçekleştirmeden önce, şunları kullandığınızdan emin olun:

- Web dağıtım paketi Web sunucusuna kopyalanamadı.
- Uygulamanızı barındırmak için bir IIS Web sunucusu yapılandırıldı.

Web dağıtım paketlerini desteklemek için bir IIS Web sunucusu yapılandırma hakkında daha fazla bilgi için bkz. [bir Web sunucusunu Web dağıtımı yayımlama Için yapılandırma (çevrimdışı dağıtım)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md).

**IIS Yöneticisi 'Ni kullanarak bir Web dağıtım paketini içeri aktarmak için**

1. IIS Yöneticisi 'nde, **Bağlantılar** BÖLMESINDE, IIS Web sitenize sağ tıklayın, **Dağıt**' ın üzerine gelin ve ardından **uygulamayı içeri aktar**' a tıklayın.

    ![](manually-installing-web-packages/_static/image3.png)
2. Uygulama paketini Içeri aktarma sihirbazında, **paketi seçin** sayfasında, Web Dağıtım paketinizin konumuna gidin ve ardından **İleri**' ye tıklayın.
3. **Paketin Içeriğini seçin** sayfasında, ihtiyacınız olmayan tüm içerikleri temizleyin ve ardından **İleri**' ye tıklayın.

    ![](manually-installing-web-packages/_static/image4.png)

    > [!NOTE]
    > Birçok durumda, bir Web Dağıtım paketiyle birlikte gelen her şeyi içeri aktarmak istemeyebilirsiniz. Örneğin, Web Dağıtımı ilişkili veritabanının değiştirilmesini sağlamak istemeyebilirsiniz.  
    > **Izin verme** girişleri, uygulama havuzu kimliğinin Web sitesi içeriğini depolayan fiziksel klasöre erişebildiğinden emin olmak için hedef dosya sisteminde izinleri ayarlar. Buna ek olarak, anonim kimlik doğrulama kullanıcısına uygulamanın çok amaçlı Internet posta uzantıları (MIME) tür dosyalarını sunmasını sağlamak için klasöre okuma izni verilir. İsterseniz, bu girişleri kaldırabilir ve izinleri el ile yapılandırabilirsiniz.
4. **Uygulama paketi bilgilerini girin** sayfasında, istenen bilgileri sağlayın.

    ![](manually-installing-web-packages/_static/image5.png)
5. Bir Web paketi oluşturduğunuzda, WPP, uygulamanızın yapılandırma dosyasını analiz eder ve bağlantı dizeleri ve hizmet uç noktaları gibi tüm değişkenleri algılar. Bu durumda:

    1. **Uygulama yolu** , uygulamanızı yüklemek istediğiniz IIS yoludur. Bu ayar, WPP 'nin oluşturduğu tüm dağıtım paketlerinde ortaktır.
    2. **ContactService hizmet uç noktası adresi** , UYGULAMANıN dağıtılan WCF hizmetiyle iletişim kurmak için kullanması gereken adrestir. Bu ayar, *Web. config* dosyasındaki bir girdiye karşılık gelir.
    3. İlk **bağlantı dizesi** ayarı, Web dağıtımı uygulamayla ilişkili veritabanını (Bu durumda bir ASP.NET üyelik veritabanı) dağıtmak için kullanması gereken bağlantı dizesidir. Bu ayar, Visual Studio 'da **paket/YAYıMLAMA SQL** sekmesindeki ayara karşılık gelir.
    4. İkinci **bağlantı dizesi** ayarı, uygulamanızın çalışır duruma geldiğinde veritabanıyla iletişim kurmak için kullanacağı bağlantı dizesidir. Bu, *Web. config* dosyasındaki bir bağlantı dizesi girişine karşılık gelir.

        > [!NOTE]
        > Bu parametrelerin nereden geldiği hakkında daha fazla bilgi için bkz. [Web paketi dağıtımı Için parametreleri yapılandırma](configuring-parameters-for-web-package-deployment.md).
6. **İleri**'ye tıklayın.
7. Uygulamayı bu Web sitesine ilk kez dağıtmadıysanız, yüklemeden önce tüm mevcut içeriği silmek isteyip istemediğinizi belirtmeniz istenir. Gereksinimleriniz için uygun olan seçeneği seçin ve ardından **İleri**' ye tıklayın.

    ![](manually-installing-web-packages/_static/image6.png)
8. IIS, paketi yüklemeyi tamamladığında **son**' a tıklayın.

    ![](manually-installing-web-packages/_static/image7.png)

Bu noktada, Web uygulamanızı başarıyla IIS 'de yayımladınız.

## <a name="conclusion"></a>Sonuç

Bu konu, bir Web dağıtım paketinin IIS Yöneticisi kullanılarak bir IIS Web sitesine nasıl içeri aktarılacağını açıklamaktadır. Web uygulaması yayımlamasına yönelik bu yaklaşım, güvenlik veya altyapı kısıtlamaları uzaktan dağıtımı olanaksız veya istenmeyen hale getirir.

## <a name="further-reading"></a>Daha Fazla Bilgi

Bir Web paketini el ile içeri aktarmaya yönelik bir IIS Web sunucusunun nasıl yapılandırılacağı hakkında yönergeler için bkz. [bir Web sunucusunu Web dağıtımı yayımlama Için yapılandırma (çevrimdışı dağıtım)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md). Web paketlerinin dağıtılması hakkında daha fazla genel bilgi için bkz. [Izlenecek yol: Web uygulaması projesi bir Web dağıtım paketi (Bölüm 1/4) kullanarak dağıtma](https://msdn.microsoft.com/library/dd483479.aspx).

> [!div class="step-by-step"]
> [Öncekini](creating-and-running-a-deployment-command-file.md)
