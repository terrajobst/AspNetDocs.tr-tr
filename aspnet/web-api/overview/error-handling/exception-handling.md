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
# <a name="exception-handling-in-aspnet-web-api"></a><span data-ttu-id="f1755-102">ASP.NET Web API 'sinde özel durum Işleme</span><span class="sxs-lookup"><span data-stu-id="f1755-102">Exception Handling in ASP.NET Web API</span></span>

<span data-ttu-id="f1755-103">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="f1755-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="f1755-104">Bu makalede ASP.NET Web API 'sindeki hata ve özel durum işleme açıklanır.</span><span class="sxs-lookup"><span data-stu-id="f1755-104">This article describes error and exception handling in ASP.NET Web API.</span></span>

- [<span data-ttu-id="f1755-105">HttpResponseException</span><span class="sxs-lookup"><span data-stu-id="f1755-105">HttpResponseException</span></span>](#httpresponserexception)
- [<span data-ttu-id="f1755-106">Özel durum filtreleri</span><span class="sxs-lookup"><span data-stu-id="f1755-106">Exception Filters</span></span>](#exception_filters)
- [<span data-ttu-id="f1755-107">Özel durum filtrelerini kaydetme</span><span class="sxs-lookup"><span data-stu-id="f1755-107">Registering Exception Filters</span></span>](#registering_exception_filters)
- [<span data-ttu-id="f1755-108">Http hatası</span><span class="sxs-lookup"><span data-stu-id="f1755-108">HttpError</span></span>](#httperror)

<a id="httpresponserexception"></a>
## <a name="httpresponseexception"></a><span data-ttu-id="f1755-109">HttpResponseException</span><span class="sxs-lookup"><span data-stu-id="f1755-109">HttpResponseException</span></span>

<span data-ttu-id="f1755-110">Web API denetleyicisi yakalanamayan bir özel durum oluşturursa ne olur?</span><span class="sxs-lookup"><span data-stu-id="f1755-110">What happens if a Web API controller throws an uncaught exception?</span></span> <span data-ttu-id="f1755-111">Varsayılan olarak, çoğu özel durum 500 durum kodu, Iç sunucu hatası ile HTTP yanıtına çevrilir.</span><span class="sxs-lookup"><span data-stu-id="f1755-111">By default, most exceptions are translated into an HTTP response with status code 500, Internal Server Error.</span></span>

<span data-ttu-id="f1755-112">**Httpresponseexception** türü özel bir durumdur.</span><span class="sxs-lookup"><span data-stu-id="f1755-112">The **HttpResponseException** type is a special case.</span></span> <span data-ttu-id="f1755-113">Bu özel durum, özel durum oluşturucuda belirttiğiniz herhangi bir HTTP durum kodunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="f1755-113">This exception returns any HTTP status code that you specify in the exception constructor.</span></span> <span data-ttu-id="f1755-114">Örneğin, aşağıdaki yöntem, *ID* parametresi geçerli değilse, bulunamadı, 404 döndürür.</span><span class="sxs-lookup"><span data-stu-id="f1755-114">For example, the following method returns 404, Not Found, if the *id* parameter is not valid.</span></span>

[!code-csharp[Main](exception-handling/samples/sample1.cs)]

<span data-ttu-id="f1755-115">Yanıt üzerinde daha fazla denetim için, tüm yanıt iletisini de oluşturabilir ve **Httpresponseexception** ile dahil edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f1755-115">For more control over the response, you can also construct the entire response message and include it with the **HttpResponseException:**</span></span> 

[!code-csharp[Main](exception-handling/samples/sample2.cs)]

<a id="exception_filters"></a>
## <a name="exception-filters"></a><span data-ttu-id="f1755-116">Özel durum filtreleri</span><span class="sxs-lookup"><span data-stu-id="f1755-116">Exception Filters</span></span>

<span data-ttu-id="f1755-117">Web API 'nin özel durumları *özel durum filtresi*yazarak nasıl işleyeceğini özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1755-117">You can customize how Web API handles exceptions by writing an *exception filter*.</span></span> <span data-ttu-id="f1755-118">Bir denetleyici yöntemi bir **Httpresponseexception** özel durumu *olmayan* işlenmemiş özel durum oluşturduğunda bir özel durum filtresi yürütülür.</span><span class="sxs-lookup"><span data-stu-id="f1755-118">An exception filter is executed when a controller method throws any unhandled exception that is *not* an **HttpResponseException** exception.</span></span> <span data-ttu-id="f1755-119">**Httpresponseexception** türü özel bir durumdur, çünkü özellıkle bir http yanıtı döndürmek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="f1755-119">The **HttpResponseException** type is a special case, because it is designed specifically for returning an HTTP response.</span></span>

<span data-ttu-id="f1755-120">Özel durum filtreleri **System. Web. http. Filters. IExceptionFilter** arabirimini uygular.</span><span class="sxs-lookup"><span data-stu-id="f1755-120">Exception filters implement the **System.Web.Http.Filters.IExceptionFilter** interface.</span></span> <span data-ttu-id="f1755-121">Bir özel durum filtresi yazmanın en basit yolu, **System. Web. http. Filters. ExceptionFilterAttribute** sınıfından türetmektir ve **OnException** metodunu geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="f1755-121">The simplest way to write an exception filter is to derive from the **System.Web.Http.Filters.ExceptionFilterAttribute** class and override the **OnException** method.</span></span>

> [!NOTE]
> <span data-ttu-id="f1755-122">ASP.NET Web API 'sindeki özel durum filtreleri ASP.NET MVC 'de olanlarla benzerdir.</span><span class="sxs-lookup"><span data-stu-id="f1755-122">Exception filters in ASP.NET Web API are similar to those in ASP.NET MVC.</span></span> <span data-ttu-id="f1755-123">Ancak, ayrı bir ad alanında ve ayrı olarak bir işlev olarak bildirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f1755-123">However, they are declared in a separate namespace and function separately.</span></span> <span data-ttu-id="f1755-124">Özellikle, MVC 'de kullanılan **HandleErrorAttribute** sınıfı, Web API denetleyicileri tarafından oluşturulan özel durumları işlemez.</span><span class="sxs-lookup"><span data-stu-id="f1755-124">In particular, the **HandleErrorAttribute** class used in MVC does not handle exceptions thrown by Web API controllers.</span></span>

<span data-ttu-id="f1755-125">**Notimplementedexception** özel durumlarını http durum koduna 501 olarak dönüştüren bir filtre aşağıda uygulanmadı:</span><span class="sxs-lookup"><span data-stu-id="f1755-125">Here is a filter that converts **NotImplementedException** exceptions into HTTP status code 501, Not Implemented:</span></span>

[!code-csharp[Main](exception-handling/samples/sample3.cs)]

<span data-ttu-id="f1755-126">**HttpActionExecutedContext** nesnesinin **Response** özelliği istemciye gönderilecek http yanıt iletisini içerir.</span><span class="sxs-lookup"><span data-stu-id="f1755-126">The **Response** property of the **HttpActionExecutedContext** object contains the HTTP response message that will be sent to the client.</span></span>

<a id="registering_exception_filters"></a>
## <a name="registering-exception-filters"></a><span data-ttu-id="f1755-127">Özel durum filtrelerini kaydetme</span><span class="sxs-lookup"><span data-stu-id="f1755-127">Registering Exception Filters</span></span>

<span data-ttu-id="f1755-128">Web API özel durum filtresini kaydetmek için çeşitli yollar vardır:</span><span class="sxs-lookup"><span data-stu-id="f1755-128">There are several ways to register a Web API exception filter:</span></span>

- <span data-ttu-id="f1755-129">Eyleme göre</span><span class="sxs-lookup"><span data-stu-id="f1755-129">By action</span></span>
- <span data-ttu-id="f1755-130">Denetleyiciye göre</span><span class="sxs-lookup"><span data-stu-id="f1755-130">By controller</span></span>
- <span data-ttu-id="f1755-131">Görünüm</span><span class="sxs-lookup"><span data-stu-id="f1755-131">Globally</span></span>

<span data-ttu-id="f1755-132">Filtreyi belirli bir eyleme uygulamak için, filtreyi eyleme bir öznitelik olarak ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f1755-132">To apply the filter to a specific action, add the filter as an attribute to the action:</span></span>

[!code-csharp[Main](exception-handling/samples/sample4.cs)]

<span data-ttu-id="f1755-133">Filtreyi bir denetleyicideki tüm eylemlere uygulamak için, filtreyi denetleyici sınıfına bir öznitelik olarak ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f1755-133">To apply the filter to all of the actions on a controller, add the filter as an attribute to the controller class:</span></span>

[!code-csharp[Main](exception-handling/samples/sample5.cs)]

<span data-ttu-id="f1755-134">Filtreyi tüm Web API denetleyicilerine Global olarak uygulamak için, **Globalconfiguration. Configuration. Filters** koleksiyonuna bir filtrenin örneği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f1755-134">To apply the filter globally to all Web API controllers, add an instance of the filter to the **GlobalConfiguration.Configuration.Filters** collection.</span></span> <span data-ttu-id="f1755-135">Bu koleksiyondaki özel durum filtreleri Web API denetleyicisi işlemleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="f1755-135">Exception filters in this collection apply to any Web API controller action.</span></span>

[!code-csharp[Main](exception-handling/samples/sample6.cs)]

<span data-ttu-id="f1755-136">Projenizi oluşturmak için "ASP.NET MVC 4 Web uygulaması" proje şablonunu kullanırsanız, Web API yapılandırma kodunuzu uygulama\_başlangıç klasörü içinde bulunan `WebApiConfig` sınıfına koyun:</span><span class="sxs-lookup"><span data-stu-id="f1755-136">If you use the "ASP.NET MVC 4 Web Application" project template to create your project, put your Web API configuration code inside the `WebApiConfig` class, which is located in the App\_Start folder:</span></span>

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

<a id="httperror"></a>
## <a name="httperror"></a><span data-ttu-id="f1755-137">Http hatası</span><span class="sxs-lookup"><span data-stu-id="f1755-137">HttpError</span></span>

<span data-ttu-id="f1755-138">**HttpError** nesnesi, yanıt gövdesinde hata bilgilerini döndürmek için tutarlı bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="f1755-138">The **HttpError** object provides a consistent way to return error information in the response body.</span></span> <span data-ttu-id="f1755-139">Aşağıdaki örnek, yanıt gövdesinde bir **HttpError** ile 404 (bulunamadı) http durum kodunu nasıl döndürün gösterir.</span><span class="sxs-lookup"><span data-stu-id="f1755-139">The following example shows how to return HTTP status code 404 (Not Found) with an **HttpError** in the response body.</span></span>

[!code-csharp[Main](exception-handling/samples/sample8.cs)]

<span data-ttu-id="f1755-140">**Createerrorresponse** , **System .net. http. HttpRequestMessageExtensions** sınıfında tanımlanmış bir genişletme yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="f1755-140">**CreateErrorResponse** is an extension method defined in the **System.Net.Http.HttpRequestMessageExtensions** class.</span></span> <span data-ttu-id="f1755-141">Dahili olarak, **Createerrorresponse** bir **HttpError** örneği oluşturur ve ardından **HttpError**'ı içeren bir **HttpResponseMessage** oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f1755-141">Internally, **CreateErrorResponse** creates an **HttpError** instance and then creates an **HttpResponseMessage** that contains the **HttpError**.</span></span>

<span data-ttu-id="f1755-142">Bu örnekte, Yöntem başarılı olursa, HTTP yanıtında ürünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="f1755-142">In this example, if the method is successful, it returns the product in the HTTP response.</span></span> <span data-ttu-id="f1755-143">Ancak istenen ürün bulunamazsa HTTP yanıtı, istek gövdesinde bir **HttpError** içerir.</span><span class="sxs-lookup"><span data-stu-id="f1755-143">But if the requested product is not found, the HTTP response contains an **HttpError** in the request body.</span></span> <span data-ttu-id="f1755-144">Yanıt aşağıdaki gibi görünebilir:</span><span class="sxs-lookup"><span data-stu-id="f1755-144">The response might look like the following:</span></span>

[!code-console[Main](exception-handling/samples/sample9.cmd)]

<span data-ttu-id="f1755-145">Bu örnekte, **HttpError** 'ın JSON olarak serileştirildiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="f1755-145">Notice that the **HttpError** was serialized to JSON in this example.</span></span> <span data-ttu-id="f1755-146">**HttpError** kullanmanın avantajlarından biri, kesin olarak belirlenmiş diğer tüm modellerde aynı [içerik anlaşması](../formats-and-model-binding/content-negotiation.md) ve serileştirme işleminden geçmesidir.</span><span class="sxs-lookup"><span data-stu-id="f1755-146">One advantage of using **HttpError** is that it goes through the same [content-negotiation](../formats-and-model-binding/content-negotiation.md) and serialization process as any other strongly-typed model.</span></span>

### <a name="httperror-and-model-validation"></a><span data-ttu-id="f1755-147">HttpError ve model doğrulaması</span><span class="sxs-lookup"><span data-stu-id="f1755-147">HttpError and Model Validation</span></span>

<span data-ttu-id="f1755-148">Model doğrulaması için, yanıtta doğrulama hatalarını dahil etmek için model durumunu **Createerrorresponse**'a geçirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f1755-148">For model validation, you can pass the model state to **CreateErrorResponse**, to include the validation errors in the response:</span></span>

[!code-csharp[Main](exception-handling/samples/sample10.cs)]

<span data-ttu-id="f1755-149">Bu örnek aşağıdaki yanıtı döndürebilir:</span><span class="sxs-lookup"><span data-stu-id="f1755-149">This example might return the following response:</span></span>

[!code-console[Main](exception-handling/samples/sample11.cmd)]

<span data-ttu-id="f1755-150">Model doğrulama hakkında daha fazla bilgi için bkz. [ASP.NET Web API 'de model doğrulaması](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="f1755-150">For more information about model validation, see [Model Validation in ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span></span>

### <a name="using-httperror-with-httpresponseexception"></a><span data-ttu-id="f1755-151">HttpResponseException ile HttpError kullanma</span><span class="sxs-lookup"><span data-stu-id="f1755-151">Using HttpError with HttpResponseException</span></span>

<span data-ttu-id="f1755-152">Önceki örneklerde, denetleyici eyleminden bir **HttpResponseMessage** iletisi döndürülür, ancak bir **HttpError**döndürmek için **httpresponseexception** da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1755-152">The previous examples return an **HttpResponseMessage** message from the controller action, but you can also use **HttpResponseException** to return an **HttpError**.</span></span> <span data-ttu-id="f1755-153">Bu, normal başarı durumunda kesin türü belirtilmiş bir model döndürmenizi sağlarken bir hata varsa, yine de **HttpError** döndürüyor:</span><span class="sxs-lookup"><span data-stu-id="f1755-153">This lets you return a strongly-typed model in the normal success case, while still returning **HttpError** if there is an error:</span></span>

[!code-csharp[Main](exception-handling/samples/sample12.cs)]
