---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-4
title: Varlık Ilişkilerini işleme | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: d2f5710c-23c7-40a5-9cd9-5d0516570cba
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-4
msc.type: authoredcontent
ms.openlocfilehash: be4948e5443a5eb4e1824c63dd0c445a7ee1928e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557465"
---
# <a name="handling-entity-relations"></a><span data-ttu-id="85b9b-102">Varlık İlişkilerini İşleme</span><span class="sxs-lookup"><span data-stu-id="85b9b-102">Handling Entity Relations</span></span>

<span data-ttu-id="85b9b-103">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="85b9b-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="85b9b-104">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="85b9b-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="85b9b-105">Bu bölümde, EF 'in ilgili varlıkları nasıl yüklediği ve model sınıflarınızda dairesel gezinti özelliklerinin nasıl işleneceği hakkında bazı ayrıntılar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="85b9b-105">This section describes some details of how EF loads related entities, and how to handle circular navigation properties in your model classes.</span></span> <span data-ttu-id="85b9b-106">(Bu bölüm, arka plan bilgisi sağlar ve öğreticiyi tamamlaması için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="85b9b-106">(This section provides background knowledge, and is not required to complete the tutorial.</span></span> <span data-ttu-id="85b9b-107">İsterseniz [Bölüm 5](part-5.md)' e atlayın..)</span><span class="sxs-lookup"><span data-stu-id="85b9b-107">If you prefer, skip to [Part 5.](part-5.md).)</span></span>

## <a name="eager-loading-versus-lazy-loading"></a><span data-ttu-id="85b9b-108">Ekip yükleme ve geç yükleme karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="85b9b-108">Eager Loading versus Lazy Loading</span></span>

<span data-ttu-id="85b9b-109">Bir ilişkisel veritabanıyla EF kullanırken, EF 'in ilgili verileri nasıl yüklediğini anlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="85b9b-109">When using EF with a relational database, it's important to understand how EF loads related data.</span></span>

<span data-ttu-id="85b9b-110">Ayrıca, EF 'in oluşturduğu SQL sorgularını görmek de yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="85b9b-110">It's also useful to see the SQL queries that EF generates.</span></span> <span data-ttu-id="85b9b-111">SQL 'i izlemek için aşağıdaki kod satırını `BookServiceContext` oluşturucusuna ekleyin:</span><span class="sxs-lookup"><span data-stu-id="85b9b-111">To trace the SQL, add the following line of code to the `BookServiceContext` constructor:</span></span>

[!code-csharp[Main](part-4/samples/sample1.cs)]

<span data-ttu-id="85b9b-112">/Api/Books 'a bir GET isteği gönderirseniz, aşağıdaki gibi JSON döndürür:</span><span class="sxs-lookup"><span data-stu-id="85b9b-112">If you send a GET request to /api/books, it returns JSON like the following:</span></span>

[!code-console[Main](part-4/samples/sample2.cmd)]

<span data-ttu-id="85b9b-113">Kitap geçerli bir AuthorId içeriyor olsa da, Author özelliğinin null olduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85b9b-113">You can see that the Author property is null, even though the book contains a valid AuthorId.</span></span> <span data-ttu-id="85b9b-114">Bunun nedeni, EF 'in ilgili yazar varlıklarını yüklememalarıdır.</span><span class="sxs-lookup"><span data-stu-id="85b9b-114">That's because EF is not loading the related Author entities.</span></span> <span data-ttu-id="85b9b-115">SQL sorgusunun izleme günlüğü şunları doğrular:</span><span class="sxs-lookup"><span data-stu-id="85b9b-115">The trace log of the SQL query confirms this:</span></span>

[!code-console[Main](part-4/samples/sample3.sql)]

<span data-ttu-id="85b9b-116">SELECT deyimleri kitaplar tablosundan geçer ve yazar tablosuna başvurmuyor.</span><span class="sxs-lookup"><span data-stu-id="85b9b-116">The SELECT statement takes from the Books table, and does not reference the Author table.</span></span>

