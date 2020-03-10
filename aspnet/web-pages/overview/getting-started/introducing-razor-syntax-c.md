---
uid: web-pages/overview/getting-started/introducing-razor-syntax-c
title: Razor söz dizimini kullanarak ASP.NET Web programlamaya giriş (C#) | Microsoft Docs
author: Rick-Anderson
description: Bu bölümde, Razor söz dizimi kullanarak ASP.NET Web sayfaları ile programlamaya genel bakış sunulmaktadır. ASP.NET, Microsoft 'un dinamik Web PA 'yi çalıştırmaya yönelik teknolojisidir...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: aa67d304-583b-4bf8-a231-195656cfb587
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-c
msc.type: authoredcontent
ms.openlocfilehash: c2f420bb7c2f7d2e31654c20fb9ec7497a30a9f7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641577"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-c"></a><span data-ttu-id="d0141-104">Razor söz dizimini kullanarak ASP.NET Web programlamaya giriş (C#)</span><span class="sxs-lookup"><span data-stu-id="d0141-104">Introduction to ASP.NET Web Programming Using the Razor Syntax (C#)</span></span>

<span data-ttu-id="d0141-105">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="d0141-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="d0141-106">Bu makalede, Razor söz dizimi kullanarak ASP.NET Web sayfaları ile programlamaya genel bakış sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d0141-106">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax.</span></span> <span data-ttu-id="d0141-107">ASP.NET, Microsoft 'un web sunucularında dinamik Web sayfaları çalıştırmaya yönelik teknolojisidir.</span><span class="sxs-lookup"><span data-stu-id="d0141-107">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span> <span data-ttu-id="d0141-108">Bu makaleler, C# programlama dilini kullanmaya odaklanır.</span><span class="sxs-lookup"><span data-stu-id="d0141-108">This articles focuses on using the C# programming language.</span></span>
> 
> <span data-ttu-id="d0141-109">Şunları **öğreneceksiniz**:</span><span class="sxs-lookup"><span data-stu-id="d0141-109">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="d0141-110">Razor söz dizimi kullanarak programlama ASP.NET Web sayfaları ile çalışmaya başlama için en iyi 8 programlama ipuçları.</span><span class="sxs-lookup"><span data-stu-id="d0141-110">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="d0141-111">İhtiyaç duyacağınız temel programlama kavramları.</span><span class="sxs-lookup"><span data-stu-id="d0141-111">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="d0141-112">ASP.NET sunucu kodu ve Razor söz dizimi hepsi ile ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="d0141-112">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="d0141-113">Yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="d0141-113">Software versions</span></span>
> 
> 
> - <span data-ttu-id="d0141-114">ASP.NET Web sayfaları (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="d0141-114">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="d0141-115">Bu öğretici, ASP.NET Web Pages 2 ile de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d0141-115">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="the-top-8-programming-tips"></a><span data-ttu-id="d0141-116">Ilk 8 programlama Ipuçları</span><span class="sxs-lookup"><span data-stu-id="d0141-116">The Top 8 Programming Tips</span></span>

<span data-ttu-id="d0141-117">Bu bölümde, Razor söz dizimi kullanarak ASP.NET sunucu kodu yazmaya başladığınızda kesinlikle bilmeniz gereken birkaç ipucu listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="d0141-117">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="d0141-118">Razor söz dizimi, C# programlama dilini temel alır ve en sık kullanılan ASP.NET Web sayfaları olan dildir.</span><span class="sxs-lookup"><span data-stu-id="d0141-118">The Razor syntax is based on the C# programming language, and that's the language that's used most often with ASP.NET Web Pages.</span></span> <span data-ttu-id="d0141-119">Ancak Razor söz dizimi Ayrıca, Visual Basic dilini ve gördüğünüz her şeyi de Visual Basic de yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-119">However, the Razor syntax also supports the Visual Basic language, and everything you see you can also do in Visual Basic.</span></span> <span data-ttu-id="d0141-120">Ayrıntılar için bkz. ek [Visual Basic dili ve sözdizimi](https://go.microsoft.com/fwlink/?LinkId=202908).</span><span class="sxs-lookup"><span data-stu-id="d0141-120">For details, see the appendix [Visual Basic Language and Syntax](https://go.microsoft.com/fwlink/?LinkId=202908).</span></span>

<span data-ttu-id="d0141-121">Makalede daha sonra bu programlama tekniklerinin birçoğu hakkında daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-121">You can find more details about most of these programming techniques later in the article.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="d0141-122">1. @ karakterini kullanarak bir sayfaya kod eklersiniz</span><span class="sxs-lookup"><span data-stu-id="d0141-122">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="d0141-123">`@` karakteri satır içi ifadeler, tek deyim blokları ve çok deyimli bloklar başlatır:</span><span class="sxs-lookup"><span data-stu-id="d0141-123">The `@` character starts inline expressions, single statement blocks, and multi-statement blocks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample1.html)]

<span data-ttu-id="d0141-124">Bu deyimler, sayfa bir tarayıcıda çalıştırıldığında şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="d0141-124">This is what these statements look like when the page runs in a browser:</span></span>

![Razor-Img1](introducing-razor-syntax-c/_static/image1.jpg)

> [!TIP] 
> 
> <span data-ttu-id="d0141-126">**HTML kodlaması**</span><span class="sxs-lookup"><span data-stu-id="d0141-126">**HTML Encoding**</span></span>
> 
> <span data-ttu-id="d0141-127">Önceki örneklerde olduğu gibi, `@` karakterini kullanarak bir sayfada içerik görüntülediğinizde, ASP.NET HTML-, çıktıyı kodluyor.</span><span class="sxs-lookup"><span data-stu-id="d0141-127">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="d0141-128">Bu, ayrılmış HTML karakterlerinin (`<` ve `>` ve `&`), karakterlerin HTML etiketleri veya varlıklar olarak yorumlanıp bir Web sayfasında karakter olarak görüntülenmesini sağlayan kodlarla değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="d0141-128">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="d0141-129">HTML kodlaması olmadan, sunucu kodunuzun çıktısı doğru görüntülenmeyebilir ve güvenlik risklerine karşı bir sayfa sunabilir.</span><span class="sxs-lookup"><span data-stu-id="d0141-129">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="d0141-130">Amacınız etiketleri biçimlendirme olarak işleyen (örneğin, bir paragraf için `<p></p>` ya da metin vurgulamak için `<em></em>`) HTML işaretlemesinin çıktısını alıyorsa, bu makalenin ilerleyen kısımlarında yer alan [kod bloklarında metin, biçimlendirme ve kod birleştirme](#BM_CombiningTextMarkupAndCode) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="d0141-130">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="d0141-131">[Formlarla çalışırken](https://go.microsoft.com/fwlink/?LinkId=202892)HTML kodlaması hakkında daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-131">You can read more about HTML encoding in [Working with Forms](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>

### <a name="2-you-enclose-code-blocks-in-braces"></a><span data-ttu-id="d0141-132">2. kod bloklarını küme ayraçları içine almalısınız</span><span class="sxs-lookup"><span data-stu-id="d0141-132">2. You enclose code blocks in braces</span></span>

<span data-ttu-id="d0141-133">*Kod bloğu* bir veya daha fazla kod deyimi içerir ve küme ayraçları içine alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="d0141-133">A *code block* includes one or more code statements and is enclosed in braces.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample2.html)]

<span data-ttu-id="d0141-134">Bir tarayıcıda gösterilecek Sonuç:</span><span class="sxs-lookup"><span data-stu-id="d0141-134">The result displayed in a browser:</span></span>

![Razor-Img2](introducing-razor-syntax-c/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-semicolon"></a><span data-ttu-id="d0141-136">3. bir blok içinde her bir kod ifadesini noktalı virgülle sonlandırın</span><span class="sxs-lookup"><span data-stu-id="d0141-136">3. Inside a block, you end each code statement with a semicolon</span></span>

<span data-ttu-id="d0141-137">Bir kod bloğu içinde, tüm kod deyimlerinin noktalı virgülle bitmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0141-137">Inside a code block, each complete code statement must end with a semicolon.</span></span> <span data-ttu-id="d0141-138">Satır içi ifadeler noktalı virgül ile bitmiyor.</span><span class="sxs-lookup"><span data-stu-id="d0141-138">Inline expressions don't end with a semicolon.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample3.html)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="d0141-139">4. değerleri depolamak için değişkenleri kullanırsınız</span><span class="sxs-lookup"><span data-stu-id="d0141-139">4. You use variables to store values</span></span>

<span data-ttu-id="d0141-140">Değerleri dizeler, sayılar ve tarihler gibi bir *değişkende*saklayabilirsiniz. `var` anahtar sözcüğünü kullanarak yeni bir değişken oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="d0141-140">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `var` keyword.</span></span> <span data-ttu-id="d0141-141">`@`kullanarak doğrudan bir sayfada değişken değerleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-141">You can insert variable values directly in a page using `@`.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample4.html)]

<span data-ttu-id="d0141-142">Bir tarayıcıda gösterilecek Sonuç:</span><span class="sxs-lookup"><span data-stu-id="d0141-142">The result displayed in a browser:</span></span>

![Razor-IMG3](introducing-razor-syntax-c/_static/image3.jpg)

<a id="ID_StringLiterals"></a>
### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="d0141-144">5. sabit dize değerlerini çift tırnak işaretleri içine alın</span><span class="sxs-lookup"><span data-stu-id="d0141-144">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="d0141-145">*Dize* , metin olarak kabul edilen bir karakter dizisidir.</span><span class="sxs-lookup"><span data-stu-id="d0141-145">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="d0141-146">Bir dize belirtmek için, bunu çift tırnak işareti içine alın:</span><span class="sxs-lookup"><span data-stu-id="d0141-146">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample5.cshtml)]

<span data-ttu-id="d0141-147">Göstermek istediğiniz dize bir ters eğik çizgi karakteri (`\`) veya çift tırnak işareti (`"`) içeriyorsa, `@` işleci önekli bir tam *dize sabit değeri* kullanın.</span><span class="sxs-lookup"><span data-stu-id="d0141-147">If the string that you want to display contains a backslash character ( `\` ) or double quotation marks ( `"` ), use a *verbatim string literal* that's prefixed with the `@` operator.</span></span> <span data-ttu-id="d0141-148">(İçinde C#, tam bir dize sabit değeri kullanmadığınız müddetçe, \ karakterinin özel anlamı vardır.)</span><span class="sxs-lookup"><span data-stu-id="d0141-148">(In C#, the \ character has special meaning unless you use a verbatim string literal.)</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample6.html)]

<span data-ttu-id="d0141-149">Çift tırnak işaretleri eklemek için, tam bir dize değişmez değeri kullanın ve tırnak işaretlerini tekrarlayın:</span><span class="sxs-lookup"><span data-stu-id="d0141-149">To embed double quotation marks, use a verbatim string literal and repeat the quotation marks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample7.html)]

<span data-ttu-id="d0141-150">Bu örneklerin her ikisini de bir sayfada kullanmanın sonucu aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d0141-150">Here's the result of using both of these examples in a page:</span></span>

![Razor-Img4](introducing-razor-syntax-c/_static/image4.jpg)

> [!NOTE]
> <span data-ttu-id="d0141-152">`@` karakterinin her ikisi de ' de C# tam dize sabit değerlerini işaretlemek için ve ASP.net sayfalarındaki kodu işaretlemek için kullanıldığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d0141-152">Notice that the `@` character is used both to mark verbatim string literals in C# and to mark code in ASP.NET pages.</span></span>

### <a name="6-code-is-case-sensitive"></a><span data-ttu-id="d0141-153">6. kod büyük/küçük harfe duyarlıdır</span><span class="sxs-lookup"><span data-stu-id="d0141-153">6. Code is case sensitive</span></span>

<span data-ttu-id="d0141-154">' C#De, anahtar sözcükler (`var`, `true`ve `if`gibi) ve değişken adları büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="d0141-154">In C#, keywords (like `var`, `true`, and `if`) and variable names are case sensitive.</span></span> <span data-ttu-id="d0141-155">Aşağıdaki kod satırları `lastName` ve `LastName.` iki farklı değişken oluşturur</span><span class="sxs-lookup"><span data-stu-id="d0141-155">The following lines of code create two different variables, `lastName` and `LastName.`</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample8.cshtml)]

<span data-ttu-id="d0141-156">Bir değişkeni `var lastName = "Smith";` olarak bildirir ve sayfanızdaki bu değişkene `@LastName`olarak başvuru yapmayı denerseniz, `"Smith"`yerine `"Jones"` değeri alırsınız.</span><span class="sxs-lookup"><span data-stu-id="d0141-156">If you declare a variable as `var lastName = "Smith";` and try to reference that variable in your page as `@LastName`, you would get the value `"Jones"` instead of `"Smith"`.</span></span>

> [!NOTE]
> <span data-ttu-id="d0141-157">Visual Basic, anahtar sözcükler ve değişkenler büyük/küçük harfe duyarlı *değildir* .</span><span class="sxs-lookup"><span data-stu-id="d0141-157">In Visual Basic, keywords and variables are *not* case sensitive.</span></span>

### <a name="7-much-of-your-coding-involves-objects"></a><span data-ttu-id="d0141-158">7. kodlarınızın çoğu nesneleri içerir</span><span class="sxs-lookup"><span data-stu-id="d0141-158">7. Much of your coding involves objects</span></span>

<span data-ttu-id="d0141-159">Bir *nesne* , bir sayfa, metin kutusu, dosya &#8212; , görüntü, Web isteği, e-posta iletisi, müşteri kaydı (veritabanı satırı) vb. ile programlama yapamayacağınız şeyi temsil eder. Nesneler, özelliklerini betimleyen ve metin kutusu `Text` nesnesini okuyabilmeniz veya değiştirebilmeniz &#8212; için özelliklere sahiptir. bir istek nesnesi bir `Url` özelliğine sahiptir, bir e-posta iletisi bir `From` özelliğine sahiptir ve bir müşteri nesnesi bir `FirstName` özelliğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d0141-159">An *object* represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics and that you can read or change &#8212; a text box object has a `Text` property (among others), a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="d0141-160">Nesneler, gerçekleştirebilecekleri&quot; &quot;fiiller olan yöntemlere de sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d0141-160">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="d0141-161">Bir dosya nesnesinin `Save` yöntemi, bir görüntü nesnesinin `Rotate` yöntemi ve bir e-posta nesnesinin `Send` yöntemi sayılabilir.</span><span class="sxs-lookup"><span data-stu-id="d0141-161">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="d0141-162">Genellikle sayfada metin kutularının (form alanları) değerleri, istek ne tür bir tarayıcı, isteğin URL 'SI, Kullanıcı kimliği vb. gibi bilgiler sunan `Request` nesnesiyle çalışırsınız. Aşağıdaki örnek, `Request` nesnesinin özelliklerine nasıl erişileceğinin yanı sıra sunucudaki sayfanın mutlak yolunu sağlayan `Request` nesnesinin `MapPath` yönteminin nasıl çağrılacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="d0141-162">You'll often work with the `Request` object, which gives you information like the values of text boxes (form fields) on the page, what type of browser made the request, the URL of the page, the user identity, etc. The following example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample9.html)]

<span data-ttu-id="d0141-163">Bir tarayıcıda gösterilecek Sonuç:</span><span class="sxs-lookup"><span data-stu-id="d0141-163">The result displayed in a browser:</span></span>

![Razor-Img5](introducing-razor-syntax-c/_static/image5.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="d0141-165">8. kararları veren kodu yazabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d0141-165">8. You can write code that makes decisions</span></span>

<span data-ttu-id="d0141-166">Dinamik Web sayfalarının temel bir özelliği, koşullara göre ne yapılacağını belirleyebileceğinize bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="d0141-166">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="d0141-167">Bunu yapmanın en yaygın yolu `if` deyimidir (ve isteğe bağlı `else` deyimidir).</span><span class="sxs-lookup"><span data-stu-id="d0141-167">The most common way to do this is with the `if` statement (and optional `else` statement).</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample10.cshtml)]

<span data-ttu-id="d0141-168">`if(IsPost)` ifade, `if(IsPost == true)`yazmanın bir Özet yoludur.</span><span class="sxs-lookup"><span data-stu-id="d0141-168">The statement `if(IsPost)` is a shorthand way of writing `if(IsPost == true)`.</span></span> <span data-ttu-id="d0141-169">`if` deyimleriyle birlikte, bu makalenin ilerleyen kısımlarında açıklanan koşulları test etme, kod blokları yineleme ve benzeri birçok yol vardır.</span><span class="sxs-lookup"><span data-stu-id="d0141-169">Along with `if` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="d0141-170">Sonuç tarayıcıda ( **Gönder**'e tıklandıktan sonra) gösterilir:</span><span class="sxs-lookup"><span data-stu-id="d0141-170">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor-Img6](introducing-razor-syntax-c/_static/image6.jpg)

> [!TIP] 
> 
> <a id="SB_HttpGetPost"></a>
> ### <a name="http-get-and-post-methods-and-the-ispost-property"></a><span data-ttu-id="d0141-172">HTTP GET ve POST yöntemleri ve ıspost özelliği</span><span class="sxs-lookup"><span data-stu-id="d0141-172">HTTP GET and POST Methods and the IsPost Property</span></span>
> 
> <span data-ttu-id="d0141-173">Web sayfaları (HTTP) için kullanılan protokol, sunucuya istek yapmak için kullanılan çok sayıda yöntemi (fiil) destekler.</span><span class="sxs-lookup"><span data-stu-id="d0141-173">The protocol used for web pages (HTTP) supports a very limited number of methods (verbs) that are used to make requests to the server.</span></span> <span data-ttu-id="d0141-174">En yaygın iki tane, bir sayfayı okumak için kullanılan ve bir sayfayı göndermek için kullanılan POST ' dır.</span><span class="sxs-lookup"><span data-stu-id="d0141-174">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="d0141-175">Genellikle, Kullanıcı ilk kez bir sayfa istediğinde, sayfa GET kullanılarak istenir.</span><span class="sxs-lookup"><span data-stu-id="d0141-175">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="d0141-176">Kullanıcı bir formu doldurduğunda ve sonra bir Gönder düğmesine tıkladığında, tarayıcı sunucuya bir POST isteği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d0141-176">If the user fills in a form and then clicks a submit button, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="d0141-177">Web programlamada, sayfayı nasıl işleyeceğini bilmeniz için bir sayfanın GET veya POST olarak istenmekte olduğunu bilmeniz genellikle yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="d0141-177">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="d0141-178">ASP.NET Web sayfalarında, bir isteğin bir GET veya POST olup olmadığını görmek için `IsPost` özelliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-178">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="d0141-179">İstek bir GÖNDERIME ise, `IsPost` özelliği true döndürür ve bir formdaki metin kutularının değerlerini okumak gibi şeyler yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-179">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="d0141-180">Birçok örnek, `IsPost`değerine bağlı olarak sayfayı farklı şekilde nasıl işleyeceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="d0141-180">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>

## <a name="a-simple-code-example"></a><span data-ttu-id="d0141-181">Basit bir kod örneği</span><span class="sxs-lookup"><span data-stu-id="d0141-181">A Simple Code Example</span></span>

<span data-ttu-id="d0141-182">Bu yordamda, temel programlama tekniklerini gösteren bir sayfanın nasıl oluşturulacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d0141-182">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="d0141-183">Örnekte, kullanıcıların iki sayı girmelerini sağlayan bir sayfa oluşturursunuz, sonra bunları ekler ve sonucu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d0141-183">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="d0141-184">Düzenleyicinizde yeni bir dosya oluşturun ve *AddNumbers. cshtml*olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="d0141-184">In your editor, create a new file and name it *AddNumbers.cshtml*.</span></span>
2. <span data-ttu-id="d0141-185">Sayfada bulunan herhangi bir şeyi değiştirerek aşağıdaki kodu ve işaretlemeyi sayfaya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d0141-185">Copy the following code and markup into the page, replacing anything already in the page.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample11.cshtml)]

    <span data-ttu-id="d0141-186">Dikkat etmeniz gereken bazı şeyler aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d0141-186">Here are some things for you to note:</span></span>

    - <span data-ttu-id="d0141-187">`@` karakteri sayfadaki ilk kod bloğunu başlatır ve sayfanın alt kısmına yakın olan `totalMessage` değişkeninden önce gelir.</span><span class="sxs-lookup"><span data-stu-id="d0141-187">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable that's embedded near the bottom of the page.</span></span>
    - <span data-ttu-id="d0141-188">Sayfanın üst kısmındaki blok küme ayraçları içine alınır.</span><span class="sxs-lookup"><span data-stu-id="d0141-188">The block at the top of the page is enclosed in braces.</span></span>
    - <span data-ttu-id="d0141-189">Üstteki blokta, tüm satırlar noktalı virgül ile biter.</span><span class="sxs-lookup"><span data-stu-id="d0141-189">In the block at the top, all lines end with a semicolon.</span></span>
    - <span data-ttu-id="d0141-190">Değişkenler `total`, `num1`, `num2`ve `totalMessage` çeşitli sayıları ve bir dizeyi depolar.</span><span class="sxs-lookup"><span data-stu-id="d0141-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="d0141-191">`totalMessage` değişkenine atanan sabit dize değeri çift tırnak işaretleri içinde.</span><span class="sxs-lookup"><span data-stu-id="d0141-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="d0141-192">Kod büyük/küçük harfe duyarlı olduğundan, `totalMessage` değişkeni sayfanın alt kısmında kullanıldığında, adının en üstteki değişkenle eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0141-192">Because the code is case-sensitive, when the `totalMessage` variable is used near the bottom of the page, its name must match the variable at the top exactly.</span></span>
    - <span data-ttu-id="d0141-193">İfade `num1.AsInt() + num2.AsInt()`, nesneler ve yöntemlerle çalışmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="d0141-193">The expression `num1.AsInt() + num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="d0141-194">Her bir değişkendeki `AsInt` yöntemi, bir kullanıcı tarafından girilen dizeyi bir sayıya (bir tamsayı) dönüştürür, böylece bunun üzerinde aritmetik yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-194">The `AsInt` method on each variable converts the string entered by a user to a number (an integer) so that you can perform arithmetic on it.</span></span>
    - <span data-ttu-id="d0141-195">`<form>` etiketi bir `method="post"` özniteliği içerir.</span><span class="sxs-lookup"><span data-stu-id="d0141-195">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="d0141-196">Bu, Kullanıcı **Ekle**' ye tıkladığında, SAYFANıN http post yöntemi kullanılarak sunucuya gönderileceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="d0141-196">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="d0141-197">Sayfa gönderildiğinde, `if(IsPost)` test doğru olarak değerlendirilir ve koşullu kod çalışır ve sayı ekleme sonucunu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d0141-197">When the page is submitted, the `if(IsPost)` test evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="d0141-198">Sayfayı kaydedin ve bir tarayıcıda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d0141-198">Save the page and run it in a browser.</span></span> <span data-ttu-id="d0141-199">(Çalıştırmadan önce sayfanın **dosyalar** çalışma alanında seçili olduğundan emin olun.) İki tam sayı girin ve **Ekle** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d0141-199">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span> 

    ![Razor-Img7](introducing-razor-syntax-c/_static/image7.jpg)

## <a name="basic-programming-concepts"></a><span data-ttu-id="d0141-201">Temel programlama kavramları</span><span class="sxs-lookup"><span data-stu-id="d0141-201">Basic Programming Concepts</span></span>

<span data-ttu-id="d0141-202">Bu makalede, ASP.NET Web programlamaya genel bakış sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d0141-202">This article provides you with an overview of ASP.NET web programming.</span></span> <span data-ttu-id="d0141-203">Geniş bir inceleme değildir, yalnızca en sık kullanacağınız programlama kavramlarıyla hızlı bir tura katılın.</span><span class="sxs-lookup"><span data-stu-id="d0141-203">It isn't an exhaustive examination, just a quick tour through the programming concepts you'll use most often.</span></span> <span data-ttu-id="d0141-204">Bu nedenle, ASP.NET Web sayfaları ile çalışmaya başlamak için ihtiyacınız olan neredeyse her şeyi de ele alır.</span><span class="sxs-lookup"><span data-stu-id="d0141-204">Even so, it covers almost everything you'll need to get started with ASP.NET Web Pages.</span></span>

<span data-ttu-id="d0141-205">Ancak ilk olarak biraz teknik bir arka plan.</span><span class="sxs-lookup"><span data-stu-id="d0141-205">But first, a little technical background.</span></span>

### <a name="the-razor-syntax-server-code-and-aspnet"></a><span data-ttu-id="d0141-206">Razor sözdizimi, sunucu kodu ve ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d0141-206">The Razor Syntax, Server Code, and ASP.NET</span></span>

<span data-ttu-id="d0141-207">Razor söz dizimi, bir Web sayfasına sunucu tabanlı kod eklemeye yönelik basit bir programlama sözdizimidir.</span><span class="sxs-lookup"><span data-stu-id="d0141-207">Razor syntax is a simple programming syntax for embedding server-based code in a web page.</span></span> <span data-ttu-id="d0141-208">Razor söz dizimi kullanan bir Web sayfasında, iki tür içerik vardır: istemci içeriği ve sunucu kodu.</span><span class="sxs-lookup"><span data-stu-id="d0141-208">In a web page that uses the Razor syntax, there are two kinds of content: client content and server code.</span></span> <span data-ttu-id="d0141-209">İstemci içeriği Web sayfalarında kullandığınız malzemedir: HTML biçimlendirme (öğeler), CSS gibi stil bilgileri, JavaScript gibi bazı istemci betikleri, belki de düz metin.</span><span class="sxs-lookup"><span data-stu-id="d0141-209">Client content is the stuff you're used to in web pages: HTML markup (elements), style information such as CSS, maybe some client script such as JavaScript, and plain text.</span></span>

<span data-ttu-id="d0141-210">Razor söz dizimi, bu istemci içeriğine sunucu kodu eklemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="d0141-210">Razor syntax lets you add server code to this client content.</span></span> <span data-ttu-id="d0141-211">Sayfada sunucu kodu varsa, sunucu tarayıcıya göndermeden önce bu kodu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="d0141-211">If there's server code in the page, the server runs that code first, before it sends the page to the browser.</span></span> <span data-ttu-id="d0141-212">Sunucu üzerinde çalışan kod, sunucu tabanlı veritabanlarına erişim gibi tek başına istemci içeriğini kullanarak çok daha karmaşık olabilecek görevler gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="d0141-212">By running on the server, the code can perform tasks that can be a lot more complex to do using client content alone, like accessing server-based databases.</span></span> <span data-ttu-id="d0141-213">En önemlisi, sunucu kodu istemci içeriğini &#8212; dinamik olarak oluşturabilir ve bu Işlem anında HTML biçimlendirme veya diğer içerik oluşturabilir ve ardından sayfanın içerebileceği herhangi BIR statik HTML ile birlikte tarayıcıya gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="d0141-213">Most importantly, server code can dynamically create client content &#8212; it can generate HTML markup or other content on the fly and then send it to the browser along with any static HTML that the page might contain.</span></span> <span data-ttu-id="d0141-214">Tarayıcınızın perspektifinden, sunucu kodunuz tarafından oluşturulan istemci içerikleri diğer istemci içeriğinden farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="d0141-214">From the browser's perspective, client content that's generated by your server code is no different than any other client content.</span></span> <span data-ttu-id="d0141-215">Zaten gördüğünüz gibi, gereken sunucu kodu oldukça basittir.</span><span class="sxs-lookup"><span data-stu-id="d0141-215">As you've already seen, the server code that's required is quite simple.</span></span>

<span data-ttu-id="d0141-216">Razor söz dizimi içeren ASP.NET Web sayfalarının özel bir dosya uzantısı ( *. cshtml* veya *. vbhtml*) vardır.</span><span class="sxs-lookup"><span data-stu-id="d0141-216">ASP.NET web pages that include the Razor syntax have a special file extension (*.cshtml* or *.vbhtml*).</span></span> <span data-ttu-id="d0141-217">Sunucu bu uzantıları tanır, Razor söz dizimi ile işaretlenen kodu çalıştırır ve sonra sayfayı tarayıcıya gönderir.</span><span class="sxs-lookup"><span data-stu-id="d0141-217">The server recognizes these extensions, runs the code that's marked with Razor syntax, and then sends the page to the browser.</span></span>

### <a name="where-does-aspnet-fit-in"></a><span data-ttu-id="d0141-218">ASP.NET nereye sığacak?</span><span class="sxs-lookup"><span data-stu-id="d0141-218">Where does ASP.NET fit in?</span></span>

<span data-ttu-id="d0141-219">Razor söz dizimi, Microsoft 'un Microsoft .NET Framework 'ü temel alan ASP.NET adlı bir teknolojiyi temel alır.</span><span class="sxs-lookup"><span data-stu-id="d0141-219">Razor syntax is based on a technology from Microsoft called ASP.NET, which in turn is based on the Microsoft .NET Framework.</span></span> <span data-ttu-id="d0141-220">The.NET Framework, Microsoft 'un neredeyse her türlü bilgisayar uygulamasının geliştirilmesi için büyük ve kapsamlı bir programlama çerçevesidir.</span><span class="sxs-lookup"><span data-stu-id="d0141-220">The.NET Framework is a big, comprehensive programming framework from Microsoft for developing virtually any type of computer application.</span></span> <span data-ttu-id="d0141-221">ASP.NET, Web uygulamaları oluşturmak için özel olarak tasarlanan .NET Framework bölümüdür.</span><span class="sxs-lookup"><span data-stu-id="d0141-221">ASP.NET is the part of the .NET Framework that's specifically designed for creating web applications.</span></span> <span data-ttu-id="d0141-222">Geliştiriciler dünyadaki en büyük ve en yüksek trafikli web sitelerinin çoğunu oluşturmak için ASP.NET kullandık.</span><span class="sxs-lookup"><span data-stu-id="d0141-222">Developers have used ASP.NET to create many of the largest and highest-traffic websites in the world.</span></span> <span data-ttu-id="d0141-223">(Dosya adı uzantısı *. aspx* ' i BIR sitedeki URL 'nin bir parçası olarak gördüğünüz zaman, sitenin ASP.NET kullanılarak yazıldığını bilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="d0141-223">(Any time you see the file-name extension *.aspx* as part of the URL in a site, you'll know that the site was written using ASP.NET.)</span></span>

<span data-ttu-id="d0141-224">Razor söz dizimi, size ASP.NET 'un tüm gücünü sunar, ancak acemi bir uzman olduğunu öğrenmenizi ve uzman olduğunuzda daha üretken olmanızı sağlayan basitleştirilmiş bir sözdizimi kullanmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d0141-224">The Razor syntax gives you all the power of ASP.NET, but using a simplified syntax that's easier to learn if you're a beginner and that makes you more productive if you're an expert.</span></span> <span data-ttu-id="d0141-225">Bu söz dizimi kullanımı basit olsa da, ASP.NET .NET Framework ile aile ilişkisi, Web siteleriniz daha karmaşık hale geldiği için, daha geniş çerçevelerin gücünden yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-225">Even though this syntax is simple to use, its family relationship to ASP.NET and the .NET Framework means that as your websites become more sophisticated, you have the power of the larger frameworks available to you.</span></span>

![Razor-Img8](introducing-razor-syntax-c/_static/image8.jpg)

> [!TIP] 
> 
> <span data-ttu-id="d0141-227">**Sınıflar ve örnekler**</span><span class="sxs-lookup"><span data-stu-id="d0141-227">**Classes and Instances**</span></span>
> 
> <span data-ttu-id="d0141-228">ASP.NET sunucu kodu, sınıflarının fikir fikrini üzerine inşa edilen nesneleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="d0141-228">ASP.NET server code uses objects, which are in turn built on the idea of classes.</span></span> <span data-ttu-id="d0141-229">Sınıfı, bir nesnenin tanımı veya şablonudur.</span><span class="sxs-lookup"><span data-stu-id="d0141-229">The class is the definition or template for an object.</span></span> <span data-ttu-id="d0141-230">Örneğin, bir uygulama herhangi bir müşteri nesnesinin ihtiyacı olan özellikleri ve yöntemleri tanımlayan bir `Customer` sınıfı içerebilir.</span><span class="sxs-lookup"><span data-stu-id="d0141-230">For example, an application might contain a `Customer` class that defines the properties and methods that any customer object needs.</span></span>
> 
> <span data-ttu-id="d0141-231">Uygulamanın gerçek müşteri bilgileriyle çalışması gerektiğinde, bir müşteri nesnesi (veya *örnekleyen*) örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d0141-231">When the application needs to work with actual customer information, it creates an instance of (or *instantiates*) a customer object.</span></span> <span data-ttu-id="d0141-232">Bireysel her müşteri, `Customer` sınıfının ayrı bir örneğidir.</span><span class="sxs-lookup"><span data-stu-id="d0141-232">Each individual customer is a separate instance of the `Customer` class.</span></span> <span data-ttu-id="d0141-233">Her örnek aynı özellikleri ve yöntemleri destekler, ancak her bir müşteri nesnesi benzersiz olduğundan her örnek için özellik değerleri genellikle farklıdır.</span><span class="sxs-lookup"><span data-stu-id="d0141-233">Every instance supports the same properties and methods, but the property values for each instance are typically different, because each customer object is unique.</span></span> <span data-ttu-id="d0141-234">Bir müşteri nesnesinde, `LastName` özelliği "Smith" olabilir; başka bir müşteri nesnesinde, `LastName` özelliği "Jones" olabilir.</span><span class="sxs-lookup"><span data-stu-id="d0141-234">In one customer object, the `LastName` property might be "Smith"; in another customer object, the `LastName` property might be "Jones."</span></span>
> 
> <span data-ttu-id="d0141-235">Benzer şekilde, sitenizdeki her bir Web sayfası, `Page` sınıfının bir örneği olan `Page` nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="d0141-235">Similarly, any individual web page in your site is a `Page` object that's an instance of the `Page` class.</span></span> <span data-ttu-id="d0141-236">Sayfadaki bir düğme, `Button` sınıfının bir örneği olan `Button` nesnesidir ve bu şekilde devam eder.</span><span class="sxs-lookup"><span data-stu-id="d0141-236">A button on the page is a `Button` object that is an instance of the `Button` class, and so on.</span></span> <span data-ttu-id="d0141-237">Her örnek kendi özelliklerine sahiptir, ancak bunların hepsi nesnenin sınıf tanımında belirtilere göre belirlenir.</span><span class="sxs-lookup"><span data-stu-id="d0141-237">Each instance has its own characteristics, but they all are based on what's specified in the object's class definition.</span></span>

## <a name="basic-syntax"></a><span data-ttu-id="d0141-238">Temel söz dizimi</span><span class="sxs-lookup"><span data-stu-id="d0141-238">Basic Syntax</span></span>

<span data-ttu-id="d0141-239">Daha önce, bir ASP.NET Web sayfaları sayfası oluşturma ve HTML biçimlendirmesine sunucu kodu ekleme hakkında temel bir örnek gördünüz.</span><span class="sxs-lookup"><span data-stu-id="d0141-239">Earlier you saw a basic example of how to create an ASP.NET Web Pages page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="d0141-240">Burada, programlama dili kuralları olan Razor söz dizimi &#8212; kullanarak ASP.NET sunucu kodu yazmanın temellerini öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-240">Here you'll learn the basics of writing ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="d0141-241">Programlamayla karşılaşırsanız (özellikle C, C++, C#, Visual Basic veya JavaScript kullandıysanız), burada okuduğunuzdan büyük bir şey tanıdık gelecektir.</span><span class="sxs-lookup"><span data-stu-id="d0141-241">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="d0141-242">Muhtemelen yalnızca sunucu kodunun *. cshtml* dosyalarındaki biçimlendirmeye nasıl eklendiği hakkında bilgi almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0141-242">You'll probably need to familiarize yourself only with how server code is added to markup in *.cshtml* files.</span></span>

<a id="BM_CombiningTextMarkupAndCode"></a>
### <a name="combining-text-markup-and-code-in-code-blocks"></a><span data-ttu-id="d0141-243">Kod bloklarında metin, biçimlendirme ve kod birleştirme</span><span class="sxs-lookup"><span data-stu-id="d0141-243">Combining Text, Markup, and Code in Code Blocks</span></span>

<span data-ttu-id="d0141-244">Sunucu kod blokları ' nda, genellikle sayfada metin veya biçimlendirme (veya her ikisi de) çıktısını almak istersiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-244">In server code blocks, you often want to output text or markup (or both) to the page.</span></span> <span data-ttu-id="d0141-245">Bir sunucu kod bloğu kod olmayan ve bunun yerine olarak işlenmesi gereken metin içeriyorsa, ASP.NET bu metni koddan ayırabilmelidir.</span><span class="sxs-lookup"><span data-stu-id="d0141-245">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="d0141-246">Bunu yapmak için birkaç yol vardır.</span><span class="sxs-lookup"><span data-stu-id="d0141-246">There are several ways to do this.</span></span>

- <span data-ttu-id="d0141-247">Metni `<p></p>` veya `<em></em>`gibi bir HTML öğesine koyun:</span><span class="sxs-lookup"><span data-stu-id="d0141-247">Enclose the text in an HTML element like `<p></p>` or `<em></em>`:</span></span>   

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample12.cshtml)]

    <span data-ttu-id="d0141-248">HTML öğesi metin, ek HTML öğeleri ve sunucu kodu ifadelerini içerebilir.</span><span class="sxs-lookup"><span data-stu-id="d0141-248">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="d0141-249">ASP.NET, açılan HTML etiketini (örneğin, `<p>`) gördüğünde, öğe ve içeriği gibi her şeyi tarayıcıya olduğu gibi işler ve sunucu kodu ifadelerini olduğu gibi çözer.</span><span class="sxs-lookup"><span data-stu-id="d0141-249">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything including the element and its content as is to the browser, resolving server-code expressions as it goes.</span></span>
- <span data-ttu-id="d0141-250">`@:` işlecini veya `<text>` öğesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d0141-250">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="d0141-251">`@:` düz metin veya eşleşmeyen HTML etiketleri içeren tek bir içerik satırı çıktısı verir; `<text>` öğesi çıktı için birden çok satır barındırır.</span><span class="sxs-lookup"><span data-stu-id="d0141-251">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="d0141-252">Bu seçenekler, çıktının bir parçası olarak bir HTML öğesi işlemek istemediğinizde yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="d0141-252">These options are useful when you don't want to render an HTML element as part of the output.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample13.cshtml)]

    <span data-ttu-id="d0141-253">Metnin birden çok satırını veya eşleşmeyen HTML etiketlerini çıkarmak istiyorsanız, her satırın önüne `@:`veya satırı bir `<text>` öğesine ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-253">If you want to output multiple lines of text or unmatched HTML tags, you can precede each line with `@:`, or you can enclose the line in a `<text>` element.</span></span> <span data-ttu-id="d0141-254">`@:` işleci gibi`<text>` Etiketler, metin içeriğini belirlemek için ASP.NET tarafından kullanılır ve sayfa çıktısında hiçbir şekilde işlenmez.</span><span class="sxs-lookup"><span data-stu-id="d0141-254">Like the `@:` operator,`<text>` tags are used by ASP.NET to identify text content and are never rendered in the page output.</span></span>

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample14.cshtml)]

    <span data-ttu-id="d0141-255">İlk örnek, önceki örneği yineler, ancak işlenecek metni kapsamak için tek bir çift `<text>` etiketi kullanır.</span><span class="sxs-lookup"><span data-stu-id="d0141-255">The first example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span> <span data-ttu-id="d0141-256">İkinci örnekte, `<text>` ve `</text>` etiketleri üç satırı kapsar; bunların hepsi, sunucu kodu ve eşleşen HTML etiketleriyle birlikte, bazı metin ve eşleşmeyen HTML etiketlerine (`<br />`) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d0141-256">In the second example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="d0141-257">Ayrıca, `@:` işleçle her bir satırdan de tek başına bir kez daha olabilirsiniz; Her iki yöntem de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d0141-257">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d0141-258">Bu bölümde &#8212; gösterildiği gibi metin yazdığınızda, bir HTML öğesi, `@:` işleci veya `<text>` öğesi &#8212; ASP.net, çıktıyı HTML olarak kodlamaz.</span><span class="sxs-lookup"><span data-stu-id="d0141-258">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="d0141-259">(Daha önce belirtildiği gibi, ASP.NET, bu bölümde belirtilen özel durumlar dışında, daha önce `@`sunucu kod ifadelerinin ve sunucu kodu bloklarının çıkışını kodladır.)</span><span class="sxs-lookup"><span data-stu-id="d0141-259">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="d0141-260">Boşlu</span><span class="sxs-lookup"><span data-stu-id="d0141-260">Whitespace</span></span>

<span data-ttu-id="d0141-261">Deyimdeki (ve dize sabit değerinin dışında) fazladan boşluklar, bu ifadeyi etkilemez:</span><span class="sxs-lookup"><span data-stu-id="d0141-261">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample15.cshtml)]

