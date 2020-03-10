---
uid: mvc/overview/getting-started/database-first-development/generating-views
title: 'Öğretici: ASP.NET MVC uygulamasıyla EF Database First için görünümler oluşturma'
description: Bu öğretici, denetleyicileri ve görünümleri oluşturmak için ASP.NET Scafkatlarını kullanmaya odaklanır.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 669367cf-8e30-4eb6-821d-10a7d9bb906c
msc.legacyurl: /mvc/overview/getting-started/database-first-development/generating-views
msc.type: authoredcontent
ms.openlocfilehash: e71e13e22d8a72e1699cfc70d4d93af603edba5b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616209"
---
# <a name="tutorial-generate-views-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="a9367-103">Öğretici: ASP.NET MVC uygulamasıyla EF Database First için görünümler oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9367-103">Tutorial: Generate views for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="a9367-104">MVC, Entity Framework ve ASP.NET Scafkatı kullanarak var olan bir veritabanına arabirim sağlayan bir Web uygulaması oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9367-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="a9367-105">Bu öğretici serisinde, kullanıcıların bir veritabanı tablosunda yer alan verileri görüntülemesini, düzenlemesini, oluşturmasını ve silmesini sağlayan nasıl otomatik olarak kod üretileyeceğiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a9367-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="a9367-106">Oluşturulan kod, veritabanı tablosundaki sütunlara karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="a9367-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="a9367-107">Bu öğretici, denetleyicileri ve görünümleri oluşturmak için ASP.NET Scafkatlarını kullanmaya odaklanır.</span><span class="sxs-lookup"><span data-stu-id="a9367-107">This tutorial focuses on using ASP.NET Scaffolding to generate the controllers and views.</span></span>

<span data-ttu-id="a9367-108">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="a9367-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a9367-109">Yapı iskelesi Ekle</span><span class="sxs-lookup"><span data-stu-id="a9367-109">Add scaffold</span></span>
> * <span data-ttu-id="a9367-110">Yeni görünümlere bağlantı ekleme</span><span class="sxs-lookup"><span data-stu-id="a9367-110">Add links to new views</span></span>
> * <span data-ttu-id="a9367-111">Öğrenci görünümlerini görüntüle</span><span class="sxs-lookup"><span data-stu-id="a9367-111">Display student views</span></span>
> * <span data-ttu-id="a9367-112">Kayıt görünümlerini görüntüle</span><span class="sxs-lookup"><span data-stu-id="a9367-112">Display enrollment views</span></span>

## <a name="prerequisite"></a><span data-ttu-id="a9367-113">Önkoşul</span><span class="sxs-lookup"><span data-stu-id="a9367-113">Prerequisite</span></span>

