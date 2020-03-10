---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
title: ASP.NET MVC 'yi farklı IIS sürümleriyle kullanma (C#) | Microsoft Docs
author: microsoft
description: Bu öğreticide, farklı Internet Information Services sürümleriyle ASP.NET MVC ve URL yönlendirmeyi nasıl kullanacağınızı öğreneceksiniz. Farklı stratejiler öğrenirsiniz...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: b0cf4a34-2c1d-4717-bb54-ff029e722990
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
msc.type: authoredcontent
ms.openlocfilehash: 3b0a9509c0600f3598fd1218a7b383430548d4c0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601103"
---
# <a name="using-aspnet-mvc-with-different-versions-of-iis-c"></a>ASP.NET MVC’yi Farklı IIS Sürümleriyle Kullanma (C#)

[Microsoft](https://github.com/microsoft) tarafından

> Bu öğreticide, farklı Internet Information Services sürümleriyle ASP.NET MVC ve URL yönlendirmeyi nasıl kullanacağınızı öğreneceksiniz. IIS 7,0 (klasik mod), IIS 6,0 ve IIS 'nin önceki sürümleriyle ASP.NET MVC 'yi kullanmak için farklı stratejiler öğrenirsiniz.

ASP.NET MVC Framework, tarayıcı isteklerini denetleyici eylemlerine yönlendirmek için ASP.NET yönlendirmeye bağımlıdır. ASP.NET yönlendirmenin avantajlarından yararlanabilmek için Web sunucunuzda ek yapılandırma adımları gerçekleştirmeniz gerekebilir. Hepsi, uygulamanız için Internet Information Services (IIS) sürümüne ve istek işleme moduna bağlıdır.

Farklı IIS sürümlerinin özeti aşağıda verilmiştir:

- IIS 7,0 (tümleşik mod)-ASP.NET yönlendirmeyi kullanmak için özel yapılandırma gerekmez.
- IIS 7,0 (klasik mod)-ASP.NET yönlendirmeyi kullanmak için özel yapılandırma gerçekleştirmeniz gerekir.
- IIS 6,0 veya altı-ASP.NET Routing kullanmak için özel yapılandırma gerçekleştirmeniz gerekir.

En son IIS sürümü 7,5 sürümüdür (Win7). IIS 7 IIS, Windows Server 2008 ve VISTA/SP1 ve üzeri sürümlerde bulunur. Ayrıca, Home Basic dışında Vista işletim sisteminin herhangi bir sürümüne IIS 7,0 ' ü yükleyebilirsiniz (bkz. [https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)).

IIS 7,0, istekleri işlemek için iki modu destekler. Tümleşik mod veya klasik mod kullanabilirsiniz. Tümleşik modda IIS 7,0 kullanırken özel yapılandırma adımları gerçekleştirmeniz gerekmez. Ancak, Klasik modda IIS 7,0 kullanırken ek yapılandırma gerçekleştirmeniz gerekir.

Microsoft Windows Server 2003, IIS 6,0 içerir. Windows Server 2003 işletim sistemini kullanırken IIS 6,0 ' i IIS 7,0 ' e yükseltemezsiniz. IIS 6,0 kullanırken ek yapılandırma adımları gerçekleştirmeniz gerekir.

Microsoft Windows XP Professional, IIS 5,1 içerir. IIS 5,1 kullanırken ek yapılandırma adımları gerçekleştirmeniz gerekir.

Son olarak, Microsoft Windows 2000 ve Microsoft Windows 2000 Professional, IIS 5,0 içerir. IIS 5,0 kullanırken ek yapılandırma adımları gerçekleştirmeniz gerekir.

## <a name="integrated-versus-classic-mode"></a>Klasik ve klasik moda karşı

IIS 7,0, istekleri iki farklı istek işleme modu kullanarak işleyebilir: tümleşik ve klasik. Tümleşik mod daha iyi performans ve daha fazla özellik sağlar. Klasik mod, önceki IIS sürümleriyle geriye dönük uyumluluk için eklenmiştir.

İstek işleme modu, uygulama havuzu tarafından belirlenir. Uygulamayla ilişkili uygulama havuzunu belirleyerek belirli bir Web uygulaması tarafından hangi işleme modunun kullanıldığını belirleyebilirsiniz. Aşağıdaki adımları uygulayın:

1. Internet Information Services Yöneticisini başlatın
2. Bağlantılar penceresinde bir uygulama seçin
3. Eylemler penceresinde, **temel ayarlar** bağlantısına tıklayarak uygulamayı Düzenle iletişim kutusunu açın (bkz. Şekil 1)
4. Seçili uygulama havuzunu bir yere göz atın.

IIS, varsayılan olarak iki uygulama havuzunu destekleyecek şekilde yapılandırılmıştır: **DefaultAppPool** ve **Klasik .NET AppPool**. DefaultAppPool seçilirse, uygulamanız tümleşik istek işleme modunda çalışır. Klasik .NET AppPool seçilirse, uygulamanız klasik istek işleme modunda çalışmaktadır.

[Yeni proje iletişim kutusunu ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.png)

**Şekil 1**: istek işleme modu algılanıyor ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.png))

