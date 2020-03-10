---
uid: web-pages/overview/getting-started/introducing-razor-syntax-vb
title: Razor söz dizimini kullanarak ASP.NET Web programlamaya giriş (Visual Basic) | Microsoft Docs
author: Rick-Anderson
description: Bu ekte, Razor söz dizimi kullanarak Visual Basic Web sayfaları ile programlamaya genel bakış sunulmaktadır.
ms.author: riande
ms.date: 02/07/2014
ms.assetid: 5da59646-e973-41cd-88a9-c6b2c0594027
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-vb
msc.type: authoredcontent
ms.openlocfilehash: 2be57655b8c9b76b94e1d9a7ae5fbee27545a0a9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78526595"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-visual-basic"></a><span data-ttu-id="0876c-103">Razor söz dizimini kullanarak ASP.NET Web programlamaya giriş (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="0876c-103">Introduction to ASP.NET Web Programming Using the Razor Syntax (Visual Basic)</span></span>

<span data-ttu-id="0876c-104">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="0876c-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="0876c-105">Bu makalede, Razor söz dizimi ve Visual Basic kullanarak ASP.NET Web sayfalarıyla programlama hakkında genel bakış sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0876c-105">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax and Visual Basic.</span></span> <span data-ttu-id="0876c-106">ASP.NET, Microsoft 'un web sunucularında dinamik Web sayfaları çalıştırmaya yönelik teknolojisidir.</span><span class="sxs-lookup"><span data-stu-id="0876c-106">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span>
> 
> <span data-ttu-id="0876c-107">Şunları **öğreneceksiniz**:</span><span class="sxs-lookup"><span data-stu-id="0876c-107">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="0876c-108">Razor söz dizimi kullanarak programlama ASP.NET Web sayfaları ile çalışmaya başlama için en iyi 8 programlama ipuçları.</span><span class="sxs-lookup"><span data-stu-id="0876c-108">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="0876c-109">İhtiyaç duyacağınız temel programlama kavramları.</span><span class="sxs-lookup"><span data-stu-id="0876c-109">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="0876c-110">ASP.NET sunucu kodu ve Razor söz dizimi hepsi ile ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="0876c-110">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="0876c-111">Yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="0876c-111">Software versions</span></span>
> 
> 
> - <span data-ttu-id="0876c-112">ASP.NET Web sayfaları (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="0876c-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="0876c-113">Bu öğretici, ASP.NET Web Pages 2 ile de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0876c-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<span data-ttu-id="0876c-114">Razor söz dizimi kullanımı C#Ile ASP.NET Web sayfaları kullanmanın çoğu örneği.</span><span class="sxs-lookup"><span data-stu-id="0876c-114">Most examples of using ASP.NET Web Pages with Razor syntax use C#.</span></span> <span data-ttu-id="0876c-115">Ancak Razor söz dizimi de Visual Basic destekler.</span><span class="sxs-lookup"><span data-stu-id="0876c-115">But the Razor syntax also supports Visual Basic.</span></span> <span data-ttu-id="0876c-116">Visual Basic bir ASP.NET Web sayfasını programlamak için *. vbhtml* dosya adı uzantısıyla bir Web sayfası oluşturun ve sonra Visual Basic kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0876c-116">To program an ASP.NET web page in Visual Basic, you create a web page with a *.vbhtml* filename extension, and then add Visual Basic code.</span></span> <span data-ttu-id="0876c-117">Bu makalede, ASP.NET Web sayfaları oluşturmak için Visual Basic dili ve söz dizimi ile çalışmaya ilişkin bir genel bakış sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0876c-117">This article gives you an overview of working with the Visual Basic language and syntax to create ASP.NET Webpages.</span></span>

> [!NOTE]
> <span data-ttu-id="0876c-118">Microsoft WebMatrix için varsayılan Web sitesi şablonları (**Bakçılık**, **Fotoğraf Galerisi**ve **Başlangıç sitesi**, vb.), C# ve Visual Basic sürümlerde mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="0876c-118">The default website templates for Microsoft WebMatrix (**Bakery**, **Photo Gallery**, and **Starter Site**, etc.) are available in C# and Visual Basic versions.</span></span> <span data-ttu-id="0876c-119">Visual Basic şablonlarını NuGet paketleri olarak yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-119">You can install the Visual Basic templates by as NuGet packages.</span></span> <span data-ttu-id="0876c-120">Web sitesi şablonları, sitenizin kök klasörüne *Microsoft şablonlar*adlı bir klasöre yüklenir.</span><span class="sxs-lookup"><span data-stu-id="0876c-120">Website templates are installed in the root folder of your site in a folder named *Microsoft Templates*.</span></span>

## <a name="the-top-8-programming-tips"></a><span data-ttu-id="0876c-121">Ilk 8 programlama Ipuçları</span><span class="sxs-lookup"><span data-stu-id="0876c-121">The Top 8 Programming Tips</span></span>

<span data-ttu-id="0876c-122">Bu bölümde, Razor söz dizimi kullanarak ASP.NET sunucu kodu yazmaya başladığınızda kesinlikle bilmeniz gereken birkaç ipucu listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="0876c-122">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="0876c-123">1. @ karakterini kullanarak bir sayfaya kod eklersiniz</span><span class="sxs-lookup"><span data-stu-id="0876c-123">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="0876c-124">`@` karakter, satır içi ifadeler, tek deyim blokları ve çok deyimli bloklar başlatır:</span><span class="sxs-lookup"><span data-stu-id="0876c-124">The `@` character starts inline expressions, single-statement blocks, and multi-statement blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample1.vbhtml)]

<span data-ttu-id="0876c-125">Bir tarayıcıda gösterilecek Sonuç:</span><span class="sxs-lookup"><span data-stu-id="0876c-125">The result displayed in a browser:</span></span>

![Razor-Img1](introducing-razor-syntax-vb/_static/image1.jpg)

