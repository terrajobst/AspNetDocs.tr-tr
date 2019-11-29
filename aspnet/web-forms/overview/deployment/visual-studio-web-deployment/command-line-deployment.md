---
uid: web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
title: 'Visual Studio kullanarak Web dağıtımı ASP.NET: komut satırı dağıtımı | Microsoft Docs'
author: tdykstra
description: Bu öğretici serisi, bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf bir barındırma sağlayıcısına, usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 82b8dea0-f062-4ee4-8784-3ffa30fbb1ca
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
msc.type: authoredcontent
ms.openlocfilehash: 13cfe4492398b59f2c80394689cc113ccb218c60
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74634200"
---
# <a name="aspnet-web-deployment-using-visual-studio-command-line-deployment"></a>Visual Studio kullanarak Web dağıtımı ASP.NET: komut satırı dağıtımı

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Başlatıcı projesi indir](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> Bu öğretici serisi, Visual Studio 2012 veya Visual Studio 2010 kullanarak bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf barındırma sağlayıcısına dağıtmayı (yayımlamayı) gösterir. Seriler hakkında daha fazla bilgi için, [serideki ilk öğreticiye](introduction.md)bakın.

## <a name="overview"></a>Genel bakış

Bu öğreticide, komut satırından Visual Studio Web yayımlama ardışık düzenini çağırma gösterilmektedir. Bu, genellikle [kaynak kodu sürüm denetim sistemi](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)kullanarak Visual Studio 'da el ile yapmak yerine [dağıtım sürecini otomatikleştirmek](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) istediğiniz senaryolar için yararlıdır.

## <a name="make-a-change-to-deploy"></a>Dağıtmak için bir değişiklik yapın

Şu anda hakkında sayfasında Şablon kodu görüntülenir.

![Şablon kodu içeren sayfa hakkında](command-line-deployment/_static/image1.png)

Bunu, öğrenci kaydı özetini görüntüleyen kodla değiştirirsiniz.

*About. aspx* sayfasını açın, `MainContent` `Content` öğesi içindeki tüm biçimlendirmeyi silin ve aşağıdaki biçimlendirmeyi onun yerine ekleyin:

[!code-aspx[Main](command-line-deployment/samples/sample1.aspx)]

Projeyi çalıştırın ve **hakkında** sayfasını seçin.

![Sayfa hakkında](command-line-deployment/_static/image2.png)

## <a name="deploy-to-test-by-using-the-command-line"></a>Komut satırını kullanarak test 'e dağıtın

Başka bir veritabanı değişikliği dağıtmayacağız. bu nedenle, ASPNET-ContosoUniversity veritabanı için dbDacFx veritabanı dağıtımını devre dışı bırakın. Web 'i **Yayımla** sihirbazını açın ve üç yayımlama profilinin her birinde, **Ayarlar** sekmesindeki **veritabanını güncelleştir** onay kutusunun işaretini kaldırın.

Windows 8 başlangıç sayfasında, **VS2012 için geliştirici komut istemi**aratın.

**VS2012 için geliştirici komut istemi** simgeye sağ tıklayın ve **yönetici olarak çalıştır**' a tıklayın.

Komut istemine aşağıdaki komutu girin ve çözüm dosyası yolunu çözüm dosyası yoluyla değiştirin:

[!code-console[Main](command-line-deployment/samples/sample2.cmd)]

MSBuild çözümü oluşturur ve test ortamına dağıtır.

![Komut satırı çıkışı](command-line-deployment/_static/image3.png)

Bir tarayıcı açın ve `http://localhost/ContosoUniversity`gidin ve sonra dağıtımın başarılı olduğunu doğrulamak için **hakkında** sayfasına tıklayın.

Testte herhangi bir öğrenci oluşturmadıysanız, **öğrenci gövdesi istatistikleri** başlığının altında boş bir sayfa görürsünüz. **Öğrenciler** sayfasına gidin, **öğrenci Ekle**' ye tıklayın ve bazı öğrenciler ekleyin ve sonra öğrenci istatistiklerini görmek için **hakkında** sayfasına dönün.

![Test ortamında sayfa hakkında](command-line-deployment/_static/image4.png)

## <a name="key-command-line-options"></a>Anahtar komut satırı seçenekleri

Girdiğiniz komut çözüm dosyası yolunu ve MSBuild 'e iki özelliği geçti:

[!code-console[Main](command-line-deployment/samples/sample3.cmd)]

### <a name="deploying-the-solution-versus-deploying-individual-projects"></a>Tek tek projeleri dağıtmaya karşı çözümü dağıtma

Çözüm dosyası belirtildiğinde Çözümdeki tüm projelerin oluşturulmasına neden olur. Çözümde birden çok Web projeniz varsa, aşağıdaki MSBuild davranışı geçerlidir:

- Komut satırında belirttiğiniz özellikler her projeye geçirilir. Bu nedenle, her Web projesinin belirttiğiniz ada sahip bir yayımlama profili olması gerekir. `/p:PublishProfile=Test`belirtirseniz, her Web projesinin *Test*adlı bir yayımlama profili olması gerekir.
- Başka bir proje bile derlenmezse, bir projeyi başarıyla yayımlayabilirsiniz. Daha fazla bilgi için bkz. StackOverflow thread [MSBuild, iki paket ile başarısız oluyor](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages).

Çözüm yerine bireysel bir proje belirtirseniz, Visual Studio sürümünü belirten bir parametre eklemeniz gerekir. Visual Studio 2012 kullanıyorsanız komut satırı aşağıdaki örneğe benzer olacaktır:

[!code-console[Main](command-line-deployment/samples/sample4.cmd?highlight=1)]

Visual Studio 2010 sürüm numarası 10,0 ' dir. Daha fazla bilgi için bkz. [Visual Studio proje uyumluluğu ve VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) on hashed 'in blogu.

### <a name="specifying-the-publish-profile"></a>Yayımlama profilini belirtme

Aşağıdaki örnekte gösterildiği gibi, yayımlama profilini adına göre veya *. pubxml* dosyasının tam yolu ile belirtebilirsiniz:

[!code-console[Main](command-line-deployment/samples/sample5.cmd?highlight=1)]

### <a name="web-publish-methods-supported-for-command-line-publishing"></a>Komut satırı yayımlama için desteklenen Web yayımlama yöntemleri

Komut satırı yayımlama için üç yayımlama yöntemi desteklenir:

- `MSDeploy`-Web Dağıtımı kullanarak yayımlayın.
- `Package`-Web Dağıtımı bir paket oluşturarak yayımlayın. Paketi, onu oluşturan MSBuild komutundan ayrı olarak yüklemelisiniz.
- `FileSystem`-dosyaları belirtilen klasöre kopyalayarak yayımlayın.

### <a name="specifying-the-build-configuration-and-platform"></a>Yapı yapılandırmasını ve platformunu belirtme

Derleme yapılandırması ve platformun Visual Studio 'da veya komut satırında ayarlanması gerekir. Yayımlama profilleri `LastUsedBuildConfiguration` ve `LastUsedPlatform`adlı özellikleri içerir, ancak projenin nasıl oluşturulduğunu belirleyebilmek için bu özellikleri ayarlayamazsınız. Daha fazla bilgi için bkz. MSBuild: saymış Hashbir Web bloguna [yapılandırma özelliğini ayarlama](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) .

## <a name="deploy-to-staging"></a>Hazırlama için dağıt

Azure 'a dağıtmak için, parolayı komut satırına eklemeniz gerekir. Parolayı Visual Studio 'daki Yayımla profilinde kaydettiyseniz, *. pubxml. User* dosyanızda şifreli biçimde depolanmıştı. Bir komut satırı dağıtımı yaptığınızda bu dosyaya MSBuild tarafından erişilmez, bu nedenle parolayı bir komut satırı parametresinde geçirmeniz gerekir.

1. Daha önce hazırlama Web sitesi için indirdiğiniz *. publishsettings* dosyasından gereken parolayı kopyalayın. Parola, Web Dağıtımı `publishProfile` öğesi için `userPWD` özniteliğinin değeridir.

    ![Web Dağıtımı parolası](command-line-deployment/_static/image5.png)
2. Windows 8 başlangıç sayfasında, **VS2012 için geliştirici komut istemi**arayın ve komut istemi ' ni açmak için simgeye tıklayın. (Yerel bilgisayarda IIS 'e dağıtmıyorsanız, bu kez yönetici olarak açmanız gerekmez.)
3. Komut istemine aşağıdaki komutu girin, çözüm dosyası yolunu çözüm dosyası yoluyla ve parolanızla parolayla değiştirin:

    [!code-console[Main](command-line-deployment/samples/sample6.cmd)]

    Bu komut satırının ek bir parametre içerdiğine dikkat edin: `/p:AllowUntrustedCertificate=true`. Bu öğretici yazıldığı için, komut satırından Azure 'da yayımladığınızda `AllowUntrustedCertificate` özelliği ayarlanmalıdır. Bu hata için düzeltildiğinde bu parametreye gerek kalmaz.
