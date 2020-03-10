---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: Dinamik güncelleştirmeleri sunmak için AJAX kullanma | Microsoft Docs
author: microsoft
description: 10. adım, oturum açan kullanıcıların, akşam yemeği ayrıntısı dahilinde tümleşik bir Ajax tabanlı yaklaşım kullanarak bir akşam yemeği ile ilgilendikleri konusunda bilgi almak için destek uygular...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 3edc02fec546609505b5e085440fa684abe7acd0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600851"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a><span data-ttu-id="d1390-103">AJAX Kullanarak Dinamik Güncelleştirmeler Sunma</span><span class="sxs-lookup"><span data-stu-id="d1390-103">Use AJAX to Deliver Dynamic Updates</span></span>

<span data-ttu-id="d1390-104">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="d1390-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="d1390-105">PDF 'YI indir</span><span class="sxs-lookup"><span data-stu-id="d1390-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="d1390-106">Bu, ASP.NET MVC 1 kullanarak küçük, ancak tam bir Web uygulamasının nasıl oluşturulacağını gösteren ücretsiz bir ["Nerdakşam yemeği" uygulama öğreticisinin](introducing-the-nerddinner-tutorial.md) adım 10 ' dur.</span><span class="sxs-lookup"><span data-stu-id="d1390-106">This is step 10 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="d1390-107">10. adım, oturum açan kullanıcıların, akşam yemeği ayrıntıları sayfasında tümleştirilmiş Ajax tabanlı bir yaklaşım kullanarak bir akşam yemeği ile ilgilenmek için destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="d1390-107">Step 10 implements support for logged-in users to RSVP their interest in attending a dinner, using an Ajax-based approach integrated within the dinner details page.</span></span>
> 
> <span data-ttu-id="d1390-108">ASP.NET MVC 3 kullanıyorsanız, [MVC 3 Ile çalışmaya başlama](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC müzik mağazası](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) öğreticilerini izlemeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="d1390-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a><span data-ttu-id="d1390-109">Nerdakşam yemeği adım 10: AJAX etkinleştirme RSVPs kabul eder</span><span class="sxs-lookup"><span data-stu-id="d1390-109">NerdDinner Step 10: AJAX Enabling RSVPs Accepts</span></span>

<span data-ttu-id="d1390-110">Şimdi, oturum açan kullanıcılar için bir akşam yemeği ile ilgilendikleri için destek uygulayalim.</span><span class="sxs-lookup"><span data-stu-id="d1390-110">Let's now implement support for logged-in users to RSVP their interest in attending a dinner.</span></span> <span data-ttu-id="d1390-111">Bunu, akşam yemeği ayrıntıları sayfasında tümleştirilmiş bir AJAX tabanlı yaklaşım kullanarak etkinleştireceğiz.</span><span class="sxs-lookup"><span data-stu-id="d1390-111">We'll enable this using an AJAX-based approach integrated within the dinner details page.</span></span>

### <a name="indicating-whether-the-user-is-rsvpd"></a><span data-ttu-id="d1390-112">Kullanıcının RSVP olup olmadığını belirtir</span><span class="sxs-lookup"><span data-stu-id="d1390-112">Indicating whether the user is RSVP'd</span></span>

<span data-ttu-id="d1390-113">Kullanıcılar, belirli bir akşam yemeği hakkındaki ayrıntıları görmek için */Dinners/details/[ID*] URL 'sini ziyaret edebilir:</span><span class="sxs-lookup"><span data-stu-id="d1390-113">Users can visit the */Dinners/Details/[id*] URL to see details about a particular dinner:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

<span data-ttu-id="d1390-114">Ayrıntılar () eylem yöntemi şöyle uygulanır:</span><span class="sxs-lookup"><span data-stu-id="d1390-114">The Details() action method is implemented like so:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

<span data-ttu-id="d1390-115">RSVP desteğini uygulamaya yönelik ilk adımımız, akşam yemeği nesnemiz için bir "ıkullanıcıkayıtlı (Kullanıcı adı)" yardımcı yöntemi eklemektir (daha önce oluşturduğumuz Dinner.cs kısmi sınıfı içinde).</span><span class="sxs-lookup"><span data-stu-id="d1390-115">Our first step to implement RSVP support will be to add an "IsUserRegistered(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="d1390-116">Bu yardımcı yöntem, kullanıcının akşam yemeği için geçerli olup olmadığına bağlı olarak true veya false değerini döndürür:</span><span class="sxs-lookup"><span data-stu-id="d1390-116">This helper method returns true or false depending on whether the user is currently RSVP'd for the Dinner:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

