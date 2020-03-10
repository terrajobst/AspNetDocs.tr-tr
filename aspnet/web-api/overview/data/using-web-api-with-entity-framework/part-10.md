---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-10
title: Uygulamayı Azure 'da yayımlayın Azure App Service | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 10fd812b-94d6-4967-be97-a31ce9c45e2c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-10
msc.type: authoredcontent
ms.openlocfilehash: a9a7b74a07c71b47253c0af304c7a26ffa4eaae5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622390"
---
# <a name="publish-the-app-to-azure-azure-app-service"></a><span data-ttu-id="1fab5-102">Uygulamayı Azure 'da yayımlayın Azure App Service</span><span class="sxs-lookup"><span data-stu-id="1fab5-102">Publish the App to Azure Azure App Service</span></span>

<span data-ttu-id="1fab5-103">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="1fab5-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="1fab5-104">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="1fab5-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="1fab5-105">Son adım olarak, uygulamayı Azure 'da yayımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="1fab5-105">As the last step, you will publish the application to Azure.</span></span> <span data-ttu-id="1fab5-106">Çözüm Gezgini, projeye sağ tıklayın ve **Yayımla**' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="1fab5-106">In Solution Explorer, right-click the project and select **Publish**.</span></span>

![](part-10/_static/image1.png)

<span data-ttu-id="1fab5-107">**Yayımla** ' ya tıklamak **Web 'i Yayımla** iletişim kutusunu çağırır.</span><span class="sxs-lookup"><span data-stu-id="1fab5-107">Clicking **Publish** invokes the **Publish Web** dialog.</span></span> <span data-ttu-id="1fab5-108">Projeyi ilk oluşturduğunuz sırada **bulutta konak** denetlediyseniz, bağlantı ve ayarlar zaten yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="1fab5-108">If you checked **Host in Cloud** when you first created the project, then the connection and settings are already configured.</span></span> <span data-ttu-id="1fab5-109">Bu durumda, yalnızca **Ayarlar** sekmesine tıkladıktan sonra Code First Migrations&quot;&quot;Yürüt ' ü kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="1fab5-109">In that case, just click the **Settings** tab and check &quot;Execute Code First Migrations&quot;.</span></span> <span data-ttu-id="1fab5-110">(Başlangıçta **Konağı bulutta** denetmediyseniz, [sonraki bölümdeki](#new-website)adımları izleyin.)</span><span class="sxs-lookup"><span data-stu-id="1fab5-110">(If you didn't check **Host in Cloud** at the beginning, then follow the steps in the [next section](#new-website).)</span></span>

[![](part-10/_static/image3.png)](part-10/_static/image2.png)

<span data-ttu-id="1fab5-111">Uygulamayı dağıtmak için **Yayımla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1fab5-111">To deploy the app, click **Publish**.</span></span> <span data-ttu-id="1fab5-112">Yayımlama ilerlemesini **Web yayımlama etkinliği** penceresinde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1fab5-112">You can view the publishing progress in the **Web Publish Activity** window.</span></span> <span data-ttu-id="1fab5-113">( **Görünüm** menüsünde **diğer pencereler**' i seçin ve ardından **Web yayımlama etkinliği**' ni seçin.)</span><span class="sxs-lookup"><span data-stu-id="1fab5-113">(From the **View** menu, select **Other Windows**, then select **Web Publish Activity**.)</span></span>

![](part-10/_static/image4.png)

<span data-ttu-id="1fab5-114">Visual Studio uygulamayı dağıtırken, varsayılan tarayıcı otomatik olarak dağıtılan Web sitesinin URL 'SI olarak açılır ve oluşturduğunuz uygulama artık bulutta çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1fab5-114">When Visual Studio finishes deploying the app, the default browser automatically opens to the URL of the deployed website, and the application that you created is now running in the cloud.</span></span> <span data-ttu-id="1fab5-115">Tarayıcı adres çubuğundaki URL, sitenin Internet 'ten yüklenmekte olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="1fab5-115">The URL in the browser address bar shows that the site is being loaded from the Internet.</span></span>

[![](part-10/_static/image6.png)](part-10/_static/image5.png)

<a id="new-website"></a>
## <a name="deploying-to-a-new-website"></a><span data-ttu-id="1fab5-116">Yeni bir Web sitesine dağıtma</span><span class="sxs-lookup"><span data-stu-id="1fab5-116">Deploying to a New Website</span></span>

<span data-ttu-id="1fab5-117">Projeyi ilk oluşturduğunuzda **bulutta konak** denetmediyseniz, şimdi yeni bir Web uygulaması yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1fab5-117">If you did not check **Host in Cloud** when you first created the project, you can configure a new web app now.</span></span> <span data-ttu-id="1fab5-118">Çözüm Gezgini, projeye sağ tıklayın ve **Yayımla**' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="1fab5-118">In Solution Explorer, right-click the project and select **Publish**.</span></span> <span data-ttu-id="1fab5-119">**Profil** sekmesini seçin ve **Microsoft Azure Web siteleri**' ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1fab5-119">Select the **Profile** tab and click **Microsoft Azure Websites**.</span></span> <span data-ttu-id="1fab5-120">Şu anda Azure 'da oturum açmadıysanız, oturum açmanız istenir.</span><span class="sxs-lookup"><span data-stu-id="1fab5-120">If you aren't currently signed in to Azure, you will be prompted to sign in.</span></span>

[![](part-10/_static/image8.png)](part-10/_static/image7.png)

<span data-ttu-id="1fab5-121">**Mevcut Web siteleri** Iletişim kutusunda **Yeni**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1fab5-121">In the **Existing Websites** dialog, click **New**.</span></span>

![](part-10/_static/image9.png)

<span data-ttu-id="1fab5-122">Bir site adı girin.</span><span class="sxs-lookup"><span data-stu-id="1fab5-122">Enter a site name.</span></span> <span data-ttu-id="1fab5-123">Azure aboneliğinizi ve bölgeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="1fab5-123">Select your Azure subscription and the region.</span></span> <span data-ttu-id="1fab5-124">**Veritabanı sunucusu**altında **Yeni sunucu oluştur**' u seçin veya var olan bir sunucuyu seçin.</span><span class="sxs-lookup"><span data-stu-id="1fab5-124">Under **Database server**, select **Create New Server**, or select an existing server.</span></span> <span data-ttu-id="1fab5-125">**Oluştur**'u tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1fab5-125">Click **Create**.</span></span>

[![](part-10/_static/image11.png)](part-10/_static/image10.png)

<span data-ttu-id="1fab5-126">**Ayarlar** sekmesine tıklayın ve Code First Migrations&quot;&quot;yürütün ' i işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="1fab5-126">Click the **Settings** tab and check &quot;Execute Code First Migrations&quot;.</span></span> <span data-ttu-id="1fab5-127">Ardından **Yayımla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1fab5-127">Then click **Publish**.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="1fab5-128">Öncekini</span><span class="sxs-lookup"><span data-stu-id="1fab5-128">Previous</span></span>](part-9.md)
