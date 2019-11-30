---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
title: Özel HTML Yardımcıları oluşturma (VB) | Microsoft Docs
author: microsoft
description: Bu öğreticinin amacı, MVC görünümleriniz dahilinde kullanabileceğiniz özel HTML Yardımcıları oluşturmayı gösterir. HTML Yardımcısı 'ndan yararlanarak...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f96f4800-19ef-44c0-b457-55e777eb5de8
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: aaeadde258a2855343a5bfb1e5ee76000e04f6bd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74593862"
---
# <a name="creating-custom-html-helpers-vb"></a><span data-ttu-id="b9310-104">Özel HTML Yardımcıları Oluşturma (VB)</span><span class="sxs-lookup"><span data-stu-id="b9310-104">Creating Custom HTML Helpers (VB)</span></span>

<span data-ttu-id="b9310-105">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="b9310-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="b9310-106">PDF 'YI indir</span><span class="sxs-lookup"><span data-stu-id="b9310-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_VB.pdf)

> <span data-ttu-id="b9310-107">Bu öğreticinin amacı, MVC görünümleriniz dahilinde kullanabileceğiniz özel HTML Yardımcıları oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="b9310-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="b9310-108">HTML yardımcılarından yararlanarak, standart bir HTML sayfası oluşturmak için gerçekleştirmeniz gereken HTML etiketlerinin sıkıcı yazma miktarını azaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9310-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="b9310-109">Bu öğreticinin amacı, MVC görünümleriniz dahilinde kullanabileceğiniz özel HTML Yardımcıları oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="b9310-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="b9310-110">HTML yardımcılarından yararlanarak, standart bir HTML sayfası oluşturmak için gerçekleştirmeniz gereken HTML etiketlerinin sıkıcı yazma miktarını azaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9310-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="b9310-111">Bu öğreticinin ilk bölümünde, ASP.NET MVC çerçevesine dahil olan mevcut HTML yardımcılarını anlatmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b9310-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="b9310-112">Sonra, özel HTML Yardımcıları oluşturmak için iki yöntem açıkladım: paylaşılan bir yöntem oluşturarak ve bir genişletme yöntemi oluşturarak özel HTML Yardımcıları oluşturmayı açıkladım.</span><span class="sxs-lookup"><span data-stu-id="b9310-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a shared method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="b9310-113">HTML Yardımcıları anlama</span><span class="sxs-lookup"><span data-stu-id="b9310-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="b9310-114">HTML Yardımcısı yalnızca bir dize döndüren bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="b9310-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="b9310-115">Dize, istediğiniz herhangi bir içerik türünü temsil edebilir.</span><span class="sxs-lookup"><span data-stu-id="b9310-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="b9310-116">Örneğin, HTML `<input>` ve `<img>` etiketleri gibi standart HTML etiketlerini işlemek için HTML Yardımcıları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9310-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="b9310-117">Ayrıca, bir sekme şeridi veya bir HTML tablosu veritabanı verileri gibi karmaşık içerikleri işlemek için HTML Yardımcıları da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9310-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="b9310-118">ASP.NET MVC çerçevesi, aşağıdaki standart HTML Yardımcıları kümesini içerir (Bu bir liste değildir):</span><span class="sxs-lookup"><span data-stu-id="b9310-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="b9310-119">HTML. ActionLink ()</span><span class="sxs-lookup"><span data-stu-id="b9310-119">Html.ActionLink()</span></span>
- <span data-ttu-id="b9310-120">HTML. BeginForm ()</span><span class="sxs-lookup"><span data-stu-id="b9310-120">Html.BeginForm()</span></span>
- <span data-ttu-id="b9310-121">HTML. CheckBox ()</span><span class="sxs-lookup"><span data-stu-id="b9310-121">Html.CheckBox()</span></span>
- <span data-ttu-id="b9310-122">HTML. DropDownList ()</span><span class="sxs-lookup"><span data-stu-id="b9310-122">Html.DropDownList()</span></span>
- <span data-ttu-id="b9310-123">HTML. EndForm ()</span><span class="sxs-lookup"><span data-stu-id="b9310-123">Html.EndForm()</span></span>
- <span data-ttu-id="b9310-124">HTML. Hidden ()</span><span class="sxs-lookup"><span data-stu-id="b9310-124">Html.Hidden()</span></span>
- <span data-ttu-id="b9310-125">HTML. ListBox ()</span><span class="sxs-lookup"><span data-stu-id="b9310-125">Html.ListBox()</span></span>
- <span data-ttu-id="b9310-126">HTML. Password ()</span><span class="sxs-lookup"><span data-stu-id="b9310-126">Html.Password()</span></span>
- <span data-ttu-id="b9310-127">HTML. RadioButton ()</span><span class="sxs-lookup"><span data-stu-id="b9310-127">Html.RadioButton()</span></span>
- <span data-ttu-id="b9310-128">HTML. TextArea ()</span><span class="sxs-lookup"><span data-stu-id="b9310-128">Html.TextArea()</span></span>
- <span data-ttu-id="b9310-129">HTML. TextBox ()</span><span class="sxs-lookup"><span data-stu-id="b9310-129">Html.TextBox()</span></span>

