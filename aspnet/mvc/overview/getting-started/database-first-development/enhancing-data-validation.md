---
uid: mvc/overview/getting-started/database-first-development/enhancing-data-validation
title: 'Öğretici: ASP.NET MVC uygulamasıyla EF Database First için veri doğrulamayı geliştirin'
description: Bu öğretici, doğrulama gereksinimlerini belirtmek ve biçimlendirmeyi göstermek için veri modeline veri ek açıklamaları eklenmesine odaklanmaktadır.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 0ed5e67a-34c0-4b57-84a6-802b0fb3cd00
msc.legacyurl: /mvc/overview/getting-started/database-first-development/enhancing-data-validation
msc.type: authoredcontent
ms.openlocfilehash: 897cd7c6a40445e2a4abede50d81e101372d3233
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616279"
---
# <a name="tutorial-enhance-data-validation-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="2c319-103">Öğretici: ASP.NET MVC uygulamasıyla EF Database First için veri doğrulamayı geliştirin</span><span class="sxs-lookup"><span data-stu-id="2c319-103">Tutorial: Enhance data validation for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="2c319-104">MVC, Entity Framework ve ASP.NET Scafkatı kullanarak var olan bir veritabanına arabirim sağlayan bir Web uygulaması oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c319-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="2c319-105">Bu öğretici serisinde, kullanıcıların bir veritabanı tablosunda yer alan verileri görüntülemesini, düzenlemesini, oluşturmasını ve silmesini sağlayan nasıl otomatik olarak kod üretileyeceğiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="2c319-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="2c319-106">Oluşturulan kod, veritabanı tablosundaki sütunlara karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="2c319-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="2c319-107">Bu öğretici, doğrulama gereksinimlerini belirtmek ve biçimlendirmeyi göstermek için veri modeline veri ek açıklamaları eklenmesine odaklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="2c319-107">This tutorial focuses on adding data annotations to the data model to specify validation requirements and display formatting.</span></span> <span data-ttu-id="2c319-108">Yorumlar bölümünde kullanıcılardan gelen geri bildirimlere göre geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="2c319-108">It was improved based on feedback from users in the comments section.</span></span>

<span data-ttu-id="2c319-109">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="2c319-109">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2c319-110">Veri ek açıklamaları Ekle</span><span class="sxs-lookup"><span data-stu-id="2c319-110">Add data annotations</span></span>
> * <span data-ttu-id="2c319-111">Meta veri sınıfları Ekle</span><span class="sxs-lookup"><span data-stu-id="2c319-111">Add metadata classes</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c319-112">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="2c319-112">Prerequisites</span></span>

* [<span data-ttu-id="2c319-113">Görünümü özelleştirme</span><span class="sxs-lookup"><span data-stu-id="2c319-113">Customize a view</span></span>](customizing-a-view.md)

## <a name="add-data-annotations"></a><span data-ttu-id="2c319-114">Veri ek açıklamaları Ekle</span><span class="sxs-lookup"><span data-stu-id="2c319-114">Add data annotations</span></span>

<span data-ttu-id="2c319-115">Daha önceki bir konu başlığında gördüğünüz gibi, bazı veri doğrulama kuralları Kullanıcı girişine otomatik olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="2c319-115">As you saw in an earlier topic, some data validation rules are automatically applied to the user input.</span></span> <span data-ttu-id="2c319-116">Örneğin, sınıf özelliği için yalnızca bir sayı sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c319-116">For example, you can only provide a number for the Grade property.</span></span> <span data-ttu-id="2c319-117">Daha fazla veri doğrulama kuralı belirtmek için model sınıfınıza veri ek açıklamaları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c319-117">To specify more data validation rules, you can add data annotations to your model class.</span></span> <span data-ttu-id="2c319-118">Bu ek açıklamalar, belirtilen özellik için Web uygulamanız genelinde uygulanır.</span><span class="sxs-lookup"><span data-stu-id="2c319-118">These annotations are applied throughout your web application for the specified property.</span></span> <span data-ttu-id="2c319-119">Özelliklerin nasıl görüntülendiğini değiştiren biçimlendirme öznitelikleri de uygulayabilirsiniz. Örneğin, metin etiketleri için kullanılan değeri değiştirme.</span><span class="sxs-lookup"><span data-stu-id="2c319-119">You can also apply formatting attributes that change how the properties are displayed; such as, changing the value used for text labels.</span></span>

