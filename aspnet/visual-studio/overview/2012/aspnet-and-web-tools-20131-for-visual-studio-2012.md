---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: Visual Studio 2012 için ASP.NET and Web Tools 2013,1 sürüm notları | Microsoft Docs
author: microsoft
description: Bu belgede, Visual Studio 2012 için ASP.NET and Web Tools 2013,1 sürümü açıklanmaktadır.
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 260af1018064d60d80cbb1002001f28c4daffffd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578444"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>Visual Studio 2012 için ASP.NET and Web Tools 2013.1 Sürüm Notları

[Microsoft](https://github.com/microsoft) tarafından

> Bu belgede, Visual Studio 2012 için ASP.NET and Web Tools 2013,1 sürümü açıklanmaktadır.

## <a name="contents"></a>İçindekiler

- [Yükleme notları](#install)
- [Yazılım gereksinimleri](#requirements)
- Visual Studio 2012 için ASP.NET and Web Tools 2013,1 ' deki yeni özellikler

    - [Yükleyebilirsiniz](#bootstrap)
    - [Şablonlar](#templates)

        - [ASP.NET MVC 5 şablonu](#mvc5template)
        - [ASP.NET Web API 2 şablonu](#apitemplate)
        - [Öğe şablonları](#itemtemplate)
    - [Entity Framework 6](#ef6)
    - [ASP.NET Scafkatlama](#scaffold)
    - [Razor Düzenleyicisi](#razor)
    - [NuGet 2.7](#nuget)
- Bilinen sorunlar ve son değişiklikler

    - [ASP.NET Scafkatlama](#issuescaffolding)

        - [MVC ve Web API 'SI yapı Iskelesi-HTTP 404, bulunamadı hatası](#404issue)
        - [Web için Visual Studio Express 2012, bir yapı iskelesi eklenen bir öğe eklendikten sonra çalışmayı durduruyor](#expressissue)
    - [ASP.NET Razor 3](#issuerazor)

        - [Cshtml dosyasını ve F5 ile görüntüleme, bir sunucu hatasına neden oluyor](#browseissue)
        - [URL yeniden yazma ve tilde (~)](#rewriteissue)
    - [Şablonlar](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a>Yükleme notları

[Yüklemesi](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) Visual Studio 2012 için ASP.NET and Web Tools 2013,1.

<a id="requirements"></a>
## <a name="software-requirements"></a>Yazılım Gereksinimleri

Web için Visual Studio 2012 veya Visual Studio Express 2012 ' ya sahip olmanız gerekir.

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>Visual Studio 2012 için ASP.NET and Web Tools 2013,1 ' deki yeni özellikler

<a id="bootstrap"></a>
### <a name="bootstrap"></a>Yükleyebilirsiniz

Ffold MVC 5 denetleyicilerini ve görünümlerini yapılandırırken, görünümler için biçimlendirme [önyükleme](http://getbootstrap.com/)kullanır.

<a id="templates"></a>
### <a name="templates"></a>Şablonlar

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a>ASP.NET MVC 5 şablonu

Yeni bir MVC 5 şablonu ekledik. En son MVC 5 NuGet paketlerine başvurur ve yapı ve görünüm eklemek için scafkatlamayı kullanabilirsiniz.

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a>ASP.NET Web API 2 şablonu

Yeni bir Web API 2 şablonu ekledik. En son Web API 2 NuGet paketlerine başvurur ve yapı ve görünüm eklemek için scafkatlamayı kullanabilirsiniz.

<a id="itemtemplate"></a>
#### <a name="item-templates"></a>Öğe şablonları

MVC 5 görünümleri, Web sayfaları (Razor 3) ve Web API 2 denetleyicileri için yeni öğe şablonları ekledik. Yeni öğeler eklenirken ilgili NuGet paketlerini projeye yükler.

<a id="ef6"></a>
### <a name="entity-framework-6"></a>Entity Framework 6

Entity Framework kullanarak bir MVC veya Web API denetleyicisi ile dolandırdığınızda, Framework 6 ' yı kullanırız. Entity Framework hakkında daha fazla bilgi için, [Entity Framework sürüm geçmişine](https://msdn.com/data/jj574253)bakın.

Ayrıca, Visual Studio 2012 için Entity Framework 6 araçlarını indirebilir ve yükleyebilirsiniz. Bkz. [Get Entity Framework](https://msdn.com/data/ee712906#tooling).

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET Scafkatlama

ASP.NET Scafkatlama, ASP.NET Web uygulamaları için bir kod oluşturma çerçevesidir. Projenize bir veri modeliyle etkileşim kuran ortak kod eklemenizi kolaylaştırır.

Visual Studio 'nun önceki sürümlerinde, scafkatlama ASP.NET MVC projeleriyle sınırlandırılmıştır. Bu güncelleştirmeyle, artık Web Forms dahil olmak üzere herhangi bir ASP.NET projesi için scafkatlamayı kullanabilirsiniz. Bu güncelleştirme, bir Web Forms projesi için sayfa oluşturmayı desteklemez, ancak projeye MVC bağımlılıkları ekleyerek Web Forms ile yapı iskelesi kullanmaya devam edebilirsiniz. Web Forms için sayfa oluşturma desteği gelecekteki bir güncelleştirmeye eklenecektir.

Yapı iskelesi kullanılırken, gerekli tüm bağımlılıkların projede yüklü olduğundan emin veriyoruz. Örneğin, bir ASP.NET Web Forms projesiyle başlayıp bir Web API denetleyicisi eklemek için scafkatlamayı kullanıyorsanız, gerekli NuGet paketleri ve başvuruları projenize otomatik olarak eklenir.

Web Forms projesine MVC yapı iskelesi eklemek için **Yeni bir yapı** İskelesi ekleyin ve Iletişim penceresinde **MVC 5 bağımlılıklarını** seçin. Yapı iskelesi MVC için iki seçenek vardır; En az ve tam. En az ' ı seçerseniz, projenize yalnızca NuGet paketleri ve ASP.NET MVC başvuruları eklenir. Tam seçeneğini belirlerseniz, en düşük bağımlılıklar ve bir MVC projesi için gerekli içerik dosyaları eklenir.

Yapı iskelesi zaman uyumsuz denetleyiciler desteği Entity Framework 6 ' dan gelen yeni zaman uyumsuz özellikleri kullanır.

Daha fazla bilgi ve öğretici için bkz. [ASP.net Scafkate genel bakış](../2013/aspnet-scaffolding-overview.md). Bu öğreticiler Visual Studio 2013 ile yapı iskelesi gösterir, ancak Visual Studio 2012 için ASP.NET and Web Tools 2013,1 için de geçerlidir.

<a id="razor"></a>
### <a name="razor-editor"></a>Razor Düzenleyicisi

Visual Studio 2012, bu güncelleştirme ile Razor 3 araç oluşturma/düzenlemesini desteklemektedir.

<a id="nuget"></a>
### <a name="nuget-27"></a>NuGet 2.7

NuGet 2,7, [nuget 2,7 sürüm notlarında](http://docs.nuget.org/docs/release-notes/nuget-2.7)ayrıntılı olarak açıklanan zengin bir dizi yeni özellik içerir.

NuGet 'in bu sürümü, kullanıcıların açıkça NuGet 'in eksik paketleri geri yüklemelerine izin verme gereksinimini ortadan kaldırır. NuGet 2,7 yüklenirken, kullanıcılar eksik paketleri otomatik olarak geri yüklemeye izin vermez. Kullanıcılar, Visual Studio 'daki NuGet ayarları aracılığıyla paket geri yüklemesini açıkça devre dışı bırakabilirsiniz. Bu değişiklik, paket geri yüklemesinin nasıl çalıştığını basitleştirir.

## <a name="known-issues-and-breaking-changes"></a>Bilinen sorunlar ve son değişiklikler

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET Scafkatlama

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC ve Web API 'SI yapı Iskelesi-HTTP 404, bulunamadı hatası

Bir projeye yapı iskelesi eklenen bir öğe eklerken bir hatayla karşılaşırsanız projenizin tutarsız bir durumda bırakılması mümkündür. Yapı iskelesi haline getirilen değişikliklerden bazıları geri alınacaktır, ancak yüklü NuGet paketleri gibi diğer değişiklikler geri alınmaz. Yönlendirme yapılandırması değişiklikleri geri alınırsa, kullanıcılar, yapı iskelesi öğelerinde gezinilirken bir HTTP 404 hatası alırlar.

MVC için bu hatayı onarmak üzere yeni bir yapı iskelesi ekleyin ve MVC 5 bağımlılıklarını (en az ya da tam) seçin. Bu işlem, gerekli tüm değişiklikleri projenize ekleyecek.

Web API 'SI için bu hatayı onarmak için:

1. Aşağıdaki WebApiConfig sınıfını projenize ekleyin.

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. WebApiConfig. Register öğesini Global. asax içindeki Application\_start yönteminde aşağıdaki gibi yapılandırın:

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a>Web için Visual Studio Express 2012, bir yapı iskelesi eklenen bir öğe eklendikten sonra çalışmayı durduruyor

Web için Visual Studio Express 2012 Entity Framework, Entity Framework sahip yapı iskelesi (Eylemler içeren Web API 2 denetleyicisi gibi) eklendikten sonra çalışmayı durduruyor, Visual Studio Express bir derlemenin yerel görüntüsünü yüklemede başarısız olabilir System. Web. Extensions 'a bağımlıdır.

Bu sorunu düzeltmek için Visual Studio Express, System. Web. Extensions MSIL görüntüsüyle çalışacak şekilde yapılandırın:

1. Yönetici modunda komut Istemi ' ni açın.
2. %ProgramFiles%\Microsoft Visual Studio 11.0 \ Common7\ıde veya% ProgramFiles (x86)% \ Microsoft Visual Studio 11.0 \ Common7\ıde (64 bit Windows için) adresine gidin.
3. Bir metin düzenleyicisinde, '. exe. config dosyasını açın.
4. &lt;yapılandırma&gt;/&lt;çalışma zamanı&gt; öğesinin altına aşağıdaki satırı ekleyin:  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. Web için Visual Studio Express 2012 ' i yeniden başlatın.

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a>ASP.NET Razor 3

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a>Cshtml dosyasını ve F5 ile görüntüleme, bir sunucu hatasına neden oluyor

Visual Studio 2012 ' de bir MVC 5 projesi oluşturduğunuzda (veya Visual Studio 2013 içinde oluşturulmuş bir MVC 5 projesinde Visual Studio 2012 ' de açın) ve bir cshtml dosyasını veya F5 'i kullanarak görüntülemeyi denerseniz, **'/' uygulamasında sunucu hatası**olduğunu bildiren bir hata alırsınız. Sunucu `http://localhost:XXXX/Views/../XXXX.cshtml` gitme girişiminde bulunur

Bu sorunu çözmek için, projenizdeki **Başlangıç eylemi** ayarını **belirli bir sayfada**değiştirin. Sayfa için bir değer belirtmeniz gerekmez.

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

Bu değişikliği yaptıktan sonra F5 ' i seçtiğinizde uygulamanızın köküne (`http://localhost:XXXX`) gider. Bu davranış, **geçerli sayfa** ayarının açık sayfayı BAŞLATTıĞıNDA Visual Studio 2013 MVC 5 projelerine yönelik davranışla aynı değildir.

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a>URL yeniden yazma ve tilde (~)

ASP.NET Razor 3 veya ASP.NET MVC 5 sürümüne yükselttikten sonra, URL yeniden yazar kullanıyorsanız, tilde (~) gösterimi artık düzgün çalışmayabilir. URL yeniden yazma, &lt;A/&gt;, &lt;BETIK/&gt;, &lt;LINK/&gt;gibi HTML öğelerinde tilde (~) gösterimini etkiler ve bu nedenle, tilde artık kök dizine eşlememez.

Örneğin, **ASP.net/Content** için istekleri **ASP.net**'e yeniden verirseniz, &lt;A href = "~/content/"/&gt; içindeki href özniteliği **/** yerine **/Content/Content/** olarak çözümlenir. Bu değişikliği engellemek için, **ııs\_** IBU bağlamı her bir Web sayfasında yanlış olarak veya Global. asax dosyasındaki **BeginRequest\_** .

<a id="templateissue"></a>
### <a name="templates"></a>Şablonlar

Windows 8.1 veya Windows Server 2012 R2 üzerinde Visual Studio 2012 ile ASP.NET MVC projeleri oluşturduğunuzda, Visual Studio "ASP.NET 4,5 için Web [URL] yapılandırma başarısız oldu." iletisini bildiren bir hata mesajı görüntüler.

![Yapılandırma hatası](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

Bu hata, Visual Studio 2012, ASP.NET 4,5 özelliğini Windows 'un bu sürümlerinde yüklü olduğunda etkinleştirmediği için görürsünüz. ASP.NET 4,5 ' i etkinleştirmek için [Windows özelliklerini açma veya kapatma](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)bölümünde açıklanan adımları uygulayın.

![Windows özelliklerini aç veya kapat](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

Alternatif olarak, komut satırı aracılığıyla ASP.NET 4,5 'yi etkinleştirebilirsiniz.

1. Yönetici modunda komut Istemi ' ni açın.
2. ASP.NET 4,5 ' i etkinleştirmek için aşağıdaki komutu çalıştırın.  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
