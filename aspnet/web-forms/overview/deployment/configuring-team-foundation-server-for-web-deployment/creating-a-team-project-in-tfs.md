---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
title: TFS 'de bir takım projesi oluşturma | Microsoft Docs
author: jrjlee
description: Bu konu, Team Foundation Server (TFS) 2010 ' de yeni bir takım projesi oluşturmayı açıklar.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b28d3e2d-0bb4-4e29-a780-af810b964722
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
msc.type: authoredcontent
ms.openlocfilehash: d12e0636ce3b6239d125305db4354278f9f24960
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639659"
---
# <a name="creating-a-team-project-in-tfs"></a>TFS’de Takım Projesi Oluşturma

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konu, Team Foundation Server (TFS) 2010 ' de yeni bir takım projesi oluşturmayı açıklar.

Bu konu, Fabrikam, Inc adlı kurgusal bir şirketin Kurumsal Dağıtım gereksinimlerini temel alarak bir öğretici serisinin bir parçasını oluşturur. Bu öğretici serisi, bir ASP.NET MVC&#x2014;3 uygulaması, Windows Communication Foundation (WCF) hizmeti ve bir veritabanı projesi dahil, gerçekçi bir karmaşıklık düzeyine sahip bir Web uygulamasını temsil etmek üzere bir örnek çözüm olan [Contact Manager çözümünü](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;kullanır.

## <a name="task-overview"></a>Göreve genel bakış

TFS 'de yeni bir takım projesi sağlamak ve kullanmak için, bu üst düzey adımları gerçekleştirmeniz gerekir:

- Yeni takım projesini oluşturacak kullanıcıya izin verin.
- Takım projesi oluşturun.
- Proje üzerinde çalışacak takım üyelerine izin verin.
- Bazı içerikleri iade edin.

Bu konu, bu yordamların nasıl gerçekleştirileceğini gösterir ve her yordamdan sorumlu olabilecek Kullanıcı ve iş rollerini belirler. Kuruluşunuzun yapısına bağlı olarak, bu görevlerin her biri farklı bir kişinin sorumluluğunda olabileceğini unutmayın.

Bu konudaki görevler ve izlenecek yollar, TFS 'yi yüklediğinizi ve yapılandırdığınızı ve yapılandırma sürecinin bir parçası olarak bir takım projesi koleksiyonu oluşturduğunuzu varsayar. Bu varsayımlar hakkında daha fazla bilgi edinmek ve senaryo hakkında daha genel arka plan bilgileri için bkz. [Web dağıtımı IÇIN TFS Build Server yapılandırma](configuring-a-tfs-build-server-for-web-deployment.md).

## <a name="grant-permissions-to-the-team-project-creator"></a>Takım projesi oluşturucusuna Izin verme

Yeni bir takım projesi oluşturmak için bu izinlere ihtiyacınız vardır:

- TFS uygulama katmanında **Yeni proje oluştur** izninizin olması gerekir. Bu izni genellikle **proje koleksiyonu yöneticileri** TFS grubuna kullanıcı ekleyerek verirsiniz. **Team Foundation yöneticileri** genel grubu da bu izni içerir.
- TFS takım projesi koleksiyonuna karşılık gelen SharePoint site koleksiyonu içinde yeni ekip siteleri oluşturmak için izninizin olması gerekir. Bu izni genellikle, kullanıcıyı SharePoint site koleksiyonunda **tam denetim** haklarına sahip bir SharePoint grubuna ekleyerek verirsiniz.
- SQL Server Reporting Services özellikler kullanıyorsanız, Raporlama Hizmetleri 'nde **Team Foundation Içerik Yöneticisi** rolünün bir üyesi olmanız gerekir.

### <a name="who-performs-these-procedures"></a>Bu yordamları kim gerçekleştiriyor?

Genellikle, TFS dağıtımını yöneten kişi veya grup bu yordamları da gerçekleştirir.

Bu, yüksek ayrıcalıklı bir izin kümesi olduğundan, yeni takım projeleri genellikle bir TFS dağıtımını yönetme sorumluluğunu içeren küçük bir kullanıcı alt kümesi tarafından oluşturulur. Geliştiricilere, genellikle yeni takım projeleri oluşturmak için gereken izinler verilmez.

### <a name="grant-permissions-in-tfs"></a>TFS 'de Izin verme

Bir kullanıcının yeni takım projeleri oluşturmasını etkinleştirmek istiyorsanız, ilk üst düzey görev, kullanıcıyı takım projesi koleksiyonu için **proje koleksiyonu yöneticileri** grubuna eklemektir.