<span data-ttu-id="d0141-262">Deyimdeki bir satır sonu deyim üzerinde hiçbir etkiye sahip değildir ve daha okunaklı olması için deyimleri kaydırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-262">A line break in a statement has no effect on the statement, and you can wrap statements for readability.</span></span> <span data-ttu-id="d0141-263">Aşağıdaki deyimler aynıdır:</span><span class="sxs-lookup"><span data-stu-id="d0141-263">The following statements are the same:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample16.cshtml)]

<span data-ttu-id="d0141-264">Ancak, bir satırı dize sabit değerinin ortasında kaydıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="d0141-264">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="d0141-265">Aşağıdaki örnek çalışmıyor:</span><span class="sxs-lookup"><span data-stu-id="d0141-265">The following example doesn't work:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample17.cshtml)]

<span data-ttu-id="d0141-266">Yukarıdaki kod gibi birden çok satıra kaydırılan uzun bir dizeyi birleştirmek için iki seçenek vardır.</span><span class="sxs-lookup"><span data-stu-id="d0141-266">To combine a long string that wraps to multiple lines like the above code, there are two options.</span></span> <span data-ttu-id="d0141-267">Bu makalede daha sonra göreceğiniz birleştirme işlecini (`+`) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-267">You can use the concatenation operator (`+`), which you'll see later in this article.</span></span> <span data-ttu-id="d0141-268">Bu makalede daha önce gördüğünüz gibi, tam bir dize sabiti oluşturmak için `@` karakterini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-268">You can also use the `@` character to create a verbatim string literal, as you saw earlier in this article.</span></span> <span data-ttu-id="d0141-269">Satırlar arasında tam dize sabit değerlerini kesebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d0141-269">You can break verbatim string literals across lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample18.cshtml)]

