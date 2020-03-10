---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
title: Kaynak denetimine Içerik ekleme | Microsoft Docs
author: jrjlee
description: Bu konuda Team Foundation Server (TFS) 2010 ' de kaynak denetimine içerik ekleme açıklanmaktadır. Takım projesine nasıl çözüm ve proje ekleneceğini açıklar...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 86c14aab-c2dd-4f73-b40c-c6d52fa44950
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
msc.type: authoredcontent
ms.openlocfilehash: 16073dd2fb0ea1cc4ddbc94c843181933dc174c1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634465"
---
# <a name="adding-content-to-source-control"></a>Kaynak Denetimine İçerik Ekleme

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konuda Team Foundation Server (TFS) 2010 ' de kaynak denetimine içerik ekleme açıklanmaktadır. TFS 'deki bir ekip projesine çözüm ve proje eklemeyi açıklar ve kaynak denetimine çerçeveler veya derlemeler gibi dış bağımlılıkların nasıl ekleneceğini açıklar.

Bu konu, Fabrikam, Inc adlı kurgusal bir şirketin Kurumsal Dağıtım gereksinimlerini temel alarak bir öğretici serisinin bir parçasını oluşturur. Bu öğretici serisi, bir ASP.NET MVC&#x2014;3 uygulaması, Windows Communication Foundation (WCF) hizmeti ve bir veritabanı projesi dahil, gerçekçi bir karmaşıklık düzeyine sahip bir Web uygulamasını temsil etmek üzere bir örnek çözüm olan [Contact Manager çözümünü](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;kullanır.

## <a name="task-overview"></a>Göreve genel bakış

Çoğu durumda, geliştirici ekibinin her üyesi kaynak denetimine içerik ekleyebilmelidir. TFS 'deki kaynak denetimine bir çözüm eklemek için, bu üst düzey adımları gerçekleştirmeniz gerekir:

- Bir takım projesine bağlanın.
- Sunucudaki takım projesi klasörü yapısını yerel bilgisayarınızdaki bir klasör yapısına eşleyin.
- Çözümü ve içeriğini kaynak denetimine ekleyin.
- Kaynak denetimine herhangi bir dış bağımlılık ekleyin.

Bu konu başlığı altında, bu yordamların nasıl gerçekleştirileceği gösterilmektedir.