> [!TIP] 
> 
> <span data-ttu-id="0876c-127">**HTML kodlaması**</span><span class="sxs-lookup"><span data-stu-id="0876c-127">**HTML Encoding**</span></span>
> 
> <span data-ttu-id="0876c-128">Önceki örneklerde olduğu gibi, `@` karakterini kullanarak bir sayfada içerik görüntülediğinizde, ASP.NET HTML-, çıktıyı kodluyor.</span><span class="sxs-lookup"><span data-stu-id="0876c-128">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="0876c-129">Bu, ayrılmış HTML karakterlerinin (`<` ve `>` ve `&`), karakterlerin HTML etiketleri veya varlıklar olarak yorumlanıp bir Web sayfasında karakter olarak görüntülenmesini sağlayan kodlarla değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="0876c-129">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="0876c-130">HTML kodlaması olmadan, sunucu kodunuzun çıktısı doğru görüntülenmeyebilir ve güvenlik risklerine karşı bir sayfa sunabilir.</span><span class="sxs-lookup"><span data-stu-id="0876c-130">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="0876c-131">Amacınız etiketleri biçimlendirme olarak işleyen (örneğin, bir paragraf için `<p></p>` ya da metin vurgulamak için `<em></em>`) HTML işaretlemesinin çıktısını alıyorsa, bu makalenin ilerleyen kısımlarında yer alan [kod bloklarında metin, biçimlendirme ve kod birleştirme](#BM_CombiningTextMarkupAndCode) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="0876c-131">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="0876c-132">HTML kodlaması hakkında daha fazla bilgi için [ASP.NET Web sayfaları SITELERINDE HTML formlarıyla çalışma](https://go.microsoft.com/fwlink/?LinkId=202892)makalesini okuyun.</span><span class="sxs-lookup"><span data-stu-id="0876c-132">You can read more about HTML encoding in [Working with HTML Forms in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>

### <a name="2-you-enclose-code-blocks-with-codeend-code"></a><span data-ttu-id="0876c-133">2. kod bloklarını kodla çevrele... Son kod</span><span class="sxs-lookup"><span data-stu-id="0876c-133">2. You enclose code blocks with Code...End Code</span></span>

<span data-ttu-id="0876c-134">Bir kod bloğu bir veya daha fazla kod deyimi içerir ve `Code` ve `End Code`anahtar sözcükleriyle alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="0876c-134">A code block includes one or more code statements and is enclosed with the keywords `Code` and `End Code`.</span></span> <span data-ttu-id="0876c-135">Açma `Code` anahtar sözcüğünü `@` karakterden &#8212; hemen sonra yerleştirin, aralarında boşluk olamaz.</span><span class="sxs-lookup"><span data-stu-id="0876c-135">Place the opening `Code` keyword immediately after the `@` character &#8212; there can't be whitespace between them.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample2.vbhtml)]

<span data-ttu-id="0876c-136">Bir tarayıcıda gösterilecek Sonuç:</span><span class="sxs-lookup"><span data-stu-id="0876c-136">The result displayed in a browser:</span></span>

![Razor-Img2](introducing-razor-syntax-vb/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-line-break"></a><span data-ttu-id="0876c-138">3. bir blok içinde her bir kod ifadesini satır sonuyla sonlandırın</span><span class="sxs-lookup"><span data-stu-id="0876c-138">3. Inside a block, you end each code statement with a line break</span></span>

<span data-ttu-id="0876c-139">Visual Basic bir kod bloğunda, her bir ifade bir satır sonuyla biter.</span><span class="sxs-lookup"><span data-stu-id="0876c-139">In a Visual Basic code block, each statement ends with a line break.</span></span> <span data-ttu-id="0876c-140">(Makalede daha sonra, uzun bir kod ifadesini, gerekirse birden çok satıra sarmanın bir yolunu görürsünüz.)</span><span class="sxs-lookup"><span data-stu-id="0876c-140">(Later in the article you'll see a way to wrap a long code statement into multiple lines if needed.)</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample3.vbhtml)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="0876c-141">4. değerleri depolamak için değişkenleri kullanırsınız</span><span class="sxs-lookup"><span data-stu-id="0876c-141">4. You use variables to store values</span></span>

<span data-ttu-id="0876c-142">Değerleri dizeler, sayılar ve tarihler gibi bir *değişkende*saklayabilirsiniz. `Dim` anahtar sözcüğünü kullanarak yeni bir değişken oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="0876c-142">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `Dim` keyword.</span></span> <span data-ttu-id="0876c-143">`@`kullanarak doğrudan bir sayfada değişken değerleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-143">You can insert variable values directly in a page using `@`.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample4.vbhtml)]

<span data-ttu-id="0876c-144">Bir tarayıcıda gösterilecek Sonuç:</span><span class="sxs-lookup"><span data-stu-id="0876c-144">The result displayed in a browser:</span></span>

![Razor-IMG3](introducing-razor-syntax-vb/_static/image3.jpg)

### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="0876c-146">5. sabit dize değerlerini çift tırnak işaretleri içine alın</span><span class="sxs-lookup"><span data-stu-id="0876c-146">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="0876c-147">*Dize* , metin olarak kabul edilen bir karakter dizisidir.</span><span class="sxs-lookup"><span data-stu-id="0876c-147">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="0876c-148">Bir dize belirtmek için, bunu çift tırnak işareti içine alın:</span><span class="sxs-lookup"><span data-stu-id="0876c-148">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample5.vbhtml)]

<span data-ttu-id="0876c-149">Bir dize değeri içinde çift tırnak işaretleri eklemek için iki çift tırnak işareti karakteri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0876c-149">To embed double quotation marks within a string value, insert two double quotation mark characters.</span></span> <span data-ttu-id="0876c-150">Çift tırnak karakterinin sayfa çıktısında bir kez görünmesini istiyorsanız, tırnak içine alınan dize içinde `""` olarak girin ve iki kez görünmesini istiyorsanız, tırnak içine alınan dize içinde `""""` girin.</span><span class="sxs-lookup"><span data-stu-id="0876c-150">If you want the double quotation character to appear once in the page output, enter it as `""` within the quoted string, and if you want it to appear twice, enter it as `""""` within the quoted string.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample6.vbhtml)]

<span data-ttu-id="0876c-151">Bir tarayıcıda gösterilecek Sonuç:</span><span class="sxs-lookup"><span data-stu-id="0876c-151">The result displayed in a browser:</span></span>

![Razor-Img4](introducing-razor-syntax-vb/_static/image4.jpg)

### <a name="6-visual-basic-code-is-not-case-sensitive"></a><span data-ttu-id="0876c-153">6. Visual Basic kod büyük/küçük harfe duyarlı değildir</span><span class="sxs-lookup"><span data-stu-id="0876c-153">6. Visual Basic code is not case sensitive</span></span>

<span data-ttu-id="0876c-154">Visual Basic dili, büyük/küçük harfe duyarlı değildir.</span><span class="sxs-lookup"><span data-stu-id="0876c-154">The Visual Basic language is not case sensitive.</span></span> <span data-ttu-id="0876c-155">Programlama anahtar sözcükleri (`Dim`, `If`ve `True`gibi) ve değişken adları (`myString`veya `subTotal`gibi) herhangi bir durumda yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="0876c-155">Programming keywords (like `Dim`, `If`, and `True`) and variable names (like `myString`, or `subTotal`) can be written in any case.</span></span>

<span data-ttu-id="0876c-156">Aşağıdaki kod satırları, küçük harfli bir ad kullanarak `lastname` değişkenine bir değer atar ve ardından değişken değerini büyük bir ad kullanarak sayfaya dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="0876c-156">The following lines of code assign a value to the variable `lastname` using a lowercase name, and then output the variable value to the page using an uppercase name.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample7.vbhtml)]

<span data-ttu-id="0876c-157">Bir tarayıcıda gösterilecek Sonuç:</span><span class="sxs-lookup"><span data-stu-id="0876c-157">The result displayed in a browser:</span></span>

![vb-söz dizimi-5](introducing-razor-syntax-vb/_static/image5.jpg)

### <a name="7-much-of-your-coding-involves-working-with-objects"></a><span data-ttu-id="0876c-159">7. kodlarınızın büyük bölümü nesnelerle çalışmayı içerir</span><span class="sxs-lookup"><span data-stu-id="0876c-159">7. Much of your coding involves working with objects</span></span>

<span data-ttu-id="0876c-160">Bir nesne, bir sayfa, metin kutusu, dosya &#8212; , görüntü, Web isteği, e-posta iletisi, müşteri kaydı (veritabanı satırı) vb. ile programlama yapamayacağınız şeyi temsil eder. Nesneler, özelliklerini &#8212; tanımlayan özellikleri içerir metin kutusu nesnesi bir `Text` özelliğine sahiptir, bir istek nesnesi bir `Url` özelliğine sahiptir, bir e-posta iletisi bir `From` özelliğine sahiptir ve bir müşteri nesnesi bir `FirstName` özelliğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0876c-160">An object represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics &#8212; a text box object has a `Text` property, a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="0876c-161">Nesneler, gerçekleştirebilecekleri&quot; &quot;fiiller olan yöntemlere de sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0876c-161">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="0876c-162">Bir dosya nesnesinin `Save` yöntemi, bir görüntü nesnesinin `Rotate` yöntemi ve bir e-posta nesnesinin `Send` yöntemi sayılabilir.</span><span class="sxs-lookup"><span data-stu-id="0876c-162">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="0876c-163">Genellikle sayfadaki (metin kutuları, vb.) form alanlarının değerleri, istek ne tür bir tarayıcı, Kullanıcı kimliği, vb. gibi bilgiler sağlayan `Request` nesnesiyle çalışırsınız. Bu örnek, `Request` nesnesinin özelliklerine nasıl erişileceğinin yanı sıra sunucu üzerinde sayfanın mutlak yolunu sağlayan `Request` nesnesinin `MapPath` yönteminin nasıl çağrılacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="0876c-163">You'll often work with the `Request` object, which gives you information like the values of form fields on the page (text boxes, etc.), what type of browser made the request, the URL of the page, the user identity, etc. This example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample8.html)]

<span data-ttu-id="0876c-164">Bir tarayıcıda gösterilecek Sonuç:</span><span class="sxs-lookup"><span data-stu-id="0876c-164">The result displayed in a browser:</span></span>

![Razor-Img5](introducing-razor-syntax-vb/_static/image6.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="0876c-166">8. kararları veren kodu yazabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0876c-166">8. You can write code that makes decisions</span></span>

<span data-ttu-id="0876c-167">Dinamik Web sayfalarının temel bir özelliği, koşullara göre ne yapılacağını belirleyebileceğinize bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="0876c-167">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="0876c-168">Bunu yapmanın en yaygın yolu `If` deyimidir (ve isteğe bağlı `Else` deyimidir).</span><span class="sxs-lookup"><span data-stu-id="0876c-168">The most common way to do this is with the `If` statement (and optional `Else` statement).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample9.vbhtml)]

