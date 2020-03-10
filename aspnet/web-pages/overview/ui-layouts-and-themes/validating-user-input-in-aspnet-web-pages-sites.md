---
uid: web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
title: ASP.NET Web Pages (Razor) sitelerindeki kullanıcı girişini doğrulama | Microsoft Docs
author: Rick-Anderson
description: Bu makalede, kullanıcıların HTML formlarında bir AS... içinde geçerli bilgiler girdiğinizden emin olmak için &mdash;, kullanıcılardan aldığınız bilgilerin nasıl doğrulanacağı açıklanmaktadır.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 4eb060cc-cf14-41ae-bab1-14a2c15332d0
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: e6f8e1051d09d11f1756bfada44a73ba7c2a1db2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563506"
---
# <a name="validating-user-input-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="bfe93-103">ASP.NET Web Pages (Razor) sitelerindeki kullanıcı girişini doğrulama</span><span class="sxs-lookup"><span data-stu-id="bfe93-103">Validating User Input in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="bfe93-104">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="bfe93-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="bfe93-105">Bu makalede, kullanıcıların bir ASP.NET Web Pages (Razor) sitesinde HTML formlarında geçerli bilgiler girdiğinizden emin olmak için &mdash;, kullanıcılardan aldığınız bilgilerin nasıl doğrulanacağı anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="bfe93-105">This article discusses how to validate information you get from users &mdash; that is, to make sure that users enter valid information in HTML forms in an ASP.NET Web Pages (Razor) site.</span></span>
> 
> <span data-ttu-id="bfe93-106">Öğrenecekleriniz:</span><span class="sxs-lookup"><span data-stu-id="bfe93-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="bfe93-107">Kullanıcı girişinin tanımladığınız doğrulama ölçütleriyle eşleşip eşleşmediğini denetleme.</span><span class="sxs-lookup"><span data-stu-id="bfe93-107">How to check that a user's input matches validation criteria that you define.</span></span>
> - <span data-ttu-id="bfe93-108">Tüm doğrulama testlerinin başarılı olup olmadığını belirleme.</span><span class="sxs-lookup"><span data-stu-id="bfe93-108">How to determine whether all validation tests have passed.</span></span>
> - <span data-ttu-id="bfe93-109">Doğrulama hatalarını görüntüleme (ve bunları biçimlendirme).</span><span class="sxs-lookup"><span data-stu-id="bfe93-109">How to display validation errors (and how to format them).</span></span>
> - <span data-ttu-id="bfe93-110">Doğrudan kullanıcılardan gelmeyen verileri doğrulama.</span><span class="sxs-lookup"><span data-stu-id="bfe93-110">How to validate data that doesn't come directly from users.</span></span>
> 
> <span data-ttu-id="bfe93-111">Makalesinde sunulan ASP.NET programlama kavramları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="bfe93-111">These are the ASP.NET programming concepts introduced in the article:</span></span>
> 
> - <span data-ttu-id="bfe93-112">`Validation` Yardımcısı.</span><span class="sxs-lookup"><span data-stu-id="bfe93-112">The `Validation` helper.</span></span>
> - <span data-ttu-id="bfe93-113">`Html.ValidationSummary` ve `Html.ValidationMessage` yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="bfe93-113">The `Html.ValidationSummary` and `Html.ValidationMessage` methods.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="bfe93-114">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="bfe93-114">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="bfe93-115">ASP.NET Web sayfaları (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="bfe93-115">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="bfe93-116">Bu öğretici, ASP.NET Web Pages 2 ile de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-116">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<span data-ttu-id="bfe93-117">Bu makale aşağıdaki bölümleri içerir:</span><span class="sxs-lookup"><span data-stu-id="bfe93-117">This article contains the following sections:</span></span>

- [<span data-ttu-id="bfe93-118">Kullanıcı girişi doğrulamasına genel bakış</span><span class="sxs-lookup"><span data-stu-id="bfe93-118">Overview of User Input Validation</span></span>](#Overview_of_User_Input_Validation)
- [<span data-ttu-id="bfe93-119">Kullanıcı girişini doğrulama</span><span class="sxs-lookup"><span data-stu-id="bfe93-119">Validating User Input</span></span>](#Validating_User_Input)
- [<span data-ttu-id="bfe93-120">Istemci tarafı doğrulama ekleme</span><span class="sxs-lookup"><span data-stu-id="bfe93-120">Adding Client-Side Validation</span></span>](#Adding_Client-Side_Validation)
- [<span data-ttu-id="bfe93-121">Doğrulama hatalarını biçimlendirme</span><span class="sxs-lookup"><span data-stu-id="bfe93-121">Formatting Validation Errors</span></span>](#Formatting_Validation_Errors)
- [<span data-ttu-id="bfe93-122">Doğrudan kullanıcılardan gelmeyen verileri doğrulama</span><span class="sxs-lookup"><span data-stu-id="bfe93-122">Validating Data That Doesn't Come Directly from Users</span></span>](#Validating_Data_That_Doesnt_Come_Directly_from_Users)

<a id="Overview_of_User_Input_Validation"></a>
## <a name="overview-of-user-input-validation"></a><span data-ttu-id="bfe93-123">Kullanıcı girişi doğrulamasına genel bakış</span><span class="sxs-lookup"><span data-stu-id="bfe93-123">Overview of User Input Validation</span></span>

<span data-ttu-id="bfe93-124">Kullanıcılardan bir sayfaya bilgi girmesini isteme (örneğin, bir forma), girdikleri değerlerin geçerli olduğundan emin olmak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-124">If you ask users to enter information in a page — for example, into a form — it's important to make sure that the values that they enter are valid.</span></span> <span data-ttu-id="bfe93-125">Örneğin, kritik bilgileri eksik olan bir formu işlemek istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="bfe93-125">For example, you don't want to process a form that's missing critical information.</span></span>

<span data-ttu-id="bfe93-126">Kullanıcılar bir HTML biçimine değer girerken, girdikleri değerler dizelerdir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-126">When users enter values into an HTML form, the values that they enter are strings.</span></span> <span data-ttu-id="bfe93-127">Çoğu durumda, ihtiyacınız olan değerler, tamsayılar veya tarihler gibi bazı diğer veri türleridir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-127">In many cases, the values you need are some other data types, like integers or dates.</span></span> <span data-ttu-id="bfe93-128">Bu nedenle, kullanıcıların girebileceği değerlerin uygun veri türlerine doğru şekilde dönüştürülebileceğinden de emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-128">Therefore, you also have to make sure that the values that users enter can be correctly converted to the appropriate data types.</span></span>

<span data-ttu-id="bfe93-129">Ayrıca, değerler üzerinde belirli kısıtlamalara de sahip olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bfe93-129">You might also have certain restrictions on the values.</span></span> <span data-ttu-id="bfe93-130">Kullanıcılar, örneğin, doğru bir tamsayı girse bile, değerin belirli bir aralık dahilinde olduğundan emin olmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-130">Even if users correctly enter an integer, for example, you might need to make sure that the value falls within a certain range.</span></span>

![CSS stil sınıflarını kullanan doğrulama hataları](validating-user-input-in-aspnet-web-pages-sites/_static/image1.png)

> [!NOTE] 
> 
> <span data-ttu-id="bfe93-132">**Önemli** Güvenlik için Kullanıcı girişinin doğrulanması da önemlidir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-132">**Important** Validating user input is also important for security.</span></span> <span data-ttu-id="bfe93-133">Kullanıcıların formlara girebilen değerleri kısıtladığınızda, birisinin sitenizin güvenliğini tehlikeye atabilecek bir değer girebilme olasılığını azaltırsınız.</span><span class="sxs-lookup"><span data-stu-id="bfe93-133">When you restrict the values that users can enter in forms, you reduce the chance that someone can enter a value that can compromise the security of your site.</span></span>

<a id="Validating_User_Input"></a>
## <a name="validating-user-input"></a><span data-ttu-id="bfe93-134">Kullanıcı girişini doğrulama</span><span class="sxs-lookup"><span data-stu-id="bfe93-134">Validating User Input</span></span>

<span data-ttu-id="bfe93-135">ASP.NET Web Pages 2 ' de, Kullanıcı girişini sınamak için `Validator` yardımcısını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bfe93-135">In ASP.NET Web Pages 2, you can use the `Validator` helper to test user input.</span></span> <span data-ttu-id="bfe93-136">Temel yaklaşım şunlardır:</span><span class="sxs-lookup"><span data-stu-id="bfe93-136">The basic approach is to do the following:</span></span>

1. <span data-ttu-id="bfe93-137">Hangi giriş öğelerinin (alanları) doğrulamak istediğinizi saptayın.</span><span class="sxs-lookup"><span data-stu-id="bfe93-137">Determine which input elements (fields) you want to validate.</span></span>

    <span data-ttu-id="bfe93-138">Genellikle bir formdaki `<input>` öğelerdeki değerleri doğrularsınız.</span><span class="sxs-lookup"><span data-stu-id="bfe93-138">You typically validate values in `<input>` elements in a form.</span></span> <span data-ttu-id="bfe93-139">Ancak, `<select>` listesi gibi kısıtlanmış bir öğeden gelen tüm giriş, hatta girişi doğrulamak iyi bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="bfe93-139">However, it's a good practice to validate all input, even input that comes from a constrained element like a `<select>` list.</span></span> <span data-ttu-id="bfe93-140">Bu, kullanıcıların bir sayfadaki denetimleri atlayıp form gönderemeyeceği konusunda emin olmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="bfe93-140">This helps to make sure that users don't bypass the controls on a page and submit a form.</span></span>
2. <span data-ttu-id="bfe93-141">Sayfa kodunda, `Validation` Yardımcısı yöntemlerini kullanarak her giriş öğesi için ayrı doğrulama denetimleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bfe93-141">In the page code, add individual validation checks for each input element by using methods of the `Validation` helper.</span></span>

    <span data-ttu-id="bfe93-142">Gerekli alanları denetlemek için `Validation.RequireField(field, [error message])` (tek bir alan için) veya `Validation.RequireFields(field1, field2, ...))` (alanların listesi için) kullanın.</span><span class="sxs-lookup"><span data-stu-id="bfe93-142">To check for required fields, use `Validation.RequireField(field, [error message])` (for an individual field) or `Validation.RequireFields(field1, field2, ...))` (for a list of fields).</span></span> <span data-ttu-id="bfe93-143">Diğer doğrulama türleri için `Validation.Add(field, ValidationType)`kullanın.</span><span class="sxs-lookup"><span data-stu-id="bfe93-143">For other types of validation, use `Validation.Add(field, ValidationType)`.</span></span> <span data-ttu-id="bfe93-144">`ValidationType`için aşağıdaki seçenekleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bfe93-144">For `ValidationType`, you can use these options:</span></span>

    `Validator.DateTime ([error message])`  
   `Validator.Decimal([error message])`  
   `Validator.EqualsTo(otherField [, error message])`  
   `Validator.Float([error message])`  
   `Validator.Integer([error message])`  
   `Validator.Range(min, max [, error message])`  
   `Validator.RegEx(pattern [, error message])`  
   `Validator.Required([error message])`  
   `Validator.StringLength(length)`  
   `Validator.Url([error message])`
3. <span data-ttu-id="bfe93-145">Sayfa gönderildiğinde doğrulamanın `Validation.IsValid`denetleyerek başarılı olup olmadığını denetleyin:</span><span class="sxs-lookup"><span data-stu-id="bfe93-145">When the page is submitted, check whether validation has passed by checking `Validation.IsValid`:</span></span>

    [!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample1.cs)]

    <span data-ttu-id="bfe93-146">Herhangi bir doğrulama hatası varsa, normal sayfa işlemeyi atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bfe93-146">If there are any validation errors, you skip normal page processing.</span></span> <span data-ttu-id="bfe93-147">Örneğin, sayfanın amacı bir veritabanını güncelleştirmediğinde, tüm doğrulama hataları düzeltilene kadar bunu yapmayın.</span><span class="sxs-lookup"><span data-stu-id="bfe93-147">For example, if the purpose of the page is to update a database, you don't do that until all validation errors have been fixed.</span></span>
4. <span data-ttu-id="bfe93-148">Doğrulama hataları varsa, `Html.ValidationSummary` veya `Html.ValidationMessage`veya her ikisini de kullanarak sayfa biçimlendirmesinde hata iletilerini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="bfe93-148">If there are validation errors, display error messages in the page's markup by using `Html.ValidationSummary` or `Html.ValidationMessage`, or both.</span></span>

<span data-ttu-id="bfe93-149">Aşağıdaki örnekte, bu adımları gösteren bir sayfa gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-149">The following example shows a page that illustrates these steps.</span></span>

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample2.cshtml)]

<span data-ttu-id="bfe93-150">Doğrulamanın nasıl çalıştığını görmek için bu sayfayı çalıştırın ve bilinçli olarak hata oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bfe93-150">To see how validation works, run this page and deliberately make mistakes.</span></span> <span data-ttu-id="bfe93-151">Örneğin, bir kurs adı girmeyi unuttuğunuzda, bir, girdiğinizde ve geçersiz bir tarih girerseniz, sayfa şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="bfe93-151">For example, here's what the page looks like if you forget to enter a course name, if you enter an, and if you enter an invalid date:</span></span>

![İşlenmiş sayfada doğrulama hataları](validating-user-input-in-aspnet-web-pages-sites/_static/image2.png)

<a id="Adding_Client-Side_Validation"></a>
## <a name="adding-client-side-validation"></a><span data-ttu-id="bfe93-153">Istemci tarafı doğrulama ekleme</span><span class="sxs-lookup"><span data-stu-id="bfe93-153">Adding Client-Side Validation</span></span>

<span data-ttu-id="bfe93-154">Varsayılan olarak, Kullanıcı girişi, kullanıcılar sayfayı gönderdikten sonra onaylanır — diğer bir deyişle, doğrulama sunucu kodunda gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-154">By default, user input is validated after users submit the page — that is, the validation is performed in server code.</span></span> <span data-ttu-id="bfe93-155">Bu yaklaşımın bir dezavantajı, kullanıcıların sayfayı gönderdikten sonra bir hata yaptığını bilmez.</span><span class="sxs-lookup"><span data-stu-id="bfe93-155">A disadvantage of this approach is that users don't know that they've made an error until after they submit the page.</span></span> <span data-ttu-id="bfe93-156">Bir form uzun veya karmaşık ise, yalnızca sayfa gönderildikten sonra hataları bildirmek Kullanıcı için kullanışlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-156">If a form is long or complex, reporting errors only after the page is submitted can be inconvenient to the user.</span></span>

<span data-ttu-id="bfe93-157">İstemci betiği içinde doğrulama gerçekleştirmek için destek ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bfe93-157">You can add support to perform validation in client script.</span></span> <span data-ttu-id="bfe93-158">Bu durumda, kullanıcı tarayıcıda çalıştığı için doğrulama gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-158">In that case, the validation is performed as users work in the browser.</span></span> <span data-ttu-id="bfe93-159">Örneğin, bir değerin tamsayı olması gerektiğini varsayalım.</span><span class="sxs-lookup"><span data-stu-id="bfe93-159">For example, suppose you specify that a value should be an integer.</span></span> <span data-ttu-id="bfe93-160">Kullanıcı tamsayı olmayan bir değer girerse, Kullanıcı giriş alanından ayrıldığında hata bildirilir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-160">If a user enters a non-integer value, the error is reported as soon as the user leaves the entry field.</span></span> <span data-ttu-id="bfe93-161">Kullanıcılar, bunlar için uygun olan anında geri bildirim alırlar.</span><span class="sxs-lookup"><span data-stu-id="bfe93-161">Users get immediate feedback, which is convenient for them.</span></span> <span data-ttu-id="bfe93-162">İstemci tabanlı doğrulama, kullanıcının birden çok hatayı düzeltmek için formu kaç kez göndermesi gerektiğini de azaltabilir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-162">Client-based validation can also reduce the number of times that the user has to submit the form to correct multiple errors.</span></span>

> [!NOTE]
> <span data-ttu-id="bfe93-163">İstemci tarafı doğrulaması kullanıyor olsanız bile, doğrulama her zaman sunucu kodunda da gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-163">Even if you use client-side validation, validation is always also performed in server code.</span></span> <span data-ttu-id="bfe93-164">Sunucu kodunda doğrulamanın gerçekleştirilmesi, kullanıcıların istemci tabanlı doğrulamayı atlaması durumunda bir güvenlik ölçümüdür.</span><span class="sxs-lookup"><span data-stu-id="bfe93-164">Performing validation in server code is a security measure, in case users bypass client-based validation.</span></span>

1. <span data-ttu-id="bfe93-165">Aşağıdaki JavaScript kitaplıklarını sayfaya kaydedin:</span><span class="sxs-lookup"><span data-stu-id="bfe93-165">Register the following JavaScript libraries in the page:</span></span>  

    [!code-html[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample3.html)]

   <span data-ttu-id="bfe93-166">Kütüphanelerin ikisi bir Content Delivery Network (CDN) ile yüklenebilir, bu nedenle bilgisayarınızda veya sunucunuzda olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="bfe93-166">Two of the libraries are loadable from a content delivery network (CDN), so you don't necessarily have to have them on your computer or server.</span></span> <span data-ttu-id="bfe93-167">Ancak, *jQuery. Validate. unobtrusive. js*' nin yerel kopyasına sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-167">However, you must have a local copy of *jquery.validate.unobtrusive.js*.</span></span> <span data-ttu-id="bfe93-168">Kitaplığı içeren bir WebMatrix şablonuyla ( **Başlatıcı site** gibi) çalışmıyorsanız, **Başlatıcı siteyi**temel alan bir Web sayfaları sitesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bfe93-168">If you are not already working with a WebMatrix template (like **Starter Site** ) that includes the library, create a Web Pages site that's based on **Starter Site**.</span></span> <span data-ttu-id="bfe93-169">Sonra *. js* dosyasını geçerli sitenize kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="bfe93-169">Then copy the *.js* file to your current site.</span></span>
2. <span data-ttu-id="bfe93-170">Biçimlendirme ' de, doğruladığınızı her öğe için `Validation.For(field)`bir çağrı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bfe93-170">In markup, for each element that you're validating, add a call to `Validation.For(field)`.</span></span> <span data-ttu-id="bfe93-171">Bu yöntem, istemci tarafı doğrulama tarafından kullanılan öznitelikleri yayar.</span><span class="sxs-lookup"><span data-stu-id="bfe93-171">This method emits attributes that are used by client-side validation.</span></span> <span data-ttu-id="bfe93-172">(Gerçek JavaScript kodunu yayma yerine, yöntem `data-val-...`gibi öznitelikleri yayar.</span><span class="sxs-lookup"><span data-stu-id="bfe93-172">(Rather than emitting actual JavaScript code, the method emits attributes like `data-val-...`.</span></span> <span data-ttu-id="bfe93-173">Bu öznitelikler, işi yapmak için jQuery kullanan istemci doğrulamasını destekler.)</span><span class="sxs-lookup"><span data-stu-id="bfe93-173">These attributes support unobtrusive client validation that uses jQuery to do the work.)</span></span>

<span data-ttu-id="bfe93-174">Aşağıdaki sayfada, daha önce gösterilen örneğe istemci doğrulama özelliklerinin nasıl ekleneceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-174">The following page shows how to add client validation features to the example shown earlier.</span></span>

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample4.cshtml?highlight=35-39,51,61,71)]

<span data-ttu-id="bfe93-175">İstemci üzerinde tüm doğrulama denetimleri çalıştırılmadı.</span><span class="sxs-lookup"><span data-stu-id="bfe93-175">Not all validation checks run on the client.</span></span> <span data-ttu-id="bfe93-176">Özellikle, veri türü doğrulama (tamsayı, tarih vb.) istemcide çalıştırılmayın.</span><span class="sxs-lookup"><span data-stu-id="bfe93-176">In particular, data-type validation (integer, date, and so on) don't run on the client.</span></span> <span data-ttu-id="bfe93-177">Aşağıdaki denetimler hem istemci hem de sunucu üzerinde çalışır:</span><span class="sxs-lookup"><span data-stu-id="bfe93-177">The following checks work on both the client and server:</span></span>

- `Required`
- `Range(minValue, maxValue)`
- `StringLength(maxLength[, minLength])`
- `Regex(pattern)`
- `EqualsTo(otherField)`

<span data-ttu-id="bfe93-178">Bu örnekte, geçerli bir tarih testi istemci kodunda çalışmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="bfe93-178">In this example, the test for a valid date won't work in client code.</span></span> <span data-ttu-id="bfe93-179">Ancak, test sunucu kodunda gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-179">However, the test will be performed in server code.</span></span>

<a id="Formatting_Validation_Errors"></a>
## <a name="formatting-validation-errors"></a><span data-ttu-id="bfe93-180">Doğrulama hatalarını biçimlendirme</span><span class="sxs-lookup"><span data-stu-id="bfe93-180">Formatting Validation Errors</span></span>

<span data-ttu-id="bfe93-181">Aşağıdaki ayrılmış adlara sahip CSS sınıfları tanımlayarak, doğrulama hatalarının nasıl görüntülendiğini denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bfe93-181">You can control how validation errors are displayed by defining CSS classes that have the following reserved names:</span></span>

- <span data-ttu-id="bfe93-182">`field-validation-error`.</span><span class="sxs-lookup"><span data-stu-id="bfe93-182">`field-validation-error`.</span></span> <span data-ttu-id="bfe93-183">Bir hata görüntülenirken `Html.ValidationMessage` yönteminin çıkışını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="bfe93-183">Defines the output of the `Html.ValidationMessage` method when it's displaying an error.</span></span>
- <span data-ttu-id="bfe93-184">`field-validation-valid`.</span><span class="sxs-lookup"><span data-stu-id="bfe93-184">`field-validation-valid`.</span></span> <span data-ttu-id="bfe93-185">Hata olmadığında `Html.ValidationMessage` yönteminin çıkışını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="bfe93-185">Defines the output of the `Html.ValidationMessage` method when there is no error.</span></span>
- <span data-ttu-id="bfe93-186">`input-validation-error`.</span><span class="sxs-lookup"><span data-stu-id="bfe93-186">`input-validation-error`.</span></span> <span data-ttu-id="bfe93-187">Bir hata olduğunda `<input>` öğelerinin nasıl işleneceğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="bfe93-187">Defines how `<input>` elements are rendered when there's an error.</span></span> <span data-ttu-id="bfe93-188">(Örneğin, bir &lt;girişi&gt; öğesinin arka plan rengini, değeri geçersizse farklı bir renge ayarlamak için bu sınıfı kullanabilirsiniz.) Bu CSS sınıfı yalnızca istemci doğrulaması sırasında kullanılır (ASP.NET Web Pages 2).</span><span class="sxs-lookup"><span data-stu-id="bfe93-188">(For example, you can use this class to set the background color of an &lt;input&gt; element to a different color if its value is invalid.) This CSS class is used only during client validation (in ASP.NET Web Pages 2).</span></span>
- <span data-ttu-id="bfe93-189">`input-validation-valid`.</span><span class="sxs-lookup"><span data-stu-id="bfe93-189">`input-validation-valid`.</span></span> <span data-ttu-id="bfe93-190">Hata olmadığında `<input>` öğelerinin görünümünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="bfe93-190">Defines the appearance of `<input>` elements when there is no error.</span></span>
- <span data-ttu-id="bfe93-191">`validation-summary-errors`.</span><span class="sxs-lookup"><span data-stu-id="bfe93-191">`validation-summary-errors`.</span></span> <span data-ttu-id="bfe93-192">`Html.ValidationSummary` yönteminin çıkışını tanımlar ve bu, hataların bir listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="bfe93-192">Defines the output of the `Html.ValidationSummary` method it's displaying a list of errors.</span></span>
- <span data-ttu-id="bfe93-193">`validation-summary-valid`.</span><span class="sxs-lookup"><span data-stu-id="bfe93-193">`validation-summary-valid`.</span></span> <span data-ttu-id="bfe93-194">Hata olmadığında `Html.ValidationSummary` yönteminin çıkışını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="bfe93-194">Defines the output of the `Html.ValidationSummary` method when there is no error.</span></span>

<span data-ttu-id="bfe93-195">Aşağıdaki `<style>` bloğu hata koşulları kurallarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-195">The following `<style>` block shows rules for error conditions.</span></span>

[!code-css[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample5.css)]

<span data-ttu-id="bfe93-196">Bu stil bloğunu, makalenin önceki kısımlarında bulunan örnek sayfalara dahil ederseniz, hata görünümü aşağıdaki çizimde gösterildiği gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="bfe93-196">If you include this style block in the example pages from earlier in the article, the error display will look like the following illustration:</span></span>

![CSS stil sınıflarını kullanan doğrulama hataları](validating-user-input-in-aspnet-web-pages-sites/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="bfe93-198">ASP.NET Web Pages 2 ' de istemci doğrulaması kullanmıyorsanız, `<input>` öğeleri için CSS sınıfları (`input-validation-error` ve `input-validation-valid` hiçbir etkiye sahip olmaz.</span><span class="sxs-lookup"><span data-stu-id="bfe93-198">If you're not using client validation in ASP.NET Web Pages 2, the CSS classes for the `<input>` elements (`input-validation-error` and `input-validation-valid` don't have any effect.</span></span>

### <a name="static-and-dynamic-error-display"></a><span data-ttu-id="bfe93-199">Statik ve dinamik hata görüntüleme</span><span class="sxs-lookup"><span data-stu-id="bfe93-199">Static and Dynamic Error Display</span></span>

<span data-ttu-id="bfe93-200">CSS kuralları `validation-summary-errors` ve `validation-summary-valid`gibi çiftler halinde gelir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-200">The CSS rules come in pairs, such as `validation-summary-errors` and `validation-summary-valid`.</span></span> <span data-ttu-id="bfe93-201">Bu çiftler her iki koşul için kurallar tanımlamanızı sağlar: bir hata durumu ve "normal" (hata olmayan) koşulu.</span><span class="sxs-lookup"><span data-stu-id="bfe93-201">These pairs let you define rules for both conditions: an error condition and a "normal" (non-error) condition.</span></span> <span data-ttu-id="bfe93-202">Hata olmadan biçimlendirmenin her zaman bir hata olmasa bile, her zaman işlenip işlenmeyeceğini anlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-202">It's important to understand that the markup for the error display is always rendered, even if there are no errors.</span></span> <span data-ttu-id="bfe93-203">Örneğin, bir sayfada biçimlendirme içinde bir `Html.ValidationSummary` yöntemi varsa, sayfa kaynağı ilk kez istendiği zaman bile aşağıdaki biçimlendirmeyi içerecektir:</span><span class="sxs-lookup"><span data-stu-id="bfe93-203">For example, if a page has an `Html.ValidationSummary` method in the markup, the page source will contain the following markup even when the page is requested for the first time:</span></span>

`<div class="validation-summary-valid" data-valmsg-summary="true"><ul></ul></div>`

<span data-ttu-id="bfe93-204">Diğer bir deyişle, `Html.ValidationSummary` yöntemi her zaman bir `<div>` öğesi ve bir liste oluşturur, bu da hata listesi boş olsa bile.</span><span class="sxs-lookup"><span data-stu-id="bfe93-204">In other words, the `Html.ValidationSummary` method always renders a `<div>` element and a list, even if the error list is empty.</span></span> <span data-ttu-id="bfe93-205">Benzer şekilde, `Html.ValidationMessage` yöntemi her zaman bir alan hatası için bir yer tutucu olarak bir `<span>` öğesi oluşturur, aksi halde bir hata yoktur.</span><span class="sxs-lookup"><span data-stu-id="bfe93-205">Similarly, the `Html.ValidationMessage` method always renders a `<span>` element as a placeholder for an individual field error, even if there is no error.</span></span>

<span data-ttu-id="bfe93-206">Bazı durumlarda, bir hata iletisi görüntülenirken sayfanın yeniden akıtılmasına neden olabilir ve sayfadaki öğelerin etrafında hareket olmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-206">In some situations, displaying an error message can cause the page to reflow and can cause elements on the page to move around.</span></span> <span data-ttu-id="bfe93-207">`-valid` biten CSS kuralları, bu sorunu önlemeye yardımcı olabilecek bir düzen tanımlamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="bfe93-207">The CSS rules that end in `-valid` let you define a layout that can help prevent this problem.</span></span> <span data-ttu-id="bfe93-208">Örneğin, `field-validation-error` tanımlayabilir ve `field-validation-valid` her ikisi de aynı sabit boyuta sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-208">For example, you can define `field-validation-error` and `field-validation-valid` to both have the same fixed size.</span></span> <span data-ttu-id="bfe93-209">Bu şekilde, alanın görüntüleme alanı statiktir ve bir hata iletisi görüntülenirse sayfa akışını değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="bfe93-209">That way, the display area for the field is static and won't change the page flow if an error message is displayed.</span></span>

<a id="Validating_Data_That_Doesnt_Come_Directly_from_Users"></a>
## <a name="validating-data-that-doesnt-come-directly-from-users"></a><span data-ttu-id="bfe93-210">Doğrudan kullanıcılardan gelmeyen verileri doğrulama</span><span class="sxs-lookup"><span data-stu-id="bfe93-210">Validating Data That Doesn't Come Directly from Users</span></span>

<span data-ttu-id="bfe93-211">Bazen bir HTML formundan doğrudan gelmeyen bilgileri doğrulamanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-211">Sometimes you have to validate information that doesn't come directly from an HTML form.</span></span> <span data-ttu-id="bfe93-212">Tipik bir örnek, aşağıdaki örnekte olduğu gibi bir sorgu dizesinde bir değerin geçirildiği bir sayfasıdır:</span><span class="sxs-lookup"><span data-stu-id="bfe93-212">A typical example is a page where a value is passed in a query string, as in the following example:</span></span>

`http://server/myapp/EditClassInformation?classid=1022`

<span data-ttu-id="bfe93-213">Bu durumda, sayfaya geçirilen değerin (burada, `classid`değeri için 1022) geçerli olduğundan emin olmak istersiniz.</span><span class="sxs-lookup"><span data-stu-id="bfe93-213">In this case, you want to make sure that the value that's passed to the page (here, 1022 for the value of `classid`) is valid.</span></span> <span data-ttu-id="bfe93-214">Bu doğrulamayı gerçekleştirmek için `Validation` yardımcısını doğrudan kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="bfe93-214">You can't directly use the `Validation` helper to perform this validation.</span></span> <span data-ttu-id="bfe93-215">Bununla birlikte, doğrulama sisteminin, doğrulama hatası iletilerini görüntüleme özelliği gibi diğer özelliklerini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bfe93-215">However, you can use other features of the validation system, like the ability to display validation error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="bfe93-216">**Önemli** Form alanı değerleri, sorgu dizesi değerleri ve tanımlama bilgisi değerleri de dahil olmak üzere *herhangi bir* kaynaktan aldığınız değerleri her zaman doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="bfe93-216">**Important** Always validate values that you get from *any* source, including form-field values, query-string values, and cookie values.</span></span> <span data-ttu-id="bfe93-217">Kişilerin bu değerleri değiştirmesi oldukça kolaydır (Belki de kötü amaçlı amaçlar için).</span><span class="sxs-lookup"><span data-stu-id="bfe93-217">It's easy for people to change these values (perhaps for malicious purposes).</span></span> <span data-ttu-id="bfe93-218">Bu nedenle, uygulamanızı korumak için bu değerleri denetlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-218">So you must check these values in order to protect your application.</span></span>

<span data-ttu-id="bfe93-219">Aşağıdaki örnek, bir sorgu dizesinde iletilen bir değeri nasıl doğrulayacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-219">The following example shows how you might validate a value that's passed in a query string.</span></span> <span data-ttu-id="bfe93-220">Kod, değerin boş ve tamsayı olduğunu sınar.</span><span class="sxs-lookup"><span data-stu-id="bfe93-220">The code tests that the value is not empty and that it's an integer.</span></span>

[!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample6.cs)]

<span data-ttu-id="bfe93-221">İstek bir form gönderimi olmadığında testin gerçekleştirildiğinden (`if(!IsPost)`) dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="bfe93-221">Notice that the test is performed when the request is not a form submission (`if(!IsPost)`).</span></span> <span data-ttu-id="bfe93-222">Bu test sayfa istendiğinde ilk kez geçer, ancak istek bir form gönderimi olduğunda bunu yapmayabilir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-222">This test would pass the first time that the page is requested, but not when the request is a form submission.</span></span>

<span data-ttu-id="bfe93-223">Bu hatayı göstermek için `Validation.AddFormError("message")`çağırarak doğrulama hataları listesine hatayı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bfe93-223">To display this error, you can add the error to the list of validation errors by calling `Validation.AddFormError("message")`.</span></span> <span data-ttu-id="bfe93-224">Sayfa `Html.ValidationSummary` yöntemine bir çağrı içeriyorsa, hata bir kullanıcı girişi doğrulama hatası gibi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="bfe93-224">If the page contains a call to the `Html.ValidationSummary` method, the error is displayed there, just like a user-input validation error.</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="bfe93-225">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="bfe93-225">Additional Resources</span></span>

[<span data-ttu-id="bfe93-226">ASP.NET Web Pages sitelerinde HTML formlarıyla çalışma</span><span class="sxs-lookup"><span data-stu-id="bfe93-226">Working with HTML Forms in ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkID=202892)
