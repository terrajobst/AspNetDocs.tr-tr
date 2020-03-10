---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
title: '2\. Bölüm: etki alanı modellerini oluşturma | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: fe3ef85f-bdc6-4e10-9768-25aa565c01d0
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
msc.type: authoredcontent
ms.openlocfilehash: 7c5ed1bdb4b390c94907b14e208231f16ad42d96
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78621823"
---
# <a name="part-2-creating-the-domain-models"></a><span data-ttu-id="a1698-102">2\. Bölüm: etki alanı modellerini oluşturma</span><span class="sxs-lookup"><span data-stu-id="a1698-102">Part 2: Creating the Domain Models</span></span>

<span data-ttu-id="a1698-103">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a1698-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="a1698-104">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="a1698-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-models"></a><span data-ttu-id="a1698-105">Model Ekle</span><span class="sxs-lookup"><span data-stu-id="a1698-105">Add Models</span></span>

<span data-ttu-id="a1698-106">Entity Framework yaklaşımın üç yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="a1698-106">There are three ways to approach Entity Framework:</span></span>

- <span data-ttu-id="a1698-107">Veritabanı-ilk: bir veritabanı ile başlar ve Entity Framework kodu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1698-107">Database-first: You start with a database, and Entity Framework generates the code.</span></span>
- <span data-ttu-id="a1698-108">Model-önce: bir görsel modelle başlar ve Entity Framework hem veritabanını hem de kodu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1698-108">Model-first: You start with a visual model, and Entity Framework generates both the database and code.</span></span>
- <span data-ttu-id="a1698-109">Kod-önce: kodla başlar ve veritabanını Entity Framework oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1698-109">Code-first: You start with code, and Entity Framework generates the database.</span></span>

<span data-ttu-id="a1698-110">İlk kod yaklaşımı kullanıyoruz, bu nedenle etki alanı nesnelerimizi POCOs (düz-eski CLR nesneleri) olarak tanımlayarak başladık.</span><span class="sxs-lookup"><span data-stu-id="a1698-110">We are using the code-first approach, so we start by defining our domain objects as POCOs (plain-old CLR objects).</span></span> <span data-ttu-id="a1698-111">Kod-ilk yaklaşımla, etki alanı nesneleri, işlemler veya kalıcılık gibi veritabanı katmanını desteklemek için ek kod gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="a1698-111">With the code-first approach, domain objects don't need any extra code to support the database layer, such as transactions or persistence.</span></span> <span data-ttu-id="a1698-112">(Özellikle, [EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx) sınıfından devralması gerekmez.) Entity Framework veritabanı şemasını nasıl oluşturduğunu denetlemek için veri açıklamalarını kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1698-112">(Specifically, they do not need to inherit from the [EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx) class.) You can still use data annotations to control how Entity Framework creates the database schema.</span></span>

