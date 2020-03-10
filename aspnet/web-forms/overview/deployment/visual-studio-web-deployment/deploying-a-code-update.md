---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
title: 'Visual Studio kullanarak ASP.NET Web dağıtımı: kod güncelleştirmesini dağıtma | Microsoft Docs'
author: tdykstra
description: Bu öğretici serisi, bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf bir barındırma sağlayıcısına, usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: c76dbc35-a914-4ee3-919c-4f4d1fa05104
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
msc.type: authoredcontent
ms.openlocfilehash: 3881833bfe2a50a38a357614f92f434a04a8ab08
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78567405"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-code-update"></a>Visual Studio kullanarak ASP.NET Web dağıtımı: kod güncelleştirmesi dağıtma

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Başlatıcı projesi indir](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> Bu öğretici serisi, Visual Studio 2012 veya Visual Studio 2010 kullanarak bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf barındırma sağlayıcısına dağıtmayı (yayımlamayı) gösterir. Seriler hakkında daha fazla bilgi için, [serideki ilk öğreticiye](introduction.md)bakın.

## <a name="overview"></a>Genel bakış

İlk dağıtımdan sonra, Web sitenizi sürdürme ve Geliştirme çalışmanız devam eder ve uzun bir güncelleştirme dağıtmak isteyeceksiniz. Bu öğretici, uygulama kodunuza bir güncelleştirme dağıtma sürecinde size kılavuzluk sağlar. Bu öğreticide uyguladığınız ve dağıttığınız güncelleştirme bir veritabanı değişikliği içermez; bir sonraki öğreticide veritabanı değişikliğini dağıtma hakkında ne farklılık olduğunu göreceksiniz.

Anımsatıcı: bir hata iletisi alırsanız veya öğreticide ilerlediyseniz bir şey çalışmadıysanız [sorun giderme sayfasını](troubleshooting.md)kontrol ettiğinizden emin olun.

## <a name="make-a-code-change"></a>Kod değişikliği yapma

Uygulamanıza yönelik bir güncelleştirmeye yönelik basit bir örnek olarak, **eğitmenler** sayfasına seçili eğitmen tarafından bir kurs listesi ekleyin.

**Eğitmenler** sayfasını çalıştırırsanız, kılavuzda **seçim** bağlantıları olduğunu fark edeceksiniz, ancak satır arka planını gri bir şekilde çevirip başka hiçbir şey yapmayamazsınız.

![Seçimle ilgili eğitmenler sayfası](deploying-a-code-update/_static/image1.png)

Şimdi **Seç** bağlantısına tıklandığında çalışan kodu ekleyecek ve seçilen eğitmen tarafından bir kurs listesi görüntülemektedir.

1. *Eğitmenler. aspx*' te, **errormessagelabel** `Label` denetiminden hemen sonra aşağıdaki biçimlendirmeyi ekleyin:

    [!code-aspx[Main](deploying-a-code-update/samples/sample1.aspx)]
2. Sayfayı çalıştırın ve bir eğitmen seçin. Bu eğitmenin bir kurs listesini görürsünüz.

    ![Kurslar ile eğitmenler sayfasında eğitim](deploying-a-code-update/_static/image2.png)
3. Tarayıcıyı kapatın.

## <a name="deploy-the-code-update-to-the-test-environment"></a>Kod güncelleştirmesini test ortamına dağıtma

Yayımlama profillerinizi test, hazırlama ve üretime dağıtmak üzere kullanabilmeniz için önce veritabanı yayımlama seçeneklerini değiştirmeniz gerekir. Artık üyelik veritabanı için verme ve veri dağıtım betikleri çalıştırmanız gerekmez.

1. ContosoUniversity projesine sağ tıklayıp **Yayımla**' ya tıklayarak **Web 'i Yayımla** Sihirbazı ' nı açın.
2. **Profil** açılır listesinden **Test** profili ' ne tıklayın.
3. **Ayarlar** sekmesine tıklayın.
4. **Veritabanları** bölümünde **DefaultConnection** ' ın altında **veritabanını güncelleştir** onay kutusunun işaretini kaldırın.
5. **Profil** sekmesine tıklayın ve ardından **profil** açılır listesinden **hazırlama** profili ' ne tıklayın.
6. **Test** profilinde yapılan değişiklikleri kaydetmek isteyip Istemediğiniz sorulduğunda **Evet**' e tıklayın.
7. Hazırlama profilinde aynı değişikliği yapın.
8. Üretim profilinde aynı değişikliği yapmak için işlemi tekrarlayın.
9. Web 'i **Yayımla** sihirbazını kapatın.

Sınama ortamına dağıtım artık tek tıklamayla yayımlamayı yeniden çalıştırmanın basit bir sorunudur. Bu işlemi daha hızlı hale getirmek için **Web 'ı tek tıklamayla Yayımla** araç çubuğunu kullanabilirsiniz.

1. **Görünüm** menüsünde **araç çubukları** ' nı ve ardından Web 'i **Yayımla ' yı**seçin.

    ![Selecting_One_Click_Publish_toolbar](deploying-a-code-update/_static/image3.png)
2. **Çözüm Gezgini**, contosouniversity projesini seçin.
3. **Web 'de Yayımla araç çubuğu ' na tıklayın** , **Test** yayımlama profilini seçin ve ardından **Web 'i Yayımla** ' ya tıklayın (sol ve sağ işaret eden oklu simge).

    ![Web_One_Click_Publish_toolbar](deploying-a-code-update/_static/image4.png)
4. Visual Studio, güncelleştirilmiş uygulamayı dağıtır ve tarayıcı otomatik olarak giriş sayfasına açılır.
5. Eğitmenler sayfasını çalıştırın ve güncelleştirmenin başarıyla dağıtıldığını doğrulamak için bir eğitmen seçin.

Normal olarak, regresyon testi de yaparsınız (yani, yeni değişikliğin mevcut işlevselliği bozmadığından emin olmak için sitenin geri kalanını test edersiniz). Ancak bu öğreticide, bu adımı atlayıp güncelleştirmeyi hazırlama ve üretime dağıtmaya devam edersiniz.

Yeniden dağıtırken, Web Dağıtımı hangi dosyaların değiştirildiğini otomatik olarak belirler ve yalnızca değiştirilen dosyaları sunucuya kopyalar. Web Dağıtımı, varsayılan olarak, hangilerinin değiştirildiğini anlamak için dosyalarda son değiştirme tarihlerini kullanır. Bazı kaynak denetim sistemleri, dosya içeriklerini değiştirmeseniz bile dosya tarihlerini değiştirir. Bu durumda, hangi dosyaların değiştirildiğini belirleyebilmek için dosya sağlama toplamlarını kullanmak üzere Web Dağıtımı yapılandırmak isteyebilirsiniz. Daha fazla bilgi için, bkz. ASP.NET dağıtımı SSS içinde, [Tüm dosyalarımı neden yeniden dağıtıldı?](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum)

## <a name="take-the-application-offline-during-deployment"></a>Dağıtım sırasında uygulamayı çevrimdışına alma

Şimdi dağıttığınız değişiklik, tek bir sayfada basit bir değişiklik. Ancak bazen daha büyük değişiklikler dağıtabilir veya hem kod hem de veritabanı değişikliklerini dağıtırsınız ve bir Kullanıcı, dağıtım tamamlanmadan önce bir sayfa istediğinde site yanlış davranabilir. Dağıtım devam ederken kullanıcıların siteye erişmesini engellemek için, bir *uygulamayı çevrimdışı. htm dosyası\_* kullanabilirsiniz. App\_adlı bir dosyayı uygulamanızın kök klasöründe *çevrimdışı. htm* olarak YERLEŞTIRDIĞINIZDE, IIS bu dosyayı uygulamanızı çalıştırmak yerine otomatik olarak görüntüler. Bu nedenle, dağıtım sırasında erişimi engellemek için, *uygulamayı\_çevrimdışı. htm* dosyasını kök klasöre yerleştirip dağıtım sürecini çalıştırın ve ardından uygulamayı başarılı bir şekilde yüklemeden sonra *çevrimdışı. htm\_* kaldırın.

Web Dağıtımı,\_otomatik olarak bir varsayılan *uygulamayı* sunucuya dağıtmaya başladığında ve bu dosyayı tamamlandığında kaldırdığınızda, bu dosyayı sunucusuna otomatik olarak koyabileceğiniz şekilde yapılandırabilirsiniz. Yapmanız gereken tek şey, yayımlama profili (. pubxml) dosyanıza aşağıdaki XML öğesini eklemektir:

[!code-xml[Main](deploying-a-code-update/samples/sample2.xml)]

Bu öğreticide, *çevrimdışı. htm dosyası\_* özel bir uygulama oluşturma ve kullanma hakkında bilgi edineceksiniz.

Hazırlama sitesine erişen kullanıcılarınız olmadığından, uygulamayı hazırlama sitesinde *çevrimdışı. htm\_* kullanmak gerekli değildir. Ancak her şeyi üretimde dağıtmayı planladığınız şekilde test etmek için hazırlama kullanmak iyi bir uygulamadır.

### <a name="create-app_offlinehtm"></a>Çevrimdışı. htm\_uygulama oluşturma

1. **Çözüm Gezgini**, çözüme sağ tıklayın ve **Ekle**' ye tıklayın ve ardından **Yeni öğe**' ye tıklayın.
2. *App\_offline. htm* adlı bir **HTML sayfası** oluşturun (varsayılan olarak Visual Studio 'nun oluşturduğu *. html* uzantısında son "l" ı silin).
3. Şablon işaretlemesini aşağıdaki biçimlendirme ile değiştirin:

    [!code-html[Main](deploying-a-code-update/samples/sample3.html)]
4. Dosyayı kaydedin ve kapatın.

### <a name="copy-app_offlinehtm-to-the-root-folder-of-the-web-site"></a>Uygulamayı çevrimdışı. htm\_Web sitesinin kök klasörüne kopyalayın

Web sitesine dosya kopyalamak için herhangi bir FTP aracını kullanabilirsiniz. [FileZilla](http://filezilla-project.org/) , popüler bir FTP aracıdır ve ekran görüntüleri içinde gösterilir.

FTP aracını kullanmak için üç şey gerekir: FTP URL 'SI, Kullanıcı adı ve parola.

URL, Azure Yönetim Portalı Web sitesinin Pano sayfasında gösterilir ve FTP için Kullanıcı adı ve parola, daha önce indirdiğiniz *. publishsettings* dosyasında bulunabilir. Aşağıdaki adımlarda bu değerlerin nasıl alınacağı gösterilmektedir.

1. Azure Yönetim Portalı ' de, **Web siteleri** sekmesi ' ne ve ardından hazırlama Web sitesine tıklayın.
2. **Pano** sayfasında, **Hızlı bakış** bölümünde FTP ana bilgisayar adını bulmak için aşağı kaydırın.

    ![FTP konak adı](deploying-a-code-update/_static/image5.png)
3. Hazırlama *. publishsettings* dosyasını Not defteri 'nde veya başka bir metin düzenleyicisinde açın.
4. FTP profili için `publishProfile` öğesini bulun.
5. `userName` ve `userPWD` değerlerini kopyalayın.

    ![FTP kimlik bilgileri](deploying-a-code-update/_static/image6.png)
6. FTP aracınızı açın ve FTP URL 'sinde oturum açın.
7. *App\_uygulamasını* çözüm klasöründen hazırlama sitesindeki */site/Wwwroot* klasörüne kopyalayın.

    ![App_offline Kopyala](deploying-a-code-update/_static/image7.png)
8. Hazırlama sitenizin URL 'sine gidin. *Uygulama\_çevrimdışı. htm* sayfasının giriş sayfanız yerine görüntülendiğini görürsünüz.

    ![tarayıcı penceresinde app_offline. htm](deploying-a-code-update/_static/image8.png)

Şimdi hazırlama işlemine dağıtmaya hazırsınız.

## <a name="deploy-the-code-update-to-staging-and-production"></a>Kod güncelleştirmesini hazırlama ve üretime dağıtma

1. Web 'de **Yayımla** araç çubuğunda, **hazırlama** yayımlama profilini seçin ve ardından **Web 'i Yayımla**' ya tıklayın.

    Visual Studio, güncelleştirilmiş uygulamayı dağıtır ve tarayıcının sitenin giriş sayfasında açılmasını sağlar. *App\_offline. htm* dosyası görüntülenir. Başarılı dağıtımı doğrulamayı test etmeden önce, *app\_offline. htm* dosyasını kaldırmanız gerekir.
2. FTP aracınızdan geri dönün ve uygulamayı hazırlama sitesinden **çevrimdışı. htm\_** silin.
3. Tarayıcıda, hazırlama sitesinde eğitmenler sayfasını açın ve güncelleştirmenin başarıyla dağıtıldığını doğrulamak için bir eğitmen seçin.
4. Hazırlama için yaptığınız gibi üretim için aynı yordamı izleyin.

<a id="specificfiles"></a>

## <a name="reviewing-changes-and-deploying-specific-files"></a>Değişiklikleri gözden geçirme ve belirli dosyaları dağıtma

Visual Studio 2012 ayrıca tek tek dosyaları dağıtmanıza olanak tanır. Seçili bir dosya için, yerel sürüm ile dağıtılan sürüm arasındaki farkları görüntüleyebilir, dosyayı hedef ortama dağıtabilir veya hedef ortamdaki dosyayı yerel projeye kopyalayabilirsiniz. Öğreticinin bu bölümünde, bu özelliklerin nasıl kullanılacağını görürsünüz.

### <a name="make-a-change-to-deploy"></a>Dağıtmak için bir değişiklik yapın

1. *Content/site. css*' yi açın ve `body` etiketinin bloğunu bulun.
2. `background-color` değerini `#fff` `darkblue`olarak değiştirin.

    [!code-css[Main](deploying-a-code-update/samples/sample4.css?highlight=2)]

### <a name="view-the-change-in-the-publish-preview-window"></a>Yayımlama önizlemesi penceresinde değişikliği görüntüleme

Projeyi yayımlamak için **Web 'ı Yayımla** Sihirbazı 'nı kullandığınızda, **Önizleme** penceresinde dosyaya çift tıklayarak hangi değişikliklerin yayımlanacak olduğunu görebilirsiniz.

1. ContosoUniversity projesine sağ tıklayın ve **Yayımla**' ya tıklayın.
2. **Profil** açılan listesinden, **Test** yayımlama profilini seçin.
3. **Önizleme**' ye ve ardından **önizlemeyi Başlat**' a tıklayın.
4. **Önizleme** bölmesinde, **site. css**' ye çift tıklayın.

    ![Site. css ' ye çift tıklayın](deploying-a-code-update/_static/image9.png)

    **Değişiklikleri Önizle** iletişim kutusu, dağıtılacak değişikliklerin önizlemesini gösterir.

    ![Site. css değişikliklerini Önizle](deploying-a-code-update/_static/image10.png)

    *Web. config* dosyasına çift tıklarsanız, **Değişiklikleri Önizle** iletişim kutusu derleme yapılandırma dönüştürmelerinizin ve yayımlama profili dönüştürmelerinin etkisini gösterir. Bu noktada, sunucuda *Web. config* dosyasının değişmesine neden olacak hiçbir şey gerçekleştirmedi, bu nedenle hiçbir değişiklik olmadığını görmeyi düşünüyorsunuz. Ancak, **Değişiklikleri Önizle** penceresi yanlış bir şekilde iki değişiklik gösterir. İki XML öğesi, kaldırılacak şekilde görünür. Bu öğeler, bir Code First bağlam sınıfı için **uygulama başlatıldığında Code First Migrations Çalıştır '** ı seçtiğinizde Yayımla işlemi tarafından eklenir. Karşılaştırma, yayımlama işlemi bu öğeleri eklemeden önce yapılır, bu nedenle kaldırılmasa da kaldırılmamaları gibi görünüyor. Bu hata gelecekteki bir sürümde düzeltilecektir.
5. **Kapat**'ı tıklatın.
6. **Yayımla**’ta tıklayın.
7. Tarayıcı, test sitesinin giriş sayfasında açıldığında, CSS değişikliğinin etkisini görmek için sabit yenilemeye yol açacak şekilde CTRL + F5 tuşlarına basın.

    ![CSS değişikliğinin etkisi](deploying-a-code-update/_static/image11.png)
8. Tarayıcıyı kapatın.

### <a name="publish-specific-files-from-solution-explorer"></a>Belirli dosyaları Çözüm Gezgini yayımlama

Mavi arka planı beğenmediğinizi ve orijinal renge dönmek istediğinizi varsayalım. Bu bölümde, belirli bir dosyayı doğrudan **Çözüm Gezgini**yayımlayarak özgün ayarları geri yükleyeceksiniz.

1. *Content/site. css* ' i açın ve `background-color` ayarını `#fff`geri yükleyin.
2. **Çözüm Gezgini**, *Content/site. css* dosyasına sağ tıklayın.

    Bağlam menüsünde üç yayımlama seçeneği gösterilir.

    ![Çözüm Gezgini seçenekleri yayımlama](deploying-a-code-update/_static/image12.png)
3. **Site. css değişikliklerini Önizle**' ye tıklayın.

    Yerel dosya ile hedef ortamdaki sürümü arasındaki farkları göstermek için bir pencere açılır.

    ![Diff-Content/site. css](deploying-a-code-update/_static/image13.png)
4. **Çözüm Gezgini**, **site. css** ' ye yeniden sağ tıklayıp site. **CSS Yayımla**' ya tıklayın.

    **Web yayımlama etkinliği** penceresi, dosyanın yayımlandığını gösterir.

    ![Web yayımlama etkinliği penceresi](deploying-a-code-update/_static/image14.png)
5. `http://localhost/contosouniversity` URL 'SI için bir tarayıcı açın ve ardından CTRL + F5 tuşlarına basarak CSS değişikliğinin etkisini görmek için bir sabit yenilemeye neden olması gerekir.

    ![Normal CSS ile ana sayfa](deploying-a-code-update/_static/image15.png)
6. Tarayıcıyı kapatın.

## <a name="summary"></a>Özet

Artık bir veritabanı değişikliği içermeyen bir uygulama güncelleştirmesi dağıtmanın birkaç yolunu gördünüz ve nelerin güncelleştirileceğini doğrulamak için değişikliklerin nasıl önizlendiğini gördünüz. Eğitmenler sayfasında şimdi bir **Kurslar taöğretme** bölümü vardır.

![Kurslar ile eğitmenler sayfasında eğitim](deploying-a-code-update/_static/image16.png)

Sonraki öğreticide bir veritabanı değişikliğini dağıtma gösterilmektedir: veritabanına ve eğitmenler sayfasına bir Doğum tarihi alanı ekleyeceksiniz.

> [!div class="step-by-step"]
> [Önceki](deploying-to-production.md)
> [İleri](deploying-a-database-update.md)