<span data-ttu-id="85b9b-117">Başvuru için, kitap listesini döndüren `BooksController` sınıfında yöntemi aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="85b9b-117">For reference, here is the method in the `BooksController` class that returns the list of books.</span></span>

[!code-csharp[Main](part-4/samples/sample4.cs)]

<span data-ttu-id="85b9b-118">Ayrıca, JSON verilerinin bir parçası olarak yazarın nasıl dönediğimiz hakkında bilgi vereceğiz.</span><span class="sxs-lookup"><span data-stu-id="85b9b-118">Let's see how we can return the Author as part of the JSON data.</span></span> <span data-ttu-id="85b9b-119">Entity Framework içinde ilgili verileri yüklemek için üç yol vardır: Eager yükleme, geç yükleme ve açık yükleme.</span><span class="sxs-lookup"><span data-stu-id="85b9b-119">There are three ways to load related data in Entity Framework: eager loading, lazy loading, and explicit loading.</span></span> <span data-ttu-id="85b9b-120">Her teknikle ilgili denge vardır. bu nedenle, nasıl çalıştığını anlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="85b9b-120">There are trade-offs with each technique, so it's important to understand how they work.</span></span>

### <a name="eager-loading"></a><span data-ttu-id="85b9b-121">Ekip yükleme</span><span class="sxs-lookup"><span data-stu-id="85b9b-121">Eager Loading</span></span>

<span data-ttu-id="85b9b-122">Bu *yüklemede*, EF ile ilgili varlıkları ilk veritabanı sorgusunun bir parçası olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="85b9b-122">With *eager loading*, EF loads related entities as part of the initial database query.</span></span> <span data-ttu-id="85b9b-123">Eager yükleme işlemini gerçekleştirmek için **System. Data. Entity. Include** genişletme yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="85b9b-123">To perform eager loading, use the **System.Data.Entity.Include** extension method.</span></span>

[!code-csharp[Main](part-4/samples/sample5.cs)]

<span data-ttu-id="85b9b-124">Bu, sorguya yazar verilerini ekleme hakkında söyleme söyler.</span><span class="sxs-lookup"><span data-stu-id="85b9b-124">This tells EF to include the Author data in the query.</span></span> <span data-ttu-id="85b9b-125">Bu değişikliği yapar ve uygulamayı çalıştırırsanız, şu anda JSON verileri şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="85b9b-125">If you make this change and run the app, now the JSON data looks like this:</span></span>

[!code-console[Main](part-4/samples/sample6.cmd)]

<span data-ttu-id="85b9b-126">İzleme günlüğünde, EF 'in kitap ve yazar tablolarında bir JOIN gerçekleştirdiği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="85b9b-126">The trace log shows that EF performed a join on the Book and Author tables.</span></span>

[!code-console[Main](part-4/samples/sample7.cmd)]

### <a name="lazy-loading"></a><span data-ttu-id="85b9b-127">Geç yükleme</span><span class="sxs-lookup"><span data-stu-id="85b9b-127">Lazy Loading</span></span>

<span data-ttu-id="85b9b-128">Yavaş yükleme ile ilgili varlık için gezinti özelliği başvurulduğunu EF, ilgili bir varlığı otomatik olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="85b9b-128">With lazy loading, EF automatically loads a related entity when the navigation property for that entity is dereferenced.</span></span> <span data-ttu-id="85b9b-129">Yavaş yüklemeyi etkinleştirmek için, gezinti özelliğini sanal yapın.</span><span class="sxs-lookup"><span data-stu-id="85b9b-129">To enable lazy loading, make the navigation property virtual.</span></span> <span data-ttu-id="85b9b-130">Örneğin, Book sınıfında:</span><span class="sxs-lookup"><span data-stu-id="85b9b-130">For example, in the Book class:</span></span>

[!code-csharp[Main](part-4/samples/sample8.cs?highlight=6)]

<span data-ttu-id="85b9b-131">Şimdi aşağıdaki kodu göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="85b9b-131">Now consider the following code:</span></span>

[!code-csharp[Main](part-4/samples/sample9.cs)]

