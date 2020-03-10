---
uid: web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
title: ASP.NET Web API-ASP.NET 4. x içinde model doğrulaması
author: MikeWasson
description: ASP.NET 4. x için ASP.NET Web API 'sinde model doğrulamasına genel bakış.
ms.author: riande
ms.date: 07/20/2012
ms.custom: seoapril2019
ms.assetid: 7d061207-22b8-4883-bafa-e89b1e7749ca
msc.legacyurl: /web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 531a66b7ab642bd012663517640f2766f1917f25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557241"
---
# <a name="model-validation-in-aspnet-web-api"></a><span data-ttu-id="c1119-103">ASP.NET Web API 'de model doğrulaması</span><span class="sxs-lookup"><span data-stu-id="c1119-103">Model Validation in ASP.NET Web API</span></span>

<span data-ttu-id="c1119-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c1119-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="c1119-105">Bu makalede, modellerinize not ekleme, veri doğrulama için ek açıklamaları kullanma ve Web API 'nizin doğrulama hatalarını işleme işlemlerinin nasıl yapılacağı gösterilir.</span><span class="sxs-lookup"><span data-stu-id="c1119-105">This article shows how to annotate your models, use the annotations for data validation, and handle validation errors in your web API.</span></span> <span data-ttu-id="c1119-106">Bir istemci Web API 'nize veri gönderdiğinde, genellikle herhangi bir işlem yapmadan önce verileri doğrulamak istersiniz.</span><span class="sxs-lookup"><span data-stu-id="c1119-106">When a client sends data to your web API, often you want to validate the data before doing any processing.</span></span> 

## <a name="data-annotations"></a><span data-ttu-id="c1119-107">Veri Açıklamaları</span><span class="sxs-lookup"><span data-stu-id="c1119-107">Data Annotations</span></span>

<span data-ttu-id="c1119-108">ASP.NET Web API 'sinde, modelinizdeki özelliklerin doğrulama kurallarını ayarlamak için [System. ComponentModel. Dataaçıklamalarda](/dotnet/api/system.componentmodel.dataannotations) ad alanındaki öznitelikleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c1119-108">In ASP.NET Web API, you can use attributes from the [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) namespace to set validation rules for properties on your model.</span></span> <span data-ttu-id="c1119-109">Aşağıdaki modeli göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="c1119-109">Consider the following model:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="c1119-110">ASP.NET MVC 'de model doğrulaması kullandıysanız, bu tanıdık gelmelidir.</span><span class="sxs-lookup"><span data-stu-id="c1119-110">If you have used model validation in ASP.NET MVC, this should look familiar.</span></span> <span data-ttu-id="c1119-111">**Gerekli** öznitelik `Name` özelliğinin null olmaması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="c1119-111">The **Required** attribute says that the `Name` property must not be null.</span></span> <span data-ttu-id="c1119-112">**Range** özniteliği `Weight` sıfır ile 999 arasında olması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="c1119-112">The **Range** attribute says that `Weight` must be between zero and 999.</span></span>

<span data-ttu-id="c1119-113">Bir istemcinin aşağıdaki JSON gösterimiyle bir POST isteği gönderdiğini varsayalım:</span><span class="sxs-lookup"><span data-stu-id="c1119-113">Suppose that a client sends a POST request with the following JSON representation:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample2.json)]

