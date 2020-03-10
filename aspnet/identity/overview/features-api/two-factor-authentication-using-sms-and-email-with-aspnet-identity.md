---
uid: identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity
title: ASP.NET Identity-ASP.NET 4. x ile SMS ve e-posta kullanarak iki öğeli kimlik doğrulama
author: HaoK
description: Bu öğreticide, SMS ve email kullanarak Iki öğeli kimlik doğrulamasının (2FA) nasıl ayarlanacağı gösterilmektedir. Bu makale, Rick Anderson (@RickAndMSFT), PR... tarafından yazılmıştır.
ms.author: riande
ms.date: 09/15/2015
ms.assetid: 053e23c4-13c9-40fa-87cb-3e9b0823b31e
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 527b4392846e60dae0b216fdeabf21fd6618e4d7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616685"
---
# <a name="two-factorauthentication-using-sms-and-email-with-aspnet-identity"></a><span data-ttu-id="9ae16-104">ASP.NET Identity ile SMS ve e-posta kullanarak iki öğeli kimlik doğrulama</span><span class="sxs-lookup"><span data-stu-id="9ae16-104">Two-factor authentication using SMS and email with ASP.NET Identity</span></span>

<span data-ttu-id="9ae16-105">, [Hao Kung](https://github.com/HaoK), [Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://twitter.com/RickAndMSFT), [suwith Joshi](https://github.com/suhasj)</span><span class="sxs-lookup"><span data-stu-id="9ae16-105">by [Hao Kung](https://github.com/HaoK), [Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://twitter.com/RickAndMSFT), [Suhas Joshi](https://github.com/suhasj)</span></span>

> <span data-ttu-id="9ae16-106">Bu öğreticide, SMS ve email kullanarak Iki öğeli kimlik doğrulamasının (2FA) nasıl ayarlanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9ae16-106">This tutorial will show you how to set up Two-factor authentication (2FA) using SMS and email.</span></span>
> 
> <span data-ttu-id="9ae16-107">Bu makale, Rick Anderson ([@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)), Pranav Rastogi ([@rustd](https://twitter.com/rustd)), Hao Kung ve suwith Joshi tarafından yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="9ae16-107">This article was written by Rick Anderson ([@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)), Pranav Rastogi ([@rustd](https://twitter.com/rustd)), Hao Kung, and Suhas Joshi.</span></span> <span data-ttu-id="9ae16-108">NuGet örneği öncelikle Hao Kung tarafından yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="9ae16-108">The NuGet sample was written primarily by Hao Kung.</span></span>

<span data-ttu-id="9ae16-109">Bu konuda aşağıdakiler ele alınmaktadır:</span><span class="sxs-lookup"><span data-stu-id="9ae16-109">This topic covers the following:</span></span>

- [<span data-ttu-id="9ae16-110">Kimlik örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="9ae16-110">Building the Identity sample</span></span>](#build)
- [<span data-ttu-id="9ae16-111">Iki öğeli kimlik doğrulaması için SMS 'yi ayarlama</span><span class="sxs-lookup"><span data-stu-id="9ae16-111">Set up SMS for Two-factor authentication</span></span>](#SMS)
- [<span data-ttu-id="9ae16-112">Iki öğeli kimlik doğrulamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="9ae16-112">Enable Two-factor authentication</span></span>](#enable2)
- [<span data-ttu-id="9ae16-113">Iki öğeli kimlik doğrulama sağlayıcısını kaydetme</span><span class="sxs-lookup"><span data-stu-id="9ae16-113">How to register a Two-factor authentication provider</span></span>](#reg)
- [<span data-ttu-id="9ae16-114">Sosyal ve yerel oturum açma hesaplarını birleştirme</span><span class="sxs-lookup"><span data-stu-id="9ae16-114">Combine social and local login accounts</span></span>](#combine)
- [<span data-ttu-id="9ae16-115">Deneme yanılma saldırılarına karşı hesap kilitleme</span><span class="sxs-lookup"><span data-stu-id="9ae16-115">Account lockout from brute force attacks</span></span>](#lock)

<a id="build"></a>

## <a name="building-the-identity-sample"></a><span data-ttu-id="9ae16-116">Kimlik örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="9ae16-116">Building the Identity sample</span></span>

<span data-ttu-id="9ae16-117">Bu bölümde, birlikte çalışacağımız bir örneği indirmek için NuGet kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="9ae16-117">In this section, you'll use NuGet to download a sample we will work with.</span></span> <span data-ttu-id="9ae16-118">Web veya [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) [için Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) yükleyip çalıştırarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="9ae16-118">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="9ae16-119">Visual Studio [2013 güncelleştirme 2](https://go.microsoft.com/fwlink/?LinkId=390521) veya üstünü yükler.</span><span class="sxs-lookup"><span data-stu-id="9ae16-119">Install Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="9ae16-120">Uyarı: Bu öğreticiyi tamamlayabilmeniz için Visual Studio [2013 güncelleştirme 2](https://go.microsoft.com/fwlink/?LinkId=390521) ' nı yüklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae16-120">Warning: You must install Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) to complete this tutorial.</span></span>

1. <span data-ttu-id="9ae16-121">Yeni ***boş*** bir ASP.NET Web projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9ae16-121">Create a new ***empty*** ASP.NET Web project.</span></span>
2. <span data-ttu-id="9ae16-122">Paket Yöneticisi konsolunda aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="9ae16-122">In the Package Manager Console, enter the following the following commands:</span></span>  
  
    `Install-Package SendGrid`  
    `Install-Package -Prerelease Microsoft.AspNet.Identity.Samples`  
  
   <span data-ttu-id="9ae16-123">Bu öğreticide, SMS için e-posta ve [Twilio](https://www.twilio.com/) ya da [aspsms](https://www.aspsms.com/asp.net/identity/testcredits/) 'Yi göndermek için [SendGrid](http://sendgrid.com/) kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="9ae16-123">In this tutorial, we'll use [SendGrid](http://sendgrid.com/) to send email and [Twilio](https://www.twilio.com/) or [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) for sms texting.</span></span> <span data-ttu-id="9ae16-124">`Identity.Samples` paketi, ile çalışduğumuz kodu yüklüyor.</span><span class="sxs-lookup"><span data-stu-id="9ae16-124">The `Identity.Samples` package installs the code we will be working with.</span></span>
3. <span data-ttu-id="9ae16-125">[PROJEYI SSL kullanacak şekilde](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9ae16-125">Set the [project to use SSL](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
4. <span data-ttu-id="9ae16-126">*Isteğe bağlı*: SendGrid 'i bağlamak ve ardından uygulamayı çalıştırmak ve bir e-posta hesabı kaydettirmek Için [e-posta onaylama öğreticimin](account-confirmation-and-password-recovery-with-aspnet-identity.md) içindeki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="9ae16-126">*Optional*: Follow the instructions in my [Email confirmation tutorial](account-confirmation-and-password-recovery-with-aspnet-identity.md) to hook up SendGrid and then run the app and register an email account.</span></span>
5. <span data-ttu-id="9ae16-127">*Isteğe bağlı:* Örnek e-posta bağlantısı onay kodunu (hesap denetleyicisindeki `ViewBag.Link` kodu) kaldırın.</span><span class="sxs-lookup"><span data-stu-id="9ae16-127">*Optional:* Remove the demo email link confirmation code from the sample (The `ViewBag.Link` code in the account controller.</span></span> <span data-ttu-id="9ae16-128">Bkz. `DisplayEmail` ve `ForgotPasswordConfirmation` eylem yöntemleri ve Razor görünümleri).</span><span class="sxs-lookup"><span data-stu-id="9ae16-128">See the `DisplayEmail` and `ForgotPasswordConfirmation` action methods and razor views ).</span></span>
6. <span data-ttu-id="9ae16-129">*Isteğe bağlı:* `ViewBag.Status` kodunu Manage ve Account denetleyicilerinden ve *Views\account\verifycode. cshtml* ve *Views\manage\doğrulamaları Yphonenumber.exe* Razor görünümlerinden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="9ae16-129">*Optional:* Remove the `ViewBag.Status` code from the Manage and Account controllers and from the *Views\Account\VerifyCode.cshtml* and *Views\Manage\VerifyPhoneNumber.cshtml* razor views.</span></span> <span data-ttu-id="9ae16-130">Alternatif olarak, bu uygulamanın, e-posta ve SMS iletileri yedeklemek ve göndermek zorunda kalmadan yerel olarak nasıl çalıştığını test etmek için `ViewBag.Status` görüntüsünü koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae16-130">Alternatively, you can keep the `ViewBag.Status` display to test how this app works locally without having to hook up and send email and SMS messages.</span></span>

> [!NOTE]
> <span data-ttu-id="9ae16-131">Uyarı: Bu örnekteki güvenlik ayarlarından herhangi birini değiştirirseniz, üretimlerin uygulamanın, yapılan değişiklikleri açıkça çağıran bir güvenlik denetimine gitmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ae16-131">Warning: If you change any of the security settings in this sample, productions apps will need to undergo a security audit that explicitly calls out the changes made.</span></span>

<a id="SMS"></a>

## <a name="set-up-sms-for-two-factor-authentication"></a><span data-ttu-id="9ae16-132">Iki öğeli kimlik doğrulaması için SMS 'yi ayarlama</span><span class="sxs-lookup"><span data-stu-id="9ae16-132">Set up SMS for Two-factor authentication</span></span>

<span data-ttu-id="9ae16-133">Bu öğreticide, Twilio veya ASPSMS 'nin kullanılmasıyla ilgili yönergeler sağlanır ancak başka herhangi bir SMS sağlayıcısını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae16-133">This tutorial provides instructions for using either Twilio or ASPSMS but you can use any other SMS provider.</span></span>

1. <span data-ttu-id="9ae16-134">**SMS sağlayıcısıyla Kullanıcı hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="9ae16-134">**Creating a User Account with an SMS provider**</span></span>  
  
   <span data-ttu-id="9ae16-135">Bir [Twilio](https://www.twilio.com/try-twilio) veya [aspsms](https://www.aspsms.com/asp.net/identity/testcredits/) hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9ae16-135">Create a [Twilio](https://www.twilio.com/try-twilio) or an [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) account.</span></span>
2. <span data-ttu-id="9ae16-136">**Ek paketler yükleme veya hizmet başvuruları ekleme**</span><span class="sxs-lookup"><span data-stu-id="9ae16-136">**Installing additional packages or adding service references**</span></span>  
  
   <span data-ttu-id="9ae16-137">Twilio</span><span class="sxs-lookup"><span data-stu-id="9ae16-137">Twilio:</span></span>  
   <span data-ttu-id="9ae16-138">Paket Yöneticisi konsolunda aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="9ae16-138">In the Package Manager Console, enter the following command:</span></span>  
    `Install-Package Twilio`  
  
   <span data-ttu-id="9ae16-139">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="9ae16-139">ASPSMS:</span></span>  
   <span data-ttu-id="9ae16-140">Aşağıdaki hizmet başvurusunun eklenmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="9ae16-140">The following service reference needs to be added:</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image1.png)  
  
   <span data-ttu-id="9ae16-141">Adrestir</span><span class="sxs-lookup"><span data-stu-id="9ae16-141">Address:</span></span>  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   <span data-ttu-id="9ae16-142">Ad alanı:</span><span class="sxs-lookup"><span data-stu-id="9ae16-142">Namespace:</span></span>  
    `ASPSMSX2`
3. <span data-ttu-id="9ae16-143">**SMS sağlayıcısı Kullanıcı kimlik bilgileri alınıyor**</span><span class="sxs-lookup"><span data-stu-id="9ae16-143">**Figuring out SMS Provider User credentials**</span></span>  
  
   <span data-ttu-id="9ae16-144">Twilio</span><span class="sxs-lookup"><span data-stu-id="9ae16-144">Twilio:</span></span>  
   <span data-ttu-id="9ae16-145">Twilio hesabınızın **Pano** SEKMESINDEN **Hesap SID** 'sini ve **kimlik doğrulama belirtecini**kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="9ae16-145">From the **Dashboard** tab of your Twilio account, copy the **Account SID** and **Auth token**.</span></span>  
  
   <span data-ttu-id="9ae16-146">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="9ae16-146">ASPSMS:</span></span>  
   <span data-ttu-id="9ae16-147">Hesap ayarlarınızda **userKey** ' e gidin ve kendi kendine tanımlı **parolanızla**birlikte kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="9ae16-147">From your account settings, navigate to **Userkey** and copy it together with your self-defined **Password**.</span></span>  
  
   <span data-ttu-id="9ae16-148">Bu değerleri daha sonra `SMSAccountIdentification` ve `SMSAccountPassword` değişkenlerde depolayacağız.</span><span class="sxs-lookup"><span data-stu-id="9ae16-148">We will later store these values in the variables `SMSAccountIdentification` and `SMSAccountPassword` .</span></span>
4. <span data-ttu-id="9ae16-149">**SenderId/oluşturana belirtme**</span><span class="sxs-lookup"><span data-stu-id="9ae16-149">**Specifying SenderID / Originator**</span></span>  
  
   <span data-ttu-id="9ae16-150">Twilio</span><span class="sxs-lookup"><span data-stu-id="9ae16-150">Twilio:</span></span>  
   <span data-ttu-id="9ae16-151">**Sayılar** sekmesinden Twilio telefon numaranızı kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="9ae16-151">From the **Numbers** tab, copy your Twilio phone number.</span></span>  
  
   <span data-ttu-id="9ae16-152">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="9ae16-152">ASPSMS:</span></span>  
   <span data-ttu-id="9ae16-153">**Kilit açma/kaldırma** menüsünde, bir veya daha fazla kaynaktan yararlanın veya alfasayısal bir kaynağı (tüm ağlar tarafından desteklenmez) seçin.</span><span class="sxs-lookup"><span data-stu-id="9ae16-153">Within the **Unlock Originators** Menu, unlock one or more Originators or choose an alphanumeric Originator (Not supported by all networks).</span></span>  
  
   <span data-ttu-id="9ae16-154">Daha sonra bu değeri `SMSAccountFrom` değişkende depolayacağız.</span><span class="sxs-lookup"><span data-stu-id="9ae16-154">We will later store this value in the variable `SMSAccountFrom` .</span></span>
5. <span data-ttu-id="9ae16-155">**SMS sağlayıcısı kimlik bilgileri uygulamaya aktarılıyor**</span><span class="sxs-lookup"><span data-stu-id="9ae16-155">**Transferring SMS provider credentials into app**</span></span>  
  
   <span data-ttu-id="9ae16-156">Kimlik bilgilerini ve gönderici telefon numarasını uygulama için kullanılabilir yap:</span><span class="sxs-lookup"><span data-stu-id="9ae16-156">Make the credentials and sender phone number available to the app:</span></span>

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample1.cs)]

    > [!WARNING]
    > <span data-ttu-id="9ae16-157">Güvenlik-önemli verileri hiçbir şekilde kaynak kodunuzda depolamayin.</span><span class="sxs-lookup"><span data-stu-id="9ae16-157">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="9ae16-158">Hesap ve kimlik bilgileri, örneği basit tutmak için yukarıdaki koda eklenir.</span><span class="sxs-lookup"><span data-stu-id="9ae16-158">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="9ae16-159">Bkz. Jon Aton 'ın [ASP.NET MVC: kaynak denetiminden özel ayarları koruyun](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx).</span><span class="sxs-lookup"><span data-stu-id="9ae16-159">See Jon Atten's [ASP.NET MVC: Keep Private Settings Out of Source Control](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx).</span></span>
6. <span data-ttu-id="9ae16-160">**SMS sağlayıcısına veri aktarımı uygulama**</span><span class="sxs-lookup"><span data-stu-id="9ae16-160">**Implementation of data transfer to SMS provider**</span></span>  
  
   <span data-ttu-id="9ae16-161">*Uygulama\_Start\ıdentityconfig.cs* dosyasını `SmsService` sınıfını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9ae16-161">Configure the `SmsService`  class in the *App\_Start\IdentityConfig.cs* file.</span></span>  
  
   <span data-ttu-id="9ae16-162">Kullanılan SMS sağlayıcısına bağlı olarak **Twilio** ya da **aspsms** bölümünü etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="9ae16-162">Depending on the used SMS provider activate either the **Twilio** or the **ASPSMS** section:</span></span> 

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample2.cs)]
7. <span data-ttu-id="9ae16-163">Uygulamayı çalıştırın ve önceden kaydolduğunuz hesapla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9ae16-163">Run the app and log in with the account you previously registered.</span></span>
8. <span data-ttu-id="9ae16-164">`Manage` denetleyicisindeki `Index` Action metodunu etkinleştiren Kullanıcı KIMLIĞINIZ ' ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ae16-164">Click on your User ID, which activates the `Index` action method in `Manage` controller.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image2.png)
9. <span data-ttu-id="9ae16-165">Ekle’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ae16-165">Click Add.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image3.png)
10. <span data-ttu-id="9ae16-166">Birkaç saniye içinde doğrulama koduna sahip bir kısa mesaj alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="9ae16-166">In a few seconds you will get a text message with the verification code.</span></span> <span data-ttu-id="9ae16-167">Girin ve **Gönder**' e basın.</span><span class="sxs-lookup"><span data-stu-id="9ae16-167">Enter it and press **Submit**.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image4.png)
11. <span data-ttu-id="9ae16-168">Yönet görünümü telefon numaranızı eklendiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="9ae16-168">The Manage view shows your phone number was added.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image5.png)

### <a name="examine-the-code"></a><span data-ttu-id="9ae16-169">Kodu inceleme</span><span class="sxs-lookup"><span data-stu-id="9ae16-169">Examine the code</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample3.cs?highlight=2)]

<span data-ttu-id="9ae16-170">`Manage` denetleyicisindeki `Index` Action yöntemi, önceki eyleminizi temel alarak durum iletisini ayarlar ve yerel parolanızı değiştirme veya yerel hesap ekleme bağlantılarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="9ae16-170">The `Index` action method in `Manage` controller sets the status message based on your previous action and provides links to change your local password or add a local account.</span></span> <span data-ttu-id="9ae16-171">`Index` yöntemi Ayrıca bu tarayıcı için durumu veya 2FA telefon numaranızı, dış oturum açma bilgilerini, 2FA 'yı etkin ve unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9ae16-171">The `Index` method also displays the state or your 2FA phone number, external logins, 2FA enabled, and remember 2FA method for this browser(explained later).</span></span> <span data-ttu-id="9ae16-172">Başlık çubuğundaki kullanıcı KIMLIĞINIZE (e-posta) tıkladığınızda bir ileti geçmez.</span><span class="sxs-lookup"><span data-stu-id="9ae16-172">Clicking on your user ID (email) in the title bar doesn't pass a message.</span></span> <span data-ttu-id="9ae16-173">**Telefon numarasına tıkladığınızda:** bağlantı geçişlerini `Message=RemovePhoneSuccess` bir sorgu dizesi olarak kaldırın.</span><span class="sxs-lookup"><span data-stu-id="9ae16-173">Clicking on the **Phone Number : remove** link passes `Message=RemovePhoneSuccess` as a query string.</span></span>  
  
`https://localhost:44300/Manage?Message=RemovePhoneSuccess`

<span data-ttu-id="9ae16-174">[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]</span><span class="sxs-lookup"><span data-stu-id="9ae16-174">[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]</span></span>

<span data-ttu-id="9ae16-175">`AddPhoneNumber` Action yöntemi, SMS iletilerini alabilen bir telefon numarası girmek için bir iletişim kutusu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9ae16-175">The `AddPhoneNumber` action method displays a dialog box to enter a phone number that can receive SMS messages.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample4.cs)]

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image7.png)

<span data-ttu-id="9ae16-176">**Doğrulama kodu gönder** düğmesine tıkladığınızda telefon numarası HTTP POST `AddPhoneNumber` eylem yöntemine gönderilir.</span><span class="sxs-lookup"><span data-stu-id="9ae16-176">Clicking on the **Send verification code** button posts the phone number to the HTTP POST `AddPhoneNumber` action method.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample5.cs?highlight=12)]

<span data-ttu-id="9ae16-177">`GenerateChangePhoneNumberTokenAsync` yöntemi, SMS iletisinde ayarlanacak güvenlik belirtecini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9ae16-177">The `GenerateChangePhoneNumberTokenAsync` method generates the security token which will be set in the SMS message.</span></span> <span data-ttu-id="9ae16-178">SMS hizmeti yapılandırılmışsa, belirteç dize olarak gönderilir &quot;güvenlik kodunuz &lt;Token&gt;&quot;.</span><span class="sxs-lookup"><span data-stu-id="9ae16-178">If the SMS service has been configured, the token is sent as the string &quot;Your security code is &lt;token&gt;&quot;.</span></span> <span data-ttu-id="9ae16-179">`SmsService.SendAsync` yöntemi zaman uyumsuz olarak çağrılır, ardından uygulama, doğrulama kodunu girebileceğiniz `VerifyPhoneNumber` eylem yöntemine (aşağıdaki iletişim kutusunu gösterir) yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="9ae16-179">The `SmsService.SendAsync` method to is called asynchronously, then the app is redirected to the `VerifyPhoneNumber` action method (which displays the following dialog), where you can enter the verification code.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image8.png)

<span data-ttu-id="9ae16-180">Kodu girdikten ve Gönder ' e tıkladığınızda, kod HTTP POST `VerifyPhoneNumber` eylem yöntemine gönderilir.</span><span class="sxs-lookup"><span data-stu-id="9ae16-180">Once you enter the code and click submit, the code is posted to the HTTP POST `VerifyPhoneNumber` action method.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample6.cs)]

<span data-ttu-id="9ae16-181">`ChangePhoneNumberAsync` yöntemi, postalanan güvenlik kodunu denetler.</span><span class="sxs-lookup"><span data-stu-id="9ae16-181">The `ChangePhoneNumberAsync` method checks the posted security code.</span></span> <span data-ttu-id="9ae16-182">Kod doğruysa, telefon numarası `AspNetUsers` tablosunun `PhoneNumber` alanına eklenir.</span><span class="sxs-lookup"><span data-stu-id="9ae16-182">If the code is correct, the phone number is added to the `PhoneNumber` field of the `AspNetUsers` table.</span></span> <span data-ttu-id="9ae16-183">Bu çağrı başarılı olursa `SignInAsync` yöntemi çağrılır:</span><span class="sxs-lookup"><span data-stu-id="9ae16-183">If that call is successful, the `SignInAsync` method is called:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample7.cs)]

