---
uid: web-pages/overview/getting-started/aspnet-web-pages-razor-faq
title: ASP.NET Web Pages (Razor) SSS | Microsoft Docs
author: Rick-Anderson
description: Bu makalede, ASP.NET Web Pages (Razor) ve WebMatrix hakkında sık sorulan bazı sorular listelenmektedir. Öğretici ASP.NET Web sayfalarında kullanılan yazılım sürümleri (R...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: b137bd04-25e1-47cb-9d96-ef2e179ecf1f
msc.legacyurl: /web-pages/overview/getting-started/aspnet-web-pages-razor-faq
msc.type: authoredcontent
ms.openlocfilehash: 6fa1b668e915af856a693e79eafb7180ed504dc2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640933"
---
# <a name="aspnet-web-pages-razor-faq"></a>ASP.NET Web Sayfaları (Razor) SSS

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> > [!NOTE] 
> > WebMatrix artık ASP.NET Web sayfaları için tümleşik bir geliştirme ortamı olarak önerilmez. [Visual Studio](xref:aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio) veya [Visual Studio Code](https://code.visualstudio.com/)kullanın.
>
> Bu makalede, ASP.NET Web Pages (Razor) ve WebMatrix hakkında sık sorulan bazı sorular listelenmektedir.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 3
> - Visual Studio 2013
> - WebMatrix 3
>   
> 
> Bu öğretici Ayrıca ASP.NET Web Pages 2, WebMatrix 2 ve Visual Studio 2012 ile de kullanılabilir.

- [ASP.NET Web sayfaları, ASP.NET Web Forms ve ASP.NET MVC arasındaki fark nedir?](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [Web sayfalarıyla çalışmak için WebMatrix 'e ihtiyacım var mı?](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [Web sayfaları sayfasında ASP.NET Web Forms denetimlerini kullanabilir miyim?](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [WebMatrix kullanmadan bir ASP.NET Web sayfaları sitesini dağıtabilir miyim?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [Oturum açma işlemlerini desteklemek için WebSecurity Yardımcısı 'nı kullanmam gerekir mi?](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [ASP.NET Web sayfaları HTML5 destekliyor mu?](#Does_ASP.NET_Web_Pages_support_HTML5)
- [Web sayfalarıyla JavaScript ve jQuery kullanabilir miyim?](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [Ek Kaynaklar](#AdditionalResources)

Hatalar ve diğer sorunlar hakkında sorularınız için [ASP.NET Web Pages (Razor) sorun giderme kılavuzu](https://go.microsoft.com/fwlink/?LinkId=253001)'na bakın.

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a>ASP.NET Web sayfaları, ASP.NET Web Forms ve ASP.NET MVC arasındaki fark nedir?

Her üçü de dinamik Web uygulamaları oluşturmak için ASP.NET teknolojileridir:

- ASP.NET Web sayfaları, HTML sayfalarına dinamik (sunucu tarafı) kod ve veritabanı erişimi ekleme ve basit ve hafif sözdizimi özelliklerine odaklanır.
- ASP.NET Web Forms, sayfa nesne modeli ve geleneksel pencere türü denetimlerine dayalıdır (düğmeler, listeler, vb.). Web Forms, istemci tabanlı (Windows Forms) geliştirmeyle çalıştıkilerle ilgili tanıdık bir olay tabanlı model kullanır.
- ASP.NET MVC, ASP.NET için Model-View-Controller modelini uygular. Vurgu "kaygıları ayırma" (işleme, veri ve Kullanıcı arabirimi katmanları).

Üç çerçeve de tam olarak desteklenir ve ASP.NET ekibi tarafından geliştirilmeye devam eder. Genel olarak, hangi Framework 'ün kullanılacağı, ASP.NET ile arka plana ve deneyiminize göre değişir.

ASP.NET Web sayfaları, HTML 'yi zaten bilen kişilerin sayfalarına sunucu işlemesi eklemesini kolaylaştırmak için tasarlanmıştır. Öğrenciler, hobler, genel olarak programlama için yeni olan kişiler için iyi bir seçimdir. Ayrıca, non-ASP.NET Web teknolojileriyle karşılaşan geliştiriciler için de iyi bir seçenek olabilir.

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a>Web sayfalarıyla çalışmak için WebMatrix 'e ihtiyacım var mı?

Hayır. WebMatrix artık ASP.NET Web sayfaları için tümleşik bir geliştirme ortamı olarak önerilmez. [Visual Studio](program-asp-net-web-pages-in-visual-studio.md) veya [Visual Studio Code](https://code.visualstudio.com/)kullanın.

Visual Studio veya Visual Studio Code kullanmak istemiyorsanız, [Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)kullanarak bileşen ürünlerini tek tek yükleyebilirsiniz. Aşağıdaki ürünlerin olması gerekir:

- Microsoft .NET Framework 4.5
- ASP.NET MVC 5 (ASP.NET Web Pages çerçevesini de yükletir)
- IIS Express (Web sunucusu)
- Microsoft SQL Server Compact 4,0 (veritabanı)

*. Cshtml* (veya *. vbhtml*) sayfalarını düzenlemek için bir metin düzenleyicisi kullanabilirsiniz.

SQL Server Compact veritabanlarının ( *. sdf* dosyaları) bir araç olmadan yönetilmesi biraz daha zordur. *. Sdf* veritabanlarını yönetmek Için Visual Studio containds araçları. Ayrıca, birçok SQL Server yönetim görevini gerçekleştirmek için kodda SQL komutları da çalıştırabilirsiniz.

*. Cshtml* sayfalarını tümleşik bir geliştirme ORTAMı (IDE) kullanmadan test etmek için bunları canlı bir sunucuya dağıtabilirsiniz. (Bkz. [ASP.NET Web Pages sitesini WebMatrix kullanmadan dağıtabilir miyim?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix))

### <a name="running-iis-express-without-using-an-ide"></a>IDE kullanmadan IIS Express çalıştırma

Bilgisayarınıza bir Web sunucusu olarak IIS Express yüklerseniz, bu sayfaları test etmek için kullanabilirsiniz. Komut satırından IIS Express çalıştırabilir ve bunu belirli bir bağlantı noktası numarasıyla ilişkilendirebilirsiniz. Daha sonra bu bağlantı noktasını tarayıcınızda *. cshtml* dosyalarını istediğinizde belirtirsiniz.

Windows 'ta, yönetici ayrıcalıklarıyla bir komut istemi açın ve *C:\Program Files\ııs Express* ' e geçin. (64 bit sistemler için, *C:\Program Files (x86) \ııS Express* klasörünü kullanın. Ardından, sitenizin gerçek yolunu kullanarak aşağıdaki komutu girin:

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

Daha önce başka bir işlem tarafından ayrılmamış olan herhangi bir bağlantı noktası numarası kullanabilirsiniz. (1024 üzerindeki bağlantı noktası numaraları genellikle ücretsizdir.) `path` değeri için, *. cshtml* dosyalarının olduğu web sitesi klasörünün yolunu kullanın.

Sayfalarınıza sunulacak IIS Express ayarlamak için bu komutu çalıştırdıktan sonra bir tarayıcı açabilir ve bir *. cshtml* dosyasına gidebilirsiniz. Aşağıdaki gibi bir URL kullanın:

`http://localhost:35896/default.cshtml`

Komut satırı seçenekleri IIS Express yardım için komut satırına `iisexpress.exe /?` girin.

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a>Web sayfaları sayfasında ASP.NET Web Forms denetimlerini kullanabilir miyim?

Hayır. [CheckBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox) denetimi, [doğrulama denetimleri](https://msdn.microsoft.com/library/bwd43d0x)ve [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview) denetimi gibi denetimler Web Forms, yalnızca Web Forms sayfalarında ( *. aspx* dosyaları) çalışır. Bu denetimler Web Forms sayfa çerçevesini gerektirir.

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a>WebMatrix kullanmadan bir ASP.NET Web sayfaları sitesini dağıtabilir miyim?

Evet. Web sitesi dosyalarını bir sunucuya el ile kopyalayabilirsiniz (genellikle FTP kullanarak). El ile kopyalama gerçekleştirirseniz, SQL Server Compact (veritabanı) destekleyen dosyaları da kopyalamanız gerekir. Ayrıntılar için bkz. [Web sayfaları uygulamalarını araç olmadan dağıtma](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317)blog girdisi.

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a>Oturum açma işlemlerini desteklemek için WebSecurity Yardımcısı 'nı kullanmam gerekir mi?

Hayır. ASP.NET Web sayfalarının bir parçası olan `SimpleMembership` sağlayıcı bir seçenektir. ASP.NET 'ın parçası olan güvenlik sağlayıcıları (Web Forms ile çalışmak için kullandığınız) de kullanılabilir. Örneğin, ASP.NET Web sayfalarında Forms kimlik doğrulamasını Web Forms ' de olduğu gibi kullanabilirsiniz. Forms kimlik doğrulamasının nasıl kullanılacağına ilişkin bir örnek için, [.NET kullanarak C#ASP.net uygulamanızda Forms tabanlı kimlik doğrulaması](https://support.microsoft.com/kb/301240)uygulama Microsoft desteği makalesine bakın. Basit bir örnek indirmek için, bkz. [ASP.NET Version in "Login &amp; Password](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm).

Windows kimlik doğrulamasını kullanma hakkında daha fazla bilgi için [ASP.NET Web sayfalarında Windows kimlik doğrulaması 'Nı kullanarak](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298)blog gönderisine bakın.

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a>ASP.NET Web sayfaları HTML5 destekliyor mu?

Evet. ASP.NET Web sayfaları ( *. cshtml* veya *. vbhtml* sayfaları) ile oluşturduğunuz sayfalar, sayfa işlenmeden önce sunucu üzerinde çalışan kodu da içeren HTML sayfalarıdır. Kullanıcının tarayıcısı HTML5 'yi desteklediği sürece, bir *. cshtml* veya *. vbhtml* sayfasında HTML5 öğelerini kullanabilirsiniz.

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a>Web sayfalarıyla JavaScript ve jQuery kullanabilir miyim?

Kesinlikle. ASP.NET Web sayfaları ( *. cshtml* veya *. vbhtml* sayfaları) ile oluşturduğunuz sayfalar yalnızca sunucu kodu bulunan HTML sayfalarıdır. Bu nedenle, JavaScript veya jQuery kullanarak normal bir HTML sayfasında yapabileceğiniz her şey, bir *. cshtml* veya *. vbhtml* sayfasında da yapabilirsiniz.

WebMatrix 'teki **Başlatıcı site** şablonu, bir dizi jQuery kitaplığı içerir. Bu şablonu kullanarak bir site oluşturursanız, *betikler* klasörü jQuery Core Library (*jQuery-1.6.2. js)* ve jQuery doğrulaması için kitaplıklar (*jQuery. Validate. js*, vb.) içerir.

ASP.NET Web sayfalarıyla jQuery kullanmanın yollarını gösteren bazı blog gönderileri aşağıda verilmiştir:

- Kchel Appel tarafından [WebMatrix kullanarak ASP.NET Web sayfalarına jQuery Iyliği ekleme](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/)
- [5 dk: WebMatrix + jQuery + jQuery](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/) 'e göre Jonas Eriksson 'e göre jQuery şablonları
- Mike Brind 'e göre [WebMatrix ve jQuery formları](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms)

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

[ASP.NET Web Sayfaları (Razor) Sorun Giderme Kılavuzu](https://go.microsoft.com/fwlink/?LinkId=253001)

ASP.NET Web sitesinde [WebMatrix ve ASP.NET Web Pages Forumu](https://forums.asp.net/1224.aspx/1?WebMatrix)
