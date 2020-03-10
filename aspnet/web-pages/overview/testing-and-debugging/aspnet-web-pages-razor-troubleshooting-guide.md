---
uid: web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
title: ASP.NET Web Pages (Razor) sorun giderme kılavuzu | Microsoft Docs
author: Rick-Anderson
description: Bu makalede, ASP.NET Web Pages (Razor) ve bazı önerilen çözümlerle çalışırken karşılaşabileceğiniz sorunlar açıklanmaktadır. Yazılım sürümleri ASP.NET Web pag...
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 2a2c1833-0bfe-4e2e-9cc0-341b52c7b121
msc.legacyurl: /web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
msc.type: authoredcontent
ms.openlocfilehash: fc03767c16f46c1e282d24ee3a7df2409a7c38bb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78585766"
---
# <a name="aspnet-web-pages-razor-troubleshooting-guide"></a>ASP.NET Web Sayfaları (Razor) Sorun Giderme Kılavuzu

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede, ASP.NET Web Pages (Razor) ve bazı önerilen çözümlerle çalışırken karşılaşabileceğiniz sorunlar açıklanmaktadır.
> 
> ## <a name="software-versions"></a>Yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 3
>   
> 
> Bu öğretici Ayrıca ASP.NET Web Pages 2 ve ASP.NET Web Pages 1,0 ile de kullanılabilir.

Bu konu aşağıdaki bölümleri içermektedir:

- [Çalışan sayfalarla ilgili sorunlar](#Issues_Running_.cshtml_Pages)
- [Razor kodlu sorunlar](#IssuesWithRazorCode)
- [Güvenlik ve üyelikle ilgili sorunlar](#membership)
- [E-posta gönderme sorunları](#email)
- [Ek Kaynaklar](#AdditionalResources)

Genel sorular için bkz. [ASP.NET Web Pages (Razor) SSS](https://go.microsoft.com/fwlink/?LinkId=253000).

<a id="Issues_Running_.cshtml_Pages"></a>
## <a name="issues-with-running-pages"></a>Çalışan sayfalarla ilgili sorunlar

Birçok sorun, *. cshtml* ve *. vbhtml* sayfalarının düzgün çalışmasını engelleyebilir. Bu bölümde, yaygın hata iletileri ve olası nedenler listelenmektedir.

### <a name="http-error-403---forbidden-access-is-denied"></a>HTTP Hatası 403-Yasak: erişim reddedildi

*Sağladığınız kimlik bilgilerini kullanarak bu dizini veya sayfayı görüntüleme izniniz yok.*

Bu hata, sunucu doğru .NET Framework sürümünü çalıştırmadığından oluşabilir. Sunucuyu (yerel olarak veya uzaktan) çalıştıran bilgisayarın en azından .NET Framework 4 ' ün yüklü olduğundan emin olun. Ayrıca, uygulamanın kendisinin doğru sürümü çalıştıracak şekilde yapılandırıldığından emin olun.

WebMatrix 'te çalışırken bu sorunu yerel olarak görürseniz, **site** çalışma alanına tıklayın ve ardından TreeView 'da **Ayarlar**' a tıklayın. **.NET Framework sürüm Seç** listesinde, **.NET 4 (tümleşik)** öğesini seçin. Bu sürüm zaten ayarlandıysa, WebMatrix 'i yönetici olarak çalıştırmayı deneyin.

Web sitenizin kökünde en az bir *. cshtml* dosyası bulunduğundan emin olun.

Web sunucusu uzak bir sunucuda olduğunda bu hatayı görürseniz, sunucu yöneticisine başvurun. Sunucuda .NET Framework 4 veya sonraki bir sürümünün yüklü olduğundan emin olun. Ayrıca, uygulamanın bu the.NET Framework sürümünü kullanacak şekilde yapılandırılmış bir uygulama havuzunda çalıştığından emin olun.

Sunucu üzerinde denetiminiz varsa, .NET Framework doğru sürümünü çalıştırdığından emin olun. Ayrıca, `aspnet_regiis -iru` komutunu çalıştırarak yüklemeyi onarmayı deneyebilirsiniz. (Örneğin, .NET Framework yükledikten sonra IIS yüklerseniz, IIS ASP.NET sayfalarını çalıştıracak şekilde doğru şekilde yapılandırılmayacak.) Daha fazla bilgi için bkz. [ASP.NET IIS Kayıt Aracı (Aspnet\_regııs. exe)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx).

### <a name="http-error-40314---forbidden"></a>HTTP Hatası 403,14-yasak

*Web sunucusu bu dizinin içeriğini listebir şekilde yapılandırılmamış.*

Bu hata, korunan bir kaynak ( *Web. config* dosyası gibi) veya korunan bir klasörde ( *App\_verileri* veya *uygulama\_kodu*gibi) istenirse oluşabilir.

### <a name="http-error-40417---not-found"></a>HTTP hatası 404,17-bulunamadı

*İstenen içerik betik gibi görünüyor ve statik dosya işleyicisi tarafından sunulmayacak.*

Bu hata, sunucu .NET Framework 4 veya üzeri bir sürümü kullanmak için doğru yapılandırılmamışsa ve bu nedenle, `@{ }` bloklarda kodu tanımadığı durumlarda meydana gelebilir. Bkz. *http hatası 403-Yasak: erişim reddedildi*.

### <a name="http-error-4047---not-found"></a>HTTP hatası 404,7-bulunamadı

*İstek filtreleme modülü dosya uzantısını reddedecek şekilde yapılandırıldı*

Bu hata, sunucuda *. cshtml* veya *. vbhtml* uzantıları açıkça engellenmişse oluşabilir. Bu sorunun belirtisi, URL 'Lerin uzantı içermediği durumlarda çalıştığı, ancak *. cshtml* veya *. vbhtml* içeren URL 'lerin çalışmamasından oluşur. Olası bir çözüm, sitenin *Web. config* dosyasındaki uzantıları yeniden etkinleştirmektir. Aşağıdaki örnekte *. cshtml* uzantısının nasıl etkinleştirileceği gösterilmektedir.

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample1.xml?highlight=5-6)]

### <a name="http-error-4048---not-found"></a>HTTP hatası 404,8-bulunamadı

*İstek filtreleme modülü, bir hiddenSegment bölümü içeren URL 'deki bir yolu reddedecek şekilde yapılandırılmıştır.*

Bu hata, korunan bir kaynak ( *Web. config* dosyası gibi) veya korunan bir klasörde ( *App\_verileri* veya *uygulama\_kodu*gibi) istenirse oluşabilir.

### <a name="this-type-of-page-is-not-served-server-error-in--application"></a>Bu tür bir sayfaya sunulmuyor ('/' uygulamasında sunucu hatası)

Daha önce HTTP hatası 404,17 için açıklamaya bakın.

<a id="IssuesWithRazorCode"></a>
## <a name="issues-with-razor-code"></a>Razor kodlu sorunlar

### <a name="the-name-class-does-not-exist-in-the-current-context"></a>'*Class*' adı geçerli bağlamda yok

Genellikle, bu hatayı görmanızın bir nedeni `class` bir yardımcı başvuru, ancak yardımcı yüklenmez. Örneğin, bir yardımcı kullanmaya çalışırsanız, ancak paketi NuGet 'den yüklemediyseniz bu hatayı görürsünüz. Yardımcıyı bulmak ve yüklemek için WebMatrix 'teki galeriyi kullanın.

Yardımcı yüklenirse, ancak sayfa hala tanınmıyorsa, koda bir `using` ekleyin ifadesini eklemeyi deneyin. `using` bildiriminde, yardımcı içeren ad alanına başvurun. Örneğin, ASP.NET Web yardımcıları paketindeki temel yardımcılar `System.Web.Helpers` ad alanıdır. Yardımcı 'yı kullanmak istediğiniz sayfanın en üstünde şu satırı ekleyin:

`@using Microsoft.Web.Helpers;`

<a id="membership"></a>
## <a name="issues-with-security-and-membership"></a>Güvenlik ve üyelikle ilgili sorunlar

ASP.NET Web Pages (Razor) içinde yerleşik güvenlik (üyelik) sistemini kullanıyorsanız, aşağıdaki sorunlarla karşılaşabilirsiniz.

### <a name="to-call-this-method-the-membershipprovider-property-must-be-an-instance-of-extendedmembershipprovider"></a>Bu yöntemi çağırmak için, "Membership. Provider" özelliği "ExtendedMembershipProvider" öğesinin bir örneği olmalıdır

Bu hata, `AspNetSqlMembershipProvider` sınıfının yapılandırılmadığını gösterebilir. (Bir belirti, sitenin yerel olarak ince çalışacağından, ancak bir barındırma sağlayıcısının sunucusunda yayımladığınızda bu hatayı oluşturur.) Bu sorunun bir onarımı, sitenin *Web. config* dosyasına aşağıdakini ekleyerek basit üyeliği açıkça etkinleştirmektir:

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample2.xml?highlight=6)]

<a id="email"></a>
## <a name="issues-with-sending-email"></a>E-posta gönderme sorunları

E-posta gönderme sorunları hata ayıklaması zor olabilir. Bir ilk sorun, SMTP sunucusuna bağlanamadan olabilir. Bağlantı başarılı olursa, iletiyi SMTP sunucusuna ASP.NET. Ancak, iletinin kendisiyle birlikte SMTP sunucusunun göndermesini önleyen sorunlar olabilir.

Uygulamanız başarılı bir şekilde e-posta göndermezse, aşağıdakileri deneyin:

- SMTP sunucusu adı genellikle `smtp.provider.com` veya `smtp.provider.net`gibi bir şeydir. Ancak, sitenizi bir barındırma sağlayıcısına yayımlarsanız, söz konusu noktada SMTP sunucu adı `localhost`olabilir. Bu durum, yayımladıktan ve sitenizin sağlayıcının sunucusunda çalışıyor olması nedeniyle, SMTP sunucusu uygulamanızın perspektifinden yerel olabilir. Sunucu adlarında bu değişiklik, yayımlama işleminizin bir parçası olarak SMTP sunucu adını değiştirmeniz gerektiği anlamına gelebilir.
- Bağlantı noktası numarası genellikle 25 ' tir. Ancak, bazı sağlayıcılar bağlantı noktası 587 ' yı veya başka bir bağlantı noktasını kullanmanızı gerektirir. SMTP sunucusunun sahibine, kullanmanız beklenen bağlantı noktası numarasını kontrol edin.
- Doğru kimlik bilgilerini kullandığınızdan emin olun. Sitenizi bir barındırma sağlayıcısına yayımladıysanız, sağlayıcının özel olarak belirttiği kimlik bilgilerini e-posta için kullanın. Bu kimlik bilgileri, yayımlamak için kullandığınız kimlik bilgilerinden farklı olabilir.
- Bazen kimlik bilgilerine gerek kalmaz. Kişisel ISS 'nizi kullanarak e-posta gönderiyorsanız, e-posta sağlayıcınız kimlik bilgilerinizi zaten bilir. Yayımladıktan sonra, yerel bilgisayarınızda sınama yaparken farklı kimlik bilgileri kullanmanız gerekebilir.
- E-posta sağlayıcınız şifreleme kullanıyorsa, `WebMail.EnableSsl` `true`olarak ayarlayın.

E-posta gönderilirken bir hata oluşursa, şuna benzer bir standart ASP.NET hata iletisi görebilirsiniz:

![E-postada bir sorun olduğunda ASP.NET hata iletisi](aspnet-web-pages-razor-troubleshooting-guide/_static/image1.png)

Ayrıca, aşağıdaki örnekte olduğu gibi `try-catch` bloğu kullanarak e-posta gönderme sorunlarını da ayıklayabilirsiniz. Bir `try-catch` bloğu kullandığınızda, ASP.NET standart hata iletilerini görüntülemez. Bunun yerine, hatayı bloğun `catch` bölümünde yakalayabilirsiniz.

[!code-cshtml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample3.cshtml)]

`your-SMTP-server-name`için uygun değerleri değiştirin ve bu şekilde devam edin. Bu şekilde, bazı hata iletileri şunları görebilirsiniz:

- *Posta gönderilirken hata oluştu.*

    veya

    *Bağlı olan taraf bir süre sonra düzgün bir şekilde yanıt vermediğinden veya bağlı konak yanıt vermediğinden bağlantı kurulamadığı için bağlantı girişimi başarısız oldu*

    Bu hata genellikle uygulamanın SMTP sunucusuna bağlanamabileceği anlamına gelir. Sunucu adını ve bağlantı noktası numarasını kontrol edin.
- *Posta kutusu kullanılamıyor. Sunucu yanıtı: 5.1.0 &lt;someuser@invaliddomain&gt; gönderen reddedildi: geçersiz gönderici etki alanı*

    Bu ileti, `From` adresinin doğru olmadığını veya eksik olduğunu gösteriyor olabilir.
- *Belirtilen dize, bir e-posta adresi için gereken biçimde değil.*

    Bu hata, `To` veya `From` özelliklerinin bir e-posta adresi olarak tanınmadığını gösterebilir. (ASP.NET, e-posta adresinin geçerli olduğunu, yalnızca *name@domain.com* gibi doğru biçimde olduğunu kontrol edemez.)

> [!NOTE]
> Sayfayı canlı bir siteye yayımlamadan önce hatayı gösteren biçimlendirmeyi kaldırın (`@errorMessage`). Kullanıcıların bir sunucudan aldığınız hata iletilerini görmesini sağlamak iyi bir fikir değildir.

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

[ASP.NET Web Sayfaları (Razor) SSS](https://go.microsoft.com/fwlink/?LinkId=253000)

ASP.NET Web sitesinde [WebMatrix ve ASP.NET Web Pages](https://forums.asp.net/1224.aspx/1?WebMatrix) Forumu
