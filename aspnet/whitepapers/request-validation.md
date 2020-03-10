---
uid: whitepapers/request-validation
title: İstek doğrulaması-betik saldırılarını önler | Microsoft Docs
author: rick-anderson
description: Bu belgede, varsayılan olarak uygulamanın, kodlanmamış HTML içerik göndermesinin yerine, varsayılan olarak, ASP.NET ' nin istek doğrulama özelliği açıklanmaktadır...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: fa429113-5f8f-4ef4-97c5-5c04900a19fa
msc.legacyurl: /whitepapers/request-validation
msc.type: content
ms.openlocfilehash: 807cccd6fe1acdd6359b014387abd3878840d4cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640849"
---
# <a name="request-validation---preventing-script-attacks"></a><span data-ttu-id="7de32-103">İstek Doğrulama - Betik Saldırılarını Önleme</span><span class="sxs-lookup"><span data-stu-id="7de32-103">Request Validation - Preventing Script Attacks</span></span>

> <span data-ttu-id="7de32-104">Bu sayfa, varsayılan olarak uygulamanın sunucuya gönderilen kodlanmamış HTML içeriğini işlemesini engellediği ASP.NET 'in istek doğrulama özelliğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="7de32-104">This paper describes the request validation feature of ASP.NET where, by default, the application is prevented from processing unencoded HTML content submitted to the server.</span></span> <span data-ttu-id="7de32-105">Bu istek doğrulama özelliği, uygulama HTML verilerini güvenle işlemek üzere tasarlandıysa devre dışı bırakılabilir.</span><span class="sxs-lookup"><span data-stu-id="7de32-105">This request validation feature can be disabled when the application has been designed to safely process HTML data.</span></span>
> 
> <span data-ttu-id="7de32-106">ASP.NET 1,1 ve ASP.NET 2,0 için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="7de32-106">Applies to ASP.NET 1.1 and ASP.NET 2.0.</span></span>

<span data-ttu-id="7de32-107">Sürüm 1,1 ' den bu yana bir ASP.NET özelliği olan istek doğrulaması, sunucunun kodlanmamış HTML içeren içeriği kabul etmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="7de32-107">Request validation, a feature of ASP.NET since version 1.1, prevents the server from accepting content containing un-encoded HTML.</span></span> <span data-ttu-id="7de32-108">Bu özellik, istemci betik kodu veya HTML 'nin bir sunucuya geri gönderilebildiği, depolandığı ve daha sonra diğer kullanıcılara sunulabildiği bazı betik ekleme saldırılarını önlemeye yardımcı olmak için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="7de32-108">This feature is designed to help prevent some script-injection attacks whereby client script code or HTML can be unknowingly submitted to a server, stored, and then presented to other users.</span></span> <span data-ttu-id="7de32-109">Ayrıca, uygun olduğunda tüm giriş verilerini doğrulamanızı ve HTML 'in kodlanmasını kesinlikle öneririz.</span><span class="sxs-lookup"><span data-stu-id="7de32-109">We still strongly recommend that you validate all input data and HTML encode it when appropriate.</span></span>

<span data-ttu-id="7de32-110">Örneğin, bir kullanıcının e-posta adresini isteyen bir Web sayfası oluşturur ve bu e-posta adresini bir veritabanında depolar.</span><span class="sxs-lookup"><span data-stu-id="7de32-110">For example, you create a Web page that requests a user's email address and then stores that email address in a database.</span></span> <span data-ttu-id="7de32-111">Kullanıcı, geçerli bir e-posta adresi yerine bir &lt;komut dosyası&gt;Uyarısı ("betikten Merhaba") girerse&lt;/SCRIPT&gt;, bu veriler sunulursa, içerik düzgün şekilde kodlanmışsa bu betik yürütülebilir.</span><span class="sxs-lookup"><span data-stu-id="7de32-111">If the user enters &lt;SCRIPT&gt;alert("hello from script")&lt;/SCRIPT&gt; instead of a valid email address, when that data is presented, this script can be executed if the content was not properly encoded.</span></span> <span data-ttu-id="7de32-112">ASP.NET öğesinin istek doğrulama özelliği, bunun oluşmasını engeller.</span><span class="sxs-lookup"><span data-stu-id="7de32-112">The request validation feature of ASP.NET prevents this from happening.</span></span>