<span data-ttu-id="a1698-113">POCOs, [veritabanı durumunu](https://msdn.microsoft.com/library/system.data.entitystate.aspx)tanımlayan ek özellikler taşımadığından, kolayca JSON veya XML olarak serileştirilir.</span><span class="sxs-lookup"><span data-stu-id="a1698-113">Because POCOs do not carry any extra properties that describe [database state](https://msdn.microsoft.com/library/system.data.entitystate.aspx), they can easily be serialized to JSON or XML.</span></span> <span data-ttu-id="a1698-114">Bununla birlikte, öğreticide daha sonra göreceğiniz gibi Entity Framework modellerinizi her zaman doğrudan istemcilere sunmalısınız.</span><span class="sxs-lookup"><span data-stu-id="a1698-114">However, that does not mean you should always expose your Entity Framework models directly to clients, as we'll see later in the tutorial.</span></span>

<span data-ttu-id="a1698-115">Aşağıdaki POCOs 'ları oluşturacağız:</span><span class="sxs-lookup"><span data-stu-id="a1698-115">We will create the following POCOs:</span></span>

- <span data-ttu-id="a1698-116">Ürün</span><span class="sxs-lookup"><span data-stu-id="a1698-116">Product</span></span>
- <span data-ttu-id="a1698-117">Sipariş verme</span><span class="sxs-lookup"><span data-stu-id="a1698-117">Order</span></span>
- <span data-ttu-id="a1698-118">OrderDetail</span><span class="sxs-lookup"><span data-stu-id="a1698-118">OrderDetail</span></span>

<span data-ttu-id="a1698-119">Her bir sınıfı oluşturmak için Çözüm Gezgini modeller klasörüne sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a1698-119">To create each class, right-click the Models folder in Solution Explorer.</span></span> <span data-ttu-id="a1698-120">Bağlam menüsünden **Ekle** ' yi ve ardından sınıf ' ı seçin **.**</span><span class="sxs-lookup"><span data-stu-id="a1698-120">From the context menu, select **Add** and then select **Class.**</span></span>

![](using-web-api-with-entity-framework-part-2/_static/image1.png)

<span data-ttu-id="a1698-121">Aşağıdaki uygulamayla bir `Product` sınıfı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a1698-121">Add a `Product` class with the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample1.cs)]

<span data-ttu-id="a1698-122">Kural gereği, Entity Framework `Id` özelliğini birincil anahtar olarak kullanır ve veritabanını veritabanı tablosundaki bir kimlik sütunuyla eşler.</span><span class="sxs-lookup"><span data-stu-id="a1698-122">By convention, Entity Framework uses the `Id` property as the primary key and maps it to an identity column in the database table.</span></span> <span data-ttu-id="a1698-123">Yeni bir `Product` örneği oluşturduğunuzda, veritabanı değeri oluşturduğundan `Id`için bir değer ayarlayamazsınız.</span><span class="sxs-lookup"><span data-stu-id="a1698-123">When you create a new `Product` instance, you won't set a value for `Id`, because the database generates the value.</span></span>

<span data-ttu-id="a1698-124">**ScaffoldColumn** özniteliği, ASP.NET MVC 'nin bir düzenleyici formu oluştururken `Id` özelliğini atlamasını söyler.</span><span class="sxs-lookup"><span data-stu-id="a1698-124">The **ScaffoldColumn** attribute tells ASP.NET MVC to skip the `Id` property when generating an editor form.</span></span> <span data-ttu-id="a1698-125">**Gerekli** öznitelik, modeli doğrulamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a1698-125">The **Required** attribute is used to validate the model.</span></span> <span data-ttu-id="a1698-126">`Name` özelliğinin boş olmayan bir dize olması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="a1698-126">It specifies that the `Name` property must be a non-empty string.</span></span>

<span data-ttu-id="a1698-127">`Order` sınıfını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a1698-127">Add the `Order` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample2.cs)]

<span data-ttu-id="a1698-128">`OrderDetail` sınıfını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a1698-128">Add the `OrderDetail` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample3.cs)]

## <a name="foreign-key-relations"></a><span data-ttu-id="a1698-129">Yabancı anahtar Ilişkileri</span><span class="sxs-lookup"><span data-stu-id="a1698-129">Foreign Key Relations</span></span>

<span data-ttu-id="a1698-130">Bir sipariş birçok sipariş ayrıntısı içerir ve her sipariş ayrıntısı tek bir ürüne başvurur.</span><span class="sxs-lookup"><span data-stu-id="a1698-130">An order contains many order details, and each order detail refers to a single product.</span></span> <span data-ttu-id="a1698-131">Bu ilişkileri göstermek için `OrderDetail` sınıfı `OrderId` ve `ProductId`adlı özellikleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a1698-131">To represent these relations, the `OrderDetail` class defines properties named `OrderId` and `ProductId`.</span></span> <span data-ttu-id="a1698-132">Entity Framework, bu özelliklerin yabancı anahtarları temsil ettiğini ve veritabanına yabancı anahtar kısıtlamaları eklemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="a1698-132">Entity Framework will infer that these properties represent foreign keys, and will add foreign-key constraints to the database.</span></span>

![](using-web-api-with-entity-framework-part-2/_static/image2.png)

<span data-ttu-id="a1698-133">`Order` ve `OrderDetail` sınıfları, ilişkili nesnelere başvurular içeren "gezinti" özelliklerini de içerir.</span><span class="sxs-lookup"><span data-stu-id="a1698-133">The `Order` and `OrderDetail` classes also include "navigation" properties, which contain references to the related objects.</span></span> <span data-ttu-id="a1698-134">Sipariş verildiğinde, gezinti özelliklerini izleyerek sırayla ürünlere gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1698-134">Given an order, you can navigate to the products in the order by following the navigation properties.</span></span>

<span data-ttu-id="a1698-135">Projeyi şimdi derle.</span><span class="sxs-lookup"><span data-stu-id="a1698-135">Compile the project now.</span></span> <span data-ttu-id="a1698-136">Entity Framework, modellerin özelliklerini saptamak için yansıma kullanır, bu nedenle veritabanı şemasını oluşturmak için derlenmiş bir bütünleştirilmiş kod gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a1698-136">Entity Framework uses reflection to discover the properties of the models, so it requires a compiled assembly to create the database schema.</span></span>

## <a name="configure-the-media-type-formatters"></a><span data-ttu-id="a1698-137">Medya türü Formatlayıcıları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a1698-137">Configure the Media-Type Formatters</span></span>

<span data-ttu-id="a1698-138">[Medya türü biçimlendirici](../../formats-and-model-binding/media-formatters.md) , Web API 'si http yanıt gövdesini yazdığında verilerinizi seri hale getirilen bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="a1698-138">A [media-type formatter](../../formats-and-model-binding/media-formatters.md) is an object that serializes your data when Web API writes the HTTP response body.</span></span> <span data-ttu-id="a1698-139">Yerleşik Biçimlendiriciler JSON ve XML çıkışını destekler.</span><span class="sxs-lookup"><span data-stu-id="a1698-139">The built-in formatters support JSON and XML output.</span></span> <span data-ttu-id="a1698-140">Varsayılan olarak, bu formatlayıcılara her ikisi de değere göre tüm nesneleri serileştirilir.</span><span class="sxs-lookup"><span data-stu-id="a1698-140">By default, both of these formatters serialize all objects by value.</span></span>

<span data-ttu-id="a1698-141">Değere göre serileştirme, bir nesne grafiğinde döngüsel başvurular varsa bir sorun oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1698-141">Serialization by value creates a problem if an object graph contains circular references.</span></span> <span data-ttu-id="a1698-142">Bu, `Order` ve `OrderDetail` sınıflarıyla tam olarak yapılır çünkü her biri birbirlerine bir başvuru içerir.</span><span class="sxs-lookup"><span data-stu-id="a1698-142">That's exactly the case with the `Order` and `OrderDetail` classes, because each holds a reference to the other.</span></span> <span data-ttu-id="a1698-143">Biçimlendirici başvuruları izler, her bir nesneyi değere göre yazıyor ve daireler içinde yer alır.</span><span class="sxs-lookup"><span data-stu-id="a1698-143">The formatter will follow the references, writing each object by value, and go in circles.</span></span> <span data-ttu-id="a1698-144">Bu nedenle, varsayılan davranışı değiştirmemiz gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="a1698-144">Therefore, we need to change the default behavior.</span></span>

<span data-ttu-id="a1698-145">Çözüm Gezgini ' de, uygulama\_Başlat klasörünü genişletin ve WebApiConfig.cs adlı dosyayı açın.</span><span class="sxs-lookup"><span data-stu-id="a1698-145">In Solution Explorer, expand the App\_Start folder and open the file named WebApiConfig.cs.</span></span> <span data-ttu-id="a1698-146">`WebApiConfig` sınıfına aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a1698-146">Add the following code to the `WebApiConfig` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample4.cs?highlight=11)]

<span data-ttu-id="a1698-147">Bu kod, nesne başvurularını korumak için JSON biçimlendirici olarak ayarlar ve XML biçimlendirici 'yi işlem hattından tamamen kaldırır.</span><span class="sxs-lookup"><span data-stu-id="a1698-147">This code sets the JSON formatter to preserve object references, and removes the XML formatter from the pipeline entirely.</span></span> <span data-ttu-id="a1698-148">(XML biçimlendirici nesne başvurularını korumak için yapılandırabilirsiniz, ancak bu çok daha fazla çalışmalardır ve bu uygulama için yalnızca JSON gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a1698-148">(You can configure the XML formatter to preserve object references, but it's a little more work, and we only need JSON for this application.</span></span> <span data-ttu-id="a1698-149">Daha fazla bilgi için bkz. [Döngüsel nesne başvurularını işleme](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).)</span><span class="sxs-lookup"><span data-stu-id="a1698-149">For more information, see [Handling Circular Object References](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a1698-150">[Önceki](using-web-api-with-entity-framework-part-1.md)
> [İleri](using-web-api-with-entity-framework-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="a1698-150">[Previous](using-web-api-with-entity-framework-part-1.md)
[Next](using-web-api-with-entity-framework-part-3.md)</span></span>
