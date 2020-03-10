---
uid: web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
title: Model bağlama ve Web formları ile verileri güncelleştirme, silme ve oluşturma | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir. Model bağlama, veri etkileşimini daha düz-... hale getirir
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 602baa94-5a4f-46eb-a717-7a9e539c1db4
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
msc.type: authoredcontent
ms.openlocfilehash: 11dc52ec79ca91119b37ea60e08164eb1b1d0e2b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586648"
---
# <a name="updating-deleting-and-creating-data-with-model-binding-and-web-forms"></a><span data-ttu-id="e6486-104">Model bağlama ve Web formları ile verileri güncelleştirme, silme ve oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6486-104">Updating, deleting, and creating data with model binding and web forms</span></span>

<span data-ttu-id="e6486-105">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="e6486-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="e6486-106">Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="e6486-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="e6486-107">Model bağlama veri kaynağı nesneleriyle (örneğin, ObjectDataSource veya SqlDataSource) çok daha basit hale getirir.</span><span class="sxs-lookup"><span data-stu-id="e6486-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="e6486-108">Bu seri giriş malzemesiyle başlar ve sonraki öğreticilerde daha gelişmiş kavramlara gider.</span><span class="sxs-lookup"><span data-stu-id="e6486-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="e6486-109">Bu öğreticide, model bağlama ile veri oluşturma, güncelleştirme ve silme işlemlerinin nasıl yapılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e6486-109">This tutorial shows how to create, update, and delete data with model binding.</span></span> <span data-ttu-id="e6486-110">Aşağıdaki özellikleri ayarlayacaksınız:</span><span class="sxs-lookup"><span data-stu-id="e6486-110">You will set the following properties:</span></span>
> 
> - <span data-ttu-id="e6486-111">DeleteMethod</span><span class="sxs-lookup"><span data-stu-id="e6486-111">DeleteMethod</span></span>
> - <span data-ttu-id="e6486-112">InsertMethod</span><span class="sxs-lookup"><span data-stu-id="e6486-112">InsertMethod</span></span>
> - <span data-ttu-id="e6486-113">UpdateMethod</span><span class="sxs-lookup"><span data-stu-id="e6486-113">UpdateMethod</span></span>
> 
> <span data-ttu-id="e6486-114">Bu özellikler, karşılık gelen işlemi işleyen yöntemin adını alır.</span><span class="sxs-lookup"><span data-stu-id="e6486-114">These properties receive the name of the method that handles the corresponding operation.</span></span> <span data-ttu-id="e6486-115">Bu yöntemde, verilerle etkileşim kurma mantığını sağlarsınız.</span><span class="sxs-lookup"><span data-stu-id="e6486-115">Within that method, you provide the logic for interacting with the data.</span></span>
> 
> <span data-ttu-id="e6486-116">Bu öğreticide, serinin ilk [bölümünde](retrieving-data.md) oluşturulan proje oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e6486-116">This tutorial builds on the project created in the first [part](retrieving-data.md) of the series.</span></span>
> 
> <span data-ttu-id="e6486-117">Tüm projeyi [](https://go.microsoft.com/fwlink/?LinkId=286116) C# veya vb 'ye indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6486-117">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="e6486-118">İndirilebilir kod, Visual Studio 2012 veya Visual Studio 2013 ile birlikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e6486-118">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="e6486-119">Bu öğreticide gösterilen Visual Studio 2013 şablonundan biraz farklı olan Visual Studio 2012 şablonunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="e6486-119">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="e6486-120">Ne oluşturacağız?</span><span class="sxs-lookup"><span data-stu-id="e6486-120">What you'll build</span></span>

<span data-ttu-id="e6486-121">Bu öğreticide şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e6486-121">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="e6486-122">Dinamik veri şablonları ekleme</span><span class="sxs-lookup"><span data-stu-id="e6486-122">Add dynamic data templates</span></span>
2. <span data-ttu-id="e6486-123">Model bağlama yöntemleriyle verileri güncelleştirme ve silmeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="e6486-123">Enable updating and deleting data through model binding methods</span></span>
3. <span data-ttu-id="e6486-124">Veri doğrulama kurallarını uygulama-veritabanında yeni bir kayıt oluşturmayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="e6486-124">Apply data validation rules - Enable creating a new record in the database</span></span>

## <a name="add-dynamic-data-templates"></a><span data-ttu-id="e6486-125">Dinamik veri şablonları ekleme</span><span class="sxs-lookup"><span data-stu-id="e6486-125">Add dynamic data templates</span></span>

<span data-ttu-id="e6486-126">En iyi kullanıcı deneyimini sağlamak ve kod tekrarlamayı en aza indirmek için dinamik veri şablonlarını kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e6486-126">To provide the best user experience and minimize code repetition, you will use dynamic data templates.</span></span> <span data-ttu-id="e6486-127">Önceden oluşturulmuş dinamik veri şablonlarını, bir NuGet paketi yükleyerek var olan sitenize kolayca tümleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6486-127">You can easily integrate pre-built dynamic data templates into your existing site by installing a NuGet package.</span></span>

<span data-ttu-id="e6486-128">**NuGet Paketlerini Yönet**' den **Dynamicdatatemplatescs**'yi yükler.</span><span class="sxs-lookup"><span data-stu-id="e6486-128">From the **Manage NuGet Packages**, install the **DynamicDataTemplatesCS**.</span></span>

![dinamik veri şablonları](updating-deleting-and-creating-data/_static/image1.png)

<span data-ttu-id="e6486-130">Projenizin artık **DynamicData**adlı bir klasör içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e6486-130">Notice that your project now includes a folder named **DynamicData**.</span></span> <span data-ttu-id="e6486-131">Bu klasörde, Web formlarınızda dinamik denetimlere otomatik olarak uygulanan şablonları bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e6486-131">In that folder, you will find the templates that are automatically applied to dynamic controls in your web forms.</span></span>

![dinamik veri klasörü](updating-deleting-and-creating-data/_static/image2.png)

## <a name="enable-updating-and-deleting"></a><span data-ttu-id="e6486-133">Güncelleştirme ve silmeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="e6486-133">Enable updating and deleting</span></span>

<span data-ttu-id="e6486-134">Kullanıcıların veritabanındaki kayıtları güncelleştirmesini ve silmesini sağlamak, verileri alma sürecine çok benzer.</span><span class="sxs-lookup"><span data-stu-id="e6486-134">Enabling users to update and delete records in the database is very similar to the process for retrieving data.</span></span> <span data-ttu-id="e6486-135">**UpdateMethod** ve **DeleteMethod** özelliklerinde, bu işlemleri gerçekleştiren yöntemlerin adlarını belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6486-135">In the **UpdateMethod** and **DeleteMethod** properties, you specify the names of the methods that perform those operations.</span></span> <span data-ttu-id="e6486-136">GridView denetimiyle, düzenleme ve silme düğmelerinin otomatik oluşturulmasını de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6486-136">With a GridView control, you can also specify the automatic generation of edit and delete buttons.</span></span> <span data-ttu-id="e6486-137">Aşağıdaki vurgulanan kod, GridView koduna yapılan eklemeleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="e6486-137">The following highlighted code shows the additions to the GridView code.</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample1.aspx?highlight=4-5)]

