---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-2
title: Modeller ve denetleyiciler ekleme | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 88908ff8-51a9-40eb-931c-a8139128b680
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-2
msc.type: authoredcontent
ms.openlocfilehash: 57dacda421968f341284d89c9a3ad80040c16e25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557542"
---
# <a name="add-models-and-controllers"></a><span data-ttu-id="9a05e-102">Model ve Denetleyici Ekleme</span><span class="sxs-lookup"><span data-stu-id="9a05e-102">Add Models and Controllers</span></span>

<span data-ttu-id="9a05e-103">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="9a05e-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="9a05e-104">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="9a05e-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="9a05e-105">Bu bölümde, veritabanı varlıklarını tanımlayan model sınıfları ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="9a05e-105">In this section, you will add model classes that define the database entities.</span></span> <span data-ttu-id="9a05e-106">Daha sonra, bu varlıklarda CRUD işlemlerini gerçekleştiren Web API denetleyicileri ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="9a05e-106">Then you will add Web API controllers that perform CRUD operations on those entities.</span></span>

## <a name="add-model-classes"></a><span data-ttu-id="9a05e-107">Model sınıfları Ekle</span><span class="sxs-lookup"><span data-stu-id="9a05e-107">Add Model Classes</span></span>

<span data-ttu-id="9a05e-108">Bu öğreticide, Entity Framework (EF) için "Code First" yaklaşımını kullanarak veritabanını oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="9a05e-108">In this tutorial, we'll create the database by using the "Code First" approach to Entity Framework (EF).</span></span> <span data-ttu-id="9a05e-109">Code First, veritabanı tablolarına karşılık C# gelen SıNıFLARı yazdığınızda EF veritabanını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9a05e-109">With Code First, you write C# classes that correspond to database tables, and EF creates the database.</span></span> <span data-ttu-id="9a05e-110">(Daha fazla bilgi için bkz. [Entity Framework geliştirme yaklaşımları](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf).)</span><span class="sxs-lookup"><span data-stu-id="9a05e-110">(For more information, see [Entity Framework Development Approaches](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf).)</span></span>

<span data-ttu-id="9a05e-111">Etki alanı nesnelerimizi POCOs (düz eski CLR nesneleri) olarak tanımlayarak başladık.</span><span class="sxs-lookup"><span data-stu-id="9a05e-111">We start by defining our domain objects as POCOs (plain-old CLR objects).</span></span> <span data-ttu-id="9a05e-112">Aşağıdaki POCOs 'ları oluşturacağız:</span><span class="sxs-lookup"><span data-stu-id="9a05e-112">We will create the following POCOs:</span></span>

- <span data-ttu-id="9a05e-113">Yazar</span><span class="sxs-lookup"><span data-stu-id="9a05e-113">Author</span></span>
- <span data-ttu-id="9a05e-114">Book</span><span class="sxs-lookup"><span data-stu-id="9a05e-114">Book</span></span>

<span data-ttu-id="9a05e-115">Çözüm Gezgini, modeller klasörüne sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9a05e-115">In Solution Explorer, right click the Models folder.</span></span> <span data-ttu-id="9a05e-116">**Ekle**' yi ve ardından **sınıf**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="9a05e-116">Select **Add**, then select **Class**.</span></span> <span data-ttu-id="9a05e-117">`Author`sınıfı adlandırın.</span><span class="sxs-lookup"><span data-stu-id="9a05e-117">Name the class `Author`.</span></span>

![](part-2/_static/image1.png)

<span data-ttu-id="9a05e-118">Author.cs içindeki tüm ortak kodu aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9a05e-118">Replace all of the boilerplate code in Author.cs with the following code.</span></span>

[!code-csharp[Main](part-2/samples/sample1.cs)]

<span data-ttu-id="9a05e-119">Aşağıdaki kodla `Book`adlı başka bir sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9a05e-119">Add another class named `Book`, with the following code.</span></span>

[!code-csharp[Main](part-2/samples/sample2.cs)]

<span data-ttu-id="9a05e-120">Entity Framework, veritabanı tabloları oluşturmak için bu modelleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="9a05e-120">Entity Framework will use these models to create database tables.</span></span> <span data-ttu-id="9a05e-121">Her model için `Id` özelliği, veritabanı tablosunun birincil anahtar sütunu olur.</span><span class="sxs-lookup"><span data-stu-id="9a05e-121">For each model, the `Id` property will become the primary key column of the database table.</span></span>

