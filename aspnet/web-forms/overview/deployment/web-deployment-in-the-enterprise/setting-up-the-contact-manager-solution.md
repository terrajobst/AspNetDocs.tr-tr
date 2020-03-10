---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
title: Contact Manager çözümünü ayarlama | Microsoft Docs
author: jrjlee
description: Bu konuda, bir geliştirici iş istasyonunda yerel olarak çalışacak olan Contact Manager çözümünün nasıl indirileceği ve yapılandırılacağı açıklanmaktadır.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 200b973c-776b-4a9b-9e82-39fda6120a52
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: d9774ee01cb0515d7e733b24baa661f2648bd7c4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78629859"
---
# <a name="setting-up-the-contact-manager-solution"></a>Kişi Yöneticisi Çözümünü Ayarlama

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konuda, bir geliştirici iş istasyonunda yerel olarak çalışacak olan Contact Manager çözümünün nasıl indirileceği ve yapılandırılacağı açıklanmaktadır.

## <a name="system-requirements"></a>Sistem Gereksinimleri

Contact Manager çözümünü yerel olarak çalıştırmak ve bu öğreticide açıklanan diğer görevleri gerçekleştirmek için, bu yazılımı geliştirici iş istasyonunuza yüklemeniz gerekir:

- Visual Studio 2010 Service Pack 1, Premium veya Ultimate sürümü
- Internet Information Services (IIS) 7,5 Express
- SQL Server Express 2008 R2
- IIS Web Dağıtım Aracı (Web Dağıtımı) 2,1 veya üzeri
- ASP.NET 4.0
- ASP.NET MVC 3
- .NET Framework 4
- .NET Framework 3.5 SP1

Visual Studio 2010 hariç olmak üzere, [Web Platformu Yükleyicisi](https://go.microsoft.com/?linkid=9805118)aracılığıyla bu ürünlerin ve bileşenlerin en son sürümlerini indirip yükleyebilirsiniz.

## <a name="download-and-extract-the-solution"></a>Çözümü indirme ve ayıklama

[Burada](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0)MSDN kod galerisinden Contact Manager örnek uygulamasını indirebilirsiniz.

## <a name="configure-and-run-the-solution"></a>Çözümü yapılandırma ve çalıştırma

Yerel makinenizde Contact Manager çözümünü yapılandırmak ve çalıştırmak için aşağıdaki üst düzey adımları gerçekleştirmeniz gerekir:

1. Henüz bir tane yoksa, üyelik ve rol yönetimi özellikleri etkin olan bir yerel ASP.NET uygulama Hizmetleri veritabanı oluşturun.
2. *Web. config* dosyalarındaki bağlantı dizelerini yerel SQL Server Express örneğinizi gösterecek şekilde düzenleyin.
3. Çözümü Visual Studio 2010 ' dan çalıştırın.

Bu bölümün geri kalanında, bu görevlerin her birini tamamlamaya yönelik daha fazla rehberlik sunulmaktadır.

**Uygulama Hizmetleri veritabanını oluşturmak için**

1. Bir Visual Studio 2010 komut istemi açın. Bunu yapmak için, **Başlat** menüsünde **tüm programlar**' ın üzerine gelin, **Microsoft Visual Studio 2010**' ye tıklayın, **Visual Studio Araçları**' a ve ardından **Visual Studio komut istemi (2010)** ' ne tıklayın.
2. Komut isteminde şu komutu yazın ve ENTER tuşuna basın:

    [!code-console[Main](setting-up-the-contact-manager-solution/samples/sample1.cmd)]

    1. Veritabanı sunucunuzun bağlantı dizesini belirtmek için **– C** anahtarını kullanın.
    2. Veritabanına eklemek istediğiniz uygulama Hizmetleri özelliklerini belirtmek için **– A** anahtarını kullanın. Bu durumda, **m** üyelik sağlayıcısı için destek eklemek istediğinizi ve **r** 'nin rol yöneticisi için destek eklemek istediğinizi belirtir.
    3. Uygulama Hizmetleri veritabanınız için bir ad belirtmek üzere **– d** anahtarını kullanın. Bu anahtarı atlarsanız, yardımcı program varsayılan **aspnetdb**adı ile bir veritabanı oluşturur.
3. Veritabanı başarılı bir şekilde oluşturulduğunda, komut isteminde bir onay gösterilecektir.

    ![](setting-up-the-contact-manager-solution/_static/image1.png)

> [!NOTE]
> ASPNET\_regsql yardımcı programı hakkında daha fazla bilgi için bkz. [ASP.NET SQL Server kayıt aracı (aspnet\_regsql. exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx).

Bir sonraki adım, Contact Manager çözümündeki bağlantı dizelerinin yerel SQL Server Express yerel örneğinizi işaret ettiğinizden emin olmak için kullanılır.

**Bağlantı dizelerini güncelleştirmek için**

1. Visual Studio 2010 ' de Contact Manager çözümünü açın.
2. **Çözüm Gezgini** penceresinde **ContactManager. Mvc** projesini genişletin ve **Web. config** düğümüne çift tıklayın.

    > [!NOTE]
    > ContactManager. Mvc projesi iki *Web. config* dosyası içerir. Proje düzeyi dosyasını düzenlemeniz gerekir.

    ![](setting-up-the-contact-manager-solution/_static/image2.png)
3. **ConnectionStrings** öğesinde, **ApplicationServices** adlı bağlantı dizesinin yerel ASP.NET uygulama hizmetleri veritabanınıza işaret ettiğini doğrulayın.

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample2.xml)]
4. **Çözüm Gezgini** penceresinde **ContactManager. Service** projesini genişletin ve **Web. config** düğümüne çift tıklayın.

    ![](setting-up-the-contact-manager-solution/_static/image3.png)
