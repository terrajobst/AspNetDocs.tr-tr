---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: OWıN kullanarak Self-Host ASP.NET Web API-ASP.NET 4. x
author: rick-anderson
description: Konsol uygulamasında ASP.NET Web API 'sinin nasıl barındıralınacağını gösteren kod ile öğretici.
ms.author: riande
ms.date: 07/09/2013
ms.custom: seoapril2019
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: 872b931391a63ef82b96e5b264c070c0b5e9605d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556541"
---
# <a name="use-owin-to-self-host-aspnet-web-api"></a><span data-ttu-id="b4d65-103">OWıN kullanarak Self-Host ASP.NET Web API 'SI</span><span class="sxs-lookup"><span data-stu-id="b4d65-103">Use OWIN to Self-Host ASP.NET Web API</span></span> 

> <span data-ttu-id="b4d65-104">Bu öğreticide, Web API çerçevesini Self barındırmak için OWIN kullanarak bir konsol uygulamasında ASP.NET Web API 'sinin nasıl barındıralınacağını gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b4d65-104">This tutorial shows how to host ASP.NET Web API in a console application, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="b4d65-105">[.Net Için açık Web arabirimi](http://owin.org) (owın), .NET Web sunucuları ile Web uygulamaları arasında bir soyutlama tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b4d65-105">[Open Web Interface for .NET](http://owin.org) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="b4d65-106">OWIN, Web uygulamasını sunucusundan ayırır, bu da bir Web uygulamasını kendi işleminizde IIS dışında bir Web uygulaması barındırmak için ideal hale getirir.</span><span class="sxs-lookup"><span data-stu-id="b4d65-106">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="b4d65-107">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="b4d65-107">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="b4d65-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="b4d65-108">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/) 
> - <span data-ttu-id="b4d65-109">Web API 5.2.7</span><span class="sxs-lookup"><span data-stu-id="b4d65-109">Web API 5.2.7</span></span>

> [!NOTE]
> <span data-ttu-id="b4d65-110">Bu öğreticinin tüm kaynak kodunu [GitHub.com/ASPNET/Samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample)adresinden bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4d65-110">You can find the complete source code for this tutorial at [github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample).</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="b4d65-111">Konsol uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="b4d65-111">Create a console application</span></span>

<span data-ttu-id="b4d65-112">**Dosya** menüsünde **Yeni**' ye ve ardından **Proje**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="b4d65-112">On the **File** menu,  **New**, then select **Project**.</span></span> <span data-ttu-id="b4d65-113">**Yüklü**, **Visual C#** altında, **Windows Masaüstü** ' nü seçin ve **konsol uygulaması (.NET Framework)** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="b4d65-113">From **Installed**, under **Visual C#**, select **Windows Desktop** and then select **Console App (.Net Framework)**.</span></span> <span data-ttu-id="b4d65-114">Projeyi "Owınselfhostsample" olarak adlandırın ve **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b4d65-114">Name the project "OwinSelfhostSample" and select **OK**.</span></span>

[![](use-owin-to-self-host-web-api/_static/image7.png)](use-owin-to-self-host-web-api/_static/image7.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="b4d65-115">Web API 'sini ve OWIN paketlerini ekleyin</span><span class="sxs-lookup"><span data-stu-id="b4d65-115">Add the Web API and OWIN packages</span></span>

<span data-ttu-id="b4d65-116">**Araçlar** menüsünde **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="b4d65-116">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="b4d65-117">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="b4d65-117">In the Package Manager Console window, enter the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

<span data-ttu-id="b4d65-118">Bu işlem, WebAPI OWıN Selfhost paketini ve tüm gerekli OWIN paketlerini yükler.</span><span class="sxs-lookup"><span data-stu-id="b4d65-118">This will install the WebAPI OWIN selfhost package and all the required OWIN packages.</span></span>

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="b4d65-119">Self-Host için Web API 'YI yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b4d65-119">Configure Web API for self-host</span></span>

<span data-ttu-id="b4d65-120">Çözüm Gezgini, projeye sağ tıklayın ve yeni bir sınıf eklemek için / **sınıfı** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="b4d65-120">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="b4d65-121">`Startup`sınıfı adlandırın.</span><span class="sxs-lookup"><span data-stu-id="b4d65-121">Name the class `Startup`.</span></span>

![](use-owin-to-self-host-web-api/_static/image5.png)

<span data-ttu-id="b4d65-122">Bu dosyadaki tüm ortak kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b4d65-122">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="b4d65-123">Web API denetleyicisi ekleme</span><span class="sxs-lookup"><span data-stu-id="b4d65-123">Add a Web API controller</span></span>

<span data-ttu-id="b4d65-124">Sonra, bir Web API denetleyici sınıfı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b4d65-124">Next, add a Web API controller class.</span></span> <span data-ttu-id="b4d65-125">Çözüm Gezgini, projeye sağ tıklayın ve yeni bir sınıf eklemek için / **sınıfı** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="b4d65-125">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="b4d65-126">`ValuesController`sınıfı adlandırın.</span><span class="sxs-lookup"><span data-stu-id="b4d65-126">Name the class `ValuesController`.</span></span>

<span data-ttu-id="b4d65-127">Bu dosyadaki tüm ortak kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b4d65-127">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-with-httpclient"></a><span data-ttu-id="b4d65-128">OWıN konağını başlatın ve HttpClient ile bir istek yapın</span><span class="sxs-lookup"><span data-stu-id="b4d65-128">Start the OWIN Host and make a request with HttpClient</span></span>

<span data-ttu-id="b4d65-129">Program.cs dosyasındaki tüm ortak kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b4d65-129">Replace all of the boilerplate code in the Program.cs file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="run-the-application"></a><span data-ttu-id="b4d65-130">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b4d65-130">Run the application</span></span>

<span data-ttu-id="b4d65-131">Uygulamayı çalıştırmak için, Visual Studio 'da F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="b4d65-131">To run the application, press F5 in Visual Studio.</span></span> <span data-ttu-id="b4d65-132">Çıktı aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="b4d65-132">The output should look like the following:</span></span>

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a><span data-ttu-id="b4d65-133">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b4d65-133">Additional resources</span></span>

[<span data-ttu-id="b4d65-134">Project Katana’ya Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b4d65-134">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[<span data-ttu-id="b4d65-135">Azure çalışan rolünde konak ASP.NET Web API 'SI</span><span class="sxs-lookup"><span data-stu-id="b4d65-135">Host ASP.NET Web API in an Azure Worker Role</span></span>](host-aspnet-web-api-in-an-azure-worker-role.md)
