---
uid: web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
title: ASP.NET Web API-ASP.NET 4. x içinde parametre bağlama
author: MikeWasson
description: Web API 'sinin parametreleri nasıl bağlatlarının ve ASP.NET 4. x içinde bağlama işleminin nasıl özelleştirileceğini açıklar.
ms.author: riande
ms.date: 07/11/2013
ms.custom: seoapril2019
ms.assetid: e42c8388-04ed-4341-9fdb-41b1b4c06320
msc.legacyurl: /web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 032368f94ce32cf6231458649e8fdd42bee685e9
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519264"
---
# <a name="parameter-binding-in-aspnet-web-api"></a><span data-ttu-id="b35e4-103">ASP.NET Web API 'sinde parametre bağlama</span><span class="sxs-lookup"><span data-stu-id="b35e4-103">Parameter Binding in ASP.NET Web API</span></span>

<span data-ttu-id="b35e4-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b35e4-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[!INCLUDE[](~/includes/coreWebAPI.md)]

<span data-ttu-id="b35e4-105">Bu makale, Web API 'sinin parametreleri nasıl bağlamakta olduğunu ve bağlama işlemini nasıl özelleştirebileceğinizi açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="b35e4-105">This article describes how Web API binds parameters, and how you can customize the binding process.</span></span> <span data-ttu-id="b35e4-106">Web API 'SI bir denetleyicide bir yöntemi çağırdığında,, *bağlama*adlı bir işlem olan parametrelerin değerlerini ayarlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b35e4-106">When Web API calls a method on a controller, it must set values for the parameters, a process called *binding*.</span></span>

<span data-ttu-id="b35e4-107">Varsayılan olarak, Web API parametreleri bağlamak için aşağıdaki kuralları kullanır:</span><span class="sxs-lookup"><span data-stu-id="b35e4-107">By default, Web API uses the following rules to bind parameters:</span></span>

- <span data-ttu-id="b35e4-108">Parametre "basit" bir tür ise, Web API 'SI URI 'den değeri almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="b35e4-108">If the parameter is a "simple" type, Web API tries to get the value from the URI.</span></span> <span data-ttu-id="b35e4-109">Basit türler, .NET [ilkel türlerini](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) (**int**, **bool**, **Double**, vb.), artı **TimeSpan**, **DateTime**, **Guid**, **Decimal**, ve **String**ve bir dizeden dönüştürebileceğiniz tür dönüştürücüsü *olan herhangi bir* türü içerir.</span><span class="sxs-lookup"><span data-stu-id="b35e4-109">Simple types include the .NET [primitive types](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) (**int**, **bool**, **double**, and so forth), plus **TimeSpan**, **DateTime**, **Guid**, **decimal**, and **string**, *plus* any type with a type converter that can convert from a string.</span></span> <span data-ttu-id="b35e4-110">(Daha sonra tür dönüştürücüler hakkında daha fazla bilgi.)</span><span class="sxs-lookup"><span data-stu-id="b35e4-110">(More about type converters later.)</span></span>
- <span data-ttu-id="b35e4-111">Karmaşık türler için Web API 'SI, bir [medya türü biçimlendirici](media-formatters.md)kullanarak ileti gövdesinden değeri okumaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="b35e4-111">For complex types, Web API tries to read the value from the message body, using a [media-type formatter](media-formatters.md).</span></span>

<span data-ttu-id="b35e4-112">Örneğin, tipik bir Web API denetleyici yöntemi aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b35e4-112">For example, here is a typical Web API controller method:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="b35e4-113">*ID* parametresi &quot;basit bir&quot; türüdür, bu nedenle Web API 'SI istek URI 'sinden değeri almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="b35e4-113">The *id* parameter is a &quot;simple&quot; type, so Web API tries to get the value from the request URI.</span></span> <span data-ttu-id="b35e4-114">*Öğe* parametresi karmaşık bir türdür, bu nedenle Web API 'si, istek gövdesinden değeri okumak için bir medya türü biçimlendirici kullanır.</span><span class="sxs-lookup"><span data-stu-id="b35e4-114">The *item* parameter is a complex type, so Web API uses a media-type formatter to read the value from the request body.</span></span>