<span data-ttu-id="b9310-130">Örneğin, liste 1 ' de formu göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="b9310-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="b9310-131">Bu form standart HTML yardımcılarını (bkz. Şekil 1) içeren yardım ile birlikte işlenir.</span><span class="sxs-lookup"><span data-stu-id="b9310-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="b9310-132">Bu form `Html.BeginForm()` ve `Html.TextBox()` yardımcı yöntemlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="b9310-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods.</span></span>

<span data-ttu-id="b9310-133">[HTML Yardımcıları ile işlenen ![sayfası](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b9310-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)</span></span>

<span data-ttu-id="b9310-134">**Şekil 01**: HTML Yardımcıları ile işlenen sayfa ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-custom-html-helpers-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="b9310-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-vb/_static/image3.png))</span></span>

<span data-ttu-id="b9310-135">**Listeleme 1 – `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="b9310-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample1.aspx)]

<span data-ttu-id="b9310-136">`Html.BeginForm()` yardımcı yöntemi, açma ve kapatma HTML `<form>` etiketlerini oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b9310-136">The `Html.BeginForm()` Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="b9310-137">`Html.BeginForm()` yönteminin bir using ifadesinin içinde çağrıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="b9310-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="b9310-138">Using ifadesinde, using bloğunun sonunda `<form>` etiketinin kapalı olması güvence altına alınır.</span><span class="sxs-lookup"><span data-stu-id="b9310-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="b9310-139">Tercih ederseniz, bir using bloğu oluşturmak yerine, `<form>` etiketini kapatmak için HTML. EndForm () yardımcı yöntemini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9310-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="b9310-140">Size çok sezgisel bir açma ve kapatma `<form>` etiketi oluşturmak için hangi yaklaşımı kullanın.</span><span class="sxs-lookup"><span data-stu-id="b9310-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="b9310-141">`Html.TextBox()` yardımcı yöntemleri, HTML `<input>` etiketlerini işlemek için 1. liste ' de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b9310-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="b9310-142">Tarayıcınızda kaynağı görüntüle ' yi seçerseniz, liste 2 ' de HTML kaynağını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b9310-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="b9310-143">Kaynağın standart HTML etiketleri içerdiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b9310-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b9310-144">`Html.TextBox()`-HTML Yardımcısı 'nın `<% %>` etiketleri yerine `<%= %>` etiketleriyle işlendiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="b9310-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="b9310-145">Eşittir işaretini eklemezseniz, hiçbir şey tarayıcıya işlenmez.</span><span class="sxs-lookup"><span data-stu-id="b9310-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="b9310-146">ASP.NET MVC çerçevesi küçük bir yardımcılar kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="b9310-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="b9310-147">Büyük olasılıkla, MVC çerçevesini özel HTML yardımcılarını genişletmenize gerek duyarsınız.</span><span class="sxs-lookup"><span data-stu-id="b9310-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="b9310-148">Bu öğreticinin geri kalanında, özel HTML Yardımcıları oluşturmak için iki yöntem öğrenirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9310-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="b9310-149">**Listeleme 2 – `Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="b9310-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-shared-methods"></a><span data-ttu-id="b9310-150">Paylaşılan yöntemlerle HTML Yardımcıları oluşturma</span><span class="sxs-lookup"><span data-stu-id="b9310-150">Creating HTML Helpers with Shared Methods</span></span>

<span data-ttu-id="b9310-151">Yeni bir HTML Yardımcısı oluşturmanın en kolay yolu, bir dize döndüren paylaşılan bir yöntem oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="b9310-151">The easiest way to create a new HTML Helper is to create a shared method that returns a string.</span></span> <span data-ttu-id="b9310-152">Örneğin, bir HTML `<label>` etiketi oluşturan yeni bir HTML Yardımcısı oluşturmaya karar verdiğinizi düşünün.</span><span class="sxs-lookup"><span data-stu-id="b9310-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="b9310-153">Bir `<label>`işlemek için liste 2 ' de sınıfını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9310-153">You can use the class in Listing 2 to render a `<label>`.</span></span>

<span data-ttu-id="b9310-154">**Listeleme 2 – `Helpers\LabelHelper.vb`**</span><span class="sxs-lookup"><span data-stu-id="b9310-154">**Listing 2 – `Helpers\LabelHelper.vb`**</span></span>

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample3.vb)]

