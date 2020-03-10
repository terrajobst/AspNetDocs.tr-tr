---
uid: visual-studio/overview/2013/release-notes
title: Visual Studio 2013 Sürüm notları için ASP.NET and Web Tools | Microsoft Docs
author: microsoft
description: Bu belgede Visual Studio 2013 için ASP.NET and Web Tools sürümü açıklanmaktadır.
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: d8af9c8e7ee1316a5eac90c5959d07c628154e09
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557934"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a>Visual Studio 2013 için ASP.NET and Web Tools Sürüm Notları

[Microsoft](https://github.com/microsoft) tarafından

> Bu belgede Visual Studio 2013 için ASP.NET and Web Tools sürümü açıklanmaktadır.

## <a name="contents"></a>İçindekiler

- [Yükleme notları](#TOC1)
- [Belgeler](#TOC2)
- [Yazılım gereksinimleri](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>Visual Studio 2013 için ASP.NET and Web Tools yeni özellikler

- [Bir ASP.NET](#TOC6)
- [Yeni Web projesi deneyimi](#newproj)
- [ASP.NET Scafkatlama](#scaffold)
- [Tarayıcı Bağlantısı](#browser-link)
- [Visual Studio Web Düzenleyicisi geliştirmeleri](#web-editor)
- [Visual Studio 'da Web Apps Azure App Service desteği](#waws)
- [Web yayımlama geliştirmeleri](#publish)
- [NuGet 2.7](#nuget)
- [ASP.NET Web Forms](#TOC9)
- [ASP.NET MVC 5](#TOC10)
- [ASP.NET Web API 2](#TOC11)
- [ASP.NET SignalR](#TOC13)
- [ASP.NET Identity](#TOC8)
- [Microsoft OWIN bileşenleri](#TOC7)
- [Entity Framework 6](#ef6)
- [ASP.NET Razor 3](#TOC14)
- [ASP.NET uygulama askıya alma](#TOC15)
- [Bilinen sorunlar ve son değişiklikler](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a>Yükleme notları

Visual Studio 2013 için ASP.NET and Web Tools ana yükleyicide paketlenmiştir ve [buradan](https://www.asp.net/downloads)indirilebilir.

<a id="TOC2"></a>
## <a name="documentation"></a>Belgeler

Visual Studio 2013 için ASP.NET and Web Tools hakkında öğreticiler ve diğer bilgiler [ASP.NET Web sitesinden](https://www.asp.net/)edinilebilir.

<a id="TOC4"></a>
## <a name="software-requirements"></a>Yazılım Gereksinimleri

ASP.NET and Web Tools Visual Studio 2013 gerektiriyor.

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>Visual Studio 2013 için ASP.NET and Web Tools yeni özellikler

Aşağıdaki bölümlerde, sürümünde tanıtılan özellikler açıklanır.

<a id="TOC6"></a>
## <a name="one-aspnet"></a>Bir ASP.NET

Visual Studio 2013 sürümünde, ASP.NET teknolojilerini kullanma deneyiminden kaçınmayı bir adım gerçekleştirdik. böylece, istediğiniz olanları kolayca karıştırıp eşleştirebilirsiniz. Örneğin, MVC kullanarak bir proje başlatabilir ve daha sonra projeye Web Forms sayfaları ekleyebilir ve bir Web Forms projesindeki Web API 'Lerini daha sonra kolayca ekleyebilirsiniz. Tek bir ASP.NET, bir geliştirici olarak ASP.NET 'de sevdiğiniz şeyleri yapmanızı kolaylaştırır. Ne tercih ettiğiniz teknolojide olsun, bir ASP.NET 'ın güvenilen temel çatısı üzerinde derleme yaptığınız güveniniz olabilir.

<a id="newproj"></a>
## <a name="new-web-project-experience"></a>Yeni Web projesi deneyimi

Visual Studio 2013 yeni Web projeleri oluşturma deneyimini geliştirdik. **Yeni ASP.NET Web projesi** iletişim kutusunda istediğiniz proje türünü seçebilir, teknolojilerin herhangi bir birleşimini (Web Forms, MVC, Web API) yapılandırabilir, kimlik doğrulama seçeneklerini yapılandırabilir ve bir birim testi projesi ekleyebilirsiniz.

![Yeni ASP.NET projesi](release-notes/_static/image1.png)

Yeni iletişim kutusu, şablonların birçoğu için varsayılan kimlik doğrulama seçeneklerini değiştirmenize olanak sağlar. Örneğin, bir ASP.NET Web Forms projesi oluşturduğunuzda, aşağıdaki seçeneklerden herhangi birini seçebilirsiniz:

- Kimlik Doğrulaması Yok
- Bireysel kullanıcı hesapları (ASP.NET üyeliği veya sosyal sağlayıcı oturum açma)
- Kuruluş hesapları (bir Internet uygulamasındaki Active Directory)
- Windows kimlik doğrulaması (bir intranet uygulamasında Active Directory)

![Kimlik doğrulaması seçenekleri](release-notes/_static/image2.png)

Web projeleri oluşturmaya yönelik yeni süreç hakkında daha fazla bilgi için, bkz. [Visual Studio 2013 ASP.NET Web projeleri oluşturma](creating-web-projects-in-visual-studio.md). Yeni kimlik doğrulama seçenekleri hakkında daha fazla bilgi için bu belgede daha sonra [ASP.NET Identity](#TOC8) bölümüne bakın.

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a>ASP.NET Scafkatlama

ASP.NET Scafkatlama, ASP.NET Web uygulamaları için bir kod oluşturma çerçevesidir. Projenize bir veri modeliyle etkileşim kuran ortak kod eklemenizi kolaylaştırır.

Visual Studio 'nun önceki sürümlerinde, scafkatlama ASP.NET MVC projeleriyle sınırlandırılmıştır. Visual Studio 2013, artık Web Forms dahil olmak üzere herhangi bir ASP.NET projesi için scafkatlamayı kullanabilirsiniz. Visual Studio 2013, şu anda bir Web Forms projesi için sayfa oluşturmayı desteklemez, ancak projeye MVC bağımlılıkları ekleyerek Web Forms ile yapı iskelesi kullanmaya devam edebilirsiniz. Web Forms için sayfa oluşturma desteği gelecekteki bir güncelleştirmeye eklenecektir.

Yapı iskelesi kullanılırken, gerekli tüm bağımlılıkların projede yüklü olduğundan emin veriyoruz. Örneğin, bir ASP.NET Web Forms projesiyle başlayıp bir Web API denetleyicisi eklemek için scafkatlamayı kullanıyorsanız, gerekli NuGet paketleri ve başvuruları projenize otomatik olarak eklenir.

Web Forms projesine MVC yapı iskelesi eklemek için **Yeni bir yapı** İskelesi ekleyin ve Iletişim penceresinde **MVC 5 bağımlılıklarını** seçin. Yapı iskelesi MVC için iki seçenek vardır; En az ve tam. En az ' ı seçerseniz, projenize yalnızca NuGet paketleri ve ASP.NET MVC başvuruları eklenir. Tam seçeneğini belirlerseniz, en düşük bağımlılıklar ve bir MVC projesi için gerekli içerik dosyaları eklenir.

Yapı iskelesi zaman uyumsuz denetleyiciler desteği Entity Framework 6 ' dan gelen yeni zaman uyumsuz özellikleri kullanır.

Daha fazla bilgi ve öğretici için bkz. [ASP.net Scafkate genel bakış](aspnet-scaffolding-overview.md).

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a>Tarayıcı bağlantısı – tarayıcı ve Visual Studio arasında SignalR kanalı

Yeni [tarayıcı bağlantısı](using-browser-link.md) özelliği, birden çok tarayıcıyı Visual Studio 'ya bağlamanıza ve araç çubuğundaki bir düğmeye tıklayarak tümünü yenilemenize imkan tanır. Mobil Öykünücüler dahil olmak üzere geliştirme sitenize birden çok tarayıcı bağlayabilirsiniz ve tüm tarayıcıları aynı anda yenilemek için Yenile ' ye tıklayabilirsiniz. Tarayıcı bağlantısı, geliştiricilerin tarayıcı bağlantısı uzantıları yazmasını sağlamak için bir API sunar.

![](release-notes/_static/image3.png)

Geliştiricilerin tarayıcı bağlantısı API 'sinden yararlanmasını etkinleştirerek, Visual Studio ve bağlı olan herhangi bir tarayıcı arasında sınırları kesen çok gelişmiş senaryolar oluşturmak mümkün olur. Web temel bileşenleri, Visual Studio ile tarayıcının geliştirici araçları arasında tümleşik bir deneyim oluşturmak, mobil öykünücüleri ve çok daha fazlasını yapmak için API 'den yararlanır.

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a>Visual Studio Web Düzenleyicisi geliştirmeleri

Visual Studio 2013, Web uygulamalarındaki Razor dosyaları ve HTML dosyaları için yeni bir HTML Düzenleyicisi içerir. Yeni HTML Düzenleyicisi HTML5 tabanlı tek bir birleştirilmiş şema sağlar. Otomatik küme ayracı tamamlama, jQuery UI ve AngularJS özniteliği IntelliSense, öznitelik IntelliSense gruplama, KIMLIK ve sınıf adı IntelliSense ve daha iyi performans, biçimlendirme ve akıllı etiketler dahil diğer iyileştirmeler vardır.

Aşağıdaki ekran görüntüsünde, HTML düzenleyicisinde IntelliSense 'in önyükleme özniteliği kullanılması gösterilmektedir.

![HTML düzenleyicisinde IntelliSense](release-notes/_static/image4.png)

Visual Studio 2013 Ayrıca, içinde yerleşik olarak bulunan CoffeeScript ve LESS düzenleyicilerle birlikte gelir. DAHA az düzenleyici CSS düzenleyiciden tüm seyrek erişimli özelliklerle gelir ve @import zincirindeki tüm daha az belge genelinde değişkenler ve mixıns için özel IntelliSense içerir.

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a>Visual Studio 'da Web Apps Azure App Service desteği

.NET 2,2 için Azure SDK ile Visual Studio 2013 içinde, uzak Web uygulamalarınızla doğrudan etkileşim kurmak için **Sunucu Gezgini** kullanabilirsiniz. Azure hesabınızda oturum açabilir, yeni Web uygulamaları oluşturabilir, uygulamaları yapılandırabilir, gerçek zamanlı günlükleri görüntüleyebilir ve daha fazlasını yapabilirsiniz. SDK 2,2 yayımlandıktan sonra yakında, Azure 'da hata ayıklama modunda uzaktan çalıştırabilirsiniz. Azure App Service Web Apps için yeni özelliklerin çoğu, .NET için Azure SDK 'sının geçerli sürümünü yüklediğinizde Visual Studio 2012 'de de çalışır.

Daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Azure App Service bir ASP.NET Web uygulaması oluşturma](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [Visual Studio 'Yu kullanarak Azure App Service bir Web uygulamasının sorunlarını giderme](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a>Web yayımlama geliştirmeleri

Visual Studio 2013 yeni ve geliştirilmiş Web yayımlama özellikleri içerir. Bunlardan bazıları şunlardır:

- [Web. config dosya şifrelemesini kolayca otomatikleştirin](https://go.microsoft.com/fwlink/?LinkId=325529). (Bu bağlantı ve aşağıdaki iki nokta, MSDN 'deki belgelerde, 10/17 tarihinde gün geç olana kadar kullanılamayabilir.)
- [Dağıtım sırasında bir uygulamayı çevrimdışına almayı kolayca otomatikleştirin](https://go.microsoft.com/fwlink/?LinkId=325530).
- Sunucuya hangi dosyaların kopyalanacağını belirlemek için [son değiştirilme tarihi yerine dosya sağlama toplamı kullanmak](https://go.microsoft.com/fwlink/?LinkId=325531) üzere Web dağıtımı yapılandırın.
- FTP veya dosya sistemi yayımlama yöntemlerini kullanırken ve Web Dağıtımı, tek tek seçili dosyaları (Web. config dahil) hızlıca yayımlayın.

ASP.NET Web dağıtımı hakkında daha fazla bilgi için bkz. [ASP.net sitesi](https://go.microsoft.com/fwlink/?LinkId=322027).

<a id="nuget"></a>
## <a name="nuget-27"></a>NuGet 2.7

NuGet 2,7, [nuget 2,7 sürüm notlarında](http://docs.nuget.org/docs/release-notes/nuget-2.7)ayrıntılı olarak açıklanan zengin bir dizi yeni özellik içerir.

NuGet 'in bu sürümü ayrıca NuGet 'in paket geri yükleme özelliğinin paketleri indirmesi için açık onay sağlama gereksinimini ortadan kaldırır. Onay (ve NuGet 'in Tercihler iletişim kutusunda ilişkili onay kutusu) artık NuGet yüklenerek verildi. Şimdi paket geri yükleme yalnızca varsayılan olarak çalışmaktadır.

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a>ASP.NET Web Forms

### <a name="one-aspnet"></a>Bir ASP.NET

Web Forms proje şablonları, yeni bir ASP.NET deneyimiyle sorunsuz bir şekilde tümleşir. Web Forms projenize MVC ve Web API desteği ekleyebilirsiniz ve tek bir ASP.NET projesi oluşturma Sihirbazı 'nı kullanarak kimlik doğrulamasını yapılandırabilirsiniz. Daha fazla bilgi için, bkz. [Visual Studio 2013 ASP.NET Web projeleri oluşturma](creating-web-projects-in-visual-studio.md).

### <a name="aspnet-identity"></a>ASP.NET Kimlik

Web Forms proje şablonları yeni ASP.NET Identity çerçevesini destekler. Ayrıca, şablonlar artık Web Forms intranet projesinin oluşturulmasını desteklemektedir. Daha fazla bilgi için, **Visual Studio 2013 'de ASP.NET Web projeleri oluşturma**Içindeki [kimlik doğrulama yöntemleri](creating-web-projects-in-visual-studio.md#auth) konusuna bakın.

### <a name="bootstrap"></a>Yükleyebilirsiniz

Web Forms şablonlar, kolayca özelleştirebileceğiniz şık ve hızlı bir görünüm sağlamak için [önyükleme](http://twitter.github.io/bootstrap/) kullanır. Daha fazla bilgi için bkz. [Visual Studio 2013 Web projesi şablonlarındaki önyükleme](creating-web-projects-in-visual-studio.md#bootstrap).

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a>ASP.NET MVC 5

### <a name="one-aspnet"></a>Bir ASP.NET

Web MVC proje şablonları, yeni bir ASP.NET deneyimiyle sorunsuz bir şekilde tümleşir. MVC projenizi özelleştirebilir ve tek bir ASP.NET projesi oluşturma Sihirbazı 'nı kullanarak kimlik doğrulamasını yapılandırabilirsiniz. [ASP.NET MVC 5 Ile çalışmaya başlama konusunda](../../../mvc/overview/getting-started/introduction/getting-started.md)ASP.NET MVC 5 ' e yönelik bir giriş öğreticisi bulabilirsiniz.

MVC 4 projelerini MVC 5 ' e yükseltme hakkında daha fazla bilgi için bkz. [ASP.NET MVC 4 ve Web API projesini ASP.NET MVC 5 ve Web API 2 ' ye yükseltme](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).

### <a name="aspnet-identity"></a>ASP.NET Kimlik

MVC proje şablonları, kimlik doğrulama ve kimlik yönetimi için ASP.NET Identity kullanacak şekilde güncelleştirilmiştir. Facebook ve Google kimlik doğrulaması ile yeni üyelik API 'SI ile ilgili bir öğretici, [Facebook ve Google OAuth2 ve OpenID oturum açma ile ASP.NET MVC 5 uygulaması oluşturma](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) ve [KIMLIK doğrulaması ve SQL DB Ile bir ASP.NET MVC uygulaması oluşturma ve Azure App Service uygulamasına dağıtma](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)konusunda da bulunabilir.

### <a name="bootstrap"></a>Yükleyebilirsiniz

MVC proje şablonu, kolayca özelleştirebileceğiniz şık ve hızlı bir görünüm sağlamak için [önyükleme](http://getbootstrap.com/) kullanmak üzere güncelleştirilmiştir. Daha fazla bilgi için bkz. [Visual Studio 2013 Web projesi şablonlarındaki önyükleme](creating-web-projects-in-visual-studio.md#bootstrap).

### <a name="authentication-filters"></a>Kimlik doğrulama filtreleri

Kimlik doğrulama filtreleri, ASP.NET MVC ardışık düzeninde yetkilendirme filtrelerinden önce çalışan ASP.NET MVC 'de yeni bir filtre türüdür ve tüm denetleyiciler için işlem başına, denetleyici başına veya küresel olarak kimlik doğrulama mantığı belirtmenize izin verir. Kimlik doğrulama filtreleri istekteki kimlik bilgilerini işler ve buna karşılık gelen bir sorumlu sağlar. Kimlik doğrulama filtreleri, yetkisiz isteklere yanıt olarak kimlik doğrulama zorlukları de ekleyebilir.

### <a name="filter-overrides"></a>Geçersiz kılmaları filtrele

Artık bir geçersiz kılma filtresi belirterek, belirli bir eylem yöntemine veya denetleyiciye uygulanan filtreleri geçersiz kılabilirsiniz. Geçersiz kılma filtreleri belirli bir kapsam (eylem veya denetleyici) için çalıştırılmamalıdır bir filtre türleri kümesi belirtir. Bu, genel olarak uygulanan filtreleri yapılandırmanıza ve sonra belirli genel filtrelerin belirli eylemlere veya denetleyicilere uygulanmasını sağlar.

### <a name="attribute-routing"></a>Öznitelik yönlendirme

ASP.NET MVC artık, [http://attributerouting.net](http://attributerouting.net)yazarı olan Tim McCall tarafından bir katkı sayesinde öznitelik yönlendirmeyi desteklemektedir. Öznitelik yönlendirme ile, eylemlerinizi ve denetleyicilerinize açıklama ekleyerek rotalarınızı belirtebilirsiniz.

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a>ASP.NET Web API 2

### <a name="attribute-routing"></a>Öznitelik yönlendirme

ASP.NET Web API 'SI artık, [http://attributerouting.net](http://attributerouting.net)yazarı olan Tim McCall tarafından bir katkı sayesinde öznitelik yönlendirmeyi desteklemektedir. Öznitelik yönlendirme ile, aşağıdaki gibi eylemleriniz ve denetleyicilerinize ek olarak Web API yollarınızı belirtebilirsiniz:

[!code-csharp[Main](release-notes/samples/sample1.cs)]

Öznitelik yönlendirme, Web API 'nizin URI 'Leri üzerinde daha fazla denetim sağlar. Örneğin, tek bir API denetleyicisi kullanarak bir kaynak hiyerarşisini kolayca tanımlayabilirsiniz:

[!code-csharp[Main](release-notes/samples/sample2.cs)]

Öznitelik yönlendirme Ayrıca isteğe bağlı parametreleri, varsayılan değerleri ve yol kısıtlamalarını belirtmek için kullanışlı bir sözdizimi sağlar:

[!code-csharp[Main](release-notes/samples/sample3.cs)]

Öznitelik yönlendirme hakkında daha fazla bilgi için bkz. [Web API 2 ' de öznitelik yönlendirme](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md).

### <a name="oauth-20"></a>OAuth 2.0

Web API 'SI ve tek sayfalı uygulama proje şablonları artık OAuth 2,0 kullanarak yetkilendirmeyi destekliyor. OAuth 2,0, korumalı kaynaklara istemci erişimini yetkilendirmek için bir çerçevedir. Tarayıcılar ve mobil cihazlar dahil olmak üzere çeşitli istemciler için geçerlidir.

OAuth 2,0 desteği, Microsoft OWIN bileşenleri tarafından taşıyıcı kimlik doğrulaması için sunulan ve yetkilendirme sunucusu rolünü uygulayan yeni güvenlik ara yazılımını temel alır. Alternatif olarak, istemciler Windows Server 2012 R2 'de Azure Active Directory veya ADFS gibi bir kurumsal yetkilendirme sunucusu kullanılarak yetkilendirilir.

### <a name="odata-improvements"></a>OData geliştirmeleri

**$Select, $expand, $batch ve $value için destek**

ASP.NET Web API OData artık $select, $expand ve $value için tam desteğe sahiptir. Ayrıca, değişiklik kümelerinin toplu işleme ve işlenmesine yönelik $batch de kullanabilirsiniz.

$Select ve $expand seçenekleri, bir OData uç noktasından döndürülen verilerin şeklini değiştirmenize olanak sağlar. Daha fazla bilgi için bkz. [Web API OData 'de $Select ve $Expand desteği](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).

**Geliştirilmiş genişletilebilirlik**

OData formatlayıcıları artık genişletilebilir. Atom giriş meta verileri ekleyebilir, adlandırılmış akış ve medya bağlantı girdilerini destekler, örnek ek açıklamaları ekleyebilir ve bağlantıların nasıl oluşturulduğunu özelleştirebilirsiniz.

**Tür-daha az destek**

Artık varlık türlerinizin CLR türlerini tanımlamaya gerek kalmadan OData Hizmetleri oluşturabilirsiniz. Bunun yerine, OData denetleyicileriniz, OData biçimlendiricileri serileştirme/seri hale getirme olan **IEdmObject**örneklerini alabilir veya döndürebilir.

**Var olan bir modeli yeniden kullanma**

Zaten var olan bir varlık veri modeli (EDM) varsa, yeni bir tane oluşturmak zorunda kalmak yerine artık doğrudan yeniden kullanabilirsiniz. Örneğin, Entity Framework kullanıyorsanız, sizin için EF derlemesi olan EDM 'ı kullanabilirsiniz.

### <a name="request-batching"></a>İstek toplu Işleme

İstek toplu işlemi, ağ trafiğini azaltmak ve daha yumuşak, daha az bir geveze Kullanıcı arabirimi sağlamak için birden çok işlemi tek bir HTTP POST isteğiyle birleştirir. ASP.NET Web API 'SI artık istek toplu işleme için birkaç strateji destekliyor:

- OData hizmetinin $batch uç noktasını kullanın.
- Birden çok isteği tek bir MIME çok parçalı isteğine paketleyin.
- Özel bir toplu işlem biçimi kullanın.

İstek toplu işlemeyi etkinleştirmek için, Web API yapılandırmanıza bir toplu işlem işleyicisi içeren bir yol eklemeniz yeterlidir:

[!code-csharp[Main](release-notes/samples/sample4.cs)]

Ayrıca, isteklerin sırayla mı yoksa istediğiniz sırada mı yürütüleceğini de denetleyebilirsiniz.

### <a name="portable-aspnet-web-api-client"></a>Taşınabilir ASP.NET Web API Istemcisi

Artık ASP.NET Web API Istemcisini kullanarak Windows Mağazası 'nda çalışan ve 8 uygulama Windows Phone taşınabilir sınıf kitaplıkları oluşturabilirsiniz. Ayrıca, istemci ve sunucu arasında paylaşılabilecek taşınabilir biçimleri de oluşturabilirsiniz.

### <a name="improved-testability"></a>Geliştirilmiş test edilebilir

Web API 2, API denetleyicilerinizi birim testi yapmayı çok daha kolay hale getirir. API denetleyicinizi istek iletinizi ve yapılandırmanızla birlikte oluşturmanız ve ardından test etmek istediğiniz eylem yöntemini çağırmanız yeterlidir. Ayrıca, bağlantı oluşturma işlemini gerçekleştiren eylem yöntemleri için **UrlHelper** sınıfını da kolayca yapılandırabilirsiniz.

### <a name="ihttpactionresult"></a>IHttpActionResult

Artık, Web API 'SI eylem yöntemlerinizin sonucunu kapsüllemek için ıhttpactionresult öğesini uygulayabilirsiniz. Bir Web API 'SI eylem yönteminden döndürülen bir ıhttpactionresult, sonuç yanıt iletisini oluşturmak için ASP.NET Web API çalışma zamanı tarafından yürütülür. Web API uygulamanızın birim testlerini basitleştirmek için herhangi bir Web API eyleminden bir ıhttpactionresult döndürülür. Kolaylık olması için, belirli durum kodlarının, biçimlendirilen içeriğin veya içeriğe dayalı yanıtların döndürülmesinin sonuçları dahil olmak üzere çok sayıda ıhttpactionresult uygulaması sunulmaktadır.

### <a name="httprequestcontext"></a>HttpRequestContext

Yeni **Httprequestcontext** , isteğe bağlı olan ancak istekten hemen kullanılamayan tüm durumları izler. Örneğin, yol verilerini, istek ile ilişkili sorumluyu, istemci sertifikasını, **Urlyardımcısını** ve sanal yol kökünü almak Için **httprequestcontext** ' i kullanabilirsiniz. Birim testi amaçları için kolayca bir **Httprequestcontext** oluşturabilirsiniz.

İsteğin sorumlusu **Iş parçacığı. CurrentPrincipal**'a güvenmek yerine istekle birlikte akışı yaptığından, bu, Web API ardışık düzeninde olduğunda, isteğin kullanım ömrü boyunca artık kullanılabilir.

### <a name="cors"></a>CORS

Brock Allen 'dan başka harika bir katkı sayesinde, ASP.NET artık çapraz kaynak Istek paylaşımını (CORS) tam olarak desteklemektedir.

Tarayıcı güvenliği, bir web sitesinin başka bir etki alanına AJAX istekleri göndermesini engeller. [CORS](http://www.w3.org/TR/cors/) , bir sunucunun aynı kaynaklı ilkeyi rahat bir şekilde sağlamasına izin veren bir W3C standardıdır. CORS kullanarak, bir sunucu bazı çapraz kaynak isteklerine, diğerlerini reddetirken açık bir şekilde izin verebilir.

Web API 2 artık, ön kontrol isteklerini otomatik olarak işleme dahil olmak üzere CORS 'yi desteklemektedir. Daha fazla bilgi için bkz. [ASP.NET Web API 'Sinde çapraz kaynak Isteklerini etkinleştirme](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).

### <a name="authentication-filters"></a>Kimlik doğrulama filtreleri

Kimlik doğrulama filtreleri, ASP.NET Web API 'sinde, ASP.NET Web API ardışık düzeninde yetkilendirme filtrelerinden önce çalışan yeni bir filtre türüdür ve tüm denetleyiciler için işlem başına, denetleyiciye göre veya küresel olarak kimlik doğrulama mantığı belirtmenize izin verir. Kimlik doğrulama filtreleri istekteki kimlik bilgilerini işler ve buna karşılık gelen bir sorumlu sağlar. Kimlik doğrulama filtreleri, yetkisiz isteklere yanıt olarak kimlik doğrulama zorlukları de ekleyebilir.

### <a name="filter-overrides"></a>Geçersiz kılmaları filtrele

Artık bir geçersiz kılma filtresi belirterek belirli bir eylem yöntemine veya denetleyiciye uygulanan filtreleri geçersiz kılabilirsiniz. Geçersiz kılma filtreleri belirli bir kapsam (eylem veya denetleyici) için çalıştırılmamalıdır bir filtre türleri kümesi belirtir. Bu, genel filtreler eklemenize olanak tanır, ancak bazılarını belirli eylemlerden veya denetleyicilerden hariç tutabilir.

### <a name="owin-integration"></a>OWıN tümleştirmesi

ASP.NET Web API 'SI artık OWIN 'u tam olarak destekliyor ve herhangi bir OWıN özellikli konağında çalıştırılabilir. Ayrıca, OWıN kimlik doğrulama sistemiyle tümleştirme sağlayan bir **Hostauthenticationfilter** da dahil edilmiştir.

OWıN tümleştirmesiyle, SignalR gibi diğer OWıN ara yazılımı ile kendi işleminizde kendi sürecinizdeki Web API 'sini kendi işleminizde barındırabilirsiniz. Daha fazla bilgi için bkz. [OWIN 'U Self-Host ASP.NET Web API 'si Için kullanma](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a>ASP.NET SignalR 2,0

Aşağıdaki bölümlerde, SignalR 2,0 özellikleri açıklanır.

- [OWıN üzerine kurulmuştur](#builtonowin)
- [MapHubs ve MapConnection artık MapSignalR](#MapSignalR)
- [Etki alanları arası destek](#crossdomain)
- [MonoTouch ve Monodroıd aracılığıyla iOS ve Android desteği](#mobile)
- [Taşınabilir .NET Istemcisi](#portable)
- [Yeni Self-Host paketi](#selfhost)
- [Geriye dönük uyumlu sunucu desteği](#backwardcompat)
- [.NET 4,0 için sunucu desteği kaldırıldı](#remove40)
- [İstemci ve grup listesine bir ileti gönderme](#messagelist)
- [Belirli bir kullanıcıya ileti gönderme](#sendtouser)
- [Daha iyi hata işleme desteği](#errorhandling)
- [Hub 'ların daha kolay birim testi](#unittesting)
- [JavaScript hata işleme](#javascripterror)

Mevcut bir 1. x projesini SignalR 2,0 ' e nasıl yükselteceğiniz hakkında bir örnek için bkz. [bir SignalR 1. x projesini yükseltme](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).

<a id="builtonowin"></a>
### <a name="built-on-owin"></a>OWıN üzerine kurulmuştur

SignalR 2,0 tamamen [Owin üzerinde oluşturulmuştur (.net Için açık Web arabirimi)](http://owin.org/). Bu değişiklik, SignalR için kurulum işleminin Web 'de barındırılan ve şirket içinde barındırılan SignalR uygulamaları arasında çok daha tutarlı olmasını sağlar, ancak aynı zamanda birkaç API değişikliği de gerektirir.

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a>MapHubs ve MapConnection artık MapSignalR

OWıN standartlarıyla uyumluluk için bu yöntemler `MapSignalR`olarak yeniden adlandırılmıştır. parametre olmadan çağrılan `MapSignalR` tüm Hub 'ları eşler (1. x sürümünde `MapHubs` olduğu gibi); tek tek **Persistentconnection** nesnelerini eşlemek için, bağlantı türünü tür parametresi olarak ve bağlantının URL uzantısını ilk bağımsız değişken olarak belirtin.

`MapSignalR` yöntemi bir Owın başlangıç sınıfında çağrılır. Visual Studio 2013 Owın başlangıç sınıfı için yeni bir şablon içerir; Bu şablonu kullanmak için şunları yapın:

1. Projeye sağ tıklayın
2. **Ekle**, **Yeni öğe...** seçeneğini belirleyin
3. **Owın başlangıç sınıfı**' nı seçin. Yeni sınıfı **Startup.cs**olarak adlandırın.

Bir **Web uygulamasında,** `MapSignalR` yöntemini Içeren owın başlangıç sınıfı, aşağıda gösterildiği gibi, Web. config dosyasının uygulama ayarları düğümündeki bir giriş kullanılarak owın başlangıç işlemine eklenecektir.

**Kendi kendine barındırılan bir uygulamada**, başlangıç sınıfı `WebApp.Start` yönteminin tür parametresi olarak geçirilir.

**SignalR 1. x içindeki hub 'ları ve bağlantıları eşleme (bir Web uygulamasındaki genel uygulama dosyasından):** 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

**SignalR 2,0 ' de hub ve bağlantıları eşleme (bir Owın başlangıç sınıfı dosyasından):** 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

**Kendi kendine barındırılan bir uygulamada**, başlangıç sınıfı aşağıda gösterildiği gibi `WebApp.Start` yöntemi için tür parametresi olarak geçirilir.

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a>Etki alanları arası destek

SignalR 1. x içinde, çapraz etki alanı istekleri tek bir EnableCrossDomain bayrağıyla denetlenir. Bu bayrak hem JSONP hem de CORS isteklerini denetlediniz. Daha fazla esneklik için, tüm CORS desteği, SignalR 'nin sunucu bileşeninden kaldırılmıştır (JavaScript istemcileri tarayıcının desteklediği algılanırsa CORS 'yi yine de kullanır) ve bu senaryoları desteklemek için yeni OWıN ara yazılımı kullanılabilir hale getirilir.

SignalR 2,0 ' de, istemcide JSONP gerekliyse (eski tarayıcılarda etki alanları arası istekleri desteklemek için), aşağıda gösterildiği gibi, `HubConfiguration` `true`nesnesindeki `EnableJSONP` ayarlanarak açıkça etkinleştirilmesi gerekecektir. JSONP, CORS 'den daha az güvenli olduğu için varsayılan olarak devre dışıdır.

SignalR 2,0 ' ye yeni CORS ara yazılımı eklemek için, `Microsoft.Owin.Cors` kitaplığı projenize ekleyin ve aşağıdaki bölümde gösterildiği gibi SignalR ara ortamınızı önce `UseCors` çağırın.

**Projenize Microsoft. Owin. CORS ekleme**: bu kitaplığı yüklemek Için, Paket Yöneticisi konsolunda aşağıdaki komutu çalıştırın:

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

Bu komut, paketin 2.0.0 sürümünü projenize ekler.

**UseCors çağrılıyor**

Aşağıdaki kod parçacıkları, SignalR 1. x ve 2,0 ' de etki alanları arası bağlantıların nasıl uygulanacağını gösterir.

**SignalR 1. x içinde etki alanları arası istekleri uygulama (genel uygulama dosyasından)**

[!code-csharp[Main](release-notes/samples/sample9.cs)]

**SignalR 2,0 ' de etki alanları arası istekleri uygulama (bir C# kod dosyasından)**

Aşağıdaki kod, bir SignalR 2,0 projesinde CORS veya JSONP 'nin nasıl etkinleştirileceğini göstermektedir. Bu kod örneği, `MapSignalR`yerine `Map` ve `RunSignalR` kullanır, böylece CORS ara yazılımı yalnızca CORS desteği gerektiren SignalR istekleri için çalışır (`MapSignalR`' de belirtilen yoldaki tüm trafik yerine). `Map`, tüm uygulama için değil belirli bir URL öneki için çalıştırılması gereken diğer tüm ara yazılımlar için de kullanılabilir.

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a>MonoTouch ve Monodroıd aracılığıyla iOS ve Android desteği

[Xamarin kitaplığından](https://xamarin.com/)MonoTouch ve Monodroıd bileşenleri kullanılarak IOS ve Android istemcileri için destek eklenmiştir. Bunların nasıl kullanılacağı hakkında daha fazla bilgi için bkz. [Xamarin bileşenlerini kullanma](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln). Bu bileşenler, SignalR RTW sürümü kullanılabilir olduğunda [Xamarin Store](https://store.xamarin.com/) 'da kullanılabilir olacaktır.

<a id="portable"></a># # # Taşınabilir .NET istemcisi

Platformlar arası geliştirmeyi daha iyi kolaylaştırmak için Silverlight, WinRT ve Windows Phone istemcileri aşağıdaki platformları destekleyen tek bir taşınabilir .NET istemcisiyle değiştirilmiştir:

- NET 4,5
- Silverlight 5
- WinRT (Windows Mağazası uygulamaları için .NET)
- Windows Phone 8

<a id="selfhost"></a>

### <a name="new-self-host-package"></a>Yeni Self-Host paketi

Artık, bir Web sunucusunda barındırılması yerine, bir işlemde veya başka bir uygulamada barındırılan SignalR Self-Host (SignalR uygulamaları) kullanmaya başlamanızı kolaylaştıracak bir NuGet paketi vardır. SignalR 1. x ile oluşturulmuş bir Self-Host projesini yükseltmek için Microsoft. AspNet. SignalR. Owin paketini kaldırın ve Microsoft. AspNet. SignalR. SelfHost paketini ekleyin. Self-Host paketiyle çalışmaya başlama hakkında daha fazla bilgi için bkz. [öğretici: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a>Geriye dönük uyumlu sunucu desteği

SignalR 'nin önceki sürümlerinde, istemcide kullanılan SignalR paketinin sürümleri ve sunucusunun aynı olması gerekir. Güncelleştirme zor olan kalın istemci uygulamalarını desteklemek için, SignalR 2,0 artık daha eski bir istemciyle daha yeni bir sunucu sürümünü kullanmayı desteklemektedir. **Not: SignalR 2,0, daha yeni istemcilerle daha eski sürümlerle oluşturulmuş sunucuları desteklemez.**

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a>.NET 4,0 için sunucu desteği kaldırıldı

SignalR 2,0, .NET 4,0 ile sunucu birlikte çalışabilirliği için desteği bıraktı. .NET 4,5, SignalR 2,0 sunucularıyla kullanılmalıdır. SignalR 2,0 için hala bir .NET 4,0 istemcisi vardır.

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a>İstemci ve grup listesine bir ileti gönderme

SignalR 2,0 ' de, istemci ve grup kimliklerinin bir listesini kullanarak bir ileti göndermek mümkündür. Aşağıdaki kod parçacıkları bunun nasıl yapılacağını göstermektedir.

**PersistentConnection kullanarak istemciler ve gruplar listesine ileti gönderme**

[!code-csharp[Main](release-notes/samples/sample11.cs)]

**Hub 'Ları kullanarak istemciler ve gruplar listesine ileti gönderme**

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a>Belirli bir kullanıcıya ileti gönderme

Bu özellik, kullanıcıların yeni bir ıuserıdprovider arabirimi aracılığıyla bir ırequest 'e göre kimliğini belirlemesine izin verir:

**Iuserıdprovider arabirimi**

[!code-csharp[Main](release-notes/samples/sample13.cs)]

Varsayılan olarak, Kullanıcı adı olarak kullanıcının IPrincipal.Identity.Name kullanan bir uygulama olacaktır.

Hub 'larda, yeni bir API aracılığıyla bu kullanıcılara ileti gönderebileceksiniz:

**Istemcileri kullanma. Kullanıcı API 'SI**

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a>Daha iyi hata Işleme desteği

Kullanıcılar artık herhangi bir hub çağrısından **Hubexception** oluşturabilir. **Hubexception** Oluşturucusu bir dize iletisi ve bir nesne ek hata verileri alabilir. SignalR, özel durumu otomatik olarak serileştirmesini ve hub yöntemi çağrısını reddetmek/başarısız kılmak için kullanılacağı istemciye gönderir.

**Ayrıntılı hub özel durumlarını göster** ayarı, istemciye geri gönderilen **hubexception** 'a hiçbir pul içermez; her zaman gönderilir.

**İstemciye HubException göndermeyi gösteren sunucu tarafı kod**

[!code-csharp[Main](release-notes/samples/sample15.cs)]

**Sunucudan gönderilen bir HubException 'a yanıt vermeyi gösteren JavaScript istemci kodu**

[!code-html[Main](release-notes/samples/sample16.html)]

**Sunucudan gönderilen bir HubException 'a yanıt vermeyi gösteren .NET istemci kodu**

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a>Hub 'ların daha kolay birim testi

SignalR 2,0, hub 'Larda, sahte istemci tarafı etkinleştirmeleri oluşturmayı kolaylaştıran `IHubCallerConnectionContext` adlı bir arabirim içerir. Aşağıdaki kod parçacıkları, bu arabirimi popüler test gücünden [xUnit.net](https://github.com/xunit/xunit) ve [moq](https://code.google.com/p/moq/)ile kullanmayı gösterir.

**XUnit.net ile birim testi SignalR**

[!code-csharp[Main](release-notes/samples/sample18.cs)]

**Moq ile birim testi SignalR**

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a>JavaScript hata işleme

SignalR 2,0 ' de tüm JavaScript hata işleme geri çağırmaları, ham dizeler yerine JavaScript hata nesnelerini döndürür. Bu, SignalR 'nin hata İşleyicileriniz için daha zengin bilgiler akışına olanak sağlar. Hatanın `source` özelliğinden iç özel durumu alabilirsiniz.

**Start. Fail özel durumunu işleyen JavaScript istemci kodu**

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a>ASP.NET Kimlik

### <a name="new-aspnet-membership-system"></a>Yeni ASP.NET üyelik sistemi

ASP.NET Identity, ASP.NET uygulamaları için yeni üyelik sistemidir. ASP.NET Identity, kullanıcıya özel profil verilerini uygulama verileriyle tümleştirmeyi kolaylaştırır. ASP.NET Identity Ayrıca uygulamanızdaki Kullanıcı profillerinin Kalıcılık modelini seçmenizi sağlar. Verileri bir SQL Server veritabanında veya Azure depolama tabloları gibi NoSQL veri depoları dahil olmak üzere başka bir veri deposunda saklayabilirsiniz. Daha fazla bilgi için **Visual Studio 2013 'de ASP.NET Web projeleri oluşturma**Içindeki [bireysel kullanıcı hesapları](creating-web-projects-in-visual-studio.md#indauth) bölümüne bakın.

### <a name="claims-based-authentication"></a>Beyana dayalı kimlik doğrulama

ASP.NET artık, kullanıcının kimliğinin güvenilen bir veren tarafından bir talep kümesi olarak temsil edildiği talep tabanlı kimlik doğrulamasını desteklemektedir. Kullanıcılara bir uygulama veritabanında tutulan bir Kullanıcı adı ve parola kullanılarak veya sosyal kimlik sağlayıcıları (örneğin, Microsoft hesapları, Facebook, Google, Twitter) kullanılarak veya Azure Active Directory aracılığıyla Kuruluş hesaplarını kullanarak kimlik doğrulaması yapılabilir. Active Directory Federasyon Hizmetleri (AD FS) (ADFS).

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a>Azure Active Directory ve Windows Server Active Directory Tümleştirmesi

Artık, kimlik doğrulaması için Azure Active Directory veya Windows Server Active Directory (AD) kullanan ASP.NET projeler oluşturabilirsiniz. Daha fazla bilgi için **Visual Studio 2013 'de ASP.NET Web projeleri oluşturma**bölümündeki [Kurumsal hesaplar](creating-web-projects-in-visual-studio.md#orgauth) bölümüne bakın.

### <a name="owin-integration"></a>OWıN tümleştirmesi

ASP.NET kimlik doğrulaması artık, herhangi bir OWIN tabanlı konakta kullanılabilen OWıN ara yazılımını temel alır. OWıN hakkında daha fazla bilgi için, aşağıdaki [MICROSOFT Owin Components](#TOC7) bölümüne bakın.

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a>Microsoft OWIN Bileşenleri

[.Net Için açık Web arabirimi](http://owin.org/) (owın), .NET Web sunucuları ile Web uygulamaları arasında bir soyutlama tanımlar. OWIN, Web uygulamasını sunucudan ayırır ve Web uygulamaları ana bilgisayar belirsiz hale getirir. Örneğin, bir OWIN tabanlı Web uygulamasını IIS 'de veya özel bir işlemde kendi kendine barındıracak şekilde barındırabilirsiniz.

Microsoft OWIN bileşenlerinde tanıtılan değişiklikler (Katana proje olarak da bilinir) yeni sunucu ve konak bileşenleri, yeni yardımcı kitaplıklar ve ara yazılım ve yeni kimlik doğrulama ara yazılımı içerir.

OWıN ve Katana hakkında daha fazla bilgi için bkz. [owın ve Katana 'daki](../../../aspnet/overview/owin-and-katana/index.md)yenilikler.

**Note: [Owın](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) uygulamaları IIS klasik modunda çalıştırılamaz; Bunların tümleşik modda çalıştırılması gerekir.**

**Note: [Owın](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) uygulamalarının tam güvende çalıştırılması gerekir.**

### <a name="new-servers-and-hosts"></a>Yeni sunucular ve konaklar

Bu sürümle birlikte, Self-Host senaryolarını etkinleştirmek için yeni bileşenler eklenmiştir. Bu bileşenler aşağıdaki NuGet paketlerini içerir:

- **Microsoft. Owin. Host. HttpListener**. HTTP isteklerini dinlemek ve bunları OWıN ardışık düzenine yönlendirmek için **HttpListener** kullanan bir owın sunucusu sağlar.
- **Microsoft. Owin. Hosting** , bir konsol uygulaması veya Windows hizmeti gibi özel bir işlemde bir owın ardışık düzenini kendi kendine barındırmak isteyen geliştiriciler için bir kitaplık sağlar.
- **Owinhost**. , `Microsoft.Owin.Hosting` kaydırılan ve özel bir ana bilgisayar uygulaması yazmak zorunda kalmadan bir OWıN işlem hattını barındırmanıza olanak sağlayan tek başına bir yürütülebilir dosya sağlar.

Ayrıca, `Microsoft.Owin.Host.SystemWeb` paketi artık, ara yazılımın belirli bir ASP.NET işlem hattı aşamasında çağrılması gerektiğini belirten **Systemweb** sunucusuna ipuçları sağlamasına olanak tanıyor. Bu özellik, ASP.NET işlem hattının başlarında çalışması gereken kimlik doğrulama ara yazılımı için özellikle yararlıdır.

### <a name="helper-libraries-and-middleware"></a>Yardımcı kitaplıkları ve ara yazılım

Owin belirtiminden yalnızca Function ve Type tanımlarını kullanarak OWIN bileşenleri yazabilirsiniz, ancak yeni `Microsoft.Owin` paketi daha kolay bir soyut dizi kümesi sağlar. Bu paket, daha önceki birkaç paketi (ör. `Owin.Extensions`, `Owin.Types`), diğer OWIN bileşenleri tarafından kolayca kullanılabilecek tek ve iyi yapılandırılmış bir nesne modelinde birleştirir. Aslında, Microsoft OWIN bileşenlerinin çoğu artık bu paketi kullanır.

> [!NOTE]
> [Owın](http://www.owin.org) uygulamaları IIS klasik modunda çalıştırılamaz; Bunların tümleşik modda çalıştırılması gerekir.

> [!NOTE]
> [Owın](http://www.owin.org) uygulamalarının tam güvende çalıştırılması gerekir.

Bu sürüm ayrıca, çalışan bir OWIN uygulamasının doğrulanması için ara yazılım, Ayrıca hataları araştırmak için hata sayfası ara yazılımı içeren Microsoft. Owin. Diagnostics paketini de içerir.

### <a name="authentication-components"></a>Kimlik doğrulama bileşenleri

Aşağıdaki kimlik doğrulama bileşenleri kullanılabilir.

- **Microsoft. Owin. Security. ActiveDirectory**. Şirket içi veya bulut tabanlı dizin hizmetlerini kullanarak kimlik doğrulamasını mümkün bir şekilde sunar.
- **Microsoft. Owin. Security. Cookies** , tanımlama bilgilerini kullanarak kimlik doğrulamaya izin vermez. Bu paket daha önce `Microsoft.Owin.Security.Forms`olarak adlandırılmıştı.
- **Microsoft. Owin. Security. Facebook** , Facebook 'un OAuth tabanlı hizmeti kullanılarak kimlik doğrulamaya izin vermez.
- **Microsoft. Owin. Security. Google** , Google 'ın OpenID tabanlı hizmetini kullanarak kimlik doğrulamaya izin vermez.
- **Microsoft. Owin. Security. JWT** , JWT belirteçlerini kullanarak kimlik doğrulamaya izin verir.
- **Microsoft. Owin. Security. MicrosoftAccount** , Microsoft hesaplarını kullanarak kimlik doğrulamaya izin vermez.
- **Microsoft. Owin. Security. OAuth**. , Bir OAuth yetkilendirme sunucusu ve ayrıca taşıyıcı belirteçleri kimlik doğrulaması için ara yazılım sağlar.
- **Microsoft. Owin. Security. Twitter** , Twitter 'nın OAuth tabanlı hizmeti kullanılarak kimlik doğrulamaya izin vermez.

Bu sürüm ayrıca, çıkış noktaları arası HTTP isteklerini işlemeye yönelik ara yazılım içeren `Microsoft.Owin.Cors` paketini içerir.

> [!NOTE]
> Visual Studio 2013 son sürümünde JWT imzalama desteği kaldırılmıştır.

<a id="ef6"></a>
## <a name="entity-framework-6"></a>Entity Framework 6

Entity Framework 6 ' daki yeni özelliklerin ve diğer değişikliklerin listesi için, bkz. [Entity Framework sürüm geçmişi](https://msdn.com/data/jj574253).

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a>ASP.NET Razor 3

ASP.NET Razor 3, aşağıdaki yeni özellikleri içerir:

- Sekme düzenlemesi desteği. Daha önce, Visual Studio 'daki **Biçim belgesi** komutu, otomatik girintileme ve otomatik biçimlendirme **sekmeleri koru** seçeneği kullanılırken düzgün çalışmadı. Bu değişiklik, sekme biçimlendirmesi için Razor kodu için Visual Studio biçimlendirmesini düzeltir.
- Bağlantılar oluşturulurken URL yeniden yazma kuralları için destek.
- Güvenlik saydam özniteliğinin kaldırılması.
  > [!NOTE]
  > Bu bir önemli değişiklik değildir ve Razor 3 ' ü MVC4 ve önceki sürümleriyle uyumsuz hale getirir. Razor 2, MVC5 veya MVC5 'e göre derlenen Derlemelerle uyumsuzdur.

Yayın öncesi sürümlerden Visual Studio 2013 düzeltilen Razor 3 sorunları [burada](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)bulabilirsiniz.

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a>ASP.NET uygulama askıya alma

ASP.NET uygulama askıya alma, tek bir makinede çok sayıda ASP.NET sitesini barındırmak için Kullanıcı deneyimini ve ekonomik modeli bir arada değiştiren .NET Framework 4.5.1 'de oyun özellikli bir özelliktir. Daha fazla bilgi için bkz. [ASP.net App Suspend – yanıt veren paylaşılan .NET Web barındırma](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a>Bilinen sorunlar ve son değişiklikler

Bu bölümde, Visual Studio 2013 için ASP.NET and Web Tools bilinen sorunlar ve son değişiklikler açıklanmaktadır.

### <a name="nuget"></a>NuGet

- [Yeni paket geri yüklemesi, sln dosyası kullanılırken mono üzerinde çalışmaz](https://nuget.codeplex.com/workitem/3596) ; gelecek bir NuGet. exe Download ve [NuGet. CommandLine paket](http://www.nuget.org/packages/NuGet.CommandLine/) güncelleştirmesinde düzeltilecektir.
- [Yeni paket geri yüklemesi Wix projeleriyle birlikte çalışmıyor](https://nuget.codeplex.com/workitem/3598) . yakında düzenlenecek bir NuGet. exe Download ve [NuGet. CommandLine paket](http://www.nuget.org/packages/NuGet.CommandLine/) güncelleştirmesinde düzeltilecektir.
- [Otomatik paket geri yükleme, bir çözüm klasörü altındaki projeler için çalışmaz](https://nuget.codeplex.com/workitem/3625) ; NuGet 2,8 ' de düzeltilir.

### <a name="aspnet-web-api"></a>ASP.NET Web API

1. `ODataQueryOptions<T>.ApplyTo(IQueryable)`, `$select` ve `$expand`için destek eklediğimiz için her zaman `IQueryable<T>` döndürmez.

    `ODataQueryOptions<T>` için önceki örneklerimiz, `ApplyTo` döndürülen değeri her zaman `IQueryable<T>`olarak. Daha önce (`$filter`, `$orderby`, `$skip`, `$top`) daha önce desteklendiğimiz sorgu seçenekleri sorgunun şeklini değiştirmediği için bu daha önce çalıştı. `$select` desteklediğimiz ve dönüş değeri `ApplyTo` `$expand`, her zaman `IQueryable<T>` olmayacaktır.

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    Daha önce örnek kodu kullanıyorsanız, istemci `$select` ve `$expand`göndermezse çalışmaya devam eder. Ancak, `$select` ve `$expand` desteklemek istiyorsanız bu kodu bu kod ile değiştirmeniz gerekir.

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. **Batch isteği sırasında istek. URL veya RequestContext. URL null**

    Bir toplu işlem senaryosunda, **Request. URL** veya **RequestContext. URL**'den erişildiğinde **UrlHelper** null olur.

    Bu sorun şu anda burada izleniyor: [Batchrequestcontext. URL, toplu işleme isteği için null](http://aspnetwebstack.codeplex.com/workitem/1301).

    Bu sorun için geçici çözüm olarak, aşağıdaki örnekte olduğu gibi, **UrlHelper**'ın yeni bir örneğini oluşturmaktır:

    **UrlHelper 'ın yeni bir örneğini oluşturma**

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a>ASP.NET MVC

1. MVC5 ve OrgAuth kullanılırken, bir görünüme sahip olan görünümleriniz varsa, görünüme veri gönderdiğinizde aşağıdaki hatayla karşılaşabilirsiniz:

    **Hata**:

    *'/' Uygulamasında sunucu hatası.*

    <em>'<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>' veya '<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' türünde bir talep, belirtilen ClaimsIdentity üzerinde yoktu. Talep tabanlı kimlik doğrulamasıyla karşı koruma belirteci desteğini etkinleştirmek için lütfen yapılandırılan talep sağlayıcısının, oluşturduğu ClaimsIdentity örneklerinde bu taleplerin her ikisini de sağladığını doğrulayın. Bunun yerine, yapılandırılmış talep sağlayıcı benzersiz bir tanımlayıcı olarak farklı bir talep türü kullanıyorsa,, Antiforgeryıconfig. UniqueClaimTypeIdentifier statik özelliği ayarlanarak yapılandırılabilir.</em>

    **Geçici çözüm**:

    Bunu onarmak için Global. asax dosyasında aşağıdaki satırı ekleyin:

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    Bu, bir sonraki sürüm için düzeltilecektir.
2. MVC4 uygulamasını MVC5 'e yükselttikten sonra çözümü derleyin ve başlatın. Aşağıdaki hatayı görmeniz gerekir:

    A System. Web. Web sayfası. Razor. Configuration. HostSection, [B] System. Web. Web sayfası. Razor. Configuration. HostSection öğesine atanamaz. ' C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35 \ System. Web. Web sayfası. Razor. dll ' konumundaki ' default ' bağlamındaki ' System. Web. Web sayfası. Razor, sürüm = 2.0.0.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35 ' öğesinden bir kaynak yazın. Tür B, ' System. Web. Web sayfaları. Razor, sürüm = 3.0.0.0 'dan kaynaklı kültür = neutral, PublicKeyToken = 31bf3856ad364e35 ' ' C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01 \ System. Web. Web sayfası. Razor. dll ' konumunda ' default ' bağlamında.

    Yukarıdaki hatayı onarmak için, projenizdeki *Tüm* Web. config dosyalarını (görünümler klasöründe olanlar dahil) açın ve aşağıdakileri yapın:

   1. "System. Web. Mvc" öğesinin "4.0.0.0" sürümünün tüm oluşumlarını "5.0.0.0" olarak güncelleştirin.
   2. "System. Web. yardımcılar", &quot;System. Web. Web sayfaları&quot; ve &quot;System. Web. Web sayfası. Razor&quot; "3.0.0.0" için "2.0.0.0" sürümünün tüm oluşumlarını Güncelleştir

      Örneğin, yukarıdaki değişiklikleri yaptıktan sonra, derleme bağlamaları şöyle görünmelidir:

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      MVC 4 projelerini MVC 5 ' e yükseltme hakkında daha fazla bilgi için bkz. [ASP.NET MVC 4 ve Web API projesini ASP.NET MVC 5 ve Web API 2 ' ye yükseltme](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).
3. JQuery unobtrusive doğrulaması ile istemci tarafı doğrulaması kullanılırken, tür = ' number ' olan HTML girişi öğesi için bazen doğrulama iletisi yanlış olur. Geçerli bir sayının gerekli olduğu doğru ileti yerine geçersiz bir sayı girildiğinde, gerekli bir değer ("yaş alanı gereklidir") için doğrulama hatası gösterilir.

    Bu sorun genellikle oluşturma ve düzenleme görünümlerinde tamsayı özelliği olan bir model için yapı iskelesi kodu ile birlikte bulunur.

    Bu sorunu geçici olarak çözmek için, düzenleyici yardımcısını şu şekilde değiştirin:

    `@Html.EditorFor(person => person.Age)`

    Hedef:

    `@Html.TextBoxFor(person => person.Age)`
4. ASP.NET MVC 5 artık kısmi güveni desteklemiyor. MVC veya WebAPI ikililerini bağlayan projeler [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) özniteliğini ve [Allowpartiallytrustedçağıranlar](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) özniteliğini kaldırmalıdır. Bu özniteliklerin kaldırılması, aşağıdaki gibi derleyici hatalarını ortadan kaldıracak.

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > Bunun yan etkisi olarak, aynı uygulamadaki 4,0 ve 5,0 derlemelerini kullanamazsınız. Bunların tümünü 5,0 olarak güncelleştirmeniz gerekir.

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a>Web sitesi intranet bölgesinde barındırılırken, Facebook yetkilendirmesi olan SPA şablonu, IE 'de kararsızlığa neden olabilir

SPA şablonu, Facebook ile dış oturum açma sağlar. Şablonla oluşturulan proje yerel olarak çalıştığında, oturum açma IE 'nin kilitlenmesine neden olabilir.

Çözüm:

1. Web sitesini Internet bölgesinde barındırın; veya

2. Senaryoyu IE dışındaki bir tarayıcıda test edin.

### <a name="web-forms-scaffolding"></a>Web Forms yapı Iskelesi

Web Forms Scafkatlama, VS2013 'den kaldırılmıştır ve sonraki bir Visual Studio güncelleştirmesinde kullanıma sunulacaktır. Ancak, MVC bağımlılıklarını ekleyerek ve MVC için yapı iskelesi oluşturarak Web Forms bir proje içinde yapı iskelesi kullanmaya devam edebilirsiniz. Projeniz, Web Forms ve MVC 'nin bir birleşimini içerir.

Web Forms projenize MVC eklemek için yeni bir yapı iskelesi ekleyin ve **MVC 5 bağımlılıklarını**seçin. Betikler gibi tüm içerik dosyalarına gereksiniminiz olmasına bağlı olarak en az veya tam ' ı seçin. Daha sonra, MVC için, projenizde görünümler ve bir denetleyici oluşturacak bir yapı iskelesi öğesi ekleyin.

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC ve Web API 'SI yapı Iskelesi-HTTP 404, bulunamadı hatası

Bir projeye bir yapı iskelesi öğesi eklenirken bir hatayla karşılaşılırsa, projeniz tutarsız bir durumda kalacak. Yapı iskelesi haline getirilen değişikliklerden bazıları geri alınacaktır, ancak yüklü NuGet paketleri gibi diğer değişiklikler geri alınmaz. Yönlendirme yapılandırması değişiklikleri geri alınırsa, kullanıcılar, yapı iskelesi öğelerinde gezinilirken bir HTTP 404 hatası alırlar.

Geçici çözüm:

- MVC için bu hatayı onarmak üzere yeni bir yapı iskelesi ekleyin ve MVC 5 bağımlılıklarını (en az ya da tam) seçin. Bu işlem, gerekli tüm değişiklikleri projenize ekleyecek.
- Web API 'SI için bu hatayı onarmak için:

  1. WebApiConfig sınıfını projenize ekleyin.

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. WebApiConfig. Register öğesini Global. asax içindeki Application\_start yönteminde aşağıdaki gibi yapılandırın:

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