<span data-ttu-id="2c319-120">Bu öğreticide, FirstName, LastName ve MiddleName özellikleri için belirtilen değerlerin uzunluğunu kısıtlamak üzere veri ek açıklamaları ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="2c319-120">In this tutorial, you will add data annotations to restrict the length of the values provided for the FirstName, LastName, and MiddleName properties.</span></span> <span data-ttu-id="2c319-121">Veritabanında, bu değerler 50 karakterle sınırlıdır; Ancak, Web uygulamanızda karakter sınırının Şu anda zorlanmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2c319-121">In the database, these values are limited to 50 characters; however, in your web application that character limit is currently not enforced.</span></span> <span data-ttu-id="2c319-122">Bir Kullanıcı bu değerlerden biri için 50 ' den fazla karakter sağlıyorsa, bu değer veritabanına kaydedilmeye çalışıldığında sayfa kilitlenir.</span><span class="sxs-lookup"><span data-stu-id="2c319-122">If a user provides more than 50 characters for one of those values, the page will crash when attempting to save the value to the database.</span></span> <span data-ttu-id="2c319-123">Ayrıca, 0 ile 4 arasındaki değerleri de sınırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c319-123">You will also restrict Grade to values between 0 and 4.</span></span>

<span data-ttu-id="2c319-124"> > **Contosomodel. edmx** > **ContosoModel.tt** **modellerini** seçin ve *Student.cs* dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="2c319-124">Select **Models** > **ContosoModel.edmx** > **ContosoModel.tt** and open the *Student.cs* file.</span></span> <span data-ttu-id="2c319-125">Aşağıdaki Vurgulanan kodu sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2c319-125">Add the following highlighted code to the class.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample1.cs?highlight=5,15,17,20)]

<span data-ttu-id="2c319-126">*Enrollment.cs* açın ve aşağıdaki vurgulanmış kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2c319-126">Open *Enrollment.cs* and add the following highlighted code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample2.cs?highlight=5,10)]

<span data-ttu-id="2c319-127">Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="2c319-127">Build the solution.</span></span>

<span data-ttu-id="2c319-128">**Öğrenciler listesi** ' ne tıklayın ve **Düzenle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="2c319-128">Click **List of students** and select **Edit**.</span></span> <span data-ttu-id="2c319-129">50 'den fazla karakter girmeye çalışırsanız bir hata iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2c319-129">If you attempt to enter more than 50 characters, an error message is displayed.</span></span>

![hata iletisini göster](enhancing-data-validation/_static/image1.png)

<span data-ttu-id="2c319-131">Giriş sayfasına geri dönün.</span><span class="sxs-lookup"><span data-stu-id="2c319-131">Go back to the home page.</span></span> <span data-ttu-id="2c319-132">Kayıt **listesi** ' ne tıklayın ve **Düzenle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="2c319-132">Click **List of enrollments** and select **Edit**.</span></span> <span data-ttu-id="2c319-133">4 ' ün üzerinde bir sınıf sağlamayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="2c319-133">Attempt to provide a grade above 4.</span></span> <span data-ttu-id="2c319-134">Bu hatayı alırsınız: *alan sınıfı 0 ile 4 arasında olmalıdır.*</span><span class="sxs-lookup"><span data-stu-id="2c319-134">You will receive this error: *The field Grade must be between 0 and 4.*</span></span>

## <a name="add-metadata-classes"></a><span data-ttu-id="2c319-135">Meta veri sınıfları Ekle</span><span class="sxs-lookup"><span data-stu-id="2c319-135">Add metadata classes</span></span>

<span data-ttu-id="2c319-136">Doğrulama özniteliklerini doğrudan model sınıfına eklemek, veritabanının değiştirilmesini beklemediğinde işe yarar; Ancak, veritabanınız değişirse ve model sınıfını yeniden oluşturmanız gerekiyorsa, model sınıfına uyguladığınız tüm öznitelikleri kaybedersiniz.</span><span class="sxs-lookup"><span data-stu-id="2c319-136">Adding the validation attributes directly to the model class works when you do not expect the database to change; however, if your database changes and you need to regenerate the model class, you will lose all of the attributes you had applied to the model class.</span></span> <span data-ttu-id="2c319-137">Bu yaklaşım çok verimsiz olabilir ve önemli doğrulama kurallarının kaybolması olabilir.</span><span class="sxs-lookup"><span data-stu-id="2c319-137">This approach can be very inefficient and prone to losing important validation rules.</span></span>

