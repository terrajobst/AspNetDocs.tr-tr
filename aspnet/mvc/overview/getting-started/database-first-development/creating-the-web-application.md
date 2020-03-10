---
uid: mvc/overview/getting-started/database-first-development/creating-the-web-application
title: 'Öğretici: ASP.NET MVC ile EF Database First için Web uygulaması ve veri modelleri oluşturma'
description: Bu öğretici, Web uygulaması oluşturmaya ve veritabanı tablolarınıza göre veri modellerini oluşturmaya odaklanmaktadır.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: bc8f2bd5-ff57-4dcd-8418-a5bd517d8953
msc.legacyurl: /mvc/overview/getting-started/database-first-development/creating-the-web-application
msc.type: authoredcontent
ms.openlocfilehash: 30fd42be5677df6fa6ee0630914098c30d21385b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616272"
---
# <a name="tutorial-create-the-web-application-and-data-models-for-ef-database-first-with-aspnet-mvc"></a><span data-ttu-id="44681-103">Öğretici: ASP.NET MVC ile EF Database First için Web uygulaması ve veri modelleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="44681-103">Tutorial: Create the Web Application and Data Models for EF Database First with ASP.NET MVC</span></span>

 <span data-ttu-id="44681-104">MVC, Entity Framework ve ASP.NET Scafkatı kullanarak var olan bir veritabanına arabirim sağlayan bir Web uygulaması oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44681-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="44681-105">Bu öğretici serisinde, kullanıcıların bir veritabanı tablosunda yer alan verileri görüntülemesini, düzenlemesini, oluşturmasını ve silmesini sağlayan nasıl otomatik olarak kod üretileyeceğiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="44681-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="44681-106">Oluşturulan kod, veritabanı tablosundaki sütunlara karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="44681-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="44681-107">Bu öğretici, Web uygulaması oluşturmaya ve veritabanı tablolarınıza göre veri modellerini oluşturmaya odaklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="44681-107">This tutorial focuses on creating the web application, and generating the data models based on your database tables.</span></span>

<span data-ttu-id="44681-108">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="44681-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="44681-109">ASP.NET web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="44681-109">Create an ASP.NET web app</span></span>
> * <span data-ttu-id="44681-110">Modelleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="44681-110">Generate the models</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44681-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="44681-111">Prerequisites</span></span>

* [<span data-ttu-id="44681-112">MVC 5 kullanarak Entity Framework 6 Database First kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="44681-112">Getting started with Entity Framework 6 Database First using MVC 5</span></span>](setting-up-database.md)

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="44681-113">ASP.NET web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="44681-113">Create an ASP.NET web app</span></span>

<span data-ttu-id="44681-114">Yeni bir çözümde veya veritabanı projesiyle aynı çözümde, Visual Studio 'da yeni bir proje oluşturun ve **ASP.NET Web uygulaması** şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="44681-114">In either a new solution or the same solution as the database project, create a new project in Visual Studio and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="44681-115">Projeyi **Contososite**olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="44681-115">Name the project **ContosoSite**.</span></span>

![proje oluştur](creating-the-web-application/_static/image1.png)

<span data-ttu-id="44681-117">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="44681-117">Click **OK**.</span></span>

<span data-ttu-id="44681-118">Yeni ASP.NET projesi penceresinde **MVC** şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="44681-118">In the New ASP.NET Project window, select the **MVC** template.</span></span> <span data-ttu-id="44681-119">Uygulamayı daha sonra buluta dağıtacağından, şimdi için **bulut seçeneğinde Konağı** temizleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44681-119">You can clear the **Host in the cloud** option for now because you will deploy the application to the cloud later.</span></span> <span data-ttu-id="44681-120">Uygulamayı oluşturmak için **Tamam** ' ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="44681-120">Click **OK** to create the application.</span></span>

<span data-ttu-id="44681-121">Proje varsayılan dosya ve klasörlerle oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="44681-121">The project is created with the default files and folders.</span></span>

