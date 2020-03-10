---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
title: 'Visual Studio kullanarak ASP.NET Web dağıtımı: üretime dağıtma | Microsoft Docs'
author: tdykstra
description: Bu öğretici serisi, bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf bir barındırma sağlayıcısına, usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 416438a1-3b2f-4d27-bf53-6b76223c33bf
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
msc.type: authoredcontent
ms.openlocfilehash: ddc3d15f0436c4c3a24491cf0377111768da67df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78632785"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-to-production"></a>Visual Studio kullanarak ASP.NET Web dağıtımı: üretime dağıtma

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Başlatıcı projesi indir](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> Bu öğretici serisi, Visual Studio 2012 veya Visual Studio 2010 kullanarak bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf barındırma sağlayıcısına dağıtmayı (yayımlamayı) gösterir. Seriler hakkında daha fazla bilgi için, [serideki ilk öğreticiye](introduction.md)bakın.

## <a name="overview"></a>Genel bakış

Bu öğreticide, bir Microsoft Azure hesabı ayarlarsınız, hazırlık ve üretim ortamları oluşturursunuz ve Visual Studio tek tıklamayla Yayımla özelliğini kullanarak ASP.NET Web uygulamanızı hazırlama ve üretim ortamlarına dağıtırsınız.

İsterseniz, üçüncü taraf bir barındırma sağlayıcısına dağıtım yapabilirsiniz. Bu öğreticide açıklanan yordamların çoğu, bir barındırma sağlayıcısı veya Azure için aynıdır, ancak her sağlayıcının hesap ve Web sitesi yönetimi için kendi kullanıcı arabirimi vardır. Microsoft.com Web sitesindeki [sağlayıcılar galerisinde](https://www.microsoft.com/web/hosting) bir barındırma sağlayıcısı bulabilirsiniz.

Anımsatıcı: bir hata iletisi alırsanız veya öğreticide ilerlediğinizden bir şey çalışmadıysanız, bu öğretici serisinde sorun giderme sayfasını kontrol ettiğinizden emin olun.

## <a name="get-a-microsoft-azure-account"></a>Microsoft Azure hesabı alın

Henüz bir Azure hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).

## <a name="create-a-staging-environment"></a>Hazırlama ortamı oluşturma

> [!NOTE]
> Bu öğretici yazıldığı için Azure App Service, hazırlama ve üretim ortamları oluşturmaya yönelik birçok işlemi otomatik hale getirmek üzere yeni bir özellik eklemiştir. Bkz. [Azure App Service Web Apps için hazırlama ortamlarını ayarlama](https://azure.microsoft.com/documentation/articles/web-sites-staged-publishing/).

[Test ortamında dağıtma öğreticisinde](deploying-to-iis.md)açıklandığı gibi, en güvenilir test ortamı, barındırma sağlayıcıdaki üretim web sitesi gibi bir Web sitesidir. Birçok barındırma sağlayıcısında bunun avantajlarına önemli ölçüde ek ücret elde etmeniz gerekir, ancak Azure 'da hazırlama uygulamanız olarak ek bir ücretsiz Web uygulaması oluşturabilirsiniz. Ayrıca bir veritabanına ihtiyacınız vardır ve üretim veritabanınızın masrafına göre daha fazla harcama yoktur. Azure 'da, her veritabanı için yerine kullandığınız veritabanı depolama alanı miktarına göre ödeme yaparsınız ve hazırlama sırasında kullanacağınız ek depolama miktarı en az olacaktır.

[Test ortamında dağıtma öğreticisinde](deploying-to-iis.md)açıklandığı gibi, hazırlama ve üretim bölümünde, iki veritabanınızı tek bir veritabanında dağıtacaksınız. Bunları ayrı tutmak isterseniz, her ortam için ek bir veritabanı oluşturmanız ve yayımlama profilini oluştururken her veritabanı için doğru hedef dizeyi seçmeniz dışında işlem aynı olur.

Öğreticinin bu bölümünde, hazırlama ortamı için kullanılacak bir Web uygulaması ve veritabanı oluşturacak ve üretim ortamına oluşturup dağıtmadan önce hazırlama ve test etme amacıyla dağıtım yapacaksınız.

> [!NOTE]
> Aşağıdaki adımlarda, Azure yönetim portalı 'nı kullanarak Azure App Service bir Web uygulamasının nasıl oluşturulacağı gösterilmektedir. Azure SDK 'sının en son sürümünde, Sunucu Gezgini kullanarak Visual Studio 'dan çıkmadan bunu da yapabilirsiniz. Visual Studio 2013, doğrudan Yayımla iletişim kutusundan bir Web uygulaması da oluşturabilirsiniz. Daha fazla bilgi için, bkz [. Azure App Service bir ASP.NET Web uygulaması oluşturma.](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)

1. [Azure yönetim portalı](https://manage.windowsazure.com/)' de, **Web siteleri**' ne ve ardından **Yeni**' ye tıklayın.
2. **Web sitesi**' ne ve ardından **özel oluştur**' a tıklayın.

    **Yeni Web sitesi-özel oluşturma** Sihirbazı açılır. **Özel oluşturma** Sihirbazı aynı anda bir Web sitesi ve bir veritabanı oluşturmanıza olanak sağlar.
3. Sihirbazın **Web sitesi oluştur** adımında, **URL** kutusuna uygulamanızın hazırlama ortamının benzersiz URL 'si olarak kullanılacak bir dize girin. Örneğin, contosouniversity-staging123 girin (Contosoüniversitesi 'nin hazırlanması için son sırada rastgele sayılar dahil olmak üzere).

    URL 'nin tamamı buraya girdiklerinize ve metin kutusunun yanında gördüğünüz sonekine sahip olacaktır.
4. **Bölge** açılan listesinde, size en yakın bölgeyi seçin.

    Bu ayar, Web uygulamanızın çalıştırılacağı veri merkezini belirtir.
5. **Veritabanı** açılan listesinde **Yeni bir SQL veritabanı oluştur**' u seçin.
6. **DB bağlantı dizesi adı** kutusunda varsayılan değer olan *DefaultConnection*' ı bırakın.
7. Kutunun altındaki sağ tarafına işaret eden oka tıklayın.

    Aşağıdaki çizimde, örnek değerlerle **Web sitesi oluştur** iletişim kutusu gösterilmektedir. Girdiğiniz URL ve bölge farklı olacaktır.

    ![Web sitesi adımı oluştur](deploying-to-production/_static/image1.png)

    Sihirbaz **veritabanı ayarlarını belirtin** adımına ilerletir.
8. **Ad** kutusuna *contosouniversity* Plus ile rastgele bir sayı girerek benzersiz hale getirin. Örneğin, *ContosoUniversity123*.
9. **Sunucu** kutusunda **Yeni SQL veritabanı sunucusu**' nu seçin.
10. Bir yönetici adı ve parola girin.

    Buraya mevcut bir ad ve parola girmemeniz gerekir. Daha sonra veritabanına eriştiğinizde kullanmak için şu anda tanımladığınız bir adı ve parolayı girersiniz.
11. **Bölge** kutusunda, Web uygulaması için seçtiğiniz bölgeyi seçin.

    Web sunucusu ve veritabanı sunucusunun aynı bölgede tutulması, size en iyi performansı sağlar ve giderleri en aza indirir.
12. Bittiğini göstermek için kutunun altındaki onay işaretine tıklayın.

    Aşağıdaki çizimde, örnek değerlerle birlikte **veritabanı ayarlarını belirtin** iletişim kutusu gösterilmektedir. Girdiğiniz değerler farklı olabilir.

    ![Yeni Web sitesinin veritabanı ayarları adımı-veritabanı ile oluşturma Sihirbazı](deploying-to-production/_static/image2.png)

    Yönetim Portalı Web siteleri sayfasına döner ve **durum** sütunu Web uygulamasının oluşturulduğunu gösterir. Bir süre sonra (genellikle bir dakikadan kısa bir süre), **durum** sütunu Web uygulamasının başarıyla oluşturulduğunu gösterir. Sol taraftaki Gezinti çubuğunda, hesabınızdaki Web uygulamalarının sayısı Web **siteleri** simgesinin yanında görünür ve **SQL veritabanları** simgesinin yanında veritabanı sayısı görüntülenir.

    ![Yönetim Portalı Web siteleri sayfası, Web sitesi oluşturuldu](deploying-to-production/_static/image3.png)

    Web uygulamanızın adı çizimdeki örnek uygulamadan farklı olacaktır.

## <a name="deploy-the-application-to-staging"></a>Hazırlama için uygulamayı dağıtma

Hazırlama ortamı için bir Web uygulaması ve veritabanı oluşturduğdığınıza göre, projeyi buna dağıtabilirsiniz.

> [!NOTE]
> Bu yönergelerde, yalnızca Azure için değil, üçüncü taraf barındırma sağlayıcıları için de kullanılabilen bir *. publishsettings* dosyasını indirerek bir yayımlama profili oluşturma işlemi gösterilmektedir. En son Azure SDK 'Sı, Visual Studio 'dan doğrudan Azure 'a bağlanmanızı ve Azure hesabınızda sahip olduğunuz Web Apps listesinden seçim yapmanızı de sağlar. Visual Studio 2013, **Web yayımlama** iletişim kutusundan veya **Sunucu Gezgini** penceresinden Azure 'da oturum açabilirsiniz. Daha fazla bilgi için, bkz. [Azure App Service bir ASP.NET Web uygulaması oluşturma](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).

### <a name="download-the-publishsettings-file"></a>. Publishsettings dosyasını indirin

1. Yeni oluşturduğunuz Web uygulamasının adına tıklayın.

    ![Panoya gitmek için siteye tıklayın](deploying-to-production/_static/image4.png)
2. **Pano** sekmesinde **Hızlı bakış** altında **Yayımlama profilini indir**' e tıklayın.

    ![Yayımlama profili bağlantısını indir](deploying-to-production/_static/image5.png)

    Bu adım, Web uygulamanıza bir uygulama dağıtmak için ihtiyacınız olan tüm ayarların bulunduğu bir dosyayı indirir. Bu dosyayı Visual Studio 'ya aktarırsınız, böylece bu bilgileri el ile girmeniz gerekmez.
3. *. Publishsettings* dosyasını Visual Studio 'dan erişebileceğiniz bir klasöre kaydedin.

    ![. publishsettings dosyası kaydediliyor](deploying-to-production/_static/image6.png)

    > [!WARNING]
    > Güvenlik- *. publishsettings* dosyası, Azure aboneliklerinizi ve hizmetlerinizi yönetmek için kullanılan kimlik bilgilerinizi (Kodlanmamış) içerir. Bu dosya için en iyi güvenlik uygulaması, kaynak dizinlerinizin dışında (örneğin, Kütüphanaries\belgeler klasöründe) geçici olarak depolanması ve içeri aktarma tamamlandıktan sonra onu silmektir. *. Publishsettings* dosyasına erişim sağlayan kötü niyetli bir Kullanıcı, Azure hizmetlerinizi düzenleyebilir, oluşturabilir ve silebilir.

### <a name="create-a-publish-profile"></a>Yayımlama profili oluşturma

1. Visual Studio 'da, **Çözüm Gezgini** ' de contosouniversity projesine sağ tıklayın ve bağlam menüsünden **Yayımla** ' yı seçin.

    **Web 'ı Yayımla** Sihirbazı açılır.
2. **Profil** sekmesine tıklayın.
3. **İçeri aktar**'a tıklayın.
4. Daha önce indirdiğiniz *. publishsettings* dosyasına gidin ve ardından **Aç**' a tıklayın.

    ![Yayımlama ayarlarını içeri aktar iletişim kutusu](deploying-to-production/_static/image7.png)
5. **Bağlantı** sekmesinde, ayarların doğru olduğundan emin olmak Için **bağlantıyı doğrula** ' ya tıklayın.

    Bağlantı doğrulandıktan sonra **bağlantıyı doğrula** düğmesinin yanında yeşil bir onay işareti görüntülenir.

    Bazı barındırma sağlayıcıları için **bağlantıyı doğrula**' ya tıkladığınızda bir **sertifika hatası** iletişim kutusu görebilirsiniz. Bunu yaparsanız sunucu adının beklediğiniz şekilde olduğunu doğrulayın. Sunucu adı doğruysa, **sonraki Visual Studio oturumları için bu sertifikayı Kaydet** ' i seçin ve **kabul et**' e tıklayın. (Bu hata, barındırma sağlayıcısının, dağıttığınız URL için bir SSL sertifikası satın alma masrafına engel olarak seçtiği anlamına gelir. Geçerli bir sertifika kullanarak güvenli bir bağlantı kurmayı tercih ediyorsanız, barındırma sağlayıcınızla görüşün.)
6. **İleri**'ye tıklayın.

    ![Bağlantı başarılı simgesi ve bağlantı sekmesinde Ileri düğmesi](deploying-to-production/_static/image8.png)
7. **Ayarlar** sekmesinde **dosya yayımlama seçenekleri**' ni genişletin ve ardından **uygulama\_verileri klasöründen dosyaları Dışla**' yı seçin.

    **Dosya yayımlama seçenekleri**altındaki diğer seçenekler hakkında daha fazla bilgi için bkz. [IIS 'e dağıtma](deploying-to-iis.md) öğreticisi. Bu adımın sonucunu gösteren ekran görüntüsü ve aşağıdaki veritabanı yapılandırma adımları veritabanı yapılandırma adımlarının sonunda bulunur.
8. **Veritabanları** bölümünde **DefaultConnection** ' ın altında, üyelik veritabanı için veritabanı dağıtımını yapılandırın.
9. 1. **Veritabanını güncelleştir**' i seçin.

        **DefaultConnection** 'ın doğrudan altındaki **uzak bağlantı dizesi** kutusu,. publishsettings dosyasındaki bağlantı dizesiyle doldurulur. Bağlantı dizesi, *. pubxml* dosyasında düz metin olarak depolanan SQL Server kimlik bilgilerini içerir. Bunları kalıcı olarak depolamamayı tercih ediyorsanız, veritabanı dağıtıldıktan sonra bunları yayımlama profilinden kaldırabilir ve bunun yerine Azure 'da saklayın. Daha fazla bilgi için, Scott Hanselman blogundan [kaynaktan Azure 'a dağıtım yaparken ASP.NET veritabanı bağlantı Dizelerinizin güvenliğini sağlama](http://www.hanselman.com/blog/HowToKeepYourASPNETDatabaseConnectionStringsSecureWhenDeployingToAzureFromSource.aspx) bölümüne bakın.
      2. **Veritabanı güncelleştirmelerini Yapılandır**öğesine tıklayın.
      3. **Veritabanı güncelleştirmelerini Yapılandır** ILETIŞIM kutusunda **SQL betiği Ekle**' ye tıklayın.
      4. **SQL betiği Ekle** kutusunda, çözüm klasöründe daha önce kaydettiğiniz *ASPNET-Data-prod. SQL* komut dosyasına gidin ve ardından **Aç**' a tıklayın.
      5. **Veritabanı güncelleştirmelerini Yapılandır** iletişim kutusunu kapatın.
10. **Veritabanları** bölümünde **SchoolContext** altında **Yürüt Code First Migrations (uygulama başlatma üzerinde çalışır)** öğesini seçin.

    Visual Studio `DbContext` sınıfları için **güncelleştirme veritabanı** yerine **yürütme Code First Migrations** görüntüler. `DbContext` bir sınıf kullanarak erişebileceğiniz bir veritabanını dağıtmak için geçiş yerine dbDacFx sağlayıcısını kullanmak istiyorsanız, bkz. [Code First veritabanını geçiş olmadan dağıtma nasıl yaparım?](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) , MSDN 'de Visual Studio ve ASP.net Için Web dağıtımı hakkında SSS.

    **Ayarlar** sekmesi artık aşağıdaki örneğe benzer şekilde görünür:

    ![Hazırlama için ayarlar sekmesi](deploying-to-production/_static/image9.png)
11. Profili kaydetmek ve *hazırlık*olarak yeniden adlandırmak için aşağıdaki adımları gerçekleştirin:

    1. **Profil** sekmesine tıklayın ve ardından **profilleri Yönet**' e tıklayın.
    2. İçeri aktarma, biri FTP ve diğeri Web Dağıtımı için olmak üzere iki yeni profil oluşturdu. Web Dağıtımı profilini yapılandırdınız: Bu profili *hazırlama*olarak yeniden adlandırın.

        ![Profili hazırlama olarak yeniden adlandır](deploying-to-production/_static/image10.png)
    3. **Web yayımlama profillerini Düzenle** iletişim kutusunu kapatın.
    4. Web 'i **Yayımla** sihirbazını kapatın.

### <a name="configure-a-publish-profile-transform-for-the-environment-indicator"></a>Ortam göstergesi için bir yayımlama profili dönüşümü yapılandırma

> [!NOTE]
> Bu bölüm, ortam göstergesi için bir Web. config dönüşümünü nasıl ayarlayabileceğinizi gösterir. Gösterge `<appSettings>` öğesinde olduğundan, Azure App Service dağıtmaya çalışırken dönüştürmeyi belirtmeye yönelik başka bir alternatiftir. Daha fazla bilgi için bkz. [Azure 'Da Web. config ayarlarını belirtme](web-config-transformations.md#watransforms).

1. **Çözüm Gezgini**, **Özellikler**' i genişletin ve ardından **publishprofiles**' ı genişletin.
2. *Hazırlama. pubxml*öğesine sağ tıklayın ve ardından **yapılandırma dönüşümü Ekle**' ye tıklayın.

    ![Hazırlama için yapılandırma dönüşümü Ekle](deploying-to-production/_static/image11.png)

    Visual Studio *Web. hazırlama. config* dönüştürme dosyasını oluşturur ve açar.
3. *Web. hazırlama. config* dönüştürme dosyasında, açma `configuration` etiketinden hemen sonra aşağıdaki kodu ekleyin.

    [!code-xml[Main](deploying-to-production/samples/sample1.xml)]

    Hazırlama yayımlama profilini kullandığınızda, bu dönüşüm ortam göstergesini "üretim" olarak ayarlar. Dağıtılan Web uygulamasında "Contoso Üniversitesi" H1 başlığından sonra "(dev)" veya "(test)" gibi herhangi bir sonek görmezsiniz.
4. *Web. hazırlama. config* dosyasına sağ tıklayın ve **dönüştürme önizlemesi** ' ne tıklayarak kodlandığı dönüştürmenin beklenen değişiklikleri ürettiğinden emin olun.

    **Web. config önizleme** penceresinde hem *Web. Release. config* dönüştürmeleri hem de *Web. basamaklandırma. config* dönüştürmelerini uygulamanın sonucu gösterilir.

### <a name="prevent-public-use-of-the-test-app"></a>Test uygulamasının genel kullanımını engelle

Hazırlama uygulaması için önemli bir göz önünde bulundurulmasının Internet 'te etkin olması, ancak genel kullanıma açık olmasını istemezsiniz. Kişilerin bunu bulmasını ve kullanmasını olasılığını en aza indirmek için aşağıdaki yöntemlerden birini veya daha fazlasını kullanabilirsiniz:

- Hazırlama uygulamasına erişime izin veren güvenlik duvarı kurallarını, yalnızca hazırlama testi için kullandığınız IP adreslerinden erişim izni verecek şekilde ayarlayın.
- Tahmin edilmesi imkansız olabilecek bir karıştırılmış URL kullanın.
- Arama altyapısının test uygulaması üzerinde gezinmemesini ve arama sonuçlarında Bu rapor bağlantılarını rapor aramasını sağlamak için bir *robots. txt* dosyası oluşturun.

Bu yöntemlerin ilki en etkilidir, ancak bu öğreticide kapsamında değildir, çünkü Azure App Service yerine bir Azure bulut hizmetine dağıtmanız gerekir. Azure 'da Cloud Services ve IP kısıtlamaları hakkında daha fazla bilgi için bkz. [Azure tarafından sunulan Işlem barındırma seçenekleri](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me) ve [belirli IP adreslerinin bir Web rolüne erişimini engelleyin](https://msdn.microsoft.com/library/windowsazure/jj154098.aspx). Üçüncü taraf bir barındırma sağlayıcısına dağıtıyorsanız, IP kısıtlamalarının nasıl uygulanacağını öğrenmek için sağlayıcıya başvurun.

Bu öğretici için bir *robots. txt* dosyası oluşturacaksınız.

1. **Çözüm Gezgini**, contosouniversity projesine sağ tıklayın ve **Yeni öğe Ekle**' ye tıklayın.
2. *Robots. txt*adlı yeni bir **metin dosyası** oluşturun ve aşağıdaki metni içine yerleştirin:

    [!code-console[Main](deploying-to-production/samples/sample2.cmd)]

    `User-agent` satırı, arama motorlarına dosyadaki kuralların tüm arama motoru web gezginlerine (robots) uygulanacağını ve `Disallow` satırı, sitedeki hiçbir sayfanın gezilmeyeceğini belirtir.

    Arama altyapılarının üretim uygulamanızı kataloglanmasını istiyorsanız, bu dosyayı üretim dağıtımından hariç bırakmanız gerekir. Bunu yapmak için, oluşturma sırasında üretim yayımlama profilinde bir ayar yapılandırırsınız.

### <a name="deploy-to-staging"></a>Hazırlık ortamına dağıtma

1. Contoso Üniversitesi projesine sağ tıklayıp **Yayımla**' ya tıklayarak **Web 'i Yayımla** Sihirbazı ' nı açın.
2. **Hazırlama** profilinin seçili olduğundan emin olun.
3. **Yayımla**’ta tıklayın.

    **Çıkış** penceresinde hangi dağıtım eylemlerinin alındığı ve dağıtımın başarılı bir şekilde tamamlandığını raporlayan görüntülenir. Varsayılan tarayıcı, dağıtılan Web uygulamasının URL 'SI için otomatik olarak açılır.

## <a name="test-in-the-staging-environment"></a>Hazırlama ortamında test etme

Ortam göstergesinin, ortam göstergesinin *Web. config* dönüştürmesinin başarılı olduğunu gösteren H1 başlığından sonra "(test)" veya "(dev)" olmadığına dikkat edin.

![Ana sayfa hazırlama](deploying-to-production/_static/image12.png)

Dağıtılan veritabanının öğrenci olmadığını doğrulamak için **öğrenciler** sayfasını çalıştırın.

Code First, veritabanını eğitmen verileriyle birlikte içerdiğini doğrulamak için **eğitmenler** sayfasını çalıştırın:

**Öğrenciler menüsünde** **öğrencileri Ekle** ' yi seçin, bir öğrenci ekleyin ve ardından **öğrenciler** sayfasında yeni öğrenci 'yi görüntüleyerek veritabanına başarıyla yazabildiğinizi doğrulayın.

**Kurslar** sayfasından **kredileri Güncelleştir**' e tıklayın. **Kredilerin güncelleştirilmesi** sayfasında yönetici izinleri olması gerekir, bu nedenle **oturum açma** sayfası görüntülenir. Daha önce oluşturduğunuz yönetici hesabı kimlik bilgilerini girin ("admin" ve "prodpwd"). **Kredileri güncelleştirme** sayfası görüntülenir ve bu, önceki öğreticide oluşturduğunuz yönetici hesabının test ortamına doğru şekilde dağıtıldığını doğrular.

ELMAH 'nin takip eden bir hataya yol açmaya yönelik geçersiz bir URL isteyin ve ardından ELMAH hata raporunu isteyin. Üçüncü taraf bir barındırma sağlayıcısına dağıtıyorsanız, büyük olasılıkla raporun boş olduğunu bir önceki öğreticide aynı nedenle görürsünüz. ELMAH 'in günlük klasörüne yazmasını sağlamak üzere klasör izinlerini yapılandırmak için barındırma sağlayıcısının hesap yönetim araçlarını kullanmanız gerekir.

Oluşturduğunuz uygulama, artık üretimde kullanacağınız gibi bir Web uygulamasında bulutta çalışmaktadır. Her şey doğru şekilde çalıştığı için, bir sonraki adım üretime dağıtılmaktır.

## <a name="deploy-to-production"></a>Üretime dağıtma

Üretim Web uygulaması oluşturma ve üretime dağıtma işlemi, *robots. txt* dosyasını dağıtımdan hariç tutmaktan emin olmanız dışında, hazırlama için de aynıdır. Bunu yapmak için, yayımlama profili dosyasını düzenlersiniz.

### <a name="create-the-production-environment-and-the-production-publish-profile"></a>Üretim ortamı ve üretim yayımlama profili oluşturma

1. Hazırlama için kullandığınız yordamın aynısını izleyerek Azure 'da üretim Web uygulamasını ve veritabanını oluşturun.

    Veritabanını oluştururken, daha önce oluşturduğunuz sunucuya ya da yeni bir sunucu oluşturabilirsiniz.
2. *. Publishsettings* dosyasını indirin.
3. Hazırlama için kullandığınız yordamın aynısını izleyerek Production *. publishsettings* dosyasını içe aktararak yayımlama profili oluşturun.

    **Ayarlar** sekmesinin **veritabanları** bölümünde, **DefaultConnection** altında veri dağıtım betiğini yapılandırmayı unutmayın.
4. Yayımla profilini *Üretim*olarak yeniden adlandırın.
5. Hazırlama için kullandığınız yordamın aynısını izleyerek ortam göstergesi için bir yayımlama profili dönüştürmesi yapılandırın.

### <a name="edit-the-pubxml-file-to-exclude-robotstxt"></a>Robots. txt dosyasını dışlamak için. pubxml dosyasını düzenleyin

Yayımlama profili dosyaları &lt;ProfileName&gt; *. pubxml* olarak adlandırılır ve *publishprofiles* klasöründe bulunur. *Publishprofiles* klasörü, bir Web uygulaması projesindeki *Özellikler* KLASÖRÜNÜN C# altında, bir vb Web uygulaması projesindeki *projem* klasörü altında veya bir Web uygulaması projesindeki *uygulama\_veri* klasörü altında bulunur. Her *. pubxml* dosyası, tek bir yayımlama profili için uygulanan ayarları içerir. Web 'i Yayımla sihirbazında girdiğiniz değerler bu dosyalarda depolanır ve Visual Studio Kullanıcı arabiriminde kullanılabilir olmayan ayarları oluşturmak veya değiştirmek için bunları düzenleyebilirsiniz.

Varsayılan olarak, *. pubxml* dosyaları bir yayımlama profili oluşturduğunuzda projeye dahil edilir, ancak bunları projeden hariç tutabilir ve Visual Studio bunları kullanmaya devam eder. Visual Studio, projeye dahil edilip edilmediğine bakılmaksızın *. pubxml* dosyaları Için *publishprofiles* klasörüne bakar.

Her *. pubxml* dosyası için bir *. pubxml. User* dosyası vardır. **Parolayı kaydet** seçeneğini belirlediyseniz ve varsayılan olarak projeden hariç tutulduğunda *. pubxml. User* dosyası şifrelenmiş parolayı içerir.

Bir *. pubxml* dosyası, belirli bir yayımlama profili ile ilgili ayarları içerir. Tüm profiller için uygulanan ayarları yapılandırmak istiyorsanız *. WPP. targets* dosyası oluşturabilirsiniz. Yapı işlemi bu dosyaları *. csproj* veya *. vbproj* proje dosyasına aktarır, böylelikle proje dosyasında yapılandırabileceğiniz ayarların çoğu bu dosyalarda yapılandırılabilir. *. Pubxml* dosyaları ve *. WPP. targets* dosyaları hakkında daha fazla bilgi Için bkz. [nasıl yapılır: Yayımlama profili (. Pubxml) dosyalarındaki dağıtım ayarlarını düzenleme ve Visual Studio Web projelerindeki. WPP. targets dosyası](https://msdn.microsoft.com/library/ff398069.aspx).

1. **Çözüm Gezgini**, **Özellikler** ' i genişletin ve **publishprofiles**' ı genişletin.
2. *Production. pubxml* öğesine sağ tıklayın ve **Aç**' a tıklayın.

    ![. Pubxml dosyasını açın](deploying-to-production/_static/image13.png)
3. *Production. pubxml* öğesine sağ tıklayın ve **Aç**' a tıklayın.
4. Kapanış `PropertyGroup` öğesinden hemen önce aşağıdaki satırları ekleyin:

    [!code-xml[Main](deploying-to-production/samples/sample3.xml)]

    . Pubxml dosyası artık aşağıdaki örneğe benzer şekilde görünür:

    [!code-xml[Main](deploying-to-production/samples/sample4.xml?highlight=18-20)]

    Dosya ve klasörlerin nasıl dışlanması hakkında daha fazla bilgi için, [bkz.](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment) **Visual Studio IÇIN Web DAĞıTıMı SSS ve** MSDN üzerinde ASP.net.

### <a name="deploy-to-production"></a>Üretime dağıtma

1. Web 'i **Yayımla** sihirbazını açın, **Üretim** yayımlama profili ' nin seçili olduğundan emin olun ve ardından **Önizleme** sekmesinde **önizlemeyi Başlat** ' a tıklayarak *robots. txt* dosyasının üretim uygulamasına kopyalanmadığını doğrulayın.

    ![Üretime yayımlanacak dosyaların önizlemesi](deploying-to-production/_static/image14.png)

    Kopyalanacak dosyaların listesini gözden geçirin. . *Aspx.cs*, *. aspx.Designer.cs*, *Master.cs*ve *Master.Designer.cs* dosyaları dahil olmak üzere tüm *. cs* dosyalarının atlanacağını görürsünüz. Bu kodun hepsi, *bin* klasöründe bulacağınız *contosouniversity. dll* ve *contosouniversity. pdb* dosyalarına derlendi. Uygulamayı çalıştırmak için yalnızca *. dll* gerekli olduğundan ve daha önce uygulamayı çalıştırmak için gereken dosyaların dağıtılması gerektiğinden, hedef ortama hiçbir *. cs* dosyası kopyalanmadı. *Obj* klasörü ve *contosouniversity. csproj* ve *. csproj. User* dosyaları aynı nedenle atlanacaktır.

    Üretim ortamına dağıtmak için **Yayımla** ' ya tıklayın.
2. Hazırlama için kullandığınız yordamın aynısını izleyerek üretim ortamında test edin.

    URL ve *robots. txt* dosyasının yokluğu dışında her şey hazırlama ile aynıdır.

## <a name="summary"></a>Özet

Web uygulamanızı başarıyla dağıtmış ve test ettiğiniz için, Internet üzerinden genel olarak kullanıma sunuldu.

![Ana Sayfa Üretimi](deploying-to-production/_static/image15.png)

Sonraki öğreticide, uygulama kodunu güncelleştireceksiniz ve değişikliği test, hazırlama ve üretim ortamlarına dağıtırsınız.

> [!NOTE]
> Uygulamanız üretim ortamında kullanımda olsa da bir kurtarma planı uygulamanız gerekir. Diğer bir deyişle, veritabanlarını üretim uygulamasından düzenli olarak güvenli bir depolama konumuna yedeklemeniz ve bu tür yedeklemelerin çeşitli nesilleri tutmanız gerekir. Veritabanını güncelleştirdiğinizde, değişiklikten hemen önce bir yedekleme kopyası oluşturmalısınız. Daha sonra, bir hata yaparsanız ve bunu üretime dağıtana kadar bulamadıysanız, veritabanını bozmadan önce bulunduğu duruma geri yükleyemezsiniz. Daha fazla bilgi için bkz. [Azure SQL Veritabanı Yedekleme ve Geri Yükleme](https://msdn.microsoft.com/library/windowsazure/jj650016.aspx).
> 
> 
> [!NOTE]
> Bu öğreticide, dağıttığınız SQL Server sürümü Azure SQL veritabanı. Dağıtım işlemi diğer SQL Server sürümlerine benzer olsa da, gerçek bir üretim uygulaması bazı senaryolarda Azure SQL veritabanı için özel kod gerektirebilir. Daha fazla bilgi için bkz. [Azure SQL veritabanı Ile çalışma](../../../../whitepapers/aspnet-data-access-content-map.md#ssdb) ve [SQL Server Ile Azure SQL veritabanı arasında seçim yapma](../../../../whitepapers/aspnet-data-access-content-map.md#ssdbchoosing).
> 
> [!div class="step-by-step"]
> [Önceki](setting-folder-permissions.md)
> [İleri](deploying-a-code-update.md)
