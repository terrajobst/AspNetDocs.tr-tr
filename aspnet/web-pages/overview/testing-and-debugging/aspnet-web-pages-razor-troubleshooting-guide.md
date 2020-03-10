---
uid: web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
title: ASP.NET Web Pages (Razor) sorun giderme kılavuzu | Microsoft Docs
author: Rick-Anderson
description: Bu makalede, ASP.NET Web Pages (Razor) ve bazı önerilen çözümlerle çalışırken karşılaşabileceğiniz sorunlar açıklanmaktadır. Yazılım sürümleri ASP.NET Web pag...
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 2a2c1833-0bfe-4e2e-9cc0-341b52c7b121
msc.legacyurl: /web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
msc.type: authoredcontent
ms.openlocfilehash: fc03767c16f46c1e282d24ee3a7df2409a7c38bb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78585766"
---
# <a name="aspnet-web-pages-razor-troubleshooting-guide"></a><span data-ttu-id="a3f68-104">ASP.NET Web Sayfaları (Razor) Sorun Giderme Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="a3f68-104">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>

<span data-ttu-id="a3f68-105">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="a3f68-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="a3f68-106">Bu makalede, ASP.NET Web Pages (Razor) ve bazı önerilen çözümlerle çalışırken karşılaşabileceğiniz sorunlar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a3f68-106">This article describes issues that you might have when working with ASP.NET Web Pages (Razor) and some suggested solutions.</span></span>
> 
> ## <a name="software-versions"></a><span data-ttu-id="a3f68-107">Yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="a3f68-107">Software versions</span></span>
> 
> 
> - <span data-ttu-id="a3f68-108">ASP.NET Web sayfaları (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="a3f68-108">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="a3f68-109">Bu öğretici Ayrıca ASP.NET Web Pages 2 ve ASP.NET Web Pages 1,0 ile de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-109">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0.</span></span>

<span data-ttu-id="a3f68-110">Bu konu aşağıdaki bölümleri içermektedir:</span><span class="sxs-lookup"><span data-stu-id="a3f68-110">This topic contains the following sections:</span></span>

- [<span data-ttu-id="a3f68-111">Çalışan sayfalarla ilgili sorunlar</span><span class="sxs-lookup"><span data-stu-id="a3f68-111">Issues with Running Pages</span></span>](#Issues_Running_.cshtml_Pages)
- [<span data-ttu-id="a3f68-112">Razor kodlu sorunlar</span><span class="sxs-lookup"><span data-stu-id="a3f68-112">Issues with Razor Code</span></span>](#IssuesWithRazorCode)
- [<span data-ttu-id="a3f68-113">Güvenlik ve üyelikle ilgili sorunlar</span><span class="sxs-lookup"><span data-stu-id="a3f68-113">Issues with Security and Membership</span></span>](#membership)
- [<span data-ttu-id="a3f68-114">E-posta gönderme sorunları</span><span class="sxs-lookup"><span data-stu-id="a3f68-114">Issues with Sending Email</span></span>](#email)
- [<span data-ttu-id="a3f68-115">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a3f68-115">Additional Resources</span></span>](#AdditionalResources)

<span data-ttu-id="a3f68-116">Genel sorular için bkz. [ASP.NET Web Pages (Razor) SSS](https://go.microsoft.com/fwlink/?LinkId=253000).</span><span class="sxs-lookup"><span data-stu-id="a3f68-116">For general questions, see [ASP.NET Web Pages (Razor) FAQ](https://go.microsoft.com/fwlink/?LinkId=253000).</span></span>

<a id="Issues_Running_.cshtml_Pages"></a>
## <a name="issues-with-running-pages"></a><span data-ttu-id="a3f68-117">Çalışan sayfalarla ilgili sorunlar</span><span class="sxs-lookup"><span data-stu-id="a3f68-117">Issues with Running Pages</span></span>

<span data-ttu-id="a3f68-118">Birçok sorun, *. cshtml* ve *. vbhtml* sayfalarının düzgün çalışmasını engelleyebilir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-118">A variety of issues can prevent *.cshtml* and *.vbhtml* pages from running properly.</span></span> <span data-ttu-id="a3f68-119">Bu bölümde, yaygın hata iletileri ve olası nedenler listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-119">This section lists common error messages and likely causes.</span></span>

### <a name="http-error-403---forbidden-access-is-denied"></a><span data-ttu-id="a3f68-120">HTTP Hatası 403-Yasak: erişim reddedildi</span><span class="sxs-lookup"><span data-stu-id="a3f68-120">HTTP Error 403 - Forbidden: Access is denied</span></span>

<span data-ttu-id="a3f68-121">*Sağladığınız kimlik bilgilerini kullanarak bu dizini veya sayfayı görüntüleme izniniz yok.*</span><span class="sxs-lookup"><span data-stu-id="a3f68-121">*You do not have permission to view this directory or page using the credentials that you supplied.*</span></span>

<span data-ttu-id="a3f68-122">Bu hata, sunucu doğru .NET Framework sürümünü çalıştırmadığından oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-122">This error can occur if the server is not running the correct version of the .NET Framework.</span></span> <span data-ttu-id="a3f68-123">Sunucuyu (yerel olarak veya uzaktan) çalıştıran bilgisayarın en azından .NET Framework 4 ' ün yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a3f68-123">Make sure that the computer that's running the server (locally or remotely) has at least the .NET Framework 4 installed.</span></span> <span data-ttu-id="a3f68-124">Ayrıca, uygulamanın kendisinin doğru sürümü çalıştıracak şekilde yapılandırıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="a3f68-124">Also make sure that the application itself is configured to run the right version.</span></span>

<span data-ttu-id="a3f68-125">WebMatrix 'te çalışırken bu sorunu yerel olarak görürseniz, **site** çalışma alanına tıklayın ve ardından TreeView 'da **Ayarlar**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a3f68-125">If you see this problem locally while working in WebMatrix, click the **Site** workspace, and then in the treeview click **Settings**.</span></span> <span data-ttu-id="a3f68-126">**.NET Framework sürüm Seç** listesinde, **.NET 4 (tümleşik)** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="a3f68-126">In the **Select .NET Framework Version** list, select **.NET 4 (Integrated)**.</span></span> <span data-ttu-id="a3f68-127">Bu sürüm zaten ayarlandıysa, WebMatrix 'i yönetici olarak çalıştırmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="a3f68-127">If this version is already set, try running WebMatrix as an administrator.</span></span>

<span data-ttu-id="a3f68-128">Web sitenizin kökünde en az bir *. cshtml* dosyası bulunduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a3f68-128">Make sure that the root of your website has at least one *.cshtml* file in it.</span></span>

<span data-ttu-id="a3f68-129">Web sunucusu uzak bir sunucuda olduğunda bu hatayı görürseniz, sunucu yöneticisine başvurun.</span><span class="sxs-lookup"><span data-stu-id="a3f68-129">If you see this error when the web server is on a remote server, contact the server administrator.</span></span> <span data-ttu-id="a3f68-130">Sunucuda .NET Framework 4 veya sonraki bir sürümünün yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a3f68-130">Make sure that the server has the .NET Framework 4 or later installed.</span></span> <span data-ttu-id="a3f68-131">Ayrıca, uygulamanın bu the.NET Framework sürümünü kullanacak şekilde yapılandırılmış bir uygulama havuzunda çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="a3f68-131">Also make sure that the application is running in an application pool that's configured to use that version of the.NET Framework.</span></span>

<span data-ttu-id="a3f68-132">Sunucu üzerinde denetiminiz varsa, .NET Framework doğru sürümünü çalıştırdığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="a3f68-132">If you have control over the server, make sure it's running the correct version of the .NET Framework.</span></span> <span data-ttu-id="a3f68-133">Ayrıca, `aspnet_regiis -iru` komutunu çalıştırarak yüklemeyi onarmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3f68-133">You might also try repairing the installation by running the `aspnet_regiis -iru` command.</span></span> <span data-ttu-id="a3f68-134">(Örneğin, .NET Framework yükledikten sonra IIS yüklerseniz, IIS ASP.NET sayfalarını çalıştıracak şekilde doğru şekilde yapılandırılmayacak.) Daha fazla bilgi için bkz. [ASP.NET IIS Kayıt Aracı (Aspnet\_regııs. exe)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx).</span><span class="sxs-lookup"><span data-stu-id="a3f68-134">(For example, if you install IIS after you install the .NET Framework, IIS will not be correctly configured to run ASP.NET pages.) For more information, see [ASP.NET IIS Registration Tool (Aspnet\_regiis.exe)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx).</span></span>

### <a name="http-error-40314---forbidden"></a><span data-ttu-id="a3f68-135">HTTP Hatası 403,14-yasak</span><span class="sxs-lookup"><span data-stu-id="a3f68-135">HTTP Error 403.14 - Forbidden</span></span>

<span data-ttu-id="a3f68-136">*Web sunucusu bu dizinin içeriğini listebir şekilde yapılandırılmamış.*</span><span class="sxs-lookup"><span data-stu-id="a3f68-136">*The Web server is configured to not list the contents of this directory.*</span></span>

<span data-ttu-id="a3f68-137">Bu hata, korunan bir kaynak ( *Web. config* dosyası gibi) veya korunan bir klasörde ( *App\_verileri* veya *uygulama\_kodu*gibi) istenirse oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-137">This error can occur if you request a resource that's protected (like the *Web.config* file) or that's in a folder that's protected (like *App\_Data* or *App\_Code*).</span></span>

### <a name="http-error-40417---not-found"></a><span data-ttu-id="a3f68-138">HTTP hatası 404,17-bulunamadı</span><span class="sxs-lookup"><span data-stu-id="a3f68-138">HTTP Error 404.17 - Not Found</span></span>

<span data-ttu-id="a3f68-139">*İstenen içerik betik gibi görünüyor ve statik dosya işleyicisi tarafından sunulmayacak.*</span><span class="sxs-lookup"><span data-stu-id="a3f68-139">*The requested content appears to be script and will not be served by the static file handler.*</span></span>

<span data-ttu-id="a3f68-140">Bu hata, sunucu .NET Framework 4 veya üzeri bir sürümü kullanmak için doğru yapılandırılmamışsa ve bu nedenle, `@{ }` bloklarda kodu tanımadığı durumlarda meydana gelebilir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-140">This error can occur if the server is not configured correctly to use the .NET Framework 4 or later, and therefore does not recognize the code in `@{ }` blocks.</span></span> <span data-ttu-id="a3f68-141">Bkz. *http hatası 403-Yasak: erişim reddedildi*.</span><span class="sxs-lookup"><span data-stu-id="a3f68-141">See the description earlier for *HTTP Error 403 - Forbidden: Access is denied*.</span></span>

### <a name="http-error-4047---not-found"></a><span data-ttu-id="a3f68-142">HTTP hatası 404,7-bulunamadı</span><span class="sxs-lookup"><span data-stu-id="a3f68-142">HTTP Error 404.7 - Not Found</span></span>

<span data-ttu-id="a3f68-143">*İstek filtreleme modülü dosya uzantısını reddedecek şekilde yapılandırıldı*</span><span class="sxs-lookup"><span data-stu-id="a3f68-143">*The request filtering module is configured to deny the file extension*</span></span>

<span data-ttu-id="a3f68-144">Bu hata, sunucuda *. cshtml* veya *. vbhtml* uzantıları açıkça engellenmişse oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-144">This error can occur if *.cshtml* or *.vbhtml* extensions have been explicitly blocked on the server.</span></span> <span data-ttu-id="a3f68-145">Bu sorunun belirtisi, URL 'Lerin uzantı içermediği durumlarda çalıştığı, ancak *. cshtml* veya *. vbhtml* içeren URL 'lerin çalışmamasından oluşur.</span><span class="sxs-lookup"><span data-stu-id="a3f68-145">A symptom of this problem is that URLs work when they do not include the extension, but URLs that include *.cshtml* or *.vbhtml* do not work.</span></span> <span data-ttu-id="a3f68-146">Olası bir çözüm, sitenin *Web. config* dosyasındaki uzantıları yeniden etkinleştirmektir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-146">A possible solution is to re-enable the extensions in the site's *Web.config* file.</span></span> <span data-ttu-id="a3f68-147">Aşağıdaki örnekte *. cshtml* uzantısının nasıl etkinleştirileceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-147">The following example shows how to enable the *.cshtml* extension.</span></span>

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample1.xml?highlight=5-6)]

### <a name="http-error-4048---not-found"></a><span data-ttu-id="a3f68-148">HTTP hatası 404,8-bulunamadı</span><span class="sxs-lookup"><span data-stu-id="a3f68-148">HTTP Error 404.8 - Not Found</span></span>

<span data-ttu-id="a3f68-149">*İstek filtreleme modülü, bir hiddenSegment bölümü içeren URL 'deki bir yolu reddedecek şekilde yapılandırılmıştır.*</span><span class="sxs-lookup"><span data-stu-id="a3f68-149">*The request filtering module is configured to deny a path in the URL that contains a hiddenSegment section.*</span></span>

<span data-ttu-id="a3f68-150">Bu hata, korunan bir kaynak ( *Web. config* dosyası gibi) veya korunan bir klasörde ( *App\_verileri* veya *uygulama\_kodu*gibi) istenirse oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-150">This error can occur if you request a resource that's protected (like the *Web.config* file) or that's in a folder that's protected (like *App\_Data* or *App\_Code*).</span></span>

### <a name="this-type-of-page-is-not-served-server-error-in--application"></a><span data-ttu-id="a3f68-151">Bu tür bir sayfaya sunulmuyor ('/' uygulamasında sunucu hatası)</span><span class="sxs-lookup"><span data-stu-id="a3f68-151">This type of page is not served (Server Error in '/' Application)</span></span>

<span data-ttu-id="a3f68-152">Daha önce HTTP hatası 404,17 için açıklamaya bakın.</span><span class="sxs-lookup"><span data-stu-id="a3f68-152">See the description earlier for HTTP Error 404.17.</span></span>

<a id="IssuesWithRazorCode"></a>
## <a name="issues-with-razor-code"></a><span data-ttu-id="a3f68-153">Razor kodlu sorunlar</span><span class="sxs-lookup"><span data-stu-id="a3f68-153">Issues with Razor code</span></span>

### <a name="the-name-class-does-not-exist-in-the-current-context"></a><span data-ttu-id="a3f68-154">'*Class*' adı geçerli bağlamda yok</span><span class="sxs-lookup"><span data-stu-id="a3f68-154">The name '*class*' does not exist in the current context</span></span>

<span data-ttu-id="a3f68-155">Genellikle, bu hatayı görmanızın bir nedeni `class` bir yardımcı başvuru, ancak yardımcı yüklenmez.</span><span class="sxs-lookup"><span data-stu-id="a3f68-155">Often, a reason you see this error is that `class` references a helper, but the helper is not installed.</span></span> <span data-ttu-id="a3f68-156">Örneğin, bir yardımcı kullanmaya çalışırsanız, ancak paketi NuGet 'den yüklemediyseniz bu hatayı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="a3f68-156">For example, if you try to use a helper, but if you haven't installed the package from NuGet, you'll see this error.</span></span> <span data-ttu-id="a3f68-157">Yardımcıyı bulmak ve yüklemek için WebMatrix 'teki galeriyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="a3f68-157">Use the Gallery in WebMatrix to find and install the helper.</span></span>

<span data-ttu-id="a3f68-158">Yardımcı yüklenirse, ancak sayfa hala tanınmıyorsa, koda bir `using` ekleyin ifadesini eklemeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="a3f68-158">If the helper is installed, but the page still doesn't recognize it, try adding add a `using` statement to the code.</span></span> <span data-ttu-id="a3f68-159">`using` bildiriminde, yardımcı içeren ad alanına başvurun.</span><span class="sxs-lookup"><span data-stu-id="a3f68-159">In the `using` statement, reference the namespace that includes the helper.</span></span> <span data-ttu-id="a3f68-160">Örneğin, ASP.NET Web yardımcıları paketindeki temel yardımcılar `System.Web.Helpers` ad alanıdır.</span><span class="sxs-lookup"><span data-stu-id="a3f68-160">For example, the basic helpers that are in the ASP.NET Web Helpers package are in the `System.Web.Helpers` namespace.</span></span> <span data-ttu-id="a3f68-161">Yardımcı 'yı kullanmak istediğiniz sayfanın en üstünde şu satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a3f68-161">At the top of the page where you want to use the helper, add this line:</span></span>

`@using Microsoft.Web.Helpers;`

<a id="membership"></a>
## <a name="issues-with-security-and-membership"></a><span data-ttu-id="a3f68-162">Güvenlik ve üyelikle ilgili sorunlar</span><span class="sxs-lookup"><span data-stu-id="a3f68-162">Issues with Security and Membership</span></span>

<span data-ttu-id="a3f68-163">ASP.NET Web Pages (Razor) içinde yerleşik güvenlik (üyelik) sistemini kullanıyorsanız, aşağıdaki sorunlarla karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3f68-163">If you are using the built-in security (membership) system in ASP.NET Web Pages (Razor), you might encounter the following issues.</span></span>

### <a name="to-call-this-method-the-membershipprovider-property-must-be-an-instance-of-extendedmembershipprovider"></a><span data-ttu-id="a3f68-164">Bu yöntemi çağırmak için, "Membership. Provider" özelliği "ExtendedMembershipProvider" öğesinin bir örneği olmalıdır</span><span class="sxs-lookup"><span data-stu-id="a3f68-164">To call this method, the "Membership.Provider" property must be an instance of "ExtendedMembershipProvider"</span></span>

<span data-ttu-id="a3f68-165">Bu hata, `AspNetSqlMembershipProvider` sınıfının yapılandırılmadığını gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-165">This error can indicate that no `AspNetSqlMembershipProvider` class is configured.</span></span> <span data-ttu-id="a3f68-166">(Bir belirti, sitenin yerel olarak ince çalışacağından, ancak bir barındırma sağlayıcısının sunucusunda yayımladığınızda bu hatayı oluşturur.) Bu sorunun bir onarımı, sitenin *Web. config* dosyasına aşağıdakini ekleyerek basit üyeliği açıkça etkinleştirmektir:</span><span class="sxs-lookup"><span data-stu-id="a3f68-166">(A symptom is that the site works fine locally but throws this error when you publish it to a hosting provider's server.) One fix for this problem is to explicitly enable simple membership by adding the following to the site's *Web.config* file:</span></span>

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample2.xml?highlight=6)]

<a id="email"></a>
## <a name="issues-with-sending-email"></a><span data-ttu-id="a3f68-167">E-posta gönderme sorunları</span><span class="sxs-lookup"><span data-stu-id="a3f68-167">Issues with Sending Email</span></span>

<span data-ttu-id="a3f68-168">E-posta gönderme sorunları hata ayıklaması zor olabilir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-168">Problems with sending email can be challenging to debug.</span></span> <span data-ttu-id="a3f68-169">Bir ilk sorun, SMTP sunucusuna bağlanamadan olabilir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-169">An initial problem can be that you can't connect to the SMTP server.</span></span> <span data-ttu-id="a3f68-170">Bağlantı başarılı olursa, iletiyi SMTP sunucusuna ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a3f68-170">If the connection is successful, ASP.NET hands the message off to the SMTP server.</span></span> <span data-ttu-id="a3f68-171">Ancak, iletinin kendisiyle birlikte SMTP sunucusunun göndermesini önleyen sorunlar olabilir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-171">However, there can be problems with the message itself that prevents the SMTP server from sending it.</span></span>

<span data-ttu-id="a3f68-172">Uygulamanız başarılı bir şekilde e-posta göndermezse, aşağıdakileri deneyin:</span><span class="sxs-lookup"><span data-stu-id="a3f68-172">If your application does not successfully send email, try the following:</span></span>

- <span data-ttu-id="a3f68-173">SMTP sunucusu adı genellikle `smtp.provider.com` veya `smtp.provider.net`gibi bir şeydir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-173">The SMTP server name is often something like `smtp.provider.com` or `smtp.provider.net`.</span></span> <span data-ttu-id="a3f68-174">Ancak, sitenizi bir barındırma sağlayıcısına yayımlarsanız, söz konusu noktada SMTP sunucu adı `localhost`olabilir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-174">However, if you publish your site to a hosting provider, the SMTP server name at that point might be `localhost`.</span></span> <span data-ttu-id="a3f68-175">Bu durum, yayımladıktan ve sitenizin sağlayıcının sunucusunda çalışıyor olması nedeniyle, SMTP sunucusu uygulamanızın perspektifinden yerel olabilir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-175">This situation occurs because after you've published and your site is running on the provider's server, the SMTP server might be local from the perspective of your application.</span></span> <span data-ttu-id="a3f68-176">Sunucu adlarında bu değişiklik, yayımlama işleminizin bir parçası olarak SMTP sunucu adını değiştirmeniz gerektiği anlamına gelebilir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-176">This change in server names might mean that you have to change the SMTP server name as part of your publishing process.</span></span>
- <span data-ttu-id="a3f68-177">Bağlantı noktası numarası genellikle 25 ' tir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-177">The port number is usually 25.</span></span> <span data-ttu-id="a3f68-178">Ancak, bazı sağlayıcılar bağlantı noktası 587 ' yı veya başka bir bağlantı noktasını kullanmanızı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-178">However, some providers require you to use port 587 or some other port.</span></span> <span data-ttu-id="a3f68-179">SMTP sunucusunun sahibine, kullanmanız beklenen bağlantı noktası numarasını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="a3f68-179">Check with the owner of the SMTP server what port number they expect you to use.</span></span>
- <span data-ttu-id="a3f68-180">Doğru kimlik bilgilerini kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a3f68-180">Make sure that you use the right credentials.</span></span> <span data-ttu-id="a3f68-181">Sitenizi bir barındırma sağlayıcısına yayımladıysanız, sağlayıcının özel olarak belirttiği kimlik bilgilerini e-posta için kullanın.</span><span class="sxs-lookup"><span data-stu-id="a3f68-181">If you've published your site to a hosting provider, use the credentials that the provider has specifically indicated are for email.</span></span> <span data-ttu-id="a3f68-182">Bu kimlik bilgileri, yayımlamak için kullandığınız kimlik bilgilerinden farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-182">These credentials might be different from the credentials you use to publish.</span></span>
- <span data-ttu-id="a3f68-183">Bazen kimlik bilgilerine gerek kalmaz.</span><span class="sxs-lookup"><span data-stu-id="a3f68-183">Sometimes you don't need credentials at all.</span></span> <span data-ttu-id="a3f68-184">Kişisel ISS 'nizi kullanarak e-posta gönderiyorsanız, e-posta sağlayıcınız kimlik bilgilerinizi zaten bilir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-184">If you're sending email by using your personal ISP, your email provider might already know your credentials.</span></span> <span data-ttu-id="a3f68-185">Yayımladıktan sonra, yerel bilgisayarınızda sınama yaparken farklı kimlik bilgileri kullanmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-185">After you publish, you might need to use different credentials than when you test on your local computer.</span></span>
- <span data-ttu-id="a3f68-186">E-posta sağlayıcınız şifreleme kullanıyorsa, `WebMail.EnableSsl` `true`olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a3f68-186">If your email provider uses encryption, set `WebMail.EnableSsl` to `true`.</span></span>

<span data-ttu-id="a3f68-187">E-posta gönderilirken bir hata oluşursa, şuna benzer bir standart ASP.NET hata iletisi görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a3f68-187">If there is an error sending email, you might see a standard ASP.NET error message, which looks like this:</span></span>

![E-postada bir sorun olduğunda ASP.NET hata iletisi](aspnet-web-pages-razor-troubleshooting-guide/_static/image1.png)

<span data-ttu-id="a3f68-189">Ayrıca, aşağıdaki örnekte olduğu gibi `try-catch` bloğu kullanarak e-posta gönderme sorunlarını da ayıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3f68-189">You can also debug problems with sending email by using a `try-catch` block, as in the following example.</span></span> <span data-ttu-id="a3f68-190">Bir `try-catch` bloğu kullandığınızda, ASP.NET standart hata iletilerini görüntülemez.</span><span class="sxs-lookup"><span data-stu-id="a3f68-190">When you use a `try-catch` block, ASP.NET does not display its standard error messages.</span></span> <span data-ttu-id="a3f68-191">Bunun yerine, hatayı bloğun `catch` bölümünde yakalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3f68-191">Instead, you can capture the error in the `catch` portion of the block.</span></span>

[!code-cshtml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample3.cshtml)]

<span data-ttu-id="a3f68-192">`your-SMTP-server-name`için uygun değerleri değiştirin ve bu şekilde devam edin.</span><span class="sxs-lookup"><span data-stu-id="a3f68-192">Substitute the appropriate values for `your-SMTP-server-name`, and so on.</span></span> <span data-ttu-id="a3f68-193">Bu şekilde, bazı hata iletileri şunları görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a3f68-193">Some of the error messages you might see this way include the following:</span></span>

- <span data-ttu-id="a3f68-194">*Posta gönderilirken hata oluştu.*</span><span class="sxs-lookup"><span data-stu-id="a3f68-194">*Failure sending mail.*</span></span>

    <span data-ttu-id="a3f68-195">veya</span><span class="sxs-lookup"><span data-stu-id="a3f68-195">-or-</span></span>

    <span data-ttu-id="a3f68-196">*Bağlı olan taraf bir süre sonra düzgün bir şekilde yanıt vermediğinden veya bağlı konak yanıt vermediğinden bağlantı kurulamadığı için bağlantı girişimi başarısız oldu*</span><span class="sxs-lookup"><span data-stu-id="a3f68-196">*A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond*</span></span>

    <span data-ttu-id="a3f68-197">Bu hata genellikle uygulamanın SMTP sunucusuna bağlanamabileceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-197">This error usually means that the application could not connect to the SMTP server.</span></span> <span data-ttu-id="a3f68-198">Sunucu adını ve bağlantı noktası numarasını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="a3f68-198">Check the server name and port number.</span></span>
- <span data-ttu-id="a3f68-199">*Posta kutusu kullanılamıyor. Sunucu yanıtı: 5.1.0 &lt;someuser@invaliddomain&gt; gönderen reddedildi: geçersiz gönderici etki alanı*</span><span class="sxs-lookup"><span data-stu-id="a3f68-199">*Mailbox unavailable. The server response was: 5.1.0 &lt;someuser@invaliddomain&gt; sender rejected : invalid sender domain*</span></span>

    <span data-ttu-id="a3f68-200">Bu ileti, `From` adresinin doğru olmadığını veya eksik olduğunu gösteriyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-200">This message can indicate that the `From` address is not correct or is missing.</span></span>
- <span data-ttu-id="a3f68-201">*Belirtilen dize, bir e-posta adresi için gereken biçimde değil.*</span><span class="sxs-lookup"><span data-stu-id="a3f68-201">*The specified string is not in the form required for an email address.*</span></span>

    <span data-ttu-id="a3f68-202">Bu hata, `To` veya `From` özelliklerinin bir e-posta adresi olarak tanınmadığını gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-202">This error might indicate that the value of the `To` or `From` properties are not recognized as email addresses.</span></span> <span data-ttu-id="a3f68-203">(ASP.NET, e-posta adresinin geçerli olduğunu, yalnızca *name@domain.com* gibi doğru biçimde olduğunu kontrol edemez.)</span><span class="sxs-lookup"><span data-stu-id="a3f68-203">(ASP.NET cannot check that the email address is valid, only that it's in the correct format, like *name@domain.com*.)</span></span>

> [!NOTE]
> <span data-ttu-id="a3f68-204">Sayfayı canlı bir siteye yayımlamadan önce hatayı gösteren biçimlendirmeyi kaldırın (`@errorMessage`).</span><span class="sxs-lookup"><span data-stu-id="a3f68-204">Remove the markup that displays the error (`@errorMessage`) before you publish the page to a live site.</span></span> <span data-ttu-id="a3f68-205">Kullanıcıların bir sunucudan aldığınız hata iletilerini görmesini sağlamak iyi bir fikir değildir.</span><span class="sxs-lookup"><span data-stu-id="a3f68-205">It's not a good idea to let users see error messages that you get from a server.</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="a3f68-206">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a3f68-206">Additional Resources</span></span>

[<span data-ttu-id="a3f68-207">ASP.NET Web Sayfaları (Razor) SSS</span><span class="sxs-lookup"><span data-stu-id="a3f68-207">ASP.NET Web Pages (Razor) FAQ</span></span>](https://go.microsoft.com/fwlink/?LinkId=253000)

<span data-ttu-id="a3f68-208">ASP.NET Web sitesinde [WebMatrix ve ASP.NET Web Pages](https://forums.asp.net/1224.aspx/1?WebMatrix) Forumu</span><span class="sxs-lookup"><span data-stu-id="a3f68-208">[WebMatrix and ASP.NET Web Pages](https://forums.asp.net/1224.aspx/1?WebMatrix) forum on the ASP.NET website</span></span>