İstek işleme modunu, uygulamayı Düzenle iletişim kutusunda değiştirebildiğinize dikkat edin. Seç düğmesine tıklayın ve uygulamayla ilişkili uygulama havuzunu değiştirin. ASP.NET uygulamasını klasik moddan tümleşik moda değiştirirken uyumluluk sorunları olduğunu unutmayın. Daha fazla bilgi için aşağıdaki makalelere bakın:

- ASP.NET 1,1 'i Windows Vista ve Windows Server 2008 'de IIS 7,0 'ye yükseltme-- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)
- ASP.NET Integration with IIS 7,0- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)

Bir ASP.NET uygulaması DefaultAppPool kullanıyorsa, ASP.NET yönlendirme (ve bu nedenle ASP.NET MVC) almak için ek adımlar gerçekleştirmeniz gerekmez. Ancak, ASP.NET uygulaması klasik .NET AppPool 'ı kullanacak şekilde yapılandırıldıysa, daha fazla işe devam edebilirsiniz.

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a>Daha eski IIS sürümleriyle ASP.NET MVC kullanma

IIS 7,0 ' den daha eski bir IIS sürümüyle ASP.NET MVC kullanmanız gerekiyorsa veya IIS 7,0 ' nı Klasik modda kullanmanız gerekiyorsa, iki seçeneğiniz vardır. İlk olarak, yol tablosunu dosya uzantılarını kullanacak şekilde değiştirebilirsiniz. Örneğin,/Store/Details gibi bir URL istemek yerine,/Store.exe gibi bir URL istemeniz gerekir.

İkinci seçenek *joker karakter betik eşlemesi*adlı bir şey oluşturmaktır. Joker karakter betik eşlemesi, her isteği ASP.NET çerçevesine eşlemenizi sağlar.

Web sunucunuza erişiminiz yoksa (örneğin, ASP.NET MVC uygulamanız bir Internet hizmeti sağlayıcısı tarafından barındırılıyorsa), ilk seçeneği kullanmanız gerekir. URL 'nizin görünümünü değiştirmek istemiyorsanız ve Web sunucunuza erişiminiz varsa, ikinci seçeneği kullanabilirsiniz.

Her bir seçeneği aşağıdaki bölümlerde ayrıntılı olarak araştırıyoruz.

## <a name="adding-extensions-to-the-route-table"></a>Yol tablosuna uzantı ekleme

Daha eski IIS sürümleriyle çalışmak için ASP.NET yönlendirme almanın en kolay yolu, Global. asax dosyasındaki yol tablonuzu değiştirmektir. Listeleme 1 ' deki varsayılan ve değiştirilmemiş Global. asax dosyası varsayılan yol adlı bir yolu yapılandırır.

**Listeleme 1-Global. asax (değiştirilmemiş)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample1.cs)]

Liste 1 ' de yapılandırılan varsayılan yol, aşağıdaki gibi görünen URL 'Leri yönlendirmenizi sağlar:

/Home/Index

/Product/Details/3

/Ürün

Ne yazık ki IIS 'nin daha eski sürümleri bu istekleri ASP.NET çerçevesine geçirmez. Bu nedenle, bu istekler bir denetleyiciye yönlendirilmez. Örneğin,/Home/Index URL 'SI için bir tarayıcı isteği yaparsanız, Şekil 2 ' de hata sayfasını alırsınız.

[Yeni proje iletişim kutusunu ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.png)

**Şekil 2**: 404 olmayan bir hata alma ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.png))

Daha eski IIS sürümleri yalnızca belirli istekleri ASP.NET çerçevesine eşler. İstek, doğru dosya uzantısına sahip bir URL için olmalıdır. Örneğin,/SomePage.aspx için bir istek ASP.NET çerçevesine eşlenir. Ancak,/SomePage.htm için bir istek değildir.

Bu nedenle, ASP.NET yönlendirmenin çalışmasını sağlamak için, varsayılan yolu ASP.NET çerçevesine eşlenmiş bir dosya uzantısı içerecek şekilde değiştirmemiz gerekir.

