---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
title: WebMatrix kullanarak Site yayımlama - ASP.NET Web sayfaları ile tanışın | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici, ASP.NET Web sayfaları ve Microsoft WebMatrix tanıtan öğretici kümesi son bölümünde bölümüdür. Bu, sitenizi t yayımlamak nasıl ele alınmaktadır...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 7e85c70e-1a88-4408-8b3d-29611c7713ed
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
msc.type: authoredcontent
ms.openlocfilehash: 49a841dbda183bf1d59153b83f694c9f517e0b94
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78633618"
---
# <a name="introducing-aspnet-web-pages---publishing-a-site-by-using-webmatrix"></a><span data-ttu-id="2f4c7-104">WebMatrix kullanarak Site yayımlama - ASP.NET Web sayfalarına giriş</span><span class="sxs-lookup"><span data-stu-id="2f4c7-104">Introducing ASP.NET Web Pages - Publishing a Site by Using WebMatrix</span></span>

<span data-ttu-id="2f4c7-105">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="2f4c7-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="2f4c7-106">Bu öğretici, ASP.NET Web sayfaları ve Microsoft WebMatrix tanıtan öğretici kümesi son bölümünde bölümüdür.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-106">This tutorial is the final installment in the tutorial set that introduces ASP.NET Web Pages and Microsoft WebMatrix.</span></span> <span data-ttu-id="2f4c7-107">Bu, diğerleri ile çalışabilmeniz için Internet'e sitenizi yayımlama açıklanır.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-107">It discusses how to publish your site to the Internet so that others can work with it.</span></span> <span data-ttu-id="2f4c7-108">[ASP.NET Web sayfaları siteleri Için tutarlı bir görünüm oluşturarak](https://go.microsoft.com/fwlink/?LinkId=251585)seriyi tamamladığınız varsayılır.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-108">It assumes you have completed the series through [Creating a Consistent Look for ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=251585).</span></span>
> 
> <span data-ttu-id="2f4c7-109">Kullanarak site yayımlama öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="2f4c7-109">You'll learn how to publish your site using:</span></span>
> 
> - <span data-ttu-id="2f4c7-110">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="2f4c7-110">Microsoft Azure</span></span>
> - <span data-ttu-id="2f4c7-111">Web barındırma şirketi</span><span class="sxs-lookup"><span data-stu-id="2f4c7-111">Web Hosting Company</span></span>

## <a name="about-publishing-your-site"></a><span data-ttu-id="2f4c7-112">Sitenizi yayımlama hakkında</span><span class="sxs-lookup"><span data-stu-id="2f4c7-112">About Publishing Your Site</span></span>

<span data-ttu-id="2f4c7-113">Şimdiye kadar test sayfalarınıza dahil olmak üzere yerel bir bilgisayardaki tüm iş yaptık.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-113">Up to now, you've done all your work on a local computer, including testing your pages.</span></span> <span data-ttu-id="2f4c7-114"><em>. Cshtml</em> sayfalarınızı çalıştırmak Için, WebMatrix içinde yerleşik olan Web sunucusunu kullandınız, yani IIS Express.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-114">To run your<em>.cshtml</em> pages, you've used the web server that's built into WebMatrix, namely IIS Express.</span></span> <span data-ttu-id="2f4c7-115">Ancak Elbette hiç dışında oluşturduğunuz site görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-115">But of course no one can see the site you've created except you.</span></span> <span data-ttu-id="2f4c7-116">Başkalarının siteniz ile çalışmak için Internet'te yayımlamak zorunda.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-116">To let others work with your site, you have to publish it to the Internet.</span></span>

<span data-ttu-id="2f4c7-117">Zaten bir genel Web sunucusuna erişiminiz yoksa, yayımlama, *bulut platformu* veya *barındırma sağlayıcısı*içeren bir hesabınız olması gerektiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-117">Unless you have access to a public web server already, publishing means that you have to have an account with a *cloud platform* or a *hosting provider*.</span></span> <span data-ttu-id="2f4c7-118">Microsoft Azure gibi bir bulut platformu, uygulamalarınız için isteğe bağlı altyapı sağlar.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-118">A cloud platform, such as Microsoft Azure, provides on-demand infrastructure for your applications.</span></span> <span data-ttu-id="2f4c7-119">Bir barındırma sağlayıcısı, kiraya ve genel olarak erişilebilir web sunucuları sahip olan bir şirket alanı siteniz için ' dir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-119">A hosting provider is a company that owns publicly accessible web servers and that will rent you space for your site.</span></span> <span data-ttu-id="2f4c7-120">Barındırma planları aylık birkaç lira karşılığında dosyasından çalıştırın (veya hatta ücretsiz) ABD Doları aylık yüksek hacimli ticari Web siteleri için yüzlerce küçük sitelere için.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-120">Hosting plans run from a few dollars a month (or even free) for small sites to many hundreds of dollars a month for high-volume commercial websites.</span></span>