### <a name="code-and-markup-comments"></a><span data-ttu-id="d0141-270">Kod (ve biçimlendirme) açıklamaları</span><span class="sxs-lookup"><span data-stu-id="d0141-270">Code (and Markup) Comments</span></span>

<span data-ttu-id="d0141-271">Açıklamalar sizin veya diğerleri için Not bırakmayı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d0141-271">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="d0141-272">Ayrıca, çalıştırmak istemediğiniz bir kod veya biçimlendirme bölümünü (*Açıklama*olarak) devre dışı bırakabilmeniz, ancak sayfada çalışmaya devam etmek isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-272">They also allow you to disable (*comment out*) a section of code or markup that you don't want to run but want to keep in your page for the time being.</span></span>

<span data-ttu-id="d0141-273">Razor kodu ve HTML işaretlemesi için farklı yorum sözdizimi vardır.</span><span class="sxs-lookup"><span data-stu-id="d0141-273">There's different commenting syntax for Razor code and for HTML markup.</span></span> <span data-ttu-id="d0141-274">Tüm razor kodlarında olduğu gibi, sayfa tarayıcıya gönderilmeden önce, Razor açıklamaları sunucu üzerinde işlenir (ve sonra kaldırılır).</span><span class="sxs-lookup"><span data-stu-id="d0141-274">As with all Razor code, Razor comments are processed (and then removed) on the server before the page is sent to the browser.</span></span> <span data-ttu-id="d0141-275">Bu nedenle, Razor açıklama sözdizimi, dosyayı düzenlerken görebileceğiniz, ancak sayfa kaynağında bile Kullanıcı görmemiş olan koda (veya biçimlendirme içine) yorum koymanıza imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="d0141-275">Therefore, the Razor commenting syntax lets you put comments into the code (or even into the markup) that you can see when you edit the file, but that users don't see, even in the page source.</span></span>