<span data-ttu-id="9ae16-184">`isPersistent` parametresi, kimlik doğrulama oturumunun birden çok istek arasında kalıcı olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="9ae16-184">The `isPersistent` parameter sets whether the authentication session is persisted across multiple requests.</span></span>

<span data-ttu-id="9ae16-185">Güvenlik profilinizi değiştirdiğinizde, *Aspnetusers* tablosunun `SecurityStamp` alanında yeni bir güvenlik damgası oluşturulur ve depolanır.</span><span class="sxs-lookup"><span data-stu-id="9ae16-185">When you change your security profile, a new security stamp is generated and stored in the `SecurityStamp` field of the *AspNetUsers* table.</span></span> <span data-ttu-id="9ae16-186">`SecurityStamp` alanının güvenlik tanımlama bilgisinden farklı olduğunu aklınızda yapın.</span><span class="sxs-lookup"><span data-stu-id="9ae16-186">Note, the `SecurityStamp` field is different from the security cookie.</span></span> <span data-ttu-id="9ae16-187">Güvenlik tanımlama bilgisi `AspNetUsers` tabloda (veya kimlik DB 'de başka herhangi bir yerde) depolanmaz.</span><span class="sxs-lookup"><span data-stu-id="9ae16-187">The security cookie is not stored in the `AspNetUsers` table (or anywhere else in the Identity DB).</span></span> <span data-ttu-id="9ae16-188">Güvenlik tanımlama bilgisi belirteci, [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) kullanılarak kendinden imzalanır ve `UserId, SecurityStamp` ile sona erme saati bilgileriyle oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9ae16-188">The security cookie token is self-signed using [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) and is created with the `UserId, SecurityStamp` and expiration time information.</span></span>

<span data-ttu-id="9ae16-189">Tanımlama bilgisi ara yazılımı her istek için tanımlama bilgisini denetler.</span><span class="sxs-lookup"><span data-stu-id="9ae16-189">The cookie middleware checks the cookie on each request.</span></span> <span data-ttu-id="9ae16-190">`Startup` sınıfındaki `SecurityStampValidator` yöntemi DB 'ye rastla ve `validateInterval`belirtilen şekilde güvenlik damgasını düzenli olarak denetler.</span><span class="sxs-lookup"><span data-stu-id="9ae16-190">The `SecurityStampValidator` method in the `Startup` class hits the DB and checks security stamp periodically, as specified with the `validateInterval`.</span></span> <span data-ttu-id="9ae16-191">Bu, güvenlik profilinizi değiştirmediğiniz müddetçe her 30 dakikada bir gerçekleşir (örneğimizde).</span><span class="sxs-lookup"><span data-stu-id="9ae16-191">This only happens every 30 minutes (in our sample) unless you change your security profile.</span></span> <span data-ttu-id="9ae16-192">Veritabanı gelişlerini en aza indirmek için 30 dakikalık Aralık seçildi.</span><span class="sxs-lookup"><span data-stu-id="9ae16-192">The 30 minute interval was chosen to minimize trips to the database.</span></span>

<span data-ttu-id="9ae16-193">Güvenlik profilinde herhangi bir değişiklik yapıldığında `SignInAsync` yönteminin çağrılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ae16-193">The `SignInAsync` method needs to be called when any change is made to the security profile.</span></span> <span data-ttu-id="9ae16-194">Güvenlik profili değiştiğinde, veritabanı `SecurityStamp` alanı güncelleştirir ve `SignInAsync` yöntemi çağrılmadan, *yalnızca* owın ardışık düzeni veritabanını (`validateInterval`) aşana kadar oturum açmış olursunuz.</span><span class="sxs-lookup"><span data-stu-id="9ae16-194">When the security profile changes, the database is updates the `SecurityStamp` field, and without calling the `SignInAsync` method you would stay logged in *only* until the next time the OWIN pipeline hits the database (the `validateInterval`).</span></span> <span data-ttu-id="9ae16-195">`SignInAsync` yöntemini hemen döndürecek şekilde değiştirerek ve tanımlama bilgisi `validateInterval` özelliğini 30 dakikadan 5 saniyeye ayarlayarak bunu test edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9ae16-195">You can test this by changing the `SignInAsync` method to return immediately, and setting the cookie `validateInterval` property from 30 minutes to 5 seconds:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample8.cs?highlight=3)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample9.cs?highlight=20-21)]