<span data-ttu-id="c1119-114">İstemcinin gerekli olarak işaretlenen `Name` özelliğini içermediğini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c1119-114">You can see that the client did not include the `Name` property, which is marked as required.</span></span> <span data-ttu-id="c1119-115">Web API 'si, JSON 'ı bir `Product` örneğine dönüştürdüğünde, doğrulama özniteliklerine karşı `Product` doğrular.</span><span class="sxs-lookup"><span data-stu-id="c1119-115">When Web API converts the JSON into a `Product` instance, it validates the `Product` against the validation attributes.</span></span> <span data-ttu-id="c1119-116">Denetleyici eyleinizde, modelin geçerli olup olmadığını kontrol edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c1119-116">In your controller action, you can check whether the model is valid:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="c1119-117">Model doğrulama, istemci verilerinin güvenli olduğunu garanti etmez.</span><span class="sxs-lookup"><span data-stu-id="c1119-117">Model validation does not guarantee that client data is safe.</span></span> <span data-ttu-id="c1119-118">Uygulamanın diğer katmanlarında ek doğrulama gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="c1119-118">Additional validation might be needed in other layers of the application.</span></span> <span data-ttu-id="c1119-119">(Örneğin, veri katmanı yabancı anahtar kısıtlamalarını uygulayabilir.) [Web API 'sini Entity Framework kullanma](../data/using-web-api-with-entity-framework/part-1.md) öğreticisinde bu sorunlardan bazıları incelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="c1119-119">(For example, the data layer might enforce foreign key constraints.) The tutorial [Using Web API with Entity Framework](../data/using-web-api-with-entity-framework/part-1.md) explores some of these issues.</span></span>

<span data-ttu-id="c1119-120">**"In-Posting"** : altında, istemci bazı özellikleri bıraktığında gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="c1119-120">**"Under-Posting"**: Under-posting happens when the client leaves out some properties.</span></span> <span data-ttu-id="c1119-121">Örneğin, istemcinin aşağıdakileri göndereceğini varsayalım:</span><span class="sxs-lookup"><span data-stu-id="c1119-121">For example, suppose the client sends the following:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample4.json)]

<span data-ttu-id="c1119-122">Burada istemci, `Price` veya `Weight`için değerler belirtmedi.</span><span class="sxs-lookup"><span data-stu-id="c1119-122">Here, the client did not specify values for `Price` or `Weight`.</span></span> <span data-ttu-id="c1119-123">JSON biçimlendiricisi eksik özelliklere sıfır varsayılan değeri atar.</span><span class="sxs-lookup"><span data-stu-id="c1119-123">The JSON formatter assigns a default value of zero to the missing properties.</span></span>