* [<span data-ttu-id="a9367-114">Web uygulaması ve veri modellerini oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9367-114">Create the web application and data models</span></span>](creating-the-web-application.md)

## <a name="add-scaffold"></a><span data-ttu-id="a9367-115">Yapı iskelesi Ekle</span><span class="sxs-lookup"><span data-stu-id="a9367-115">Add scaffold</span></span>

<span data-ttu-id="a9367-116">Model sınıfları için standart veri işlemleri sağlayacak kod oluşturmaya hazırsınızdır.</span><span class="sxs-lookup"><span data-stu-id="a9367-116">You are ready to generate code that will provide standard data operations for the model classes.</span></span> <span data-ttu-id="a9367-117">Bir yapı iskelesi öğesi ekleyerek kodu eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="a9367-117">You add the code by adding a scaffold item.</span></span> <span data-ttu-id="a9367-118">Ekleyebileceğiniz yapı iskelesi türü için birçok seçenek vardır; Bu öğreticide, scafkatlama, önceki bölümde oluşturduğunuz öğrenci ve kayıt modellerine karşılık gelen bir denetleyiciyi ve görünümleri içerir.</span><span class="sxs-lookup"><span data-stu-id="a9367-118">There are many options for the type of scaffolding you can add; in this tutorial, the scaffold will include a controller and views that correspond to the Student and Enrollment models you created in the previous section.</span></span>

<span data-ttu-id="a9367-119">Projenizde tutarlılığı sürdürmek için, yeni denetleyiciyi var olan **denetleyiciler** klasörüne ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="a9367-119">To maintain consistency in your project, you will add the new controller to the existing **Controllers** folder.</span></span> <span data-ttu-id="a9367-120">**Denetleyiciler** klasörüne sağ tıklayın ve > **yeni yapı Iskelesi öğesi** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="a9367-120">Right-click the **Controllers** folder, and select **Add** > **New Scaffolded Item**.</span></span>

<span data-ttu-id="a9367-121">Entity Framework seçeneğini **kullanarak, görünümler Içeren MVC 5 denetleyiciyi** seçin.</span><span class="sxs-lookup"><span data-stu-id="a9367-121">Select the **MVC 5 Controller with views, using Entity Framework** option.</span></span> <span data-ttu-id="a9367-122">Bu seçenek, modelinizdeki verileri güncelleştirme, silme, oluşturma ve görüntülemeye yönelik denetleyiciyi ve görünümleri oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="a9367-122">This option will generate the controller and views for updating, deleting, creating and displaying the data in your model.</span></span>

![MVC denetleyicisi Ekle](generating-views/_static/image2.png)

<span data-ttu-id="a9367-124">Model sınıfı için **öğrenci (ContosoSite. modeller)** öğesini seçin ve bağlam sınıfı Için **Contosoüniversıtydataentities (Contososite. modeller)** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="a9367-124">Select **Student (ContosoSite.Models)** for the model class and select the **ContosoUniversityDataEntities (ContosoSite.Models)** for the context class.</span></span> <span data-ttu-id="a9367-125">Denetleyici adını **Studentscontroller**olarak tutun.</span><span class="sxs-lookup"><span data-stu-id="a9367-125">Keep the controller name as **StudentsController**.</span></span>

<span data-ttu-id="a9367-126">**Ekle**'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a9367-126">Click **Add**.</span></span>

<span data-ttu-id="a9367-127">Bir hata alırsanız, bunun nedeni, önceki bölümde projeyi derlemeniz olabilir.</span><span class="sxs-lookup"><span data-stu-id="a9367-127">If you receive an error, it may be because you did not build the project in the previous section.</span></span> <span data-ttu-id="a9367-128">Bu durumda projeyi oluşturmayı deneyin ve ardından yapı iskelesi öğesini yeniden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a9367-128">If so, try building the project, and then add the scaffolded item again.</span></span>

<span data-ttu-id="a9367-129">Kod oluşturma işlemi tamamlandıktan sonra, projenizin **denetleyicileri** ve **görünümleri** > **öğrenciler** klasörlerinde yeni bir denetleyici ve görünümler görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="a9367-129">After the code generation process is complete, you will see a new controller and views in your project's **Controllers** and **Views** > **Students** folders.</span></span>

<span data-ttu-id="a9367-130">Aynı adımları yeniden gerçekleştirin, ancak **kayıt** sınıfı için bir yapı iskelesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a9367-130">Perform the same steps again, but add a scaffold for the **Enrollment** class.</span></span> <span data-ttu-id="a9367-131">İşiniz bittiğinde, bir **EnrollmentsController.cs** dosyanız ve oluşturma, silme, ayrıntılar, düzenleme ve dizin görünümleri ile **kayıtlar adlı** **Görünümler** altında bir klasör vardır.</span><span class="sxs-lookup"><span data-stu-id="a9367-131">When finished, you have an **EnrollmentsController.cs** file, and a folder under **Views** named **Enrollments** with the Create, Delete, Details, Edit and Index views.</span></span>

## <a name="add-links-to-new-views"></a><span data-ttu-id="a9367-132">Yeni görünümlere bağlantı ekleme</span><span class="sxs-lookup"><span data-stu-id="a9367-132">Add links to new views</span></span>

<span data-ttu-id="a9367-133">Yeni görünümleriniz üzerinde gezinmenize daha kolay hale getirmek için öğrenciler ve kayıtlar için Dizin görünümlerine birkaç köprü ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9367-133">To make it easier for you to navigate to your new views, you can add a couple of hyperlinks to the Index views for students and enrollments.</span></span> <span data-ttu-id="a9367-134">Dosyayı, sitenizin ana sayfası olan > **home** > *Index. cshtml* **' de açın** .</span><span class="sxs-lookup"><span data-stu-id="a9367-134">Open the file at **Views** > **Home** > *Index.cshtml*, which is the home page for your site.</span></span> <span data-ttu-id="a9367-135">Aşağıdaki kodu jumbotron altına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a9367-135">Add the following code below the jumbotron.</span></span>

[!code-cshtml[Main](generating-views/samples/sample1.cshtml)]

<span data-ttu-id="a9367-136">ActionLink yöntemi için ilk parametre, bağlantıda görüntülenecek metindir.</span><span class="sxs-lookup"><span data-stu-id="a9367-136">For the ActionLink method, the first parameter is the text to display in the link.</span></span> <span data-ttu-id="a9367-137">İkinci parametre eylemdir ve üçüncü parametre denetleyicinin adıdır.</span><span class="sxs-lookup"><span data-stu-id="a9367-137">The second parameter is the action and the third parameter is the name of the controller.</span></span> <span data-ttu-id="a9367-138">Örneğin, ilk bağlantı, StudentsController içindeki dizin eylemine işaret eder.</span><span class="sxs-lookup"><span data-stu-id="a9367-138">For example, the first link points to the Index action in StudentsController.</span></span> <span data-ttu-id="a9367-139">Gerçek köprü bu değerlerden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a9367-139">The actual hyperlink is constructed from these values.</span></span> <span data-ttu-id="a9367-140">İlk bağlantı, kullanıcıları **Görünümler/öğrenciler** klasörü içindeki **Index. cshtml** dosyasına alır.</span><span class="sxs-lookup"><span data-stu-id="a9367-140">The first link ultimately takes users to the **Index.cshtml** file within the **Views/Students** folder.</span></span>

## <a name="display-student-views"></a><span data-ttu-id="a9367-141">Öğrenci görünümlerini görüntüle</span><span class="sxs-lookup"><span data-stu-id="a9367-141">Display student views</span></span>

<span data-ttu-id="a9367-142">Projenize eklenen kodun öğrencilerinin bir listesini görüntüleyeceğini ve kullanıcıların veritabanındaki öğrenci kayıtlarını düzenlemesini, oluşturmasını veya silmesini sağlayan bir kod görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="a9367-142">You will verify that the code added to your project correctly displays a list of the students, and enables users to edit, create, or delete the student records in the database.</span></span>

<span data-ttu-id="a9367-143">**Görünümler** > **giriş** > *Index. cshtml* dosyasına sağ tıklayın ve **Tarayıcıda görüntüle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="a9367-143">Right-click the **Views** > **Home** > *Index.cshtml* file, and select **View in Browser**.</span></span> <span data-ttu-id="a9367-144">Uygulama giriş sayfasında, **öğrenci listesi**' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="a9367-144">On the application home page, select **List of students**.</span></span>

![](generating-views/_static/image6.png)

<span data-ttu-id="a9367-145">**Dizin** sayfasında, bu verileri değiştirmek için öğrenciler ve bağlantılar listesine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a9367-145">On the **Index** page, notice the list of the students and links to modify this data.</span></span> <span data-ttu-id="a9367-146">**Yeni oluştur** bağlantısını seçin ve yeni bir öğrenci için bazı değerler sağlayın.</span><span class="sxs-lookup"><span data-stu-id="a9367-146">Select the **Create New** link and provide some values for a new student.</span></span> <span data-ttu-id="a9367-147">**Oluştur**' a tıklayın ve yeni öğrencinin listenize eklendiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a9367-147">Click **Create**, and notice the new student is added to your list.</span></span>

<span data-ttu-id="a9367-148">**Dizin** sayfasında, **Düzenle** bağlantısını seçin ve bir öğrenci için bazı değerleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a9367-148">Back on the **Index** page, select the **Edit** link, and change some of the values for a student.</span></span> <span data-ttu-id="a9367-149">**Kaydet**' e tıklayın ve Öğrenci kaydının değiştirildiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a9367-149">Click **Save**, and notice the student record has been changed.</span></span>

<span data-ttu-id="a9367-150">Son olarak, **Sil** bağlantısını seçin ve **Sil** düğmesine tıklayarak kaydı silmek istediğinizi onaylayın.</span><span class="sxs-lookup"><span data-stu-id="a9367-150">Finally, select the **Delete** link and confirm that you want to delete the record by clicking the **Delete** button.</span></span>

<span data-ttu-id="a9367-151">Herhangi bir kod yazmadan, öğrenci tablosundaki veriler üzerinde yaygın işlemler gerçekleştiren görünümler eklediniz.</span><span class="sxs-lookup"><span data-stu-id="a9367-151">Without writing any code, you have added views that perform common operations on the data in the Student table.</span></span>

<span data-ttu-id="a9367-152">Bir alanın metin etiketinin, Web sayfasında görüntülenmesini istediğiniz zaman olmayan veritabanı özelliğine ( **LastName**gibi) göre olduğunu fark etmiş olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9367-152">You may have noticed that the text label for a field is based on the database property (such as **LastName**) which is not necessarily what you want to display on the web page.</span></span> <span data-ttu-id="a9367-153">Örneğin, etiketi **Soyadı**olacak şekilde tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9367-153">For example, you may prefer the label to be **Last Name**.</span></span> <span data-ttu-id="a9367-154">Bu görüntü sorunu öğreticide daha sonra düzeltilecektir.</span><span class="sxs-lookup"><span data-stu-id="a9367-154">You will fix this display issue later in the tutorial.</span></span>

## <a name="display-enrollment-views"></a><span data-ttu-id="a9367-155">Kayıt görünümlerini görüntüle</span><span class="sxs-lookup"><span data-stu-id="a9367-155">Display enrollment views</span></span>

<span data-ttu-id="a9367-156">Veritabanınız, öğrenci ve kayıt tabloları arasında bire çok bir ilişki ve kurs ve kayıt tabloları arasında bire çok ilişki içerir.</span><span class="sxs-lookup"><span data-stu-id="a9367-156">Your database includes a one-to-many relationship between the Student and Enrollment tables, and a one-to-many relationship between the Course and Enrollment tables.</span></span> <span data-ttu-id="a9367-157">Kayıt görünümleri bu ilişkileri doğru bir şekilde işler.</span><span class="sxs-lookup"><span data-stu-id="a9367-157">The views for Enrollment correctly handle these relationships.</span></span> <span data-ttu-id="a9367-158">Sitenizin ana sayfasına gidin ve kayıt **listesi** bağlantısı ' nı ve ardından **Yeni bağlantı oluştur** ' u seçin.</span><span class="sxs-lookup"><span data-stu-id="a9367-158">Navigate to the home page for your site and select the **List of enrollments** link and then the **Create New** link.</span></span>

<span data-ttu-id="a9367-159">Görünüm yeni bir kayıt kaydı oluşturmak için bir form görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a9367-159">The view displays a form for creating a new enrollment record.</span></span> <span data-ttu-id="a9367-160">Özellikle, formun bir **CourseID** açılır listesi ve bir **studentid** açılır listesi içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a9367-160">In particular, notice that the form contains a **CourseID** drop-down list and a **StudentID** drop-down list.</span></span> <span data-ttu-id="a9367-161">Her ikisi de ilgili tablolardaki değerlerle doldurulur.</span><span class="sxs-lookup"><span data-stu-id="a9367-161">Both are populated with values from the related tables.</span></span>

<span data-ttu-id="a9367-162">Ayrıca, girilen değerlerin doğrulanması alanın veri türüne göre otomatik olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="a9367-162">Furthermore, validation of the provided values is automatically applied based on the data type of the field.</span></span> <span data-ttu-id="a9367-163">**Sınıf** için bir sayı gerekir, bu nedenle uyumsuz bir değer sağlamaya çalışırsanız bir hata iletisi görüntülenir: *alan sınıfı bir sayı olmalıdır.*</span><span class="sxs-lookup"><span data-stu-id="a9367-163">**Grade** requires a number, so an error message is displayed if you try to provide an incompatible value: *The field Grade must be a number.*</span></span>

<span data-ttu-id="a9367-164">Otomatik olarak oluşturulan görünümlerin, kullanıcıların veritabanındaki verilerle çalışmasını olanaklı olduğunu doğruladınız.</span><span class="sxs-lookup"><span data-stu-id="a9367-164">You have verified that the automatically-generated views enable users to work with the data in the database.</span></span> <span data-ttu-id="a9367-165">Bu serinin sonraki öğreticide, veritabanını güncelleştirecek ve ilgili değişiklikleri Web uygulamasında yapacaksınız.</span><span class="sxs-lookup"><span data-stu-id="a9367-165">In the next tutorial in this series, you will update the database and make the corresponding changes in the web application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9367-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a9367-166">Next steps</span></span>

<span data-ttu-id="a9367-167">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="a9367-167">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a9367-168">Yapı iskelesi eklendi</span><span class="sxs-lookup"><span data-stu-id="a9367-168">Added scaffold</span></span>
> * <span data-ttu-id="a9367-169">Yeni görünümlere bağlantılar eklendi</span><span class="sxs-lookup"><span data-stu-id="a9367-169">Added links to new views</span></span>
> * <span data-ttu-id="a9367-170">Görünen öğrenci görünümleri</span><span class="sxs-lookup"><span data-stu-id="a9367-170">Displayed student views</span></span>
> * <span data-ttu-id="a9367-171">Görüntülenmiş kayıt görünümleri</span><span class="sxs-lookup"><span data-stu-id="a9367-171">Displayed enrollment views</span></span>

<span data-ttu-id="a9367-172">Veritabanını değiştirme hakkında bilgi edinmek için sonraki öğreticiye ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="a9367-172">Advance to the next tutorial to learn how to change the database.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="a9367-173">Veritabanını değiştirme</span><span class="sxs-lookup"><span data-stu-id="a9367-173">Change the database</span></span>](changing-the-database.md)