<span data-ttu-id="e6486-138">Arka plan kod dosyasında, **System. Data. Entity. Infrastructure**için bir using açıklaması ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e6486-138">In the code-behind file, add a using statement for **System.Data.Entity.Infrastructure**.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample2.cs)]

<span data-ttu-id="e6486-139">Ardından, aşağıdaki güncelleştirmeyi ve silme yöntemlerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e6486-139">Then, add the following update and delete methods.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample3.cs)]

<span data-ttu-id="e6486-140">**TryUpdateModel** yöntemi, Web formundan eşleşen veri bağlantılı değerleri veri öğesine uygular.</span><span class="sxs-lookup"><span data-stu-id="e6486-140">The **TryUpdateModel** method applies the matching data-bound values from the web form to the data item.</span></span> <span data-ttu-id="e6486-141">Veri öğesi, ID parametresinin değerine göre alınır.</span><span class="sxs-lookup"><span data-stu-id="e6486-141">The data item is retrieved based on the value of the id parameter.</span></span>

## <a name="enforce-validation-requirements"></a><span data-ttu-id="e6486-142">Doğrulama gereksinimlerini zorla</span><span class="sxs-lookup"><span data-stu-id="e6486-142">Enforce validation requirements</span></span>

<span data-ttu-id="e6486-143">Öğrenci sınıfındaki FirstName, LastName ve Year özelliklerine uyguladığınız doğrulama öznitelikleri, veriler güncelleştirilirken otomatik olarak zorlanır.</span><span class="sxs-lookup"><span data-stu-id="e6486-143">The validation attributes that you applied to the FirstName, LastName, and Year properties in the Student class are automatically enforced when updating the data.</span></span> <span data-ttu-id="e6486-144">DynamicField denetimleri, doğrulama özniteliklerine göre istemci ve sunucu Doğrulayıcıları ekler.</span><span class="sxs-lookup"><span data-stu-id="e6486-144">The DynamicField controls add client and server validators based on the validation attributes.</span></span> <span data-ttu-id="e6486-145">FirstName ve LastName özelliklerinin ikisi de gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e6486-145">The FirstName and LastName properties are both required.</span></span> <span data-ttu-id="e6486-146">FirstName uzunluğu 20 karakteri aşamaz ve LastName 40 karakteri aşamaz.</span><span class="sxs-lookup"><span data-stu-id="e6486-146">FirstName cannot exceed 20 characters in length, and LastName cannot exceed 40 characters.</span></span> <span data-ttu-id="e6486-147">Yıl, akademik Micyear numaralandırması için geçerli bir değer olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e6486-147">Year must be a valid value for the AcademicYear enumeration.</span></span>