![](model-validation-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="c1119-124">Sıfır değeri bu özellikler için geçerli bir değer olduğundan model durumu geçerli.</span><span class="sxs-lookup"><span data-stu-id="c1119-124">The model state is valid, because zero is a valid value for these properties.</span></span> <span data-ttu-id="c1119-125">Bunun bir sorun olup olmadığı, senaryonuza bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="c1119-125">Whether this is a problem depends on your scenario.</span></span> <span data-ttu-id="c1119-126">Örneğin, bir güncelleştirme işleminde, "sıfır" ve "ayarlanmadı" arasında ayrım yapmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c1119-126">For example, in an update operation, you might want to distinguish between "zero" and "not set."</span></span> <span data-ttu-id="c1119-127">İstemcileri bir değer ayarlamaya zorlamak için özelliği null yapılabilir yapın ve **gerekli** özniteliği ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="c1119-127">To force clients to set a value, make the property nullable and set the **Required** attribute:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample5.cs?highlight=1-2)]

<span data-ttu-id="c1119-128">**"Aşırı gönderme"** : bir istemci, beklediğinizden *daha fazla* veri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="c1119-128">**"Over-Posting"**: A client can also send *more* data than you expected.</span></span> <span data-ttu-id="c1119-129">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c1119-129">For example:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample6.json)]

<span data-ttu-id="c1119-130">Burada JSON, `Product` modelinde mevcut olmayan bir Özellik ("Color") içerir.</span><span class="sxs-lookup"><span data-stu-id="c1119-130">Here, the JSON includes a property ("Color") that does not exist in the `Product` model.</span></span> <span data-ttu-id="c1119-131">Bu durumda, JSON biçimlendiricisi yalnızca bu değeri yoksayar.</span><span class="sxs-lookup"><span data-stu-id="c1119-131">In this case, the JSON formatter simply ignores this value.</span></span> <span data-ttu-id="c1119-132">(XML biçimlendiricisi aynı şekilde yapılır.) Daha fazla bilgi için, modelinizde salt okunurdur.</span><span class="sxs-lookup"><span data-stu-id="c1119-132">(The XML formatter does the same.) Over-posting causes problems if your model has properties that you intended to be read-only.</span></span> <span data-ttu-id="c1119-133">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c1119-133">For example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="c1119-134">Kullanıcıların `IsAdmin` özelliğini güncelleştirmesini ve kendilerini yöneticilere yükseltmenizi istemezsiniz!</span><span class="sxs-lookup"><span data-stu-id="c1119-134">You don't want users to update the `IsAdmin` property and elevate themselves to administrators!</span></span> <span data-ttu-id="c1119-135">En güvenli strateji, istemcinin gönderilmesine izin verilen şekilde tam olarak eşleşen bir model sınıfı kullanmaktır:</span><span class="sxs-lookup"><span data-stu-id="c1119-135">The safest strategy is to use a model class that exactly matches what the client is allowed to send:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="c1119-136">Atacan Solson 'un blog gönderisine "[giriş doğrulaması ve ASP.NET MVC 'de model doğrulama](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)",-Posting ve over-Posting konusunda iyi bir tartışmaya sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c1119-136">Brad Wilson's blog post "[Input Validation vs. Model Validation in ASP.NET MVC](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)" has a good discussion of under-posting and over-posting.</span></span> <span data-ttu-id="c1119-137">Post, ASP.NET MVC 2 ile ilgili olsa da, sorunlar hala Web API 'SI ile ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="c1119-137">Although the post is about ASP.NET MVC 2, the issues are still relevant to Web API.</span></span>

## <a name="handling-validation-errors"></a><span data-ttu-id="c1119-138">Doğrulama hatalarını işleme</span><span class="sxs-lookup"><span data-stu-id="c1119-138">Handling Validation Errors</span></span>

<span data-ttu-id="c1119-139">Doğrulama başarısız olduğunda Web API 'SI istemciye otomatik olarak bir hata döndürmez.</span><span class="sxs-lookup"><span data-stu-id="c1119-139">Web API does not automatically return an error to the client when validation fails.</span></span> <span data-ttu-id="c1119-140">Bu, model durumunu denetlemek ve uygun şekilde yanıt vermek için denetleyici eylemine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c1119-140">It is up to the controller action to check the model state and respond appropriately.</span></span>

<span data-ttu-id="c1119-141">Ayrıca, denetleyici eylemi çağrılmadan önce model durumunu denetlemek için bir eylem filtresi de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c1119-141">You can also create an action filter to check the model state before the controller action is invoked.</span></span> <span data-ttu-id="c1119-142">Aşağıdaki kodda bir örnek gösterilir:</span><span class="sxs-lookup"><span data-stu-id="c1119-142">The following code shows an example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="c1119-143">Model doğrulaması başarısız olursa, bu filtre doğrulama hatalarını içeren bir HTTP yanıtı döndürür.</span><span class="sxs-lookup"><span data-stu-id="c1119-143">If model validation fails, this filter returns an HTTP response that contains the validation errors.</span></span> <span data-ttu-id="c1119-144">Bu durumda, denetleyici eylemi çağrılmaz.</span><span class="sxs-lookup"><span data-stu-id="c1119-144">In that case, the controller action is not invoked.</span></span>

[!code-console[Main](model-validation-in-aspnet-web-api/samples/sample10.cmd)]

<span data-ttu-id="c1119-145">Bu filtreyi tüm Web API denetleyicilerine uygulamak için, yapılandırma sırasında **HttpConfiguration. Filters** koleksiyonuna filtrenin bir örneğini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c1119-145">To apply this filter to all Web API controllers, add an instance of the filter to the **HttpConfiguration.Filters** collection during configuration:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="c1119-146">Farklı bir seçenek, filtreyi ayrı denetleyicilerde veya denetleyici eylemlerinde bir öznitelik olarak ayarlamanıza olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="c1119-146">Another option is to set the filter as an attribute on individual controllers or controller actions:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample12.cs)]
