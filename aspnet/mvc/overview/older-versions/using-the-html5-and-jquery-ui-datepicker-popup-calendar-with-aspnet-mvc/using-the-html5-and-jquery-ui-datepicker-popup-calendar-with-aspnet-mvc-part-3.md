---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
title: ASP.NET MVC ile HTML5 ve jQuery kullanıcı arabirimi DatePicker açılan takvimini kullanma-Bölüm 3 | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici, düzenleyici şablonları, görüntüleme şablonları ve jQuery UI DatePicker açılan takvimini bir ASP.NET MV içinde nasıl çalışabileceğiniz hakkında temel bilgileri öğretir...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 8f5f91ae-12d7-4cf3-ac09-4bb53d07ee60
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
msc.type: authoredcontent
ms.openlocfilehash: b3249397e54e64538c4dc78e5fe8b94656e8962b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538908"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-3"></a><span data-ttu-id="d7439-103">ASP.NET MVC ile HTML5 ve jQuery kullanıcı arabirimi DatePicker açılan takvimini kullanma-Bölüm 3</span><span class="sxs-lookup"><span data-stu-id="d7439-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 3</span></span>

<span data-ttu-id="d7439-104">[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından</span><span class="sxs-lookup"><span data-stu-id="d7439-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="d7439-105">Bu öğreticide, bir ASP.NET MVC web uygulamasında düzenleyici şablonları, görüntüleme şablonları ve jQuery UI DatePicker açılan takvim ile çalışma hakkında temel bilgiler verilir.</span><span class="sxs-lookup"><span data-stu-id="d7439-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>

## <a name="working-with-complex-types"></a><span data-ttu-id="d7439-106">Karmaşık türlerle çalışma</span><span class="sxs-lookup"><span data-stu-id="d7439-106">Working with Complex Types</span></span>

<span data-ttu-id="d7439-107">Bu bölümde bir adres sınıfı oluşturacak ve bunu göstermek için bir şablon oluşturmayı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d7439-107">In this section you'll create an address class and learn how to create a template to display it.</span></span>

<span data-ttu-id="d7439-108">*Modeller* klasöründe, *Person.cs* adlı yeni bir sınıf dosyası oluşturun; burada iki tür koyacaksınız: bir `Person` sınıfı ve bir `Address` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="d7439-108">In the *Models* folder, create a new class file named *Person.cs* where you'll put two types: a `Person` class and an `Address` class.</span></span> <span data-ttu-id="d7439-109">`Person` sınıfı, `Address`olarak yazılmış bir özelliği içerir.</span><span class="sxs-lookup"><span data-stu-id="d7439-109">The `Person` class will contain a property that's typed as `Address`.</span></span> <span data-ttu-id="d7439-110">`Address` türü karmaşık bir türdür, yani `int`, `string`veya `double`gibi yerleşik türlerden biri değildir.</span><span class="sxs-lookup"><span data-stu-id="d7439-110">The `Address` type is a complex type, meaning it's not one of the built-in types like `int`, `string`, or `double`.</span></span> <span data-ttu-id="d7439-111">Bunun yerine, birkaç özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="d7439-111">Instead, it has several properties.</span></span> <span data-ttu-id="d7439-112">Yeni sınıfların kodu şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="d7439-112">The code for the new classes looks like this:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample1.cs)]

<span data-ttu-id="d7439-113">`Movie` denetleyicisinde, bir kişi örneğini göstermek için aşağıdaki `PersonDetail` eylemini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d7439-113">In the `Movie` controller, add the following `PersonDetail` action to display a person instance:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample2.cs)]

<span data-ttu-id="d7439-114">Sonra, `Person` modelini bazı örnek verilerle doldurmak için `Movie` denetleyicisine aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d7439-114">Then add the following code to the `Movie` controller to populate the `Person` model with some sample data:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample3.cs)]

<span data-ttu-id="d7439-115">*Views\Movies\PersonDetail.cshtml* dosyasını açın ve `PersonDetail` görünümü için aşağıdaki biçimlendirmeyi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d7439-115">Open the *Views\Movies\PersonDetail.cshtml* file and add the following markup for the `PersonDetail` view.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample4.cshtml)]

<span data-ttu-id="d7439-116">Uygulamayı çalıştırmak için CTRL + F5 tuşlarına basın ve *filmler/PersonDetail*' a gidin.</span><span class="sxs-lookup"><span data-stu-id="d7439-116">Press Ctrl+F5 to run the application and navigate to *Movies/PersonDetail*.</span></span>

<span data-ttu-id="d7439-117">Bu ekran görüntüsünde görebileceğiniz gibi `PersonDetail` görünümü `Address` karmaşık türü içermez.</span><span class="sxs-lookup"><span data-stu-id="d7439-117">The `PersonDetail` view doesn't contain the `Address` complex type, as you can see in this screenshot.</span></span> <span data-ttu-id="d7439-118">(Hiçbir adres gösterilmez.)</span><span class="sxs-lookup"><span data-stu-id="d7439-118">(No address is shown.)</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image1.png)

<span data-ttu-id="d7439-119">`Address` modeli verileri, karmaşık bir tür olduğundan görüntülenmiyor.</span><span class="sxs-lookup"><span data-stu-id="d7439-119">The `Address` model data is not displayed because it's a complex type.</span></span> <span data-ttu-id="d7439-120">Adres bilgilerini göstermek için *Views\Movies\PersonDetail.cshtml* dosyasını yeniden açın ve aşağıdaki biçimlendirmeyi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d7439-120">To display the address information, open the *Views\Movies\PersonDetail.cshtml* file again and add the following markup.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample5.cshtml)]

<span data-ttu-id="d7439-121">Şimdi `PersonDetail` görünümü için biçimlendirmenin tamamı şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="d7439-121">The complete markup for the `PersonDetail` now view looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample6.cshtml)]

