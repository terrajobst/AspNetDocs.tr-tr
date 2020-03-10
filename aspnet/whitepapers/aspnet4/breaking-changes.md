---
uid: whitepapers/aspnet4/breaking-changes
title: ASP.NET 4 Son değişiklik | Microsoft Docs
author: rick-anderson
description: Bu belgede, kullanılarak oluşturulan uygulamalar potansiyel olarak etkileyebilecek .NET Framework sürüm 4 sürümü için yapılmış değişiklikler açıklanmaktadır...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: d601c540-f86b-4feb-890c-20c806b3da6c
msc.legacyurl: /whitepapers/aspnet4/breaking-changes
msc.type: content
ms.openlocfilehash: 8ccad3b40a723c92a3164de082e1f94577141008
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78546251"
---
# <a name="aspnet-4-breaking-changes"></a>ASP.NET 4 Sürümündeki Hataya Neden Olan Değişiklikler

> Bu belgede, ASP.NET 4 Beta 1 ve Beta 2 sürümleri de dahil olmak üzere önceki sürümler kullanılarak oluşturulan uygulamaları etkileyebilecek .NET Framework sürüm 4 sürümü için yapılmış değişiklikler açıklanmaktadır.
> 
> [Bu teknik incelemeyi indirin](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_Breaking_Changes.pdf)

<a id="0.1__Toc256768952"></a><a id="0.1__Toc256770056"></a>

## <a name="contents"></a>İçindekiler

