---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
title: Belirli bir derlemeyi dağıtma | Microsoft Docs
author: jrjlee
description: Bu konu, bir hazırlama veya üretim Enviro gibi belirli bir önceki derlemeden yeni bir hedefe Web paketleri ve veritabanı betikleri dağıtmayı açıklar...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c979535f-48a3-4ec4-a633-a77889b86ddb
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
msc.type: authoredcontent
ms.openlocfilehash: 6bede6b36c24ade928ab052e14daec1e017bd0b2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639673"
---
# <a name="deploying-a-specific-build"></a>Belirli bir Derlemeyi Dağıtma

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konuda, belirli bir önceki derlemeden, hazırlama veya üretim ortamı gibi yeni bir hedefe Web paketlerinin ve veritabanı betiklerinin nasıl dağıtılacağı açıklanmaktadır.

Bu konu, Fabrikam, Inc adlı kurgusal bir şirketin Kurumsal Dağıtım gereksinimlerini temel alarak bir öğretici serisinin bir parçasını oluşturur. Bu öğretici serisi, bir ASP.NET MVC&#x2014;3 uygulaması, Windows Communication Foundation (WCF) hizmeti ve bir veritabanı projesi dahil, gerçekçi bir karmaşıklık düzeyine sahip bir Web uygulamasını temsil etmek üzere bir örnek çözüm olan [Contact Manager çözümünü](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;kullanır.

Bu öğreticilerin temelini oluşturan dağıtım yöntemi, derleme ve dağıtım sürecinin, her hedef ortam için uygulanan derleme yönergelerini içeren iki proje&#x2014;dosyası tarafından denetlendiği ve ortama özgü derleme ve dağıtım ayarlarını içeren, proje [dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md)bölümünde açıklanan bölünmüş proje dosyası yaklaşımını temel alır. Derleme zamanında, ortama özgü proje dosyası, derleme yönergelerinin tam bir kümesini oluşturmak için ortam agtik proje dosyası ile birleştirilir.

## <a name="task-overview"></a>Göreve genel bakış

Bu öğreticide, bu öğretici kümesindeki konular, tek adımlı veya otomatik bir işlemin bir parçası olarak Web uygulamaları ve veritabanlarının nasıl derlenmesi, paketlenecek ve dağıtılacağı konusunda odaklanılmıştır. Ancak bazı yaygın senaryolarda, bir bırakma klasöründeki derlemelerin listesinden dağıttığınız kaynakları seçmek isteyeceksiniz. Diğer bir deyişle, en son derleme dağıtmak istediğiniz derleme olmayabilir.

[Dağıtımı destekleyen bir yapı tanımı oluşturarak](creating-a-build-definition-that-supports-deployment.md)önceki konuda açıklanan sürekli TÜMLEŞTIRME (CI) senaryosunu göz önünde bulundurun. Team Foundation Server (TFS) 2010 ' de bir derleme tanımı oluşturdunuz. Bir geliştirici TFS 'ye kod denetlediğinde, takım derlemesi kodunuzu derler, derleme sürecinin bir parçası olarak Web paketleri ve veritabanı betikleri oluşturur, tüm birim testlerini çalıştırır ve kaynaklarınızı bir test ortamına dağıtır. Yapı tanımını oluştururken yapılandırdığınız bekletme ilkesine bağlı olarak, TFS belirli sayıda önceki yapıyı tutar.

![](deploying-a-specific-build/_static/image1.png)

Şimdi, test ortamınızda bu derlemelerin birine karşı doğrulama ve doğrulama testi gerçekleştirdiğinizi ve uygulamanızı hazırlama ortamına dağıtmaya hazır olduğunuzu varsayalım. Bu sırada, geliştiriciler yeni kodu iade edebilir. Çözümü yeniden oluşturmak ve hazırlama ortamına dağıtmak istemezsiniz ve en son derlemeyi hazırlama ortamına dağıtmak istemezsiniz. Bunun yerine, doğrulama ve doğrulama yaptığınız belirli derlemeyi test sunucularında dağıtmak istiyorsunuz.

Bunu gerçekleştirmek için, belirli bir derlemeyi oluşturan Web paketlerinin ve veritabanı betiklerinin Microsoft Build Engine (MSBuild) nerede bulunacağını söylemeniz gerekir.