<span data-ttu-id="b35e4-115">URI 'den bir değer almak için Web API 'si yol verilerine ve URI sorgu dizesine bakar.</span><span class="sxs-lookup"><span data-stu-id="b35e4-115">To get a value from the URI, Web API looks in the route data and the URI query string.</span></span> <span data-ttu-id="b35e4-116">Yönlendirme sistemi URI 'yi ayrıştırdığında ve bir rota ile eşleştiğinde rota verileri doldurulur.</span><span class="sxs-lookup"><span data-stu-id="b35e4-116">The route data is populated when the routing system parses the URI and matches it to a route.</span></span> <span data-ttu-id="b35e4-117">Daha fazla bilgi için bkz. [Yönlendirme ve eylem seçimi](../web-api-routing-and-actions/routing-and-action-selection.md).</span><span class="sxs-lookup"><span data-stu-id="b35e4-117">For more information, see [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span>

<span data-ttu-id="b35e4-118">Bu makalenin geri kalanında, model bağlama işlemini nasıl özelleştirebileceğinizi göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="b35e4-118">In the rest of this article, I'll show how you can customize the model binding process.</span></span> <span data-ttu-id="b35e4-119">Ancak karmaşık türler için, mümkün olduğunda medya türü formatlayıcıları kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="b35e4-119">For complex types, however, consider using media-type formatters whenever possible.</span></span> <span data-ttu-id="b35e4-120">HTTP 'nin önemli prensibi, kaynak gösterimini belirtmek için içerik görüşmesi kullanılarak ileti gövdesinde kaynakların gönderilmektir.</span><span class="sxs-lookup"><span data-stu-id="b35e4-120">A key principle of HTTP is that resources are sent in the message body, using content negotiation to specify the representation of the resource.</span></span> <span data-ttu-id="b35e4-121">Medya türü formatlayıcıları tam olarak bu amaçla tasarlanmıştı.</span><span class="sxs-lookup"><span data-stu-id="b35e4-121">Media-type formatters were designed for exactly this purpose.</span></span>

## <a name="using-fromuri"></a><span data-ttu-id="b35e4-122">[FromUri] kullanma</span><span class="sxs-lookup"><span data-stu-id="b35e4-122">Using [FromUri]</span></span>

<span data-ttu-id="b35e4-123">Web API 'sini URI 'den karmaşık bir tür okuyacak şekilde zorlamak için, parametresine **[Fromuri]** özniteliğini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b35e4-123">To force Web API to read a complex type from the URI, add the **[FromUri]** attribute to the parameter.</span></span> <span data-ttu-id="b35e4-124">Aşağıdaki örnek, URI 'den `GeoPoint` alan bir denetleyici yöntemiyle birlikte `GeoPoint` türünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b35e4-124">The following example defines a `GeoPoint` type, along with a controller method that gets the `GeoPoint` from the URI.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="b35e4-125">İstemci, enlem ve boylam değerlerini sorgu dizesine yerleştirebilir ve Web API 'SI bunları bir `GeoPoint`oluşturmak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="b35e4-125">The client can put the Latitude and Longitude values in the query string and Web API will use them to construct a `GeoPoint`.</span></span> <span data-ttu-id="b35e4-126">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b35e4-126">For example:</span></span>

`http://localhost/api/values/?Latitude=47.678558&Longitude=-122.130989`

## <a name="using-frombody"></a><span data-ttu-id="b35e4-127">[FromBody] kullanma</span><span class="sxs-lookup"><span data-stu-id="b35e4-127">Using [FromBody]</span></span>

<span data-ttu-id="b35e4-128">Web API 'sini istek gövdesinden basit bir tür okuyacak şekilde zorlamak için, **[Frombody]** özniteliğini parametresine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b35e4-128">To force Web API to read a simple type from the request body, add the **[FromBody]** attribute to the parameter:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="b35e4-129">Bu örnekte, Web API 'SI, istek gövdesinden *adı* değerini okumak için bir medya türü biçimlendirici kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="b35e4-129">In this example, Web API will use a media-type formatter to read the value of *name* from the request body.</span></span> <span data-ttu-id="b35e4-130">Örnek bir istemci isteği aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b35e4-130">Here is an example client request.</span></span>

[!code-console[Main](parameter-binding-in-aspnet-web-api/samples/sample4.cmd)]

<span data-ttu-id="b35e4-131">Bir parametre [FromBody] olduğunda, Web API 'SI bir biçimlendirici seçmek için Content-Type üst bilgisini kullanır.</span><span class="sxs-lookup"><span data-stu-id="b35e4-131">When a parameter has [FromBody], Web API uses the Content-Type header to select a formatter.</span></span> <span data-ttu-id="b35e4-132">Bu örnekte, içerik türü &quot;Application/JSON&quot; ve istek gövdesi ham JSON dizesidir (JSON nesnesi değil).</span><span class="sxs-lookup"><span data-stu-id="b35e4-132">In this example, the content type is &quot;application/json&quot; and the request body is a raw JSON string (not a JSON object).</span></span>

