---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12
title: 'Visual Studio veya Visual Web Developer kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: Web. config dosyası dönüştürmeleri-3/12 | Microsoft Docs'
author: tdykstra
description: Bu öğretici dizisinde, Visual Stu kullanarak bir SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesinin nasıl dağıtılacağı (yayımlanacağı) gösterilmektedir.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 2b0df3d9-450b-4ea6-b315-4c9650722cad
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12
msc.type: authoredcontent
ms.openlocfilehash: fe71e6cfb0f4c5f1d99b326e9d90edb6c8c5feee
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600520"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-webconfig-file-transformations---3-of-12"></a>Visual Studio veya Visual Web Developer kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: Web. config dosyası dönüştürmeleri-3/12

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Başlatıcı projesi indir](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> Bu öğretici serisi, Visual Studio 2012 RC veya Web için Visual Studio Express 2012 RC kullanarak SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesini dağıtmayı (yayımlamayı) gösterir. Ayrıca, Web yayımlama güncelleştirmesini yüklerseniz Visual Studio 2010 de kullanabilirsiniz. Seriye giriş için, [serideki ilk öğreticiye](deployment-to-a-hosting-provider-introduction-1-of-12.md)bakın.
> 
> Visual Studio 2012 RC yayımlandıktan sonra tanıtılan dağıtım özelliklerini gösteren bir öğretici için, SQL Server Compact dışındaki SQL Server sürümlerinin nasıl dağıtılacağını gösterir ve Web Apps Azure App Service nasıl dağıtılacağını gösterir. bkz. [Visual Studio kullanarak ASP.NET Web dağıtımı](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Genel bakış

Bu öğreticide, *Web. config* dosyasını farklı hedef ortamlara dağıtırken değiştirme işlemini nasıl otomatikleştirebileceğiniz gösterilmektedir. Çoğu uygulama, *Web. config* dosyasında, uygulama dağıtıldığında farklı olması gereken ayarlara sahiptir. Bu değişikliklerin yapılması işleminin otomatikleştirilmesi, her dağıttığınız zaman bunları el ile yapmak zorunda kalmaktan, bu da sıkıcı ve hataya açık olmanızı sağlar.

Anımsatıcı: bir hata iletisi alırsanız veya öğreticide ilerlediyseniz bir şey çalışmadıysanız [sorun giderme sayfasını](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)kontrol ettiğinizden emin olun.

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Web. config dönüştürmeleri Web Dağıtımı parametrelere karşı

*Web. config* dosya ayarlarını değiştirme işlemini otomatik hale getirmenin iki yolu vardır: [Web. config dönüşümleri](https://msdn.microsoft.com/library/dd465326.aspx) ve [Web dağıtımı parametreleri](https://msdn.microsoft.com/library/ff398068.aspx). *Web. config* dönüşüm dosyası dağıtıldığında *Web. config* dosyasının nasıl değiştirileceğini belirten xml biçimlendirmesi içerir. Belirli derleme yapılandırmalarının ve belirli yayımlama profillerinin farklı değişikliklerini belirtebilirsiniz. Varsayılan derleme yapılandırması hata ayıklama ve sürümdür ve özel derleme yapılandırması oluşturabilirsiniz. Bir yayımlama profili, genellikle bir hedef ortama karşılık gelir. (Yayımlama profilleri hakkında daha fazla bilgi için bkz. [bir test ortamı olarak IIS 'e dağıtma](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) öğreticisi.)

Web Dağıtımı parametreler, *Web. config* dosyalarında bulunan ayarlar dahil olmak üzere, dağıtım sırasında yapılandırılması gereken birçok farklı tür ayarı belirtmek için kullanılabilir. *Web. config* dosyası değişikliklerini belirtmek için kullanıldığında Web dağıtımı parametrelerin ayarlanması daha karmaşıktır, ancak dağıtana kadar ayarlanacak değeri bilemezsiniz. Örneğin, bir kurumsal ortamda bir *dağıtım paketi* oluşturabilir ve bu kişiye BT departmanındaki bir kişiye üretime yükleyebilirsiniz ve bu kişinin tanımadığınız bağlantı dizelerini veya parolalarını girebilmesi gerekir.

Bu öğreticinin kapsamakta olduğu senaryo için, *Web. config* dosyasında yapılması gereken her şeyi bildiğiniz için Web dağıtımı parametrelerini kullanmanız gerekmez. Kullanılan derleme yapılandırmasına bağlı olarak farklı bazı dönüşümler ve kullanılan yayımlama profiline göre farklılık gösteren bazı dönüştürmeleri yapılandıracaksınız.

## <a name="creating-transformation-files-for-publish-profiles"></a>Yayımlama profilleri için dönüşüm dosyaları oluşturma

**Çözüm Gezgini**' de, varsayılan olarak iki varsayılan derleme yapılandırması Için oluşturulan *Web. Debug. config* ve *Web. Release. config* dönüşüm dosyalarını görmek için *Web. config* ' i genişletin.

![Web. config_transform_files](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image1.png)

Web. config dosyasına sağ tıklayıp bağlam menüsünden **yapılandırma dönüşümleri Ekle** ' yi seçerek özel derleme yapılandırmalarına yönelik dönüşüm dosyaları oluşturabilirsiniz, ancak bu öğreticide bunu yapmanız gerekmez.

Yapı yapılandırması yerine dağıtım hedefi ile ilgili değişiklikleri yapılandırmak için iki farklı dönüştürme dosyasına ihtiyacınız vardır. Bu tür bir ayarın tipik bir örneği, test ve üretime karşı farklı olan bir WCF uç noktasıdır. Sonraki öğreticilerde, test ve üretim adlı yayımlama profilleri oluşturacaksınız, bu nedenle bir *Web. test. config* dosyası ve bir *Web. Production. config* dosyası gereklidir.

Yayımlama profillerine bağlı olan dönüştürme dosyalarının el ile oluşturulması gerekir. **Çözüm Gezgini**, contosouniversity projesine sağ tıklayın ve **klasörü Windows Gezgini 'nde aç**' ı seçin.

![Open_folder_in_Windows_Explorer](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image2.png)

**Windows Gezgini**'nde *Web. Release. config* dosyasını seçin, dosyayı kopyalayın ve sonra iki kopyasını yapıştırın. Bu kopyaları *Web. Production. config* ve *Web. test. config*olarak yeniden adlandırın ve sonra **Windows Gezgini**'ni kapatın.

**Çözüm Gezgini**' de, yeni dosyaları görmek için **Yenile** ' ye tıklayın.

Yeni dosyaları seçin, sağ tıklayın ve bağlam menüsünde **projeye dahil et** ' e tıklayın.

![Projedeki test ve üretim yapılandırma dosyalarını dahil etme](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image3.png)

Bu dosyaların dağıtılmasını engellemek için **Çözüm Gezgini**içinde seçin ve ardından **Özellikler** penceresinde **derleme eylemi** özelliğini **içerikten** **hiçbiri**olarak değiştirin. (Derleme yapılandırmalarına dayanan dönüştürme dosyalarının dağıtımı otomatik olarak engellenir.)

Artık *Web. config dönüştürme* dosyalarına *Web. config* dönüştürmeleri girmeye hazırsınız.

## <a name="limiting-error-log-access-to-administrators"></a>Yöneticilere hata günlüğü erişimini sınırlandırma

Uygulama çalışırken bir hata oluşursa, uygulama sistem tarafından oluşturulan hata sayfasının yerine genel bir hata sayfası görüntüler ve hata günlüğü ve raporlama için [ELMAH NuGet paketini](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) kullanır. *Web. config* dosyasındaki `customErrors` öğesi hata sayfasını belirtir:

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample1.xml)]

Hata sayfasını görmek için, `customErrors` öğesinin `mode` özniteliğini geçici olarak "RemoteOnly" iken "on" olarak değiştirin ve uygulamayı Visual Studio 'dan çalıştırın. *Studentsxxx. aspx*gibi GEÇERSIZ bir URL isteyerek hataya neden olur. IIS tarafından oluşturulan bir "sayfa bulunamadı" hata sayfası yerine *Genericerrorpage. aspx* sayfasını görürsünüz.

[![Error_page](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image5.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image4.png)

Hata günlüğünü görmek için, URL 'deki her şeyi *ELMAH. axd* ile bağlantı noktası numarasından sonra değiştirin (ekran görüntüsündeki örnek için `http://localhost:51130/elmah.axd`) ve ENTER tuşuna basın:

[![Elmah_log_page](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image7.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image6.png)

İşiniz bittiğinde `customErrors` öğeyi "RemoteOnly" moduna ayarlamayı unutmayın.

Geliştirme bilgisayarınızda hata günlüğü sayfasına ücretsiz erişime izin vermek kolaydır, ancak üretimde bir güvenlik riski olabilir. Üretim sitesi için, *Web. Production. config* dosyasında bir dönüşüm yapılandırarak yalnızca yöneticilere hata günlüğü erişimini sınırlayan bir yetkilendirme kuralı ekleyebilirsiniz.

*Web. Production. config* dosyasını açın ve burada gösterildiği gibi, açma `configuration` etiketinden hemen sonra yeni bir `location` öğesi ekleyin. (Burada yalnızca bir bağlam sağlamak için gösterilen çevreleyen biçimlendirmeyi değil yalnızca `location` öğesini eklediğinizden emin olun.)

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample2.xml?highlight=2-9)]

"INSERT" öğesinin `Transform` özniteliği değeri, bu `location` öğesinin *Web. config* dosyasındaki mevcut `location` öğelerine eşdüzey olarak eklenmesine neden olur. ( **Güncelleştirme kredileri** sayfası için yetkilendirme kurallarını belirten bir `location` öğesi zaten var.) Dağıtım sonrasında üretim sitesini test ettiğinizde, bu yetkilendirme kuralının etkin olduğunu doğrulamayı test edersiniz.

Test ortamında hata günlüğü erişimini kısıtlamak zorunda değilsiniz, bu nedenle *Web. test. config* dosyasına bu kodu eklemeniz gerekmez.

> [!NOTE] 
> 
> **Güvenlik notunun** Bir üretim uygulamasında herkese hiçbir şekilde hata ayrıntılarını görüntülemez veya bu bilgileri genel bir konumda depolayın. Saldırganlar, bir sitedeki güvenlik açıklarını saptamak için hata bilgilerini kullanabilir. Kendi uygulamanızda ELMAH kullanırsanız, güvenlik risklerini en aza indirmek için ELMAH 'nin yapılandırılabileceği yolları araştırdığınızdan emin olun. Bu öğreticideki ELMAH örneği önerilen bir yapılandırma olarak düşünülmemelidir. Uygulamanın içinde dosya oluşturabilme gereken bir klasörü nasıl işleyeceğinizi göstermek için seçilmiş bir örnektir.

## <a name="setting-an-environment-indicator"></a>Ortam göstergesini ayarlama

Ortak bir senaryo, dağıttığınız her ortamda farklı olması gereken *Web. config* dosya ayarlarına sahip olacaktır. Örneğin, bir WCF hizmetini çağıran bir uygulama, test ve üretim ortamlarında farklı bir uç nokta gerektirebilir. Contoso Üniversitesi uygulaması bu tür bir ayarı da içerir. Bu ayar, bir sitenin sayfalarında geliştirme, test veya üretim gibi hangi ortama sahip olduğunu bildiren görünür bir göstergeyi denetler. Ayar değeri, uygulamanın sitedeki ana başlığa "(dev)" veya "(test)" ekleyip eklemeyeceğini belirler *. ana* ana sayfa:

[![Environment_indicator](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image9.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image8.png)

Uygulama üretimde çalışırken ortam göstergesi atlanır.

Contoso University Web sayfaları, uygulamanın hangi ortamda çalıştığını belirlemek için *Web. config* dosyasında `appSettings` olarak ayarlanan bir değeri okur:

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample3.xml)]

