---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
title: EF 5 MVC 4 öğreticileri için bölüm Indirmeleri oluşturma | Microsoft Docs
author: Rick-Anderson
description: Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: d0a89089-eed8-4f61-a478-c5ffa30186f5
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
msc.type: authoredcontent
ms.openlocfilehash: 0e720b3e4c5d3b8f779afe3a6e2b47baa86eec4c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74592701"
---
# <a name="building-the-chapter-downloads-for-the-ef-5-mvc-4-tutorials"></a><span data-ttu-id="69546-103">EF 5 MVC 4 öğreticileri için bölüm Indirmeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="69546-103">Building the Chapter Downloads for the EF 5 MVC 4 Tutorials</span></span>

<span data-ttu-id="69546-104">[Rick Anderson]((https://twitter.com/RickAndMSFT)) tarafından</span><span class="sxs-lookup"><span data-stu-id="69546-104">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

[<span data-ttu-id="69546-105">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="69546-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="69546-106">Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio 2012 kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="69546-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="69546-107">Öğretici serisi hakkında daha fazla bilgi için, [serideki ilk öğreticiye](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="69546-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

## <a name="building-the-chapter-downloads"></a><span data-ttu-id="69546-108">Bölüm İndirmeleri Oluşturma</span><span class="sxs-lookup"><span data-stu-id="69546-108">Building the Chapter Downloads</span></span>

1. <span data-ttu-id="69546-109">Proje örnek ZIP dosyasını indirip sıkıştırmasını açın.</span><span class="sxs-lookup"><span data-stu-id="69546-109">Download and unzip the  project sample zip file.</span></span> <span data-ttu-id="69546-110">Sıkıştırılmış indirme paketinde, her bölümün tamamlanması için bir tane olmak üzere ek ZIP dosyaları bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="69546-110">In the unzipped download package, you will find additional zip files, one for the completion of each chapter.</span></span>
2. <span data-ttu-id="69546-111">İstenen ZIP dosyasına sağ tıklayın, **Özellikler**' e tıklayın ve **Engellemeyi kaldır** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="69546-111">Right click on the desired zip file, click **Properties**, and click the **Unblock** button.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image1.png)
3. <span data-ttu-id="69546-112">Dosyayı sıkıştırmayı açın.</span><span class="sxs-lookup"><span data-stu-id="69546-112">Unzip the file.</span></span>
4. <span data-ttu-id="69546-113">Visual Studio 'Yu başlatmak için *cux. sln* dosyasına çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="69546-113">Double-click the *CUx.sln* file to launch Visual Studio.</span></span>
5. <span data-ttu-id="69546-114">**Araçlar** menüsünde, **NuGet Paket Yöneticisi**' ne ve ardından **Paket Yöneticisi konsolu**' na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="69546-114">From the **Tools** menu, click **NuGet Package Manager**, then **Package Manager Console**.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image2.png)
6. <span data-ttu-id="69546-115">Paket Yöneticisi konsolunda (PMC) **geri yükle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="69546-115">In the Package Manager Console (PMC), click **Restore**.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image3.png)
7. <span data-ttu-id="69546-116">Visual Studio 'dan çıkın.</span><span class="sxs-lookup"><span data-stu-id="69546-116">Exit Visual Studio.</span></span>
8. <span data-ttu-id="69546-117">Yukarıdaki adımda kapattığınız çözüm dosyasını açarak Visual Studio 'Yu yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="69546-117">Restart Visual Studio, opening the solution file you closed in the step above.</span></span>
9. <span data-ttu-id="69546-118">Paket Yöneticisi konsolunda (PMC) `Update-Database` komutunu girin:</span><span class="sxs-lookup"><span data-stu-id="69546-118">In the Package Manager Console (PMC), enter the `Update-Database` command:</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image4.png)  

    > [!NOTE]
    > <span data-ttu-id="69546-119">Aşağıdaki hatayı alırsanız:</span><span class="sxs-lookup"><span data-stu-id="69546-119">If you get the following error:</span></span>  
    >   
    >  <span data-ttu-id="69546-120">*' Update-Database ' terimi bir cmdlet, işlev, betik dosyası veya çalıştırılabilir programının adı olarak tanınmıyor. Adın yazımını denetleyin veya bir yol içerilip yolun doğru olduğundan emin olun ve yeniden deneyin.*</span><span class="sxs-lookup"><span data-stu-id="69546-120">*The term 'Update-Database' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.*</span></span>  
    > <span data-ttu-id="69546-121">Çıkın ve Visual Studio 'Yu yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="69546-121">Exit and restart Visual Studio.</span></span>

    <span data-ttu-id="69546-122">Her geçiş çalışır ve ardından çekirdek yöntemi çalışacaktır.</span><span class="sxs-lookup"><span data-stu-id="69546-122">Each migration will run, then the seed method will run.</span></span> <span data-ttu-id="69546-123">Artık uygulamayı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69546-123">You can now run the app.</span></span>

    ![](building-the-ef5-mvc4-chapter-downloads/_static/image5.png)

> [!div class="step-by-step"]
> [<span data-ttu-id="69546-124">Öncekini</span><span class="sxs-lookup"><span data-stu-id="69546-124">Previous</span></span>](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