<span data-ttu-id="d1390-117">Daha sonra, kullanıcının kaydedilip edilmeyeceğini belirten uygun bir ileti görüntülemek için details. aspx görünüm şablonumuza aşağıdaki kodu ekleyebiliriz:</span><span class="sxs-lookup"><span data-stu-id="d1390-117">We can then add the following code to our Details.aspx view template to display an appropriate message indicating whether the user is registered or not for the event:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

<span data-ttu-id="d1390-118">Şimdi de bir Kullanıcı akşam yemeği ziyaret ettiğinde şu iletiyi görür:</span><span class="sxs-lookup"><span data-stu-id="d1390-118">And now when a user visits a Dinner they are registered for they'll see this message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

<span data-ttu-id="d1390-119">Bir akşam yemeği ziyaret ettiğinde, bu kişiler için kayıtlı değildir ve şu iletiyi görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="d1390-119">And when they visit a Dinner they are not registered for they'll see the below message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a><span data-ttu-id="d1390-120">Register ACTION metodunu uygulama</span><span class="sxs-lookup"><span data-stu-id="d1390-120">Implementing the Register Action Method</span></span>

<span data-ttu-id="d1390-121">Şimdi, Ayrıntılar sayfasından kullanıcıların bir akşam yemeği için RSVP 'e yanıt vermek üzere gerekli işlevselliği ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="d1390-121">Let's now add the functionality necessary to enable users to RSVP for a dinner from the details page.</span></span>

<span data-ttu-id="d1390-122">Bunu uygulamak için, \Controllers dizinine sağ tıklayıp add-&gt;Controller menü komutunu seçerek yeni bir "RSVPController" sınıfı oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="d1390-122">To implement this, we'll create a new "RSVPController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span>

<span data-ttu-id="d1390-123">Bağımsız değişken olarak akşam yemeği için bir kimlik alan yeni RSVPController sınıfında bir "Register" eylem yöntemi uygulayacağız, uygun akşam yemeği nesnesini alır, oturum açan kullanıcının o anda kendisi için Kaydolmakta olup olmadığını denetler ve Bunlar için bir RSVP nesnesi eklememez:</span><span class="sxs-lookup"><span data-stu-id="d1390-123">We'll implement a "Register" action method within the new RSVPController class that takes an id for a Dinner as an argument, retrieves the appropriate Dinner object, checks to see if the logged-in user is currently in the list of users who have registered for it, and if not adds an RSVP object for them:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

<span data-ttu-id="d1390-124">Eylem yönteminin çıktısı olarak nasıl basit bir dize döndüyoruz hakkında bildirim.</span><span class="sxs-lookup"><span data-stu-id="d1390-124">Notice above how we are returning a simple string as the output of the action method.</span></span> <span data-ttu-id="d1390-125">Bu iletiyi bir görünüm şablonu içinde katıştırıyoruz, ancak bu nedenle küçük olduğundan, denetleyici temel sınıfında Content () yardımcı yöntemini kullanacağız ve yukarıdaki gibi bir dize iletisi döndürdük.</span><span class="sxs-lookup"><span data-stu-id="d1390-125">We could have embedded this message within a view template – but since it is so small we'll just use the Content() helper method on the controller base class and return a string message like above.</span></span>

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a><span data-ttu-id="d1390-126">AJAX kullanarak RSVPForEvent eylem yöntemini çağırma</span><span class="sxs-lookup"><span data-stu-id="d1390-126">Calling the RSVPForEvent Action Method using AJAX</span></span>

<span data-ttu-id="d1390-127">AJAX ' i, Ayrıntılar görünümümüzde kaydetme eylemi yöntemini çağırmak için kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="d1390-127">We'll use AJAX to invoke the Register action method from our Details view.</span></span> <span data-ttu-id="d1390-128">Bunu uygulamak oldukça kolaydır.</span><span class="sxs-lookup"><span data-stu-id="d1390-128">Implementing this is pretty easy.</span></span> <span data-ttu-id="d1390-129">İlk olarak iki betik kitaplığı başvurusu ekleyeceğiz:</span><span class="sxs-lookup"><span data-stu-id="d1390-129">First we'll add two script library references:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