<span data-ttu-id="b9310-155">Kod 2 ' de sınıf hakkında özel bir şey yoktur.</span><span class="sxs-lookup"><span data-stu-id="b9310-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="b9310-156">`Label()` yöntemi yalnızca bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="b9310-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="b9310-157">Listeleme 3 ' teki değiştirilen dizin görünümü HTML `<label>` etiketlerini işlemek için `LabelHelper` kullanır.</span><span class="sxs-lookup"><span data-stu-id="b9310-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="b9310-158">Görünümün Application1. yardımcılar ad alanını içeri aktaran bir `<%@ imports %>` yönergesi içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="b9310-158">Notice that the view includes an `<%@ imports %>` directive that imports the Application1.Helpers namespace.</span></span>

<span data-ttu-id="b9310-159">**Listeleme 2 – `Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="b9310-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="b9310-160">Uzantı yöntemleriyle HTML Yardımcıları oluşturma</span><span class="sxs-lookup"><span data-stu-id="b9310-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="b9310-161">Yalnızca ASP.NET MVC çerçevesinin içerdiği standart HTML Yardımcıları gibi çalışan HTML Yardımcıları oluşturmak istiyorsanız, uzantı yöntemleri oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b9310-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="b9310-162">Uzantı yöntemleri varolan bir sınıfa yeni yöntemler eklemenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b9310-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="b9310-163">Bir HTML yardımcı yöntemi oluştururken, görünümün HTML özelliği tarafından temsil edilen `HtmlHelper` sınıfına yeni yöntemler eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="b9310-163">When creating an HTML Helper method, you add new methods to the `HtmlHelper` class represented by a view's Html property.</span></span>

<span data-ttu-id="b9310-164">Listeleme 3 ' teki Visual Basic modülü, `HtmlHelper` sınıfına `Label()` adlı bir uzantı yöntemi ekler.</span><span class="sxs-lookup"><span data-stu-id="b9310-164">The Visual Basic module in Listing 3 adds an extension method named `Label()` to the `HtmlHelper` class.</span></span> <span data-ttu-id="b9310-165">Bu modülle ilgili dikkat etmeniz gereken birkaç şey vardır.</span><span class="sxs-lookup"><span data-stu-id="b9310-165">There are a couple of things that you should notice about this module.</span></span> <span data-ttu-id="b9310-166">İlk olarak, modülün `<Extension()>` özniteliğiyle donatılmış olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="b9310-166">First, notice that the module is decorated with the `<Extension()>` attribute.</span></span> <span data-ttu-id="b9310-167">Bu özniteliği kullanabilmeniz için `System.Runtime.CompilerServices` ad alanını içeri aktarmanız gerekir</span><span class="sxs-lookup"><span data-stu-id="b9310-167">In order to use this attribute, you must import the `System.Runtime.CompilerServices` namespace</span></span>

<span data-ttu-id="b9310-168">İkincisi, `Label()` yönteminin ilk parametresinin `HtmlHelper` sınıfını temsil ettiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b9310-168">Second, notice that the first parameter of the `Label()` method represents the `HtmlHelper` class.</span></span> <span data-ttu-id="b9310-169">Bir genişletme yönteminin ilk parametresi, genişletme yönteminin genişlettiği sınıfı gösterir.</span><span class="sxs-lookup"><span data-stu-id="b9310-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="b9310-170">**Listeleme 3 – `Helpers\LabelExtensions.vb`**</span><span class="sxs-lookup"><span data-stu-id="b9310-170">**Listing 3 – `Helpers\LabelExtensions.vb`**</span></span>

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample5.vb)]

<span data-ttu-id="b9310-171">Bir genişletme yöntemi oluşturup uygulamanızı başarılı bir şekilde oluşturduktan sonra, genişletme yöntemi bir sınıfın tüm diğer yöntemleri gibi Visual Studio IntelliSense 'de görünür (bkz. Şekil 2).</span><span class="sxs-lookup"><span data-stu-id="b9310-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="b9310-172">Tek fark, genişletme yöntemlerinin bunların yanında özel bir simge (aşağı ok simgesi) ile görünme sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="b9310-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>

<span data-ttu-id="b9310-173">[HTML. Label () genişletme yöntemini kullanarak ![](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="b9310-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)</span></span>

<span data-ttu-id="b9310-174">**Şekil 02**: HTML. Label () genişletme yöntemini kullanma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-custom-html-helpers-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="b9310-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-vb/_static/image6.png))</span></span>

<span data-ttu-id="b9310-175">Liste 4 ' te değiştirilen dizin görünümü, tüm &lt;etiket&gt; etiketlerini işlemek için HTML. Label () genişletme yöntemini kullanır.</span><span class="sxs-lookup"><span data-stu-id="b9310-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its &lt;label&gt; tags.</span></span>

<span data-ttu-id="b9310-176">**Listeleme 4 – `Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="b9310-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="b9310-177">Özet</span><span class="sxs-lookup"><span data-stu-id="b9310-177">Summary</span></span>