<span data-ttu-id="b35e4-133">İleti gövdesinden en fazla bir parametrenin okumasına izin verilir.</span><span class="sxs-lookup"><span data-stu-id="b35e4-133">At most one parameter is allowed to read from the message body.</span></span> <span data-ttu-id="b35e4-134">Bu nedenle, bu çalışmaz:</span><span class="sxs-lookup"><span data-stu-id="b35e4-134">So this will not work:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="b35e4-135">Bu kuralın nedeni, istek gövdesinin yalnızca bir kez okunabilecek, arabelleğe alınmamış bir akışa depolanabileceği bir akışdır.</span><span class="sxs-lookup"><span data-stu-id="b35e4-135">The reason for this rule is that the request body might be stored in a non-buffered stream that can only be read once.</span></span>

## <a name="type-converters"></a><span data-ttu-id="b35e4-136">Tür dönüştürücüler</span><span class="sxs-lookup"><span data-stu-id="b35e4-136">Type Converters</span></span>

<span data-ttu-id="b35e4-137">Bir **TypeConverter** 'ı oluşturarak ve bir dize dönüştürmesi sağlayarak Web API 'sinin bir sınıfı basit bir tür olarak (Web API 'sini URI 'den bağlamaya çalışacak şekilde) görmesini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b35e4-137">You can make Web API treat a class as a simple type (so that Web API will try to bind it from the URI) by creating a **TypeConverter** and providing a string conversion.</span></span>

<span data-ttu-id="b35e4-138">Aşağıdaki kod, bir coğrafi noktayı temsil eden bir `GeoPoint` sınıfını ve dizelerden `GeoPoint` örneklerine dönüştüren bir **TypeConverter** 'ı gösterir.</span><span class="sxs-lookup"><span data-stu-id="b35e4-138">The following code shows a `GeoPoint` class that represents a geographical point, plus a **TypeConverter** that converts from strings to `GeoPoint` instances.</span></span> <span data-ttu-id="b35e4-139">`GeoPoint` sınıfı, tür dönüştürücüsünü belirtmek için bir **[TypeConverter]** özniteliğiyle donatılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b35e4-139">The `GeoPoint` class is decorated with a **[TypeConverter]** attribute to specify the type converter.</span></span> <span data-ttu-id="b35e4-140">(Bu örnek, Mike Stall 'ın Web günlüğü gönderisini [MVC/WebAPI içindeki eylem imzalarındaki özel nesnelere bağlama](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx).)</span><span class="sxs-lookup"><span data-stu-id="b35e4-140">(This example was inspired by Mike Stall's blog post [How to bind to custom objects in action signatures in MVC/WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx).)</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="b35e4-141">Şimdi Web API 'SI `GeoPoint` basit bir tür olarak değerlendirir, yani `GeoPoint` parametrelerini URI 'den bağlamaya çalışacaktır.</span><span class="sxs-lookup"><span data-stu-id="b35e4-141">Now Web API will treat `GeoPoint` as a simple type, meaning it will try to bind `GeoPoint` parameters from the URI.</span></span> <span data-ttu-id="b35e4-142">Parametreye **[Fromuri]** eklemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="b35e4-142">You don't need to include **[FromUri]** on the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="b35e4-143">İstemci, yöntemi aşağıdaki gibi bir URI ile çağırabilir:</span><span class="sxs-lookup"><span data-stu-id="b35e4-143">The client can invoke the method with a URI like this:</span></span>

`http://localhost/api/values/?location=47.678558,-122.130989`

## <a name="model-binders"></a><span data-ttu-id="b35e4-144">Model ciltleri</span><span class="sxs-lookup"><span data-stu-id="b35e4-144">Model Binders</span></span>

<span data-ttu-id="b35e4-145">Tür dönüştürücüden daha esnek bir seçenek, özel model Bağlayıcısı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="b35e4-145">A more flexible option than a type converter is to create a custom model binder.</span></span> <span data-ttu-id="b35e4-146">Model Ciltçi ile HTTP isteği, eylem açıklaması ve rota verilerinden ham değerler gibi şeylere erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b35e4-146">With a model binder, you have access to things like the HTTP request, the action description, and the raw values from the route data.</span></span>

<span data-ttu-id="b35e4-147">Bir model Bağlayıcısı oluşturmak için **ımodelciltçi** arabirimini uygulayın.</span><span class="sxs-lookup"><span data-stu-id="b35e4-147">To create a model binder, implement the **IModelBinder** interface.</span></span> <span data-ttu-id="b35e4-148">Bu arabirim tek bir yöntemi tanımlar, **BindModel**:</span><span class="sxs-lookup"><span data-stu-id="b35e4-148">This interface defines a single method, **BindModel**:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample8.cs)]