<span data-ttu-id="44681-122">Bu öğreticide Entity Framework 6 kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="44681-122">In this tutorial, you will use Entity Framework 6.</span></span> <span data-ttu-id="44681-123">NuGet Paketlerini Yönet penceresi aracılığıyla projenizdeki Entity Framework sürümünü bir kez daha kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44681-123">You can double-check the version of Entity Framework in your project through the Manage NuGet Packages window.</span></span> <span data-ttu-id="44681-124">Gerekirse, Entity Framework sürümünüzü güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="44681-124">If necessary, update your version of Entity Framework.</span></span>

![sürümü göster](creating-the-web-application/_static/image3.png)

## <a name="generate-the-models"></a><span data-ttu-id="44681-126">Modelleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="44681-126">Generate the models</span></span>

<span data-ttu-id="44681-127">Artık veritabanı tablolarından Entity Framework modeller oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="44681-127">You will now create Entity Framework models from the database tables.</span></span> <span data-ttu-id="44681-128">Bu modeller, verilerle çalışmak için kullanacağınız sınıflardır.</span><span class="sxs-lookup"><span data-stu-id="44681-128">These models are classes that you will use to work with the data.</span></span> <span data-ttu-id="44681-129">Her model veritabanındaki bir tabloyu yansıtır ve tablodaki sütunlara karşılık gelen özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="44681-129">Each model mirrors a table in the database and contains properties that correspond to the columns in the table.</span></span>

<span data-ttu-id="44681-130">**Modeller** klasörüne sağ tıklayın ve **Ekle** ' ye ve **Yeni öğe**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="44681-130">Right-click the **Models** folder, and select **Add** and **New Item**.</span></span>

<span data-ttu-id="44681-131">Yeni öğe Ekle penceresinde, sol bölmedeki **veriler** ' i seçin ve orta bölmedeki seçeneklerden **ADO.net varlık veri modeli** .</span><span class="sxs-lookup"><span data-stu-id="44681-131">In the Add New Item window, select **Data** in the left pane and **ADO.NET Entity Data Model** from the options in the center pane.</span></span> <span data-ttu-id="44681-132">Yeni model dosyası **Contosomodel**olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="44681-132">Name the new model file **ContosoModel**.</span></span>

<span data-ttu-id="44681-133">**Ekle**'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="44681-133">Click **Add**.</span></span>

<span data-ttu-id="44681-134">Varlık Veri Modeli sihirbazında, **veritabanından EF Designer**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="44681-134">In the Entity Data Model Wizard, select **EF Designer from database**.</span></span>

<span data-ttu-id="44681-135">**İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="44681-135">Click **Next**.</span></span>

<span data-ttu-id="44681-136">Geliştirme ortamınızda tanımlanmış veritabanı bağlantılarınız varsa, bu bağlantılardan birini önceden seçmiş olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44681-136">If you have database connections defined within your development environment, you may see one of these connections pre-selected.</span></span> <span data-ttu-id="44681-137">Ancak, Bu öğreticinin ilk bölümünde oluşturduğunuz veritabanına yeni bir bağlantı oluşturmak istersiniz.</span><span class="sxs-lookup"><span data-stu-id="44681-137">However, you want to create a new connection to the database you created in the first part of this tutorial.</span></span> <span data-ttu-id="44681-138">**Yeni bağlantı** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="44681-138">Click the **New Connection** button.</span></span>

<span data-ttu-id="44681-139">Bağlantı Özellikler penceresi, veritabanınızın oluşturulduğu yerel sunucunun adını girin (Bu örnekte **(LocalDB) \ProjectsV13**).</span><span class="sxs-lookup"><span data-stu-id="44681-139">In the Connection Properties window, provide the name of the local server where your database was created (in this case **(localdb)\ProjectsV13**).</span></span> <span data-ttu-id="44681-140">Sunucu adını sağladıktan sonra, kullanılabilir veritabanlarından Contosoüniversıdata ' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="44681-140">After providing the server name, select the ContosoUniversityData from the available databases.</span></span>

![bağlantı özelliklerini ayarlama](creating-the-web-application/_static/image8.png)

<span data-ttu-id="44681-142">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="44681-142">Click **OK**.</span></span>

