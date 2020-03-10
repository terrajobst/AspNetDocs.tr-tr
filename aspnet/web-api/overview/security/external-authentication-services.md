---
uid: web-api/overview/security/external-authentication-services
title: ASP.NET Web API 'SI (C#) Ile dış kimlik doğrulama hizmetleri Microsoft Docs
author: rmcmurray
description: ASP.NET Web API 'sinde dış kimlik doğrulama hizmetlerinin kullanımını açıklar.
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 3bb8eb15-b518-44f5-a67d-a27e051aedc6
msc.legacyurl: /web-api/overview/security/external-authentication-services
msc.type: authoredcontent
ms.openlocfilehash: b2571552a3f8040ff42bfa0a9fa48981f71a1e4b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555477"
---
# <a name="external-authentication-services-with-aspnet-web-api-c"></a><span data-ttu-id="bb7ca-103">ASP.NET Web API 'SI (C#) Ile dış kimlik doğrulama hizmetleri</span><span class="sxs-lookup"><span data-stu-id="bb7ca-103">External Authentication Services with ASP.NET Web API (C#)</span></span>

<span data-ttu-id="bb7ca-104">Visual Studio 2017 ve ASP.NET 4.7.2, birden çok OAuth/OpenID ve sosyal medya kimlik doğrulama hizmeti içeren dış kimlik doğrulama hizmetleriyle tümleştirilecek [tek sayfalı uygulamalar](../../../single-page-application/index.md) (Spa) ve [Web API](../../index.md) hizmetlerinin güvenlik seçeneklerini genişletin: Microsoft hesapları, Twitter, Facebook ve Google.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-104">Visual Studio 2017 and ASP.NET 4.7.2 expand the security options for [Single Page Applications](../../../single-page-application/index.md) (SPA) and [Web API](../../index.md) services to integrate with external authentication services, which include several OAuth/OpenID and social media authentication services: Microsoft Accounts, Twitter, Facebook, and Google.</span></span>  

### <a name="in-this-walkthrough"></a><span data-ttu-id="bb7ca-105">Bu Izlenecek yolda</span><span class="sxs-lookup"><span data-stu-id="bb7ca-105">In this Walkthrough</span></span>

