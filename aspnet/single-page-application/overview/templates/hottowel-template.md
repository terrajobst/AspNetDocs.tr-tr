---
uid: single-page-application/overview/templates/hottowel-template
title: Etkin şablon | Microsoft Docs
author: madskristensen
description: Hottohavtemplate
ms.author: riande
ms.date: 02/09/2013
ms.assetid: 75af2e17-6ed3-4d24-8ea1-bc340027c318
msc.legacyurl: /single-page-application/overview/templates/hottowel-template
msc.type: authoredcontent
ms.openlocfilehash: eeab69e75546791978bb09d7823d95caf9dca1a0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578486"
---
# <a name="hot-towel-template"></a>Hot Towel şablonu

[Mads Kristensen](https://github.com/madskristensen) tarafından

> Etkin yazı MVC şablonu John Papa tarafından yazılmıştır
> 
> Hangi sürümün indirileceği seçin:
> 
> [Visual Studio 2012 için sık erişimli MVC şablonu](https://visualstudiogallery.msdn.microsoft.com/1f68fbe8-b4e9-4968-9fd3-ddc7cbc52dca)
> 
> [Visual Studio 2013 için sık erişimli MVC şablonu](https://visualstudiogallery.msdn.microsoft.com/1eb8780d-d522-4dcf-bf56-56f0eab305c2)
> 
> 
> Etkin kısayol: yalnızca bir tane olmadan SPA 'ya gitmek istemezsiniz!

SPA oluşturmak istiyor ancak nereden başlayacağınıza karar veremiyorum mi? Etkin kısayol kullanın ve saniyeler içinde oluşturmanız gereken bir SPA ve tüm araçlara sahip olacaksınız!

Sık erişimli, ASP.NET ile tek sayfalı uygulama (SPA) oluşturmak için harika bir başlangıç noktası oluşturur. Seçtiğiniz kutudan biri, kodunuz için modüler bir yapı, gezinti, veri bağlama, zengin veri yönetimi ve basit ancak zarif stillendirme sağlar. Sıcak şey, SPA 'yı oluşturmak için ihtiyacınız olan her şeyi sağlar. böylece, devam etmenize değil uygulamanıza odaklanırsınız.

> [John Papa 'nin videolarının videoları, öğreticiler ve Plurun kursu](http://johnpapa.net/spa?vsix)hakkında daha fazla bilgi edinin.

## <a name="application-structure"></a>Uygulama yapısı

Sık erişimli SPA, uygulamanızı tanımlayan JavaScript ve HTML dosyalarını içeren bir uygulama klasörü sağlar.

Uygulama klasörü içinde:

- Durandal
- hizmetler
- ViewModel 'lar
- görünümler

Uygulama klasörü bir modül koleksiyonu içerir. Bu modüller işlevleri kapsüller ve diğer modüller üzerinde bağımlılıklar bildirir. Görünümler klasörü, uygulamanız için HTML içerir ve viewmodeller klasörü, görünümler (ortak bir MVVM modeli) için sunum mantığını içerir. Hizmetler klasörü, uygulamanızın HTTP veri alımı veya yerel depolama etkileşimi gibi ihtiyaç duyduğu tüm ortak hizmetleri muhafazası için idealdir. Hizmet modüllerindeki kodu yeniden kullanmak için birden çok ViewModel kullanılması yaygındır.

## <a name="aspnet-mvc-server-side-application-structure"></a>ASP.NET MVC sunucu tarafı uygulama yapısı

Bilinen ve güçlü ASP.NET MVC yapısında sık erişimli yapılar.

- Uygulama\_başlangıç
- İçerik
- Denetleyiciler
- Modeller
- Komut dosyaları
- Görünümler

## <a name="featured-libraries"></a>Öne çıkan kitaplıklar

- ASP.NET MVC
- ASP.NET Web API
- ASP.NET Web Iyileştirmesi-paketleme ve minbirleşme
- [Breeze. js](http://Breezejs.com) -zengin veri yönetimi
- [Durandal. js](http://Durandaljs.com) -gezinti ve görünüm bileşimi
- [Altını gizleme. js](http://Knockoutjs.com) -veri bağlamaları
- AMD ve iyileştirme ile [. js](http://requirejs.org) -modülerlik gerektir
- [Toastr. js](http://jpapa.me/c7toastr) -açılan iletiler
- [Twitter önyüklemesi](https://twitter.github.com/bootstrap/) -sağlam CSS stili

## <a name="installing-via-the-visual-studio-2012-hot-towel-spa-template"></a>Visual Studio 2012 Hot Toceksel SPA şablonu aracılığıyla yükleme

Etkin kısayol, Visual Studio 2012 şablonu olarak yüklenebilir. `File` | `New Project` ' ne tıklayıp `ASP.NET MVC 4 Web Application`' i seçmeniz yeterlidir. Sonra ' etkin olan tek sayfalı uygulama "şablonunu seçin ve çalıştırın!

## <a name="installing-via-the-nuget-package"></a>NuGet paketi aracılığıyla yükleme

Sık erişimli, var olan bir boş ASP.NET MVC projesini genişlettiğini de bir NuGet paketidir. Yalnızca NuGet kullanarak yükleyip çalıştırmanız yeterlidir!

[!code-powershell[Main](hottowel-template/samples/sample1.ps1)]

## <a name="how-do-i-build-on-hot-towel"></a>Etkin bir yerde nasıl oluşturabilirim?

Kod eklemeye başlamanız yeterlidir!

1. Kendi sunucu tarafı kodunuzu ekleyin, tercihen Entity Framework ve WebAPI (Breeze. js ile gerçekten uyumlu)
2. `App/views` klasöre görünümler ekleme
3. `App/viewmodels` klasöre viewmodeller ekleme
4. Yeni Görünümleriniz için HTML ve altını gizleme veri bağlamaları ekleme
5. `shell.js` gezinti rotalarını güncelleştirme

## <a name="walkthrough-of-the-htmljavascript"></a>HTML/JavaScript için İzlenecek yol

### <a name="viewshottowelindexcshtml"></a>Görünümler/Hottohava/index. cshtml

Index. cshtml, MVC uygulaması için başlangıç rotası ve görünümüdür. Bu, bekleeceğiniz tüm standart meta etiketlerini, CSS bağlantılarını ve JavaScript başvurularını içerir. Gövde, istendiklerinde tüm içeriğin (görünümlerinizin) yerleştirileceği tek bir `<div>` içerir. `@Scripts.Render`, uygulama kodunun giriş noktasını çalıştırmak için, `main.js` dosyasında bulunan. js ' yi kullanır. Uygulamanız yüklenirken giriş ekranı oluşturmayı göstermek için bir giriş ekranı sağlanır.

[!code-cshtml[Main](hottowel-template/samples/sample2.cshtml)]

### <a name="appmainjs"></a>App/Main. js

`main.js` dosyası, uygulamanız yüklendikten hemen sonra çalıştırılacak kodu içerir. Bu, gezinti rotalarınızı tanımlamak, başlangıç görünümlerinizi ayarlamak ve uygulamanızın verilerini eklemek gibi Kurulum/önyükleme işlemleri gerçekleştirmek istediğiniz yerdir.

`main.js` dosyası, uygulamanın başlamasını sağlamak için birkaç Durandal modülünü tanımlar. Define deyimleri, işlev için kullanılabilir olmaları için modüller bağımlılıklarını çözmeye yardımcı olur. İlk olarak hata ayıklama iletileri etkinleştirilir ve bu, uygulamanın konsol penceresinde gerçekleştirdiği olaylar hakkında iletiler gönderir. App. Start kodu, uygulamayı başlatmak için Durandal çerçevesine bildirir. Bu kurallar, Durandal 'ın tüm görünümleri ve viewmodellerinin sırasıyla aynı adlı klasörlerde yer aldığı şekilde ayarlanır. Son olarak, `app.setRoot` KIKS, önceden tanımlanmış bir `entrance` animasyonunu kullanarak `shell` yükler.

[!code-javascript[Main](hottowel-template/samples/sample3.js)]

## <a name="views"></a>Görünümler

Görünümler `App/views` klasöründe bulunur.

### <a name="shellhtml"></a>Shell. html

`shell.html`, HTML 'nizin ana yerleşimini içerir. Diğer görünümleriniz `shell` görünümlerinizin yanında bir yerde oluşturulur. Sık kullanılan: bir başlık, içerik alanı ve bir altbilgi olmak üzere üç bölge içeren bir `shell` sağlar. Bu bölgelerin her biri, istendiğinde diğer görünümlerle birlikte yüklenir.

Üst bilgi ve alt bilgi için `compose` bağlamaları, sırasıyla `nav` ve `footer` görünümlerine işaret etmek üzere sık erişimli olarak sabit kodlanmış. `#content` bölüm için oluşturma bağlaması `router` modülünün etkin öğesine bağlanır. Diğer bir deyişle, bir gezinti bağlantısına tıkladığınızda bu alana karşılık gelen görünüm yüklenir.

[!code-html[Main](hottowel-template/samples/sample4.html)]

### <a name="navhtml"></a>NAV. html

`nav.html` SPA 'nın gezinti bağlantılarını içerir. Bu, örneğin, menü yapısının yerleştirilebileceği yerdir. Bu, genellikle `shell.js`tanımladığınız gezintiyi göstermek için `router` modülüne veri bağımlıdır (altını gizleme kullanılarak). Altını gizleme, veri bağlama özniteliklerini gösterir ve `shell` ViewModel 'e bağlar ve `router` modülü bir görünümden diğerine gezinmesinin ortasındaysa bir ProgressBar (Twitter önyüklemesi kullanarak) görüntülenir (bkz. `router.isNavigating`).

[!code-html[Main](hottowel-template/samples/sample5.html)]

### <a name="homehtml-and-detailshtml"></a>Home. html ve details. html

Bu görünümler özel görünümler için HTML içerir. `nav` görünümü menüsündeki `home` bağlantısına tıklandığında, `home` görünümü `shell` görünümünün içerik alanına yerleştirilir. Bu görünümler, kendi özel görünümleriniz ile genişletilebilir veya değiştirilebilir.

### <a name="footerhtml"></a>footer. html

`footer.html`, `shell` görünümünün altındaki altbilgide görüntülenen HTML içerir.

## <a name="viewmodels"></a>ViewModel 'lar

Viewmodeller `App/viewmodels` klasöründe bulunur.

### <a name="shelljs"></a>Shell. js

`shell` ViewModel `shell` görünümüne bağlanan özellikleri ve işlevleri içerir. Genellikle bu, menü gezintisi bağlamalarının bulunduğu yerdir (bkz. `router.mapNav` Logic).

[!code-javascript[Main](hottowel-template/samples/sample6.js)]

### <a name="homejs-and-detailsjs"></a>Home. js ve details. js

Bu viewmodeller `home` görünümüne bağlanan özellikleri ve işlevleri içerir. Ayrıca, görünüm için sunum mantığını içerir ve veriler ile görünüm arasında yapıştırıcı olur.

[!code-javascript[Main](hottowel-template/samples/sample7.js)]

## <a name="services"></a>Hizmetler

Hizmetler App/Services klasöründe bulunur. İdeal olarak, uzak verileri alma ve göndermekten sorumlu olan bir veri hizmeti modülü gibi gelecekteki hizmetlerinizin yerleştirilmesi önerilir.

### <a name="loggerjs"></a>günlükçü. js

Sık erişimli, Hizmetler klasöründe bir `logger` modülü sağlar. `logger` modülü, iletileri konsola ve açılan menüden kullanıcıya günlüğe kaydetmek için idealdir.
