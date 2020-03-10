---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: Facebook, Twitter, LinkedIn ve Google OAuth2 oturum açma (C#) ile MVC 5 uygulaması oluşturun | Microsoft Docs
author: Rick-Anderson
description: Bu öğreticide, kullanıcıların bir dış ön kimlik bilgileriyle OAuth 2,0 kullanarak oturum açmasını sağlayan bir ASP.NET MVC 5 Web uygulamasının nasıl oluşturulacağı gösterilmektedir...
ms.author: riande
ms.date: 04/03/2015
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: dd2e55d68ceb5a90134e394c00f3a3a231cb27d6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78566082"
---
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a><span data-ttu-id="8bf71-103">Facebook, Twitter, LinkedIn ve Google OAuth2 Oturum Açma Özellikli Bir ASP.NET MVC 5 Uygulaması Oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="8bf71-103">Create an ASP.NET MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on (C#)</span></span>

<span data-ttu-id="8bf71-104">[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından</span><span class="sxs-lookup"><span data-stu-id="8bf71-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="8bf71-105">Bu öğreticide, kullanıcıların bir dış kimlik doğrulama sağlayıcısından (Facebook, Twitter, LinkedIn, Microsoft veya Google gibi) kimlik bilgileriyle [OAuth 2,0](http://oauth.net/2/) kullanarak oturum açmasını sağlayan BIR ASP.NET MVC 5 Web uygulaması oluşturma yöntemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8bf71-105">This tutorial shows you how to build an ASP.NET MVC 5 web application that enables users to log in using [OAuth 2.0](http://oauth.net/2/) with credentials from an external authentication provider, such as Facebook, Twitter, LinkedIn, Microsoft, or Google.</span></span> <span data-ttu-id="8bf71-106">Kolaylık olması için, bu öğretici Facebook ve Google kimlik bilgileriyle çalışmaya odaklanır.</span><span class="sxs-lookup"><span data-stu-id="8bf71-106">For simplicity, this tutorial focuses on working with credentials from Facebook and Google.</span></span>
> 
> <span data-ttu-id="8bf71-107">Bu kimlik bilgilerini Web sitelerinizde etkinleştirmek, milyonlarca kullanıcının zaten bu dış sağlayıcıları olan hesapları olduğundan önemli bir avantaj sağlar.</span><span class="sxs-lookup"><span data-stu-id="8bf71-107">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="8bf71-108">Bu kullanıcılar yeni bir kimlik bilgileri kümesi oluşturup hatırlamaları zorunda olmadıkları takdirde sitenize kaydolmak için daha fazla işlem yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="8bf71-108">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span>
> 
> <span data-ttu-id="8bf71-109">Ayrıca bkz. [ASP.NET MVC 5 UYGULAMASı SMS ve e-posta Iki öğeli kimlik doğrulaması](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8bf71-109">See also [ASP.NET MVC 5 app with SMS and email Two-Factor Authentication](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span></span>
> 
> <span data-ttu-id="8bf71-110">Öğretici Ayrıca, Kullanıcı için profil verilerinin nasıl ekleneceğini ve rol eklemek için üyelik API 'sinin nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="8bf71-110">The tutorial also shows how to add profile data for the user, and how to use the Membership API to add roles.</span></span> <span data-ttu-id="8bf71-111">Bu öğretici [Rick Anderson](https://blogs.msdn.com/rickAndy) tarafından yazılmıştır (lütfen Twitter 'da şu adımları izleyin: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span><span class="sxs-lookup"><span data-stu-id="8bf71-111">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Please follow me on Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>

<a id="start"></a>
## <a name="getting-started"></a><span data-ttu-id="8bf71-112">Başlarken</span><span class="sxs-lookup"><span data-stu-id="8bf71-112">Getting Started</span></span>

<span data-ttu-id="8bf71-113">Web veya [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) [için Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) yükleyip çalıştırarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-113">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="8bf71-114">Visual Studio [2013 güncelleştirme 3](https://go.microsoft.com/fwlink/?LinkId=390521) veya üstünü yükler.</span><span class="sxs-lookup"><span data-stu-id="8bf71-114">Install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span> <span data-ttu-id="8bf71-115">Dropbox, GitHub, LinkedIn, Instagram, buffer, Salesforce, STEHAR, Stack Exchange, Tripit, Twitch, Twitter, Yahoo! ve daha birçok konuda yardım almak için bu [örnek projeye](https://github.com/matthewdunsdon/oauthforaspnet)bakın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-115">For help with Dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo!, and more, see this [sample project](https://github.com/matthewdunsdon/oauthforaspnet).</span></span>

> [!NOTE]
> <span data-ttu-id="8bf71-116">Google OAuth 2 ' i kullanmak ve SSL uyarıları olmadan yerel olarak hata ayıklamak için Visual Studio [2013 güncelleştirme 3](https://go.microsoft.com/fwlink/?LinkId=390521) veya üstünü yüklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="8bf71-116">You must install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher to use Google OAuth 2 and to debug locally without SSL warnings.</span></span>

<span data-ttu-id="8bf71-117">**Başlangıç** sayfasından **Yeni proje** ' ye tıklayın veya menüyü ve ardından **Dosya**' yı ve ardından **Yeni proje**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="8bf71-117">Click **New Project** from the **Start** page, or you can use the menu and select **File**, and then **New Project**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a><span data-ttu-id="8bf71-118">Ilk uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8bf71-118">Creating Your First Application</span></span>

<span data-ttu-id="8bf71-119">**Yeni proje**' ye tıklayın, ardından sol taraftaki **görsel C#**  ' i **seçin ve sonra** **ASP.NET Web uygulaması**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="8bf71-119">Click **New Project**, then select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="8bf71-120">Projenizi "MvcAuth" olarak adlandırın ve ardından **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-120">Name your project "MvcAuth" and then click **OK**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

<span data-ttu-id="8bf71-121">**Yeni ASP.NET projesi** Iletişim kutusunda **MVC**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-121">In the **New ASP.NET Project** dialog, click **MVC**.</span></span> <span data-ttu-id="8bf71-122">Kimlik doğrulaması **ayrı kullanıcı hesapları**değilse, **kimlik doğrulamasını Değiştir** düğmesine tıklayın ve **bireysel kullanıcı hesapları**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="8bf71-122">If the Authentication is not **Individual User Accounts**, click the **Change Authentication** button and select **Individual User Accounts**.</span></span> <span data-ttu-id="8bf71-123">**Bulutta ana bilgisayar**denetlenerek, uygulamanın Azure 'da barındırmak çok kolay olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8bf71-123">By checking **Host in the cloud**, the app will be very easy to host in Azure.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

<span data-ttu-id="8bf71-124">**Bulutta ana bilgisayar**' ı seçtiyseniz, Yapılandır iletişim kutusunu doldurun.</span><span class="sxs-lookup"><span data-stu-id="8bf71-124">If you selected **Host in the cloud**, complete the configure dialog.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a><span data-ttu-id="8bf71-125">En son OWıN ara yazılım sürümüne güncelleştirmek için NuGet kullanın</span><span class="sxs-lookup"><span data-stu-id="8bf71-125">Use NuGet to update to the latest OWIN middleware</span></span>

<span data-ttu-id="8bf71-126">[Owın ara yazılımını](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)güncelleştirmek için NuGet paket yöneticisini kullanın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-126">Use the NuGet package manager to update the [OWIN middleware](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md).</span></span> <span data-ttu-id="8bf71-127">Soldaki menüden **güncelleştirmeler** ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="8bf71-127">Select **Updates** in the left menu.</span></span> <span data-ttu-id="8bf71-128">**Tümünü Güncelleştir** düğmesine tıklayabilirsiniz veya yalnızca owın paketleri için arama yapabilirsiniz (bir sonraki görüntüde gösterilmektedir):</span><span class="sxs-lookup"><span data-stu-id="8bf71-128">You can click on the **Update All** button or you can search for only OWIN packages (shown in the next image):</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

<span data-ttu-id="8bf71-129">Aşağıdaki görüntüde yalnızca OWıN paketleri gösteriliyor:</span><span class="sxs-lookup"><span data-stu-id="8bf71-129">In the image below, only OWIN packages are shown:</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

<span data-ttu-id="8bf71-130">Paket Yöneticisi konsolundan (PMC), tüm paketleri güncelleştirecek `Update-Package` komutunu girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bf71-130">From the Package Manager Console (PMC), you can enter the `Update-Package` command, which will update all packages.</span></span>

<span data-ttu-id="8bf71-131">Uygulamayı çalıştırmak için **F5** veya **CTRL + F5** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-131">Press **F5** or **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="8bf71-132">Aşağıdaki görüntüde, bağlantı noktası numarası 1234 ' dir.</span><span class="sxs-lookup"><span data-stu-id="8bf71-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="8bf71-133">Uygulamayı çalıştırdığınızda, farklı bir bağlantı noktası numarası görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="8bf71-133">When you run the application, you'll see a different port number.</span></span>

<span data-ttu-id="8bf71-134">Tarayıcı pencerenizin boyutuna bağlı olarak, **giriş**, **hakkında**, **Iletişim kurma**, **kayıt** ve **oturum açma** bağlantılarını görmek için gezinti simgesine tıklamanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="8bf71-134">Depending on the size of your browser window, you might need to click the navigation icon to see the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a><span data-ttu-id="8bf71-135">Projede SSL ayarlama</span><span class="sxs-lookup"><span data-stu-id="8bf71-135">Setting up SSL in the Project</span></span>

<span data-ttu-id="8bf71-136">Google ve Facebook gibi kimlik doğrulama sağlayıcılarına bağlanmak için IIS-Express ' i SSL kullanacak şekilde ayarlamanız gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="8bf71-136">To connect to authentication providers like Google and Facebook, you will need to set up IIS-Express to use SSL.</span></span> <span data-ttu-id="8bf71-137">Oturum açtıktan sonra SSL 'yi kullanmaya devam etmek ve HTTP 'ye geri dönmek önemlidir, oturum açma tanımlama bilgileriniz yalnızca Kullanıcı adınız ve parolanız olarak gizli olur ve SSL kullanmadan, bunu kablolu olarak düz metin halinde gönderiyoruz.</span><span class="sxs-lookup"><span data-stu-id="8bf71-137">It's important to keep using SSL after login and not drop back to HTTP, your login cookie is just as secret as your username and password, and without using SSL you're sending it in clear-text across the wire.</span></span> <span data-ttu-id="8bf71-138">Bunun yanı sıra, MVC işlem hattı çalıştırılmadan önce el sıkışma gerçekleştirme ve kanalı güvenli hale getirme (HTTP 'den daha yavaş olan HTTP 'den yavaş olan), bu nedenle oturum açtıktan sonra HTTP 'ye yeniden yönlendirme geçerli istek veya gelecekteki istekleri çok daha hızlı.</span><span class="sxs-lookup"><span data-stu-id="8bf71-138">Besides, you've already taken the time to perform the handshake and secure the channel (which is the bulk of what makes HTTPS slower than HTTP) before the MVC pipeline is run, so redirecting back to HTTP after you're logged in won't make the current request or future requests much faster.</span></span>

1. <span data-ttu-id="8bf71-139">**Çözüm Gezgini**, **mvcauth** projesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-139">In **Solution Explorer**, click the **MvcAuth** project.</span></span>
2. <span data-ttu-id="8bf71-140">Proje özelliklerini göstermek için F4 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-140">Hit the F4 key to show the project properties.</span></span> <span data-ttu-id="8bf71-141">Alternatif olarak, **Görünüm** menüsünden **Özellikler penceresi**' ni seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bf71-141">Alternatively, from the **View** menu you can select **Properties Window**.</span></span>
3. <span data-ttu-id="8bf71-142">**SSL etkin** ' i true olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8bf71-142">Change **SSL Enabled** to True.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. <span data-ttu-id="8bf71-143">SSL URL 'sini kopyalayın (başka bir SSL projesi oluşturmadığınız müddetçe `https://localhost:44300/` olur).</span><span class="sxs-lookup"><span data-stu-id="8bf71-143">Copy the SSL URL (which will be `https://localhost:44300/` unless you've created other SSL projects).</span></span>
5. <span data-ttu-id="8bf71-144">**Çözüm Gezgini**, **mvcauth** projesine sağ tıklayın ve **Özellikler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="8bf71-144">In **Solution Explorer**, right click the **MvcAuth** project and select **Properties**.</span></span>
6. <span data-ttu-id="8bf71-145">**Web** sekmesini seçin ve ardından SSL URL 'Sini **proje URL** 'si kutusuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-145">Select the **Web** tab, and then paste the SSL URL into the **Project Url** box.</span></span> <span data-ttu-id="8bf71-146">Dosyayı kaydedin (CTL + S).</span><span class="sxs-lookup"><span data-stu-id="8bf71-146">Save the file (Ctl+S).</span></span> <span data-ttu-id="8bf71-147">Facebook ve Google kimlik doğrulama uygulamalarını yapılandırmak için bu URL 'ye ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="8bf71-147">You will need this URL to configure Facebook and Google authentication apps.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. <span data-ttu-id="8bf71-148">Tüm isteklerin HTTPS kullanması gerektiğini gerektirmek için `Home` denetleyiciye [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) özniteliğini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8bf71-148">Add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) attribute to the `Home` controller to require all requests must use HTTPS.</span></span> <span data-ttu-id="8bf71-149">Daha güvenli bir yaklaşım uygulamaya [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filtresini eklemektir.</span><span class="sxs-lookup"><span data-stu-id="8bf71-149">A more secure approach is to add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter to the application.</span></span> <span data-ttu-id="8bf71-150">Uygulamayı SSL ile koruma &quot;bölümüne bakın ve öğreticimde Yetkilendir özniteliği&quot; [kimlik doğrulama ve SQL DB ile bir ASP.NET MVC uygulaması oluşturun ve Azure App Service 'e dağıtın](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="8bf71-150">See the section &quot;Protect the Application with SSL and the Authorize Attribute&quot; in my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="8bf71-151">Ana denetleyicinin bir bölümü aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8bf71-151">A portion of the Home controller is shown below.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. <span data-ttu-id="8bf71-152">Uygulamayı çalıştırmak için CTRL+F5'e basın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-152">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="8bf71-153">Sertifikayı geçmişte yüklediyseniz, bu bölümün geri kalanını atlayabilir ve [OAuth 2 Için Google uygulaması oluşturmaya ve uygulamayı projeye bağlamaya](#goog)geçebilirsiniz, aksi takdirde, IIS Express oluşturduğu otomatik olarak imzalanan sertifikaya güvenmek için yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="8bf71-153">If you've installed the certificate in the past, you can skip the rest of this section and jump to [Creating a Google app for OAuth 2 and connecting the app to the project](#goog), otherwise, follow the instructions to trust the self-signed certificate that IIS Express has generated.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. <span data-ttu-id="8bf71-154">**Güvenlik uyarısı** iletişim kutusunu okuyun ve ardından localhost 'u temsil eden sertifikayı yüklemek istiyorsanız **Evet** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-154">Read the **Security Warning** dialog and then click **Yes** if you want to install the certificate representing localhost.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. <span data-ttu-id="8bf71-155">IE *giriş* sayfasını gösterır ve SSL uyarısı yoktur.</span><span class="sxs-lookup"><span data-stu-id="8bf71-155">IE shows the *Home* page and there are no SSL warnings.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. <span data-ttu-id="8bf71-156">Google Chrome sertifikayı da kabul eder ve HTTPS içeriğini uyarı olmadan gösterir.</span><span class="sxs-lookup"><span data-stu-id="8bf71-156">Google Chrome also accepts the certificate and will show HTTPS content without a warning.</span></span> <span data-ttu-id="8bf71-157">Firefox kendi sertifika deposunu kullanır, bu nedenle bir uyarı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="8bf71-157">Firefox uses its own certificate store, so it will display a warning.</span></span> <span data-ttu-id="8bf71-158">Uygulamamız için **riskleri anladım**' ı güvenle deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bf71-158">For our application you can safely click **I Understand the Risks**.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a><span data-ttu-id="8bf71-159">OAuth 2 için Google App oluşturma ve uygulamayı projeye bağlama</span><span class="sxs-lookup"><span data-stu-id="8bf71-159">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="8bf71-160">Geçerli Google OAuth yönergeleri için bkz. [ASP.NET Core Google kimlik doğrulamasını yapılandırma](/aspnet/core/security/authentication/social/google-logins).</span><span class="sxs-lookup"><span data-stu-id="8bf71-160">For current Google OAuth instructions, see [Configuring Google authentication in ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).</span></span>

1. <span data-ttu-id="8bf71-161">[Google geliştiricileri konsoluna](https://console.developers.google.com/)gidin.</span><span class="sxs-lookup"><span data-stu-id="8bf71-161">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span>
2. <span data-ttu-id="8bf71-162">Daha önce bir proje oluşturmadıysanız, sol sekmede **kimlik bilgileri** ' ni seçin ve ardından **Oluştur**' u seçin.</span><span class="sxs-lookup"><span data-stu-id="8bf71-162">If you haven't created a project before, select **Credentials** in the left tab, and then select **Create**.</span></span>
3. <span data-ttu-id="8bf71-163">Sol sekmede **kimlik bilgileri**' ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-163">In the left tab, click **Credentials**.</span></span>
4. <span data-ttu-id="8bf71-164">**Kimlik bilgileri oluştur** ' a tıklayın, **OAuth istemci kimliği**.</span><span class="sxs-lookup"><span data-stu-id="8bf71-164">Click **Create credentials** then **OAuth client ID**.</span></span> 

    1. <span data-ttu-id="8bf71-165">**ISTEMCI kimliği oluştur** iletişim kutusunda, uygulama türü Için varsayılan **Web uygulamasını** saklayın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-165">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
    2. <span data-ttu-id="8bf71-166">**Yetkili JavaScript** kaynakları ' nı yukarıda KULLANDıĞıNıZ SSL URL 'sine ayarlayın (başka bir SSL projesi oluşturmadığınız müddetçe`https://localhost:44300/`)</span><span class="sxs-lookup"><span data-stu-id="8bf71-166">Set the **Authorized JavaScript** origins to the SSL URL you used above (`https://localhost:44300/` unless you've created other SSL projects)</span></span>
    3. <span data-ttu-id="8bf71-167">**Yetkilendirilmiş yeniden YÖNLENDIRME URI** 'sini şu şekilde ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="8bf71-167">Set the **Authorized redirect URI** to:</span></span>  
         `https://localhost:44300/signin-google`
5. <span data-ttu-id="8bf71-168">OAuth onay ekranı menü öğesine tıklayın, ardından e-posta adresinizi ve ürün adınızı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-168">Click the OAuth Consent screen menu item, then set your email address and product name.</span></span> <span data-ttu-id="8bf71-169">Formu tamamladığınızda **Kaydet**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-169">When you have completed the form click **Save**.</span></span>
6. <span data-ttu-id="8bf71-170">Kitaplık menü öğesine tıklayın, **Google + API**ara ' ya tıklayın, ardından Etkinleştir ' e basın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-170">Click the Library menu item, search **Google+ API**, click on it then press Enable.</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   <span data-ttu-id="8bf71-171">Aşağıdaki görüntüde etkin API 'Ler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8bf71-171">The image below shows the enabled APIs.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. <span data-ttu-id="8bf71-172">Google API 'Leri API Manager 'dan, **ISTEMCI kimliğini**edinmek Için **kimlik bilgileri** sekmesini ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="8bf71-172">From the Google APIs API Manager, visit the **Credentials** tab to obtain the **Client ID**.</span></span> <span data-ttu-id="8bf71-173">Bir JSON dosyasını uygulama gizli dizileri ile kaydetmek için indirin.</span><span class="sxs-lookup"><span data-stu-id="8bf71-173">Download to save a JSON file with application secrets.</span></span> <span data-ttu-id="8bf71-174">**ClientID** ve **clientsecret** dosyalarını kopyalayıp *App_Start* klasöründeki *Startup.auth.cs* dosyasında bulunan `UseGoogleAuthentication` yöntemine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-174">Copy and paste the **ClientId** and **ClientSecret** into the `UseGoogleAuthentication` method found in the *Startup.Auth.cs* file in the *App_Start* folder.</span></span> <span data-ttu-id="8bf71-175">Aşağıda gösterilen **ClientID** ve **ClientSecret** değerleri, örnekler ve çalışmalardır.</span><span class="sxs-lookup"><span data-stu-id="8bf71-175">The **ClientId** and **ClientSecret** values shown below are samples and don't work.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > <span data-ttu-id="8bf71-176">Güvenlik-önemli verileri hiçbir şekilde kaynak kodunuzda depolamayin.</span><span class="sxs-lookup"><span data-stu-id="8bf71-176">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="8bf71-177">Hesap ve kimlik bilgileri, örneği basit tutmak için yukarıdaki koda eklenir.</span><span class="sxs-lookup"><span data-stu-id="8bf71-177">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="8bf71-178">[ASP.net ve Azure App Service için parola ve diğer hassas verileri dağıtmaya yönelik en iyi uygulamalar](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-178">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
8. <span data-ttu-id="8bf71-179">Uygulamayı derlemek ve çalıştırmak için **CTRL + F5** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-179">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="8bf71-180">**Oturum aç** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-180">Click the **Log in** link.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. <span data-ttu-id="8bf71-181">**Oturum açmak için başka bir hizmet kullan**' ın altında **Google**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-181">Under **Use another service to log in**, click **Google**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > <span data-ttu-id="8bf71-182">Yukarıdaki adımlardan herhangi birini kaçırırsanız, bir HTTP 401 hatası alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="8bf71-182">If you miss any of the steps above you will get a HTTP 401 error.</span></span> <span data-ttu-id="8bf71-183">Yukarıdaki adımları yeniden denetleyin.</span><span class="sxs-lookup"><span data-stu-id="8bf71-183">Recheck your steps above.</span></span> <span data-ttu-id="8bf71-184">Gerekli bir ayarı (örneğin, **ürün adı**) kaçırırsanız, eksik öğeyi ekleyin ve kaydedin; kimlik doğrulamasının çalışması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="8bf71-184">If you miss a required setting (for example **product name**), add the missing item and save; it can take a few minutes for authentication to work.</span></span>
10. <span data-ttu-id="8bf71-185">Kimlik bilgilerinizi gireceğiniz Google sitesine yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bf71-185">You will be redirected to the Google site where you will enter your credentials.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. <span data-ttu-id="8bf71-186">Kimlik bilgilerinizi girdikten sonra, yeni oluşturduğunuz Web uygulamasına izin vermeniz istenir:</span><span class="sxs-lookup"><span data-stu-id="8bf71-186">After you enter your credentials, you will be prompted to give permissions to the web application you just created:</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. <span data-ttu-id="8bf71-187">**Kabul et**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-187">Click **Accept**.</span></span> <span data-ttu-id="8bf71-188">Şimdi, Google hesabınızı kaydedebileceğiniz MvcAuth uygulamasının **kayıt** sayfasına yeniden yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bf71-188">You will now be redirected back to the **Register** page of the MvcAuth application where you can register your Google account.</span></span> <span data-ttu-id="8bf71-189">Gmail hesabınız için kullanılan yerel e-posta kayıt adını değiştirme seçeneğiniz vardır, ancak genellikle varsayılan e-posta diğer adını (yani, kimlik doğrulaması için kullandığınız hesap) korumak istersiniz.</span><span class="sxs-lookup"><span data-stu-id="8bf71-189">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="8bf71-190">**Kaydol**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-190">Click **Register**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a><span data-ttu-id="8bf71-191">Facebook 'ta uygulama oluşturma ve uygulamayı projeye bağlama</span><span class="sxs-lookup"><span data-stu-id="8bf71-191">Creating the app in Facebook and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="8bf71-192">Güncel Facebook OAuth2 kimlik doğrulama yönergeleri için bkz. [Facebook kimlik doğrulamasını yapılandırma](/aspnet/core/security/authentication/social/facebook-logins)</span><span class="sxs-lookup"><span data-stu-id="8bf71-192">For current Facebook OAuth2 authentication instructions, see [Configuring Facebook authentication](/aspnet/core/security/authentication/social/facebook-logins)</span></span>

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a><span data-ttu-id="8bf71-193">Üyelik verilerini İnceleme</span><span class="sxs-lookup"><span data-stu-id="8bf71-193">Examine the Membership Data</span></span>

<span data-ttu-id="8bf71-194">**Görünüm** menüsünde **Sunucu Gezgini**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-194">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

<span data-ttu-id="8bf71-195">**DefaultConnection (MvcAuth)** öğesini genişletin, **Tablolar**' ı genişletin, **Aspnetusers** öğesine sağ tıklayıp **tablo verilerini göster**' e tıklayın</span><span class="sxs-lookup"><span data-stu-id="8bf71-195">Expand **DefaultConnection (MvcAuth)**, expand **Tables**, right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetusers tablosu verileri](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a><span data-ttu-id="8bf71-197">Kullanıcı sınıfına profil verileri ekleme</span><span class="sxs-lookup"><span data-stu-id="8bf71-197">Adding Profile Data to the User Class</span></span>

<span data-ttu-id="8bf71-198">Bu bölümde, aşağıdaki görüntüde gösterildiği gibi, kayıt sırasında kullanıcı verilerine Doğum tarihi ve giriş şehir ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="8bf71-198">In this section you'll add birth date and home town to the user data during registration, as shown in the following image.</span></span>

![ev Town ve bday ile Reg](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

<span data-ttu-id="8bf71-200">*Models\ıdentitymodels.cs* dosyasını açın ve Doğum tarihi ve ev Town özellikleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="8bf71-200">Open the *Models\IdentityModels.cs* file and add birth date and home town properties:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

<span data-ttu-id="8bf71-201">*Models\accountviewmodels.cs* dosyasını açın ve `ExternalLoginConfirmationViewModel`Doğum tarihi ve giriş kasayı özelliklerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-201">Open the *Models\AccountViewModels.cs* file and the set birth date and home town properties in `ExternalLoginConfirmationViewModel`.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

<span data-ttu-id="8bf71-202">*Controllers\accountcontroller.cs* dosyasını açın ve şu şekilde gösterildiği gibi `ExternalLoginConfirmation` Action yöntemine Doğum tarihi ve ev Town kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="8bf71-202">Open the *Controllers\AccountController.cs* file and add code for birth date and home town in the `ExternalLoginConfirmation` action method as shown:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

<span data-ttu-id="8bf71-203">*Views\Account\ExternalLoginConfirmation.cshtml* dosyasına Doğum tarihi ve ev Town ekleyin:</span><span class="sxs-lookup"><span data-stu-id="8bf71-203">Add birth date and home town to the *Views\Account\ExternalLoginConfirmation.cshtml* file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

<span data-ttu-id="8bf71-204">Üyelik veritabanını silin, böylece Facebook hesabınızı uygulamanız ile kaydedebilir ve yeni Doğum tarihi ile ev kasaprofili bilgilerini ekleyebildiğinizi doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bf71-204">Delete the membership database so you can again register your Facebook account with your application and verify you can add the new birth date and home town profile information.</span></span>

<span data-ttu-id="8bf71-205">**Çözüm Gezgini**, **tüm dosyaları göster** simgesine tıklayın ve ardından *Ekle\_Data\aspnet-MvcAuth-&lt;dateStamp&gt;. mdf* öğesine sağ tıklayın ve **Sil**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-205">From **Solution Explorer**, click the **Show All Files** icon, then right click *Add\_Data\aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* and click **Delete**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

<span data-ttu-id="8bf71-206">**Araçlar** menüsünde **NuGet Paket Yöneticisi**' ne ve ardından **Paket Yöneticisi konsolu** (PMC) seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-206">From the **Tools** menu, click **NuGet Package Manger**, then click **Package Manager Console** (PMC).</span></span> <span data-ttu-id="8bf71-207">PMC 'de aşağıdaki komutları girin.</span><span class="sxs-lookup"><span data-stu-id="8bf71-207">Enter the following commands in the PMC.</span></span>

1. <span data-ttu-id="8bf71-208">Geçişi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="8bf71-208">Enable-Migrations</span></span>
2. <span data-ttu-id="8bf71-209">Geçiş geçişi Init</span><span class="sxs-lookup"><span data-stu-id="8bf71-209">Add-Migration Init</span></span>
3. <span data-ttu-id="8bf71-210">Güncelleştirme-veritabanı</span><span class="sxs-lookup"><span data-stu-id="8bf71-210">Update-Database</span></span>

<span data-ttu-id="8bf71-211">Uygulamayı çalıştırın ve FaceBook ve Google kullanarak oturum açın ve bazı kullanıcıları kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8bf71-211">Run the application and use FaceBook and Google to log in and register some users.</span></span>

## <a name="examine-the-membership-data"></a><span data-ttu-id="8bf71-212">Üyelik verilerini İnceleme</span><span class="sxs-lookup"><span data-stu-id="8bf71-212">Examine the Membership Data</span></span>

<span data-ttu-id="8bf71-213">**Görünüm** menüsünde **Sunucu Gezgini**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-213">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

<span data-ttu-id="8bf71-214">**Aspnetusers** öğesine sağ tıklayın ve **tablo verilerini göster**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-214">Right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

<span data-ttu-id="8bf71-215">`HomeTown` ve `BirthDate` alanları aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8bf71-215">The `HomeTown` and `BirthDate` fields are shown below.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a><span data-ttu-id="8bf71-216">Uygulamanızı günlüğe kaydetme ve başka bir hesapla oturum açma</span><span class="sxs-lookup"><span data-stu-id="8bf71-216">Logging off your App and Logging in With Another Account</span></span>

<span data-ttu-id="8bf71-217">Uygulamanızda Facebook ile oturum açın ve ardından farklı bir Facebook hesabıyla (aynı tarayıcıyı kullanarak) yeniden oturum açmayı denerseniz, kullandığınız önceki Facebook hesabında hemen oturum açarsınız.</span><span class="sxs-lookup"><span data-stu-id="8bf71-217">If you log on to your app with Facebook,, and then log out and try to log in again with a different Facebook account (using the same browser), you will be immediately logged in to the previous Facebook account you used.</span></span> <span data-ttu-id="8bf71-218">Başka bir hesap kullanmak için Facebook 'a gitmeniz ve Facebook 'ta oturumunuzu açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bf71-218">In order to use another account, you need to navigate to Facebook and log out at Facebook.</span></span> <span data-ttu-id="8bf71-219">Aynı kural diğer 3. taraf kimlik doğrulama sağlayıcıları için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="8bf71-219">The same rule applies to any other 3rd party authentication provider.</span></span> <span data-ttu-id="8bf71-220">Alternatif olarak, farklı bir tarayıcı kullanarak başka bir hesapla oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bf71-220">Alternatively, you can log in with another account by using a different browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bf71-221">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="8bf71-221">Next Steps</span></span>

<span data-ttu-id="8bf71-222">Yahoo ve LinkedIn yönergeleri için Jerrie Pelser tarafından [OWıN Için Yahoo ve LinkedIn OAuth güvenlik sağlayıcılarının tanıtımı](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="8bf71-222">See [Introducing the Yahoo and LinkedIn OAuth security providers for OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) by Jerrie Pelser for Yahoo and LinkedIn instructions.</span></span> <span data-ttu-id="8bf71-223">Sosyal oturum açma düğmelerini etkinleştirmek için bkz. ASP.NET MVC 5 için Jerrie 'nin oldukça sosyal oturum açma düğmeleri.</span><span class="sxs-lookup"><span data-stu-id="8bf71-223">See Jerrie's Pretty social login buttons for ASP.NET MVC 5 to get enable social login buttons.</span></span>

<span data-ttu-id="8bf71-224">Öğreticimi izleyin, [kimlik doğrulama ve SQL DB ile ASP.NET MVC uygulaması oluşturun ve](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)bu öğreticiyi devam eden Azure App Service için dağıtın ve şunları gösterir:</span><span class="sxs-lookup"><span data-stu-id="8bf71-224">Follow my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), which continues this tutorial and shows the following:</span></span>

1. <span data-ttu-id="8bf71-225">Uygulamanızı Azure 'a dağıtma.</span><span class="sxs-lookup"><span data-stu-id="8bf71-225">How to deploy your app to Azure.</span></span>
2. <span data-ttu-id="8bf71-226">Uygulamanızı rollerle güvenli hale getirme.</span><span class="sxs-lookup"><span data-stu-id="8bf71-226">How to secure you app with roles.</span></span>
3. <span data-ttu-id="8bf71-227">[RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) ve [Yetkilendirme](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filtreleriyle uygulamanızın güvenliğini sağlama.</span><span class="sxs-lookup"><span data-stu-id="8bf71-227">How to secure your app with the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) and [Authorize](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filters.</span></span>
4. <span data-ttu-id="8bf71-228">Kullanıcı ve rolleri eklemek için üyelik API 'sini kullanma.</span><span class="sxs-lookup"><span data-stu-id="8bf71-228">How to use the membership API to add users and roles.</span></span>

<span data-ttu-id="8bf71-229">Lütfen bu öğreticiyi beğentireceğiniz ve neleri iyileştireceğiz hakkında geri bildirimde bulunun.</span><span class="sxs-lookup"><span data-stu-id="8bf71-229">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="8bf71-230">Ayrıca, [kodu nasıl kullanacağınızı göster hakkında](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)yeni konular da isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bf71-230">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span> <span data-ttu-id="8bf71-231">Hatta, ASP.NET 'e eklenecek yeni özellikler isteyebilir ve oylayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bf71-231">You can even ask for and vote on new features to be added to ASP.NET.</span></span> <span data-ttu-id="8bf71-232">Örneğin, [Kullanıcı ve rolleri oluşturup yönetmek](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use) için bir araç için oy verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bf71-232">For example, you can vote for a tool to [create and manage users and roles.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span></span>

<span data-ttu-id="8bf71-233">ASP.NET dış kimlik doğrulama hizmetlerinin nasıl çalıştığı hakkında iyi bir açıklama için bkz. Robert McMurray 'ın [dış kimlik doğrulama hizmetleri](https://asp.net/web-api/overview/security/external-authentication-services).</span><span class="sxs-lookup"><span data-stu-id="8bf71-233">For an good explanation of how ASP.NET External Authentication Services work, see Robert McMurray's [External Authentication Services](https://asp.net/web-api/overview/security/external-authentication-services).</span></span> <span data-ttu-id="8bf71-234">Robert 's makalesi, Microsoft ve Twitter kimlik doğrulamasını etkinleştirme konusunda da ayrıntıya gider.</span><span class="sxs-lookup"><span data-stu-id="8bf71-234">Robert's article also goes into detail in enabling Microsoft and Twitter authentication.</span></span> <span data-ttu-id="8bf71-235">Tom Dykstra 'ın mükemmel [EF/MVC öğreticisi](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) Entity Framework nasıl çalışalınacağını göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="8bf71-235">Tom Dykstra's excellent [EF/MVC tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) shows how to work with the Entity Framework.</span></span>
