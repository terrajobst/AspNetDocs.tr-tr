---
uid: web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
title: 'Visual Studio kullanarak Web dağıtımını ASP.NET: klasör Izinlerini ayarlama | Microsoft Docs'
author: tdykstra
description: Bu öğretici serisi, bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf bir barındırma sağlayıcısına, usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 9715a121-fa55-4f1b-a5d2-fb3f6cd8be8f
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
msc.type: authoredcontent
ms.openlocfilehash: 410525bb2e3f6e5a0be6d7d6b33fb3a40509041a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78576064"
---
# <a name="aspnet-web-deployment-using-visual-studio-setting-folder-permissions"></a>Visual Studio kullanarak Web dağıtımı ASP.NET: klasör Izinlerini ayarlama

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Başlatıcı projesi indir](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> Bu öğretici serisi, Visual Studio 2012 veya Visual Studio 2010 kullanarak bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf barındırma sağlayıcısına dağıtmayı (yayımlamayı) gösterir. Seriler hakkında daha fazla bilgi için, [serideki ilk öğreticiye](introduction.md)bakın.

## <a name="overview"></a>Genel bakış

Bu öğreticide, uygulamanın bu klasörde günlük dosyaları oluşturabilmesi için dağıtılan Web sitesindeki *ELMAH* klasörü için klasör izinlerini ayarlarsınız.

Visual Studio geliştirme sunucusu (Cassini) veya IIS Express kullanarak bir Web uygulamasını test ettiğinizde, uygulama kimliğiniz altında çalışır. Büyük olasılıkla geliştirme bilgisayarınızda bir yöneticidir ve herhangi bir klasördeki herhangi bir dosya için herhangi bir şey yapmak üzere tam yetkiye sahip olursunuz. Ancak bir uygulama IIS altında çalıştığında, sitenin atandığı uygulama havuzu için tanımlanan kimlik altında çalışır. Bu, genellikle sınırlı izinlere sahip sistem tanımlı bir hesaptır. Varsayılan olarak, Web uygulamanızın dosya ve klasörlerinde okuma ve yürütme izinlerine sahiptir, ancak yazma erişimine sahip değildir.

Bu durum, uygulamanız Web uygulamalarında ortak olması gereken dosyaları oluşturduğunda veya güncelleştirirse bir sorun haline gelir. Contoso University uygulamasında, ELMAH, hatalarla ilgili ayrıntıları kaydetmek için *ELMAH* klasöründe XML dosyaları oluşturur. ELMAH gibi bir şey kullanmasanız bile siteniz, kullanıcıların dosyaları karşıya yüklemesine veya sitenizdeki bir klasöre veri yazan diğer görevleri gerçekleştirmesine izin verebilir.

Anımsatıcı: bir hata iletisi alırsanız veya öğreticide ilerlediyseniz bir şey çalışmadıysanız [sorun giderme sayfasını](troubleshooting.md)kontrol ettiğinizden emin olun.

## <a name="test-error-logging-and-reporting"></a>Test hatası günlüğü ve raporlama

Uygulamanın IIS 'de düzgün bir şekilde nasıl çalışmadığını görmek için (Visual Studio 'da test ettiğinizde), normalde ELMAH tarafından günlüğe kaydedilecek bir hataya neden olabilir ve ardından ayrıntıları görmek için ELMAH hata günlüğünü açın. ELMAH bir XML dosyası oluşturamadı ve hata ayrıntılarını depoladıysa boş bir hata raporu görürsünüz.

Bir tarayıcı açın ve `http://localhost/ContosoUniversity`gidin ve sonra *Studentsxxx. aspx*gibi GEÇERSIZ bir URL isteyin. Web. config dosyasındaki `customErrors` ayarı "RemoteOnly" olduğundan ve IIS 'yi yerel olarak çalıştırdığınız için *Genericerrorpage. aspx* sayfası yerine sistem tarafından oluşturulan bir hata sayfası görürsünüz:

![HTTP 404 hata sayfası](setting-folder-permissions/_static/image1.png)