<span data-ttu-id="85b9b-132">Yavaş yükleme etkinleştirildiğinde, `books[0]` `Author` özelliğine erişmek, yazma için veritabanını sorgulamak için EF 'e neden olur.</span><span class="sxs-lookup"><span data-stu-id="85b9b-132">When lazy loading is enabled, accessing the `Author` property on `books[0]` causes EF to query the database for the author.</span></span>

<span data-ttu-id="85b9b-133">EF, her ilgili varlığı aldığında bir sorgu gönderdiğinden, yavaş yükleme birden çok veritabanı gezilerini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="85b9b-133">Lazy loading requires multiple database trips, because EF sends a query each time it retrieves a related entity.</span></span> <span data-ttu-id="85b9b-134">Genellikle, seri hale getirmek istediğiniz nesneler için yavaş yüklemeyi devre dışı istersiniz.</span><span class="sxs-lookup"><span data-stu-id="85b9b-134">Generally, you want lazy loading disabled for objects that you serialize.</span></span> <span data-ttu-id="85b9b-135">Seri hale getirici modeldeki tüm özellikleri okumalı ve bu da ilgili varlıkları yüklemeyi tetikler.</span><span class="sxs-lookup"><span data-stu-id="85b9b-135">The serializer has to read all of the properties on the model, which triggers loading the related entities.</span></span> <span data-ttu-id="85b9b-136">Örneğin, yavaş yükleme özelliği etkin olan kitaplar listesini seri hale geldiğinde SQL sorguları burada açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="85b9b-136">For example, here are the SQL queries when EF serializes the list of books with lazy loading enabled.</span></span> <span data-ttu-id="85b9b-137">EF 'in üç yazar için üç ayrı sorgu yaptığı hakkında bilgi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85b9b-137">You can see that EF makes three separate queries for the three authors.</span></span>

[!code-console[Main](part-4/samples/sample10.sql)]

<span data-ttu-id="85b9b-138">Yavaş yükleme kullanmak isteyebileceğiniz zamanlar hala vardır.</span><span class="sxs-lookup"><span data-stu-id="85b9b-138">There are still times when you might want to use lazy loading.</span></span> <span data-ttu-id="85b9b-139">Eager yüklemesi, EF 'in çok karmaşık bir birleşme oluşturmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="85b9b-139">Eager loading can cause EF to generate a very complex join.</span></span> <span data-ttu-id="85b9b-140">Ya da verilerin küçük bir alt kümesi için ilgili varlıklara ihtiyacınız olabilir ve yavaş yükleme daha verimli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="85b9b-140">Or you might need related entities for a small subset of the data, and lazy loading would be more efficient.</span></span>

<span data-ttu-id="85b9b-141">Serileştirme sorunlarından kaçınmak için bir yol, varlık nesneleri yerine veri aktarımı nesneleri (DTOs) serileştirilmenin bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="85b9b-141">One way to avoid serialization problems is to serialize data transfer objects (DTOs) instead of entity objects.</span></span> <span data-ttu-id="85b9b-142">Bu yaklaşımı makalenin ilerleyen kısımlarında göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="85b9b-142">I'll show this approach later in the article.</span></span>

### <a name="explicit-loading"></a><span data-ttu-id="85b9b-143">Açık yükleme</span><span class="sxs-lookup"><span data-stu-id="85b9b-143">Explicit Loading</span></span>

<span data-ttu-id="85b9b-144">Açık yükleme, kod içinde ilgili verileri açıkça almanız dışında, yavaş yüklemeye benzer. bir gezinti özelliğine eriştiğinizde otomatik olarak gerçekleşmez.</span><span class="sxs-lookup"><span data-stu-id="85b9b-144">Explicit loading is similar to lazy loading, except that you explicitly get the related data in code; it doesn't happen automatically when you access a navigation property.</span></span> <span data-ttu-id="85b9b-145">Açık yükleme, ilgili verilerin ne zaman yükleneceği konusunda daha fazla denetim sağlar, ancak ek kod gerektirir.</span><span class="sxs-lookup"><span data-stu-id="85b9b-145">Explicit loading gives you more control over when to load related data, but requires extra code.</span></span> <span data-ttu-id="85b9b-146">Açık yükleme hakkında daha fazla bilgi için bkz. [Ilgili varlıkları yükleme](https://msdn.microsoft.com/data/jj574232#explicit).</span><span class="sxs-lookup"><span data-stu-id="85b9b-146">For more information about explicit loading, see [Loading Related Entities](https://msdn.microsoft.com/data/jj574232#explicit).</span></span>

