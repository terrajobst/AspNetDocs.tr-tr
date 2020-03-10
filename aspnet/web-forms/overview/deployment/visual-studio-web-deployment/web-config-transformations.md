---
uid: web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
title: 'Visual Studio kullanarak Web dağıtımı ASP.NET: Web. config dosyası dönüşümleri | Microsoft Docs'
author: tdykstra
description: Bu öğretici serisi, bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf bir barındırma sağlayıcısına, usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 5a2a927b-14cb-40bc-867a-f0680f9febd7
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
msc.type: authoredcontent
ms.openlocfilehash: a9d39547c94a63003442ba6fe1257693dde24b05
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78632834"
---
# <a name="aspnet-web-deployment-using-visual-studio-webconfig-file-transformations"></a>Visual Studio kullanarak Web dağıtımı ASP.NET: Web. config dosyası dönüşümleri

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Başlatıcı projesi indir](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> Bu öğretici serisi, Visual Studio 2012 veya Visual Studio 2010 kullanarak bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf barındırma sağlayıcısına dağıtmayı (yayımlamayı) gösterir. Seriler hakkında daha fazla bilgi için, [serideki ilk öğreticiye](introduction.md)bakın.

## <a name="overview"></a>Genel bakış

Bu öğreticide, *Web. config* dosyasını farklı hedef ortamlara dağıtırken değiştirme işlemini nasıl otomatikleştirebileceğiniz gösterilmektedir. Çoğu uygulama, *Web. config* dosyasında, uygulama dağıtıldığında farklı olması gereken ayarlara sahiptir. Bu değişikliklerin yapılması işleminin otomatikleştirilmesi, her dağıttığınız zaman bunları el ile yapmak zorunda kalmaktan, bu da sıkıcı ve hataya açık olmanızı sağlar.

Anımsatıcı: bir hata iletisi alırsanız veya öğreticide ilerlediyseniz bir şey çalışmadıysanız [sorun giderme sayfasını](troubleshooting.md)kontrol ettiğinizden emin olun.

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Web. config dönüştürmeleri Web Dağıtımı parametrelere karşı

*Web. config* dosya ayarlarını değiştirme işlemini otomatik hale getirmenin iki yolu vardır: [Web. config dönüşümleri](https://msdn.microsoft.com/library/dd465326.aspx) ve [Web dağıtımı parametreleri](https://msdn.microsoft.com/library/ff398068.aspx). *Web. config* dönüşüm dosyası dağıtıldığında *Web. config* dosyasının nasıl değiştirileceğini belirten xml biçimlendirmesi içerir. Belirli derleme yapılandırmalarının ve belirli yayımlama profillerinin farklı değişikliklerini belirtebilirsiniz. Varsayılan derleme yapılandırması hata ayıklama ve sürümdür ve özel derleme yapılandırması oluşturabilirsiniz. Bir yayımlama profili, genellikle bir hedef ortama karşılık gelir. (Yayımlama profilleri hakkında daha fazla bilgi için bkz. [bir test ortamı olarak IIS 'e dağıtma](deploying-to-iis.md) öğreticisi.)

Web Dağıtımı parametreler, *Web. config* dosyalarında bulunan ayarlar dahil olmak üzere, dağıtım sırasında yapılandırılması gereken birçok farklı tür ayarı belirtmek için kullanılabilir. *Web. config* dosyası değişikliklerini belirtmek için kullanıldığında Web dağıtımı parametrelerin ayarlanması daha karmaşıktır, ancak dağıtana kadar ayarlanacak değeri bilemezsiniz. Örneğin, bir kurumsal ortamda bir *dağıtım paketi* oluşturabilir ve bu kişiye BT departmanındaki bir kişiye üretime yükleyebilirsiniz ve bu kişinin tanımadığınız bağlantı dizelerini veya parolalarını girebilmesi gerekir.

Bu öğretici serisinin kapsamakta olduğu senaryo için, *Web. config* dosyasında yapılacak her şeyi ilerletin, bu nedenle Web dağıtımı parametrelerini kullanmanız gerekmez. Kullanılan derleme yapılandırmasına bağlı olarak farklı bazı dönüşümler ve kullanılan yayımlama profiline göre farklılık gösteren bazı dönüştürmeleri yapılandıracaksınız.

<a id="watransforms"></a>

## <a name="specifying-webconfig-settings-in-azure"></a>Azure 'da Web. config ayarlarını belirtme

Değiştirmek istediğiniz *Web. config* dosyası ayarları `<connectionStrings>` veya `<appSettings>` öğesi ise ve Azure App Service 'de Web Apps dağıtıyorsanız, dağıtım sırasında değişiklikleri otomatikleştirme için başka bir seçeneğiniz vardır. Web uygulamanız için Yönetim Portalı sayfasının **Yapılandır** sekmesinden Azure 'da etkili olmasını istediğiniz ayarları girebilirsiniz ( **uygulama ayarları** ve **bağlantı dizeleri** bölümlerine ilerleyin). Projeyi dağıttığınızda, Azure değişiklikleri otomatik olarak uygular. Daha fazla bilgi için bkz. [Microsoft Azure Web siteleri: uygulama dizeleri ve bağlantı dizeleri nasıl çalışır?](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx).

## <a name="default-transformation-files"></a>Varsayılan dönüşüm dosyaları

**Çözüm Gezgini**' de, varsayılan olarak iki varsayılan derleme yapılandırması Için oluşturulan *Web. Debug. config* ve *Web. Release. config* dönüşüm dosyalarını görmek için *Web. config* ' i genişletin.

![Web. config_transform_files](web-config-transformations/_static/image1.png)

Web. config dosyasına sağ tıklayıp bağlam menüsünden **yapılandırma dönüşümleri Ekle** ' yi seçerek özel derleme yapılandırmalarına yönelik dönüşüm dosyaları oluşturabilirsiniz. Bu öğreticide, herhangi bir özel derleme yapılandırması oluşturmadıysanız, bunu yapmanız gerekmez ve menü seçeneği devre dışı bırakılır.

Daha sonra test, hazırlama ve üretim yayımlama profilleri için birer tane olmak üzere üç dönüştürme dosyası oluşturacaksınız. Bir yayımlama profili dönüştürme dosyasında işletireceğinize ilişkin tipik bir örnek, hedef ortama bağlı olduğundan, test ve üretime karşı farklılık gösteren bir WCF uç noktasıdır. Sonraki öğreticilerde, devam ettikleri yayımlama profillerini oluşturduktan sonra Yayımlama profili dönüştürme dosyaları oluşturacaksınız.

## <a name="disable-debug-mode"></a>Hata ayıklama modunu devre dışı bırak

Hedef ortam yerine derleme yapılandırmasına bağlı olan bir ayara örnek `debug` özniteliğidir. Bir yayın derlemesi için, dağıtım yaptığınız ortama bakılmaksızın hata ayıklamanın devre dışı olmasını istersiniz. Bu nedenle, varsayılan olarak Visual Studio proje şablonları, `compilation` öğesinden `debug` özniteliğini kaldıran kod ile *Web. Release. config* dönüşüm dosyaları oluşturur. Varsayılan *Web. Release. config*' dir: açıklama eklenen bazı örnek dönüştürme kodları buna ek olarak, `debug` özniteliğini kaldıran `compilation` öğesindeki kodu içerir:

[!code-xml[Main](web-config-transformations/samples/sample1.xml?highlight=18)]

`xdt:Transform="RemoveAttributes(debug)"` özniteliği, `debug` özniteliğinin dağıtılmış *Web. config* dosyasındaki `system.web/compilation` öğesinden kaldırılmasını istediğinizi belirtir. Bu, bir yayın derlemesini her dağıttığınızda yapılır.

## <a name="limit-error-log-access-to-administrators"></a>Yöneticilere hata günlüğü erişimini sınırlama

Uygulama çalışırken bir hata oluşursa, uygulama sistem tarafından oluşturulan hata sayfasının yerine genel bir hata sayfası görüntüler ve hata günlüğü ve raporlama için [ELMAH NuGet paketini](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) kullanır. Application *Web. config* dosyasındaki `customErrors` öğesi hata sayfasını belirtir:

[!code-xml[Main](web-config-transformations/samples/sample2.xml)]

Hata sayfasını görmek için, `customErrors` öğesinin `mode` özniteliğini geçici olarak "RemoteOnly" iken "on" olarak değiştirin ve uygulamayı Visual Studio 'dan çalıştırın. *Studentsxxx. aspx*gibi GEÇERSIZ bir URL isteyerek hataya neden olur. IIS tarafından oluşturulan "kaynak bulunamıyor" hata sayfasında, *Genericerrorpage. aspx* sayfasını görürsünüz.

![Hata sayfası](web-config-transformations/_static/image2.png)

Hata günlüğünü görmek için, URL 'deki her şeyi *ELMAH. axd* ile bağlantı noktası numarasından sonra değiştirin (örneğin, `http://localhost:51130/elmah.axd`) ve ENTER tuşuna basın:

![ELMAH sayfası](web-config-transformations/_static/image3.png)

İşiniz bittiğinde `customErrors` öğeyi "RemoteOnly" moduna ayarlamayı unutmayın.

Geliştirme bilgisayarınızda hata günlüğü sayfasına ücretsiz erişime izin vermek kolaydır, ancak üretimde bir güvenlik riski olabilir. Üretim sitesi için, yöneticilere hata günlüğü erişimini sınırlayan bir yetkilendirme kuralı eklemek ve kısıtlamanın test ve hazırlama aşamasında olduğundan emin olmak istiyorsunuz. Bu nedenle, bir yayın yapısını her dağıttığınızda uygulamak istediğiniz başka bir değişiklik de *Web. Release. config* dosyasına aittir.

*Web. Release. config* dosyasını açın ve burada gösterildiği gibi, kapanış `configuration` etiketinden hemen önce yeni bir `location` öğesi ekleyin.

[!code-xml[Main](web-config-transformations/samples/sample3.xml?highlight=27-34)]

"INSERT" öğesinin `Transform` özniteliği değeri, bu `location` öğesinin *Web. config* dosyasındaki mevcut `location` öğelerine eşdüzey olarak eklenmesine neden olur. ( **Güncelleştirme kredileri** sayfası için yetkilendirme kurallarını belirten bir `location` öğesi zaten var.)

Artık dönüştürmeyi doğru şekilde kodlediğinizden emin olmak için dönüşümün önizlemesini yapabilirsiniz.

**Çözüm Gezgini**, *Web. Release. config dosyasına* sağ tıklayın ve **dönüşümü Önizle**' ye tıklayın.

![Önizleme dönüşümü menüsü](web-config-transformations/_static/image4.png)

Sol taraftaki geliştirme *Web. config* dosyasını ve dağıtılan *Web. config* dosyasının sağ tarafta, değişiklikler vurgulanmış şekilde göründüğünü gösteren bir sayfa açılır.

![Hata ayıklama dönüştürmesinin önizlemesi](web-config-transformations/_static/image5.png)

![Konum dönüştürmesinin önizlemesi](web-config-transformations/_static/image6.png)

(Önizlemede, dönüştürmelerini yazmadığınız bazı ek değişiklikler fark edebilirsiniz: Bunlar genellikle işlevselliği etkilemeyen beyaz alanın kaldırılmasını içerir.)

Dağıtımı tamamladıktan sonra siteyi test ettiğinizde, yetkilendirme kuralının etkin olduğunu doğrulamayı da test edersiniz.

> [!NOTE] 
> 
> **Güvenlik notunun** Bir üretim uygulamasında herkese hiçbir şekilde hata ayrıntılarını görüntülemez veya bu bilgileri genel bir konumda depolayın. Saldırganlar, bir sitedeki güvenlik açıklarını saptamak için hata bilgilerini kullanabilir. Kendi uygulamanızda ELMAH kullanırsanız, güvenlik risklerini en aza indirmek için ELMAH 'yi yapılandırın. Bu öğreticideki ELMAH örneği önerilen bir yapılandırma olarak düşünülmemelidir. Uygulamanın içinde dosya oluşturabilme gereken bir klasörü nasıl işleyeceğinizi göstermek için seçilmiş bir örnektir. Daha fazla bilgi için bkz. [ELMAH uç noktasını güvenli hale getirme](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages).

## <a name="a-setting-that-youll-handle-in-publish-profile-transformation-files"></a>Yayımlama profili dönüştürme dosyalarında işleyecek bir ayar

Ortak bir senaryo, dağıttığınız her ortamda farklı olması gereken *Web. config* dosya ayarlarına sahip olacaktır. Örneğin, bir WCF hizmetini çağıran bir uygulama, test ve üretim ortamlarında farklı bir uç nokta gerektirebilir. Contoso Üniversitesi uygulaması bu tür bir ayarı da içerir. Bu ayar, bir sitenin sayfalarında geliştirme, test veya üretim gibi hangi ortama sahip olduğunu bildiren görünür bir göstergeyi denetler. Ayar değeri, uygulamanın sitedeki ana başlığa "(dev)" veya "(test)" ekleyip eklemeyeceğini belirler *. ana* ana sayfa:

![Ortam göstergesi](web-config-transformations/_static/image7.png)

Uygulama hazırlama veya üretim aşamasında çalışırken ortam göstergesi atlanır.

Contoso University Web sayfaları, uygulamanın hangi ortamda çalıştığını belirlemek için *Web. config* dosyasında `appSettings` olarak ayarlanan bir değeri okur:

[!code-xml[Main](web-config-transformations/samples/sample4.xml)]

Değer, test ortamında "test", hazırlama ve üretim için "üretim" olmalıdır.

Bir dönüştürme dosyasında aşağıdaki kod bu dönüşümü uygular:

[!code-xml[Main](web-config-transformations/samples/sample5.xml)]

"SetAttributes" `xdt:Transform` özniteliği değeri, bu dönüşümün amacının, *Web. config* dosyasındaki var olan bir öğenin öznitelik değerlerini değiştirmesinin olduğunu gösterir. `xdt:Locator` öznitelik değeri "Match (Key)", değiştirilecek öğenin burada belirtilen `key` özniteliğiyle eşleşen bir `key` özniteliği olduğunu gösterir. `add` öğesinin yalnızca diğer özniteliği `value`ve dağıtılan *Web. config* dosyasında değiştirilecek. Burada gösterilen kod, `Environment` `appSettings` öğesinin `value` özniteliğinin dağıtılan *Web. config* dosyasında "test" olarak ayarlanmasına neden olur.

Bu dönüşüm, henüz oluşturmadığınız yayımlama profili dönüştürme dosyalarına aittir. Bu değişikliği uygulayan dönüştürme dosyalarını, test, hazırlama ve üretim ortamları için yayımlama profilleri oluştururken oluşturur ve güncelleştirebilirsiniz. Bunu, [IIS 'ye dağıt](deploying-to-iis.md) ve üretim öğreticilerine [dağıtmak için](deploying-to-production.md) yapmanız gerekir.

> [!NOTE]
> Bu ayar `<appSettings>` öğesinde olduğundan, bu konunun önceki kısımlarında yer alarak [Azure 'da Web Apps Web. config ayarlarını belirtme](#watransforms) bölümüne bakın Azure App Service

## <a name="setting-connection-strings"></a>Bağlantı dizelerini ayarlama

Varsayılan dönüşüm dosyası, bir bağlantı dizesinin nasıl güncelleştirilmesini gösteren bir örnek içerse de, çoğu durumda, yayımlama profilinde bağlantı dizelerini belirtebilmeniz için bağlantı dizesi dönüştürmeleri ayarlamanız gerekmez. Bunu, [IIS 'ye dağıt](deploying-to-iis.md) ve üretim öğreticilerine [dağıtmak için](deploying-to-production.md) yapmanız gerekir.

## <a name="summary"></a>Özet

Yayımlama profillerini oluşturmadan önce *Web. config* dönüşümlerine sahip olduğunuz kadar çok şey yaptınız ve dağıtılan Web. config dosyasında nelerin olacağını gördünüz.

![Konum dönüştürmesinin önizlemesi](web-config-transformations/_static/image8.png)

Aşağıdaki öğreticide, proje özelliklerinin ayarlanmasını gerektiren dağıtım kurulum görevlerinin ele alınır.

## <a name="more-information"></a>Daha Fazla Bilgi

Bu öğreticinin kapsadığı konular hakkında daha fazla bilgi için bkz. Web. config dönüşümlerini kullanarak Visual Studio ve ASP.NET için Web dağıtımı Içerik haritasında [dağıtım sırasında hedef Web. config dosyasında veya App. config dosyasında ayarları değiştirme](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms) .

> [!div class="step-by-step"]
> [Önceki](preparing-databases.md)
> [İleri](project-properties.md)