## <a name="overriding-the-outputroot-property"></a>OutputRoot özelliğini geçersiz kılma

[Örnek çözümde](../web-deployment-in-the-enterprise/the-contact-manager-solution.md), *Publish. proj* dosyası **outputroot**adlı bir özellik bildirir. Adından da anlaşılacağı gibi, bu, yapı sürecinin ürettiği her şeyi içeren kök klasördür. *Publish. proj* dosyasında, **outputroot** özelliğinin tüm dağıtım kaynakları için kök konuma başvurduğunu görebilirsiniz.

> [!NOTE]
> **Outputroot** , yaygın olarak kullanılan bir özellik adıdır. Görsel C# ve Visual Basic proje dosyaları ayrıca bu özelliği tüm derleme çıktıları için kök konumu depolamak üzere bildirir.

[!code-xml[Main](deploying-a-specific-build/samples/sample1.xml)]

Proje dosyanızın, önceki bir TFS derlemesinin&#x2014;&#x2014;çıkışları gibi farklı bir konumdan Web paketleri ve veritabanı betikleri dağıtmasını Istiyorsanız, yalnızca **outputroot** özelliğini geçersiz kılmanız gerekir. Özellik değerini, ekip oluşturma sunucusunda ilgili derleme klasörü olarak ayarlamanız gerekir. Komut satırından MSBuild çalıştırıyorsanız, bir komut satırı bağımsız değişkeni olarak **Outputroot** için bir değer belirtebilirsiniz:

[!code-console[Main](deploying-a-specific-build/samples/sample2.cmd)]

Ancak uygulamada, derleme hedefini kullanmayı planlamıyorsanız, çözüm oluşturma konusunda hiçbir nokta olmadığı&#x2014;için de derleme hedefini atlamak isteyeceksiniz. Bunu, komut satırından yürütmek istediğiniz hedefleri belirterek yapabilirsiniz:

[!code-console[Main](deploying-a-specific-build/samples/sample3.cmd)]

Ancak çoğu durumda, dağıtım mantığınızı bir TFS derleme tanımına derlemek isteyeceksiniz. Bu sayede, bir Visual Studio yüklemesinden dağıtımı, TFS sunucusuyla bir bağlantıyla tetiklemeye yönelik Kullanıcı **kuyruğu** oluşturma izni sağlanır.

## <a name="creating-a-build-definition-to-deploy-specific-builds"></a>Belirli derlemeleri dağıtmak için derleme tanımı oluşturma

Sonraki yordamda, kullanıcıların tek bir komutla hazırlama ortamına dağıtımları tetiklemesine olanak tanıyan bir yapı tanımının nasıl oluşturulacağı açıklanmaktadır.

Bu durumda, derleme tanımının özel proje dosyanızda dağıtım mantığını yürütmek istediğiniz her şeyi&#x2014;gerçekten oluşturmasını istemezsiniz. *Publish. proj* dosyası, dosya takım derlemesinde çalışıyorsa **derleme** hedefini atlayan koşullu mantığı içerir. Bunu, takım derlemesinde proje dosyanızı çalıştırırsanız otomatik olarak **true** olarak ayarlanan yerleşik **Buildinginteambuild** özelliğini değerlendirerek yapar. Sonuç olarak, yapı sürecini atlayabilir ve var olan bir derlemeyi dağıtmak için proje dosyasını çalıştırmanız yeterlidir.

**Dağıtımı el ile tetiklemek üzere bir yapı tanımı oluşturmak için**

1. Visual Studio 2010 ' de, **Takım Gezgini** penceresinde, takım projesi düğümünüz ' ı genişletin, **yapılar**' a sağ tıklayın ve ardından **Yeni derleme tanımı**' na tıklayın.

    ![](deploying-a-specific-build/_static/image2.png)
2. **Genel** sekmesinde, derleme tanımına bir ad (örneğin, **deploytohazırlama**) ve isteğe bağlı bir açıklama verin.
3. **Tetikleyici** sekmesinde **el ile-iadeler ' ı seçerek yeni bir derlemeyi tetiklemeyin**.
4. **Derleme Varsayılanları** sekmesinde, **derleme çıkışını aşağıdaki bırakma klasörüne kopyala** kutusuna bırakma klasörünüzün evrensel adlandırma kuralı (UNC) yolunu yazın (örneğin, **tfsbuild\bırakı\\** ).

    ![](deploying-a-specific-build/_static/image3.png)
