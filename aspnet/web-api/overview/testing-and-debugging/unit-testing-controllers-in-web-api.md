---
uid: web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
title: ASP.NET Web API 2 ' deki birim testi denetleyicileri | Microsoft Docs
author: MikeWasson
description: Bu konuda, Web API 2 ' deki birim testi denetleyicileri için bazı özel teknikler açıklanmaktadır. Bu konuyu okumadan önce öğretici birimini okumak isteyebilirsiniz...
ms.author: riande
ms.date: 06/11/2014
ms.assetid: 43a6cce7-a3ef-42aa-ad06-90d36d49f098
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: cdb1700537021e276669de1a9e0330a62659746c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554994"
---
# <a name="unit-testing-controllers-in-aspnet-web-api-2"></a>ASP.NET Web API 2’deki Birim Testi Denetleyicileri

, [Mike te son](https://github.com/MikeWasson)

> Bu konuda, Web API 2 ' deki birim testi denetleyicileri için bazı özel teknikler açıklanmaktadır. Bu konuyu okumadan önce, çözümünüze bir birim testi projesinin nasıl ekleneceğini gösteren [ASP.NET Web API 2 öğretici birim testini](unit-testing-with-aspnet-web-api.md)okumak isteyebilirsiniz.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - Web API 2
> - [Moq](https://github.com/Moq) 4.5.30

> [!NOTE]
> Moq kullandım, ancak aynı fikir herhangi bir sahte işlem çerçevesi için de geçerlidir. Moq 4.5.30 (ve üzeri), Visual Studio 2017, Roslyn ve .NET 4,5 ve sonraki sürümlerini destekler.

Birim testlerinde ortak bir model &quot;düzenleme-işlem onaylama&quot;:

- Düzenle: testin çalıştırılacağı önkoşulları ayarlayın.
- Davran: testi gerçekleştirin.
- Onaylama: testin başarılı olduğunu doğrulayın.

Düzenleme adımında, genellikle sahte veya saplama nesneleri kullanacaksınız. Bu, bağımlılıkların sayısını en aza indirir, böylece test bir şeyi test etmeye odaklanır.

Web API denetleyicilerinizde birim testi yapmanız gereken bazı şeyler aşağıda verilmiştir:

- Eylem doğru yanıt türünü döndürür.
- Geçersiz parametreler doğru hata yanıtını döndürür.
- Eylem, depoda veya hizmet katmanında doğru yöntemi çağırır.
- Yanıt bir etki alanı modeli içeriyorsa, model türünü doğrulayın.

Bunlar, test etmek için bazı genel şeylerdir, ancak Ayrıntılar denetleyici uygulamanıza bağlıdır. Özellikle, denetleyici eylemlerinizin **HttpResponseMessage** veya **ıhttpactionresult**döndürme konusunda büyük bir farklılık yapar. Bu sonuç türleri hakkında daha fazla bilgi için bkz. [Web API 2 ' de eylem sonuçları](../getting-started-with-aspnet-web-api/action-results.md).

## <a name="testing-actions-that-return-httpresponsemessage"></a>HttpResponseMessage döndüren eylemleri test etme

Eylemleri **HttpResponseMessage**döndüren bir denetleyiciye örnek aşağıda verilmiştir.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample1.cs)]

Denetleyicinin bir `IProductRepository`eklemek için bağımlılık ekleme işlemini kullandığını unutmayın. Bu, bir sahte depo ekleyebildiğinden denetleyiciyi daha kararlı hale getirir. Aşağıdaki birim testi, `Get` yönteminin yanıt gövdesine bir `Product` yazdığını doğrular. `repository` bir sahte `IProductRepository`olduğunu varsayalım.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample2.cs)]

Denetleyici üzerinde **istek** ve **yapılandırma** ayarlamak önemlidir. Aksi takdirde, test bir **ArgumentNullException** veya **InvalidOperationException**ile başarısız olur.

## <a name="testing-link-generation"></a>Bağlantı oluşturma test ediliyor

`Post` yöntemi, yanıtta bağlantı oluşturmak için **UrlHelper. Link** öğesini çağırır. Bu, birim testinde biraz daha fazla kurulum gerektirir:

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample3.cs)]

**UrlHelper** sınıfı için istek URL 'si ve rota verileri gerekir, bu nedenle testin bu değerler için değerleri ayarlaması gerekir. Diğer bir seçenek de sahte veya saplama **UrlHelper**. Bu yaklaşımda, [Apicontroller. URL](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx) ' nin varsayılan değerini sabit bir değer döndüren bir sahte veya saplama sürümüyle değiştirirsiniz.

