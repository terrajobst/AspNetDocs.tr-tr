---
uid: web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
title: JQuery UI DatePicker model bağlama ve Web formlarıyla tümleştirme | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir. Model bağlama, veri etkileşimini daha düz-... hale getirir
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 3cbab37b-fb0f-4751-9ec4-74e068c3f380
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: c8d711dd44950116f3a3e09d5d12c507918c543f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78642480"
---
# <a name="integrating-jquery-ui-datepicker-with-model-binding-and-web-forms"></a><span data-ttu-id="8bd62-104">JQuery UI DatePicker model bağlama ve Web formlarıyla tümleştirme</span><span class="sxs-lookup"><span data-stu-id="8bd62-104">Integrating JQuery UI Datepicker with model binding and web forms</span></span>

<span data-ttu-id="8bd62-105">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="8bd62-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="8bd62-106">Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="8bd62-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="8bd62-107">Model bağlama veri kaynağı nesneleriyle (örneğin, ObjectDataSource veya SqlDataSource) çok daha basit hale getirir.</span><span class="sxs-lookup"><span data-stu-id="8bd62-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="8bd62-108">Bu seri giriş malzemesiyle başlar ve sonraki öğreticilerde daha gelişmiş kavramlara gider.</span><span class="sxs-lookup"><span data-stu-id="8bd62-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="8bd62-109">Bu öğretici, JQuery UI [DatePicker pencere](http://jqueryui.com/datepicker/) öğesinin bir Web formuna nasıl ekleneceğini ve veritabanını seçili değerle güncellemek için model bağlamayı nasıl kullanacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="8bd62-109">This tutorial shows how to add the JQuery UI [Datepicker widget](http://jqueryui.com/datepicker/) to a Web Form, and use model binding to update the database with the selected value.</span></span>
> 
> <span data-ttu-id="8bd62-110">Bu öğreticide, serinin [Birinci](retrieving-data.md) ve [ikinci](updating-deleting-and-creating-data.md) bölümlerinde oluşturulan projede derleme yapılır.</span><span class="sxs-lookup"><span data-stu-id="8bd62-110">This tutorial builds on the project created in the [first](retrieving-data.md) and [second](updating-deleting-and-creating-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="8bd62-111">Tüm projeyi [](https://go.microsoft.com/fwlink/?LinkId=286116) C# veya vb 'ye indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bd62-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="8bd62-112">İndirilebilir kod, Visual Studio 2012 veya Visual Studio 2013 ile birlikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8bd62-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="8bd62-113">Bu öğreticide gösterilen Visual Studio 2013 şablonundan biraz farklı olan Visual Studio 2012 şablonunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="8bd62-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="8bd62-114">Ne oluşturacağız?</span><span class="sxs-lookup"><span data-stu-id="8bd62-114">What you'll build</span></span>

<span data-ttu-id="8bd62-115">Bu öğreticide şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8bd62-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="8bd62-116">Öğrencinin kayıt tarihini kaydetmek için modelinize bir özellik ekleyin</span><span class="sxs-lookup"><span data-stu-id="8bd62-116">Add a property to your model to record the student's enrollment date</span></span>
2. <span data-ttu-id="8bd62-117">Kullanıcının JQuery Kullanıcı arabirimi DatePicker pencere öğesini kullanarak kayıt tarihini seçmesini sağlama</span><span class="sxs-lookup"><span data-stu-id="8bd62-117">Enable the user to select the enrollment date using the JQuery UI Datepicker widget</span></span>
3. <span data-ttu-id="8bd62-118">Kayıt tarihi için doğrulama kurallarını zorla</span><span class="sxs-lookup"><span data-stu-id="8bd62-118">Enforce validation rules for the enrollment date</span></span>

<span data-ttu-id="8bd62-119">JQuery kullanıcı ARABIRIMI DatePicker pencere öğesi, kullanıcıların alanla etkileşime geçtiğinde bir takvimden bir tarihi kolayca seçmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="8bd62-119">The JQuery UI Datepicker widget enables users to easily select a date from a calendar that pops up when the user interacts with the field.</span></span> <span data-ttu-id="8bd62-120">Bu pencere öğesinin kullanılması, kullanıcıların el ile tarih yazmakla daha kullanışlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8bd62-120">Using this widget can be more convenient for users than manually typing a date.</span></span> <span data-ttu-id="8bd62-121">DatePicker pencere öğesini, veri işlemleri için model bağlama kullanan bir sayfayla tümleştirmek yalnızca az miktarda ek iş gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8bd62-121">Integrating the Datepicker widget into a page that uses model binding for data operations requires only a small amount of additional work.</span></span>

## <a name="add-a-new-property-to-the-model"></a><span data-ttu-id="8bd62-122">Modele yeni bir özellik ekleyin</span><span class="sxs-lookup"><span data-stu-id="8bd62-122">Add a new property to the model</span></span>

<span data-ttu-id="8bd62-123">İlk olarak, öğrenci modelinize bir **DateTime** özelliği ekleyecek ve bu değişikliği veritabanına geçirecaksınız.</span><span class="sxs-lookup"><span data-stu-id="8bd62-123">First, you will add a **Datetime** property to your Student model and migrate that change to the database.</span></span> <span data-ttu-id="8bd62-124">**UniversityModels.cs**' yi açın ve vurgulanan kodu öğrenci modeline ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8bd62-124">Open **UniversityModels.cs**, and add the highlighted code to the Student model.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample1.cs?highlight=16-18)]

<span data-ttu-id="8bd62-125">**RangeAttribute** , özelliği için doğrulama kurallarını zorlamak için eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="8bd62-125">The **RangeAttribute** is included to enforce validation rules for the property.</span></span> <span data-ttu-id="8bd62-126">Bu öğreticide, Contoso University 'in 1 Ocak 2013 ' de yer aldığı ve bu nedenle daha önceki kayıt tarihlerinin geçerli olmadığı varsayıyoruz.</span><span class="sxs-lookup"><span data-stu-id="8bd62-126">For this tutorial, we will assume that Contoso University was founded on January 1st, 2013 and therefore earlier enrollment dates are not valid.</span></span>

<span data-ttu-id="8bd62-127">Paket Yönetimi penceresinde, **Add-Migration AddEnrollmentDate**komutunu çalıştırarak bir geçiş ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8bd62-127">In the Package Management window, add a migration by running the command **add-migration AddEnrollmentDate**.</span></span> <span data-ttu-id="8bd62-128">Geçiş kodunun yeni tarih saat sütununu öğrenci tablosuna eklediğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="8bd62-128">Notice that the migration code adds the new Datetime column to the Student table.</span></span> <span data-ttu-id="8bd62-129">RangeAttribute içinde belirttiğiniz değeri eşleştirmek için, aşağıdaki vurgulanan kodda gösterildiği gibi yeni sütun için varsayılan bir değer ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8bd62-129">To match the value you specified in the RangeAttribute, add a default value for the new column, as shown in the highlighted code below.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample2.cs?highlight=11)]

<span data-ttu-id="8bd62-130">Değişiklerinizi geçiş dosyasına kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8bd62-130">Save your change to the migration file.</span></span>

<span data-ttu-id="8bd62-131">Verileri yeniden temel almanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="8bd62-131">You do not need to seed the data again.</span></span> <span data-ttu-id="8bd62-132">Bu nedenle, geçişler klasöründe **Configuration.cs** açın ve **çekirdek** yöntemindeki kodu kaldırın veya not edin.</span><span class="sxs-lookup"><span data-stu-id="8bd62-132">Therefore, open **Configuration.cs** in the Migrations folder and remove or comment out the code in the **Seed** method.</span></span> <span data-ttu-id="8bd62-133">Dosyayı kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="8bd62-133">Save and close the file.</span></span>

<span data-ttu-id="8bd62-134">Şimdi, **Update-Database**komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8bd62-134">Now, run the command **update-database**.</span></span> <span data-ttu-id="8bd62-135">Sütunun artık veritabanında var olduğunu ve var olan tüm kayıtların kayıt tarihi için varsayılan değere sahip olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="8bd62-135">Notice that the column now exists in the database and all of the existing records have the default value for EnrollmentDate.</span></span>

## <a name="add-dynamic-controls-for-enrollment-date"></a><span data-ttu-id="8bd62-136">Kayıt tarihi için dinamik denetimler ekleme</span><span class="sxs-lookup"><span data-stu-id="8bd62-136">Add dynamic controls for enrollment date</span></span>

<span data-ttu-id="8bd62-137">Şimdi kayıt tarihini görüntüleme ve düzenlemeyle ilgili denetimler ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="8bd62-137">You will now add controls for displaying and editing the enrollment date.</span></span> <span data-ttu-id="8bd62-138">Bu noktada, değer bir metin kutusuyla düzenlenir.</span><span class="sxs-lookup"><span data-stu-id="8bd62-138">At this point, the value is edited through a text box.</span></span> <span data-ttu-id="8bd62-139">Öğreticide daha sonra, metin kutusunu JQuery DatePicker pencere öğesi olarak değiştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bd62-139">Later in the tutorial, you will change the text box to the JQuery Datepicker widget.</span></span>

<span data-ttu-id="8bd62-140">İlk olarak, **Addstudent. aspx** dosyasında herhangi bir değişiklik yapmanız gerekmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8bd62-140">First, it is important to note that you do not need to make any change to the **AddStudent.aspx** file.</span></span> <span data-ttu-id="8bd62-141">DynamicEntity denetimi, yeni özelliği otomatik olarak işler.</span><span class="sxs-lookup"><span data-stu-id="8bd62-141">The DynamicEntity control will automatically render the new property.</span></span>

<span data-ttu-id="8bd62-142">**Öğrenciler. aspx**' i açın ve aşağıdaki vurgulanmış kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8bd62-142">Open **Students.aspx**, and add the following highlighted code.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample3.aspx?highlight=13)]

<span data-ttu-id="8bd62-143">Uygulamayı çalıştırın ve bir tarih yazarak kayıt tarihinin değerini ayarlayabildiğinize dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="8bd62-143">Run the application and notice that you can set the value of the enrollment date by typing a date.</span></span> <span data-ttu-id="8bd62-144">Yeni öğrenci eklerken:</span><span class="sxs-lookup"><span data-stu-id="8bd62-144">When adding a new student:</span></span>

![tarihi ayarla](integrating-jquery-ui/_static/image1.png)

<span data-ttu-id="8bd62-146">Ya da varolan bir değeri düzenleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8bd62-146">Or, editing an existing value:</span></span>

![tarihi Düzenle](integrating-jquery-ui/_static/image2.png)

<span data-ttu-id="8bd62-148">Çalışma tarihi yazılması, ancak sağlamak istediğiniz müşteri deneyimi olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="8bd62-148">Typing the date works, but it might not be the customer experience you wish to provide.</span></span> <span data-ttu-id="8bd62-149">Sonraki bölümde, bir takvim üzerinden tarih seçmeyi etkinleştirecektir.</span><span class="sxs-lookup"><span data-stu-id="8bd62-149">In the next section, you will enable selecting a date through a calendar.</span></span>

## <a name="install-nuget-package-to-work-with-jquery-ui"></a><span data-ttu-id="8bd62-150">JQuery Kullanıcı arabirimi ile çalışmak için NuGet paketini yükler</span><span class="sxs-lookup"><span data-stu-id="8bd62-150">Install NuGet package to work with JQuery UI</span></span>

<span data-ttu-id="8bd62-151">Bu **Kullanıcı arabirimi** NuGet paketi, jQuery kullanıcı arabirimi Pencere öğelerinin Web uygulamanıza kolay bir şekilde tümleştirilmesini sunar.</span><span class="sxs-lookup"><span data-stu-id="8bd62-151">The **Juice UI** NuGet package enables easy integration of the JQuery UI widgets into your web application.</span></span> <span data-ttu-id="8bd62-152">Bu paketi kullanmak için NuGet aracılığıyla yükleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bd62-152">To use this package, install it through NuGet.</span></span>

![SBU Kullanıcı arabirimi Ekle](integrating-jquery-ui/_static/image3.png)

<span data-ttu-id="8bd62-154">Yüklediğiniz bu kullanıcı arabirimi sürümü uygulamanızdaki JQuery sürümü ile çakışabilir.</span><span class="sxs-lookup"><span data-stu-id="8bd62-154">The version of Juice UI that you install may conflict with the version of JQuery in your application.</span></span> <span data-ttu-id="8bd62-155">Bu öğreticiye devam etmeden önce, uygulamanızı çalıştırmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="8bd62-155">Before proceeding with this tutorial, try running your application.</span></span> <span data-ttu-id="8bd62-156">JavaScript hatasıyla karşılaşırsanız, JQuery sürümünü bağdaştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bd62-156">If you encounter a JavaScript error, you need to reconcile the JQuery version.</span></span> <span data-ttu-id="8bd62-157">JQuery 'in beklenen sürümünü Scripts klasörünüze (Bu öğreticiyi yazma sırasında sürüm 1.8.2) veya sitesinde ekleyebilirsiniz. Master JQuery dosyasının yolunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="8bd62-157">You can either add the expected version of JQuery to your Scripts folder (version 1.8.2 at time of writing this tutorial), or in Site.master specify the path to the JQuery file.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample4.aspx)]

## <a name="customize-datetime-template-to-include-datepicker-widget"></a><span data-ttu-id="8bd62-158">DateTime şablonunu DatePicker pencere öğesini içerecek şekilde özelleştirme</span><span class="sxs-lookup"><span data-stu-id="8bd62-158">Customize DateTime template to include Datepicker widget</span></span>

<span data-ttu-id="8bd62-159">DatePicker pencere öğesini dinamik veri şablonuna ekleyerek bir tarih saat değerini düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bd62-159">You will add the Datepicker widget to the dynamic data template for editing a datetime value.</span></span> <span data-ttu-id="8bd62-160">Pencere öğesini şablona ekleyerek, otomatik olarak yeni öğrenci ekleme ve öğrencilerin düzenlenmesine yönelik kılavuz görünümünde otomatik olarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="8bd62-160">By adding the widget to the template, it is automatically rendered in both the form for adding a new student and in the grid view for editing students.</span></span> <span data-ttu-id="8bd62-161">**Tarih/saat\_açın. ascx**' i düzenleyin ve aşağıdaki vurgulanmış kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8bd62-161">Open **DateTime\_Edit.ascx**, and add the following highlighted code.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample5.aspx?highlight=3)]

