---
uid: aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: Özel HTML Yardımcıları oluşturma (C#) | Microsoft Docs
author: microsoft
description: Bu öğreticinin amacı, MVC görünümleriniz dahilinde kullanabileceğiniz özel HTML Yardımcıları oluşturmayı gösterir. HTML Yardımcısı 'ndan yararlanarak...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 264ff9850bad397826b45649d52fbfefafc53a01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600242"
---
# <a name="creating-custom-html-helpers-c"></a><span data-ttu-id="514a4-104">Özel HTML Yardımcıları Oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="514a4-104">Creating Custom HTML Helpers (C#)</span></span>

<span data-ttu-id="514a4-105">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="514a4-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="514a4-106">PDF 'YI indir</span><span class="sxs-lookup"><span data-stu-id="514a4-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> <span data-ttu-id="514a4-107">Bu öğreticinin amacı, MVC görünümleriniz dahilinde kullanabileceğiniz özel HTML Yardımcıları oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="514a4-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="514a4-108">HTML yardımcılarından yararlanarak, standart bir HTML sayfası oluşturmak için gerçekleştirmeniz gereken HTML etiketlerinin sıkıcı yazma miktarını azaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="514a4-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="514a4-109">Bu öğreticinin amacı, MVC görünümleriniz dahilinde kullanabileceğiniz özel HTML Yardımcıları oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="514a4-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="514a4-110">HTML yardımcılarından yararlanarak, standart bir HTML sayfası oluşturmak için gerçekleştirmeniz gereken HTML etiketlerinin sıkıcı yazma miktarını azaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="514a4-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="514a4-111">Bu öğreticinin ilk bölümünde, ASP.NET MVC çerçevesine dahil olan mevcut HTML yardımcılarını anlatmaktadır.</span><span class="sxs-lookup"><span data-stu-id="514a4-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="514a4-112">Sonra, özel HTML Yardımcıları oluşturmak için iki yöntem açıkladım: statik bir yöntem oluşturarak ve bir genişletme yöntemi oluşturarak özel HTML Yardımcıları oluşturmayı açıkladım.</span><span class="sxs-lookup"><span data-stu-id="514a4-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a static method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="514a4-113">HTML Yardımcıları anlama</span><span class="sxs-lookup"><span data-stu-id="514a4-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="514a4-114">HTML Yardımcısı yalnızca bir dize döndüren bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="514a4-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="514a4-115">Dize, istediğiniz herhangi bir içerik türünü temsil edebilir.</span><span class="sxs-lookup"><span data-stu-id="514a4-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="514a4-116">Örneğin, HTML `<input>` ve `<img>` etiketleri gibi standart HTML etiketlerini işlemek için HTML Yardımcıları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="514a4-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="514a4-117">Ayrıca, bir sekme şeridi veya bir HTML tablosu veritabanı verileri gibi karmaşık içerikleri işlemek için HTML Yardımcıları da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="514a4-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="514a4-118">ASP.NET MVC çerçevesi, aşağıdaki standart HTML Yardımcıları kümesini içerir (Bu bir liste değildir):</span><span class="sxs-lookup"><span data-stu-id="514a4-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="514a4-119">HTML. ActionLink ()</span><span class="sxs-lookup"><span data-stu-id="514a4-119">Html.ActionLink()</span></span>
- <span data-ttu-id="514a4-120">HTML. BeginForm ()</span><span class="sxs-lookup"><span data-stu-id="514a4-120">Html.BeginForm()</span></span>
- <span data-ttu-id="514a4-121">Html.CheckBox()</span><span class="sxs-lookup"><span data-stu-id="514a4-121">Html.CheckBox()</span></span>
- <span data-ttu-id="514a4-122">HTML. DropDownList ()</span><span class="sxs-lookup"><span data-stu-id="514a4-122">Html.DropDownList()</span></span>
- <span data-ttu-id="514a4-123">Html.EndForm()</span><span class="sxs-lookup"><span data-stu-id="514a4-123">Html.EndForm()</span></span>
- <span data-ttu-id="514a4-124">HTML. Hidden ()</span><span class="sxs-lookup"><span data-stu-id="514a4-124">Html.Hidden()</span></span>
- <span data-ttu-id="514a4-125">Html.ListBox()</span><span class="sxs-lookup"><span data-stu-id="514a4-125">Html.ListBox()</span></span>
- <span data-ttu-id="514a4-126">HTML. Password ()</span><span class="sxs-lookup"><span data-stu-id="514a4-126">Html.Password()</span></span>
- <span data-ttu-id="514a4-127">Html.RadioButton()</span><span class="sxs-lookup"><span data-stu-id="514a4-127">Html.RadioButton()</span></span>
- <span data-ttu-id="514a4-128">HTML. TextArea ()</span><span class="sxs-lookup"><span data-stu-id="514a4-128">Html.TextArea()</span></span>
- <span data-ttu-id="514a4-129">Html.TextBox()</span><span class="sxs-lookup"><span data-stu-id="514a4-129">Html.TextBox()</span></span>

<span data-ttu-id="514a4-130">Örneğin, liste 1 ' de formu göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="514a4-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="514a4-131">Bu form standart HTML yardımcılarını (bkz. Şekil 1) içeren yardım ile birlikte işlenir.</span><span class="sxs-lookup"><span data-stu-id="514a4-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="514a4-132">Bu form basit bir HTML formu işlemek için `Html.BeginForm()` ve `Html.TextBox()` yardımcı yöntemlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="514a4-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods to render a simple HTML form.</span></span>

<span data-ttu-id="514a4-133">[HTML Yardımcıları ile işlenen ![sayfası](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="514a4-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span></span>

<span data-ttu-id="514a4-134">**Şekil 01**: HTML Yardımcıları ile işlenen sayfa ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-custom-html-helpers-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="514a4-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image3.png))</span></span>

<span data-ttu-id="514a4-135">**Listeleme 1 – `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="514a4-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

<span data-ttu-id="514a4-136">HTML. BeginForm () yardımcı yöntemi, açma ve kapatma HTML `<form>` etiketlerini oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="514a4-136">The Html.BeginForm() Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="514a4-137">`Html.BeginForm()` yönteminin bir using ifadesinin içinde çağrıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="514a4-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="514a4-138">Using ifadesinde, using bloğunun sonunda `<form>` etiketinin kapalı olması güvence altına alınır.</span><span class="sxs-lookup"><span data-stu-id="514a4-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="514a4-139">Tercih ederseniz, bir using bloğu oluşturmak yerine, `<form>` etiketini kapatmak için HTML. EndForm () yardımcı yöntemini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="514a4-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="514a4-140">Size çok sezgisel bir açma ve kapatma `<form>` etiketi oluşturmak için hangi yaklaşımı kullanın.</span><span class="sxs-lookup"><span data-stu-id="514a4-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="514a4-141">`Html.TextBox()` yardımcı yöntemleri, HTML `<input>` etiketlerini işlemek için 1. liste ' de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="514a4-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="514a4-142">Tarayıcınızda kaynağı görüntüle ' yi seçerseniz, liste 2 ' de HTML kaynağını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="514a4-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="514a4-143">Kaynağın standart HTML etiketleri içerdiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="514a4-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="514a4-144">`Html.TextBox()`-HTML Yardımcısı 'nın `<% %>` etiketleri yerine `<%= %>` etiketleriyle işlendiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="514a4-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="514a4-145">Eşittir işaretini eklemezseniz, hiçbir şey tarayıcıya işlenmez.</span><span class="sxs-lookup"><span data-stu-id="514a4-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="514a4-146">ASP.NET MVC çerçevesi küçük bir yardımcılar kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="514a4-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="514a4-147">Büyük olasılıkla, MVC çerçevesini özel HTML yardımcılarını genişletmenize gerek duyarsınız.</span><span class="sxs-lookup"><span data-stu-id="514a4-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="514a4-148">Bu öğreticinin geri kalanında, özel HTML Yardımcıları oluşturmak için iki yöntem öğrenirsiniz.</span><span class="sxs-lookup"><span data-stu-id="514a4-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="514a4-149">**Listeleme 2 – `Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="514a4-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a><span data-ttu-id="514a4-150">Statik yöntemlerle HTML Yardımcıları oluşturma</span><span class="sxs-lookup"><span data-stu-id="514a4-150">Creating HTML Helpers with Static Methods</span></span>

<span data-ttu-id="514a4-151">Yeni bir HTML Yardımcısı oluşturmanın en kolay yolu, bir dize döndüren statik bir yöntem oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="514a4-151">The easiest way to create a new HTML Helper is to create a static method that returns a string.</span></span> <span data-ttu-id="514a4-152">Örneğin, bir HTML `<label>` etiketi oluşturan yeni bir HTML Yardımcısı oluşturmaya karar verdiğinizi düşünün.</span><span class="sxs-lookup"><span data-stu-id="514a4-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="514a4-153">Bir `<label>` işlemek için liste 2 ' de sınıfını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="514a4-153">You can use the class in Listing 2 to render a `<label>` .</span></span>

<span data-ttu-id="514a4-154">**Listeleme 2 – `Helpers\LabelHelper.cs`**</span><span class="sxs-lookup"><span data-stu-id="514a4-154">**Listing 2 – `Helpers\LabelHelper.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

<span data-ttu-id="514a4-155">Kod 2 ' de sınıf hakkında özel bir şey yoktur.</span><span class="sxs-lookup"><span data-stu-id="514a4-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="514a4-156">`Label()` yöntemi yalnızca bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="514a4-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="514a4-157">Listeleme 3 ' teki değiştirilen dizin görünümü HTML `<label>` etiketlerini işlemek için `LabelHelper` kullanır.</span><span class="sxs-lookup"><span data-stu-id="514a4-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="514a4-158">Görünümün, `Application1.Helpers` ad alanını içeri aktaran bir `<%@ imports %>` yönergesi içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="514a4-158">Notice that the view includes an `<%@ imports %>` directive that imports the `Application1.Helpers` namespace.</span></span>

<span data-ttu-id="514a4-159">**Listeleme 2 – `Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="514a4-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="514a4-160">Uzantı yöntemleriyle HTML Yardımcıları oluşturma</span><span class="sxs-lookup"><span data-stu-id="514a4-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="514a4-161">Yalnızca ASP.NET MVC çerçevesinin içerdiği standart HTML Yardımcıları gibi çalışan HTML Yardımcıları oluşturmak istiyorsanız, uzantı yöntemleri oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="514a4-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="514a4-162">Uzantı yöntemleri varolan bir sınıfa yeni yöntemler eklemenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="514a4-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="514a4-163">Bir HTML yardımcı yöntemi oluştururken, bir görünümün HTML özelliği tarafından temsil edilen HtmlHelper sınıfına yeni yöntemler eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="514a4-163">When creating an HTML Helper method, you add new methods to the HtmlHelper class represented by a view's Html property.</span></span>

<span data-ttu-id="514a4-164">Listeleme 3 ' teki sınıfı, `Label()`adlı `HtmlHelper` sınıfına bir genişletme yöntemi ekler.</span><span class="sxs-lookup"><span data-stu-id="514a4-164">The class in Listing 3 adds an extension method to the `HtmlHelper` class named `Label()`.</span></span> <span data-ttu-id="514a4-165">Bu sınıf hakkında dikkat etmeniz gereken birkaç nokta vardır.</span><span class="sxs-lookup"><span data-stu-id="514a4-165">There are a couple of things that you should notice about this class.</span></span> <span data-ttu-id="514a4-166">İlk olarak, sınıfın bir statik sınıf olduğunu fark edersiniz.</span><span class="sxs-lookup"><span data-stu-id="514a4-166">First, notice that the class is a static class.</span></span> <span data-ttu-id="514a4-167">Statik sınıfla bir genişletme yöntemi tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="514a4-167">You must define an extension method with a static class.</span></span>

<span data-ttu-id="514a4-168">İkincisi, `Label()` yönteminin ilk parametresinin önünde `this`anahtar sözcüğünün olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="514a4-168">Second, notice that the first parameter of the `Label()` method is preceded by the keyword `this`.</span></span> <span data-ttu-id="514a4-169">Bir genişletme yönteminin ilk parametresi, genişletme yönteminin genişlettiği sınıfı gösterir.</span><span class="sxs-lookup"><span data-stu-id="514a4-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="514a4-170">**Listeleme 3 – `Helpers\LabelExtensions.cs`**</span><span class="sxs-lookup"><span data-stu-id="514a4-170">**Listing 3 – `Helpers\LabelExtensions.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

<span data-ttu-id="514a4-171">Bir genişletme yöntemi oluşturup uygulamanızı başarılı bir şekilde oluşturduktan sonra, genişletme yöntemi bir sınıfın tüm diğer yöntemleri gibi Visual Studio IntelliSense 'de görünür (bkz. Şekil 2).</span><span class="sxs-lookup"><span data-stu-id="514a4-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="514a4-172">Tek fark, genişletme yöntemlerinin bunların yanında özel bir simge (aşağı ok simgesi) ile görünme sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="514a4-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>

<span data-ttu-id="514a4-173">[HTML. Label () genişletme yöntemini kullanarak ![](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="514a4-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span></span>

<span data-ttu-id="514a4-174">**Şekil 02**: HTML. Label () genişletme yöntemini kullanma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-custom-html-helpers-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="514a4-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image6.png))</span></span>

<span data-ttu-id="514a4-175">Liste 4 ' te değiştirilen dizin görünümü, tüm `<label>` etiketlerini işlemek için HTML. Label () genişletme yöntemini kullanır.</span><span class="sxs-lookup"><span data-stu-id="514a4-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its `<label>` tags.</span></span>

<span data-ttu-id="514a4-176">**Listeleme 4 – `Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="514a4-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="514a4-177">Özet</span><span class="sxs-lookup"><span data-stu-id="514a4-177">Summary</span></span>

<span data-ttu-id="514a4-178">Bu öğreticide, özel HTML Yardımcıları oluşturmak için iki yöntem öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="514a4-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="514a4-179">İlk olarak, bir dize döndüren statik bir yöntem oluşturarak özel bir `Label()` HTML Yardımcısı oluşturmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="514a4-179">First, you learned how to create a custom `Label()` HTML Helper by creating a static method that returns a string.</span></span> <span data-ttu-id="514a4-180">Daha sonra, `HtmlHelper` sınıfında bir genişletme yöntemi oluşturarak özel bir `Label()` HTML Yardımcısı yöntemi oluşturmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="514a4-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="514a4-181">Bu öğreticide son derece basit bir HTML yardımcı yöntemi oluşturmaya odaklandım.</span><span class="sxs-lookup"><span data-stu-id="514a4-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="514a4-182">Bir HTML Yardımcısı 'nın istediğiniz kadar karmaşık olduğunu fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="514a4-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="514a4-183">Ağaç görünümleri, menüler veya veritabanı verilerinin tabloları gibi zengin içerik işleyen HTML Yardımcıları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="514a4-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="514a4-184">[Önceki](asp-net-mvc-views-overview-cs.md)
> [İleri](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span><span class="sxs-lookup"><span data-stu-id="514a4-184">[Previous](asp-net-mvc-views-overview-cs.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span></span>