> [!NOTE]
> <span data-ttu-id="2f4c7-121">Bir genel web sunucusuna internet hizmet evde almak için kullandığınız internet hizmet sağlayıcısı (ISS) aracılığıyla erişimi olabilir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-121">You might have access to a public web server via the internet service provider (ISP) that you use to get internet service at home.</span></span> <span data-ttu-id="2f4c7-122">Ancak, barındırma sağlayıcınızda ASP.NET Web Pages desteklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-122">However, your hosting provider must support ASP.NET Web Pages.</span></span> <span data-ttu-id="2f4c7-123">Birçok ISS yoktur, ancak bu her zaman denetimi değerindedir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-123">Many ISPs don't, but it's always worth checking.</span></span>

<span data-ttu-id="2f4c7-124">Bu öğreticide, biz, nasıl yayımlamak genel bir bakış sunacağız.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-124">In this tutorial, we'll give you an overview of how to publish.</span></span> <span data-ttu-id="2f4c7-125">Her şey için tam Ayrıntılar sağlayan pratik değildir, çünkü işlemi, her bir barındırma sağlayıcısı için biraz farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-125">It's not practical to provide exact details for everything, because the process differs a bit for every hosting provider.</span></span> <span data-ttu-id="2f4c7-126">Ancak, işlemin nasıl çalıştığına ilişkin bir fikir elde edersiniz.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-126">But you'll get a good idea of how the process works.</span></span>

<span data-ttu-id="2f4c7-127">Bu öğreticide, dört bölüm içerir:</span><span class="sxs-lookup"><span data-stu-id="2f4c7-127">This tutorial contains four sections:</span></span>