<span data-ttu-id="d1390-130">İlk kitaplık, çekirdek ASP.NET AJAX istemci tarafı komut dosyası kitaplığına başvurur.</span><span class="sxs-lookup"><span data-stu-id="d1390-130">The first library references the core ASP.NET AJAX client-side script library.</span></span> <span data-ttu-id="d1390-131">Bu dosya yaklaşık 24k boyutunda (sıkıştırılmış) ve çekirdek istemci tarafı AJAX işlevleri içerir.</span><span class="sxs-lookup"><span data-stu-id="d1390-131">This file is approximately 24k in size (compressed) and contains core client-side AJAX functionality.</span></span> <span data-ttu-id="d1390-132">İkinci kitaplık, ASP.NET MVC 'nin yerleşik AJAX Yardımcısı yöntemleriyle (kısa süre içinde kullanacağız) tümleştirilen yardımcı program işlevlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="d1390-132">The second library contains utility functions that integrate with ASP.NET MVC's built-in AJAX helper methods (which we'll use shortly).</span></span>

<span data-ttu-id="d1390-133">Daha sonra, daha önce eklediğimiz görünüm şablonu kodunu, "Bu olay için kaydolmadıysanız" iletisini almak yerine daha sonra güncelleştirebiliriz. bunun yerine, gönderildiğinde, RSVP denetleyicimizde RSVPForEvent eylem yöntemini çağıran bir AJAX çağrısı gerçekleştirdiğinde bir bağlantı oluşturuyoruz RSVPs ve Kullanıcı:</span><span class="sxs-lookup"><span data-stu-id="d1390-133">We can then update the view template code we added earlier so that instead of outputting a "You are not registered for this event" message, we instead render a link that when pushed performs an AJAX call that invokes our RSVPForEvent action method on our RSVP controller and RSVPs the user:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

<span data-ttu-id="d1390-134">Yukarıda kullanılan Ajax. ActionLink () yardımcı yöntemi yerleşik ASP.NET MVC 'dir ve HTML. ActionLink () yardımcı yöntemine benzer ve standart bir gezinti gerçekleştirmek yerine, bağlantı tıklandığında eylem yöntemine bir AJAX çağrısı yapar.</span><span class="sxs-lookup"><span data-stu-id="d1390-134">The Ajax.ActionLink() helper method used above is built-into ASP.NET MVC and is similar to the Html.ActionLink() helper method except that instead of performing a standard navigation it makes an AJAX call to the action method when the link is clicked.</span></span> <span data-ttu-id="d1390-135">Yukarıdaki "RSVP" denetleyicisindeki "Register" eylem yöntemini çağırıyoruz ve DinnerID ' i "ID" parametresi olarak geçiririz.</span><span class="sxs-lookup"><span data-stu-id="d1390-135">Above we are calling the "Register" action method on the "RSVP" controller and passing the DinnerID as the "id" parameter to it.</span></span> <span data-ttu-id="d1390-136">Geçirdiğimiz son AjaxOptions parametresi, eylem yönteminden döndürülen içeriği almak ve kimliği "rsvpmsg" olan sayfada HTML &lt;div&gt; öğesini güncelleştirmek istediğimiz olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="d1390-136">The final AjaxOptions parameter we are passing indicates that we want to take the content returned from the action method and update the HTML &lt;div&gt; element on the page whose id is "rsvpmsg".</span></span>

<span data-ttu-id="d1390-137">Şimdi de bir Kullanıcı bir akşam yemeği 'ye gözattığında, bunun için bir RSVP bağlantısı görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="d1390-137">And now when a user browses to a dinner they aren't registered for yet they'll see a link to RSVP for it:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

<span data-ttu-id="d1390-138">"Bu olaya yönelik RSVP" bağlantısını tıkladıklarında, RSVP denetleyicisindeki kayıt eylemi yöntemine bir AJAX çağrısı yapar ve tamamlandığında aşağıdaki gibi güncelleştirilmiş bir ileti görür:</span><span class="sxs-lookup"><span data-stu-id="d1390-138">If they click the "RSVP for this event" link they'll make an AJAX call to the Register action method on the RSVP controller, and when it completes they'll see an updated message like below:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

<span data-ttu-id="d1390-139">Bu AJAX çağrısını yapmak için kullanılan ağ bant genişliği ve trafik gerçekten hafif.</span><span class="sxs-lookup"><span data-stu-id="d1390-139">The network bandwidth and traffic involved when making this AJAX call is really lightweight.</span></span> <span data-ttu-id="d1390-140">Kullanıcı "Bu olaya yönelik RSVP" bağlantısı üzerine tıkladığında, */Dinners/Register/1* URL 'sine şu şekilde BIR küçük http post ağı isteği yapılır:</span><span class="sxs-lookup"><span data-stu-id="d1390-140">When the user clicks on the "RSVP for this event" link, a small HTTP POST network request is made to the */Dinners/Register/1* URL that looks like below on the wire:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

<span data-ttu-id="d1390-141">Kayıt eylemi yönteminizin yanıtı yalnızca şu şekilde yapılır:</span><span class="sxs-lookup"><span data-stu-id="d1390-141">And the response from our Register action method is simply:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

<span data-ttu-id="d1390-142">Bu hafif çağrı hızlıdır ve yavaş bir ağ üzerinden bile çalışacaktır.</span><span class="sxs-lookup"><span data-stu-id="d1390-142">This lightweight call is fast and will work even over a slow network.</span></span>

### <a name="adding-a-jquery-animation"></a><span data-ttu-id="d1390-143">JQuery animasyonu ekleme</span><span class="sxs-lookup"><span data-stu-id="d1390-143">Adding a jQuery Animation</span></span>

<span data-ttu-id="d1390-144">Uyguladığımız AJAX işlevleri iyi ve hızlı bir şekilde çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d1390-144">The AJAX functionality we implemented works well and fast.</span></span> <span data-ttu-id="d1390-145">Bazen hızlı bir şekilde gerçekleşebilir, ancak Kullanıcı RSVP bağlantısının yeni metinle değiştirildiğini fark edemeyebilir.</span><span class="sxs-lookup"><span data-stu-id="d1390-145">Sometimes it can happen so fast, though, that a user might not notice that the RSVP link has been replaced with new text.</span></span> <span data-ttu-id="d1390-146">Sonucu daha belirgin hale getirmek için, güncelleştirme iletisine dikkat çekmek üzere basit bir animasyon ekleyebiliriz.</span><span class="sxs-lookup"><span data-stu-id="d1390-146">To make the outcome a little more obvious we can add a simple animation to draw attention to the update message.</span></span>

<span data-ttu-id="d1390-147">Varsayılan ASP.NET MVC proje şablonu, Microsoft tarafından da desteklenen jQuery: mükemmel (ve çok popüler) açık kaynaklı JavaScript kitaplığı içerir.</span><span class="sxs-lookup"><span data-stu-id="d1390-147">The default ASP.NET MVC project template includes jQuery – an excellent (and very popular) open source JavaScript library that is also supported by Microsoft.</span></span> <span data-ttu-id="d1390-148">jQuery, iyi bir HTML DOM seçimi ve efektler kitaplığı dahil olmak üzere çeşitli özellikler sağlar.</span><span class="sxs-lookup"><span data-stu-id="d1390-148">jQuery provides a number of features, including a nice HTML DOM selection and effects library.</span></span>

<span data-ttu-id="d1390-149">JQuery kullanmak için önce buna bir betik başvurusu ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="d1390-149">To use jQuery we'll first add a script reference to it.</span></span> <span data-ttu-id="d1390-150">Sitemizdeki çeşitli konumlarda jQuery kullanacağınızı öğrendiğimiz için, tüm sayfaların onu kullanabilmesi için, site. Master ana sayfa dosyası içinde betik başvurusunu ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="d1390-150">Because we are going to be using jQuery within a variety of places within our site, we'll add the script reference within our Site.master master page file so that all pages can use it.</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

<span data-ttu-id="d1390-151">*İpucu: JavaScript dosyaları için daha zengin IntelliSense desteğini sağlayan VS 2008 SP1 için JavaScript IntelliSense düzeltmesini (jQuery dahil) yüklediğinizden emin olun. Buradan indirebilirsiniz: http://tinyurl.com/vs2008javascripthotfix*</span><span class="sxs-lookup"><span data-stu-id="d1390-151">*Tip: make sure you have installed the JavaScript intellisense hotfix for VS 2008 SP1 that enables richer intellisense support for JavaScript files (including jQuery). You can download it from: http://tinyurl.com/vs2008javascripthotfix*</span></span>

<span data-ttu-id="d1390-152">JQuery kullanılarak yazılan kod genellikle CSS seçiciyi kullanarak bir veya daha fazla HTML öğesi alan Global "$ ()" JavaScript yöntemini kullanır.</span><span class="sxs-lookup"><span data-stu-id="d1390-152">Code written using JQuery often uses a global "$()" JavaScript method that retrieves one or more HTML elements using a CSS selector.</span></span> <span data-ttu-id="d1390-153">Örneğin, *$ ("#rsvpmsg")* , rsvpmsg kimliğine sahip HERHANGI bir HTML öğesini seçer, ancak *$ (". bir")* , "bir" CSS sınıfı adı olan tüm öğeleri seçer.</span><span class="sxs-lookup"><span data-stu-id="d1390-153">For example, *$("#rsvpmsg")* selects any HTML element with the id of rsvpmsg, while *$(".something")* would select all elements with the "something" CSS class name.</span></span> <span data-ttu-id="d1390-154">Ayrıca, "işaretlenmiş radyo düğmelerinin tümünü Döndür" gibi daha gelişmiş sorgular da yazabilirsiniz: *$ ("input [@type= Radio] [@checked]")* .</span><span class="sxs-lookup"><span data-stu-id="d1390-154">You can also write more advanced queries like "return all of the checked radio buttons" using a selector query like: *$("input[@type=radio][@checked]")*.</span></span>

<span data-ttu-id="d1390-155">Öğeleri seçtikten sonra, bunları gizleme gibi eyleme geçmek için yöntemler çağırabilirsiniz: *$ ("#rsvpmsg"). Hide ();*</span><span class="sxs-lookup"><span data-stu-id="d1390-155">Once you've selected elements, you can call methods on them to take action, like hiding them: *$("#rsvpmsg").hide();*</span></span>

<span data-ttu-id="d1390-156">RSVP senaryomız için, "rsvpmsg" &lt;div&gt; seçen ve metin içeriğinin boyutunu canlandırmış olan "AnimateRSVPMessage" adlı basit bir JavaScript işlevi tanımlayacağız.</span><span class="sxs-lookup"><span data-stu-id="d1390-156">For our RSVP scenario, we'll define a simple JavaScript function named "AnimateRSVPMessage" that selects the "rsvpmsg" &lt;div&gt; and animates the size of its text content.</span></span> <span data-ttu-id="d1390-157">Aşağıdaki kod, metni küçük ve 400 milisaniyelik zaman diliminde artmasına neden olur:</span><span class="sxs-lookup"><span data-stu-id="d1390-157">The below code starts the text small and then causes it to increase over a 400 milliseconds timeframe:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

<span data-ttu-id="d1390-158">Daha sonra bu JavaScript işlevinin adı Ajax. ActionLink () yardımcı yöntemimize (AjaxOptions "OnSuccess" olay özelliği aracılığıyla) başarılı bir şekilde tamamlandıktan sonra, AJAX çağrımız başarıyla tamamlandıktan sonra çağrılabilir:</span><span class="sxs-lookup"><span data-stu-id="d1390-158">We can then wire-up this JavaScript function to be called after our AJAX call successfully completes by passing its name to our Ajax.ActionLink() helper method (via the AjaxOptions "OnSuccess" event property):</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

<span data-ttu-id="d1390-159">Artık "Bu olaya yönelik RSVP" bağlantısı tıklandığında ve AJAX çağrımız başarıyla tamamlanırsa, geri gönderilen içerik iletisi animasyon uygular ve büyük büyüyülecektir:</span><span class="sxs-lookup"><span data-stu-id="d1390-159">And now when the "RSVP for this event" link is clicked and our AJAX call completes successfully, the content message sent back will animate and grow large:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

<span data-ttu-id="d1390-160">"OnSuccess" olayı sağlamaya ek olarak, AjaxOptions nesnesi, işleyebileceğiniz Onbegın, OnFailure ve Ontamamlanmış olayları (diğer özellikler ve yararlı seçeneklerle birlikte) kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="d1390-160">In addition to providing an "OnSuccess" event, the AjaxOptions object exposes OnBegin, OnFailure, and OnComplete events that you can handle (along with a variety of other properties and useful options).</span></span>

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a><span data-ttu-id="d1390-161">Temizleme-bir RSVP kısmi görünümünü yeniden düzenleme</span><span class="sxs-lookup"><span data-stu-id="d1390-161">Cleanup - Refactor out a RSVP Partial View</span></span>

<span data-ttu-id="d1390-162">Ayrıntılar görünümü şablonu biraz uzun sürer, bu da fazla mesainin anlaşılması biraz daha zor hale gelir.</span><span class="sxs-lookup"><span data-stu-id="d1390-162">Our details view template is starting to get a little long, which overtime will make it a little harder to understand.</span></span> <span data-ttu-id="d1390-163">Kod okunabilirliğini artırmaya yardımcı olmak için, Ayrıntılar sayfamız için tüm RSVP görünüm kodunu kapsülleyen kısmi bir görünüm – RSVPStatus. ascx ' i oluşturarak bitelim.</span><span class="sxs-lookup"><span data-stu-id="d1390-163">To help improve the code readability, let's finish up by creating a partial view – RSVPStatus.ascx – that encapsulate all of the RSVP view code for our Details page.</span></span>

<span data-ttu-id="d1390-164">Bunu, \Views\dıntik klasörüne sağ tıklayıp ardından Ekle-&gt;görünümü menü komutunu seçerek yapabiliriz.</span><span class="sxs-lookup"><span data-stu-id="d1390-164">We can do this by right-clicking on the \Views\Dinners folder and then choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="d1390-165">Bir akşam yemeği nesnesini kesin belirlenmiş ViewModel olarak ele alacağız.</span><span class="sxs-lookup"><span data-stu-id="d1390-165">We'll have it take a Dinner object as its strongly-typed ViewModel.</span></span> <span data-ttu-id="d1390-166">Bundan sonra, details. aspx görünümümüzden gelir içeriğini kopyalayabilir/yapıştırabilir.</span><span class="sxs-lookup"><span data-stu-id="d1390-166">We can then copy/paste the RSVP content from our Details.aspx view into it.</span></span>

<span data-ttu-id="d1390-167">Bunu yaptıktan sonra, Düzenle ve Sil bağlantı görünümü kodumuzu kapsülleyen bir kısmi görünüm – EditAndDeleteLinks. ascx ' i de oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="d1390-167">Once we've done that, let's also create another partial view – EditAndDeleteLinks.ascx - that encapsulates our Edit and Delete link view code.</span></span> <span data-ttu-id="d1390-168">Ayrıca, bunu kesin belirlenmiş ViewModel olarak bir akşam yemeği nesnesi alacak ve details. aspx görünümümüzde düzenleme ve silme mantığını kopyalayacak/yapıştırıyoruz.</span><span class="sxs-lookup"><span data-stu-id="d1390-168">We'll also have it take a Dinner object as its strongly-typed ViewModel, and copy/paste the Edit and Delete logic from our Details.aspx view into it.</span></span>

<span data-ttu-id="d1390-169">Ayrıntılar görünümü şablonu, en alta yalnızca iki HTML. RenderPartial () yöntem çağrısı içerebilir:</span><span class="sxs-lookup"><span data-stu-id="d1390-169">Our details view template can then just include two Html.RenderPartial() method calls at the bottom:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

<span data-ttu-id="d1390-170">Bu, kod temizleyiciyi okumayı ve bakımını yapmayı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d1390-170">This makes the code cleaner to read and maintain.</span></span>

### <a name="next-step"></a><span data-ttu-id="d1390-171">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="d1390-171">Next Step</span></span>

<span data-ttu-id="d1390-172">Artık AJAX 'ı daha da nasıl kullanabileceğimizi ve uygulamamıza etkileşimli eşleme desteği eklemenizi inceleyelim.</span><span class="sxs-lookup"><span data-stu-id="d1390-172">Let's now look at how we can use AJAX even further and add interactive mapping support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d1390-173">[Önceki](secure-applications-using-authentication-and-authorization.md)
> [İleri](use-ajax-to-implement-mapping-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="d1390-173">[Previous](secure-applications-using-authentication-and-authorization.md)
[Next](use-ajax-to-implement-mapping-scenarios.md)</span></span>