<span data-ttu-id="d0141-276">ASP.NET Razor açıklamaları için, yorumu `@*` ile başlatır ve `*@`ile sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="d0141-276">For ASP.NET Razor comments, you start the comment with `@*` and end it with `*@`.</span></span> <span data-ttu-id="d0141-277">Yorum bir veya birden çok satırda olabilir:</span><span class="sxs-lookup"><span data-stu-id="d0141-277">The comment can be on one line or multiple lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample19.cshtml)]

<span data-ttu-id="d0141-278">Kod bloğu içindeki bir açıklama aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d0141-278">Here is a comment within a code block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample20.cshtml)]

<span data-ttu-id="d0141-279">Bu kod, kod satırı açıklama satırı ile birlikte, aşağıdaki çalıştırılmayacak şekilde kod bloğu aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d0141-279">Here is the same block of code, with the line of code commented out so that it won't run:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample21.cshtml)]

<span data-ttu-id="d0141-280">Bir kod bloğu içinde, Razor açıklama sözdizimi kullanmanın alternatifi olarak, kullanmakta olduğunuz programlama dilinin yorum söz dizimini kullanabilirsiniz, örneğin C#:</span><span class="sxs-lookup"><span data-stu-id="d0141-280">Inside a code block, as an alternative to using Razor comment syntax, you can use the commenting syntax of the programming language you're using, such as C#:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample22.cshtml)]

<span data-ttu-id="d0141-281">' C#De, tek satırlık açıklamaların önünde `//` karakterleri ve çok satırlı açıklamalar `/*` ile başlayıp `*/`ile biter.</span><span class="sxs-lookup"><span data-stu-id="d0141-281">In C#, single-line comments are preceded by the `//` characters, and multi-line comments begin with `/*` and end with `*/`.</span></span> <span data-ttu-id="d0141-282">(Razor yorumlarında olduğu gibi C# , açıklamalar tarayıcıda işlenmez.)</span><span class="sxs-lookup"><span data-stu-id="d0141-282">(As with Razor comments, C# comments are not rendered to the browser.)</span></span>

<span data-ttu-id="d0141-283">Biçimlendirme için, büyük olasılıkla bildiğiniz gibi, bir HTML açıklaması oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d0141-283">For markup, as you probably know, you can create an HTML comment:</span></span>

[!code-xml[Main](introducing-razor-syntax-c/samples/sample23.xml)]

<span data-ttu-id="d0141-284">HTML açıklamaları `<!--` karakterle başlar ve `-->`biter.</span><span class="sxs-lookup"><span data-stu-id="d0141-284">HTML comments start with `<!--` characters and end with `-->`.</span></span> <span data-ttu-id="d0141-285">HTML açıklamalarını yalnızca metin değil, aynı zamanda sayfada tutmak isteyebileceğiniz ancak işlemek istemediğiniz HTML işaretlemesini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-285">You can use HTML comments to surround not only text, but also any HTML markup that you may want to keep in the page but don't want to render.</span></span> <span data-ttu-id="d0141-286">Bu HTML yorumu, etiketlerin ve içerdikleri metnin tüm içeriğini gizler:</span><span class="sxs-lookup"><span data-stu-id="d0141-286">This HTML comment will hide the entire content of the tags and the text they contain:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample24.html)]

<span data-ttu-id="d0141-287">Razor yorumlarından farklı olarak, HTML açıklamaları *sayfada işlenir ve* Kullanıcı bunları sayfa kaynağını görüntüleyerek görebilir.</span><span class="sxs-lookup"><span data-stu-id="d0141-287">Unlike Razor comments, HTML comments *are* rendered to the page and the user can see them by viewing the page source.</span></span>

<span data-ttu-id="d0141-288">Razor 'in C#iç içe bloklar üzerinde sınırlamalar vardır.</span><span class="sxs-lookup"><span data-stu-id="d0141-288">Razor has limitations on nested blocks of C#.</span></span> <span data-ttu-id="d0141-289">Daha fazla bilgi için bkz. [ C# adlandırılmış değişkenler ve Iç Içe bloklar bozuk kod oluşturur](http://aspnetwebstack.codeplex.com/workitem/1914)</span><span class="sxs-lookup"><span data-stu-id="d0141-289">For more information see [Named C# Variables and Nested Blocks Generate Broken Code](http://aspnetwebstack.codeplex.com/workitem/1914)</span></span>

## <a name="variables"></a><span data-ttu-id="d0141-290">Değişkenler</span><span class="sxs-lookup"><span data-stu-id="d0141-290">Variables</span></span>

<span data-ttu-id="d0141-291">Değişken, verileri depolamak için kullandığınız adlandırılmış bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="d0141-291">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="d0141-292">Değişkenleri herhangi bir şekilde adlandırın, ancak ad alfabetik bir karakterle başlamalı ve boşluk ya da ayrılmış karakterler içeremez.</span><span class="sxs-lookup"><span data-stu-id="d0141-292">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="d0141-293">Değişkenler ve veri türleri</span><span class="sxs-lookup"><span data-stu-id="d0141-293">Variables and Data Types</span></span>

<span data-ttu-id="d0141-294">Değişken, değişkende ne tür verilerin depolandığını gösteren belirli bir veri türüne sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="d0141-294">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="d0141-295">Dize değerlerini depolayan dize değişkenleriniz (&quot;Hello World&quot;), tam sayı değerlerini depolayan tamsayı değişkenleri (3 veya 79 gibi) ve tarih değerlerini çeşitli biçimlerde depolayan Tarih değişkenlerini (4/12/2012 veya Mart 2009 gibi) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-295">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="d0141-296">Ve kullanabileceğiniz pek çok farklı veri türü vardır.</span><span class="sxs-lookup"><span data-stu-id="d0141-296">And there are many other data types you can use.</span></span>