Şimdi hata raporunu görmek için *ELMAH. axd* ' i çalıştırın. Yönetici hesabı kimlik bilgileri (&quot;yönetici&quot; ve &quot;devpwd&quot;) ile oturum açtıktan sonra, ELMAH, *ELMAH* KLASÖRÜNDE bir XML dosyası oluşturamadığından boş bir hata günlüğü sayfası görürsünüz:

![Hata günlüğü boş](setting-folder-permissions/_static/image2.png)

## <a name="set-write-permission-on-the-elmah-folder"></a>ELMAH klasörü üzerinde yazma izni ayarlama

Klasör izinlerini el ile ayarlayabilir veya dağıtım sürecinin otomatik bir parçası yapabilirsiniz. Bunu otomatik hale getirmek için karmaşık MSBuild kodu gerekir ve bunu yalnızca ilk dağıttığınız zaman yapmanız gerektiğinden, el ile nasıl yapılacağını aşağıdaki adımları izleyin. (Dağıtım işleminin bu bölümünü oluşturma hakkında daha fazla bilgi için bkz. [Web 'de klasör Izinlerini ayarlama](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) , saymış hashed 'in blogu üzerinde yayımlama.)

1. **Dosya Gezgini**'nde *C:\inetpub\wwwroot\contosoüniversitesi*' ne gidin. *ELMAH* klasörüne sağ tıklayın, **Özellikler**' i seçin ve ardından **güvenlik** sekmesini seçin.
2. **Düzenle**‘ye tıklayın.
3. **ELMAH izinleri** iletişim kutusunda, **DefaultAppPool**' ı seçin ve ardından **izin ver** sütununda **yazma** onay kutusunu seçin.

    ![ELMAH klasörü için izinler](setting-folder-permissions/_static/image3.png)

    ( **Grup veya Kullanıcı adları** listesinde **DefaultAppPool** ÖĞESINI görmüyorsanız, bilgisayarınızda IIS ve ASP.NET 4 ' ü ayarlamak için bu öğreticide belirtilenden farklı bir yöntem kullanmışsınızdır. Bu durumda, Contoso Üniversitesi uygulamasına atanan uygulama havuzu tarafından kullanılan kimliği öğrenin ve bu kimliğe yazma izni verin. Bu öğreticinin sonundaki uygulama havuzu kimlikleri hakkındaki bağlantılara bakın.) Her iki iletişim kutusunda **Tamam** ' a tıklayın.

## <a name="retest-error-logging-and-reporting"></a>Hata günlüğü ve raporlama yeniden test etme

Aynı şekilde bir hataya neden olan (hatalı URL iste) ve **hata günlüğü** sayfasını çalıştırarak test edin. Bu kez hata sayfada görüntülenir.

![ELMAH hata günlüğü sayfası](setting-folder-permissions/_static/image4.png)

## <a name="summary"></a>Özet

Contoso Üniversitesi 'nin yerel bilgisayarınızda IIS 'de düzgün şekilde çalışmasını sağlamak için gereken tüm görevleri tamamladınız. Sonraki öğreticide, siteyi Azure 'a dağıtarak genel kullanıma sunulacaktır.

## <a name="more-information"></a>Daha fazla bilgi

Bu örnekte, ELMAH 'nin günlük dosyalarını kaydedememesinin nedeni oldukça açıktır. Sorun nedeninin açık olmadığı durumlarda IIS izlemeyi kullanabilirsiniz; IIS.net sitesinde [IIS 7 ' de Izleme kullanarak başarısız Isteklerin sorunlarını giderme](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis) bölümüne bakın.

Uygulama havuzu kimliklerine izin verme hakkında daha fazla bilgi için, IIS.net sitesindeki [dosya sistemi ACL 'Leri aracılığıyla IIS 'Deki](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls) [uygulama havuzu kimlikleri](https://www.iis.net/learn/manage/configuring-security/application-pool-identities) ve güvenli içerik bölümüne bakın.

> [!div class="step-by-step"]
> [Önceki](deploying-to-iis.md)
> [İleri](deploying-to-production.md)