<span data-ttu-id="b9310-178">Bu öğreticide, özel HTML Yardımcıları oluşturmak için iki yöntem öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="b9310-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="b9310-179">İlk olarak, bir dize döndüren paylaşılan bir yöntem oluşturarak özel bir `Label()` HTML Yardımcısı oluşturmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="b9310-179">First, you learned how to create a custom `Label()` HTML Helper by creating a shared method that returns a string.</span></span> <span data-ttu-id="b9310-180">Daha sonra, `HtmlHelper` sınıfında bir genişletme yöntemi oluşturarak özel bir `Label()` HTML Yardımcısı yöntemi oluşturmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="b9310-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="b9310-181">Bu öğreticide son derece basit bir HTML yardımcı yöntemi oluşturmaya odaklandım.</span><span class="sxs-lookup"><span data-stu-id="b9310-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="b9310-182">Bir HTML Yardımcısı 'nın istediğiniz kadar karmaşık olduğunu fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9310-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="b9310-183">Ağaç görünümleri, menüler veya veritabanı verilerinin tabloları gibi zengin içerik işleyen HTML Yardımcıları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9310-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b9310-184">[Önceki](asp-net-mvc-views-overview-vb.md)
> [İleri](using-the-tagbuilder-class-to-build-html-helpers-vb.md)</span><span class="sxs-lookup"><span data-stu-id="b9310-184">[Previous](asp-net-mvc-views-overview-vb.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-vb.md)</span></span>
