---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'Öğretici: ASP.NET MVC 5 uygulamalarında EF ile devralma uygulama'
description: Bu öğretici, veri modelinde devralmayı nasıl uygulayacağınızı gösterir.
author: tdykstra
ms.author: riande
ms.date: 01/21/2019
ms.topic: tutorial
ms.assetid: 08834147-77ec-454a-bb7a-d931d2a40dab
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 73a01ed47b0935a1a9734c197377470defb1fe36
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583064"
---
# <a name="tutorial-implement-inheritance-with-ef-in-an-aspnet-mvc-5-app"></a><span data-ttu-id="43fa2-103">Öğretici: ASP.NET MVC 5 uygulamasında EF ile devralma uygulama</span><span class="sxs-lookup"><span data-stu-id="43fa2-103">Tutorial: Implement Inheritance with EF in an ASP.NET MVC 5 app</span></span>

<span data-ttu-id="43fa2-104">Önceki öğreticide eşzamanlılık özel durumları ele alınır.</span><span class="sxs-lookup"><span data-stu-id="43fa2-104">In the previous tutorial you handled concurrency exceptions.</span></span> <span data-ttu-id="43fa2-105">Bu öğretici, veri modelinde devralmayı nasıl uygulayacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="43fa2-105">This tutorial will show you how to implement inheritance in the data model.</span></span>

