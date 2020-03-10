---
uid: visual-studio/overview/2013/creating-web-projects-in-visual-studio
title: Visual Studio 2013 'de ASP.NET Web projeleri oluşturuluyor | Microsoft Docs
author: tdykstra
description: Bu konuda, ASP.NET Web projeleri oluşturma seçenekleri açıklanmaktadır. güncelleştirme 3 ile Visual Studio 2013 web geliştirme c için yeni özelliklerden bazıları aşağıda verilmiştir...
ms.author: riande
ms.date: 12/01/2014
ms.assetid: 61941e64-0c0d-4996-9270-cb8ccfd0cabc
msc.legacyurl: /visual-studio/overview/2013/creating-web-projects-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: fbb4cd7afa2506879d47bce980bf0164aad40c2c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555225"
---
# <a name="creating-aspnet-web-projects-in-visual-studio-2013"></a>Visual Studio 2013’te ASP.NET Web Projeleri Oluşturma

[Tom Dykstra](https://github.com/tdykstra) tarafından

> Bu konu, güncelleştirme 3 ile Visual Studio 2013 'de ASP.NET Web projeleri oluşturma seçeneklerini açıklamaktadır.
> 
> Visual Studio 'nun önceki sürümleriyle karşılaştırıldığında Web geliştirme için yeni özelliklerden bazıları şunlardır:
> 
> - [Çoklu ASP.net çerçeveleri](#add) (Web Forms, MVC ve Web API) için destek sunan projeler oluşturmaya yönelik basit bir kullanıcı arabirimi.
> - [ASP.NET Identity](#indauth), tüm ASP.net çerçeveleri ile aynı ve IIS dışında Web barındırma yazılımıyla birlikte çalışarak yeni bir ASP.NET üyelik sistemidir.
> - Yanıt veren tasarım ve tema özellikleri sağlamak için [önyükleme](#bootstrap) kullanımı.
> - Yalnızca MVC için sunulan, [otomatik test projesi oluşturma](#testproj) ve bir [Intranet site şablonu](#winauth)gibi Web Forms yeni özellikler.
> 
> Azure Cloud Services veya Azure Mobile Services için Web projeleri oluşturma hakkında daha fazla bilgi için bkz. [azure Cloud Services Ile çalışmaya başlama ve ASP.net](https://azure.microsoft.com/documentation/articles/cloud-services-dotnet-get-started/) ve [Azure Mobile Services .net arka ucu Ile bir Leaderboard uygulaması oluşturma](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/).

<a id="prerequisites"></a>
## <a name="prerequisites"></a>Önkoşullar

Bu makale, [güncelleştirme 3](https://go.microsoft.com/fwlink/?linkid=397827&amp;clcid=0x409) ' ün yüklü olduğu [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) için geçerlidir.

<a id="wap"></a>
## <a name="web-application-projects-versus-web-site-projects"></a>Web uygulaması projeleri Web sitesi projelerine karşı

ASP.NET iki tür Web projesi arasında seçim sağlar: *Web uygulaması projeleri* ve *Web sitesi projeleri*. Web uygulaması projelerini yeni geliştirme için öneriyoruz ve bu makale yalnızca Web uygulaması projeleri için geçerlidir. Daha fazla bilgi için MSDN sitesinde [Visual Studio 'daki Web sitesi projelerine karşı Web uygulaması projelerine](https://msdn.microsoft.com/library/dd547590(v=vs.120).aspx) bakın.

<a id="overview"></a>
## <a name="overview-of-web-application-project-creation"></a>Web uygulaması projesi oluşturmaya genel bakış

Aşağıdaki adımlarda bir Web projesinin nasıl oluşturulacağı gösterilmektedir:

1. **Başlangıç** sayfasında veya **Dosya** menüsünde **Yeni proje** ' ye tıklayın.
2. **Yeni proje** iletişim kutusunda sol bölmedeki **Web** ' e tıklayın ve ortadaki bölmedeki **Web uygulamasında ASP.net** .

    ![Yeni Proje iletişim kutusu](creating-web-projects-in-visual-studio/_static/image1.png)

    [Azure bulut hizmeti](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy), [Azure Mobile Service](https://msdn.microsoft.com/library/windows/apps/dn629482.aspx)veya [Azure WebJob](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-webjobs)oluşturmak için sol bölmedeki **bulut** ' u seçebilirsiniz. Bu konu, bu şablonları kapsamaz.
3. Uygulamanızın sistem durumu ve kullanım izlemesini istiyorsanız sağ bölmede, **projeye Application Insights Ekle** onay kutusunu tıklatın. Daha fazla bilgi için bkz. [Web uygulamalarında performansı izleme](https://azure.microsoft.com/documentation/articles/app-insights-web-monitor-performance/).
4. Proje **adını**, **konumunu**ve diğer seçenekleri belirtin ve ardından **Tamam**' a tıklayın.

    **Yeni ASP.NET projesi** iletişim kutusu görüntülenir.

    ![Yeni Proje iletişim kutusu](creating-web-projects-in-visual-studio/_static/image2.png)
5. Bir şablona tıklayın.

    ![Şablon seçin](creating-web-projects-in-visual-studio/_static/image3.png)
6. Şablona dahil olan ek çerçeveler için destek eklemek istiyorsanız, ilgili onay kutusuna tıklayın. (Gösterilen örnekte, bir Web Forms projesine MVC ve/veya Web API 'SI ekleyebilirsiniz.)

    ![Çerçeve ekleme](creating-web-projects-in-visual-studio/_static/image4.png)
7. <a id="testproj"></a>Birim testi projesi eklemek istiyorsanız **birim testleri Ekle**' ye tıklayın.

    ![Birim testi ekleme](creating-web-projects-in-visual-studio/_static/image5.png)
8. Şablonun varsayılan olarak sağladığı farklı bir kimlik doğrulama yöntemi istiyorsanız, **kimlik doğrulamasını Değiştir**' e tıklayın.

    ![Kimlik doğrulama düğmesini Yapılandır](creating-web-projects-in-visual-studio/_static/image6.png)

    ![Kimlik doğrulamasını Yapılandır iletişim kutusu](creating-web-projects-in-visual-studio/_static/image7.png)

<a id="azurenewproj"></a>
### <a name="create-a-web-app-or-virtual-machine-in-azure"></a>Azure 'da bir Web uygulaması veya sanal makine oluşturma

Visual Studio, Web uygulamalarını barındırmak için Azure hizmetleriyle çalışmayı kolaylaştıran özellikler içerir. Örneğin, Visual Studio IDE 'den aşağıdaki her türlü hakkı gerçekleştirebilirsiniz:

- Uygulamanızı Internet üzerinden kullanılabilir hale getirmek için Web uygulamaları veya sanal makineler oluşturun ve yönetin.
- Uygulama tarafından bulutta çalışırken oluşturulan günlükleri görüntüleyin.
- Uygulama bulutta çalışırken hata ayıklama modunda uzaktan çalıştırın.
- SQL veritabanları gibi diğer Azure hizmetlerini görüntüleyin ve yönetin.

Ücretsiz olarak Web Apps gibi temel hizmetleri içeren [bir Azure hesabı oluşturabilir](https://www.windowsazure.com/pricing/free-trial/) ve bir MSDN abonesi olduğunuzda, ek Azure hizmetlerine yönelik aylık krediler sunan [avantajları etkinleştirebilirsiniz](https://azure.microsoft.com/pricing/member-offers/visual-studio-subscriptions/) . 

Varsayılan olarak, **yeni ASP.NET projesi** iletişim kutusu yeni bir Web projesi için bir Web uygulaması veya sanal makine oluşturmanızı sağlar. Yeni bir Web uygulaması veya sanal makine oluşturmak istemiyorsanız, **bulutta konak** onay kutusunun işaretini kaldırın.

![Uzak kaynaklar oluşturma](creating-web-projects-in-visual-studio/_static/image8.png)

Onay kutusu başlığı, **bulutta ana bilgisayar** olabilir veya **Uzak kaynaklar oluşturabilir**, aksi durumda etkilerden biri aynı olur. Onay kutusunu seçili bırakırsanız, Visual Studio varsayılan olarak Azure App Service bir Web uygulaması oluşturur. İsterseniz açılan kutuyu bir **sanal makineye** değiştirmek için kullanabilirsiniz. Zaten Azure 'da oturum açmadıysanız Azure kimlik bilgileri istenir. Oturum açtıktan sonra bir iletişim kutusu, Visual Studio 'Nun projeniz için oluşturulacağı kaynakları yapılandırmanızı sağlar. Aşağıdaki çizimde bir Web uygulaması için iletişim kutusu gösterilmektedir; bir sanal makine oluşturmayı seçerseniz farklı seçenekler görüntülenir.

![Azure uygulama ayarlarını yapılandırma](creating-web-projects-in-visual-studio/_static/image9.png)

Bu işlemin Azure kaynakları oluşturmak için nasıl kullanılacağı hakkında daha fazla bilgi için bkz. [Azure ve ASP.NET kullanmaya başlama](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) ve [Visual Studio ile bir Web sitesi Için sanal makine oluşturma](https://azure.microsoft.com/documentation/articles/virtual-machines-dotnet-create-visual-studio-powershell/).

Bu makalenin geri kalanında, kullanılabilir şablonlar ve bunların seçenekleri hakkında daha fazla bilgi sağlanmaktadır. Makalede ayrıca, şablonlarda kullanılan düzen ve tema çerçevesi de önyükleme, kullanıma sunulmuştur.

<a id="vs2013"></a>
## <a name="visual-studio-2013-web-project-templates"></a>Visual Studio 2013 Web projesi şablonları

Visual Studio, Web projeleri oluşturmak için şablonlar kullanır. Proje şablonu yeni projede dosya ve klasörler oluşturabilir, NuGet paketlerini yükleyebilir ve ilkel çalışan bir uygulama için örnek kod verebilir. Şablonlar en son web standartlarını uygular ve ASP.NET teknolojilerinin nasıl kullanılacağına ilişkin en iyi yöntemleri göstermek ve kendi uygulamanızı oluşturmaya yönelik bir hızlı başlangıç sağlamak üzere tasarlanmıştır.

Visual Studio 2013, .NET Framework 'ün .NET 4,5 veya sonraki sürümlerini hedefleyen projeler için Web projesi şablonları için aşağıdaki seçenekleri sağlar:

- [Boş şablon](#empty)
- [Web Forms şablonu](#wf)
- [MVC şablonu](#mvc)
- [Web API şablonu](#webapi)
- [Tek sayfalı uygulama şablonu](#spa)
- [Azure mobil hizmet şablonu](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)
- [Visual Studio 2012 şablonları](#vs2012)

Ayrıca, [Facebook şablonu](#facebook)sağlayan bir Visual Studio uzantısı da yükleyebilirsiniz.

.NET 4 ' ü hedefleyen projeler oluşturma hakkında daha fazla bilgi için bu konunun ilerleyen kısımlarında yer alan [Visual Studio 2012 şablonları](#vs2012) bölümüne bakın.

Mobil istemciler için ASP.NET uygulamaları oluşturma hakkında daha fazla bilgi için bkz. [ASP.net 'de mobil destek](../../../mobile/overview.md).

<a id="empty"></a>
### <a name="empty-template"></a>Boş şablon

Boş şablon, bir ASP.NET Web uygulaması için bir proje dosyası ( *. csproj* veya gibi) için en az klasör ve dosya sağlar. *vbproj*) ve bir *Web. config* dosyası. Web Forms, MVC ve/veya Web API 'SI için, **Klasör Ekle ve temel başvurular:** etiketi altındaki onay kutularını kullanarak destek ekleyebilirsiniz.

Boş şablon için kimlik doğrulama seçeneği yok. Kimlik doğrulama işlevselliği örnek uygulamalarda uygulanır ve boş şablon bir örnek uygulama oluşturmaz.

<a id="wf"></a>
### <a name="web-forms-template"></a>Web Forms şablonu

Web Forms Framework, Kullanıcı arabirimi ve veri erişim özelliklerinde zengin Web sitelerini hızlı bir şekilde oluşturmanıza olanak sağlayan aşağıdaki özellikleri sağlar:

- Visual Studio 'da bir WYSıWYG Tasarımcısı.
- HTML işleyen ve özellikleri ve stilleri ayarlayarak özelleştirebileceğiniz sunucu denetimleri.
- Veri erişimi ve veri görüntüleme için zengin bir denetim yelpazesi.
- WPF gibi bir istemci uygulamasını programlayabilirsiniz gibi programlayabilirsiniz.
- HTTP istekleri arasında durum (veri) otomatik olarak korunması.

Genel olarak, Web Forms bir uygulama oluşturmak, ASP.NET MVC çerçevesini kullanarak aynı uygulamayı oluşturmaktan daha az programlama çabasını gerektirir. Ancak, Web Forms yalnızca hızlı uygulama geliştirmeye yönelik değildir. Web Forms en üstünde oluşturulmuş çok karmaşık ticari uygulamalar ve çerçeveler vardır.

Bir Web Forms sayfası ve sayfadaki denetimler tarayıcıya gönderilen biçimlendirmenin çoğunu otomatik olarak oluşturduğundan, ASP.NET MVC 'nin sunduğu HTML üzerinde ayrıntılı denetim türü yoktur. Sayfaları ve denetimleri yapılandırmaya yönelik bildirim temelli model, HTML ve HTTP 'nin bazı davranışlarının yazılması için yazdığınız kod miktarını en aza indirir. Örneğin, bir denetim tarafından tam olarak hangi biçimlendirmenin üretibileceğini belirtmek her zaman mümkün değildir.

Web Forms Framework kendisini, [test odaklı geliştirme](http://en.wikipedia.org/wiki/Test-driven_development), [kaygıları ayırma](http://en.wikipedia.org/wiki/Separation_of_concerns), [denetimin sürümü](http://en.wikipedia.org/wiki/Inversion_of_control)ve [bağımlılık ekleme](http://en.wikipedia.org/wiki/Dependency_injection)gibi desenlere dayalı geliştirme uygulamalarına ASP.NET MVC olarak kullanıma hazır değildir. Bu şekilde kod yazmak istiyorsanız, şunları yapabilirsiniz; ASP.NET MVC çerçevesinde olduğu kadar otomatik değildir. [ASP.NET Web Forms MVP](http://webformsmvp.com/) projesinde, Web Forms sunmaya yönelik olarak oluşturulan hızlı geliştirmeyi sürdürirken kaygıları ve test edilebilir ayrımı sağlayan bir yaklaşım gösterilmektedir. Microsoft SharePoint, Web Forms MVP üzerine kurulmuştur.

Web Forms şablonu, yanıt veren tasarım ve tema özellikleri sağlamak için [bootstrap](#bootstrap) kullanan bir örnek Web Forms uygulaması oluşturur. Aşağıdaki çizimde giriş sayfası gösterilmektedir.

![Web Forms şablon uygulaması giriş sayfası](creating-web-projects-in-visual-studio/_static/image10.png)

Web Forms hakkında daha fazla bilgi için bkz. [ASP.NET Web Forms](https://asp.net/web-forms). Web Forms şablonunun sizin için yaptığı bilgiler hakkında daha fazla bilgi için, bkz. [Visual Studio 2013 kullanarak temel Web Forms uygulaması oluşturma](https://blogs.msdn.com/b/webdev/archive/2013/12/19/building-a-basic-web-forms-application-using-visual-studio-2013.aspx).

<a id="mvc"></a>
### <a name="mvc-template"></a>MVC şablonu

ASP.NET MVC, [test odaklı geliştirme](http://en.wikipedia.org/wiki/Test-driven_development), [kaygıları ayırma](http://en.wikipedia.org/wiki/Separation_of_concerns), [denetimin INVERSION](http://en.wikipedia.org/wiki/Inversion_of_control)ve [bağımlılık ekleme](http://en.wikipedia.org/wiki/Dependency_injection)gibi desenlere dayalı geliştirme uygulamalarını kolaylaştırmak için tasarlanmıştır. Framework, bir Web uygulamasının iş mantığı katmanını sunum katmanından ayırmayı teşvik eder. Uygulamayı modeller (M), görünümler (V) ve denetleyiciler (C) olarak bölerek ASP.NET MVC, daha büyük uygulamalarda karmaşıklığı yönetmeyi kolaylaştırabilir.

ASP.NET MVC ile doğrudan HTML ve HTTP ile Web Forms daha fazla çalışırsınız. Örneğin, Web Forms HTTP istekleri arasındaki durumu otomatik olarak koruyabilir, ancak MVC 'de açıkça kod yazmanız gerekir. MVC modelinin avantajı, tam olarak uygulamanızın yaptığı ve Web ortamında nasıl davrandığı konusunda tam denetim yapmanızı sağlar. Dezavantajı, daha fazla kod yazmanız gerekir.

MVC genişletilebilir olacak şekilde tasarlandı, Power Developers 'ın uygulama ihtiyaçları için çerçeveyi özelleştirme yeteneği sağlar. Ayrıca, ASP.NET MVC kaynak kodu bir OSı lisansı altında bulunabilir.

MVC şablonu, yanıt veren tasarım ve tema özellikleri sağlamak için [bootstrap](#bootstrap) kullanan örnek bir MVC 5 uygulaması oluşturur. Aşağıdaki çizimde giriş sayfası gösterilmektedir.

![MVC örnek uygulaması](creating-web-projects-in-visual-studio/_static/image11.png)

MVC hakkında daha fazla bilgi için bkz. [ASP.NET MVC](https://asp.net/mvc). MVC 4 şablonunu seçme hakkında daha fazla bilgi için bu makaledeki [Visual Studio 2012 şablonlar](#vs2012) bölümüne bakın.

<a id="webapi"></a>
### <a name="web-api-template"></a>Web API şablonu

Web API şablonu, MVC 'ye dayalı API Yardım sayfaları da dahil olmak üzere Web API 'sini temel alan örnek bir Web hizmeti oluşturur.

ASP.NET Web API; tarayıcılar ve mobil cihazlar dahil olmak üzere, geniş bir yelpazedeki istemcilere erişen HTTP hizmetlerini oluşturmayı kolaylaştıran bir çerçevedir. ASP.NET Web API 'SI, .NET Framework daha fazla hizmet oluşturmaya yönelik ideal bir platformdur.

Web API şablonu, örnek bir Web hizmeti oluşturur. Aşağıdaki çizimler, örnek yardım sayfalarını gösterir.

![Web API Yardım sayfası](creating-web-projects-in-visual-studio/_static/image12.png)

![GET API için Web API Yardım sayfası](creating-web-projects-in-visual-studio/_static/image13.png)

Web API 'SI hakkında daha fazla bilgi için bkz. [ASP.NET Web API](https://asp.net/web-api).

<a id="spa"></a>
### <a name="single-page-application-template"></a>Tek Sayfalı Uygulama Şablonu

Tek sayfalı uygulama (SPA) şablonu, istemcide JavaScript, HTML 5 ve [altını gizleme](http://knockoutjs.com/) ve ASP.NET Web API 'si kullanan bir örnek uygulama oluşturur.

SPA şablonuna yönelik tek kimlik doğrulama seçeneği [bireysel kullanıcı hesaplarıdır](#indauth).

Aşağıdaki çizimde, SPA şablonunun Derlemeleriyle ilgili örnek uygulamanın ilk durumu gösterilmektedir.

![SPA örnek uygulaması](creating-web-projects-in-visual-studio/_static/image14.png)

SPA şablonunu kullanarak bir uygulama oluşturma hakkında daha fazla bilgi için bkz. [Web API-dış kimlik doğrulama hizmetleri](../../../web-api/overview/security/external-authentication-services.md).

ASP.NET tek sayfalı uygulamalar hakkında daha fazla bilgi edinmek ve altını gizleme dışında JavaScript çerçeveleri kullanan ek SPA şablonları hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ASP.net tek sayfalı uygulama](../../../single-page-application/index.md).
- [VS2013 RC için SPA şablonundaki güvenlik özelliklerini anlama](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)
- [Tek sayfalı uygulamalar: ASP.NET ile modern, yanıt veren Web Apps oluşturma](https://msdn.microsoft.com/magazine/dn463786.aspx)

<a id="facebook"></a>
### <a name="facebook-template"></a>Facebook şablonu

[Facebook şablonu sağlayan bir Visual Studio uzantısı](https://go.microsoft.com/fwlink/?LinkID=509965&amp;clcid=0x409)yükleyebilirsiniz. Bu şablon, Facebook web sitesi içinde çalışacak şekilde tasarlanan bir örnek uygulama oluşturur. Bu, ASP.NET MVC 'yi temel alır ve gerçek zamanlı güncelleştirme işlevselliği için Web API kullanır.

Facebook uygulaması Facebook sitesi içinde çalıştığından ve Facebook kimlik doğrulamasına güventiğinden Facebook şablonu için kimlik doğrulama seçeneği yok.

ASP.NET Facebook uygulamaları hakkında daha fazla bilgi için bkz. [MVC Facebook API 'Sini güncelleştirme](https://blogs.msdn.com/b/webdev/archive/2014/06/10/updating-the-mvc-facebook-api.aspx).

<a id="vs2012"></a>
### <a name="visual-studio-2012-templates"></a>Visual Studio 2012 şablonları

Visual Studio 2013 Web projesi oluşturma iletişim kutusu, Visual Studio 2012 ' de bulunan bazı şablonlara erişim sağlamaz. Bu şablonlardan birini kullanmak istiyorsanız, Visual Studio yeni proje iletişim kutusunun sol bölmesinde Visual Studio 2012 düğümüne tıklayabilirsiniz.

![Visual Studio 2012 şablonları](creating-web-projects-in-visual-studio/_static/image15.png)

**Visual Studio 2012** düğümü, Visual Studio 2013 için varsayılan şablon listesinde erişiminizin olmadığı aşağıdaki Web şablonlarını seçmenizi sağlar:

- ASP.NET MVC 4 Web uygulaması
- ASP.NET dinamik veri varlıkları Web uygulaması
- ASP.NET AJAX sunucu denetimi
- ASP.NET AJAX Server Control genişletici
- ASP.NET sunucu denetimi

<a id="bootstrap"></a>
## <a name="bootstrap-in-the-visual-studio-2013-web-project-templates"></a>Visual Studio 2013 Web projesi şablonlarında önyükleme

Visual Studio 2013 proje şablonları, Twitter tarafından oluşturulan bir düzen ve tema çerçevesi olan [önyükleme](http://getbootstrap.com/)'yi kullanır. Bootstrap, yanıt veren tasarım sağlamak için CSS3 kullanır, bu da mizanpajlar farklı tarayıcı pencere boyutlarına dinamik olarak uyum sağlayabilir. Örneğin, geniş bir tarayıcı penceresinde Web Forms şablonu tarafından oluşturulan giriş sayfası aşağıdaki çizimde gösterildiği gibi görünür:

![Web Forms şablon uygulaması giriş sayfası](creating-web-projects-in-visual-studio/_static/image16.png)

Pencereyi daha dar yapın ve yatay olarak düzenlenmiş sütunlar dikey düzenlemeye geçer:

![Dikey sütun düzenlemesini önyükleme](creating-web-projects-in-visual-studio/_static/image17.png)

Pencereyi biraz daha daraltın ve yatay üst menü, dikey yönelimli bir menüye genişletmek için tıklabileceğiniz bir simgeye dönüşür:

![Önyükleme menüsü simgesi](creating-web-projects-in-visual-studio/_static/image18.png)

![Önyükleme dikey menüsü](creating-web-projects-in-visual-studio/_static/image19.png)

Uygulamanın görünüm veya hisde bir değişikliği kolay bir şekilde uygulamak için önyükleme 'nin Tema özelliğini de kullanabilirsiniz. Örneğin, temayı değiştirmek için aşağıdaki adımları uygulayabilirsiniz.

1. Tarayıcınızda [http://Bootswatch.com](http://Bootswatch.com)' a gidin, bir tema seçin ve ardından **İndir**' e tıklayın. (Bu, varsayılan olarak *Bootstrap. min. css* dosyasını INDIRIR; CSS kodunu incelemek istiyorsanız, Mini belirtilen sürüm yerine *Bootstrap. css* dosyasını alın.)
2. İndirilen CSS dosyasının içeriğini kopyalayın.
3. Visual Studio 'da, *içerik* klasöründe *bootstrap-Theme. css* adlı yeni bir **stıl sayfası** oluşturun ve indirilen CSS kodunu bu dosyaya yapıştırın.
4. *App\_start/paketi. config* dosyasını açın ve *Bootstrap. css* dosyasını *bootstrap-Theme. css*dosyasına değiştirin.

Projeyi yeniden çalıştırın ve uygulamanın yeni bir görünümü vardır. Aşağıdaki çizimde Amelia temasının etkisi gösterilmektedir:

![Bootstrap Amelia teması](creating-web-projects-in-visual-studio/_static/image20.png)

Birçok önyükleme teması mevcuttur, hem ücretsiz hem de Premium sürümler. Bootstrap Ayrıca, [açılan](http://twitter.github.io/bootstrap/components.html#dropdowns)listeler, [düğme grupları](http://twitter.github.io/bootstrap/components.html#buttonGroups)ve [simgeler](http://twitter.github.io/bootstrap/base-css.html#images)gibi çok çeşitli kullanıcı arabirimi bileşenleri sunar. Önyükleme hakkında daha fazla bilgi için bkz. [önyükleme sitesi](http://twitter.github.io/bootstrap/).

Visual Studio 'da Web Forms Tasarımcısını kullanıyorsanız, tasarımcı 'nın CSS3 desteklemediğini, bu nedenle önyükleme temalarının veya yanıt veren düzen değişikliklerinin tüm etkilerini doğru bir şekilde göstermediğini unutmayın. Ancak, Web Forms sayfaları bir tarayıcıyla görüntülenirken doğru şekilde görüntülenir.

<a id="add"></a>
## <a name="adding-support-for-additional-frameworks"></a>Ek çerçeveler için destek ekleme

Bir şablon seçtiğinizde, şablon tarafından kullanılan çerçeve (ler) i onay kutusu otomatik olarak seçilir. Örneğin, **Web Forms** şablonunu seçerseniz, **Web Forms** onay kutusu seçilidir ve bunu temizleyemezsiniz.

![Şablon seçin](creating-web-projects-in-visual-studio/_static/image21.png)

![Çerçeve ekleme](creating-web-projects-in-visual-studio/_static/image22.png)

Proje oluşturulduğunda, bu çerçeveye yönelik destek eklemek için şablonda bulunmayan bir çerçevenin onay kutusunu seçebilirsiniz. Örneğin, MVC şablonunu seçtiğinizde Web Forms *. aspx* sayfalarının kullanımını etkinleştirmek için **Web Forms** onay kutusunu seçin. Veya Web Forms şablonunu kullanırken MVC 'yi etkinleştirmek için **MVC** onay kutusuna tıklayın. Bir Framework eklemek tasarım zamanı ve çalışma zamanı desteği sunar. Örneğin, bir Web Forms projesine MVC desteği eklerseniz, fkatlama denetleyicilerini ve görünümlerini dolandırabileceksiniz.

Bir projede Web Forms ve MVC 'yi birleştirip Web Forms [kolay URL 'leri](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx) etkinleştirirseniz, BIR URL 'nin birden çok olası hedefi olduğu beklenmeyen yönlendirme sorunları olabilir. İlk olarak tanımlanan yollar öncelikli olur. Örneğin, bir `Home` denetleyiciniz ve bir *Home. aspx* sayfanız varsa, `http://contoso.com/home` URL 'si, *RouteConfig.cs*' de `MapRoute` yöntemini çağırmadan önce `EnableFriendlyUrls` metodunu çağırırsanız veya aynı URL `Home` önce `MapRoute` çağırırsanız, `EnableFriendlyUrls`denetleyicinizin varsayılan görünümüne gidecektir *.*

Çerçeve eklemek, örnek uygulama işlevselliği eklemez. Örneğin, MVC şablonunu seçtiğinizde Web Forms desteği eklerseniz, *default. aspx* giriş sayfası dosyası oluşturulmaz. Yalnızca çerçeveyi desteklemek için gereken klasörler, dosyalar ve başvurular eklenir. Bu nedenle, çerçeveler eklendiğinde, şablonlar tarafından oluşturulan örnek uygulamalardaki kodla uygulanan kimlik doğrulama seçenekleri değişmez. Örneğin, boş şablonu seçer ve Web Forms veya MVC desteği eklerseniz, **kimlik doğrulamasını Yapılandır** düğmesi yine de devre dışı bırakılır.

Aşağıdaki bölümlerde her onay kutusunun etkisi kısaca açıklanmıştır.

### <a name="add-web-forms-support"></a>Web Forms desteği ekle

Boş *uygulama\_veri* ve *model* klasörleri ve *Global. asax* dosyası oluşturur. Bunlar, boş şablon dışındaki tüm şablonlar tarafından zaten oluşturulmuştur, bu nedenle Web Forms onay kutusunun seçilmesi diğer şablonlar için farklılık yapmaz.

Web Forms şablonu, varsayılan olarak kolay URL 'Ler sağlar, ancak Web Forms onay kutusunu seçerek diğer şablonlara Web Forms desteği eklediğinizde kolay URL 'Ler otomatik olarak etkinleştirilmez.

### <a name="add-mvc-support"></a>MVC desteği ekle

MVC, Razor ve Web sayfası NuGet paketlerini yükleme, boş *uygulama\_verileri*, *denetleyicileri*, *modelleri*ve *görünümleri* klasörler oluşturur, *RouteConfig.cs* dosyası ile *uygulama\_başlangıç* klasörü oluşturur ve *Global. asax* dosyası oluşturur.

### <a name="add-web-api-support"></a>Web API desteği ekle

WebApi ve Newtonsoft. JSON NuGet paketlerini yükleyip boş *uygulama\_veri*, *Denetleyici*ve *model* klasörleri oluşturur, *WebApiConfig.cs* dosyası ile *uygulama\_başlangıç* klasörü oluşturur ve *Global. asax* dosyası oluşturur.

<a id="auth"></a>
## <a name="authentication-methods"></a>Kimlik Doğrulaması Yöntemleri

Visual Studio 2013, Web Forms, MVC ve Web API şablonları için çeşitli kimlik doğrulama seçenekleri sunar:

- [Kimlik doğrulaması yok](#noauth)
- [Bireysel kullanıcı hesapları](#indauth) (ASP.NET Identity, eski adıyla ASP.NET üyeliği olarak biliniyordu)
- [Kuruluş hesapları](#orgauth) (Windows Server Active Directory veya Azure Active Directory)
- [Windows kimlik doğrulaması](#winauth) (Intranet)

![Kimlik doğrulamasını Yapılandır iletişim kutusu](creating-web-projects-in-visual-studio/_static/image23.png)

<a id="noauth"></a>

### <a name="no-authentication"></a>Kimlik Doğrulaması Yok

**Kimlik doğrulaması yok**' u seçerseniz, örnek uygulama oturum açma için Web sayfası içermez, oturum açmış kişiyi belirten kullanıcı arabirimi, bir üyelik veritabanı için varlık sınıfı yok ve bir üyelik veritabanı için bağlantı dizesi yok.

<a id="indauth"></a>
### <a name="individual-user-accounts"></a>Bireysel kullanıcı hesapları

**Bireysel kullanıcı hesapları**seçerseniz, örnek uygulama kullanıcı kimlik doğrulaması için ASP.NET Identity (eski adıyla ASP.NET üyeliği) kullanacak şekilde yapılandırılır. ASP.NET Identity, kullanıcının sitede Kullanıcı adı ve parola oluşturarak ya da Facebook, Google, Microsoft hesabı veya Twitter gibi sosyal sağlayıcılarla oturum açarak bir hesabı kaydetmesini sağlar. ASP.NET Identity 'daki Kullanıcı profilleri için varsayılan veri deposu, üretim sitesi için SQL Server veya Azure SQL veritabanı 'na dağıtabileceğiniz bir SQL Server LocalDB veritabanıdır.

Visual Studio 2013 Bu özellikler Visual Studio 2012 ile aynıdır, ancak ASP.NET üyelik sisteminin temel alınan kodu yeniden yazıldı. Yeni kod tabanının avantajları şunları içerir:

- Yeni üyelik sistemi, ASP.NET Forms kimlik doğrulama modülü yerine [owın](http://owin.org/) 'u temel alır. Bu, IIS 'de Web Forms veya MVC kullanırken aynı kimlik doğrulama mekanizmasını kullanabileceğiniz gibi, Web API 'SI veya SignalR 'yi de kendi kendine barındırmanıza yol açabilir.
- Yeni üyelik veritabanı Entity Framework Code First tarafından yönetilir ve tüm tablolar, değiştirebileceğiniz varlık sınıfları tarafından temsil edilir. Bu, veritabanı şemasını ve profille ilgili Web Kullanıcı arabirimini kendi gereksinimlerinize uyacak şekilde kolayca özelleştirebilmeniz ve Code First Migrations kullanarak güncelleştirmelerinizi kolayca dağıtabilmeniz anlamına gelir.

Yeni üyelik sistemi yeni şablonlarda otomatik olarak uygulanır ve .NET 4,5 veya üstünü hedefleyen herhangi bir projede el ile uygulanabilir.

ASP.NET Identity, genellikle dış müşterilere yönelik bir Internet Web sitesi oluşturuyorsanız iyi bir seçenektir. Kuruluşunuz Active Directory veya Office 365 kullanıyorsa ve çalışanlar ve iş ortakları için çoklu oturum açma olanağı sağlayan bir proje oluşturmak istiyorsanız, **kuruluş hesapları** seçeneği daha iyi bir seçim olabilir.

Bireysel kullanıcı hesapları seçeneği hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [www.asp.net/identity](../../../identity/index.md). ASP.NET Web sitesindeki ASP.NET Identity hakkındaki belgeler.
- [Facebook ve Google OAuth2 ve OpenID oturum açma ile ASP.NET MVC 5 uygulaması oluşturun](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md). Ayrıca, Kullanıcı profili verilerinin nasıl özelleştirileceğini gösterir.
- [Web API-dış kimlik doğrulama hizmetleri](../../../web-api/overview/security/external-authentication-services.md)
- [Visual Studio 2013 'de ASP.NET uygulamanıza dış oturum açma işlemleri ekleme](https://blogs.msdn.com/b/webdev/archive/2013/06/27/adding-external-logins-to-your-asp-net-application-in-visual-studio-2013.aspx)

<a id="orgauth"></a>
### <a name="organizational-accounts"></a>Kuruluş hesapları

**Kuruluş hesapları**' nı seçerseniz örnek uygulama, Azure Active Directory (Office 365 IÇEREN Azure AD) veya Windows Server Active Directory Kullanıcı hesaplarına dayalı kimlik doğrulaması Için Windows Identity Foundation (WIF) kullanacak şekilde yapılandırılır. Daha fazla bilgi için bu konunun ilerleyen kısımlarında bulunan [kuruluş hesabı kimlik doğrulaması seçenekleri](#orgauthoptions) bölümüne bakın.

<a id="winauth"></a>
### <a name="windows-authentication"></a>Windows Kimlik Doğrulaması

**Windows kimlik doğrulaması**' nı seçerseniz örnek uygulama, kimlik doğrulaması Için Windows KIMLIK doğrulaması IIS modülünü kullanacak şekilde yapılandırılır. Uygulama, Windows 'da oturum açan ancak kullanıcı kaydı veya oturum açma kullanıcı ARABIRIMI içermeyen Active Directory veya yerel makine hesabının etki alanını ve kullanıcı KIMLIĞINI görüntüler. Bu seçenek Intranet web sitelerine yöneliktir.

Alternatif olarak, [kuruluş hesapları altında şirket içi seçeneğini](#orgauthonprem)belirleyerek ad kimlik doğrulaması kullanan bir Intranet sitesi oluşturabilirsiniz. Şirket Içi seçeneği Windows kimlik doğrulama modülü yerine Windows Identity Foundation (WıF) kullanır. Şirket Içi seçeneğini ayarlamak için bazı ek adımlar gereklidir, ancak WıF, Windows kimlik doğrulama modülü ile kullanılamayan özellikleri sağlar. Örneğin, Active Directory ve sorgu dizini verilerinde uygulama erişimini yapılandırabiliyorsanız, WıF ile.

<a id="orgauthoptions"></a>
## <a name="organizational-account-authentication-options"></a>Kuruluş hesabı kimlik doğrulama seçenekleri

**Kimlik doğrulaması yapılandırma** iletişim kutusu, Azure Active Directory (Office 365 IÇEREN Azure AD) veya Windows Server ACTIVE DIRECTORY (ad) hesabı kimlik doğrulaması için çeşitli seçenekler sunar:

- [Bulut-tek kuruluş](#orgauthsingle) (Azure AD veya Azure AD ile dizin TÜMLEŞTIRMESI kullanarak ad)
- [Bulut çoklu kuruluş](#orgauthmulti) (Azure AD ile dizin tümleştirmesini kullanarak Azure AD veya ad)
- Şirket [içi](#orgauthonprem) (ad)

Azure AD seçeneklerinden birini denemek ancak henüz bir hesabınız yoksa, [Azure AD hesabına kaydolmak için buraya tıklayın](https://go.microsoft.com/fwlink/?LinkId=309942).

> [!NOTE]
> Azure AD seçeneklerinden birini seçerseniz, projeniz bir veritabanı gerektirir ve Azure AD kiracınız için bir genel yönetici hesabında oturum açmanız gerekir. Azure AD kiracınız için yönetici izinlerine sahip olan bir kuruluş hesabının adını ve parolasını (örneğin, admin@contoso.onmicrosoft.com) girin.
> 
> **Oturum açma iletişim kutusunda bir Microsoft hesabı (örneğin, contoso@hotmail.com) için kimlik bilgilerini girmeyin.**

<a id="orgauthsingle"></a>
### <a name="cloud---single-organization-authentication"></a>Bulut-tek kuruluş kimlik doğrulaması

![Tek kuruluş kimlik doğrulaması](creating-web-projects-in-visual-studio/_static/image24.png)

Tek bir Azure AD [kiracısında](https://technet.microsoft.com/library/jj573650.aspx)tanımlanan Kullanıcı hesapları için kimlik doğrulamasını etkinleştirmek istiyorsanız bu seçeneği belirleyin. Örneğin, site contoso.com ve contoso.onmicrosoft.com kiracısında bulunan contoso şirketinin çalışanları tarafından kullanılabilir hale getirilir. Diğer kiracılardan gelen kullanıcıların uygulamaya erişmesine izin vermek için Azure AD 'yi yapılandıramayacaksınız.

#### <a name="domain"></a>Etki Alanı

Uygulamayı kurmak istediğiniz Azure AD etki alanını girin, örneğin: `contoso.onmicrosoft.com`. `contoso.onmicrosoft.com`yerine `contoso.com` gibi [özel bir etki alanınız](http://www.cloudidentity.com/blog/2013/04/14/adding-a-custom-domain-to-your-windows-azure-ad/)varsa buraya girebilirsiniz.

#### <a name="access-level"></a>Erişim düzeyi

Uygulamanın Graph API kullanarak dizin bilgilerini sorgulaması veya güncelleştirmesi gerekiyorsa, **Çoklu oturum açma, dizin verilerini okuma** veya **Çoklu oturum açma, dizin verilerini okuma ve yazma**seçeneklerini belirleyin. Aksi takdirde, **Çoklu oturum açma**seçeneğini belirleyin. Daha fazla bilgi için bkz. [uygulama erişim düzeyleri](https://msdn.microsoft.com/library/windowsazure/b08d91fa-6a64-4deb-92f4-f5857add9ed8#BKMK_AccessLevels) ve [Graph API kullanarak Azure AD 'yi sorgulama](https://msdn.microsoft.com/library/windowsazure/dn151791.aspx).

#### <a name="application-id-uri"></a>Uygulama KIMLIĞI URI 'SI

Varsayılan olarak, şablon proje adını Azure AD etki alanına ekleyerek sizin için bir uygulama KIMLIĞI URI 'SI oluşturur. Örneğin, proje adı `Example` ve etki alanı `contoso.onmicrosoft.com`, uygulama KIMLIĞI URI 'SI `https://contoso.onmicrosoft.com/Example`olur. Uygulama KIMLIĞI URI 'sini el ile belirtmek istiyorsanız, **diğer seçenekler** bölümünü genişletin ve metin kutusuna uygulama kimliği URI 'sini girin. Uygulama KIMLIĞI URI 'SI `https://`ile başlamalıdır.

Varsayılan olarak, Azure AD 'de zaten sağlanmış olan bir uygulama, Visual Studio 'nun proje için kullandığı aynı uygulama KIMLIĞI URI 'sine sahipse, proje yeni bir tane sağlamak yerine mevcut uygulamaya bağlanır. Bu durumda yeni bir uygulamanın sağlanmasını istiyorsanız, **aynı kimliğe sahip bir tane zaten varsa, uygulama girişinin üzerine yaz** onay kutusunu temizleyin.

**Üzerine yaz** onay kutusu silinirse ve Visual Studio aynı uygulama kimliği URI 'sine sahip mevcut bir uygulamayı bulursa, kullanacağı URI 'ye bir sayı ekleyerek yenı bir URI oluşturur. Örneğin, proje adının `Example`olduğunu varsayalım, metin kutusunu boş bırakın, **üzerine yazma** onay kutusunun işaretini kaldırın ve Azure AD KIRACıSı zaten URI `https://contoso.onmicrosoft.com/Example`olan bir uygulamaya sahiptir. Bu durumda, `https://contoso.onmicrosoft.com/Example_20130619330903`gibi bir uygulama KIMLIĞI URI 'SI ile yeni bir uygulama sağlanır.

#### <a name="provisioning-the-application-in-azure-ad"></a>Azure AD 'de uygulamayı sağlama

Uygulamayı Azure AD 'de sağlamak veya projeyi mevcut bir uygulamaya bağlamak için, Visual Studio 'nun etki alanı için bir genel yönetici kimlik bilgilerine ihtiyacı vardır. **Kimlik doğrulamasını Yapılandır** Iletişim kutusunda **Tamam** ' a tıkladığınızda, belirttiğiniz etki alanı için bir genel yöneticinin Kullanıcı adı ve parolası istenir. Daha sonra, **yeni ASP.NET proje** Iletişim kutusunda **proje oluştur** ' u tıklattığınızda, VISUAL Studio uygulamayı Azure AD 'de sağlar. Bu işlemin bir parçası olarak, Visual Studio 'nun, oluşturulduktan sonra bir yıl dolan Web. config dosyasında istemci gizli değerlerini götini unutmayın.

**Bulut tek kuruluş** kimlik doğrulaması kullanan uygulamalar oluşturma hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Azure kimlik doğrulaması](../2012/windows-azure-authentication.md)
- [Azure AD kullanarak Web uygulamanıza oturum açma ekleme](https://msdn.microsoft.com/library/windowsazure/dn151790.aspx)
- [Azure Active Directory ile ASP.NET Uygulamaları geliştirme](../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)
- [Azure AD ve Microsoft OWIN bileşenleriyle güvenli ASP.NET Web API 'SI](https://msdn.microsoft.com/magazine/dn463788.aspx)

Öğreticiler henüz Visual Studio 2013 için güncelleştirilmemiş; el ile yapmanız gereken öğreticilerin bazıları Visual Studio 2013 ' de otomatikleştirilmiştir.

<a id="orgauthmulti"></a>
### <a name="cloud---multi-organization-authentication"></a>Bulut-çoklu kuruluş kimlik doğrulaması

![Birden çok kuruluş kimlik doğrulaması](creating-web-projects-in-visual-studio/_static/image25.png)

Birden çok Azure AD [kiracılarında](https://technet.microsoft.com/library/jj573650.aspx)tanımlanan Kullanıcı hesapları için kimlik doğrulamasını etkinleştirmek istiyorsanız bu seçeneği belirleyin. Örneğin, site contoso.com ve contoso.onmicrosoft.com kiracısındaki contoso şirketinin çalışanları ve fabrikam.onmicrosoft.com kiracısında bulunan Fabrikam şirketinin çalışanları tarafından kullanılabilir hale getirilir.

Girdiğiniz ayarlar ve uygulama sağlama adımı [tek kuruluş kimlik doğrulamasına](#orgauthsingle)benzerdir.

**Bulut çoklu kuruluş** kimlik doğrulaması kullanan uygulamalar oluşturma hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- Active Directory ekip blogu üzerinde [Azure Active Directory, ASP.NET &amp; Visual Studio Ile kolay Web uygulaması tümleştirmesi](https://blogs.msdn.com/b/active_directory_team_blog/archive/2013/06/26/improved-windows-azure-active-directory-integration-with-asp-net-amp-visual-studio.aspx) .
- [Azure AD öğreticisi Ile çok kiracılı web uygulamaları geliştirme](https://msdn.microsoft.com/library/windowsazure/dn151789.aspx) . Öğretici henüz Visual Studio 2013 için güncelleştirilmedi; öğreticinin ne kadar el ile yapılacağını yönlendirdikleriniz Visual Studio 2013 ' de otomatikleştirilir.
- [Oturum açabilmeniz Için kendi birden çok kuruluşların ASP.NET uygulamasına kaydolmanız gerekir](http://www.cloudidentity.com/blog/2013/10/26/you-have-to-sign-up-with-your-own-multiple-organizations-asp-net-app-before-you-can-sign-in/). Birden çok kuruluş kimlik doğrulaması kullanan bir proje oluştururken karşılaştığı yaygın bir sorunu çözmeyi açıklayan Vittorio Bertoccı tarafından blog.

<a id="orgauthonprem"></a>
### <a name="on-premises-organizational-authentication"></a>Şirket Içi kuruluş kimlik doğrulaması

![Şirket içi kuruluş kimlik doğrulaması](creating-web-projects-in-visual-studio/_static/image26.png)

Windows Server Active Directory (AD) ' de tanımlı kullanıcı hesapları için kimlik doğrulamasını etkinleştirmek istiyorsanız ve Azure AD 'yi kullanmak istemiyorsanız bu seçeneği belirleyin. Bu seçeneği, bir Intranet sitesi veya bir Internet sitesi oluşturmak için kullanabilirsiniz. Bir Internet sitesi için AD 'ye erişim sağlamak üzere Active Directory Federasyon Hizmetleri (AD FS) (ADFS) kullanın. Daha fazla bilgi için, bkz. [ASP.net Ile şirket Içi kuruluş kimlik doğrulaması seçeneğini (ADFS) kullanma Visual Studio 2013](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/).

Bir Intranet sitesi için, alternatif olarak, bu seçenek yerine [Windows kimlik doğrulaması](#winauth) ' nı seçebilirsiniz. Windows kimlik doğrulama seçeneği için bir meta veri belgesi URL 'SI sağlamanız gerekmez. Ancak, Windows kimlik doğrulaması size Active Directory veya dizin verilerini sorgulamak için uygulama erişimini denetleme olanağı sağlamaz.

#### <a name="on-premises-authority"></a>Şirket Içi yetkili

Meta veri belgesine işaret eden bir URL girin. Meta veri belgesi, yetkilinin koordinatlarını içerir. Uygulama, Web oturumu açma akışını barındıracak şekilde bu koordinatları kullanacaktır.

#### <a name="application-id-uri"></a>Uygulama KIMLIĞI URI 'SI

AD 'nin bu uygulamayı tanımlamak için kullanabileceği benzersiz bir URI sağlayın veya Visual Studio 'Nun bir tane oluşturmasını sağlamak için boş bırakın.

<a id="nextsteps"></a>
## <a name="next-steps"></a>Sonraki adımlar

Bu belge, Visual Studio 2013 yeni bir ASP.NET Web projesi oluşturmak için bazı temel yardım sağladı. Web geliştirme için Visual Studio 'yu kullanma hakkında daha fazla bilgi için bkz. [https://www.asp.net/visual-studio/](../../index.md).