<span data-ttu-id="b35e4-149">`GeoPoint` nesneler için bir model Bağlayıcısı aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b35e4-149">Here is a model binder for `GeoPoint` objects.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="b35e4-150">Model Ciltçi, bir *değer sağlayıcısından*ham giriş değerleri alır.</span><span class="sxs-lookup"><span data-stu-id="b35e4-150">A model binder gets raw input values from a *value provider*.</span></span> <span data-ttu-id="b35e4-151">Bu tasarım iki ayrı işlevi ayırır:</span><span class="sxs-lookup"><span data-stu-id="b35e4-151">This design separates two distinct functions:</span></span>

- <span data-ttu-id="b35e4-152">Değer sağlayıcısı, HTTP isteğini alır ve anahtar-değer çiftlerinin bir sözlüğünü doldurur.</span><span class="sxs-lookup"><span data-stu-id="b35e4-152">The value provider takes the HTTP request and populates a dictionary of key-value pairs.</span></span>
- <span data-ttu-id="b35e4-153">Model Ciltçi, modeli doldurmak için bu sözlüğü kullanır.</span><span class="sxs-lookup"><span data-stu-id="b35e4-153">The model binder uses this dictionary to populate the model.</span></span>

<span data-ttu-id="b35e4-154">Web API 'sindeki varsayılan değer sağlayıcısı, rota verilerinden ve sorgu dizesinden değerleri alır.</span><span class="sxs-lookup"><span data-stu-id="b35e4-154">The default value provider in Web API gets values from the route data and the query string.</span></span> <span data-ttu-id="b35e4-155">Örneğin, URI `http://localhost/api/values/1?location=48,-122`ise, değer sağlayıcı aşağıdaki anahtar-değer çiftlerini oluşturur:</span><span class="sxs-lookup"><span data-stu-id="b35e4-155">For example, if the URI is `http://localhost/api/values/1?location=48,-122`, the value provider creates the following key-value pairs:</span></span>

- <span data-ttu-id="b35e4-156">kimlik = &quot;1&quot;</span><span class="sxs-lookup"><span data-stu-id="b35e4-156">id = &quot;1&quot;</span></span>
- <span data-ttu-id="b35e4-157">Konum = &quot;48.122&quot;</span><span class="sxs-lookup"><span data-stu-id="b35e4-157">location = &quot;48,122&quot;</span></span>