1. [<span data-ttu-id="2f4c7-128">Varsayılan sayfayı ayarlama</span><span class="sxs-lookup"><span data-stu-id="2f4c7-128">Setting up the default page</span></span>](#defaultpage)
2. <span data-ttu-id="2f4c7-129">Yayımlama (aşağıdakilerden birini seçin)</span><span class="sxs-lookup"><span data-stu-id="2f4c7-129">Publishing (choose one of the following)</span></span>  
 <span data-ttu-id="2f4c7-130">a.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-130">a.</span></span> [<span data-ttu-id="2f4c7-131">Sitenizi Microsoft Azure yayımlama</span><span class="sxs-lookup"><span data-stu-id="2f4c7-131">Publishing Your Site to Microsoft Azure</span></span>](#azure)  
 <span data-ttu-id="2f4c7-132">b.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-132">b.</span></span> [<span data-ttu-id="2f4c7-133">Sitenizi bir Web barındırma şirketine yayımlama</span><span class="sxs-lookup"><span data-stu-id="2f4c7-133">Publishing Your Site to a Web Hosting Company</span></span>](#host)
3. [<span data-ttu-id="2f4c7-134">Canlı siteyi güncelleştirme: yeniden yayımlama</span><span class="sxs-lookup"><span data-stu-id="2f4c7-134">Updating the Live Site: Republishing</span></span>](#update)

<a id="defaultpage"></a>
## <a name="setting-up-the-default-page"></a><span data-ttu-id="2f4c7-135">Varsayılan sayfayı ayarlama</span><span class="sxs-lookup"><span data-stu-id="2f4c7-135">Setting up the default page</span></span>

<span data-ttu-id="2f4c7-136">Bir kullanıcının web siteniz için temel adresi gittiğinde, siteniz için varsayılan sayfa kullanıcıya görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-136">When a user navigates to the base address for your web site, the default page for your site is displayed to the user.</span></span> <span data-ttu-id="2f4c7-137">Örneğin, *default. htm* , `www.contoso.com`site için varsayılan sayfa olarak ayarlandığında, `www.contoso.com` 'ye gidildiğinde `www.contoso.com/Default.htm`gezinme ile aynı olur.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-137">For example, when *Default.htm* is set as the default page for the site at `www.contoso.com`, then navigating to `www.contoso.com` is the same as navigating to `www.contoso.com/Default.htm`.</span></span>

<span data-ttu-id="2f4c7-138">Şu anda siteniz varsayılan sayfa olarak **default. cshtml** kullanır.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-138">Currently, your site uses **Default.cshtml** as the default page.</span></span> <span data-ttu-id="2f4c7-139">Bu sayfada varsayılan sayfanız için uygundur, ancak boş bir sayfa görüntülemek için Bu öğreticide, herhangi bir içerik söz konusu sayfaya eklemediniz.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-139">This page is fine for your default page, but in this tutorial you have not added any content to that page so it would display a blank page.</span></span> <span data-ttu-id="2f4c7-140">Default.cshtml açın ve içeriğini aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-140">Open Default.cshtml and replace the content with the following code.</span></span>

[!code-cshtml[Main](publishing/samples/sample1.cshtml)]

<span data-ttu-id="2f4c7-141">Artık sitenizin yayın için hazırdır.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-141">Now your site is ready for publication.</span></span> <span data-ttu-id="2f4c7-142">İlk olarak, sitesinin Azure'a nasıl dağıtılacağı ve bir web barındırma şirketi dağıtma görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-142">First, you will see how to deploy the site to Azure, and then how to deploy it to a web hosting company.</span></span> <span data-ttu-id="2f4c7-143">Her iki seçeneği çalışır ve web siteniz için yalnızca dağıtım seçeneklerinden birini izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-143">Either option works for your web site, and you only need to follow one of the deployment options.</span></span>

<a id="azure"></a>
## <a name="publishing-your-site-to-microsoft-azure"></a><span data-ttu-id="2f4c7-144">Sitenizi Microsoft Azure'a yayımlama</span><span class="sxs-lookup"><span data-stu-id="2f4c7-144">Publishing Your Site to Microsoft Azure</span></span>

<span data-ttu-id="2f4c7-145">Bu öğreticide ilk sitenizi Microsoft Azure'a dağıtmak nasıl gösterilecek.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-145">This tutorial will first show you how to deploy your site to Microsoft Azure.</span></span> <span data-ttu-id="2f4c7-146">Bir Microsoft hesabıyla oturum açarak, Azure'da en fazla 10 ücretsiz siteleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-146">By signing in with a Microsoft account, you can create up to 10 free sites on Azure.</span></span> <span data-ttu-id="2f4c7-147">Bu ücretsiz siteleri sitelerinizi test etmek için kullanışlı bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-147">These free sites provide a convenient way to test your sites.</span></span> <span data-ttu-id="2f4c7-148">Bu örnek site daha sonra tüm ücretsiz sitelerinizden kullanarak önlemek için her zaman silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-148">You can always delete this example site later to avoid using all of your free sites.</span></span> <span data-ttu-id="2f4c7-149">Yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-149">You can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2f4c7-150">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span><span class="sxs-lookup"><span data-stu-id="2f4c7-150">For details, see [Azure Free Trial](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span>

<span data-ttu-id="2f4c7-151">WebMatrix şeridinde **Yayımla** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-151">In the WebMatrix ribbon, click the **Publish** button.</span></span>

![WebMatrix şeridinde 'Publish' düğmesi](publishing/_static/image1.png)

<span data-ttu-id="2f4c7-153">**Sitenizi Yayımla** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-153">The **Publish Your Site** dialog box is displayed.</span></span> <span data-ttu-id="2f4c7-154">Microsoft hesabı oturumunuzu açmadıysanız, iletişim kutusunda **Azure ile çalışmaya başlama** bağlantısı bulunur.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-154">If you have not signed in to your Microsoft account, the dialog box will contain a **Get started with Azure** link.</span></span> <span data-ttu-id="2f4c7-155">Bu bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-155">Click this link.</span></span>

![Sitenizi yayımlayın](publishing/_static/image2.png)

<span data-ttu-id="2f4c7-157">Bir Microsoft hesabı ile oturum açmanızdan değil ise, yeniden oturum açmak için bir fırsat sunulur.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-157">If you have not signed in to a Microsoft account, you are again given the opportunity to sign in.</span></span> <span data-ttu-id="2f4c7-158">Bir Microsoft hesabına sitenizi azure'da yayımlamak için oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-158">You must sign in to a Microsoft account to publish your site on Azure.</span></span>

![Oturum Açma](publishing/_static/image3.png)

<span data-ttu-id="2f4c7-160">Microsoft hesabınızda oturum açtıktan sonra iletişim kutusu, Azure'da yeni bir site oluşturmak veya mevcut sitelerinizi azure'da birine bağlanmak için bağlantılar içerir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-160">After signing in to your Microsoft account, the dialog box contains links to create a new site on Azure or connect to one of your existing sites on Azure.</span></span>

![Yeni Site oluşturma](publishing/_static/image4.png)

<span data-ttu-id="2f4c7-162">**Yeni site oluştur**' u seçin.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-162">Select **Create a new site**.</span></span>

<span data-ttu-id="2f4c7-163">Projenizi **Webpagesfilmlerini**olarak adlandırdıysanız sitenizin varsayılan adı **webpagesmovies.azurewebsites.net**olacaktır.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-163">If you named your project **WebPagesMovies**, the default name for your site will be **webpagesmovies.azurewebsites.net**.</span></span> <span data-ttu-id="2f4c7-164">Büyük olasılıkla bu varsayılan adı kullanılamıyor, kırmızı bir ünlem işareti tarafından belirtildiği şekilde.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-164">This default name is most likely not available, as indicated by the red exclamation mark.</span></span>

![Varsayılan Web sitesi adı](publishing/_static/image5.png)

<span data-ttu-id="2f4c7-166">Kullanılabilir olan bir site adı değiştirin ve konumunuz yakın bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-166">Change the site name to something that is available, and select a location that is close to your location.</span></span>

![Değiştirilen site adı](publishing/_static/image6.png)

<span data-ttu-id="2f4c7-168">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-168">Click **OK**.</span></span>

<span data-ttu-id="2f4c7-169">WebMatrix performss sunucu siteniz ile uyumlu olup olmadığını belirlemek için bir test.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-169">WebMatrix performss a test to determine if the server is compatible with your site.</span></span>

![Uyumluluk testi](publishing/_static/image7.png)

<span data-ttu-id="2f4c7-171">**Devam**'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-171">Select **Continue**.</span></span>

<span data-ttu-id="2f4c7-172">Uyumluluk testinin sonuçları görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-172">The results of the compatibility test are displayed.</span></span>

![Uyumluluk sonucu](publishing/_static/image8.png)

<span data-ttu-id="2f4c7-174">**Devam**'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-174">Select **Continue**.</span></span>

<span data-ttu-id="2f4c7-175">WebMatrix sitede yayınlanan veritabanları ve dosyaları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-175">WebMatrix displays the files and databases that will be published to the site.</span></span> <span data-ttu-id="2f4c7-176">Bu sitenin yayımladığınız ilk kez olduğundan, tüm dosyalar listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-176">Since this is the first time you are publishing the site, all of the files are listed.</span></span> <span data-ttu-id="2f4c7-177">Yayımlanmaya hazır olmayan bir dosya işaretini kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-177">You can uncheck a file that is not ready to be published.</span></span> <span data-ttu-id="2f4c7-178">Sonraki yayınlarda yalnızca değişen dosyaları görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-178">In the subsequent publications, only the files that have changed will be displayed.</span></span> <span data-ttu-id="2f4c7-179">Bkz. [canlı siteyi güncelleştirme: yeniden yayımlama](#update).</span><span class="sxs-lookup"><span data-stu-id="2f4c7-179">See [Updating the Live Site: Republishing](#update).</span></span>

![Yayımlama önizlemesi](publishing/_static/image9.png)

<span data-ttu-id="2f4c7-181">**Devam**'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-181">Select **Continue**.</span></span>

<span data-ttu-id="2f4c7-182">Site Azure'a dağıtıldıktan sonra dağıtımın tamamlandığını bir ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-182">After the site has been deployed to Azure, a message is displayed that indicates the deployment has completed.</span></span>

![Yayımlama tamamlandı](publishing/_static/image10.png)

<span data-ttu-id="2f4c7-184">Sitenizi ve veritabanınızı Azure'a yayımlandı ve genel kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-184">Your site and database have been published to Azure, and are now available to the public.</span></span> <span data-ttu-id="2f4c7-185">Yayımlama tamamlandı ve artık dağıtılan sitenizi görürsünüz belirten iletiyi bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-185">Click the link in the message indicating publishing has completed, and you will now see your deployed site.</span></span> <span data-ttu-id="2f4c7-186">Siz veya Internet erişimi olan herkes, ekleyin veya veritabanında kayıt değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-186">You or anyone with Internet access can add or modify records in the database.</span></span>

![](publishing/_static/image11.png)

<a id="host"></a>
## <a name="publishing-your-site-to-a-web-hosting-company"></a><span data-ttu-id="2f4c7-187">Barındırma şirketi bir Web sitenizi yayımlama</span><span class="sxs-lookup"><span data-stu-id="2f4c7-187">Publishing Your Site to a Web Hosting Company</span></span>

<span data-ttu-id="2f4c7-188">Azure'a yayımlama değil karar verirseniz, bunun yerine bir web barındırma şirketi, sitenizi yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-188">If you decide to not publish to Azure, you can instead publish your site to a web hosting company.</span></span>

<span data-ttu-id="2f4c7-189">**Web barındırma 'Yı bul** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-189">Click the **Find web hosting** link.</span></span>

![Yayımlama Ayarları iletişim kutusunda 'web barındırma Bul' düğmesi](publishing/_static/image12.png)

<span data-ttu-id="2f4c7-191">ASP.NET'i destekleyen barındırma sağlayıcılarının listeleyen Microsoft sitesi bir sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-191">You go to a page on the Microsoft site that lists hosting providers that support ASP.NET.</span></span>

![Barındırma sağlayıcıları listeler Microsoft sitesinde sayfası](publishing/_static/image13.png)

<span data-ttu-id="2f4c7-193">Kuşkusuz, artık tam olarak uzun vadeli gerektirebilir barındırma özellikleri anlamak zor olabilir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-193">Obviously, it can be difficult to know now exactly what hosting features you might require over the long term.</span></span> <span data-ttu-id="2f4c7-194">Birkaç göz önünde bulundurulması gerekenler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="2f4c7-194">Here are a couple of things to consider:</span></span>

- <span data-ttu-id="2f4c7-195">WebPagesMovies site amacı doğrultusunda, genellikle ek maliyetler SQL Server için ayrı bir eklenti olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-195">For purposes of the WebPagesMovies site, you don't have to have a separate add-on for SQL Server, which often costs extra.</span></span> <span data-ttu-id="2f4c7-196">Sitenizdeki, kendi içinde olduğu SQL Server Compact Edition kullanıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-196">In your site, you're using SQL Server Compact Edition, which is self-contained.</span></span> <span data-ttu-id="2f4c7-197">Ancak, bazı gelecek Web sitesi iş yaptığınız için SQL Server erişimi gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-197">However, you might need SQL Server access for some future website work you do.</span></span> <span data-ttu-id="2f4c7-198">Yapabileceğiniz düşünüyorsanız, SQL Server özelliği daha sonra ekleyebilirsiniz emin olun.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-198">If you think you might, make sure that you can add SQL Server capability later.</span></span>
- <span data-ttu-id="2f4c7-199">Barındırma sağlayıcısı, Web dağıtımı yayımlama Protokolü destekleyip desteklemediğini kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-199">Check whether the hosting provider supports the Web Deploy publishing protocol.</span></span> <span data-ttu-id="2f4c7-200">FTP protokolünü kullanarak yayımlayabilirsiniz ancak Web dağıtımı kullanabilmeniz daha uygundur.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-200">You can publish by using FTP protocol, but it's more convenient to use Web Deploy.</span></span>

<span data-ttu-id="2f4c7-201">Bazı siteler ücretsiz deneme süresi sunar.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-201">Some sites offer a free trial period.</span></span> <span data-ttu-id="2f4c7-202">Ücretsiz deneme yayımlama denemek için iyi bir yoludur ve basılı barındırma hala denemeler WebMatrix ve ASP.NET Web sayfaları ile.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-202">A free trial is a good way to try publishing and hosting while you're still experimenting with WebMatrix and ASP.NET Web Pages.</span></span>

<span data-ttu-id="2f4c7-203">İstediğiniz birini seçin.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-203">Pick one that you like.</span></span> <span data-ttu-id="2f4c7-204">Bu öğretici için şu öğreticiyi kalıyorduk, ancak bu şirket birkaç ay boyunca ücretsiz olan bir site konak kişilere bir promosyon olduğundan DiscountASP.NET, seçtik.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-204">For this tutorial, we selected DiscountASP.NET, because while we were creating the tutorial, that company had a promotion that let people host a site free for a few months.</span></span>

> [!NOTE]
> <span data-ttu-id="2f4c7-205">Bu öğretici için bir barındırma sağlayıcısının kendi, şirketin bir onay diğer yorumlanacağını olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-205">Our choice of a hosting provider for this tutorial shouldn't be interpreted as an endorsement of that company over any other.</span></span> <span data-ttu-id="2f4c7-206">Ancak bir çizim için çekme vardı ve yayımlama için ASP.NET Web sayfaları ve Web dağıtımı protokolünü destekleyen birçok şirket, DiscountASP.NET biridir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-206">But we had to pick one for illustration, and DiscountASP.NET is one of the many companies that supports ASP.NET Web Pages and the Web Deploy protocol for publishing.</span></span>

<span data-ttu-id="2f4c7-207">Genellikle, bir barındırma sağlayıcısında açtıktan sonra şirket, bir kullanıcı adı ve parola, web sunucusu ve benzeri URL'sini içeren bir e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-207">Typically, after you've signed up with the hosting provider, the company sends you an email that contains a user name and password, the URL of the web server, and so on.</span></span> <span data-ttu-id="2f4c7-208">Barındırma şirketinin Web dağıtımı protokolünü destekliyorsa, içeren bir dosya yayımlama ayarları veya bir indirme izin gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-208">If the hosting company supports Web Deploy protocol, they might send you a file that contains publish settings, or let you download one.</span></span> <span data-ttu-id="2f4c7-209">Yayımlama ayarları dosyası işlemi sizin için basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-209">A publish settings file simplifies the process for you.</span></span>

<span data-ttu-id="2f4c7-210">Kaydolup yayımlamaya hazırsanız, WebMatrix şeridinde **Yayımla** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-210">When you've signed up and are ready to publish, click the **Publish** button in the WebMatrix ribbon.</span></span> <span data-ttu-id="2f4c7-211">**Ayarları Yayımla** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-211">The **Publish Settings** dialog box is displayed.</span></span>

<span data-ttu-id="2f4c7-212">Barındırma sağlayıcısı size bir yayımlama ayarları dosyası gönderdiyse, **Yayımlama ayarlarını Içeri aktar** bağlantısına tıklayın ve dosyayı içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-212">If the hosting provider sent you a publish settings file, click the **Import publish settings** link and import the file.</span></span> <span data-ttu-id="2f4c7-213">Yayımlama ayarları dosyası yoksa, barındırma şirket e-posta ile gönderilen değerler kullanılarak alanları doldurun.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-213">If you don't have a publish settings file, fill in the fields by using the values that the hosting company sent you in email.</span></span> <span data-ttu-id="2f4c7-214">İşte **yayınlama ayarları** iletişim kutusu işiniz bittiğinde şöyle görünebilir:</span><span class="sxs-lookup"><span data-stu-id="2f4c7-214">Here's what the **Publish Settings** dialog box might look like when you're done:</span></span>

![Yayımlama ayarlarını 'Yayımlama Ayarları' iletişim kutusunda doldurulur](publishing/_static/image14.png)

<span data-ttu-id="2f4c7-216">**Bağlantıyı doğrula**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-216">Click **Validate Connection**.</span></span> <span data-ttu-id="2f4c7-217">Her şey tamam ise, iletişim kutusu **başarıyla bağlanır**, bu da barındırma sağlayıcısının sunucusuyla iletişim kurabildiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-217">If everything is ok, the dialog box reports **Connected successfully**, which means it can communicate with the hosting provider's server.</span></span>

![Başarılı iletisi, yayımlama ayarları doğru](publishing/_static/image15.png)

<span data-ttu-id="2f4c7-219">Bir sorun varsa, WebMatrix sorunun ne olduğunu söylemek için en iyi şekilde yapar:</span><span class="sxs-lookup"><span data-stu-id="2f4c7-219">If there's a problem, WebMatrix does its best to tell you what the problem is:</span></span>

![Yayımlama ayarları ile ilgili bir sorun varsa hata iletisi](publishing/_static/image16.png)

<span data-ttu-id="2f4c7-221">Ayarlarınızı kaydetmek için **Kaydet** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-221">Click **Save** to save your settings.</span></span> <span data-ttu-id="2f4c7-222">WebMatrix, onu doğru barındırma siteyle iletişim kurabildiğinden emin olmak için bir test gerçekleştirmek sunar:</span><span class="sxs-lookup"><span data-stu-id="2f4c7-222">WebMatrix offers to perform a test to make sure that it can communicate correctly with the hosting site:</span></span>

![İleti yayımlama işleminin bir test gerçekleştirmek teklifi](publishing/_static/image17.png)

<span data-ttu-id="2f4c7-224">**Evet**'i tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-224">Click **Yes**.</span></span> <span data-ttu-id="2f4c7-225">WebMatrix, barındırma sağlayıcısının bazı örnek dosyalarını yükler.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-225">WebMatrix uploads some sample files to the hosting provider.</span></span> <span data-ttu-id="2f4c7-226">WebMatrix, uyumluluk testi tamamlandığında, sonuçları raporları:</span><span class="sxs-lookup"><span data-stu-id="2f4c7-226">When the compatibility test is done, WebMatrix reports the results:</span></span>

![Yayımlama test sonuçları](publishing/_static/image18.png)

<span data-ttu-id="2f4c7-228">Çalışmaya hazırsanız, **devam** ' a tıklayarak yayımlama işlemini gerçek için başlatın.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-228">If you're ready to go, go ahead and click **Continue** to start the publish process for real.</span></span> <span data-ttu-id="2f4c7-229">WebMatrix, hangi dosyalar sitenizdeki ve ana bilgisayar sunucusunda (şu anda hiçbiri) durumda ve yayımlama işlemi, bir önizleme sunar kullanıma rakamları:</span><span class="sxs-lookup"><span data-stu-id="2f4c7-229">WebMatrix figures out what files are in your site and are already on the host server (right now, none) and gives you a preview of the publish process:</span></span>

![Yayımlama işlemi yükleyeceği hangi dosyaların önizlemesini](publishing/_static/image19.png)

<span data-ttu-id="2f4c7-231">Yayımlanacak dosyaların listesi, *filmler. cshtml*gibi oluşturduğunuz Web sayfalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-231">The list of files to publish includes the web pages that you've created like *Movies.cshtml*.</span></span> <span data-ttu-id="2f4c7-232">Bu liste, dosyaları, yüklemiş olduğunuz için Yardımcıları veritabanınız için SQL Server Compact Edition'ı çalıştırın ve benzeri için dosyaları da içerir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-232">The list also includes files for helpers that you've installed, the files to run SQL Server Compact Edition for your database, and so on.</span></span> <span data-ttu-id="2f4c7-233">Sonuç olarak, ilk yayımlama işlemi olabilmektedir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-233">As a result, the initial publish process can be substantial.</span></span>

<span data-ttu-id="2f4c7-234">**Devam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-234">Click **Continue**.</span></span> <span data-ttu-id="2f4c7-235">WebMatrix, dosyalar, barındırma sağlayıcısının sunucusuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-235">WebMatrix copies your files to the hosting provider's server.</span></span> <span data-ttu-id="2f4c7-236">İşlem tamamlandığında, sonuçları durum çubuğunda bildirilir:</span><span class="sxs-lookup"><span data-stu-id="2f4c7-236">When it's done, the results are reported in the status bar:</span></span>

![Yayımlama işlemi başarıyla tamamlandığında durum çubuğu iletisi](publishing/_static/image20.png)

<span data-ttu-id="2f4c7-238">Sitenizin Canlı görmek için durum çubuğundaki bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-238">To see your live site, click the link in the status bar.</span></span> <span data-ttu-id="2f4c7-239">URL 'ye *film* ekleyin ve oluşturduğunuz *filmler. cshtml* dosyasını görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="2f4c7-239">Add *Movies* to the URL, and you'll see the *Movies.cshtml* file that you created:</span></span>

![Filmler sayfasını gösteren Canlı site](publishing/_static/image21.png)

<a id="update"></a>
## <a name="updating-the-live-site-republishing"></a><span data-ttu-id="2f4c7-241">Canlı siteyi güncelleştirmeden: yeniden yayımlama</span><span class="sxs-lookup"><span data-stu-id="2f4c7-241">Updating the Live Site: Republishing</span></span>

<span data-ttu-id="2f4c7-242">Sitenizi yayımladıktan sonra (Azure 'a veya bir Web barındırma şirketine), bilgisayarınızın sürümü ve Hizmet sağlayıcısındaki sürüm &mdash; iki kopyası vardır.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-242">Once you've published your site (to either Azure or a web hosting company), there are two copies of it &mdash; the version on your computer and the version on the service provider.</span></span> <span data-ttu-id="2f4c7-243">Site geliştirmeye devam isteyebilirsiniz (başka bir şey varsa sonraki öğretici kümesinin bir parçası olarak).</span><span class="sxs-lookup"><span data-stu-id="2f4c7-243">You'll probably want to continue developing the site (if nothing else, as part of the next tutorial set).</span></span> <span data-ttu-id="2f4c7-244">Bunu yaptığınızda, değişiklikler hizmet sağlayıcısına bilgisayarınızdan kopyalanması için sitenizi yeniden yayımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-244">When you do, you have to republish your site in order to copy changes from your computer to the service provider.</span></span> <span data-ttu-id="2f4c7-245">WebMatrix yayımlama işleminde, sitenizde hangi dosyaların değiştiğini belirlemek ve yalnızca bu dosyaları yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-245">The publish process in WebMatrix can determine what files have changed on your site and publish just those files.</span></span>

<span data-ttu-id="2f4c7-246">Yeniden yayımmadan nasıl çalıştığını görmek için, *filmler. cshtml* sitesini açın, küçük bir değişiklik yapın ve dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-246">To see how republishing works, open the *Movies.cshtml* site, make some small change, and then save the file.</span></span> <span data-ttu-id="2f4c7-247">Örneğin, başlığı `Movies - Updated`olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-247">For example, change the title to `Movies - Updated`.</span></span>

<span data-ttu-id="2f4c7-248">Şeritteki **Yayımla** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-248">Click the **Publish** button in the ribbon.</span></span> <span data-ttu-id="2f4c7-249">WebMatrix, neyin değiştirilir ve bu yayımlayacak dosyaların önizlemesini belirler.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-249">WebMatrix determines what's changed and shows you a preview of the files it will publish.</span></span>

![Yeniden yayımlanması için hazır dosyalar değiştirilmiş gösteren 'Yayımla' iletişim kutusu](publishing/_static/image22.png)

> [!IMPORTANT] 
> 
> <span data-ttu-id="2f4c7-251">Varsayılan olarak, WebMatrix veritabanını ( *. sdf* dosyası) yalnızca siteyi ilk kez yayımladığınızda yayımlar.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-251">By default, WebMatrix publishes your database (*.sdf* file) only the first time you publish the site.</span></span> <span data-ttu-id="2f4c7-252">Sitenizi yayımlanır ve kişiler ile Web sitesi etkileşim sonra canlı site veritabanında sitenin gerçek veriler genellikle vardır.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-252">Once your site is published and people are interacting with the website, the database on the live site typically has the site's real data.</span></span> <span data-ttu-id="2f4c7-253">Bilgisayarınızda genellikle test verilerini içeren *. sdf* dosyası ile canlı veritabanının üzerine yazılmamaya dikkat etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-253">You have to be very careful not to overwrite the live database with the *.sdf* file that's on your computer, which usually contains only test data.</span></span> <span data-ttu-id="2f4c7-254">Uyarı **yayımlamanın her türlü uzak veritabanının üzerine yazılmasına**neden olduğunu ve *webpagesfilmlerini. sdf* onay kutusunun neden varsayılan olarak temizlendiğinizi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-254">That's why you see the warning **Publishing will overwrite any remote databases**, and why the check box for *WebPagesMovies.sdf* is cleared by default.</span></span>

<span data-ttu-id="2f4c7-255">**Devam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-255">Click **Continue**.</span></span> <span data-ttu-id="2f4c7-256">WebMatrix, değiştirilmiş dosyalar yayımlar ve yayımladığınız ilk kez yaptığınız gibi bir başarı iletisi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-256">WebMatrix publishes the changed files and shows you a success message, like it did the first time you published.</span></span>

<span data-ttu-id="2f4c7-257">Canlı site (tıklayabilirsiniz başarılı iletisi bağlantıdaki hala gösteriliyorsa) gidin ve değişikliğinizi yayımlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-257">Go to the live site (you can click the link in the success message if it's still showing) and verify that your change has been published.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="2f4c7-258">**Dosyaları uzaktan Düzenle**</span><span class="sxs-lookup"><span data-stu-id="2f4c7-258">**Editing Files Remotely**</span></span>
> 
> <span data-ttu-id="2f4c7-259">Sitenizi değiştirme ve ardından yeniden yayımlanması için alternatif olarak, WebMatrix uzak dosyaları doğrudan düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-259">As an alternative to changing your site and then republishing, you can edit remote files directly in WebMatrix.</span></span> <span data-ttu-id="2f4c7-260">Bu senaryoda, hizmet sağlayıcısına bir dosya açın ve bir kopyasını düzenlemek, Webmatrix'i yükler.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-260">In this scenario, you open a file that's on the service provider, and WebMatrix downloads a copy of it for you to edit.</span></span> <span data-ttu-id="2f4c7-261">Her dosyayı kaydettiğinizde, WebMatrix değişiklikleri siteye gönderir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-261">Every time you save the file, WebMatrix sends the changes to the site.</span></span>
> 
> <span data-ttu-id="2f4c7-262">Uzaktan düzenleme, Canlı sitenize değişiklik yapmak için kolay bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-262">Remote editing is an easy way to make changes to your live site.</span></span> <span data-ttu-id="2f4c7-263">Ancak, böylece yaptığınız değişiklikler sitenizde yerel dosyalarla eşitlenmedi.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-263">However, the changes you make this way aren't synchronized with the files in your local site.</span></span> <span data-ttu-id="2f4c7-264">Yerel dosyaları uzak siteyle eşitlemek için Uzak dosyaları indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-264">To synchronize the local files with the remote site, you can download the remote files.</span></span> <span data-ttu-id="2f4c7-265">Bu işlem, yayımlama gibi dışında tersten çalışır.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-265">This process works much like publishing, except in reverse.</span></span>
> 
> <span data-ttu-id="2f4c7-266">Uzaktan düzenleme ve Uzaktan Yükleme özelliklerine WebMatrix hakkında burada fazla açıklanmaktadır olmaz.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-266">We won't describe more about the remote-editing and remote-download facilities of WebMatrix here.</span></span> <span data-ttu-id="2f4c7-267">Bunlar birden çok kişinin aynı sitede farklı bilgisayarlarda çalışması varsa oldukça kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-267">They're quite useful if multiple people have to work on the same site on different computers.</span></span> <span data-ttu-id="2f4c7-268">Daha fazla bilgi için bkz. [WebMatrix 2 Beta Ile uzak site yayımlama ve düzenleme](https://go.microsoft.com/fwlink/?LinkId=251591).</span><span class="sxs-lookup"><span data-stu-id="2f4c7-268">For more information, see [Publish and Edit a Remote Site with WebMatrix 2 Beta](https://go.microsoft.com/fwlink/?LinkId=251591).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2f4c7-269">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2f4c7-269">Additional Resources</span></span>

- <span data-ttu-id="2f4c7-270">[ASP.net WebMatrix ASP.NET Web sayfaları Forumu](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages), sorularınızı göndermek ve yanıt almak için harika bir yerdir.</span><span class="sxs-lookup"><span data-stu-id="2f4c7-270">[ASP.NET WebMatrix ASP.NET Web Pages forum](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages), a great place to post questions and get answers.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="2f4c7-271">Öncekini</span><span class="sxs-lookup"><span data-stu-id="2f4c7-271">Previous</span></span>](layouts.md)