<span data-ttu-id="9ae16-196">Yukarıdaki kod değişiklikleriyle güvenlik profilinizi değiştirebilirsiniz (örneğin, **Iki faktörün durumunu etkin**olarak değiştirerek) ve `SecurityStampValidator.OnValidateIdentity` yöntemi başarısız olduğunda 5 saniye içinde oturumunuz açılır.</span><span class="sxs-lookup"><span data-stu-id="9ae16-196">With the above code changes, you can change your security profile (for example, by changing the state of **Two Factor Enabled**) and you will be logged out in 5 seconds when the `SecurityStampValidator.OnValidateIdentity` method fails.</span></span> <span data-ttu-id="9ae16-197">`SignInAsync` yönteminde dönüş satırını kaldırın, başka bir güvenlik profili değişikliği yapın ve oturumu açmadınız. `SignInAsync` yöntemi yeni bir güvenlik tanımlama bilgisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9ae16-197">Remove the return line in the `SignInAsync` method, make another security profile change and you will not be logged out. The `SignInAsync` method generates a new security cookie.</span></span>

<a id="enable2"></a>

## <a name="enable-two-factor-authentication"></a><span data-ttu-id="9ae16-198">İki öğeli kimlik doğrulamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="9ae16-198">Enable two-factor authentication</span></span>

