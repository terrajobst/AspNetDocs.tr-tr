---
uid: whitepapers/aspnet-mvc2-upgrade-notes
title: ASP.NET MVC 1,0 uygulamasını ASP.NET MVC 2 ' ye yükseltme | Microsoft Docs
author: rick-anderson
description: Bu belgede hem el ile yükseltme hem de bir sihirbaz ile ASP.NET MVC 1,0 uygulaması ile ASP.NET MVC 2 açıklanır. Bu belge d... için de kullanılabilir.
ms.author: riande
ms.date: 04/08/2010
ms.assetid: f1a01759-d251-4b09-8835-e112e336c6dd
msc.legacyurl: /whitepapers/aspnet-mvc2-upgrade-notes
msc.type: content
ms.openlocfilehash: 27589f1b1c9d5038118e5ff0cc2e7cecae17d5ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637020"
---
# <a name="upgrading-an-aspnet-mvc-10-application-to-aspnet-mvc-2"></a><span data-ttu-id="22edd-104">Bir ASP.NET MVC 1.0 Uygulamasını ASP.NET MVC 2 Sürümüne Yükseltme</span><span class="sxs-lookup"><span data-stu-id="22edd-104">Upgrading an ASP.NET MVC 1.0 Application to ASP.NET MVC 2</span></span>

> <span data-ttu-id="22edd-105">Bu belgede hem el ile yükseltme hem de bir sihirbaz ile ASP.NET MVC 1,0 uygulaması ile ASP.NET MVC 2 açıklanır.</span><span class="sxs-lookup"><span data-stu-id="22edd-105">This document describes both how to upgrade manually and with a wizard an ASP.NET MVC 1.0 Application to ASP.NET MVC 2.</span></span> <span data-ttu-id="22edd-106">Bu belge [Indirileceği](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/MVC2-Upgrade-Notes.pdf) için de kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="22edd-106">This document is also available for [Download](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/MVC2-Upgrade-Notes.pdf)</span></span>

## <a name="introduction"></a><span data-ttu-id="22edd-107">Giriş</span><span class="sxs-lookup"><span data-stu-id="22edd-107">Introduction</span></span>

<span data-ttu-id="22edd-108">ASP.NET MVC 2 aynı sunucuda ASP.NET MVC 1,0 ile yan yana yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="22edd-108">ASP.NET MVC 2 can be installed side by side with ASP.NET MVC 1.0 on the same server.</span></span> <span data-ttu-id="22edd-109">Bu, ASP.NET MVC 1,0 uygulamasının ASP.NET MVC 2 ' ye ne zaman yükseltileceğini seçerken uygulama geliştiricileri esnekliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="22edd-109">This gives application developers flexibility in choosing when to upgrade an ASP.NET MVC 1.0 application to ASP.NET MVC 2.</span></span>

<span data-ttu-id="22edd-110">Visual Studio 2010, Visual Studio 2008 ile oluşturulan mevcut ASP.NET MVC 1,0 projelerini ASP.NET MVC 2 ' ye yükselten bir sihirbaz içerir.</span><span class="sxs-lookup"><span data-stu-id="22edd-110">Visual Studio 2010 includes a wizard that upgrades existing ASP.NET MVC 1.0 projects built with Visual Studio 2008 to ASP.NET MVC 2.</span></span> <span data-ttu-id="22edd-111">Yükseltme Sihirbazı, Visual Studio 2010 ' de bir ASP.NET MVC 1,0 projesi açılarak başlatılır.</span><span class="sxs-lookup"><span data-stu-id="22edd-111">The upgrade wizard is initiated by opening an ASP.NET MVC 1.0 project in Visual Studio 2010.</span></span>

## <a name="upgrade-wizard-for-aspnet-mvc-10-on-visual-studio-2008-sp1"></a><span data-ttu-id="22edd-112">Visual Studio 2008 SP1 üzerinde ASP.NET MVC 1,0 için Yükseltme Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="22edd-112">Upgrade Wizard for ASP.NET MVC 1.0 on Visual Studio 2008 SP1</span></span>

<span data-ttu-id="22edd-113">ASP.NET MVC 1,0 uygulamasını Visual Studio 2008 SP1 'de ASP.NET MVC 2 ' ye yükseltmek için (desteklenmeyen) MvcAppConverter uygulamasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="22edd-113">To upgrade an ASP.NET MVC 1.0 application to ASP.NET MVC 2 in Visual Studio 2008 SP1, use the (unsupported) MvcAppConverter application.</span></span> <span data-ttu-id="22edd-114">Bu uygulamayı Şu URL 'den indirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="22edd-114">You can download this application from the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=185351](https://go.microsoft.com/fwlink/?LinkID=185351)

## <a name="manually-upgrading-an-aspnet-mvc-10-project"></a><span data-ttu-id="22edd-115">ASP.NET MVC 1,0 projesini el ile yükseltme</span><span class="sxs-lookup"><span data-stu-id="22edd-115">Manually Upgrading an ASP.NET MVC 1.0 Project</span></span>

