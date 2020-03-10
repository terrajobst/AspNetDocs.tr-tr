---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
title: 'Visual Studio kullanarak ASP.NET Web dağıtımı: veritabanı güncelleştirmesi dağıtma | Microsoft Docs'
author: tdykstra
description: Bu öğretici serisi, bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf bir barındırma sağlayıcısına, usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 9cad0833-486a-4474-a7f3-7715542ec4ce
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
msc.type: authoredcontent
ms.openlocfilehash: 805eb84c24764cf921291f89054435601dbac48e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78547742"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-database-update"></a>Visual Studio kullanarak ASP.NET Web dağıtımı: veritabanı güncelleştirmesi dağıtma

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Başlatıcı projesi indir](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> Bu öğretici serisi, Visual Studio 2012 veya Visual Studio 2010 kullanarak bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf barındırma sağlayıcısına dağıtmayı (yayımlamayı) gösterir. Seriler hakkında daha fazla bilgi için, [serideki ilk öğreticiye](introduction.md)bakın.

## <a name="overview"></a>Genel bakış

Bu öğreticide, bir veritabanı değişikliği ve ilgili kod değişiklikleri yapar, değişiklikleri Visual Studio 'da test edin ve ardından bu güncelleştirmeyi test, hazırlama ve üretim ortamlarına dağıtın.

Öğreticide ilk olarak Code First Migrations tarafından yönetilen bir veritabanını güncelleştirme ve daha sonra dbDacFx sağlayıcısı kullanılarak bir veritabanının nasıl güncelleşmekte olduğu gösterilmektedir.

Anımsatıcı: bir hata iletisi alırsanız veya öğreticide ilerlediyseniz bir şey çalışmadıysanız [sorun giderme sayfasını](troubleshooting.md)kontrol ettiğinizden emin olun.

## <a name="deploy-a-database-update-by-using-code-first-migrations"></a>Code First Migrations kullanarak bir veritabanı güncelleştirmesi dağıtma

Bu bölümde, `Student` ve `Instructor` varlıkları için `Person` taban sınıfına bir Doğum tarihi sütunu eklersiniz. Ardından, eğitmen verilerini görüntüleyen sayfayı yeni sütunu görüntüleyecek şekilde güncelleştirin. Son olarak, değişiklikleri test, hazırlama ve üretime dağıtırsınız.

### <a name="add-a-column-to-a-table-in-the-application-database"></a>Uygulama veritabanındaki bir tabloya sütun ekleme

1. *Contosouniversity. dal* projesinde, *Person.cs* açın ve `Person` sınıfının sonuna aşağıdaki özelliği ekleyin (bundan sonra iki kapatma küme ayracı olmalıdır):

    [!code-csharp[Main](deploying-a-database-update/samples/sample1.cs)]

    Sonra, `Seed` yöntemini yeni sütun için bir değer sağlayacak şekilde güncelleştirin. *Migrations\configuration.cs* ' i açın ve `var instructors = new List<Instructor>` başlayan kod bloğunu, Doğum tarihi bilgilerini içeren aşağıdaki kod bloğu ile değiştirin:

    [!code-csharp[Main](deploying-a-database-update/samples/sample2.cs)]
2. Çözümü oluşturun ve ardından **Paket Yöneticisi konsol** penceresini açın. ContosoUniversity. DAL ' nin hala **varsayılan proje**olarak seçildiğinden emin olun.
3. **Paket Yöneticisi konsolu** penceresinde, **varsayılan proje**olarak **contosouniversity. dal** ' ı seçin ve aşağıdaki komutu girin:

    [!code-powershell[Main](deploying-a-database-update/samples/sample3.ps1)]

    Bu komut tamamlandığında, Visual Studio yeni `DbMigration` sınıfını tanımlayan sınıf dosyasını açar ve `Up` yönteminde yeni sütunu oluşturan kodu görebilirsiniz. `Up` yöntemi, değişikliği uygularken sütunu oluşturur ve `Down` yöntemi, değişikliği geri aldığınızda sütunu siler.

    ![AddBirthDate_migration_code](deploying-a-database-update/_static/image1.png)
4. Çözümü oluşturun ve ardından **Paket Yöneticisi konsol** penceresine aşağıdaki komutu girin (contosouniversity. dal projesinin hala seçili olduğundan emin olun):

    [!code-powershell[Main](deploying-a-database-update/samples/sample4.ps1)]

    Entity Framework `Up` yöntemini çalıştırır ve sonra `Seed` metodunu çalıştırır.

### <a name="display-the-new-column-in-the-instructors-page"></a>Eğitmenler sayfasında yeni sütunu görüntüle

1. ContosoUniversity projesinde, *eğitmenler. aspx* ' i açın ve Doğum tarihini göstermek için yeni bir şablon alanı ekleyin. İşe alma tarihi ve Office ataması için olanlar arasına ekleyin:

    [!code-aspx[Main](deploying-a-database-update/samples/sample5.aspx?highlight=9-17)]

    (Kod girintileme eşitlenmemiş ise, CTRL + K tuşlarına basabilir ve sonra dosyayı otomatik olarak yeniden biçimlendirmek için CTRL-D ' ye basabilirsiniz.)
2. Uygulamayı çalıştırın ve **eğitmenler** bağlantısına tıklayın.

    Sayfa yüklendiğinde, yeni Doğum tarihi alanına sahip olduğunu görürsünüz.

    ![Doğum tarihi olan eğitmenler sayfası](deploying-a-database-update/_static/image2.png)
3. Tarayıcıyı kapatın.

### <a name="deploy-the-database-update"></a>Veritabanı güncelleştirmesini dağıtma

1. **Çözüm Gezgini** contosouniversity projesini seçin.
2. Web 'de **Yayımla** araç çubuğunda, **Test** yayımlama profili ' ne tıklayın ve ardından **Web 'i Yayımla**' ya tıklayın. (Araç çubuğu devre dışıysa, **Çözüm Gezgini**' de contosouniversity projesini seçin.)

    Visual Studio, güncelleştirilmiş uygulamayı dağıtır ve tarayıcı giriş sayfasında açılır.
3. Güncelleştirmenin başarıyla dağıtıldığını doğrulamak için **eğitmenler** sayfasını çalıştırın.

    Uygulama bu sayfanın veritabanına erişmeye çalıştığında, Code First veritabanı şemasını güncelleştirir ve `Seed` metodunu çalıştırır. Sayfa görüntülendiğinde, içindeki tarihlerle birlikte beklenen **Doğum tarihi** sütununu görürsünüz.
4. Web 'de **Yayımla** araç çubuğunda, **hazırlama** yayımlama profili ' ne tıklayın ve ardından **Web 'i Yayımla**' ya tıklayın.
5. Güncelleştirmenin başarıyla dağıtıldığını doğrulamak için hazırlama aşamasında **eğitmenler** sayfasını çalıştırın.
6. Web 'de **Yayımla** araç çubuğunda, **Üretim** yayımlama profili ' ne tıklayın ve ardından **Web 'i Yayımla**' ya tıklayın.
7. Güncelleştirmenin başarıyla dağıtıldığını doğrulamak için üretimde **eğitmenler** sayfasını çalıştırın.

    Bir veritabanı değişikliğini içeren gerçek bir üretim uygulaması güncelleştirmesi için, önceki öğreticide gördüğünüz gibi *app\_offline. htm*' yi kullanarak dağıtım sırasında uygulamayı çevrimdışı duruma de çevrimdışına almanız gerekir.

## <a name="deploy-a-database-update-by-using-the-dbdacfx-provider"></a>DbDacFx sağlayıcısını kullanarak bir veritabanı güncelleştirmesi dağıtma

Bu bölümde, üyelik veritabanındaki *Kullanıcı* tablosuna bir *Açıklama* sütunu ekler ve her bir kullanıcı için açıklamaları görüntülemenize ve düzenlemenize olanak tanıyan bir sayfa oluşturacaksınız. Ardından, değişiklikleri test, hazırlama ve üretime dağıtabilirsiniz.

### <a name="add-a-column-to-a-table-in-the-membership-database"></a>Üyelik veritabanındaki bir tabloya sütun ekleme

1. Visual Studio 'da **SQL Server Nesne Gezgini**açın.
2. Expand **(LocalDB) \v11.0**, **veritabanları**' nı genişletin, **ASPNET-ContosoUniversity** ( **ASPNET-contosouniversity-prod**) öğesini genişletin ve ardından **Tablolar**' ı genişletin.

    **SQL Server** düğümü altında **(LocalDB) \v11.0** görmüyorsanız, **SQL Server** düğümüne sağ tıklayıp **SQL Server Ekle**' ye tıklayın. **Sunucuya Bağlan** Iletişim kutusunda **sunucu adı**olarak *(LocalDB) \v11.0* girin ve ardından **Bağlan**' a tıklayın.

    **ASPNET-Contosoüniversitesi**' ni görmüyorsanız, projeyi çalıştırın ve *yönetici* kimlik bilgilerini (parola *devpwd*) kullanarak oturum açın ve **SQL Server Nesne Gezgini** penceresini yenileyin.
3. **Kullanıcılar** tablosuna sağ tıklayın ve sonra **Tasarımcı görüntüle**' ye tıklayın.

    ![SSOX Görünüm Tasarımcısı](deploying-a-database-update/_static/image3.png)
4. Tasarımcıda bir *Açıklama* sütunu ekleyin ve bunu *nvarchar (128)* ve null yapılabilir yapın ve ardından **Güncelleştir**' e tıklayın.

    ![Açıklama sütunu ekleme](deploying-a-database-update/_static/image4.png)
5. **Veritabanı güncelleştirmelerini Önizle** kutusunda **veritabanını güncelleştir**' e tıklayın.

    ![Veritabanı güncelleştirmelerini Önizle](deploying-a-database-update/_static/image5.png)

### <a name="create-a-page-to-display-and-edit-the-new-column"></a>Yeni sütunu göstermek ve düzenlemek için bir sayfa oluşturun

1. **Çözüm Gezgini**, contosouniversity projesindeki **Hesap** klasörüne sağ tıklayın, **Ekle**' ye ve ardından **Yeni öğe**' ye tıklayın.
2. **Ana sayfayı kullanarak yeni bir Web formu** oluşturun ve bunu *UserInfo. aspx*olarak adlandırın. Varsayılan *site. Master* dosyasını ana sayfa olarak kabul edin.
3. Aşağıdaki işaretlemeyi `MainContent` `Content` öğesine kopyalayın (3 `Content` öğelerinden son):

    [!code-aspx[Main](deploying-a-database-update/samples/sample6.aspx)]
4. *UserInfo. aspx* sayfasına sağ tıklayın ve **Tarayıcıda görüntüle**' ye tıklayın.
5. *Yönetici* Kullanıcı kimlik bilgilerinizle (parola *devpwd*) oturum açın ve sayfanın düzgün çalıştığını doğrulamak için bir kullanıcıya bazı yorumlar ekleyin.

    ![UserInfo sayfası](deploying-a-database-update/_static/image6.png)
6. Tarayıcıyı kapatın.

## <a name="deploy-the-database-update"></a>Veritabanı güncelleştirmesini dağıtma

DbDacFx sağlayıcısını kullanarak dağıtmak için, yayımlama profilinde **veritabanını güncelleştir** seçeneğini belirlemeniz yeterlidir. Bununla birlikte, bu seçeneği kullandığınızda ilk dağıtım için bazı ek SQL betikleri da yapılandırmış olursunuz: Bunlar hala profilde bulunur ve bunların yeniden çalıştırılmasını engellemeniz gerekir.

1. ContosoUniversity projesine sağ tıklayıp **Yayımla**' ya tıklayarak **Web 'i Yayımla** Sihirbazı ' nı açın.
2. **Test** profilini seçin.
3. **Ayarlar** sekmesine tıklayın.
4. **DefaultConnection**altında **veritabanını güncelleştir**' i seçin.
5. İlk dağıtım için çalıştırmak üzere yapılandırdığınız ek betikleri devre dışı bırakın:

    1. **Veritabanı güncelleştirmelerini Yapılandır**öğesine tıklayın.
    2. **Veritabanı güncelleştirmelerini Yapılandır** iletişim kutusunda, *ver. SQL* ve *ASPNET-Data-dev. SQL*' ın yanındaki onay kutularını temizleyin.
    3. **Kapat**'ı tıklatın.
6. **Önizleme** sekmesine tıklayın.
7. **DefaultConnection**'un **veritabanları** ve sağ tarafındaki **veritabanı önizleme** bağlantısına tıklayın.

    ![Veritabanı önizlemesi](deploying-a-database-update/_static/image7.png)

    Önizleme penceresi, veritabanı şemasının kaynak veritabanının şemasıyla eşleşmesini sağlamak için hedef veritabanında çalıştırılacak betiği gösterir. Komut dosyası, yeni sütunu ekleyen bir ALTER TABLE komutu içerir.
8. **Veritabanı önizlemesi** iletişim kutusunu kapatın ve ardından **Yayımla**' ya tıklayın.

    Visual Studio, güncelleştirilmiş uygulamayı dağıtır ve tarayıcı giriş sayfasında açılır.
9. Güncelleştirmenin başarıyla dağıtıldığını doğrulamak için UserInfo sayfasını (giriş sayfası URL 'sine *Hesap/UserInfo. aspx* ekleyin) çalıştırın. *Yönetici* ve *devpwd*girerek oturum açmanız gerekir.

    Tablolardaki veriler varsayılan olarak dağıtılır ve çalıştırmak için bir veri dağıtım betiği yapılandırmadıysanız, geliştirmede eklediğiniz yorumu bulamayacaksınız. Değişikliğin veritabanına dağıtıldığını ve sayfanın doğru şekilde çalıştığını doğrulamak için şimdi hazırlama aşamasında yeni bir yorum ekleyebilirsiniz.
10. Hazırlama ve üretime dağıtmak için aynı yordamı izleyin.

    Ek betikleri devre dışı bırakmayı unutmayın. Test profiliyle karşılaştırılan tek fark, hazırlama ve üretim profillerindeki yalnızca bir betiği devre dışı bırakacağından yalnızca *ASPNET-prod-Data. SQL*' i çalıştıracak şekilde yapılandırılmanızdır.

    Hazırlama ve üretim için kimlik bilgileri yönetici ve prodpwd ' dir.

    Bir veritabanı değişikliğini içeren gerçek bir üretim uygulaması güncelleştirmesi için, [önceki öğreticide](deploying-a-code-update.md)gördüğünüz şekilde, uygulamayı yayımlamadan ve silmeden önce *çevrimdışı. htm\_* yükleme sırasında uygulamayı çevrimdışı olarak da çevrimdışına almanız gerekir.

## <a name="summary"></a>Özet

Artık Code First Migrations ve dbDacFx sağlayıcısını kullanarak bir veritabanı değişikliği içeren bir uygulama güncelleştirmesi dağıttınız.

![Doğum tarihi olan eğitmenler sayfası](deploying-a-database-update/_static/image8.png)

![UserInfo sayfası](deploying-a-database-update/_static/image9.png)

Sonraki öğreticide, komut satırını kullanarak dağıtımların nasıl yürütüleceği gösterilmektedir.

> [!div class="step-by-step"]
> [Önceki](deploying-a-code-update.md)
> [İleri](command-line-deployment.md)
