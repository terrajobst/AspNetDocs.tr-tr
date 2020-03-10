---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
title: Web dağıtımı için TFS derleme sunucusunu yapılandırma | Microsoft Docs
author: jrjlee
description: Bu konu başlığı altında, takım derlemesi ve Internet ınformat kullanarak çözümlerinizi derlemek ve dağıtmak için bir Team Foundation Server (TFS) derleme sunucusunun nasıl hazırlanacağı açıklanmaktadır...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f8400241-4f4b-4bbd-9994-54fb64909e6e
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: b3aaf7234706d149a3c784347528923f662c3511
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78631098"
---
# <a name="configuring-a-tfs-build-server-for-web-deployment"></a>Bir TFS Derleme Sunucusunu Web Dağıtımı için Yapılandırma

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konuda, ekip oluşturma ve Internet Information Services (IIS) Web Dağıtım Aracı (Web Dağıtımı) kullanarak çözümlerinizi derlemek ve dağıtmak için bir Team Foundation Server (TFS) derleme sunucusunun nasıl hazırlanacağı açıklanmaktadır.

Bu konu, Fabrikam, Inc adlı kurgusal bir şirketin Kurumsal Dağıtım gereksinimlerini temel alarak bir öğretici serisinin bir parçasını oluşturur. Bu öğretici serisi, bir ASP.NET MVC&#x2014;3 uygulaması, Windows Communication Foundation (WCF) hizmeti ve bir veritabanı projesi dahil, gerçekçi bir karmaşıklık düzeyine sahip bir Web uygulamasını temsil etmek üzere bir örnek çözüm olan [Contact Manager çözümünü](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;kullanır.

Bu öğreticilerin temelini oluşturan dağıtım yöntemi, derleme işleminin her hedef ortam için uygulanan derleme yönergelerini içeren ve ortama özel yapı ve dağıtım ayarlarını içeren iki proje&#x2014;dosyası tarafından kontrol edilen proje [dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md)bölümünde açıklanan bölünmüş proje dosyası yaklaşımını temel alır. Derleme zamanında, ortama özgü proje dosyası, derleme yönergelerinin tam bir kümesini oluşturmak için ortam agtik proje dosyası ile birleştirilir.

## <a name="task-overview"></a>Göreve genel bakış

Çözümünüzü derlemek ve dağıtmak üzere bir yapı sunucusu hazırlamak için şunları yapmanız gerekir:

- TFS Build Service 'i yükleyip yapılandırın.
- Visual Studio 2010 ' i yükler.
- Çözümünüzü derlemek için gereken tüm ürünleri veya bileşenleri, .NET Framework veya ASP.NET MVC sürümleri gibi yükler.
- Web Dağıtımı 2,0 veya üstünü yükler.

Bu konu başlığı altında, bu yordamları nasıl gerçekleştireceğiniz veya var oldukları diğer kaynaklara işaret eden yönergeler gösterilecektir. Bu konudaki görevler ve izlenecek yollar şu şekilde kabul eder:

- Windows Server 2008 R2 Service Pack 1 çalıştıran bir temiz sunucu derlemesi ile başlıyoruz.
- Sunucu, bir statik IP adresi ile etki alanına katılmış.
- TFS uygulama katmanını, Kurumsal Web dağıtımı ' nda açıklandığı gibi ayrı bir sunucuya yüklediniz [: senaryoya genel bakış](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md).

### <a name="who-performs-these-procedures"></a>Bu yordamları kim gerçekleştiriyor?

Çoğu durumda, yapı sunucularını yapılandırmadan bir TFS Yöneticisi sorumlu olacaktır. Bazı durumlarda, geliştirici ekibi belirli yapı sunucularının sahipliğini alabilir.

## <a name="install-and-configure-the-tfs-build-service"></a>TFS Build Service 'i yükleyip yapılandırma

Bir yapı sunucusu yapılandırdığınızda, ilk göreviniz TFS derleme hizmetini yüklemek ve yapılandırmak olur. Bu işlemin bir parçası olarak şunları yapmanız gerekir:

- TFS derleme hizmetini yükleyip bir hizmet hesabı yapılandırın. Dağıtım dahil olmak üzere tüm derleme görevleri, yapı hizmeti hesabının kimliği kullanılarak çalıştırılır.
- Bir *Yapı denetleyicisi* ve bir veya daha fazla *Yapı Aracısı*oluşturun. Her yapı denetleyicisi bir yapı Aracısı kümesini yönetir. Bir derlemeyi kuyruğa aldığınızda, yapı denetleyicisi derleme görevini kullanılabilir bir yapı aracısına atar. TFS 'deki her takım projesi koleksiyonu, tek bir yapı denetleyicisi ile eşleştirilir.
- Derleme çıktılarınız için bir bırakma klasörü yapılandırın. Bu bir ağ paylaşımıdır. Web dağıtım paketleri gibi tüm derleme çıktıları bırakma klasörüne gönderilir.

MSDN üzerinde [Team Foundation Build 'ı yönetme](https://msdn.microsoft.com/library/ms252495.aspx) bölümü, bu görevleri gerçekleştirmek için ihtiyacınız olan tüm kaynakları içerir:

- Yapı Hizmeti, yapı denetleyicileri ve yapı aracıları dahil olmak üzere Team Foundation derlemesi 'ne kavramsal bir genel bakış için bkz. [Team Foundation yapı sistemini anlama](https://msdn.microsoft.com/library/dd793166.aspx).
- Yapı hizmetini yükleme ve yapılandırma hakkında daha fazla bilgi için bkz. [yapı makinesini yapılandırma](https://msdn.microsoft.com/library/ms181712.aspx).
- Derleme denetleyicileri oluşturma hakkında bilgi için bkz. [oluşturma ve derleme denetleyicisi Ile çalışma](https://msdn.microsoft.com/library/ee330987.aspx).
- Derleme aracıları oluşturma hakkında bilgi için bkz. [oluşturma ve derleme aracıları Ile çalışma](https://msdn.microsoft.com/library/bb399135.aspx).
- Bırakma klasörleri oluşturma ve yapılandırma hakkında bilgi için bkz. [bırakma klasörlerini ayarlama](https://msdn.microsoft.com/library/bb778394.aspx).

## <a name="install-required-products-and-components"></a>Gerekli ürünleri ve bileşenleri yükler

Çözümlerinizi derlemek için yapı sunucusunu etkinleştirmek üzere çözümünüzün gerektirdiği tüm ürünleri, bileşenleri veya derlemeleri yüklemelisiniz. Herhangi bir Web platformu bileşenini yüklemeden önce, derleme sunucusuna Visual Studio 2010 (herhangi bir sürüm) yüklemelisiniz. Bu, çekirdek Microsoft Build Engine (MSBuild) hedef dosyalarının ve Web yayımlama işlem hattı (WPP) hedef dosyalarının derleme hizmeti tarafından kullanılabilmesini sağlar. Visual Studio yükleyicisi Ayrıca, derleme işleminizin bir parçası olarak Web paketleri dağıtmayı planlıyorsanız, gereken Web Dağıtımı de yüklemelidir.

Ortak Web Platformu bileşenlerini yüklemenin en iyi yolu [Web Platformu Yükleyicisi](https://go.microsoft.com/?linkid=9805118)'ni kullanmaktır. Bu, her bir ürünün en son sürümünü yüklemenizi sağlar ve ayrıca her ürün için önkoşulları otomatik olarak algılar ve kurar. [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) çözümü söz konusu olduğunda, bu ürünleri ve bileşenleri yüklemek Için Web Platformu Yükleyicisi ' ni kullanmanız gerekir:

- **.NET Framework 4,0**. Bu, .NET Framework bu sürümünde oluşturulan uygulamaları çalıştırmak için gereklidir.
- **Web dağıtımı aracı 2,1 veya sonraki bir sürümü**. Bu, sunucunuza Web Dağıtımı (ve temel alınan yürütülebilir dosyası, MSDeploy. exe) yüklenir. Bu işlemin bir parçası olarak Web Deployment Agent hizmetini yükleyip başlatır. Bu hizmet, uzak bir bilgisayardan Web paketleri dağıtmanızı sağlar.
- **ASP.NET MVC 3**. Bu, ASP.NET MVC 3 uygulamalarını çalıştırmak için gereken derlemeleri kurar.

**Gerekli ürünleri ve bileşenleri yüklemek için**

1. Visual Studio 2010 ' i yükler. Yüklenecek özellikleri seçmeniz istendiğinde şunları dahil etmelisiniz:

    1. Derlemek için gereken programlama dilleri.
    2. Visual Web Developer. Bu, WPP hedeflerinin derleme sunucunuza eklenmesini sağlar.

        ![](configuring-a-tfs-build-server-for-web-deployment/_static/image1.png)
2. Visual Studio 2010 yüklemesi tamamlandığında, [Visual studio 2010 Service Pack 1](https://go.microsoft.com/?linkid=9805133) ' i indirip yükleyin (yükleme medyanıza henüz eklenmadıysanız).

    > [!NOTE]
    > Visual Studio 2010 Service Pack 1, MSBuild 'in MSDeploy yürütülebiliri bulmasını engelleyebilen bir hata çözer.
3. [Web platformu yükleyicisini](https://go.microsoft.com/?linkid=9805118)indirip başlatın.
4. **Web platformu yükleyicisi 3,0** penceresinin en üstünde, **Ürünler**' e tıklayın.
5. Pencerenin sol tarafında, gezinti bölmesinde, **çerçeveler**' e tıklayın.
6. **Microsoft .NET Framework 4** satırında, .NET Framework zaten yüklenmemişse **Ekle**' ye tıklayın.

    > [!NOTE]
    > .NET Framework 4,0 ' i Windows Update aracılığıyla zaten yüklemiş olabilirsiniz. Bir ürün veya bileşen zaten yüklüyse, Web Platformu Yükleyicisi, **Ekle** düğmesini **yüklü**olan metinle değiştirerek bunu gösterir.

    ![](configuring-a-tfs-build-server-for-web-deployment/_static/image2.png)
7. **ASP.NET MVC 3 (Visual Studio 2010)** satırında **Ekle**' ye tıklayın.
8. Gezinti bölmesinde **sunucu**' ya tıklayın.
9. **Web Dağıtım aracı 2,1** satırında **Ekle**' ye tıklayın.
10. **Yükle**'ye tıklatın. Web Platformu yükleyicisi ürünleri &#x2014; herhangi bir ilişkili bağımlılıkları &#x2014; yüklenecek birlikte listesini gösterir ve lisans koşullarını kabul isteyip istemediğinizi sorar.
11. Lisans koşullarını gözden geçirin ve koşulları **onayladıysanız kabul ediyorum**' a tıklayın.
12. Yükleme tamamlandığında, **son**' a tıklayın ve ardından **Web Platformu Yükleyicisi 3,0** penceresini kapatın.

> [!NOTE]
> Dağıtım işleminiz VSDBCMD. exe veya SQLCMD. exe gibi araçların kullanımını içeriyorsa, bunların derleme sunucunuzda yüklü olduğundan emin olmanız gerekir. VSDBCMD. exe bir Visual Studio aracıdır ve genellikle Team Foundation Build yüklediğinizde sunucuya eklenir. SQLCMD. exe bir SQL Server aracıdır. SQLCMD. exe ' nin tek başına bir sürümünü [Microsoft SQL Server 2008 R2 özellik paketi](https://go.microsoft.com/?linkid=9805134) sayfasından indirebilirsiniz.

## <a name="conclusion"></a>Sonuç

Bu noktada, derleme sunucunuz Web uygulaması projelerinizi oluşturmaya ve dağıtmaya başlamaya hazırlanmaya başladı. Bir sonraki konu, [dağıtımı destekleyen bir yapı tanımı oluşturmak](creating-a-build-definition-that-supports-deployment.md)için, projelerinizin ne zaman ve nasıl dağıtıldığını denetlemek için bir derleme tanımının nasıl oluşturulup yapılandırılacağını açıklar.

## <a name="further-reading"></a>Daha Fazla Bilgi

Takım derlemesi ile çalışma hakkında daha genel rehberlik için bkz. [Team Foundation Build 'ı yönetme](https://msdn.microsoft.com/library/ms252495.aspx).

> [!div class="step-by-step"]
> [Önceki](adding-content-to-source-control.md)
> [İleri](creating-a-build-definition-that-supports-deployment.md)