## <a name="navigation-properties-and-circular-references"></a><span data-ttu-id="85b9b-147">Gezinti özellikleri ve döngüsel başvurular</span><span class="sxs-lookup"><span data-stu-id="85b9b-147">Navigation Properties and Circular References</span></span>

<span data-ttu-id="85b9b-148">Kitap ve yazar modellerini tanımladığımda, kitap yazarı ilişkisinin `Book` sınıfında bir gezinti özelliği tanımlıyorum, ancak başka bir yönde bir gezinti özelliği tanımlıyorum.</span><span class="sxs-lookup"><span data-stu-id="85b9b-148">When I defined the Book and Author models, I defined a navigation property on the `Book` class for the Book-Author relationship, but I did not define a navigation property in the other direction.</span></span>

<span data-ttu-id="85b9b-149">Karşılık gelen gezinti özelliğini `Author` sınıfa eklerseniz ne olur?</span><span class="sxs-lookup"><span data-stu-id="85b9b-149">What happens if you add the corresponding navigation property to the `Author` class?</span></span>

[!code-csharp[Main](part-4/samples/sample11.cs?highlight=7)]

<span data-ttu-id="85b9b-150">Ne yazık ki, modelleri seri hale alırken bir sorun oluşturur.</span><span class="sxs-lookup"><span data-stu-id="85b9b-150">Unfortunately, this creates a problem when you serialize the models.</span></span> <span data-ttu-id="85b9b-151">İlgili verileri yüklerseniz, döngüsel bir nesne grafiği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="85b9b-151">If you load the related data, it creates a circular object graph.</span></span>

![](part-4/_static/image1.png)

<span data-ttu-id="85b9b-152">JSON veya XML biçimlendiricisi grafiği serileştirmek denediğinde, bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="85b9b-152">When the JSON or XML formatter tries to serialize the graph, it will throw an exception.</span></span> <span data-ttu-id="85b9b-153">İki biçimlendirme farklı özel durum iletileri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="85b9b-153">The two formatters throw different exception messages.</span></span> <span data-ttu-id="85b9b-154">JSON biçimlendiricisi için bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="85b9b-154">Here is an example for the JSON formatter:</span></span>

[!code-console[Main](part-4/samples/sample12.cmd)]

<span data-ttu-id="85b9b-155">XML biçimlendiricisi aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="85b9b-155">Here is the XML formatter:</span></span>

[!code-xml[Main](part-4/samples/sample13.xml)]

<span data-ttu-id="85b9b-156">Bir çözüm, sonraki bölümde tanımlandığım DTOs 'ı kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="85b9b-156">One solution is to use DTOs, which I describe in the next section.</span></span> <span data-ttu-id="85b9b-157">Alternatif olarak, JSON ve XML formatlarını grafik döngülerini işleyecek şekilde yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85b9b-157">Alternatively, you can configure the JSON and XML formatters to handle graph cycles.</span></span> <span data-ttu-id="85b9b-158">Daha fazla bilgi için bkz. [Döngüsel nesne başvurularını işleme](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).</span><span class="sxs-lookup"><span data-stu-id="85b9b-158">For more information, see [Handling Circular Object References](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).</span></span>

<span data-ttu-id="85b9b-159">Bu öğreticide, `Author.Book` gezinti özelliğine ihtiyacınız yoktur, bu nedenle bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85b9b-159">For this tutorial, you don't need the `Author.Book` navigation property, so you can leave it out.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="85b9b-160">[Önceki](part-3.md)
> [İleri](part-5.md)</span><span class="sxs-lookup"><span data-stu-id="85b9b-160">[Previous](part-3.md)
[Next](part-5.md)</span></span>