Bu, `registermvc.wsf`adlı bir komut dosyası kullanılarak yapılır. Bu, `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`'de ASP.NET MVC 1 sürümüne eklenmiştir, ancak ASP.NET 2 ' den itibaren bu betik [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978)adresinde bulunan ASP.NET Futures 'a taşınmıştır.

Bu betiği yürütmek, IIS ile yeni bir. Mvc uzantısını kaydeder. . Mvc uzantısını kaydettikten sonra, yolların. Mvc uzantısını kullanması için Global. asax dosyasındaki rotalarınızı değiştirebilirsiniz.

Listeleme 2 ' de değiştirilen Global. asax dosyası IIS 'in eski sürümleriyle birlikte çalışmaktadır.

**Listeleme 2-Global. asax (uzantılara göre değiştirilmiş)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample2.cs)]

**Önemli**: Global. asax dosyasını değiştirdikten sonra ASP.NET MVC uygulamanızı derlemeyi unutmayın.

Liste 2 ' deki Global. asax dosyasında iki önemli değişiklik vardır. Artık Global. asax içinde tanımlanmış iki yol vardır. Varsayılan yolun URL 'SI, ilk yol, şu şekilde görünür:

{controller}.mvc/{action}/{id}

. Mvc uzantısının eklenmesi, ASP.NET yönlendirme modülünün kesmesinin aldığı dosya türünü değiştirir. Bu değişiklik ile, ASP.NET MVC uygulaması şu şekilde istekleri yönlendirir:

/Home.mvc/Index/

/Product.mvc/Details/3

/Product.exe Mvc/

İkinci yol, kök yolu yenidir. Kök yolu için bu URL stili boş bir dizedir. Bu yol, uygulamanızın kökünde yapılan eşleşen istekler için gereklidir. Örneğin, kök yolu şuna benzer bir istekle eşleşir:

[http://www.YourApplication.com/](http://www.YourApplication.com/)

Yol tablonuzda bu değişiklikleri yaptıktan sonra, uygulamanızdaki tüm bağlantıların bu yeni URL desenleriyle uyumlu olduğundan emin olmanız gerekir. Diğer bir deyişle, tüm bağlantılarınızın. Mvc uzantısını içerdiğinden emin olun. Bağlantılarınızı oluşturmak için HTML. ActionLink () yardımcı yöntemini kullanırsanız, herhangi bir değişiklik yapmanız gerekmez.

Registermvc. WCF betiğini kullanmak yerine, el ile ASP.NET Framework 'e eşlenmiş bir IIS 'e yeni bir uzantı ekleyebilirsiniz. Yeni bir uzantı eklerken, **dosyayı doğrula** etiketli onay kutusunun işaretli olmadığından emin olun.

## <a name="hosted-server"></a>Barındırılan sunucu

Web sunucunuza her zaman erişemezsiniz. Örneğin, ASP.NET MVC uygulamanızı bir Internet barındırma sağlayıcısı kullanarak barındırıyorsanız, IIS 'ye erişiminizin olması gerekmez.

Bu durumda, ASP.NET çerçevesine eşlenmiş mevcut dosya uzantılarından birini kullanmalısınız. ASP.NET ile eşlenen dosya uzantılarına örnek olarak. aspx,. axd ve. ashx uzantıları verilebilir.

Örneğin, Listeleme 3 ' teki değiştirilen Global. asax dosyası. Mvc uzantısı yerine. aspx uzantısını kullanır.

**Listeleme 3-Global. asax (. aspx uzantıları ile değiştirilmiş)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample3.cs)]

Listeleme 3 ' teki Global. asax dosyası,. Mvc uzantısı yerine. aspx uzantısını kullanması dışında, önceki Global. asax dosyasıyla tamamen aynıdır. . Aspx uzantısını kullanmak için uzak Web sunucunuzda herhangi bir kurulum gerçekleştirmeniz gerekmez.

## <a name="creating-a-wildcard-script-map"></a>Joker karakter betik eşlemesi oluşturma

ASP.NET MVC uygulamanız için URL 'Leri değiştirmek istemiyorsanız ve Web sunucunuza erişiminiz varsa, ek bir seçeneğiniz vardır. Web sunucusuna yapılan tüm istekleri ASP.NET Framework ile eşleyen bir joker karakter betik eşlemesi oluşturabilirsiniz. Bu şekilde, varsayılan ASP.NET MVC yol tablosunu IIS 7,0 (Klasik modda) veya IIS 6,0 ile kullanabilirsiniz.