**Proje koleksiyonu yöneticileri grubuna bir kullanıcı eklemek için**

1. TFS sunucusunda, **Başlat** menüsünde **tüm programlar**' ın üzerine gelin, **Microsoft Team Foundation Server 2010**' a ve ardından **Team Foundation Yönetim Konsolu**' e tıklayın.
2. Gezinti ağacı görünümünde, **uygulama katmanı**' nı genişletin ve ardından **Takım projesi koleksiyonları**' na tıklayın.

    ![](creating-a-team-project-in-tfs/_static/image1.png)
3. **Takım projesi koleksiyonları** bölmesinde, yönetmek istediğiniz takım projesi koleksiyonunu seçin.

    ![](creating-a-team-project-in-tfs/_static/image2.png)
4. **Genel** sekmesinde **Grup üyeliği**' ne tıklayın.

    ![](creating-a-team-project-in-tfs/_static/image3.png)
5. **Genel gruplar** iletişim kutusunda, **proje koleksiyonu yöneticileri** grubunu seçin ve ardından **Özellikler**' e tıklayın.
6. **Team Foundation Server grubu özellikleri** Iletişim kutusunda **Windows kullanıcısı veya grubu**' nu seçin ve ardından **Ekle**' ye tıklayın.

    ![](creating-a-team-project-in-tfs/_static/image4.png)
7. **Kullanıcıları, bilgisayarları veya grupları seç** iletişim kutusunda, yeni takım projeleri oluşturmak istediğiniz kullanıcının Kullanıcı adını yazın, **adları denetle**' ye tıklayın ve ardından **Tamam**' a tıklayın.

    ![](creating-a-team-project-in-tfs/_static/image5.png)
8. **Team Foundation Server grubu özellikleri** Iletişim kutusunda **Tamam**' a tıklayın.
9. **Genel gruplar** Iletişim kutusunda **Kapat**' a tıklayın.

### <a name="grant-permissions-in-sharepoint-services"></a>SharePoint hizmetlerinde Izin verme

Daha sonra, TFS takım projesi koleksiyonunuza karşılık gelen SharePoint site koleksiyonunda yeni ekip siteleri oluşturmak için kullanıcıya izin vermeniz gerekir.

**SharePoint site koleksiyonunda tam denetim izinleri vermek için**

1. Team Foundation Server Yönetim Konsolu, **Takım projesi koleksiyonları** sayfasında, yönetmek istediğiniz takım projesi koleksiyonunu seçin.
2. **SharePoint sitesi** sekmesinde, **geçerli varsayılan site konumu** URL 'sinin değerini aklınızda edin.

    ![](creating-a-team-project-in-tfs/_static/image6.png)
3. Internet Explorer 'ı açın ve ardından 2. adımda not ettiğiniz URL 'ye gidin.

    > [!NOTE]
    > Takım projesi koleksiyonunu oluşturan kullanıcı olarak Windows 'da oturum açmadıysanız, devam edebilmek için bu kullanıcı olarak SharePoint 'te oturum açmanız gerekir.
4. **Site eylemleri** menüsünde, **site ayarları**' na tıklayın.

    ![](creating-a-team-project-in-tfs/_static/image7.png)
5. **Site ayarları** sayfasında, **Kullanıcılar ve Izinler**altında, **kişiler ve gruplar**' a tıklayın.
6. Sol gezinti panelinde, **gruplar**' a tıklayın.

    ![](creating-a-team-project-in-tfs/_static/image8.png)
7. **Kişiler ve gruplar: tüm gruplar** sayfasında, **Bu site için grupları ayarla**' ya tıklayın.

    ![](creating-a-team-project-in-tfs/_static/image9.png)

   > [!NOTE]
   > Çift HTTP kodlama hatası nedeniyle bir <strong>http 404 bulunamadı</strong> hatası alabilirsiniz. Bu gerçekleşirse URL 'YI şu şekilde değiştirin:   
   > `[site_collection_URL]/_layouts/permsetup.aspx` örneğin:  
   > `http://tfs/sites/Fabrikam%20Web%20Projects/_layouts/permsetup.aspx` 
8. **Bu sitenin gruplarını ayarla** sayfasında, takım projelerini oluşturacak kullanıcıyı **sahipler** grubuna ekleyin ve ardından **Tamam**' a tıklayın.

    ![](creating-a-team-project-in-tfs/_static/image10.png)

