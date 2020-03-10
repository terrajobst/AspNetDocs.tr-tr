---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
title: Dağıtımı destekleyen bir derleme tanımı oluşturma | Microsoft Docs
author: jrjlee
description: Team Foundation Server (TFS) 2010 ' de herhangi bir tür derlemeyi gerçekleştirmek istiyorsanız, takım projeniz içinde bir yapı tanımı oluşturmanız gerekir. Bu konu,...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: fe47a018-f6d0-4979-80e7-5b1fa75a5865
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
msc.type: authoredcontent
ms.openlocfilehash: e11c91a824446572aaf0b3bc6954b9b8ffb4eaff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78604001"
---
# <a name="creating-a-build-definition-that-supports-deployment"></a>Dağıtımı Destekleyen Bir Derleme Tanımı Oluşturma

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Team Foundation Server (TFS) 2010 ' de herhangi bir tür derlemeyi gerçekleştirmek istiyorsanız, takım projeniz içinde bir yapı tanımı oluşturmanız gerekir. Bu konu, TFS 'de yeni bir derleme tanımı oluşturmayı ve takım derlemesi içindeki derleme işleminin bir parçası olarak Web dağıtımını denetlemeyi açıklar.

Bu konu, Fabrikam, Inc adlı kurgusal bir şirketin Kurumsal Dağıtım gereksinimlerini temel alarak bir öğretici serisinin bir parçasını oluşturur. Bu öğretici serisi, bir ASP.NET MVC&#x2014;3 uygulaması, Windows Communication Foundation (WCF) hizmeti ve bir veritabanı projesi dahil, gerçekçi bir karmaşıklık düzeyine sahip bir Web uygulamasını temsil etmek üzere bir örnek çözüm olan [Contact Manager çözümünü](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;kullanır.

Bu öğreticilerin temelini oluşturan dağıtım yöntemi, derleme ve dağıtım sürecinin, her hedef ortam için uygulanan derleme yönergelerini içeren iki proje&#x2014;dosyası tarafından denetlendiği ve ortama özgü derleme ve dağıtım ayarlarını içeren, proje [dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md)bölümünde açıklanan bölünmüş proje dosyası yaklaşımını temel alır. Derleme zamanında, ortama özgü proje dosyası, derleme yönergelerinin tam bir kümesini oluşturmak için ortam agtik proje dosyası ile birleştirilir.

## <a name="task-overview"></a>Göreve genel bakış

Yapı tanımı, TFS 'deki takım projeleri için derlemelerin nasıl ve ne zaman gerçekleşeceğini denetleyen mekanizmadır. Her derleme tanımı şunları belirtir:

- Visual Studio çözüm dosyaları veya özel Microsoft Build Engine (MSBuild) proje dosyaları gibi derlemek istediğiniz şeyler.
- El ile Tetikleyiciler, sürekli tümleştirme (CI) veya geçişli iadeler gibi bir yapı ne zaman gerçekleşmesi gerektiğini belirleme ölçütleri.
- Ekip derlemesinin, Web paketleri ve veritabanı betikleri gibi dağıtım yapıtları dahil olmak üzere derleme çıktıları göndereceği konum.
- Her bir yapılandırmanın korunması gereken süre miktarı.
- Yapı sürecinin diğer çeşitli parametreleri.