Değer, test ortamında "test" ve üretim ortamında "üretim" olmalıdır.

*Web. Production. config* dosyasını açın ve daha önce eklediğiniz `location` öğesinin açılış etiketinden hemen önce bir `appSettings` öğesi ekleyin:

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample4.xml)]

"SetAttributes" `xdt:Transform` özniteliği değeri, bu dönüşümün amacının, *Web. config* dosyasındaki var olan bir öğenin öznitelik değerlerini değiştirmesinin olduğunu gösterir. `xdt:Locator` öznitelik değeri "Match (Key)", değiştirilecek öğenin burada belirtilen `key` özniteliğiyle eşleşen bir `key` özniteliği olduğunu gösterir. `add` öğesinin yalnızca diğer özniteliği `value`ve dağıtılan *Web. config* dosyasında değiştirilecek. Bu kod, `Environment` `appSettings` öğesinin `value` özniteliğinin üretime dağıtılan *Web. config* dosyasında "prod" olarak ayarlanmasına neden olur.

Daha sonra, aynı değişikliği *Web. test. config* dosyasına uygulayın, bunun dışında, `value` "üretim" yerine "test" olarak ayarlayın. İşiniz bittiğinde, *Web. test. config* dosyasındaki `appSettings` bölümü aşağıdaki örneğe benzer şekilde görünür:

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample5.xml)]