<span data-ttu-id="9ae16-199">Örnek uygulamada, iki öğeli kimlik doğrulamayı (2FA) etkinleştirmek için Kullanıcı arabirimini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ae16-199">In the sample app, you need to use the UI to enable two-factor authentication (2FA).</span></span> <span data-ttu-id="9ae16-200">2FA 'yı etkinleştirmek için, gezinti çubuğundaki kullanıcı KIMLIĞINIZ (e-posta diğer adı) seçeneğine tıklayın.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="9ae16-200">To enable 2FA, click on your user ID (email alias) in the navigation bar.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)</span></span>  
<span data-ttu-id="9ae16-201">2FA 'yı etkinleştir ' e tıklayın.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="9ae16-201">Click on enable 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png)</span></span> <span data-ttu-id="9ae16-202">Oturumu kapatın ve yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9ae16-202">Log out, then log back in.</span></span> <span data-ttu-id="9ae16-203">E-postayı etkinleştirdiyseniz ( [önceki öğreticime](account-confirmation-and-password-recovery-with-aspnet-identity.md)bakın),/FA için SMS veya e-postayı seçebilirsiniz.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="9ae16-203">If you've enabled email (see my [previous tutorial](account-confirmation-and-password-recovery-with-aspnet-identity.md)), you can select the SMS or email for 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png)</span></span> <span data-ttu-id="9ae16-204">Kodu doğrula sayfası görüntülenir (SMS veya e-posta).![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="9ae16-204">The Verify Code page is displayed where you can enter the code (from SMS or email).![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png)</span></span> <span data-ttu-id="9ae16-205">**Bu tarayıcıya** göz atma onay kutusunun tıklanması, bu bilgisayar ve tarayıcıyla oturum açmak için 2FA kullanmanıza gerek duymasını da muaf tutacaktır.</span><span class="sxs-lookup"><span data-stu-id="9ae16-205">Clicking on the **Remember this browser** check box will exempt you from needing to use 2FA to log on with that computer and browser.</span></span> <span data-ttu-id="9ae16-206">2FA 'yı etkinleştirmek ve **Bu tarayıcıya** tıklanması, bilgisayarınıza erişimi olmadığı sürece hesabınıza erişmeye çalışan kötü amaçlı kullanıcılardan güçlü bir 2FA koruması sunacaktır.</span><span class="sxs-lookup"><span data-stu-id="9ae16-206">Enabling 2FA and clicking on the **Remember this browser** will provide you with strong 2FA protection from malicious users trying to access your account, as long as they don't have access to your computer.</span></span> <span data-ttu-id="9ae16-207">Bunu, düzenli olarak kullandığınız tüm özel makineler için yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae16-207">You can do this on any private machine you regularly use.</span></span> <span data-ttu-id="9ae16-208">**Bu tarayıcıyı aklınızda**bulundurarak, düzenli olarak kullanmayan BILGISAYARLARDAN 2FA 'nın ek güvenliğine sahip olursunuz ve kendi bilgisayarlarınızda 2FA 'yı kullanmaya gerek kalmadan rahatlığını elde edersiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae16-208">By setting **Remember this browser**, you get the added security of 2FA from computers you don't regularly use, and you get the convenience on not having to go through 2FA on your own computers.</span></span> 