<span data-ttu-id="0876c-169">`If IsPost` ifade, `If IsPost = True`yazmanın bir Özet yoludur.</span><span class="sxs-lookup"><span data-stu-id="0876c-169">The statement `If IsPost` is a shorthand way of writing `If IsPost = True`.</span></span> <span data-ttu-id="0876c-170">`If` deyimleriyle birlikte, bu makalenin ilerleyen kısımlarında açıklanan koşulları test etme, kod blokları yineleme ve benzeri birçok yol vardır.</span><span class="sxs-lookup"><span data-stu-id="0876c-170">Along with `If` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="0876c-171">Sonuç tarayıcıda ( **Gönder**'e tıklandıktan sonra) gösterilir:</span><span class="sxs-lookup"><span data-stu-id="0876c-171">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor-Img6](introducing-razor-syntax-vb/_static/image7.jpg)

> [!TIP] 
> 
> <span data-ttu-id="0876c-173">**HTTP GET ve POST yöntemleri ve ıspost özelliği**</span><span class="sxs-lookup"><span data-stu-id="0876c-173">**HTTP GET and POST Methods and the IsPost Property**</span></span>
> 
> <span data-ttu-id="0876c-174">Web sayfaları (HTTP) için kullanılan protokol, sunucuya istek yapmak için kullanılan çok sınırlı sayıda yöntemi (&quot;fiiller&quot;) destekler.</span><span class="sxs-lookup"><span data-stu-id="0876c-174">The protocol used for web pages (HTTP) supports a very limited number of methods (&quot;verbs&quot;) that are used to make requests to the server.</span></span> <span data-ttu-id="0876c-175">En yaygın iki tane, bir sayfayı okumak için kullanılan ve bir sayfayı göndermek için kullanılan POST ' dır.</span><span class="sxs-lookup"><span data-stu-id="0876c-175">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="0876c-176">Genellikle, Kullanıcı ilk kez bir sayfa istediğinde, sayfa GET kullanılarak istenir.</span><span class="sxs-lookup"><span data-stu-id="0876c-176">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="0876c-177">Kullanıcı bir formu doldurduğunda ve **Gönder**' e tıkladığında, tarayıcı sunucuya bir post isteği yapar.</span><span class="sxs-lookup"><span data-stu-id="0876c-177">If the user fills in a form and then clicks **Submit**, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="0876c-178">Web programlamada, sayfayı nasıl işleyeceğini bilmeniz için bir sayfanın GET veya POST olarak istenmekte olduğunu bilmeniz genellikle yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="0876c-178">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="0876c-179">ASP.NET Web sayfalarında, bir isteğin bir GET veya POST olup olmadığını görmek için `IsPost` özelliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-179">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="0876c-180">İstek bir GÖNDERIME ise, `IsPost` özelliği true döndürür ve bir formdaki metin kutularının değerlerini okumak gibi şeyler yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-180">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="0876c-181">Birçok örnek, `IsPost`değerine bağlı olarak sayfayı farklı şekilde nasıl işleyeceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="0876c-181">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>

## <a name="a-simple-code-example"></a><span data-ttu-id="0876c-182">Basit bir kod örneği</span><span class="sxs-lookup"><span data-stu-id="0876c-182">A Simple Code Example</span></span>

<span data-ttu-id="0876c-183">Bu yordamda, temel programlama tekniklerini gösteren bir sayfanın nasıl oluşturulacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="0876c-183">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="0876c-184">Örnekte, kullanıcıların iki sayı girmelerini sağlayan bir sayfa oluşturursunuz, sonra bunları ekler ve sonucu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="0876c-184">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="0876c-185">Düzenleyicinizde yeni bir dosya oluşturun ve *AddNumbers. vbhtml*olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="0876c-185">In your editor, create a new file and name it *AddNumbers.vbhtml*.</span></span>
2. <span data-ttu-id="0876c-186">Sayfada bulunan herhangi bir şeyi değiştirerek aşağıdaki kodu ve işaretlemeyi sayfaya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="0876c-186">Copy the following code and markup into the page, replacing anything already in the page.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample10.vbhtml)]

    <span data-ttu-id="0876c-187">Dikkat etmeniz gereken bazı şeyler aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="0876c-187">Here are some things for you to note:</span></span>

    - <span data-ttu-id="0876c-188">`@` karakteri sayfadaki ilk kod bloğunu başlatır ve en alta eklenen `totalMessage` değişkeninden önce gelir.</span><span class="sxs-lookup"><span data-stu-id="0876c-188">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable embedded near the bottom.</span></span>
    - <span data-ttu-id="0876c-189">Sayfanın üst kısmındaki blok `Code...End Code`alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="0876c-189">The block at the top of the page is enclosed in `Code...End Code`.</span></span>
    - <span data-ttu-id="0876c-190">Değişkenler `total`, `num1`, `num2`ve `totalMessage` çeşitli sayıları ve bir dizeyi depolar.</span><span class="sxs-lookup"><span data-stu-id="0876c-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="0876c-191">`totalMessage` değişkenine atanan sabit dize değeri çift tırnak işaretleri içinde.</span><span class="sxs-lookup"><span data-stu-id="0876c-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="0876c-192">Visual Basic kod büyük/küçük harfe duyarlı olmadığından, sayfanın alt kısmında `totalMessage` değişkeni kullanıldığında, adının sayfanın en üstündeki değişken bildiriminin yazımla eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="0876c-192">Because Visual Basic code is not case sensitive, when the `totalMessage` variable is used near the bottom of the page, its name only needs to match the spelling of the variable declaration at the top of the page.</span></span> <span data-ttu-id="0876c-193">Büyük küçük harf büyük bir önemi yoktur.</span><span class="sxs-lookup"><span data-stu-id="0876c-193">The casing doesn't matter.</span></span>
    - <span data-ttu-id="0876c-194">`num1.AsInt()` + `num2.AsInt()` nesne ve yöntemlerle çalışmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="0876c-194">The expression `num1.AsInt()` + `num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="0876c-195">Her bir değişkendeki `AsInt` yöntemi, bir kullanıcı tarafından girilen dizeyi eklenebilen bir tam sayıya (tamsayı) dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="0876c-195">The `AsInt` method on each variable converts the string entered by a user to a whole number (an integer) that can be added.</span></span>
    - <span data-ttu-id="0876c-196">`<form>` etiketi bir `method="post"` özniteliği içerir.</span><span class="sxs-lookup"><span data-stu-id="0876c-196">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="0876c-197">Bu, Kullanıcı **Ekle**' ye tıkladığında, SAYFANıN http post yöntemi kullanılarak sunucuya gönderileceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="0876c-197">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="0876c-198">Sayfa gönderildiğinde, kod `If IsPost` doğru olarak değerlendirilir ve koşullu kod çalışır ve sayı ekleme sonucunu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="0876c-198">When the page is submitted, the code `If IsPost` evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="0876c-199">Sayfayı kaydedin ve bir tarayıcıda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0876c-199">Save the page and run it in a browser.</span></span> <span data-ttu-id="0876c-200">(Çalıştırmadan önce sayfanın **dosyalar** çalışma alanında seçili olduğundan emin olun.) İki tam sayı girin ve **Ekle** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0876c-200">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span>

    ![Razor-Img7](introducing-razor-syntax-vb/_static/image8.jpg)

## <a name="visual-basic-language-and-syntax"></a><span data-ttu-id="0876c-202">Visual Basic dil ve sözdizimi</span><span class="sxs-lookup"><span data-stu-id="0876c-202">Visual Basic Language and Syntax</span></span>

<span data-ttu-id="0876c-203">Daha önce, bir ASP.NET Web sayfası oluşturma ve HTML biçimlendirmesine sunucu kodu ekleme hakkında temel bir örnek gördünüz.</span><span class="sxs-lookup"><span data-stu-id="0876c-203">Earlier you saw a basic example of how to create an ASP.NET web page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="0876c-204">Burada, programlama dili kuralları Razor söz dizimi &#8212; kullanarak ASP.NET sunucu kodu yazmak için Visual Basic kullanmanın temellerini öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-204">Here you'll learn the basics of using Visual Basic to write ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="0876c-205">Programlamayla karşılaşırsanız (özellikle C, C++, C#, Visual Basic veya JavaScript kullandıysanız), burada okuduğunuzdan büyük bir şey tanıdık gelecektir.</span><span class="sxs-lookup"><span data-stu-id="0876c-205">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="0876c-206">Muhtemelen yalnızca WebMatrix kodunun *. vbhtml* dosyalarındaki biçimlendirmeye nasıl eklendiği hakkında bilgi almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0876c-206">You'll probably need to familiarize yourself only with how WebMatrix code is added to markup in *.vbhtml* files.</span></span>

### <a id="BM_CombiningTextMarkupAndCode"></a><span data-ttu-id="0876c-207">Kod bloklarında metin, biçimlendirme ve kod birleştirme</span><span class="sxs-lookup"><span data-stu-id="0876c-207">Combining text, markup, and code in code blocks</span></span>

<span data-ttu-id="0876c-208">Sunucu kod blokları ' nda, genellikle sayfada metin ve biçimlendirmeyi çıkarmak isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-208">In server code blocks, you'll often want to output text and markup to the page.</span></span> <span data-ttu-id="0876c-209">Bir sunucu kod bloğu kod olmayan ve bunun yerine olarak işlenmesi gereken metin içeriyorsa, ASP.NET bu metni koddan ayırabilmelidir.</span><span class="sxs-lookup"><span data-stu-id="0876c-209">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="0876c-210">Bunu yapmak için birkaç yol vardır.</span><span class="sxs-lookup"><span data-stu-id="0876c-210">There are several ways to do this.</span></span>

- <span data-ttu-id="0876c-211">Metni `<p></p>` veya `<em></em>`gibi bir HTML blok öğesine iliştirin:</span><span class="sxs-lookup"><span data-stu-id="0876c-211">Enclose the text in an HTML block element like `<p></p>` or `<em></em>`:</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample11.vbhtml)]

    <span data-ttu-id="0876c-212">HTML öğesi metin, ek HTML öğeleri ve sunucu kodu ifadelerini içerebilir.</span><span class="sxs-lookup"><span data-stu-id="0876c-212">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="0876c-213">ASP.NET, açılan HTML etiketini (örneğin, `<p>`) gördüğünde, öğe ve içeriğinin her şeyi tarayıcıya olduğu gibi işler (ve sunucu kodu ifadelerini çözümler).</span><span class="sxs-lookup"><span data-stu-id="0876c-213">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything the element and its content as is to the browser (and resolves the server-code expressions).</span></span>

- <span data-ttu-id="0876c-214">`@:` işlecini veya `<text>` öğesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0876c-214">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="0876c-215">`@:` düz metin veya eşleşmeyen HTML etiketleri içeren tek bir içerik satırı çıktısı verir; `<text>` öğesi çıktı için birden çok satır barındırır.</span><span class="sxs-lookup"><span data-stu-id="0876c-215">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="0876c-216">Bu seçenekler, çıktının bir parçası olarak bir HTML öğesi işlemek istemediğinizde yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="0876c-216">These options are useful when you don't want to render an HTML element as part of the output.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample12.vbhtml)]

    <span data-ttu-id="0876c-217">Aşağıdaki örnek, önceki örneği yineler, ancak işlemek için metni içine almak için tek bir `<text>` etiketi kullanır.</span><span class="sxs-lookup"><span data-stu-id="0876c-217">The following example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample13.vbhtml)]

    <span data-ttu-id="0876c-218">Aşağıdaki örnekte, `<text>` ve `</text>` etiketleri üç satırı kapsar; bunların hepsi, sunucu kodu ve eşleşen HTML etiketleriyle birlikte, bazı metin ve eşleşmeyen HTML etiketlerine (`<br />`) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0876c-218">In the following example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="0876c-219">Ayrıca, `@:` işleçle her bir satırdan de tek başına bir kez daha olabilirsiniz; Her iki yöntem de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="0876c-219">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample14.vbhtml)]

    > [!NOTE]
    > <span data-ttu-id="0876c-220">Bu bölümde &#8212; gösterildiği gibi metin yazdığınızda, bir HTML öğesi, `@:` işleci veya `<text>` öğesi &#8212; ASP.net, çıktıyı HTML olarak kodlamaz.</span><span class="sxs-lookup"><span data-stu-id="0876c-220">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="0876c-221">(Daha önce belirtildiği gibi, ASP.NET, bu bölümde belirtilen özel durumlar dışında, daha önce `@`sunucu kod ifadelerinin ve sunucu kodu bloklarının çıkışını kodladır.)</span><span class="sxs-lookup"><span data-stu-id="0876c-221">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="0876c-222">Boşlu</span><span class="sxs-lookup"><span data-stu-id="0876c-222">Whitespace</span></span>

<span data-ttu-id="0876c-223">Deyimdeki (ve dize sabit değerinin dışında) fazladan boşluklar, bu ifadeyi etkilemez:</span><span class="sxs-lookup"><span data-stu-id="0876c-223">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample15.vbhtml)]

### <a name="breaking-long-statements-into-multiple-lines"></a><span data-ttu-id="0876c-224">Uzun deyimleri birden çok satıra ayırma</span><span class="sxs-lookup"><span data-stu-id="0876c-224">Breaking long statements into multiple lines</span></span>

<span data-ttu-id="0876c-225">Her kod satırından sonra `_` alt çizgi karakterini (Visual Basic *devamlılık karakteri*olarak adlandırılır) kullanarak, uzun bir kod ifadesini birden çok satıra kesebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-225">You can break a long code statement into multiple lines by using the underscore character `_` (which in Visual Basic is called the *continuation character*) after each line of code.</span></span> <span data-ttu-id="0876c-226">Bir ifadeyi sonraki satıra bölmek için satırın sonunda bir boşluk ve sonra devamlılık karakteri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0876c-226">To break a statement onto the next line, at the end of the line add a space and then the continuation character.</span></span> <span data-ttu-id="0876c-227">Sonraki satırda ifadeye devam edin.</span><span class="sxs-lookup"><span data-stu-id="0876c-227">Continue the statement on the next line.</span></span> <span data-ttu-id="0876c-228">Daha okunaklı olması için deyimlerini gereken sayıda satıra kaydırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-228">You can wrap statements onto as many lines as you need to improve readability.</span></span> <span data-ttu-id="0876c-229">Aşağıdaki deyimler aynıdır:</span><span class="sxs-lookup"><span data-stu-id="0876c-229">The following statements are the same:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample16.vbhtml)]

<span data-ttu-id="0876c-230">Ancak, bir satırı dize sabit değerinin ortasında kaydıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="0876c-230">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="0876c-231">Aşağıdaki örnek çalışmıyor:</span><span class="sxs-lookup"><span data-stu-id="0876c-231">The following example doesn't work:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample17.vbhtml)]

<span data-ttu-id="0876c-232">Yukarıdaki kod gibi birden çok satıra kaydırılan uzun bir dizeyi birleştirmek için, bu makalede daha sonra göreceğiniz *birleştirme işlecini* (`&`) kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0876c-232">To combine a long string that wraps to multiple lines like the above code, you would need to use the *concatenation operator* (`&`), which you'll see later in this article.</span></span>

### <a name="code-comments"></a><span data-ttu-id="0876c-233">Kod açıklamaları</span><span class="sxs-lookup"><span data-stu-id="0876c-233">Code comments</span></span>

<span data-ttu-id="0876c-234">Açıklamalar sizin veya diğerleri için Not bırakmayı sağlar.</span><span class="sxs-lookup"><span data-stu-id="0876c-234">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="0876c-235">Razor söz dizimi yorumlara ön ek olarak `@*` ve `*@`ile biter.</span><span class="sxs-lookup"><span data-stu-id="0876c-235">Razor syntax comments are prefixed with `@*` and end with `*@`.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-vb/samples/sample18.cshtml)]

<span data-ttu-id="0876c-236">Kod blokları içinde Razor söz dizimi açıklamalarını kullanabilir veya her satıra ait tek tırnak (`'`) olan sıradan Visual Basic açıklama karakterini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-236">Within code blocks you can use the Razor syntax comments, or you can use ordinary Visual Basic comment character, which is a single quote (`'`) prefixed to each line.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample19.vbhtml)]

## <a name="variables"></a><span data-ttu-id="0876c-237">Değişkenler</span><span class="sxs-lookup"><span data-stu-id="0876c-237">Variables</span></span>

<span data-ttu-id="0876c-238">Değişken, verileri depolamak için kullandığınız adlandırılmış bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="0876c-238">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="0876c-239">Değişkenleri herhangi bir şekilde adlandırın, ancak ad alfabetik bir karakterle başlamalı ve boşluk ya da ayrılmış karakterler içeremez.</span><span class="sxs-lookup"><span data-stu-id="0876c-239">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span> <span data-ttu-id="0876c-240">Visual Basic ' de, daha önce gördüğünüz gibi, bir değişken adındaki harflerin büyük/küçük harf durumu büyük değildir.</span><span class="sxs-lookup"><span data-stu-id="0876c-240">In Visual Basic, as you saw earlier, the case of the letters in a variable name doesn't matter.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="0876c-241">Değişkenler ve veri türleri</span><span class="sxs-lookup"><span data-stu-id="0876c-241">Variables and data types</span></span>

<span data-ttu-id="0876c-242">Değişken, değişkende ne tür verilerin depolandığını gösteren belirli bir veri türüne sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="0876c-242">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="0876c-243">Dize değerlerini depolayan dize değişkenleriniz (&quot;Hello World&quot;), tam sayı değerlerini depolayan tamsayı değişkenleri (3 veya 79 gibi) ve tarih değerlerini çeşitli biçimlerde depolayan Tarih değişkenlerini (4/12/2012 veya Mart 2009 gibi) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-243">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="0876c-244">Ve kullanabileceğiniz pek çok farklı veri türü vardır.</span><span class="sxs-lookup"><span data-stu-id="0876c-244">And there are many other data types you can use.</span></span>

<span data-ttu-id="0876c-245">Ancak, bir değişken için bir tür belirtmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="0876c-245">However, you don't have to specify a type for a variable.</span></span> <span data-ttu-id="0876c-246">Çoğu durumda ASP.NET, değişken içindeki verilerin nasıl kullanıldığını temel alarak türü belirleyebilir.</span><span class="sxs-lookup"><span data-stu-id="0876c-246">In most cases ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="0876c-247">(Bazen bir tür belirtmeniz gerekir; bunun doğru olduğu örnekleri görürsünüz.)</span><span class="sxs-lookup"><span data-stu-id="0876c-247">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="0876c-248">Bir tür belirtmeden bir değişken bildirmek için `Dim` ve değişken adını (örneğin, `Dim myVar`) kullanın.</span><span class="sxs-lookup"><span data-stu-id="0876c-248">To declare a variable without specifying a type, use `Dim` plus the variable name (for instance, `Dim myVar`).</span></span> <span data-ttu-id="0876c-249">Bir türü olan bir değişken bildirmek için `Dim` ve değişken adını, ardından `As` ve ardından tür adını (örneğin, `Dim myVar As String`) kullanın.</span><span class="sxs-lookup"><span data-stu-id="0876c-249">To declare a variable with a type, use `Dim` plus the variable name, followed by `As` and then the type name (for instance, `Dim myVar As String`).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample20.vbhtml)]

<span data-ttu-id="0876c-250">Aşağıdaki örnek, bir Web sayfasındaki değişkenleri kullanan bazı satır içi ifadeleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="0876c-250">The following example shows some inline expressions that use the variables in a web page.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample21.vbhtml)]

<span data-ttu-id="0876c-251">Bir tarayıcıda gösterilecek Sonuç:</span><span class="sxs-lookup"><span data-stu-id="0876c-251">The result displayed in a browser:</span></span>

![Razor-Img9](introducing-razor-syntax-vb/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="0876c-253">Veri türlerini dönüştürme ve test etme</span><span class="sxs-lookup"><span data-stu-id="0876c-253">Converting and testing data types</span></span>

<span data-ttu-id="0876c-254">ASP.NET genellikle bir veri türünü otomatik olarak belirleyebilse de bazen olamaz.</span><span class="sxs-lookup"><span data-stu-id="0876c-254">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="0876c-255">Bu nedenle, açık bir dönüştürme gerçekleştirerek ASP.NET Out 'a yardımcı olmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="0876c-255">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="0876c-256">Türleri dönüştürmeniz gerekmese de, ne zaman çalıştığınız veri türlerini görmek için test etmeniz yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="0876c-256">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="0876c-257">En yaygın durum, bir dizeyi tamsayı veya tarih gibi başka bir türe dönüştürmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0876c-257">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="0876c-258">Aşağıdaki örnek, bir dizeyi bir sayıya dönüştürmeniz gereken tipik bir durumu gösterir.</span><span class="sxs-lookup"><span data-stu-id="0876c-258">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample22.vbhtml)]

<span data-ttu-id="0876c-259">Kural olarak, Kullanıcı girişi size dizeler olarak gelir.</span><span class="sxs-lookup"><span data-stu-id="0876c-259">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="0876c-260">Kullanıcıdan bir sayı girmesini isteyip istememiş olsanız bile, bir rakam girse bile, Kullanıcı girişi gönderildiğinde ve kodu kodda okuduğunuzda, veriler dize biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="0876c-260">Even if you've prompted the user to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="0876c-261">Bu nedenle, dizeyi bir sayıya dönüştürmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0876c-261">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="0876c-262">Örnekte, değerleri dönüşümlemeden aritmetik gerçekleştirmeye çalışırsanız, ASP.NET iki dize ekleyemediğinden aşağıdaki hata oluşur:</span><span class="sxs-lookup"><span data-stu-id="0876c-262">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

`Cannot implicitly convert type 'string' to 'int'.`

<span data-ttu-id="0876c-263">Değerleri tamsayılara dönüştürmek için `AsInt` yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="0876c-263">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="0876c-264">Dönüştürme başarılı olursa, sayıları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-264">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="0876c-265">Aşağıdaki tabloda, değişkenler için bazı ortak dönüştürme ve test yöntemleri listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="0876c-265">The following table lists some common conversion and test methods for variables.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="0876c-266"><strong>Yöntem</strong></span><span class="sxs-lookup"><span data-stu-id="0876c-266"><strong>Method</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="0876c-267"><strong>Açıklama</strong></span><span class="sxs-lookup"><span data-stu-id="0876c-267"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="0876c-268"><strong>Örnek</strong></span><span class="sxs-lookup"><span data-stu-id="0876c-268"><strong>Example</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="0876c-269">Tam sayıyı temsil eden bir dizeyi (&quot;593&quot;gibi) tamsayıya dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="0876c-269">Converts a string that represents a whole number (like &quot;593&quot;) to an integer.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample23.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="0876c-270">&quot;true&quot; veya &quot;false&quot; gibi bir dizeyi Boolean bir türe dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="0876c-270">Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample24.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="0876c-271">&quot;1,3&quot; veya &quot;&quot; 7,439 gibi ondalık değeri olan bir dizeyi kayan noktalı bir sayıya dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="0876c-271">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample25.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="0876c-272">&quot;1,3&quot; veya &quot;&quot; 7,439 gibi ondalık bir değere sahip bir dizeyi ondalık bir sayıya dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="0876c-272">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number.</span></span> <span data-ttu-id="0876c-273">(ASP.NET ' de, ondalık sayı bir kayan noktalı sayıdan daha belirgin olur.)</span><span class="sxs-lookup"><span data-stu-id="0876c-273">(In ASP.NET, a decimal number is more precise than a floating-point number.)</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample26.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="0876c-274">Bir tarih ve saat değerini temsil eden bir dizeyi ASP.NET `DateTime` türüne dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="0876c-274">Converts a string that represents a date and time value to the ASP.NET `DateTime` type.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample27.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="0876c-275">Diğer veri türlerini bir dizeye dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="0876c-275">Converts any other data type to a string.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a><span data-ttu-id="0876c-276">İşleçler</span><span class="sxs-lookup"><span data-stu-id="0876c-276">Operators</span></span>

<span data-ttu-id="0876c-277">İşleci, bir ifadede ne tür komutun gerçekleştirileceğini ASP.NET söyleyen bir anahtar sözcüktür veya karakterdir.</span><span class="sxs-lookup"><span data-stu-id="0876c-277">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="0876c-278">Visual Basic birçok işleci destekler, ancak ASP.NET Web sayfaları geliştirmeye başlamak için yalnızca birkaçını belirlemeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="0876c-278">Visual Basic supports many operators, but you only need to recognize a few to get started developing ASP.NET web pages.</span></span> <span data-ttu-id="0876c-279">Aşağıdaki tabloda en yaygın operatörler özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="0876c-279">The following table summarizes the most common operators.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="0876c-280"><strong>İşlecinde</strong></span><span class="sxs-lookup"><span data-stu-id="0876c-280"><strong>Operator</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="0876c-281"><strong>Açıklama</strong></span><span class="sxs-lookup"><span data-stu-id="0876c-281"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="0876c-282"><strong>Örnekler</strong></span><span class="sxs-lookup"><span data-stu-id="0876c-282"><strong>Examples</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+ - * /`
    :::column-end:::
    :::column:::
        <span data-ttu-id="0876c-283">Sayısal ifadelerde kullanılan matematik işleçleri.</span><span class="sxs-lookup"><span data-stu-id="0876c-283">Math operators used in numerical expressions.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample29.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
        <span data-ttu-id="0876c-284">Atama ve eşitlik.</span><span class="sxs-lookup"><span data-stu-id="0876c-284">Assignment and equality.</span></span> <span data-ttu-id="0876c-285">Bağlama bağlı olarak, bir deyimin sağ tarafındaki değeri, sol taraftaki nesneye atar ya da değerleri eşitlik için denetler.</span><span class="sxs-lookup"><span data-stu-id="0876c-285">Depending on context, either assigns the value on the right side of a statement to the object on the left side, or checks the values for equality.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample30.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `<>`
    :::column-end:::
    :::column:::
        <span data-ttu-id="0876c-286">Olmama.</span><span class="sxs-lookup"><span data-stu-id="0876c-286">Inequality.</span></span> <span data-ttu-id="0876c-287">Değerler eşit değilse `True` döndürür.</span><span class="sxs-lookup"><span data-stu-id="0876c-287">Returns `True` if the values are not equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample31.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
        <span data-ttu-id="0876c-288">Küçüktür, büyüktür, küçüktür veya eşittir, büyüktür veya eşittir.</span><span class="sxs-lookup"><span data-stu-id="0876c-288">Less than, greater than, less than or equal, and greater than or equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample32.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&`
    :::column-end:::
    :::column:::
        <span data-ttu-id="0876c-289">Dizeleri birleştirmek için kullanılan birleştirme.</span><span class="sxs-lookup"><span data-stu-id="0876c-289">Concatenation, which is used to join strings.</span></span>
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample33.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+= -=`
    :::column-end:::
    :::column:::
        <span data-ttu-id="0876c-290">Bir değişkenden 1 (sırasıyla) ekleyen ve çıkartacak artırma ve azaltma işleçleri.</span><span class="sxs-lookup"><span data-stu-id="0876c-290">The increment and decrement operators, which add and subtract 1 (respectively) from a variable.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample34.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
        <span data-ttu-id="0876c-291">Nokta.</span><span class="sxs-lookup"><span data-stu-id="0876c-291">Dot.</span></span> <span data-ttu-id="0876c-292">Nesneleri ve bunların özelliklerini ve yöntemlerini ayırt etmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0876c-292">Used to distinguish objects and their properties and methods.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample35.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="0876c-293">Ayraçlar.</span><span class="sxs-lookup"><span data-stu-id="0876c-293">Parentheses.</span></span> <span data-ttu-id="0876c-294">İfadeleri gruplandırmak, parametreleri yöntemlere geçirmek ve dizi ve koleksiyonların üyelerine erişmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0876c-294">Used to group expressions, to pass parameters to methods, and to access members of arrays and collections.</span></span>
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample36.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `Not`
    :::column-end:::
    :::column:::
        <span data-ttu-id="0876c-295">Başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="0876c-295">Not.</span></span> <span data-ttu-id="0876c-296">True değerini false değerine tersine çevirir ve tam tersi de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="0876c-296">Reverses a true value to false and vice versa.</span></span> <span data-ttu-id="0876c-297">Genellikle `False` test etmek için (`True`değil) kısayol yöntemi olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0876c-297">Typically used as a shorthand way to test for `False` (that is, for not `True`).</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample37.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AndAlso OrElse`
    :::column-end:::
    :::column:::
        <span data-ttu-id="0876c-298">Koşulları birbirine bağlamak için kullanılan mantıksal AND ve OR.</span><span class="sxs-lookup"><span data-stu-id="0876c-298">Logical AND and OR, which are used to link conditions together.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)]
    :::column-end:::
