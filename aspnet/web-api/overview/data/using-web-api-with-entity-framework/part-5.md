---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-5
title: Veri Aktarımı nesneleri oluşturma (DTOs) | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0fd07176-b74b-48f0-9fac-0f02e3ffa213
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-5
msc.type: authoredcontent
ms.openlocfilehash: fc0463420207eba764014b8ec7123c5150e38247
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445754"
---
# <a name="create-data-transfer-objects-dtos"></a><span data-ttu-id="b6049-102">Veri Aktarımı Nesneleri (DTO) Oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6049-102">Create Data Transfer Objects (DTOs)</span></span>

<span data-ttu-id="b6049-103">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b6049-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="b6049-104">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="b6049-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="b6049-105">Şu anda Web API 'imiz, veritabanı varlıklarını istemciye kullanıma sunuyor.</span><span class="sxs-lookup"><span data-stu-id="b6049-105">Right now, our web API exposes the database entities to the client.</span></span> <span data-ttu-id="b6049-106">İstemci doğrudan veritabanı tablolarınıza eşleyen verileri alır.</span><span class="sxs-lookup"><span data-stu-id="b6049-106">The client receives data that maps directly to your database tables.</span></span> <span data-ttu-id="b6049-107">Bununla birlikte, her zaman iyi bir fikir değildir.</span><span class="sxs-lookup"><span data-stu-id="b6049-107">However, that's not always a good idea.</span></span> <span data-ttu-id="b6049-108">Bazen istemciye göndereceğiniz verilerin şeklini değiştirmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6049-108">Sometimes you want to change the shape of the data that you send to client.</span></span> <span data-ttu-id="b6049-109">Örneğin, şunları yapmak isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b6049-109">For example, you might want to:</span></span>

- <span data-ttu-id="b6049-110">Döngüsel başvuruları Kaldır (önceki bölüme bakın).</span><span class="sxs-lookup"><span data-stu-id="b6049-110">Remove circular references (see previous section).</span></span>
- <span data-ttu-id="b6049-111">İstemcilerin görüntülemesi beklenen belirli özellikleri gizleyin.</span><span class="sxs-lookup"><span data-stu-id="b6049-111">Hide particular properties that clients are not supposed to view.</span></span>
- <span data-ttu-id="b6049-112">Yük boyutunu azaltmak için bazı özellikleri atlayın.</span><span class="sxs-lookup"><span data-stu-id="b6049-112">Omit some properties in order to reduce payload size.</span></span>
- <span data-ttu-id="b6049-113">İstemcilere daha uygun hale getirmek için iç içe geçmiş nesneler içeren nesne grafiklerini düzleştirin.</span><span class="sxs-lookup"><span data-stu-id="b6049-113">Flatten object graphs that contain nested objects, to make them more convenient for clients.</span></span>
- <span data-ttu-id="b6049-114">"Aşırı gönderme" güvenlik açıklarını önleyin.</span><span class="sxs-lookup"><span data-stu-id="b6049-114">Avoid "over-posting" vulnerabilities.</span></span> <span data-ttu-id="b6049-115">(Bkz. Yük nakli hakkında bir tartışma için [model doğrulama](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) .)</span><span class="sxs-lookup"><span data-stu-id="b6049-115">(See [Model Validation](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) for a discussion of over-posting.)</span></span>
- <span data-ttu-id="b6049-116">Hizmet katmanınızı veritabanı katmanınızdan ayırın.</span><span class="sxs-lookup"><span data-stu-id="b6049-116">Decouple your service layer from your database layer.</span></span>

<span data-ttu-id="b6049-117">Bunu gerçekleştirmek için bir *veri aktarımı nesnesi* (DTO) tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6049-117">To accomplish this, you can define a *data transfer object* (DTO).</span></span> <span data-ttu-id="b6049-118">Bir DTO, verilerin ağ üzerinden nasıl gönderileceğini tanımlayan bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="b6049-118">A DTO is an object that defines how the data will be sent over the network.</span></span> <span data-ttu-id="b6049-119">Bunun, kitap varlığıyla nasıl çalıştığını görelim.</span><span class="sxs-lookup"><span data-stu-id="b6049-119">Let's see how that works with the Book entity.</span></span> <span data-ttu-id="b6049-120">Modeller klasöründe, iki DTO sınıfı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b6049-120">In the Models folder, add two DTO classes:</span></span>

[!code-csharp[Main](part-5/samples/sample1.cs)]

<span data-ttu-id="b6049-121">`BookDetailDto` sınıfı, kitabın yazar adını tutan bir dize olması `AuthorName` dışında, kitap modelindeki tüm özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b6049-121">The `BookDetailDto` class includes all of the properties from the Book model, except that `AuthorName` is a string that will hold the author name.</span></span> <span data-ttu-id="b6049-122">`BookDto` sınıfı `BookDetailDto`bir özellikler alt kümesini içerir.</span><span class="sxs-lookup"><span data-stu-id="b6049-122">The `BookDto` class contains a subset of properties from `BookDetailDto`.</span></span>

<span data-ttu-id="b6049-123">Sonra, `BooksController` sınıfındaki iki GET yöntemini DTOs döndüren sürümlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b6049-123">Next, replace the two GET methods in the `BooksController` class, with versions that return DTOs.</span></span> <span data-ttu-id="b6049-124">Kitap varlıklarından DTOs 'a dönüştürmek için LINQ **Select** ifadesini kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="b6049-124">We'll use the LINQ **Select** statement to convert from Book entities into DTOs.</span></span>

[!code-csharp[Main](part-5/samples/sample2.cs)]

<span data-ttu-id="b6049-125">Yeni `GetBooks` yöntemi tarafından oluşturulan SQL aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b6049-125">Here is the SQL generated by the new `GetBooks` method.</span></span> <span data-ttu-id="b6049-126">EF 'in LINQ **seçimini** BIR SQL SELECT ifadesine dönüştürdüğünde emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6049-126">You can see that EF translates the LINQ **Select** into a SQL SELECT statement.</span></span>

[!code-sql[Main](part-5/samples/sample3.sql)]

<span data-ttu-id="b6049-127">Son olarak, `PostBook` yöntemini bir DTO döndürecek şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b6049-127">Finally, modify the `PostBook` method to return a DTO.</span></span>

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="b6049-128">Bu öğreticide, kodda el ile DTOs 'a dönüştürüyoruz.</span><span class="sxs-lookup"><span data-stu-id="b6049-128">In this tutorial, we're converting to DTOs manually in code.</span></span> <span data-ttu-id="b6049-129">Diğer bir seçenek de, dönüştürmeyi otomatik olarak işleyen [Automaber](http://automapper.org/) gibi bir kitaplık kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="b6049-129">Another option is to use a library like [AutoMapper](http://automapper.org/) that handles the conversion automatically.</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="b6049-130">[Önceki](part-4.md)
> [İleri](part-6.md)</span><span class="sxs-lookup"><span data-stu-id="b6049-130">[Previous](part-4.md)
[Next](part-6.md)</span></span>