<span data-ttu-id="e6486-148">Kullanıcı doğrulama gereksinimlerinden birini ihlal ederse güncelleştirme devam etmez.</span><span class="sxs-lookup"><span data-stu-id="e6486-148">If the user violates one of the validation requirements, the update does not proceed.</span></span> <span data-ttu-id="e6486-149">Hata iletisini görmek için GridView 'un üzerine bir ValidationSummary denetimi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e6486-149">To see the error message, add a ValidationSummary control above the GridView.</span></span> <span data-ttu-id="e6486-150">Model bağlamasındaki doğrulama hatalarını göstermek için **ShowModelStateErrors** özelliğini **true**olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e6486-150">To display the validation errors from model binding, set the **ShowModelStateErrors** property set to **true**.</span></span> 

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample4.aspx)]

<span data-ttu-id="e6486-151">Web uygulamasını çalıştırın ve kayıtları güncelleştirin ve silin.</span><span class="sxs-lookup"><span data-stu-id="e6486-151">Run the web application, and update and delete any of the records.</span></span>

![verileri güncelleştirme](updating-deleting-and-creating-data/_static/image3.png)

<span data-ttu-id="e6486-153">Düzenleme modunda Year özelliğinin değeri otomatik olarak bir açılan liste olarak işlendiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e6486-153">Notice that when in the edit mode the value for the Year property is automatically rendered as a drop down list.</span></span> <span data-ttu-id="e6486-154">Year özelliği bir sabit listesi değeridir ve bir numaralandırma değeri için dinamik veri şablonu, düzenlemenin açılan listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="e6486-154">The Year property is an enumeration value, and the dynamic data template for an enumeration value specifies a drop down list for editing.</span></span> <span data-ttu-id="e6486-155">Bu şablonu, **DynamicData**/**FieldTemplates** klasöründe **numaralandırma\_. ascx** dosyasını açarak bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6486-155">You can find that template by opening the **Enumeration\_Edit.ascx** file in the **DynamicData**/**FieldTemplates** folder.</span></span>

<span data-ttu-id="e6486-156">Geçerli değerler sağlarsanız güncelleştirme başarıyla tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="e6486-156">If you provide valid values, the update completes successfully.</span></span> <span data-ttu-id="e6486-157">Doğrulama gereksinimlerinden birini ihlal ederseniz, güncelleştirme devam etmez ve kılavuzun üzerinde bir hata mesajı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e6486-157">If you violate one of the validation requirements, the update does not proceed and an error message is displayed above the grid.</span></span>

![hata iletisi](updating-deleting-and-creating-data/_static/image4.png)

## <a name="add-new-records"></a><span data-ttu-id="e6486-159">Yeni kayıt Ekle</span><span class="sxs-lookup"><span data-stu-id="e6486-159">Add new records</span></span>

<span data-ttu-id="e6486-160">GridView denetimi **InsertMethod** özelliğini içermez ve bu nedenle model bağlamaya sahip yeni bir kayıt eklemek için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="e6486-160">The GridView control does not include the **InsertMethod** property and therefore cannot be used for adding a new record with model binding.</span></span> <span data-ttu-id="e6486-161">InsertMethod özelliğini **FormView**, **DetailsView**veya **ListView** denetimlerinde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6486-161">You can find the InsertMethod property in the **FormView**, **DetailsView**, or **ListView** controls.</span></span> <span data-ttu-id="e6486-162">Bu öğreticide yeni bir kayıt eklemek için bir FormView denetimi kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e6486-162">In this tutorial, you will use a FormView control to add a new record.</span></span>

<span data-ttu-id="e6486-163">İlk olarak, yeni bir kayıt eklemek için oluşturacağınız yeni sayfanın bağlantısını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e6486-163">First, add a link to the new page you will create for adding a new record.</span></span> <span data-ttu-id="e6486-164">ValidationSummary üzerinde şunu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e6486-164">Above the ValidationSummary, add:</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample5.aspx)]

<span data-ttu-id="e6486-165">Yeni bağlantı öğrenciler sayfasının içeriğinin en üstünde görünür.</span><span class="sxs-lookup"><span data-stu-id="e6486-165">The new link will appear at the top of the content for the Students page.</span></span>

![Yeni bağlantı](updating-deleting-and-creating-data/_static/image5.png)

<span data-ttu-id="e6486-167">Ardından, ana sayfa kullanarak yeni bir Web formu ekleyin ve **Addöğrenci**olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="e6486-167">Then, add a new web form using a master page, and name it **AddStudent**.</span></span> <span data-ttu-id="e6486-168">Ana sayfa olarak site. Master ' u seçin.</span><span class="sxs-lookup"><span data-stu-id="e6486-168">Select Site.Master as the master page.</span></span>

<span data-ttu-id="e6486-169">**DynamicEntity** denetimini kullanarak yeni bir öğrenci eklemek için alanları oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e6486-169">You will render the fields for adding a new student by using a **DynamicEntity** control.</span></span> <span data-ttu-id="e6486-170">DynamicEntity denetimi, ItemType özelliğinde belirtilen sınıfta düzenlenebilir özellikleri işler.</span><span class="sxs-lookup"><span data-stu-id="e6486-170">The DynamicEntity control renders that editable properties in the class specified in the ItemType property.</span></span> <span data-ttu-id="e6486-171">Studentitıd özelliği, **[ScaffoldColumn (false)]** özniteliğiyle işaretlendi, bu nedenle işlenmiyor.</span><span class="sxs-lookup"><span data-stu-id="e6486-171">The StudentID property was marked with the **[ScaffoldColumn(false)]** attribute so it is not rendered.</span></span> <span data-ttu-id="e6486-172">Addöğrenci sayfasının MainContent yer tutucusuna aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e6486-172">In the MainContent placeholder of the AddStudent page, add the following code.</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample6.aspx)]

<span data-ttu-id="e6486-173">Arka plan kod dosyasında (AddStudent.aspx.cs), **Contosoüniversıtymodelbinding. model** ad alanı için bir **using** açıklaması ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e6486-173">In the code-behind file (AddStudent.aspx.cs), add a **using** statement for the **ContosoUniversityModelBinding.Models** namespace.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample7.cs)]

<span data-ttu-id="e6486-174">Ardından, iptal düğmesi için nasıl yeni bir kayıt ve olay işleyicisi ekleneceğini belirtmek üzere aşağıdaki yöntemleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e6486-174">Then, add the following methods to specify how to insert a new record and an event handler for the cancel button.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample8.cs)]

<span data-ttu-id="e6486-175">Tüm değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e6486-175">Save all of the changes.</span></span>

<span data-ttu-id="e6486-176">Web uygulamasını çalıştırın ve yeni bir öğrenci oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e6486-176">Run the web application and create a new student.</span></span>

![Yeni öğrenci Ekle](updating-deleting-and-creating-data/_static/image6.png)

<span data-ttu-id="e6486-178">**Ekle** ' ye tıklayın ve yeni öğrenciye oluşturulduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e6486-178">Click **Insert** and notice the new student has been created.</span></span>

![Yeni öğrenci görüntüle](updating-deleting-and-creating-data/_static/image7.png)

## <a name="conclusion"></a><span data-ttu-id="e6486-180">Sonuç</span><span class="sxs-lookup"><span data-stu-id="e6486-180">Conclusion</span></span>

<span data-ttu-id="e6486-181">Bu öğreticide, verileri güncelleştirme, silme ve oluşturma özelliği etkinleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e6486-181">In this tutorial, you enabled updating, deleting, and creating data.</span></span> <span data-ttu-id="e6486-182">Verilerle etkileşim kurarken doğrulama kuralları uygulanır.</span><span class="sxs-lookup"><span data-stu-id="e6486-182">You ensured validation rules are applied when interacting with the data.</span></span>

<span data-ttu-id="e6486-183">Bu serinin sonraki [öğreticide](sorting-paging-and-filtering-data.md) sıralama, sayfalama ve filtreleme verilerini etkinleştirecektir.</span><span class="sxs-lookup"><span data-stu-id="e6486-183">In the next [tutorial](sorting-paging-and-filtering-data.md) in this series, you will enable sorting, paging, and filtering data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e6486-184">[Önceki](retrieving-data.md)
> [İleri](sorting-paging-and-filtering-data.md)</span><span class="sxs-lookup"><span data-stu-id="e6486-184">[Previous](retrieving-data.md)
[Next](sorting-paging-and-filtering-data.md)</span></span>