:::row-end:::

## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="0876c-299">Kodda dosya ve klasör yollarıyla çalışma</span><span class="sxs-lookup"><span data-stu-id="0876c-299">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="0876c-300">Genellikle kodunuzda dosya ve klasör yolları ile çalışırsınız.</span><span class="sxs-lookup"><span data-stu-id="0876c-300">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="0876c-301">Geliştirme bilgisayarınızda görünebilen bir Web sitesi için fiziksel klasör yapısına bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="0876c-301">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="0876c-302">URL 'Ler ve yollarla ilgili bazı temel ayrıntılar aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="0876c-302">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="0876c-303">URL, bir etki alanı adı (`http://www.example.com`) veya sunucu adı (`http://localhost`, `http://mycomputer`) ile başlar.</span><span class="sxs-lookup"><span data-stu-id="0876c-303">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="0876c-304">Bir URL, ana bilgisayardaki fiziksel bir yola karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="0876c-304">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="0876c-305">Örneğin, `http://myserver` sunucuda *C:\websites\mywebsite* klasörüne karşılık gelebilir.</span><span class="sxs-lookup"><span data-stu-id="0876c-305">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="0876c-306">Sanal yol, tüm yolu belirtmek zorunda kalmadan koddaki yolları temsil etmek için toplu bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="0876c-306">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="0876c-307">Bu, etki alanı veya sunucu adını izleyen bir URL 'nin bölümünü içerir.</span><span class="sxs-lookup"><span data-stu-id="0876c-307">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="0876c-308">Sanal yollar kullandığınızda, yolları güncelleştirmek zorunda kalmadan kodunuzu farklı bir etki alanına veya sunucuya taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-308">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="0876c-309">Farklılıkları anlamanıza yardımcı olacak bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="0876c-309">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="0876c-310">URL 'YI doldurun</span><span class="sxs-lookup"><span data-stu-id="0876c-310">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="0876c-311">Sunucu adı</span><span class="sxs-lookup"><span data-stu-id="0876c-311">Server name</span></span> | <span data-ttu-id="0876c-312">*mycompanyserver*</span><span class="sxs-lookup"><span data-stu-id="0876c-312">*mycompanyserver*</span></span> |
| <span data-ttu-id="0876c-313">Sanal yol</span><span class="sxs-lookup"><span data-stu-id="0876c-313">Virtual path</span></span> | <span data-ttu-id="0876c-314">*/humanresources/CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="0876c-314">*/humanresources/CompanyPolicy.htm*</span></span> |
| <span data-ttu-id="0876c-315">Fiziksel yol</span><span class="sxs-lookup"><span data-stu-id="0876c-315">Physical path</span></span> | <span data-ttu-id="0876c-316">*C:\websites\humanresources\companypolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="0876c-316">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span></span> |

