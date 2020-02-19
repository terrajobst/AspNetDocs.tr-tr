---
uid: mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
title: ASP.NET MVC Uygulamanızda hatalarla hata ayıklayın ve göz at! Microsoft Docs
author: Rick-Anderson
description: Imampte, ASP.NET a için ayrıntılı performans, hata ayıklama ve tanılama bilgileri sağlayan açık kaynaklı ve büyüyen açık kaynaklı NuGet paketleri ailesidir.
ms.author: riande
ms.date: 03/26/2015
ms.assetid: c205805f-efdd-4fa7-9616-f26eab180611
msc.legacyurl: /mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
msc.type: authoredcontent
ms.openlocfilehash: d3689147a3bc3aa1f4180c377d2483a94bdd95a9
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457667"
---
# <a name="profile-and-debug-your-aspnet-mvc-app-with-glimpse"></a>Glimpse ile ASP.NET MVC uygulamanızın profilini oluşturma ve hatalarını ayıklama

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> Imampte, ASP.NET uygulamaları için ayrıntılı performans, hata ayıklama ve tanılama bilgileri sağlayan açık kaynaklı bir ve büyüyen açık kaynaklı NuGet paketleri ailesidir. Her sayfanın en altında önemli performans ölçümlerini yüklemek, basit, ultra hızlı bir şekilde yüklemektir. Sunucuda neler olduğunu bulmanız gerektiğinde uygulamanızın detayına gitmenizi sağlar. Bu sayede, Azure test ortamınız dahil olmak üzere geliştirme döngünüzde kullanmanızı önerdiğimiz çok değerli bilgiler sunulmaktadır. [Fiddler](http://www.telerik.com/fiddler) ve [F-12 geliştirme araçları](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx) bir istemci tarafı görünümü sağlarken, bu, sunucudan ayrıntılı bir görünüm sağlar. Bu öğretici, bir diğer çok paket olan ASP.NET MVC ve EF paketlerini kullanmaya odaklanacaktır. Mümkün olduğunca, bakımı istediğim uygun bir yardım [belgelerine](http://getglimpse.com/Docs/) bağlayacağım. Bir açık kaynaklı projem, kaynak koda ve belgelere de katkıda bulunabilirsiniz.

- [Göz at yükleme](#ig)
- [Localhost için göz at 'ı etkinleştir](#eg)
- [Zaman çizelgesi sekmesi](#Time)
- [Model Bağlamaları](#mb)
- [Rotalar](#route)
- [Azure 'da göz at kullanma](#da)
- [Ek Kaynaklar](#addRes)

<a id="ig"></a>
## <a name="installing-glimpse"></a>Göz at yükleme

, NuGet paket yöneticisi konsolundan veya **NuGet Paketlerini Yönet** konsolundan bir göz atmak sağlayabilirsiniz. Bu demo için Mvc5 ve EF6 paketlerini yükleyeceğim:

![NuGet DLG 'ten bir göz at yüklemesi](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image1.png)

*Göz at. EF* için arama

![NuGet Install DLG 'ten tımpi. EF](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image2.png)

**Yüklü paketler**' i seçerek, yüklü olan tımpde bağımlı modüllerin yüklendiğini görebilirsiniz:

![DLg 'ten bir Tımpo paketleri yüklendi](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image3.png)

Aşağıdaki komutlar, paket yöneticisi konsolundan Tımpo MVC5 ve EF6 modüllerini yükler:

[!code-console[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample1.cmd)]

<a id="eg"></a>
## <a name="enable-glimpse-for-localhost"></a>Localhost için göz at 'ı etkinleştir

http://localhost:&lt;p ort #&gt;/tımpse.exe öğesine gidin ve <strong>Aç</strong> düğmesine tıklayın.

![Göz atlama sayfası](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image4.png)

Sık Kullanılanlar çubuğunuzu görüntüleniyorsa, Tımpi düğmelerini sürükleyip bırakabilir ve bunları bookmarkas olarak ekleyebilirsiniz:

![Göz at ile IE](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image5.png)

Artık uygulamanızda gezinebilirsiniz ve sayfanın alt kısmında **başlık ekranı** (HUD) gösterilir.

![HUD ile Contact Manager sayfası](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image6.png)

[Göz at sayfası](http://getglimpse.com/Docs/Heads-up-Display) , yukarıda gösterilen zamanlama bilgilerinin ayrıntılarını. HUD 'nin görüntülediği performans verileri, test döngüsüne başlamadan önce bir sorunla hemen haberdar edebilir. Sağ alt köşedeki &quot;g&quot; tıklamak, bu paneli getirir:

![Göz at bölmesi](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image7.png)

Yukarıdaki görüntüde, işlem hattındaki eylemlerin ve filtrelerin zamanlama ayrıntılarını gösteren [yürütme sekmesi](http://getglimpse.com/Docs/Execution-Tab) seçilidir. [Durdurma izleme filtre süreölçeri](http://www.nuget.org/packages/StopWatch/) ' nin işlem hattının 6. aşamasında başlamasını sağlayabilirsiniz. Hafif ağırlık zamanımı faydalı profil/zamanlama verileri sağlayabiliyorsa, yetkilendirme ve Görünüm işleme için harcanan tüm süreyi yok bulur. [ASP.NET MVC uygulamanızı profilde ve zaman zaman Azure 'a yönelik olarak](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx)zamanımı hakkında bilgi edinebilirsiniz. [Sekmeler](http://getglimpse.com/Docs/Tabs) sayfası, her sekme hakkında ayrıntılı bilgi için bağlantılar sağlar.

<a id="Time"></a>
## <a name="the-timeline-tab"></a>Zaman çizelgesi sekmesi

Aşağıdaki kod ile ilgili olarak, Dykstra 'in bekleyen [EF 6/MVC 5 öğreticisini](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) , Eğitmenler denetleyicisine değiştirdim:

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample2.cs?highlight=1,20-31)]

Yukarıdaki kod, verilerin Eager veya açıkça yüklenmesini denetlemek için sorgu dizesinde (`eager`) geçiş yapmasına olanak tanır. Aşağıdaki görüntüde, açık yükleme kullanılır ve zamanlama sayfası `Index` eylem yönteminde yüklenen her kaydı gösterir:

![açık yükleme](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image8.png)

Aşağıdaki kodda, Eager belirtilir ve `Index` görünümü çağrıldıktan sonra her kayıt getirilir:

![Eager belirtildi](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image9.png)

Ayrıntılı zamanlama bilgileri almak için bir zaman diliminin üzerine geleleyebilirsiniz:

![ayrıntılı zamanlamayı görmek için üzerine gelin](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image10.png)

<a id="mb"></a>
## <a name="model-binding"></a>Model bağlama

[Model bağlama sekmesi](http://getglimpse.com/Docs/Model-Binding-Tab) , form değişkenlerinizin nasıl bağlandığını anlamanıza yardımcı olmak için çok fazla bilgi sağlar. Aşağıdaki görüntüde gösterir **?** simgesine tıklayarak bu özellik için yardım sayfasını bulabilirsiniz.

![göz uyumlu model bağlama görünümü](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image11.png)

<a id="route"></a>
## <a name="routes"></a>Yollar

 Diğer yollar sekmesi, yönlendirmeye hata ayıklamanıza ve anlamanıza yardımcı olabilir. Aşağıdaki görüntüde, ürün rotası seçilidir (ve yeşil, bir bir göz kuralı olarak gösterilir). ![ürün adı](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) yol kısıtlamaları, bölgeler ve veri belirteçleri de görüntülenir. Daha fazla bilgi için bkz. [ASP.NET MVC 5 içindeki](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx) [Tımpo rotaları](http://getglimpse.com/Docs/Routes-Tab) ve öznitelik yönlendirme. 

<a id="da"></a>
## <a name="using-glimpse-on-azure"></a>Azure 'da göz at kullanma

Bu varsayılan güvenlik ilkesi, yalnızca bir yerel konaktan tımpo verilerinin görüntülenmesine izin verir. Bu verileri uzak bir sunucuda (örneğin, Azure 'da bir Web uygulaması) görüntüleyebilmeniz için bu güvenlik ilkesini değiştirebilirsiniz. Azure 'daki test ortamları için, dikkat etmek üzere *Web. config* dosyasının en altına vurgulanan işareti ekleyin:

[!code-xml[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample3.xml?highlight=2-6)]

Bu değişiklik tek başına, herhangi bir Kullanıcı, uzak bir sitede bulunan tüm kullanıcılar için veri görebilir. Yukarıdaki biçimlendirmeyi bir yayımlama profiline eklemeyi göz önünde bulundurun, böylece yalnızca bu yayımlama profilini kullandığınızda (örneğin, Azure test profiliniz) uygulanan bir uygulanmış şekilde dağıtılır. Diğer verileri kısıtlamak için `canViewGlimpseData` rolünü ekleyecek ve yalnızca bu roldeki kullanıcıların, Tımpo verilerini görüntülemesine izin vereceğiz.

*GlimpseSecurityPolicy.cs* dosyasından açıklamaları kaldırın ve `Administrator` [isinrole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx) çağrısını `canViewGlimpseData` rolüne değiştirin:

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample4.cs?highlight=6)]

> [!WARNING]
> Güvenlik-bir bakışta sunulan zengin veriler, uygulamanızın güvenliğini açığa çıkarır. Microsoft, üretimler uygulamalarında kullanım için bir güvenlik denetimi gerçekleştirmedi.

Rol ekleme hakkında daha fazla bilgi için bkz. [Üyelik, OAuth ve SQL veritabanı Ile güvenli ASP.NET MVC 5 Web uygulamasını Azure 'Da dağıtma](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) öğreticisi.

<a id="addRes"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

- [Üyelik, OAuth ve SQL veritabanı ile güvenli bir ASP.NET MVC 5 uygulamasını Azure 'a dağıtma](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)
- Bir [yapılandırma](http://getglimpse.com/Docs/Configuration) , çalışma zamanı ilkesi, günlüğe kaydetme ve daha fazlasını yapılandırma üzerindeki bir disk sayfası.