<span data-ttu-id="d7439-122">Uygulamayı yeniden çalıştırın ve `PersonDetail` görünümünü görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="d7439-122">Run the application again and display the `PersonDetail` view.</span></span> <span data-ttu-id="d7439-123">Adres bilgileri artık görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="d7439-123">The address information is now displayed:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image2.png)

### <a name="creating-a-template-for-a-complex-type"></a><span data-ttu-id="d7439-124">Karmaşık bir tür için şablon oluşturma</span><span class="sxs-lookup"><span data-stu-id="d7439-124">Creating a Template for a Complex Type</span></span>

<span data-ttu-id="d7439-125">Bu bölümde, `Address` karmaşık türünü işlemek için kullanılacak bir şablon oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d7439-125">In this section you'll create a template that will be used to render the `Address` complex type.</span></span> <span data-ttu-id="d7439-126">`Address` türü için bir şablon oluşturduğunuzda, ASP.NET MVC uygulamayı uygulamanın herhangi bir yerinden bir adres modelini biçimlendirmek için otomatik olarak kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="d7439-126">When you create a template for the `Address` type, ASP.NET MVC can automatically use it to format an address model anywhere in the application.</span></span> <span data-ttu-id="d7439-127">Bu, `Address` türünün işlemeyi uygulamada tek bir yerden denetlemek için bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="d7439-127">This gives you a way to control the rendering of the `Address` type from just one place in the application.</span></span>

<span data-ttu-id="d7439-128">*Views\shared\displaytemplates* klasöründe, **Adres**adlı bir kesin türü belirtilmiş kısmi görünüm oluşturun:</span><span class="sxs-lookup"><span data-stu-id="d7439-128">In the *Views\Shared\DisplayTemplates* folder, create a strongly typed partial view named **Address**:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image3.png)

<span data-ttu-id="d7439-129">**Ekle**' ye tıklayın ve ardından yeni *Views\shared\displaytemplates\address.cshtml* dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d7439-129">Click **Add**, and then open the new *Views\Shared\DisplayTemplates\Address.cshtml* file.</span></span> <span data-ttu-id="d7439-130">Yeni görünüm aşağıdaki oluşturulan biçimlendirmeyi içerir:</span><span class="sxs-lookup"><span data-stu-id="d7439-130">The new view contains the following generated markup:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample7.cshtml)]

<span data-ttu-id="d7439-131">Uygulamayı çalıştırın ve `PersonDetail` görünümünü görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="d7439-131">Run the application and display the `PersonDetail` view.</span></span> <span data-ttu-id="d7439-132">Bu kez, yeni oluşturduğunuz `Address` şablonu `Address` karmaşık türü göstermek için kullanılır; bu nedenle, ekran aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="d7439-132">This time, the `Address` template that you just created is used to display the `Address` complex type, so the display looks like the following:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image4.png)

### <a name="summary-ways-to-specify-the-model-display-format-and-template"></a><span data-ttu-id="d7439-133">Özet: model görüntüleme biçimini ve şablonu belirtme yolları</span><span class="sxs-lookup"><span data-stu-id="d7439-133">Summary: Ways to Specify the Model Display Format and Template</span></span>

<span data-ttu-id="d7439-134">Aşağıdaki yaklaşımlardan birini kullanarak bir model özelliğinin biçimini veya şablonunu belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d7439-134">You've seen that you can specify the format or template for a model property by using the following approaches:</span></span>