<span data-ttu-id="0876c-317">Sanal kök, C: sürücünüzün kökünde olduğu gibi/olur.</span><span class="sxs-lookup"><span data-stu-id="0876c-317">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="0876c-318">(Sanal klasör yolları her zaman eğik çizgi kullanır.) Bir klasörün sanal yolunun fiziksel klasörle aynı ada sahip olması gerekmez; Bu bir diğer ad olabilir.</span><span class="sxs-lookup"><span data-stu-id="0876c-318">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="0876c-319">(Üretim sunucularında, sanal yol nadiren tam bir fiziksel yolla eşleşir.)</span><span class="sxs-lookup"><span data-stu-id="0876c-319">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="0876c-320">Kodda dosya ve klasörlerle çalışırken, çalıştığınız nesnelere bağlı olarak, bazen fiziksel yola ve bazen bir sanal yola başvurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0876c-320">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="0876c-321">ASP.NET, kodda dosya ve klasör yollarıyla çalışmak için size bu araçları sağlar: `Server.MapPath` yöntemi ve `~` işleci ve `Href` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="0876c-321">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="0876c-322">Sanal fiziksel yollara dönüştürme: Server. MapPath yöntemi</span><span class="sxs-lookup"><span data-stu-id="0876c-322">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="0876c-323">`Server.MapPath` yöntemi, bir sanal yolu ( */default.exe*gibi) mutlak bir fiziksel yola ( *C:\websites\mywebsitefolder\default.exe*gibi) dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="0876c-323">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="0876c-324">Bu yöntemi, tüm fiziksel yola ihtiyacınız olduğunda kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="0876c-324">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="0876c-325">Tipik bir örnek, Web sunucusunda bir metin dosyası veya resim dosyası okurken veya yazarken bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="0876c-325">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="0876c-326">Genellikle sitenizin bir barındırma sitesinin sunucusunda mutlak fiziksel yolunu bilemezsiniz; bu nedenle, bu yöntem, bildiğiniz yolu (sanal yol) sizin için sunucuda karşılık gelen yola dönüştürebilir.</span><span class="sxs-lookup"><span data-stu-id="0876c-326">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="0876c-327">Bir dosya veya klasörün sanal yolunu yöntemine geçirirsiniz ve fiziksel yolu döndürür:</span><span class="sxs-lookup"><span data-stu-id="0876c-327">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample39.vbhtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="0876c-328">Sanal köke başvuruluyor: ~ operator ve href yöntemi</span><span class="sxs-lookup"><span data-stu-id="0876c-328">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="0876c-329">Bir *. cshtml* veya *. vbhtml* dosyasında, `~` işlecini kullanarak sanal kök yoluna başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-329">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="0876c-330">Sayfaları bir sitede bir konuma taşıyabilmeniz ve içerdikleri bağlantıların diğer sayfalara bölünememesi nedeniyle bu çok yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="0876c-330">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="0876c-331">Web sitenizi farklı bir konuma taşımanız durumunda da yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="0876c-331">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="0876c-332">İşte bazı örnekler:</span><span class="sxs-lookup"><span data-stu-id="0876c-332">Here are some examples:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample40.vbhtml)]

<span data-ttu-id="0876c-333">Web sitesi `http://myserver/myapp`, sayfa çalışırken ASP.NET bu yolları nasıl değerlendilecektir:</span><span class="sxs-lookup"><span data-stu-id="0876c-333">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- <span data-ttu-id="0876c-334">`myImagesFolder`: `http://myserver/myapp/images`</span><span class="sxs-lookup"><span data-stu-id="0876c-334">`myImagesFolder`: `http://myserver/myapp/images`</span></span>
- <span data-ttu-id="0876c-335">`myStyleSheet`: `http://myserver/myapp/styles/Stylesheet.css`</span><span class="sxs-lookup"><span data-stu-id="0876c-335">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span></span>

<span data-ttu-id="0876c-336">(Bu yolları gerçekten değişkenin değerleri olarak görmezsiniz, ancak ASP.NET, bu gibi yollar gibi davranır.)</span><span class="sxs-lookup"><span data-stu-id="0876c-336">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="0876c-337">`~` işlecini hem sunucu kodunda (yukarıdaki gibi) hem de biçimlendirme ' de şu şekilde kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0876c-337">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample41.html)]

