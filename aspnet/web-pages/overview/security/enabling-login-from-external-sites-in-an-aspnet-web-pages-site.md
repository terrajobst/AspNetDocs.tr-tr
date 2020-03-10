---
uid: web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
title: ASP.NET Web Pages (Razor) sitesindeki dış siteleri kullanarak oturum açma | Microsoft Docs
author: Rick-Anderson
description: Bu makalede, Facebook, Google, Twitter, Yahoo ve diğer siteleri kullanarak ASP.NET Web Pages (Razor) sitesinde oturum açma ve diğer bir deyişle, nasıl destekleneceği açıklanır.
ms.author: riande
ms.date: 02/21/2014
ms.assetid: ef852096-a5bf-47b3-9945-125cde065093
msc.legacyurl: /web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 860b75422c3df1d191ed861344963bfc19270e8f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638756"
---
# <a name="logging-in-using-external-sites-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="d3166-103">Bir ASP.NET Web Pages (Razor) sitesinde dış siteleri kullanarak oturum açma</span><span class="sxs-lookup"><span data-stu-id="d3166-103">Logging In Using External Sites in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="d3166-104">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="d3166-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="d3166-105">Bu makalede, Facebook, Google, Twitter, Yahoo ve diğer siteleri kullanarak ASP.NET Web sayfaları (Razor) sitenizde oturum açma, diğer bir deyişle, sitenizdeki OAuth ve OpenID desteği açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d3166-105">This article explains how to log in to your ASP.NET Web Pages (Razor) site using Facebook, Google, Twitter, Yahoo, and other sites — that is, how to support OAuth and OpenID in your site.</span></span>
> 
> <span data-ttu-id="d3166-106">Öğrenecekleriniz:</span><span class="sxs-lookup"><span data-stu-id="d3166-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="d3166-107">WebMatrix Başlatıcı site şablonunu kullandığınızda diğer sitelerden oturum açmayı etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="d3166-107">How to enable login from other sites when you use the WebMatrix Starter Site template.</span></span>
> 
> <span data-ttu-id="d3166-108">Bu, makalesinde sunulan ASP.NET özelliğidir:</span><span class="sxs-lookup"><span data-stu-id="d3166-108">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="d3166-109">`OAuthWebSecurity` Yardımcısı.</span><span class="sxs-lookup"><span data-stu-id="d3166-109">The `OAuthWebSecurity` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="d3166-110">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="d3166-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="d3166-111">ASP.NET Web sayfaları (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="d3166-111">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="d3166-112">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="d3166-112">WebMatrix 3</span></span>

