---
uid: mvc/overview/getting-started/database-first-development/enhancing-data-validation
title: 'Öğretici: Veri doğrulama EF veritabanı ilk için ASP.NET MVC uygulaması ile geliştirin'
description: Bu öğreticide, doğrulama gereksinimlerini belirtin ve biçimlendirme görüntülemek için veri modeline veri ek açıklamaları ekleme odaklanır.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 0ed5e67a-34c0-4b57-84a6-802b0fb3cd00
msc.legacyurl: /mvc/overview/getting-started/database-first-development/enhancing-data-validation
msc.type: authoredcontent
ms.openlocfilehash: 897cd7c6a40445e2a4abede50d81e101372d3233
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57070599"
---
# <a name="tutorial-enhance-data-validation-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="a03f4-103">Öğretici: Veri doğrulama EF veritabanı ilk için ASP.NET MVC uygulaması ile geliştirin</span><span class="sxs-lookup"><span data-stu-id="a03f4-103">Tutorial: Enhance data validation for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="a03f4-104">MVC, Entity Framework ve ASP.NET iskeleti oluşturma kullanarak mevcut bir veritabanı için bir arabirim sunan bir web uygulaması oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a03f4-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="a03f4-105">Bu öğretici serisinde, otomatik olarak kullanıcıların görüntüleme, düzenleme, oluşturma olanak sağlayan bir kod oluşturmak ve bir veritabanı tablosu, bulunan verileri silmek gösterilir.</span><span class="sxs-lookup"><span data-stu-id="a03f4-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="a03f4-106">Oluşturulan kod, veritabanı tablosundaki sütunlara karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="a03f4-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="a03f4-107">Bu öğreticide, doğrulama gereksinimlerini belirtin ve biçimlendirme görüntülemek için veri modeline veri ek açıklamaları ekleme odaklanır.</span><span class="sxs-lookup"><span data-stu-id="a03f4-107">This tutorial focuses on adding data annotations to the data model to specify validation requirements and display formatting.</span></span> <span data-ttu-id="a03f4-108">Bu temel kullanıcıların yorumlar bölümünde geri bildirim üzerinde geliştirildi.</span><span class="sxs-lookup"><span data-stu-id="a03f4-108">It was improved based on feedback from users in the comments section.</span></span>

<span data-ttu-id="a03f4-109">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="a03f4-109">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a03f4-110">Veri ek açıklama Ekle</span><span class="sxs-lookup"><span data-stu-id="a03f4-110">Add data annotations</span></span>
> * <span data-ttu-id="a03f4-111">Meta veri sınıfları ekleme</span><span class="sxs-lookup"><span data-stu-id="a03f4-111">Add metadata classes</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a03f4-112">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="a03f4-112">Prerequisites</span></span>

* [<span data-ttu-id="a03f4-113">Bir görünümü özelleştirme</span><span class="sxs-lookup"><span data-stu-id="a03f4-113">Customize a view</span></span>](customizing-a-view.md)

## <a name="add-data-annotations"></a><span data-ttu-id="a03f4-114">Veri ek açıklama Ekle</span><span class="sxs-lookup"><span data-stu-id="a03f4-114">Add data annotations</span></span>

<span data-ttu-id="a03f4-115">Bir önceki konu başlığında gördüğünüz gibi bazı veri doğrulama kuralları, kullanıcı girişi için otomatik olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="a03f4-115">As you saw in an earlier topic, some data validation rules are automatically applied to the user input.</span></span> <span data-ttu-id="a03f4-116">Örneğin, sınıf özelliği için yalnızca bir sayı sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="a03f4-116">For example, you can only provide a number for the Grade property.</span></span> <span data-ttu-id="a03f4-117">Daha fazla veri doğrulama kurallarını belirtmek için veri ek açıklamaları model sınıfınızın ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a03f4-117">To specify more data validation rules, you can add data annotations to your model class.</span></span> <span data-ttu-id="a03f4-118">Bu ek açıklamalar, belirtilen özellik için web uygulamanızda uygulanır.</span><span class="sxs-lookup"><span data-stu-id="a03f4-118">These annotations are applied throughout your web application for the specified property.</span></span> <span data-ttu-id="a03f4-119">Ayrıca, özelliklerini nasıl görüntüleneceğini Değiştir biçimlendirme öznitelikleri de uygulayabilirsiniz; metin etiketlerini için kullanılan değer gibi değiştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="a03f4-119">You can also apply formatting attributes that change how the properties are displayed; such as, changing the value used for text labels.</span></span>

