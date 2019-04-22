---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: OWIN, ASP.NET Web API - ASP.NET barındırma kullanmasını 4.x
author: rick-anderson
description: Kodu bir konsol uygulamasında ASP.NET Web API'yi barındırmak nasıl gösteren öğretici.
ms.author: riande
ms.date: 07/09/2013
ms.custom: seoapril2019
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: a67db0bd061846af2db3599e0843ed7c6a22db1e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59386521"
---
# <a name="use-owin-to-self-host-aspnet-web-api"></a><span data-ttu-id="52946-103">Barındırılan ASP.NET Web API'si için OWIN kullanın</span><span class="sxs-lookup"><span data-stu-id="52946-103">Use OWIN to Self-Host ASP.NET Web API</span></span> 


> <span data-ttu-id="52946-104">Bu öğreticide, ASP.NET Web API OWIN barındırma Web API çerçevesini kullanarak bir konsol uygulamasında barındırmak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="52946-104">This tutorial shows how to host ASP.NET Web API in a console application, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="52946-105">[.NET için açık Web arabirimi](http://owin.org) (OWIN) .NET web sunucuları ve web uygulaması arasında bir Özet tanımlar.</span><span class="sxs-lookup"><span data-stu-id="52946-105">[Open Web Interface for .NET](http://owin.org) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="52946-106">OWIN OWIN kendi işleminizde IIS dışında bir web uygulaması kendi kendine barındırma için ideal hale getirir sunucu web uygulamasından ayırır.</span><span class="sxs-lookup"><span data-stu-id="52946-106">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="52946-107">Bu öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="52946-107">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="52946-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="52946-108">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/) 
> - <span data-ttu-id="52946-109">Web API 5.2.7</span><span class="sxs-lookup"><span data-stu-id="52946-109">Web API 5.2.7</span></span>


> [!NOTE]
> <span data-ttu-id="52946-110">Bu öğreticinin için tam kaynak kodunu bulabilirsiniz [github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample).</span><span class="sxs-lookup"><span data-stu-id="52946-110">You can find the complete source code for this tutorial at [github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample).</span></span>


## <a name="create-a-console-application"></a><span data-ttu-id="52946-111">Konsol uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="52946-111">Create a console application</span></span>

<span data-ttu-id="52946-112">Üzerinde **dosya** menüsünde **yeni**, ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="52946-112">On the **File** menu,  **New**, then select **Project**.</span></span> <span data-ttu-id="52946-113">Gelen **yüklü**altında **Visual C#** seçin **Windows Masaüstü** seçip **konsol uygulaması (.Net Framework)**.</span><span class="sxs-lookup"><span data-stu-id="52946-113">From **Installed**, under **Visual C#**, select **Windows Desktop** and then select **Console App (.Net Framework)**.</span></span> <span data-ttu-id="52946-114">"OwinSelfhostSample" Projeyi adlandırın ve seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="52946-114">Name the project "OwinSelfhostSample" and select **OK**.</span></span>

[![](use-owin-to-self-host-web-api/_static/image7.png)](use-owin-to-self-host-web-api/_static/image7.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="52946-115">Web API ve OWIN paketleri ekleme</span><span class="sxs-lookup"><span data-stu-id="52946-115">Add the Web API and OWIN packages</span></span>

<span data-ttu-id="52946-116">Gelen **Araçları** menüsünde **NuGet Paket Yöneticisi**, ardından **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="52946-116">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="52946-117">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="52946-117">In the Package Manager Console window, enter the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

<span data-ttu-id="52946-118">Bu Webapı OWIN selfhost paketi ve tüm gerekli OWIN paketlerini yükler.</span><span class="sxs-lookup"><span data-stu-id="52946-118">This will install the WebAPI OWIN selfhost package and all the required OWIN packages.</span></span>

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="52946-119">Web API'sini yapılandırmak için barındırma</span><span class="sxs-lookup"><span data-stu-id="52946-119">Configure Web API for self-host</span></span>

<span data-ttu-id="52946-120">Çözüm Gezgini'nde projeye sağ tıklayıp seçin **Ekle** / **sınıfı** yeni bir sınıf eklemek için.</span><span class="sxs-lookup"><span data-stu-id="52946-120">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="52946-121">Sınıf adını `Startup`.</span><span class="sxs-lookup"><span data-stu-id="52946-121">Name the class `Startup`.</span></span>

![](use-owin-to-self-host-web-api/_static/image5.png)

<span data-ttu-id="52946-122">Tüm bu dosya ortak kodun aşağıdakiyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="52946-122">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="52946-123">Bir Web API denetleyicisi Ekle</span><span class="sxs-lookup"><span data-stu-id="52946-123">Add a Web API controller</span></span>

<span data-ttu-id="52946-124">Ardından, bir Web API denetleyici sınıfı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52946-124">Next, add a Web API controller class.</span></span> <span data-ttu-id="52946-125">Çözüm Gezgini'nde projeye sağ tıklayıp seçin **Ekle** / **sınıfı** yeni bir sınıf eklemek için.</span><span class="sxs-lookup"><span data-stu-id="52946-125">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="52946-126">Sınıf adını `ValuesController`.</span><span class="sxs-lookup"><span data-stu-id="52946-126">Name the class `ValuesController`.</span></span>

<span data-ttu-id="52946-127">Tüm bu dosya ortak kodun aşağıdakiyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="52946-127">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-with-httpclient"></a><span data-ttu-id="52946-128">OWIN konak başlatın ve bir istekte içeren HttpClient</span><span class="sxs-lookup"><span data-stu-id="52946-128">Start the OWIN Host and make a request with HttpClient</span></span>

<span data-ttu-id="52946-129">Tüm ortak kod Program.cs dosyasındaki aşağıdakiyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="52946-129">Replace all of the boilerplate code in the Program.cs file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="run-the-application"></a><span data-ttu-id="52946-130">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="52946-130">Run the application</span></span>

<span data-ttu-id="52946-131">Uygulamayı çalıştırmak için Visual Studio'da F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="52946-131">To run the application, press F5 in Visual Studio.</span></span> <span data-ttu-id="52946-132">Çıktı aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="52946-132">The output should look like the following:</span></span>

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a><span data-ttu-id="52946-133">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="52946-133">Additional resources</span></span>

[<span data-ttu-id="52946-134">Project Katana’ya Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="52946-134">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[<span data-ttu-id="52946-135">Bir Azure çalışan rolünde ASP.NET Web API barındırma</span><span class="sxs-lookup"><span data-stu-id="52946-135">Host ASP.NET Web API in an Azure Worker Role</span></span>](host-aspnet-web-api-in-an-azure-worker-role.md)