<span data-ttu-id="9a05e-122">Kitap sınıfında `AuthorId`, `Author` tabloya bir yabancı anahtar tanımlar.</span><span class="sxs-lookup"><span data-stu-id="9a05e-122">In the Book class, the `AuthorId` defines a foreign key into the `Author` table.</span></span> <span data-ttu-id="9a05e-123">(Basitlik için, her kitabın tek bir yazarı olduğunu kabul ediyorum.) Kitap sınıfı ayrıca ilgili `Author`bir gezinti özelliği içerir.</span><span class="sxs-lookup"><span data-stu-id="9a05e-123">(For simplicity, I'm assuming that each book has a single author.) The book class also contains a navigation property to the related `Author`.</span></span> <span data-ttu-id="9a05e-124">Koddaki ilgili `Author` erişmek için gezinti özelliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a05e-124">You can use the navigation property to access the related `Author` in code.</span></span> <span data-ttu-id="9a05e-125">Bölüm 4 ' te gezinti özellikleri hakkında daha fazla bilgi alıyorum ve [varlık Ilişkilerini işliyor](part-4.md).</span><span class="sxs-lookup"><span data-stu-id="9a05e-125">I say more about navigation properties in part 4, [Handling Entity Relations](part-4.md).</span></span>

## <a name="add-web-api-controllers"></a><span data-ttu-id="9a05e-126">Web API denetleyicileri ekleme</span><span class="sxs-lookup"><span data-stu-id="9a05e-126">Add Web API Controllers</span></span>

<span data-ttu-id="9a05e-127">Bu bölümde, CRUD işlemlerini (oluşturma, okuma, güncelleştirme ve silme) destekleyen Web API denetleyicileri ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="9a05e-127">In this section, we'll add Web API controllers that support CRUD operations (create, read, update, and delete).</span></span> <span data-ttu-id="9a05e-128">Denetleyiciler veritabanı katmanıyla iletişim kurmak için Entity Framework kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="9a05e-128">The controllers will use Entity Framework to communicate with the database layer.</span></span>

<span data-ttu-id="9a05e-129">Önce dosya denetleyicilerini/ValuesController. cs dosyasını silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a05e-129">First, you can delete the file Controllers/ValuesController.cs.</span></span> <span data-ttu-id="9a05e-130">Bu dosya, örnek bir Web API denetleyicisi içerir, ancak bu öğretici için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="9a05e-130">This file contains an example Web API controller, but you don't need it for this tutorial.</span></span>

![](part-2/_static/image2.png)

<span data-ttu-id="9a05e-131">Sonra, projeyi derleyin.</span><span class="sxs-lookup"><span data-stu-id="9a05e-131">Next, build the project.</span></span> <span data-ttu-id="9a05e-132">Web API 'SI yapı iskelesi, model sınıflarını bulmak için yansıma kullanır, bu nedenle derlenen derlemeye ihtiyaç duyuyor.</span><span class="sxs-lookup"><span data-stu-id="9a05e-132">The Web API scaffolding uses reflection to find the model classes, so it needs the compiled assembly.</span></span>

<span data-ttu-id="9a05e-133">Çözüm Gezgini, denetleyiciler klasörüne sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9a05e-133">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="9a05e-134">**Ekle**' yi ve ardından **Denetleyici**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="9a05e-134">Select **Add**, then select **Controller**.</span></span>

![](part-2/_static/image3.png)

<span data-ttu-id="9a05e-135">**Yapı Iskelesi Ekle** iletişim kutusunda, "Entity Framework kullanarak eylemler Ile Web API 2 denetleyicisi" ni seçin.</span><span class="sxs-lookup"><span data-stu-id="9a05e-135">In the **Add Scaffold** dialog, select "Web API 2 Controller with actions, using Entity Framework".</span></span> <span data-ttu-id="9a05e-136">**Ekle**'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="9a05e-136">Click **Add**.</span></span>

![](part-2/_static/image4.png)

<span data-ttu-id="9a05e-137">**Denetleyici Ekle** iletişim kutusunda aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="9a05e-137">In the **Add Controller** dialog, do the following:</span></span>

1. <span data-ttu-id="9a05e-138">**Model sınıfı** açılan menüsünde `Author` sınıfını seçin.</span><span class="sxs-lookup"><span data-stu-id="9a05e-138">In the **Model class** dropdown, select the `Author` class.</span></span> <span data-ttu-id="9a05e-139">(Açılan listede görmüyorsanız, projeyi derlediğinizden emin olun.)</span><span class="sxs-lookup"><span data-stu-id="9a05e-139">(If you don't see it listed in the dropdown, make sure that you built the project.)</span></span>
2. <span data-ttu-id="9a05e-140">"Zaman uyumsuz denetleyici eylemlerini kullan" öğesini işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="9a05e-140">Check "Use async controller actions".</span></span>
3. <span data-ttu-id="9a05e-141">Denetleyici adını &quot;AuthorsController&quot;olarak bırakın.</span><span class="sxs-lookup"><span data-stu-id="9a05e-141">Leave the controller name as &quot;AuthorsController&quot;.</span></span>
4. <span data-ttu-id="9a05e-142">**Veri bağlam sınıfının**yanındaki artı (+) düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9a05e-142">Click plus (+) button next to **Data Context Class**.</span></span>

![](part-2/_static/image5.png)

<span data-ttu-id="9a05e-143">**Yeni veri bağlamı** iletişim kutusunda varsayılan adı bırakın ve **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9a05e-143">In the **New Data Context** dialog, leave the default name and click **Add**.</span></span>

![](part-2/_static/image6.png)

<span data-ttu-id="9a05e-144">**Denetleyici Ekle** iletişim kutusunu doldurmak için **Ekle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9a05e-144">Click **Add** to complete the **Add Controller** dialog.</span></span> <span data-ttu-id="9a05e-145">İletişim kutusu projenize iki sınıf ekler:</span><span class="sxs-lookup"><span data-stu-id="9a05e-145">The dialog adds two classes to your project:</span></span>

- <span data-ttu-id="9a05e-146">`AuthorsController` bir Web API denetleyicisi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="9a05e-146">`AuthorsController` defines a Web API controller.</span></span> <span data-ttu-id="9a05e-147">Denetleyici, istemcilerin yazar listesinde CRUD işlemleri gerçekleştirmek için kullandığı REST API uygular.</span><span class="sxs-lookup"><span data-stu-id="9a05e-147">The controller implements the REST API that clients use to perform CRUD operations on the list of authors.</span></span>
- <span data-ttu-id="9a05e-148">`BookServiceContext`, çalışma zamanında nesne nesnelerini yönetir, bu da nesneleri bir veritabanından verilerle doldurmayı, değişiklik izlemeyi ve kalıcı verileri veritabanına getirmeyi içerir.</span><span class="sxs-lookup"><span data-stu-id="9a05e-148">`BookServiceContext` manages entity objects during run time, which includes populating objects with data from a database, change tracking, and persisting data to the database.</span></span> <span data-ttu-id="9a05e-149">`DbContext`devralır.</span><span class="sxs-lookup"><span data-stu-id="9a05e-149">It inherits from `DbContext`.</span></span>

![](part-2/_static/image7.png)

<span data-ttu-id="9a05e-150">Bu noktada, projeyi yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="9a05e-150">At this point, build the project again.</span></span> <span data-ttu-id="9a05e-151">Artık `Book` varlıkları için bir API denetleyicisi eklemek üzere aynı adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="9a05e-151">Now go through the same steps to add an API controller for `Book` entities.</span></span> <span data-ttu-id="9a05e-152">Bu kez, model sınıfı için `Book` ' ı seçin ve veri bağlamı sınıfı için mevcut `BookServiceContext` sınıfını seçin.</span><span class="sxs-lookup"><span data-stu-id="9a05e-152">This time, select `Book` for the model class, and select the existing `BookServiceContext` class for the data context class.</span></span> <span data-ttu-id="9a05e-153">(Yeni bir veri bağlamı oluşturmayın.) Denetleyiciyi eklemek için **Ekle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9a05e-153">(Don't create a new data context.) Click **Add** to add the controller.</span></span>

![](part-2/_static/image8.png)

> [!div class="step-by-step"]
> <span data-ttu-id="9a05e-154">[Önceki](part-1.md)
> [İleri](part-3.md)</span><span class="sxs-lookup"><span data-stu-id="9a05e-154">[Previous](part-1.md)
[Next](part-3.md)</span></span>