<span data-ttu-id="0876c-338">Biçimlendirme ' de, görüntü dosyaları, diğer Web sayfaları ve CSS dosyaları gibi kaynaklara yollar oluşturmak için `~` işlecini kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="0876c-338">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="0876c-339">Sayfa çalıştığında, ASP.NET sayfayı (hem kod hem de biçimlendirme) arar ve tüm `~` başvurularını uygun yola çözümler.</span><span class="sxs-lookup"><span data-stu-id="0876c-339">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="0876c-340">Koşullu mantık ve döngüler</span><span class="sxs-lookup"><span data-stu-id="0876c-340">Conditional Logic and Loops</span></span>

<span data-ttu-id="0876c-341">ASP.NET sunucu kodu, koşullara göre görevleri gerçekleştirmenize ve deyimleri belirli sayıda kez tekrardan yineleme yapan kodu, yani bir döngüsü çalıştıran kodu yazmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="0876c-341">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="0876c-342">Test koşulları</span><span class="sxs-lookup"><span data-stu-id="0876c-342">Testing conditions</span></span>

<span data-ttu-id="0876c-343">Basit bir koşulu test etmek için, belirttiğiniz bir teste göre `True` veya `False` döndüren `If...Then` ifadesini kullanın:</span><span class="sxs-lookup"><span data-stu-id="0876c-343">To test a simple condition you use the `If...Then` statement, which returns `True` or `False` based on a test you specify:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample42.vbhtml)]

<span data-ttu-id="0876c-344">`If` anahtar sözcüğü bir blok başlatır.</span><span class="sxs-lookup"><span data-stu-id="0876c-344">The `If` keyword starts a block.</span></span> <span data-ttu-id="0876c-345">Gerçek test (koşul) `If` anahtar sözcüğünü izler ve true veya false değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="0876c-345">The actual test (condition) follows the `If` keyword and returns true or false.</span></span> <span data-ttu-id="0876c-346">`If` deyimin bitişi `Then`.</span><span class="sxs-lookup"><span data-stu-id="0876c-346">The `If` statement ends with `Then`.</span></span> <span data-ttu-id="0876c-347">Test true ise çalıştırılacak deyimler `If` ve `End If`tarafından alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="0876c-347">The statements that will run if the test is true are enclosed by `If` and `End If`.</span></span> <span data-ttu-id="0876c-348">`If` deyimi, koşul yanlış ise çalıştırılacak deyimleri belirten bir `Else` bloğu içerebilir:</span><span class="sxs-lookup"><span data-stu-id="0876c-348">An `If` statement can include an `Else` block that specifies statements to run if the condition is false:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample43.vbhtml)]

<span data-ttu-id="0876c-349">`If` deyimi bir kod bloğu başlattığında, blokları dahil etmek için normal `Code...End Code` deyimlerini kullanmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="0876c-349">If an `If` statement starts a code block, you don't have to use the normal `Code...End Code` statements to include the blocks.</span></span> <span data-ttu-id="0876c-350">Yalnızca bloğa `@` ekleyebilirsiniz ve bu işlem çalışır.</span><span class="sxs-lookup"><span data-stu-id="0876c-350">You can just add `@` to the block, and it will work.</span></span> <span data-ttu-id="0876c-351">Bu yaklaşım, `For`, `For Each`, `Do While`, vb. dahil olmak üzere kod blokları tarafından izlenen `If` ve diğer Visual Basic programlama anahtar kelimeleriyle birlikte kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0876c-351">This approach works with `If` as well as other Visual Basic programming keywords that are followed by code blocks, including `For`, `For Each`, `Do While`, etc.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample44.vbhtml)]

<span data-ttu-id="0876c-352">Bir veya daha çok `ElseIf` bloğu kullanarak birden çok koşul ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0876c-352">You can add multiple conditions using one or more `ElseIf` blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample45.vbhtml)]

<span data-ttu-id="0876c-353">Bu örnekte, `If` bloğundaki ilk koşul doğru değilse, `ElseIf` koşulu denetlenir.</span><span class="sxs-lookup"><span data-stu-id="0876c-353">In this example, if the first condition in the `If` block is not true, the `ElseIf` condition is checked.</span></span> <span data-ttu-id="0876c-354">Bu koşul karşılanıyorsa, `ElseIf` bloğundaki deyimler yürütülür.</span><span class="sxs-lookup"><span data-stu-id="0876c-354">If that condition is met, the statements in the `ElseIf` block are executed.</span></span> <span data-ttu-id="0876c-355">Koşulların hiçbiri karşılanmazsa, `Else` bloğundaki deyimler yürütülür.</span><span class="sxs-lookup"><span data-stu-id="0876c-355">If none of the conditions are met, the statements in the `Else` block are executed.</span></span> <span data-ttu-id="0876c-356">Herhangi bir sayıda `ElseIf` blok ekleyebilir ve sonra &quot;her şeyi&quot; koşulu olarak bir `Else` bloğuyla kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-356">You can add any number of `ElseIf` blocks, and then close with an `Else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="0876c-357">Çok sayıda koşulu test etmek için `Select Case` bloğunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="0876c-357">To test a large number of conditions, use a `Select Case` block:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample46.vbhtml)]

<span data-ttu-id="0876c-358">Sınanacak değer parantez içinde (örnekte, haftanın günü değişkeni).</span><span class="sxs-lookup"><span data-stu-id="0876c-358">The value to test is in parentheses (in the example, the weekday variable).</span></span> <span data-ttu-id="0876c-359">Her bir test, bir değeri listeleyen `Case` bir ifade kullanır.</span><span class="sxs-lookup"><span data-stu-id="0876c-359">Each individual test uses a `Case` statement that lists a value.</span></span> <span data-ttu-id="0876c-360">Bir `Case` deyimin değeri test değeriyle eşleşiyorsa, bu `Case` bloğundaki kod yürütülür.</span><span class="sxs-lookup"><span data-stu-id="0876c-360">If the value of a `Case` statement matches the test value, the code in that `Case` block is executed.</span></span>

<span data-ttu-id="0876c-361">Bir tarayıcıda görünen son iki koşullu blok sonucu:</span><span class="sxs-lookup"><span data-stu-id="0876c-361">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor-Img10](introducing-razor-syntax-vb/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="0876c-363">Döngü kodu</span><span class="sxs-lookup"><span data-stu-id="0876c-363">Looping code</span></span>

<span data-ttu-id="0876c-364">Genellikle aynı deyimleri tekrar tekrar çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0876c-364">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="0876c-365">Bu, döngüye göre yapılır.</span><span class="sxs-lookup"><span data-stu-id="0876c-365">You do this by looping.</span></span> <span data-ttu-id="0876c-366">Örneğin, çoğu kez bir veri koleksiyonundaki her öğe için aynı deyimleri çalıştırırsınız.</span><span class="sxs-lookup"><span data-stu-id="0876c-366">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="0876c-367">Kaç kez döngüye almak istediğinizi biliyorsanız `For` döngüsünü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-367">If you know exactly how many times you want to loop, you can use a `For` loop.</span></span> <span data-ttu-id="0876c-368">Bu tür bir döngü, özellikle daha fazla sayım veya sayım için yararlıdır:</span><span class="sxs-lookup"><span data-stu-id="0876c-368">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample47.vbhtml)]

<span data-ttu-id="0876c-369">Döngü, `For` anahtar sözcüğüyle başlar ve bunu üç öğe izler:</span><span class="sxs-lookup"><span data-stu-id="0876c-369">The loop begins with the `For` keyword, followed by three elements:</span></span>

- <span data-ttu-id="0876c-370">`For` deyimden hemen sonra, bir sayaç değişkeni bildirir (`Dim`kullanmanız gerekmez) ve sonra aralığı `i = 10 to 20`gibi belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0876c-370">Immediately after the `For` statement, you declare a counter variable (you don't have to use `Dim`) and then indicate the range, as in `i = 10 to 20`.</span></span> <span data-ttu-id="0876c-371">Bu, `i` değişkeninin 10 ' da sayımının başlayacağı ve 20 ' ye (dahil) ulaşıncaya kadar devam edecek.</span><span class="sxs-lookup"><span data-stu-id="0876c-371">This means the variable `i` will start counting at 10 and continue until it reaches 20 (inclusive).</span></span>
- <span data-ttu-id="0876c-372">`For` ve `Next` deyimleri arasında bloğunun içeridir.</span><span class="sxs-lookup"><span data-stu-id="0876c-372">Between the `For` and `Next` statements is the content of the block.</span></span> <span data-ttu-id="0876c-373">Bu, her döngüyle yürütülen bir veya daha fazla kod deyimi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="0876c-373">This can contain one or more code statements that execute with each loop.</span></span>
- <span data-ttu-id="0876c-374">`Next i` deyimin döngüsü sona erer.</span><span class="sxs-lookup"><span data-stu-id="0876c-374">The `Next i` statement ends the loop.</span></span> <span data-ttu-id="0876c-375">Sayacı artırır ve döngünün bir sonraki yinelemesini başlatır.</span><span class="sxs-lookup"><span data-stu-id="0876c-375">It increments the counter and starts the next iteration of the loop.</span></span>

<span data-ttu-id="0876c-376">`For` ve `Next` çizgileri arasındaki kod satırı, döngünün her yinelemesi için çalışan kodu içerir.</span><span class="sxs-lookup"><span data-stu-id="0876c-376">The line of code between the `For` and `Next` lines contains the code that runs for each iteration of the loop.</span></span> <span data-ttu-id="0876c-377">Biçimlendirme, her seferinde yeni bir paragraf (`<p>` öğesi) oluşturur ve t değerini (sayaç) görüntüleyerek çıkışa bir satır ekler.</span><span class="sxs-lookup"><span data-stu-id="0876c-377">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of i (the counter).</span></span> <span data-ttu-id="0876c-378">Bu sayfayı çalıştırdığınızda örnek, her satırda öğe numarasını gösteren metinle birlikte çıktıyı görüntüleyen 11 satır oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0876c-378">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor-Img11](introducing-razor-syntax-vb/_static/image11.jpg)

