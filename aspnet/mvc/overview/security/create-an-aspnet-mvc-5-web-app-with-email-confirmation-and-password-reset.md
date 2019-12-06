---
uid: mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
title: Oturum açma, e-posta onayı ve parola sıfırlama (C#) | ile güvenli BIR ASP.NET MVC 5 Web uygulaması oluşturma | Microsoft Docs
author: Rick-Anderson
description: Bu öğreticide, ASP.NET Identity üyelik sistemini kullanarak e-posta onayı ve parola sıfırlama ile bir ASP.NET MVC 5 Web uygulaması oluşturma işlemlerinin nasıl yapılacağı gösterilmektedir. CA 'nız...
ms.author: riande
ms.date: 03/26/2015
ms.assetid: d4911cb3-1afb-4805-b860-10818c4b1280
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: 07f5b290b73f75000e6f29fe09e4dc25e144452f
ms.sourcegitcommit: 969e7db924ebad3cc0f0cb0d65d148e8b9221b9a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/06/2019
ms.locfileid: "74899705"
---
# <a name="create-a-secure-aspnet-mvc-5-web-app-with-log-in-email-confirmation-and-password-reset-c"></a><span data-ttu-id="c3e3b-104">Oturum açma, e-posta onayı ve parola sıfırlama özellikli, güvenli bir ASP.NET MVC 5 web uygulaması oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="c3e3b-104">Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset (C#)</span></span>

<span data-ttu-id="c3e3b-105">[Rick Anderson]((https://twitter.com/RickAndMSFT)) tarafından</span><span class="sxs-lookup"><span data-stu-id="c3e3b-105">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

<span data-ttu-id="c3e3b-106">Bu öğreticide, ASP.NET Identity üyelik sistemini kullanarak e-posta onayı ve parola sıfırlama ile bir ASP.NET MVC 5 Web uygulaması oluşturma işlemlerinin nasıl yapılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-106">This tutorial shows you how to build an ASP.NET MVC 5 web app with email confirmation and password reset using the ASP.NET Identity membership system.</span></span>

<span data-ttu-id="c3e3b-107">.NET Core kullanan Bu öğreticinin güncelleştirilmiş bir sürümü için, bkz. [hesap onaylama ve parola kurtarma ASP.NET Core [/ASPNET/Core/Security/Authentication/acconaylayın).</span><span class="sxs-lookup"><span data-stu-id="c3e3b-107">For an updated version of this tutorial that uses .NET Core, see [Account confirmation and password recovery in ASP.NET Core[/aspnet/core/security/authentication/accconfirm).</span></span>

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a><span data-ttu-id="c3e3b-108">ASP.NET MVC uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="c3e3b-108">Create an ASP.NET MVC app</span></span>

<span data-ttu-id="c3e3b-109">Web veya [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) [için Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) yükleyip çalıştırarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-109">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="c3e3b-110">[Visual Studio 2013 güncelleştirme 3](https://go.microsoft.com/fwlink/?LinkId=390465) veya üstünü yükler.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-110">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="c3e3b-111">Uyarı: Bu öğreticiyi tamamlayabilmeniz için [Visual Studio 2013 güncelleştirme 3](https://go.microsoft.com/fwlink/?LinkId=390465) veya sonraki bir sürümü yüklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-111">Warning: You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>

1. <span data-ttu-id="c3e3b-112">Yeni bir ASP.NET Web projesi oluşturun ve MVC şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-112">Create a new ASP.NET Web project and select the MVC template.</span></span> <span data-ttu-id="c3e3b-113">Web Forms Ayrıca ASP.NET Identity destekler, böylece bir Web Forms uygulamasındaki benzer adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-113">Web Forms also supports ASP.NET Identity, so you could follow similar steps in a web forms app.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image1.png)
2. <span data-ttu-id="c3e3b-114">Varsayılan kimlik doğrulamasını **bireysel kullanıcı hesapları**olarak bırakın.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-114">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="c3e3b-115">Uygulamayı Azure 'da barındırmak isterseniz onay kutusunu işaretli bırakın.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-115">If you'd like to host the app in Azure, leave the check box checked.</span></span> <span data-ttu-id="c3e3b-116">Öğreticide daha sonra Azure 'a dağıtacağız.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-116">Later in the tutorial we will deploy to Azure.</span></span> <span data-ttu-id="c3e3b-117">[Bir Azure hesabını ücretsiz olarak açabilirsiniz](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="c3e3b-117">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
3. <span data-ttu-id="c3e3b-118">[PROJEYI SSL kullanacak şekilde](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-118">Set the [project to use SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
4. <span data-ttu-id="c3e3b-119">Uygulamayı çalıştırın, **Kaydet** bağlantısına tıklayın ve bir Kullanıcı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-119">Run the app, click the **Register** link and register a user.</span></span> <span data-ttu-id="c3e3b-120">Bu noktada, e-postadaki tek doğrulama [[Emapostaadresi]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) özniteliğiyle aynıdır.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-120">At this point, the only validation on the email is with the [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) attribute.</span></span>
5. <span data-ttu-id="c3e3b-121">Sunucu Gezgini ' de **veri bağlantısı \ Defaultconnection\tables\aspnetusers**' a gidin, sağ tıklayın ve **tablo tanımını aç**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-121">In Server Explorer, navigate to **Data Connections\DefaultConnection\Tables\AspNetUsers**, right click and select **Open table definition**.</span></span>

    <span data-ttu-id="c3e3b-122">Aşağıdaki görüntüde `AspNetUsers` şeması gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="c3e3b-122">The following image shows the `AspNetUsers` schema:</span></span>

    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image2.png)
6. <span data-ttu-id="c3e3b-123">**Aspnetusers** tablosuna sağ tıklayın ve **tablo verilerini göster**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-123">Right click on the **AspNetUsers** table and select **Show Table Data**.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image3.png)  
 <span data-ttu-id="c3e3b-124">Bu noktada e-posta onaylanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-124">At this point the email has not been confirmed.</span></span>
7. <span data-ttu-id="c3e3b-125">Satıra tıklayın ve Sil ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-125">Click on the row and select delete.</span></span> <span data-ttu-id="c3e3b-126">Bu e-postayı bir sonraki adımda tekrar ekleyecek ve bir onay e-postası göndereceğiz.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-126">You'll add this email again in the next step, and send a confirmation email.</span></span>

## <a name="email-confirmation"></a><span data-ttu-id="c3e3b-127">E-posta onayı</span><span class="sxs-lookup"><span data-stu-id="c3e3b-127">Email confirmation</span></span>

<span data-ttu-id="c3e3b-128">Başka birinin taklit etmeyeceğinden emin olmak için yeni bir Kullanıcı kaydının e-postasını onaylamak en iyi uygulamadır. (diğer bir deyişle, başka birinin e-postasına kaydolmamaları).</span><span class="sxs-lookup"><span data-stu-id="c3e3b-128">It's a best practice to confirm the email of a new user registration to verify they are not impersonating someone else (that is, they haven't registered with someone else's email).</span></span> <span data-ttu-id="c3e3b-129">Bir tartışma forumu olduğunu varsayalım, `"bob@example.com"` `"joe@contoso.com"`olarak kaydolmasını engellemek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-129">Suppose you had a discussion forum, you would want to prevent `"bob@example.com"` from registering as `"joe@contoso.com"`.</span></span> <span data-ttu-id="c3e3b-130">E-posta onayı olmadan `"joe@contoso.com"`, uygulamanızdan istenmeyen e-posta alabilir.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-130">Without email confirmation, `"joe@contoso.com"` could get unwanted email from your app.</span></span> <span data-ttu-id="c3e3b-131">Emre 'nin yanlışlıkla `"bib@example.com"` olarak kaydolduğunu ve olduğunu fark etmemiş olduğunu varsayalım, uygulamanın doğru e-postası olmadığından parola kurtarma kullanamayacak.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-131">Suppose Bob accidentally registered as `"bib@example.com"` and hadn't noticed it, he wouldn't be able to use password recover because the app doesn't have his correct email.</span></span> <span data-ttu-id="c3e3b-132">E-posta onayı yalnızca botlardan sınırlı koruma sağlar ve belirlenen istenmeyen posta gönderenlerin korumasını sağlamaz, kaydolmak için kullanabilecekleri birçok çalışma e-posta diğer adı vardır.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-132">Email confirmation provides only limited protection from bots and doesn't provide protection from determined spammers, they have many working email aliases they can use to register.</span></span>

<span data-ttu-id="c3e3b-133">Genellikle yeni kullanıcıların e-posta, SMS mesajı veya başka bir mekanizma tarafından onaylanmadan önce Web sitenize veri göndermeleri önlemektir.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-133">You generally want to prevent new users from posting any data to your web site before they have been confirmed by email, a SMS text message or another mechanism.</span></span> <a id="build"></a><span data-ttu-id="c3e3b-134">Aşağıdaki bölümlerde, e-posta onayını etkinleştireceğiz ve yeni kayıtlı kullanıcıların e-postaları onaylanana kadar oturum açmasını önleyecek şekilde kodu değiştireceğiz.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-134">In the sections below, we will enable email confirmation and modify the code to prevent newly registered users from logging in until their email has been confirmed.</span></span>

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a><span data-ttu-id="c3e3b-135">SendGrid 'i bağlama</span><span class="sxs-lookup"><span data-stu-id="c3e3b-135">Hook up SendGrid</span></span>

<span data-ttu-id="c3e3b-136">Bu bölümdeki yönergeler güncel değil.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-136">The instructions in this section are not current.</span></span> <span data-ttu-id="c3e3b-137">Bkz. güncelleştirilmiş yönergeler için [SendGrid e-posta sağlayıcısını yapılandırma](/aspnet/core/security/authentication/accconfirm#configure-email-provider) .</span><span class="sxs-lookup"><span data-stu-id="c3e3b-137">See [Configure SendGrid email provider](/aspnet/core/security/authentication/accconfirm#configure-email-provider) for updated instructions.</span></span>

<span data-ttu-id="c3e3b-138">Bu öğretici yalnızca [SendGrid](http://sendgrid.com/)aracılığıyla e-posta bildirimi Eklemeyi gösterir, ancak SMTP ve diğer mekanizmaları kullanarak e-posta gönderebilirsiniz ( [ek kaynaklara](#addRes)bakın).</span><span class="sxs-lookup"><span data-stu-id="c3e3b-138">Although this tutorial only shows how to add email notification through [SendGrid](http://sendgrid.com/), you can send email using SMTP and other mechanisms (see [additional resources](#addRes)).</span></span>

1. <span data-ttu-id="c3e3b-139">Paket Yöneticisi konsolunda aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="c3e3b-139">In the Package Manager Console, enter the following command:</span></span> 

    [!code-console[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample1.cmd)]
2. <span data-ttu-id="c3e3b-140">[Azure SendGrid kaydolma sayfasına](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) gidin ve ücretsiz bir SendGrid hesabına kaydolun.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-140">Go to the [Azure SendGrid sign up page](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) and register for a free SendGrid account.</span></span> <span data-ttu-id="c3e3b-141">*App_Start/ıdentityconfig.cs*içinde aşağıdakine benzer kod ekleyerek SendGrid 'i yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="c3e3b-141">Configure SendGrid by adding code similar to the following in *App_Start/IdentityConfig.cs*:</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample2.cs?highlight=3,5)]

<span data-ttu-id="c3e3b-142">Şunları eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="c3e3b-142">You'll need to add the following includes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample3.cs)]

<span data-ttu-id="c3e3b-143">Bu örneği basit tutmak için uygulama ayarlarını *Web. config* dosyasında depolayacağız:</span><span class="sxs-lookup"><span data-stu-id="c3e3b-143">To keep this sample simple, we'll store the app settings in the *web.config* file:</span></span>

[!code-xml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample4.xml)]

> [!WARNING]
> <span data-ttu-id="c3e3b-144">Güvenlik-önemli verileri hiçbir şekilde kaynak kodunuzda depolamayin.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-144">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="c3e3b-145">Hesap ve kimlik bilgileri appSetting 'de depolanır.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-145">The account and credentials are stored in the appSetting.</span></span> <span data-ttu-id="c3e3b-146">Azure 'da, bu değerleri Azure portal **[Yapılandır](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** sekmesinde güvenli bir şekilde depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-146">On Azure, you can securely store these values on the **[Configure](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** tab in the Azure portal.</span></span> <span data-ttu-id="c3e3b-147">[ASP.net ve Azure 'a parola ve diğer hassas verileri dağıtmaya yönelik en iyi uygulamalar](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-147">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>

### <a name="enable-email-confirmation-in-the-account-controller"></a><span data-ttu-id="c3e3b-148">Hesap denetleyicisinde e-posta onayını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c3e3b-148">Enable email confirmation in the Account controller</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample5.cs?highlight=16-21)]

<span data-ttu-id="c3e3b-149">*Views\Account\ConfirmEmail.cshtml* dosyasının doğru Razor söz dizimini içerdiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-149">Verify the *Views\Account\ConfirmEmail.cshtml* file has correct razor syntax.</span></span> <span data-ttu-id="c3e3b-150">(İlk satırdaki @ karakteri eksik olabilir.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-150">( The @ character in the first line might be missing.</span></span> <span data-ttu-id="c3e3b-151">)</span><span class="sxs-lookup"><span data-stu-id="c3e3b-151">)</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample6.cshtml?highlight=1)]

<span data-ttu-id="c3e3b-152">Uygulamayı çalıştırın ve Kaydet bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-152">Run the app and click the Register link.</span></span> <span data-ttu-id="c3e3b-153">Kayıt formunu gönderdikten sonra oturumunuz açıldı.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-153">Once you submit the registration form, you are logged in.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image4.png)

<span data-ttu-id="c3e3b-154">E-posta hesabınızı denetleyin ve e-postanızı onaylamak için bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-154">Check your email account and click on the link to confirm your email.</span></span>

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a><span data-ttu-id="c3e3b-155">Oturum açmadan önce e-posta onayı gerektir</span><span class="sxs-lookup"><span data-stu-id="c3e3b-155">Require email confirmation before log in</span></span>

<span data-ttu-id="c3e3b-156">Şu anda bir kullanıcı kayıt formunu tamamladıktan sonra oturum açar.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-156">Currently once a user completes the registration form, they are logged in.</span></span> <span data-ttu-id="c3e3b-157">Genellikle e-postalarını oturum açmadan önce doğrulamak istersiniz.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-157">You generally want to confirm their email before logging them in.</span></span> <span data-ttu-id="c3e3b-158">Aşağıdaki bölümde, yeni kullanıcıların oturum açmadan (kimliği doğrulanmış) önce onaylanan bir e-postaya sahip olmasını gerektirecek şekilde kodu değiştiririz.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-158">In the section below, we will modify the code to require new users to have a confirmed email before they are logged in (authenticated).</span></span> <span data-ttu-id="c3e3b-159">`HttpPost Register` yöntemini aşağıdaki vurgulanan değişikliklerle güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="c3e3b-159">Update the `HttpPost Register` method with the following highlighted changes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample7.cs?highlight=14-15,23-30)]

<span data-ttu-id="c3e3b-160">`SignInAsync` yöntemi yorum yaparak, Kullanıcı kayıt tarafından oturum açmamış olur.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-160">By commenting out the `SignInAsync` method, the user will not be signed in by the registration.</span></span> <span data-ttu-id="c3e3b-161">`TempData["ViewBagLink"] = callbackUrl;` satırı, e-posta göndermeden uygulama ve test kaydı [hatalarını ayıklamak](#dbg) için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-161">The `TempData["ViewBagLink"] = callbackUrl;` line can be used to [debug the app](#dbg) and test registration without sending email.</span></span> <span data-ttu-id="c3e3b-162">`ViewBag.Message`, onaylama yönergelerini göstermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-162">`ViewBag.Message` is used to display the confirm instructions.</span></span> <span data-ttu-id="c3e3b-163">[İndirme örneği](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) , e-posta onayını e-posta ayarlamadan test etmek için kod içerir ve ayrıca uygulamada hata ayıklamak için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-163">The [download sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) contains code to test email confirmation without setting up email, and can also be used to debug the application.</span></span>

<span data-ttu-id="c3e3b-164">`Views\Shared\Info.cshtml` bir dosya oluşturun ve aşağıdaki Razor işaretlemesini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c3e3b-164">Create a `Views\Shared\Info.cshtml` file and add the following razor markup:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample8.cshtml)]

<span data-ttu-id="c3e3b-165">[Yetkilendirme özniteliğini](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) , ana denetleyicinin `Contact` Action yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-165">Add the [Authorize attribute](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) to the `Contact` action method of the Home controller.</span></span> <span data-ttu-id="c3e3b-166">Anonim kullanıcıların erişimi yok ve kimliği doğrulanmış kullanıcıların erişimi olduğunu doğrulamak için **iletişim** bağlantısına tıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-166">You can click on the **Contact** link to verify anonymous users don't have access and authenticated users do have access.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample9.cs?highlight=1)]

<span data-ttu-id="c3e3b-167">`HttpPost Login` eylem yöntemini de güncelleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="c3e3b-167">You must also update the `HttpPost Login` action method:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample10.cs?highlight=13-22)]