> [!NOTE]
> Derleme tanımları hakkında daha fazla bilgi için bkz. [Yapı Işleminizi tanımlama](https://msdn.microsoft.com/library/ms181715.aspx).

Bu konuda, bir geliştirici yeni içerikte denetlediğinde bir derlemeyi tetiklenmesi için CI kullanan bir yapı tanımı oluşturma işlemi gösterilir. Oluşturma işlemi başarılı olursa, yapı hizmeti çözümü bir test ortamına dağıtmak için özel bir proje dosyası çalıştırır.

Bir derlemeyi tetiklemeniz durumunda, bu eylemlerin olması gerekir:

- İlk olarak, takım derlemesinin çözümü oluşturması gerekir. Bu işlemin bir parçası olarak, takım derlemesi, çözümdeki Web uygulaması projelerinin her biri için Web dağıtım paketleri oluşturmak üzere Web yayımlama işlem hattını (WPP) çağırır. Ekip derlemesi, Çözümle ilişkili tüm birim testlerini de çalıştırır.
- Çözüm derlemesi başarısız olursa, takım derlemesinin başka bir eylem yapması gerekmez. Birim testi hataları derleme hatası olarak değerlendirilmelidir.
- Çözüm derlemesi başarılı olursa, takım derlemesi çözümün dağıtımını denetleyen özel proje dosyasını çalıştırmalıdır. Bu işlemin bir parçası olarak, takım derlemesi paketlenmiş Web uygulamalarını hedef Web sunucularına yüklemek için Internet Information Services (IIS) Web Dağıtım aracı 'nı (Web Dağıtımı) çağırır ve veritabanı oluşturmayı çalıştırmak için VSDBCMD. exe yardımcı programını çağıracaktır hedef veritabanı sunucularındaki betikler.

Bu işlem gösterilmektedir:

![](creating-a-build-definition-that-supports-deployment/_static/image1.png)

[Ilgili kişi Yöneticisi](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) örnek çözümü, MSBuild veya takım derlemesi 'nden çalıştırabileceğiniz, *Publish. proj*adlı özel bir MSBuild proje dosyası içerir. Bu proje dosyası, [Yapı sürecini anlama](../web-deployment-in-the-enterprise/understanding-the-build-process.md)bölümünde açıklandığı gibi, Web paketlerinizi ve veritabanlarınızı bir hedef ortama dağıtan mantığı tanımlar. Dosya, ekip derlemesinde çalışıyorsa yalnızca dağıtım görevlerinin çalıştırılmasını terk eden oluşturma ve paketleme sürecini atlalayan mantığı içerir. Bunun nedeni, dağıtımı bu şekilde otomatikleştirdiğiniz için genellikle çözümün başarıyla oluşturulduğundan ve dağıtım işlemi yapılmadan önce herhangi bir birim testini geçirdiğinden emin olmak isteyeceksiniz.

Sonraki bölümde, yeni bir derleme tanımı oluşturarak bu işlemin nasıl uygulanacağı açıklanmaktadır.

> [!NOTE]
> Tek bir&#x2014;otomatik işlemin bir çözüm&#x2014;derlemesi, testleri ve dağıttığı bu yordam, test ortamlarına dağıtıma en uygun olasılıktır. Hazırlama ve üretim ortamları için bir test ortamında önceden doğrulamış ve doğruladığınız önceki bir derlemeden içerik dağıtmak istemeniz çok daha olasıdır. Bu yaklaşım, [belirli bir derlemeyi dağıtmaya yönelik bir](deploying-a-specific-build.md)sonraki konu başlığında açıklanmıştır.

### <a name="who-performs-this-procedure"></a>Bu yordamı kim gerçekleştiriyor?

Genellikle, bir TFS Yöneticisi bu yordamı gerçekleştirir. Bazı durumlarda, bir geliştirici ekibi lideri TFS 'deki takım projesi koleksiyonu için sorumluluk alabilir. Yeni bir derleme tanımı oluşturmak için çözümünüzü içeren takım projesi koleksiyonu için **proje koleksiyonu derleme yöneticileri** grubunun bir üyesi olmanız gerekir.

## <a name="create-a-build-definition-for-ci-and-deployment"></a>CI ve dağıtım için derleme tanımı oluşturma

Sonraki yordamda, CI 'nin tetiklediği derleme tanımının nasıl oluşturulacağı açıklanmaktadır. Yapı başarılı olursa çözüm, özel bir MSBuild proje dosyasındaki mantığı kullanılarak dağıtılır.

**CI ve dağıtım için bir derleme tanımı oluşturmak için**

1. Visual Studio 2010 ' de, **Takım Gezgini** penceresinde, takım projesi düğümünüz ' ı genişletin, **yapılar**' a sağ tıklayın ve ardından **Yeni derleme tanımı**' na tıklayın.

    ![](creating-a-build-definition-that-supports-deployment/_static/image2.png)
2. **Genel** sekmesinde, derleme tanımına bir ad (örneğin, **deploytotest**) ve isteğe bağlı bir açıklama verin.
3. **Tetikleyici** sekmesinde, yeni bir derlemeyi tetiklemek istediğiniz ölçütü seçin. Örneğin, çözümü derlemek ve bir geliştirici yeni kodu her denetlediğinde test ortamına dağıtmak istiyorsanız **sürekli tümleştirme**' i seçin.
4. **Derleme Varsayılanları** sekmesinde, **derleme çıkışını aşağıdaki bırakma klasörüne kopyala** kutusuna bırakma klasörünüzün evrensel adlandırma kuralı (UNC) yolunu yazın (örneğin, **tfsbuild\bırakı\\** ).

    ![](creating-a-build-definition-that-supports-deployment/_static/image3.png)

    > [!NOTE]
    > Bu bırakma konumu, yapılandırdığınız bekletme ilkesine bağlı olarak çeşitli derlemeler depolar. Belirli bir derlemeden hazırlama veya üretim ortamına dağıtım yapıtları yayınlamak istediğinizde, burada bulabilirsiniz.
5. **İşlem** sekmesinde, **işlem dosyası oluştur** açılır listesinde **DefaultTemplate. xaml** ' i seçili bırakın. Bu, tüm yeni takım projelerine eklenen varsayılan yapı işlem şablonlarından biridir.
6. **Yapı işlemi parametreleri** tablosunda, oluşturulacak **öğeler** satırına tıklayın ve ardından **üç nokta** düğmesine tıklayın.

    ![](creating-a-build-definition-that-supports-deployment/_static/image4.png)
7. **Derlenecek Öğeler** Iletişim kutusunda **Ekle**' ye tıklayın.
8. Çözüm dosyanızın konumuna gidin ve ardından **Tamam**' a tıklayın.

    ![](creating-a-build-definition-that-supports-deployment/_static/image5.png)
9. **Derlenecek Öğeler** Iletişim kutusunda **Ekle**' ye tıklayın.
10. **Tür öğeleri** açılan listesinde **MSBuild proje dosyaları**' nı seçin.
11. Dağıtım işlemini denetlediğiniz özel proje dosyasının konumuna gidin, dosyayı seçin ve ardından **Tamam**' a tıklayın.

    ![](creating-a-build-definition-that-supports-deployment/_static/image6.png)
12. **Oluşturulacak öğeler** iletişim kutusunda artık iki öğe gösterilmelidir. **Tamam**’a tıklayın.

    ![](creating-a-build-definition-that-supports-deployment/_static/image7.png)
13. **İşlem** sekmesinde, **Yapı işlemi parametreleri** tablosunda, **Gelişmiş** bölümünü genişletin.
14. **MSBuild bağımsız değişkenleri** satırında, oluşturulacak öğelerinizin *her biri için gereken MSBuild* komut satırı bağımsız değişkenlerini ekleyin. Contact Manager çözüm senaryosunda, bu bağımsız değişkenler gereklidir:

    [!code-console[Main](creating-a-build-definition-that-supports-deployment/samples/sample1.cmd)]

    ![](creating-a-build-definition-that-supports-deployment/_static/image8.png)
15. Bu örnekte:

    1. Contact Manager çözümünü oluştururken **Deployonbuild = true** ve **deploytarget = paket** bağımsız değişkenleri gereklidir. Bu, Web [uygulaması projelerini oluşturma ve paketleme](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)bölümünde açıklandığı gibi, her bir Web uygulaması projesini derlemeden sonra Web dağıtım paketleri oluşturmayı MSBuild 'e söyler.
    2. *Publish. proj* dosyasını oluşturduğunuzda **Targetenvpropsfile** bağımsız değişkeni gereklidir. Bu özellik, [Yapı sürecini anlama](../web-deployment-in-the-enterprise/understanding-the-build-process.md)bölümünde açıklandığı gibi ortama özgü yapılandırma dosyasının konumunu gösterir.
16. **Bekletme ilkesi** sekmesinde, her bir türün kaç tane türünü gerektiği şekilde saklamak istediğinizi yapılandırın.
17. **Kaydet**'e tıklayın.

## <a name="queue-a-build"></a>Bir Derlemeyi Sıraya Koyma

Bu noktada, en az bir yeni derleme tanımı oluşturdunuz. Tanımladığınız derleme işlemi artık derleme tanımında belirttiğiniz tetikleyicilere göre çalışacaktır.

Derleme tanımınızı CI kullanacak şekilde yapılandırdıysanız, derleme tanımınızı iki şekilde test edebilirsiniz:

- Bir otomatik derlemeyi tetiklemek için takım projesine bazı içerikleri iade edin.
- Derlemeyi el ile sıraya koyun.

**Bir derlemeyi el ile sıraya alma**

1. **Takım Gezgini** penceresinde, derleme tanımına sağ tıklayın ve sonra **yeni derlemeyi kuyruğa al**' a tıklayın.

    ![](creating-a-build-definition-that-supports-deployment/_static/image9.png)
2. **Derlemeyi kuyruğa al** iletişim kutusunda derleme özelliklerini gözden geçirin ve ardından **kuyruk**' ı tıklatın.

    ![](creating-a-build-definition-that-supports-deployment/_static/image10.png)

Bir derlemeyi el ile mi tetiklediğini ne olursa olsun&#x2014;, bir derleme sonucunu gözden geçirmek için **Takım Gezgini** penceresinde&#x2014;yapı tanımına otomatik olarak çift tıklayın. Bu, bir **Yapı Gezgini** sekmesi açar.

![](creating-a-build-definition-that-supports-deployment/_static/image11.png)

Buradan başarısız olan derlemelerin sorunlarını giderebilirsiniz. Tek bir yapıya çift tıklarsanız Özet bilgilerini görüntüleyebilir ve ayrıntılı günlük dosyalarına tıklayabilirsiniz.

![](creating-a-build-definition-that-supports-deployment/_static/image12.png)

Bu bilgileri, başka bir derlemeyi denemeden önce başarısız yapıların sorunlarını gidermek ve sorunları gidermek için kullanabilirsiniz.

> [!NOTE]
> Dağıtım mantığını çalıştıran derlemeler, yapı sunucusuna hedef ortamda gerekli izinleri verene kadar başarısız olabilir. Daha fazla bilgi için bkz. [Takım derleme dağıtımı Için Izinleri yapılandırma](configuring-permissions-for-team-build-deployment.md).

## <a name="monitor-the-build-process"></a>Yapı Işlemini izleme

TFS, yapı sürecini izlemenize yardımcı olacak çok çeşitli işlevler sağlar. Örneğin, TFS size bir e-posta gönderebilir veya bir derleme tamamlandığında görev çubuğu bildirim alanında uyarılar görüntüleyebilir. Daha fazla bilgi için bkz. [derlemeleri çalıştırma ve izleme](https://msdn.microsoft.com/library/ms181721.aspx).

## <a name="conclusion"></a>Sonuç

Bu konu, TFS 'de bir derleme tanımının nasıl oluşturulacağını açıklamaktadır. Derleme tanımı CI için yapılandırılmıştır, bu nedenle derleme işlemi bir geliştirici takım projesine içerik iade ettiğinde çalışır. Derleme tanımı, Web paketleri ve veritabanı betikleri için bir hedef sunucu ortamına dağıtmak üzere özel bir MSBuild proje dosyası yürütür.

Otomatik dağıtımın bir yapı sürecinin bir parçası olarak başarılı olması için, hedef Web sunucularındaki ve hedef veritabanı sunucusundaki yapı hizmeti hesabına uygun izinleri vermeniz gerekir. Bu öğreticideki son konu, [ekip derleme dağıtımı Için Izinleri yapılandırırken](configuring-permissions-for-team-build-deployment.md), bir Team Build Server 'dan otomatik dağıtım için gerekli izinlerin nasıl belirleneceğini ve yapılandırılacağını açıklar.

## <a name="further-reading"></a>Daha Fazla Bilgi

Derleme tanımları oluşturma hakkında daha fazla bilgi için bkz. [temel yapı tanımı oluşturma](https://msdn.microsoft.com/library/ms181716.aspx) ve [derleme işleminizi tanımlama](https://msdn.microsoft.com/library/ms181715.aspx). Yapıları sıraya alma hakkında daha fazla bilgi için bkz. [bir derlemeyi sıraya](https://msdn.microsoft.com/library/ms181722.aspx)alma.

> [!div class="step-by-step"]
> [Önceki](configuring-a-tfs-build-server-for-web-deployment.md)
> [İleri](deploying-a-specific-build.md)