<span data-ttu-id="2c319-138">Bu sorundan kaçınmak için, özniteliklerini içeren bir meta veri sınıfı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c319-138">To avoid this problem, you can add a metadata class that contains the attributes.</span></span> <span data-ttu-id="2c319-139">Model sınıfını meta veri sınıfıyla ilişkilendirdiğinizde, bu öznitelikler modele uygulanır.</span><span class="sxs-lookup"><span data-stu-id="2c319-139">When you associate the model class to the metadata class, those attributes are applied to the model.</span></span> <span data-ttu-id="2c319-140">Bu yaklaşımda model sınıfı, meta veri sınıfına uygulanan tüm öznitelikleri kaybetmeden yeniden oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="2c319-140">In this approach, the model class can be regenerated without losing all of the attributes that have been applied to the metadata class.</span></span>

<span data-ttu-id="2c319-141">**Modeller** klasöründe, *Metadata.cs*adlı bir sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2c319-141">In the **Models** folder, add a class named *Metadata.cs*.</span></span>

<span data-ttu-id="2c319-142">*Metadata.cs* içindeki kodu aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2c319-142">Replace the code in *Metadata.cs* with the following code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample3.cs)]

<span data-ttu-id="2c319-143">Bu meta veri sınıfları, daha önce model sınıflarına uyguladığınız tüm doğrulama özniteliklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="2c319-143">These metadata classes contain all of the validation attributes that you had previously applied to the model classes.</span></span> <span data-ttu-id="2c319-144">**Görüntü** özniteliği, metin etiketleri için kullanılan değeri değiştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2c319-144">The **Display** attribute is used to change the value used for text labels.</span></span>

<span data-ttu-id="2c319-145">Şimdi, model sınıflarını meta veri sınıflarıyla ilişkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2c319-145">Now, you must associate the model classes with the metadata classes.</span></span>

<span data-ttu-id="2c319-146">**Modeller** klasöründe, *PartialClasses.cs*adlı bir sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2c319-146">In the **Models** folder, add a class named *PartialClasses.cs*.</span></span>

<span data-ttu-id="2c319-147">Dosyanın içeriğini aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2c319-147">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample4.cs)]

<span data-ttu-id="2c319-148">Her sınıfın bir `partial` sınıfı olarak işaretlendiğinden ve her birinin otomatik olarak oluşturulan sınıf ile ad ve ad alanıyla eşleştiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2c319-148">Notice that each class is marked as a `partial` class, and each matches the name and namespace as the class that is automatically generated.</span></span> <span data-ttu-id="2c319-149">Meta veri özniteliğini kısmi sınıfa uygulayarak, veri doğrulama özniteliklerinin otomatik olarak oluşturulan sınıfa uygulandığından emin olursunuz.</span><span class="sxs-lookup"><span data-stu-id="2c319-149">By applying the metadata attribute to the partial class, you ensure that the data validation attributes will be applied to the automatically-generated class.</span></span> <span data-ttu-id="2c319-150">Meta veri özniteliği yeniden üretilmediği kısmi sınıflarda uygulandığından, model sınıflarını yeniden oluşturduğunuzda bu öznitelikler kaybolmaz.</span><span class="sxs-lookup"><span data-stu-id="2c319-150">These attributes will not be lost when you regenerate the model classes because the metadata attribute is applied in partial classes that are not regenerated.</span></span>

<span data-ttu-id="2c319-151">Otomatik olarak oluşturulan sınıfları yeniden oluşturmak için *Contosomodel. edmx* dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="2c319-151">To regenerate the automatically-generated classes, open the *ContosoModel.edmx* file.</span></span> <span data-ttu-id="2c319-152">Bir kez daha, tasarım yüzeyine sağ tıklayın ve **modeli veritabanından Güncelleştir**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="2c319-152">Once again, right-click on the design surface and select **Update Model from Database**.</span></span> <span data-ttu-id="2c319-153">Veritabanını değiştirmeseniz bile, bu işlem sınıfları yeniden oluşturacak.</span><span class="sxs-lookup"><span data-stu-id="2c319-153">Even though you have not changed the database, this process will regenerate the classes.</span></span> <span data-ttu-id="2c319-154">**Yenile** sekmesinde **Tablolar** ve **son**' u seçin.</span><span class="sxs-lookup"><span data-stu-id="2c319-154">In the **Refresh** tab, select **Tables** and **Finish**.</span></span>

<span data-ttu-id="2c319-155">Değişiklikleri uygulamak için *Contosomodel. edmx* dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2c319-155">Save the *ContosoModel.edmx* file to apply the changes.</span></span>