<span data-ttu-id="c3e3b-168">*Views\shared\error.exe* görünümünü şu hata iletisini görüntüleyecek şekilde güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="c3e3b-168">Update the *Views\Shared\Error.cshtml* view to display the error message:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample11.cshtml?highlight=8-17)]

<span data-ttu-id="c3e3b-169">Test etmek istediğiniz e-posta diğer adını içeren **Aspnetusers** tablosundaki tüm hesapları silin.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-169">Delete any accounts in the **AspNetUsers** table that contain the email alias you wish to test with.</span></span> <span data-ttu-id="c3e3b-170">Uygulamayı çalıştırın ve e-posta adresinizi onaylaana kadar oturum açabildiğinizi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-170">Run the app and verify you can't log in until you have confirmed your email address.</span></span> <span data-ttu-id="c3e3b-171">E-posta adresinizi onaylayın, **iletişim** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-171">Once you confirm your email address, click the **Contact** link.</span></span>

<a id="reset"></a>
## <a name="password-recoveryreset"></a><span data-ttu-id="c3e3b-172">Parola kurtarma/sıfırlama</span><span class="sxs-lookup"><span data-stu-id="c3e3b-172">Password recovery/reset</span></span>

<span data-ttu-id="c3e3b-173">Açıklama karakterlerini hesap denetleyicisindeki `HttpPost ForgotPassword` Action yönteminden kaldırın:</span><span class="sxs-lookup"><span data-stu-id="c3e3b-173">Remove the comment characters from the `HttpPost ForgotPassword` action method in the account controller:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample12.cs?highlight=17-20)]