<span data-ttu-id="b35e4-158">(&quot;API/{Controller}/{ID}&quot;varsayılan yol şablonunu kabul ediyorum.)</span><span class="sxs-lookup"><span data-stu-id="b35e4-158">(I'm assuming the default route template, which is &quot;api/{controller}/{id}&quot;.)</span></span>

<span data-ttu-id="b35e4-159">Bağlanacak parametrenin adı, **ModelBindingContext. ModelName** özelliğinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="b35e4-159">The name of the parameter to bind is stored in the **ModelBindingContext.ModelName** property.</span></span> <span data-ttu-id="b35e4-160">Model Ciltçi, sözlükte bu değere sahip bir anahtar arar.</span><span class="sxs-lookup"><span data-stu-id="b35e4-160">The model binder looks for a key with this value in the dictionary.</span></span> <span data-ttu-id="b35e4-161">Değer varsa ve bir `GeoPoint`dönüştürülebiliyorsanız model Ciltçi, bağlantılı değeri **ModelBindingContext. model** özelliğine atar.</span><span class="sxs-lookup"><span data-stu-id="b35e4-161">If the value exists and can be converted into a `GeoPoint`, the model binder assigns the bound value to the **ModelBindingContext.Model** property.</span></span>

<span data-ttu-id="b35e4-162">Model cildin basit bir tür dönüştürmesi ile sınırlı olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="b35e4-162">Notice that the model binder is not limited to a simple type conversion.</span></span> <span data-ttu-id="b35e4-163">Bu örnekte, model cildi ilk olarak bilinen konumların bir tablosuna bakar ve bu başarısız olursa, tür dönüştürme kullanır.</span><span class="sxs-lookup"><span data-stu-id="b35e4-163">In this example, the model binder first looks in a table of known locations, and if that fails, it uses type conversion.</span></span>

<span data-ttu-id="b35e4-164">**Model cildi ayarlama**</span><span class="sxs-lookup"><span data-stu-id="b35e4-164">**Setting the Model Binder**</span></span>

<span data-ttu-id="b35e4-165">Model cildi ayarlamak için çeşitli yollar vardır.</span><span class="sxs-lookup"><span data-stu-id="b35e4-165">There are several ways to set a model binder.</span></span> <span data-ttu-id="b35e4-166">İlk olarak, parametresine bir **[Modelciltçi]** özniteliği ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b35e4-166">First, you can add a **[ModelBinder]** attribute to the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample10.cs)]

<span data-ttu-id="b35e4-167">Ayrıca, türüne bir **[Modelciltçi]** özniteliği ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b35e4-167">You can also add a **[ModelBinder]** attribute to the type.</span></span> <span data-ttu-id="b35e4-168">Web API 'SI, bu türün tüm parametreleri için belirtilen model cildi kullanır.</span><span class="sxs-lookup"><span data-stu-id="b35e4-168">Web API will use the specified model binder for all parameters of that type.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="b35e4-169">Son olarak, bir model Ciltçi sağlayıcısını **HttpConfiguration**'a ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b35e4-169">Finally, you can add a model-binder provider to the **HttpConfiguration**.</span></span> <span data-ttu-id="b35e4-170">Model Ciltçi sağlayıcısı, model cildi oluşturan bir fabrika sınıfıdır.</span><span class="sxs-lookup"><span data-stu-id="b35e4-170">A model-binder provider is simply a factory class that creates a model binder.</span></span> <span data-ttu-id="b35e4-171">[ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) sınıfından türeterek bir sağlayıcı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b35e4-171">You can create a provider by deriving from the [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) class.</span></span> <span data-ttu-id="b35e4-172">Ancak, model Ciltçi tek bir tür işlediğinde, bu amaçla tasarlanan yerleşik **SimpleModelBinderProvider**kullanımı daha kolay olur.</span><span class="sxs-lookup"><span data-stu-id="b35e4-172">However, if your model binder handles a single type, it's easier to use the built-in **SimpleModelBinderProvider**, which is designed for this purpose.</span></span> <span data-ttu-id="b35e4-173">Aşağıdaki kod bunun nasıl yapılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b35e4-173">The following code shows how to do this.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample12.cs)]

<span data-ttu-id="b35e4-174">Model bağlama sağlayıcısıyla, Web API 'sini bir medya türü biçimlendirici değil, model cildi kullanması gerektiğini söylemek için, **[modelciltçi]** özniteliğini parametreye eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b35e4-174">With a model-binding provider, you still need to add the **[ModelBinder]** attribute to the parameter, to tell Web API that it should use a model binder and not a media-type formatter.</span></span> <span data-ttu-id="b35e4-175">Ancak şimdi özniteliğinde model cildin türünü belirtmeniz gerekmez:</span><span class="sxs-lookup"><span data-stu-id="b35e4-175">But now you don't need to specify the type of model binder in the attribute:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample13.cs)]

## <a name="value-providers"></a><span data-ttu-id="b35e4-176">Değer sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="b35e4-176">Value Providers</span></span>

<span data-ttu-id="b35e4-177">Model cildin bir değer sağlayıcısından değerler aldığından bahsetdim.</span><span class="sxs-lookup"><span data-stu-id="b35e4-177">I mentioned that a model binder gets values from a value provider.</span></span> <span data-ttu-id="b35e4-178">Özel bir değer sağlayıcısı yazmak için **IValueProvider** arabirimini uygulayın.</span><span class="sxs-lookup"><span data-stu-id="b35e4-178">To write a custom value provider, implement the **IValueProvider** interface.</span></span> <span data-ttu-id="b35e4-179">İşte, istekteki tanımlama bilgilerinden değer çeken bir örnek:</span><span class="sxs-lookup"><span data-stu-id="b35e4-179">Here is an example that pulls values from the cookies in the request:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample14.cs)]

<span data-ttu-id="b35e4-180">Ayrıca, **ValueProviderFactory** sınıfından türeterek bir değer sağlayıcısı fabrikası oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b35e4-180">You also need to create a value provider factory by deriving from the **ValueProviderFactory** class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample15.cs)]

<span data-ttu-id="b35e4-181">Değer sağlayıcısı fabrikasını **HttpConfiguration** öğesine aşağıdaki şekilde ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b35e4-181">Add the value provider factory to the **HttpConfiguration** as follows.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample16.cs)]

