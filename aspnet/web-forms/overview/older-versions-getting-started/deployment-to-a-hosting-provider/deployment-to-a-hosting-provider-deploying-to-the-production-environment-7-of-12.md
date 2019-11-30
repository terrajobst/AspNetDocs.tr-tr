---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12
title: 'Visual Studio veya Visual Web Developer kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: üretim ortamına dağıtma-7/12 | Microsoft Docs'
author: tdykstra
description: Bu öğretici dizisinde, Visual Stu kullanarak bir SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesinin nasıl dağıtılacağı (yayımlanacağı) gösterilmektedir.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: b83ab819-2b05-4776-b7b4-79ef78d457a5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12
msc.type: authoredcontent
ms.openlocfilehash: db838633accdedd7c0693b126a007e254ca681e4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74627460"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-to-the-production-environment---7-of-12"></a>Visual Studio veya Visual Web Developer kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: üretim ortamına dağıtım-7/12

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Başlatıcı projesi indir](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> Bu öğretici serisi, Visual Studio 2012 RC veya Web için Visual Studio Express 2012 RC kullanarak SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesini dağıtmayı (yayımlamayı) gösterir. Ayrıca, Web yayımlama güncelleştirmesini yüklerseniz Visual Studio 2010 de kullanabilirsiniz. Seriye giriş için, [serideki ilk öğreticiye](deployment-to-a-hosting-provider-introduction-1-of-12.md)bakın.
> 
> Visual Studio 2012 RC yayımlandıktan sonra tanıtılan dağıtım özelliklerini gösteren bir öğretici için, SQL Server Compact dışındaki SQL Server sürümlerinin nasıl dağıtılacağını gösterir ve Web Apps Azure App Service nasıl dağıtılacağını gösterir. bkz. [Visual Studio kullanarak ASP.NET Web dağıtımı](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Genel bakış

Bu öğreticide, bir barındırma sağlayıcısı ile bir hesap ayarlarsınız ve Visual Studio One-tıklama Yayımla özelliğini kullanarak ASP.NET Web uygulamanızı üretim ortamına dağıtırsınız.

Anımsatıcı: bir hata iletisi alırsanız veya öğreticide ilerlediyseniz bir şey çalışmadıysanız [sorun giderme sayfasını](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)kontrol ettiğinizden emin olun.

## <a name="selecting-a-hosting-provider"></a>Barındırma sağlayıcısı seçme

Contoso Üniversitesi uygulaması ve bu öğretici serisi için ASP.NET 4 ve Web Dağıtımı destekleyen bir sağlayıcıya ihtiyacınız vardır. Öğreticilerin canlı bir Web sitesine dağıtmanın tüm deneyimini görebilmesi için belirli bir barındırma şirketi seçilmiştir. Her barındırma şirketi farklı özellikler sağlar ve sunucularına dağıtım deneyimi biraz farklılık gösterir. Ancak, bu öğreticide açıklanan işlem, genel işlem için tipik bir işlemdir. Bu öğretici için kullanılan barındırma sağlayıcısı, Cytanium.com, kullanılabilir birçok bir tane ve bu öğreticide kullanımı bir onay veya öneri oluşturmaz.

Kendi barındırma sağlayıcınızı seçmek için hazırsanız, Microsoft.com/web sitesindeki [sağlayıcı galerisindeki](https://www.microsoft.com/web/hosting) özellikleri ve fiyatları karşılaştırabilirsiniz.

## <a name="creating-an-account"></a>Hesap oluşturma

Seçtiğiniz sağlayıcıda bir hesap oluşturun. Tam bir SQL Server veritabanına yönelik destek eklenirse, bu öğretici için bu öğreticide seçim yapmanız gerekmez, ancak bu serinin ilerleyen kısımlarında SQL Server öğreticiye [geçiş yapmak](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md) için ihtiyacınız olacaktır.

Bu öğreticiler için yeni bir etki alanı adı kaydetmeniz gerekmez. Sağlayıcı tarafından siteye atanan geçici URL 'YI kullanarak başarılı dağıtımı doğrulamaya test edebilirsiniz.

Hesap oluşturulduktan sonra genellikle sitenizi dağıtmak ve yönetmek için ihtiyacınız olan tüm bilgileri içeren bir hoş geldiniz e-postası alırsınız. Barındırma sağlayıcınızın size gönderdiği bilgiler burada gösterilenlere benzer olacaktır. Yeni hesap sahiplerine gönderilen Cytanium hoş geldiniz e-postası aşağıdaki bilgileri içerir:

- Sitenizin ayarlarını yönetebileceğiniz sağlayıcının Denetim Masası sitesinin URL 'SI. Belirttiğiniz KIMLIK ve parola, hoş geldiniz e-postası 'nın bu bölümüne kolay başvuru için dahil edilmiştir. (Her ikisi de bu çizim için bir demo değeri olarak değiştirilmiştir.)

    [![Welcome_Email_Control_Panel_URL](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image1.png)
- Varsayılan .NET Framework sürümü ve nasıl değiştirileceği hakkında bilgi. Birçok barındırma sitesi varsayılan 2,0 ' dir ve bu, 2,0, 3,0 veya 3,5 .NET Framework hedeflenen ASP.NET uygulamalarıyla birlikte geçerlidir. Ancak Contoso Üniversitesi bir .NET Framework 4 uygulaması olduğundan bu ayarı değiştirmeniz gerekir. (Bir ASP.NET 4,5 uygulaması için .NET 4,0 ayarını kullanmanız gerekir.)

    [![Welcome_Email_Framework_Version](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image3.png)
- Web sitenize erişmek için kullanabileceğiniz geçici URL. Bu hesap oluşturulduğunda, var olan etki alanı adı olarak "contosouniversity.com" girildi. Bu nedenle, geçici URL `http://contosouniversity.com.vserver01.cytanium.com`.

    [![Welcome_Email_Temporary_URL](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image6.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image5.png)
- Veritabanlarının nasıl ayarlanacağı ve bunlara erişmek için ihtiyacınız olan bağlantı dizelerinin hakkında bilgi:

    [![Welcome_Email_Database_Info](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image7.png)
- Sitenizi dağıtmaya yönelik araçlar ve ayarlar hakkında bilgi. (Cytanium 'den e-posta, burada atlanan WebMatrix 'e de değinmektedir.)

    [![Welcome_Email_Deploy_info](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image10.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image9.png)

## <a name="setting-the-net-framework-version"></a>.NET Framework sürümünü ayarlama

Cytanium hoş geldiniz e-postası, .NET Framework sürümünün nasıl değiştirileceği hakkında yönergeler için bir bağlantı içerir. Bu yönergeler bunun Cytanium Denetim Masası aracılığıyla yapılabileceğini açıklamaktadır. Diğer sağlayıcılar, farklı görünen Denetim Masası sitelerine sahiptir veya bunu farklı bir şekilde yapmanızı isteyebilir.

Denetim Masası URL 'sine gidin. Kullanıcı adınız ve parolanızla oturum açtıktan sonra Denetim Masası ' nı görürsünüz.

[![Cytanium_Control_Panel](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image11.png)

**Barındırma alanları** kutusunda, işaretçiyi Web simgesinin üzerine tutun ve menüden **Web siteleri** ' ni seçin.

[![Cytanium_Control_Panel_selecting_Web_Sites](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image13.png)

**Web siteleri** kutusunda, **contosouniversity.com** (hesabı oluştururken kullandığınız sitenin adı) seçeneğine tıklayın.

[![Cytanium_Control_Panel_selecting_contosouniversity](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image15.png)

**Web sitesi özellikleri** kutusunda **Uzantılar** sekmesini seçin.

[![Cytanium_Control_Panel_Extensions_tab](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image17.png)

**2,0 tümleşik** işlem hattından **4,0 (tümleşik işlem hattı)** ASP.net değiştirin ve ardından **Güncelleştir**' e tıklayın.

## <a name="publishing-to-the-hosting-provider"></a>Barındırma sağlayıcısına yayımlama

Barındırma sağlayıcısından hoş geldiniz e-postası, projeyi yayımlamak için ihtiyacınız olan tüm ayarları içerir ve bu bilgileri bir yayımlama profiline el ile girebilirsiniz. Ancak sağlayıcıya dağıtımı yapılandırmak için daha kolay ve daha az hata durumunda olan bir yöntem kullanacaksınız: bir *. publishsettings* dosyası indirip bir yayımlama profiline içeri aktarırsınız.

Tarayıcınızda Cytanium Denetim Masası ' na gidin ve **Web** ' i seçip **Web siteleri** ' ni seçin.

![Web siteleri seçme Denetim Masası](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image19.png)

**Contosouniversity.com** Web sitesini seçin.

![Denetim Masası contosouniversity.com seçme](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image20.png)

**Web yayımlama** sekmesini seçin.

![Denetim Masası Web yayımlama sekmesi](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image21.png)

Bir Kullanıcı adı ve parola girerek Web yayımlaması için kullanılacak kimlik bilgilerini oluşturun. Denetim Masası 'nda oturum açmak için kullandığınız kimlik bilgilerini girebilirsiniz. Ardından **Etkinleştir**' e tıklayın.

![Denetim Masası yayımlama kimlik bilgileri oluştur](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image22.png)

**Bu web sitesi Için yayımlama profilini indir**' e tıklayın.

![Denetim Masası indirme yayımlama profili](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image23.png)

Dosyayı açmanız veya kaydetmeniz istendiğinde kaydedin.

![Yayımlama profili dosyasını Kaydet](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image24.png)

Visual Studio 'da **Çözüm Gezgini** , contosouniversity projesine sağ tıklayın ve **Yayımla**' yı seçin. **Web 'ı Yayımla** iletişim kutusu, kullandığınız son profil olduğundan, **Test** profili seçili olan **Önizleme** sekmesinde açılır.

**Profil** sekmesini seçin ve ardından **içeri aktar**' a tıklayın.

![Web 'i Yayımlama Sihirbazı Içeri aktarma düğmesi](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image25.png)

**Yayımlama ayarlarını Içeri aktar** iletişim kutusunda, indirdiğiniz *. publishsettings* dosyasını seçin ve **Aç**' a tıklayın. Sihirbaz, doldurulmuş tüm alanlarla bağlantı sekmesine ilerler.

![Web 'i Yayımlama Sihirbazı bağlantı sekmesi](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image26.png)

. Publishsettings dosyası, site için planlı kalıcı URL 'yi hedef URL kutusuna koyar, ancak bu etki alanını henüz satın almadıysanız değeri geçici URL ile değiştirin. Bu örnekte, URL  *[http://contosouniversity.com.vserver01.cytanium.com](http://contosouniversity.com.vserver01.cytanium.com).* Bu kutunun tek amacı, tarayıcının dağıtımdan sonra başarıyla sonra otomatik olarak açılacağı URL 'YI belirtmektir. Boş bırakırsanız, tek sonuç tarayıcının dağıtımdan sonra otomatik olarak başlamasıdır.

Ayarların doğru olduğundan ve sunucuya bağlanabildiğinizi doğrulamak için **bağlantıyı doğrula** ' ya tıklayın. Daha önce gördüğünüz gibi yeşil onay işareti, bağlantının başarılı olduğunu doğrular.

Bağlantıyı doğrula ' ya tıkladığınızda bir **sertifika hatası** iletişim kutusu görebilirsiniz. Bunu yaparsanız sunucu adının beklediğiniz şekilde olduğunu doğrulayın. Bu ise, **sonraki Visual Studio oturumları için bu sertifikayı Kaydet** ' i seçin ve **kabul et**' e tıklayın. (Bu hata, barındırma sağlayıcısının, dağıttığınız URL için bir SSL sertifikası satın alma masrafına engel olarak seçtiği anlamına gelir. Geçerli bir sertifika kullanarak güvenli bir bağlantı kurmayı tercih ediyorsanız, barındırma sağlayıcınızla görüşün.)

![Sertifika hatası](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image27.png)

**İleri**'ye tıklayın.

**Ayarlar** sekmesinin **veritabanları** bölümünde, test yayımlama profili için girdiğiniz değerleri girin. Açılan listelerde ihtiyacınız olan bağlantı dizelerini bulacaksınız.

- SchoolContext için bağlantı dizesi kutusunda `Data Source=|DataDirectory|School-Prod.sdf` **' yi** seçin.
- **SchoolContext**altında **Code First Migrations Uygula**' yı seçin.
- **DefaultConnection**bağlantı dizesi kutusunda `Data Source=|DataDirectory|aspnet-Prod.sdf` ' yi seçin.
- **DefaultConnection**altında **güncelleştirme veritabanını** temizlenmiş olarak bırakın.

![Web 'i Yayımlama Sihirbazı ayarları sekmesi](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image28.png)

**İleri**'ye tıklayın.

Kopyalanacak dosyaların listesini görmek için **Önizleme** sekmesinde **önizlemeyi Başlat** ' a tıklayın. Yerel bilgisayarda IIS 'e dağıtırken daha önce gördüğünüz listeyi görürsünüz.

Yayımlamadan önce, Web. Production. config dönüştürme dosyanızın uygulanacağı şekilde profilin adını değiştirin. **Profil** sekmesini seçin ve **profilleri Yönet**' e tıklayın.

![Web 'i Yayımlama Sihirbazı Profilleri yönetme](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image29.png)

**Web yayımlama profillerini Düzenle** iletişim kutusunda, üretim profilini seçin, **Yeniden Adlandır**' a tıklayın ve profil adını üretim olarak değiştirin. Ardından **Kapat**' a tıklayın.

![Web yayımlama profillerini Düzenle iletişim kutusu](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image30.png)

**Yayımla**' ya tıklayın.

Uygulama barındırma sağlayıcısına yayımlanır. Sonuç, **Çıkış** penceresinde gösterilir.

![Dağıtımdan sonra çıkış penceresi](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image31.png)

Tarayıcı, **Web 'ı Yayımla** sihirbazının **bağlantı** sekmesinde, **hedef URL** kutusunda girdiğiniz URL 'ye otomatik olarak açılır. Artık başlık çubuğunda "(test)" veya "(dev)" ortam göstergesi olmadığı sürece, siteyi Visual Studio 'da çalıştırdığınızda aynı giriş sayfasını görürsünüz. Bu, ortam göstergesi *Web. config* dönüşümünün doğru şekilde çalıştığını gösterir.

> [!NOTE]
> Başlıkta "(test)" görüyorsanız, Contosoüniversitesi projesinden *obj* klasörünü silin ve yeniden dağıtın. Yazılımın yayın öncesi sürümlerinde, daha önce uygulanan dönüştürme dosyası (Web. test. config), üretim profilini kullanıyor olsanız da yeniden uygulanabilir.

[![Home_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image33.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image32.png)

Veritabanı erişimine neden olan bir sayfayı çalıştırmadan önce, ELMAH 'nin oluşan hataları günlüğe kaydedebilmesini sağlayın.

## <a name="setting-folder-permissions-for-elmah"></a>ELMAH için klasör Izinlerini ayarlama

Bu serideki önceki öğreticiden hatırlamanız sırasında, uygulamanızın uygulamanızdaki klasör için yazma izinlerine sahip olduğundan emin olmanız gerekir ve bu, ELMAH hata günlüğü dosyalarını depolar. Bilgisayarınızda yerel olarak IIS 'ye dağıtıldığında, bu izinleri el ile ayarlarsınız. Bu bölümde, Cytanium adresinde nasıl izin ayarlanacağını göreceksiniz. (Bazı barındırma sağlayıcıları bunu sizin için etkinleştiremeyebilir; yazma izinlerine sahip bir veya daha fazla önceden tanımlanmış klasör sunabilir. Bu durumda, uygulamanızı belirtilen klasörleri kullanacak şekilde değiştirmeniz gerekir.)

Cytanium Denetim Masası 'nda klasör izinlerini ayarlayabilirsiniz. Denetim Masası URL 'sine gidin ve **Dosya Yöneticisi**' ni seçin.

[![Cytanium_Control_Panel_with_File_Manager_selected](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image35.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image34.png)

**Dosya Yöneticisi** kutusunda **contosouniversity.com** ve ardından **Wwwroot** ' ı seçerek uygulamanın kök klasörünü görüntüleyin. **ELMAH**' ın yanındaki asma kilit simgesine tıklayın.

[![Cytanium_Control_Panel_File_Manager_at_root_folder](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image37.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image36.png)

**Dosya**/**klasör izinleri** penceresinde, **contosouniversity.com** için **okuma** ve **yazma** onay kutularını seçin ve **izinleri ayarla**' ya tıklayın.

[![Cytanium_Control_Panel_File_Folder_Permissions_Elmah](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image39.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image38.png)

ELMAH 'nin, bir hataya neden olacak ve ardından ELMAH hata raporunu görüntüleyerek *ELMAH* klasörüne yazma erişimi olduğundan emin olun. *Studentsxxx. aspx*gibi GEÇERSIZ bir URL isteyin. Daha önce olduğu gibi, *Genericerrorpage. aspx* sayfasını görürsünüz. **Günlüğe kaydet** bağlantısına tıklayın ve ardından *ELMAH. axd*' yi çalıştırın. Önce, *Web. config* dönüştürmesinin ELMAH yetkilendirmesini başarıyla eklediğini doğrulayan bir **oturum açma** sayfası alırsınız. Oturum açtıktan sonra, yaptığınız hatayı gösteren raporu görürsünüz.

[ELMAH. axd_Prod ![](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image41.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image40.png)

## <a name="testing-in-the-production-environment"></a>Üretim ortamında test etme

**Öğrenciler** sayfasını çalıştırın. Uygulama, okul veritabanına ilk kez erişmeyi dener, bu da veritabanını oluşturmak için Code First Migrations tetikler. Sayfa bir süre gecikmeden sonra görüntülendiğinde, öğrenci olmadığını gösterir.

[![Students_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image43.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image42.png)

Çekirdek verilerinin, eğitmen verilerini veritabanına başarıyla eklendiğini doğrulamak için **eğitmenler** sayfasını çalıştırın.

[![Instructors_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image45.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image44.png)

Test ortamında yaptığınız gibi, veritabanı güncelleştirmelerinin üretim ortamında çalıştığını doğrulamak istersiniz, ancak genellikle üretim veritabanınıza test verileri girmek istemezsiniz. Bu öğreticide, test içinde yaptığınız aynı yöntemi kullanacaksınız. Ancak gerçek bir uygulamada, veritabanı güncelleştirmelerinin test verileri üretim veritabanına girmeden başarılı olduğunu doğrulayan bir yöntem bulmak isteyebilirsiniz. Bazı uygulamalarda, bir şeyi eklemek ve ardından silmek pratik olabilir.

Veritabanındaki verileri güncelleştirebildiğinizi doğrulamak için bir öğrenci ekleyin ve ardından **öğrenciler** sayfasına girdiğiniz verileri görüntüleyin.

[![Add_Students_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image47.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image46.png)

[![Students_page_with_new_student_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image49.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image48.png)

**Kurslar** menüsünden **kredileri Güncelleştir** ' i seçerek yetkilendirme kurallarının doğru çalıştığını doğrulayın. **Oturum açma** sayfası görüntülenir. Yönetici hesabı kimlik bilgilerinizi girin, **oturum aç**' a tıklayın ve **kredileri güncelleştirme** sayfası görüntülenir.

[![Log_In_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image51.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image50.png)

Oturum açma başarılı olursa **kredileri güncelleştirme** sayfası görüntülenir. Bu, ASP.NET üyelik veritabanının (tek yönetici hesabıyla) başarıyla dağıtıldığını gösterir.

[![Update_Credits_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image53.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image52.png)

Artık sitenizi başarıyla dağıtmış ve test ettiğiniz için Internet üzerinden genel kullanıma sunuldu.

## <a name="creating-a-more-reliable-test-environment"></a>Daha güvenilir bir test ortamı oluşturma

[Sınama ortamına dağıtım](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) öğreticisinde açıklandığı gibi, en güvenilir test ortamı, barındırma sağlayıcısında üretim hesabı gibi ikinci bir hesap olacaktır. İkinci bir barındırma hesabına kaydolmanız gerektiğinden, bu, test ortamınız olarak yerel IIS kullanmaktan daha pahalıdır. Ancak üretim sitesi hatalarını veya kesintilerini engelliyorsa, maliyete değer olarak karar verebilirsiniz.

Test hesabına oluşturma ve dağıtma sürecinin çoğu, üretime dağıtmak için yapmış olduğunuz şeydir.

- *Web. config* dönüşüm dosyası oluşturun.
- Barındırma sağlayıcısında bir hesap oluşturun.
- Yeni bir yayımlama profili oluşturun ve test hesabına dağıtın.

### <a name="preventing-public-access-to-the-test-site"></a>Test sitesine genel erişimi önler

Sınama hesabı için önemli bir göz önünde bulundurulmalıdır, ancak bu, genel kullanıma açık olmasını istemezsiniz. Siteyi özel tutmak için aşağıdaki yöntemlerden birini veya daha fazlasını kullanabilirsiniz:

- Test sitesine yalnızca test için kullandığınız IP adreslerinden erişime izin veren güvenlik duvarı kuralları ayarlamak için barındırma sağlayıcısına başvurun.
- URL 'yi, ortak sitenin URL 'sine benzemez olacak şekilde gizleme.
- Arama altyapısının test sitesi üzerinde gezinmemesini sağlamak ve arama sonuçlarında buna rapor bağlantıları bildirmek için bir *robots. txt* dosyası kullanın.

Bu yöntemlerin ilki, en güvenli seçenektir, ancak bu yordam, her barındırma sağlayıcısına özeldir ve bu öğreticide ele alınmeyecektir. Yalnızca IP adresinizin sınama hesabı URL 'sine gözatmasına izin vermek için barındırma sağlayıcınızla düzenleme yaparsanız, bu arama motorları üzerinde gezinmenize gerek kalmaz. Bu durumda bile, bir *robots. txt* dosyasının dağıtımı, güvenlik duvarı kuralının yanlışlıkla kapalı olması durumunda yedekleme olarak iyi bir fikirdir.

*Robots. txt* dosyası proje klasörünüze gider ve içinde aşağıdaki metin olmalıdır:

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/samples/sample1.cmd)]

`User-agent` satırı, arama motorlarına dosyadaki kuralların tüm arama motoru web gezginlerine (robots) uygulanacağını ve `Disallow` satırı, sitedeki hiçbir sayfanın gezilmeyeceğini belirtir.

Büyük olasılıkla, arama altyapılarınızın üretim sitenizi kataloglanmasını istiyorsanız, bu dosyayı üretim dağıtımından hariç bırakmanız gerekir. Bunu yapmak için, bkz. [ASP.NET Web uygulaması proje DAĞıTıMı SSS](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment)' de, **belirli dosyaları veya klasörleri dağıtımdan nasıl dışlayabilir?** Dışlamasını yalnızca üretim yayımlama profili için belirttiğinizden emin olun.

İkinci bir barındırma hesabı oluşturmak, gerekli olmayan bir test ortamı ile çalışmaya yönelik bir yaklaşımdır ancak eklenen ücretle ilgili olabilir. Aşağıdaki öğreticilerde, IIS 'yi test ortamınız olarak kullanmaya devam edersiniz.

Sonraki öğreticide, uygulama kodunu güncelleştirecek ve yaptığınız değişikliği test ve üretim ortamlarına dağıtırsınız.

> [!div class="step-by-step"]
> [Önceki](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)
> [İleri](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