<span data-ttu-id="c3e3b-174">*Views\account\login.exe* Razor görünüm dosyasında `ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) ' den açıklama karakterlerini kaldırın:</span><span class="sxs-lookup"><span data-stu-id="c3e3b-174">Remove the comment characters from the `ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) in the *Views\Account\Login.cshtml* razor view file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample13.cshtml?highlight=47-50)]

<span data-ttu-id="c3e3b-175">Oturum aç sayfasında artık parola sıfırlama bağlantısı gösterilir.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-175">The Log in page will now show a link to reset the password.</span></span>

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a><span data-ttu-id="c3e3b-176">E-posta onay bağlantısını yeniden gönder</span><span class="sxs-lookup"><span data-stu-id="c3e3b-176">Resend email confirmation link</span></span>

<span data-ttu-id="c3e3b-177">Bir Kullanıcı yeni bir yerel hesap oluşturduktan sonra, oturum açmadan önce kullanmaları gereken bir onay bağlantısına e-posta gönderilir.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-177">Once a user creates a new local account, they are emailed a confirmation link they are required to use before they can log on.</span></span> <span data-ttu-id="c3e3b-178">Kullanıcı onay e-postasını yanlışlıkla silerse veya e-posta hiçbir daha ulaşmadıysa, onay bağlantısının yeniden gönderilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-178">If the user accidentally deletes the confirmation email, or the email never arrives, they will need the confirmation link sent again.</span></span> <span data-ttu-id="c3e3b-179">Aşağıdaki kod değişiklikleri, bunun nasıl etkinleştirileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-179">The following code changes show how to enable this.</span></span>