<a id="reg"></a>
## <a name="how-to-register-a-two-factor-authentication-provider"></a><span data-ttu-id="9ae16-209">Iki öğeli kimlik doğrulama sağlayıcısını kaydetme</span><span class="sxs-lookup"><span data-stu-id="9ae16-209">How to register a Two-factor authentication provider</span></span>

<span data-ttu-id="9ae16-210">Yeni bir MVC projesi oluşturduğunuzda, *IdentityConfig.cs* dosyası iki öğeli kimlik doğrulama sağlayıcısını kaydetmek için aşağıdaki kodu içerir:</span><span class="sxs-lookup"><span data-stu-id="9ae16-210">When you create a new MVC project, the *IdentityConfig.cs* file contains the following code to register a Two-factor authentication provider:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample10.cs?highlight=22-35)]

## <a name="add-a-phone-number-for-2fa"></a><span data-ttu-id="9ae16-211">2FA için telefon numarası ekleyin</span><span class="sxs-lookup"><span data-stu-id="9ae16-211">Add a phone number for 2FA</span></span>

<span data-ttu-id="9ae16-212">`Manage` denetleyicisindeki `AddPhoneNumber` Action yöntemi bir güvenlik belirteci oluşturur ve bunu verdiğiniz telefon numarasına gönderir.</span><span class="sxs-lookup"><span data-stu-id="9ae16-212">The `AddPhoneNumber` action method in the `Manage` controller generates a security token and sends it to the phone number you have provided.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample11.cs)]