- <span data-ttu-id="d7439-135">`DisplayFormat` özniteliği modeldeki bir özelliğe uygulanıyor.</span><span class="sxs-lookup"><span data-stu-id="d7439-135">Applying the `DisplayFormat` attribute to a property in the model.</span></span> <span data-ttu-id="d7439-136">Örneğin, aşağıdaki kod, tarihin zaman olmadan görüntülenmesine neden olur:</span><span class="sxs-lookup"><span data-stu-id="d7439-136">For example, the following code causes the date to be displayed without the time:</span></span>

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample8.cs)]
- <span data-ttu-id="d7439-137">Modeldeki bir özelliğe bir [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) özniteliği uygulama ve veri türünü belirtme.</span><span class="sxs-lookup"><span data-stu-id="d7439-137">Applying a [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute to a property in the model and specifying the data type.</span></span> <span data-ttu-id="d7439-138">Örneğin, aşağıdaki kod, tarihin zaman olmadan görüntülenmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="d7439-138">For example, the following code causes the date to be displayed without the time.</span></span>

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample9.cs)]

    <span data-ttu-id="d7439-139">Uygulama *Views\shared\displaytemplates* klasöründe veya *Views\Movies\DisplayTemplates* klasöründe *date. cshtml* şablonu içeriyorsa, bu şablon `DateTime` özelliğini işlemek için kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="d7439-139">If the application contains a *date.cshtml* template in the *Views\Shared\DisplayTemplates* folder or the *Views\Movies\DisplayTemplates* folder, that template will be used to render the `DateTime` property.</span></span> <span data-ttu-id="d7439-140">Aksi halde, yerleşik ASP.NET şablon oluşturma sistemi, bir tarih olarak özelliği görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d7439-140">Otherwise the built-in ASP.NET templating system displays the property as a date.</span></span>
- <span data-ttu-id="d7439-141">*Views\shared\displaytemplates* klasöründe veya adı biçimlendirmek istediğiniz veri türüyle eşleşen *Views\Movies\DisplayTemplates* klasöründe bir görüntüleme şablonu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="d7439-141">Creating a display template in the *Views\Shared\DisplayTemplates* folder or the *Views\Movies\DisplayTemplates* folder whose name matches the data type that you want to format.</span></span> <span data-ttu-id="d7439-142">Örneğin, model için bir öznitelik eklemeden ve görünümlere herhangi bir biçimlendirme eklemeden, bir modeldeki `DateTime` özellikleri işlemek için *Views\shared\displaytemplates\datetime.exe* kullanıldığını gördünüz.</span><span class="sxs-lookup"><span data-stu-id="d7439-142">For example, you saw that the *Views\Shared\DisplayTemplates\DateTime.cshtml* was used to render `DateTime` properties in a model, without adding an attribute to the model and without adding any markup to views.</span></span>
- <span data-ttu-id="d7439-143">Model özelliğinin görüntüleneceği şablonu belirtmek için modelde [Uııınt](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) özniteliği kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="d7439-143">Using the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute on the model to specify the template to display the model property.</span></span>
- <span data-ttu-id="d7439-144">Görüntüleme şablonu adını, bir görünümdeki çağrı [Için HTML. displayto](https://msdn.microsoft.com/library/ee407420.aspx) 'a açıkça ekleme.</span><span class="sxs-lookup"><span data-stu-id="d7439-144">Explicitly adding the display template name to the [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) call in a view.</span></span>

<span data-ttu-id="d7439-145">Kullandığınız yaklaşım, uygulamanızda ne yapmanız gerektiği konusunda farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="d7439-145">The approach you use depends on what you need to do in your application.</span></span> <span data-ttu-id="d7439-146">Tam olarak ihtiyacınız olan biçimlendirme türünü almak için bu yaklaşımların karıştığı yaygın olmayan bir durumdur.</span><span class="sxs-lookup"><span data-stu-id="d7439-146">It's not uncommon to mix these approaches to get exactly the kind of formatting that you need.</span></span>

<span data-ttu-id="d7439-147">Sonraki bölümde, bir bit olarak geçiş yapar ve verilerin nasıl girildiğini özelleştirmek için verilerin nasıl görüntülendiğini özelleştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7439-147">In the next section, you'll switch gears a bit and move from customizing how data is displayed to customizing how it's entered.</span></span> <span data-ttu-id="d7439-148">Tarihleri belirtmek için bir yol yolu sağlamak üzere uygulamadaki düzenleme görünümlerine jQuery DatePicker ' i kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d7439-148">You'll hook up the jQuery datepicker to the edit views in the application in order to provide a slick way to specify dates.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d7439-149">[Önceki](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
> [İleri](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="d7439-149">[Previous](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
[Next](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)</span></span>