- [<span data-ttu-id="bb7ca-106">Dış kimlik doğrulama hizmetlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="bb7ca-106">Using External Authentication Services</span></span>](#USING)
- [<span data-ttu-id="bb7ca-107">Örnek Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="bb7ca-107">Creating the Sample Web Application</span></span>](#SAMPLE)
- [<span data-ttu-id="bb7ca-108">Facebook kimlik doğrulamasını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="bb7ca-108">Enabling Facebook Authentication</span></span>](#FACEBOOK)
- [<span data-ttu-id="bb7ca-109">Google kimlik doğrulamasını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="bb7ca-109">Enabling Google Authentication</span></span>](#GOOGLE)
- [<span data-ttu-id="bb7ca-110">Microsoft kimlik doğrulamasını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="bb7ca-110">Enabling Microsoft Authentication</span></span>](#MICROSOFT)
- [<span data-ttu-id="bb7ca-111">Twitter kimlik doğrulamasını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="bb7ca-111">Enabling Twitter Authentication</span></span>](#TWITTER)
- [<span data-ttu-id="bb7ca-112">Ek Bilgiler</span><span class="sxs-lookup"><span data-stu-id="bb7ca-112">Additional Information</span></span>](#MOREINFO)

    - [<span data-ttu-id="bb7ca-113">Dış kimlik doğrulama hizmetlerini birleştirme</span><span class="sxs-lookup"><span data-stu-id="bb7ca-113">Combining External Authentication Services</span></span>](#COMBINE)
    - [<span data-ttu-id="bb7ca-114">Tam etki alanı adını kullanmak için IIS Express yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bb7ca-114">Configuring IIS Express to use a Fully Qualified Domain Name</span></span>](#FQDN)
    - [<span data-ttu-id="bb7ca-115">Microsoft kimlik doğrulaması için uygulama ayarlarınızı edinme</span><span class="sxs-lookup"><span data-stu-id="bb7ca-115">How to Obtain your Application Settings for Microsoft Authentication</span></span>](#OBTAIN)
    - [<span data-ttu-id="bb7ca-116">İsteğe bağlı: yerel kaydı devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="bb7ca-116">Optional: Disable Local Registration</span></span>](#DISABLE)

### <a name="prerequisites"></a><span data-ttu-id="bb7ca-117">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="bb7ca-117">Prerequisites</span></span>

<span data-ttu-id="bb7ca-118">Bu yönergedeki örnekleri izlemek için aşağıdakilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-118">To follow the examples in this walkthrough, you need to have the following:</span></span>

- <span data-ttu-id="bb7ca-119">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="bb7ca-119">Visual Studio 2017</span></span>
- <span data-ttu-id="bb7ca-120">Aşağıdaki sosyal medya kimlik doğrulama hizmetlerinden biri için uygulama tanımlayıcısı ve gizli anahtarı olan bir geliştirici hesabı:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-120">A developer account with the application identifier and secret key for one of the following social media authentication services:</span></span>

  - <span data-ttu-id="bb7ca-121">Microsoft hesapları ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))</span><span class="sxs-lookup"><span data-stu-id="bb7ca-121">Microsoft Accounts ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))</span></span>
  - <span data-ttu-id="bb7ca-122">Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))</span><span class="sxs-lookup"><span data-stu-id="bb7ca-122">Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))</span></span>
  - <span data-ttu-id="bb7ca-123">Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))</span><span class="sxs-lookup"><span data-stu-id="bb7ca-123">Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))</span></span>
  - <span data-ttu-id="bb7ca-124">Google ([https://developers.google.com/](https://developers.google.com))</span><span class="sxs-lookup"><span data-stu-id="bb7ca-124">Google ([https://developers.google.com/](https://developers.google.com))</span></span>

<a id="USING"></a>
## <a name="using-external-authentication-services"></a><span data-ttu-id="bb7ca-125">Dış kimlik doğrulama hizmetlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="bb7ca-125">Using External Authentication Services</span></span>

<span data-ttu-id="bb7ca-126">Web geliştiricileri için şu anda kullanılabilir olan dış kimlik doğrulama hizmetlerinin her biri, yeni Web uygulamaları oluştururken geliştirme süresini azaltmaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-126">The abundance of external authentication services that are currently available to web developers help to reduce development time when creating new web applications.</span></span> <span data-ttu-id="bb7ca-127">Web kullanıcıları genellikle popüler Web Hizmetleri ve sosyal medya web siteleri için birkaç mevcut hesaba sahiptir, bu nedenle bir Web uygulaması kimlik doğrulama hizmetlerini bir dış Web hizmetinden veya sosyal medya web sitesinden uygularsa, , bir kimlik doğrulama uygulamasının oluşturulması için harcanacak.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-127">Web users typically have several existing accounts for popular web services and social media websites, therefore when a web application implements the authentication services from an external web service or social media website, it saves the development time that would have been spent creating an authentication implementation.</span></span> <span data-ttu-id="bb7ca-128">Bir dış kimlik doğrulama hizmeti kullanmak, son kullanıcıların Web uygulamanız için başka bir hesap oluşturmak zorunda kalmadan ve ayrıca başka bir Kullanıcı adı ve parola hatırlamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-128">Using an external authentication service saves end users from having to create another account for your web application, and also from having to remember another username and password.</span></span>

<span data-ttu-id="bb7ca-129">Geçmişte, geliştiricilerin iki seçeneği vardı: kendi kimlik doğrulama uygulamasını oluşturun veya bir dış kimlik doğrulama hizmetini uygulamalarıyla tümleştirmeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-129">In the past, developers have had two choices: create their own authentication implementation, or learn how to integrate an external authentication service into their applications.</span></span> <span data-ttu-id="bb7ca-130">En temel düzeyde aşağıdaki diyagramda, bir Kullanıcı Aracısı (Web tarayıcısı) için bir dış kimlik doğrulama hizmeti kullanmak üzere yapılandırılmış bir Web uygulamasından bilgi isteyen basit bir istek akışı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-130">At the most basic level, the following diagram illustrates a simple request flow for a user agent (web browser) that is requesting information from a web application that is configured to use an external authentication service:</span></span>

[![](external-authentication-services/_static/image2.png "Click to Expand the Image")](external-authentication-services/_static/image1.png)

<span data-ttu-id="bb7ca-131">Önceki diyagramda, Kullanıcı Aracısı (veya bu örnekteki Web tarayıcısı), Web tarayıcısını bir dış kimlik doğrulama hizmetine yönlendiren bir Web uygulamasına istek yapar.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-131">In the preceding diagram, the user agent (or web browser in this example) makes a request to a web application, which redirects the web browser to an external authentication service.</span></span> <span data-ttu-id="bb7ca-132">Kullanıcı Aracısı kimlik bilgilerini dış kimlik doğrulama hizmetine gönderir ve Kullanıcı aracısının kimliği başarıyla doğrulandıktan sonra, dış kimlik doğrulama hizmeti, Kullanıcı aracısını bir belirteç formuyla, Kullanıcı Aracısı Web uygulamasına gönderilir.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-132">The user agent sends its credentials to the external authentication service, and if the user agent has successfully authenticated, the external authentication service will redirect the user agent to the original web application with some form of token which the user agent will send to the web application.</span></span> <span data-ttu-id="bb7ca-133">Web uygulaması, Kullanıcı aracısının dış kimlik doğrulama hizmeti tarafından başarıyla doğrulandığını doğrulamak için belirtecini kullanır ve Web uygulaması, Kullanıcı Aracısı hakkında daha fazla bilgi toplamak için belirteci kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-133">The web application will use the token to verify that the user agent has been successfully authenticated by the external authentication service, and the web application may use the token to gather more information about the user agent.</span></span> <span data-ttu-id="bb7ca-134">Uygulama, Kullanıcı aracısının bilgilerini işlemeyi tamamladıktan sonra, Web uygulaması, yetkilendirme ayarlarına bağlı olarak kullanıcı aracısına uygun yanıtı döndürür.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-134">Once the application is done processing the user agent's information, the web application will return the appropriate response to the user agent based on its authorization settings.</span></span>

<span data-ttu-id="bb7ca-135">Bu ikinci örnekte, Kullanıcı Aracısı Web uygulaması ve dış yetkilendirme sunucusu ile anlaşır ve Web uygulaması, Kullanıcı hakkında ek bilgi almak için dış yetkilendirme sunucusuyla ek iletişim gerçekleştirir Aracısı</span><span class="sxs-lookup"><span data-stu-id="bb7ca-135">In this second example, the user agent negotiates with the web application and external authorization server, and the web application performs additional communication with the external authorization server to retrieve additional information about the user agent:</span></span>

[![](external-authentication-services/_static/image4.png "Click to Expand the Image")](external-authentication-services/_static/image3.png)

<span data-ttu-id="bb7ca-136">Visual Studio 2017 ve ASP.NET 4.7.2, aşağıdaki kimlik doğrulama hizmetleri için yerleşik tümleştirme sağlayarak, dış kimlik doğrulama hizmetleriyle tümleştirmeyi daha kolay hale getirir:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-136">Visual Studio 2017 and ASP.NET 4.7.2 make integration with external authentication services easier for developers by providing built-in integration for the following authentication services:</span></span>

- <span data-ttu-id="bb7ca-137">Facebook</span><span class="sxs-lookup"><span data-stu-id="bb7ca-137">Facebook</span></span>
- <span data-ttu-id="bb7ca-138">Google</span><span class="sxs-lookup"><span data-stu-id="bb7ca-138">Google</span></span>
- <span data-ttu-id="bb7ca-139">Microsoft hesapları (Windows Live ID hesapları)</span><span class="sxs-lookup"><span data-stu-id="bb7ca-139">Microsoft Accounts (Windows Live ID accounts)</span></span>
- <span data-ttu-id="bb7ca-140">Twitter</span><span class="sxs-lookup"><span data-stu-id="bb7ca-140">Twitter</span></span>

<span data-ttu-id="bb7ca-141">Bu yönergedeki örneklerde, Visual Studio 2017 ile birlikte gelen yeni ASP.NET Web uygulaması şablonunu kullanarak desteklenen dış kimlik doğrulama hizmetlerinin her birinin nasıl yapılandırılacağı gösterilir.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-141">The examples in this walkthrough will demonstrate how to configure each of the supported external authentication services by using the new ASP.NET Web Application template that ships with Visual Studio 2017.</span></span>

> [!NOTE]
> <span data-ttu-id="bb7ca-142">Gerekirse, FQDN 'nizi dış kimlik doğrulama hizmetinizin ayarlarına eklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-142">If necessary, you may need to add your FQDN to the settings for your external authentication service.</span></span> <span data-ttu-id="bb7ca-143">Bu gereksinim, uygulama ayarlarınızda FQDN 'nin istemcileriniz tarafından kullanılan FQDN ile eşleşmesini gerektiren bazı dış kimlik doğrulama hizmetleri için güvenlik kısıtlamalarını temel alır.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-143">This requirement is based on security constraints for some external authentication services which require the FQDN in your application settings to match the FQDN that is used by your clients.</span></span> <span data-ttu-id="bb7ca-144">(Bunun adımları her dış kimlik doğrulama hizmeti için büyük ölçüde farklılık gösterir; bu gerekli olup olmadığını ve bu ayarların nasıl yapılandırılacağını öğrenmek için her bir dış kimlik doğrulama hizmetine yönelik belgelere başvurmanız gerekir.) Bu ortamın test edilmesi için bir FQDN kullanmak üzere IIS Express yapılandırmanız gerekiyorsa, bu kılavuzda daha sonra [tam etki alanı adı kullanmak için IIS Express yapılandırma](#FQDN) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-144">(The steps for this will vary greatly for each external authentication service; you will need to consult the documentation for each external authentication service to see if this is required and how to configure these settings.) If you need to configure IIS Express to use an FQDN for testing this environment, see the [Configuring IIS Express to use a Fully Qualified Domain Name](#FQDN) section later in this walkthrough.</span></span>

<a id="SAMPLE"></a>
## <a name="create-a-sample-web-application"></a><span data-ttu-id="bb7ca-145">Örnek Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="bb7ca-145">Create a Sample Web Application</span></span>

<span data-ttu-id="bb7ca-146">Aşağıdaki adımlar, ASP.NET Web uygulaması şablonunu kullanarak örnek bir uygulama oluşturma konusunda size yol açacağından, bu kılavuzda daha sonra bu örnek uygulamayı dış kimlik doğrulama hizmetlerinin her biri için kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-146">The following steps will lead you through creating a sample application by using the ASP.NET Web Application template, and you will use this sample application for each of the external authentication services later in this walkthrough.</span></span>

<span data-ttu-id="bb7ca-147">Visual Studio 2017 ' u başlatın ve başlangıç sayfasından **Yeni proje** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-147">Start Visual Studio 2017 and select **New Project** from the Start page.</span></span> <span data-ttu-id="bb7ca-148">Ya da **Dosya** menüsünde **Yeni** ' yi ve ardından **Proje**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-148">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<!-- [![](external-authentication-services/_static/image6.png "Click to Expand the Image")](external-authentication-services/_static/image5.png) -->

<span data-ttu-id="bb7ca-149">**Yeni proje** iletişim kutusu görüntülendiğinde, **yüklü** ' ı seçin ve **görsel C#** ' i genişletin.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-149">When the **New Project** dialog box is displayed, select **Installed** and expand **Visual C#**.</span></span> <span data-ttu-id="bb7ca-150">**Görsel C#** bölümünde **Web**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-150">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="bb7ca-151">Proje şablonları listesinde **ASP.NET Web uygulaması (.NET Framework)** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-151">In the list of project templates, select **ASP.NET Web Application (.Net Framework)**.</span></span> <span data-ttu-id="bb7ca-152">Projeniz için bir ad girin ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-152">Enter a name for your project and click **OK**.</span></span>

[![](external-authentication-services/_static/image71.png "Click to Expand the Image")](external-authentication-services/_static/image71.png)

<span data-ttu-id="bb7ca-153">**Yeni ASP.NET projesi** görüntülendiğinde **tek sayfalı uygulama** şablonunu seçin ve **proje oluştur**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-153">When the **New ASP.NET Project** is displayed, select the **Single Page Application** template and click **Create Project**.</span></span>

[![](external-authentication-services/_static/image72.png "Click to Expand the Image")](external-authentication-services/_static/image72.png)

<span data-ttu-id="bb7ca-154">Visual Studio 2017, projenizi oluşturduğundan bekleyin.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-154">Wait as Visual Studio 2017 creates your project.</span></span>

<!-- [![](external-authentication-services/_static/image12.png "Click to Expand the Image")](external-authentication-services/_static/image11.png) -->

<span data-ttu-id="bb7ca-155">Visual Studio 2017, projenizi oluşturmayı tamamladığında, **uygulama\_başlangıç** klasöründe bulunan *Startup.auth.cs* dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-155">When Visual Studio 2017 has finished creating your project, open the *Startup.Auth.cs* file that is located in the **App\_Start** folder.</span></span>

<span data-ttu-id="bb7ca-156">Projeyi ilk oluşturduğunuzda, *Startup.auth.cs* dosyasında dış kimlik doğrulama hizmetlerinden hiçbiri etkinleştirilmemiştir; Aşağıda, kodunuzun neye benzebileceği, bir dış kimlik doğrulama hizmetini ve ASP.NET uygulamanızla Microsoft hesapları, Twitter, Facebook veya Google kimlik doğrulamasını kullanabilmeniz için gereken tüm ayarları vurgulayabileceğiniz bölümler verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-156">When you first create the project, none of the external authentication services are enabled in *Startup.Auth.cs* file; the following illustrates what your code might resemble, with the sections highlighted for where you would enable an external authentication service and any relevant settings in order to use Microsoft Accounts, Twitter, Facebook, or Google authentication with your ASP.NET application:</span></span>

[!code-csharp[Main](external-authentication-services/samples/sample1.cs)]

<span data-ttu-id="bb7ca-157">Web uygulamanızı derlemek ve hata ayıklamak için F5 tuşuna bastığınızda, hiçbir dış kimlik doğrulama hizmeti tanımlanmayacak olduğunu göreceğiniz bir oturum açma ekranı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-157">When you press F5 to build and debug your web application, it will display a login screen where you will see that no external authentication services have been defined.</span></span>

[![](external-authentication-services/_static/image73.png "Click to Expand the Image")](external-authentication-services/_static/image73.png)

<span data-ttu-id="bb7ca-158">Aşağıdaki bölümlerde, Visual Studio 2017 ' de ASP.NET ile birlikte sunulan dış kimlik doğrulama hizmetlerinin her birini nasıl etkinleştireceğinizi öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-158">In the following sections, you will learn how to enable each of the external authentication services that are provided with ASP.NET in Visual Studio 2017.</span></span>

<a id="FACEBOOK"></a>
## <a name="enabling-facebook-authentication"></a><span data-ttu-id="bb7ca-159">Facebook kimlik doğrulamasını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="bb7ca-159">Enabling Facebook authentication</span></span>

<span data-ttu-id="bb7ca-160">Facebook kimlik doğrulamasının kullanılması için bir Facebook Geliştirici hesabı oluşturmanız gerekir ve projeniz, Facebook 'tan çalışması için bir uygulama KIMLIĞI ve gizli anahtar gerektirir.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-160">Using Facebook authentication requires you to create a Facebook developer account, and your project will require an application ID and secret key from Facebook in order to function.</span></span> <span data-ttu-id="bb7ca-161">Facebook Geliştirici hesabı oluşturma ve uygulama KIMLIĞINIZI ve gizli anahtarınızı alma hakkında daha fazla bilgi için bkz. [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span><span class="sxs-lookup"><span data-stu-id="bb7ca-161">For information about creating a Facebook developer account and obtaining your application ID and secret key, see [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span></span>

<span data-ttu-id="bb7ca-162">Uygulama KIMLIĞI ve gizli anahtarı aldıktan sonra, Web uygulamanız için Facebook kimlik doğrulamasını etkinleştirmek üzere aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-162">Once you have obtained your application ID and secret key, use the following steps to enable Facebook authentication for your web application:</span></span>

1. <span data-ttu-id="bb7ca-163">Projeniz Visual Studio 2017 ' de açıldığında, *Startup.auth.cs* dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-163">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="bb7ca-164">Kodun Facebook kimlik doğrulaması bölümünü bulun:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-164">Locate the Facebook authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample2.cs)]
3. <span data-ttu-id="bb7ca-165">Vurgulanan kod satırlarının açıklamalarını kaldırmak için &quot;//&quot; karakterleri kaldırın ve ardından uygulama KIMLIĞINIZI ve gizli anahtarınızı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-165">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your application ID and secret key.</span></span> <span data-ttu-id="bb7ca-166">Bu parametreleri ekledikten sonra projenizi yeniden derleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-166">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample3.cs)]
4. <span data-ttu-id="bb7ca-167">Web uygulamanızı Web tarayıcınızda açmak için F5 tuşuna bastığınızda Facebook 'un bir dış kimlik doğrulama hizmeti olarak tanımlandığını görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-167">When you press F5 to open your web application in your web browser, you will see that Facebook has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image74.png "Click to Expand the Image")](external-authentication-services/_static/image74.png)
5. <span data-ttu-id="bb7ca-168">**Facebook** düğmesine tıkladığınızda, tarayıcınız Facebook oturum açma sayfasına yönlendirilir:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-168">When you click the **Facebook** button, your browser will be redirected to the Facebook login page:</span></span>

    [![](external-authentication-services/_static/image22.png "Click to Expand the Image")](external-authentication-services/_static/image21.png)
6. <span data-ttu-id="bb7ca-169">Facebook kimlik bilgilerinizi girdikten ve **oturum aç**' a tıkladıktan sonra, Web tarayıcınız Web uygulamanıza geri yönlendirilir ve bu, Facebook hesabınızla Ilişkilendirmek istediğiniz **Kullanıcı adını** ister:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-169">After you enter your Facebook credentials and click **Log in**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Facebook account:</span></span>

    [![](external-authentication-services/_static/image24.png "Click to Expand the Image")](external-authentication-services/_static/image23.png)
7. <span data-ttu-id="bb7ca-170">Kullanıcı adınızı girdikten ve **Kaydol** düğmesine tıkladıktan sonra, Web uygulamanız Facebook hesabınız için varsayılan **giriş sayfasını** görüntüleyecektir:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-170">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Facebook account:</span></span>

    [![](external-authentication-services/_static/image26.png "Click to Expand the Image")](external-authentication-services/_static/image25.png)

<a id="GOOGLE"></a>
## <a name="enabling-google-authentication"></a><span data-ttu-id="bb7ca-171">Google kimlik doğrulamasını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="bb7ca-171">Enabling Google Authentication</span></span>

<span data-ttu-id="bb7ca-172">Google kimlik doğrulamasının kullanılması için bir Google Geliştirici hesabı oluşturmanız gerekir ve projenizin çalışması için Google 'dan bir uygulama KIMLIĞI ve gizli anahtar gerekir.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-172">Using Google authentication requires you to create a Google developer account, and your project will require an application ID and secret key from Google in order to function.</span></span> <span data-ttu-id="bb7ca-173">Google Geliştirici hesabı oluşturma ve uygulama KIMLIĞINIZI ve gizli anahtarınızı alma hakkında bilgi için bkz. [https://developers.google.com](https://developers.google.com).</span><span class="sxs-lookup"><span data-stu-id="bb7ca-173">For information about creating a Google developer account and obtaining your application ID and secret key, see [https://developers.google.com](https://developers.google.com).</span></span>

<span data-ttu-id="bb7ca-174">Web uygulamanızda Google kimlik doğrulamasını etkinleştirmek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-174">To enable Google authentication for your web application, use the following steps:</span></span>

1. <span data-ttu-id="bb7ca-175">Projeniz Visual Studio 2017 ' de açıldığında, *Startup.auth.cs* dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-175">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="bb7ca-176">Kodun Google Authentication bölümünü bulun:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-176">Locate the Google authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample4.cs)]
3. <span data-ttu-id="bb7ca-177">Vurgulanan kod satırlarının açıklamalarını kaldırmak için &quot;//&quot; karakterleri kaldırın ve ardından uygulama KIMLIĞINIZI ve gizli anahtarınızı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-177">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your application ID and secret key.</span></span> <span data-ttu-id="bb7ca-178">Bu parametreleri ekledikten sonra projenizi yeniden derleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-178">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample5.cs)]
4. <span data-ttu-id="bb7ca-179">Web uygulamanızı Web tarayıcınızda açmak için F5 tuşuna bastığınızda, Google 'ın dış kimlik doğrulama hizmeti olarak tanımlandığını görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-179">When you press F5 to open your web application in your web browser, you will see that Google has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image75.png "Click to Expand the Image")](external-authentication-services/_static/image75.png)
5. <span data-ttu-id="bb7ca-180">**Google** düğmesine tıkladığınızda, tarayıcınız Google oturum açma sayfasına yönlendirilir:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-180">When you click the **Google** button, your browser will be redirected to the Google login page:</span></span>

    [![](external-authentication-services/_static/image32.png "Click to Expand the Image")](external-authentication-services/_static/image31.png)
6. <span data-ttu-id="bb7ca-181">Google kimlik bilgilerinizi girdikten ve **oturum aç**' a tıkladıktan sonra Google, Web uygulamanızın Google hesabınıza erişmek için gereken izinlere sahip olduğunu doğrulamanızı ister:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-181">After you enter your Google credentials and click **Sign in**, Google will prompt you to verify that your web application has permissions to access your Google account:</span></span>

    [![](external-authentication-services/_static/image34.png "Click to Expand the Image")](external-authentication-services/_static/image33.png)
7. <span data-ttu-id="bb7ca-182">**Kabul et**' e tıkladığınızda, Web tarayıcınız Web uygulamanıza geri yönlendirilir ve bu, Google hesabınızla Ilişkilendirmek istediğiniz **Kullanıcı adını** ister:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-182">When you click **Accept**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Google account:</span></span>

    [![](external-authentication-services/_static/image36.png "Click to Expand the Image")](external-authentication-services/_static/image35.png)
8. <span data-ttu-id="bb7ca-183">Kullanıcı adınızı girdikten ve **Kaydol** düğmesine tıkladıktan sonra, Web uygulamanız Google hesabınız için varsayılan **giriş sayfasını** görüntüleyecektir:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-183">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Google account:</span></span>

    [![](external-authentication-services/_static/image38.png "Click to Expand the Image")](external-authentication-services/_static/image37.png)

<a id="MICROSOFT"></a>
## <a name="enabling-microsoft-authentication"></a><span data-ttu-id="bb7ca-184">Microsoft kimlik doğrulamasını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="bb7ca-184">Enabling Microsoft Authentication</span></span>

<span data-ttu-id="bb7ca-185">Microsoft kimlik doğrulaması, bir geliştirici hesabı oluşturmanızı gerektirir ve çalışması için istemci KIMLIĞI ve istemci gizli anahtarı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-185">Microsoft authentication requires you to create a developer account, and it requires a client ID and client secret in order to function.</span></span> <span data-ttu-id="bb7ca-186">Bir Microsoft Geliştirici hesabı oluşturma ve istemci KIMLIĞINIZI ve istemci gizli anahtarını alma hakkında bilgi için bkz. [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070).</span><span class="sxs-lookup"><span data-stu-id="bb7ca-186">For information about creating a Microsoft developer account and obtaining your client ID and client secret, see [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070).</span></span>

<span data-ttu-id="bb7ca-187">Tüketici anahtarınızı ve tüketici gizli anahtarını aldıktan sonra, Web uygulamanız için Microsoft kimlik doğrulamasını etkinleştirmek üzere aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-187">Once you have obtained your consumer key and consumer secret, use the following steps to enable Microsoft authentication for your web application:</span></span>

1. <span data-ttu-id="bb7ca-188">Projeniz Visual Studio 2017 ' de açıldığında, *Startup.auth.cs* dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-188">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="bb7ca-189">Kodun Microsoft kimlik doğrulama bölümünü bulun:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-189">Locate the Microsoft authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample6.cs)]
3. <span data-ttu-id="bb7ca-190">Vurgulanan kod satırlarının açıklamalarını kaldırmak için &quot;//&quot; karakterleri kaldırın ve ardından istemci KIMLIĞINIZI ve istemci gizli anahtarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-190">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your client ID and client secret.</span></span> <span data-ttu-id="bb7ca-191">Bu parametreleri ekledikten sonra projenizi yeniden derleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-191">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample7.cs)]
4. <span data-ttu-id="bb7ca-192">Web uygulamanızı Web tarayıcınızda açmak için F5 tuşuna bastığınızda, Microsoft 'un bir dış kimlik doğrulama hizmeti olarak tanımlandığını görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-192">When you press F5 to open your web application in your web browser, you will see that Microsoft has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image42.png "Click to Expand the Image")](external-authentication-services/_static/image41.png)
5. <span data-ttu-id="bb7ca-193">**Microsoft** düğmesine tıkladığınızda, tarayıcınız Microsoft oturum açma sayfasına yönlendirilir:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-193">When you click the **Microsoft** button, your browser will be redirected to the Microsoft login page:</span></span>

    [![](external-authentication-services/_static/image44.png "Click to Expand the Image")](external-authentication-services/_static/image43.png)
6. <span data-ttu-id="bb7ca-194">Microsoft kimlik bilgilerinizi girdikten ve **oturum aç**' a tıkladıktan sonra, web uygulamanızın Microsoft hesabı erişim izinleri olduğunu doğrulamanız istenir:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-194">After you enter your Microsoft credentials and click **Sign in**, you will be prompted to verify that your web application has permissions to access your Microsoft account:</span></span>

    [![](external-authentication-services/_static/image46.png "Click to Expand the Image")](external-authentication-services/_static/image45.png)
7. <span data-ttu-id="bb7ca-195">**Evet**' e tıkladığınızda, Web tarayıcınız Web uygulamanıza geri yönlendirilir ve bu, Microsoft hesabı Ilişkilendirmek istediğiniz **Kullanıcı adını** ister:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-195">When you click **Yes**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Microsoft account:</span></span>

    [![](external-authentication-services/_static/image48.png "Click to Expand the Image")](external-authentication-services/_static/image47.png)
8. <span data-ttu-id="bb7ca-196">Kullanıcı adınızı girdikten ve **Kaydol** düğmesine tıkladıktan sonra, web uygulamanız Microsoft hesabı varsayılan **giriş sayfasını** görüntüleyecektir:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-196">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Microsoft account:</span></span>

    [![](external-authentication-services/_static/image50.png "Click to Expand the Image")](external-authentication-services/_static/image49.png)

<a id="TWITTER"></a>
## <a name="enabling-twitter-authentication"></a><span data-ttu-id="bb7ca-197">Twitter kimlik doğrulamasını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="bb7ca-197">Enabling Twitter Authentication</span></span>

<span data-ttu-id="bb7ca-198">Twitter kimlik doğrulaması bir geliştirici hesabı oluşturmanızı gerektirir ve çalışması için bir tüketici anahtarı ve tüketici parolası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-198">Twitter authentication requires you to create a developer account, and it requires a consumer key and consumer secret in order to function.</span></span> <span data-ttu-id="bb7ca-199">Twitter geliştirici hesabı oluşturma ve tüketici anahtarınızı ve tüketici gizli anahtarını alma hakkında daha fazla bilgi için bkz. [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span><span class="sxs-lookup"><span data-stu-id="bb7ca-199">For information about creating a Twitter developer account and obtaining your consumer key and consumer secret, see [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span></span>

<span data-ttu-id="bb7ca-200">Tüketici anahtarınızı ve tüketici gizli anahtarını aldıktan sonra, Web uygulamanız için Twitter kimlik doğrulamasını etkinleştirmek üzere aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-200">Once you have obtained your consumer key and consumer secret, use the following steps to enable Twitter authentication for your web application:</span></span>

1. <span data-ttu-id="bb7ca-201">Projeniz Visual Studio 2017 ' de açıldığında, *Startup.auth.cs* dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-201">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="bb7ca-202">Kodun Twitter kimlik doğrulaması bölümünü bulun:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-202">Locate the Twitter authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample8.cs)]
3. <span data-ttu-id="bb7ca-203">Vurgulanan kod satırlarının açıklamalarını kaldırmak için &quot;//&quot; karakterleri kaldırın ve ardından tüketici anahtarınızı ve tüketici gizli anahtarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-203">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your consumer key and consumer secret.</span></span> <span data-ttu-id="bb7ca-204">Bu parametreleri ekledikten sonra projenizi yeniden derleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-204">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample9.cs)]
4. <span data-ttu-id="bb7ca-205">Web uygulamanızı Web tarayıcınızda açmak için F5 tuşuna bastığınızda, Twitter 'nın bir dış kimlik doğrulama hizmeti olarak tanımlandığını görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-205">When you press F5 to open your web application in your web browser, you will see that Twitter has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image54.png "Click to Expand the Image")](external-authentication-services/_static/image53.png)
5. <span data-ttu-id="bb7ca-206">**Twitter** düğmesine tıkladığınızda, tarayıcınız Twitter oturum açma sayfasına yönlendirilir:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-206">When you click the **Twitter** button, your browser will be redirected to the Twitter login page:</span></span>

    [![](external-authentication-services/_static/image56.png "Click to Expand the Image")](external-authentication-services/_static/image55.png)
6. <span data-ttu-id="bb7ca-207">Twitter kimlik bilgilerinizi girdikten ve **uygulamayı Yetkilendir**' e tıkladıktan sonra, Web tarayıcınız Web uygulamanıza yeniden yönlendirilir ve bu, Twitter hesabınızla Ilişkilendirmek istediğiniz **Kullanıcı adını** ister:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-207">After you enter your Twitter credentials and click **Authorize app**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Twitter account:</span></span>

    [![](external-authentication-services/_static/image58.png "Click to Expand the Image")](external-authentication-services/_static/image57.png)
7. <span data-ttu-id="bb7ca-208">Kullanıcı adınızı girdikten ve **Kaydol** düğmesine tıkladıktan sonra, Web uygulamanız Twitter hesabınız için varsayılan **giriş sayfasını** görüntüleyecektir:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-208">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Twitter account:</span></span>

    [![](external-authentication-services/_static/image60.png "Click to Expand the Image")](external-authentication-services/_static/image59.png)

<a id="MOREINFO"></a>
## <a name="additional-information"></a><span data-ttu-id="bb7ca-209">Ek Bilgiler</span><span class="sxs-lookup"><span data-stu-id="bb7ca-209">Additional Information</span></span>

<span data-ttu-id="bb7ca-210">OAuth ve OpenID kullanan uygulamalar oluşturma hakkında daha fazla bilgi için aşağıdaki URL 'Lere bakın:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-210">For additional information about creating applications that use OAuth and OpenID, see the following URLs:</span></span>

- [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)
- [https://go.microsoft.com/fwlink/?LinkID=243995](https://go.microsoft.com/fwlink/?LinkID=243995)

<a id="COMBINE"></a>
### <a name="combining-external-authentication-services"></a><span data-ttu-id="bb7ca-211">Dış kimlik doğrulama hizmetlerini birleştirme</span><span class="sxs-lookup"><span data-stu-id="bb7ca-211">Combining External Authentication Services</span></span>

<span data-ttu-id="bb7ca-212">Daha fazla esneklik için, aynı anda birden çok dış kimlik doğrulama hizmeti tanımlayabilirsiniz. Bu, Web uygulamanızın kullanıcılarının etkinleştirilmiş dış kimlik doğrulama hizmetlerinden herhangi birinden bir hesap kullanmasına izin verir:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-212">For greater flexibility, you can define multiple external authentication services at the same time - this allows your web application's users to use an account from any of the enabled external authentication services:</span></span>

[![](external-authentication-services/_static/image62.png "Click to Expand the Image")](external-authentication-services/_static/image61.png)

<a id="FQDN"></a>
### <a name="configure-iis-express-to-use-a-fully-qualified-domain-name"></a><span data-ttu-id="bb7ca-213">Tam etki alanı adını kullanmak için IIS Express yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bb7ca-213">Configure IIS Express to use a fully qualified domain name</span></span>

<span data-ttu-id="bb7ca-214">Bazı dış kimlik doğrulama sağlayıcıları, `http://localhost:port/`gibi bir HTTP adresi kullanarak uygulamanızı test etmeyi desteklemez.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-214">Some external authentication providers do not support testing your application by using an HTTP address like `http://localhost:port/`.</span></span> <span data-ttu-id="bb7ca-215">Bu sorunu geçici olarak çözmek için, ana bilgisayar dosyanıza statik bir tam etki alanı adı (FQDN) eşlemesi ekleyebilir ve Visual Studio 2017 ' de proje seçeneklerinizi, test/hata ayıklama için FQDN kullanacak şekilde yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-215">To work around this issue, you can add a static Fully Qualified Domain Name (FQDN) mapping to your HOSTS file and configure your project options in Visual Studio 2017 to use the FQDN for testing/debugging.</span></span> <span data-ttu-id="bb7ca-216">Bunu yapmak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-216">To do so, use the following steps:</span></span>

- <span data-ttu-id="bb7ca-217">Ana bilgisayar dosyanıza eşlenen statik bir FQDN ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-217">Add a static FQDN mapping your HOSTS file:</span></span>

  1. <span data-ttu-id="bb7ca-218">Windows 'da yükseltilmiş bir komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-218">Open an elevated command prompt in Windows.</span></span>
  2. <span data-ttu-id="bb7ca-219">Şu komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-219">Type the following command:</span></span>

      <span data-ttu-id="bb7ca-220"><kbd>Not defteri%WinDir%\system32\drivers\etc\hosts</kbd></span><span class="sxs-lookup"><span data-stu-id="bb7ca-220"><kbd>notepad %WinDir%\system32\drivers\etc\hosts</kbd></span></span>
  3. <span data-ttu-id="bb7ca-221">HOSTS dosyasına aşağıdakine benzer bir giriş ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-221">Add an entry like the following to the HOSTS file:</span></span>

      <span data-ttu-id="bb7ca-222"><kbd>127.0.0.1 www.wingtiptoys.com</kbd></span><span class="sxs-lookup"><span data-stu-id="bb7ca-222"><kbd>127.0.0.1 www.wingtiptoys.com</kbd></span></span>
  4. <span data-ttu-id="bb7ca-223">HOSTS dosyanızı kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-223">Save and close your HOSTS file.</span></span>

- <span data-ttu-id="bb7ca-224">Visual Studio projenizi FQDN kullanacak şekilde yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-224">Configure your Visual Studio project to use the FQDN:</span></span>

  1. <span data-ttu-id="bb7ca-225">Projeniz Visual Studio 2017 ' de açıldığında, **Proje** menüsüne tıklayın ve ardından projenizin özelliklerini seçin.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-225">When your project is open in Visual Studio 2017, click the **Project** menu, and then select your project's properties.</span></span> <span data-ttu-id="bb7ca-226">Örneğin, **WebApplication1 özelliklerini**seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-226">For example, you might select **WebApplication1 Properties**.</span></span>
  2. <span data-ttu-id="bb7ca-227">**Web** sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-227">Select the **Web** tab.</span></span>
  3. <span data-ttu-id="bb7ca-228"><strong>Proje URL 'si</strong>için FQDN 'nizi girin.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-228">Enter your FQDN for the <strong>Project Url</strong>.</span></span> <span data-ttu-id="bb7ca-229">Örneğin, ana bilgisayar dosyanıza eklediğiniz FQDN eşlemesiyle <kbd><http://www.wingtiptoys.com></kbd> girersiniz.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-229">For example, you would enter <kbd><http://www.wingtiptoys.com></kbd> if that was the FQDN mapping that you added to your HOSTS file.</span></span>

- <span data-ttu-id="bb7ca-230">Uygulamanız için FQDN kullanmak üzere IIS Express yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-230">Configure IIS Express to use the FQDN for your application:</span></span>

    1. <span data-ttu-id="bb7ca-231">Windows 'da yükseltilmiş bir komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-231">Open an elevated command prompt in Windows.</span></span>
    2. <span data-ttu-id="bb7ca-232">IIS Express klasörünüze geçmek için aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-232">Type the following command to change to your IIS Express folder:</span></span>

        <span data-ttu-id="bb7ca-233"><kbd>CD/d &quot;%ProgramFiles%\IIS Express&quot;</kbd></span><span class="sxs-lookup"><span data-stu-id="bb7ca-233"><kbd>cd /d &quot;%ProgramFiles%\IIS Express&quot;</kbd></span></span>
    3. <span data-ttu-id="bb7ca-234">FQDN 'yi uygulamanıza eklemek için aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-234">Type the following command to add the FQDN to your application:</span></span>

        <span data-ttu-id="bb7ca-235"><kbd>Appcmd. exe set config-Section: System. applicationHost/Sites/+&quot;[ad = ' WebApplication1 ']. Bindings. [Protocol = ' http ', bindingInformation = ' \*: 80: www. wingtiptoys. com ']&quot;/Commit: apphost</kbd></span><span class="sxs-lookup"><span data-stu-id="bb7ca-235"><kbd>appcmd.exe set config -section:system.applicationHost/sites /+&quot;[name='WebApplication1'].bindings.[protocol='http',bindingInformation='\*:80:www.wingtiptoys.com']&quot; /commit:apphost</kbd></span></span>

  <span data-ttu-id="bb7ca-236">Burada **WebApplication1** , projenizin adı ve **bindingInformation** , testiniz için kullanmak istediğiniz bağlantı noktası numarasını ve FQDN 'yi içerir.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-236">Where **WebApplication1** is the name of your project and **bindingInformation** contains the port number and FQDN that you want to use for your testing.</span></span>

<a id="OBTAIN"></a>
### <a name="how-to-obtain-your-application-settings-for-microsoft-authentication"></a><span data-ttu-id="bb7ca-237">Microsoft kimlik doğrulaması için uygulama ayarlarınızı edinme</span><span class="sxs-lookup"><span data-stu-id="bb7ca-237">How to Obtain your Application Settings for Microsoft Authentication</span></span>

<span data-ttu-id="bb7ca-238">Microsoft kimlik doğrulaması için bir uygulamayı Windows Live 'a bağlama basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-238">Linking an application to Windows Live for Microsoft Authentication is a simple process.</span></span> <span data-ttu-id="bb7ca-239">Bir uygulamayı Windows Live 'a henüz bağladıysanız, aşağıdaki adımları kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-239">If you have not already linked an application to Windows Live, you can use the following steps:</span></span>

1. <span data-ttu-id="bb7ca-240">[https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070) gidin ve istendiğinde Microsoft hesabı adınızı ve parolanızı girip **oturum aç**' a tıklayın:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-240">Browse to [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070) and enter your Microsoft account name and password when prompted, then click **Sign in**:</span></span>

   <!--  [![](external-authentication-services/_static/image64.png "Click to Expand the Image")](external-authentication-services/_static/image63.png) -->
2. <span data-ttu-id="bb7ca-241">**Uygulama Ekle** ' yi seçin ve sorulduğunda uygulamanızın adını girin ve ardından **Oluştur**' a tıklayın:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-241">Select **Add an app** and enter the name of your application when prompted, and then click **Create**:</span></span>

    [![](external-authentication-services/_static/image79.png "Click to Expand the Image")](external-authentication-services/_static/image79.png)
3. <span data-ttu-id="bb7ca-242">**Ad** ' ın altında uygulamanızı seçin ve uygulamanın Özellikler sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-242">Select your app under **Name** and its application properties page appears.</span></span>

4. <span data-ttu-id="bb7ca-243">Uygulamanız için yeniden yönlendirme etki alanını girin.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-243">Enter the redirect domain for your application.</span></span> <span data-ttu-id="bb7ca-244">**Uygulama kimliği** ' ni kopyalayın ve **Uygulama parolaları**' nın altında **parola oluştur**' u seçin.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-244">Copy the **Application ID** and, under **Application Secrets**, select **Generate Password**.</span></span> <span data-ttu-id="bb7ca-245">Görüntülenen parolayı kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-245">Copy the password that appears.</span></span> <span data-ttu-id="bb7ca-246">Uygulama KIMLIĞI ve parolası, istemci KIMLIĞINIZ ve istemci gizli anahtarı.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-246">The application ID and password are your client ID and client secret.</span></span> <span data-ttu-id="bb7ca-247">**Tamam** ' ı ve ardından **Kaydet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-247">Select **Ok** and then **Save**.</span></span>

    [![](external-authentication-services/_static/image77.png "Click to Expand the Image")](external-authentication-services/_static/image77.png)

<a id="DISABLE"></a>
### <a name="optional-disable-local-registration"></a><span data-ttu-id="bb7ca-248">İsteğe bağlı: yerel kaydı devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="bb7ca-248">Optional: Disable Local Registration</span></span>

<span data-ttu-id="bb7ca-249">Geçerli ASP.NET yerel kayıt işlevselliği otomatik programların (botların) üye hesaplarını oluşturmasını engellemez; Örneğin, [CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md)gibi bir bot önleme ve doğrulama teknolojisi kullanarak.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-249">The current ASP.NET local registration functionality does not prevent automated programs (bots) from creating member accounts; for example, by using a bot-prevention and validation technology like [CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md).</span></span> <span data-ttu-id="bb7ca-250">Bu nedenle, oturum açma sayfasındaki yerel oturum açma formunu ve kayıt bağlantısını kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-250">Because of this, you should remove the local login form and registration link on the login page.</span></span> <span data-ttu-id="bb7ca-251">Bunu yapmak için, projenizdeki *login. cshtml sayfasını\_* açın ve ardından yerel oturum açma paneli ve kayıt bağlantısı için satırları açıklama olarak inceleyin.</span><span class="sxs-lookup"><span data-stu-id="bb7ca-251">To do so, open the *\_Login.cshtml* page in your project, and then comment out the lines for the local login panel and the registration link.</span></span> <span data-ttu-id="bb7ca-252">Sonuç sayfası aşağıdaki kod örneği gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-252">The resulting page should look like the following code sample:</span></span>

[!code-html[Main](external-authentication-services/samples/sample10.html)]

<span data-ttu-id="bb7ca-253">Yerel oturum açma paneli ve kayıt bağlantısı devre dışı bırakıldıktan sonra, oturum açma sayfanız yalnızca etkinleştirdiğiniz dış kimlik doğrulama sağlayıcılarını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="bb7ca-253">Once the local login panel and the registration link have been disabled, your login page will only display the external authentication providers that you have enabled:</span></span>

[![](external-authentication-services/_static/image70.png "Click to Expand the Image")](external-authentication-services/_static/image69.png)