Bu seçeneğin, IIS 'nin Web sunucusunda yapılan her isteği ele almasına neden olduğunu unutmayın. Bu, görüntülerin, klasik ASP sayfalarının ve HTML sayfalarının isteklerini içerir. Bu nedenle, ASP.NET için joker karakter betik eşlemesinin etkinleştirilmesi performansı etkiler.

IIS 7,0 için bir joker karakter betik haritasını nasıl etkinleştireceğinizi aşağıda bulabilirsiniz:

1. Bağlantılar penceresinde uygulamanızı seçin
2. **Özellikler** görünümünün seçili olduğundan emin olun
3. **Işleyici eşlemeleri** düğmesine çift tıklayın
4. **Joker Karakter Betik Eşlemesi Ekle** bağlantısına tıklayın (bkz. Şekil 3)
5. ASPNET\_ISAPI. dll dosyasının yolunu girin (bu yolu PageHandlerFactory komut dosyası eşlemesinden kopyalayabilirsiniz)
6. MVC adını girin
7. **Tamam** düğmesine tıklayın

[Yeni proje iletişim kutusunu ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.png)

**Şekil 3**: IIS 7,0 ile joker karakter betik haritası oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image6.png))

IIS 6,0 ile bir joker karakter betik eşlemesi oluşturmak için aşağıdaki adımları izleyin:

1. Bir Web sitesine sağ tıklayıp Özellikler ' i seçin
2. **Giriş dizini** sekmesini seçin
3. **Yapılandırma** düğmesine tıklayın
4. **Eşlemeler** sekmesini seçin
5. **Ekle** düğmesine tıklayın (bkz. Şekil 4)
6. ASPNET\_ISAPI. dll ' ye yolu çalıştırılabilir alana yapıştırın (bu yolu. aspx dosyaları için komut dosyası eşlemesinden kopyalayabilirsiniz)
7. **Dosyanın var olduğunu doğrulayın** etiketli onay kutusunun işaretini kaldırın
8. **Tamam** düğmesine tıklayın

[Yeni proje iletişim kutusunu ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image7.png)

**Şekil 4**: IIS 6,0 ile joker karakter betik haritası oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image8.png))

Joker karakter betik eşlemelerini etkinleştirdikten sonra, Global. asax dosyasındaki yol tablosunu bir kök yolu içerecek şekilde değiştirmeniz gerekir. Aksi takdirde, uygulamanızın kök sayfası için bir istek yaptığınızda Şekil 5 ' te hata sayfasını alırsınız. Değiştirilen Global. asax dosyasını liste 4 ' te kullanabilirsiniz.

[Yeni proje iletişim kutusunu ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image9.png)

**Şekil 5**: eksik kök yol hatası ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image10.png))

**Listeleme 4-Global. asax (kök rotayla değiştirilir)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample4.cs)]

IIS 7,0 veya IIS 6,0 için bir joker karakter betik eşlemesini etkinleştirdikten sonra, aşağıdaki gibi görünen varsayılan yol tablosuyla çalışan istekler yapabilirsiniz:

/

/Home/Index

/Product/Details/3

/Ürün

## <a name="summary"></a>Özet

Bu öğreticinin amacı, IIS 'nin daha eski bir sürümünü (veya Klasik modda IIS 7,0) kullanırken ASP.NET MVC 'yi nasıl kullanabileceğinizi açıklamaktır. ASP.NET yönlendirme 'yi IIS 'nin eski sürümleriyle çalışacak şekilde almanın iki yöntemi tartışıyoruz: varsayılan yol tablosunu değiştirme veya joker karakter betik eşlemesi oluşturma.

İlk seçenek, ASP.NET MVC uygulamanızda kullanılan URL 'Leri değiştirmenizi gerektirir. Bu ilk seçenekten çok önemli bir avantajı, yol tablosunu değiştirmek için bir Web sunucusuna erişmeniz gerekmez. Bu, ASP.NET MVC uygulamanızı bir Internet barındırma şirketi ile barındırırken bile bu ilk seçeneği kullanabileceğiniz anlamına gelir.

İkinci seçenek joker karakter betik eşlemesi oluşturmaktır. Bu ikinci seçeneğin avantajı, URL 'lerinizi değiştirmenize gerek kalmaz. Bu ikinci seçeneğin dezavantajı, ASP.NET MVC uygulamanızın performansını etkileyebilir.

> [!div class="step-by-step"]
> [Next](using-asp-net-mvc-with-different-versions-of-iis-vb.md)
