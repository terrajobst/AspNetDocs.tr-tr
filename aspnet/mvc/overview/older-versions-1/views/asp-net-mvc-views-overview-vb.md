---
uid: mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
title: ASP.NET MVC görünümlerine genel bakış (VB) | Microsoft Docs
author: StephenWalther
description: ASP.NET MVC görünümü nedir ve bir HTML sayfasından farklılık gösterir? Bu öğreticide, Stephen Walther size görünümleri ve nasıl yapılacağını gösterir...
ms.author: riande
ms.date: 02/16/2008
ms.assetid: c28ba88d-3a93-47f5-a306-049bd766714d
msc.legacyurl: /mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: f02728ed248f29b09d654e509977ed43889cbb83
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541309"
---
# <a name="aspnet-mvc-views-overview-vb"></a><span data-ttu-id="a7623-104">ASP.NET MVC Görünümlerine Genel Bakış (VB)</span><span class="sxs-lookup"><span data-stu-id="a7623-104">ASP.NET MVC Views Overview (VB)</span></span>

<span data-ttu-id="a7623-105">ile [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="a7623-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="a7623-106">ASP.NET MVC görünümü nedir ve bir HTML sayfasından farklılık gösterir?</span><span class="sxs-lookup"><span data-stu-id="a7623-106">What is an ASP.NET MVC View and how does it differ from a HTML page?</span></span> <span data-ttu-id="a7623-107">Bu öğreticide, Stephen Walther bir görünüm içinde verileri ve HTML yardımcılarını görüntülemeyi nasıl kullanabileceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="a7623-107">In this tutorial, Stephen Walther introduces you to Views and demonstrates how you can take advantage of View Data and HTML Helpers within a View.</span></span>

<span data-ttu-id="a7623-108">Bu öğreticinin amacı, ASP.NET MVC görünümleri, verileri görüntülemek ve HTML Yardımcıları hakkında kısa bir giriş sunmaktır.</span><span class="sxs-lookup"><span data-stu-id="a7623-108">The purpose of this tutorial is to provide you with a brief introduction to ASP.NET MVC views, view data, and HTML Helpers.</span></span> <span data-ttu-id="a7623-109">Bu öğreticinin sonunda, yeni görünümler oluşturmayı, bir denetleyiciden bir görünüme veri geçişi ve bir görünümde içerik oluşturmak için HTML Yardımcıları kullanmayı anlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="a7623-109">By the end of this tutorial, you should understand how to create new views, pass data from a controller to a view, and use HTML Helpers to generate content in a view.</span></span>

## <a name="understanding-views"></a><span data-ttu-id="a7623-110">Görünümleri anlama</span><span class="sxs-lookup"><span data-stu-id="a7623-110">Understanding Views</span></span>

<span data-ttu-id="a7623-111">ASP.NET veya Active Server sayfalarından farklı olarak, ASP.NET MVC doğrudan bir sayfaya karşılık gelen herhangi bir şeyi içermez.</span><span class="sxs-lookup"><span data-stu-id="a7623-111">Unlike ASP.NET or Active Server Pages, ASP.NET MVC does not include anything that directly corresponds to a page.</span></span> <span data-ttu-id="a7623-112">Bir ASP.NET MVC uygulamasında, bir diskte, tarayıcınızın adres çubuğuna yazdığınız URL 'deki yola karşılık gelen bir sayfa yoktur.</span><span class="sxs-lookup"><span data-stu-id="a7623-112">In an ASP.NET MVC application, there is not a page on disk that corresponds to the path in the URL that you type into the address bar of your browser.</span></span> <span data-ttu-id="a7623-113">ASP.NET MVC uygulamasındaki bir sayfaya en yakın şey, *Görünüm*olarak adlandırılan bir şeydir.</span><span class="sxs-lookup"><span data-stu-id="a7623-113">The closest thing to a page in an ASP.NET MVC application is something called a *view*.</span></span>

<span data-ttu-id="a7623-114">ASP.NET MVC uygulamasında, gelen tarayıcı istekleri denetleyici eylemlerine eşlenir.</span><span class="sxs-lookup"><span data-stu-id="a7623-114">In an ASP.NET MVC application, incoming browser requests are mapped to controller actions.</span></span> <span data-ttu-id="a7623-115">Bir denetleyici eylemi bir görünüm döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="a7623-115">A controller action might return a view.</span></span> <span data-ttu-id="a7623-116">Ancak, bir denetleyici eylemi sizi başka bir denetleyici eylemine yönlendirme gibi başka bir eylem türü gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="a7623-116">However, a controller action might perform some other type of action such as redirecting you to another controller action.</span></span>

<span data-ttu-id="a7623-117">Listeleme 1, HomeController adlı basit bir denetleyici içerir.</span><span class="sxs-lookup"><span data-stu-id="a7623-117">Listing 1 contains a simple controller named the HomeController.</span></span> <span data-ttu-id="a7623-118">HomeController, Index () ve details () adlı iki denetleyici eylemini kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="a7623-118">The HomeController exposes two controller actions named Index() and Details().</span></span>

<span data-ttu-id="a7623-119">**Listeleme 1-HomeController. vb**</span><span class="sxs-lookup"><span data-stu-id="a7623-119">**Listing 1 - HomeController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample1.vb)]

