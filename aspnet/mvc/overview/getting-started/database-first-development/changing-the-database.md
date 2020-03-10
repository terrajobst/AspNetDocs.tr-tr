---
uid: mvc/overview/getting-started/database-first-development/changing-the-database
title: 'Öğretici: EF Database First için veritabanını ASP.NET MVC uygulamasıyla değiştirme'
description: Bu öğretici, veritabanı yapısına bir güncelleştirme yapma ve bu değişikliği Web uygulaması genelinde yayma konusunda odaklanır.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: cfd5c083-a319-482e-8f25-5b38caa93954
msc.legacyurl: /mvc/overview/getting-started/database-first-development/changing-the-database
msc.type: authoredcontent
ms.openlocfilehash: 52cad1120908cf0d4f85770f8e2690f9415c5f56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616265"
---
# <a name="tutorial-change-the-database-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="2c80f-103">Öğretici: EF Database First için veritabanını ASP.NET MVC uygulamasıyla değiştirme</span><span class="sxs-lookup"><span data-stu-id="2c80f-103">Tutorial: Change the database for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="2c80f-104">MVC, Entity Framework ve ASP.NET Scafkatı kullanarak var olan bir veritabanına arabirim sağlayan bir Web uygulaması oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c80f-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="2c80f-105">Bu öğretici serisinde, kullanıcıların bir veritabanı tablosunda yer alan verileri görüntülemesini, düzenlemesini, oluşturmasını ve silmesini sağlayan nasıl otomatik olarak kod üretileyeceğiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="2c80f-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="2c80f-106">Oluşturulan kod, veritabanı tablosundaki sütunlara karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="2c80f-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="2c80f-107">Bu öğretici, veritabanı yapısına bir güncelleştirme yapma ve bu değişikliği Web uygulaması genelinde yayma konusunda odaklanır.</span><span class="sxs-lookup"><span data-stu-id="2c80f-107">This tutorial focuses on making an update to the database structure and propagating that change throughout the web application.</span></span>

<span data-ttu-id="2c80f-108">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="2c80f-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2c80f-109">Sütun ekleme</span><span class="sxs-lookup"><span data-stu-id="2c80f-109">Add a column</span></span>
> * <span data-ttu-id="2c80f-110">Özelliği görünümlere ekleyin</span><span class="sxs-lookup"><span data-stu-id="2c80f-110">Add the property to the views</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c80f-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="2c80f-111">Prerequisites</span></span>

* [<span data-ttu-id="2c80f-112">Görünümler üretiliyor</span><span class="sxs-lookup"><span data-stu-id="2c80f-112">Generating views</span></span>](generating-views.md)

## <a name="add-a-column"></a><span data-ttu-id="2c80f-113">Sütun ekleme</span><span class="sxs-lookup"><span data-stu-id="2c80f-113">Add a column</span></span>

<span data-ttu-id="2c80f-114">Veritabanınızdaki bir tablonun yapısını güncelleştirirseniz, yaptığınız değişikliğin veri modeline, görünümlere ve denetleyiciye yayıldığından emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2c80f-114">If you update the structure of a table in your database, you need to ensure that your change is propagated to the data model, views, and controller.</span></span>

<span data-ttu-id="2c80f-115">Bu öğretici için öğrencinin orta adını kaydetmek üzere öğrenci tablosuna yeni bir sütun ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="2c80f-115">For this tutorial, you will add a new column to the Student table to record the middle name of the student.</span></span> <span data-ttu-id="2c80f-116">Bu sütunu eklemek için veritabanı projesini açın ve öğrenci. SQL dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="2c80f-116">To add this column, open the database project, and open the Student.sql file.</span></span> <span data-ttu-id="2c80f-117">Tasarımcı ya da T-SQL kodu aracılığıyla, NVARCHAR (50) olan **MiddleName** adlı bir sütun ekleyın ve null değerlere izin verir.</span><span class="sxs-lookup"><span data-stu-id="2c80f-117">Through either the designer or the T-SQL code, add a column named **MiddleName** that is an NVARCHAR(50) and allows NULL values.</span></span>

<span data-ttu-id="2c80f-118">Veritabanı projenizi (veya F5) başlatarak bu değişikliği yerel veritabanınıza dağıtın.</span><span class="sxs-lookup"><span data-stu-id="2c80f-118">Deploy this change to your local database by starting your database project (or F5).</span></span> <span data-ttu-id="2c80f-119">Yeni alan tabloya eklenir.</span><span class="sxs-lookup"><span data-stu-id="2c80f-119">The new field is added to the table.</span></span> <span data-ttu-id="2c80f-120">SQL Server Nesne Gezgini görmüyorsanız, bölmedeki Yenile düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2c80f-120">If you do not see it in the SQL Server Object Explorer, click the Refresh button in the pane.</span></span>

![Yeni sütun göster](changing-the-database/_static/image2.png)

<span data-ttu-id="2c80f-122">Yeni sütun veritabanı tablosunda var, ancak şu anda veri modeli sınıfında mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="2c80f-122">The new column exists in the database table, but it does not currently exist in the data model class.</span></span> <span data-ttu-id="2c80f-123">Modeli yeni sütununuzu içerecek şekilde güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2c80f-123">You must update the model to include your new column.</span></span> <span data-ttu-id="2c80f-124">**Modeller** klasöründe, model diyagramını göstermek Için **contosomodel. edmx** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="2c80f-124">In the **Models** folder, open the **ContosoModel.edmx** file to display the model diagram.</span></span> <span data-ttu-id="2c80f-125">Öğrenci modelinin MiddleName özelliğini içermediğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="2c80f-125">Notice that the Student model does not contain the MiddleName property.</span></span> <span data-ttu-id="2c80f-126">Tasarım yüzeyinde herhangi bir yere sağ tıklayın ve **modeli veritabanından Güncelleştir**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="2c80f-126">Right-click anywhere on the design surface, and select **Update Model from Database**.</span></span>