<span data-ttu-id="b35e4-182">Web API 'SI, tüm değer sağlayıcılarını oluşturur, bu nedenle model Ciltçi **ValueProvider. GetValue**' yi çağırdığında, model cildi onu üretebilecek ilk değer sağlayıcısından değeri alır.</span><span class="sxs-lookup"><span data-stu-id="b35e4-182">Web API composes all of the value providers, so when a model binder calls **ValueProvider.GetValue**, the model binder receives the value from the first value provider that is able to produce it.</span></span>

<span data-ttu-id="b35e4-183">Alternatif olarak, değer sağlayıcı fabrikasını parametre düzeyinde, **ValueProvider** özniteliğini kullanarak aşağıdaki gibi ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b35e4-183">Alternatively, you can set the value provider factory at the parameter level by using the **ValueProvider** attribute, as follows:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample17.cs)]

<span data-ttu-id="b35e4-184">Bu, Web API 'sinin belirtilen değer sağlayıcı fabrikası ile model bağlamayı kullanmasını söyler ve diğer kayıtlı değer sağlayıcılarının hiçbirini kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="b35e4-184">This tells Web API to use model binding with the specified value provider factory, and not to use any of the other registered value providers.</span></span>

## <a name="httpparameterbinding"></a><span data-ttu-id="b35e4-185">HttpParameterBinding</span><span class="sxs-lookup"><span data-stu-id="b35e4-185">HttpParameterBinding</span></span>

<span data-ttu-id="b35e4-186">Model ciltleri, daha genel bir mekanizmanın belirli bir örneğidir.</span><span class="sxs-lookup"><span data-stu-id="b35e4-186">Model binders are a specific instance of a more general mechanism.</span></span> <span data-ttu-id="b35e4-187">**[Modelciltçi]** özniteliğine bakarsanız, onun soyut **ParameterBindingAttribute** sınıfından türetildiğinden emin olursunuz.</span><span class="sxs-lookup"><span data-stu-id="b35e4-187">If you look at the **[ModelBinder]** attribute, you will see that it derives from the abstract **ParameterBindingAttribute** class.</span></span> <span data-ttu-id="b35e4-188">Bu sınıf, bir **Httpparameterbinding** nesnesi döndüren **GetBinding**tek bir yöntemini tanımlar:</span><span class="sxs-lookup"><span data-stu-id="b35e4-188">This class defines a single method, **GetBinding**, which returns an **HttpParameterBinding** object:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample18.cs)]

<span data-ttu-id="b35e4-189">Bir **Httpparameterbinding** , bir parametreyi bir değere bağlamaktan sorumludur.</span><span class="sxs-lookup"><span data-stu-id="b35e4-189">An **HttpParameterBinding** is responsible for binding a parameter to a value.</span></span> <span data-ttu-id="b35e4-190">**[Modelciltçi]** söz konusu olduğunda, öznitelik gerçek bağlamayı gerçekleştirmek Için **ımodelciltçi** kullanan bir **httpparameterbinding** uygulaması döndürür.</span><span class="sxs-lookup"><span data-stu-id="b35e4-190">In the case of **[ModelBinder]**, the attribute returns an **HttpParameterBinding** implementation that uses an **IModelBinder** to perform the actual binding.</span></span> <span data-ttu-id="b35e4-191">Ayrıca kendi **Httpparameterbinding**'nizi de uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b35e4-191">You can also implement your own **HttpParameterBinding**.</span></span>

<span data-ttu-id="b35e4-192">Örneğin, istekteki `if-match` ve `if-none-match` üst bilgilerden ETags almak istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="b35e4-192">For example, suppose you want to get ETags from `if-match` and `if-none-match` headers in the request.</span></span> <span data-ttu-id="b35e4-193">ETags temsil eden bir sınıf tanımlayarak başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="b35e4-193">We'll start by defining a class to represent ETags.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample19.cs)]

<span data-ttu-id="b35e4-194">Ayrıca, `if-match` üst bilgisinden veya `if-none-match` üst bilgisinden ETag 'in mi alınacağını göstermek için bir sabit listesi tanımlayacağız.</span><span class="sxs-lookup"><span data-stu-id="b35e4-194">We'll also define an enumeration to indicate whether to get the ETag from the `if-match` header or the `if-none-match` header.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample20.cs)]

<span data-ttu-id="b35e4-195">Burada, istenen üst bilgiden ETag 'i alan ve ETag türü bir parametreye bağlayan bir **Httpparameterbinding** yer alır:</span><span class="sxs-lookup"><span data-stu-id="b35e4-195">Here is an **HttpParameterBinding** that gets the ETag from the desired header and binds it to a parameter of type ETag:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample21.cs)]