<span data-ttu-id="a7623-120">Tarayıcı adres çubuğuna aşağıdaki URL 'YI yazarak dizin () eylemini ilk eylemi çağırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a7623-120">You can invoke the first action, the Index() action, by typing the following URL into your browser address bar:</span></span>

<span data-ttu-id="a7623-121">/Home/Index</span><span class="sxs-lookup"><span data-stu-id="a7623-121">/Home/Index</span></span>

<span data-ttu-id="a7623-122">Bu adresi tarayıcınıza yazarak, ayrıntılar () eylemini ikinci eylemi çağırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a7623-122">You can invoke the second action, the Details() action, by typing this address into your browser:</span></span>

<span data-ttu-id="a7623-123">/Home/Details</span><span class="sxs-lookup"><span data-stu-id="a7623-123">/Home/Details</span></span>

<span data-ttu-id="a7623-124">Index () eylemi bir görünüm döndürür.</span><span class="sxs-lookup"><span data-stu-id="a7623-124">The Index() action returns a view.</span></span> <span data-ttu-id="a7623-125">Oluşturduğunuz çoğu eylem, görünümleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="a7623-125">Most actions that you create will return views.</span></span> <span data-ttu-id="a7623-126">Ancak, bir eylem diğer eylem sonuçları türlerini döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="a7623-126">However, an action can return other types of action results.</span></span> <span data-ttu-id="a7623-127">Örneğin, Details () eylemi, gelen isteği dizin () eylemine yönlendiren bir RedirectToActionResult döndürür.</span><span class="sxs-lookup"><span data-stu-id="a7623-127">For example, the Details() action returns a RedirectToActionResult that redirects incoming request to the Index() action.</span></span>

<span data-ttu-id="a7623-128">Index () eylemi aşağıdaki tek kod satırını içerir:</span><span class="sxs-lookup"><span data-stu-id="a7623-128">The Index() action contains the following single line of code:</span></span>

<span data-ttu-id="a7623-129">Görüntüleme ()</span><span class="sxs-lookup"><span data-stu-id="a7623-129">View()</span></span>

<span data-ttu-id="a7623-130">Bu kod satırı, Web sunucunuzdaki aşağıdaki yolda bulunması gereken bir görünüm döndürür:</span><span class="sxs-lookup"><span data-stu-id="a7623-130">This line of code returns a view that must be located at the following path on your web server:</span></span>