5. **İşlem** sekmesinde, **işlem dosyası oluştur** açılır listesinde **DefaultTemplate. xaml** ' i seçili bırakın. Bu, tüm yeni takım projelerine eklenen varsayılan yapı işlem şablonlarından biridir.
6. **Yapı işlemi parametreleri** tablosunda, oluşturulacak **öğeler** satırına tıklayın ve ardından **üç nokta** düğmesine tıklayın.

    ![](deploying-a-specific-build/_static/image4.png)
7. **Derlenecek Öğeler** Iletişim kutusunda **Ekle**' ye tıklayın.
8. **Tür öğeleri** açılan listesinde **MSBuild proje dosyaları**' nı seçin.
9. Dağıtım işlemini denetlediğiniz özel proje dosyasının konumuna gidin, dosyayı seçin ve ardından **Tamam**' a tıklayın.

    ![](deploying-a-specific-build/_static/image5.png)
10. **Derlenecek Öğeler** Iletişim kutusunda **Tamam**' a tıklayın.
11. **Yapı işlemi parametreleri** tablosunda, **Gelişmiş** bölümünü genişletin.
12. **MSBuild bağımsız değişkenleri** satırında, ortama özgü proje dosyanızın konumunu belirtin ve yapı klasörünüzün konumu için bir yer tutucu ekleyin:

    [!code-console[Main](deploying-a-specific-build/samples/sample4.cmd)]

    ![](deploying-a-specific-build/_static/image6.png)

    > [!NOTE]
    > Bir derlemeyi her sıraışınızda **Outputroot** değerini geçersiz kılmanız gerekir. Bu, sonraki yordamda ele alınmıştır.
13. **Kaydet**'e tıklayın.

Bir derlemeyi tetiklemeniz durumunda, **Outputroot** özelliğini, dağıtmak istediğiniz yapıya işaret etmek için güncelleştirmeniz gerekir.

**Belirli bir derlemeyi bir yapı tanımından dağıtmak için**

1. **Takım Gezgini** penceresinde, derleme tanımına sağ tıklayın ve sonra **yeni derlemeyi kuyruğa al**' a tıklayın.

    ![](deploying-a-specific-build/_static/image7.png)
2. **Derlemeyi kuyruğa al** iletişim kutusunda, **Parametreler** sekmesinde, **Gelişmiş** bölümünü genişletin.
3. **MSBuild bağımsız değişkenleri** satırında, **outputroot** özelliğinin değerini yapı klasörünüzün konumuyla değiştirin. Örneğin:

    [!code-console[Main](deploying-a-specific-build/samples/sample5.cmd)]

    ![](deploying-a-specific-build/_static/image8.png)

    > [!NOTE]
    > Yapı klasörünüzün yolunun sonuna bir eğik çizgi eklediğinizden emin olun.
4. **Kuyruk**' a tıklayın.

Derlemeyi kuyruğa aldığınızda proje dosyası, **Outputroot** özelliğinde belirttiğiniz yapı bırakma klasöründen veritabanı betikleri ve Web paketleri dağıtır.

## <a name="conclusion"></a>Sonuç

Bu konuda, bölünmüş proje dosyası dağıtım modelini kullanarak belirli bir önceki derlemeden Web paketleri ve veritabanı betikleri gibi dağıtım kaynaklarının nasıl yayımlanacağı açıklanmaktadır. **Outputroot** özelliğinin nasıl geçersiz kılınacağını ve dağıtım MANTıĞıNıN bir TFS derleme tanımına nasıl ekleneceğini açıklandı.

## <a name="further-reading"></a>Daha Fazla Bilgi

Derleme tanımları oluşturma hakkında daha fazla bilgi için bkz. [temel yapı tanımı oluşturma](https://msdn.microsoft.com/library/ms181716.aspx) ve [derleme işleminizi tanımlama](https://msdn.microsoft.com/library/ms181715.aspx). Yapıları sıraya alma hakkında daha fazla bilgi için bkz. [bir derlemeyi sıraya](https://msdn.microsoft.com/library/ms181722.aspx)alma.

> [!div class="step-by-step"]
> [Önceki](creating-a-build-definition-that-supports-deployment.md)
> [İleri](configuring-permissions-for-team-build-deployment.md)