<span data-ttu-id="8bd62-162">Arka plan kod dosyasında, DatePicker için en düşük ve en büyük tarihleri ayarlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="8bd62-162">In the code-behind file, you will set the minimum and maximum dates for the DatePicker.</span></span> <span data-ttu-id="8bd62-163">Bu değerleri ayarlayarak, kullanıcıların geçersiz tarihlere gitmesini önleyecaksınız.</span><span class="sxs-lookup"><span data-stu-id="8bd62-163">By setting these values, you will prevent users from navigating to invalid dates.</span></span> <span data-ttu-id="8bd62-164">Tarih saat özelliğindeki en düşük ve en yüksek değerleri, varsa DateTime özelliğinde elde edersiniz.</span><span class="sxs-lookup"><span data-stu-id="8bd62-164">You will retrieve the minimum and maximum values from the **RangeAttribute** on the DateTime property, if one is provided.</span></span> <span data-ttu-id="8bd62-165">**DateTime\_Edit.ascx.cs**açın ve sayfa\_Load yöntemine aşağıdaki vurgulanmış kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8bd62-165">Open **DateTime\_Edit.ascx.cs**, and add the following highlighted code to the Page\_Load method.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample6.cs?highlight=9-14)]

<span data-ttu-id="8bd62-166">Web uygulamasını çalıştırın ve Addöğrenci sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="8bd62-166">Run the web application and navigate to the AddStudent page.</span></span> <span data-ttu-id="8bd62-167">Alanlar için değerler sağlayın ve kayıt tarihi için metin kutusuna tıkladığınızda takvimin görüntülendiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8bd62-167">Provide values for the fields and notice that when you click on the text box for Enrollment Date, the calendar is displayed.</span></span>