<span data-ttu-id="9ae16-213">Belirteci gönderdikten sonra, `VerifyPhoneNumber` Action yöntemine yeniden yönlendirilir. burada, kodu 2FA için kaydetmek üzere kodu girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae16-213">After sending the token, it redirects to the `VerifyPhoneNumber` action method, where you can enter the code to register SMS for 2FA.</span></span> <span data-ttu-id="9ae16-214">Telefon numarasını doğrulayana kadar SMS 2FA kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="9ae16-214">SMS 2FA is not used until you have verified the phone number.</span></span>

## <a name="enabling-2fa"></a><span data-ttu-id="9ae16-215">2FA 'yı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="9ae16-215">Enabling 2FA</span></span>

<span data-ttu-id="9ae16-216">`EnableTFA` Action yöntemi 2FA 'yı sunar:</span><span class="sxs-lookup"><span data-stu-id="9ae16-216">The `EnableTFA` action method enables 2FA:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample12.cs)]

<span data-ttu-id="9ae16-217">`SignInAsync`, 2FA 'yı etkinleştir güvenlik profilinde bir değişiklik olduğundan, bunun çağrılması gerektiğini aklınızda olun.</span><span class="sxs-lookup"><span data-stu-id="9ae16-217">Note the `SignInAsync` must be called because enable 2FA is a change to the security profile.</span></span> <span data-ttu-id="9ae16-218">2FA etkinleştirildiğinde, kullanıcının kaydoldukları 2FA yaklaşımlarını (örnekteki SMS ve e-posta) kullanarak oturum açması için 2FA kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ae16-218">When 2FA is enabled, the user will need to use 2FA to log in, using the 2FA approaches they have registered (SMS and email in the sample).</span></span>

