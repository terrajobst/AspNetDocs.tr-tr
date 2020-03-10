---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: ASP.NET 4,5 ve Visual Studio 2012 ' deki yenilikler | Microsoft Docs
author: rick-anderson
description: Bu belge, ASP.NET 4,5 ' de tanıtılan yeni özellikleri ve geliştirmeleri açıklamaktadır. Ayrıca Web geliştirme için yapılan geliştirmeleri açıklar...
ms.author: riande
ms.date: 02/29/2012
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: 32fbf7c25b00f3f0796c4c3fdd38ca2a86c89199
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78526679"
---
# <a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a>ASP.NET 4.5 ve Visual Studio 2012’deki Yenilikler

> Bu belge, ASP.NET 4,5 ' de tanıtılan yeni özellikleri ve geliştirmeleri açıklamaktadır. Ayrıca, Visual Studio 2012 ' de Web geliştirme için yapılan geliştirmeleri açıklar. Bu belge ilk olarak 29 Şubat 2012 tarihinde yayımlandı.

- [Çalışma zamanı ve Framework 'Ü ASP.NET Core](#_Toc318097372)

    - [HTTP Isteklerini ve yanıtlarını zaman uyumsuz olarak okuma ve yazma](#_Toc318097373)
    - [HttpRequest işleme geliştirmeleri](#_Toc318097374)
    - [Zaman uyumsuz olarak bir yanıtı Temizleme](#_Toc318097375)
    - [*Await* ve *görev*tabanlı zaman uyumsuz modüller ve işleyiciler için destek](#_Toc318097376)
    - [Zaman uyumsuz HTTP modülleri](#_Toc318097377)
    - [Zaman uyumsuz HTTP işleyicileri](#_Toc318097378)
    - [Yeni ASP.NET Isteği doğrulama özellikleri](#_Toc318097379)
    - [Ertelenmiş ("Lazy") istek doğrulaması](#_Toc318097380)
    - [Doğrulanmamış istekler için destek](#_Toc318097381)
    - [AntiXSS Kitaplığı](#_Toc318097382)
    - [WebSockets protokolü desteği](#_Toc318097383)
    - [Paketleme ve Küçültme](#_Toc318097384)
    - [Web barındırma için performans Iyileştirmeleri](#_Toc_perf)

        - [Ana performans faktörleri](#_Toc_perf_1)
        - [Yeni performans özellikleri için gereksinimler](#_Toc_perf_2)
        - [Ortak derlemeleri paylaşma](#_Toc_perf_3)
        - [Daha hızlı başlangıç için çok çekirdekli JıT derlemesini kullanma](#_Toc_perf_4)
        - [Belleği iyileştirmek için çöp toplamayı ayarlama](#_Toc_perf_5)
        - [Web uygulamaları için önceden getirme](#_Toc_perf_6)
- [ASP.NET Web Forms](#_Toc318097385)

    - [Kesin Türü Belirtilmiş Veri Denetimleri](#_Toc318097386)
    - [Model Bağlamaları](#_Toc318097387)

        - [Veri seçme](#_Toc318097388)
        - [Değer sağlayıcıları](#_Toc318097389)
        - [Bir denetimden değerlere göre filtreleme](#_Toc318097390)
    - [HTML kodlamalı veri bağlama Ifadeleri](#_Toc318097391)
    - [Unobtrusive doğrulaması](#_Toc318097392)
    - [HTML5 güncelleştirmeleri](#_Toc318097393)
- [ASP.NET MVC 4](#_Toc318097394)
- [ASP.NET Web sayfaları 2](#_Toc318097395)
- [Visual Studio 2012 sürüm adayı](#_Toc318097396)

    - [Visual Studio 2010 ile Visual Studio 2012 sürüm adayı (proje uyumluluğu) arasında proje paylaşımı](#project-compatibility)
    - [ASP.NET 4,5 Web sitesi şablonlarındaki yapılandırma değişiklikleri](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [ASP.NET yönlendirme için IIS 7 ' de yerel destek](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [HTML Düzenleyicisi](#_Toc318097397)

        - [Akıllı görevler](#_Toc318097398)
        - [WAı-ARIA desteği](#_Toc318097399)
        - [Yeni HTML5 parçacıkları](#_Toc318097400)
        - [Kullanıcı denetimine Ayıkla](#_Toc318097401)
        - [Kod nugal için IntelliSense özniteliklere](#_Toc318097402)
        - [Bir açılış veya kapanış etiketini yeniden adlandırdığınızda eşleşen etiketin otomatik olarak yeniden adlandırılması](#_Toc318097403)
        - [Olay işleyicisi oluşturma](#_Toc318097404)
        - [Akıllı girinti](#_Toc318097405)
        - [Deyimin tamamlanmasını otomatik azalt](#_Toc318097406)
    - [JavaScript Düzenleyicisi](#_Toc318097407)

        - [Kod anahat oluşturma](#_Toc318097408)
        - [Ayraç eşleştirme](#_Toc318097409)
        - [Tanıma Git](#_Toc318097410)
        - [ECMAScript5 desteği](#_Toc318097411)
        - [DOM IntelliSense](#_Toc318097412)
        - [VSDOC imza aşırı yüklemeleri](#_Toc318097413)
        - [Örtük başvurular](#_Toc318097414)
    - [CSS Düzenleyicisi](#_Toc318097415)

        - [Deyimin tamamlanmasını otomatik azalt](#_Toc318097416)
        - [Hiyerarşik girintileme.](#_Toc318097417)
        - [CSS Hacks desteği](#_Toc318097418)
        - [Satıcıya özgü şemalar (-Moz-,-WebKit)](#_Toc318097419)
        - [Açıklama ekleme ve açıklama kaldırma desteği](#_Toc318097420)
        - [Renk seçici](#_Toc318097421)
        - [Kod Parçacıkları](#_Toc318097422)
        - [Özel bölgeler](#_Toc318097423)
    - [Sayfa denetçisi](#_Toc318097424)
    - [Yayımlama](#_Toc318097425)

        - [Yayımlama profilleri](#_Toc318097426)
        - [ASP.NET ön derleme ve birleştirme](#_Toc318097427)
- [IIS Express](#_Toc318097428)
- [Sorumluluk reddi](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a>Çalışma zamanı ve Framework 'Ü ASP.NET Core

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a>HTTP Isteklerini ve yanıtlarını zaman uyumsuz olarak okuma ve yazma

ASP.NET 4, bir HTTP isteği varlığını *HttpRequest. GetBufferlessInputStream* yöntemini kullanarak akış olarak okuma yeteneği getirmiştir. Bu yöntem, istek varlığına akış erişimi sağladı. Ancak, bir istek süresince iş parçacığını bağlayan zaman uyumlu olarak yürütülür.

ASP.NET 4,5, bir HTTP istek varlığında zaman uyumsuz akışları okuma ve zaman uyumsuz olarak temizleme olanağını destekler. ASP.NET 4,5 Ayrıca,. aspx sayfa işleyicileri ve ASP.NET MVC denetleyicileri gibi aşağı akış HTTP işleyicileriyle daha kolay tümleştirme sağlayan bir HTTP isteği varlığını çift arabelleğe alma olanağı sağlar.

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a>HttpRequest işleme geliştirmeleri

*HttpRequest. GetBufferlessInputStream* öğesinden ASP.NET 4,5 tarafından döndürülen akış başvurusu hem zaman uyumlu hem de zaman uyumsuz okuma yöntemlerini destekler. *GetBufferlessInputStream* 'Den döndürülen *Stream* nesnesi şimdi BeginRead ve EndRead yöntemlerini uyguluyor. Zaman uyumsuz *akış* yöntemleri, bir zaman uyumsuz okuma döngüsünün her yinelemesi arasında geçerli iş parçacığını yayınlarken, ASP.NET istek varlığı öbeklerini zaman uyumsuz olarak okuduğunuzdan izin verir.

ASP.NET 4,5, istek varlığını arabelleğe alınmış bir şekilde okumak için bir yardımcı yöntem de ekledi: *HttpRequest. GetBufferedInputStream çağrıldıktan*. Bu yeni aşırı yükleme, hem zaman uyumlu hem de zaman uyumsuz okumaları destekleyen *GetBufferlessInputStream*gibi çalışmaktadır. Ancak, *GetBufferedInputStream çağrıldıktan* , Ayrıca, aşağı akış modüllerinin ve işleyicilerinin istek varlığına erişmeye devam edebilmesi için varlık baytlarını ASP.NET iç arabelleklerine kopyalar. Örneğin, işlem hattındaki bazı yukarı akış kodu *GetBufferedInputStream çağrıldıktan*kullanarak istek varlığını zaten okuduysa, *HttpRequest. form* veya *HttpRequest. Files*kullanmaya devam edebilirsiniz. Bu, bir istekte zaman uyumsuz işleme gerçekleştirmenizi sağlar (örneğin, bir veritabanına büyük bir dosya yükleme akışı), ancak yine de. aspx sayfalarını ve MVC ASP.NET denetleyicilerini çalıştırın.

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a>Zaman uyumsuz olarak bir yanıtı Temizleme

HTTP istemcisine Yanıt gönderilmesi, istemcinin uzakta olduğu veya düşük bant genişliğine sahip bir bağlantıya sahip olması önemli ölçüde zaman alabilir. Normalde ASP.NET, yanıt baytlarını bir uygulama tarafından oluşturuldukları şekilde arabelleğe alır. ASP.NET ardından, istek işlemenin çok sonunda, tahakkuk eden arabelleklerin tek bir gönderme işlemini gerçekleştirir.

Arabelleğe alınan yanıt büyükse (örneğin, bir istemciye büyük bir dosya akışı), istemciye arabelleğe alınmış çıkış göndermek ve denetim altında bellek kullanımını tutmak için *HttpResponse. Flush* 'yi düzenli olarak çağırmanız gerekir. Ancak, *Temizleme* zaman uyumlu bir çağrı olduğundan, *Yinelenekli çağırma Temizleme* , uzun süreli isteklerin süresi için bir iş parçacığı kullanır.

ASP.NET 4,5, *HttpResponse* sınıfının *BeginFlush* ve *EndFlush* yöntemlerini kullanarak zaman uyumsuz olarak temizlemeleri gerçekleştirmeye yönelik destek ekler. Bu yöntemleri kullanarak, işletim sistemi iş parçacıklarını bağlamadan bir istemciye artımlı olarak veri gönderebilen zaman uyumsuz modüller ve zaman uyumsuz işleyiciler oluşturabilirsiniz. *BeginFlush* Ile *EndFlush* çağrıları arasında ASP.net, geçerli iş parçacığını yayınlar. Bu, uzun süre çalışan HTTP indirmelerini desteklemek için gereken toplam etkin iş parçacığı sayısını önemli ölçüde azaltır.

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a>*Await* ve *görev* tabanlı zaman uyumsuz modüller ve işleyiciler için destek

.NET Framework 4, *görev*olarak adlandırılan zaman uyumsuz programlama kavramını sunmuştur. Görevler, *görev* türü ve *System. Threading. Tasks* ad alanındaki ilgili türler tarafından temsil edilir. .NET Framework 4,5, *görev* nesneleriyle daha basit bir şekilde çalışmayı sağlayan derleyici geliştirmeleriyle bu sayfada derleme yapar. .NET Framework 4,5 ' de, derleyiciler iki yeni anahtar sözcüğü destekler: *await* ve *Async*. *Await* anahtar sözcüğü, kod parçasının zaman uyumsuz olarak başka bir kod parçasına beklemesi gerektiğini belirten sözdizimsel bir toplu özelliktir. *Async* anahtar sözcüğü, yöntemleri görev tabanlı zaman uyumsuz yöntemler olarak işaretlemek için kullanabileceğiniz bir ipucunu temsil eder.

*Await*, *Async*ve *Task* nesnesinin birleşimi, .NET 4,5 'e zaman uyumsuz kod yazmanızı çok daha kolay hale getirir. ASP.NET 4,5, yeni derleyici geliştirmelerini kullanarak zaman uyumsuz HTTP modülleri ve zaman uyumsuz HTTP işleyicileri yazmanıza olanak tanıyan yeni API 'Ler ile bu basitleştirmeleri destekler.

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a>Zaman uyumsuz HTTP modülleri

Bir *görev* nesnesi döndüren bir yöntem içinde zaman uyumsuz çalışma gerçekleştirmek istediğinizi varsayalım. Aşağıdaki kod örneği, Microsoft giriş sayfasını indirmek için zaman uyumsuz bir çağrı yapan zaman uyumsuz bir yöntemi tanımlar. Yöntem imzasında *Async* anahtar sözcüğünün ve *DownloadStringTaskAsync*için *await* çağrısının kullanımına dikkat edin.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

Tüm yazmanız gereken — .NET Framework, indirme işleminin tamamlanmasını beklerken çağrı yığınını otomatik olarak işleyecek ve indirme yapıldıktan sonra çağrı yığınını otomatik olarak geri yükleyecek.

Artık bu zaman uyumsuz yöntemi bir zaman uyumsuz ASP.NET HTTP modülünde kullanmak istediğinizi varsayalım. ASP.NET 4,5, görev tabanlı zaman uyumsuz yöntemleri ASP.NET HTTP işlem hattı tarafından kullanıma sunulan eski zaman uyumsuz programlama modeliyle tümleştirmede kullanabileceğiniz bir yardımcı yöntemi (*EventHandlerTaskAsyncHelper*) ve yeni bir temsilci türü (*TaskEventHandler*) içerir. Bu örnekte nasıl yapılacağı gösterilmektedir:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a>Zaman uyumsuz HTTP işleyicileri

ASP.NET ' de zaman uyumsuz işleyiciler yazmak için geleneksel yaklaşım *IHttpAsyncHandler* arabirimini uygulamaktır. ASP.NET 4,5, öğesinden türetilebilir *HttpTaskAsyncHandler* zaman uyumsuz temel türünü tanıtır, bu, zaman uyumsuz işleyicileri yazmayı çok daha kolay hale getirir.

*HttpTaskAsyncHandler* türü soyuttur ve *ProcessRequestAsync* metodunu geçersiz kılmanızı gerektirir. Dahili ASP.NET, *ProcessRequestAsync* 'ın dönüş imzasını (bir *görev* nesnesi) ASP.NET işlem hattı tarafından kullanılan eski zaman uyumsuz programlama modeliyle tümleştirmeyle ilgileniyor.

Aşağıdaki örnek, zaman uyumsuz HTTP işleyicisi uygulamasının bir parçası olarak *görevi* ve *await* 'yi nasıl kullanabileceğinizi gösterir:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a>Yeni ASP.NET Isteği doğrulama özellikleri

Varsayılan olarak, ASP.NET istek doğrulaması gerçekleştirir; alanlarda, başlıklarında ve tanımlama bilgilerinde biçimlendirme veya betiği aramak için istekleri inceler. Herhangi biri algılanırsa, ASP.NET bir özel durum oluşturur. Bu, olası siteler arası betik saldırılarına karşı ilk savunma hattı görevi görür.

ASP.NET 4,5, doğrulanmamış istek verilerini seçmeli olarak okumayı kolaylaştırır. ASP.NET 4,5, daha önce bir dış kitaplık olan popüler AntiXSS kitaplığını de tümleştirir.

Geliştiriciler, genellikle uygulamaları için istek doğrulamayı seçmeli olarak kapatma özelliğini istedi. Örneğin, uygulamanız Forum yazılımtıysa, kullanıcıların HTML biçimli Forum yayınlarını ve açıklamalarını göndermesine izin vermek isteyebilirsiniz, ancak yine de istek doğrulamasının diğer her şeyi kontrol ettiğinden emin olabilirsiniz.

ASP.NET 4,5, doğrulanmamış giriş ile seçmeli olarak çalışmanızı kolaylaştıran iki özellik sunar: ertelenmiş ("Lazy") istek doğrulaması ve doğrulanmamış istek verilerine erişim.

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a>Ertelenmiş ("Lazy") istek doğrulaması

ASP.NET 4,5 ' de, varsayılan olarak tüm istek verileri istek doğrulamasına tabidir. Ancak, istek verilerine gerçekten erişene kadar uygulamayı istek doğrulamayı erteleyin. (Bu bazen, belirli veri senaryoları için yavaş yükleme gibi koşullara bağlı olarak yavaş istek doğrulaması olarak adlandırılır.) Aşağıdaki örnekte olduğu gibi, aşağıdaki örnekte olduğu gibi, bir uygulamayı, Web. config dosyasında, *istek onaylama modu* özniteliğini, *httpRUntime* öğesinde 4,5 olarak ayarlayarak, ertelenmiş doğrulamayı kullanacak şekilde yapılandırabilirsiniz:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

İstek doğrulama modu 4,5 olarak ayarlandığında, istek doğrulaması yalnızca belirli bir istek değeri ve yalnızca kodunuz bu değere eriştiğinde tetiklenir. Örneğin, kodunuz Isteğin değerini alıyorsa. form ["Forum\_Post"], istek doğrulaması yalnızca form koleksiyonundaki bu öğe için çağırılır. *Form* koleksiyonundaki diğer öğelerin hiçbiri doğrulanmadı. Önceki ASP.NET sürümlerinde, koleksiyondaki herhangi bir öğeye erişildiği zaman tüm istek koleksiyonu için istek doğrulaması tetiklendi. Yeni davranış, farklı uygulama bileşenlerinin diğer parçalar üzerinde istek doğrulaması tetiklemeden farklı veri parçalarına bakmayı kolaylaştırır.

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a>Doğrulanmamış istekler için destek

Ertelenmiş istek doğrulaması tek başına isteğe bağlı istek doğrulamasını atlama sorununu çözmez. Request. form ["Forum\_Post"] çağrısı, bu belirli istek değeri için istek doğrulamasını hala tetikler. Ancak, bu alana, bu alanda biçimlendirmeye izin vermek istediğiniz için doğrulamayı tetiklemeden erişmek isteyebilirsiniz.

Buna izin vermek için, ASP.NET 4,5 artık istek verilerine yönelik doğrulanmamış erişimi desteklemektedir. ASP.NET 4,5, *HttpRequest* sınıfında yeni *doğrulanmamış* bir koleksiyon özelliği içerir. Bu koleksiyon, istek verilerinin *form*, *QueryString*, *tanımlama bilgileri*ve *URL*gibi tüm ortak değerlerine erişim sağlar.

Forum örneğini kullanarak, doğrulanmamış istek verilerini okuyabilmeniz için önce uygulamayı yeni istek doğrulama modunu kullanacak şekilde yapılandırmanız gerekir:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

Daha sonra, doğrulanmamış form değerini okumak için *HttpRequest. undoğrulanabilen* özelliğini kullanabilirsiniz:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]

> [!WARNING]
> Güvenlik- *doğrulanmamış istek verilerini dikkatli kullanın!* ASP.NET 4,5, kimliği doğrulanmamış istek özellikleri ve koleksiyonlar eklenerek, çok özel doğrulanmamış istek verilerine erişmenizi kolaylaştırır. Ancak, tehlikeli metnin kullanıcılara işlenmemesini sağlamak için ham istek verilerinde özel doğrulama gerçekleştirmeniz gerekir.

<a id="_Toc318097382"></a>
### <a name="antixss-library"></a>AntiXSS Kitaplığı

ASP.NET 4,5, Microsoft AntiXSS Kitaplığı 'nın popülerliği nedeniyle bu kitaplığın 4,0 sürümünden temel kodlama yordamlarını içerir.

Kodlama yordamları, yeni *System. Web. Security. AntiXss* ad alanındaki *AntiXssEncoder* türü tarafından uygulanır. Türünde uygulanan statik kodlama yöntemlerinden herhangi birini çağırarak, *AntiXssEncoder* türünü doğrudan kullanabilirsiniz. Ancak, yeni XSS önleme yordamlarını kullanmanın en kolay yaklaşımı, bir ASP.NET uygulamasını *AntiXssEncoder* sınıfını varsayılan olarak kullanacak şekilde yapılandırmaktır. Bunu yapmak için, Web. config dosyasına aşağıdaki özniteliği ekleyin:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

*EncoderType* özniteliği, *AntiXssEncoder* türünü kullanacak şekilde ayarlandığında, ASP.NET içindeki tüm çıkış kodlaması otomatik olarak yeni kodlama yordamlarını kullanır.

Bu, ASP.NET 4,5 'e eklenmiş dış AntiXSS Kitaplığı 'nın kısımlardır:

- *HtmlEncode*, *HtmlFormUrlEncode*ve *HtmlAttributeEncode*
- *XmlAttributeEncode* ve *XmlEncode*
- *Urlencode* ve *UrlPathEncode* (yeni)
- *CssEncode*

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a>WebSockets protokolü desteği

WebSockets protokolü, bir istemci ile HTTP üzerinden sunucu arasında güvenli, gerçek zamanlı çift yönlü iletişimin nasıl oluşturulacağını tanımlayan standart tabanlı bir ağ protokolüdür. Microsoft, protokolü tanımlamaya yardımcı olmak için hem IETF hem de W3C standartları gövdeleriyle birlikte çalışmıştır. WebSockets protokolü, Microsoft 'un hem istemci hem de mobil işletim sistemlerinde WebSockets protokolünü destekleyen önemli kaynaklara sahip olan tüm istemciler tarafından (yalnızca tarayıcılar değil) desteklenir.

WebSockets protokolü, istemci ve sunucu arasında uzun süre çalışan veri aktarımları oluşturmayı çok daha kolay hale getirir. Örneğin, bir istemci ile sunucu arasında gerçek zamanlı bir bağlantı kurabildiğimizde bir sohbet uygulaması yazmak çok daha kolay. Bir yuva davranışının benzetimini yapmak için düzenli yoklama veya HTTP uzun yoklama gibi geçici çözümlere izin almanız gerekmez.

ASP.NET 4,5 ve IIS 8, bir WebSockets nesnesi üzerinde zaman uyumsuz olarak okumak ve hem dize hem de ikili verileri yazmak için yönetilen API 'Leri kullanmasını sağlayan alt düzey WebSockets desteğini içerir. ASP.NET 4,5 için, WebSockets protokolüyle çalışma türlerini içeren yeni bir *System. Web. WebSockets* ad alanı vardır.

Tarayıcı istemcisi, aşağıdaki örnekte olduğu gibi bir ASP.NET uygulamasındaki URL 'yi işaret eden bir DOM *WebSocket* nesnesi oluşturarak WebSockets bağlantısı kurar:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

Herhangi bir tür modül veya işleyici kullanarak, ASP.NET 'de WebSockets uç noktaları oluşturabilirsiniz. Önceki örnekte,. ashx dosyaları bir işleyici oluşturmanın hızlı bir yolu olduğundan, bir. ashx dosyası kullanılmıştır.

WebSockets protokolüne göre, bir ASP.NET uygulaması isteğin bir HTTP GET isteğinden WebSockets isteğine yükseltilmesi gerektiğini belirten bir istemcinin WebSockets isteğini kabul eder. Örnek buradadır:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

*AcceptWebSocketRequest* yöntemi bir işlev temsilcisini kabul eder çünkü ASP.net, geçerli http isteğini kaldırır ve sonra denetimi işlev temsilcisine aktarır. Kavramsal olarak bu yaklaşım, arka plan işinin gerçekleştirildiği bir iş parçacığı başlatma temsilcisini tanımladığınız *System. Threading. Thread*' i kullanmanıza benzer.

ASP.NET ve istemci bir WebSockets anlaşmasını başarıyla tamamladıktan sonra, ASP.NET temsilcinizi çağırır ve WebSockets uygulaması çalışmaya başlar. Aşağıdaki kod örneği, ASP.NET içinde yerleşik WebSockets desteğini kullanan basit bir yankı uygulaması göstermektedir:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

*Await* anahtar sözcüğü ve zaman uyumsuz görev tabanlı işlemler için .NET 4,5 desteği, WebSockets uygulamalarını yazmaya yönelik doğal bir uyum. Kod örneği, WebSockets isteğinin ASP.NET içinde tamamen zaman uyumsuz çalıştığını gösterir. Uygulama, await yuvasını çağırarak bir istemciden bir iletinin gönderilmesini zaman uyumsuz olarak bekler *. ReceiveAsync*. Benzer şekilde, await yuvasını çağırarak bir istemciye zaman uyumsuz bir ileti gönderebilirsiniz *. Sendadsync*.

Tarayıcıda, bir uygulama *OnMessage* Işlevi aracılığıyla WebSockets iletileri alır. Bir tarayıcıdan ileti göndermek için aşağıdaki örnekte gösterildiği gibi *WebSocket* Dom türünün *Send* yöntemini çağırın:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

Gelecekte bu işlevselliğe, WebSockets uygulamaları için bu sürümde gerekli olan bazı düşük düzey kodlarınızdan bazılarının soyutlamasına yönelik güncelleştirmeler yayınlarız.

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a>Paketleme ve Küçültme

Paketleme, bireysel JavaScript ve CSS dosyalarını tek bir dosya gibi davranılan bir pakette birleştirmenizi sağlar. Minbirleşme, boşluk ve gerekli olmayan diğer karakterleri kaldırarak JavaScript ve CSS dosyalarını daraltabilir. Bu özellikler Web Forms, ASP.NET MVC ve Web sayfalarıyla çalışır.

Paketler, paket sınıfı veya alt sınıflarından biri olan Scriptdemeti ve Stildemeti kullanılarak oluşturulur. Bir paketin örneğini yapılandırdıktan sonra, paket yalnızca genel bir paketleme Licollection örneğine eklenerek gelen istekler için kullanılabilir hale getirilir. Varsayılan şablonlarda, paket yapılandırması bir paketleme Liconfig dosyasında gerçekleştirilir. Bu varsayılan yapılandırma, şablonlar tarafından kullanılan tüm çekirdek betikler ve CSS dosyaları için bir paket oluşturur.

Paketlerdeki paketleri, birkaç olası yardımcı yöntemden birini kullanarak görünümler içerisinden başvurulur. Hata ayıklama ve sürüm modundayken bir paket için farklı biçimlendirme işlemeyi desteklemek amacıyla, Scriptdemeti ve Styledemeti sınıflarının yardımcı yöntemi, render ' dir. Hata ayıklama modundayken render, paketteki her kaynak için biçimlendirme oluşturacaktır. Yayın modundayken, Işleme tüm paket için tek bir biçimlendirme öğesi oluşturur. Web. config dosyasındaki derleme öğesinin hata ayıklama özniteliği aşağıda gösterildiği gibi değiştirilerek hata ayıklama ve yayın modu arasında geçiş yapılabilir:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

Ayrıca, iyileştirmenin etkinleştirilmesi veya devre dışı bırakılması doğrudan paketleme Litable. Enableiyileştirmeler özelliği aracılığıyla ayarlanabilir.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

Dosyalar gruplandırılabildiklerinde, ilk başta alfabetik olarak sıralanır ( **Çözüm Gezgini**olarak görüntülendikleri şekilde). Daha sonra, bilinen kitaplıkların ve özel uzantılarının (jQuery, MooTools ve Dojo gibi) önce yüklenmesi için düzenlenir. Örneğin, yukarıda gösterildiği gibi betikler klasörünün paketlemeye ilişkin son sıra şöyle olacaktır:

1. jQuery-1.6.2. js
2. jQuery-ui. js
3. jQuery. Tools. js
4. a. js

CSS dosyaları da alfabetik olarak sıralanır ve sonra Reset. css ve normal. css diğer herhangi bir dosyadan önce gelmelidir. Yukarıda gösterilen stiller klasörü için paketleme son sıralaması bu olacaktır:

1. . css 'yi Sıfırla
2. Content. css
3. Forms. css
4. Globals. css
5. menü. css
6. Styles. css

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a>Web barındırma için performans Iyileştirmeleri

.NET Framework 4,5 ve Windows 8, Web-Server iş yükleri için önemli bir performans artışı elde etmenize yardımcı olabilecek özellikler sunar. Buna bir azaltma dahildir (en fazla %35) hem başlangıç zamanında hem de ASP.NET kullanan Web barındırma sitelerinin bellek parmak izine.

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a>Ana performans faktörleri

İdeal olarak, bir sonraki isteğe hızlı yanıt sağlamak için tüm Web sitelerinin etkin ve bellekte olması gerekir. Site yanıt hızını etkileyebilecek faktörler şunlardır:

- Bir uygulama havuzu geri dönüştürüldüğünde bir sitenin yeniden başlatılması için gereken süre. Bu, site derlemeleri artık bellekte olmadığında site için bir Web sunucusu işlemini başlatmak için gereken süredir. (Platform derlemeleri başka siteler tarafından kullanıldıklarından hala bellekte bulunur.) Bu durum "soğuk site, normal çerçeve başlatma" veya yalnızca "soğuk site başlatma" olarak adlandırılır.
- Sitenin kapladığı bellek miktarı. Bu koşulların "site başına bellek kullanımı" veya "paylaşılmayan çalışma kümesi" olması.

Yeni performans geliştirmeleri Bu faktörlerin her ikisinde de odaklanılmıştır.

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a>Yeni performans özellikleri için gereksinimler

Yeni özellikler için gereksinimler şu kategorilere ayrılabilir:

- .NET Framework 4 üzerinde çalışan geliştirmeler.
- .NET Framework 4,5 gerektiren, ancak herhangi bir Windows sürümünde çalışabilen geliştirmeler.
- Yalnızca Windows 8 üzerinde çalışan .NET Framework 4,5 ile kullanılabilen geliştirmeler.

Performans arttıkça, etkinleştirebileceğiniz her geliştirme düzeyi artar.

Bazı .NET Framework 4,5 geliştirmeleri, diğer senaryolar için de uygulanan daha geniş performans özelliklerinden yararlanır.

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a>Ortak derlemeleri paylaşma

**Gereksinim**: .NET Framework 4 ve Visual Studio 11 Geliştirici Önizleme SDK 'sı

Bir sunucudaki farklı siteler genellikle aynı yardımcı derlemeleri (örneğin, bir başlatıcı Kit veya örnek uygulamadan derlemeler) kullanır. Her sitenin kendi bin dizininde bu derlemelerin kendi kopyası vardır. Derlemeler için nesne kodu özdeş olsa da, bunlar fiziksel olarak ayrı derlemelerdir, böylece her derlemenin soğuk site başlatması sırasında ayrı olarak okunması ve bellekte ayrı tutulması gerekir.

Yeni bir özelliği bu inefficiency çözer ve hem RAM gereksinimlerini hem de yükleme süresini azaltır. ' Nin, Windows 'un dosya sistemindeki her bir derlemenin tek bir kopyasını tutmasını sağlar ve site bin klasörlerindeki bireysel derlemeler tek kopyanın sembolik bağlantılarıyla değiştirilmiştir. Tek bir sitede derlemenin ayrı bir sürümü gerekiyorsa, sembolik bağlantı derlemenin yeni sürümü ile değiştirilmiştir ve yalnızca bu site etkilenir.

Sembolik bağlantıları kullanarak derlemeleri paylaşma, ASPNET\_Intern. exe adlı yeni bir araç gerektirir. Bu, birlikte bulunan derlemelerin mağazasını oluşturmanızı ve yönetmenizi sağlar. Visual Studio 11 Geliştirici Önizleme SDK 'sının bir parçası olarak sağlanır. (Ancak, en son [güncelleştirmeyi](https://support.microsoft.com/kb/2468871)yüklediğiniz varsayılarak yalnızca .NET Framework 4 ' ün yüklü olduğu bir sistemde çalışır.)

Tüm uygun derlemelerin sağlandığından emin olmak için, ASPNET\_Intern. exe ' yi düzenli olarak (örneğin, bir haftada bir zamanlanan görev olarak) çalıştırırsınız. Tipik bir kullanım aşağıdaki gibidir:

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

Tüm seçenekleri görmek için, aracı bağımsız değişken olmadan çalıştırın.

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a>Daha hızlı başlangıç için çok çekirdekli JıT derlemesini kullanma

**Gereksinim**: .NET Framework 4,5

Soğuk bir site başlatması için, yalnızca derleme derlemeleri diskten okunmamalıdır, ancak site JıT derlenmiş olmalıdır. Karmaşık bir site için bu, önemli gecikmeler ekleyebilir. .NET Framework 4,5 ' deki yeni bir genel amaçlı teknik, kullanılabilir işlemci çekirdekleri arasında JıT derlemesini dağıtarak bu gecikmeleri azaltır. Bu, siteyi önceki başlatma sırasında toplanan bilgileri kullanarak bu kadar çok ve mümkün olduğunca erken yapar. Bu işlevsellik [System. Runtime. Profileiyileştirmeli. StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) yöntemi tarafından uygulandı.

Birden çok çekirdek kullanarak JıT derleme, ASP.NET içinde varsayılan olarak etkindir, bu nedenle bu özellikten yararlanmak için herhangi bir şey yapmanız gerekmez. Bu özelliği devre dışı bırakmak istiyorsanız, Web. config dosyasında aşağıdaki ayarı yapın:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a>Belleği iyileştirmek için çöp toplamayı ayarlama

**Gereksinim**: .NET Framework 4,5

Bir site çalışmaya başladıktan sonra çöp toplayıcı (GC) yığınının kullanımı, bellek tüketimine göre önemli bir faktör olabilir. Herhangi bir çöp toplayıcı gibi, GC .NET Framework, CPU zamanı (koleksiyonların sıklığı ve önemi) ve bellek tüketimi (yeni, serbest bırakılmış veya serbest bırakılmış nesneler için kullanılan ek alan) arasında denge sağlar. Önceki sürümlerde, GC 'nin doğru dengeyi elde etmek için nasıl yapılandırılacağı hakkında rehberlik sunuyoruz (örneğin, bkz. [ASP.NET 2.0/3,5 paylaşılan barındırma yapılandırması](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)).

.NET Framework 4,5 için birden çok bağımsız ayar yerine, daha önce önerilen GC ayarlarının yanı sıra site başına ek performans sağlayan yeni ayarlamayı sağlayan bir iş yükü tanımlı yapılandırma ayarı vardır çalışma kümesi.

GC bellek ayarlamayı etkinleştirmek için, Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config dosyasına aşağıdaki ayarı ekleyin:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

(Aspnet. config dosyasında yapılan değişikliklere ilişkin önceki kılavuza alışkın değilseniz, bu ayarın eski ayarların yerini aldığını unutmayın; Örneğin, gcServer, gcConcurrent vb. ayarlamanız gerekmez. Eski ayarları kaldırmanız gerekmez.)

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a>Web uygulamaları için önceden getirme

**Gereksinim**: .NET Framework 4,5 Windows 8 ' de çalışıyor

Windows, çeşitli sürümler için, uygulama başlatmanın disk okuma maliyetini azaltan [Prefetcher](http://en.wikipedia.org/wiki/Prefetcher) olarak bilinen bir teknolojiyi içeriyordu. Soğuk başlatma, istemci uygulamaları için bir sorun ağırlıklı olduğundan, bu teknoloji yalnızca bir sunucu için gerekli olan bileşenleri içeren Windows Server 'a eklenmemiştir. Önceden getirme, Windows Server 'ın en son sürümünde kullanıma sunulmuştur ve burada ayrı Web sitelerinin başlatılması iyileştirebileceği için geçerlidir.

Windows Server için, Prefetcher varsayılan olarak etkinleştirilmemiştir. Yüksek yoğunluklu Web barındırma için Prefetcher 'i etkinleştirmek ve yapılandırmak için komut satırında aşağıdaki komut kümesini çalıştırın:

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

Ardından, Prefetcher ASP.NET uygulamalarıyla tümleştirmek için aşağıdakini Web. config dosyasına ekleyin:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a>ASP.NET Web Forms

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a>Kesin Türü Belirtilmiş Veri Denetimleri

ASP.NET 4,5 ' de Web Forms, verilerle çalışmaya yönelik bazı geliştirmeler içerir. İlk iyileştirme kesin türü belirtilmiş veri denetimleridir. Önceki ASP.NET sürümlerindeki Web Forms denetimleri için, *eval* ve bir veri bağlama ifadesi kullanarak veriye dayalı bir değer görüntüleriz:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

İki yönlü veri bağlama için *bağlama*kullanırsınız:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

Çalışma zamanında, bu çağrılar belirtilen üyenin değerini okumak için yansıma kullanır ve sonra sonucu İşaretlemede görüntüler. Bu yaklaşım, verileri rastgele, düzensiz verilere göre bağlamayı kolaylaştırır.

Ancak, bu gibi veri bağlama ifadeleri üye adları için IntelliSense gibi özellikleri, gezinti (tanıma git gibi) veya bu adlar için derleme zamanı denetimini desteklemez.

Bu sorunu gidermek için, ASP.NET 4,5, bir denetimin bağlandığı verilerin veri türünü bildirme yeteneğini ekler. Bunu, yeni *ItemType* özelliğini kullanarak yapabilirsiniz. Bu özelliği ayarladığınızda, veri bağlama ifadeleri kapsamında iki yeni türü belirlenmiş değişken mevcuttur: *Item* ve *BindItem*. Değişkenler kesin olarak yazıldığından, Visual Studio geliştirme deneyiminin tüm avantajlarını elde edersiniz.

İki yönlü veri bağlama ifadeleri için, *BindItem* değişkenini kullanın:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]

Veri bağlamayı destekleyen ASP.NET Web Forms çerçevesindeki denetimlerin çoğu *ItemType* özelliğini destekleyecek şekilde güncelleştirilmiştir.

<a id="_Toc318097387"></a>
### <a name="model-binding"></a>Model bağlama

Model bağlama, kod odaklı veri erişimiyle çalışmak için ASP.NET Web Forms Denetimlerinde veri bağlamayı genişletir. Bu, *ObjectDataSource* denetiminden ve ASP.NET MVC içindeki model bağlamasındaki kavramları içerir.

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a>Veri seçme

Veri seçmek üzere model bağlamayı kullanmak üzere bir veri denetimi yapılandırmak için denetimin *SelectMethod* özelliğini sayfanın kodundaki bir yöntemin adı olarak ayarlarsınız. Veri denetimi, yöntemi sayfa yaşam döngüsünde uygun zamanda çağırır ve döndürülen verileri otomatik olarak bağlar. *DataBind* metodunu açıkça çağırmanız gerekmez.

Aşağıdaki örnekte, *GridView* denetimi *GetCategories*adlı bir yöntemi kullanacak şekilde yapılandırılmıştır:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

*GetCategories* metodunu sayfanın kodunda oluşturursunuz. Basit bir select işlemi için yöntem parametre gerektirmez ve bir *IEnumerable* veya *IQueryable* nesnesi döndürmelidir. New *ItemType* özelliği ayarlandıysa ( [kesin türü belirtilmiş veri denetimleri](#_Toc318097386) altında açıklandığı gibi, türü kesin belirlenmiş veri bağlama ifadelerine izin verir), bu arabirimlerin genel sürümlerinin döndürülmesi gerekir — *IEnumerable&lt;t&gt;* veya *IQueryable&lt;t&gt;* , *ItemType* özelliğinin türüyle eşleşen *t* parametresiyle (örneğin, *IQueryable&lt;category&gt;* ).

Aşağıdaki örnek bir *GetCategories* yöntemi için kodu gösterir. Bu örnek, Northwind örnek veritabanıyla Entity Framework Code First modelini kullanır. Kod, sorgunun her kategori için ilgili ürünlerin ayrıntılarını *Include* yöntemi yoluyla döndürdüğünden emin olur. (Bu, İşaretlemede *TemplateField* öğesinin her bir kategorideki ürünlerin sayısını [n + 1 seçimi](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem)gerektirmeden göstermesini sağlar.)

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

Sayfa çalıştırıldığında, *GridView* denetimi *GetCategories* yöntemini otomatik olarak çağırır ve yapılandırılan alanları kullanarak döndürülen verileri işler:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

Select yöntemi bir *IQueryable* nesnesi döndürdüğünden, *GridView* denetimi Sorguyu yürütmeden önce daha sonra işleyebilir. Örneğin, *GridView* denetimi yürütülmeden önce döndürülen *IQueryable* nesnesine sıralama ve sayfalama için sorgu ifadeleri ekleyebilir, böylece bu işlemler temeldeki LINQ sağlayıcısı tarafından gerçekleştirilir. Bu durumda Entity Framework, bu işlemlerin veritabanında gerçekleştirildiğinden emin olur.

Aşağıdaki örnek, sıralama ve disk belleğine izin vermek için değiştirilen *GridView* denetimini gösterir:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

Artık sayfa çalıştırıldığında, denetim yalnızca geçerli veri sayfasının görüntülendiğini ve seçilen sütuna göre sıralandığından emin olabilir:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

Döndürülen verileri filtrelemek için, parametrelerin Select yöntemine eklenmesi gerekir. Bu parametreler, çalışma zamanında model bağlamaya göre doldurulacak ve verileri döndürmeden önce sorguyu değiştirmek için kullanabilirsiniz.

Örneğin, kullanıcıların bir sorgu dizesine anahtar sözcük girerek ürünleri filtrelemesine izin vermek istediğinizi varsayalım. Yöntemine bir parametre ekleyebilir ve kodu parametre değerini kullanacak şekilde güncelleştirebilirsiniz:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

Bu kod, *anahtar sözcüğü* için bir değer sağlanmışsa bir *WHERE* ifadesi içerir ve ardından sorgu sonuçlarını döndürür.

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a>Değer sağlayıcıları

Önceki örnek, *anahtar sözcük* parametresinin değerinin geldiği konum hakkında özel değildi. Bu bilgileri belirtmek için bir parametre özniteliği kullanabilirsiniz. Bu örnek için, *System. Web. ModelBinding* ad alanındaki *QueryStringAttribute* sınıfını kullanabilirsiniz:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

Bu, model bağlamaya bir değeri sorgu dizesinden çalışma zamanında *anahtar sözcük* parametresine bağlamayı denemeye yönlendirir. (Bu durumda olmasa da tür dönüştürmesi gerçekleştirmeyi gerektirebilir.) Bir değer sağlanamayacak ve tür null atanamaz ise, bir özel durum oluşturulur.

Bu yöntemlere ait değer kaynakları değer sağlayıcıları olarak adlandırılır ve kullanılacak değer sağlayıcısını belirten parametre öznitelikleri, değer sağlayıcı öznitelikleri olarak adlandırılır. Web Forms, sorgu dizesi, tanımlama bilgileri, form değerleri, denetimler, Görünüm durumu, oturum durumu ve profil özellikleri gibi Web Forms bir uygulamadaki tüm tipik Kullanıcı girişi kaynakları için değer sağlayıcılarını ve karşılık gelen öznitelikleri içerir. Ayrıca, özel değer sağlayıcıları yazabilirsiniz.

Varsayılan olarak parametre adı, değer sağlayıcı koleksiyonunda bir değer bulmak için anahtar olarak kullanılır. Örnekte, kod anahtar sözcük adlı bir sorgu dizesi değeri arar (örneğin, ~/default.aspx? anahtar sözcüğü = Chef). Parametre özniteliğine bir bağımsız değişken olarak geçirerek özel bir anahtar belirtebilirsiniz. Örneğin, soru-cevap adlı sorgu dizesi değişkeninin değerini kullanmak için şunu yapabilirsiniz:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

Bu yöntem sayfanın koddaysa, kullanıcılar sorgu dizesini kullanarak bir anahtar sözcük geçirerek sonuçlara filtre uygulayabilir:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

Model bağlama, aksi takdirde el ile kod yazmanız gereken pek çok görevi gerçekleştirir: değeri okumak, null bir değer denetlemek, uygun türe dönüştürmeye çalışmak, dönüştürmenin başarılı olup olmadığını ve son olarak ' deki değeri kullanarak sorgulayamadı. Model bağlama sonuçları, çok daha az kod ve uygulamanızın tamamında işlevselliği yeniden kullanma olanağıdır.

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a>Bir denetimden değerlere göre filtreleme

Kullanıcının açılan listeden bir filtre değeri seçmesini sağlamak için örneği genişletmek istediğinizi varsayalım. Aşağıdaki açılan listeyi biçimlendirmeye ekleyin ve *SelectMethod* özelliğini kullanarak başka bir yöntemden verileri almak için yapılandırın:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

Genellikle, *GridView* denetimine bir *EmptyDataTemplate* öğesi ekleyerek denetimin eşleşen ürün bulunmazsa bir ileti görüntülemesi gerekir:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

Sayfa kodunda, açılan liste için yeni seçme yöntemini ekleyin:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

Son olarak, açılan listeden seçilen kategorinin KIMLIĞINI içeren yeni bir parametre almak için *GetProducts* Select yöntemini güncelleştirin:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

Artık sayfa çalıştırıldığında, kullanıcılar açılan listeden bir kategori seçebilir ve *GridView* denetimi filtrelenmiş verileri göstermek için otomatik olarak yeniden bağlanır. Model bağlama, select yöntemlerine ait parametrelerin değerlerini izlediği ve geri gönderimin ardından herhangi bir parametre değerinin değişip değişmediğini algıladığı için bu mümkündür. Bu durumda model bağlama, ilişkili veri denetimini verileri yeniden bağlamaya zorlar.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a>HTML kodlamalı veri bağlama Ifadeleri

Artık veri bağlama ifadelerinin sonucunu HTML olarak kodlayabilirsiniz. İki nokta üst üste ekleme (:) veri bağlama ifadesini işaretleyen &lt;% # ön ekinin sonuna kadar:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a>Unobtrusive doğrulaması

Artık yerleşik Doğrulayıcı denetimlerini, istemci tarafı doğrulama mantığı için unobtrusive JavaScript kullanacak şekilde yapılandırabilirsiniz. Bu, sayfa biçimlendirmesinde satır içi işlenen JavaScript miktarını önemli ölçüde azaltır ve toplam sayfa boyutunu azaltır. Doğrulayıcı denetimleri için unobtrusive JavaScript 'ı şu yollarla yapılandırabilirsiniz:

- Genel olarak, Web. config dosyasındaki *&lt;appSettings&gt;* öğesine aşağıdaki ayarı ekleyerek: 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- Statik *System. Web. UI. ValidationSettings. UnobtrusiveValidationMode* özelliğini *UnobtrusiveValidationMode. WebForms* (genellikle Global. asax dosyasındaki *Application\_start* yönteminde) olarak ayarlayarak Global olarak.
- *Sayfa sınıfının yeni* *UnobtrusiveValidationMode* özelliğini *UnobtrusiveValidationMode. WebForms*olarak ayarlayarak bir sayfa için ayrı ayrı.

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a>HTML5 güncelleştirmeleri

HTML5 'in yeni özelliklerinden yararlanmak için Web Forms sunucu denetimlerine bazı geliştirmeler yapılmıştır:

- *TextBox* denetiminin *TextMode* özelliği, *e-posta*, *DateTime*vb. gibi yeni HTML5 giriş türlerini destekleyecek şekilde güncelleştirilmiştir.
- *FileUpload* denetimi artık bu HTML5 özelliğini destekleyen tarayıcılardan birden çok dosya yüklemeyi destekliyor.
- Doğrulayıcı denetimleri artık HTML5 giriş öğelerinin doğrulanmasını destekliyor.
- URL 'YI temsil eden özniteliklere sahip yeni HTML5 öğeleri artık runat = "Server" öğesini destekliyor. Sonuç olarak, uygulama kökünü temsil etmek için ~ işleci gibi URL yollarındaki ASP.NET kurallarını kullanabilirsiniz (örneğin, &lt;video runat = "Server" src = "~/MyVideo.exe"/&gt;).
- *UpdatePanel* denetimi HTML5 giriş alanlarının nakledilmesini destekleyecek şekilde düzeltildi.

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

ASP.NET MVC 4 Beta sürümü artık Visual Studio 11 Beta sürümüne dahildir. ASP.NET MVC, Model-View-Controller (MVC) düzeninden yararlanarak yüksek düzeyde test edilebilir ve sürdürülebilir Web uygulamaları geliştirmeye yönelik bir çerçevedir. ASP.NET MVC 4, Mobil Web için uygulama oluşturmayı kolaylaştırır ve ASP.NET Web API 'sini içerir ve bu da herhangi bir cihaza ulaşabilme HTTP Hizmetleri oluşturmanıza yardımcı olur. Daha fazla bilgi için bkz. [ASP.NET MVC 4 sürüm notları](mvc4-release-notes.md).

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a>ASP.NET Web Sayfaları 2

Yeni özellikler şunları içerir:

- Yeni ve güncelleştirilmiş site şablonları.
- *Doğrulama* Yardımcısını kullanarak sunucu tarafı ve istemci tarafı doğrulama ekleme.
- Bir varlık Yöneticisi kullanarak betikleri kaydetme yeteneği.
- OAuth ve OpenID kullanan Facebook ve diğer sitelerden oturum açma işlemlerini etkinleştirme.
- *Haritalar* Yardımcısını kullanarak haritalar ekleme.
- Web sayfaları uygulamalarını yan yana çalıştırma.
- Mobil cihazlar için sayfaları işleme.

Bu özellikler ve tam sayfa kodu örnekleri hakkında daha fazla bilgi için bkz. [Web Pages 2 Beta 'Da en üstteki Özellikler](https://go.microsoft.com/fwlink/?LinkID=227824).

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a>Visual Web Developer 11 Beta

Bu bölümde, Visual Web Developer 11 Beta ve Visual Studio 2012 sürüm adayı 'nda Web geliştirme geliştirmeleri hakkında bilgi verilmektedir.

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a>Visual Studio 2010 ile Visual Studio 2012 sürüm adayı (proje uyumluluğu) arasında proje paylaşımı

Visual Studio 2012 sürüm adayı 'na kadar, mevcut bir projeyi Visual Studio 'nun daha yeni bir sürümünde açmak Dönüştürme Sihirbazı 'nı başlattı. Bu, bir proje ve çözümün içeriğinin (varlıkların), geriye dönük olarak uyumlu olmayan yeni biçimlere yükseltmesini zordu. Bu nedenle, dönüştürmeden sonra projeyi Visual Studio 'nun eski sürümünde açamazsınız.

Birçok müşteri, doğru yaklaşımda olduğunu söyledi. Visual Studio 11 Beta sürümünde, artık Visual Studio 2010 SP1 ile proje ve çözüm paylaşmayı destekliyoruz. Bu, Visual Studio 2012 sürüm adayı 'nda bir 2010 projesi açarsanız projeyi yine Visual Studio 2010 SP1 'de açabiliyor demektir.

> [!NOTE]
> Visual Studio 2010 SP1 ve Visual Studio 2012 sürüm adayı arasında birkaç tür proje paylaştırılamaz. Bunlar, bazı eski projeler (örneğin, ASP.NET MVC 2 projeleri) veya özel amaçlar için projeler (örneğin, Kurulum projeleri) içerir.

Visual Studio 11 Beta sürümünde bir Visual Studio 2010 SP1 Web projesini ilk kez açtığınızda, proje dosyasına aşağıdaki özellikler eklenir:

- Fileyükseltilebilir Deflags
- UpgradeBackupLocation
- Oldaraçları sürümü
- VisualStudioVersion
- VSToolsPath

Fileyükseltideflags, UpgradeBackupLocation ve Oldaraçları sürümü, proje dosyasını yükselten işlem tarafından kullanılır. Visual Studio 2010 ' de projeyle çalışma üzerinde hiçbir etkisi yoktur.

VisualStudioVersion, geçerli proje için Visual Studio sürümünü gösteren MSBuild 4,5 tarafından kullanılan yeni bir özelliktir. Bu özellik MSBuild 4,0 ' de olmadığı için (Visual Studio 2010 SP1 'in kullandığı MSBuild sürümü), proje dosyasına varsayılan bir değer ekleyeceğiz.

VSToolsPath özelliği, MSBuildExtensionsPath32 ayarıyla temsil edilen yoldan içeri aktarılacak doğru. targets dosyasını tespit etmek için kullanılır.

Ayrıca Içeri aktarma öğeleriyle ilgili bazı değişiklikler de vardır. Bu değişiklikler, Visual Studio 'nun her iki sürümü arasındaki uyumluluğu desteklemek için gereklidir.

> [!NOTE]
> Bir proje iki farklı bilgisayarda Visual Studio 2010 SP1 ve Visual Studio 11 Beta arasında paylaşılmışsa ve proje, App\_Data klasöründe bir yerel veritabanı içeriyorsa, veritabanı tarafından kullanılan SQL Server sürümünün her iki bilgisayarda da yüklü olduğundan emin olmanız gerekir.

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a>ASP.NET 4,5 Web sitesi şablonlarındaki yapılandırma değişiklikleri

Visual Studio 2012 sürüm adayı 'nda Web sitesi şablonları kullanılarak oluşturulan site için varsayılan *Web. config* dosyasında aşağıdaki değişiklikler yapılmıştır:

- `<httpRuntime>` öğesinde, `encoderType` özniteliği artık ASP.NET 'e eklenmiş olan AntiXSS türlerini kullanmak için varsayılan olarak ayarlanır. Ayrıntılar için bkz. [AntiXSS Kitaplığı](#_Toc318097382).
- Ayrıca, `<httpRuntime>` öğesinde, `requestValidationMode` özniteliği "4,5" olarak ayarlanır. Bu, varsayılan olarak, istek doğrulaması ertelenmiş ("Lazy") doğrulaması kullanacak şekilde yapılandırıldığı anlamına gelir. Ayrıntılar için bkz. [yeni ASP.net Isteği doğrulama özellikleri](#_Toc318097379).
- `<system.webServer>` bölümünün `<modules>` öğesi bir `runAllManagedModulesForAllRequests` özniteliği içermiyor. (Varsayılan değer false 'dur.) Yani, SP1 'e güncelleştirilmemiş bir IIS 7 sürümü kullanıyorsanız, yeni bir sitede yönlendirme sorunlarıyla karşılaşabilirsiniz. Daha fazla bilgi için bkz. [ASP.net Routing IÇIN IIS 7 ' de yerel destek](#Native_Support_In_IIS7_For_ASPNET_Routine).

Bu değişiklikler mevcut uygulamaları etkilemez. Ancak, mevcut Web siteleri ve yeni şablonlar kullanılarak ASP.NET 4,5 için oluşturduğunuz yeni Web siteleri arasındaki davranıştaki bir farkı temsil edebilir.

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a>ASP.NET yönlendirme için IIS 7 ' de yerel destek

Bu, ASP.NET ' de bir değişiklik değildir, ancak yeni Web sitesi projeleri için, SP1 güncelleştirmesi uygulanmış bir IIS 7 sürümü çalışıyorsanız sizi etkileyebilecek bir değişiklik değildir.

ASP.NET ' de, yönlendirmeyi desteklemek için uygulamalara aşağıdaki yapılandırma ayarını ekleyebilirsiniz:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

**RunAllManagedModulesForAllRequests** true olduğunda, URL 'de *. aspx*, *. Mvc*veya benzer UZANTı olmasa bile `http://mysite/myapp/home` gibi bir URL ASP.net 'e gider.

IIS 7 ' de yapılan bir güncelleştirme, **runAllManagedModulesForAllRequests** ayarını gereksiz hale getirir ve ASP.net yönlendirmeyi yerel olarak destekler. (Güncelleştirme hakkında bilgi için, [belırlı ııs 7,0 veya ııs 7,5 işleyicilerinin, URL 'lerin noktayla bitmeyen istekleri işlemesini sağlayan bir güncelleştirme](https://support.microsoft.com/kb/980368)Microsoft desteği makalesine bakın.)

Web siteniz IIS 7 ' de çalışıyorsa ve IIS güncellendiyse, **runAllManagedModulesForAllRequests** ' i true olarak ayarlamanız gerekmez. Aslında, istek için gereksiz işleme yükü eklediğinden, true olarak ayarlanması önerilmez. Bu ayar doğru olduğunda, *. htm*, *. jpg*ve diğer statik dosyalar dahil olmak üzere tüm istekler de ASP.NET istek ardışık düzenine geçer.

Visual Studio 2012 RC 'de sunulan şablonları kullanarak yeni bir ASP.NET 4,5 Web sitesi oluşturursanız, Web sitesinin yapılandırması **runAllManagedModulesForAllRequests** ayarını içermez. Bu, varsayılan olarak ayarın false olduğu anlamına gelir.

Daha sonra Web sitesini SP1 yüklü olmayan Windows 7 ' de çalıştırırsanız, IIS 7 gerekli güncelleştirmeyi içermez. Sonuç olarak, yönlendirme çalışmaz ve hata görürsünüz. Yönlendirmenin çalışmabileceği bir sorun yaşıyorsanız, aşağıdakilerden birini yapabilirsiniz:

- Windows 7 ' yi SP1 'e güncelleştirin ve bu güncelleştirme IIS 7 ' ye eklenir.
- Daha önce listelenen Microsoft Desteği makalesinde açıklanan güncelleştirmeyi yükler.
- Bu Web sitesinin Web. config dosyasında **runAllManagedModulesForAllRequests** değerini true olarak ayarlayın. Bu, isteklere bazı ek yük ekleneceğini unutmayın.

<a id="_Toc318097397"></a>
### <a name="html-editor"></a>HTML Düzenleyicisi

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a>Akıllı görevler

Tasarım görünümü, sunucu denetimlerinin karmaşık özelliklerinin çoğu zaman kolayca ayarlamayı kolaylaştırmak için ilişkili iletişim kutuları ve sihirbazlar vardır. Örneğin, bir *Yineleyici* denetimine veri kaynağı eklemek veya *GridView* denetimine sütun eklemek için özel bir iletişim kutusu kullanabilirsiniz.

Ancak, karmaşık özellikler için bu tür UI Yardımı kaynak görünümünde kullanılamaz. Bu nedenle, Visual Studio 11 kaynak görünümü için akıllı görevleri tanıtır. Akıllı görevler, C# ve Visual Basic düzenleyicilerinde yaygın olarak kullanılan özellikler için bağlam duyarlı kısayollardır.

ASP.NET Web Forms Denetimlerinde, ekleme noktası öğenin içindeyken akıllı görevler küçük bir karakter olarak sunucu etiketlerinde görünür:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

Akıllı Görev, glifi tıkladığınızda veya CTRL + tuşlarına basıldığında genişler. (nokta), kod düzenleyicilerde olduğu gibi. Daha sonra Tasarım görünümü içindeki akıllı görevlere benzer kısayollar görüntüler.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

Örneğin, önceki çizimdeki Akıllı Görev GridView görevleri seçeneklerini gösterir. Sütunları Düzenle ' yi seçerseniz, aşağıdaki iletişim kutusu görüntülenir:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

İletişim kutusunda doldurma, Tasarım görünümü ayarlayabileceğiniz özellikleri ayarlar. Tamam ' a tıkladığınızda, denetimin biçimlendirmesi yeni ayarlarla güncelleştirilir:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a>WAı-ARIA desteği

Erişilebilir Web sitelerini yazma işlemi giderek daha önemli hale geliyor. [WAI-ARIA erişilebilirlik standardı](http://www.w3.org/WAI/intro/aria) , geliştiricilerin erişilebilir Web sitelerini nasıl yazması gerektiğini tanımlar. Bu standart, Visual Studio 'da artık tam olarak desteklenmektedir.

Örneğin, *rol* özniteliği artık tam IntelliSense 'e sahiptir:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

WAI-ARIA standardı Ayrıca, bir HTML5 belgesine semantik bir belge eklemenize olanak tanıyan, *Aria* önekli öznitelikleri de tanıtır. Visual Studio bu *Aria* özniteliklerini de tam olarak destekler:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a>Yeni HTML5 parçacıkları

Yaygın olarak kullanılan HTML5 işaretlemesini daha hızlı ve kolay bir şekilde yazmayı kolaylaştırmak için, Visual Studio çok sayıda kod parçacığı içerir. Video kod parçacığı bir örnektir:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

Kod parçacığını çağırmak için, IntelliSense 'de öğe seçiliyken Tab tuşuna iki kez basın:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

Bu, özelleştirebileceğiniz bir kod parçacığı oluşturur.

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a>Kullanıcı denetimine Ayıkla

Büyük web sayfalarında, bireysel parçaları kullanıcı denetimlerine taşımak iyi bir fikir olabilir. Bu yeniden düzenleme biçimi sayfanın okunabilirliğini artırmaya ve sayfa yapısını basitleştirmeye yardımcı olabilir.

Bunun daha kolay olması için, kaynak görünümünde Web Forms sayfalarını düzenlediğinizde, sayfada metin seçebilir, sağ tıklayıp, ardından Kullanıcı denetimine Ayıkla ' yı seçebilirsiniz:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a>Kod nugal için IntelliSense özniteliklere

Visual Studio her zaman herhangi bir sayfa veya denetimde sunucu tarafı kod nugal için IntelliSense 'i sağladı. Artık Visual Studio, HTML özniteliklerine de kod nugal için IntelliSense içerir.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

Bu, veri bağlama ifadeleri oluşturmayı kolaylaştırır:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a>Bir açılış veya kapanış etiketini yeniden adlandırdığınızda eşleşen etiketin otomatik olarak yeniden adlandırılması

Bir HTML öğesini yeniden adlandırırsanız (örneğin, bir *div* etiketini bir *başlık* etiketi olacak şekilde değiştirirseniz), karşılık gelen açma veya kapatma etiketi de gerçek zamanlı olarak değişir.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

Bu, bir kapanış etiketini değiştirmeyi veya yanlış bir etiketi değiştirmeyi unuttuğunuzda hata oluşmasını önlemeye yardımcı olur.

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a>Olay işleyicisi oluşturma

Visual Studio artık olay işleyicilerini yazmanızı ve bunları el ile bağlamayı sağlamak için kaynak görünümündeki özellikleri içerir. Kaynak görünümünde bir olay adı düzenliyorsanız, IntelliSense, doğru imzaya sahip sayfanın kodunda bir olay işleyicisi oluşturacak &lt;yeni olay&gt;oluşturma ' yı görüntüler.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

Varsayılan olarak, olay işleyicisi olay işleme yönteminin adı için denetimin KIMLIĞINI kullanır:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

Sonuç olay işleyicisi şuna benzer (Bu durumda, içinde C#):

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a>Akıllı girinti

Boş bir HTML öğesi içindeyken ENTER tuşuna bastığınızda, düzenleyici ekleme noktasını doğru yere koyar:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

Bu konumda ENTER tuşuna basarsanız, kapanış etiketi aşağı taşınır ve açılış etiketiyle eşleşecek şekilde girintilenir. Ekleme noktası da girintilenir:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a>Deyimin tamamlanmasını otomatik azalt

Visual Studio 'daki IntelliSense listesi artık, yalnızca ilgili seçenekleri görüntüleyecek şekilde, yazdığınıza göre filtreliyor:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

IntelliSense, IntelliSense listesindeki tek sözcüklerin başlık durumuna göre de filtre uygular. Örneğin, "DL" yazarsanız, hem DL hem de ASP: DataList görüntülenir:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

Bu özellik, bilinen öğeler için deyimin tamamlanmasını daha hızlı bir şekilde almanızı sağlar.

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a>JavaScript Düzenleyicisi

Visual Studio 2012 sürüm adayı 'ndaki JavaScript Düzenleyicisi tamamen yenidir ve Visual Studio 'da JavaScript ile çalışma deneyimini büyük ölçüde geliştirir.

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a>Kod anahat oluşturma

Ana hat bölgeleri artık tüm işlevler için otomatik olarak oluşturulur ve bu, dosyanın geçerli odağıyla ilgili olmayan parçalarını daraltmanıza olanak tanır.

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a>Ayraç eşleştirme

Ekleme noktasını bir açma veya kapatma küme ayracı üzerine yerleştirdiğinizde, düzenleyici eşleşen bir tane vurgular.

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a>Tanıma Git

Tanıma Git komutu, bir işlev veya değişken için kaynağa atlamanızı sağlar.

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a>ECMAScript5 desteği

Düzenleyici, ECMAScript5 ' deki yeni sözdizimi ve API 'Leri destekler. Bu, standart, JavaScript dilini tanımlayan en son sürümüdür.

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a>DOM IntelliSense

*QuerySelector*, Dom depolama, çapraz belge mesajlaşma ve *tuval*gibi birçok yeni HTML5 API desteği sayesinde Dom API 'leri için IntelliSense geliştirilmiştir. DOM IntelliSense artık yerel bir tür kitaplığı tanımı yerine tek bir basit JavaScript dosyası tarafından yönlendiriliyor. Bu, genişletmeyi veya değiştirmeyi kolaylaştırır.

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a>VSDOC imza aşırı yüklemeleri

Ayrıntılı IntelliSense açıklamaları artık, aşağıdaki örnekte gösterildiği gibi yeni *&lt;signature&gt;* öğesi kullanılarak JavaScript işlevlerinin ayrı olarak aşırı yüklemeleri için de bildirilebilecek:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a>Örtük başvurular

Artık, belirli bir JavaScript dosyasının veya bloğunun başvurduğu dosya listesine örtülü olarak dahil edilecek bir merkezi listeye JavaScript dosyaları ekleyebilirsiniz, bu da içerikleri için IntelliSense 'i alacaksınız. Örneğin, jQuery dosyalarını merkezi dosya listesine ekleyebilirsiniz ve bu dosya, açıkça (///&lt;Reference/&gt;) ile Başvurulmuş olmanız durumunda herhangi bir JavaScript bloğunda jQuery işlevleri için IntelliSense 'i alırsınız.

<a id="_Toc318097415"></a>
### <a name="css-editor"></a>CSS Düzenleyicisi

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a>Deyimin tamamlanmasını otomatik azalt

CSS için IntelliSense listesi artık seçili şemanın desteklediği CSS özelliklerine ve değerlerine göre filtrelenecektir.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

IntelliSense Ayrıca başlık büyük/küçük harf aramalarını destekler:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a>Hiyerarşik girintileme

CSS Düzenleyicisi, basamaklı kuralların mantıksal olarak nasıl düzenlendiğini gösteren bir genel bakış sunan hiyerarşik kuralları göstermek için girinti kullanır. Aşağıdaki örnekte, seçici #list listenin basamaklı bir alt öğesidir ve bu nedenle girintilenir.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

Aşağıdaki örnekte daha karmaşık devralma gösterilmektedir:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

Bir kuralın girintisi, üst kurallarına göre belirlenir. Hiyerarşik girintileme varsayılan olarak etkindir, ancak Seçenekler iletişim kutusunu (Araçlar, menü çubuğundan Seçenekler) devre dışı bırakabilirsiniz:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a>CSS Hacks desteği

Yüzlerce gerçek dünyada CSS dosyası analizi, CSS hackilerinin çok yaygın olduğunu gösterir ve artık Visual Studio, en yaygın olarak kullanılan programları destekler. Bu destek, yıldız (\*) ve alt çizgi (\_) özellik korsanları için IntelliSense ve doğrulama içerir:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

Normal seçici hacki 'lar, uygulandıklarında bile hiyerarşik girintileme sürdürülmesi için de desteklenir. Internet Explorer 7 ' yi hedeflemek için kullanılan tipik bir seçici, *\*: First-Child + HTML*gibi bir seçiciyi sonuna eklemek için kullanılır. Bu kuralın kullanılması, hiyerarşik Girintiyi korur:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a>Satıcıya özgü şemalar (-Moz-,-WebKit)

CSS3 farklı zamanlarda farklı tarayıcılar tarafından uygulanan birçok özellik sunar. Bu, daha önce geliştiricilere satıcıya özgü söz dizimini kullanarak belirli tarayıcıları kodlamasına zorlanır. Bu tarayıcıya özgü özellikler artık IntelliSense 'e dahildir.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a>Açıklama ekleme ve açıklama kaldırma desteği

Artık, kod Düzenleyicisi 'nde kullandığınız kısayolları (CTRL + K, C açıklama ve CTRL + K) kullanarak CSS kuralları hakkında yorum yapabilir ve açıklama ekleyebilirsiniz.

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a>Renk seçici

Visual Studio 'nun önceki sürümlerinde, renkle ilgili öznitelikler için IntelliSense, adlandırılmış renk değerlerinin açılan listesinden oluşur. Bu liste, tam özellikli bir renk seçiciyle değiştirilmiştir.

Bir renk değeri girdiğinizde, renk seçici otomatik olarak görüntülenir ve daha önce kullanılan renklerin bir listesini izleyen bir varsayılan renk paleti gösterir. Fareyi veya klavyeyi kullanarak bir renk seçebilirsiniz.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

Liste, bir bütün renk seçicisine genişletilebilir. Seçici, Opaklık kaydırıcısını taşırken tüm renkleri RGBA 'ya otomatik olarak dönüştürerek alfa kanalını denetlemenizi sağlar:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a>Kod Parçacıkları

CSS düzenleyicideki kod parçacıkları, tarayıcılar arası stiller oluşturmayı kolaylaştırır ve daha hızlı hale getirir. Tarayıcıya özgü ayarlar gerektiren birçok CSS3 özelliği artık kod parçacıklarına alındı.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

CSS parçacıkları, IntelliSense listesini gösteren-symbol (@) yazarak gelişmiş senaryoları (CSS3 medya sorguları gibi) destekler.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

@media değeri seçip Tab tuşuna basarsanız, CSS Düzenleyicisi aşağıdaki kod parçacığını ekler:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

Kod parçacıklarında olduğu gibi, kendi CSS kod parçacıklarınızı oluşturabilirsiniz.

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a>Özel bölgeler

Kod düzenleyicisinde zaten kullanılabilir olan adlandırılmış kod bölgeleri artık CSS düzenleme için kullanılabilir. Bu, ilgili stil bloklarını kolayca gruplamanızı sağlar.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

Bir bölge daraltıldığında bölgenin adını görüntüler:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a>Sayfa Denetçisi

Sayfa denetçisi, Visual Studio IDE 'de bir Web sayfası (HTML, Web Forms, ASP.NET MVC veya Web sayfaları) işleyen ve hem kaynak kodu hem de elde edilen çıktıyı incelemenize olanak tanıyan bir araçtır. ASP.NET sayfaları için sayfa denetçisi, tarayıcıda işlenen HTML işaretlemesini hangi sunucu tarafı kodunun üretdiğine belirlemenizi sağlar.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

Sayfa denetçisi hakkında daha fazla bilgi için lütfen aşağıdaki öğreticilere bakın:

- [ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md) 'de sayfa denetçisini kullanma
- [ASP.NET Web Forms](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md) sayfa denetçisini kullanma

<a id="_Toc318097425"></a>
### <a name="publishing"></a>Yayımlama

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a>Yayımlama profilleri

Visual Studio 2010 ' de, Web uygulaması projeleri için yayımlama bilgileri sürüm denetiminde depolanmaz ve başkalarıyla paylaşmak için tasarlanmamıştır. Visual Studio 2012 sürüm adayı 'nda yayımlama profili biçimi değiştirilmiştir. Bu, bir ekip yapıtı yapıldı ve MSBuild 'e göre yapılardan daha kolay bir şekilde faydalanır. Derlemeyi yayımlamadan önce derleme yapılandırmalarını kolayca geçiş yapabilmeniz için, derleme yapılandırma bilgileri Yayımla iletişim kutusudur.

Yayımlama profilleri PublishProfiles klasöründe depolanır. Klasörün konumu, kullanmakta olduğunuz programlama diline bağlıdır:

- C#: Properties\PublishProfiles
- Visual Basic: Project\PublishProfiles

Her profil bir MSBuild dosyasıdır. Yayımlama sırasında, bu dosya projenin MSBuild dosyasına aktarılır. Visual Studio 2010 ' de, Yayımla veya paket işleminde değişiklik yapmak istiyorsanız, özelleştirmelerinizi **ProjectName**. WPP. targets adlı bir dosyaya koymanız gerekir. Bu yine de desteklenir, ancak artık Özelleştirmeleri yayımlama profilinin kendisinde yerleştirebilirsiniz. Bu şekilde, özelleştirmeler yalnızca bu profil için kullanılacaktır.

Artık MSBuild 'ten yayımlama profillerden de yararlanabilirsiniz. Bunu yapmak için, projeyi oluştururken aşağıdaki komutu kullanın:

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

Project. csproj değeri projenin yoludur ve ProfileName, yayımlanacak profilin adıdır. Alternatif olarak, *PublishProfile* özelliği için profil adını geçirmek yerine, yayımlama profilinin tam yolunu geçirebilirsiniz.

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a>ASP.NET ön derleme ve birleştirme

Web uygulaması projelerinde, Visual Studio 2012 Release Candidate, projeyi yayımladığınızda veya paketlerseniz sitenizin içeriğini önceden derleyip birleştirmeye olanak sağlayan, paket/yayımlama Web Özellikleri sayfasına bir seçenek ekler. Bu seçenekleri görmek için Çözüm Gezgini ' de projeye sağ tıklayın, Özellikler ' i seçin ve sonra paket/Web özelliği Yayımla sayfasını seçin. Aşağıdaki çizimde yayımlamadan önce bu uygulamayı önceden derle seçeneği gösterilmektedir.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

Bu seçenek belirlendiğinde, Web uygulamasını yayımladığınızda veya paketlediğiniz zaman Visual Studio uygulamayı önceden derler. Sitenin nasıl ön derlenmiş olduğunu veya derlemelerin nasıl birleştirildiğini denetlemek istiyorsanız, bu seçenekleri yapılandırmak için Gelişmiş düğmesine tıklayın.

<a id="_Toc318097428"></a>
### <a name="iis-express"></a>IIS Express

Visual Studio 'da Web projelerini test etmeye yönelik varsayılan Web sunucusu artık IIS Express. Visual Studio geliştirme sunucusu, geliştirme sırasında yerel Web sunucusu için hala bir seçenektir, ancak IIS Express artık önerilen sunucusudur. Visual Studio 11 Beta 'da IIS Express kullanma deneyimi, Visual Studio 2010 SP1 'de kullanmaya çok benzer.

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a>Sorumluluk reddi

Bu bir ön belgedir ve burada açıklanan yazılımın son ticari sürümünden önce önemli ölçüde değiştirilebilir.

Bu belgede yer alan bilgiler, Yayın tarihi itibariyle ele alınan sorunlar hakkında Microsoft Corporation 'ın geçerli görünümünü temsil eder. Microsoft 'un değişen piyasa koşullarını yanıtlaması gerektiğinden, Microsoft 'un kapsamında bir taahhüt olarak yorumlanmamalıdır ve Microsoft 'un, yayın tarihinden sonra sunulan bilgilerin doğruluğunu garanti edemez.

Bu teknik Inceleme yalnızca bilgilendirme amaçlıdır. MICROSOFT, BU BELGEDEKI BILGILERE GÖRE HIÇBIR GARANTI VERMEZ, ÖRTÜLÜ VEYA YASAL DEĞILDIR.

Tüm geçerli telif hakkı yasaları ile uyumlu olması, kullanıcının sorumluluğundadır. Telif hakkı kapsamındaki hakları sınırlandırmadan, bu belgenin hiçbir bölümü çoğaltılamaz, bir alma sisteminde depolanabilir veya bir alma sisteminde bulunabilir ya da herhangi bir biçimde ya da herhangi bir amaçla (elektronik, mekanik, Fotokopi, kayıt veya diğer yollarla) veya herhangi bir amaçla iletilebilir Microsoft Corporation 'ın Express yazılı izni olmadan.

Microsoft 'un bu belgede ilgili konuyu kapsayan patentler, patent uygulamaları, ticari markalar, telif hakları veya diğer fikri mülkiyet hakları olabilir. Microsoft 'un herhangi bir yazılı lisans sözleşmesinde açık bir şekilde sağlanmasının dışında, bu belgenin bu patentinin bir lisansını, ticari markalara, telif haklarına veya diğer fikri mülkiyet için herhangi bir lisansa vermez.

Aksi belirtilmedikçe, burada adı geçen örnek şirketler, kuruluşlar, ürünler, etki alanı adları, e-posta adresleri, logolar, kişiler, konumlar ve olaylar kurgusaldır ve gerçek şirket, kuruluş, ürün, etki alanı adı, e-posta ile hiçbir ilişki yoktur Adres, logo, kişi, yer veya olay amaçlıdır veya çıkarsanmalıdır.

© 2012 Microsoft Corporation. Tüm hakları saklıdır.

Microsoft ve Windows, Microsoft Corporation 'ın Birleşik Devletler ve/veya diğer ülkelerde kayıtlı ticari markaları veya ticari markalarıdır.

Burada bahsedilen gerçek şirketlerin ve ürünlerin adları, ilgili sahiplerinin ticari markaları olabilir.