<span data-ttu-id="a7623-131">\Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="a7623-131">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="a7623-132">Görünümün yolu, denetleyicinin adından ve denetleyici eyleminin adıyla algılanır.</span><span class="sxs-lookup"><span data-stu-id="a7623-132">The path to the view is inferred from the name of the controller and the name of the controller action.</span></span>

<span data-ttu-id="a7623-133">İsterseniz, görünüm hakkında açık olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7623-133">If you prefer, you can be explicit about the view.</span></span> <span data-ttu-id="a7623-134">Aşağıdaki kod satırı, Fred adlı bir görünüm döndürür:</span><span class="sxs-lookup"><span data-stu-id="a7623-134">The following line of code returns a view named Fred :</span></span>

<span data-ttu-id="a7623-135">Görünüm (Fred)</span><span class="sxs-lookup"><span data-stu-id="a7623-135">View( Fred )</span></span>

<span data-ttu-id="a7623-136">Bu kod satırı yürütüldüğünde, aşağıdaki yoldan bir görünüm döndürülür:</span><span class="sxs-lookup"><span data-stu-id="a7623-136">When this line of code is executed, a view is returned from the following path:</span></span>

<span data-ttu-id="a7623-137">\Views\Home\Fred.aspx</span><span class="sxs-lookup"><span data-stu-id="a7623-137">\Views\Home\Fred.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="a7623-138">ASP.NET MVC uygulamanız için birim testleri oluşturmayı planlıyorsanız, görünüm adları hakkında açık olması iyi bir fikirdir.</span><span class="sxs-lookup"><span data-stu-id="a7623-138">If you plan to create unit tests for your ASP.NET MVC application then it is a good idea to be explicit about view names.</span></span> <span data-ttu-id="a7623-139">Bu şekilde, beklenen görünümün bir denetleyici eylemi tarafından döndürüldüğünü doğrulamak için bir birim testi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7623-139">That way, you can create a unit test to verify that the expected view was returned by a controller action.</span></span>

## <a name="adding-content-to-a-view"></a><span data-ttu-id="a7623-140">Görünüme Içerik ekleme</span><span class="sxs-lookup"><span data-stu-id="a7623-140">Adding Content to a View</span></span>

<span data-ttu-id="a7623-141">Görünüm, komut dosyaları içerebilen standart (X) HTML belgesidir.</span><span class="sxs-lookup"><span data-stu-id="a7623-141">A view is a standard (X)HTML document that can contain scripts.</span></span> <span data-ttu-id="a7623-142">Bir görünüme dinamik içerik eklemek için betikleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="a7623-142">You use scripts to add dynamic content to a view.</span></span>

<span data-ttu-id="a7623-143">Örneğin, liste 2 ' deki görünüm geçerli tarih ve saati gösterir.</span><span class="sxs-lookup"><span data-stu-id="a7623-143">For example, the view in Listing 2 displays the current date and time.</span></span>

<span data-ttu-id="a7623-144">**Listeleme 2-\Views\home\ındex.aspx**</span><span class="sxs-lookup"><span data-stu-id="a7623-144">**Listing 2 - \Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample2.aspx)]

<span data-ttu-id="a7623-145">Liste 2 ' deki HTML sayfasının gövdesi aşağıdaki betiği içerir:</span><span class="sxs-lookup"><span data-stu-id="a7623-145">Notice that the body of the HTML page in Listing 2 contains the following script:</span></span>

<span data-ttu-id="a7623-146">&lt;% Response. Write (DateTime. Now)%&gt;</span><span class="sxs-lookup"><span data-stu-id="a7623-146">&lt;% Response.Write(DateTime.Now)%&gt;</span></span>