[Moq](https://github.com/Moq) çerçevesini kullanarak testi yeniden yazalım. `Moq` NuGet paketini test projesine yükler.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample4.cs)]

Bu sürümde, bir yol verisi ayarlamanız gerekmez, çünkü sahte **UrlHelper** sabit bir dize döndürür.

## <a name="testing-actions-that-return-ihttpactionresult"></a>Ihttpactionresult döndüren test eylemleri

Web API 2 ' de, bir denetleyici eylemi **ıhttpactionresult**döndürebilir ve bu, ASP.NET MVC 'de **ActionResult** öğesine benzer. **Ihttpactionresult** ARABIRIMI, http yanıtları oluşturmak için bir komut kalıbı tanımlar. Yanıt doğrudan oluşturmak yerine, denetleyici bir **ıhttpactionresult**döndürür. Daha sonra, işlem hattı yanıtı oluşturmak için **ıhttpactionresult** öğesini çağırır. Bu yaklaşım, **HttpResponseMessage**için gereken birçok ayarı atlayabilmeniz için birim testlerini yazmayı kolaylaştırır.

Eylemleri **ıhttpactionresult**döndüren örnek bir denetleyici aşağıda verilmiştir.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample5.cs)]

Bu örnekte, **ıhttpactionresult**kullanılarak bazı yaygın desenler gösterilmektedir. Ayrıca, birim testinin nasıl test olduğunu görelim.

### <a name="action-returns-200-ok-with-a-response-body"></a>Eylem, yanıt gövdesi ile 200 (Tamam) döndürür

`Get` yöntemi, ürün bulunursa `Ok(product)` çağırır. Birim testinde, dönüş türünün **Oknegoti, ContentResult** olduğundan ve döndürülen ürünün doğru kimliğe sahip olduğundan emin olun.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample6.cs)]

Birim testinin eylem sonucunu yürütmediğine dikkat edin. Eylem sonucunun HTTP yanıtını doğru bir şekilde oluşturduğunu varsayabilirsiniz. (Web API çerçevesinin kendi birim testlerine neden vardır!)

### <a name="action-returns-404-not-found"></a>Eylem 404 döndürüyor (bulunamadı)

`Get` yöntemi, ürün bulunamazsa `NotFound()` çağırır. Bu durumda, birim testi yalnızca dönüş türünün **Notfoundsonucu**olup olmadığını denetler.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample7.cs)]

### <a name="action-returns-200-ok-with-no-response-body"></a>Eylem, yanıt gövdesi olmayan 200 (Tamam) döndürür

`Delete` yöntemi, boş bir HTTP 200 yanıtı döndürmek için `Ok()` çağırır. Önceki örnekte olduğu gibi, birim testi dönüş türünü denetler, bu durumda **Okresult**.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample8.cs)]

### <a name="action-returns-201-created-with-a-location-header"></a>Eylem, konum üst bilgisi ile 201 (oluşturuldu) döndürüyor

`Post` yöntemi, konum üstbilgisinde bir URI ile HTTP 201 yanıtı döndürmek için `CreatedAtRoute` çağırır. Birim testinde, eylemin doğru yönlendirme değerlerini ayarladiğini doğrulayın.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample9.cs)]

### <a name="action-returns-another-2xx-with-a-response-body"></a>Eylem, yanıt gövdesi olan bir 2xx döndürür

`Put` yöntemi bir yanıt gövdesi ile HTTP 202 (kabul edildi) yanıtı döndürmek için `Content` çağırır. Bu durum 200 (Tamam) döndürmeye benzer, ancak birim testi de durum kodunu denetlemelidir.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample10.cs)]

## <a name="additional-resources"></a>Ek Kaynaklar

- [Birim testi ASP.NET Web API 2 ' de Entity Framework Mocking](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)
- [Bir ASP.NET Web API hizmeti için testler yazma](https://blogs.msdn.com/b/youssefm/archive/2013/01/28/writing-tests-for-an-asp-net-webapi-service.aspx) (Youssef Moussaouı tarafından blog gönderisi).
- [Yol hata ayıklayıcı ile ASP.NET Web API 'SI hata ayıklaması](https://blogs.msdn.com/b/webdev/archive/2013/04/04/debugging-asp-net-web-api-with-route-debugger.aspx)
