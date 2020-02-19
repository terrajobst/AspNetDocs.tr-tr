---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: 'Ek: BT örneğini yapılandırma örnek uygulaması (Azure ile gerçek hayatta bulut uygulamaları oluşturma) | Microsoft Docs'
author: MikeWasson
description: Azure e-Book ile gerçek dünyada bulut uygulamaları oluşturma, Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. 13 desen ve şunları yapabilir...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: 896196bdb6a6b0d12a6c798ead510e37dd38a9fc
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456887"
---
# <a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a>Ek: BT örneğini yapılandırma örnek uygulaması (Azure ile gerçek hayatta bulut uygulamaları oluşturma)

, [Mike te son](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra) tarafından

[Çözüm projesini indirin](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> Azure e-book **Ile gerçek dünyada bulut uygulamaları oluşturma** , Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. Bulut için Web Apps 'i başarılı bir şekilde geliştirmeye yardımcı olabilecek 13 desen ve uygulamaları açıklar. E-kitap hakkında daha fazla bilgi için [ilk bölüme](introduction.md)bakın.

Azure e-Book ile gerçek dünyada bulut uygulamaları oluşturmaya yönelik bu ek, indirebileceğiniz BT örnek uygulaması hakkında ek bilgiler sağlayan aşağıdaki bölümleri içerir:

- [Bilinen sorunlar](#knownissues)
- [En iyi uygulamalar](#bestpractices)
- [Yerel bilgisayarınızda Visual Studio 'dan uygulamayı çalıştırma](#run-in-vs)
- [Windows PowerShell betiklerini kullanarak temel uygulamayı Azure App Service Web Apps dağıtma](#deploybase)
- [Windows PowerShell betiklerinin sorunlarını giderme](#troubleshooting)
- [Azure App Service Web Apps ve Azure bulut hizmeti için kuyruk işleme ile uygulamayı dağıtma](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a>Bilinen sorunlar

BT BT uygulaması, bu e-kitapta sunulan bazı desenlerin olabildiğince basit olması için ilk olarak geliştirilmiştir. Ancak, e-kitap gerçek dünyada uygulamalar oluşturmaya yönelik olduğundan, BT kodunu, piyasaya çıkarılan yazılım için yaptığımız gibi bir gözden geçirme ve test süreci olarak tabi. Herhangi bir gerçek dünya uygulamasında olduğu gibi birkaç sorun bulduk ve bunlardan bazılarının düzeltilmesi ve bazıları daha sonraki bir sürüme erteliyoruz.

Aşağıdaki liste, bir üretim uygulamasında ele alınmalıdır, ancak bir neden veya başka bir nedenle Düzelt örnek uygulamasının ilk sürümünde ele kurmamaya karar verdiğimiz sorunları içerir.

### <a name="security"></a>Güvenlik

- Bir görevi var olmayan bir sahibe atayamazsınız.
- Yalnızca sizin oluşturduğunuz veya size atanan görevleri görüntüleyebilmeniz ve değiştirediğinizden emin olun.
- Oturum açma sayfaları ve kimlik doğrulama tanımlama bilgileri için HTTPS kullanın.
- Kimlik doğrulama tanımlama bilgileri için bir zaman sınırı belirtin.

### <a name="input-validation"></a>Giriş doğrulaması

Genel olarak, bir üretim uygulaması, BT uygulamasından daha fazla giriş doğrulaması yapacağından, bu uygulamayı düzeltir. Örneğin, karşıya yükleme için izin verilen görüntü boyutu/resim dosya boyutu sınırlı olmalıdır.

### <a name="administrator-functionality"></a>Yönetici işlevselliği

Yönetici, mevcut görevlerdeki sahipliği değiştirebilmelidir. Örneğin, bir görevin Oluşturucusu şirketten ayrılırken, yönetim erişimi etkinleştirilmediği takdirde görevi sürdürmek için herhangi bir yetkiliyle ayrılmayabilir.

### <a name="queue-message-processing"></a>İleti işlemeyi sıraya al

BT BT uygulamasındaki sıra iletisi işleme, en az sayıdaki kodla sıra merkezli iş düzenini göstermek için basit olacak şekilde tasarlanmıştır. Bu basit kod, gerçek bir üretim uygulaması için yeterli değildir.

- Kod, her kuyruk iletisinin en çok bir kez işleneceğini garanti etmez. Sıradan bir ileti aldığınızda, iletinin diğer kuyruk dinleyicileri tarafından görülemiyorsa zaman aşımı süresi vardır. İleti silinmeden önce zaman aşımı süresi dolarsa ileti yeniden görünür hale gelir. Bu nedenle, bir çalışan rolü örneği bir iletiyi işlemeye uzun süre harcadıysanız, aynı iletinin iki kez işlenebilmesi için teorik olarak, veritabanında yinelenen bir görevin oluşmasına neden olur. Bu sorun hakkında daha fazla bilgi için bkz. [Azure depolama kuyruklarını kullanma](https://msdn.microsoft.com/library/ff803365.aspx#sec7).
- Sıra yoklama mantığı, ileti alımı toplu işlem tarafından daha düşük maliyetli olabilir. [Cloudqueue. GetMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx)her çağırdığınızda, işlem maliyeti vardır. Bunun yerine, tek bir işlemde birden çok ileti alan [Cloudqueue. GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (plural ') çağırabilirsiniz. Azure depolama kuyrukları için işlem maliyetleri çok düşüktür, bu nedenle maliyetlerle ilgili etki çoğu senaryoda önemli değildir.
- Kuyruk ileti işleme kodundaki sıkı döngü, çok çekirdekli VM 'Leri verimli bir şekilde kullanmadan CPU benzeşimi sağlar. Daha iyi bir tasarım, görev paralelliği kullanarak birkaç zaman uyumsuz görevi paralel olarak çalıştırır.
- Kuyruk ileti işleme yalnızca ilkel özel durum işleme sahiptir. Örneğin, kod, [zarar iletilerini](https://msdn.microsoft.com/library/ms789028.aspx)işlemez. (İleti işleme bir özel duruma neden olursa, hatayı günlüğe kaydedin ve iletiyi silmeniz ya da çalışan rolü onu tekrar işlemeye çalışır ve döngü süresiz olarak devam eder.)

### <a name="sql-queries-are-unbounded"></a>SQL sorguları sınırsız

Geçerli onarım BT kodu, dizin sayfaları sorgularının kaç satır döndürebileceğini gösteren hiçbir sınır yoktur. Veritabanına büyük bir görev hacmi girilirse, alınan sonuç listelerinin boyutu performans sorunlarına neden olabilir. Çözüm, sayfalama uygulamadır. Bir örnek için, bkz. [bir ASP.NET MVC uygulamasındaki Entity Framework sıralama, filtreleme ve sayfalama](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md).

### <a name="view-models-recommended"></a>Modelleri görüntüleme önerilir

BT BT uygulamasını düzeltme, denetleyici ve görünüm arasında bilgi geçirmek için FixItTask varlık sınıfını kullanır. En iyi uygulama, görüntüleme modellerini kullanmaktır. Etki alanı modeli (örn., FixItTask varlık sınıfı), veri kalıcılığı için gerekli olanlar etrafında tasarlanmıştır, ancak bir görünüm modeli veri sunumu için tasarlanamaz. Daha fazla bilgi için bkz. [12 ASP.NET MVC En Iyi yöntemleri](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx).

### <a name="secure-image-blob-recommended"></a>Güvenli görüntü blobu önerilir

BT BT uygulaması, karşıya yüklenen görüntüleri ortak olarak depolar, yani URL 'YI bulan herkesin görüntülere erişebileceği anlamına gelir. Resimler genel yerine güvenli hale getirilmiş olabilir.

### <a name="no-powershell-automation-scripts-for-queues"></a>Kuyruklar için PowerShell Otomasyonu betikleri yok

Örnek PowerShell Otomasyon betikleri yalnızca Azure App Service Web Apps tamamen çalışan, düzeltilmesi için yalnızca temel sürüm için yazılmıştır. Web uygulamasına kurulum ve dağıtım için kullanılacak betikler ve sıra işleme için gereken bulut hizmeti ortamı için betik sağlamadık.

### <a name="special-handling-for-html-codes-in-user-input"></a>Kullanıcı girişinde HTML kodları için özel işleme

ASP.NET, kötü amaçlı kullanıcıların, Kullanıcı girişi metin kutularına komut dosyası girerek siteler arası komut dosyası saldırıları deneyebileceği birçok yolu otomatik olarak engeller. Ayrıca, görev başlıklarını ve notları göstermek için kullanılan MVC `DisplayFor` Yardımcısı, tarayıcıya gönderdiği değerleri otomatik olarak HTML olarak kodlar. Ancak bir üretim uygulamasında ek ölçüler yapmak isteyebilirsiniz. Daha fazla bilgi için bkz. [ASP.net Içinde Istek doğrulaması](https://msdn.microsoft.com/library/hh882339.aspx).

<a id="bestpractices"></a>
## <a name="best-practices"></a>En iyi uygulamalar

Düzeltme BT uygulamasının orijinal sürümünün kod incelemesinin ve test edilmesine sonra düzeltilen bazı sorunlar aşağıda verilmiştir. Özgün kodlayıcı 'ın bazı bir en iyi uygulama farkında olmamasından kaynaklandı, çünkü kod hızla yazıldığı ve piyasaya sürülen yazılım için tasarlanmamıştır. Bu gözden geçirme ve test etme konusunda öğrendiğimiz bir şey, Web uygulamaları geliştirmekte olan başkaları için yararlı olabilecek bir sorun olması durumunda buradaki sorunları listeliyoruz.

### <a name="dispose-the-database-repository"></a>Veritabanı deposunu atma

`FixItTaskRepository` sınıfı Entity Framework `DbContext` örneğini atmalıdır. Bunu `FixItTaskRepository` sınıfında `IDisposable` uygulayarak yaptık:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

AutoFac 'ın `FixItTaskRepository` örneği otomatik olarak atıyacağını unutmayın. bu nedenle, açıkça elden atmaları gerekmez.

Başka bir seçenek de `DbContext` üye değişkenini `FixItTaskRepository`' dan kaldırmak ve bunun yerine her bir depo yöntemi içinde bir `using` deyimin içinde yerel bir `DbContext` değişkeni oluşturmaktır. Örneğin:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a>Dı ile birlikte tekton Kaydet

`PhotoService` sınıfının ve `Logger` sınıfının yalnızca bir örneği gerekli olduğundan, bu sınıfların *DependenciesConfig.cs*içinde [bağımlılık ekleme için tek örnek olarak kaydedilmesi](https://code.google.com/p/autofac/wiki/InstanceScope) gerekir:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a>Güvenlik: kullanıcılara hata ayrıntılarını gösterme

Özgün çözüm BT uygulamasının genel bir hata sayfası yoktu ve tüm özel durumların Kullanıcı arabirimine balon oluşturmasını sağlayın, bu nedenle veritabanı bağlantı hataları gibi bazı özel durumlar tarayıcıya bir tam yığın izlemenin görüntülenmesine neden olabilir. Ayrıntılı hata bilgileri, bazı durumlarda kötü amaçlı kullanıcılar tarafından gerçekleştirilen saldırıları kolaylaştırabilir. Çözüm, özel durum ayrıntılarını günlüğe kaydetmek ve kullanıcıya hata ayrıntılarını içermeyen bir hata sayfası görüntülemektir. BT uygulaması zaten günlüğe kaydediliyor ve bir hata sayfası göstermek için, Web. config dosyasına `<customErrors mode=On>` ekledik.

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

Varsayılan olarak, *Views\shared\error.exe* hata için görüntülenmesine neden olur. *Error. cshtml* 'yi özelleştirebilir veya kendi hata sayfası görünümünüzü oluşturabilir ve bir `defaultRedirect` özniteliği ekleyebilirsiniz. Ayrıca, belirli hatalar için farklı hata sayfaları belirtebilirsiniz.

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a>Güvenlik: yalnızca bir görevin Oluşturucusu tarafından düzenlenmesine izin ver

Pano dizini sayfası yalnızca oturum açan kullanıcı tarafından oluşturulan görevleri gösterir, ancak kötü niyetli bir Kullanıcı, başka bir kullanıcının görevine KIMLIĞI olan bir URL oluşturabilir. Bu durumda 404 döndürmek için *DashboardController.cs* 'e kod ekledik:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a>Özel durumlara izin verme

Özgün BT BT uygulaması, bir SQL sorgusundan kaynaklanan bir özel durum günlüğe kaydedildikten sonra null değer döndürdü:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

Bu, sorguyu başarılı bir şekilde, ancak hiçbir satır döndürmediğiniz şekilde kullanıcıya baktı. Çözüm, yakalama ve günlüğe kaydetme işleminden sonra özel durumu yeniden oluşturmak için:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a>Çalışan rollerinde tüm özel durumları yakala

Bir çalışan rolündeki işlenmemiş özel durumlar, sanal makinenin geri dönüştürülmesine neden olur, böylece bir try-catch bloğunda yaptığınız her şeyi kaydırmak ve tüm özel durumları işlemek istiyorsunuz.

### <a name="specify-length-for-string-properties-in-entity-classes"></a>Varlık sınıflarında dize özellikleri için uzunluğu belirtin

Basit kodu göstermek için, Düzeltme BT uygulamasının özgün sürümü, FixItTask varlığının alanları için uzunluk belirtmiyordu ve sonuç olarak veritabanında varchar (max) olarak tanımlanmıştı. Sonuç olarak, Kullanıcı arabirimi neredeyse her türlü girişi kabul eder. Uzunlukları belirtme, hem Web sayfasında hem de veritabanındaki sütun boyutunda bulunan kullanıcı girişine uygulanan limitleri belirler:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a>Değişmeleri beklenmediği zaman özel üyeleri ReadOnly olarak işaretle

Örneğin, `DashboardController` sınıfında bir `FixItTaskRepository` örneği oluşturulur ve değiştirilmesi beklenmediğinden, [salt okunur](https://msdn.microsoft.com/library/acdd6hb7.aspx)olarak tanımlandık.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a>Liste kullan. Herhangi bir () liste yerine. Count () &gt; 0

Bütün olarak bir listedeki bir veya daha fazla öğenin belirtilen ölçütlere uygun olup olmadığı hakkında bilgi alıyorsa [, her bir yöntemi kullanın](https://msdn.microsoft.com/library/bb534972.aspx) çünkü bu, ölçütlere uyan bir öğe olduğu anda, `Count` yöntemi her öğe için her zaman yinelemek zorunda KALIDIR. Pano *dizini. cshtml* dosyası başlangıçta bu koda sahipti:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

Bunu şu şekilde değiştirdik:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a>MVC yardımcıları kullanarak MVC görünümlerinde URL oluşturma

Ana sayfada **bir düzelme BT uygulaması oluştur** düğmesi Için, BT uygulamasını onarma bir bağlantı öğesini sabit olarak kodlanmış olarak düzeltir:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

Bu gibi görünüm/eylem bağlantıları için, [URL. Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML Yardımcısı ' nı kullanmak daha iyidir, örneğin:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a>Çalışan rolünde Thread. Sleep yerine Task. Delay kullanın

Yeni-proje şablonu, bir çalışan rolü için örnek kodda `Thread.Sleep` koyar, ancak iş parçacığının uykuya geçmesine neden olan iş parçacığı havuzunun ek gereksiz iş parçacıkları oluşturmasına neden olabilir. Bunun yerine [Task. Delay](https://msdn.microsoft.com/library/hh139096.aspx) kullanarak bundan kaçınabilirsiniz.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a>Async void kullanmaktan kaçının

Zaman uyumsuz bir yöntemin bir değer döndürmesi gerekmiyorsa, `void`yerine `Task` türü döndürün.

Bu örnek `FixItQueueManager` sınıfından olur:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

Yalnızca üst düzey olay işleyicileri için `async void` kullanmanız gerekir. Bir yöntemi `async void`olarak tanımlarsanız, çağıran yöntemi **bekler** veya yöntemin aldığı özel durumları yakalayabilir. Daha fazla bilgi için bkz. [zaman uyumsuz programlamada En Iyi uygulamalar](https://msdn.microsoft.com/magazine/jj991977.aspx).

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a>Çalışan rolü döngüsünden ayırmak için iptal belirteci kullanın

Genellikle, çalışan rolündeki **Run** yöntemi sonsuz bir döngü içerir. Çalışan rolü durdurulduğunda, [Roleentrypoint. OnStop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) yöntemi çağrılır. Bu yöntemi, **Run** yöntemi içinde yapılan çalışmayı iptal etmek ve sorunsuz bir şekilde çıkmak için kullanmanız gerekir. Aksi takdirde, işlem bir işlemin ortasında sonlandırılabilir.

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a>Otomatik MIME algılaması yordamının oturumunu kapat

Bazı durumlarda, Internet Explorer, Web sunucusu tarafından belirtilen türden farklı bir MIME türü raporlar. Örneğin, Internet Explorer HTTP yanıt üst bilgisi Içerik-türü: metin/düz olan bir dosyada HTML içeriğini bulursa, içeriğin HTML olarak işlenip işlenmeyeceğini belirler. Ne yazık ki bu "MIME algılaması", güvenilmeyen içeriği barındıran sunucular için güvenlik sorunlarına da yol açabilir. Bu sorunu çözmek için, Internet Explorer 8, MIME türü belirleme kodunda birkaç değişiklik yaptı ve uygulama geliştiricilerinin [MIME algılaması](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)'nı geri almasına izin veriyor. Aşağıdaki kod *Web. config* dosyasına eklendi.

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a>Paketlemeyi ve küçültmeye izin

Visual Studio yeni bir Web projesi oluşturduğunda, JavaScript dosyalarını paketleme ve küçültmeye yönelik varsayılan olarak etkin değildir. BundleConfig.cs içinde bir kod satırı ekledik:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a>Kimlik doğrulama tanımlama bilgileri için bir süre sonu zaman aşımı ayarlama

Varsayılan olarak, kimlik doğrulama tanımlama bilgileri iki hafta içinde sona erer. Daha kısa bir süre daha güvenlidir. Bu ayarı, *StartupAuth.cs*içinde değiştirebilirsiniz:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a>Yerel bilgisayarınızda Visual Studio 'dan uygulamayı çalıştırma

Çözümü onarma uygulamasını çalıştırmanın iki yolu vardır:

- Yeni görevleri doğrudan SQL veritabanına yazan temel uygulamayı çalıştırın.
- Görevleri oluşturmak için bir kuyruk ve arka uç hizmeti kullanarak uygulamayı çalıştırın. Sıra stili, bölüm [sırası merkezli çalışma](queue-centric-work-pattern.md)düzeninde açıklanmıştır.

<a id="runbase"></a>
### <a name="run-the-base-application"></a>Temel uygulamayı çalıştırma

1. [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)'yi yükleyin.
2. [Visual Studio için .net Için Azure SDK 'sını](https://azure.microsoft.com/downloads/)yükler.
3. . Zip dosyasını [MSDN kod galerisinden](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)indirin.
4. Dosya Gezgini 'nde. zip dosyasına sağ tıklayın ve Özellikler ' e ve ardından Özellikler penceresi engellemeyi kaldır ' a tıklayın.
5. Dosyayı sıkıştırmayı açın.
6. Visual Studio 'Yu başlatmak için. sln dosyasına çift tıklayın.
7. **Araçlar** menüsünde, **NuGet Paket Yöneticisi**' ne ve ardından **Paket Yöneticisi konsolu**' na tıklayın.
8. Paket Yöneticisi konsolunda (PMC) geri yükle ' ye tıklayın.
9. Visual Studio 'dan çıkın.
10. [Azure depolama öykünücüsünü](/azure/storage/common/storage-use-emulator)başlatın.
11. Önceki adımda kapattığınız çözüm dosyasını açarak Visual Studio 'Yu yeniden başlatın.
12. FixIt projesinin başlangıç projesi olarak ayarlandığından emin olun ve ardından projeyi çalıştırmak için CTRL + F5 tuşlarına basın.

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a>Uygulamayı kuyruk işleme ile çalıştırma

1. [Temel uygulamayı çalıştırmak](#runbase)için yönergeleri izleyin ve ardından tarayıcıyı kapatın ve Visual Studio 'yu kapatın.
2. Visual Studio 'Yu yönetici ayrıcalıklarıyla başlatın. (Azure işlem öykünücüsü 'nü kullanıyorsunuz ve bu, yönetici ayrıcalıkları gerektirir.)
3. *Myfixıt* projesindeki uygulama *Web. config* dosyasında (Web projesi), `appSettings/UseQueues` değerini "true" olarak değiştirin:

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. [Azure depolama öykünücüsü](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx) hala çalışmıyorsa, yeniden başlatın.
5. FixIt Web projesini ve MyFixItCloudService projesini eşzamanlı olarak çalıştırın.

    Visual Studio 'Yu kullanarak:

   1. FixIt projesini çalıştırmak için **F5** tuşuna basın.
   2. **Çözüm Gezgini**, MyFixItCloudService projesine sağ tıklayın ve ardından **yeni örnek Başlat** > **Hata Ayıkla** ' ya tıklayın.

    Web için Visual Studio 2013 Express 'ı kullanma:

   3. Çözüm Gezgini, FixIt çözümüne sağ tıklayın ve **Özellikler**' i seçin.
   4. **Birden çok başlangıç projesi**seçin.
   5. MyFixIt ve MyFixItCloudService altındaki **eylem** açılan listesinde **Başlat**' ı seçin.
   6. **Tamam**'a tıklayın.
   7. Her iki projeyi de çalıştırmak için **F5**'e basın.

      MyFixItCloudService projesini çalıştırdığınızda, Visual Studio Azure işlem öykünücüsü ' nü başlatır. Güvenlik Duvarı yapılandırmanıza bağlı olarak, güvenlik duvarı üzerinden öykünücüye izin vermeniz gerekebilir.

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a>Windows PowerShell betiklerini kullanarak temel uygulamayı Azure App Service Web Apps dağıtma

[Her şeyi otomatikleştirin](automate-everything.md) . BT BT uygulaması, Azure 'da bir ortam oluşturan ve projeyi yeni ortama dağıtan betikler ile sağlanır. Aşağıdaki yönergeler betiklerin nasıl kullanılacağını açıklamaktadır.

Azure 'da kuyrukları kullanmadan çalıştırmak istiyorsanız ve kuyruklar ile yerel olarak çalıştırılacak değişiklikleri yaptıysanız, aşağıdaki yönergelere geçmeden önce UseQueues appSetting değerini false olarak ayarladığınızdan emin olun.

Bu yönergeler zaten indirdiğiniz ve BT çözümünü yerel olarak yüklediğinizi ve Azure hesabınız olduğunu veya yönetmek için yetkiniz olan bir Azure aboneliğiniz olduğunu varsayar.

1. **Azure PowerShell** konsolunu yükler. Yönergeler için bkz. [Azure PowerShell nasıl yüklenir ve yapılandırılır](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).

    Bu özelleştirilmiş konsol Azure aboneliğinizle çalışacak şekilde yapılandırılmıştır. Azure modülü *Program dosyaları* dizinine yüklenir ve Azure PowerShell konsolunun her kullanımıyla otomatik olarak içeri aktarılır.

    Windows PowerShell ISE gibi farklı bir ana bilgisayar programında çalışmayı tercih ediyorsanız, Azure modülünü içeri aktarmak için [Import-Module](https://go.microsoft.com/fwlink/?LinkID=141553) cmdlet 'ini kullandığınızdan emin olun veya modülün otomatik içeri aktarılmasını tetiklemek için Azure modülündeki bir komutu kullanın.
2. **Yönetici olarak çalıştır** seçeneğiyle Azure PowerShell başlatın.
3. Azure PowerShell yürütme ilkesini `RemoteSigned`olarak ayarlamak için [set-ExecutionPolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) cmdlet 'ini çalıştırın. İlke değişikliğini gerçekleştirmek için **Y** (Evet için) girin.

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    Bu ayar, dijital olarak imzalanmamış yerel betikleri çalıştırmanızı sağlar. (Yürütme ilkesini, daha sonra engellemeyi kaldır adımının gereksinimini ortadan kaldıran `Unrestricted`olarak da ayarlayabilirsiniz, ancak bu durum güvenlik nedenleriyle önerilmez.)
4. PowerShell 'i hesabınıza yönelik kimlik bilgileriyle ayarlamak için `Add-AzureAccount` cmdlet 'ini çalıştırın.

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    Bu kimlik bilgilerinin süresi bir süre sonra doluyor ve `Add-AzureAccount` cmdlet 'ini yeniden çalıştırmanız gerekir. Bu e-kitap yazıldığı için, kimlik bilgilerinin süresinin dolması için geçen zaman sınırı 12 saattir.
5. Birden çok aboneliğiniz varsa, ' de test ortamı oluşturmak istediğiniz aboneliği belirtmek için Select-Azuyeniden gönderiliyor Scription cmdlet 'ini kullanın.
6. `Get-AzurePublishSettingsFile` ve `Import-AzurePublishSettingsFile` cmdlet 'lerini kullanarak aynı Azure aboneliği için bir yönetim sertifikasını içeri aktarın. Bu cmdlet 'lerden ilki bir sertifika dosyasını indirir ve ikinci adımda bu dosyanın yerini içeri aktarmak için belirtirsiniz. > [!IMPORTANT]
   > İndirilen dosyayı güvenli bir yerde tutun veya Azure hizmetlerinizi yönetmek için kullanılabilecek bir sertifika içerdiğinden, bununla işiniz bittiğinde silin.

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    Sertifika, SQL veritabanı sunucusunda bir güvenlik duvarı kuralı ayarlamak için geliştirme makinesinin IP adresini algılayan bir REST API çağrısı için kullanılır.
7. Komut dosyalarını içeren dizine gitmek için [set-location](https://go.microsoft.com/fwlink/p/?linkid=293912) cmdlet 'ini (diğer adlar `cd`, `chdir`ve `sl`) çalıştırın. (Çözüm çözümü klasöründeki *Otomasyon* klasöründe bulunur.) Dizin adlarından herhangi biri boşluk içeriyorsa, yolu tırnak içine alın. Örneğin, `c:\Sample Apps\FixIt\Automation` dizinine gitmek için aşağıdaki komutu girebilirsiniz:

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. Windows PowerShell 'in bu betikleri çalıştırmasına izin vermek için, [Engellemeyi kaldır-File](https://go.microsoft.com/fwlink/p/?linkid=294021) cmdlet 'ini kullanın. (Internet 'ten indirilen betikler engellenir.)

    > [!WARNING]
    > Güvenlik-herhangi bir betik veya yürütülebilir dosya üzerinde `Unblock-File` çalıştırmadan önce, dosyayı Not defteri 'nde açın, komutları inceleyin ve kötü amaçlı kodlar içermediğini doğrulayın.

    Örneğin, aşağıdaki komut, geçerli dizindeki tüm betiklerin `Unblock-File` cmdlet 'ini çalıştırır.

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. Temel için Web uygulaması oluşturmak için (kuyruk işleme yok) BT uygulamasını onarın, ortam oluşturma betiği çalıştırın.

    Gerekli `Name` parametresi, veritabanının adını belirtir ve ayrıca betiğin oluşturduğu depolama hesabı için de kullanılır. Ad, azurewebsites.net etki alanı içinde genel olarak benzersiz olmalıdır. Armadeğer veya test gibi benzersiz olmayan bir ad belirtirseniz (ya da örnek, fixitdemo), `New-AzureWebsite` cmdlet 'i bir çakışmayı raporlayan Iç hata ile başarısız olur. Betik, Web Apps, depolama hesapları ve veritabanlarının ad gereksinimleriyle uyumlu olması için adı tüm küçük harfe dönüştürür.

    Gerekli `SqlDatabasePassword` parametresi, SQL veritabanı için oluşturulacak yönetici hesabının parolasını belirtir. Parolada özel XML karakterleri eklemeyin (&amp; &lt; &gt;;). Bu, betiklerin yazıldığı, Azure 'un sınırlandırılmasıyla sınırlı bir kısıtlamadır.

    Örneğin, "fixitdemo" adlı bir Web uygulaması oluşturmak ve "Passw0rd1" SQL Server yönetici parolasını kullanmak istiyorsanız, aşağıdaki komutu girebilirsiniz:

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    Ad, azurewebsites.net etki alanında benzersiz olmalıdır ve parolanın, parola karmaşıklığı için SQL veritabanı gereksinimlerini karşılaması gerekir. (Örnek Passw0rd1, gereksinimleri karşılar.)

    Komutun "ile başladığını unutmayın.\". Betiklerin kötü amaçlı olarak yürütülmesini önlemeye yardımcı olmak için, Windows PowerShell bir betiği çalıştırdığınızda betik dosyasının tam yolunu sağlamanızı gerektirir. Geçerli dizini (") göstermek için bir nokta kullanabilirsiniz.\") veya tam yolu sağlayın, örneğin:

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    Betik hakkında daha fazla bilgi için `Get-Help` cmdlet 'ini kullanın.

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    Döndürülen yardımı filtrelemek için Get-Help cmdlet 'inin `Detailed`, `Full`, `Parameters`ve `Examples` parametrelerini kullanabilirsiniz.

    Komut dosyası başarısız olursa veya "New-AzureWebsite: Call set-Azuyeniden gönderiliyor ve Select-Azuyeniden komut adı" gibi hatalar oluşturursa, Azure PowerShell yapılandırmasını tamamlamadıysanız.

    Betik tamamlandıktan sonra, [her şeyi otomatikleştirin](automate-everything.md) bölümünde gösterildiği gibi, oluşturulan kaynakları görmek için Azure yönetim portalı kullanabilirsiniz.
10. Yeni Azure ortamına FixIt projesini dağıtmak için *AzureWebsite. ps1* betiğini kullanın. Örneğin:

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    Dağıtım tamamlandığında, tarayıcı Azure 'da çalışan düzeltmeyle birlikte açılır.

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a>Windows PowerShell betiklerinin sorunlarını giderme

Bu betikler çalıştırılırken karşılaşılan en yaygın hatalar izinlerle ilgilidir. `Add-AzureAccount` ve `Import-AzurePublishSettingsFile` başarılı olduğundan ve aynı Azure aboneliği için kullandığınızdan emin olun. `Add-AzureAccount` başarılı olsa bile, yeniden çalıştırmanız gerekebilir. `Add-AzureAccount` tarafından eklenen izinler 12 saat içinde sona erer.

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a>Nesne başvurusu bir nesnenin örneğine ayarlanmadı.

Betik, "nesne başvurusu bir nesnenin örneğine ayarlanmadı" gibi hatalar döndürürse, Windows PowerShell 'in işlenecek bir nesne bulamadığı (Bu null başvuru özel durumu) anlamına gelir, `Add-AzureAccount` cmdlet 'ini çalıştırın ve betiği yeniden deneyin.

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a>InternalError: sunucu bir iç hatayla karşılaştı.

`New-AzureWebsite` cmdlet 'i, ad azurewebsites.net etki alanında benzersiz olmadığında bir iç hata döndürür. Hatayı gidermek için, ad için *New-AzureWebsiteEnv. ps1*adlı ad parametresinde bulunan farklı bir değer kullanın.

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a>Betiği yeniden başlatma

*New-AzureWebsiteEnv. ps1* betiğini, "betiği tamamlanmıştır" iletisini yazdırmadan önce başarısız olduğu için yeniden başlatmanız gerekiyorsa, komut dosyasının durdurulmadan önce oluşturduğu kaynakları silmek isteyebilirsiniz. Örneğin, komut dosyası ContosoFixItDemo Web uygulamasını zaten oluşturduysanız ve betiği aynı adla yeniden çalıştırırsanız, ad kullanımda olduğundan komut dosyası başarısız olur.

Komut dosyasının durdurulmadan önce oluşturduğu kaynakları öğrenmek için aşağıdaki cmdlet 'leri kullanın:

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- `Get-AzureSqlDatabase`: Bu cmdlet 'i çalıştırmak Için veritabanı sunucusu adını `Get-AzureSqlDatabase`olarak kanal: `Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`

Bu kaynakları silmek için aşağıdaki komutları kullanın. Veritabanı sunucusunu silerseniz, sunucusuyla ilişkili veritabanlarını otomatik olarak sildiğini unutmayın.

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a>Azure App Service Web Apps ve Azure bulut hizmeti için kuyruk işleme ile uygulamayı dağıtma

Kuyrukları etkinleştirmek için MyFixIt\Web.config dosyasında aşağıdaki değişikliği yapın. `appSettings`altında, `UseQueues` değerini "true" olarak değiştirin:

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

Daha [önce](#deploybase)açıklandığı gıbı, MVC uygulamasını Azure App Service bir Web uygulamasına dağıtın.

Sonra yeni bir Azure bulut hizmeti oluşturun. BT BT uygulamasına dahil olan betikler bulut hizmetini oluşturmaz veya dağıtmaz, bu nedenle Azure portal kullanmanız gerekir. Portalda **yeni** -- **Işlem** – **bulut hizmeti** -- **hızlı oluştur**' a tıklayın ve ardından bir URL ve veri merkezi konumu girin. Web uygulamasını dağıttığınız veri merkezini kullanın.

![](the-fix-it-sample-application/_static/image1.png)

Bulut hizmetini dağıtabilmeniz için önce bazı yapılandırma dosyalarını güncelleştirmeniz gerekir.

MyFixIt. Workerrole\app.exe içinde, `connectionStrings`altında `appdb` bağlantı dizesinin değerini SQL veritabanının gerçek bağlantı dizesiyle değiştirin. Bağlantı dizesini portaldan alabilirsiniz. Portalda **SQL veritabanları** - **appdb** - ' e tıklayın **ve ADO .net, ODBC, php ve JDBC Için SQL veritabanı bağlantı dizelerini görüntüleyin**. ADO.NET bağlantı dizesini kopyalayın ve değeri App. config dosyasına yapıştırın. "{\_parolanız\_}" yerine veritabanı parolanızı yazın. (MVC uygulamasını dağıtmak için betikleri kullandığınız varsayılarak, `SqlDatabasePassword` betik parametresinde veritabanı parolasını belirttiniz.)

Sonuç aşağıdaki gibi görünmelidir:

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

Aynı MyFixIt. Workerrole\app,config dosyasında, `appSettings`altında, Azure depolama hesabı için iki yer tutucu değerini değiştirin.

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

Portaldan erişim anahtarını edinebilirsiniz. Bkz. [depolama hesaplarını yönetme](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account).

MyFixItCloudService\ServiceConfiguration.Cloud.cscfg ' de, Azure depolama hesabı için aynı iki yer tutucu değerini değiştirin.

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

Artık bulut hizmetini dağıtmaya hazırsınız. Çözüm araştırırken, MyFixItCloudService projesine sağ tıklayın ve **Yayımla**' yı seçin. Daha fazla bilgi için, [Bu öğreticinin](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)2. bölümünde olan "[uygulamayı Azure 'a dağıtma](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)" bölümüne bakın.

> [!div class="step-by-step"]
> [Öncekini](more-patterns-and-guidance.md)