[Web. config dosyasındaki ControlRenderingCompatibilityVersion ayarı](#0.1__Toc256770141 "_Toc256770141")  
[Clienentidmode değişiklikleri](#0.1__Toc256770142 "_Toc256770142")  
[HtmlEncode ve UrlEncode artık tek tırnak Işaretlerini kodlayamıyor](#0.1__Toc256770143 "_Toc256770143")  
[ASP.NET Page (. aspx) ayrıştırıcısı daha sıkı](#0.1__Toc256770144 "_Toc256770144")  
[Tarayıcı tanım dosyaları güncelleştirildi](#0.1__Toc256770145 "_Toc256770145")  
[System. Web. Mobile. dll kök Web yapılandırma dosyasından kaldırıldı](#0.1__Toc256770146 "_Toc256770146")  
[ASP.NET Istek doğrulaması](#0.1__Toc256770147 "_Toc256770147")  
[Varsayılan karma algoritması artık HMACSHA256](#0.1__Toc256770148 "_Toc256770148")  
[Yeni ASP.NET 4 kök yapılandırmasıyla Ilgili yapılandırma hataları](#0.1__Toc256770149 "_Toc256770149")  
[ASP.NET 4 alt uygulamaları ASP.NET 2,0 veya ASP.NET 3,5 uygulamaları altındayken başlatılamaz](#0.1__Toc256770150 "_Toc256770150")  
[ASP.NET 4 Web siteleri, SharePoint 'In yüklü olduğu bilgisayarlarda başlatılamaz](#0.1__Toc256770151 "_Toc256770151")  
[HttpRequest. FilePath özelliği artık PathInfo değerleri Içermiyor](#0.1__Toc256770152 "_Toc256770152")  
[ASP.NET 2,0 uygulamaları eurl. axd öğesine başvuran HttpException hataları oluşturabilir](#0.1__Toc256770153 "_Toc256770153")  
[Olay Işleyicileri, IIS 7 veya IIS 7,5 tümleşik modundaki bir varsayılan belgede Çıkarılmayabilir](#0.1__Toc256770154 "_Toc256770154")  
[ASP.NET kod erişim güvenliği (CAS) uygulamasında yapılan değişiklikler](#0.1__Toc256770155 "_Toc256770155")  
[System. Web. Security ad alanındaki MembershipUser ve diğer türler taşınmıştır](#0.1__Toc256770156 "_Toc256770156")  
[\* HTTP üst bilgisinde değişiklik yapmak için çıktıyı önbelleğe alma değişiklikleri](#0.1__Toc256770157 "_Toc256770157")  
[Passport için System. Web. Security türleri artık kullanılmıyor](#0.1__Toc256770158 "_Toc256770158")  
[MenuItem. PopOutImageUrl özelliği, ASP.NET 4 ' te bir görüntüyü Işlemek için başarısız oluyor](#0.1__Toc256770159 "_Toc256770159")  
[Menu. StaticPopOutImageUrl ve Menu. DynamicPopOutImageUrl, yollar ters eğik çizgi Içerdiğinde görüntü Işleme başarısız olur](#0.1__Toc256770160 "_Toc256770160")  
[Sorumluluk reddi](#0.1__Toc256770161 "_Toc256770161")

<a id="0.1__ControlRenderingCompatibilityVersio"></a><a id="0.1__Toc245724853"></a><a id="0.1__Toc255587630"></a><a id="0.1__Toc256770141"></a>

## <a name="controlrenderingcompatibilityversion-setting-in-the-webconfig-file"></a>Web. config dosyasındaki ControlRenderingCompatibilityVersion ayarı

ASP.NET denetimleri, nasıl biçimlendirme oluşturdukları hakkında daha kesin bir şekilde belirtmenizi sağlamak için .NET Framework sürüm 4 ' te değiştirilmiştir. .NET Framework önceki sürümlerinde, bazı denetimler devre dışı bırakmak için herhangi bir yol bulunmayan biçimlendirme olarak yayınlanır. Varsayılan olarak, ASP.NET 4 Bu biçimlendirme türü artık oluşturulmaz.

Uygulamanızı ASP.NET 2,0 veya ASP.NET 3,5 sürümüne yükseltmek için Visual Studio 2010 kullanıyorsanız, araç, eski işlemeyi koruyan `Web.config` dosyasına otomatik olarak bir ayar ekler. Ancak, IIS 'deki uygulama havuzunu .NET Framework 4 ' ü hedefleyecek şekilde değiştirerek bir uygulamayı yükseltirseniz, ASP.NET varsayılan olarak yeni işleme modunu kullanır. Yeni işleme modunu devre dışı bırakmak için `Web.config` dosyasına aşağıdaki ayarı ekleyin:

[!code-xml[Main](breaking-changes/samples/sample1.xml)]

Yeni davranışın getirdiği ana işleme değişiklikleri aşağıdaki gibidir:

- **Image** ve **ımagebutton** denetimleri artık `border="0"` özniteliği işlemez.
- **Temel Doğrulayıcı** sınıfı ve bundan türetilen doğrulama denetimleri artık varsayılan olarak kırmızı metin işlemez.
- **HtmlForm** denetimi bir **ad** özniteliği işlemez.
- **Tablo** denetimi artık `border="0"` özniteliği içermiyor.
- Kullanıcı girişi için tasarlanmamış denetimler (örneğin, **etiket** denetimi), **etkin** özelliği **false** olarak ayarlandıysa (veya bu ayarı bir kapsayıcı denetiminden kalıtımla alıyorsa) artık `disabled="disabled"` özniteliğini işlemez.

<a id="0.1__Toc245724854"></a><a id="0.1__Toc255587631"></a><a id="0.1__Toc256770142"></a>

## <a name="clientidmode-changes"></a>Clienentidmode değişiklikleri

ASP.NET 4 ' teki **Clienentidmode** ayarı, ASP.net 'ın HTML öğeleri için **ID** özniteliğini nasıl üretmenizi belirlemenizi sağlar. Önceki ASP.NET sürümlerinde, varsayılan davranış **Clienentidmode**öğesinin **Oto ID** ayarına eşdeğerdir. Ancak, varsayılan ayar artık **tahmin edilebilir**.

Uygulamanızı ASP.NET 2,0 veya ASP.NET 3,5 sürümüne yükseltmek için Visual Studio 2010 kullanıyorsanız, araç otomatik olarak .NET Framework önceki sürümlerinin davranışını koruyan `Web.config` dosyasına bir ayar ekler. Ancak, IIS 'deki uygulama havuzunu .NET Framework 4 ' ü hedefleyecek şekilde değiştirerek bir uygulamayı yükseltirseniz, ASP.NET varsayılan olarak yeni modu kullanır. Yeni istemci KIMLIĞI modunu devre dışı bırakmak için `Web.config` dosyasına aşağıdaki ayarı ekleyin:

[!code-xml[Main](breaking-changes/samples/sample2.xml)]

<a id="0.1__Toc245724855"></a><a id="0.1__Toc255587632"></a><a id="0.1__Toc256770143"></a>

## <a name="htmlencode-and-urlencode-now-encode-single-quotation-marks"></a>HtmlEncode ve UrlEncode artık tek tırnak Işaretlerini kodlayamıyor

ASP.NET 4 ' te, **HttpUtility** ve **HttpServerUtility** sınıflarının **HtmlEncode** ve **urlencode** yöntemleri, tek tırnak işareti karakteri (') şu şekilde kodlamak üzere güncelleştirilmiştir:

- **HtmlEncode** yöntemi tek tırnak işaretinin örneklerini ' olarak kodlar.
- **Urlencode** yöntemi tek tırnak işaretinin örneklerini %27 olarak kodlar.

<a id="0.1__Toc255587633"></a><a id="0.1__Toc256770144"></a><a id="0.1__Toc245724856"></a>

## <a name="aspnet-page-aspx-parser-is-stricter"></a>ASP.NET Page (. aspx) ayrıştırıcısı daha sıkı

ASP.NET Pages (`.aspx` Files) ve Kullanıcı denetimleri (`.ascx` dosyaları) için sayfa ayrıştırıcısı, ASP.NET 4 ' te daha sıkı ve geçersiz biçimlendirmenin daha fazla örneğini reddeder. Örneğin, aşağıdaki iki kod parçacığı ASP.NET 'in önceki sürümlerinde başarıyla ayrıştırılabilir, ancak şimdi ASP.NET 4 ' te Ayrıştırıcı hataları oluşturacak.

[!code-aspx[Main](breaking-changes/samples/sample3.aspx)]

**HiddenField** etiketinin sonunda geçersiz noktalı virgülden dikkat edin.

[!code-aspx[Main](breaking-changes/samples/sample4.aspx)]

**CssClass** özniteliğinde çalışan kapatılmamış **Stil** özniteliğine dikkat edin.

<a id="0.1__Toc255587634"></a><a id="0.1__Toc256770145"></a>

## <a name="browser-definition-files-updated"></a>Tarayıcı tanım dosyaları güncelleştirildi

Tarayıcı tanım dosyaları, yeni ve güncelleştirilmiş tarayıcı ve cihazlarla ilgili bilgileri içerecek şekilde güncelleştirilmiştir. Netscape Navigator gibi eski tarayıcılar ve cihazlar kaldırılmıştır ve Google Chrome ve Apple iPhone gibi yeni tarayıcılar ve cihazlar eklenmiştir.

Uygulamanız kaldırılmış tarayıcı tanımlarından birinden kalıtımla alan özel tarayıcı tanımları içeriyorsa, bir hata görürsünüz. Örneğin, `App_Browsers` klasörü IE2 tarayıcı tanımından devralan bir tarayıcı tanımı içeriyorsa, aşağıdaki yapılandırma hata iletisini alırsınız:

- ' IE2 ' KIMLIKLI tarayıcı veya ağ geçidi öğesi bulunamıyor.

> [!NOTE]
> **HttpBrowserCapabilities** nesnesi (sayfa **isteği. Browser** özelliği tarafından gösterilir) tarayıcı tanımları dosyaları tarafından çalıştırılır. Bu nedenle, ASP.NET 4 ' te bu nesnenin bir özelliğine erişerek döndürülen bilgiler, ASP.NET 'in önceki bir sürümünde döndürülen bilgilerden farklı olabilir.

Tarayıcı tanımı dosyalarını aşağıdaki klasörden kopyalayarak eski tarayıcı tanımı dosyalarına döndürebilirsiniz:

[!code-console[Main](breaking-changes/samples/sample5.cmd)]

Dosyaları ASP.NET 4 için karşılık gelen `\CONFIG\Browsers` klasörüne kopyalayın. Dosyaları kopyaladıktan sonra, ASPNET\_regbrowsers. exe komut satırı aracını çalıştırın.

<a id="0.1__Toc255587635"></a><a id="0.1__Toc256770146"></a>

## <a name="systemwebmobiledll-removed-from-root-web-configuration-file"></a>System. Web. Mobile. dll kök Web yapılandırma dosyasından kaldırıldı

Önceki ASP.NET sürümlerinde System. Web. Mobile. dll derlemesine bir başvuru, altındaki **derlemeler** bölümündeki kök `Web.config` dosyasına eklenmiştir. Performansı artırmak için bu derlemeye başvuru kaldırılmıştır.

System. Web. Mobile. dll derlemesi ASP.NET 4 ' te bulunur, ancak kullanım dışıdır. System. Web. Mobile. dll derlemesinden türler kullanmak istiyorsanız, bu derlemeye kök `Web.config` dosyasına veya bir uygulama `Web.config` dosyasına bir başvuru ekleyin. Örneğin, (kullanım dışı) ASP.NET mobil denetimlerinden birini kullanmak istiyorsanız, System. Web. Mobile. dll derlemesine `Web.config` dosyasına bir başvuru eklemeniz gerekir.

<a id="0.1__Toc245724857"></a><a id="0.1__Toc255587636"></a><a id="0.1__Toc256770147"></a>

## <a name="aspnet-request-validation"></a>ASP.NET Istek doğrulaması

ASP.NET ' deki istek doğrulama özelliği, siteler arası komut dosyası (XSS) saldırılarına karşı belirli bir varsayılan koruma düzeyi sağlar. Önceki ASP.NET sürümlerinde, istek doğrulaması varsayılan olarak etkinleştirilmiştir. Ancak, yalnızca ASP.NET sayfaları (`.aspx` dosyaları ve bunların sınıf dosyaları) ve yalnızca bu sayfalar yürütüldüğü zaman uygulanır.

ASP.NET 4 ' te, varsayılan olarak, HTTP isteğinin **BeginRequest** aşamasından önce etkinleştirildiğinden, tüm istekler için istek doğrulaması etkinleştirilir. Sonuç olarak, yalnızca. aspx sayfa istekleri değil, tüm ASP.NET kaynakları için istek doğrulaması geçerlidir. Bu, Web hizmeti çağrıları ve özel HTTP işleyicileri gibi istekleri içerir. Özel HTTP modülleri bir HTTP isteğinin içeriğini okurken de istek doğrulaması da etkindir.

Sonuç olarak, daha önce hata tetiklemeyen isteklerde istek doğrulama hataları oluşabilir. ASP.NET 2,0 istek doğrulama özelliğinin davranışına dönmek için `Web.config` dosyasına aşağıdaki ayarı ekleyin:

[!code-xml[Main](breaking-changes/samples/sample6.xml)]

Ancak, mevcut işleyiciler, modüller veya diğer özel kodun, XSS saldırı vektörü olabilecek güvenli olmayan HTTP girdilerine erişip erişemeyeceğini belirlemek için istek doğrulama hatalarını analiz etmenizi öneririz.

<a id="0.1__Toc245724858"></a><a id="0.1__Toc255587637"></a><a id="0.1__Toc256770148"></a>

## <a name="default-hashing-algorithm-is-now-hmacsha256"></a>Varsayılan karma algoritması artık HMACSHA256

ASP.NET, form kimlik doğrulaması tanımlama bilgileri ve Görünüm durumu gibi verilerin güvenliğini sağlamaya yardımcı olmak için hem şifreleme hem de karma algoritmaları kullanır Varsayılan olarak, ASP.NET 4, artık tanımlama bilgileri ve görünüm durumundaki karma işlemleri için HMACSHA256 algoritmasını kullanır. Önceki ASP.NET sürümleri eski HMACSHA1 algoritmasını kullandı.

Forms kimlik doğrulama tanımlama bilgileri gibi verilerin across.NET Framework sürümlerini çalışması gereken karma ASP.NET 2.0/ASP. NET 4 ortamları çalıştırırsanız uygulamalarınız etkilenebilir. ASP.NET 4 Web uygulamasını eski HMACSHA1 algoritmasını kullanacak şekilde yapılandırmak için `Web.config` dosyasına aşağıdaki ayarı ekleyin:

[!code-xml[Main](breaking-changes/samples/sample7.xml)]

<a id="0.1__Toc245724859"></a><a id="0.1__Toc255587638"></a><a id="0.1__Toc256770149"></a>

## <a name="configuration-errors-related-to-new-aspnet-4-root-configuration"></a>Yeni ASP.NET 4 kök yapılandırmasıyla Ilgili yapılandırma hataları

.NET Framework 4 (ve bu nedenle ASP.NET 4) için kök yapılandırma dosyaları (`machine.config` dosyası ve kök `Web.config` dosyası), uygulama `Web.config` dosyalarında ASP.NET 3,5 ' de bulunan ortak yapılandırma bilgilerinin çoğunu içerecek şekilde güncelleştirilmiştir. Yönetilen IIS 7 ve IIS 7,5 yapılandırma sistemlerinin karmaşıklığı nedeniyle, ASP.NET 4 ve IIS 7 ve IIS 7,5 altında ASP.NET 3,5 uygulamalarını çalıştırmak ASP.NET veya IIS yapılandırma hatalarına neden olabilir.

Pratik ise, Visual Studio 2010 ' de proje yükseltme araçlarını kullanarak ASP.NET 3,5 uygulamalarını ASP.NET 4 ' e yükseltmenizi öneririz. Visual Studio 2010, ASP.NET 4 için uygun ayarları içerecek şekilde ASP.NET 3,5 uygulamasının `Web.config` dosyasını otomatik olarak değiştirir.

Ancak, yeniden derleme olmadan .NET Framework 4 ' ü kullanarak ASP.NET 3,5 uygulamalarını çalıştırmak için desteklenen bir senaryodur. Bu durumda, uygulamayı .NET Framework 4 ve IIS 7 veya IIS 7,5 altında çalıştırmadan önce uygulamanın `Web.config` dosyasını el ile değiştirmeniz gerekebilir.

Sonraki iki bölümde, farklı yazılım birleşimleri için yapmanız gerekebilecek değişiklikler açıklanır.

**Windows Vista SP1 veya Windows Server 2008 SP1, burada düzeltme KB958854 veya SP2 yüklü değil.** Bu yapılandırmada, IIS 7 yapılandırma sistemi uygulama düzeyi `Web.config` dosyasını ASP.NET 2,0 `machine.config` dosyalarla karşılaştırarak uygulamanın yönetilen yapılandırmasını yanlış bir şekilde birleştirir. Bu nedenle, uygulama düzeyi `Web.config` .NET Framework 3,5 veya sonraki bir sürümde, IIS 7 doğrulama hatasına neden olmak için bir **System. Web. Extensions** yapılandırma bölümü tanımına (öğesi) sahip olmalıdır.

Ancak, Visual Studio 2008 ile tanıtılan özgün ortak yapılandırma bölüm tanımlarıyla tam olarak eşleşmeyen uygulama düzeyi `Web.config` dosya girdileri, ASP.NET yapılandırma hatalarına neden olur. (Visual Studio 2008 tarafından oluşturulan varsayılan yapılandırma girdileri doğru şekilde çalışır.) Yaygın bir sorun, el ile değiştirilen `Web.config` dosyaları, çeşitli yapılandırma bölümü tanımlarında bulunan **allowDefinition** ve **RequirePermission** yapılandırma özniteliklerini bırakmıştır. Bu, uygulama düzeyindeki `Web.config` dosyalardaki kısaltılmış yapılandırma bölümü ve ASP.NET 4 `machine.config` dosyasındaki tam tanım arasında uyuşmazlık oluşmasına neden olur. Sonuç olarak, çalışma zamanında ASP.NET 4 yapılandırma sistemi bir yapılandırma hatası oluşturur.

**Windows Vista SP2, Windows Server 2008 SP2, Windows 7, Windows Server 2008 R2 ve ayrıca düzeltme KB958854 yüklü olan Windows Vista SP1 ve Windows Server 2008 SP1.**

Bu senaryoda, IIS 7 ve IIS 7,5 yerel yapılandırma sistemi, yönetilen yapılandırma bölümü işleyicisi için tanımlanan **tür** özniteliğinde bir metin karşılaştırması gerçekleştirdiğinden bir yapılandırma hatası döndürüyor. Visual Studio 2008 ve Visual Studio 2008 SP1 tarafından oluşturulan tüm `Web.config` dosyalarının, sistem için tür dizesinde "3,5" olduğundan emin olmanız gerekir **. Web. Extensions** (ve ilgili) yapılandırma bölümü işleyicileri ve ASP.NET 4 `machine.config` dosyası aynı yapılandırma bölümü işleyicilerinin **tür** özniteliğinde "4,0" sahip olduğundan, Visual Studio 2008 veya Visual Studio 2008 SP1 'de oluşturulan uygulamalar her zaman ııs 7 ve IIS 7,5 içinde yapılandırma doğrulamasında başarısız olur.

<a id="0.1__Toc251910248"></a>

### <a name="resolving-these-issues"></a>Bu sorunları çözme

İlk senaryonun geçici çözümü, Visual Studio 2008 tarafından otomatik olarak oluşturulan bir `Web.config` dosyasından ortak yapılandırma metnini ekleyerek uygulama düzeyi `Web.config` dosyasını güncelleştirmedir.

İlk senaryoya alternatif bir geçici çözüm olarak, bilgisayarınıza Vista veya Windows Server 2008 için Service Pack 2 veya IIS yapılandırma sisteminin yanlış yapılandırma birleştirme davranışını giderecek düzeltme KB958854 ([https://support.microsoft.com/kb/958854](https://support.microsoft.com/kb/958854)) yüklenir. Ancak, bu eylemlerden birini gerçekleştirdikten sonra uygulamanız, İkinci senaryo için açıklanan sorun nedeniyle bir yapılandırma hatasıyla karşılaşacaktır.

İkinci senaryoya geçici çözüm olarak, uygulama düzeyi `Web.config` dosyasından tüm **System. Web. Extensions** yapılandırma bölümü tanımlarını ve yapılandırma bölümü grubu tanımlarını silmek veya buradan açıklama eklemek. Bu tanımlar genellikle uygulama düzeyi `Web.config` dosyasının en üstünde yer alabilir ve **configSections** öğesi ve alt öğeleri tarafından tanımlanabilir.

Her iki senaryo için de **System. CodeDom** bölümünü el ile silmeniz önerilir, ancak bu gerekli değildir.

<a id="0.1__Toc252995490"></a><a id="0.1__Toc255587639"></a><a id="0.1__Toc256770150"></a><a id="0.1__Toc245724860"></a>

## <a name="aspnet-4-child-applications-fail-to-start-when-under-aspnet-20-or-aspnet-35-applications"></a>ASP.NET 4 alt uygulamaları ASP.NET 2,0 veya ASP.NET 3,5 uygulamaları altındayken başlatılamaz

ASP.NET 'ın önceki sürümlerini çalıştıran uygulamaların alt öğeleri olarak yapılandırılan ASP.NET 4 uygulamaları yapılandırma veya derleme hataları nedeniyle başlayamayabilir. Aşağıdaki örnekte, etkilenen bir uygulama için bir dizin yapısı gösterilmektedir.

`/parentwebapp` (ASP.NET 2,0 veya ASP.NET 3,5 kullanacak şekilde yapılandırıldı)  
`/childwebapp` (ASP.NET 4 kullanacak şekilde yapılandırıldı)

`childwebapp` klasöründeki uygulama, IIS 7 veya IIS 7,5 ' de başlayamaz ve bir yapılandırma hatası rapor eder. Hata metni aşağıdakine benzer bir ileti içerecektir:

- `The requested page cannot be accessed because the related configuration data for the page is invalid.`

- `The configuration section 'configSections' cannot be read because it is missing a section declaration.`

IIS 6 ' da, `childwebapp` klasöründeki uygulama da başlayamaz, ancak farklı bir hata raporlacaktır. Örneğin, hata metni şunları verebilir:

- `The value for the 'compilerVersion' attribute in the provider options must be 'v4.0' or later if you are compiling for version 4.0 or later of the .NET Framework. To compile this Web application for version 3.5 or earlier of the .NET Framework, remove the 'targetFramework' attribute from the element of the Web.config file`

Bu senaryolar, `parentwebapp` klasöründeki üst uygulamadaki yapılandırma bilgileri `childwebapp` klasöründe alt Web uygulaması tarafından kullanılan son birleştirilmiş yapılandırma ayarlarını belirleyen yapılandırma bilgileri hiyerarşisinin bir parçası olduğundan oluşur. ASP.NET 4 Web uygulamasının IIS 7 ' de (veya IIS 7,5) veya IIS 6 ' da çalışıp çalışmadığını bağlı olarak, IIS yapılandırma sistemi veya ASP.NET 4 derleme sistemi bir hata döndürür.

Bu sorunu gidermek ve alt ASP.NET 4 uygulamasının çalışmasını sağlamak için izlemeniz gereken adımlar, ASP.NET 4 uygulamasının IIS 6 ' da veya IIS 7 ' de (veya IIS 7,5) çalışmasına bağlı olarak değişir.

### <a name="step-1-iis-7-or-iis-75-only"></a>1\. adım (yalnızca IIS 7 veya IIS 7,5)

Bu adım yalnızca, Windows Vista, Windows Server 2008, Windows 7 ve Windows Server 2008 R2 içeren IIS 7 veya IIS 7,5 çalıştıran işletim sistemlerinde gereklidir.

Üst uygulamanın `Web.config` dosyasına (ASP.NET 2,0 veya ASP.NET 3,5 çalıştıran uygulama) the.NET Framework 2,0 için kök `Web.config` dosyasında, **configSections** tanımını taşıyın. IIS 7 ve IIS 7,5 yerel yapılandırma sistemi, yapılandırma dosyalarının hiyerarşisini birleşdiğinde **configSections** öğesini tarar. **ConfigSections** tanımını üst Web uygulamasının `Web.config` dosyasından kök `Web.config` dosyasına taşımak, öğeyi alt ASP.NET 4 uygulaması için oluşan yapılandırma birleştirme işleminden etkin bir şekilde gizler.

32 bit işletim sisteminde veya 32 bit uygulama havuzları için, ASP.NET 2,0 ve ASP.NET 3,5 için kök `Web.config` dosyası normalde aşağıdaki klasörde bulunur:

`C:\Windows\Microsoft.NET\Framework\v2.0.50727\CONFIG`

64 bit işletim sisteminde veya 64 bit uygulama havuzları için, ASP.NET 2,0 ve ASP.NET 3,5 için kök `Web.config` dosyası normalde aşağıdaki klasörde bulunur:

`C:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG`

Her iki 32 bit ve 64 bit Web uygulamasını bir 64-bit bilgisayarda çalıştırırsanız, hem 32 hem de 64-bit sistemler için **configSections** öğesini kök `Web.config` dosyalarına taşımanız gerekir.

**ConfigSections** öğesini kök `Web.config` dosyasına yerleştirdiğinizde, bölümü **yapılandırma** öğesinden hemen sonra yapıştırın. Aşağıdaki örnek, öğeleri taşımayı bitirdiğinizde kök `Web.config` dosyasının en üst kısmının nasıl göründüğünü gösterir.

> [!NOTE]
> Aşağıdaki örnekte, satırlar okunabilirlik için sarmalanmış.

[!code-xml[Main](breaking-changes/samples/sample8.xml)]

### <a name="step-2-all-versions-of-iis"></a>2\. adım (IIS 'nin tüm sürümleri)

Bu adım, ASP.NET 4 alt Web uygulamasının IIS 6 ' da veya IIS 7 ' de (veya IIS 7,5) çalışıp çalışmadığını gerektirir.

ASP.NET 2 veya ASP.NET 3,5 çalıştıran üst Web uygulamasının `Web.config` dosyasında, yapılandırma girdilerinin yalnızca üst Web uygulamasına uygulanacağını açıkça belirten bir **konum** etiketi ekleyın (ııs ve ASP.NET yapılandırma sistemleri için). Aşağıdaki örnek, eklenecek **konum** öğesinin söz dizimini gösterir:

[!code-xml[Main](breaking-changes/samples/sample9.xml)]

Aşağıdaki örnek, **appSettings** bölümü ile başlayan ve **System. webserver** bölümüyle biten tüm yapılandırma bölümlerini kaydırmak için **Location** etiketinin nasıl kullanıldığını gösterir.

[!code-xml[Main](breaking-changes/samples/sample10.xml)]

1 ve 2. adımları tamamladığınızda, alt ASP.NET 4 Web uygulamaları hatasız başlayacaktır.

<a id="0.1__Toc252995491"></a><a id="0.1__Toc255587640"></a><a id="0.1__Toc256770151"></a>

## <a name="aspnet-4-web-sites-fail-to-start-on-computers-where-sharepoint-is-installed"></a>ASP.NET 4 Web siteleri, SharePoint 'In yüklü olduğu bilgisayarlarda başlatılamaz

SharePoint çalıştıran Web sunucularının bir SharePoint Web sitesinin kökünde dağıtılan bir `Web.config` dosyası (örneğin, varsayılan Web sitesi için `c:\inetpub\wwwroot\web.config`) vardır. Bu `Web.config` dosyasında, SharePoint WSS\_minimal adlı özel kısmi güven düzeyini ayarlar.

Bu SharePoint Web sitesi türünün bir alt öğesi olarak dağıtılan bir ASP.NET 4 Web sitesi çalıştırmayı denerseniz, aşağıdaki hatayı görürsünüz:

`Could not find permission set named 'ASP.NET'.`

Bu hata, ASP.NET 4 kod erişim güvenliği (CAS) altyapısının ASP.NET adında bir izin kümesi aradığı için oluşur. Ancak, WSS\_en düşük tarafından başvurulan kısmi güven yapılandırma dosyası, bu ada sahip herhangi bir izin kümesi içermez.

Şu anda, ASP.NET ile uyumlu bir SharePoint sürümü mevcut değil. Sonuç olarak, ASP.NET 4 Web sitesini SharePoint Web siteleri altında bir alt site olarak çalıştırmayı denememelisiniz.

<a id="0.1__Toc255587641"></a><a id="0.1__Toc256770152"></a>

## <a name="the-httprequestfilepath-property-no-longer-includes-pathinfo-values"></a>HttpRequest. FilePath özelliği artık PathInfo değerleri Içermiyor

Önceki ASP.NET sürümleri, **HttpRequest. FilePath**, **HttpRequest. AppRelativeCurrentExecutionFilePath**ve **HttpRequest. CurrentExecutionFilePath**dahil olmak üzere çeşitli dosya yolundan Ilgili özelliklerden döndürülen değerde bir **PathInfo** değeri içeriyordu. ASP.NET 4 artık bu özelliklerden dönüş değerlerinde **PathInfo** değeri içermiyor. Bunun yerine, **PathInfo** bilgileri **HttpRequest. PathInfo**içinde kullanılabilir. Örneğin, aşağıdaki URL parçasını düşünün:

`/testapp/Action.mvc/SomeAction`

Önceki ASP.NET sürümlerinde, **HttpRequest** özellikleri aşağıdaki değerlere sahiptir:

**HttpRequest. FilePath**: `/testapp/Action.mvc/SomeAction`

**HttpRequest. PathInfo**: (boş)

ASP.NET 4 ' te, yerine **HttpRequest** özellikleri aşağıdaki değerlere sahiptir:

**HttpRequest. FilePath**: `/testapp/Action.mvc`

**HttpRequest. PathInfo**: `SomeAction`

<a id="0.1__Toc252995493"></a><a id="0.1__Toc255587642"></a><a id="0.1__Toc256770153"></a><a id="0.1__Toc245724861"></a>

## <a name="aspnet-20-applications-might-generate-httpexception-errors-that-reference-eurlaxd"></a>ASP.NET 2,0 uygulamaları eurl. axd öğesine başvuran HttpException hataları oluşturabilir

ASP.NET 4 IIS 6 ' da etkinleştirildikten sonra, IIS 6 ' da (Windows Server 2003 veya Windows Server 2003 R2 'de) çalışan ASP.NET 2,0 uygulamaları aşağıdakiler gibi hatalar oluşturabilir:

`System.Web.HttpException: Path '/[yourApplicationRoot]/eurl.axd/[Value]' was not found.`

Bu hata, ASP.net bir Web sitesinin ASP.NET 4 kullanacak şekilde yapılandırıldığını algıladığında, ASP.NET 4 ' ün yerel bir bileşeni, daha fazla işleme için ASP.net 'in yönetilen bölümüne uzantısız eşle URL 'yi geçirdiğinde oluşur. Ancak, bir ASP.NET 4 Web sitesinin altındaki sanal dizinler ASP.NET 2,0 kullanacak şekilde yapılandırıldıysa, uzantısız eşle URL 'yi bu şekilde işlemek, "eurl. axd" dizesini içeren değiştirilmiş bir URL 'ye neden olur. Bu değiştirilen URL daha sonra ASP.NET 2,0 uygulamasına gönderilir. ASP.NET 2,0, "eurl. axd" biçimini tanımıyor. Bu nedenle, ASP.NET 2,0 `eurl.axd` adlı bir dosya bulmaya çalışır ve bunu yürütür. Böyle bir dosya mevcut olmadığından, istek **HttpException** özel durumuyla başarısız olur.

Aşağıdaki seçeneklerden birini kullanarak bu soruna geçici bir çözüm bulabilirsiniz.

### <a name="option-1"></a>seçenek 1

Web sitesini çalıştırmak için ASP.NET 4 gerekli değilse, site yerine ASP.NET 2,0 kullanacak şekilde yeniden eşleyin.

### <a name="option-2"></a>Seçenek 2

Web sitesini çalıştırmak için ASP.NET 4 gerekliyse, herhangi bir alt ASP.NET 2,0 sanal dizinini ASP.NET 2,0 ile eşlenmiş farklı bir Web sitesine taşıyın.

### <a name="option-3"></a>Seçenek 3

Web sitesini ASP.NET 2,0 olarak yeniden eşlemek veya bir sanal dizinin konumunu değiştirmek pratik değilse, ASP.NET 4 ' te uzantısız eşle URL işlemeyi açıkça devre dışı bırakın. Aşağıdaki yordamı kullanın:

1. Windows kayıt defteri 'nde aşağıdaki düğümü açın:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ASP.NET\4.0.30319.0`

1. **Enableextensionlessurls**adlı yeni bir **DWORD** değeri oluşturun.
2. **Enableextensionlessurls** değerini 0 olarak ayarlayın. Bu, uzantısız URL davranışını devre dışı bırakır.
3. Kayıt defteri değerini kaydedin ve kayıt defteri düzenleyicisini kapatın.
4. IIS 'nin yeni kayıt defteri değerini okumasına neden olan **IISReset** komut satırı aracını çalıştırın.

> [!NOTE]
> **Enableextensionlessurls** 1 olarak ayarlandığında uzantısız eşle URL davranışı etkinleştirilir. Hiçbir değer belirtilmemişse bu varsayılan ayardır.

<a id="0.1__Toc252995494"></a><a id="0.1__Toc255587643"></a><a id="0.1__Toc256770154"></a><a id="0.1__Toc245724862"></a>

## <a name="event-handlers-might-not-be-not-raised-in-a-default-document-in-iis-7-or-iis-75-integrated-mode"></a>Olay Işleyicileri, IIS 7 veya IIS 7,5 tümleşik modundaki bir varsayılan belgede Çıkarılmayabilir

ASP.NET 4 ' te, bir uzantısız URL varsayılan bir belgeye çözümlenirse HTML **form** öğesinin **Action** özniteliğinin nasıl işlendiğine ilişkin değişiklikler bulunur. Varsayılan bir belgeyi çözümlemek için bir uzantısız eşle URL 'si örneği, [http://contoso.com/Default.aspx](http://contoso.com/Default.aspx)bir istek sonucu [http://contoso.com/](http://contoso.com/)olacaktır.

ASP.NET 4, varsayılan bir belgeye eşlenmiş bir uzantısız URL 'ye istek yapıldığında, artık HTML **form** öğesinin **Action** öznitelik değerini boş bir dize olarak oluşturur. Örneğin, ASP.NET 'in önceki sürümlerinde, [http://contoso.com](http://contoso.com) isteği `Default.aspx`bir istek oluşmasına neden olur. Bu belgede, açma **formu** etiketi aşağıdaki örnekte olduğu gibi işlenir:

`<form action="Default.aspx" />`

ASP.NET 4 ' te, [http://contoso.com](http://contoso.com) bir istek da `Default.aspx`isteğine neden olur. Ancak, ASP.NET artık HTML açılış **formu** etiketini aşağıdaki örnekte olduğu gibi işler:

`<form action="" />`

**Eylem** özniteliğinin nasıl işlendiği konusunda bu fark, form GÖNDERISINI ııs ve ASP.NET tarafından nasıl işlendiği üzerinde hafif değişikliklere neden olabilir. **Action** özniteliği boş bir dize olduğunda, IIS **defaultdocumentmodule** nesnesi `Default.aspx`için bir alt istek oluşturur. Çoğu koşul altında, bu alt istek uygulama koduna saydamdır ve `Default.aspx` sayfası normal şekilde çalışır.

Ancak, yönetilen kod ile IIS 7 veya IIS 7,5 tümleşik modu arasında olası bir etkileşim, yönetilen. aspx sayfalarının alt istek sırasında düzgün çalışmayı durdurmasına neden olabilir. Aşağıdaki koşullar gerçekleşirse, bir `Default.aspx` belgeye yönelik alt istek bir hata ya da beklenmeyen davranışlara neden olur:

1. **Form** öğesinin **Action** özniteliği "" olarak ayarlanmış şekilde tarayıcıya bir. aspx sayfası gönderilir.
2. Form, ASP.NET 'e geri gönderilir.
3. Yönetilen bir HTTP modülü varlık gövdesinin bir bölümünü okur. Örneğin, bir modül **Request. form** veya **Request. params**okur. Bu, POST isteğinin varlık gövdesinin yönetilen bellekle okunmasına neden olur. Sonuç olarak, varlık gövdesi artık IIS 7 veya IIS 7,5 tümleşik modunda çalışan herhangi bir yerel kod modülü için kullanılamaz.
4. IIS **Defaultdocumentmodule** nesnesi sonunda çalışır ve `Default.aspx` belgeye bir alt istek oluşturur. Ancak, varlık gövdesi bir yönetilen kod parçası tarafından zaten okunduğu için, alt isteğe gönderilmek üzere kullanılabilecek bir varlık gövdesi yok.
5. HTTP işlem hattı alt istek için çalıştığında, `.aspx` dosyaları işleyicisi işleyici yürütme aşamasında çalışır.
6. Hiçbir varlık gövdesi olmadığından, hiçbir form değişkeni yoktur ve Görünüm durumu yoktur ve bu nedenle, hangi olayın (varsa) oluşturulması gerektiğini belirlemek için. aspx sayfa işleyicisi için herhangi bir bilgi bulunmamaktadır. Sonuç olarak, etkilenen. aspx sayfası için geri gönderme olayı işleyicilerinin hiçbiri çalışmaz.

Aşağıdaki yollarla bu davranışa geçici bir çözüm bulabilirsiniz:

- Varsayılan belge istekleri sırasında isteğin varlık gövdesine erişen HTTP modülünü belirleme ve yalnızca yönetilen istekler için çalışacak şekilde yapılandırılıp yapılandırılamayacağını belirleme. Hem IIS 7 hem de IIS 7,5 için tümleşik modda, HTTP modülleri yalnızca modülün **System. webserver/modüller** girdisine aşağıdaki özniteliği eklenerek yönetilen istekler için çalıştırılacak şekilde işaretlenebilir:

- `precondition="managedHandler"`

- Bu ayar, IIS 7 ve IIS 7,5 ' nin yönetilmeyen istekler olarak belirleyebilmesi için modülünü devre dışı bırakır. Varsayılan belge isteklerinde, ilk istek bir uzantısız eşle URL 'sidir. Bu nedenle, IIS, ilk istek işleme sırasında yönetilen Işleyicinin bir önkoşulu ile işaretlenmiş yönetilen modülleri çalıştırmaz. Sonuç olarak, yönetilen modüller yanlışlıkla varlık gövdesini okumaz ve bu nedenle varlık gövdesi hala kullanılabilir ve alt istek ve varsayılan belgeye geçirilir.

- Sorunlu http modüllerinin tüm istekler için (statik dosyalar için, **defaultdocumentmodule** nesnesine çözümlenmiş olan uzantısız eşle URL 'ler için, vb.) çalıştırılması gerekiyorsa, sayfanın **System. Web. UI. HtmlControls. HtmlForm** denetiminin **Action** özelliğini açık bir dizeye ayarlayarak etkilenen. aspx sayfalarını değiştirin. Örneğin, varsayılan belge `Default.aspx`ise, **HtmlForm** denetiminin **Action** özelliğini "default. aspx" olarak ayarlamak için sayfanın kodunu değiştirin.

<a id="0.1__Toc255587644"></a><a id="0.1__Toc256770155"></a>

## <a name="changes-to-the-aspnet-code-access-security-cas-implementation"></a>ASP.NET kod erişim güvenliği (CAS) uygulamasında yapılan değişiklikler

ASP.NET 2,0 ve uzantıya göre 3,5 ' de eklenen ASP.NET özellikleri, .NET Framework 1,1 ve 2,0 kod erişim güvenliği (CAS) modelini kullanın. Ancak, CA 'ların ASP.NET 4 ' te uygulanması önemli ölçüde fazla oldu. Sonuç olarak, genel derleme önbelleğinde (GAC) çalışan güvenilir koda dayanan kısmi güven ASP.NET uygulamaları çeşitli güvenlik özel durumlarıyla başarısız olabilir. Makine CAS ilkesi üzerinde kapsamlı değişikliklere dayanan kısmi güven uygulamaları güvenlik özel durumlarıyla de başarısız olabilir.

Aşağıdaki örnekte gösterildiği gibi, **güvenilir** yapılandırma öğesinde yeni **LegacyCasModel** özniteliğini kullanarak, kısmi-trust ASP.NET 4 uygulamalarını ASP.NET 1,1 ve 2,0 davranışına döndürebilirsiniz:

`<trust level= "Medium" legacyCasModel="true" />`

Eski CAS modeline dönzaman, aşağıdaki eski CAS davranışları etkinleştirilir:

- Makine CA 'ları ilkesi kabul edilir.
- Tek bir uygulama etki alanında birden çok farklı izin kümesine izin verilir.
- Yalnızca ASP.NET veya diğer .NET Framework kodu yığında olduğunda çağrılan GAC 'deki derlemeler için açık izin onayları gerekli değildir.

.NET Framework 4 ' te bir senaryo geri döndürülemez: Web 'de olmayan kısmi güven uygulamaları artık System. Web. dll ve System. Web. Extensions. dll dosyasındaki belirli API 'Leri çağıramaz. .NET Framework önceki sürümlerinde, Web olmayan kısmi güven uygulamaları için açıkça **AspNetHostingPermission** izinlerinin verilmesi olasıdır. Bu uygulamalar daha sonra **System. Web. HttpUtility**, **System. Web. clientservices.\*** ad alanları ve üyelik, roller ve profillerle ilgili türlerde türler kullanabilir. Bu türleri Web dışı kısmi güven uygulamalarından çağırmak artık .NET Framework 4 ' te desteklenmiyor.

> [!NOTE]
> **System. Web. HttpUtility** sınıfının **HtmlEncode** ve **htmlşifre çözme** işlevleri yeni .NET Framework 4 **System .net. webubir** sınıfına taşındı. Bu, kullanılmakta olan tek ASP.NET işlevsellikiydi, bunun yerine yeni **Webuıla** sınıfını kullanmak için uygulamanın kodunu değiştirin.

Aşağıda, ASP.NET 4 ' te varsayılan CAS uygulamasındaki değişikliklerin üst düzey bir özeti verilmiştir:

- ASP.NET uygulama etki alanları artık homojen uygulama etki alanları. Bir uygulama etki alanında yalnızca kısmi güven ve tam güven izni kümeleri kullanılabilir.
- ASP.NET kısmi güven verme kümeleri, tüm kurumsal düzeydeki, makine düzeyindeki veya kullanıcı düzeyindeki CA ilkelerinin bağımsızdır.
- 3,5 ve 3,5 SP1 'e gönderilen ASP.NET derlemeleri .NET Framework 4 Saydamlık modelini kullanacak şekilde dönüştürüldü.
- ASP.NET **AspNetHostingPermission** özniteliğinin kullanımı önemli ölçüde azaltılmıştır. Bu özniteliğin çoğu örneği genel ASP.NET API 'Lerinden kaldırılmıştır.
- ASP.NET derleme sağlayıcıları tarafından oluşturulan dinamik olarak derlenen derlemeler, derlemeleri açıkça saydam olarak işaretlemek üzere güncelleştirilmiştir.
- Tüm ASP.NET derlemeleri artık, APTCA özniteliği yalnızca Web barındırma ortamlarında kabul edilecek şekilde işaretlenir. ClickOnce gibi kısmen güvenilen Web barındırma ortamları, ASP.NET derlemelerini arayamayacak.

Yeni ASP.NET 4 kod erişimi güvenlik modeli hakkında daha fazla bilgi için MSDN Web sitesindeki [ASP.NET uygulamalarında kod erişim güvenliğini kullanma](https://msdn.microsoft.com/library/dd984947%28VS.100%29.aspx) konusuna bakın.

<a id="0.1__Toc256770156"></a><a id="0.1__Toc245724863"></a><a id="0.1__Toc252995496"></a><a id="0.1__Toc255587645"></a><a id="0.1__Toc245724864"></a>

## <a name="membershipuser-and-other-types-in-the-systemwebsecurity-namespace-have-been-moved"></a>System. Web. Security ad alanındaki MembershipUser ve diğer türler taşınmıştır

ASP.NET üyeliğinde kullanılan bazı türler `System.Web.dll` ' dan yeni System. Web. ApplicationServices. dll derlemesine taşınmıştır. Türler, istemcideki türler ve genişletilmiş .NET Framework SKU 'Lar arasında mimari katmanlama bağımlılıklarını çözümlemek için taşınmıştır.

System. Web. ApplicationServices. dll, varsayılan olarak ASP.NET derleme sistemi tarafından kullanılan Başvurulmuş derlemeler listesine eklendiğinden, Web sitesi projelerinin bu türleri taşıma sonucunda sorun yoktur. Önceki bir ASP.NET sürümü kullanılarak oluşturulan bir Web sitesi projesini Visual Studio 2010 ' de açarak ASP.NET 4 ' e yükseltirseniz, proje hata olmadan derlenir.

Benzer şekilde, ASP.NET 'in önceki bir sürümünde oluşturulmuş bir Web uygulaması projesini Visual Studio 2010 ' de açarak ASP.NET 4 ' e yükseltirseniz, yükseltme işlemi projeye System. Web. ApplicationServices. dll dosyasına bir başvuru ekler. Bu nedenle, yükseltilen Web uygulaması projeleri de hatasız olarak derlenir.

Önceki ASP.NET sürümleri kullanılarak oluşturulan derlenmiş (ikili) dosyalar, üyelik türleri farklı bir derlemeye taşınsa bile ASP.NET 4 ' te hatasız olarak da çalışır. Tür iletme bilgileri, bu türler için çalışma zamanı başvurularını otomatik olarak türler için yeni konuma yönlendiren `System.Web.dll` ASP.NET 4 sürümüne eklenmiştir.

Ancak, belirli üyelik türlerini kullanan ve önceki ASP.NET sürümlerinden yükseltilen sınıf kitaplıkları bir ASP.NET 4 projesinde kullanıldığında derlenemeyecektir. Örneğin, bir sınıf kitaplığı projesi derlenmesi ve aşağıdakiler gibi bir hata bildiremeyebilir:

- `The type 'System.Web.Security.MembershipUser' is defined in an assembly that is not referenced. You must add a reference to assembly 'System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`

- `The type name 'MembershipUser' could not be found. This type has been forwarded to assembly 'System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'. Consider adding a reference to that assembly.`

System. Web. ApplicationServices. dll ' ye sınıf kitaplığı projenize bir başvuru ekleyerek bu sorunu geçici olarak çözebilirsiniz.

Aşağıdaki listede, `System.Web.dll` 'den System. Web. ApplicationServices. dll dosyasına taşınan *System. Web. Security* türleri gösterilmektedir:

- *System. Web. Security. MembershipCreateStatus*
- *System. Web. Security. Membership. CreateUserException*
- *System. Web. Security. MembershipPasswordException*
- *System. Web. Security. MembershipPasswordFormat*
- *System. Web. Security. MembershipProvider*
- *System. Web. Security. MembershipProviderCollection*
- *System. Web. Security. MembershipUser*
- *System. Web. Security. MembershipUserCollection*
- *System. Web. Security. MembershipValidatePasswordEventHandler*
- *System. Web. Security. ValidatePasswordEventArgs*
- *System. Web. Security. RoleProvider*
- <a id="0.1_a"></a>*System. Web. Configuration. MembershipPasswordCompatibilityMode*

<a id="0.1__Toc256770157"></a>

## <a name="output-caching-changes-to-vary--http-header"></a>\* HTTP üst bilgisinde değişiklik yapmak için çıktıyı önbelleğe alma değişiklikleri

ASP.NET 1,0 ' de bir hata, yanıt olarak `Location="ServerAndClient"` belirtilen önbelleğe alınmış sayfalara bir `Vary:*` HTTP üst bilgisi yaymak için bir çıktı – Cache ayarı olarak neden oldu. Bu, istemci tarayıcılarına sayfayı hiçbir şekilde yerel olarak önbelleğe almamasını söyleme etkisi içeriyordu.

ASP.NET 1,1 ' de, **System. Web. HttpCachePolicy. SetOmitVaryStar** yöntemi eklenmiştir ve bu, `Vary:*` üst bilgisini bastırmak için çağırabilirler. Bu yöntem, yayınlanan HTTP üstbilgisinin değiştirilmesi, zaman içinde olası bir değişiklik olduğu kabul edildiği için seçildi. Ancak, geliştiriciler ASP.NET ' deki davranış tarafından karıştırılır ve hata raporları geliştiricilerin var olan **SetOmitVaryStar** davranışının farkında olduğunu öneriyor.

ASP.NET 4 ' te, kök sorunu gidermek için karar yapıldı. `Vary:*` HTTP üst bilgisi artık aşağıdaki yönergeyi belirten yanıtlardan yayılmadı:

`<%@OutputCache Location="ServerAndClient" %>`

Sonuç olarak, `Vary:*` üst bilgisini bastırmak için **SetOmitVaryStar** artık gerekli değildir.

Bir sayfada **@ OutputCache** yönergesinde `Location="ServerAndClient"` belirten uygulamalarda, artık **Location** özniteliği değerinin adı tarafından belirtilen davranışı görürsünüz. diğer bir deyişle, **SetOmitVaryStar** yöntemini çağırmanız gerekmeden sayfalar tarayıcıda önbelleğe alınır.

Uygulamanızdaki sayfaların `Vary:*`yaymalıdır, aşağıdaki örnekte olduğu gibi **AppendHeader** metodunu çağırın:

`HttpResponse.AppendHeader("Vary","*");`

Alternatif olarak, çıktı önbelleği **konum** özniteliğinin değerini "sunucu" olarak değiştirebilirsiniz.

<a id="0.1__Toc255587646"></a><a id="0.1__Toc256770158"></a>

## <a name="systemwebsecurity-types-for-passport-are-obsolete"></a>Passport için System. Web. Security türleri artık kullanılmıyor

ASP.NET 2,0 ' de yerleşik olarak bulunan Passport desteği, Passport (şimdi LiveId) değişikliklerinden kaynaklanan bazı yıllar için kullanımdan kaldırılmıştır ve desteklenmez. Sonuç olarak, **System. Web. Security** içindeki Passport ile ilgili beş tür artık **kullanımdan kalkmaattribute** özniteliğiyle işaretlenir.

<a id="0.1__The_MenuItem.PopOutImageUrl_Propert"></a><a id="0.1__Toc256770159"></a>

## <a name="the-menuitempopoutimageurl-property-fails-to-render-an-image-in-aspnet-4"></a>MenuItem. PopOutImageUrl özelliği, ASP.NET 4 ' te bir görüntüyü Işlemek için başarısız oluyor

ASP.NET 3,5 ' de, *MenuItem. PopOutImageUrl* özelliği menü öğesinde görüntülenen bir görüntünün URL 'sini belirtmenize izin verir. Aşağıdaki örnek, ASP.NET 3,5 ' de bu özelliğin biçimlendirme içinde nasıl ekleneceğini gösterir.

[!code-aspx[Main](breaking-changes/samples/sample11.aspx)]

ASP.NET 4 ' te bir tasarım değişikliği sonucunda, özelliği *MenuItem* sınıfı Için ayarlandıysa *PopOutImageUrl 'si* için çıkış işlenmez. Bunun yerine, *StaticPopOutImageUrl* özelliğini ya da *DynamicPopOutImageUrl* özelliğini kullanarak doğrudan *menü* denetimindeki bir görüntü URL 'si belirtmeniz gerekir. Statik bir menü ile çalışırken, *Menu. StaticPopOutImageUrl* özelliği, aşağıdaki örnekte gösterildiği gibi statik menü öğesinin bir alt menü olduğunu göstermek için görüntülenen görüntünün URL 'sini belirtir:

[!code-aspx[Main](breaking-changes/samples/sample12.aspx)]

Dinamik bir menü ile çalışıyorsanız, bir dinamik menü öğesinin bir alt menü olduğunu gösteren bir görüntünün URL 'sini belirtmek için *Menu. DynamicPopOutImageUrl* özelliğini kullanın. Aşağıdaki örnek öncekiyle benzerdir, ancak dinamik bir menü için *DynamicPopOutImageUrl* özelliğinin nasıl ayarlanacağını gösterir.

[!code-aspx[Main](breaking-changes/samples/sample13.aspx)]

Menu. *DynamicPopOutImageUrl* özelliği ayarlanmamışsa ve *Menu. DynamicEnableDefaultPopOutImage* özelliği *false*olarak ayarlandıysa, görüntü görüntülenmez. Benzer şekilde, *StaticPopOutImageUrl* özelliği ayarlanmamışsa ve *Staticenabledefaultpopoutimage* özelliği *false*olarak ayarlandıysa, görüntü görüntülenmez.

Bu özelliklerin yollarını ayarladığınızda, ters eğik çizgi (\)) yerine bir eğik çizgi (/) kullanın. Daha fazla bilgi için bkz. [Menu. StaticPopOutImageUrl ve Menu. DynamicPopOutImageUrl, yollar bu belgenin başka bir yerinde ters eğik çizgi Içerdiğinde görüntüleri Işleyemeyebilir](#0.1__Menu.StaticPopOutImageUrl_and_Menu. "_Menu. StaticPopOutImageUrl_and_Menu.") .

<a id="0.1__Menu.StaticPopOutImageUrl_and_Menu."></a><a id="0.1__Toc256770160"></a>

## <a name="menustaticpopoutimageurl-and-menudynamicpopoutimageurl-fail-to-render-images-when-paths-contain-backslashes"></a>Menu. StaticPopOutImageUrl ve Menu. DynamicPopOutImageUrl, yollar ters eğik çizgi Içerdiğinde görüntü Işleme başarısız olur

ASP.NET 4 ' te, *menü. StaticPopOutImageUrl 'si* ve *Menu. DynamicPopOutImageUrl* özellikleri kullanılarak belirttiğiniz görüntüler, yol backlashes içeriyorsa (\). Bu, önceki ASP.NET sürümlerinden bir değişiklik.

Aşağıdaki *menü* denetimi işaretlemesi örneği, bir ters eğik çizgi içeren bir yol kullanarak *StaticPopOutImageUrl* özelliği kümesini gösterir. ASP.NET 4 ' te, özelliğinde belirtilen görüntü işlenmeyecektir.

[!code-aspx[Main](breaking-changes/samples/sample14.aspx)]

Bu sorunu düzeltmek için, *StaticPopOutImageUrl* ve *dynamicpopoutimageurl* özelliklerinde belirtilen yol değerlerini eğik çizgi (/) kullanacak şekilde değiştirin. Aşağıdaki örnekte bu değişiklik gösterilmektedir:

[!code-aspx[Main](breaking-changes/samples/sample15.aspx)]

*MenuItem. PopOutImageUrl* özelliği değiştirildiğinden, ASP.net 'in önceki sürümlerinden ASP.NET 4 ' e geçirilmiş uygulamaların de etkilenebileceğini unutmayın. Daha fazla bilgi için bkz [. MenuItem. PopOutImageUrl özelliği, bu belgenin başka bir yerinde bir görüntüyü ASP.NET 4 ' te işlemek Için başarısız oluyor](#0.1__The_MenuItem.PopOutImageUrl_Propert "_The_MenuItem. PopOutImageUrl_Propert") .

<a id="0.1__Toc224729061"></a><a id="0.1__Toc255587647"></a><a id="0.1__Toc256770161"></a>

## <a name="disclaimer"></a>Sorumluluk reddi

Bu bir ön belgedir ve burada açıklanan yazılımın son ticari sürümünden önce önemli ölçüde değiştirilebilir.

Bu belgede yer alan bilgiler, Yayın tarihi itibariyle ele alınan sorunlar hakkında Microsoft Corporation 'ın geçerli görünümünü temsil eder. Microsoft 'un değişen piyasa koşullarını yanıtlaması gerektiğinden, Microsoft 'un kapsamında bir taahhüt olarak yorumlanmamalıdır ve Microsoft 'un, yayın tarihinden sonra sunulan bilgilerin doğruluğunu garanti edemez.

Bu teknik Inceleme yalnızca bilgilendirme amaçlıdır. MICROSOFT, BU BELGEDEKI BILGILERE GÖRE HIÇBIR GARANTI VERMEZ, ÖRTÜLÜ VEYA YASAL DEĞILDIR.

Tüm geçerli telif hakkı yasaları ile uyumlu olması, kullanıcının sorumluluğundadır. Telif hakkı kapsamındaki hakları sınırlandırmadan, bu belgenin hiçbir bölümü çoğaltılamaz, bir alma sisteminde depolanabilir veya bir alma sisteminde bulunabilir ya da herhangi bir biçimde ya da herhangi bir amaçla (elektronik, mekanik, Fotokopi, kayıt veya diğer yollarla) veya herhangi bir amaçla iletilebilir Microsoft Corporation 'ın Express yazılı izni olmadan.

Microsoft 'un bu belgede ilgili konuyu kapsayan patentler, patent uygulamaları, ticari markalar, telif hakları veya diğer fikri mülkiyet hakları olabilir. Microsoft 'un herhangi bir yazılı lisans sözleşmesinde açık bir şekilde sağlanmasının dışında, bu belgenin bu patentinin bir lisansını, ticari markalara, telif haklarına veya diğer fikri mülkiyet için herhangi bir lisansa vermez.

Aksi belirtilmedikçe, burada adı geçen örnek şirketler, kuruluşlar, ürünler, etki alanı adları, e-posta adresleri, logolar, kişiler, konumlar ve olaylar kurgusaldır ve gerçek şirket, kuruluş, ürün, etki alanı adı, e-posta ile hiçbir ilişki yoktur Adres, logo, kişi, yer veya olay amaçlıdır veya çıkarsanmalıdır.

© 2010 Microsoft Corporation. Tüm hakları saklıdır.

Microsoft ve Windows, Microsoft Corporation 'ın Birleşik Devletler ve/veya diğer ülkelerde kayıtlı ticari markaları veya ticari markalarıdır.

Burada bahsedilen gerçek şirketlerin ve ürünlerin adları, ilgili sahiplerinin ticari markaları olabilir.