<span data-ttu-id="a03f4-120">Bu öğreticide, FirstName ve LastName MiddleName özellikleri için sağlanan değerler uzunluğunu kısıtlamak için veri ek açıklamalarını ekler.</span><span class="sxs-lookup"><span data-stu-id="a03f4-120">In this tutorial, you will add data annotations to restrict the length of the values provided for the FirstName, LastName, and MiddleName properties.</span></span> <span data-ttu-id="a03f4-121">Veritabanında, bu değerleri 50 karakterle sınırlıdır; Ancak, web uygulamanızda bu karakter sınırı şu anda zorlanmaz.</span><span class="sxs-lookup"><span data-stu-id="a03f4-121">In the database, these values are limited to 50 characters; however, in your web application that character limit is currently not enforced.</span></span> <span data-ttu-id="a03f4-122">Bir kullanıcı bu değerlerden biri 50 karakterden uzun sağlıyorsa sayfası değeri veritabanına kaydedilmeye çalışıldığında kilitlenir.</span><span class="sxs-lookup"><span data-stu-id="a03f4-122">If a user provides more than 50 characters for one of those values, the page will crash when attempting to save the value to the database.</span></span> <span data-ttu-id="a03f4-123">Ayrıca, değerleri 0 ile 4 arasında sınıf kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="a03f4-123">You will also restrict Grade to values between 0 and 4.</span></span>

<span data-ttu-id="a03f4-124">Seçin **modelleri** > **ContosoModel.edmx** > **ContosoModel.tt** açın *Student.cs* dosya.</span><span class="sxs-lookup"><span data-stu-id="a03f4-124">Select **Models** > **ContosoModel.edmx** > **ContosoModel.tt** and open the *Student.cs* file.</span></span> <span data-ttu-id="a03f4-125">Sınıfına aşağıdaki vurgulanmış kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a03f4-125">Add the following highlighted code to the class.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample1.cs?highlight=5,15,17,20)]

<span data-ttu-id="a03f4-126">Açık *Enrollment.cs* ve aşağıdaki vurgulanmış kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a03f4-126">Open *Enrollment.cs* and add the following highlighted code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample2.cs?highlight=5,10)]

<span data-ttu-id="a03f4-127">Çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a03f4-127">Build the solution.</span></span>

<span data-ttu-id="a03f4-128">Tıklayın **Öğrenciler listesi** seçip **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="a03f4-128">Click **List of students** and select **Edit**.</span></span> <span data-ttu-id="a03f4-129">50'den fazla karakter girin çalışırsanız, bir hata iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a03f4-129">If you attempt to enter more than 50 characters, an error message is displayed.</span></span>

![hata iletisi göster](enhancing-data-validation/_static/image1.png)

<span data-ttu-id="a03f4-131">Giriş sayfasına geri dönün.</span><span class="sxs-lookup"><span data-stu-id="a03f4-131">Go back to the home page.</span></span> <span data-ttu-id="a03f4-132">Tıklayın **kayıtları listesi** seçip **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="a03f4-132">Click **List of enrollments** and select **Edit**.</span></span> <span data-ttu-id="a03f4-133">Bir sınıf 4 yukarıda sağlamak çalışır.</span><span class="sxs-lookup"><span data-stu-id="a03f4-133">Attempt to provide a grade above 4.</span></span> <span data-ttu-id="a03f4-134">Bu hatayı alırsınız: *Alanı, sınıf 0 ile 4 arasında olması gerekir.*</span><span class="sxs-lookup"><span data-stu-id="a03f4-134">You will receive this error: *The field Grade must be between 0 and 4.*</span></span>

## <a name="add-metadata-classes"></a><span data-ttu-id="a03f4-135">Meta veri sınıfları ekleme</span><span class="sxs-lookup"><span data-stu-id="a03f4-135">Add metadata classes</span></span>

<span data-ttu-id="a03f4-136">Değiştirmek üzere veritabanını beklemiyoruz doğrudan model sınıfı için doğrulama öznitelikleri ekleyerek çalışır; Ancak, veritabanı değişikliklerinizi ve model sınıfı yeniden oluşturmanız gerekiyorsa, tüm model sınıfa uygulanmış özniteliklerini kaybedersiniz.</span><span class="sxs-lookup"><span data-stu-id="a03f4-136">Adding the validation attributes directly to the model class works when you do not expect the database to change; however, if your database changes and you need to regenerate the model class, you will lose all of the attributes you had applied to the model class.</span></span> <span data-ttu-id="a03f4-137">Bu yaklaşım çok verimsiz ve önemli doğrulama kuralları kaybetme potansiyeli olabilir.</span><span class="sxs-lookup"><span data-stu-id="a03f4-137">This approach can be very inefficient and prone to losing important validation rules.</span></span>