<span data-ttu-id="0876c-380">Bir koleksiyon veya dizi ile çalışıyorsanız, genellikle bir `For Each` döngüsü kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="0876c-380">If you're working with a collection or array, you often use a `For Each` loop.</span></span> <span data-ttu-id="0876c-381">Bir koleksiyon benzer nesneler grubudur ve `For Each` döngüsü koleksiyondaki her öğe üzerinde bir görevi gerçekleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="0876c-381">A collection is a group of similar objects, and the `For Each` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="0876c-382">Bu tür bir döngü koleksiyonlar için uygundur, çünkü `For` döngüsünün aksine sayacı artırmanız veya bir sınır ayarlamanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="0876c-382">This type of loop is convenient for collections, because unlike a `For` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="0876c-383">Bunun yerine, `For Each` döngü kodu yalnızca, tamamlanana kadar koleksiyon üzerinden ilerler.</span><span class="sxs-lookup"><span data-stu-id="0876c-383">Instead, the `For Each` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="0876c-384">Bu örnek, `Request.ServerVariables` koleksiyonundaki öğeleri döndürür (Web sunucunuz hakkında bilgi içerir).</span><span class="sxs-lookup"><span data-stu-id="0876c-384">This example returns the items in the `Request.ServerVariables` collection (which contains information about your web server).</span></span> <span data-ttu-id="0876c-385">HTML madde işaretli listesinde yeni bir `<li>` öğesi oluşturarak her öğenin adını göstermek için `For Each` döngüsünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="0876c-385">It uses a `For Each` loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample48.vbhtml)]

<span data-ttu-id="0876c-386">`For Each` anahtar kelimesinin ardından, koleksiyondaki tek bir öğeyi temsil eden bir değişken gelir (örneğin, `myItem`), ardından `In` anahtar sözcüğü ve sonra, içinde döngü uygulamak istediğiniz koleksiyon.</span><span class="sxs-lookup"><span data-stu-id="0876c-386">The `For Each` keyword is followed by a variable that represents a single item in the collection (in the example, `myItem`), followed by the `In` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="0876c-387">`For Each` döngüsünün gövdesinde, daha önce bildirdiğiniz değişkeni kullanarak geçerli öğeye erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-387">In the body of the `For Each` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor-Img12](introducing-razor-syntax-vb/_static/image12.jpg)

<span data-ttu-id="0876c-389">Daha genel amaçlı bir döngü oluşturmak için `Do While` ifadesini kullanın:</span><span class="sxs-lookup"><span data-stu-id="0876c-389">To create a more general-purpose loop, use the `Do While` statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample49.vbhtml)]