<span data-ttu-id="c3e3b-180">Aşağıdaki yardımcı yöntemi *Controllers\accountcontroller.cs* dosyasının altına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c3e3b-180">Add the following helper method to the bottom of the *Controllers\AccountController.cs* file:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample14.cs)]

<span data-ttu-id="c3e3b-181">Yeni yardımcıyı kullanmak için Register metodunu güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="c3e3b-181">Update the Register method to use the new helper:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample15.cs?highlight=17)]

<span data-ttu-id="c3e3b-182">Kullanıcı hesabı onaylanmazsa parolayı yeniden göndermek için oturum açma yöntemini güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="c3e3b-182">Update the Login method to resend the password if the user account has not been confirmed:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample16.cs?highlight=20)]

<a id="combine"></a>
## <a name="combine-social-and-local-login-accounts"></a><span data-ttu-id="c3e3b-183">Sosyal ve yerel oturum açma hesaplarını birleştirme</span><span class="sxs-lookup"><span data-stu-id="c3e3b-183">Combine social and local login accounts</span></span>

<span data-ttu-id="c3e3b-184">E-posta bağlantısına tıklayarak Yerel ve sosyal hesapları birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-184">You can combine local and social accounts by clicking on your email link.</span></span> <span data-ttu-id="c3e3b-185">Aşağıdaki sırada **RickAndMSFT@gmail.com** önce yerel bir oturum açma olarak oluşturulur, ancak önce hesabı önce bir sosyal oturum günlüğü olarak oluşturabilir, ardından yerel bir oturum açma ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-185">In the following sequence **RickAndMSFT@gmail.com** is first created as a local login, but you can create the account as a social log in first, then add a local login.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image5.png)