## <a name="why-this-feature-is-useful"></a><span data-ttu-id="7de32-113">Bu özelliğin neden yararlı olduğu</span><span class="sxs-lookup"><span data-stu-id="7de32-113">Why this feature is useful</span></span>

<span data-ttu-id="7de32-114">Birçok site basit betik ekleme saldırılarına açık olduğunu bilmez.</span><span class="sxs-lookup"><span data-stu-id="7de32-114">Many sites are not aware that they are open to simple script injection attacks.</span></span> <span data-ttu-id="7de32-115">Bu saldırıların amacı, HTML 'yi görüntüleyerek siteyi erteleyerek veya kullanıcıyı bir korsanın sitesine yönlendirmek için büyük olasılıkla istemci komut dosyasını yürütmeye yönelik bir sorun olsun, komut dosyası ekleme saldırıları Web geliştiricilerinin ile devam etmelidir.</span><span class="sxs-lookup"><span data-stu-id="7de32-115">Whether the purpose of these attacks is to deface the site by displaying HTML, or to potentially execute client script to redirect the user to a hacker's site, script injection attacks are a problem that Web developers must contend with.</span></span>

<span data-ttu-id="7de32-116">Betik ekleme saldırıları, ASP.NET, ASP veya diğer web geliştirme teknolojileri kullanıp kullandıklarından bağımsız olarak tüm Web geliştiricilerinin bir kaygıdır.</span><span class="sxs-lookup"><span data-stu-id="7de32-116">Script injection attacks are a concern of all web developers, whether they are using ASP.NET, ASP, or other web development technologies.</span></span>

<span data-ttu-id="7de32-117">ASP.NET istek doğrulama özelliği, geliştirici bu içeriğe izin vermeye karar vermediği takdirde, bu saldırıların, kodlanamayan HTML içeriğinin sunucu tarafından işlenmesine izin vermez.</span><span class="sxs-lookup"><span data-stu-id="7de32-117">The ASP.NET request validation feature proactively prevents these attacks by not allowing unencoded HTML content to be processed by the server unless the developer decides to allow that content.</span></span>

## <a name="what-to-expect-error-page"></a><span data-ttu-id="7de32-118">Bekleneceğiniz: hata sayfası</span><span class="sxs-lookup"><span data-stu-id="7de32-118">What to expect: Error Page</span></span>

<span data-ttu-id="7de32-119">Aşağıdaki ekran görüntüsünde örnek ASP.NET kodu gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="7de32-119">The screen shot below shows some sample ASP.NET code:</span></span>

![](request-validation/_static/image1.png)

<span data-ttu-id="7de32-120">Bu kodun çalıştırılması, metin kutusuna bir metin girmenize izin veren basit bir sayfa ile sonuçlanır, düğmeye tıklayın ve metni etiket denetiminde görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7de32-120">Running this code results in a simple page that allows you to enter some text in the textbox, click the button, and display the text in the label control:</span></span>

![](request-validation/_static/image2.png)

<span data-ttu-id="7de32-121">Ancak, girilecek ve gönderilecek `<script>alert("hello!")</script>` özel bir durum alırız gibi JavaScript vardı:</span><span class="sxs-lookup"><span data-stu-id="7de32-121">However, were JavaScript, such as `<script>alert("hello!")</script>` to be entered and submitted we would get an exception:</span></span>

![](request-validation/_static/image3.png)

