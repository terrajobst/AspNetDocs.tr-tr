---
uid: web-api/overview/error-handling/exception-handling
title: ASP.NET Web API-ASP.NET 4. x içinde özel durum Işleme
author: MikeWasson
description: ''
ms.author: riande
ms.date: 03/12/2012
ms.custom: seoapril2019
ms.assetid: cbebeb37-2594-41f2-b71a-f4f26520d512
msc.legacyurl: /web-api/overview/error-handling/exception-handling
msc.type: authoredcontent
ms.openlocfilehash: dbdbab6aefec840e2fec9e9cd33f3d124093750e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622320"
---
# <a name="exception-handling-in-aspnet-web-api"></a>ASP.NET Web API 'sinde özel durum Işleme

, [Mike te son](https://github.com/MikeWasson)

Bu makalede ASP.NET Web API 'sindeki hata ve özel durum işleme açıklanır.

- [HttpResponseException](#httpresponserexception)
- [Özel durum filtreleri](#exception_filters)
- [Özel durum filtrelerini kaydetme](#registering_exception_filters)
- [Http hatası](#httperror)

<a id="httpresponserexception"></a>
## <a name="httpresponseexception"></a>HttpResponseException

Web API denetleyicisi yakalanamayan bir özel durum oluşturursa ne olur? Varsayılan olarak, çoğu özel durum 500 durum kodu, Iç sunucu hatası ile HTTP yanıtına çevrilir.

**Httpresponseexception** türü özel bir durumdur. Bu özel durum, özel durum oluşturucuda belirttiğiniz herhangi bir HTTP durum kodunu döndürür. Örneğin, aşağıdaki yöntem, *ID* parametresi geçerli değilse, bulunamadı, 404 döndürür.

[!code-csharp[Main](exception-handling/samples/sample1.cs)]

Yanıt üzerinde daha fazla denetim için, tüm yanıt iletisini de oluşturabilir ve **Httpresponseexception** ile dahil edebilirsiniz: 

[!code-csharp[Main](exception-handling/samples/sample2.cs)]

<a id="exception_filters"></a>
## <a name="exception-filters"></a>Özel durum filtreleri

Web API 'nin özel durumları *özel durum filtresi*yazarak nasıl işleyeceğini özelleştirebilirsiniz. Bir denetleyici yöntemi bir **Httpresponseexception** özel durumu *olmayan* işlenmemiş özel durum oluşturduğunda bir özel durum filtresi yürütülür. **Httpresponseexception** türü özel bir durumdur, çünkü özellıkle bir http yanıtı döndürmek için tasarlanmıştır.

Özel durum filtreleri **System. Web. http. Filters. IExceptionFilter** arabirimini uygular. Bir özel durum filtresi yazmanın en basit yolu, **System. Web. http. Filters. ExceptionFilterAttribute** sınıfından türetmektir ve **OnException** metodunu geçersiz kılar.

> [!NOTE]
> ASP.NET Web API 'sindeki özel durum filtreleri ASP.NET MVC 'de olanlarla benzerdir. Ancak, ayrı bir ad alanında ve ayrı olarak bir işlev olarak bildirilmiştir. Özellikle, MVC 'de kullanılan **HandleErrorAttribute** sınıfı, Web API denetleyicileri tarafından oluşturulan özel durumları işlemez.

**Notimplementedexception** özel durumlarını http durum koduna 501 olarak dönüştüren bir filtre aşağıda uygulanmadı:

[!code-csharp[Main](exception-handling/samples/sample3.cs)]

**HttpActionExecutedContext** nesnesinin **Response** özelliği istemciye gönderilecek http yanıt iletisini içerir.

<a id="registering_exception_filters"></a>
## <a name="registering-exception-filters"></a>Özel durum filtrelerini kaydetme

Web API özel durum filtresini kaydetmek için çeşitli yollar vardır:

- Eyleme göre
- Denetleyiciye göre
- Görünüm

Filtreyi belirli bir eyleme uygulamak için, filtreyi eyleme bir öznitelik olarak ekleyin:

[!code-csharp[Main](exception-handling/samples/sample4.cs)]

Filtreyi bir denetleyicideki tüm eylemlere uygulamak için, filtreyi denetleyici sınıfına bir öznitelik olarak ekleyin:

[!code-csharp[Main](exception-handling/samples/sample5.cs)]

Filtreyi tüm Web API denetleyicilerine Global olarak uygulamak için, **Globalconfiguration. Configuration. Filters** koleksiyonuna bir filtrenin örneği ekleyin. Bu koleksiyondaki özel durum filtreleri Web API denetleyicisi işlemleri için geçerlidir.

[!code-csharp[Main](exception-handling/samples/sample6.cs)]

Projenizi oluşturmak için "ASP.NET MVC 4 Web uygulaması" proje şablonunu kullanırsanız, Web API yapılandırma kodunuzu uygulama\_başlangıç klasörü içinde bulunan `WebApiConfig` sınıfına koyun:

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

<a id="httperror"></a>
## <a name="httperror"></a>Http hatası

**HttpError** nesnesi, yanıt gövdesinde hata bilgilerini döndürmek için tutarlı bir yol sağlar. Aşağıdaki örnek, yanıt gövdesinde bir **HttpError** ile 404 (bulunamadı) http durum kodunu nasıl döndürün gösterir.

[!code-csharp[Main](exception-handling/samples/sample8.cs)]

**Createerrorresponse** , **System .net. http. HttpRequestMessageExtensions** sınıfında tanımlanmış bir genişletme yöntemidir. Dahili olarak, **Createerrorresponse** bir **HttpError** örneği oluşturur ve ardından **HttpError**'ı içeren bir **HttpResponseMessage** oluşturur.

Bu örnekte, Yöntem başarılı olursa, HTTP yanıtında ürünü döndürür. Ancak istenen ürün bulunamazsa HTTP yanıtı, istek gövdesinde bir **HttpError** içerir. Yanıt aşağıdaki gibi görünebilir:

[!code-console[Main](exception-handling/samples/sample9.cmd)]

Bu örnekte, **HttpError** 'ın JSON olarak serileştirildiğine dikkat edin. **HttpError** kullanmanın avantajlarından biri, kesin olarak belirlenmiş diğer tüm modellerde aynı [içerik anlaşması](../formats-and-model-binding/content-negotiation.md) ve serileştirme işleminden geçmesidir.

### <a name="httperror-and-model-validation"></a>HttpError ve model doğrulaması

Model doğrulaması için, yanıtta doğrulama hatalarını dahil etmek için model durumunu **Createerrorresponse**'a geçirebilirsiniz:

[!code-csharp[Main](exception-handling/samples/sample10.cs)]

Bu örnek aşağıdaki yanıtı döndürebilir:

[!code-console[Main](exception-handling/samples/sample11.cmd)]

Model doğrulama hakkında daha fazla bilgi için bkz. [ASP.NET Web API 'de model doğrulaması](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).

### <a name="using-httperror-with-httpresponseexception"></a>HttpResponseException ile HttpError kullanma

Önceki örneklerde, denetleyici eyleminden bir **HttpResponseMessage** iletisi döndürülür, ancak bir **HttpError**döndürmek için **httpresponseexception** da kullanabilirsiniz. Bu, normal başarı durumunda kesin türü belirtilmiş bir model döndürmenizi sağlarken bir hata varsa, yine de **HttpError** döndürüyor:

[!code-csharp[Main](exception-handling/samples/sample12.cs)]