<span data-ttu-id="a03f4-138">Bu sorunu önlemek için özniteliklerini içeren bir meta veri sınıfının ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a03f4-138">To avoid this problem, you can add a metadata class that contains the attributes.</span></span> <span data-ttu-id="a03f4-139">Model sınıfı için meta veri sınıfının ilişkilendirdiğinizde, bu öznitelikleri modele uygulanır.</span><span class="sxs-lookup"><span data-stu-id="a03f4-139">When you associate the model class to the metadata class, those attributes are applied to the model.</span></span> <span data-ttu-id="a03f4-140">Bu yaklaşımda, tüm meta verileri sınıfına uygulanan öznitelikleri kaybetmeden model sınıfı üretilebilir.</span><span class="sxs-lookup"><span data-stu-id="a03f4-140">In this approach, the model class can be regenerated without losing all of the attributes that have been applied to the metadata class.</span></span>

<span data-ttu-id="a03f4-141">İçinde **modelleri** klasör adında bir sınıf ekleyin *Metadata.cs*.</span><span class="sxs-lookup"><span data-stu-id="a03f4-141">In the **Models** folder, add a class named *Metadata.cs*.</span></span>

<span data-ttu-id="a03f4-142">Değiştirin *Metadata.cs* aşağıdaki kod ile.</span><span class="sxs-lookup"><span data-stu-id="a03f4-142">Replace the code in *Metadata.cs* with the following code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample3.cs)]

<span data-ttu-id="a03f4-143">Bu meta veri sınıfları tüm model sınıfları, daha önce uyguladığınız doğrulama özniteliklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="a03f4-143">These metadata classes contain all of the validation attributes that you had previously applied to the model classes.</span></span> <span data-ttu-id="a03f4-144">**Görünen** özniteliği metin etiketleri için kullanılan değeri değiştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a03f4-144">The **Display** attribute is used to change the value used for text labels.</span></span>

<span data-ttu-id="a03f4-145">Şimdi, meta veri sınıfları ile model sınıfları ilişkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a03f4-145">Now, you must associate the model classes with the metadata classes.</span></span>

<span data-ttu-id="a03f4-146">İçinde **modelleri** klasör adında bir sınıf ekleyin *PartialClasses.cs*.</span><span class="sxs-lookup"><span data-stu-id="a03f4-146">In the **Models** folder, add a class named *PartialClasses.cs*.</span></span>

<span data-ttu-id="a03f4-147">Dosyanın içeriğini aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a03f4-147">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample4.cs)]

<span data-ttu-id="a03f4-148">Her sınıf olarak işaretlenmiş olduğuna dikkat edin. bir `partial` sınıfı ve her otomatik olarak oluşturulan sınıf olarak eşleşen ad alanı ve adını.</span><span class="sxs-lookup"><span data-stu-id="a03f4-148">Notice that each class is marked as a `partial` class, and each matches the name and namespace as the class that is automatically generated.</span></span> <span data-ttu-id="a03f4-149">Kısmi sınıfa meta veri özniteliği uygulayarak veri doğrulama özniteliklerinin otomatik olarak oluşturulan sınıfa uygulanan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a03f4-149">By applying the metadata attribute to the partial class, you ensure that the data validation attributes will be applied to the automatically-generated class.</span></span> <span data-ttu-id="a03f4-150">Meta veri özniteliği değil yeniden kısmi sınıflar uygulandığından model sınıfları yeniden oluştururken bu öznitelikler kaybolmaz.</span><span class="sxs-lookup"><span data-stu-id="a03f4-150">These attributes will not be lost when you regenerate the model classes because the metadata attribute is applied in partial classes that are not regenerated.</span></span>

<span data-ttu-id="a03f4-151">Otomatik olarak oluşturulan sınıflar yeniden oluşturmak için açık *ContosoModel.edmx* dosya.</span><span class="sxs-lookup"><span data-stu-id="a03f4-151">To regenerate the automatically-generated classes, open the *ContosoModel.edmx* file.</span></span> <span data-ttu-id="a03f4-152">Bir kez daha, tasarım yüzeyi ve select sağ **veritabanından bir güncelleştirme modeli**.</span><span class="sxs-lookup"><span data-stu-id="a03f4-152">Once again, right-click on the design surface and select **Update Model from Database**.</span></span> <span data-ttu-id="a03f4-153">Bu işlem, veritabanı değişmemiştir. olsa da, sınıfları yeniden oluşturulacak.</span><span class="sxs-lookup"><span data-stu-id="a03f4-153">Even though you have not changed the database, this process will regenerate the classes.</span></span> <span data-ttu-id="a03f4-154">İçinde **Yenile** sekmesinde **tabloları** ve **son**.</span><span class="sxs-lookup"><span data-stu-id="a03f4-154">In the **Refresh** tab, select **Tables** and **Finish**.</span></span>

<span data-ttu-id="a03f4-155">Kaydet *ContosoModel.edmx* değişiklikleri uygulamak için dosya.</span><span class="sxs-lookup"><span data-stu-id="a03f4-155">Save the *ContosoModel.edmx* file to apply the changes.</span></span>