<span data-ttu-id="7de32-122">Hata iletisinde ' potansiyel olarak tehlikeli bir Istek. form değeri algılandı ' belirtilir ve açıklamada tam olarak ne olduğu ve davranışın nasıl değiştirileceği hakkında daha fazla ayrıntı sağlar.</span><span class="sxs-lookup"><span data-stu-id="7de32-122">The error message states that a 'potentially dangerous Request.Form value was detected' and provides more details in the description as to exactly what occurred and how to change the behavior.</span></span> <span data-ttu-id="7de32-123">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="7de32-123">For example:</span></span>

<span data-ttu-id="7de32-124">İstek doğrulaması potansiyel olarak tehlikeli bir istemci giriş değeri algıladı ve isteğin işlenmesi durduruldu.</span><span class="sxs-lookup"><span data-stu-id="7de32-124">Request validation has detected a potentially dangerous client input value, and processing of the request has been aborted.</span></span> <span data-ttu-id="7de32-125">Bu değer, bir siteler arası betik saldırısı gibi uygulamanızın güvenliğini tehlikeye atabilir.</span><span class="sxs-lookup"><span data-stu-id="7de32-125">This value may indicate an attempt to compromise the security of your application, such as a cross-site scripting attack.</span></span> <span data-ttu-id="7de32-126">Sayfa yönergesinde veya yapılandırma bölümünde `validateRequest=false` ayarlayarak istek doğrulamayı devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7de32-126">You can disable request validation by setting `validateRequest=false` in the Page directive or in the configuration section.</span></span> <span data-ttu-id="7de32-127">Ancak, uygulamanızın bu durumda tüm girdileri açıkça denetlemesi önemle önerilir.</span><span class="sxs-lookup"><span data-stu-id="7de32-127">However, it is strongly recommended that your application explicitly check all inputs in this case.</span></span>

## <a name="disabling-request-validation-on-a-page"></a><span data-ttu-id="7de32-128">Sayfada istek doğrulamayı devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="7de32-128">Disabling request validation on a page</span></span>

<span data-ttu-id="7de32-129">Bir sayfada istek doğrulamayı devre dışı bırakmak için, sayfa yönergesinin `validateRequest` özniteliğini `false`olarak ayarlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="7de32-129">To disable request validation on a page you must set the `validateRequest` attribute of the Page directive to `false`:</span></span>

[!code-aspx[Main](request-validation/samples/sample1.aspx)]

> [!CAUTION]
> <span data-ttu-id="7de32-130">İstek doğrulaması devre dışı bırakıldığında, içerik bir sayfaya gönderilebilir; Bu, içeriğin düzgün şekilde kodlandığından veya işlendiğinden emin olmak için sayfa geliştiricisinin sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="7de32-130">When request validation is disabled, content can be submitted to a page; it is the responsibility of the page developer to ensure that content is properly encoded or processed.</span></span>

## <a name="disabling-request-validation-for-your-application"></a><span data-ttu-id="7de32-131">Uygulamanız için istek doğrulamasını devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="7de32-131">Disabling request validation for your application</span></span>

<span data-ttu-id="7de32-132">Uygulamanız için istek doğrulamayı devre dışı bırakmak için, uygulamanız için bir Web. config dosyası değiştirmeniz veya oluşturmanız ve `<pages />` bölümünün validateRequest özniteliğini `false`olarak ayarlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="7de32-132">To disable request validation for your application, you must modify or create a Web.config file for your application and set the validateRequest attribute of the `<pages />` section to `false`:</span></span>

[!code-xml[Main](request-validation/samples/sample2.xml)]

<span data-ttu-id="7de32-133">Sunucunuzdaki tüm uygulamalar için istek doğrulamayı devre dışı bırakmak istiyorsanız, bu değişikliği Machine. config dosyanızda yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7de32-133">If you wish to disable request validation for all applications on your server, you can make this modification to your Machine.config file.</span></span>