<span data-ttu-id="44681-143">Doğru bağlantı özellikleri artık gösteriliyor.</span><span class="sxs-lookup"><span data-stu-id="44681-143">The correct connection properties are now displayed.</span></span> <span data-ttu-id="44681-144">Web. config dosyasında bağlantı için varsayılan adı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44681-144">You can use the default name for connection in the Web.Config file.</span></span>

<span data-ttu-id="44681-145">**İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="44681-145">Click **Next**.</span></span>

<span data-ttu-id="44681-146">En son Entity Framework sürümünü seçin.</span><span class="sxs-lookup"><span data-stu-id="44681-146">Select the latest version of Entity Framework.</span></span>

<span data-ttu-id="44681-147">**İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="44681-147">Click **Next**.</span></span>

<span data-ttu-id="44681-148">Üç tabloya yönelik modeller oluşturmak için **Tablolar** ' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="44681-148">Select **Tables** to generate models for all three tables.</span></span>

<span data-ttu-id="44681-149">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="44681-149">Click **Finish**.</span></span>

<span data-ttu-id="44681-150">Bir güvenlik uyarısı alırsanız, şablonu çalıştırmaya devam etmek için **Tamam** ' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="44681-150">If you receive a security warning, select **OK** to continue running the template.</span></span>

<span data-ttu-id="44681-151">Modeller veritabanı tablolarından oluşturulur ve tablolar arasındaki özellikleri ve ilişkileri gösteren bir diyagram görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="44681-151">The models are generated from the database tables, and a diagram is displayed that shows the properties and relationships between the tables.</span></span>

![Model diyagramı](creating-the-web-application/_static/image11.png)

<span data-ttu-id="44681-153">Modeller klasörü artık veritabanından oluşturulan modellerle ilgili birçok yeni dosya içerir.</span><span class="sxs-lookup"><span data-stu-id="44681-153">The Models folder now includes many new files related to the models that were generated from the database.</span></span>

<span data-ttu-id="44681-154">**ContosoModel.Context.cs** dosyası **DbContext** sınıfından türetilen bir sınıf içerir ve bir veritabanı tablosuna karşılık gelen her model sınıfı için bir özellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="44681-154">The **ContosoModel.Context.cs** file contains a class that derives from the **DbContext** class, and provides a property for each model class that corresponds to a database table.</span></span> <span data-ttu-id="44681-155">**Course.cs**, **enrollment.cs**ve **Student.cs** dosyaları, veritabanları tablolarını temsil eden model sınıflarını içerir.</span><span class="sxs-lookup"><span data-stu-id="44681-155">The **Course.cs**, **Enrollment.cs**, and **Student.cs** files contain the model classes that represent the databases tables.</span></span> <span data-ttu-id="44681-156">Yapı iskelesi ile çalışırken hem bağlam sınıfını hem de model sınıflarını kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="44681-156">You will use both the context class and the model classes when working with scaffolding.</span></span>

<span data-ttu-id="44681-157">Bu öğreticiye devam etmeden önce projeyi derleyin.</span><span class="sxs-lookup"><span data-stu-id="44681-157">Before proceeding with this tutorial, build the project.</span></span> <span data-ttu-id="44681-158">Sonraki bölümde, veri modellerini temel alan kod oluşturacaksınız, ancak bu bölüm, proje oluşturulmadığında çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="44681-158">In the next section, you will generate code based on the data models, but that section will not work if the project has not been built.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44681-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="44681-159">Next steps</span></span>

<span data-ttu-id="44681-160">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="44681-160">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="44681-161">Bir ASP.NET Web uygulaması oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="44681-161">Created an ASP.NET web app</span></span>
> * <span data-ttu-id="44681-162">Modeller üretildi</span><span class="sxs-lookup"><span data-stu-id="44681-162">Generated the models</span></span>

<span data-ttu-id="44681-163">Veri modellerini temel alan oluşturma kodu oluşturma hakkında bilgi edinmek için sonraki öğreticiye ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="44681-163">Advance to the next tutorial to learn how to create generate code based on the data models.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="44681-164">Görünümler üretiliyor</span><span class="sxs-lookup"><span data-stu-id="44681-164">Generating views</span></span>](generating-views.md)