<span data-ttu-id="a7623-147">Bir betiğin başlangıcını ve sonunu işaretlemek için% &lt;% ve%&gt; komut dosyası sınırlayıcılarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="a7623-147">You use the script delimiters &lt;% and %&gt; to mark the beginning and end of a script.</span></span> <span data-ttu-id="a7623-148">Bu betik, Visual Basic 'te yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="a7623-148">This script is written in Visual basic.</span></span> <span data-ttu-id="a7623-149">İçeriği tarayıcıya işlemek için Response. Write () yöntemini çağırarak geçerli tarih ve saati görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a7623-149">It displays the current date and time by calling the Response.Write() method to render content to the browser.</span></span> <span data-ttu-id="a7623-150">&lt;% ve%&gt; betik sınırlayıcıları bir veya daha fazla deyimi yürütmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a7623-150">The script delimiters &lt;% and %&gt; can be used to execute one or more statements.</span></span>

<span data-ttu-id="a7623-151">Genellikle Response. Write () çağrısı yaptığından, Microsoft size Response. Write () metodunu çağırma için bir kısayol sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7623-151">Since you call Response.Write() so often, Microsoft provides you with a shortcut for calling the Response.Write() method.</span></span> <span data-ttu-id="a7623-152">Listeleme 3 ' teki görünüm, yanıt. Write () çağrısı için bir kısayol olarak &lt;% = ve%&gt; sınırlayıcılarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="a7623-152">The view in Listing 3 uses the delimiters &lt;%= and %&gt; as a shortcut for calling Response.Write().</span></span>

<span data-ttu-id="a7623-153">**Listeleme 3-Views\home\ındex2,aspx**</span><span class="sxs-lookup"><span data-stu-id="a7623-153">**Listing 3 - Views\Home\Index2.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample3.aspx)]

<span data-ttu-id="a7623-154">Bir görünümde dinamik içerik oluşturmak için herhangi bir .NET dili kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7623-154">You can use any .NET language to generate dynamic content in a view.</span></span> <span data-ttu-id="a7623-155">Normalde, Visual Basic .NET veya C# denetleyicilerinizi ve görünümlerinizi yazmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="a7623-155">Normally, you�ll use either Visual Basic .NET or C# to write your controllers and views.</span></span>

## <a name="using-html-helpers-to-generate-view-content"></a><span data-ttu-id="a7623-156">Görünüm Içeriği oluşturmak için HTML Yardımcıları kullanma</span><span class="sxs-lookup"><span data-stu-id="a7623-156">Using HTML Helpers to Generate View Content</span></span>

<span data-ttu-id="a7623-157">Bir görünüme içerik eklemenizi kolaylaştırmak için, *HTML Yardımcısı*adlı bir şeyin avantajlarından yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7623-157">To make it easier to add content to a view, you can take advantage of something called an *HTML Helper*.</span></span> <span data-ttu-id="a7623-158">Genellikle bir HTML Yardımcısı, bir dize üreten bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="a7623-158">An HTML Helper, typically, is a method that generates a string.</span></span> <span data-ttu-id="a7623-159">HTML Yardımcıları, metin kutuları, bağlantılar, açılan listeler ve liste kutuları gibi standart HTML öğeleri oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7623-159">You can use HTML Helpers to generate standard HTML elements such as textboxes, links, dropdown lists, and list boxes.</span></span>

<span data-ttu-id="a7623-160">Örneğin, kod 4 ' teki görünüm üç HTML yardımcıdan faydalanır: BeginForm (), TextBox () ve Password () yardımcıları--oturum açma formu oluşturmak için (bkz. Şekil 1).</span><span class="sxs-lookup"><span data-stu-id="a7623-160">For example, the view in Listing 4 takes advantage of three HTML Helpers -- the BeginForm(), the TextBox() and Password() helpers -- to generate a Login form (see Figure 1).</span></span>

<span data-ttu-id="a7623-161">**Listeleme 4--\Views\Home\Login.aspx**</span><span class="sxs-lookup"><span data-stu-id="a7623-161">**Listing 4 -- \Views\Home\Login.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample4.aspx)]