<span data-ttu-id="43fa2-106">Nesne odaklı programlamada, [kod yeniden kullanımını](http://en.wikipedia.org/wiki/Code_reuse)kolaylaştırmak için [devralmayı](http://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43fa2-106">In object-oriented programming, you can use [inheritance](http://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)) to facilitate [code reuse](http://en.wikipedia.org/wiki/Code_reuse).</span></span> <span data-ttu-id="43fa2-107">Bu öğreticide, `Instructor` ve `Student` sınıflarını, hem Eğitmenler hem de öğrenciler için ortak olan `LastName` gibi özellikleri içeren bir `Person` taban sınıftan türetireceğiz olacak şekilde değiştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="43fa2-107">In this tutorial, you'll change the `Instructor` and `Student` classes so that they derive from a `Person` base class which contains properties such as `LastName` that are common to both instructors and students.</span></span> <span data-ttu-id="43fa2-108">Herhangi bir Web sayfası eklemez veya değiştirmezsiniz, ancak koddan bazılarını değiştireceksiniz ve bu değişiklikler otomatik olarak veritabanına yansıtılacaktır.</span><span class="sxs-lookup"><span data-stu-id="43fa2-108">You won't add or change any web pages, but you'll change some of the code and those changes will be automatically reflected in the database.</span></span>

<span data-ttu-id="43fa2-109">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="43fa2-109">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="43fa2-110">Devralmayı veritabanına eşlemeyi öğrenin</span><span class="sxs-lookup"><span data-stu-id="43fa2-110">Learn to map inheritance to database</span></span>
> * <span data-ttu-id="43fa2-111">Kişi sınıfını oluşturma</span><span class="sxs-lookup"><span data-stu-id="43fa2-111">Create the Person class</span></span>
> * <span data-ttu-id="43fa2-112">Eğitmeni ve öğrenci 'yi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="43fa2-112">Update Instructor and Student</span></span>
> * <span data-ttu-id="43fa2-113">Modele kişi ekleme</span><span class="sxs-lookup"><span data-stu-id="43fa2-113">Add Person to the Model</span></span>
> * <span data-ttu-id="43fa2-114">Geçişleri oluşturma ve güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="43fa2-114">Create and Update Migrations</span></span>
> * <span data-ttu-id="43fa2-115">Uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="43fa2-115">Test the implementation</span></span>
> * <span data-ttu-id="43fa2-116">Azure’a dağıtma</span><span class="sxs-lookup"><span data-stu-id="43fa2-116">Deploy to Azure</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43fa2-117">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="43fa2-117">Prerequisites</span></span>

* [<span data-ttu-id="43fa2-118">Eşzamanlılığı İşleme</span><span class="sxs-lookup"><span data-stu-id="43fa2-118">Handling Concurrency</span></span>](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="map-inheritance-to-database"></a><span data-ttu-id="43fa2-119">Devralmayı veritabanına eşle</span><span class="sxs-lookup"><span data-stu-id="43fa2-119">Map inheritance to database</span></span>

<span data-ttu-id="43fa2-120">`School` veri modelindeki `Instructor` ve `Student` sınıfları özdeş olan birkaç özelliğe sahiptir:</span><span class="sxs-lookup"><span data-stu-id="43fa2-120">The `Instructor` and `Student` classes in the `School` data model have several properties that are identical:</span></span>

![Student_and_Instructor_classes](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="43fa2-122">`Instructor` ve `Student` varlıkları tarafından paylaşılan özellikler için gereksiz kodu ortadan kaldırmak istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="43fa2-122">Suppose you want to eliminate the redundant code for the properties that are shared by the `Instructor` and `Student` entities.</span></span> <span data-ttu-id="43fa2-123">Ya da adın bir eğitmenden veya bir öğrenciye ait olup olmadığına bakılmaksızın adları biçimlendirmeden bir hizmet yazmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43fa2-123">Or you want to write a service that can format names without caring whether the name came from an instructor or a student.</span></span> <span data-ttu-id="43fa2-124">Yalnızca bu paylaşılan özellikleri içeren `Person` bir temel sınıf oluşturabilirsiniz, sonra `Instructor` ve `Student` varlıkların aşağıdaki çizimde gösterildiği gibi bu temel sınıftan devralmasını sağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="43fa2-124">You could create a `Person` base class which contains only those shared properties, then make the `Instructor` and `Student` entities inherit from that base class, as shown in the following illustration:</span></span>

![Student_and_Instructor_classes_deriving_from_Person_class](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="43fa2-126">Bu devralma yapısının veritabanında temsil edilebilmesi için birkaç yol vardır.</span><span class="sxs-lookup"><span data-stu-id="43fa2-126">There are several ways this inheritance structure could be represented in the database.</span></span> <span data-ttu-id="43fa2-127">Tek bir tabloda hem öğrenciler hem de eğitmenler hakkında bilgi içeren bir `Person` tablonuz olabilir.</span><span class="sxs-lookup"><span data-stu-id="43fa2-127">You could have a `Person` table that includes information about both students and instructors in a single table.</span></span> <span data-ttu-id="43fa2-128">Bazı sütunlar yalnızca Eğitmenler (`HireDate`), bazıları yalnızca öğrencilerle (`EnrollmentDate`), bazıları ise (`LastName`, `FirstName`) uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="43fa2-128">Some of the columns could apply only to instructors (`HireDate`), some only to students (`EnrollmentDate`), some to both (`LastName`, `FirstName`).</span></span> <span data-ttu-id="43fa2-129">Genellikle, her bir satırın temsil ettiği türü belirtmek için bir *ayrıştırıcı* sütunu vardır.</span><span class="sxs-lookup"><span data-stu-id="43fa2-129">Typically, you'd have a *discriminator* column to indicate which type each row represents.</span></span> <span data-ttu-id="43fa2-130">Örneğin, ayrıştırıcı sütununda, Eğitmenler için "eğitmen" ve öğrenciler için "öğrenci" bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="43fa2-130">For example, the discriminator column might have "Instructor" for instructors and "Student" for students.</span></span>

![Hierarchy_example başına tablo](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="43fa2-132">Tek bir veritabanı tablosundan bir varlık devralma yapısı oluşturmanın bu düzeni, *hiyerarşi başına tablo* (TPH) devralma olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="43fa2-132">This pattern of generating an entity inheritance structure from a single database table is called *table-per-hierarchy* (TPH) inheritance.</span></span>

<span data-ttu-id="43fa2-133">Alternatif olarak, veritabanının devralma yapısına benzer bir şekilde görünmesini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43fa2-133">An alternative is to make the database look more like the inheritance structure.</span></span> <span data-ttu-id="43fa2-134">Örneğin, `Person` tablosunda yalnızca ad alanları olabilir ve Tarih alanlarıyla ayrı `Instructor` ve `Student` tabloları vardır.</span><span class="sxs-lookup"><span data-stu-id="43fa2-134">For example, you could have only the name fields in the `Person` table and have separate `Instructor` and `Student` tables with the date fields.</span></span>

![Type_inheritance başına tablo](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="43fa2-136">Her varlık sınıfı için bir veritabanı tablosu yapmanın bu düzeni, *tür başına tablo* (TPT) devralma olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="43fa2-136">This pattern of making a database table for each entity class is called *table per type* (TPT) inheritance.</span></span>

<span data-ttu-id="43fa2-137">Başka bir seçenek de Özet olmayan tüm türleri tek tek tablolarla eşlemenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="43fa2-137">Yet another option is to map all non-abstract types to individual tables.</span></span> <span data-ttu-id="43fa2-138">Devralınan özellikler de dahil olmak üzere bir sınıfın tüm özellikleri karşılık gelen tablonun sütunlarına eşlenir.</span><span class="sxs-lookup"><span data-stu-id="43fa2-138">All properties of a class, including inherited properties, map to columns of the corresponding table.</span></span> <span data-ttu-id="43fa2-139">Bu düzene, tablo başına somut sınıf (TPC) devralma adı verilir.</span><span class="sxs-lookup"><span data-stu-id="43fa2-139">This pattern is called Table-per-Concrete Class (TPC) inheritance.</span></span> <span data-ttu-id="43fa2-140">Daha önce gösterildiği gibi `Person`, `Student`ve `Instructor` sınıfları için TPC devralmayı uyguladıysanız, `Student` ve `Instructor` tabloları, daha önce olduğu gibi devralma uygulandıktan sonra farklı şekilde görünür.</span><span class="sxs-lookup"><span data-stu-id="43fa2-140">If you implemented TPC inheritance for the `Person`, `Student`, and `Instructor` classes as shown earlier, the `Student` and `Instructor` tables would look no different after implementing inheritance than they did before.</span></span>

<span data-ttu-id="43fa2-141">TPC ve TPH devralma desenleri genellikle TPT devralma desenlerinden daha iyi Entity Framework performans sağlar, çünkü TPT desenleri karmaşık JOIN sorgularına yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="43fa2-141">TPC and TPH inheritance patterns generally deliver better performance in the Entity Framework than TPT inheritance patterns, because TPT patterns can result in complex join queries.</span></span>

<span data-ttu-id="43fa2-142">Bu öğreticide, TPH devralmanın nasıl uygulanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="43fa2-142">This tutorial demonstrates how to implement TPH inheritance.</span></span> <span data-ttu-id="43fa2-143">TPH Entity Framework varsayılan devralma modelidir, bu yüzden tek yapmanız gerekir `Person` bir sınıf oluşturmak, `Person`türetmek için `Instructor` ve `Student` sınıfları değiştirmek, yeni sınıfı `DbContext`eklemek ve bir geçiş oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="43fa2-143">TPH is the default inheritance pattern in the Entity Framework, so all you have to do is create a `Person` class, change the `Instructor` and `Student` classes to derive from `Person`, add the new class to the `DbContext`, and create a migration.</span></span> <span data-ttu-id="43fa2-144">(Diğer devralma düzenlerini uygulama hakkında daha fazla bilgi için, bkz. [tür başına tablo (TPT) devralmayı eşleme](https://msdn.microsoft.com/data/jj591617#2.5) ve MSDN Entity Framework belgelerinde [somut sınıf başına tablo (TPC) devralmayı](https://msdn.microsoft.com/data/jj591617#2.6) eşleme.)</span><span class="sxs-lookup"><span data-stu-id="43fa2-144">(For information about how to implement the other inheritance patterns, see [Mapping the Table-Per-Type (TPT) Inheritance](https://msdn.microsoft.com/data/jj591617#2.5) and [Mapping the Table-Per-Concrete Class (TPC) Inheritance](https://msdn.microsoft.com/data/jj591617#2.6) in the MSDN Entity Framework documentation.)</span></span>

## <a name="create-the-person-class"></a><span data-ttu-id="43fa2-145">Kişi sınıfını oluşturma</span><span class="sxs-lookup"><span data-stu-id="43fa2-145">Create the Person class</span></span>

<span data-ttu-id="43fa2-146">*Modeller* klasöründe *Person.cs* oluşturun ve şablon kodunu şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="43fa2-146">In the *Models* folder, create *Person.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="update-instructor-and-student"></a><span data-ttu-id="43fa2-147">Eğitmeni ve öğrenci 'yi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="43fa2-147">Update Instructor and Student</span></span>

<span data-ttu-id="43fa2-148">Şimdi *Person.SC*değerlerini devralması için *Instructor.cs* ve *Student.cs* güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="43fa2-148">Now update the *Instructor.cs* and *Student.cs* to inherit values from the *Person.sc*.</span></span>

<span data-ttu-id="43fa2-149">*Instructor.cs*' de, `Instructor` sınıfını `Person` sınıfından türetirsiniz ve anahtar ve ad alanlarını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="43fa2-149">In *Instructor.cs*, derive the `Instructor` class from the `Person` class and remove the key and name fields.</span></span> <span data-ttu-id="43fa2-150">Kod aşağıdaki örneğe benzer şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="43fa2-150">The code will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="43fa2-151">*Student.cs*'de benzer değişiklikler yapın.</span><span class="sxs-lookup"><span data-stu-id="43fa2-151">Make similar changes to *Student.cs*.</span></span> <span data-ttu-id="43fa2-152">`Student` sınıfı aşağıdaki örneğe benzer şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="43fa2-152">The `Student` class will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="add-person-to-the-model"></a><span data-ttu-id="43fa2-153">Modele kişi ekleme</span><span class="sxs-lookup"><span data-stu-id="43fa2-153">Add Person to the Model</span></span>

<span data-ttu-id="43fa2-154">*SchoolContext.cs*' de, `Person` varlık türü için bir `DbSet` özelliği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="43fa2-154">In *SchoolContext.cs*, add a `DbSet` property for the `Person` entity type:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="43fa2-155">Bu, Entity Framework hiyerarşinin devralma devralınmasını yapılandırmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="43fa2-155">This is all that the Entity Framework needs in order to configure table-per-hierarchy inheritance.</span></span> <span data-ttu-id="43fa2-156">Gördüğünüz gibi, veritabanı güncelleştirildiği sırada `Student` ve `Instructor` tablolarının yerine bir `Person` tablosu olacaktır.</span><span class="sxs-lookup"><span data-stu-id="43fa2-156">As you'll see, when the database is updated, it will have a `Person` table in place of the `Student` and `Instructor` tables.</span></span>

## <a name="create-and-update-migrations"></a><span data-ttu-id="43fa2-157">Geçişleri oluşturma ve güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="43fa2-157">Create and Update Migrations</span></span>

<span data-ttu-id="43fa2-158">Paket Yöneticisi konsolunda (PMC), aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="43fa2-158">In the Package Manager Console (PMC), enter the following command:</span></span>

`Add-Migration Inheritance`

<span data-ttu-id="43fa2-159">PMC 'de `Update-Database` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="43fa2-159">Run the `Update-Database` command in the PMC.</span></span> <span data-ttu-id="43fa2-160">Bu noktada, geçiş işlemi nasıl işleneceğini bilmez.</span><span class="sxs-lookup"><span data-stu-id="43fa2-160">The command will fail at this point because we have existing data that migrations doesn't know how to handle.</span></span> <span data-ttu-id="43fa2-161">Aşağıdakine benzer bir hata iletisi alırsınız:</span><span class="sxs-lookup"><span data-stu-id="43fa2-161">You get an error message like the following one:</span></span>

> <span data-ttu-id="43fa2-162">*' Dbo ' nesnesi bırakılamıyor. Eğitmen ', yabancı anahtar kısıtlaması tarafından başvurulduğu için.*</span><span class="sxs-lookup"><span data-stu-id="43fa2-162">*Could not drop object 'dbo.Instructor' because it is referenced by a FOREIGN KEY constraint.*</span></span>

<span data-ttu-id="43fa2-163">*Geçişleri\&lt; timestamp&gt;\_Inheritance.cs* açın ve `Up` yöntemini aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="43fa2-163">Open *Migrations\&lt;timestamp&gt;\_Inheritance.cs* and replace the `Up` method with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

<span data-ttu-id="43fa2-164">Bu kod aşağıdaki veritabanı güncelleştirme görevlerini gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="43fa2-164">This code takes care of the following database update tasks:</span></span>

- <span data-ttu-id="43fa2-165">Yabancı anahtar kısıtlamalarını ve öğrenci tablosuna işaret eden dizinleri kaldırır.</span><span class="sxs-lookup"><span data-stu-id="43fa2-165">Removes foreign key constraints and indexes that point to the Student table.</span></span>
- <span data-ttu-id="43fa2-166">Eğitmen tablosunu kişi olarak yeniden adlandırır ve öğrenci verilerini depolamak için gerekli değişiklikleri yapar:</span><span class="sxs-lookup"><span data-stu-id="43fa2-166">Renames the Instructor table as Person and makes changes needed for it to store Student data:</span></span>

    - <span data-ttu-id="43fa2-167">Öğrenciler için Nullable kayıt tarihi ekler.</span><span class="sxs-lookup"><span data-stu-id="43fa2-167">Adds nullable EnrollmentDate for students.</span></span>
    - <span data-ttu-id="43fa2-168">Bir satırın bir öğrenci mi yoksa bir eğitmen mi olduğunu göstermek için ayrıştırıcı sütunu ekler.</span><span class="sxs-lookup"><span data-stu-id="43fa2-168">Adds Discriminator column to indicate whether a row is for a student or an instructor.</span></span>
    - <span data-ttu-id="43fa2-169">Öğrenci satırlarında işe alma tarihleri olmadığından, HireDate null yapılabilir hale gelir.</span><span class="sxs-lookup"><span data-stu-id="43fa2-169">Makes HireDate nullable since student rows won't have hire dates.</span></span>
    - <span data-ttu-id="43fa2-170">Öğrencilere işaret eden yabancı anahtarları güncelleştirmek için kullanılacak geçici bir alan ekler.</span><span class="sxs-lookup"><span data-stu-id="43fa2-170">Adds a temporary field that will be used to update foreign keys that point to students.</span></span> <span data-ttu-id="43fa2-171">Öğrencileri kişi tablosuna kopyaladığınızda yeni birincil anahtar değerleri alırlar.</span><span class="sxs-lookup"><span data-stu-id="43fa2-171">When you copy students into the Person table they'll get new primary key values.</span></span>
- <span data-ttu-id="43fa2-172">Öğrenci tablosundaki verileri kişi tablosuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="43fa2-172">Copies data from the Student table into the Person table.</span></span> <span data-ttu-id="43fa2-173">Bu, öğrencilerden yeni birincil anahtar değerleri atanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="43fa2-173">This causes students to get assigned new primary key values.</span></span>
- <span data-ttu-id="43fa2-174">Öğrencilere işaret eden yabancı anahtar değerlerini düzeltir.</span><span class="sxs-lookup"><span data-stu-id="43fa2-174">Fixes foreign key values that point to students.</span></span>
- <span data-ttu-id="43fa2-175">Yabancı anahtar kısıtlamalarını ve dizinleri yeniden oluşturur, şimdi bunları kişi tablosuna işaret eder.</span><span class="sxs-lookup"><span data-stu-id="43fa2-175">Re-creates foreign key constraints and indexes, now pointing them to the Person table.</span></span>

<span data-ttu-id="43fa2-176">(Birincil anahtar türü olarak tamsayı yerine GUID kullandıysanız, öğrenci birincil anahtar değerlerinin değiştirilmesi gerekmez ve bu adımların bazıları atlanamaz.)</span><span class="sxs-lookup"><span data-stu-id="43fa2-176">(If you had used GUID instead of integer as the primary key type, the student primary key values wouldn't have to change, and several of these steps could have been omitted.)</span></span>

<span data-ttu-id="43fa2-177">`update-database` komutunu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="43fa2-177">Run the `update-database` command again.</span></span>

<span data-ttu-id="43fa2-178">(Bir üretim sisteminde, önceki veritabanı sürümüne geri dönmek için bunu kullanmak zorunda kalbilmeniz durumunda, ilgili değişiklikleri aşağı doğru yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="43fa2-178">(In a production system you would make corresponding changes to the Down method in case you ever had to use that to go back to the previous database version.</span></span> <span data-ttu-id="43fa2-179">Bu öğreticide, aşağı yöntemini kullanmayacağız.)</span><span class="sxs-lookup"><span data-stu-id="43fa2-179">For this tutorial you won't be using the Down method.)</span></span>

> [!NOTE]
> <span data-ttu-id="43fa2-180">Verileri geçirirken ve şema değişiklikleri yaparken başka hatalar almak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="43fa2-180">It's possible to get other errors when migrating data and making schema changes.</span></span> <span data-ttu-id="43fa2-181">Çözümleyemez geçiş hataları alırsanız, *Web. config* dosyasındaki bağlantı dizesini değiştirerek veya veritabanını silerek öğreticiye devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43fa2-181">If you get migration errors you can't resolve, you can continue with the tutorial by changing the connection string in the *Web.config* file or by deleting the database.</span></span> <span data-ttu-id="43fa2-182">En basit yaklaşım, *Web. config* dosyasındaki veritabanını yeniden adlandırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="43fa2-182">The simplest approach is to rename the database in the *Web.config* file.</span></span> <span data-ttu-id="43fa2-183">Örneğin, aşağıdaki örnekte gösterildiği gibi, veritabanı adını ContosoUniversity2 olarak değiştirin:</span><span class="sxs-lookup"><span data-stu-id="43fa2-183">For example, change the database name to ContosoUniversity2 as shown in the following example:</span></span>
>
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.xml?highlight=2)]
>
> <span data-ttu-id="43fa2-184">Yeni bir veritabanı ile geçirilecek veri yoktur ve `update-database` komutunun hatasız tamamlanabilmesi çok daha yüksektir.</span><span class="sxs-lookup"><span data-stu-id="43fa2-184">With a new database, there is no data to migrate, and the `update-database` command is much more likely to complete without errors.</span></span> <span data-ttu-id="43fa2-185">Veritabanının nasıl silineceği hakkında yönergeler için bkz. [Visual Studio 'dan bir veritabanını bırakma 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span><span class="sxs-lookup"><span data-stu-id="43fa2-185">For instructions on how to delete the database, see [How to Drop a Database from Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span></span> <span data-ttu-id="43fa2-186">Öğreticiye devam etmek için bu yaklaşımla karşılaşırsanız, Bu öğreticinin sonundaki dağıtım adımını atlayın veya yeni bir siteye ve veritabanına dağıtın.</span><span class="sxs-lookup"><span data-stu-id="43fa2-186">If you take this approach in order to continue with the tutorial, skip the deployment step at the end of this tutorial or deploy to a new site and database.</span></span> <span data-ttu-id="43fa2-187">Zaten dağıtmakta olduğunuz siteye bir güncelleştirme dağıtırsanız,, geçişleri otomatik olarak çalıştırdığında EF aynı hatayı alır.</span><span class="sxs-lookup"><span data-stu-id="43fa2-187">If you deploy an update to the same site you've been deploying to already, EF will get the same error there when it runs migrations automatically.</span></span> <span data-ttu-id="43fa2-188">Bir geçiş hatasıyla ilgili sorunları gidermek istiyorsanız en iyi kaynak Entity Framework forumlarından veya StackOverflow.com biridir.</span><span class="sxs-lookup"><span data-stu-id="43fa2-188">If you want to troubleshoot a migrations error, the best resource is one of the Entity Framework forums or StackOverflow.com.</span></span>

## <a name="test-the-implementation"></a><span data-ttu-id="43fa2-189">Uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="43fa2-189">Test the implementation</span></span>

<span data-ttu-id="43fa2-190">Siteyi çalıştırın ve çeşitli sayfaları deneyin.</span><span class="sxs-lookup"><span data-stu-id="43fa2-190">Run the site and try various pages.</span></span> <span data-ttu-id="43fa2-191">Her şey, daha önce olduğu gibi çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="43fa2-191">Everything works the same as it did before.</span></span>

<span data-ttu-id="43fa2-192">**Sunucu Gezgini** **veri Connections\SchoolContext** ve ardından **Tablolar**' ı genişletin ve **öğrenci** ve **eğitmen** tablolarının bir **kişi** tablosu ile değiştirildiğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="43fa2-192">In **Server Explorer,** expand **Data Connections\SchoolContext** and then **Tables**, and you see that the **Student** and **Instructor** tables have been replaced by a **Person** table.</span></span> <span data-ttu-id="43fa2-193">**Kişi** tablosunu genişletin ve **öğrenci** ve **eğitmen** tablolarında, kullanılan tüm sütunları olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="43fa2-193">Expand the **Person** table and you see that it has all of the columns that used to be in the **Student** and **Instructor** tables.</span></span>

<span data-ttu-id="43fa2-194">Kişi tablosuna sağ tıklayın ve ardından **tablo verilerini göster** ' e tıklayarak ayrıştırıcı sütununu görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="43fa2-194">Right-click the Person table, and then click **Show Table Data** to see the discriminator column.</span></span>

<span data-ttu-id="43fa2-195">Aşağıdaki diyagramda, yeni okul veritabanının yapısı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="43fa2-195">The following diagram illustrates the structure of the new School database:</span></span>

![School_database_diagram](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="43fa2-197">Azure’a dağıtma</span><span class="sxs-lookup"><span data-stu-id="43fa2-197">Deploy to Azure</span></span>

<span data-ttu-id="43fa2-198">Bu bölümde, bu öğretici serisinin bölüm [3, sıralama, filtreleme ve sayfalama](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md) bölümünde **Azure 'a uygulamayı** isteğe bağlı olarak dağıtma bölümünden tamamlamış olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="43fa2-198">This section requires you to have completed the optional **Deploying the app to Azure** section in [Part 3, Sorting, Filtering, and Paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md) of this tutorial series.</span></span> <span data-ttu-id="43fa2-199">Yerel projenizde veritabanını silerek çözümladığınız hataları geçirseniz, bu adımı atlayın; ya da yeni bir site ve veritabanı oluşturup yeni ortama dağıtın.</span><span class="sxs-lookup"><span data-stu-id="43fa2-199">If you had migrations errors that you resolved by deleting the database in your local project, skip this step; or create a new site and database, and deploy to the new environment.</span></span>

1. <span data-ttu-id="43fa2-200">Visual Studio 'da **Çözüm Gezgini** projeye sağ tıklayın ve bağlam menüsünden **Yayımla** ' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="43fa2-200">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>

2. <span data-ttu-id="43fa2-201">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="43fa2-201">Click **Publish**.</span></span>

    <span data-ttu-id="43fa2-202">Web uygulaması varsayılan tarayıcınızda açılır.</span><span class="sxs-lookup"><span data-stu-id="43fa2-202">The Web app opens in your default browser.</span></span>

3. <span data-ttu-id="43fa2-203">Çalışıp çalışmadığını doğrulamak için uygulamayı test edin.</span><span class="sxs-lookup"><span data-stu-id="43fa2-203">Test the application to verify it's working.</span></span>

    <span data-ttu-id="43fa2-204">Veritabanına erişen bir sayfayı ilk kez çalıştırdığınızda Entity Framework, geçerli veri modeliyle veritabanını güncel hale getirmek için gereken tüm geçişleri `Up` yöntemlerini çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="43fa2-204">The first time you run a page that accesses the database, the Entity Framework runs all of the migrations `Up` methods required to bring the database up to date with the current data model.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="43fa2-205">Kodu alma</span><span class="sxs-lookup"><span data-stu-id="43fa2-205">Get the code</span></span>

[<span data-ttu-id="43fa2-206">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="43fa2-206">Download Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="43fa2-207">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="43fa2-207">Additional resources</span></span>

<span data-ttu-id="43fa2-208">Diğer Entity Framework kaynaklarına bağlantılar [ASP.NET Data Access-önerilen kaynaklarda](../../../../whitepapers/aspnet-data-access-content-map.md)bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="43fa2-208">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

<span data-ttu-id="43fa2-209">Bu ve diğer devralma yapıları hakkında daha fazla bilgi için MSDN 'deki [TPT devralma deseninin](https://msdn.microsoft.com/data/jj618293) ve [TPH devralma deseninin](https://msdn.microsoft.com/data/jj618292) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="43fa2-209">For more information about this and other inheritance structures, see [TPT Inheritance Pattern](https://msdn.microsoft.com/data/jj618293) and [TPH Inheritance Pattern](https://msdn.microsoft.com/data/jj618292) on MSDN.</span></span> <span data-ttu-id="43fa2-210">Sonraki öğreticide, çeşitli görece gelişmiş Entity Framework senaryolarını nasıl işleyeceğinizi göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="43fa2-210">In the next tutorial you'll see how to handle a variety of relatively advanced Entity Framework scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43fa2-211">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="43fa2-211">Next steps</span></span>

<span data-ttu-id="43fa2-212">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="43fa2-212">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="43fa2-213">Devralma veritabanına eşlenmeli</span><span class="sxs-lookup"><span data-stu-id="43fa2-213">Learned to map inheritance to database</span></span>
> * <span data-ttu-id="43fa2-214">Kişi sınıfı oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="43fa2-214">Created the Person class</span></span>
> * <span data-ttu-id="43fa2-215">Güncelleştirilmiş eğitmen ve öğrenci</span><span class="sxs-lookup"><span data-stu-id="43fa2-215">Updated Instructor and Student</span></span>
> * <span data-ttu-id="43fa2-216">Modele kişi eklendi</span><span class="sxs-lookup"><span data-stu-id="43fa2-216">Added Person to the Model</span></span>
> * <span data-ttu-id="43fa2-217">Geçişleri oluşturma ve güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="43fa2-217">Created and Update Migrations</span></span>
> * <span data-ttu-id="43fa2-218">Uygulama test edildi</span><span class="sxs-lookup"><span data-stu-id="43fa2-218">Tested the implementation</span></span>
> * <span data-ttu-id="43fa2-219">Azure 'a dağıtıldı</span><span class="sxs-lookup"><span data-stu-id="43fa2-219">Deployed to Azure</span></span>

<span data-ttu-id="43fa2-220">Entity Framework Code First kullanan ASP.NET Web uygulamaları geliştirme hakkında temel bilgileri aşdığınızda bilmeniz gereken konular hakkında bilgi edinmek için sonraki makaleye ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="43fa2-220">Advance to the next article to learn about topics that are useful to be aware of when you go beyond the basics of developing ASP.NET web applications that use Entity Framework Code First.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="43fa2-221">Gelişmiş Entity Framework Senaryoları</span><span class="sxs-lookup"><span data-stu-id="43fa2-221">Advanced Entity Framework Scenarios</span></span>](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