## <a name="disabling-debug-mode"></a>Hata ayıklama modunu devre dışı bırakma

Bir yayın derlemesi için, hangi ortamdan dağıtmakta olduğunuza bakılmaksızın hata ayıklamanın etkinleştirilmesini istemezsiniz. Varsayılan olarak, *Web. Release. config* dönüşüm dosyası, `compilation` öğesinden `debug` özniteliğini kaldıran kodla otomatik olarak oluşturulur:

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample6.xml)]

`Transform` özniteliği, bir yayın derlemesi dağıttığınız her seferinde dağıtılan *Web. config* dosyasından `debug` özniteliği atlanmasına neden olur.

Aynı dönüşüm test ve üretim dönüştürme dosyalarında olduğundan, yayın dönüşüm dosyasını kopyalayarak bunları oluşturdunuz. Burada yinelenmeniz gerekmez, bu dosyaların her birini açın, **derleme** öğesini kaldırın ve her bir dosyayı kaydedip kapatın.

## <a name="setting-connection-strings"></a>Bağlantı dizelerini ayarlama

Çoğu durumda, yayımlama profilinde bağlantı dizelerini belirtebileceğiniz için bağlantı dizesi dönüştürmeleri ayarlamanız gerekmez. Ancak, bir SQL Server Compact veritabanı dağıttığınızda ve hedef sunucudaki veritabanını güncelleştirmek için Entity Framework Code First Migrations kullandığınızda bir özel durum vardır. Bu senaryo için, veritabanı şemasını güncelleştirmek üzere sunucuda kullanılacak ek bir bağlantı dizesi belirtmeniz gerekir. Bu dönüştürmeyi ayarlamak için hem *Web. test. config* hem de *Web. Production. config* dönüştürme dosyalarındaki **&lt;Configuration&gt;** etiketinin hemen ardından bir **&lt;connectionStrings&gt;** öğesi ekleyin:

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample7.xml)]