<span data-ttu-id="2c319-156">*Student.cs* dosyasını veya *enrollment.cs* dosyasını açın ve daha önce uyguladığınız veri doğrulama özniteliklerinin artık dosyada bulunmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="2c319-156">Open the *Student.cs* file or the *Enrollment.cs* file, and notice that the data validation attributes you applied earlier are no longer in the file.</span></span> <span data-ttu-id="2c319-157">Ancak, uygulamayı çalıştırın ve veri girerken doğrulama kurallarının hala uygulanmış olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="2c319-157">However, run the application, and notice that the validation rules are still applied when you enter data.</span></span>

## <a name="conclusion"></a><span data-ttu-id="2c319-158">Sonuç</span><span class="sxs-lookup"><span data-stu-id="2c319-158">Conclusion</span></span>

<span data-ttu-id="2c319-159">Bu seri, kullanıcıların verileri düzenlemesini, güncelleştirmesini, oluşturmasını ve silmesini sağlayan mevcut bir veritabanından kod oluşturmaya yönelik basit bir örnek sağlamıştır.</span><span class="sxs-lookup"><span data-stu-id="2c319-159">This series provided a simple example of how to generate code from an existing database that enables users to edit, update, create and delete data.</span></span> <span data-ttu-id="2c319-160">Projeyi oluşturmak için ASP.NET MVC 5, Entity Framework ve ASP.NET Scafkatlesi kullandı.</span><span class="sxs-lookup"><span data-stu-id="2c319-160">It used ASP.NET MVC 5, Entity Framework and ASP.NET Scaffolding to create the project.</span></span> 

<span data-ttu-id="2c319-161">Code First geliştirmenin açıklayıcı bir örneği için bkz. [ASP.NET MVC 5 Ile çalışmaya](../introduction/getting-started.md)başlama.</span><span class="sxs-lookup"><span data-stu-id="2c319-161">For an introductory example of Code First development, see [Getting Started with ASP.NET MVC 5](../introduction/getting-started.md).</span></span> 

<span data-ttu-id="2c319-162">Daha gelişmiş bir örnek için bkz. [ASP.NET MVC 4 uygulaması için Entity Framework veri modeli oluşturma](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="2c319-162">For a more advanced example, see [Creating an Entity Framework Data Model for an ASP.NET MVC 4 App](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="2c319-163">Database First verileriyle çalışırken kullandığınız DbContext API 'sinin, Code First verilerle çalışırken kullandığınız API ile aynı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2c319-163">Note that the DbContext API that you use for working with data in Database First is the same as the API you use for working with data in Code First.</span></span> <span data-ttu-id="2c319-164">Database First kullanmayı amaçlasanız bile, ilgili verileri okuma ve güncelleştirme, eşzamanlılık çakışmalarını işleme gibi daha karmaşık senaryoları nasıl işleyeceğinizi ve bir Code First öğreticiden yapmayı öğrenebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c319-164">Even if you intend to use Database First, you can learn how to handle more complex scenarios such as reading and updating related data, handling concurrency conflicts, and so forth from a Code First tutorial.</span></span> <span data-ttu-id="2c319-165">Tek fark, veritabanının, bağlam sınıfının ve varlık sınıflarının oluşturulma biçiminde olur.</span><span class="sxs-lookup"><span data-stu-id="2c319-165">The only difference is in how the database, context class, and entity classes are created.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2c319-166">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2c319-166">Additional resources</span></span>

<span data-ttu-id="2c319-167">Veri doğrulama ek açıklamalarının tam listesi için, Özellikler ve sınıflar için uygulayabileceğiniz, bkz. [System. ComponentModel. Dataaçıklamalarda](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c319-167">For a full list of data validation annotations you can apply to properties and classes, see [System.ComponentModel.DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c319-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2c319-168">Next steps</span></span>

<span data-ttu-id="2c319-169">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="2c319-169">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2c319-170">Eklenen veri açıklamaları</span><span class="sxs-lookup"><span data-stu-id="2c319-170">Added data annotations</span></span>
> * <span data-ttu-id="2c319-171">Meta veri sınıfları eklendi</span><span class="sxs-lookup"><span data-stu-id="2c319-171">Added metadata classes</span></span>

<span data-ttu-id="2c319-172">Azure App Service için bir Web uygulaması ve SQL veritabanı dağıtmayı öğrenmek için şu öğreticiye bakın:</span><span class="sxs-lookup"><span data-stu-id="2c319-172">To learn how to deploy a web app and SQL database to Azure App Service, see this tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="2c319-173">Azure App Service için bir .NET uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="2c319-173">Deploy a .NET app to Azure App Service</span></span>](/azure/app-service/app-service-web-tutorial-dotnet-sqldatabase/)