<span data-ttu-id="0876c-390">Bu döngü, `Do While` anahtar sözcüğüyle başlar ve sonra bir koşul gelir ve ardından yineleme, yinelenir.</span><span class="sxs-lookup"><span data-stu-id="0876c-390">This loop begins with the `Do While` keyword, followed by a condition, followed by the block to repeat.</span></span> <span data-ttu-id="0876c-391">Döngüler genellikle sayma için kullanılan bir değişken veya nesneden artış (ekleme) veya azaltma (çıkarma).</span><span class="sxs-lookup"><span data-stu-id="0876c-391">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="0876c-392">Örnekte `+=` işleci, döngü her çalıştığında bir değişkenin değerine 1 ekler.</span><span class="sxs-lookup"><span data-stu-id="0876c-392">In the example, the `+=` operator adds 1 to the value of a variable each time the loop runs.</span></span> <span data-ttu-id="0876c-393">(Bir döngüdeki bir değişkeni azaltmak için, azaltma işlecini `-=`kullanırsınız.)</span><span class="sxs-lookup"><span data-stu-id="0876c-393">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`.)</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="0876c-394">Nesneler ve koleksiyonlar</span><span class="sxs-lookup"><span data-stu-id="0876c-394">Objects and Collections</span></span>

<span data-ttu-id="0876c-395">Bir ASP.NET Web sitesindeki neredeyse her şey, Web sayfasının kendisi de dahil olmak üzere bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="0876c-395">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="0876c-396">Bu bölümde, kodunuzda sıkça çalışacağımız bazı önemli nesneler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0876c-396">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="0876c-397">Sayfa nesneleri</span><span class="sxs-lookup"><span data-stu-id="0876c-397">Page objects</span></span>

<span data-ttu-id="0876c-398">ASP.NET ' deki en temel nesne, sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="0876c-398">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="0876c-399">Sayfa nesnesinin özelliklerine, uygun herhangi bir nesne olmadan doğrudan erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-399">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="0876c-400">Aşağıdaki kod, sayfanın `Request` nesnesini kullanarak sayfanın dosya yolunu alır:</span><span class="sxs-lookup"><span data-stu-id="0876c-400">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample50.vbhtml)]

<span data-ttu-id="0876c-401">`Page` nesnenin özelliklerini kullanarak çok fazla bilgi alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0876c-401">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- <span data-ttu-id="0876c-402">`Request`.</span><span class="sxs-lookup"><span data-stu-id="0876c-402">`Request`.</span></span> <span data-ttu-id="0876c-403">Zaten gördüğünüze göre, bu, istek ne tür bir tarayıcı, sayfanın URL 'SI, Kullanıcı kimliği vb. gibi geçerli istek hakkındaki bilgilerin bir koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="0876c-403">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- <span data-ttu-id="0876c-404">`Response`.</span><span class="sxs-lookup"><span data-stu-id="0876c-404">`Response`.</span></span> <span data-ttu-id="0876c-405">Bu, sunucu kodunun çalışmayı tamamladığında tarayıcıya gönderilecek yanıt (sayfa) hakkındaki bilgilerin bir koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="0876c-405">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="0876c-406">Örneğin, yanıta bilgi yazmak için bu özelliği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-406">For example, you can use this property to write information into the response.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample51.vbhtml)]

### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="0876c-407">Koleksiyon nesneleri (diziler ve sözlükler)</span><span class="sxs-lookup"><span data-stu-id="0876c-407">Collection objects (arrays and dictionaries)</span></span>

<span data-ttu-id="0876c-408">Bir koleksiyon, bir veritabanından `Customer` nesneleri koleksiyonu gibi aynı türde bir nesne grubudur.</span><span class="sxs-lookup"><span data-stu-id="0876c-408">A collection is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="0876c-409">ASP.NET, `Request.Files` koleksiyonu gibi birçok yerleşik koleksiyon içerir.</span><span class="sxs-lookup"><span data-stu-id="0876c-409">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="0876c-410">Genellikle koleksiyonlardaki verilerle çalışırsınız.</span><span class="sxs-lookup"><span data-stu-id="0876c-410">You'll often work with data in collections.</span></span> <span data-ttu-id="0876c-411">İki ortak koleksiyon türü *dizi* ve *sözlüktür*.</span><span class="sxs-lookup"><span data-stu-id="0876c-411">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="0876c-412">Bir dizi benzer öğeler koleksiyonunu depolamak istediğinizde ancak her bir öğeyi tutacak ayrı bir değişken oluşturmak istemediğinizde yararlıdır:</span><span class="sxs-lookup"><span data-stu-id="0876c-412">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample52.vbhtml)]

<span data-ttu-id="0876c-413">Diziler ile, `String`, `Integer`veya `DateTime`gibi belirli bir veri türünü bildirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-413">With arrays, you declare a specific data type, such as `String`, `Integer`, or `DateTime`.</span></span> <span data-ttu-id="0876c-414">Değişkenin bir dizi içerebileceğini belirtmek için, bildirimdeki değişken adına parantez eklersiniz (örneğin, `Dim myVar() As String`).</span><span class="sxs-lookup"><span data-stu-id="0876c-414">To indicate that the variable can contain an array, you add parentheses to the variable name in the declaration (such as `Dim myVar() As String`).</span></span> <span data-ttu-id="0876c-415">Bir dizideki öğelere konumlarını (Dizin) veya `For Each` ifadesini kullanarak erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-415">You can access items in an array using their position (index) or by using the `For Each` statement.</span></span> <span data-ttu-id="0876c-416">Dizi dizinleri sıfır tabanlıdır &#8212; , ilk öğe 0 ' dır, ikinci öğe ise 1 konumunda ve bu şekilde devam eder.</span><span class="sxs-lookup"><span data-stu-id="0876c-416">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample53.vbhtml)]

<span data-ttu-id="0876c-417">Bir dizideki öğelerin sayısını `Length` özelliğini alarak belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-417">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="0876c-418">Dizideki belirli bir öğenin konumunu almak için (yani, diziyi aramak için) `Array.IndexOf` yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0876c-418">To get the position of a specific item in the array (that is, to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="0876c-419">Ayrıca, bir dizinin içeriğini ters çevirme (`Array.Reverse` yöntemi) veya içeriği sıralama (`Array.Sort` yöntemi) gibi işlemleri de yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-419">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="0876c-420">Bir tarayıcıda görünen dize dizisi kodunun çıkışı:</span><span class="sxs-lookup"><span data-stu-id="0876c-420">The output of the string array code displayed in a browser:</span></span>

![Razor-Img13](introducing-razor-syntax-vb/_static/image13.jpg)

<span data-ttu-id="0876c-422">Sözlük, anahtar/değer çiftleri koleksiyonudur ve buna karşılık gelen değeri ayarlamak ya da almak için anahtarı (veya adı) sağlarsınız:</span><span class="sxs-lookup"><span data-stu-id="0876c-422">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample54.vbhtml)]

<span data-ttu-id="0876c-423">Sözlük oluşturmak için `New` anahtar sözcüğünü kullanarak yeni bir `Dictionary` nesnesi oluşturduğunuz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="0876c-423">To create a dictionary, you use the `New` keyword to indicate that you're creating a new `Dictionary` object.</span></span> <span data-ttu-id="0876c-424">`Dim` anahtar sözcüğünü kullanarak bir değişkene bir sözlük atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-424">You can assign a dictionary to a variable using the `Dim` keyword.</span></span> <span data-ttu-id="0876c-425">Parantez (`( )`) kullanarak Sözlükteki öğelerin veri türlerini gösterebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-425">You indicate the data types of the items in the dictionary using parentheses ( `( )` ).</span></span> <span data-ttu-id="0876c-426">Bildirimin sonunda, bu gerçekte yeni bir sözlük oluşturan bir yöntem olduğundan, başka bir parantez çifti eklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-426">At the end of the declaration, you must add another pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="0876c-427">Sözlüğe öğe eklemek için, sözlük değişkeninin (Bu durumda`myScores`) `Add` yöntemini çağırabilir ve sonra bir anahtar ve bir değer belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-427">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="0876c-428">Alternatif olarak, aşağıdaki örnekte olduğu gibi anahtarı göstermek ve basit bir atama yapmak için parantezleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0876c-428">Alternatively, you can use parentheses to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample55.vbhtml)]

<span data-ttu-id="0876c-429">Sözlükten bir değer almak için anahtarı parantez içinde belirtirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0876c-429">To get a value from the dictionary, you specify the key in parentheses:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample56.vbhtml)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="0876c-430">Yöntemler parametrelerle çağırma</span><span class="sxs-lookup"><span data-stu-id="0876c-430">Calling Methods with Parameters</span></span>

<span data-ttu-id="0876c-431">Bu makalede daha önce gördüğünüz gibi, ile programlayabilmeniz gereken nesneler yöntemlerine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0876c-431">As you saw earlier in this article, the objects that you program with have methods.</span></span> <span data-ttu-id="0876c-432">Örneğin, bir `Database` nesnesi bir `Database.Connect` yöntemine sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="0876c-432">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="0876c-433">Birçok yöntemde de bir veya daha fazla parametre vardır.</span><span class="sxs-lookup"><span data-stu-id="0876c-433">Many methods also have one or more parameters.</span></span> <span data-ttu-id="0876c-434">*Parametresi* , bir yöntemine geçirdiğiniz bir değerdir ve bu yöntem, görevini tamamlamaya yönelik yöntemi etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="0876c-434">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="0876c-435">Örneğin, üç parametre alan `Request.MapPath` yöntemi için bir bildirime bakın:</span><span class="sxs-lookup"><span data-stu-id="0876c-435">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-vb[Main](introducing-razor-syntax-vb/samples/sample57.vb)]

<span data-ttu-id="0876c-436">Bu yöntem, belirtilen sanal yola karşılık gelen sunucudaki fiziksel yolu döndürür.</span><span class="sxs-lookup"><span data-stu-id="0876c-436">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="0876c-437">Yöntemi için üç parametre `virtualPath`, `baseVirtualDir`ve `allowCrossAppMapping`.</span><span class="sxs-lookup"><span data-stu-id="0876c-437">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="0876c-438">(Bildiriminde, parametrelerin kabul edeceği verilerin veri türleriyle listelendiğine dikkat edin.) Bu yöntemi çağırdığınızda, üç parametrenin de değerlerini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0876c-438">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="0876c-439">Razor söz dizimi Visual Basic kullanırken, parametreleri bir yönteme geçirmek için iki seçeneğiniz vardır: *Konumsal parametreler* veya *adlandırılmış parametreler*.</span><span class="sxs-lookup"><span data-stu-id="0876c-439">When you're using Visual Basic with the Razor syntax, you have two options for passing parameters to a method: *positional parameters* or *named parameters*.</span></span> <span data-ttu-id="0876c-440">Konumsal parametreleri kullanarak bir yöntemi çağırmak için, parametreleri yöntem bildiriminde belirtilen katı bir sıraya geçirin.</span><span class="sxs-lookup"><span data-stu-id="0876c-440">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="0876c-441">(Bu sırayı genellikle yöntemi için belgeleri okuyarak bilirsiniz.) Sırayı izlemeniz gerekir ve gerekirse parametrelerden &#8212; hiçbirini atlayamazsınız, bir değeri olmayan Konumsal parametre için boş bir dize (`""`) veya null geçirin.</span><span class="sxs-lookup"><span data-stu-id="0876c-441">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or null for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="0876c-442">Aşağıdaki örnek, Web sitenizde *betikler* adında bir klasörünüz olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="0876c-442">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="0876c-443">Kod `Request.MapPath` yöntemini çağırır ve üç parametrenin değerlerini doğru sırada geçirir.</span><span class="sxs-lookup"><span data-stu-id="0876c-443">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="0876c-444">Ardından, sonuçta elde edilen eşleştirilmiş yolu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="0876c-444">It then displays the resulting mapped path.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample58.vbhtml)]

<span data-ttu-id="0876c-445">Bir yöntem için çok sayıda parametre olduğunda, adlandırılmış parametreleri kullanarak kodunuzu temizleyicinizi ve daha okunaklı tutabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-445">When there are many parameters for a method, you can keep your code cleaner and more readable by using named parameters.</span></span> <span data-ttu-id="0876c-446">Adlandırılmış parametreleri kullanarak bir yöntemi çağırmak için, parametre adını ve ardından `:=` belirtip değeri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="0876c-446">To call a method using named parameters, specify the parameter name followed by `:=` and then provide the value.</span></span> <span data-ttu-id="0876c-447">Adlandırılmış parametrelerin avantajı, bunları istediğiniz sırada ekleyebilmeniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-447">An advantage of named parameters is that you can add them in any order you want.</span></span> <span data-ttu-id="0876c-448">(Bir dezavantajı yöntem çağrısının sıkışık olmaması.)</span><span class="sxs-lookup"><span data-stu-id="0876c-448">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="0876c-449">Aşağıdaki örnek, yukarıdaki gibi aynı yöntemi çağırır, ancak değerleri sağlamak için adlandırılmış parametreleri kullanır:</span><span class="sxs-lookup"><span data-stu-id="0876c-449">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample59.vbhtml)]

<span data-ttu-id="0876c-450">Görebileceğiniz gibi, parametreler farklı bir sırayla geçirilir.</span><span class="sxs-lookup"><span data-stu-id="0876c-450">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="0876c-451">Ancak, önceki örneği çalıştırırsanız ve bu örnekte, aynı değer döndürülür.</span><span class="sxs-lookup"><span data-stu-id="0876c-451">However, if you run the previous example and this example, they'll return the same value.</span></span>

## <a name="handling-errors"></a><span data-ttu-id="0876c-452">Hataları İşleme</span><span class="sxs-lookup"><span data-stu-id="0876c-452">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="0876c-453">Try-catch deyimleri</span><span class="sxs-lookup"><span data-stu-id="0876c-453">Try-Catch statements</span></span>

<span data-ttu-id="0876c-454">Kodunuzda, denetiminizin dışındaki nedenlerle başarısız olabilecek deyimler vardır.</span><span class="sxs-lookup"><span data-stu-id="0876c-454">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="0876c-455">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="0876c-455">For example:</span></span>

- <span data-ttu-id="0876c-456">Kodunuz bir dosyayı açmaya, oluşturmaya, okumaya veya yazmaya çalışırsa, tüm hata sıralamaları meydana gelebilir.</span><span class="sxs-lookup"><span data-stu-id="0876c-456">If your code tries to open, create, read, or write a file, all sorts of errors might occur.</span></span> <span data-ttu-id="0876c-457">İstediğiniz dosya mevcut olmayabilir, kilitli olabilir, kod izinlere sahip olmayabilir ve bu şekilde devam eder.</span><span class="sxs-lookup"><span data-stu-id="0876c-457">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="0876c-458">Benzer şekilde, kodunuz bir veritabanındaki kayıtları güncelleştirmeye çalışırsa, izin sorunları olabilir, veritabanı bağlantısı bırakılmış olabilir, kaydedilecek veriler geçersiz olabilir ve bu şekilde devam eder.</span><span class="sxs-lookup"><span data-stu-id="0876c-458">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="0876c-459">Programlama koşullarında, bu durumlara *özel durumlar*denir.</span><span class="sxs-lookup"><span data-stu-id="0876c-459">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="0876c-460">Kodunuz bir özel durumla karşılaşırsa, en iyi ve rahatsız edici kullanıcılara bir hata mesajı üretir (atar).</span><span class="sxs-lookup"><span data-stu-id="0876c-460">If your code encounters an exception, it generates (throws) an error message that is, at best, annoying to users.</span></span>

![Razor-Img14](introducing-razor-syntax-vb/_static/image14.jpg)

<span data-ttu-id="0876c-462">Kodunuzun özel durumlarla karşılaşmasına ve bu türden hata iletilerinden kaçınmak için `Try/Catch` deyimlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-462">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `Try/Catch` statements.</span></span> <span data-ttu-id="0876c-463">`Try` bildiriminde, kontrol ettiğiniz kodu çalıştırırsınız.</span><span class="sxs-lookup"><span data-stu-id="0876c-463">In the `Try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="0876c-464">Bir veya daha fazla `Catch` deyiminde, oluşmuş olabilecek belirli hatalara (özel durum türleri) bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-464">In one or more `Catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="0876c-465">Benimsemeyi bekleme olduğunuz hatalara bakmak için gereken sayıda `Catch` deyimi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0876c-465">You can include as many `Catch` statements as you need to look for errors that you're anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="0876c-466">`Try/Catch` deyimlerde `Response.Redirect` yöntemini kullanmaktan kaçınmanızı öneririz, çünkü sayfanızda bir özel duruma neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="0876c-466">We recommend that you avoid using the `Response.Redirect` method in `Try/Catch` statements, because it can cause an exception in your page.</span></span>

<span data-ttu-id="0876c-467">Aşağıdaki örnek, ilk istekte bir metin dosyası oluşturan ve sonra kullanıcının dosyayı açmasına olanak tanıyan bir düğme görüntüleyen bir sayfa gösterir.</span><span class="sxs-lookup"><span data-stu-id="0876c-467">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="0876c-468">Örnek, bir özel duruma neden olacak şekilde hatalı bir dosya adı kullanır.</span><span class="sxs-lookup"><span data-stu-id="0876c-468">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="0876c-469">Kod, olası iki özel durum için `Catch` deyimlerini içerir: dosya adı bozuksa oluşan `FileNotFoundException`ve ASP.NET bile klasörü bulamazsa oluşan `DirectoryNotFoundException`.</span><span class="sxs-lookup"><span data-stu-id="0876c-469">The code includes `Catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="0876c-470">(Her şey düzgün şekilde çalıştığında nasıl çalıştığını görmek için örnekteki bir deyimin açıklamasını değiştirebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="0876c-470">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="0876c-471">Kodunuz özel durumu işlemediyse, önceki ekran görüntüsündeki gibi bir hata sayfası görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="0876c-471">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="0876c-472">Ancak, `Try/Catch` bölümü kullanıcının bu hata türlerini görmesini önlemeye yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="0876c-472">However, the `Try/Catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample60.vbhtml)]

## <a name="additional-resources"></a><span data-ttu-id="0876c-473">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="0876c-473">Additional Resources</span></span>

### <a name="reference-documentation"></a><span data-ttu-id="0876c-474">Başvuru Belgeleri</span><span class="sxs-lookup"><span data-stu-id="0876c-474">Reference Documentation</span></span>

- [<span data-ttu-id="0876c-475">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="0876c-475">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)
- [<span data-ttu-id="0876c-476">Visual Basic dili</span><span class="sxs-lookup"><span data-stu-id="0876c-476">Visual Basic Language</span></span>](https://msdn.microsoft.com/library/2x7h1hfk.aspx)