Kullanıcıların bir takım projesi koleksiyonu içinde yeni takım projeleri oluşturmalarına olanak sağlama hakkında daha fazla bilgi için bkz. [Takım projesi koleksiyonları Için yönetici Izinlerini ayarlama](https://msdn.microsoft.com/library/dd547204.aspx).

## <a name="create-a-new-team-project-and-add-users"></a>Yeni bir takım projesi oluşturun ve kullanıcı ekleyin

Gerekli izinlere sahip olduktan sonra, yeni bir takım projesi oluşturmak için Visual Studio 2010 ' de **Takım Gezgini** penceresini kullanabilirsiniz. Bu yaklaşım, gerekli tüm bilgileri toplayan ve TFS, SharePoint ve SQL Server Reporting Services gerekli görevleri gerçekleştiren bir sihirbaz sağlar. Ayrıca, kullanıcıların içerik eklemesini ve değiştirmesini sağlamak için, geliştirici ekibinin üyelerine yeni takım projesi için izinler vermeniz gerekir.

### <a name="who-performs-these-procedures"></a>Bu yordamları kim gerçekleştiriyor?

Genellikle bir TFS Yöneticisi veya bir geliştirici ekibi lideri bu yordamları gerçekleştirir.

### <a name="create-a-new-team-project"></a>Yeni takım projesi oluştur

Sonraki yordamda TFS 2010 ' de yeni bir takım projesi oluşturma işlemi açıklanmaktadır.

**Yeni bir takım projesi oluşturmak için**

1. **Başlat** menüsünde **tüm programlar**' ın üzerine gelin, **Microsoft Visual Studio 2010**' ye tıklayın, **Microsoft Visual Studio 2010**' e sağ tıklayın ve ardından **yönetici olarak çalıştır**' a tıklayın.

    > [!NOTE]
    > Visual Studio 2010 ' ı yönetici olarak çalıştırmazsanız, son adımda yeni takım projesi Sihirbazı başarısız olur.
2. **Kullanıcı hesabı denetimi** iletişim kutusu görüntülenirse, **Evet**' e tıklayın.
3. Visual Studio 'da, **Takım** menüsünde **Team Foundation Server Bağlan**' a tıklayın.

    > [!NOTE]
    > TFS sunucusuna zaten bir bağlantı yapılandırdıysanız 4-7 arasındaki adımları atlayabilirsiniz.
4. **Takım projesi bağlantısı** Iletişim kutusunda **sunucular**' a tıklayın.
5. **Team Foundation Server Ekle/Kaldır** Iletişim kutusunda **Ekle**' ye tıklayın.
6. **Team Foundation Server Ekle** ILETIŞIM kutusunda TFS örneğinizin ayrıntılarını belirtin ve ardından **Tamam**' a tıklayın.

    ![](creating-a-team-project-in-tfs/_static/image11.png)
7. **Team Foundation Server Ekle/Kaldır** Iletişim kutusunda **Kapat**' a tıklayın.
8. **Takım Projesine Bağlan** iletişim kutusunda, bağlanmak istediğiniz TFS örneğini seçin, eklemek istediğiniz takım projesi koleksiyonunu seçin ve ardından **Bağlan**' a tıklayın.

    ![](creating-a-team-project-in-tfs/_static/image12.png)
9. **Takım Gezgini** penceresinde, takım projesi koleksiyonuna sağ tıklayın ve sonra **Yeni takım projesi**' ne tıklayın.

    ![](creating-a-team-project-in-tfs/_static/image13.png)
10. **Yeni takım projesi** iletişim kutusunda, takım projesi için bir ad ve açıklama girin ve ardından **İleri**' ye tıklayın.

    > [!NOTE]
    > Takım projeniz boşluk içeriyorsa, çıkış yolundan paketleri dağıtmak için Internet Information Services (IIS) Web Dağıtım aracı 'nı (Web Dağıtımı) kullandığınızda bazı sorunlar yaşayabilirsiniz. Yoldaki boşluklar, Web Dağıtımı komutlarının çalıştırılması çok daha zor hale gelir.

    ![](creating-a-team-project-in-tfs/_static/image14.png)
11. **Işlem şablonu seçin** sayfasında, geliştirme sürecini yönetmek için kullanmak istediğiniz işlem şablonunu seçin ve ardından **İleri**' ye tıklayın.

    > [!NOTE]
    > TFS için işlem şablonları hakkında daha fazla bilgi için bkz. [Işlem şablonları ve araçları](https://msdn.microsoft.com/vstudio/aa718795).
12. **Takım sitesi ayarları** sayfasında, varsayılan ayarları değiştirmeden bırakın ve **İleri**' ye tıklayın.
13. Bu ayar, TFS takım projesiyle ilişkili bir SharePoint ekip sitesi oluşturur veya tanımlar. Geliştirme ekibiniz bu siteyi belgeleri yönetmek, tartışma zincirlerine katılmak, wiki sayfaları oluşturmak ve kodla ilgili olmayan çeşitli diğer görevleri gerçekleştirmek için kullanabilir. Daha fazla bilgi için bkz. [SharePoint ürünleri ve Team Foundation Server arasındaki etkileşimler](https://msdn.microsoft.com/library/ms253177.aspx).
14. **Kaynak denetimi ayarlarını belirtin** sayfasında, varsayılan ayarları değiştirmeden bırakın ve **İleri**' ye tıklayın.
15. Bu ayar, TFS klasör hiyerarşisinde, içeriğiniz için bir kök klasör olarak görev yapacak konumu tanımlar veya oluşturur.
16. **Takım projesi ayarlarını Onayla** sayfasında, **son**' a tıklayın.
17. Yeni takım projesi başarıyla oluşturulduğunda, **Takım projesi oluşturulan** sayfasında **Kapat**' a tıklayın.

### <a name="add-users-to-a-team-project"></a>Takım projesine Kullanıcı ekleme

Yeni takım projesini oluşturduğunuza göre, kullanıcılara içeriğe ekleme ve işbirliği yapmaya başlamasını sağlamak için izinler verebilirsiniz.

**Bir takım projesine Kullanıcı eklemek için**

1. Visual Studio 2010 ' de, **Takım Gezgini** penceresinde, takım projesine sağ tıklayın, **Takım Projesi Ayarları**' nın üzerine gelin ve ardından **Grup üyeliği**' ne tıklayın.

    ![](creating-a-team-project-in-tfs/_static/image15.png)
2. Bir kullanıcının kaynak denetimi altında kod eklemesini, değiştirmesini ve kaldırmasını sağlamak için, bunu **katkıda bulunanlar** grubuna eklemeniz gerekir.
3. **Proje grupları** iletişim kutusunda, **katkıda bulunanlar** grubunu seçin ve ardından **Özellikler**' e tıklayın.

    ![](creating-a-team-project-in-tfs/_static/image16.png)
4. **Team Foundation Server grubu özellikleri** Iletişim kutusunda **Windows kullanıcısı veya grubu**' nu seçin ve ardından **Ekle**' ye tıklayın.

    ![](creating-a-team-project-in-tfs/_static/image17.png)
5. **Kullanıcıları, bilgisayarları veya grupları seç** iletişim kutusunda, takım projesine eklemek istediğiniz kullanıcının Kullanıcı adını yazın, **adları denetle**' ye tıklayın ve ardından **Tamam**' a tıklayın.

    ![](creating-a-team-project-in-tfs/_static/image18.png)
6. **Team Foundation Server grubu özellikleri** Iletişim kutusunda **Tamam**' a tıklayın.
7. **Proje grupları** Iletişim kutusunda **Kapat**' a tıklayın.

## <a name="conclusion"></a>Sonuç

Bu noktada, yeni takım projeniz kullanıma uygun hale gelmiştir ve geliştirici ekibiniz geliştirme sürecinde içerik eklemeye ve işbirliği yapmaya başlayabilir.

Sonraki konu, [kaynak denetimine Içerik ekleme](adding-content-to-source-control.md), kaynak denetimine içerik eklemeyi açıklar.

## <a name="further-reading"></a>Daha Fazla Bilgi

TFS 'de takım projeleri oluşturmaya yönelik daha geniş yönergeler için bkz. [Takım projesi oluşturma](https://msdn.microsoft.com/library/ms181477(v=VS.100).aspx). Kullanıcıların bir takım projesi koleksiyonu içinde yeni takım projeleri oluşturmalarına olanak sağlama hakkında daha fazla bilgi için bkz. [Takım projesi koleksiyonları Için yönetici Izinlerini ayarlama](https://msdn.microsoft.com/library/dd547204.aspx). Takım projelerine Kullanıcı ekleme hakkında daha fazla bilgi için bkz. [Takım projelerine Kullanıcı ekleme](https://msdn.microsoft.com/library/bb558971.aspx).

> [!div class="step-by-step"]
> [Önceki](configuring-team-foundation-server-for-web-deployment.md)
> [İleri](adding-content-to-source-control.md)