<span data-ttu-id="b35e4-196">**Executebindingasync** yöntemi bağlamayı yapar.</span><span class="sxs-lookup"><span data-stu-id="b35e4-196">The **ExecuteBindingAsync** method does the binding.</span></span> <span data-ttu-id="b35e4-197">Bu yöntemde, bir bağlama parametre değerini **Httpactioncontext**Içindeki **actionargument** sözlüğüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b35e4-197">Within this method, add the bound parameter value to the **ActionArgument** dictionary in the **HttpActionContext**.</span></span>

> [!NOTE]
> <span data-ttu-id="b35e4-198">**Executebindingasync** yönteminiz istek iletisinin gövdesini okuyorsa, true döndürecek şekilde **willreadbody** özelliğini geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="b35e4-198">If your **ExecuteBindingAsync** method reads the body of the request message, override the **WillReadBody** property to return true.</span></span> <span data-ttu-id="b35e4-199">İstek gövdesi, yalnızca bir kez okunabilecek, arabelleğe alınmamış bir akış olabilir, bu nedenle Web API 'SI en çok bir bağlamanın ileti gövdesini okuyabilecek bir kuralı zorlar.</span><span class="sxs-lookup"><span data-stu-id="b35e4-199">The request body might be an unbuffered stream that can only be read once, so Web API enforces a rule that at most one binding can read the message body.</span></span>

<span data-ttu-id="b35e4-200">Özel bir **Httpparameterbinding**uygulamak Için **ParameterBindingAttribute**öğesinden türetilen bir öznitelik tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b35e4-200">To apply a custom **HttpParameterBinding**, you can define an attribute that derives from **ParameterBindingAttribute**.</span></span> <span data-ttu-id="b35e4-201">`ETagParameterBinding`için biri `if-match` üst bilgileri ve bir `if-none-match` üst bilgisi için olmak üzere iki öznitelik tanımlayacağız.</span><span class="sxs-lookup"><span data-stu-id="b35e4-201">For `ETagParameterBinding`, we'll define two attributes, one for `if-match` headers and one for `if-none-match` headers.</span></span> <span data-ttu-id="b35e4-202">Her ikisi de soyut bir temel sınıftan türetir.</span><span class="sxs-lookup"><span data-stu-id="b35e4-202">Both derive from an abstract base class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample22.cs)]

<span data-ttu-id="b35e4-203">`[IfNoneMatch]` özniteliğini kullanan bir Controller yöntemi aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b35e4-203">Here is a controller method that uses the `[IfNoneMatch]` attribute.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample23.cs)]

<span data-ttu-id="b35e4-204">**ParameterBindingAttribute**'un yanı sıra özel bir **httpparameterbinding**eklemek için başka bir kanca vardır.</span><span class="sxs-lookup"><span data-stu-id="b35e4-204">Besides **ParameterBindingAttribute**, there is another hook for adding a custom **HttpParameterBinding**.</span></span> <span data-ttu-id="b35e4-205">**HttpConfiguration** nesnesinde **parameterbindingrules** özelliği, (**HttpParameterDescriptor** -&gt; **httpparameterbinding**) türündeki anonim işlevlerin bir koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="b35e4-205">On the **HttpConfiguration** object, the **ParameterBindingRules** property is a collection of anonymous functions of type (**HttpParameterDescriptor** -&gt; **HttpParameterBinding**).</span></span> <span data-ttu-id="b35e4-206">Örneğin, GET yöntemindeki herhangi bir ETag parametresinin `if-none-match``ETagParameterBinding` kullandığı bir kural ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b35e4-206">For example, you could add a rule that any ETag parameter on a GET method uses `ETagParameterBinding` with `if-none-match`:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample24.cs)]

<span data-ttu-id="b35e4-207">İşlev, bağlamanın geçerli olmadığı parametreler için `null` döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="b35e4-207">The function should return `null` for parameters where the binding is not applicable.</span></span>

## <a name="iactionvaluebinder"></a><span data-ttu-id="b35e4-208">Iactionvalueciltçi</span><span class="sxs-lookup"><span data-stu-id="b35e4-208">IActionValueBinder</span></span>