<span data-ttu-id="9ae16-219">QR kod oluşturucuları gibi daha fazla 2FA sağlayıcısı ekleyebilir veya size kendinizinkini yazabilirsiniz (bkz. [ASP.NET Identity Google Authenticator kullanma](https://www.jerriepelser.com//blog/using-google-authenticator-asp-net-identity/)).</span><span class="sxs-lookup"><span data-stu-id="9ae16-219">You can add more 2FA providers such as QR code generators or you can write you own (See [Using Google Authenticator with ASP.NET Identity](https://www.jerriepelser.com//blog/using-google-authenticator-asp-net-identity/)).</span></span>

> [!NOTE]
> <span data-ttu-id="9ae16-220">2FA kodları [zamana bağlı bir kerelik parola algoritması](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm) kullanılarak oluşturulur ve kodlar altı dakika için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="9ae16-220">The 2FA codes are generated using [Time-based One-time Password Algorithm](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm) and codes are valid for six minutes.</span></span> <span data-ttu-id="9ae16-221">Kodu girmek için altı dakikadan fazla süre alırsanız geçersiz bir kod hata iletisi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="9ae16-221">If you take more than six minutes to enter the code, you'll get an Invalid code error message.</span></span>

<a id="combine"></a>

## <a name="combine-social-and-local-login-accounts"></a><span data-ttu-id="9ae16-222">Sosyal ve yerel oturum açma hesaplarını birleştirme</span><span class="sxs-lookup"><span data-stu-id="9ae16-222">Combine social and local login accounts</span></span>

<span data-ttu-id="9ae16-223">E-posta bağlantısına tıklayarak Yerel ve sosyal hesapları birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae16-223">You can combine local and social accounts by clicking on your email link.</span></span> <span data-ttu-id="9ae16-224">Aşağıdaki dizide &quot;RickAndMSFT@gmail.com&quot; önce yerel bir oturum açma olarak oluşturulur, ancak önce hesabı önce bir sosyal oturum günlüğü olarak oluşturabilir, sonra da yerel bir oturum açma ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae16-224">In the following sequence &quot;RickAndMSFT@gmail.com&quot; is first created as a local login, but you can create the account as a social log in first, then add a local login.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image13.png)

<span data-ttu-id="9ae16-225">**Yönet** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ae16-225">Click on the **Manage** link.</span></span> <span data-ttu-id="9ae16-226">Bu hesapla ilişkili 0 harici (sosyal oturumlar) ' a göz önüne alın.</span><span class="sxs-lookup"><span data-stu-id="9ae16-226">Note the 0 external (social logins) associated with this account.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image14.png)

<span data-ttu-id="9ae16-227">Başka bir oturum açma hizmetine bağlantıyı tıklatın ve uygulama isteklerini kabul edin.</span><span class="sxs-lookup"><span data-stu-id="9ae16-227">Click the link to another log in service and accept the app requests.</span></span> <span data-ttu-id="9ae16-228">İki hesap birleştirildi, herhangi bir hesapla oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae16-228">The two accounts have been combined, you will be able to log on with either account.</span></span> <span data-ttu-id="9ae16-229">Kullanıcılarınızın, sosyal oturum açma kimlik doğrulaması hizmeti kapatılmış veya sosyal hesaplarına erişimi kaybetmiş olması olasılığına karşı yerel hesaplar eklemesini isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae16-229">You might want your users to add local accounts in case their social log in authentication service is down, or more likely they have lost access to their social account.</span></span>

<span data-ttu-id="9ae16-230">Aşağıdaki görüntüde, Tom bir sosyal oturum günlüğü (dış oturum açmalarından görebileceğiniz **: 1** gösterilen sayfada görebilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="9ae16-230">In the following image, Tom is a social log in (which you can see from the **External Logins: 1** shown on the page).</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image15.png)

<span data-ttu-id="9ae16-231">**Parola Seç** ' e tıkladığınızda, aynı hesapla ilişkili bir yerel günlük eklemenize izin verir.</span><span class="sxs-lookup"><span data-stu-id="9ae16-231">Clicking on **Pick a password** allows you to add a local log on associated with the same account.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image16.png)

<a id="lock"></a>

## <a name="account-lockout-from-brute-force-attacks"></a><span data-ttu-id="9ae16-232">Deneme yanılma saldırılarına karşı hesap kilitleme</span><span class="sxs-lookup"><span data-stu-id="9ae16-232">Account lockout from brute force attacks</span></span>

<span data-ttu-id="9ae16-233">Kullanıcı kilitlemeyi etkinleştirerek, uygulamanızdaki hesapları sözlük saldırılarına karşı koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae16-233">You can protect the accounts on your app from dictionary attacks by enabling user lockout.</span></span> <span data-ttu-id="9ae16-234">`ApplicationUserManager Create` yönteminde aşağıdaki kod kilitleme yapılandırmasını yapılandırır:</span><span class="sxs-lookup"><span data-stu-id="9ae16-234">The following code in the `ApplicationUserManager Create` method configures lock out:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample13.cs)]

<span data-ttu-id="9ae16-235">Yukarıdaki kod yalnızca iki öğeli kimlik doğrulaması için kilitlemeyi sunar.</span><span class="sxs-lookup"><span data-stu-id="9ae16-235">The code above enables lockout for two factor authentication only.</span></span> <span data-ttu-id="9ae16-236">Hesap denetleyicisinin `Login` yönteminde `shouldLockout` true olarak değiştirerek oturum açma işlemleri için kilitlemeyi etkinleştirebiliriz, ancak hesabı [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) oturum açma saldırılarına açık hale getiren oturum açma işlemleri için oturumu açmamız önerilir.</span><span class="sxs-lookup"><span data-stu-id="9ae16-236">While you can enable lock out for logins by changing `shouldLockout` to true in the `Login` method of the account controller, we recommend you not enable lock out for logins because it makes the account susceptible to [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) login attacks.</span></span> <span data-ttu-id="9ae16-237">Örnek kodda, `ApplicationDbInitializer Seed` yönteminde oluşturulan yönetici hesabı için kilitleme devre dışıdır:</span><span class="sxs-lookup"><span data-stu-id="9ae16-237">In the sample code, lockout is disabled for the admin account created in the `ApplicationDbInitializer Seed` method:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample14.cs?highlight=19)]

## <a name="requiring-a-user-to-have-a-validated-email-account"></a><span data-ttu-id="9ae16-238">Kullanıcının onaylanmış bir e-posta hesabına sahip olmasını gerektirme</span><span class="sxs-lookup"><span data-stu-id="9ae16-238">Requiring a user to have a validated email account</span></span>

<span data-ttu-id="9ae16-239">Aşağıdaki kod, oturum açabilmeleri için bir kullanıcının doğrulanan bir e-posta hesabına sahip olmasını gerektirir:</span><span class="sxs-lookup"><span data-stu-id="9ae16-239">The following code requires a user to have a validated email account before they can log in:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample15.cs?highlight=8-17)]

## <a name="how-signinmanager-checks-for-2fa-requirement"></a><span data-ttu-id="9ae16-240">SignInManager 'ın 2FA gereksinimini denetlemesi</span><span class="sxs-lookup"><span data-stu-id="9ae16-240">How SignInManager checks for 2FA requirement</span></span>

<span data-ttu-id="9ae16-241">Hem yerel oturum açma hem de sosyal oturum açma, 2FA 'nın etkin olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="9ae16-241">Both the local log in and social log in check to see if 2FA is enabled.</span></span> <span data-ttu-id="9ae16-242">2FA etkinleştirilmişse, `SignInManager` oturum açma yöntemi `SignInStatus.RequiresVerification`döndürür ve Kullanıcı, günlüğü sırayla tamamlayacak kodu girmek zorunda olabilecekleri `SendCode` eylem yöntemine yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="9ae16-242">If 2FA is enabled, the `SignInManager` logon method returns `SignInStatus.RequiresVerification`, and the user will be redirected to the `SendCode` action method, where they will have to enter the code to complete the log in sequence.</span></span> <span data-ttu-id="9ae16-243">Kullanıcı yerel tanımlama bilgisinde RememberMe ayarlandıysa, `SignInManager` `SignInStatus.Success` döndürür ve 2FA 'ya gitmeleri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="9ae16-243">If the user has RememberMe is set on the users local cookie, the `SignInManager` will return `SignInStatus.Success` and they will not have to go through 2FA.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample16.cs?highlight=20-22)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample17.cs?highlight=10-11,17-18)]

