---
uid: mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
title: ASP.NET MVC Uygulamanızda hatalarla hata ayıklayın ve göz at! Microsoft Docs
author: Rick-Anderson
description: Imampte, ASP.NET a için ayrıntılı performans, hata ayıklama ve tanılama bilgileri sağlayan açık kaynaklı ve büyüyen açık kaynaklı NuGet paketleri ailesidir.
ms.author: riande
ms.date: 03/26/2015
ms.assetid: c205805f-efdd-4fa7-9616-f26eab180611
msc.legacyurl: /mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
msc.type: authoredcontent
ms.openlocfilehash: d3689147a3bc3aa1f4180c377d2483a94bdd95a9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538537"
---
# <a name="profile-and-debug-your-aspnet-mvc-app-with-glimpse"></a><span data-ttu-id="7c66a-103">Glimpse ile ASP.NET MVC uygulamanızın profilini oluşturma ve hatalarını ayıklama</span><span class="sxs-lookup"><span data-stu-id="7c66a-103">Profile and debug your ASP.NET MVC app with Glimpse</span></span>

<span data-ttu-id="7c66a-104">[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından</span><span class="sxs-lookup"><span data-stu-id="7c66a-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="7c66a-105">Imampte, ASP.NET uygulamaları için ayrıntılı performans, hata ayıklama ve tanılama bilgileri sağlayan açık kaynaklı bir ve büyüyen açık kaynaklı NuGet paketleri ailesidir.</span><span class="sxs-lookup"><span data-stu-id="7c66a-105">Glimpse is a thriving and growing family of open source NuGet packages that provides detailed performance, debugging and diagnostic information for ASP.NET apps.</span></span> <span data-ttu-id="7c66a-106">Her sayfanın en altında önemli performans ölçümlerini yüklemek, basit, ultra hızlı bir şekilde yüklemektir.</span><span class="sxs-lookup"><span data-stu-id="7c66a-106">It's trivial to install, lightweight, ultra-fast, and displays key performance metrics at the bottom of every page.</span></span> <span data-ttu-id="7c66a-107">Sunucuda neler olduğunu bulmanız gerektiğinde uygulamanızın detayına gitmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c66a-107">It allows you to drill down into your app when you need to find out what's going on at the server.</span></span> <span data-ttu-id="7c66a-108">Bu sayede, Azure test ortamınız dahil olmak üzere geliştirme döngünüzde kullanmanızı önerdiğimiz çok değerli bilgiler sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7c66a-108">Glimpse provides so much valuable information we recommend you use it throughout your development cycle, including your Azure test environment.</span></span> <span data-ttu-id="7c66a-109">[Fiddler](http://www.telerik.com/fiddler) ve [F-12 geliştirme araçları](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx) bir istemci tarafı görünümü sağlarken, bu, sunucudan ayrıntılı bir görünüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c66a-109">While [Fiddler](http://www.telerik.com/fiddler) and the [F-12 development tools](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx) provide a client side view, Glimpse provides a detailed view from the server.</span></span> <span data-ttu-id="7c66a-110">Bu öğretici, bir diğer çok paket olan ASP.NET MVC ve EF paketlerini kullanmaya odaklanacaktır.</span><span class="sxs-lookup"><span data-stu-id="7c66a-110">This tutorial will focus on using the Glimpse ASP.NET MVC and EF packages, but many other packages are available.</span></span> <span data-ttu-id="7c66a-111">Mümkün olduğunca, bakımı istediğim uygun bir yardım [belgelerine](http://getglimpse.com/Docs/) bağlayacağım.</span><span class="sxs-lookup"><span data-stu-id="7c66a-111">Where possible I will link to the appropriate [Glimpse docs](http://getglimpse.com/Docs/) which I help maintain.</span></span> <span data-ttu-id="7c66a-112">Bir açık kaynaklı projem, kaynak koda ve belgelere de katkıda bulunabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c66a-112">Glimpse is an open source project, you too can contribute to the source code and the docs.</span></span>

- [<span data-ttu-id="7c66a-113">Göz at yükleme</span><span class="sxs-lookup"><span data-stu-id="7c66a-113">Installing Glimpse</span></span>](#ig)
- [<span data-ttu-id="7c66a-114">Localhost için göz at 'ı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="7c66a-114">Enable Glimpse for localhost</span></span>](#eg)
- [<span data-ttu-id="7c66a-115">Zaman çizelgesi sekmesi</span><span class="sxs-lookup"><span data-stu-id="7c66a-115">The Timeline tab</span></span>](#Time)
- [<span data-ttu-id="7c66a-116">Model Bağlamaları</span><span class="sxs-lookup"><span data-stu-id="7c66a-116">Model Binding</span></span>](#mb)
- [<span data-ttu-id="7c66a-117">Rotalar</span><span class="sxs-lookup"><span data-stu-id="7c66a-117">Routes</span></span>](#route)
- [<span data-ttu-id="7c66a-118">Azure 'da göz at kullanma</span><span class="sxs-lookup"><span data-stu-id="7c66a-118">Using Glimpse on Azure</span></span>](#da)
- [<span data-ttu-id="7c66a-119">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="7c66a-119">Additional Resources</span></span>](#addRes)

<a id="ig"></a>
## <a name="installing-glimpse"></a><span data-ttu-id="7c66a-120">Göz at yükleme</span><span class="sxs-lookup"><span data-stu-id="7c66a-120">Installing Glimpse</span></span>

<span data-ttu-id="7c66a-121">, NuGet paket yöneticisi konsolundan veya **NuGet Paketlerini Yönet** konsolundan bir göz atmak sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c66a-121">You can install Glimpse from the NuGet package manager console or from the **Manage NuGet Packages** console.</span></span> <span data-ttu-id="7c66a-122">Bu demo için Mvc5 ve EF6 paketlerini yükleyeceğim:</span><span class="sxs-lookup"><span data-stu-id="7c66a-122">For this demo, I'll install the Mvc5 and EF6 packages:</span></span>

![NuGet DLG 'ten bir göz at yüklemesi](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image1.png)

<span data-ttu-id="7c66a-124">*Göz at. EF* için arama</span><span class="sxs-lookup"><span data-stu-id="7c66a-124">Search for *Glimpse.EF*</span></span>

![NuGet Install DLG 'ten tımpi. EF](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image2.png)

<span data-ttu-id="7c66a-126">**Yüklü paketler**' i seçerek, yüklü olan tımpde bağımlı modüllerin yüklendiğini görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7c66a-126">By selecting **Installed packages**, you can see the Glimpse dependent modules installed:</span></span>

![DLg 'ten bir Tımpo paketleri yüklendi](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image3.png)

<span data-ttu-id="7c66a-128">Aşağıdaki komutlar, paket yöneticisi konsolundan Tımpo MVC5 ve EF6 modüllerini yükler:</span><span class="sxs-lookup"><span data-stu-id="7c66a-128">The following commands install Glimpse MVC5 and EF6 modules from the package manager console:</span></span>

[!code-console[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample1.cmd)]

<a id="eg"></a>
## <a name="enable-glimpse-for-localhost"></a><span data-ttu-id="7c66a-129">Localhost için göz at 'ı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="7c66a-129">Enable Glimpse for localhost</span></span>

<span data-ttu-id="7c66a-130">http://localhost:&lt;p ort #&gt;/tımpse.exe öğesine gidin ve <strong>Aç</strong> düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c66a-130">Navigate to http://localhost:&lt;port #&gt;/glimpse.axd and click the <strong>Turn Glimpse On</strong> button.</span></span>

![Göz atlama sayfası](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image4.png)

<span data-ttu-id="7c66a-132">Sık Kullanılanlar çubuğunuzu görüntüleniyorsa, Tımpi düğmelerini sürükleyip bırakabilir ve bunları bookmarkas olarak ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7c66a-132">If you have your favorites bar displayed, you can drag and drop the Glimpse buttons and add them as bookmarklets:</span></span>

![Göz at ile IE](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image5.png)

<span data-ttu-id="7c66a-134">Artık uygulamanızda gezinebilirsiniz ve sayfanın alt kısmında **başlık ekranı** (HUD) gösterilir.</span><span class="sxs-lookup"><span data-stu-id="7c66a-134">You can now navigate your app, and the **Heads Up Display** (HUD) is shown at the bottom of the page.</span></span>

![HUD ile Contact Manager sayfası](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image6.png)

<span data-ttu-id="7c66a-136">[Göz at sayfası](http://getglimpse.com/Docs/Heads-up-Display) , yukarıda gösterilen zamanlama bilgilerinin ayrıntılarını.</span><span class="sxs-lookup"><span data-stu-id="7c66a-136">The [Glimpse HUD page](http://getglimpse.com/Docs/Heads-up-Display) details the timing information shown above.</span></span> <span data-ttu-id="7c66a-137">HUD 'nin görüntülediği performans verileri, test döngüsüne başlamadan önce bir sorunla hemen haberdar edebilir.</span><span class="sxs-lookup"><span data-stu-id="7c66a-137">The unobtrusive performance data the HUD displays can notify you of a problem immediately - before you get to the test cycle.</span></span> <span data-ttu-id="7c66a-138">Sağ alt köşedeki &quot;g&quot; tıklamak, bu paneli getirir:</span><span class="sxs-lookup"><span data-stu-id="7c66a-138">Clicking on the &quot;g&quot; in the lower right corner brings up the Glimpse panel:</span></span>

![Göz at bölmesi](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image7.png)

<span data-ttu-id="7c66a-140">Yukarıdaki görüntüde, işlem hattındaki eylemlerin ve filtrelerin zamanlama ayrıntılarını gösteren [yürütme sekmesi](http://getglimpse.com/Docs/Execution-Tab) seçilidir.</span><span class="sxs-lookup"><span data-stu-id="7c66a-140">In the image above, the [Execution tab](http://getglimpse.com/Docs/Execution-Tab) is selected, which shows timing details of the actions and filters in the pipeline.</span></span> <span data-ttu-id="7c66a-141">[Durdurma izleme filtre süreölçeri](http://www.nuget.org/packages/StopWatch/) ' nin işlem hattının 6. aşamasında başlamasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c66a-141">You can see my [Stop Watch filter timer](http://www.nuget.org/packages/StopWatch/) start at stage 6 of the pipeline.</span></span> <span data-ttu-id="7c66a-142">Hafif ağırlık zamanımı faydalı profil/zamanlama verileri sağlayabiliyorsa, yetkilendirme ve Görünüm işleme için harcanan tüm süreyi yok bulur.</span><span class="sxs-lookup"><span data-stu-id="7c66a-142">While my light weight timer can provide useful profile/timing data, it misses all the time spent in authorization and rendering the view.</span></span> <span data-ttu-id="7c66a-143">[ASP.NET MVC uygulamanızı profilde ve zaman zaman Azure 'a yönelik olarak](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx)zamanımı hakkında bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c66a-143">You can read about my timer at [Profile and Time your ASP.NET MVC app all the way to Azure](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx).</span></span> <span data-ttu-id="7c66a-144">[Sekmeler](http://getglimpse.com/Docs/Tabs) sayfası, her sekme hakkında ayrıntılı bilgi için bağlantılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c66a-144">The [Tabs](http://getglimpse.com/Docs/Tabs) page provides links to detailed information on each tab.</span></span>

<a id="Time"></a>
## <a name="the-timeline-tab"></a><span data-ttu-id="7c66a-145">Zaman çizelgesi sekmesi</span><span class="sxs-lookup"><span data-stu-id="7c66a-145">The Timeline tab</span></span>

<span data-ttu-id="7c66a-146">Aşağıdaki kod ile ilgili olarak, Dykstra 'in bekleyen [EF 6/MVC 5 öğreticisini](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) , Eğitmenler denetleyicisine değiştirdim:</span><span class="sxs-lookup"><span data-stu-id="7c66a-146">I've modified Tom Dykstra's outstanding [EF 6/MVC 5 tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) with the following code change to the instructors controller:</span></span>

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample2.cs?highlight=1,20-31)]

<span data-ttu-id="7c66a-147">Yukarıdaki kod, verilerin Eager veya açıkça yüklenmesini denetlemek için sorgu dizesinde (`eager`) geçiş yapmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="7c66a-147">The code above allows me to pass in query string (`eager`) to control eager or explicit loading of data.</span></span> <span data-ttu-id="7c66a-148">Aşağıdaki görüntüde, açık yükleme kullanılır ve zamanlama sayfası `Index` eylem yönteminde yüklenen her kaydı gösterir:</span><span class="sxs-lookup"><span data-stu-id="7c66a-148">In the image below, explicit loading is used and the timing page shows each enrollment loaded in the `Index` action method:</span></span>

![açık yükleme](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image8.png)

<span data-ttu-id="7c66a-150">Aşağıdaki kodda, Eager belirtilir ve `Index` görünümü çağrıldıktan sonra her kayıt getirilir:</span><span class="sxs-lookup"><span data-stu-id="7c66a-150">In the following code, eager is specified, and each enrollment is fetched after the `Index` view is called:</span></span>

![Eager belirtildi](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image9.png)

<span data-ttu-id="7c66a-152">Ayrıntılı zamanlama bilgileri almak için bir zaman diliminin üzerine geleleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7c66a-152">You can hover over a time segment to get detailed timing information:</span></span>

![ayrıntılı zamanlamayı görmek için üzerine gelin](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image10.png)

<a id="mb"></a>
## <a name="model-binding"></a><span data-ttu-id="7c66a-154">Model bağlama</span><span class="sxs-lookup"><span data-stu-id="7c66a-154">Model Binding</span></span>

<span data-ttu-id="7c66a-155">[Model bağlama sekmesi](http://getglimpse.com/Docs/Model-Binding-Tab) , form değişkenlerinizin nasıl bağlandığını anlamanıza yardımcı olmak için çok fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c66a-155">The [model binding tab](http://getglimpse.com/Docs/Model-Binding-Tab) provides a wealth of information to help you understand how your form variables are bound and why some are not bound as would expect.</span></span> <span data-ttu-id="7c66a-156">Aşağıdaki görüntüde gösterir **?**</span><span class="sxs-lookup"><span data-stu-id="7c66a-156">The image below shows the **?**</span></span> <span data-ttu-id="7c66a-157">simgesine tıklayarak bu özellik için yardım sayfasını bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c66a-157">icon, which you can click on to bring up the glimpse help page for that feature.</span></span>

![göz uyumlu model bağlama görünümü](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image11.png)

<a id="route"></a>
## <a name="routes"></a><span data-ttu-id="7c66a-159">Yollar</span><span class="sxs-lookup"><span data-stu-id="7c66a-159">Routes</span></span>

 <span data-ttu-id="7c66a-160">Diğer yollar sekmesi, yönlendirmeye hata ayıklamanıza ve anlamanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="7c66a-160">The Glimpse Routes tab will can help you debug and understand routing.</span></span> <span data-ttu-id="7c66a-161">Aşağıdaki görüntüde, ürün rotası seçilidir (ve yeşil, bir bir göz kuralı olarak gösterilir).</span><span class="sxs-lookup"><span data-stu-id="7c66a-161">In the image below, the product route is selected (and it shows in green, a Glimpse convention).</span></span> <span data-ttu-id="7c66a-162">![ürün adı](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) yol kısıtlamaları, bölgeler ve veri belirteçleri de görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="7c66a-162">![product name selected](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) Route constraints, Areas and data tokens are also displayed.</span></span> <span data-ttu-id="7c66a-163">Daha fazla bilgi için bkz. [ASP.NET MVC 5 içindeki](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx) [Tımpo rotaları](http://getglimpse.com/Docs/Routes-Tab) ve öznitelik yönlendirme.</span><span class="sxs-lookup"><span data-stu-id="7c66a-163">See [Glimpse Routes](http://getglimpse.com/Docs/Routes-Tab) and [Attribute Routing in ASP.NET MVC 5](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx) for more information.</span></span> 

<a id="da"></a>
## <a name="using-glimpse-on-azure"></a><span data-ttu-id="7c66a-164">Azure 'da göz at kullanma</span><span class="sxs-lookup"><span data-stu-id="7c66a-164">Using Glimpse on Azure</span></span>

<span data-ttu-id="7c66a-165">Bu varsayılan güvenlik ilkesi, yalnızca bir yerel konaktan tımpo verilerinin görüntülenmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="7c66a-165">The Glimpse default security policy only allows Glimpse data to be displayed from local host.</span></span> <span data-ttu-id="7c66a-166">Bu verileri uzak bir sunucuda (örneğin, Azure 'da bir Web uygulaması) görüntüleyebilmeniz için bu güvenlik ilkesini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c66a-166">You can change this security policy so you can view this data on a remote server (such as a web app on Azure).</span></span> <span data-ttu-id="7c66a-167">Azure 'daki test ortamları için, dikkat etmek üzere *Web. config* dosyasının en altına vurgulanan işareti ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7c66a-167">For test environments on Azure, add the highlighted mark up to the bottom of the *web.config* file to enable Glimpse:</span></span>

[!code-xml[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample3.xml?highlight=2-6)]

<span data-ttu-id="7c66a-168">Bu değişiklik tek başına, herhangi bir Kullanıcı, uzak bir sitede bulunan tüm kullanıcılar için veri görebilir.</span><span class="sxs-lookup"><span data-stu-id="7c66a-168">With this change alone, any user can see your Glimpse data on a remote site.</span></span> <span data-ttu-id="7c66a-169">Yukarıdaki biçimlendirmeyi bir yayımlama profiline eklemeyi göz önünde bulundurun, böylece yalnızca bu yayımlama profilini kullandığınızda (örneğin, Azure test profiliniz) uygulanan bir uygulanmış şekilde dağıtılır. Diğer verileri kısıtlamak için `canViewGlimpseData` rolünü ekleyecek ve yalnızca bu roldeki kullanıcıların, Tımpo verilerini görüntülemesine izin vereceğiz.</span><span class="sxs-lookup"><span data-stu-id="7c66a-169">Consider adding the markup above to a publish profile so it's only deployed an applied when you use that publish profile (for example, your Azure test profile.) To restrict Glimpse data, we will add the `canViewGlimpseData` role and only allow users in this role to view Glimpse data.</span></span>

<span data-ttu-id="7c66a-170">*GlimpseSecurityPolicy.cs* dosyasından açıklamaları kaldırın ve `Administrator` [isinrole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx) çağrısını `canViewGlimpseData` rolüne değiştirin:</span><span class="sxs-lookup"><span data-stu-id="7c66a-170">Remove the comments from the *GlimpseSecurityPolicy.cs* file and change the [IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx) call from `Administrator` to the `canViewGlimpseData` role:</span></span>

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample4.cs?highlight=6)]

> [!WARNING]
> <span data-ttu-id="7c66a-171">Güvenlik-bir bakışta sunulan zengin veriler, uygulamanızın güvenliğini açığa çıkarır.</span><span class="sxs-lookup"><span data-stu-id="7c66a-171">Security - The rich data provided by Glimpse could expose the security of your app.</span></span> <span data-ttu-id="7c66a-172">Microsoft, üretimler uygulamalarında kullanım için bir güvenlik denetimi gerçekleştirmedi.</span><span class="sxs-lookup"><span data-stu-id="7c66a-172">Microsoft has not performed a security audit of Glimpse for use on productions apps.</span></span>

<span data-ttu-id="7c66a-173">Rol ekleme hakkında daha fazla bilgi için bkz. [Üyelik, OAuth ve SQL veritabanı Ile güvenli ASP.NET MVC 5 Web uygulamasını Azure 'Da dağıtma](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="7c66a-173">For information on adding roles, see my [Deploy a Secure ASP.NET MVC 5 web app with Membership, OAuth, and SQL Database to Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) tutorial.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="7c66a-174">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="7c66a-174">Additional Resources</span></span>

- [<span data-ttu-id="7c66a-175">Üyelik, OAuth ve SQL veritabanı ile güvenli bir ASP.NET MVC 5 uygulamasını Azure 'a dağıtma</span><span class="sxs-lookup"><span data-stu-id="7c66a-175">Deploy a Secure ASP.NET MVC 5 app with Membership, OAuth, and SQL Database to Azure</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)
- <span data-ttu-id="7c66a-176">Bir [yapılandırma](http://getglimpse.com/Docs/Configuration) , çalışma zamanı ilkesi, günlüğe kaydetme ve daha fazlasını yapılandırma üzerindeki bir disk sayfası.</span><span class="sxs-lookup"><span data-stu-id="7c66a-176">[Glimpse Configuration](http://getglimpse.com/Docs/Configuration) - Doc page on configuring tabs, runtime policy, logging and more.</span></span>