<span data-ttu-id="2c80f-127">Güncelleştirme sihirbazında **Yenile** sekmesini seçin ve ardından **tablo** > **dbo** > **öğrenci**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="2c80f-127">In the Update Wizard, select the **Refresh** tab and then select **Tables** > **dbo** > **Student**.</span></span> <span data-ttu-id="2c80f-128">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2c80f-128">Click **Finish**.</span></span>

<span data-ttu-id="2c80f-129">Güncelleştirme işlemi tamamlandıktan sonra, veritabanı diyagramı yeni **MiddleName** özelliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="2c80f-129">After the update process is finished, the database diagram includes the new **MiddleName** property.</span></span> <span data-ttu-id="2c80f-130">**Contosomodel. edmx** dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2c80f-130">Save the **ContosoModel.edmx** file.</span></span> <span data-ttu-id="2c80f-131">Bu dosyayı, **Student.cs** sınıfına yayılacağı yeni özellik için kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2c80f-131">You must save this file for the new property to be propagated to the **Student.cs** class.</span></span> <span data-ttu-id="2c80f-132">Artık veritabanını ve modeli güncelleştirmiş oldunuz.</span><span class="sxs-lookup"><span data-stu-id="2c80f-132">You have now updated the database and the model.</span></span>

<span data-ttu-id="2c80f-133">Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="2c80f-133">Build the solution.</span></span>

## <a name="add-the-property-to-the-views"></a><span data-ttu-id="2c80f-134">Özelliği görünümlere ekleyin</span><span class="sxs-lookup"><span data-stu-id="2c80f-134">Add the property to the views</span></span>

<span data-ttu-id="2c80f-135">Ne yazık ki, görünümler yine de yeni özelliği içermiyor.</span><span class="sxs-lookup"><span data-stu-id="2c80f-135">Unfortunately, the views still do not contain the new property.</span></span> <span data-ttu-id="2c80f-136">Görünümleri güncelleştirmek için iki seçeneğiniz vardır. bir kez daha, öğrenci sınıfı için yapı iskelesi ekleyerek görünümleri yeniden oluşturabilir ya da yeni özelliği mevcut görünümlerinize el ile ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c80f-136">To update the views you have two options - you can either re-generate the views by once again adding scaffolding for the Student class, or you can manually add the new property to your existing views.</span></span> <span data-ttu-id="2c80f-137">Bu öğreticide, otomatik olarak oluşturulan görünümlerde özelleştirilmiş bir değişiklik yapmadığından, yapı iskelesi 'ni yeniden ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="2c80f-137">In this tutorial, you will add the scaffolding again because you have not made any customized changes to the automatically-generated views.</span></span> <span data-ttu-id="2c80f-138">Görünümlerde değişiklikler yaptığınızda ve bu değişiklikleri kaybetmek istemediğinizde özelliği el ile eklemeyi düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c80f-138">You might consider manually adding the property when you have made changes to the views and do not want to lose those changes.</span></span>

<span data-ttu-id="2c80f-139">Görünümlerin yeniden oluşturulduğundan emin olmak için, **Görünümler**altındaki **öğrenciler** klasörünü silin ve **studentscontroller**öğesini silin.</span><span class="sxs-lookup"><span data-stu-id="2c80f-139">To ensure the views are re-created, delete the **Students** folder under **Views**, and delete the **StudentsController**.</span></span> <span data-ttu-id="2c80f-140">Ardından, **denetleyiciler** klasörüne sağ tıklayın ve **öğrenci** modeli için yapı iskelesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2c80f-140">Then, right-click the **Controllers** folder and add scaffolding for the **Student** model.</span></span> <span data-ttu-id="2c80f-141">Yine, denetleyiciyi **Studentscontroller**olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="2c80f-141">Again, name the controller **StudentsController**.</span></span> <span data-ttu-id="2c80f-142">**Add (Ekle)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="2c80f-142">Select **Add**.</span></span>

<span data-ttu-id="2c80f-143">Çözümü yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2c80f-143">Build the solution again.</span></span> <span data-ttu-id="2c80f-144">Görünümler artık MiddleName özelliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="2c80f-144">The views now contain the MiddleName property.</span></span>

![İkinci adı göster](changing-the-database/_static/image5.png)

## <a name="next-steps"></a><span data-ttu-id="2c80f-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2c80f-146">Next steps</span></span>

<span data-ttu-id="2c80f-147">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="2c80f-147">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2c80f-148">Sütun eklendi</span><span class="sxs-lookup"><span data-stu-id="2c80f-148">Added a column</span></span>
> * <span data-ttu-id="2c80f-149">Özellik görünümlere eklendi</span><span class="sxs-lookup"><span data-stu-id="2c80f-149">Added the property to the views</span></span>

<span data-ttu-id="2c80f-150">Bir öğrenci kaydıyla ilgili ayrıntıları göstermek için görünümü özelleştirmeyi öğrenmek üzere sonraki öğreticiye ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="2c80f-150">Advance to the next tutorial to learn how to customize the view for showing details about a student record.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="2c80f-151">Görünümü özelleştirme</span><span class="sxs-lookup"><span data-stu-id="2c80f-151">Customize a view</span></span>](customizing-a-view.md)