<span data-ttu-id="9ae16-244">Aşağıdaki kod `SendCode` Action yöntemini gösterir.</span><span class="sxs-lookup"><span data-stu-id="9ae16-244">The following code shows the `SendCode` action method.</span></span> <span data-ttu-id="9ae16-245">Kullanıcı için etkinleştirilen tüm 2FA yöntemleriyle bir [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9ae16-245">A [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) is created with all the 2FA methods enabled for the user.</span></span> <span data-ttu-id="9ae16-246">[SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) , kullanıcının 2FA yaklaşımını seçmesini sağlayan [DropDownListFor](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx) Helper 'a geçirilir (genellikle e-posta ve SMS).</span><span class="sxs-lookup"><span data-stu-id="9ae16-246">The [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) is passed to the [DropDownListFor](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx) helper, which allows the user to select the 2FA approach (typically email and SMS).</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample18.cs)]

<span data-ttu-id="9ae16-247">Kullanıcı 2FA yaklaşımını gönderdikten sonra, `HTTP POST SendCode` Action yöntemi çağrılır, `SignInManager` 2FA kodunu gönderir ve Kullanıcı oturum açma işlemini tamamlamaya yönelik kodu girebilecekleri `VerifyCode` Action yöntemine yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="9ae16-247">Once the user posts the 2FA approach, the `HTTP POST SendCode` action method is called, the `SignInManager` sends the 2FA code, and the user is redirected to the `VerifyCode` action method where they can enter the code to complete the log in.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample19.cs?highlight=3,13-14,18)]

## <a name="2fa-lockout"></a><span data-ttu-id="9ae16-248">2FA kilitleme</span><span class="sxs-lookup"><span data-stu-id="9ae16-248">2FA Lockout</span></span>

<span data-ttu-id="9ae16-249">Oturum açma parolası denemesi hatalarında hesap kilitlemeyi ayarlayabilseniz de bu yaklaşım, oturum açma bilgilerinizi [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) kilitlenmelerinden kaynaklanabilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="9ae16-249">Although you can set account lockout on login password attempt failures, that approach makes your login susceptible to [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) lockouts.</span></span> <span data-ttu-id="9ae16-250">Hesap kilitlemeyi yalnızca 2FA ile kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="9ae16-250">We recommend you use account lockout only with 2FA.</span></span> <span data-ttu-id="9ae16-251">`ApplicationUserManager` oluşturulduğunda, örnek kod 2FA kilitleme ve `MaxFailedAccessAttemptsBeforeLockout` beş olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="9ae16-251">When the `ApplicationUserManager` is created, the sample code sets 2FA lockout and `MaxFailedAccessAttemptsBeforeLockout` to five.</span></span> <span data-ttu-id="9ae16-252">Kullanıcı oturum açtıktan sonra (yerel hesap veya sosyal hesap aracılığıyla), 2FA 'da başarısız olan her girişim depolanır ve en fazla deneme sayısına ulaşıldığında Kullanıcı beş dakika boyunca kilitlenir (kilitleme süresini `DefaultAccountLockoutTimeSpan`) olarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae16-252">Once a user logs in (through local account or social account), each failed attempt at 2FA is stored, and if the maximum attempts is reached, the user is locked out for five minutes (you can set the lock out time with `DefaultAccountLockoutTimeSpan`).</span></span>

<a id="addRes"></a>

## <a name="additional-resources"></a><span data-ttu-id="9ae16-253">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="9ae16-253">Additional Resources</span></span>

- <span data-ttu-id="9ae16-254">[Önerilen kaynakları ASP.NET Identity](../getting-started/aspnet-identity-recommended-resources.md) Kimlik bloglarının, videoların, öğreticilerin ve harika bağlantıların tüm listesini listeleyin.</span><span class="sxs-lookup"><span data-stu-id="9ae16-254">[ASP.NET Identity Recommended Resources](../getting-started/aspnet-identity-recommended-resources.md) Complete list of Identity blogs, videos, tutorials and great SO links.</span></span>
- <span data-ttu-id="9ae16-255">[Facebook, Twitter, LinkedIn ve Google OAuth2 oturum açma Ile MVC 5 uygulaması](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) Ayrıca, profil bilgilerinin kullanıcılar tablosuna nasıl ekleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="9ae16-255">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) also shows how to add profile information to the users table.</span></span>
- <span data-ttu-id="9ae16-256">[ASP.NET MVC ve kimlik 2,0:](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) John Aton 'un temellerini anlama.</span><span class="sxs-lookup"><span data-stu-id="9ae16-256">[ASP.NET MVC and Identity 2.0: Understanding the Basics](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) by John Atten.</span></span>
- [<span data-ttu-id="9ae16-257">ASP.NET Identity ile hesap onaylama ve parola kurtarma</span><span class="sxs-lookup"><span data-stu-id="9ae16-257">Account Confirmation and Password Recovery with ASP.NET Identity</span></span>](account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [<span data-ttu-id="9ae16-258">ASP.NET Identity’ye Giriş</span><span class="sxs-lookup"><span data-stu-id="9ae16-258">Introduction to ASP.NET Identity</span></span>](../getting-started/introduction-to-aspnet-identity.md)
- <span data-ttu-id="9ae16-259">Pranav Oystogi tarafından [RTM ASP.NET Identity 2.0.0 duyurusu](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) .</span><span class="sxs-lookup"><span data-stu-id="9ae16-259">[Announcing RTM of ASP.NET Identity 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) by Pranav Rastogi.</span></span>
- <span data-ttu-id="9ae16-260">[ASP.NET Identity 2,0: John Aton tarafından hesap doğrulama ve Iki öğeli yetkilendirme ayarlama](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) .</span><span class="sxs-lookup"><span data-stu-id="9ae16-260">[ASP.NET Identity 2.0: Setting Up Account Validation and Two-Factor Authorization](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) by John Atten.</span></span>
