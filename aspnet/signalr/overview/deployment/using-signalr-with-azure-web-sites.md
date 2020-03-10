---
uid: signalr/overview/deployment/using-signalr-with-azure-web-sites
title: Azure App Service Web Apps ile SignalR kullanma | Microsoft Docs
author: bradygaster
description: Bu belgede, Microsoft Azure üzerinde çalışan bir SignalR uygulamasının nasıl yapılandırılacağı açıklanmaktadır. Öğreticide kullanılan yazılım sürümleri Visual Studio 2013 veya VIS...
ms.author: bradyg
ms.date: 07/01/2015
ms.assetid: 2a7517a0-b88c-4162-ade3-9bf6ca7062fd
msc.legacyurl: /signalr/overview/deployment/using-signalr-with-azure-web-sites
msc.type: authoredcontent
ms.openlocfilehash: 0e6a18bdbe9cc47e89b5a458753845afb53595f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558704"
---
# <a name="using-signalr-with-web-apps-in-azure-app-service"></a><span data-ttu-id="91291-104">Azure App Service'te Web Apps ile SignalR Kullanma</span><span class="sxs-lookup"><span data-stu-id="91291-104">Using SignalR with Web Apps in Azure App Service</span></span>

<span data-ttu-id="91291-105">, [Patrick Fleti](https://github.com/pfletcher) tarafından</span><span class="sxs-lookup"><span data-stu-id="91291-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="91291-106">Bu belgede, Microsoft Azure üzerinde çalışan bir SignalR uygulamasının nasıl yapılandırılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="91291-106">This document describes how to configure a SignalR application that runs on Microsoft Azure.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="91291-107">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="91291-107">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="91291-108">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) veya Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="91291-108">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) or Visual Studio 2012</span></span>
> - <span data-ttu-id="91291-109">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="91291-109">.NET 4.5</span></span>
> - <span data-ttu-id="91291-110">SignalR sürüm 2</span><span class="sxs-lookup"><span data-stu-id="91291-110">SignalR version 2</span></span>
> - <span data-ttu-id="91291-111">Visual Studio 2013 veya 2012 için Azure SDK 2,3</span><span class="sxs-lookup"><span data-stu-id="91291-111">Azure SDK 2.3 for Visual Studio 2013 or 2012</span></span>
>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="91291-112">Sorular ve açıklamalar</span><span class="sxs-lookup"><span data-stu-id="91291-112">Questions and comments</span></span>
>
> <span data-ttu-id="91291-113">Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun.</span><span class="sxs-lookup"><span data-stu-id="91291-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="91291-114">Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR), [StackOverflow.com](http://stackoverflow.com/)veya [Microsoft Azure forumlarına](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform)gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91291-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR), [StackOverflow.com](http://stackoverflow.com/), or the [Microsoft Azure forums](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform).</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="91291-115">İçindekiler</span><span class="sxs-lookup"><span data-stu-id="91291-115">Table of Contents</span></span>

- [<span data-ttu-id="91291-116">Giriş</span><span class="sxs-lookup"><span data-stu-id="91291-116">Introduction</span></span>](#introduction)
- [<span data-ttu-id="91291-117">Azure App Service için bir SignalR Web uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="91291-117">Deploying a SignalR Web App to Azure App Service</span></span>](#deploying)
- [<span data-ttu-id="91291-118">Azure App Service üzerinde WebSockets etkinleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="91291-118">Enabling WebSockets on Azure App Service</span></span>](#websocket)
- [<span data-ttu-id="91291-119">Azure Redis Cache Arkadüzlemi kullanma</span><span class="sxs-lookup"><span data-stu-id="91291-119">Using the Azure Redis Cache Backplane</span></span>](#backplane)
- [<span data-ttu-id="91291-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="91291-120">Next Steps</span></span>](#nextsteps)

<a id="introduction"></a>
## <a name="introduction"></a><span data-ttu-id="91291-121">Giriş</span><span class="sxs-lookup"><span data-stu-id="91291-121">Introduction</span></span>

<span data-ttu-id="91291-122">ASP.NET SignalR, sunucular ve Web veya .NET istemcileri arasında yeni bir etkileşim düzeyi getirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="91291-122">ASP.NET SignalR can be used to bring a new level of interactivity between servers and web or .NET clients.</span></span> <span data-ttu-id="91291-123">Azure 'da barındırıldığında, SignalR uygulamaları, bulutta çalışan yüksek oranda kullanılabilir, ölçeklenebilir ve performanslı ortamlarından faydalanabilir.</span><span class="sxs-lookup"><span data-stu-id="91291-123">When hosted in Azure, SignalR applications can take advantage of the highly available, scalable, and performant environment that running in the cloud provides.</span></span>

<a id="deploying"></a>
## <a name="deploying-a-signalr-web-app-to-azure-app-service"></a><span data-ttu-id="91291-124">Azure App Service için bir SignalR Web uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="91291-124">Deploying a SignalR Web App to Azure App Service</span></span>

<span data-ttu-id="91291-125">SignalR, bir uygulamayı Azure 'a dağıtmaya ve şirket içi bir sunucuya dağıtmaya yönelik belirli bir karmaşıklıklar eklemez.</span><span class="sxs-lookup"><span data-stu-id="91291-125">SignalR doesn't add any particular complications to deploying an application to Azure versus deploying to an on-premises server.</span></span> <span data-ttu-id="91291-126">SignalR kullanan bir uygulama, yapılandırmada veya diğer ayarlarda herhangi bir değişiklik yapılmadan Azure 'da barındırılabilir (ancak WebSockets desteği için, aşağıdaki Azure App Service için bkz. [etkinleştirme WebSockets](#websocket) .) Bu öğreticide, Başlangıç [öğreticisinde](../getting-started/tutorial-getting-started-with-signalr.md) oluşturulan uygulamayı Azure 'a dağıtırsınız.</span><span class="sxs-lookup"><span data-stu-id="91291-126">An application that uses SignalR can be hosted in Azure without any changes in configuration or other settings (though for WebSockets support, see [Enabling WebSockets on Azure App Service](#websocket) below.) For this tutorial, you'll deploy the application created in the [Getting Started Tutorial](../getting-started/tutorial-getting-started-with-signalr.md) to Azure.</span></span>

<span data-ttu-id="91291-127">**Önkoşullar**</span><span class="sxs-lookup"><span data-stu-id="91291-127">**Prerequisites**</span></span>

- <span data-ttu-id="91291-128">Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="91291-128">Visual Studio 2013.</span></span> <span data-ttu-id="91291-129">Visual Studio yoksa, Azure SDK yüklemesine Web için Visual Studio 2013 Express eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="91291-129">If you don't have Visual Studio, Visual Studio 2013 Express for Web is included in the install of the Azure SDK.</span></span>
- <span data-ttu-id="91291-130">[Visual Studio 2013 Için Azure sdk 2,3](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409) veya [Visual Studio 2012 için Azure SDK 2,3](https://go.microsoft.com/fwlink/p/?linkid=323511).</span><span class="sxs-lookup"><span data-stu-id="91291-130">[Azure SDK 2.3 for Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409) or [Azure SDK 2.3 for Visual Studio 2012](https://go.microsoft.com/fwlink/p/?linkid=323511).</span></span>
- <span data-ttu-id="91291-131">Bu öğreticiyi tamamlayabilmeniz için bir Azure aboneliğine ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="91291-131">To complete this tutorial, you will need an Azure subscription.</span></span> <span data-ttu-id="91291-132">[MSDN abonesi avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)veya [deneme aboneliği için kaydolabilirsiniz](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="91291-132">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), or [sign up for a trial subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

### <a name="deploying-a-signalr-web-app-to-azure"></a><span data-ttu-id="91291-133">Azure 'a bir SignalR Web uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="91291-133">Deploying a SignalR web app to Azure</span></span>

1. <span data-ttu-id="91291-134">Başlangıç [öğreticisini](../getting-started/tutorial-getting-started-with-signalr.md)doldurun veya [kod galerisinden](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)tamamlanmış projeyi indirin.</span><span class="sxs-lookup"><span data-stu-id="91291-134">Complete the [Getting Started Tutorial](../getting-started/tutorial-getting-started-with-signalr.md), or download the finished project from [Code Gallery](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).</span></span>
2. <span data-ttu-id="91291-135">Visual Studio 'da **Build**, **SignalR sohbeti Yayımla**' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="91291-135">In Visual Studio, select **Build**, **Publish SignalR Chat**.</span></span>
3. <span data-ttu-id="91291-136">"Web 'i Yayımla" iletişim kutusunda "Windows Azure Web siteleri" ni seçin.</span><span class="sxs-lookup"><span data-stu-id="91291-136">In the "Publish Web" dialog, select "Windows Azure Web Sites".</span></span>

    ![Azure Web siteleri seçin](using-signalr-with-azure-web-sites/_static/image1.png)
4. <span data-ttu-id="91291-138">Microsoft hesabı oturum açmadıysanız, "var olan Web sitesini Seç" iletişim kutusunda **oturum aç...** öğesine tıklayın ve oturum açın.</span><span class="sxs-lookup"><span data-stu-id="91291-138">If you aren't signed in to your Microsoft account, click **Sign In...** in the "Select Existing Web Site" dialog, and sign in.</span></span>

    ![Mevcut Web sitesini seçin](using-signalr-with-azure-web-sites/_static/image2.png)    ![Azure'da oturum açma](using-signalr-with-azure-web-sites/_static/image3.png)
5. <span data-ttu-id="91291-141">"Varolan Web sitesini Seç" iletişim kutusunda **Yeni**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="91291-141">In the "Select Existing Web Site" dialog, click **New**.</span></span>

    ![Yeni Web sitesi](using-signalr-with-azure-web-sites/_static/image4.png)
6. <span data-ttu-id="91291-143">"Windows Azure 'da site oluştur" iletişim kutusunda benzersiz bir uygulama adı girin.</span><span class="sxs-lookup"><span data-stu-id="91291-143">In the "Create site on Windows Azure" dialog, enter a unique app name.</span></span> <span data-ttu-id="91291-144">Bölge açılan kutusunda size en yakın bölgeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="91291-144">Select the region closest to you in the Region dropdown.</span></span> <span data-ttu-id="91291-145">**Oluştur**'u tıklatın.</span><span class="sxs-lookup"><span data-stu-id="91291-145">Click **Create**.</span></span>

    ![Azure 'da site oluşturma](using-signalr-with-azure-web-sites/_static/image5.png)
7. <span data-ttu-id="91291-147">"Web 'i Yayımla" iletişim kutusunda **Yayımla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="91291-147">In the "Publish Web" dialog, click **Publish**.</span></span>

    ![Siteyi Yayımla](using-signalr-with-azure-web-sites/_static/image6.png)
8. <span data-ttu-id="91291-149">Uygulamanın yayımlanması tamamlandığında, Azure App Service Web Apps barındırılan SignalR sohbet uygulaması bir tarayıcıda açılır.</span><span class="sxs-lookup"><span data-stu-id="91291-149">When the app has completed publishing, the SignalR Chat application hosted in Azure App Service Web Apps will open in a browser.</span></span>

    ![Tarayıcıda açılan site](using-signalr-with-azure-web-sites/_static/image7.png)

<a id="websocket"></a>
### <a name="enabling-websockets-on-azure-app-service-web-apps"></a><span data-ttu-id="91291-151">Azure App Service Web Apps üzerinde WebSockets etkinleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="91291-151">Enabling WebSockets on Azure App Service Web Apps</span></span>

<span data-ttu-id="91291-152">WebSockets 'in bir SignalR uygulamasında kullanılabilmesi için Web uygulamanızda açık bir şekilde etkinleştirilmesi gerekir; Aksi takdirde, diğer protokoller kullanılacaktır (Ayrıntılar için bkz. [taşımalar ve Fallyedekler](../getting-started/introduction-to-signalr.md#transports) ).</span><span class="sxs-lookup"><span data-stu-id="91291-152">WebSockets needs to be explicitly enabled in your web app to be used in a SignalR application; otherwise, other protocols will be used (See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for details).</span></span>

<span data-ttu-id="91291-153">WebSockets Azure App Service Web Apps kullanmak için, Web uygulamasının yapılandırma bölümünde etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="91291-153">In order to use WebSockets on Azure App Service Web Apps, enable it in the configuration section of the web app.</span></span> <span data-ttu-id="91291-154">Bunu yapmak için, Web uygulamanızı [Azure yönetim portalı](https://manage.windowsazure.com/)açın ve Yapılandır ' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="91291-154">To do this, open your web app in the [Azure Management Portal](https://manage.windowsazure.com/), and select Configure.</span></span>

![Yapılandır sekmesi](using-signalr-with-azure-web-sites/_static/image8.png)

<span data-ttu-id="91291-156">Yapılandırma sayfasının en üstünde, .NET 4,5 ' in Web uygulamanız için kullanıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="91291-156">At the top of the configuration page, ensure that .NET 4.5 is used for your web app.</span></span>

![.NET Framework sürüm 4,5 ayarı](using-signalr-with-azure-web-sites/_static/image9.png)

<span data-ttu-id="91291-158">Yapılandırma sayfasında, **WebSockets** ayarında **Açık**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="91291-158">On the configuration page, in the **WebSockets** setting, select **On**.</span></span>

![WebSockets ayarı: açık](using-signalr-with-azure-web-sites/_static/image10.png)

<span data-ttu-id="91291-160">Değişikliklerinizi kaydetmek için yapılandırma sayfasının alt kısmındaki **Kaydet** ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="91291-160">At the bottom of the Configuration page, select **Save** to save your changes.</span></span>

![Ayarları Kaydet](using-signalr-with-azure-web-sites/_static/image11.png)

<a id="backplane"></a>
## <a name="using-the-azure-redis-cache-backplane"></a><span data-ttu-id="91291-162">Azure Redis Cache Arkadüzlemi kullanma</span><span class="sxs-lookup"><span data-stu-id="91291-162">Using the Azure Redis Cache Backplane</span></span>

<span data-ttu-id="91291-163">Web uygulamanız için birden çok örnek kullanıyorsanız ve bu örneklerin kullanıcılarının birbirleriyle etkileşime ihtiyacı varsa (örneğin, bir örnekte oluşturulan sohbet iletileri diğer örneklere bağlı olan kullanıcılara ulaşabilmesi için), [Azure Redis Cache backdüzlemi](../performance/scaleout-with-redis.md) uygulamanızda uygulanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="91291-163">If you use multiple instances for your web app, and the users of those instances need to interact with one another (so that, for instance, chat messages created in one instance can reach the users connected to other instances), the [Azure Redis Cache backplane](../performance/scaleout-with-redis.md) must be implemented in your application.</span></span>

<a id="nextsteps"></a>
## <a name="next-steps"></a><span data-ttu-id="91291-164">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="91291-164">Next Steps</span></span>

<span data-ttu-id="91291-165">Azure App Service Web Apps hakkında daha fazla bilgi için bkz. [Web Apps genel bakış](https://azure.microsoft.com/documentation/articles/app-service-web-overview/).</span><span class="sxs-lookup"><span data-stu-id="91291-165">For more information on Web Apps in Azure App Service, see [Web Apps overview](https://azure.microsoft.com/documentation/articles/app-service-web-overview/).</span></span>
