---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC uygulamasında Entity Framework devralma uygulama (8/10) | Microsoft Docs
author: tdykstra
description: Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: a5c3feff-5335-4cdd-a97d-f7a8785c2494
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9507cba71b976825257cc9948d54f2651355959d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595314"
---
# <a name="implementing-inheritance-with-the-entity-framework-in-an-aspnet-mvc-application-8-of-10"></a><span data-ttu-id="d75ba-103">Bir ASP.NET MVC uygulamasında Entity Framework devralma uygulama (8/10)</span><span class="sxs-lookup"><span data-stu-id="d75ba-103">Implementing Inheritance with the Entity Framework in an ASP.NET MVC Application (8 of 10)</span></span>

<span data-ttu-id="d75ba-104">[Tom Dykstra](https://github.com/tdykstra) tarafından</span><span class="sxs-lookup"><span data-stu-id="d75ba-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="d75ba-105">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="d75ba-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="d75ba-106">Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio 2012 kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="d75ba-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="d75ba-107">Öğretici serisi hakkında daha fazla bilgi için, [serideki ilk öğreticiye](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="d75ba-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="d75ba-108">Öğretici serisini başlangıçtan başlatabilir veya [Bu bölüm için bir başlangıç projesi indirebilir](building-the-ef5-mvc4-chapter-downloads.md) ve buradan başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d75ba-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="d75ba-109">Giderebileceğiniz bir sorunla karşılaşırsanız, [Tamamlanan bölümü indirin](building-the-ef5-mvc4-chapter-downloads.md) ve sorununuzu yeniden oluşturmaya çalışın.</span><span class="sxs-lookup"><span data-stu-id="d75ba-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="d75ba-110">Sorunu, kodunuzun tamamlanan kodla karşılaştırarak genellikle soruna çözüm olarak ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d75ba-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="d75ba-111">Bazı yaygın hatalar ve bunların nasıl çözüleceği için bkz [. hatalar ve geçici çözümler.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="d75ba-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="d75ba-112">Önceki öğreticide eşzamanlılık özel durumları ele alınır.</span><span class="sxs-lookup"><span data-stu-id="d75ba-112">In the previous tutorial you handled concurrency exceptions.</span></span> <span data-ttu-id="d75ba-113">Bu öğretici, veri modelinde devralmayı nasıl uygulayacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="d75ba-113">This tutorial will show you how to implement inheritance in the data model.</span></span>

<span data-ttu-id="d75ba-114">Nesne odaklı programlamada, gereksiz kodu kaldırmak için devralmayı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d75ba-114">In object-oriented programming, you can use inheritance to eliminate redundant code.</span></span> <span data-ttu-id="d75ba-115">Bu öğreticide, `Instructor` ve `Student` sınıflarını, hem Eğitmenler hem de öğrenciler için ortak olan `LastName` gibi özellikleri içeren bir `Person` taban sınıftan türetireceğiz olacak şekilde değiştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d75ba-115">In this tutorial, you'll change the `Instructor` and `Student` classes so that they derive from a `Person` base class which contains properties such as `LastName` that are common to both instructors and students.</span></span> <span data-ttu-id="d75ba-116">Herhangi bir Web sayfası eklemez veya değiştirmezsiniz, ancak koddan bazılarını değiştireceksiniz ve bu değişiklikler otomatik olarak veritabanına yansıtılacaktır.</span><span class="sxs-lookup"><span data-stu-id="d75ba-116">You won't add or change any web pages, but you'll change some of the code and those changes will be automatically reflected in the database.</span></span>

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a><span data-ttu-id="d75ba-117">Tablo başına hiyerarşi ve tablo başına tür devralma</span><span class="sxs-lookup"><span data-stu-id="d75ba-117">Table-per-Hierarchy versus Table-per-Type Inheritance</span></span>

<span data-ttu-id="d75ba-118">Nesne odaklı programlamada, ilgili sınıflarla çalışmayı kolaylaştırmak için devralmayı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d75ba-118">In object-oriented programming, you can use inheritance to make it easier to work with related classes.</span></span> <span data-ttu-id="d75ba-119">Örneğin, `School` veri modelindeki `Instructor` ve `Student` sınıfları, çok sayıda özelliği paylaşır ve bu da gereksiz kod ile sonuçlanır:</span><span class="sxs-lookup"><span data-stu-id="d75ba-119">For example, the `Instructor` and `Student` classes in the `School` data model share several properties, which results in redundant code:</span></span>

![Student_and_Instructor_classes](https://asp.net/media/2578113/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_e7a32f99-8bc4-48ce-aeaf-216a18071a8b.png)

<span data-ttu-id="d75ba-121">`Instructor` ve `Student` varlıkları tarafından paylaşılan özellikler için gereksiz kodu ortadan kaldırmak istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="d75ba-121">Suppose you want to eliminate the redundant code for the properties that are shared by the `Instructor` and `Student` entities.</span></span> <span data-ttu-id="d75ba-122">Yalnızca bu paylaşılan özellikleri içeren `Person` bir temel sınıf oluşturabilirsiniz, sonra `Instructor` ve `Student` varlıkların aşağıdaki çizimde gösterildiği gibi bu temel sınıftan devralmasını sağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d75ba-122">You could create a `Person` base class which contains only those shared properties, then make the `Instructor` and `Student` entities inherit from that base class, as shown in the following illustration:</span></span>

![Student_and_Instructor_classes_deriving_from_Person_class](https://asp.net/media/2578119/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_deriving_from_Person_class_671d708c-cbb8-454a-a8f8-c2d99439acd9.png)

<span data-ttu-id="d75ba-124">Bu devralma yapısının veritabanında temsil edilebilmesi için birkaç yol vardır.</span><span class="sxs-lookup"><span data-stu-id="d75ba-124">There are several ways this inheritance structure could be represented in the database.</span></span> <span data-ttu-id="d75ba-125">Tek bir tabloda hem öğrenciler hem de eğitmenler hakkında bilgi içeren bir `Person` tablonuz olabilir.</span><span class="sxs-lookup"><span data-stu-id="d75ba-125">You could have a `Person` table that includes information about both students and instructors in a single table.</span></span> <span data-ttu-id="d75ba-126">Bazı sütunlar yalnızca Eğitmenler (`HireDate`), bazıları yalnızca öğrencilerle (`EnrollmentDate`), bazıları ise (`LastName`, `FirstName`) uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="d75ba-126">Some of the columns could apply only to instructors (`HireDate`), some only to students (`EnrollmentDate`), some to both (`LastName`, `FirstName`).</span></span> <span data-ttu-id="d75ba-127">Genellikle, her bir satırın temsil ettiği türü belirtmek için bir *ayrıştırıcı* sütunu vardır.</span><span class="sxs-lookup"><span data-stu-id="d75ba-127">Typically, you'd have a *discriminator* column to indicate which type each row represents.</span></span> <span data-ttu-id="d75ba-128">Örneğin, ayrıştırıcı sütununda, Eğitmenler için "eğitmen" ve öğrenciler için "öğrenci" bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="d75ba-128">For example, the discriminator column might have "Instructor" for instructors and "Student" for students.</span></span>

![Hierarchy_example başına tablo](https://asp.net/media/2578125/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-hierarchy_example_244067cd-b451-4e9b-9595-793b9afca505.png)

<span data-ttu-id="d75ba-130">Tek bir veritabanı tablosundan bir varlık devralma yapısı oluşturmanın bu düzeni, *hiyerarşi başına tablo* (TPH) devralma olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="d75ba-130">This pattern of generating an entity inheritance structure from a single database table is called *table-per-hierarchy* (TPH) inheritance.</span></span>

<span data-ttu-id="d75ba-131">Alternatif olarak, veritabanının devralma yapısına benzer bir şekilde görünmesini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d75ba-131">An alternative is to make the database look more like the inheritance structure.</span></span> <span data-ttu-id="d75ba-132">Örneğin, `Person` tablosunda yalnızca ad alanları olabilir ve Tarih alanlarıyla ayrı `Instructor` ve `Student` tabloları vardır.</span><span class="sxs-lookup"><span data-stu-id="d75ba-132">For example, you could have only the name fields in the `Person` table and have separate `Instructor` and `Student` tables with the date fields.</span></span>

![Type_inheritance başına tablo](https://asp.net/media/2578131/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-type_inheritance.png)

<span data-ttu-id="d75ba-134">Her varlık sınıfı için bir veritabanı tablosu yapmanın bu düzeni, *tür başına tablo* (TPT) devralma olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="d75ba-134">This pattern of making a database table for each entity class is called *table per type* (TPT) inheritance.</span></span>

<span data-ttu-id="d75ba-135">TPH devralma desenleri genellikle TPT devralma desenlerinden daha iyi Entity Framework performans sağlar, çünkü TPT desenleri karmaşık JOIN sorgularına yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="d75ba-135">TPH inheritance patterns generally deliver better performance in the Entity Framework than TPT inheritance patterns, because TPT patterns can result in complex join queries.</span></span> <span data-ttu-id="d75ba-136">Bu öğreticide, TPH devralmanın nasıl uygulanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d75ba-136">This tutorial demonstrates how to implement TPH inheritance.</span></span> <span data-ttu-id="d75ba-137">Bunu aşağıdaki adımları gerçekleştirerek gerçekleştirirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d75ba-137">You'll do that by performing the following steps:</span></span>

- <span data-ttu-id="d75ba-138">`Person` sınıf oluşturun ve `Person`türetmede `Instructor` ve `Student` sınıfları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d75ba-138">Create a `Person` class and change the `Instructor` and `Student` classes to derive from `Person`.</span></span>
- <span data-ttu-id="d75ba-139">Veritabanı bağlamı sınıfına modelden veritabanına eşleme kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d75ba-139">Add model-to-database mapping code to the database context class.</span></span>
- <span data-ttu-id="d75ba-140">Proje genelinde `InstructorID` ve `StudentID` başvurularını `PersonID`olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d75ba-140">Change `InstructorID` and `StudentID` references throughout the project to `PersonID`.</span></span>

## <a name="creating-the-person-class"></a><span data-ttu-id="d75ba-141">Kişi sınıfı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d75ba-141">Creating the Person Class</span></span>

 <span data-ttu-id="d75ba-142">Note: Bu sınıfları kullanan denetleyicileri güncelleştirene kadar, aşağıdaki sınıfları oluşturduktan sonra projeyi derleyemeyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d75ba-142">Note: You won't be able to compile the project after creating the classes below until you update the controllers that uses these classes.</span></span> 

<span data-ttu-id="d75ba-143">*Modeller* klasöründe *Person.cs* oluşturun ve şablon kodunu şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="d75ba-143">In the *Models* folder, create *Person.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="d75ba-144">*Instructor.cs*' de, `Instructor` sınıfını `Person` sınıfından türetirsiniz ve anahtar ve ad alanlarını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="d75ba-144">In *Instructor.cs*, derive the `Instructor` class from the `Person` class and remove the key and name fields.</span></span> <span data-ttu-id="d75ba-145">Kod aşağıdaki örneğe benzer şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="d75ba-145">The code will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="d75ba-146">*Student.cs*'de benzer değişiklikler yapın.</span><span class="sxs-lookup"><span data-stu-id="d75ba-146">Make similar changes to *Student.cs*.</span></span> <span data-ttu-id="d75ba-147">`Student` sınıfı aşağıdaki örneğe benzer şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="d75ba-147">The `Student` class will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="adding-the-person-entity-type-to-the-model"></a><span data-ttu-id="d75ba-148">Kişi varlık türü modele ekleniyor</span><span class="sxs-lookup"><span data-stu-id="d75ba-148">Adding the Person Entity Type to the Model</span></span>

<span data-ttu-id="d75ba-149">*SchoolContext.cs*' de, `Person` varlık türü için bir `DbSet` özelliği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d75ba-149">In *SchoolContext.cs*, add a `DbSet` property for the `Person` entity type:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="d75ba-150">Bu, Entity Framework hiyerarşinin devralma devralınmasını yapılandırmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d75ba-150">This is all that the Entity Framework needs in order to configure table-per-hierarchy inheritance.</span></span> <span data-ttu-id="d75ba-151">Gördüğünüz gibi, veritabanı yeniden oluşturulduğunda, `Student` ve `Instructor` tablolarının yerine bir `Person` tablosu olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d75ba-151">As you'll see, when the database is re-created, it will have a `Person` table in place of the `Student` and `Instructor` tables.</span></span>

## <a name="changing-instructorid-and-studentid-to-personid"></a><span data-ttu-id="d75ba-152">Komutctorıd ve StudentID ile PersonID arasında değişiklik</span><span class="sxs-lookup"><span data-stu-id="d75ba-152">Changing InstructorID and StudentID to PersonID</span></span>

<span data-ttu-id="d75ba-153">*SchoolContext.cs*' de, eğitmen-kurs eşleme bildiriminde `MapRightKey("InstructorID")` `MapRightKey("PersonID")`olarak değiştirin:</span><span class="sxs-lookup"><span data-stu-id="d75ba-153">In *SchoolContext.cs*, in the Instructor-Course mapping statement, change `MapRightKey("InstructorID")` to `MapRightKey("PersonID")`:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=4)]

<span data-ttu-id="d75ba-154">Bu değişiklik gerekli değildir; yalnızca çok-çok birleşme tablosundaki Komutctorıd sütununun adını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="d75ba-154">This change isn't required; it just changes the name of the InstructorID column in the many-to-many join table.</span></span> <span data-ttu-id="d75ba-155">Adı Komutctorıd olarak bıraktıysanız, uygulama yine de doğru şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="d75ba-155">If you left the name as InstructorID, the application would still work correctly.</span></span> <span data-ttu-id="d75ba-156">Tamamlanan *SchoolContext.cs*şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d75ba-156">Here is the completed *SchoolContext.cs*:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=15,24)]

<span data-ttu-id="d75ba-157">Daha sonra, *geçişler* klasöründeki zaman damgalı geçişler dosyaları ***hariç*** `InstructorID` `PersonID` ve proje genelinde `PersonID` `StudentID` değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d75ba-157">Next you need to change `InstructorID` to `PersonID` and `StudentID` to `PersonID` throughout the project ***except*** in the time-stamped migrations files in the *Migrations* folder.</span></span> <span data-ttu-id="d75ba-158">Bunu yapmak için yalnızca değiştirilmesi gereken dosyaları bulup açarak açılan dosyalarda genel bir değişiklik yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d75ba-158">To do that you'll find and open only the files that need to be changed, then perform a global change on the opened files.</span></span> <span data-ttu-id="d75ba-159">*Geçiş* klasörünüzdeki tek dosya *Migrations\configuration.exe* ' dir.</span><span class="sxs-lookup"><span data-stu-id="d75ba-159">The only file in the *Migrations* folder you should change is *Migrations\Configuration.cs.*</span></span>

1. > [!IMPORTANT]
   > <span data-ttu-id="d75ba-160">Visual Studio 'daki tüm açık dosyaları kapatarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="d75ba-160">Begin by closing all the open files in Visual Studio.</span></span>
2. <span data-ttu-id="d75ba-161">Bul ve Değiştir ' e tıklayın, **Düzenle** menüsünde **tüm dosyaları bul** ' u ve ardından projede `InstructorID`içeren tüm dosyaları ara ' yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d75ba-161">Click **Find and Replace -- Find all Files** in the **Edit** menu, and then search for all files in the project that contain `InstructorID`.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. <span data-ttu-id="d75ba-162">Her dosya için bir satıra çift tıklayarak *geçişler* klasöründeki &lt;zaman damgası&gt; *\_. cs* geçiş dosyaları ***dışında*** her bir dosyayı açın.</span><span class="sxs-lookup"><span data-stu-id="d75ba-162">Open each file in the **Find Results** window ***except*** the &lt;time-stamp&gt;*\_.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)
4. <span data-ttu-id="d75ba-163">**Dosyaları değiştir** iletişim kutusunu açın ve **açık belgelerin tümünde** **görünümü** değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d75ba-163">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
5. <span data-ttu-id="d75ba-164">Tüm `InstructorID` `PersonID.` olarak değiştirmek için **dosyaları değiştir** iletişim kutusunu kullanın</span><span class="sxs-lookup"><span data-stu-id="d75ba-164">Use the **Replace in Files** dialog to change all `InstructorID` to `PersonID.`</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)
6. <span data-ttu-id="d75ba-165">Projedeki `StudentID`içeren tüm dosyaları bulun.</span><span class="sxs-lookup"><span data-stu-id="d75ba-165">Find all the files in the project that contain `StudentID`.</span></span>
7. <span data-ttu-id="d75ba-166">Her bir dosya için bir satıra çift tıklayarak *geçişler* klasöründeki &lt;zaman damgası&gt; *\_\*. cs* geçiş dosyaları ***dışında*** her bir dosyayı açın.</span><span class="sxs-lookup"><span data-stu-id="d75ba-166">Open each file in the **Find Results** window ***except*** the &lt;time-stamp&gt;*\_\*.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
8. <span data-ttu-id="d75ba-167">**Dosyaları değiştir** iletişim kutusunu açın ve **açık belgelerin tümünde** **görünümü** değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d75ba-167">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
9. <span data-ttu-id="d75ba-168">Tüm `StudentID` `PersonID`olacak şekilde değiştirmek için **dosyaları değiştir** iletişim kutusunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="d75ba-168">Use the **Replace in Files** dialog to change all `StudentID` to `PersonID`.</span></span>   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
10. <span data-ttu-id="d75ba-169">Projeyi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d75ba-169">Build the project.</span></span>

<span data-ttu-id="d75ba-170">(Bunun, birincil anahtarları adlandırırken `classnameID` deseninin bir *dezavantajı* olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d75ba-170">(Note that this demonstrates a *disadvantage* of the `classnameID` pattern for naming primary keys.</span></span> <span data-ttu-id="d75ba-171">Sınıf adını önek olmadan PRIMARY Keys ID olarak adlandırdıysanız, şu anda *yeniden adlandırma* gerekmez.)</span><span class="sxs-lookup"><span data-stu-id="d75ba-171">If you had named primary keys ID without prefixing the class name, *no* renaming would be necessary now.)</span></span>

## <a name="create-and-update-a-migrations-file"></a><span data-ttu-id="d75ba-172">Geçiş dosyası oluşturma ve güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="d75ba-172">Create and Update a Migrations File</span></span>

<span data-ttu-id="d75ba-173">Paket Yöneticisi konsolunda (PMC), aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="d75ba-173">In the Package Manager Console (PMC), enter the following command:</span></span>

`Add-Migration Inheritance`

<span data-ttu-id="d75ba-174">PMC 'de `Update-Database` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d75ba-174">Run the `Update-Database` command in the PMC.</span></span> <span data-ttu-id="d75ba-175">Bu noktada, geçiş işlemi nasıl işleneceğini bilmez.</span><span class="sxs-lookup"><span data-stu-id="d75ba-175">The command will fail at this point because we have existing data that migrations doesn't know how to handle.</span></span> <span data-ttu-id="d75ba-176">Şu hatayı alırsınız:</span><span class="sxs-lookup"><span data-stu-id="d75ba-176">You get the following error:</span></span>

<span data-ttu-id="d75ba-177">*ALTER TABLE ifadesi, "FK\_dbo yabancı anahtar kısıtlaması ile çakışıyor. Departman\_dbo. Kişi\_kişisimliği ". "ContosoUniversity" veritabanında, "dbo" tablosunda çakışma oluştu. Kişi ", sütun ' PersonID '.*</span><span class="sxs-lookup"><span data-stu-id="d75ba-177">*The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK\_dbo.Department\_dbo.Person\_PersonID". The conflict occurred in database "ContosoUniversity", table "dbo.Person", column 'PersonID'.*</span></span>

<span data-ttu-id="d75ba-178">*Geçişleri\&lt; timestamp&gt;\_Inheritance.cs* açın ve `Up` yöntemini aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="d75ba-178">Open *Migrations\&lt;timestamp&gt;\_Inheritance.cs* and replace the `Up` method with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=25,29-40)]

<span data-ttu-id="d75ba-179">`update-database` komutunu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d75ba-179">Run the `update-database` command again.</span></span>

> [!NOTE]
> <span data-ttu-id="d75ba-180">Verileri geçirirken ve şema değişiklikleri yaparken başka hatalar almak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="d75ba-180">It's possible to get other errors when migrating data and making schema changes.</span></span> <span data-ttu-id="d75ba-181">Çözümleyemez geçiş hataları alırsanız, *Web. config* dosyasındaki bağlantı dizesini değiştirerek veya veritabanını silerek öğreticiye devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d75ba-181">If you get migration errors you can't resolve, you can continue with the tutorial by changing the connection string in the *Web.config* file or deleting the database.</span></span> <span data-ttu-id="d75ba-182">En basit yaklaşım, *Web. config* dosyasındaki veritabanını yeniden adlandırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d75ba-182">The simplest approach is to rename the database in the *Web.config* file.</span></span> <span data-ttu-id="d75ba-183">Örneğin, aşağıdaki örnekte gösterildiği gibi, veritabanı adını\_test olarak değiştirin:</span><span class="sxs-lookup"><span data-stu-id="d75ba-183">For example, change the database name to CU\_test as shown in the following example:</span></span>
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.xml?highlight=1-2)]
> 
> <span data-ttu-id="d75ba-184">Yeni bir veritabanı ile geçirilecek veri yoktur ve `update-database` komutunun hatasız tamamlanabilmesi çok daha yüksektir.</span><span class="sxs-lookup"><span data-stu-id="d75ba-184">With a new database, there is no data to migrate, and the `update-database` command is much more likely to complete without errors.</span></span> <span data-ttu-id="d75ba-185">Veritabanının nasıl silineceği hakkında yönergeler için bkz. [Visual Studio 'dan bir veritabanını bırakma 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span><span class="sxs-lookup"><span data-stu-id="d75ba-185">For instructions on how to delete the database, see [How to Drop a Database from Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span></span> <span data-ttu-id="d75ba-186">Öğreticiye devam etmek için bu yaklaşımla karşılaşırsanız, Bu öğreticinin sonundaki dağıtım adımını atlayın, çünkü dağıtılan site, geçişleri otomatik olarak çalıştırırken aynı hatayı alır.</span><span class="sxs-lookup"><span data-stu-id="d75ba-186">If you take this approach in order to continue with the tutorial, skip the deployment step at the end of this tutorial, since the deployed site would get the same error when it runs migrations automatically.</span></span> <span data-ttu-id="d75ba-187">Bir geçiş hatasıyla ilgili sorunları gidermek istiyorsanız en iyi kaynak Entity Framework forumlarından veya StackOverflow.com biridir.</span><span class="sxs-lookup"><span data-stu-id="d75ba-187">If you want to troubleshoot a migrations error, the best resource is one of the Entity Framework forums or StackOverflow.com.</span></span>

## <a name="testing"></a><span data-ttu-id="d75ba-188">Sınama</span><span class="sxs-lookup"><span data-stu-id="d75ba-188">Testing</span></span>

<span data-ttu-id="d75ba-189">Siteyi çalıştırın ve çeşitli sayfaları deneyin.</span><span class="sxs-lookup"><span data-stu-id="d75ba-189">Run the site and try various pages.</span></span> <span data-ttu-id="d75ba-190">Her şey, daha önce olduğu gibi çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d75ba-190">Everything works the same as it did before.</span></span>

<span data-ttu-id="d75ba-191">**Sunucu Gezgini** ' de, **SchoolContext** ve ardından **Tablolar**' ı genişletin ve **öğrenci** ve **eğitmen** tablolarının bir **kişi** tablosu ile değiştirildiğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d75ba-191">In **Server Explorer,** expand **SchoolContext** and then **Tables**, and you see that the **Student** and **Instructor** tables have been replaced by a **Person** table.</span></span> <span data-ttu-id="d75ba-192">**Kişi** tablosunu genişletin ve **öğrenci** ve **eğitmen** tablolarında, kullanılan tüm sütunları olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d75ba-192">Expand the **Person** table and you see that it has all of the columns that used to be in the **Student** and **Instructor** tables.</span></span>

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="d75ba-194">Kişi tablosuna sağ tıklayın ve ardından **tablo verilerini göster** ' e tıklayarak ayrıştırıcı sütununu görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="d75ba-194">Right-click the Person table, and then click **Show Table Data** to see the discriminator column.</span></span>

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="d75ba-195">Aşağıdaki diyagramda, yeni okul veritabanının yapısı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="d75ba-195">The following diagram illustrates the structure of the new School database:</span></span>

![School_database_diagram](https://asp.net/media/2578143/Windows-Live-Writer_58f5a93579b2_CC7B_School_database_diagram_6350a801-7199-413f-bbac-4a2009ed19d7.png)

## <a name="summary"></a><span data-ttu-id="d75ba-197">Özet</span><span class="sxs-lookup"><span data-stu-id="d75ba-197">Summary</span></span>

<span data-ttu-id="d75ba-198">`Person`, `Student`ve `Instructor` sınıfları için hiyerarşi başına tablo devralma işlemi artık uygulandı.</span><span class="sxs-lookup"><span data-stu-id="d75ba-198">Table-per-hierarchy inheritance has now been implemented for the `Person`, `Student`, and `Instructor` classes.</span></span> <span data-ttu-id="d75ba-199">Bu ve diğer devralma yapıları hakkında daha fazla bilgi için bkz. morteza, Web günlüğü üzerinde [Devralma eşleme stratejileri](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d75ba-199">For more information about this and other inheritance structures, see [Inheritance Mapping Strategies](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) on Morteza Manavi's blog.</span></span> <span data-ttu-id="d75ba-200">Sonraki öğreticide, depo ve iş deseni birimi uygulamak için bazı yollar görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d75ba-200">In the next tutorial you'll see some ways to implement the repository and unit of work patterns.</span></span>

<span data-ttu-id="d75ba-201">Diğer Entity Framework kaynaklarına bağlantılar [ASP.NET veri erişimi Içerik haritasında](../../../../whitepapers/aspnet-data-access-content-map.md)bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="d75ba-201">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d75ba-202">[Önceki](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [İleri](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="d75ba-202">[Previous](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span></span>