<span data-ttu-id="c3e3b-186">**Yönet** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-186">Click on the **Manage** link.</span></span> <span data-ttu-id="c3e3b-187">Bu hesapla ilişkili **dış oturum açma sayısı: 0** ' a göz önüne alın.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-187">Note the **External Logins: 0** associated with this account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image6.png)

<span data-ttu-id="c3e3b-188">Başka bir oturum açma hizmetine bağlantıyı tıklatın ve uygulama isteklerini kabul edin.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-188">Click the link to another log in service and accept the app requests.</span></span> <span data-ttu-id="c3e3b-189">İki hesap birleştirildi, herhangi bir hesapla oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-189">The two accounts have been combined, you will be able to log on with either account.</span></span> <span data-ttu-id="c3e3b-190">Kullanıcılarınızın, sosyal oturum açma kimlik doğrulaması hizmeti kapatılmış veya sosyal hesaplarına erişimi kaybetmiş olması olasılığına karşı yerel hesaplar eklemesini isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-190">You might want your users to add local accounts in case their social log in authentication service is down, or more likely they have lost access to their social account.</span></span>

<span data-ttu-id="c3e3b-191">Aşağıdaki görüntüde, Tom bir sosyal oturum günlüğü (dış oturum açmalarından görebileceğiniz **: 1** gösterilen sayfada görebilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="c3e3b-191">In the following image, Tom is a social log in (which you can see from the **External Logins: 1** shown on the page).</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image7.png)

