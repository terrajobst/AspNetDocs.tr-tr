---
uid: mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
title: SMS ve e-posta Iki öğeli kimlik doğrulaması ile ASP.NET MVC 5 uygulaması | Microsoft Docs
author: Rick-Anderson
description: Bu öğreticide, Iki öğeli kimlik doğrulama ile bir ASP.NET MVC 5 Web uygulaması oluşturma gösterilmektedir. Güvenli bir ASP.NET MVC 5 Web uygulaması oluşturmayı ile tamamlamalısınız...
ms.author: riande
ms.date: 08/20/2015
ms.assetid: f50a5cdb-c06a-46ed-aa14-fc5b049dc8dc
msc.legacyurl: /mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: c14149d802bfc0a227a839a2981dc3e8a3849c25
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457602"
---
# <a name="aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication"></a><span data-ttu-id="ad230-104">SMS ve e-posta iki öğeli kimlik doğrulaması özellikli ASP.NET MVC 5 uygulaması</span><span class="sxs-lookup"><span data-stu-id="ad230-104">ASP.NET MVC 5 app with SMS and email Two-Factor Authentication</span></span>

<span data-ttu-id="ad230-105">[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından</span><span class="sxs-lookup"><span data-stu-id="ad230-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="ad230-106">Bu öğreticide, Iki öğeli kimlik doğrulama ile bir ASP.NET MVC 5 Web uygulaması oluşturma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ad230-106">This tutorial shows you how to build an ASP.NET MVC 5 web app with Two-Factor Authentication.</span></span> <span data-ttu-id="ad230-107">Devam etmeden önce [, oturum açma, e-posta onayı ve parola sıfırlama ile güvenli bir ASP.NET MVC 5 Web uygulaması oluşturma](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) işleminin tamamlanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad230-107">You should complete [Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) before proceeding.</span></span> <span data-ttu-id="ad230-108">Tamamlanmış uygulamayı [buradan](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad230-108">You can download the completed application [here](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="ad230-109">Bu indirme, e-posta veya SMS sağlayıcısı ayarlamadan e-posta onayını ve SMS 'yi test etmenize olanak sağlayan hata ayıklama yardımcıları içerir.</span><span class="sxs-lookup"><span data-stu-id="ad230-109">The download contains debugging helpers that let you test email confirmation and SMS without setting up an email or SMS provider.</span></span>
> 
> <span data-ttu-id="ad230-110">Bu öğretici [Rick Anderson](https://blogs.msdn.com/rickAndy) tarafından yazılmıştır (Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span><span class="sxs-lookup"><span data-stu-id="ad230-110">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>

- [<span data-ttu-id="ad230-111">ASP.NET MVC uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad230-111">Create an ASP.NET MVC app</span></span>](#createMvc)
- [<span data-ttu-id="ad230-112">Iki öğeli kimlik doğrulaması için SMS 'yi ayarlama</span><span class="sxs-lookup"><span data-stu-id="ad230-112">Set up SMS for Two-factor authentication</span></span>](#SMS)
- [<span data-ttu-id="ad230-113">Iki öğeli kimlik doğrulamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="ad230-113">Enable Two-factor authentication</span></span>](#enable2)
- [<span data-ttu-id="ad230-114">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ad230-114">Additional Resources</span></span>](#addRes)

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a><span data-ttu-id="ad230-115">ASP.NET MVC uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad230-115">Create an ASP.NET MVC app</span></span>

<span data-ttu-id="ad230-116">Web veya [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) [için Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) yükleyip çalıştırarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="ad230-116">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="ad230-117">[Visual Studio 2013 güncelleştirme 3](https://go.microsoft.com/fwlink/?LinkId=390465) veya üstünü yükler.</span><span class="sxs-lookup"><span data-stu-id="ad230-117">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="ad230-118">Uyarı: devam etmeden önce [oturum açma, e-posta onayı ve parola sıfırlama ile güvenli bir ASP.NET MVC 5 Web uygulaması oluşturma](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) işleminin tamamlanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad230-118">Warning: You should complete [Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) before proceeding.</span></span> <span data-ttu-id="ad230-119">Bu öğreticiyi tamamlayabilmeniz için [Visual Studio 2013 güncelleştirme 3](https://go.microsoft.com/fwlink/?LinkId=390465) veya sonraki bir sürümü yüklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="ad230-119">You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>

1. <span data-ttu-id="ad230-120">Yeni bir ASP.NET Web projesi oluşturun ve MVC şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="ad230-120">Create a new ASP.NET Web project and select the MVC template.</span></span> <span data-ttu-id="ad230-121">Web Forms Ayrıca ASP.NET Identity destekler, böylece bir Web Forms uygulamasındaki benzer adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad230-121">Web Forms also supports ASP.NET Identity, so you could follow similar steps in a web forms app.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image1.png)
2. <span data-ttu-id="ad230-122">Varsayılan kimlik doğrulamasını **bireysel kullanıcı hesapları**olarak bırakın.</span><span class="sxs-lookup"><span data-stu-id="ad230-122">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="ad230-123">Uygulamayı Azure 'da barındırmak isterseniz onay kutusunu işaretli bırakın.</span><span class="sxs-lookup"><span data-stu-id="ad230-123">If you'd like to host the app in Azure, leave the check box checked.</span></span> <span data-ttu-id="ad230-124">Öğreticide daha sonra Azure 'a dağıtacağız.</span><span class="sxs-lookup"><span data-stu-id="ad230-124">Later in the tutorial we will deploy to Azure.</span></span> <span data-ttu-id="ad230-125">[Bir Azure hesabını ücretsiz olarak açabilirsiniz](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="ad230-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
3. <span data-ttu-id="ad230-126">[PROJEYI SSL kullanacak şekilde](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ad230-126">Set the [project to use SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>

<a id="SMS"></a>
## <a name="set-up-sms-for-two-factor-authentication"></a><span data-ttu-id="ad230-127">Iki öğeli kimlik doğrulaması için SMS 'yi ayarlama</span><span class="sxs-lookup"><span data-stu-id="ad230-127">Set up SMS for Two-factor authentication</span></span>

<span data-ttu-id="ad230-128">Bu öğreticide, Twilio veya ASPSMS 'nin kullanılmasıyla ilgili yönergeler sağlanır ancak başka herhangi bir SMS sağlayıcısını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad230-128">This tutorial provides instructions for using either Twilio or ASPSMS but you can use any other SMS provider.</span></span>

1. <span data-ttu-id="ad230-129">**SMS sağlayıcısıyla Kullanıcı hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="ad230-129">**Creating a User Account with an SMS provider**</span></span>  
  
   <span data-ttu-id="ad230-130">Bir [Twilio](https://www.twilio.com/try-twilio) veya [aspsms](https://www.aspsms.com/asp.net/identity/testcredits/) hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ad230-130">Create a [Twilio](https://www.twilio.com/try-twilio) or an [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) account.</span></span>
2. <span data-ttu-id="ad230-131">**Ek paketler yükleme veya hizmet başvuruları ekleme**</span><span class="sxs-lookup"><span data-stu-id="ad230-131">**Installing additional packages or adding service references**</span></span>  
  
   <span data-ttu-id="ad230-132">Twilio</span><span class="sxs-lookup"><span data-stu-id="ad230-132">Twilio:</span></span>  
   <span data-ttu-id="ad230-133">Paket Yöneticisi konsolunda aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="ad230-133">In the Package Manager Console, enter the following command:</span></span>  
    `Install-Package Twilio`  
  
   <span data-ttu-id="ad230-134">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="ad230-134">ASPSMS:</span></span>  
   <span data-ttu-id="ad230-135">Aşağıdaki hizmet başvurusunun eklenmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="ad230-135">The following service reference needs to be added:</span></span>  
  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image2.png)  
  
   <span data-ttu-id="ad230-136">Adrestir</span><span class="sxs-lookup"><span data-stu-id="ad230-136">Address:</span></span>  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   <span data-ttu-id="ad230-137">{1&gt;Ad Alanı:&lt;1}</span><span class="sxs-lookup"><span data-stu-id="ad230-137">Namespace:</span></span>  
    `ASPSMSX2`
3. <span data-ttu-id="ad230-138">**SMS sağlayıcısı Kullanıcı kimlik bilgileri alınıyor**</span><span class="sxs-lookup"><span data-stu-id="ad230-138">**Figuring out SMS Provider User credentials**</span></span>  
  
   <span data-ttu-id="ad230-139">Twilio</span><span class="sxs-lookup"><span data-stu-id="ad230-139">Twilio:</span></span>  
   <span data-ttu-id="ad230-140">Twilio hesabınızın **Pano** SEKMESINDEN **Hesap SID** 'sini ve **kimlik doğrulama belirtecini**kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="ad230-140">From the **Dashboard** tab of your Twilio account, copy the **Account SID** and **Auth token**.</span></span>  
  
   <span data-ttu-id="ad230-141">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="ad230-141">ASPSMS:</span></span>  
   <span data-ttu-id="ad230-142">Hesap ayarlarınızda **userKey** ' e gidin ve kendi kendine tanımlı **parolanızla**birlikte kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="ad230-142">From your account settings, navigate to **Userkey** and copy it together with your self-defined **Password**.</span></span>  
  
   <span data-ttu-id="ad230-143">Daha sonra bu değerleri anahtarlar içindeki *Web. config* dosyasında depolayacağız `"SMSAccountIdentification"` ve `"SMSAccountPassword"`.</span><span class="sxs-lookup"><span data-stu-id="ad230-143">We will later store these values in the *web.config* file within the keys `"SMSAccountIdentification"` and `"SMSAccountPassword"` .</span></span>
4. <span data-ttu-id="ad230-144">**SenderId/oluşturana belirtme**</span><span class="sxs-lookup"><span data-stu-id="ad230-144">**Specifying SenderID / Originator**</span></span>  
  
   <span data-ttu-id="ad230-145">Twilio</span><span class="sxs-lookup"><span data-stu-id="ad230-145">Twilio:</span></span>  
   <span data-ttu-id="ad230-146">**Sayılar** sekmesinden Twilio telefon numaranızı kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="ad230-146">From the **Numbers** tab, copy your Twilio phone number.</span></span>  
  
   <span data-ttu-id="ad230-147">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="ad230-147">ASPSMS:</span></span>  
   <span data-ttu-id="ad230-148">**Kilit açma/kaldırma** menüsünde, bir veya daha fazla kaynaktan yararlanın veya alfasayısal bir kaynağı (tüm ağlar tarafından desteklenmez) seçin.</span><span class="sxs-lookup"><span data-stu-id="ad230-148">Within the **Unlock Originators** Menu, unlock one or more Originators or choose an alphanumeric Originator (Not supported by all networks).</span></span>  
  
   <span data-ttu-id="ad230-149">Daha sonra bu değeri, anahtar `"SMSAccountFrom"` içindeki *Web. config* dosyasında depolayacağız.</span><span class="sxs-lookup"><span data-stu-id="ad230-149">We will later store this value in the *web.config* file within the key `"SMSAccountFrom"` .</span></span>
5. <span data-ttu-id="ad230-150">**SMS sağlayıcısı kimlik bilgileri uygulamaya aktarılıyor**</span><span class="sxs-lookup"><span data-stu-id="ad230-150">**Transferring SMS provider credentials into app**</span></span>  
  
   <span data-ttu-id="ad230-151">Kimlik bilgilerini ve gönderici telefon numarasını uygulama için kullanılabilir hale getirin.</span><span class="sxs-lookup"><span data-stu-id="ad230-151">Make the credentials and sender phone number available to the app.</span></span> <span data-ttu-id="ad230-152">Şeyleri basit tutmak için bu değerleri *Web. config* dosyasında depolayacağız.</span><span class="sxs-lookup"><span data-stu-id="ad230-152">To keep things simple we will store these values in the *web.config* file.</span></span> <span data-ttu-id="ad230-153">Azure 'a dağıtırken, verileri Web sitesi Yapılandır sekmesindeki **uygulama ayarları** bölümünde güvenli bir şekilde depolayabiliriz.</span><span class="sxs-lookup"><span data-stu-id="ad230-153">When we deploy to Azure, we can store the values securely in the **app settings** section on the web site configure tab.</span></span> 

    [!code-xml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample1.xml?highlight=8-10)]

    > [!WARNING]
    > <span data-ttu-id="ad230-154">Güvenlik-önemli verileri hiçbir şekilde kaynak kodunuzda depolamayin.</span><span class="sxs-lookup"><span data-stu-id="ad230-154">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="ad230-155">Hesap ve kimlik bilgileri, örneği basit tutmak için yukarıdaki koda eklenir.</span><span class="sxs-lookup"><span data-stu-id="ad230-155">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="ad230-156">[ASP.net ve Azure 'a parola ve diğer hassas verileri dağıtmaya yönelik en iyi uygulamalar](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="ad230-156">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
6. <span data-ttu-id="ad230-157">**SMS sağlayıcısına veri aktarımı uygulama**</span><span class="sxs-lookup"><span data-stu-id="ad230-157">**Implementation of data transfer to SMS provider**</span></span>  
  
   <span data-ttu-id="ad230-158">*Uygulama\_Start\ıdentityconfig.cs* dosyasını `SmsService` sınıfını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ad230-158">Configure the `SmsService`  class in the *App\_Start\IdentityConfig.cs* file.</span></span>  
  
   <span data-ttu-id="ad230-159">Kullanılan SMS sağlayıcısına bağlı olarak **Twilio** ya da **aspsms** bölümünü etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="ad230-159">Depending on the used SMS provider activate either the **Twilio** or the **ASPSMS** section:</span></span> 

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample2.cs)]
7. <span data-ttu-id="ad230-160">*Views\manage\ındex.cshtml* Razor görünümünü güncelleştirin: (Note: çıkış kodundaki açıklamaları kaldırın, aşağıdaki kodu kullanın.)</span><span class="sxs-lookup"><span data-stu-id="ad230-160">Update the *Views\Manage\Index.cshtml* Razor view: (note: don't just remove the comments in the exiting code, use the code below.)</span></span>  

    [!code-cshtml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample3.cshtml?highlight=29-66)]
8. <span data-ttu-id="ad230-161">`ManageController` içindeki `EnableTwoFactorAuthentication` ve `DisableTwoFactorAuthentication` eylemi yöntemlerinin[[Validateantiforgerytoken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx) özniteliğine sahip olduğunu doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="ad230-161">Verify the `EnableTwoFactorAuthentication` and `DisableTwoFactorAuthentication` action methods in the `ManageController` have the[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx) attribute:</span></span>  

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample4.cs?highlight=3,16)]
9. <span data-ttu-id="ad230-162">Uygulamayı çalıştırın ve önceden kaydolduğunuz hesapla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ad230-162">Run the app and log in with the account you previously registered.</span></span>
10. <span data-ttu-id="ad230-163">`Manage` denetleyicisindeki `Index` Action metodunu etkinleştiren Kullanıcı KIMLIĞINIZ ' ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ad230-163">Click on your User ID, which activates the `Index` action method in `Manage` controller.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image3.png)
11. <span data-ttu-id="ad230-164">Ekle'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ad230-164">Click Add.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image4.png)
12. <span data-ttu-id="ad230-165">`AddPhoneNumber` Action yöntemi, SMS iletilerini alabilen bir telefon numarası girmek için bir iletişim kutusu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ad230-165">The `AddPhoneNumber` action method displays a dialog box to enter a phone number that can receive SMS messages.</span></span>

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample5.cs)]

    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image5.png)
13. <span data-ttu-id="ad230-166">Birkaç saniye içinde doğrulama koduna sahip bir kısa mesaj alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="ad230-166">In a few seconds you will get a text message with the verification code.</span></span> <span data-ttu-id="ad230-167">Girin ve **Gönder**' e basın.</span><span class="sxs-lookup"><span data-stu-id="ad230-167">Enter it and press **Submit**.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image6.png)
14. <span data-ttu-id="ad230-168">Yönet görünümü telefon numaranızı eklendiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="ad230-168">The Manage view shows your phone number was added.</span></span>

<a id="enable2"></a>
## <a name="enable-two-factor-authentication"></a><span data-ttu-id="ad230-169">İki öğeli kimlik doğrulamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="ad230-169">Enable two-factor authentication</span></span>

<span data-ttu-id="ad230-170">Şablon tarafından oluşturulan uygulamada, iki öğeli kimlik doğrulamayı (2FA) etkinleştirmek için Kullanıcı arabirimini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad230-170">In the template generated app, you need to use the UI to enable two-factor authentication (2FA).</span></span> <span data-ttu-id="ad230-171">2FA 'yı etkinleştirmek için, gezinti çubuğundaki kullanıcı KIMLIĞINIZ (e-posta diğer adı) seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ad230-171">To enable 2FA, click on your user ID (email alias) in the navigation bar.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image7.png)

<span data-ttu-id="ad230-172">2FA 'yı etkinleştir ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ad230-172">Click on enable 2FA.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image8.png)

<span data-ttu-id="ad230-173">Oturumu kapatın ve yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ad230-173">Logout, then log back in.</span></span> <span data-ttu-id="ad230-174">E-postayı etkinleştirdiyseniz ( [önceki öğreticime](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)bakın),/FA için SMS veya e-postayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad230-174">If you've enabled email (see my [previous tutorial](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)), you can select the SMS or email for 2FA.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image9.png)

<span data-ttu-id="ad230-175">Kodu doğrula sayfası görüntülenir (SMS veya e-posta).</span><span class="sxs-lookup"><span data-stu-id="ad230-175">The Verify Code page is displayed where you can enter the code (from SMS or email).</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image10.png)

<span data-ttu-id="ad230-176">**Bu tarayıcıya** göz atma onay kutusunun tıklanması, kutuyu seçtiğiniz tarayıcı ve cihazı kullanırken oturum açmak için 2FA kullanmaya gerek duymasını da muaf tutacaktır.</span><span class="sxs-lookup"><span data-stu-id="ad230-176">Clicking on the **Remember this browser** check box will exempt you from needing to use 2FA to log in when using the browser and device where you checked the box.</span></span> <span data-ttu-id="ad230-177">Kötü amaçlı kullanıcılar cihazınıza erişim sağlayabilmediği sürece, 2FA 'yı etkinleştirmek ve **Bu tarayıcıyı anımsa** ' ya tıklamak, güvenilir olmayan cihazlardan tüm erişimler için güçlü bir adım parola erişimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ad230-177">As long as malicious users can't gain access to your device, enabling 2FA and clicking on the **Remember this browser** will provide you with convenient one step password access, while still retaining strong 2FA protection for all access from non-trusted devices.</span></span> <span data-ttu-id="ad230-178">Düzenli olarak kullandığınız özel cihaz üzerinde bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad230-178">You can do this on any private device you regularly use.</span></span>

<span data-ttu-id="ad230-179">Bu öğretici, yeni bir ASP.NET MVC uygulamasında 2FA 'yı etkinleştirmeye yönelik hızlı bir giriş sağlar.</span><span class="sxs-lookup"><span data-stu-id="ad230-179">This tutorial provides a quick introduction to enabling 2FA on a new ASP.NET MVC app.</span></span> <span data-ttu-id="ad230-180">[ASP.NET Identity Ile SMS ve e-posta kullanarak öğreticimin iki öğeli kimlik doğrulaması](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) , örneğin arkasındaki kodla ilgili ayrıntılara gider.</span><span class="sxs-lookup"><span data-stu-id="ad230-180">My tutorial [Two-factor authentication using SMS and email with ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) goes into detail on the code behind the sample.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="ad230-181">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ad230-181">Additional Resources</span></span>

- <span data-ttu-id="ad230-182">[ASP.NET Identity Ile SMS ve e-posta kullanarak iki öğeli kimlik doğrulama](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) Iki öğeli kimlik doğrulama ile ilgili ayrıntılara gider</span><span class="sxs-lookup"><span data-stu-id="ad230-182">[Two-factor authentication using SMS and email with ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) Goes into detail on Two-factor authentication</span></span>
- [<span data-ttu-id="ad230-183">Önerilen kaynakların ASP.NET Identity bağlantıları</span><span class="sxs-lookup"><span data-stu-id="ad230-183">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- <span data-ttu-id="ad230-184">[ASP.NET Identity Ile hesap onaylama ve parola kurtarma](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Parola kurtarma ve hesap onaylama hakkında daha fazla ayrıntıya gider.</span><span class="sxs-lookup"><span data-stu-id="ad230-184">[Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Goes into more detail on password recovery and account confirmation.</span></span>
- <span data-ttu-id="ad230-185">[Facebook, Twitter, LinkedIn ve Google OAuth2 oturum açma Ile MVC 5 uygulaması](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) Bu öğreticide, Facebook ve Google OAuth 2 yetkilendirmesi ile ASP.NET MVC 5 uygulamasının nasıl yazılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ad230-185">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) This tutorial shows you how to write an ASP.NET MVC 5 app with Facebook and Google OAuth 2 authorization.</span></span> <span data-ttu-id="ad230-186">Ayrıca, kimlik veritabanına nasıl ek veri ekleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="ad230-186">It also shows how to add additional data to the Identity database.</span></span>
- <span data-ttu-id="ad230-187">[Üyelik, OAuth ve SQL veritabanı Ile Azure Web 'e güvenli bir ASP.NET MVC uygulaması dağıtın](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="ad230-187">[Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure Web](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="ad230-188">Bu öğreticide, Azure dağıtımı, rollerle uygulamanızı güvenli hale getirme, Kullanıcı ve rolleri eklemek için üyelik API 'sini kullanma ve ek güvenlik özellikleri eklenir.</span><span class="sxs-lookup"><span data-stu-id="ad230-188">This tutorial adds Azure deployment, how to secure your app with roles, how to use the membership API to add users and roles, and additional security features.</span></span>
- [<span data-ttu-id="ad230-189">OAuth 2 için Google App oluşturma ve uygulamayı projeye bağlama</span><span class="sxs-lookup"><span data-stu-id="ad230-189">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [<span data-ttu-id="ad230-190">Facebook 'ta uygulama oluşturma ve uygulamayı projeye bağlama</span><span class="sxs-lookup"><span data-stu-id="ad230-190">Creating the app in Facebook and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [<span data-ttu-id="ad230-191">Projede SSL ayarlama</span><span class="sxs-lookup"><span data-stu-id="ad230-191">Setting up SSL in the Project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
- [<span data-ttu-id="ad230-192">C# Ve ASP.NET MVC geliştirme ortamınızı ayarlama</span><span class="sxs-lookup"><span data-stu-id="ad230-192">How to set up your C# and ASP.NET MVC development environment</span></span>](https://www.twilio.com/docs/usage/tutorials/how-to-set-up-your-csharp-and-asp-net-mvc-development-environment)