<span data-ttu-id="a7623-162">[Yeni proje iletişim kutusunu ![](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a7623-162">[![The New Project dialog box](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)</span></span>

<span data-ttu-id="a7623-163">**Şekil 01**: standart bir oturum açma formu ([tam boyutlu görüntüyü görüntülemek için tıklayın](asp-net-mvc-views-overview-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="a7623-163">**Figure 01**: A standard Login form ([Click to view full-size image](asp-net-mvc-views-overview-vb/_static/image2.png))</span></span>

<span data-ttu-id="a7623-164">HTML yardımcılarının tümü, görünümün HTML özelliğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="a7623-164">All of the HTML Helpers methods are called on the Html property of the view.</span></span> <span data-ttu-id="a7623-165">Örneğin, HTML. TextBox () yöntemini çağırarak bir metin kutusunu işleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7623-165">For example, you render a TextBox by calling the Html.TextBox() method.</span></span>

<span data-ttu-id="a7623-166">Hem HTML. TextBox () hem de HTML. Password () yardımcıları çağrılırken% = ve%&gt; &lt;komut dosyası sınırlayıcılarının kullanıldığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a7623-166">Notice that you use the script delimiters &lt;%= and %&gt; when calling both the Html.TextBox() and Html.Password() helpers.</span></span> <span data-ttu-id="a7623-167">Bu yardımcılar yalnızca bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="a7623-167">These helpers simply return a string.</span></span> <span data-ttu-id="a7623-168">Dizeyi tarayıcıya işlemek için Response. Write () çağrısı yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7623-168">You need to call Response.Write() in order to render the string to the browser.</span></span>

<span data-ttu-id="a7623-169">HTML Yardımcısı yöntemlerini kullanmak isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="a7623-169">Using HTML Helper methods is optional.</span></span> <span data-ttu-id="a7623-170">Yazmanız gereken HTML ve betiğin miktarını azaltarak yaşamınızı daha kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="a7623-170">They make your life easier by reducing the amount of HTML and script that you need to write.</span></span> <span data-ttu-id="a7623-171">Listeleme 5 ' teki görünüm, HTML Yardımcıları kullanmadan liste 4 ' teki görünümle tam olarak aynı formu işler.</span><span class="sxs-lookup"><span data-stu-id="a7623-171">The view in Listing 5 renders the exact same form as the view in Listing 4 without using HTML Helpers.</span></span>

<span data-ttu-id="a7623-172">**Listeleme 5--\Views\Home\Login.aspx**</span><span class="sxs-lookup"><span data-stu-id="a7623-172">**Listing 5 -- \Views\Home\Login.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample5.aspx)]

<span data-ttu-id="a7623-173">Kendi HTML Yardımcıları oluşturma seçeneğiniz de vardır.</span><span class="sxs-lookup"><span data-stu-id="a7623-173">You also have the option of creating your own HTML Helpers.</span></span> <span data-ttu-id="a7623-174">Örneğin, bir HTML tablosunda otomatik olarak bir veritabanı kaydı kümesi görüntüleyen bir GridView () yardımcı yöntemi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7623-174">For example, you can create a GridView() helper method that displays a set of database records in an HTML table automatically.</span></span> <span data-ttu-id="a7623-175">Bu konu, **özel HTML Yardımcıları oluşturma**öğreticisinde araştırıyoruz.</span><span class="sxs-lookup"><span data-stu-id="a7623-175">We explore this topic in the tutorial **Creating Custom HTML Helpers**.</span></span>

## <a name="using-view-data-to-pass-data-to-a-view"></a><span data-ttu-id="a7623-176">Verileri görünüme geçirmek için Görünüm verilerini kullanma</span><span class="sxs-lookup"><span data-stu-id="a7623-176">Using View Data to Pass Data to a View</span></span>

<span data-ttu-id="a7623-177">Bir denetleyiciden bir görünüme veri geçirmek için verileri görüntüle 'yi kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="a7623-177">You use view data to pass data from a controller to a view.</span></span> <span data-ttu-id="a7623-178">Verileri posta aracılığıyla göndereceğiniz bir paket gibi görüntülemeyi düşünün.</span><span class="sxs-lookup"><span data-stu-id="a7623-178">Think of view data like a package that you send through the mail.</span></span> <span data-ttu-id="a7623-179">Bir denetleyiciden bir görünüme geçirilen tüm verilerin bu paket kullanılarak gönderilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7623-179">All data passed from a controller to a view must be sent using this package.</span></span> <span data-ttu-id="a7623-180">Örneğin, liste 6 ' daki denetleyici verileri görüntülemek için bir ileti ekler.</span><span class="sxs-lookup"><span data-stu-id="a7623-180">For example, the controller in Listing 6 adds a message to view data.</span></span>

<span data-ttu-id="a7623-181">**6-ProductController. vb dosyasını listeleme**</span><span class="sxs-lookup"><span data-stu-id="a7623-181">**Listing 6 - ProductController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample6.vb)]