4. Bir tarayıcı açın ve hazırlama sitenizin URL 'sine gidin ve sonra dağıtımın başarılı olduğunu doğrulamak için **hakkında** sayfasına tıklayın.

    Daha önce test ortamı için gördüğünüz gibi, **hakkında** sayfasında istatistikleri görmek için bazı öğrenciler oluşturmanız gerekebilir.

## <a name="deploy-to-production"></a>Üretime dağıtma

Üretime dağıtma işlemi, hazırlama işlemine benzerdir.

1. Daha önce üretim web sitesi için indirdiğiniz *. publishsettings* dosyasından gereken parolayı kopyalayın.
2. **VS2012 için geliştirici komut istemi**açın.
3. Komut istemine aşağıdaki komutu girin, çözüm dosyası yolunu çözüm dosyası yoluyla ve parolanızla parolayla değiştirin:

    [!code-console[Main](command-line-deployment/samples/sample7.cmd)]

    Gerçek bir üretim sitesi için aynı zamanda bir veritabanı değişikliği varsa, genellikle *uygulamayı çevrimdışı. htm dosyası\_* dağıtımdan önce siteye kopyalayabilir ve başarılı dağıtımdan sonra silmeniz gerekir.
4. Bir tarayıcı açın ve hazırlama sitenizin URL 'sine gidin ve sonra dağıtımın başarılı olduğunu doğrulamak için **hakkında** sayfasına tıklayın.

## <a name="summary"></a>Özet

Artık komut satırını kullanarak bir uygulama güncelleştirmesi dağıttınız.

![Test ortamında sayfa hakkında](command-line-deployment/_static/image6.png)

Sonraki öğreticide, Web yayımlama işlem hattının nasıl uzatılayabileceğinizi gösteren bir örnek görürsünüz. Örnek, projeye dahil olmayan dosyaları nasıl dağıtacağınızı gösterir.

> [!div class="step-by-step"]
> [Önceki](deploying-a-database-update.md)
> [İleri](deploying-extra-files.md)