`Transform` özniteliği, bu bağlantı dizesinin dağıtılan *Web. config* dosyasındaki *connectionStrings* öğesine ekleneceğini belirtir. (Yayımlama işlemi, mevcut değilse bu ek bağlantı dizesini sizin için otomatik olarak oluşturur, ancak varsayılan olarak **ProviderName** özniteliği, SQL Server Compact için değil `System.Data.SqlClient`olarak ayarlanır. Bağlantı dizesini el ile ekleyerek, dağıtım işlemini yanlış sağlayıcı adıyla bir bağlantı dizesi öğesi oluşturmaktan haberdar olursunuz.)

Artık Contoso University uygulamasını test ve üretime dağıtmak için ihtiyacınız olan tüm *Web. config* dönüştürmelerini belirttiniz. Aşağıdaki öğreticide, proje özelliklerinin ayarlanmasını gerektiren dağıtım kurulum görevlerinin ele alınır.

## <a name="more-information"></a>Daha fazla bilgi

Bu öğreticinin kapsadığı konular hakkında daha fazla bilgi için [ASP.NET dağıtım Içerik eşlemesindeki](https://msdn.microsoft.com/library/bb386521.aspx)Web. config dönüştürme senaryosuna bakın.

> [!div class="step-by-step"]
> [Önceki](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)
> [İleri](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)