<span data-ttu-id="a7623-182">Controller ViewData özelliği bir ad ve değer çiftleri koleksiyonunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="a7623-182">The controller ViewData property represents a collection of name and value pairs.</span></span> <span data-ttu-id="a7623-183">Liste 6 ' da, Index () yöntemi, Merhaba Dünya! değerine sahip ileti adlı görünüm verileri koleksiyonuna bir öğe ekler.</span><span class="sxs-lookup"><span data-stu-id="a7623-183">In Listing 6, the Index() method adds an item to the view data collection named message with the value Hello World!.</span></span> <span data-ttu-id="a7623-184">Görünüm, Index () yöntemiyle döndürüldüğünde görünüm verileri otomatik olarak görünüme geçirilir.</span><span class="sxs-lookup"><span data-stu-id="a7623-184">When the view is returned by the Index() method, the view data is passed to the view automatically.</span></span>

<span data-ttu-id="a7623-185">Liste 7 ' deki görünüm, verileri görünüm verilerinden alır ve iletiyi tarayıcıya işler.</span><span class="sxs-lookup"><span data-stu-id="a7623-185">The view in Listing 7 retrieves the message from the view data and renders the message to the browser.</span></span>

<span data-ttu-id="a7623-186">**Listeleme 7--\Views\product\ındex.aspx**</span><span class="sxs-lookup"><span data-stu-id="a7623-186">**Listing 7 -- \Views\Product\Index.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample7.aspx)]

<span data-ttu-id="a7623-187">Görünümün, iletiyi işlerken HTML. Encode () HTML yardımcı yönteminden yararlandığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a7623-187">Notice that the view takes advantage of the Html.Encode() HTML Helper method when rendering the message.</span></span> <span data-ttu-id="a7623-188">HTML. Encode () HTML Yardımcısı, &lt; gibi özel karakterleri ve bir Web sayfasında görüntülenmek üzere güvenli karakterler halinde &gt; kodlar.</span><span class="sxs-lookup"><span data-stu-id="a7623-188">The Html.Encode() HTML Helper encodes special characters such as &lt; and &gt; into characters that are safe to display in a web page.</span></span> <span data-ttu-id="a7623-189">Bir kullanıcının bir Web sitesine gönderdiği içeriği her oluşturduğunuzda, JavaScript ekleme saldırılarını engellemek için içeriği kodlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7623-189">Whenever you render content that a user submits to a website, you should encode the content to prevent JavaScript injection attacks.</span></span>