<span data-ttu-id="b35e4-209">Tüm parametre bağlama işlemi takılabilir bir hizmet olan **ıactionvalueciltçi**tarafından denetlenir.</span><span class="sxs-lookup"><span data-stu-id="b35e4-209">The entire parameter-binding process is controlled by a pluggable service, **IActionValueBinder**.</span></span> <span data-ttu-id="b35e4-210">**Iactionvalueciltçi** 'nin varsayılan uygulaması aşağıdakileri yapar:</span><span class="sxs-lookup"><span data-stu-id="b35e4-210">The default implementation of **IActionValueBinder** does the following:</span></span>

1. <span data-ttu-id="b35e4-211">Parametresinde bir **ParameterBindingAttribute** bulun.</span><span class="sxs-lookup"><span data-stu-id="b35e4-211">Look for a **ParameterBindingAttribute** on the parameter.</span></span> <span data-ttu-id="b35e4-212">Buna **[Frombody]** , **[fromuri]** ve **[modelciltçi]** ya da özel öznitelikler dahildir.</span><span class="sxs-lookup"><span data-stu-id="b35e4-212">This includes **[FromBody]**, **[FromUri]**, and **[ModelBinder]**, or custom attributes.</span></span>
2. <span data-ttu-id="b35e4-213">Aksi halde, null olmayan bir **Httpparameterbinding**döndüren bir Işlev Için **HttpConfiguration. parameterbindingrules** bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="b35e4-213">Otherwise, look in **HttpConfiguration.ParameterBindingRules** for a function that returns a non-null **HttpParameterBinding**.</span></span>
3. <span data-ttu-id="b35e4-214">Aksi takdirde, daha önce açıklananlardan varsayılan kuralları kullanın.</span><span class="sxs-lookup"><span data-stu-id="b35e4-214">Otherwise, use the default rules that I described previously.</span></span> 

    - <span data-ttu-id="b35e4-215">Parametre türü "basittir" ise veya tür dönüştürücüsüyle, URI 'den bağlayın.</span><span class="sxs-lookup"><span data-stu-id="b35e4-215">If the parameter type is "simple"or has a type converter, bind from the URI.</span></span> <span data-ttu-id="b35e4-216">Bu, **[Fromuri]** özniteliğini parametreye koymaya eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="b35e4-216">This is equivalent to putting the **[FromUri]** attribute on the parameter.</span></span>
    - <span data-ttu-id="b35e4-217">Aksi takdirde, ileti gövdesinden parametresini okumayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="b35e4-217">Otherwise, try to read the parameter from the message body.</span></span> <span data-ttu-id="b35e4-218">Bu parametre üzerine **[Frombody]** koymaya eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="b35e4-218">This is equivalent to putting **[FromBody]** on the parameter.</span></span>

<span data-ttu-id="b35e4-219">İsterseniz, tüm **ıactionvalueciltçi** hizmetini özel bir uygulamayla değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b35e4-219">If you wanted, you could replace the entire **IActionValueBinder** service with a custom implementation.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b35e4-220">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b35e4-220">Additional Resources</span></span>

[<span data-ttu-id="b35e4-221">Özel parametre bağlama örneği</span><span class="sxs-lookup"><span data-stu-id="b35e4-221">Custom Parameter Binding Sample</span></span>](http://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/CustomParameterBinding)

<span data-ttu-id="b35e4-222">Mike Stall, Web API parametresi bağlaması hakkında iyi bir blog gönderisi serisi yazdı:</span><span class="sxs-lookup"><span data-stu-id="b35e4-222">Mike Stall wrote a good series of blog posts about Web API parameter binding:</span></span>

- [<span data-ttu-id="b35e4-223">Web API parametre bağlamayı nasıl yapar</span><span class="sxs-lookup"><span data-stu-id="b35e4-223">How Web API does Parameter Binding</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/16/how-webapi-does-parameter-binding.aspx)
- [<span data-ttu-id="b35e4-224">Web API 'SI için MVC stil parametresi bağlama</span><span class="sxs-lookup"><span data-stu-id="b35e4-224">MVC Style parameter binding for Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/18/mvc-style-parameter-binding-for-webapi.aspx)
- [<span data-ttu-id="b35e4-225">MVC/web API 'de eylem imzalarında özel nesnelere bağlama</span><span class="sxs-lookup"><span data-stu-id="b35e4-225">How to bind to custom objects in action signatures in MVC/Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)
- [<span data-ttu-id="b35e4-226">Web API 'de özel değer sağlayıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b35e4-226">How to create a custom value provider in Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)
- [<span data-ttu-id="b35e4-227">Altyapı altında Web API parametresi bağlama</span><span class="sxs-lookup"><span data-stu-id="b35e4-227">Web API Parameter binding under the hood</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)