<span data-ttu-id="c3e3b-192">**Parola Seç** ' e tıkladığınızda, aynı hesapla ilişkili bir yerel günlük eklemenize izin verir.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-192">Clicking on **Pick a password** allows you to add a local log on associated with the same account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image8.png)

## <a name="email-confirmation-in-more-depth"></a><span data-ttu-id="c3e3b-193">Daha ayrıntılı bir şekilde e-posta onayı</span><span class="sxs-lookup"><span data-stu-id="c3e3b-193">Email confirmation in more depth</span></span>

<span data-ttu-id="c3e3b-194">Öğretici [hesabı onaylama ve parola kurtarma ASP.NET Identity ile,](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) daha fazla ayrıntı için bu konuya gider.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-194">My tutorial [Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) goes into this topic with more details.</span></span>

<a id="dbg"></a>
## <a name="debugging-the-app"></a><span data-ttu-id="c3e3b-195">Uygulamada hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="c3e3b-195">Debugging the app</span></span>

<span data-ttu-id="c3e3b-196">Bağlantıyı içeren bir e-posta alamazsanız:</span><span class="sxs-lookup"><span data-stu-id="c3e3b-196">If you don't get an email containing the link:</span></span>

- <span data-ttu-id="c3e3b-197">Önemsiz veya istenmeyen posta klasörünüzü kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-197">Check your junk or spam folder.</span></span>
- <span data-ttu-id="c3e3b-198">SendGrid hesabınızda oturum açın ve [e-posta etkinliği bağlantısına](https://sendgrid.com/logs/index)tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-198">Log into your SendGrid account and click on the [Email Activity link](https://sendgrid.com/logs/index).</span></span>

<span data-ttu-id="c3e3b-199">Doğrulama bağlantısını e-posta olmadan test etmek için [Tamamlanan örneği](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)indirin.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-199">To test the verification link without email, download the [completed sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="c3e3b-200">Onay bağlantısı ve onay kodları sayfada görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-200">The confirmation link and confirmation codes will be displayed on the page.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="c3e3b-201">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c3e3b-201">Additional Resources</span></span>

- [<span data-ttu-id="c3e3b-202">Önerilen kaynakların ASP.NET Identity bağlantıları</span><span class="sxs-lookup"><span data-stu-id="c3e3b-202">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- <span data-ttu-id="c3e3b-203">[ASP.NET Identity Ile hesap onaylama ve parola kurtarma](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Parola kurtarma ve hesap onaylama hakkında daha fazla ayrıntıya gider.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-203">[Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Goes into more detail on password recovery and account confirmation.</span></span>
- <span data-ttu-id="c3e3b-204">[Facebook, Twitter, LinkedIn ve Google OAuth2 oturum açma Ile MVC 5 uygulaması](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) Bu öğreticide, Facebook ve Google OAuth 2 yetkilendirmesi ile ASP.NET MVC 5 uygulamasının nasıl yazılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-204">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) This tutorial shows you how to write an ASP.NET MVC 5 app with Facebook and Google OAuth 2 authorization.</span></span> <span data-ttu-id="c3e3b-205">Ayrıca, kimlik veritabanına nasıl ek veri ekleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-205">It also shows how to add additional data to the Identity database.</span></span>
- <span data-ttu-id="c3e3b-206">[Üyelik, OAuth ve SQL veritabanı Ile Azure 'Da güvenli bir ASP.NET MVC uygulaması dağıtın](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="c3e3b-206">[Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="c3e3b-207">Bu öğreticide, Azure dağıtımı, rollerle uygulamanızı güvenli hale getirme, Kullanıcı ve rolleri eklemek için üyelik API 'sini kullanma ve ek güvenlik özellikleri eklenir.</span><span class="sxs-lookup"><span data-stu-id="c3e3b-207">This tutorial adds Azure deployment, how to secure your app with roles, how to use the membership API to add users and roles, and additional security features.</span></span>
- [<span data-ttu-id="c3e3b-208">OAuth 2 için Google App oluşturma ve uygulamayı projeye bağlama</span><span class="sxs-lookup"><span data-stu-id="c3e3b-208">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [<span data-ttu-id="c3e3b-209">Facebook 'ta uygulama oluşturma ve uygulamayı projeye bağlama</span><span class="sxs-lookup"><span data-stu-id="c3e3b-209">Creating the app in Facebook and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [<span data-ttu-id="c3e3b-210">Projede SSL ayarlama</span><span class="sxs-lookup"><span data-stu-id="c3e3b-210">Setting up SSL in the Project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