<span data-ttu-id="a7623-190">(ProductController 'da kendimize iletisini oluşturduğumuz için, gerçekten iletiyi kodlamak zorunda kalmaz.</span><span class="sxs-lookup"><span data-stu-id="a7623-190">(Because we created the message ourselves in the ProductController, we don�t really need to encode the message.</span></span> <span data-ttu-id="a7623-191">Ancak, görünümün içindeki verilerden alınan içeriği görüntülerken, her zaman HTML. Encode () yöntemini çağırmak iyi bir alışkanlıktır.)</span><span class="sxs-lookup"><span data-stu-id="a7623-191">However, it is a good habit to always call the Html.Encode() method when displaying content retrieved from view data within a view.)</span></span>

<span data-ttu-id="a7623-192">Liste 7 ' de, bir denetleyiciden bir görünüme basit bir dize iletisi geçirmek için verileri görüntüle ' den faydalanır.</span><span class="sxs-lookup"><span data-stu-id="a7623-192">In Listing 7, we took advantage of view data to pass a simple string message from a controller to a view.</span></span> <span data-ttu-id="a7623-193">Ayrıca, veritabanı kayıtlarının bir koleksiyonu gibi diğer veri türlerini bir denetleyiciden bir görünüme geçirmek için verileri görüntüle ' yi de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7623-193">You also can use view data to pass other types of data, such as a collection of database records, from a controller to a view.</span></span> <span data-ttu-id="a7623-194">Örneğin, Products veritabanı tablosunun içeriğini bir görünümde görüntülemek istiyorsanız, veritabanı kayıtlarının koleksiyonunu görünüm verilerinde geçitirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7623-194">For example, if you want to display the contents of the Products database table in a view, then you would pass the collection of database records in view data.</span></span>

<span data-ttu-id="a7623-195">Bir denetleyiciden bir görünüme kesin olarak belirlenmiş görünüm verisi geçirme seçeneğiniz de vardır.</span><span class="sxs-lookup"><span data-stu-id="a7623-195">You also have the option of passing strongly typed view data from a controller to a view.</span></span> <span data-ttu-id="a7623-196">Bu konuyu, **kesin türü belirtilmiş Görünüm verilerini ve görünümlerini anlama**öğreticisinde araştırıyoruz.</span><span class="sxs-lookup"><span data-stu-id="a7623-196">We explore this topic in the tutorial **Understanding Strongly Typed View Data and Views**.</span></span>

## <a name="summary"></a><span data-ttu-id="a7623-197">Özet</span><span class="sxs-lookup"><span data-stu-id="a7623-197">Summary</span></span>

<span data-ttu-id="a7623-198">Bu öğreticide, ASP.NET MVC görünümleri, verileri görüntüleme ve HTML Yardımcıları hakkında kısa bir giriş sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a7623-198">This tutorial provided a brief introduction to ASP.NET MVC views, view data, and HTML Helpers.</span></span> <span data-ttu-id="a7623-199">İlk bölümde, projenize yeni görünümler eklemeyi öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="a7623-199">In the first section, you learned how to add new views to your project.</span></span> <span data-ttu-id="a7623-200">Belirli bir denetleyiciden çağırmak için doğru klasöre bir görünüm eklemeniz gerektiğini öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="a7623-200">You learned that you must add a view to the right folder in order to call it from a particular controller.</span></span> <span data-ttu-id="a7623-201">Daha sonra, HTML yardımcılarını ele aldık.</span><span class="sxs-lookup"><span data-stu-id="a7623-201">Next, we discussed the topic of HTML Helpers.</span></span> <span data-ttu-id="a7623-202">HTML yardımcıların standart HTML içeriğini kolayca oluşturmanıza nasıl imkan sağladığını öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="a7623-202">You learned how HTML Helpers enable you to easily generate standard HTML content.</span></span> <span data-ttu-id="a7623-203">Son olarak, bir denetleyiciden bir görünüme veri geçirmek için verileri görüntüleme özelliğinden nasıl yararlanırsınız hakkında öğrenirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7623-203">Finally, you learned how to take advantage of view data to pass data from a controller to a view.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a7623-204">[Önceki](passing-data-to-view-master-pages-cs.md)
> [İleri](creating-custom-html-helpers-vb.md)</span><span class="sxs-lookup"><span data-stu-id="a7623-204">[Previous](passing-data-to-view-master-pages-cs.md)
[Next](creating-custom-html-helpers-vb.md)</span></span>
