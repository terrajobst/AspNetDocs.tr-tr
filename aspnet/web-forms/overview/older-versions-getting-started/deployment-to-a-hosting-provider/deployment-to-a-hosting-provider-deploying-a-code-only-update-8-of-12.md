---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
title: 'Visual Studio veya Visual Web Developer kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: yalnızca kod güncelleştirme dağıtma-8/12 | Microsoft Docs'
author: tdykstra
description: Bu öğretici dizisinde, Visual Stu kullanarak bir SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesinin nasıl dağıtılacağı (yayımlanacağı) gösterilmektedir.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: ddf6252f-9413-4c0c-a360-2cef8d231717
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
msc.type: authoredcontent
ms.openlocfilehash: e4d094ef84a747c36ce05ddb0e3d1ce0391d5605
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78564409"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-code-only-update---8-of-12"></a>Visual Studio veya Visual Web Developer kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: yalnızca kod güncelleştirme dağıtımı-8/12

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Başlatıcı projesi indir](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> Bu öğretici serisi, Visual Studio 2012 RC veya Web için Visual Studio Express 2012 RC kullanarak SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesini dağıtmayı (yayımlamayı) gösterir. Ayrıca, Web yayımlama güncelleştirmesini yüklerseniz Visual Studio 2010 de kullanabilirsiniz. Seriye giriş için, [serideki ilk öğreticiye](deployment-to-a-hosting-provider-introduction-1-of-12.md)bakın.
> 
> Visual Studio 2012 RC yayımlandıktan sonra tanıtılan dağıtım özelliklerini gösteren bir öğretici için, SQL Server Compact dışındaki SQL Server sürümlerinin nasıl dağıtılacağını gösterir ve Web Apps Azure App Service nasıl dağıtılacağını gösterir. bkz. [Visual Studio kullanarak ASP.NET Web dağıtımı](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Genel bakış

İlk dağıtımdan sonra, Web sitenizi sürdürme ve Geliştirme çalışmanız devam eder ve uzun bir güncelleştirme dağıtmak isteyeceksiniz. Bu öğretici, uygulama kodunuza bir güncelleştirme dağıtma sürecinde size kılavuzluk sağlar. Bu güncelleştirme bir veritabanı değişikliği içermez; bir sonraki öğreticide veritabanı değişikliğini dağıtma hakkında ne farklılık olduğunu göreceksiniz.

Anımsatıcı: bir hata iletisi alırsanız veya öğreticide ilerlediyseniz bir şey çalışmadıysanız [sorun giderme sayfasını](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)kontrol ettiğinizden emin olun.

## <a name="making-a-code-change"></a>Kod değişikliği yapma

Uygulamanıza yönelik bir güncelleştirmeye yönelik basit bir örnek olarak, **eğitmenler** sayfasına seçili eğitmen tarafından bir kurs listesi ekleyin.

**Eğitmenler** sayfasını çalıştırırsanız, kılavuzda **seçim** bağlantıları olduğunu fark edeceksiniz, ancak satır arka planını gri bir şekilde çevirip başka hiçbir şey yapmayamazsınız.

[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)

Şimdi **Seç** bağlantısına tıklandığında çalışan kodu ekleyecek ve seçilen eğitmen tarafından bir kurs listesi görüntülemektedir.

*Eğitmenler. aspx*' te, **errormessagelabel** `Label` denetiminden hemen sonra aşağıdaki biçimlendirmeyi ekleyin:

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample1.aspx)]

Sayfayı çalıştırın ve bir eğitmen seçin. Bu eğitmenin bir kurs listesini görürsünüz.

[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)

## <a name="deploying-the-code-update-to-the-test-environment"></a>Kod güncelleştirmesini test ortamına dağıtma

Sınama ortamına dağıtım, tek tıklamayla yayımlamayı yeniden çalıştırmanın basit bir sorunudur. Bu işlemi daha hızlı hale getirmek için **Web 'ı tek tıklamayla Yayımla** araç çubuğunu kullanabilirsiniz.

**Görünüm** menüsünde **araç çubukları** ' nı ve ardından Web 'i **Yayımla ' yı**seçin.

![Selecting_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image5.png)

**Çözüm Gezgini**, contosouniversity projesini seçin.

**Web 'de Yayımla araç çubuğu ' na tıklayın** , **Test** yayımlama profilini seçin ve ardından **Web 'i Yayımla** ' ya tıklayın (sol ve sağ işaret eden oklu simge).

![Web_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image6.png)

Visual Studio, güncelleştirilmiş uygulamayı dağıtır ve tarayıcı otomatik olarak giriş sayfasına açılır. Eğitmenler sayfasını çalıştırın ve güncelleştirmenin başarıyla dağıtıldığını doğrulamak için bir eğitmen seçin.

[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)

Normal olarak, regresyon testi de yaparsınız (yani, yeni değişikliğin mevcut işlevselliği bozmadığından emin olmak için sitenin geri kalanını test edersiniz). Ancak bu öğreticide, bu adımı atlayıp güncelleştirmeyi üretime dağıtmaya devam edersiniz.

## <a name="preventing-redeployment-of-the-initial-database-state-to-production"></a>Ilk veritabanı durumunun üretime yeniden dağıtımı engelleniyor

Gerçek bir uygulamada, kullanıcılar ilk dağıtımınız sonrasında üretim siteniz ile etkileşim kurar ve veritabanları canlı verilerle doldurulur. Bu nedenle, üyelik veritabanını başlangıçtaki durumunda yeniden dağıtmak istemezsiniz, bu da tüm canlı verileri temizler. SQL Server Compact veritabanları *app\_Data* klasöründeki dosyalar olduğundan, *uygulama\_veri* klasöründeki dosyaların dağıtılmaması için dağıtım ayarlarını değiştirerek bunu engellemeniz gerekir.

