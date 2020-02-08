---
uid: single-page-application/overview/templates/backbonejs-template
title: Omurga şablonu | Microsoft Docs
author: madskristensen
description: Omurga. js SPA şablonu
ms.author: riande
ms.date: 04/04/2013
ms.assetid: 00aca413-f067-4108-9bd1-cf21e64a2646
msc.legacyurl: /single-page-application/overview/templates/backbonejs-template
msc.type: authoredcontent
ms.openlocfilehash: 7297db7d5b35a53b40f9d9162960e529a167bd12
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/07/2020
ms.locfileid: "77074897"
---
# <a name="backbone-template"></a>Omurga Şablonu

[Mads Kristensen](https://github.com/madskristensen) tarafından

> Omurga SPA şablonu, kazi MANZUR Kshıd tarafından yazılmıştır
> 
> [Omurga. js SPA şablonunu indirin](https://go.microsoft.com/fwlink/?LinkId=293631)

Omurga. js SPA şablonu, [omurga. js](http://backbonejs.org/) kullanarak etkileşimli istemci tarafı Web uygulamalarını hızlıca oluşturmaya başlamanızı sağlayacak şekilde tasarlanmıştır.

Şablon, ASP.NET MVC 'de bir omurga. js uygulaması geliştirmek için bir başlangıç iskelet sağlar. Bu, temel e-posta şablonlarıyla Kullanıcı kaydolma, oturum açma, parola sıfırlama ve kullanıcı onayı dahil olmak üzere temel Kullanıcı oturum açma işlevlerini sağlar.

Gereksinimler:

- [ASP.NET and Web Tools 2012,2 güncelleştirmesi](https://go.microsoft.com/fwlink/?LinkId=282650)

## <a name="create-a-backbone-template-project"></a>Omurga şablonu projesi oluşturma

Yukarıdaki Indir düğmesine tıklayarak şablonu indirip yükleyin. Şablon, Visual Studio uzantısı (VSıX) dosyası olarak paketlenmiştir. Visual Studio 'Yu yeniden başlatmanız gerekebilir.

**Şablonlar** bölmesinde, **yüklü şablonlar** ' ı seçin ve **görsel C#**  düğümünü genişletin. **Görsel C#** bölümünde **Web**' i seçin. Proje şablonları listesinde **ASP.NET MVC 4 Web uygulaması**' nı seçin. Projeyi adlandırın ve **Tamam**' a tıklayın.

![](backbonejs-template/_static/image1.png)

**Yeni proje** sihirbazında omurga. js Spa projesi ' ni seçin.

![](backbonejs-template/_static/image2.png)

Hata ayıklama olmadan uygulamayı derlemek ve çalıştırmak için CTRL-F5 tuşlarına basın ya da hata ayıklama ile çalıştırmak için F5 'e basın.

![](backbonejs-template/_static/image3.png)

"Hesabım" a tıklamak oturum açma sayfasını getirir:

![](backbonejs-template/_static/image4.png)

## <a name="walkthrough-client-code"></a>İzlenecek yol: Istemci kodu

İstemci tarafı ile başlayalım. İstemci uygulama betikleri ~/Scripts/Application klasöründe bulunur. Uygulama, JavaScript (. js dosyaları) ile derlenen [TypeScript](http://www.typescriptlang.org/) (. TS dosyaları) dilinde yazılır.

**Uygulama**

`Application`, Application. TS içinde tanımlanır. Bu nesne uygulamayı başlatır ve kök ad alanı olarak davranır. Kullanıcının oturum açmış olup olmadığı gibi, uygulama genelinde paylaşılan yapılandırma ve durum bilgilerini tutar.

`application.start` yöntemi, kalıcı görünümler oluşturur ve Kullanıcı oturumu açma gibi uygulama düzeyi olaylar için olay işleyicileri ekler. Ardından, varsayılan yönlendiriciyi oluşturur ve herhangi bir istemci tarafı URL 'sinin belirtilmediğini denetler. Aksi takdirde, varsayılan URL 'ye (#!/) yeniden yönlendirir.

**Olaylar**

Gevşek olarak bağlanmış bileşenler geliştirirken olaylar her zaman önemlidir. Uygulamalar, genellikle bir kullanıcı eylemine yanıt olarak birden çok işlem gerçekleştirir. Omurga, model, koleksiyon ve görünüm gibi bileşenlerle yerleşik Olaylar sağlar. Bu bileşenler arasında bağımlılıklar oluşturmak yerine, şablon bir "pub/Sub" modeli kullanır: Events. TS içinde tanımlanan `events` nesnesi, uygulama olaylarını yayımlamak ve abone olmak için bir olay hub 'ı görevi görür. `events` nesnesi tek bir. Aşağıdaki kod, bir olaya abone olmayı ve sonra olayı tetiklemeyi gösterir:

[!code-csharp[Main](backbonejs-template/samples/sample1.cs)]

**Abilmesi**

Omurga. js ' de yönlendirici, istemci tarafı sayfalarını yönlendirme ve bunları eylemler ve olaylara bağlama yöntemleri sağlar. Şablon, yönlendirici. TS ' de tek bir yönlendirici tanımlar. Yönlendirici activable görünümlerini oluşturur ve görünümleri değiştirirken durumu korur. (Activable görünümleri sonraki bölümde açıklanmıştır.) Başlangıçta proje, ana ve hakkında iki sözde görünüm içerir. Ayrıca, yol bilinmiyorsa görüntülenecek NotFound görünümü de vardır.

**Görünümler**

Görünümler ~/Scripts/Application/viewklasöründe tanımlanmıştır. İki tür görünüm, activable görünümü ve kalıcı iletişim kutusu görünümleri vardır. Activable görünümleri yönlendirici tarafından çağrılır. Bir activable görünümü gösterildiğinde, diğer tüm activable görünümleri devre dışı olur. Bir activable görünümü oluşturmak için, görünümü `Activable` nesnesiyle genişletin:

[!code-javascript[Main](backbonejs-template/samples/sample2.js)]

`Activable` ile genişletmek, görünüme, `activate` ve `deactivate`iki yeni yöntem ekler. Yönlendirici, görünümü etkinleştirmek ve etkin hale eklemek için bu yöntemleri çağırır.

Kalıcı Görünümler [Twitter önyükleme](https://twitter.github.com/bootstrap/) kalıcı iletişim kutuları olarak uygulanır. `Membership` ve `Profile` görünümleri kalıcı görünümlerdir. Model görünümleri, herhangi bir uygulama olayı tarafından çağrılabilir. Örneğin, `Navigation` görünümünde, "Hesabım" bağlantısına tıkladığınızda, kullanıcının oturum açıp açmadığına bağlı olarak, `Membership` görünümü veya `Profile` görünümü görüntülenir. `Navigation`, Click olay işleyicilerini `data-command` özniteliğine sahip herhangi bir alt öğeye iliştirir. HTML biçimlendirmesi aşağıda verilmiştir:

[!code-html[Main](backbonejs-template/samples/sample3.html)]

Bu, olayları bağlamak için gezinti. TS ' deki koddur:

[!code-csharp[Main](backbonejs-template/samples/sample4.cs)]

**Modelde**

Modeller, ~/Scripts/Application/models. içinde tanımlanmıştır. Modellerin hepsi üç temel şeyi vardır: varsayılan öznitelikler, doğrulama kuralları ve sunucu tarafı uç noktası. Tipik bir örnek aşağıda verilmiştir:

[!code-javascript[Main](backbonejs-template/samples/sample5.js)]

**Eklentiler**

~/Scripts/Application/lib klasörü birkaç kullanışlı jQuery eklentisi içerir. Form. ts dosyası form verileriyle çalışmak için bir eklenti tanımlar. Genellikle form verilerini serileştirmek veya serisini kaldırmak ve model doğrulama hatalarını göstermek gerekir. Form. TS eklentisinin `serializeFields`, `deserializeFields`ve `showFieldErrors`gibi yöntemleri vardır. Aşağıdaki örnek, bir formun bir modele nasıl serileştirilmek olduğunu gösterir.

[!code-javascript[Main](backbonejs-template/samples/sample6.js)]

Flashbar. TS eklentisi kullanıcıya çeşitli türlerde geri bildirim iletileri sağlar. Yöntemler `$.showSuccessbar`, `$.showErrorbar` ve `$.showInfobar`. Arka planda, doğru animasyonlu iletileri göstermek için Twitter önyükleme uyarılarını kullanır.

Onayla. TS eklentisi tarayıcının onaylama iletişim kutusunun yerini alır, ancak API biraz farklı olur:

[!code-javascript[Main](backbonejs-template/samples/sample7.js)]

## <a name="walkthrough-server-code"></a>İzlenecek yol: sunucu kodu

Şimdi sunucu tarafına göz atalım.

**Denetleyiciler**

Tek sayfalı bir uygulamada, sunucu Kullanıcı arabiriminde yalnızca küçük bir rol oynar. Genellikle, sunucu ilk sayfayı işler ve sonra JSON verilerini gönderir ve alır.

Şablonda iki MVC denetleyicisi vardır: `HomeController` ilk sayfayı işler ve yeni kullanıcı hesaplarını doğrulamak ve parolaları sıfırlamak için `SupportsController` kullanılır. Şablondaki diğer tüm denetleyiciler, JSON verilerini gönderen ve alan ASP.NET Web API denetleyicileridir. Varsayılan olarak, denetleyiciler Kullanıcı ile ilgili görevleri gerçekleştirmek için yeni `WebSecurity` sınıfını kullanır. Ancak, bu görevler için temsilcileri geçirmenize olanak sağlayan isteğe bağlı oluşturucuları de vardır. Bu, testi kolaylaştırır ve bir IOC kapsayıcısı kullanarak `WebSecurity` başka bir şeyle değiştirmenize olanak sağlar. Aşağıda bir örnek verilmiştir:

[!code-csharp[Main](backbonejs-template/samples/sample8.cs)]

## <a name="views"></a>Görünümler

Görünümler modüler olacak şekilde tasarlanmıştır: bir sayfanın her bölümü kendi adanmış görünümüne sahiptir. Tek sayfalı bir uygulamada, kendisine karşılık gelen denetleyiciye sahip olmayan görünümleri eklemek yaygındır. `@Html.Partial('myView')`çağırarak bir görünüm ekleyebilirsiniz, ancak bu sıkıcı bir alır. Bunun daha kolay olması için, şablon, belirtilen bir klasördeki tüm görünümleri işleyen bir yardımcı yöntemi `IncludeClientViews`tanımlar:

[!code-cshtml[Main](backbonejs-template/samples/sample9.cshtml)]

Klasör adı belirtilmemişse, varsayılan klasör adı "ClientViews" olur. İstemci görünümünüz de kısmi görünümler kullanıyorsa, kısmi görünümü bir alt çizgi karakteriyle (örneğin, `_SignUp`) adlandırın. `IncludeClientViews` yöntemi, adı alt çizgi ile başlayan tüm görünümleri dışlar. İstemci görünümünde kısmi bir görünüm eklemek için `Html.Partial('_SignUp')`yerine `Html.ClientView('SignUp')` çağırın.

**E-posta gönderiliyor**

E-posta göndermek için, şablon [posta](http://aboutcode.net/postal)'yı kullanır. Bununla birlikte, posta, `IMailer` arabirimiyle kodun geri kalanından soyutlandığından, kolayca başka bir uygulamayla de değiştirebilirsiniz. E-posta şablonları, görünümler/e-postalar klasöründe bulunur. Gönderenin e-posta adresi, **appSettings** bölümünün `sender.email` anahtarındaki Web. config dosyasında belirtilir. Ayrıca, Web. config dosyasında `debug="true"`, uygulama geliştirmeyi hızlandırmak için kullanıcı e-posta onayı gerektirmez.

## <a name="github"></a>GitHub

Ayrıca, [GitHub](https://github.com/kazimanzurrashid/AspNetMvcBackboneJsSpa)'da omurga. js Spa şablonunu bulabilirsiniz.