![Tarih Seçici](integrating-jquery-ui/_static/image4.png)

<span data-ttu-id="8bd62-169">Bir tarih seçin ve **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bd62-169">Pick a date, and click **Insert**.</span></span> <span data-ttu-id="8bd62-170">RangeAttribute, sunucuda doğrulamayı zorlar.</span><span class="sxs-lookup"><span data-stu-id="8bd62-170">The RangeAttribute enforces validation on the server.</span></span> <span data-ttu-id="8bd62-171">DatePicker üzerinde minDate özelliğini ayarlayarak, istemciye doğrulama de uygularsınız.</span><span class="sxs-lookup"><span data-stu-id="8bd62-171">By setting the minDate property on the Datepicker, you also apply validation on the client.</span></span> <span data-ttu-id="8bd62-172">Takvim, kullanıcının minDate değerinden önceki bir tarihe gitmasına izin vermez.</span><span class="sxs-lookup"><span data-stu-id="8bd62-172">The calendar does not let the user navigate to a date prior to the value of minDate.</span></span>

<span data-ttu-id="8bd62-173">Kılavuz görünümünde bir kayıt düzenlediğinizde, takvim de görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8bd62-173">When you edit a record in the grid view, the calendar is also displayed.</span></span>

![GridView 'da DatePicker](integrating-jquery-ui/_static/image5.png)

## <a name="conclusion"></a><span data-ttu-id="8bd62-175">Sonuç</span><span class="sxs-lookup"><span data-stu-id="8bd62-175">Conclusion</span></span>

<span data-ttu-id="8bd62-176">Bu öğreticide, bir JQuery pencere öğesini model bağlama kullanan bir Web formuna nasıl ekleyeceğinizi öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="8bd62-176">In this tutorial, you learned how to incorporate a JQuery widget into a web form that uses model binding.</span></span>

<span data-ttu-id="8bd62-177">Sonraki [öğreticide](using-query-string-values-to-retrieve-data.md), veri seçerken bir sorgu dizesi değeri kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="8bd62-177">In the next [tutorial](using-query-string-values-to-retrieve-data.md), you will use a query string value when selecting data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8bd62-178">[Önceki](sorting-paging-and-filtering-data.md)
> [İleri](using-query-string-values-to-retrieve-data.md)</span><span class="sxs-lookup"><span data-stu-id="8bd62-178">[Previous](sorting-paging-and-filtering-data.md)
[Next](using-query-string-values-to-retrieve-data.md)</span></span>
