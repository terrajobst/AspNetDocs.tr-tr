---
uid: visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
title: Visual Studio 2013 Sürüm notları için ASP.NET and Web Tools 2013,2 | Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 03/06/2014
ms.assetid: 7ef5f73c-ca60-43c1-bdb2-702800347e7e
msc.legacyurl: /visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
msc.type: authoredcontent
ms.openlocfilehash: 22d4d4afd6963f23d6cfef1745a859c20b69d599
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623195"
---
# <a name="aspnet-and-web-tools-20132--for-visual-studio-2013-release-notes"></a>Visual Studio 2013 için ASP.NET and Web Tools 2013.2 Sürüm Notları

[Microsoft](https://github.com/microsoft) tarafından

## <a name="installation-notes"></a>Yükleme notları

Visual Studio 2013,2 için ASP.NET and Web Tools ana yükleyicide paketlenmiştir ve [Visual Studio 2013 güncelleştirme 2](https://go.microsoft.com/fwlink/?LinkId=390521)' nin bir parçası olarak indirilebilir.

## <a name="documentation"></a>Belgeler

Visual Studio 2013,2 için ASP.NET and Web Tools hakkında öğreticiler ve diğer bilgiler [ASP.NET Web sitesinden](https://www.asp.net/)edinilebilir.

## <a name="software-requirements"></a>Yazılım Gereksinimleri

Visual Studio 2013,2 için ASP.NET and Web Tools Visual Studio 2013 gerekir.

## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-20132"></a>Visual Studio 2013,2 için ASP.NET and Web Tools yeni özellikler

Aşağıdaki bölümlerde, sürümünde tanıtılan özellikler açıklanır.

- [Bir ASP.NET proje şablonu](#oneaspnet)
- [IIS Express üzerinde Web uygulamaları başlatırken SSL desteği](#ssl)
- [Visual Studio Web Düzenleyicisi geliştirmeleri](#vswebeditor)
- [Tarayıcı Bağlantısı](#browserlink)
- [Visual Studio 'da Azure App Service Web Apps için destek](#waws)
- [Yeni bir Web projesi oluştururken uzak Azure kaynakları oluştur](#AzureResources)
- [Web yayımlama geliştirmeleri](#webpublish)
- [ASP.NET Scafkatlama](#scaffolding)
- [NuGet 2.8.1](#nuget)
- [ASP.NET Web Forms](#webforms)
- [ASP.NET MVC 5.1.2](#mvc)
- [ASP.NET Web API 2.1.2 'yi](#webapi)
- [ASP.NET Web Pages 3.1.2](#webpages)
- [Entity Framework 6,1](#ef)
- [ASP.NET Identity 2.0.0](#identity)
- [Microsoft OWIN bileşenleri](#owin)
- [ASP.NET SignalR 2.0.2](#signalr)

<a id="oneaspnet"></a>
### <a name="one-aspnet-project-templates"></a>Bir ASP.NET proje şablonu

- Hesap onaylama ve parola sıfırlamayı desteklemek için ASP.NET proje şablonlarına yönelik güncelleştirmeler.
- Şirket Içi kurumsal hesapları kullanarak kimlik doğrulamasını desteklemek için ASP.NET Web API şablonunu güncelleştirin.
- ASP.NET SPA şablonu artık MVC ve sunucu tarafı görünümlerini temel alan kimlik doğrulamasını içerir. Şablonda yalnızca kimliği doğrulanmış kullanıcılar tarafından erişilebilen bir WebAPI denetleyicisi vardır.

<a id="ssl"></a>
### <a name="support-ssl-when-launching-web-applications-on-iis-express"></a>IIS Express üzerinde Web uygulamaları başlatırken SSL desteği

Localhost üzerinde gözatarken ve hata ayıklarken güvenlik uyarısını ortadan kaldırmak için Internet Explorer ve Chrome 'un otomatik olarak imzalanan IIS Express SSL sertifikasına güvenmesine izin veren bir iletişim kutusu ekledik.

Örneğin, bir Web projesi özelliği SSL kullanmak üzere ayarlanabilir. Özellikler iletişim kutusunu açmak için F4 ' e tıklayın. **SSL etkin** ' i true olarak değiştirin. SSL URL 'sini kopyalayın.

![SSL etkin özelliği](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image1.png)

Web projesi Özellik sayfası Web sekmesini HTTPS tabanlı URL 'YI kullanacak şekilde ayarlayın (SSL URL 'SI, daha önce SSL Web siteleri oluşturmadığınız müddetçe `https://localhost:44300/` olur.)

![Proje URL 'sini (HTTPS) ayarla](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image2.png)

Uygulamayı çalıştırmak için CTRL+F5'e basın. IIS Express oluşturduğu kendinden imzalı sertifikaya güvenmek için yönergeleri izleyin.

![SSL uyarısı](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image3.png)

**Güvenlik uyarısı** iletişim kutusunu okuyun ve ardından localhost 'u temsil eden sertifikayı yüklemek istiyorsanız **Evet** ' e tıklayın.

![Güvenlik Uyarısı](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image4.png)

Site, tarayıcıda sertifika uyarısı olmadan IE veya Chrome 'da gösterilir.

![Uyarı olmadan HTTPS sayfası](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image5.png)

Firefox kendi sertifika deposunu kullanır, bu nedenle bir uyarı görüntüler.

<a id="vswebeditor"></a>
### <a name="visual-studio-web-editor-enhancements"></a>Visual Studio Web Düzenleyicisi geliştirmeleri

- **Yenı JSON proje öğesi ve Düzenleyicisi**: Visual Studio 'ya bir JSON proje öğesi ve Düzenleyicisi ekledik. Geçerli JSON Düzenleyicisi özellikleri renklendirme, sözdizimi doğrulaması, küme ayracı tamamlama, ana hat, Araçlar seçenek ayarı ve daha fazlasını içerir.

    ![JSON Düzenleyicisi](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image6.png)

    IntelliSense artık [JSON şeması](http://json-schema.org/) v3 ve v4 'yi destekliyor. Var olan şemaları seçmek için bir şema açılan kutusu bulunur, yerel şema yolunu düzenleyebilir veya bir proje JSON dosyasını buraya sürükleyerek göreli yolu alın.

    ![JSON IntelliSense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image7.png)    ![JSON Şema Düzenleyicisi](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image8.png)
- **Yeni Sass (SCSS) Düzenleyicisi**: VS2013 RTM 'ye daha az ekledik ve artık bir Sass proje öğesi ve düzenleyicimiz var. Sass Düzenleyici özellikleri, daha az düzenleyiciyle karşılaştırılabilir ve renklendirme, değişken ve Mixins IntelliSense, açıklama/açıklama, hızlı bilgi, biçimlendirme, sözdizimi doğrulama, ana hat, goto tanımı, renk seçici, Araçlar seçenek ayarı vb. dahil olmak üzere daha az düzenleyiciye benzer.

    ![Yeni öğe Ekle: SCSS stil sayfası](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image9.png)    ![Stil sayfası Düzenleyicisi](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image10.png)
- **HTML, Razor, CSS, daha az ve Sass belgelerindeki yenı URL seçicisi:** VS 2013, Web Forms sayfaların dışında URL seçici olmadan sevk edildi. HTML, Razor, CSS, LESS ve Sass düzenleyicilerinin yeni URL Seçicisi, '.. ' öğesini anlayan bir iletişim kutusu ücretsiz, akıcı yazı seçicisinin ve dosya listelerine img etiketleri ve bağlantıları için uygun şekilde filtre uygular.

    ![Resim etiketi için URL seçici](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image11.png)    ![Görünümler için URL seçici](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image12.png)    ![CSS URL Seçicisi](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image13.png)
- **Daha fazla özellik ekleyerek daha az düzenleyicide güncelleştirme yapın**
- **IntelliSense yükseltmesini altını gizleme**: vs IntelliSense, "Ko-vs-Editor ViewModel:" söz dizimi için standart olmayan bir altını gizleme sözdizimi ekledik. Bu, formdaki açıklamaları kullanarak bir sayfada birden çok görünüm modeline bağlamak için kullanılabilir:

    ![Altını gizleme IntelliSense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image14.png)

    Ayrıca, iç içe geçmiş ViewModel IntelliSense için destek ekledik. bu nedenle, ViewModel üzerinde derin iç içe geçmiş nesnelerde detaya inebilir.

    `<div data-bind="text: foo.bar.baz.etc" />`

    Görünen IntelliSense, JavaScript nesnesinin tam IntelliSense ' dir.

    ![Tam JavaScript nesnesini gösteren IntelliSense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image15.png)
- **HTML, Razor, CSS, daha az ve Sass belgelerindeki yenı URL Seçicisi**: vs 2013, Web Forms SAYFALARıN dışında URL seçici olmadan sevk edildi. HTML, Razor, CSS, LESS ve Sass düzenleyicilerinin yeni URL Seçicisi, '.. ' öğesini anlayan bir iletişim kutusu ücretsiz, akıcı yazı seçicisinin ve dosya listelerine img etiketleri ve bağlantıları için uygun şekilde filtre uygular.

    ![Resim etiketi için URL seçici](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image16.png)    ![Görünümler için URL seçici](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image17.png)    ![CSS URL Seçicisi](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image18.png)

<a id="browserlink"></a>
### <a name="browser-link"></a>Tarayıcı Bağlantısı

- Tarayıcı bağlantısı artık HTTPS bağlantılarını destekliyor ve bu durumda, sertifikaya tarayıcıda güvenildiği sürece diğer bağlantılarla panoda listelenir.
- Statik HTML kaynağı eşleme
- Veri eşleme için SPA desteği
- Eşleme verilerini otomatik güncelleştir

<a id="waws"></a>
### <a name="support-for-azure-app-service-web-apps-in-visual-studio"></a>Visual Studio 'da Azure App Service Web Apps için destek

- **Azure oturum açma desteği.**
- **Uzaktan hata ayıklama ve Web Apps Için uzak görünüm**: artık Sunucu Gezgininde Web Apps içerik dosyalarının Azure App Service ve uzak görünümündeki [Web uygulamaları için uzaktan hata ayıklamayı](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio) destekliyoruz.

<a id="AzureResources"></a>
### <a name="create-remote-azure-resources-when-creating-a-new-web-project"></a>Yeni bir Web projesi oluştururken uzak Azure kaynakları oluştur

Yeni Web uygulaması iletişim kutusunda bir Azure ["Uzak kaynaklar oluştur"](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) onay kutusunu ekledik. Bunu seçerek, yeni bir Web uygulaması oluşturma, test için Azure yayımlama sitesini ayarlama ve birkaç basit adımda yayımlama profili oluşturma deneyimini tümleştirebileceksiniz.

![Azure kaynakları ile yeni proje](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image19.png)![Azure 'da yayımlama](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image20.png)

<a id="webpublish"></a>
### <a name="web-publish-enhancements"></a>Web yayımlama geliştirmeleri

- Yayımlama için Kullanıcı deneyimini geliştirme.

<a id="scaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET Scafkatlama

- **Sabit listesi desteği:** Modelinize enum 'lar kullanılıyorsa, MVC Scaffolder, numaralandırma için açılan menü oluşturacaktır. Bu, MVC 'de numaralandırma yardımcıları kullanır.
- **Önyükleme desteği**: önyükleme sınıflarını KULLANABILMESI için MVC yapı iskelesi Içindeki şablonlar için editorupdated güncelleştirildi.
- **Paket desteği**: MVC ve Web API 'Si Scaffolders, MVC ve Web API 'si için 5,1 paketleri ekler

Aşağıdaki ekran görüntüleri, yapı iskelesi modellerini göstermektedir.

- Model kodu:

     ![Model kodu](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image21.png)
- Model kodunu derleyin, sağ tıklayın ve **Ekle**, **Yeni Iskele öğe öğesi**' ni seçin.

     ![Yeni yapı Iskelesi öğesi Ekle](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image22.png)
- **Entity Framework kullanarak görünümler Ile MVC5 denetleyicisi**seçin:

     ![Görünümlerle yeni MVC5 denetleyicisi ekleme](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image23.png)
- Modeli kullanarak **Denetleyici ekleyin** :

    ![](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image24.png)
- Oluşturulan kodu denetleyin (örneğin, görünümler/Weekdaymodeller/Edit. cshtml) `@Html.EnumDropDownListFor`:](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image25.png) Enumdropdownlistiçeren ![görünümünü içerir
- Enum ComboBox 'ın oluşturulduğunu görmek için sayfayı çalıştırın. bir değer null ise, Birleşik giriş kutusu için boş bir dize seçilebilir olduğunu unutmayın. Örneğin, **Oluştur** sayfası aşağıdakileri gösterir:

    ![Boş dizeye izin veren Birleşik giriş kutusu](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image26.png)

<a id="nuget"></a>
### <a name="nuget-281"></a>NuGet 2.8.1

NuGet 2.8.1 RTM, Nisan 2014 ' de yayımlanacak. Sürüm notlarından oluşan önemli noktalar şunlardır, ancak bu değişiklikler hakkında daha fazla bilgi için lütfen [tam sürüm notlarını](http://docs.nuget.org/docs/release-notes/nuget-2.8) gözden geçirin.

- **Hedef Windows Phone 8,1 uygulamaları**: NuGet 2.8.1 artık ' WindowsPhoneApp ', ' WPA ', ' WindowsPhoneApp81 ' ve ' WPA81 ' hedef Framework takma adları kullanılarak Windows Phone 8,1 uygulamalarının hedeflenmesini destekliyor.

- **Bağımlılıklar Için düzeltme eki çözümü**: paket bağımlılıklarını çözümlerken, NuGet geçmişte, paketteki bağımlılıkları karşılayan en düşük ana ve ikincil paket sürümünü seçme stratejisi uygulamış. Ancak, büyük ve küçük sürümden farklı olarak, düzeltme eki sürümü her zaman en yüksek sürüme çözümlenmelidir. Davranış iyi bir şekilde olsa da, bağımlılıkları olan paketleri yüklemek için bir belirleyici eksiklik oluşturmıştı.
- **Dependencyversion anahtarı**: NuGet 2,8, bağımlılıkları çözümlemek için *varsayılan* davranışı değiştirse de, Paket Yöneticisi konsolundaki-dependencyversion anahtarı aracılığıyla bağımlılık çözümleme işlemi üzerinde daha kesin denetim de ekler. Anahtar olası en düşük sürüme (varsayılan davranış), mümkün olan en yüksek sürüme veya en yüksek alt veya düzeltme eki sürümüne bağımlılıkları çözmeyi sağlar. Bu anahtar yalnızca PowerShell komutunda install-Package için geçerlidir.
- **Dependencyversion özniteliği**: yukarıda açıklanan-dependencyversion anahtarına ek olarak, NuGet. config dosyasında varsayılan değerin ne olduğunu tanımlayan,-dependencyversion anahtarı bir Install-Package çağrısında belirtilmemişse NuGet. config dosyasında yeni bir öznitelik ayarlayabilme özelliği de buna izin verilir. Bu değer, herhangi bir paket yüklemesi işlemi için NuGet Paket Yöneticisi Iletişim kutusu tarafından da kullanılacaktır. Bu değeri ayarlamak için aşağıdaki özniteliği NuGet. config dosyanıza ekleyin:

    `<config> <add key="dependencyversion" value="Highest" /> </config>`
- **-WhatIf Ile NuGet Işlemlerini önizleyin**: bazı NuGet paketlerinde derin bağımlılık grafikleri bulunabilir ve bu nedenle, ne olacağını görmek için bir yükleme, kaldırma veya güncelleştirme işlemi sırasında yararlı olabilir. NuGet 2,8, standart PowerShell 'i ekler-Install-Package, Uninstall-Package ve Update-Package komutları, komutun uygulanacağı paketlerin tüm kapanışına görselleştirmeyi etkinleştirmek için kullanılır.
- **Paketi düşürme**: yeni özellikleri araştırmak ve sonra son kararlı sürüme geri alma kararı vermek için bir paketin ön sürümü sürümünün yüklenmesi yaygın olmayan bir durumdur. NuGet 2,8 ' den önce bu, ön sürüm paketini ve bağımlılıklarını kaldırıp daha sonra önceki sürümü yüklerken çok adımlı bir işlemdir. Ancak NuGet 2,8 ile, güncelleştirme paketi artık tüm paket kapatılmasını (ör. paketin bağımlılık ağacı) önceki sürüme geri alacak.
- **Geliştirme bağımlılıkları**: geliştirme sürecini iyileştirmek için kullanılan araçlar da dahil olmak üzere birçok farklı özellik türü NuGet paketleri olarak teslim edilebilir. Bu bileşenler, yeni bir paket geliştirilirken, daha sonra yayımlandığında yeni paketin bağımlılığı olarak değerlendirilmemelidir. NuGet 2,8, bir paketin kendisini. nuspec dosyasında bir developmentDependency olarak belirlemesine olanak sağlar. Yüklendiğinde, bu meta veriler paketin yüklendiği projenin Packages. config dosyasına da eklenecektir. Bu paket. config dosyası daha sonra NuGet. exe paketi sırasında NuGet bağımlılıkları için çözümlendikten sonra, bu bağımlılıklar geliştirme bağımlılıkları olarak işaretlenir.
- **Farklı platformlar Için tek tek paketleri. config dosyaları**: birden çok hedef platform için uygulama geliştirirken, ilgili Yapı ortamlarının her biri için farklı proje dosyaları olması yaygındır. Farklı proje dosyalarındaki farklı NuGet paketlerini kullanmak da yaygındır, çünkü paketler farklı platformlar için farklı destek düzeylerine sahiptir. NuGet 2,8, platforma özgü farklı proje dosyaları için farklı Packages. config dosyaları oluşturarak bu senaryoya yönelik gelişmiş destek sağlar.
- **Yerel önbelleğe geri dönüş**: NuGet paketleri genellikle bir ağ bağlantısı kullanan [NuGet Galerisi](http://www.nuget.org) gibi uzak bir galeriden tüketilebilse de, istemcinin bağlı olmadığı birçok senaryo vardır. Ağ bağlantısı olmadan, NuGet istemcisi paketleri başarılı bir şekilde yükleyemedi-bu paketler, yerel NuGet önbelleğindeki istemci makinesinde zaten mevcut olduğunda bile. NuGet 2,8, Paket Yöneticisi konsoluna otomatik önbellek geri dönüşü ekler.

    Önbellek geri dönüş özelliği belirli bir komut bağımsız değişkeni gerektirmez. Ayrıca, şu anda önbellek geri dönüşü yalnızca Paket Yöneticisi konsolunda çalışır; bu davranış Şu anda Paket Yöneticisi iletişim kutusunda çalışmıyor.
- **Hata düzeltmeleri**: Update-Package-REINSTALL komutunda performans iyileştirmesinden oluşan önemli hata düzeltmelerinden biri.

    Bu özelliklere ve belirtilen performans düzeltmesine ek olarak, NuGet 'in bu sürümü diğer birçok hata düzeltmesini de içerir. Yayında ele alınan toplam 181 sorun oluştu. NuGet 2,8 ' de düzeltilen iş öğelerinin tam listesi için lütfen bu yayın için [NuGet sorun İzleyicisi](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all) ' ni görüntüleyin.

<a id="webforms"></a>
### <a name="aspnet-web-forms"></a>ASP.NET Web Forms

- Web Forms şablonlar artık ASP.NET Identity için hesap onaylama ve parola sıfırlama işlemlerinin nasıl yapılacağını gösterir.
- Entity Framework 6 için varlık veri kaynağı denetimi ve Dinamik Veri Sağlayıcısı. Daha fazla ayrıntı için lütfen şu MSDN bloguna bakın: [Entity Framework 6 Için dinamik veri sağlayıcısı ve EntityDataSource denetimi](https://blogs.msdn.com/b/webdev/archive/2014/01/30/announcing-preview-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx).

<a id="mvc"></a>
### <a name="aspnet-mvc-512"></a>ASP.NET MVC 5.1.2

- [Öznitelik yönlendirme geliştirmeleri](../../../mvc/overview/releases/mvc51-release-notes.md#AttributeRouting)
- [Düzenleyici şablonları için önyükleme desteği](../../../mvc/overview/releases/mvc51-release-notes.md#Bootstrap)
- [Görünümlerde enum desteği](../../../mvc/overview/releases/mvc51-release-notes.md#Enum)
- [MinLength/MaxLength öznitelikleri için unobtrusive desteği](../../../mvc/overview/releases/mvc51-release-notes.md#Unobtrusive)
- [Unobtrusive Ajax 'ta ' this ' bağlamını destekleme](../../../mvc/overview/releases/mvc51-release-notes.md#thisContext)
- Çeşitli [hata düzeltmeleri](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=MVC&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webapi"></a>
### <a name="aspnet-web-api-212"></a>ASP.NET Web API 2.1.2 'yi

- [Genel hata işleme](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#global-error)
- [Öznitelik yönlendirme geliştirmeleri](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#attribute-routing)
- [Yardım sayfası geliştirmeleri](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#help-page)
- [IgnoreRoute desteği](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#ignoreroute)
- [BSON medya türü biçimlendirici](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#bson)
- [Zaman uyumsuz filtreler için daha iyi destek](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#async-filters)
- [İstemci biçimlendirme kitaplığı için sorgu ayrıştırma](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#query-parsing)
- Çeşitli [hata düzeltmeleri](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20API%7cWeb%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webpages"></a>
### <a name="aspnet-web-pages-312"></a>ASP.NET Web Pages 3.1.2

- Çeşitli [hata düzeltmeleri](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20Pages/Razor&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="ef"></a>
### <a name="entity-framework-61"></a>Entity Framework 6,1

Entity Framework hem çalışma zamanı hem de araçları için sürüm 6,1 ' e güncelleştirilmiştir. Entity Framework (EF) 6,1, Entity Framework 6 ' a yönelik küçük bir güncelleştirmedir ve çeşitli hata düzeltmeleri ve yeni özellikler içerir. Yeni özelliklere yönelik belgelerin bağlantıları dahil olmak üzere EF 6.1 hakkında ayrıntılı bilgi için bkz. [Entity Framework Version History](https://msdn.microsoft.com/data/jj574253). Bu sürümdeki yeni özellikler şunlardır:

- **Araç birleştirme** , yenı bir EF modeli oluşturmak için tutarlı bir yol sağlar. Bu özellik, var olan bir veritabanından ters mühendislik dahil olmak üzere Code First modelleri oluşturmayı desteklemek için ADO.NET Varlık Veri Modeli Sihirbazı 'nı genişletir. Bu özellikler daha önce, EF güç araçlarında Beta kalitede kullanıma sunulmuştur.
- **İşlem işleme hatalarının işlenmesi** , işlem işlemlerini ele almak için yeni tanıtılan özelliği kullanan yeni [System. Data. Entity. Infrastructure. commitfailurehandler](https://msdn.microsoft.com/library/system.data.entity.infrastructure.commitfailurehandler(v=vs.113).aspx) sağlar. **Commitfailurehandler** , işlem yürüten bağlantı hatalarından otomatik kurtarmaya izin verir.
- **Indexattribute** , Code First modelinizdeki bir özelliğe (veya özelliklere) bir öznitelik yerleştirilerek dizinlerin belirtilmesini sağlar. Code First, veritabanında karşılık gelen bir dizin oluşturur.
- **Ortak eşleme API 'si** , Özellikler ve türlerin veritabanındaki sütunlara ve tablolarla nasıl eşlendiğine ilişkin EF bilgisine erişim sağlar. Geçmişte bu API, iç sürümiydi.
- Uygulama **/Web. config dosyası aracılığıyla yakalayıcılar yapılandırma**(uygulamayı yeniden derlemeden bir dinleyici eklenmesine izin verme).
- **Databasegünlükçü** , tüm veritabanı işlemlerini bir dosyaya günlüğe kaydetmek kolay hale getiren yeni bir yakalayıcısı. Önceki özellikle birlikte, bu, yeniden derlemenize gerek kalmadan dağıtılan bir uygulama için veritabanı işlemlerinin günlüğe kaydedilmesini kolayca değiştirmenize olanak sağlar.
- **Geçiş modeli değişikliği algılaması** geliştirilmiştir, böylece yapı iskelesi geçişleri daha doğru olur; değişiklik algılama sürecinin performansı de büyük ölçüde geliştirilmiştir.
- Başlatma sırasında azaltılmış veritabanı işlemleri, LINQ sorgularında null eşitlik karşılaştırması için iyileştirmeler, daha hızlı görünüm oluşturma (model oluşturma) ve birden çok ilişki içeren izlenen varlıkların daha verimli bir şekilde hazırlanması gibi **performans iyileştirmeleri** .

<a id="identity"></a>
### <a name="aspnet-identity-200"></a>ASP.NET Identity 2.0.0

- **İki öğeli kimlik doğrulaması**: ASP.NET Identity artık iki öğeli kimlik doğrulamasını desteklemektedir. İki öğeli kimlik doğrulama, parolanızın tehlikeye düşmesi durumunda kullanıcı hesaplarınıza ek bir güvenlik katmanı sağlar. Ayrıca iki faktör koduna karşı deneme yanılma saldırılarına karşı koruma de vardır.
- **Hesap kilitleme:** Kullanıcı parolasını veya iki öğeli kodları yanlış girerse kullanıcıyı kilitlemek için bir yol sağlar. Geçersiz deneme sayısı ve kullanıcılar için TimeSpan değeri yapılandırılabilir. Bir geliştirici, isteğe bağlı olarak belirli kullanıcı hesapları için hesap kilitlemeyi kapatabilir.
- **Hesap onayı:** ASP.NET Identity sistem artık hesap onayını desteklemektedir. Bu, Web sitesinde yeni bir hesap için kayıt yaptırdığınızda, Web sitesinde bir şey yapmadan önce e-postanızı onaylamanız gerektiğinde, çoğu web sitesinde bugün çok yaygın bir senaryodur. Sahte hesapların oluşturulmasını önlediği için e-posta onayı kullanışlıdır. Forum siteleri, bankacılık, eTicaret veya sosyal web siteleri gibi Web sitenizin kullanıcılarıyla iletişim kurmak için bir yöntem olarak e-posta kullanıyorsanız bu son derece yararlıdır.
- **Parola sıfırlama:** Parola sıfırlama, kullanıcının parolasını unutmaları durumunda parolalarını sıfırlayabileceği bir özelliktir.
- **Güvenlik damgası (her yerde oturum Kapat):** Kullanıcı parolasını değiştirdiğinde Kullanıcı veya ilişkili bir oturum açma (Facebook, Google, Microsoft hesabı vb. gibi güvenlikle ilgili herhangi bir bilgi) gibi güvenlik belirtecini yeniden oluşturmanın bir yolunu destekler. Bu, eski parolayla oluşturulan belirteçlerin geçersiz kılındığından emin olmak için gereklidir. Örnek projede, kullanıcının parolasını değiştirirseniz, Kullanıcı için yeni bir belirteç oluşturulur ve önceki belirteçler geçersiz kılınır. Bu özellik, parolanızı değiştirdiğinizde uygulamanıza ek bir güvenlik katmanı sağlar, bu uygulamada oturum açtığınız her yerde (diğer tüm tarayıcılar) oturumunuz açılır.
- **Birincil anahtar türü kullanıcılar ve roller için Genişletilebilir olsun**: ASP.NET Identity 1,0 ' de, tablo kullanıcıları ve rollerinin birincil anahtar türü dizelerdir. Bu, ASP.NET Identity sisteminin Entity Framework kullanarak SQL Server kalıcı hale geldiğini, nvarchar kullandığımızda olduğunu gösterir. Bu varsayılan uygulama etrafında Stack Overflow ve gelen geri bildirime göre birçok tartışma vardı. Kullanıcılarınızın ve rol tablonuzun birincil anahtarı ne olması gerektiğini belirtebileceğiniz bir genişletilebilirlik kancası sağladık. Uygulamanızı geçiriyorsanız bu genişletilebilirlik kancası özellikle yararlıdır ve uygulama kullanıcı kimliklerini depoladığında, GUID 'Ler veya litre olur.
- **Kullanıcılar ve roller üzerinde IQueryable desteği**: Userssson ve rolessstore üzerinde IQueryable desteği eklendi, Kullanıcı ve rol listesini kolayca alabilirsiniz.
- **UserManager aracılığıyla silme işlemini destekleme**
- **Kullanıcı adında dizin oluşturma**: ASP.NET Identity Entity Framework UYGULAMASıNDA, EF 6.1.0 Içinde Yeni ındexattribute kullanarak Kullanıcı adına benzersiz bir dizin ekledik. Bu, Kullanıcı adlarının her zaman benzersiz olduğundan ve yinelenen kullanıcı adlarıyla bitebilmeniz için bir yarış durumu olmadığından emin olur.
- **Gelişmiş parola doğrulayıcısı:** ASP.NET Identity 1,0 ' de gönderilen parola Doğrulayıcısı, yalnızca minimum uzunluğu doğrulayan oldukça temel bir parola doğrulayıcısıdır. Parolanın karmaşıklığı üzerinde size daha fazla denetim sağlayan yeni bir parola doğrulayıcısı vardır. Bu parolada tüm ayarları açmış olsanız bile, Kullanıcı hesapları için iki öğeli kimlik doğrulamayı etkinleştirmenizi öneririz.
- **Identityfactory ara yazılımı/CreatePerOwinContext**:

    - **Kullanıcı Yöneticisi**: Owin bağlamından UserManager 'ın bir örneğini almak için fabrika uygulamasını kullanabilirsiniz. Bu model, oturum açma ve SignOut için OWIN bağlamından AuthenticationManager almak üzere kullandığımız şeydir. Bu, uygulama için istek başına UserManager örneği elde etmenin önerilen bir yoludur.
    - **Dbcontextfactory**: ASP.NET Identity, SQL Server kimlik sistemini kalıcı hale getiren Entity Framework kullanır. Bunu yapmak için kimlik sisteminin ApplicationDbContext başvurusu vardır. DbContextFactory ara yazılımı, uygulamanızda kullanabileceğiniz istek başına ApplicationDbContext örneğini döndürür.
- **ASP.NET Identity örnekleri NuGet paketi**: örnekler NuGet paketi, ASP.NET Identity için örnekleri yüklemeyi ve çalıştırmayı kolaylaştırabilir ve en iyi yöntemleri takip edebilir. Bu örnek bir ASP.NET MVC uygulamasıdır. Üretim ortamında dağıtmadan önce lütfen kodu uygulamanıza uyacak şekilde değiştirin. Örnek, boş bir ASP.NET uygulamasına yüklenmelidir. Paket hakkında daha fazla bilgi için şu blog gönderisine gidin: [ASP.NET Identity 2.0.0 for RTM](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx)

<a id="owin"></a>
### <a name="microsoft-owin-components"></a>Microsoft OWIN bileşenleri

Bu sürümde düzeltilen çok sayıda hata oluştu. Daha ayrıntılı bilgi için lütfen [2.1.0 sürümü için sürüm notlarına](https://katanaproject.codeplex.com/releases/view/113281) bakın.

<a id="signalr"></a>
### <a name="aspnet-signalr-202"></a>ASP.NET SignalR 2.0.2

Bu sürümde düzeltilen çok sayıda hata oluştu. Daha ayrıntılı bilgi için lütfen [2.0.2 sürümü için sürüm notlarına](https://github.com/SignalR/SignalR/releases/tag/2.0.2) bakın.