> [!CAUTION]
> <span data-ttu-id="7de32-134">İstek doğrulaması devre dışı bırakıldığında, uygulamanıza içerik gönderilebilir; içeriğin doğru şekilde kodlandığından veya işlendiğinden emin olmak için uygulama geliştiricisinin sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="7de32-134">When request validation is disabled, content can be submitted to your application; it is the responsibility of the application developer to ensure that content is properly encoded or processed.</span></span>

<span data-ttu-id="7de32-135">Aşağıdaki kod, istek doğrulamasını devre dışı bırakmak için değiştirilmiştir:</span><span class="sxs-lookup"><span data-stu-id="7de32-135">The code below is modified to turn off request validation:</span></span>

![](request-validation/_static/image4.png)

<span data-ttu-id="7de32-136">Şimdi aşağıdaki JavaScript metin kutusuna girilmişse `<script>alert("hello!")</script>` sonuç şöyle olur:</span><span class="sxs-lookup"><span data-stu-id="7de32-136">Now if the following JavaScript was entered into the textbox `<script>alert("hello!")</script>` the result would be:</span></span>

![](request-validation/_static/image5.png)

<span data-ttu-id="7de32-137">Bunun oluşmasını engellemek için, istek doğrulama kapalıyken, içeriği HTML olarak kodlamamız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7de32-137">To prevent this from happening, with request validation turned off, we need to HTML encode the content.</span></span>

## <a name="how-to-html-encode-content"></a><span data-ttu-id="7de32-138">HTML kodlama içeriği</span><span class="sxs-lookup"><span data-stu-id="7de32-138">How to HTML encode content</span></span>

<span data-ttu-id="7de32-139">İstek doğrulamayı devre dışı bırakırsanız, daha sonra kullanılmak üzere depolanacak olan HTML kodlaması içerik için iyi bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="7de32-139">If you have disabled request validation, it is good practice to HTML-encode content that will be stored for future use.</span></span> <span data-ttu-id="7de32-140">HTML kodlaması, karşılık gelen HTML kodlu gösterimle birlikte otomatik olarak '&lt;' veya '&gt;' (diğer simgelerle birlikte) değiştirir.</span><span class="sxs-lookup"><span data-stu-id="7de32-140">HTML encoding will automatically replace any ‘&lt;' or ‘&gt;' (together with several other symbols) with their corresponding HTML encoded representation.</span></span> <span data-ttu-id="7de32-141">Örneğin, '&lt;', '&amp;lt; ' ile değiştirilmiştir ve '&gt;', '&amp;gt; ' ile değiştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7de32-141">For example, ‘&lt;' is replaced by ‘&amp;lt;' and ‘&gt;' is replaced by ‘&amp;gt;'.</span></span> <span data-ttu-id="7de32-142">Tarayıcılar tarayıcıda '&lt;' veya '&gt;' görüntülenmesini sağlamak için bu özel kodları kullanır.</span><span class="sxs-lookup"><span data-stu-id="7de32-142">Browsers use these special codes to display the ‘&lt;' or ‘&gt;' in the browser.</span></span>

<span data-ttu-id="7de32-143">İçerik, `Server.HtmlEncode(string)` API kullanılarak sunucu üzerinde kolayca HTML kodlanabilir.</span><span class="sxs-lookup"><span data-stu-id="7de32-143">Content can be easily HTML-encoded on the server using the `Server.HtmlEncode(string)` API.</span></span> <span data-ttu-id="7de32-144">İçerik ayrıca HTML kodu çözülemiyor, diğer bir deyişle `Server.HtmlDecode(string)` yöntemi kullanılarak standart HTML 'ye geri döndürülebilir.</span><span class="sxs-lookup"><span data-stu-id="7de32-144">Content can also be easily HTML-decoded, that is, reverted back to standard HTML using the `Server.HtmlDecode(string)` method.</span></span>

![](request-validation/_static/image6.png)

<span data-ttu-id="7de32-145">Sonuç:</span><span class="sxs-lookup"><span data-stu-id="7de32-145">Resulting in:</span></span>

![](request-validation/_static/image7.png)