<span data-ttu-id="d0141-297">Ancak, genellikle bir değişken için bir tür belirtmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d0141-297">However, you generally don't have to specify a type for a variable.</span></span> <span data-ttu-id="d0141-298">Çoğu zaman, ASP.NET değişkende bulunan verilerin nasıl kullanıldığını temel alarak türü belirleyebilir.</span><span class="sxs-lookup"><span data-stu-id="d0141-298">Most of the time, ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="d0141-299">(Bazen bir tür belirtmeniz gerekir; bunun doğru olduğu örnekleri görürsünüz.)</span><span class="sxs-lookup"><span data-stu-id="d0141-299">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="d0141-300">`var` anahtar sözcüğünü kullanarak bir değişken bildirir (bir tür belirtmek istemiyorsanız) veya türün adını kullanarak:</span><span class="sxs-lookup"><span data-stu-id="d0141-300">You declare a variable using the `var` keyword (if you don't want to specify a type) or by using the name of the type:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample25.cshtml)]

<span data-ttu-id="d0141-301">Aşağıdaki örnekte, bir Web sayfasındaki değişkenlerin bazı tipik kullanımları gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="d0141-301">The following example shows some typical uses of variables in a web page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample26.cshtml)]

<span data-ttu-id="d0141-302">Önceki örnekleri bir sayfada birleştirirseniz, bunu bir tarayıcıda görüntülenmiş olarak görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="d0141-302">If you combine the previous examples in a page, you see this displayed in a browser:</span></span>

![Razor-Img9](introducing-razor-syntax-c/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="d0141-304">Veri türlerini dönüştürme ve test etme</span><span class="sxs-lookup"><span data-stu-id="d0141-304">Converting and Testing Data Types</span></span>

<span data-ttu-id="d0141-305">ASP.NET genellikle bir veri türünü otomatik olarak belirleyebilse de bazen olamaz.</span><span class="sxs-lookup"><span data-stu-id="d0141-305">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="d0141-306">Bu nedenle, açık bir dönüştürme gerçekleştirerek ASP.NET Out 'a yardımcı olmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="d0141-306">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="d0141-307">Türleri dönüştürmeniz gerekmese de, ne zaman çalıştığınız veri türlerini görmek için test etmeniz yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="d0141-307">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="d0141-308">En yaygın durum, bir dizeyi tamsayı veya tarih gibi başka bir türe dönüştürmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0141-308">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="d0141-309">Aşağıdaki örnek, bir dizeyi bir sayıya dönüştürmeniz gereken tipik bir durumu gösterir.</span><span class="sxs-lookup"><span data-stu-id="d0141-309">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample27.cshtml)]

<span data-ttu-id="d0141-310">Kural olarak, Kullanıcı girişi size dizeler olarak gelir.</span><span class="sxs-lookup"><span data-stu-id="d0141-310">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="d0141-311">Kullanıcılardan bir sayı girmeleri ve bir rakam girseler bile, Kullanıcı girişi gönderildiğinde ve kodu kodda okuduğunuzda, veriler dize biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="d0141-311">Even if you've prompted users to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="d0141-312">Bu nedenle, dizeyi bir sayıya dönüştürmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0141-312">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="d0141-313">Örnekte, değerleri dönüşümlemeden aritmetik gerçekleştirmeye çalışırsanız, ASP.NET iki dize ekleyemediğinden aşağıdaki hata oluşur:</span><span class="sxs-lookup"><span data-stu-id="d0141-313">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

<span data-ttu-id="d0141-314">*' String ' türü örtük olarak ' int ' türüne dönüştürülemez.*</span><span class="sxs-lookup"><span data-stu-id="d0141-314">*Cannot implicitly convert type 'string' to 'int'.*</span></span>

<span data-ttu-id="d0141-315">Değerleri tamsayılara dönüştürmek için `AsInt` yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="d0141-315">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="d0141-316">Dönüştürme başarılı olursa, sayıları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-316">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="d0141-317">Aşağıdaki tabloda, değişkenler için bazı ortak dönüştürme ve test yöntemleri listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="d0141-317">The following table lists some common conversion and test methods for variables.</span></span>

:::row:::
    :::column:::
    <span data-ttu-id="d0141-318"><strong>Yöntem</strong></span><span class="sxs-lookup"><span data-stu-id="d0141-318"><strong>Method</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="d0141-319"><strong>Açıklama</strong></span><span class="sxs-lookup"><span data-stu-id="d0141-319"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="d0141-320"><strong>Örnek</strong></span><span class="sxs-lookup"><span data-stu-id="d0141-320"><strong>Example</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="d0141-321">Tam sayıyı temsil eden bir dizeyi ("593" gibi) tamsayıya dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="d0141-321">Converts a string that represents a whole number (like "593") to an integer.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample28.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="d0141-322">&quot;true&quot; veya &quot;false&quot; gibi bir dizeyi Boolean bir türe dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="d0141-322">Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample29.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="d0141-323">&quot;1,3&quot; veya &quot;&quot; 7,439 gibi ondalık değeri olan bir dizeyi kayan noktalı bir sayıya dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="d0141-323">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample30.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="d0141-324">&quot;1,3&quot; veya &quot;&quot; 7,439 gibi ondalık bir değere sahip bir dizeyi ondalık bir sayıya dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="d0141-324">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number.</span></span> <span data-ttu-id="d0141-325">(ASP.NET ' de, ondalık sayı bir kayan noktalı sayıdan daha belirgin olur.)</span><span class="sxs-lookup"><span data-stu-id="d0141-325">(In ASP.NET, a decimal number is more precise than a floating-point number.)</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample31.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="d0141-326">Bir tarih ve saat değerini temsil eden bir dizeyi ASP.NET `DateTime` türüne dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="d0141-326">Converts a string that represents a date and time value to the ASP.NET `DateTime` type.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample32.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="d0141-327">Diğer veri türlerini bir dizeye dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="d0141-327">Converts any other data type to a string.</span></span>
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample33.js)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a><span data-ttu-id="d0141-328">İşleçler</span><span class="sxs-lookup"><span data-stu-id="d0141-328">Operators</span></span>

<span data-ttu-id="d0141-329">İşleci, bir ifadede ne tür komutun gerçekleştirileceğini ASP.NET söyleyen bir anahtar sözcüktür veya karakterdir.</span><span class="sxs-lookup"><span data-stu-id="d0141-329">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="d0141-330">C# Dil (ve buna dayalı Razor söz dizimi) birçok işleci destekler, ancak kullanmaya başlamak için yalnızca birkaç tane tanımak yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="d0141-330">The C# language (and the Razor syntax that's based on it) supports many operators, but you only need to recognize a few to get started.</span></span> <span data-ttu-id="d0141-331">Aşağıdaki tabloda en yaygın operatörler özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="d0141-331">The following table summarizes the most common operators.</span></span>

:::row:::
    :::column:::
    <span data-ttu-id="d0141-332"><strong>İşlecinde</strong></span><span class="sxs-lookup"><span data-stu-id="d0141-332"><strong>Operator</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="d0141-333"><strong>Açıklama</strong></span><span class="sxs-lookup"><span data-stu-id="d0141-333"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="d0141-334"><strong>Örnekler</strong></span><span class="sxs-lookup"><span data-stu-id="d0141-334"><strong>Examples</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="d0141-335">`+` `-` `*` `/`</span><span class="sxs-lookup"><span data-stu-id="d0141-335">`+` `-` `*` `/`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="d0141-336">Sayısal ifadelerde kullanılan matematik işleçleri.</span><span class="sxs-lookup"><span data-stu-id="d0141-336">Math operators used in numerical expressions.</span></span>
    :::column-end:::
    :::column:::
        [!code-css[Main](introducing-razor-syntax-c/samples/sample34.css)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="d0141-337">Atama.</span><span class="sxs-lookup"><span data-stu-id="d0141-337">Assignment.</span></span> <span data-ttu-id="d0141-338">Bir deyimin sağ tarafındaki değeri, sol taraftaki nesneye atar.</span><span class="sxs-lookup"><span data-stu-id="d0141-338">Assigns the value on the right side of a statement to the object on the left side.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample35.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `==`
    :::column-end:::
    :::column:::
    <span data-ttu-id="d0141-339">Eþit.</span><span class="sxs-lookup"><span data-stu-id="d0141-339">Equality.</span></span> <span data-ttu-id="d0141-340">Değerler eşitse `true` döndürür.</span><span class="sxs-lookup"><span data-stu-id="d0141-340">Returns `true` if the values are equal.</span></span> <span data-ttu-id="d0141-341">(`=` işleci ve `==` işleci arasındaki ayrımı fark ettiğini unutmayın.)</span><span class="sxs-lookup"><span data-stu-id="d0141-341">(Notice the distinction between the `=` operator and the `==` operator.)</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample36.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="d0141-342">Olmama.</span><span class="sxs-lookup"><span data-stu-id="d0141-342">Inequality.</span></span> <span data-ttu-id="d0141-343">Değerler eşit değilse `true` döndürür.</span><span class="sxs-lookup"><span data-stu-id="d0141-343">Returns `true` if the values are not equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample37.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="d0141-344">Küçüktür, büyüktür, küçüktür, küçüktür ve eşittir, veya eşittir.</span><span class="sxs-lookup"><span data-stu-id="d0141-344">Less-than, greater-than, less-than-or-equal, and greater-than-or-equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample38.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+`
    :::column-end:::
    :::column:::
    <span data-ttu-id="d0141-345">Dizeleri birleştirmek için kullanılan birleştirme.</span><span class="sxs-lookup"><span data-stu-id="d0141-345">Concatenation, which is used to join strings.</span></span> <span data-ttu-id="d0141-346">ASP.NET bu işleç ile toplama işleci arasındaki farkı, ifadenin veri türüne göre bilir.</span><span class="sxs-lookup"><span data-stu-id="d0141-346">ASP.NET knows the difference between this operator and the addition operator based on the data type of the expression.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample39.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="d0141-347">`+=` `-=`</span><span class="sxs-lookup"><span data-stu-id="d0141-347">`+=` `-=`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="d0141-348">Bir değişkenden 1 (sırasıyla) ekleyen ve çıkartacak artırma ve azaltma işleçleri.</span><span class="sxs-lookup"><span data-stu-id="d0141-348">The increment and decrement operators, which add and subtract 1 (respectively) from a variable.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample40.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
    <span data-ttu-id="d0141-349">Nokta.</span><span class="sxs-lookup"><span data-stu-id="d0141-349">Dot.</span></span> <span data-ttu-id="d0141-350">Nesneleri ve bunların özelliklerini ve yöntemlerini ayırt etmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d0141-350">Used to distinguish objects and their properties and methods.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample41.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="d0141-351">Ayraçlar.</span><span class="sxs-lookup"><span data-stu-id="d0141-351">Parentheses.</span></span> <span data-ttu-id="d0141-352">İfadeleri gruplandırmak ve parametreleri yöntemlere geçirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d0141-352">Used to group expressions and to pass parameters to methods.</span></span>
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample42.js)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `[]`
    :::column-end:::
    :::column:::
    <span data-ttu-id="d0141-353">Köşeli.</span><span class="sxs-lookup"><span data-stu-id="d0141-353">Brackets.</span></span> <span data-ttu-id="d0141-354">Dizilerde veya koleksiyonlardaki değerlere erişmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d0141-354">Used for accessing values in arrays or collections.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample43.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!`
    :::column-end:::
    :::column:::
    <span data-ttu-id="d0141-355">Başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="d0141-355">Not.</span></span> <span data-ttu-id="d0141-356">`true` bir değeri `false` tersine çevirir ve tam tersi de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d0141-356">Reverses a `true` value to `false` and vice versa.</span></span> <span data-ttu-id="d0141-357">Genellikle `false` test etmek için (`true`değil) kısayol yöntemi olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d0141-357">Typically used as a shorthand way to test for `false` (that is, for not `true`).</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample44.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="d0141-358">`&&` `||`</span><span class="sxs-lookup"><span data-stu-id="d0141-358">`&&` `||`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="d0141-359">Koşulları birbirine bağlamak için kullanılan mantıksal AND ve OR.</span><span class="sxs-lookup"><span data-stu-id="d0141-359">Logical AND and OR, which are used to link conditions together.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample45.cs)]
    :::column-end:::
:::row-end:::