ContosoUniversity projesi için **Proje özellikleri** penceresini açın ve **paketle/Yayımla Web** sekmesini seçin. **yapılandırma** açılan kutusunda **etkin (yayın)** veya **yayın** seçili olduğundan emin olun, **dosyaları uygulama\_verileri klasöründen hariç tut**' u seçin.

![Exclude_files_from_the_App_Data_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image9.png)

İleride bir hata ayıklama derlemesini dağıtmaya karar verirseniz, hata ayıklama oluşturma yapılandırması için aynı değişikliği yapmak iyi bir fikirdir: **yapılandırmayı** **Hata Ayıkla** olarak değiştirin ve ardından **uygulama\_veri klasöründen dosyaları Dışla**' yı seçin.

**Paketle/Yayımla Web** sekmesini kaydedin ve kapatın.

> [!NOTE] 
> 
> [!IMPORTANT]
> Yayımlama profilinizde seçili **Hedefteki ek dosyaları kaldırdığınızdan** emin olun. Bu seçeneği belirlerseniz, dağıtım işlemi, dağıtılan sitedeki verileri\_uygulamanızdaki veritabanlarını siler ve uygulama\_veri klasörünün kendisini siler.

## <a name="preventing-user-access-to-the-production-site-during-update"></a>Güncelleştirme sırasında üretim sitesine kullanıcı erişimini önler

Şimdi dağıttığınız değişiklik, tek bir sayfada basit bir değişiklik. Ancak bazen daha büyük değişiklikler dağıtırsınız ve bu durumda, bir Kullanıcı dağıtım tamamlanmadan önce bir sayfa isterse, site Strangely davranabilir. Bunu engellemek için, bir *uygulamayı çevrimdışı. htm dosyası\_* kullanabilirsiniz. App\_adlı bir dosyayı uygulamanızın kök klasöründe *çevrimdışı. htm* olarak YERLEŞTIRDIĞINIZDE, IIS bu dosyayı uygulamanızı çalıştırmak yerine otomatik olarak görüntüler. Bu nedenle, dağıtım sırasında erişimi engellemek için, *uygulamayı\_çevrimdışı. htm* dosyasını kök klasöre yerleştirip dağıtım sürecini çalıştırın ve ardından *uygulamayı çevrimdışı. htm\_* kaldırın.

**Çözüm Gezgini**, çözüme (projelerden birine değil) sağ tıklayın ve **yeni çözüm klasörü**' nü seçin.

![Creating_a_solution_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image10.png)

Klasörü *Solutionfiles*olarak adlandırın.

Yeni klasörde, *app\_offline. htm*ADLı bir HTML sayfası oluşturun. Mevcut içeriği aşağıdaki biçimlendirme ile değiştirin:

[!code-html[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample2.html)]

Bir FTP bağlantısı veya barındırma sağlayıcısının Denetim Masası 'ndaki **Dosya Yöneticisi** yardımcı programını kullanarak, *uygulamayı çevrimdışı. htm dosyasını\_* kopyalayabilirsiniz. Bu öğretici için **Dosya Yöneticisi**kullanacaksınız.

Denetim Masası 'nı açın ve [üretim ortamına dağıtma](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) öğreticisinde yaptığınız gibi **Dosya Yöneticisi** ' ni seçin. **Contosouniversity.com** ve ardından **Wwwroot** ' ı seçip uygulamanızın kök klasörüne gidin ve ardından **karşıya yükle**' ye tıklayın.

[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)

**Dosyayı karşıya yükle** iletişim kutusunda, *App\_offline. htm* dosyasını seçin ve ardından **karşıya yükle**' ye tıklayın.

[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)

Sitenizin URL 'sine gidin. *Uygulama\_çevrimdışı. htm* sayfasının giriş sayfanız yerine görüntülendiğini görürsünüz.

[![App_offline. htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)

Artık üretime dağıtmaya hazırsınız.

## <a name="deploying-the-code-update-to-the-production-environment"></a>Kod güncelleştirmesini üretim ortamına dağıtma

Web 'de **Yayımla** araç çubuğunda, **Üretim** yayımlama profilini seçin ve ardından **Web 'i Yayımla**' ya tıklayın.

Visual Studio, güncelleştirilmiş uygulamayı dağıtır ve tarayıcının sitenin giriş sayfasında açılmasını sağlar. *App\_offline. htm* dosyası görüntülenir. Başarılı dağıtımı doğrulamayı test etmeden önce, *app\_offline. htm* dosyasını kaldırmanız gerekir.

Denetim Masası 'ndaki **Dosya Yöneticisi** uygulamasına geri dönün. **Contosouniversity.com** ve **Wwwroot**' u seçin, **App\_offline. htm**öğesini seçin ve **Sil**' e tıklayın.

[![Deleting_app_offline. htm](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)

Tarayıcıda, ortak sitedeki eğitmenler sayfasını açın ve güncelleştirmenin başarıyla dağıtıldığını doğrulamak için bir eğitmen seçin.

[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)

Artık bir veritabanı değişikliği içermeyen bir uygulama güncelleştirmesi dağıttıysanız. Sonraki öğreticide, bir veritabanı değişikliğini dağıtma gösterilmektedir.

> [!div class="step-by-step"]
> [Önceki](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
> [İleri](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