<span data-ttu-id="a03f4-156">Açık *Student.cs* dosya veya *Enrollment.cs* dosya ve daha önce uyguladığınız veri doğrulama öznitelikleri artık dosyasındadır dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a03f4-156">Open the *Student.cs* file or the *Enrollment.cs* file, and notice that the data validation attributes you applied earlier are no longer in the file.</span></span> <span data-ttu-id="a03f4-157">Ancak, uygulamayı çalıştırmak ve veri girdiğinizde doğrulama kuralları hala uygulandığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a03f4-157">However, run the application, and notice that the validation rules are still applied when you enter data.</span></span>

## <a name="conclusion"></a><span data-ttu-id="a03f4-158">Sonuç</span><span class="sxs-lookup"><span data-stu-id="a03f4-158">Conclusion</span></span>

<span data-ttu-id="a03f4-159">Bu seri, düzenleyebilir, güncelleştirebilir, oluşturabilir ve verileri silmek kullanıcıların sağlayan varolan bir veritabanından kodu oluşturmak nasıl basit bir örnek sağlanır.</span><span class="sxs-lookup"><span data-stu-id="a03f4-159">This series provided a simple example of how to generate code from an existing database that enables users to edit, update, create and delete data.</span></span> <span data-ttu-id="a03f4-160">Projeyi oluşturmak için ASP.NET MVC 5, Entity Framework ve ASP.NET iskeleti oluşturma kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a03f4-160">It used ASP.NET MVC 5, Entity Framework and ASP.NET Scaffolding to create the project.</span></span> 

<span data-ttu-id="a03f4-161">Code First geliştirmeye giriş örneği için bkz: [ASP.NET MVC 5 ile çalışmaya başlama](../introduction/getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="a03f4-161">For an introductory example of Code First development, see [Getting Started with ASP.NET MVC 5](../introduction/getting-started.md).</span></span> 

<span data-ttu-id="a03f4-162">Daha gelişmiş bir örnek için bkz: [ASP.NET MVC 4 uygulaması için bir Entity Framework veri modeli oluşturma](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="a03f4-162">For a more advanced example, see [Creating an Entity Framework Data Model for an ASP.NET MVC 4 App](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="a03f4-163">Veritabanı ilk verilerle çalışmak için kullandığınız DbContext API Code First verilerle çalışmak için kullandığınız API ile aynı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a03f4-163">Note that the DbContext API that you use for working with data in Database First is the same as the API you use for working with data in Code First.</span></span> <span data-ttu-id="a03f4-164">Veritabanı ilk kullanmak istediğinize olsa bile, vb. kod ilk öğreticide öğesinden eşzamanlılık çakışmalarını işleme okuma ve ilgili verileri güncelleştirme gibi daha karmaşık senaryolarda işlemek nasıl öğrenebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a03f4-164">Even if you intend to use Database First, you can learn how to handle more complex scenarios such as reading and updating related data, handling concurrency conflicts, and so forth from a Code First tutorial.</span></span> <span data-ttu-id="a03f4-165">Tek fark, nasıl veritabanı bağlamı sınıfının ve varlık sınıfları oluşturulur ' dir.</span><span class="sxs-lookup"><span data-stu-id="a03f4-165">The only difference is in how the database, context class, and entity classes are created.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a03f4-166">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a03f4-166">Additional resources</span></span>

<span data-ttu-id="a03f4-167">Veri doğrulama ek özellikleri ve sınıflarına uygulayabilirsiniz tam bir listesi için bkz. [System.ComponentModel.DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx).</span><span class="sxs-lookup"><span data-stu-id="a03f4-167">For a full list of data validation annotations you can apply to properties and classes, see [System.ComponentModel.DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a03f4-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a03f4-168">Next steps</span></span>

<span data-ttu-id="a03f4-169">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="a03f4-169">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a03f4-170">Eklenen veri ek açıklamaları</span><span class="sxs-lookup"><span data-stu-id="a03f4-170">Added data annotations</span></span>
> * <span data-ttu-id="a03f4-171">Ek meta veri sınıfları</span><span class="sxs-lookup"><span data-stu-id="a03f4-171">Added metadata classes</span></span>

<span data-ttu-id="a03f4-172">Bir web uygulaması ve SQL veritabanı, Azure App Service'e dağıtma konusunda bilgi almak için bu öğreticiye bakın:</span><span class="sxs-lookup"><span data-stu-id="a03f4-172">To learn how to deploy a web app and SQL database to Azure App Service, see this tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="a03f4-173">Azure App Service'e .NET uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="a03f4-173">Deploy a .NET app to Azure App Service</span></span>](/azure/app-service/app-service-web-tutorial-dotnet-sqldatabase/)