<a id="ID_WorkingWithFileAndFolderPaths"></a>
## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="d0141-360">Kodda dosya ve klasör yollarıyla çalışma</span><span class="sxs-lookup"><span data-stu-id="d0141-360">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="d0141-361">Genellikle kodunuzda dosya ve klasör yolları ile çalışırsınız.</span><span class="sxs-lookup"><span data-stu-id="d0141-361">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="d0141-362">Geliştirme bilgisayarınızda görünebilen bir Web sitesi için fiziksel klasör yapısına bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d0141-362">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="d0141-363">URL 'Ler ve yollarla ilgili bazı temel ayrıntılar aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d0141-363">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="d0141-364">URL, bir etki alanı adı (`http://www.example.com`) veya sunucu adı (`http://localhost`, `http://mycomputer`) ile başlar.</span><span class="sxs-lookup"><span data-stu-id="d0141-364">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="d0141-365">Bir URL, ana bilgisayardaki fiziksel bir yola karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="d0141-365">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="d0141-366">Örneğin, `http://myserver` sunucuda *C:\websites\mywebsite* klasörüne karşılık gelebilir.</span><span class="sxs-lookup"><span data-stu-id="d0141-366">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="d0141-367">Sanal yol, tüm yolu belirtmek zorunda kalmadan koddaki yolları temsil etmek için toplu bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="d0141-367">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="d0141-368">Bu, etki alanı veya sunucu adını izleyen bir URL 'nin bölümünü içerir.</span><span class="sxs-lookup"><span data-stu-id="d0141-368">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="d0141-369">Sanal yollar kullandığınızda, yolları güncelleştirmek zorunda kalmadan kodunuzu farklı bir etki alanına veya sunucuya taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-369">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="d0141-370">Farklılıkları anlamanıza yardımcı olacak bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d0141-370">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="d0141-371">URL 'YI doldurun</span><span class="sxs-lookup"><span data-stu-id="d0141-371">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="d0141-372">Sunucu adı</span><span class="sxs-lookup"><span data-stu-id="d0141-372">Server name</span></span> | <span data-ttu-id="d0141-373">*mycompanyserver*</span><span class="sxs-lookup"><span data-stu-id="d0141-373">*mycompanyserver*</span></span> |
| <span data-ttu-id="d0141-374">Sanal yol</span><span class="sxs-lookup"><span data-stu-id="d0141-374">Virtual path</span></span> | <span data-ttu-id="d0141-375">*/humanresources/CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="d0141-375">*/humanresources/CompanyPolicy.htm*</span></span> |
| <span data-ttu-id="d0141-376">Fiziksel yol</span><span class="sxs-lookup"><span data-stu-id="d0141-376">Physical path</span></span> | <span data-ttu-id="d0141-377">*C:\websites\humanresources\companypolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="d0141-377">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span></span> |

<span data-ttu-id="d0141-378">Sanal kök, C: sürücünüzün kökünde olduğu gibi/olur.</span><span class="sxs-lookup"><span data-stu-id="d0141-378">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="d0141-379">(Sanal klasör yolları her zaman eğik çizgi kullanır.) Bir klasörün sanal yolunun fiziksel klasörle aynı ada sahip olması gerekmez; Bu bir diğer ad olabilir.</span><span class="sxs-lookup"><span data-stu-id="d0141-379">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="d0141-380">(Üretim sunucularında, sanal yol nadiren tam bir fiziksel yolla eşleşir.)</span><span class="sxs-lookup"><span data-stu-id="d0141-380">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="d0141-381">Kodda dosya ve klasörlerle çalışırken, çalıştığınız nesnelere bağlı olarak, bazen fiziksel yola ve bazen bir sanal yola başvurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0141-381">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="d0141-382">ASP.NET, kodda dosya ve klasör yollarıyla çalışmak için size bu araçları sağlar: `Server.MapPath` yöntemi ve `~` işleci ve `Href` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d0141-382">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="d0141-383">Sanal fiziksel yollara dönüştürme: Server. MapPath yöntemi</span><span class="sxs-lookup"><span data-stu-id="d0141-383">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="d0141-384">`Server.MapPath` yöntemi, bir sanal yolu ( */default.exe*gibi) mutlak bir fiziksel yola ( *C:\websites\mywebsitefolder\default.exe*gibi) dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="d0141-384">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="d0141-385">Bu yöntemi, tüm fiziksel yola ihtiyacınız olduğunda kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="d0141-385">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="d0141-386">Tipik bir örnek, Web sunucusunda bir metin dosyası veya resim dosyası okurken veya yazarken bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="d0141-386">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="d0141-387">Genellikle sitenizin bir barındırma sitesinin sunucusunda mutlak fiziksel yolunu bilemezsiniz; bu nedenle, bu yöntem, bildiğiniz yolu (sanal yol) sizin için sunucuda karşılık gelen yola dönüştürebilir.</span><span class="sxs-lookup"><span data-stu-id="d0141-387">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="d0141-388">Bir dosya veya klasörün sanal yolunu yöntemine geçirirsiniz ve fiziksel yolu döndürür:</span><span class="sxs-lookup"><span data-stu-id="d0141-388">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample46.cshtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="d0141-389">Sanal köke başvuruluyor: ~ operator ve href yöntemi</span><span class="sxs-lookup"><span data-stu-id="d0141-389">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="d0141-390">Bir *. cshtml* veya *. vbhtml* dosyasında, `~` işlecini kullanarak sanal kök yoluna başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-390">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="d0141-391">Sayfaları bir sitede bir konuma taşıyabilmeniz ve içerdikleri bağlantıların diğer sayfalara bölünememesi nedeniyle bu çok yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="d0141-391">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="d0141-392">Web sitenizi farklı bir konuma taşımanız durumunda da yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="d0141-392">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="d0141-393">İşte bazı örnekler:</span><span class="sxs-lookup"><span data-stu-id="d0141-393">Here are some examples:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample47.cshtml)]

<span data-ttu-id="d0141-394">Web sitesi `http://myserver/myapp`, sayfa çalışırken ASP.NET bu yolları nasıl değerlendilecektir:</span><span class="sxs-lookup"><span data-stu-id="d0141-394">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- <span data-ttu-id="d0141-395">`myImagesFolder`: `http://myserver/myapp/images`</span><span class="sxs-lookup"><span data-stu-id="d0141-395">`myImagesFolder`: `http://myserver/myapp/images`</span></span>
- <span data-ttu-id="d0141-396">`myStyleSheet`: `http://myserver/myapp/styles/Stylesheet.css`</span><span class="sxs-lookup"><span data-stu-id="d0141-396">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span></span>

<span data-ttu-id="d0141-397">(Bu yolları gerçekten değişkenin değerleri olarak görmezsiniz, ancak ASP.NET, bu gibi yollar gibi davranır.)</span><span class="sxs-lookup"><span data-stu-id="d0141-397">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="d0141-398">`~` işlecini hem sunucu kodunda (yukarıdaki gibi) hem de biçimlendirme ' de şu şekilde kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d0141-398">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample48.html)]

<span data-ttu-id="d0141-399">Biçimlendirme ' de, görüntü dosyaları, diğer Web sayfaları ve CSS dosyaları gibi kaynaklara yollar oluşturmak için `~` işlecini kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="d0141-399">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="d0141-400">Sayfa çalıştığında, ASP.NET sayfayı (hem kod hem de biçimlendirme) arar ve tüm `~` başvurularını uygun yola çözümler.</span><span class="sxs-lookup"><span data-stu-id="d0141-400">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="d0141-401">Koşullu mantık ve döngüler</span><span class="sxs-lookup"><span data-stu-id="d0141-401">Conditional Logic and Loops</span></span>

<span data-ttu-id="d0141-402">ASP.NET sunucu kodu, koşullara göre görevleri gerçekleştirmenize ve deyimleri belirli sayıda kez tekrardan (bir döngü çalıştıran kod) tekrarlamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d0141-402">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times (that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="d0141-403">Test koşulları</span><span class="sxs-lookup"><span data-stu-id="d0141-403">Testing Conditions</span></span>

<span data-ttu-id="d0141-404">Basit bir koşulu test etmek için, belirttiğiniz bir teste göre doğru veya yanlış döndüren `if` deyiminizi kullanırsınız:</span><span class="sxs-lookup"><span data-stu-id="d0141-404">To test a simple condition you use the `if` statement, which returns true or false based on a test you specify:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample49.cshtml)]

<span data-ttu-id="d0141-405">`if` anahtar sözcüğü bir blok başlatır.</span><span class="sxs-lookup"><span data-stu-id="d0141-405">The `if` keyword starts a block.</span></span> <span data-ttu-id="d0141-406">Gerçek test (koşul) parantez içinde ve true veya false değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="d0141-406">The actual test (condition) is in parentheses and returns true or false.</span></span> <span data-ttu-id="d0141-407">Test true olursa çalıştırılan deyimler küme ayraçları içine alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="d0141-407">The statements that run if the test is true are enclosed in braces.</span></span> <span data-ttu-id="d0141-408">`if` deyimi, koşul yanlış ise çalıştırılacak deyimleri belirten bir `else` bloğu içerebilir:</span><span class="sxs-lookup"><span data-stu-id="d0141-408">An `if` statement can include an `else` block that specifies statements to run if the condition is false:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample50.cshtml)]

<span data-ttu-id="d0141-409">`else if` bloğunu kullanarak birden çok koşul ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d0141-409">You can add multiple conditions using an `else if` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample51.cshtml)]

<span data-ttu-id="d0141-410">Bu örnekte, IF bloğundaki ilk koşul true değilse `else if` koşulu denetlenir.</span><span class="sxs-lookup"><span data-stu-id="d0141-410">In this example, if the first condition in the if block is not true, the `else if` condition is checked.</span></span> <span data-ttu-id="d0141-411">Bu koşul karşılanıyorsa, `else if` bloğundaki deyimler yürütülür.</span><span class="sxs-lookup"><span data-stu-id="d0141-411">If that condition is met, the statements in the `else if` block are executed.</span></span> <span data-ttu-id="d0141-412">Koşulların hiçbiri karşılanmazsa, `else` bloğundaki deyimler yürütülür.</span><span class="sxs-lookup"><span data-stu-id="d0141-412">If none of the conditions are met, the statements in the `else` block are executed.</span></span> <span data-ttu-id="d0141-413">Herhangi bir sayıda başka If bloğu ekleyebilirsiniz ve ardından &quot;başka&quot; koşulu olan her şeyi `else` bir blok ile kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-413">You can add any number of else if blocks, and then close with an `else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="d0141-414">Çok sayıda koşulu test etmek için `switch` bloğunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="d0141-414">To test a large number of conditions, use a `switch` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample52.cshtml)]

<span data-ttu-id="d0141-415">Sınanacak değer parantez içinde (örnekte, `weekday` değişken).</span><span class="sxs-lookup"><span data-stu-id="d0141-415">The value to test is in parentheses (in the example, the `weekday` variable).</span></span> <span data-ttu-id="d0141-416">Her bir test, iki nokta üst üste (:) ile biten `case` bir ifade kullanır.</span><span class="sxs-lookup"><span data-stu-id="d0141-416">Each individual test uses a `case` statement that ends with a colon (:).</span></span> <span data-ttu-id="d0141-417">Bir `case` deyimin değeri test değeriyle eşleşiyorsa, bu durum bloğundaki kod yürütülür.</span><span class="sxs-lookup"><span data-stu-id="d0141-417">If the value of a `case` statement matches the test value, the code in that case block is executed.</span></span> <span data-ttu-id="d0141-418">Her Case ifadesini bir `break` ifadesiyle kapatırsınız.</span><span class="sxs-lookup"><span data-stu-id="d0141-418">You close each case statement with a `break` statement.</span></span> <span data-ttu-id="d0141-419">(Her bir `case` bloğuna kesme eklemeyi unutursanız, sonraki `case` deyimindeki kod de çalıştırılır.) `switch` bloğu, diğer durumların hiçbiri doğru değilse, başka bir &quot;her şey&quot; seçeneğinin son durumu olarak bir `default` bildirimine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d0141-419">(If you forget to include break in each `case` block, the code from the next `case` statement will run also.) A `switch` block often has a `default` statement as the last case for an &quot;everything else&quot; option that runs if none of the other cases are true.</span></span>

<span data-ttu-id="d0141-420">Bir tarayıcıda görünen son iki koşullu blok sonucu:</span><span class="sxs-lookup"><span data-stu-id="d0141-420">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor-Img10](introducing-razor-syntax-c/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="d0141-422">Döngü kodu</span><span class="sxs-lookup"><span data-stu-id="d0141-422">Looping Code</span></span>

<span data-ttu-id="d0141-423">Genellikle aynı deyimleri tekrar tekrar çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0141-423">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="d0141-424">Bu, döngüye göre yapılır.</span><span class="sxs-lookup"><span data-stu-id="d0141-424">You do this by looping.</span></span> <span data-ttu-id="d0141-425">Örneğin, çoğu kez bir veri koleksiyonundaki her öğe için aynı deyimleri çalıştırırsınız.</span><span class="sxs-lookup"><span data-stu-id="d0141-425">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="d0141-426">Kaç kez döngüye almak istediğinizi biliyorsanız `for` döngüsünü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-426">If you know exactly how many times you want to loop, you can use a `for` loop.</span></span> <span data-ttu-id="d0141-427">Bu tür bir döngü, özellikle daha fazla sayım veya sayım için yararlıdır:</span><span class="sxs-lookup"><span data-stu-id="d0141-427">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample53.html)]