5. **ConnectionStrings** öğesinde, **contactmanagercontext**adlı bağlantı dizesinde, **veri kaynağı** özelliğinin yerel SQL Server Express olarak ayarlandığını doğrulayın. Bağlantı dizesinde başka herhangi bir şeyi değiştirmeniz gerekmez.

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample3.xml)]
6. Tüm açık dosyaları kaydedin.

Şimdi yerel makinenizde Contact Manager çözümünü çalıştırmaya hazır olmanız gerekir.

> [!NOTE]
> Uygulama Hizmetleri veritabanı oluşturmadan önce bu adımları izlerseniz, ASP.NET ilk kez kullanıcı oluşturmaya çalıştığınızda veritabanını oluşturur. Ancak, veritabanının el ile oluşturulması, desteklemek istediğiniz uygulama hizmetleri özellik kümesi üzerinde çok daha fazla denetim sağlar.

**Contact Manager çözümünü çalıştırmak için**

1. Visual Studio 2010 ' de F5 tuşuna basın.
2. Internet Explorer başlatılır ve Contact Manager ASP.NET MVC 3 uygulamasının URL 'sini ister. Varsayılan olarak, uygulama **tüm kişiler** sayfasını görüntüler.

    ![](setting-up-the-contact-manager-solution/_static/image4.png)
3. Birkaç kişi ekleyin ve sonra uygulamanın beklendiği gibi çalıştığını doğrulayın.

    ![](setting-up-the-contact-manager-solution/_static/image5.png)
4. `http://localhost:50114/Account/Register` gidin (uygulamayı farklı bir bağlantı noktasında barındırıyorsanız URL 'YI ayarlayın). Bir Kullanıcı adı, e-posta adresi ve parola ekleyin ve bir hesabı başarıyla kaydedebildiğinizi doğrulayın.

    ![](setting-up-the-contact-manager-solution/_static/image6.png)
5. `http://localhost:50114/Account/LogOn` gidin (uygulamayı farklı bir bağlantı noktasında barındırıyorsanız URL 'YI ayarlayın). Yeni oluşturduğunuz hesabı kullanarak oturum açabildiğinizi doğrulayın.

    ![](setting-up-the-contact-manager-solution/_static/image7.png)
6. Hata ayıklamayı durdurmak için Internet Explorer 'ı kapatın.

## <a name="conclusion"></a>Sonuç

Bu noktada, Contact Manager çözümünün yerel makinenizde çalışacak şekilde tam olarak yapılandırılması gerekir. Bu öğreticideki diğer konularda çalışırken çözümü başvuru olarak kullanabilirsiniz.

Bir sonraki konu, [Proje dosyasını anlamak](understanding-the-project-file.md)için, dağıtım işlemini denetlemek üzere Contact Manager çözümünde özel Microsoft Build Engine (MSBuild) proje dosyalarını nasıl kullanabileceğinizi açıklar.

> [!div class="step-by-step"]
> [Önceki](the-contact-manager-solution.md)
> [İleri](understanding-the-project-file.md)