<span data-ttu-id="22edd-116">Mevcut bir ASP.NET MVC 1,0 uygulamasını sürüm 2 ' ye el ile yükseltmek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="22edd-116">To manually upgrade an existing ASP.NET MVC 1.0 application to version 2, follow these steps:</span></span>

1. <span data-ttu-id="22edd-117">Mevcut projenin yedeğini alın.</span><span class="sxs-lookup"><span data-stu-id="22edd-117">Make a backup of the existing project.</span></span>
2. <span data-ttu-id="22edd-118">Bir metin düzenleyicisinde, proje dosyasını (. csproj veya. vbproj dosyası uzantılı dosya) açın ve ProjectTypeGuid öğesini bulun.</span><span class="sxs-lookup"><span data-stu-id="22edd-118">In a text editor, open the project file (the file with the .csproj or .vbproj file extension) and find the ProjectTypeGuid element.</span></span> <span data-ttu-id="22edd-119">Bu öğenin değeri olarak, {603c0e0b-db56-11dc-be95-000d561079b0} DEĞERINI {F85E285D-A4E0-4152-9332-AB1D724D3325} ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="22edd-119">As the value of that element, replace the GUID {603c0e0b-db56-11dc-be95-000d561079b0} with {F85E285D-A4E0-4152-9332-AB1D724D3325}.</span></span> <span data-ttu-id="22edd-120">İşiniz bittiğinde, bu öğenin değeri şu şekilde olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="22edd-120">When you are done, the value of that element should be as follows:</span></span> 

    `{F85E285D-A4E0-4152-9332-AB1D724D3325};{349c5851-65df-11da-9384-00065b846f21};{fae04ec0-301f-11d3-bf4b-00c04f79efbc}`
3. <span data-ttu-id="22edd-121">Web uygulaması kök klasöründe, Web. config dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="22edd-121">In the Web application root folder, edit the Web.config file.</span></span> <span data-ttu-id="22edd-122">System. Web. Mvc, Version = 1.0.0.0 araması yapın ve tüm örnekleri System. Web. Mvc, Version = 2.0.0.0 ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="22edd-122">Search for System.Web.Mvc, Version=1.0.0.0 and replace all instances with System.Web.Mvc, Version=2.0.0.0.</span></span>
4. <span data-ttu-id="22edd-123">Görünümler klasöründe bulunan Web. config dosyası için önceki adımı yineleyin.</span><span class="sxs-lookup"><span data-stu-id="22edd-123">Repeat the previous step for the Web.config file located in the Views folder.</span></span>
5. <span data-ttu-id="22edd-124">Visual Studio 'Yu kullanarak projeyi açın ve **Çözüm Gezgini**' de **Başvurular** düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="22edd-124">Open the project using Visual Studio, and in **Solution Explorer**, expand the **References** node.</span></span> <span data-ttu-id="22edd-125">System. Web. Mvc başvurusunu silin (sürüm 1,0 derlemesini işaret eder).</span><span class="sxs-lookup"><span data-stu-id="22edd-125">Delete the reference to System.Web.Mvc (which points to the version 1.0 assembly).</span></span> <span data-ttu-id="22edd-126">System. Web. Mvc (v 2.0.0.0) öğesine bir başvuru ekleyin.</span><span class="sxs-lookup"><span data-stu-id="22edd-126">Add a reference to System.Web.Mvc (v2.0.0.0).</span></span>
6. <span data-ttu-id="22edd-127">Aşağıdaki bindingRedirect öğesini yapılandırma bölümünün altındaki uygulama kökündeki Web. config dosyasına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="22edd-127">Add the following bindingRedirect element to the Web.config file in the application root under the configuraton section:</span></span>   

    [!code-xml[Main](aspnet-mvc2-upgrade-notes/samples/sample1.xml)]
7. <span data-ttu-id="22edd-128">Yeni boş bir ASP.NET MVC 2 uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="22edd-128">Create a new empty ASP.NET MVC 2 application.</span></span> <span data-ttu-id="22edd-129">Dosyaları yeni uygulamanın betikler klasöründen mevcut uygulamanın betikler klasörüne kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="22edd-129">Copy the files from the Scripts folder of the new application into the Scripts folder of the existing application.</span></span>
8. <span data-ttu-id="22edd-130">Mevcut applicationâ €™ s CSS dosyasını, site. CSS dosyasındaki CSS stili tanımlarıyla güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="22edd-130">Update the existing applicationâ€™s CSS file with the CSS style definitions in the Site.css file.</span></span>
9. <span data-ttu-id="22edd-131">Uygulamayı derleyin ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="22edd-131">Compile the application and run it.</span></span> <span data-ttu-id="22edd-132">Herhangi bir hata oluşursa, [ASP.NET MVC 2 ' deki](https://go.microsoft.com/fwlink/?LinkID=185038) yenilikler sayfasındaki son değişiklikler bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="22edd-132">If any errors occur, refer to the Breaking Changes section of the [What's New in ASP.NET MVC 2](https://go.microsoft.com/fwlink/?LinkID=185038) page.</span></span>