<span data-ttu-id="d0141-428">Döngü `for` anahtar sözcüğüyle başlar, sonra parantez içinde üç deyim gelir, her biri noktalı virgül ile sonlandırılır.</span><span class="sxs-lookup"><span data-stu-id="d0141-428">The loop begins with the `for` keyword, followed by three statements in parentheses, each terminated with a semicolon.</span></span>

- <span data-ttu-id="d0141-429">Parantez içinde, ilk ifade (`var i=10;`) bir sayaç oluşturur ve 10 ' a başlatır.</span><span class="sxs-lookup"><span data-stu-id="d0141-429">Inside the parentheses, the first statement (`var i=10;`) creates a counter and initializes it to 10.</span></span> <span data-ttu-id="d0141-430">Herhangi bir değişkeni kullanabileceğiniz `i` &#8212; sayaç adını yazmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d0141-430">You don't have to name the counter `i` &#8212; you can use any variable.</span></span> <span data-ttu-id="d0141-431">`for` döngüsü çalıştığında, sayaç otomatik olarak artırılır.</span><span class="sxs-lookup"><span data-stu-id="d0141-431">When the `for` loop runs, the counter is automatically incremented.</span></span>
- <span data-ttu-id="d0141-432">İkinci ifade (`i < 21;`), ne kadar saymak istediğinize ilişkin koşulu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d0141-432">The second statement (`i < 21;`) sets the condition for how far you want to count.</span></span> <span data-ttu-id="d0141-433">Bu durumda, en fazla 20 ' ye gitmesini istersiniz (yani sayaç 21 ' den az olduğunda devam edin).</span><span class="sxs-lookup"><span data-stu-id="d0141-433">In this case, you want it to go to a maximum of 20 (that is, keep going while the counter is less than 21).</span></span>
- <span data-ttu-id="d0141-434">Üçüncü ifade (`i++`) bir artırma işleci kullanır, bu da her döngü her çalıştığında sayacın kendisine 1 ekleneceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="d0141-434">The third statement (`i++` ) uses an increment operator, which simply specifies that the counter should have 1 added to it each time the loop runs.</span></span>

<span data-ttu-id="d0141-435">Küme ayraçları içinde döngünün her yinelemesi için çalıştırılacak koddur.</span><span class="sxs-lookup"><span data-stu-id="d0141-435">Inside the braces is the code that will run for each iteration of the loop.</span></span> <span data-ttu-id="d0141-436">Biçimlendirme, her seferinde yeni bir paragraf (`<p>` öğesi) oluşturur ve `i` değerini (sayaç) görüntüleyerek çıktıya bir satır ekler.</span><span class="sxs-lookup"><span data-stu-id="d0141-436">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of `i` (the counter).</span></span> <span data-ttu-id="d0141-437">Bu sayfayı çalıştırdığınızda örnek, her satırda öğe numarasını gösteren metinle birlikte çıktıyı görüntüleyen 11 satır oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d0141-437">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor-Img11](introducing-razor-syntax-c/_static/image11.jpg)

<span data-ttu-id="d0141-439">Bir koleksiyon veya dizi ile çalışıyorsanız, genellikle bir `foreach` döngüsü kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="d0141-439">If you're working with a collection or array, you often use a `foreach` loop.</span></span> <span data-ttu-id="d0141-440">Bir koleksiyon benzer nesneler grubudur ve `foreach` döngüsü koleksiyondaki her öğe üzerinde bir görevi gerçekleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="d0141-440">A collection is a group of similar objects, and the `foreach` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="d0141-441">Bu tür bir döngü koleksiyonlar için uygundur, çünkü `for` döngüsünün aksine sayacı artırmanız veya bir sınır ayarlamanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d0141-441">This type of loop is convenient for collections, because unlike a `for` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="d0141-442">Bunun yerine, `foreach` döngü kodu yalnızca, tamamlanana kadar koleksiyon üzerinden ilerler.</span><span class="sxs-lookup"><span data-stu-id="d0141-442">Instead, the `foreach` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="d0141-443">Örneğin, aşağıdaki kod, Web sunucunuz hakkında bilgi içeren bir nesnesi olan `Request.ServerVariables` koleksiyonundaki öğeleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="d0141-443">For example, the following code returns the items in the `Request.ServerVariables` collection, which is an object that contains information about your web server.</span></span> <span data-ttu-id="d0141-444">HTML madde işaretli listesinde yeni bir `<li>` öğesi oluşturarak her öğenin adını göstermek için `foreac` h döngüsünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="d0141-444">It uses a `foreac` h loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample54.html)]

<span data-ttu-id="d0141-445">`foreach` anahtar kelimesinin ardından, koleksiyondaki tek bir öğeyi temsil eden (örnekte, `var item`), ardından `in` anahtar sözcüğünü ve ardından, sonra da kullanmak istediğiniz koleksiyonu içeren bir değişken bildirdiğiniz parantezler gelir.</span><span class="sxs-lookup"><span data-stu-id="d0141-445">The `foreach` keyword is followed by parentheses where you declare a variable that represents a single item in the collection (in the example, `var item`), followed by the `in` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="d0141-446">`foreach` döngüsünün gövdesinde, daha önce bildirdiğiniz değişkeni kullanarak geçerli öğeye erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-446">In the body of the `foreach` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor-Img12](introducing-razor-syntax-c/_static/image12.jpg)

<span data-ttu-id="d0141-448">Daha genel amaçlı bir döngü oluşturmak için `while` ifadesini kullanın:</span><span class="sxs-lookup"><span data-stu-id="d0141-448">To create a more general-purpose loop, use the `while` statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample55.cshtml)]