<span data-ttu-id="d3166-113">ASP.NET Web sayfaları, [OAuth](http://oauth.net/) ve [OpenID](http://openid.net/) sağlayıcıları için destek içerir.</span><span class="sxs-lookup"><span data-stu-id="d3166-113">ASP.NET Web Pages includes support for [OAuth](http://oauth.net/) and [OpenID](http://openid.net/) providers.</span></span> <span data-ttu-id="d3166-114">Bu sağlayıcıları kullanarak, kullanıcıların Facebook, Twitter, Microsoft ve Google 'daki mevcut kimlik bilgilerini kullanarak sitenizde oturum açmasına izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3166-114">Using these providers, you can let users log into your site using their existing credentials from Facebook, Twitter, Microsoft, and Google.</span></span> <span data-ttu-id="d3166-115">Örneğin, Facebook hesabı kullanarak oturum açmak için kullanıcılar yalnızca bir Facebook simgesi seçerek bunları Kullanıcı bilgilerini girdikleri Facebook oturum açma sayfasına yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="d3166-115">For example, to log in using a Facebook account, users can just choose a Facebook icon, which redirects them to the Facebook login page where they enter their user information.</span></span> <span data-ttu-id="d3166-116">Daha sonra Facebook oturum açma bilgilerini sitenizdeki hesabıyla ilişkilendirebilirler.</span><span class="sxs-lookup"><span data-stu-id="d3166-116">They can then associate the Facebook login with their account on your site.</span></span> <span data-ttu-id="d3166-117">Web sayfaları üyelik özellikleri için ilgili geliştirmelerden bazıları, kullanıcıların Web sitenizdeki tek bir hesapla birden çok oturum açma işlemi (sosyal ağ sitelerine ait oturumlar dahil) ilişkilendirebilirler.</span><span class="sxs-lookup"><span data-stu-id="d3166-117">A related enhancement to the Web Pages membership features is that users can associate multiple logins (including logins from social networking sites) with a single account on your website.</span></span>

<span data-ttu-id="d3166-118">Bu görüntüde, bir kullanıcının bir dış hesapla oturum açmasını etkinleştirmek üzere Facebook, Twitter, Google veya Microsoft simgesini seçebildiği **Başlatıcı site** şablonundan oturum açma sayfası gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="d3166-118">This image shows the Login page from the **Starter Site** template, where a user can choose a Facebook, Twitter, Google or Microsoft icon to enable logging in with an external account:</span></span>

![dış sağlayıcılar](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image1.png)

<span data-ttu-id="d3166-120">**Başlangıç site** şablonunda birkaç satır kod satırını kaldırarak OAuth ve OpenID üyeliğini etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3166-120">You can enable OAuth and OpenID membership by uncommenting a few lines of code in the **Starter Site** template.</span></span> <span data-ttu-id="d3166-121">OAuth ve OpenID sağlayıcılarıyla çalışmak için kullandığınız yöntemler ve Özellikler `WebMatrix.Security.OAuthWebSecurity` sınıftır.</span><span class="sxs-lookup"><span data-stu-id="d3166-121">The methods and properties you use to work with the OAuth and OpenID providers are in the `WebMatrix.Security.OAuthWebSecurity` class.</span></span> <span data-ttu-id="d3166-122">**Başlatıcı site** şablonu, bir oturum açma sayfası, bir üyelik veritabanı ve kullanıcıların sitenizde yerel kimlik bilgileri veya başka bir siteden oturum açmasını sağlamak için ihtiyacınız olan tüm kod ile tam bir üyelik altyapısı içerir.</span><span class="sxs-lookup"><span data-stu-id="d3166-122">The **Starter Site** template includes a full membership infrastructure, complete with a login page, a membership database, and all the code you need to let users log into your site using either local credentials or those from another site.</span></span>

<span data-ttu-id="d3166-123">Bu bölümde, kullanıcıların dış sitelerden **Başlatıcı site** şablonunu temel alan bir siteye oturum açmasına izin veren bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d3166-123">This section provides an example of how to let users log in from external sites to a site that's based on the **Starter Site** template.</span></span> <span data-ttu-id="d3166-124">Bir başlangıç sitesi oluşturduktan sonra, bunu yapabilirsiniz (Ayrıntılar aşağıda):</span><span class="sxs-lookup"><span data-stu-id="d3166-124">After creating a starter site, you do this (details follow):</span></span>

- <span data-ttu-id="d3166-125">Bir OAuth sağlayıcısı kullanan siteler (Facebook, Twitter ve Microsoft) için dış sitede bir uygulama oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="d3166-125">For the sites that use an OAuth provider (Facebook, Twitter, and Microsoft), you create an application on the external site.</span></span> <span data-ttu-id="d3166-126">Bu, bu siteler için oturum açma özelliğini çağırmak üzere ihtiyacınız olan uygulama anahtarlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="d3166-126">This gives you application keys that you'll need in order to invoke the login feature for those sites.</span></span>
- <span data-ttu-id="d3166-127">OpenID sağlayıcısı (Google) kullanan siteler için, bir uygulama oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d3166-127">For sites that use an OpenID provider (Google), you do not have to create an application.</span></span> <span data-ttu-id="d3166-128">Bu sitelerin tümünde, oturum açmak ve geliştirici uygulamaları oluşturmak için hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3166-128">For all of these sites, you must have an account in order to log in and to create developer applications.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d3166-129">Microsoft uygulamaları, çalışan bir Web sitesi için yalnızca canlı URL 'yi kabul eder, bu nedenle oturum açma işlemleri için yerel bir Web sitesi URL 'SI kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="d3166-129">Microsoft applications only accept a live URL for a working website, so you cannot use a local website URL for testing logins.</span></span>
- <span data-ttu-id="d3166-130">Uygun kimlik doğrulama sağlayıcısını belirtmek ve kullanmak istediğiniz siteye bir oturum açma göndermek için Web sitenizde birkaç dosyayı düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="d3166-130">Edit a few files in your website in order to specify the appropriate authentication provider and to submit a login to the site you want to use.</span></span>

<span data-ttu-id="d3166-131">Bu makalede, aşağıdaki görevler için ayrı yönergeler sağlanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="d3166-131">This article provides separate instructions for the following tasks:</span></span>

- [<span data-ttu-id="d3166-132">Google oturumlarını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d3166-132">Enabling Google logins</span></span>](#To_enable_Google_logins)
- [<span data-ttu-id="d3166-133">Facebook oturumlarını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d3166-133">Enabling Facebook logins</span></span>](#To_enable_Facebook_logins)
- [<span data-ttu-id="d3166-134">Twitter oturumlarını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d3166-134">Enabling Twitter logins</span></span>](#To_enable_Twitter_logins)

<a id="To_enable_Google_logins"></a>
## <a name="enabling-google-logins"></a><span data-ttu-id="d3166-135">Google oturumlarını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d3166-135">Enabling Google Logins</span></span>

1. <span data-ttu-id="d3166-136">WebMatrix Başlatıcı site şablonunu temel alan bir ASP.NET Web sayfaları sitesi oluşturun veya açın.</span><span class="sxs-lookup"><span data-stu-id="d3166-136">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="d3166-137">*\_AppStart. cshtml* sayfasını açın ve aşağıdaki kod satırının açıklamasını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="d3166-137">Open the *\_AppStart.cshtml* page and uncomment the following line of code.</span></span> 

    [!code-css[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample1.css)]

### <a name="testing-google-login"></a><span data-ttu-id="d3166-138">Google oturum açma testi</span><span class="sxs-lookup"><span data-stu-id="d3166-138">Testing Google login</span></span>

1. <span data-ttu-id="d3166-139">Sitenizin *default. cshtml* sayfasını çalıştırın ve **oturum aç** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d3166-139">Run the *default.cshtml* page of your site and choose the **Log in** button.</span></span>
2. <span data-ttu-id="d3166-140">Oturum *açma* sayfasında, **oturum açmak için başka bir hizmet kullan** bölümünde **Google** veya **Yahoo** Gönder düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d3166-140">On the *Login* page, in the **Use another service to log in** section, choose either the **Google** or **Yahoo** submit button.</span></span> <span data-ttu-id="d3166-141">Bu örnek Google oturum açma bilgilerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="d3166-141">This example uses the Google login.</span></span> 

    <span data-ttu-id="d3166-142">Web sayfası, isteği Google Login sayfasına yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="d3166-142">The web page redirects the request to the Google login page.</span></span>

    ![Google oturum açma](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image2.png)
3. <span data-ttu-id="d3166-144">Mevcut bir Google hesabının kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="d3166-144">Enter credentials for an existing Google account.</span></span>
4. <span data-ttu-id="d3166-145">Google *'ın hesaptaki bilgileri kullanmasına izin vermek* isteyip istemediğinizi sorduğunda, **izin ver**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d3166-145">If Google asks you whether you want to allow *Localhost* to use information from the account, click **Allow**.</span></span>

    <span data-ttu-id="d3166-146">Kod, kullanıcının kimliğini doğrulamak için Google belirtecini kullanır ve ardından Web sitenizde bu sayfaya geri döner.</span><span class="sxs-lookup"><span data-stu-id="d3166-146">The code uses the Google token to authenticate the user, and then returns to this page on your website.</span></span> <span data-ttu-id="d3166-147">Bu sayfa, kullanıcıların Google oturum açmaları Web sitenizde mevcut bir hesapla ilişkilendirmelerini sağlar veya dış oturum açma bilgilerini ile ilişkilendirmek için sitenize yeni bir hesap kaydedebilir.</span><span class="sxs-lookup"><span data-stu-id="d3166-147">This page lets users associate their Google login with an existing account on your website, or they can register a new account on your site to associate the external login with.</span></span>

    ![OAuth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image3.png)
5. <span data-ttu-id="d3166-149">**İlişkilendir** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d3166-149">Choose the **Associate** button.</span></span> <span data-ttu-id="d3166-150">Tarayıcı, uygulamanızın giriş sayfasına geri döner.</span><span class="sxs-lookup"><span data-stu-id="d3166-150">The browser returns to your application's home page.</span></span>

<a id="To_enable_Facebook_logins"></a>
## <a name="enabling-facebook-logins"></a><span data-ttu-id="d3166-151">Facebook oturumlarını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d3166-151">Enabling Facebook Logins</span></span>

1. <span data-ttu-id="d3166-152">[Facebook geliştiricileri sitesine](https://developers.facebook.com/apps) gidin (henüz oturum açmadıysanız oturum açın).</span><span class="sxs-lookup"><span data-stu-id="d3166-152">Go to the [Facebook developers site](https://developers.facebook.com/apps) (log in if you're not already logged in).</span></span>
2. <span data-ttu-id="d3166-153">Yeni uygulama **Oluştur** düğmesini seçin ve ardından yeni uygulamayı adlandırmak ve oluşturmak için istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="d3166-153">Choose the **Create New App** button, and then follow the prompts to name and create the new application.</span></span>
3. <span data-ttu-id="d3166-154">**Uygulamanızın Facebook ile nasıl tümleştirileceğini seçin**bölümünde, **Web sitesi** bölümünü seçin.</span><span class="sxs-lookup"><span data-stu-id="d3166-154">In the section **Select how your app will integrate with Facebook**, choose the **Website** section.</span></span>
4. <span data-ttu-id="d3166-155">**Site URL 'si** ALANıNı sitenizin URL 'siyle (örneğin, `http://www.example.com`) girin.</span><span class="sxs-lookup"><span data-stu-id="d3166-155">Fill in the **Site URL** field with the URL of your site (for example, `http://www.example.com`).</span></span> <span data-ttu-id="d3166-156">**Etki alanı** alanı isteğe bağlıdır; Bu, tüm etki alanı ( *example.com*gibi) için kimlik doğrulaması sağlamak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3166-156">The **Domain** field is optional; you can use this to provide authentication for an entire domain (such as *example.com*).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="d3166-157">Yerel bilgisayarınızda `http://localhost:12345` (sayının bir yerel bağlantı noktası numarası olduğu) gibi bir URL 'yi çalıştırıyorsanız, sitenizi test etmek için bu değeri **site URL 'si** alanına ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3166-157">If you are running a site on your local computer with a URL like `http://localhost:12345` (where the number is a local port number), you can add this value to the **Site URL** field for testing your site.</span></span> <span data-ttu-id="d3166-158">Ancak, yerel sitenizin bağlantı noktası numarası değiştiğinde uygulamanızın **site URL 'si** alanını güncelleştirmeniz gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="d3166-158">However, any time the port number of your local site changes, you will need to update the **Site URL** field of your application.</span></span>
5. <span data-ttu-id="d3166-159">**Değişiklikleri Kaydet** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d3166-159">Choose the **Save Changes** button.</span></span>
6. <span data-ttu-id="d3166-160">**Uygulamalar** sekmesini yeniden seçin ve ardından uygulamanızın başlangıç sayfasını görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="d3166-160">Choose the **Apps** tab again, and then view the start page for your application.</span></span>
7. <span data-ttu-id="d3166-161">Uygulamanızın uygulama **kimliği** ve **uygulama gizli** değerlerini kopyalayın ve bunları geçici bir metin dosyasına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="d3166-161">Copy the **App ID** and **App Secret** values for your application and paste them into a temporary text file.</span></span> <span data-ttu-id="d3166-162">Bu değerleri, Web sitesi kodunuzda Facebook sağlayıcısına geçitirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3166-162">You will pass these values to the Facebook provider in your website code.</span></span>
8. <span data-ttu-id="d3166-163">Facebook geliştirici sitesinden çıkın.</span><span class="sxs-lookup"><span data-stu-id="d3166-163">Exit the Facebook developer site.</span></span>

<span data-ttu-id="d3166-164">Artık Web sitenizdeki iki sayfada değişiklikler yaparsınız. böylece kullanıcılar, Facebook hesaplarını kullanarak sitede oturum açabilirler.</span><span class="sxs-lookup"><span data-stu-id="d3166-164">Now you make changes to two pages in your website so that users will able to log into the site using their Facebook accounts.</span></span>

1. <span data-ttu-id="d3166-165">WebMatrix Başlatıcı site şablonunu temel alan bir ASP.NET Web sayfaları sitesi oluşturun veya açın.</span><span class="sxs-lookup"><span data-stu-id="d3166-165">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="d3166-166">*\_AppStart. cshtml* sayfasını açın ve Facebook OAuth sağlayıcısı için kodun açıklamasını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="d3166-166">Open the *\_AppStart.cshtml* page and uncomment the code for the Facebook OAuth provider.</span></span> <span data-ttu-id="d3166-167">Açıklamalı olmayan kod bloğu aşağıdakine benzer:</span><span class="sxs-lookup"><span data-stu-id="d3166-167">The uncommented code block looks like the following:</span></span> 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample2.cs)]
3. <span data-ttu-id="d3166-168">**Uygulama kimliği** değerini, Facebook uygulamasından `appId` parametresinin değeri olarak (tırnak işaretleri içinde) kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d3166-168">Copy the **App ID** value from the Facebook application as the value of the `appId` parameter (inside the quotation marks).</span></span>
4. <span data-ttu-id="d3166-169">Facebook uygulamasından **uygulama gizli** değerini `appSecret` parametre değeri olarak kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d3166-169">Copy **App Secret** value from the Facebook application as the `appSecret` parameter value.</span></span>
5. <span data-ttu-id="d3166-170">Dosyayı kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="d3166-170">Save and close the file.</span></span>

### <a name="testing-facebook-login"></a><span data-ttu-id="d3166-171">Facebook oturum açma testi</span><span class="sxs-lookup"><span data-stu-id="d3166-171">Testing Facebook login</span></span>

1. <span data-ttu-id="d3166-172">Sitenin *default. cshtml* sayfasını çalıştırın ve **oturum aç** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d3166-172">Run the site's *default.cshtml* page and choose the **Login** button.</span></span>
2. <span data-ttu-id="d3166-173">*Oturum açma* sayfasında, **oturum açmak için başka bir hizmet kullan** bölümünde **Facebook** simgesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d3166-173">On the *Login* page, in the **Use another service to log in** section, choose the **Facebook** icon.</span></span> 

    <span data-ttu-id="d3166-174">Web sayfası, isteği Facebook oturum açma sayfasına yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="d3166-174">The web page redirects the request to the Facebook login page.</span></span>

    ![OAuth-2](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image4.png)
3. <span data-ttu-id="d3166-176">Facebook hesabında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d3166-176">Log into a Facebook account.</span></span> 

    <span data-ttu-id="d3166-177">Kod, kimliğinizi doğrulamak için Facebook belirtecini kullanır ve ardından Facebook oturum açma bilgilerinizi sitenizin oturum açmayla ilişkilendirebileceğiniz bir sayfaya geri döner.</span><span class="sxs-lookup"><span data-stu-id="d3166-177">The code uses the Facebook token to authenticate you and then returns to a page where you can associate your Facebook login with your site's login.</span></span> <span data-ttu-id="d3166-178">Kullanıcı adınız veya e-posta adresiniz formundaki **e-posta** alanına girilir.</span><span class="sxs-lookup"><span data-stu-id="d3166-178">Your user name or email address is filled into the **Email** field on the form.</span></span>

    ![OAuth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image5.png)
4. <span data-ttu-id="d3166-180">**İlişkilendir** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d3166-180">Choose the **Associate** button.</span></span> 

    <span data-ttu-id="d3166-181">Tarayıcı, giriş sayfasına geri döner ve oturum açarsınız.</span><span class="sxs-lookup"><span data-stu-id="d3166-181">The browser returns to the home page and you are logged in.</span></span>

<a id="To_enable_Twitter_logins"></a>
## <a name="enabling-twitter-logins"></a><span data-ttu-id="d3166-182">Twitter oturumlarını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d3166-182">Enabling Twitter Logins</span></span>

1. <span data-ttu-id="d3166-183">[Twitter geliştiricileri sitesine](https://dev.twitter.com/)gidin.</span><span class="sxs-lookup"><span data-stu-id="d3166-183">Browse to the [Twitter developers site](https://dev.twitter.com/).</span></span>
2. <span data-ttu-id="d3166-184">**Uygulama oluştur** bağlantısını seçin ve ardından sitede oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d3166-184">Choose the **Create an App** link and then log into the site.</span></span>
3. <span data-ttu-id="d3166-185">**Uygulama oluştur** formunda **ad** ve **Açıklama** alanlarını girin.</span><span class="sxs-lookup"><span data-stu-id="d3166-185">On the **Create an Application** form, fill in the **Name** and **Description** fields.</span></span>
4. <span data-ttu-id="d3166-186">**Web sitesi** alanına sitenizin URL 'sini girin (örneğin, `http://www.example.com`).</span><span class="sxs-lookup"><span data-stu-id="d3166-186">In the **WebSite** field, enter the URL of your site (for example, `http://www.example.com`).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="d3166-187">Sitenizi yerel olarak test ediyorsanız (`http://localhost:12345`gibi bir URL kullanarak) Twitter, URL 'YI kabul etmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="d3166-187">If you're testing your site locally (using a URL like `http://localhost:12345`), Twitter might not accept the URL.</span></span> <span data-ttu-id="d3166-188">Ancak, yerel geri döngü IP adresini (örneğin `http://127.0.0.1:12345`) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3166-188">However, you might be able to use the local loopback IP address (for example `http://127.0.0.1:12345`).</span></span> <span data-ttu-id="d3166-189">Bu, uygulamanızı yerel olarak test etme işlemini basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="d3166-189">This simplifies the process of testing your application locally.</span></span> <span data-ttu-id="d3166-190">Ancak, yerel sitenizin bağlantı noktası numarası her değiştiğinde uygulamanızın **Web sitesi** alanını güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3166-190">However, every time the port number of your local site changes, you'll need to update the **WebSite** field of your application.</span></span>
5. <span data-ttu-id="d3166-191">**Geri arama URL 'si** alanına, Web sitenizde Twitter 'da oturum açtıktan sonra geri dönmesini istediğiniz sayfa IÇIN bir URL girin.</span><span class="sxs-lookup"><span data-stu-id="d3166-191">In the **Callback URL** field, enter a URL for the page in your website that you want users to return to after logging into Twitter.</span></span> <span data-ttu-id="d3166-192">Örneğin, kullanıcıları Başlatıcı sitesinin giriş sayfasına (oturum açma durumunu tanıyacak) göndermek için, **Web sitesi** alanına girdiğiniz aynı URL 'yi girin.</span><span class="sxs-lookup"><span data-stu-id="d3166-192">For example, to send users to the home page of the Starter Site (which will recognize their logged-in status), enter the same URL that you entered in the **WebSite** field.</span></span>
6. <span data-ttu-id="d3166-193">Koşulları kabul edin ve **Twitter uygulamanızı oluştur** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d3166-193">Accept the terms and choose the **Create your Twitter application** button.</span></span>
7. <span data-ttu-id="d3166-194">**Uygulamalarım** giriş sayfasında, oluşturduğunuz uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="d3166-194">On the **My Applications** landing page, choose the application you created.</span></span>
8. <span data-ttu-id="d3166-195">**Ayrıntılar** sekmesinde, en alta kaydırın ve **erişim belirtecinden oluştur** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d3166-195">On the **Details** tab, scroll to the bottom and choose the **Create My Access Token** button.</span></span>
9. <span data-ttu-id="d3166-196">**Ayrıntılar** sekmesinde, uygulamanız Için **tüketici anahtarı** ve **Tüketici gizli** değerlerini kopyalayın ve bunları geçici bir metin dosyasına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="d3166-196">On the **Details** tab, copy the **Consumer Key** and **Consumer Secret** values for your application and paste them into a temporary text file.</span></span> <span data-ttu-id="d3166-197">Bu değerleri, Web sitesi kodunuzda Twitter sağlayıcısına geçireceğiz.</span><span class="sxs-lookup"><span data-stu-id="d3166-197">You'll pass these values to the Twitter provider in your website code.</span></span>
10. <span data-ttu-id="d3166-198">Twitter sitesinden çıkın.</span><span class="sxs-lookup"><span data-stu-id="d3166-198">Exit the Twitter site.</span></span>

<span data-ttu-id="d3166-199">Artık Web sitenizdeki iki sayfada değişiklikler yaparsınız, böylece kullanıcılar kendi Twitter hesaplarını kullanarak sitede oturum açabilirler.</span><span class="sxs-lookup"><span data-stu-id="d3166-199">Now you make changes to two pages in your website so that users will be able to log into the site using their Twitter accounts.</span></span>

1. <span data-ttu-id="d3166-200">WebMatrix Başlatıcı site şablonunu temel alan bir ASP.NET Web sayfaları sitesi oluşturun veya açın.</span><span class="sxs-lookup"><span data-stu-id="d3166-200">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="d3166-201">*\_AppStart. cshtml* sayfasını açın ve Twitter OAuth sağlayıcısı için kodun açıklamasını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="d3166-201">Open the *\_AppStart.cshtml* page and uncomment the code for the Twitter OAuth provider.</span></span> <span data-ttu-id="d3166-202">Açıklamalı olmayan kod bloğu şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="d3166-202">The uncommented code block looks like this:</span></span> 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample3.cs)]
3. <span data-ttu-id="d3166-203">**Kullanıcı anahtarı** değerini Twitter uygulamasından `consumerKey` parametresinin değeri olarak (tırnak işaretleri içinde) kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d3166-203">Copy the **Consumer Key** value from the Twitter application as the value of the `consumerKey` parameter (inside the quotation marks).</span></span>
4. <span data-ttu-id="d3166-204">**Kullanıcı gizli** değerini Twitter uygulamasından `consumerSecret` parametresinin değeri olarak kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d3166-204">Copy the **Consumer Secret** value from the Twitter application as the value of the `consumerSecret` parameter.</span></span>
5. <span data-ttu-id="d3166-205">Dosyayı kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="d3166-205">Save and close the file.</span></span>

### <a name="testing-twitter-login"></a><span data-ttu-id="d3166-206">Twitter oturum açma testi</span><span class="sxs-lookup"><span data-stu-id="d3166-206">Testing Twitter login</span></span>

1. <span data-ttu-id="d3166-207">Sitenizin *default. cshtml* sayfasını çalıştırın ve **oturum aç** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d3166-207">Run the *default.cshtml* page of your site and choose the **Login** button.</span></span>
2. <span data-ttu-id="d3166-208">Oturum *açma* sayfasında, **oturum açmak için başka bir hizmet kullan** bölümünde **Twitter** simgesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d3166-208">On the *Login* page, in the **Use another service to log in** section, choose the **Twitter** icon.</span></span> 

    <span data-ttu-id="d3166-209">Web sayfası, oluşturduğunuz uygulama için isteği Twitter oturum açma sayfasına yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="d3166-209">The web page redirects the request to a Twitter login page for the application you created.</span></span>

    ![OAuth-4](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image6.png)
3. <span data-ttu-id="d3166-211">Twitter hesabında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d3166-211">Log into a Twitter account.</span></span>
4. <span data-ttu-id="d3166-212">Kod, kullanıcının kimliğini doğrulamak için Twitter belirtecini kullanır ve ardından sizi, oturum açma bilgilerinizi Web sitesi hesabınızla ilişkilendirebileceğiniz bir sayfaya geri döndürür.</span><span class="sxs-lookup"><span data-stu-id="d3166-212">The code uses the Twitter token to authenticate the user and then returns you to a page where you can associate your login with your website account.</span></span> <span data-ttu-id="d3166-213">Ad veya e-posta adresiniz, formdaki **e-posta** alanına girilir.</span><span class="sxs-lookup"><span data-stu-id="d3166-213">Your name or email address is filled into the **Email** field on the form.</span></span>

    ![OAuth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image7.png)
5. <span data-ttu-id="d3166-215">**İlişkilendir** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d3166-215">Choose the **Associate** button.</span></span> 

    <span data-ttu-id="d3166-216">Tarayıcı, giriş sayfasına geri döner ve oturum açarsınız.</span><span class="sxs-lookup"><span data-stu-id="d3166-216">The browser returns to the home page and you are logged in.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="d3166-217">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d3166-217">Additional Resources</span></span>

- [<span data-ttu-id="d3166-218">Site Geneline Yönelik Davranışını Özelleştirme</span><span class="sxs-lookup"><span data-stu-id="d3166-218">Customizing Site-Wide Behavior</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="d3166-219">ASP.NET Web sayfaları sitesine güvenlik ve üyelik ekleme</span><span class="sxs-lookup"><span data-stu-id="d3166-219">Adding Security and Membership to an ASP.NET Web Pages Site</span></span>](https://go.microsoft.com/fwlink/?LinkID=202904)