Bu konudaki görevler ve izlenecek yollar, içeriğinizi yönetmek için zaten yeni bir TFS takım projesi oluşturmuş olduğunuz varsayılmaktadır. Yeni bir takım projesi oluşturma hakkında daha fazla bilgi için bkz. [TFS 'de bir takım projesi oluşturma](creating-a-team-project-in-tfs.md).

### <a name="who-performs-these-procedures"></a>Bu yordamları kim gerçekleştiriyor?

Çoğu durumda, geliştirici ekibinin her üyesi belirli takım projeleri içinde içerik ekleyip değiştirebilmelidir.

## <a name="connect-to-a-team-project-and-create-a-folder-mapping"></a>Bir takım projesine bağlanın ve bir klasör eşlemesi oluşturun

Kaynak denetimine içerik eklemeden önce, bir ekip projesine bağlanmanız ve yerel makinenizde dosya sistemi ve sunucu üzerindeki klasör yapısı arasında bir eşleme oluşturmanız gerekir.

**Bir takım projesine bağlanmak ve yerel bir yolu eşlemek için**

1. Geliştirici iş istasyonunuzda, Visual Studio 2010 ' u açın.
2. Visual Studio 'da, **Takım** menüsünde **Team Foundation Server Bağlan**' a tıklayın.

    > [!NOTE]
    > TFS sunucusuna zaten bir bağlantı yapılandırdıysanız 3-6 arasındaki adımları atlayabilirsiniz.
3. **Takım projesi bağlantısı** Iletişim kutusunda **sunucular**' a tıklayın.
4. **Team Foundation Server Ekle/Kaldır** Iletişim kutusunda **Ekle**' ye tıklayın.
5. **Team Foundation Server Ekle** ILETIŞIM kutusunda TFS örneğinizin ayrıntılarını belirtin ve ardından **Tamam**' a tıklayın.

    ![](adding-content-to-source-control/_static/image1.png)
6. **Team Foundation Server Ekle/Kaldır** Iletişim kutusunda **Kapat**' a tıklayın.
7. **Takım Projesine Bağlan** iletişim kutusunda, bağlanmak istediğiniz TFS örneğini seçin, takım projesi koleksiyonunu seçin, eklemek istediğiniz takım projesini seçin ve ardından **Bağlan**' a tıklayın.

    ![](adding-content-to-source-control/_static/image2.png)
8. **Takım Gezgini** penceresinde, takım projenizi genişletin ve ardından **kaynak denetimi**' ne çift tıklayın.

    ![](adding-content-to-source-control/_static/image3.png)
9. **Kaynak Denetim Gezgini** sekmesinde **eşlenmemiş**' e tıklayın.

    ![](adding-content-to-source-control/_static/image4.png)
10. **Harita** iletişim kutusunda, **yerel klasör** kutusunda, takım projesi için kök klasör olarak davranacak yerel bir klasöre gidin (veya oluşturun) ve ardından **eşle**' ye tıklayın.

    ![](adding-content-to-source-control/_static/image5.png)
11. Kaynak dosyaları indirmek isteyip istemediğiniz sorulduğunda **Evet**' e tıklayın.

    ![](adding-content-to-source-control/_static/image6.png)

Bu noktada, takım projesi için sunucu tarafı klasörünü geliştirici iş istasyonunuzda yerel bir klasöre eşlediniz. Ayrıca, var olan tüm içeriği takım projesinden yerel klasör yapınıza indirdiniz. Artık kaynak denetimine kendi içeriğinizi eklemeye başlayabilirsiniz.

## <a name="add-projects-and-solutions-to-source-control"></a>Kaynak denetimine proje ve çözüm ekleme

Kaynak denetimine projeler ve çözümler eklemek için, önce bunları yerel makinenizde takım projesi için eşlenmiş klasöre taşımanız gerekir. Daha sonra, eklemelerinizi sunucuyla eşitlemenize sonra içeriği iade edebilirsiniz.

**Kaynak denetimine proje eklemek için**

1. Geliştirici iş istasyonunuzda, projelerinizi ve çözümlerinizi takım projesi için eşlenmiş klasör yapısı içinde uygun bir konuma taşıyın.

    > [!NOTE]
    > Birçok kuruluş, proje ve çözümlerin kaynak denetiminde nasıl düzenleneceğine yönelik tercih edilen bir yaklaşıma sahip olacaktır. Klasörleri nasıl yapılandıracağınıza ilişkin yönergeler için bkz. [nasıl yapılır: kaynak denetim klasörlerinizi yapılandırma Team Foundation Server](https://msdn.microsoft.com/library/bb668992.aspx).
2. Visual Studio 2010 ' de çözümü açın.
3. **Çözüm Gezgini** penceresinde çözüme sağ tıklayın ve ardından **kaynak denetimine çözüm Ekle**' ye tıklayın.

    ![](adding-content-to-source-control/_static/image7.png)

    > [!NOTE]
    > Bazı durumlarda, kuruluşunuzun TFS 'de içerik yapısını nasıl sağladığına bağlı olarak kaynak denetimine proje eklemeniz gerekebilir. böylece, kaynak kodunuza nasıl düzenleneceğine daha ayrıntılı bir denetim sağlayabilirsiniz.
4. **Kaynak Denetim Gezgini** sekmesinin, takım projesi için sunucu klasörü yapısı içinde eklediğiniz içeriği görüntülediğini doğrulayın.

    ![](adding-content-to-source-control/_static/image8.png)

    > [!NOTE]
    > **Kaynak Denetim Gezgini** sekmesi, çözümünüzü yerel dosya sistemindeki eşlenmiş bir klasöre eklediğiniz için daha fazla istem yapmadan içeriğinizi görüntüler. Çözümünüz eşlenmemiş bir konumdaysa, hem TFS 'de hem de yerel dosya sisteminizde klasör konumları belirtmeniz istenir.
5. **Kaynak Denetim Gezgini** sekmesinde, **Klasörler** bölmesinde, takım projesine (örneğin, **ContactManager**) sağ tıklayın ve ardından **bekleyen değişiklikleri iade et**' e tıklayın.
6. **Iade et – kaynak dosyalar** iletişim kutusunda bir açıklama yazın ve **iade et**' e tıklayın.

    ![](adding-content-to-source-control/_static/image9.png)

Bu noktada, çözümünüzü TFS 'deki kaynak denetimine eklediniz.

## <a name="add-external-dependencies-to-source-control"></a>Kaynak denetimine dış bağımlılıklar ekleme

Kaynak denetimine bir proje veya çözüm eklediğinizde, projeniz veya çözümünüz içindeki tüm dosyalar ve klasörler de eklenir. Ancak, çok sayıda durumda, projeler ve çözümler, yerel derlemeler gibi dış bağımlılıklara de dayanır, bu da düzgün şekilde çalışır. Her iki ekip derlemesinin ve geliştirici ekibinin diğer üyelerinin kodunuzu başarıyla oluşturmasını sağlamak için kaynak denetimine bu tür kaynakları eklemeniz gerekir.

Örneğin, Contact Manager örnek çözümünün klasör yapısı, paketler adlı bir klasör içerir. Bu, derlemeyi ve ADO.NET Entity Framework 4,1 için çeşitli destekleyici kaynakları içerir. Paketler klasörü, Contact Manager çözümünün bir parçası değildir, ancak çözüm bu olmadan başarıyla derlenmeyecektir. Çözümü oluşturmak üzere ekip yapısını etkinleştirmek için, kaynak denetimine paketler klasörünü eklemeniz gerekir.

> [!NOTE]
> Bir paketler klasörünün dahil edilmesi, Visual Studio 2010 için NuGet uzantısını kullanarak çözümünüze Entity Framework veya benzer kaynakları eklediğinizde ne olacağı hakkında tipik bir şeydir.

**Kaynak denetimine proje olmayan içerik eklemek için**

1. Eklemek istediğiniz öğelerin (örneğin, paketler klasörü) yerel dosya sisteminizdeki eşlenmiş bir klasör içinde uygun bir konumda olduğundan emin olun.
2. Visual Studio 2010 ' de **Takım Gezgini** penceresinde, takım projenizi genişletin ve ardından **kaynak denetimi**' ne çift tıklayın.

    ![](adding-content-to-source-control/_static/image10.png)
3. **Kaynak Denetim Gezgini** sekmesinde, **Klasörler** bölmesinde, eklemek istediğiniz öğe veya öğeleri içeren klasörü seçin.
4. **Klasöre öğe Ekle** düğmesine tıklayın.

    ![](adding-content-to-source-control/_static/image11.png)
5. **Kaynak denetimine Ekle** iletişim kutusunda, eklemek istediğiniz klasörü veya öğeleri seçin ve ardından **İleri**' ye tıklayın.

    ![](adding-content-to-source-control/_static/image12.png)
6. **Dışlanan öğeler** sekmesinde, otomatik olarak dışlanan gerekli öğeleri (örneğin, derlemeler) seçin ve ardından **öğeleri dahil et**' e tıklayın.

    ![](adding-content-to-source-control/_static/image13.png)
7. **Eklenecek öğeler** sekmesinde, dahil etmek istediğiniz tüm dosyaların listelendiğinden emin olun ve ardından **son**' a tıklayın.

    ![](adding-content-to-source-control/_static/image14.png)
8. **Kaynak Denetim Gezgini** penceresinde, **iade et** düğmesine tıklayın.

    ![](adding-content-to-source-control/_static/image15.png)
9. **Iade et – kaynak dosyalar** iletişim kutusunda bir açıklama yazın ve **iade et**' e tıklayın.

Bu noktada, çözümünüz için dış bağımlılıkları kaynak denetimine eklediniz.

## <a name="conclusion"></a>Sonuç

Bu konu, bir ekip projesine bağlanma, bir klasör yapısını eşleme ve kaynak denetimine içerik ekleme konularında anlatılmıştır. Kaynak denetimi altındaki öğelerle çalışma hakkında daha fazla bilgi için bkz. [Sürüm denetimini kullanma](https://msdn.microsoft.com/library/ms181368.aspx).

Bir sonraki konu, [Web dağıtımı için BIR TFS derleme sunucusu yapılandırırken](configuring-a-tfs-build-server-for-web-deployment.md), çözümünüzü derlemek ve dağıtmak IÇIN bir TFS ekip yapı sunucusunun nasıl hazırlanacağını açıklar.

## <a name="further-reading"></a>Daha Fazla Bilgi

TFS 'de kaynak denetimiyle çalışma hakkında daha ayrıntılı bilgi için bkz. [Sürüm denetimini kullanma](https://msdn.microsoft.com/library/ms181368.aspx).

> [!div class="step-by-step"]
> [Önceki](creating-a-team-project-in-tfs.md)
> [İleri](configuring-a-tfs-build-server-for-web-deployment.md)