<span data-ttu-id="d0141-449">Bir `while` döngüsü, `while` anahtar sözcüğüyle başlar ve sonra parantez, döngünün ne kadar süreyle devam ettiğini (`countNum` 50 ' den az olduğu sürece), sonra da yinelemeyi yineleme olarak belirler.</span><span class="sxs-lookup"><span data-stu-id="d0141-449">A `while` loop begins with the `while` keyword, followed by parentheses where you specify how long the loop continues (here, for as long as `countNum` is less than 50), then the block to repeat.</span></span> <span data-ttu-id="d0141-450">Döngüler genellikle sayma için kullanılan bir değişken veya nesneden artış (ekleme) veya azaltma (çıkarma).</span><span class="sxs-lookup"><span data-stu-id="d0141-450">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="d0141-451">Örnekte, `+=` işleci döngünün her çalıştığında `countNum` 1 ' i ekler.</span><span class="sxs-lookup"><span data-stu-id="d0141-451">In the example, the `+=` operator adds 1 to `countNum` each time the loop runs.</span></span> <span data-ttu-id="d0141-452">(Döngüsel bir döngüsünde bir değişkeni azaltmak için, azaltma işleci `-=`) kullanın.</span><span class="sxs-lookup"><span data-stu-id="d0141-452">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`).</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="d0141-453">Nesneler ve koleksiyonlar</span><span class="sxs-lookup"><span data-stu-id="d0141-453">Objects and Collections</span></span>

<span data-ttu-id="d0141-454">Bir ASP.NET Web sitesindeki neredeyse her şey, Web sayfasının kendisi de dahil olmak üzere bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="d0141-454">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="d0141-455">Bu bölümde, kodunuzda sıkça çalışacağımız bazı önemli nesneler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d0141-455">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="d0141-456">Sayfa nesneleri</span><span class="sxs-lookup"><span data-stu-id="d0141-456">Page Objects</span></span>

<span data-ttu-id="d0141-457">ASP.NET ' deki en temel nesne, sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="d0141-457">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="d0141-458">Sayfa nesnesinin özelliklerine, uygun herhangi bir nesne olmadan doğrudan erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-458">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="d0141-459">Aşağıdaki kod, sayfanın `Request` nesnesini kullanarak sayfanın dosya yolunu alır:</span><span class="sxs-lookup"><span data-stu-id="d0141-459">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample56.cshtml)]

<span data-ttu-id="d0141-460">Geçerli sayfa nesnesindeki özelliklere ve yöntemlere başvurduğunuzdan emin olmak için, kodunuzda sayfa nesnesini göstermek üzere `this` anahtar sözcüğünü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-460">To make it clear that you're referencing properties and methods on the current page object, you can optionally use the keyword `this` to represent the page object in your code.</span></span> <span data-ttu-id="d0141-461">Aşağıda, sayfayı göstermek için `this` eklenen önceki kod örneği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d0141-461">Here is the previous code example, with `this` added to represent the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample57.cshtml)]

<span data-ttu-id="d0141-462">`Page` nesnenin özelliklerini kullanarak çok fazla bilgi alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d0141-462">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- <span data-ttu-id="d0141-463">`Request`.</span><span class="sxs-lookup"><span data-stu-id="d0141-463">`Request`.</span></span> <span data-ttu-id="d0141-464">Zaten gördüğünüze göre, bu, istek ne tür bir tarayıcı, sayfanın URL 'SI, Kullanıcı kimliği vb. gibi geçerli istek hakkındaki bilgilerin bir koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="d0141-464">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- <span data-ttu-id="d0141-465">`Response`.</span><span class="sxs-lookup"><span data-stu-id="d0141-465">`Response`.</span></span> <span data-ttu-id="d0141-466">Bu, sunucu kodunun çalışmayı tamamladığında tarayıcıya gönderilecek yanıt (sayfa) hakkındaki bilgilerin bir koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="d0141-466">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="d0141-467">Örneğin, yanıta bilgi yazmak için bu özelliği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-467">For example, you can use this property to write information into the response.</span></span> 

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample58.cshtml)]

<a id="ID_CollectionsAndObjects"></a>
### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="d0141-468">Koleksiyon nesneleri (diziler ve sözlükler)</span><span class="sxs-lookup"><span data-stu-id="d0141-468">Collection Objects (Arrays and Dictionaries)</span></span>

<span data-ttu-id="d0141-469">Bir *koleksiyon* , bir veritabanından `Customer` nesneleri koleksiyonu gibi aynı türde bir nesne grubudur.</span><span class="sxs-lookup"><span data-stu-id="d0141-469">A *collection* is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="d0141-470">ASP.NET, `Request.Files` koleksiyonu gibi birçok yerleşik koleksiyon içerir.</span><span class="sxs-lookup"><span data-stu-id="d0141-470">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="d0141-471">Genellikle koleksiyonlardaki verilerle çalışırsınız.</span><span class="sxs-lookup"><span data-stu-id="d0141-471">You'll often work with data in collections.</span></span> <span data-ttu-id="d0141-472">İki ortak koleksiyon türü *dizi* ve *sözlüktür*.</span><span class="sxs-lookup"><span data-stu-id="d0141-472">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="d0141-473">Bir dizi benzer öğeler koleksiyonunu depolamak istediğinizde ancak her bir öğeyi tutacak ayrı bir değişken oluşturmak istemediğinizde yararlıdır:</span><span class="sxs-lookup"><span data-stu-id="d0141-473">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample59.cshtml)]

<span data-ttu-id="d0141-474">Diziler ile, `string`, `int`veya `DateTime`gibi belirli bir veri türünü bildirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-474">With arrays, you declare a specific data type, such as `string`, `int`, or `DateTime`.</span></span> <span data-ttu-id="d0141-475">Değişkenin bir dizi içerebileceğini göstermek için bildirime köşeli ayraç eklersiniz (`string[]` veya `int[]`gibi).</span><span class="sxs-lookup"><span data-stu-id="d0141-475">To indicate that the variable can contain an array, you add brackets to the declaration (such as `string[]` or `int[]`).</span></span> <span data-ttu-id="d0141-476">Bir dizideki öğelere konumlarını (Dizin) veya `foreach` ifadesini kullanarak erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-476">You can access items in an array using their position (index) or by using the `foreach` statement.</span></span> <span data-ttu-id="d0141-477">Dizi dizinleri sıfır tabanlıdır &#8212; , ilk öğe 0 ' dır, ikinci öğe ise 1 konumunda ve bu şekilde devam eder.</span><span class="sxs-lookup"><span data-stu-id="d0141-477">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample60.cshtml)]

<span data-ttu-id="d0141-478">Bir dizideki öğelerin sayısını `Length` özelliğini alarak belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-478">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="d0141-479">Dizideki belirli bir öğenin konumunu almak için (diziyi aramak için) `Array.IndexOf` yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d0141-479">To get the position of a specific item in the array (to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="d0141-480">Ayrıca, bir dizinin içeriğini ters çevirme (`Array.Reverse` yöntemi) veya içeriği sıralama (`Array.Sort` yöntemi) gibi işlemleri de yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-480">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="d0141-481">Bir tarayıcıda görünen dize dizisi kodunun çıkışı:</span><span class="sxs-lookup"><span data-stu-id="d0141-481">The output of the string array code displayed in a browser:</span></span>

![Razor-Img13](introducing-razor-syntax-c/_static/image13.jpg)

<span data-ttu-id="d0141-483">Sözlük, anahtar/değer çiftleri koleksiyonudur ve buna karşılık gelen değeri ayarlamak ya da almak için anahtarı (veya adı) sağlarsınız:</span><span class="sxs-lookup"><span data-stu-id="d0141-483">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample61.cshtml)]

<span data-ttu-id="d0141-484">Sözlük oluşturmak için, `new` anahtar sözcüğünü kullanarak yeni bir sözlük nesnesi kullandığınızı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-484">To create a dictionary, you use the `new` keyword to indicate that you're creating a new dictionary object.</span></span> <span data-ttu-id="d0141-485">`var` anahtar sözcüğünü kullanarak bir değişkene bir sözlük atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-485">You can assign a dictionary to a variable using the `var` keyword.</span></span> <span data-ttu-id="d0141-486">Sözlükteki öğelerin veri türlerini köşeli ayraç (`< >`) kullanarak gösterebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-486">You indicate the data types of the items in the dictionary using angle brackets ( `< >` ).</span></span> <span data-ttu-id="d0141-487">Bildirimin sonunda, bu gerçekte yeni bir sözlük oluşturan bir yöntem olduğundan, parantez çifti eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0141-487">At the end of the declaration, you must add a pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="d0141-488">Sözlüğe öğe eklemek için, sözlük değişkeninin (Bu durumda`myScores`) `Add` yöntemini çağırabilir ve sonra bir anahtar ve bir değer belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-488">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="d0141-489">Alternatif olarak, aşağıdaki örnekte olduğu gibi anahtarı göstermek ve basit bir atama yapmak için köşeli ayraçları kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d0141-489">Alternatively, you can use square brackets to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample62.cs)]

<span data-ttu-id="d0141-490">Sözlükten bir değer almak için anahtarı köşeli ayraç içinde belirtirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d0141-490">To get a value from the dictionary, you specify the key in brackets:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample63.cs)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="d0141-491">Yöntemler parametrelerle çağırma</span><span class="sxs-lookup"><span data-stu-id="d0141-491">Calling Methods with Parameters</span></span>

<span data-ttu-id="d0141-492">Bu makalede daha önce okuduğunuzdan, ile programlarındaki nesneler yöntemlere sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="d0141-492">As you read earlier in this article, the objects that you program with can have methods.</span></span> <span data-ttu-id="d0141-493">Örneğin, bir `Database` nesnesi bir `Database.Connect` yöntemine sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="d0141-493">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="d0141-494">Birçok yöntemde de bir veya daha fazla parametre vardır.</span><span class="sxs-lookup"><span data-stu-id="d0141-494">Many methods also have one or more parameters.</span></span> <span data-ttu-id="d0141-495">*Parametresi* , bir yöntemine geçirdiğiniz bir değerdir ve bu yöntem, görevini tamamlamaya yönelik yöntemi etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="d0141-495">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="d0141-496">Örneğin, üç parametre alan `Request.MapPath` yöntemi için bir bildirime bakın:</span><span class="sxs-lookup"><span data-stu-id="d0141-496">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample64.cs)]

<span data-ttu-id="d0141-497">(Satır daha okunabilir hale getirmek için sarmalanmış.</span><span class="sxs-lookup"><span data-stu-id="d0141-497">(The line has been wrapped to make it more readable.</span></span> <span data-ttu-id="d0141-498">Satır sonlarını, tırnak işaretleri içine alınan dizeler hariç neredeyse her bir yere koyabildiğiniz unutulmamalıdır.)</span><span class="sxs-lookup"><span data-stu-id="d0141-498">Remember that you can put line breaks almost any place except inside strings that are enclosed in quotation marks.)</span></span>

<span data-ttu-id="d0141-499">Bu yöntem, belirtilen sanal yola karşılık gelen sunucudaki fiziksel yolu döndürür.</span><span class="sxs-lookup"><span data-stu-id="d0141-499">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="d0141-500">Yöntemi için üç parametre `virtualPath`, `baseVirtualDir`ve `allowCrossAppMapping`.</span><span class="sxs-lookup"><span data-stu-id="d0141-500">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="d0141-501">(Bildiriminde, parametrelerin kabul edeceği verilerin veri türleriyle listelendiğine dikkat edin.) Bu yöntemi çağırdığınızda, üç parametrenin de değerlerini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0141-501">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="d0141-502">Razor söz dizimi, parametreleri bir yönteme geçirmek için kullanabileceğiniz iki seçenek sunar: *Konumsal parametreler* ve *adlandırılmış parametreler*.</span><span class="sxs-lookup"><span data-stu-id="d0141-502">The Razor syntax gives you two options for passing parameters to a method: *positional parameters* and *named parameters*.</span></span> <span data-ttu-id="d0141-503">Konumsal parametreleri kullanarak bir yöntemi çağırmak için, parametreleri yöntem bildiriminde belirtilen katı bir sıraya geçirin.</span><span class="sxs-lookup"><span data-stu-id="d0141-503">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="d0141-504">(Bu sırayı genellikle yöntemi için belgeleri okuyarak bilirsiniz.) Sırayı izlemeniz gerekir ve gerekirse parametrelerden &#8212; hiçbirini atlayamazsınız, bir değeri olmayan bir Konumsal parametre için boş bir dize (`""`) veya `null` geçirin.</span><span class="sxs-lookup"><span data-stu-id="d0141-504">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or `null` for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="d0141-505">Aşağıdaki örnek, Web sitenizde *betikler* adında bir klasörünüz olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="d0141-505">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="d0141-506">Kod `Request.MapPath` yöntemini çağırır ve üç parametrenin değerlerini doğru sırada geçirir.</span><span class="sxs-lookup"><span data-stu-id="d0141-506">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="d0141-507">Ardından, sonuçta elde edilen eşleştirilmiş yolu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d0141-507">It then displays the resulting mapped path.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample65.cshtml)]

<span data-ttu-id="d0141-508">Bir yöntemin çok sayıda parametresi olduğunda, adlandırılmış parametreleri kullanarak kodunuzun daha okunabilir olmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-508">When a method has many parameters, you can keep your code more readable by using named parameters.</span></span> <span data-ttu-id="d0141-509">Adlandırılmış parametreleri kullanarak bir yöntemi çağırmak için parametre adının ardından iki nokta üst üste (:) ve ardından değeri belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-509">To call a method using named parameters, you specify the parameter name followed by a colon (:), and then the value.</span></span> <span data-ttu-id="d0141-510">Adlandırılmış parametrelerin avantajı, bunları istediğiniz sırada geçirebilmeniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-510">The advantage of named parameters is that you can pass them in any order you want.</span></span> <span data-ttu-id="d0141-511">(Bir dezavantajı yöntem çağrısının sıkışık olmaması.)</span><span class="sxs-lookup"><span data-stu-id="d0141-511">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="d0141-512">Aşağıdaki örnek, yukarıdaki gibi aynı yöntemi çağırır, ancak değerleri sağlamak için adlandırılmış parametreleri kullanır:</span><span class="sxs-lookup"><span data-stu-id="d0141-512">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample66.cshtml)]

<span data-ttu-id="d0141-513">Görebileceğiniz gibi, parametreler farklı bir sırayla geçirilir.</span><span class="sxs-lookup"><span data-stu-id="d0141-513">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="d0141-514">Ancak, önceki örneği çalıştırırsanız ve bu örnekte, aynı değer döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d0141-514">However, if you run the previous example and this example, they'll return the same value.</span></span>

<a id="ID_HandlingErrors"></a>
## <a name="handling-errors"></a><span data-ttu-id="d0141-515">Hataları İşleme</span><span class="sxs-lookup"><span data-stu-id="d0141-515">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="d0141-516">Try-catch deyimleri</span><span class="sxs-lookup"><span data-stu-id="d0141-516">Try-Catch Statements</span></span>

<span data-ttu-id="d0141-517">Kodunuzda, denetiminizin dışındaki nedenlerle başarısız olabilecek deyimler vardır.</span><span class="sxs-lookup"><span data-stu-id="d0141-517">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="d0141-518">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d0141-518">For example:</span></span>

- <span data-ttu-id="d0141-519">Kodunuz bir dosya oluşturmayı veya bir dosyayı erişmeyi denediğinde, tüm hata sıralamaları meydana gelebilir.</span><span class="sxs-lookup"><span data-stu-id="d0141-519">If your code tries to create or access a file, all sorts of errors might occur.</span></span> <span data-ttu-id="d0141-520">İstediğiniz dosya mevcut olmayabilir, kilitli olabilir, kod izinlere sahip olmayabilir ve bu şekilde devam eder.</span><span class="sxs-lookup"><span data-stu-id="d0141-520">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="d0141-521">Benzer şekilde, kodunuz bir veritabanındaki kayıtları güncelleştirmeye çalışırsa, izin sorunları olabilir, veritabanı bağlantısı bırakılmış olabilir, kaydedilecek veriler geçersiz olabilir ve bu şekilde devam eder.</span><span class="sxs-lookup"><span data-stu-id="d0141-521">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="d0141-522">Programlama koşullarında, bu durumlara *özel durumlar*denir.</span><span class="sxs-lookup"><span data-stu-id="d0141-522">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="d0141-523">Kodunuz bir özel durumla karşılaşırsa, en iyi şekilde kullanıcılara sinir bozucu bir hata iletisi üretir (atar):</span><span class="sxs-lookup"><span data-stu-id="d0141-523">If your code encounters an exception, it generates (throws) an error message that's, at best, annoying to users:</span></span>

![Razor-Img14](introducing-razor-syntax-c/_static/image14.jpg)

<span data-ttu-id="d0141-525">Kodunuzun özel durumlarla karşılaşmasına ve bu türden hata iletilerinden kaçınmak için `try/catch` deyimlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-525">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `try/catch` statements.</span></span> <span data-ttu-id="d0141-526">`try` bildiriminde, kontrol ettiğiniz kodu çalıştırırsınız.</span><span class="sxs-lookup"><span data-stu-id="d0141-526">In the `try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="d0141-527">Bir veya daha fazla `catch` deyiminde, oluşmuş olabilecek belirli hatalara (özel durum türleri) bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-527">In one or more `catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="d0141-528">Benimsemeyi bekleme olduğunuz hatalara bakmak için gereken sayıda `catch` deyimi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0141-528">You can include as many `catch` statements as you need to look for errors that you are anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="d0141-529">`try/catch` deyimlerde `Response.Redirect` yöntemini kullanmaktan kaçınmanızı öneririz, çünkü sayfanızda bir özel duruma neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="d0141-529">We recommend that you avoid using the `Response.Redirect` method in `try/catch` statements, because it can cause an exception in your page.</span></span>

<span data-ttu-id="d0141-530">Aşağıdaki örnek, ilk istekte bir metin dosyası oluşturan ve sonra kullanıcının dosyayı açmasına olanak tanıyan bir düğme görüntüleyen bir sayfa gösterir.</span><span class="sxs-lookup"><span data-stu-id="d0141-530">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="d0141-531">Örnek, bir özel duruma neden olacak şekilde hatalı bir dosya adı kullanır.</span><span class="sxs-lookup"><span data-stu-id="d0141-531">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="d0141-532">Kod, olası iki özel durum için `catch` deyimlerini içerir: dosya adı bozuksa oluşan `FileNotFoundException`ve ASP.NET bile klasörü bulamazsa oluşan `DirectoryNotFoundException`.</span><span class="sxs-lookup"><span data-stu-id="d0141-532">The code includes `catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="d0141-533">(Her şey düzgün şekilde çalıştığında nasıl çalıştığını görmek için örnekteki bir deyimin açıklamasını değiştirebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="d0141-533">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="d0141-534">Kodunuz özel durumu işlemediyse, önceki ekran görüntüsündeki gibi bir hata sayfası görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d0141-534">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="d0141-535">Ancak, `try/catch` bölümü kullanıcının bu hata türlerini görmesini önlemeye yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d0141-535">However, the `try/catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample67.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="d0141-536">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d0141-536">Additional Resources</span></span>

<span data-ttu-id="d0141-537">**Visual Basic ile programlama**</span><span class="sxs-lookup"><span data-stu-id="d0141-537">**Programming with Visual Basic**</span></span>

[<span data-ttu-id="d0141-538">Ek: Visual Basic dil ve sözdizimi</span><span class="sxs-lookup"><span data-stu-id="d0141-538">Appendix: Visual Basic Language and Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkId=202908)

<span data-ttu-id="d0141-539">**Başvuru Belgeleri**</span><span class="sxs-lookup"><span data-stu-id="d0141-539">**Reference Documentation**</span></span>

[<span data-ttu-id="d0141-540">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d0141-540">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)

[<span data-ttu-id="d0141-541">C#Dildir</span><span class="sxs-lookup"><span data-stu-id="d0141-541">C# Language</span></span>](https://msdn.microsoft.com/library/kx37x362.aspx)
