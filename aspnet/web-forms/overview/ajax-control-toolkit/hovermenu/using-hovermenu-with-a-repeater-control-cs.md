---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
title: Repeater denetimiyle HoverMenu kullanma (C#) | Microsoft Docs
author: wenz
description: 'AJAX denetim araç setinde HoverMenu denetimi basit bir açılan efekt sağlar: fare işaretçisi bir öğenin üzerine geldiğinde, bir açılan pencere bir öğe üzerinde görünür...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e7700e7b-edc3-4183-a713-70e507cc7490
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 3e38b91d837c65191d4b3797fa31ef6112a1f070
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606710"
---
# <a name="using-hovermenu-with-a-repeater-control-c"></a><span data-ttu-id="02de0-103">Repeater Denetimiyle HoverMenu Kullanma (C#)</span><span class="sxs-lookup"><span data-stu-id="02de0-103">Using HoverMenu with a Repeater Control (C#)</span></span>

<span data-ttu-id="02de0-104">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="02de0-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="02de0-105">[Kodu indirin](https://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="02de0-105">[Download Code](https://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span></span>

> <span data-ttu-id="02de0-106">AJAX denetim araç setinde HoverMenu denetimi basit bir açılan efekt sağlar: fare işaretçisi bir öğenin üzerine geldiğinde, belirtilen konumda bir açılan pencere görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="02de0-106">The HoverMenu control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="02de0-107">Bu denetimi bir yineleyici içinde kullanmak da mümkündür.</span><span class="sxs-lookup"><span data-stu-id="02de0-107">It is also possible to use this control within a repeater.</span></span>

## <a name="overview"></a><span data-ttu-id="02de0-108">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="02de0-108">Overview</span></span>

<span data-ttu-id="02de0-109">AJAX denetim araç setinde `HoverMenu` denetimi basit bir açılan efekti sağlar: fare işaretçisi bir öğenin üzerine geldiğinde, belirtilen konumda bir açılan pencere görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="02de0-109">The `HoverMenu` control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="02de0-110">Bu denetimi bir yineleyici içinde kullanmak da mümkündür.</span><span class="sxs-lookup"><span data-stu-id="02de0-110">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="02de0-111">Adımlar</span><span class="sxs-lookup"><span data-stu-id="02de0-111">Steps</span></span>

<span data-ttu-id="02de0-112">Birincisi, bir veri kaynağı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="02de0-112">First of all, a data source is required.</span></span> <span data-ttu-id="02de0-113">Bu örnek, AdventureWorks veritabanını ve Microsoft SQL Server 2005 Express sürümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="02de0-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="02de0-114">Veritabanı, Visual Studio yüklemesinin (Express Edition dahil) isteğe bağlı bir parçasıdır ve [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)altında ayrı bir indirme olarak da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="02de0-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="02de0-115">AdventureWorks veritabanı SQL Server 2005 örnek ve örnek veritabanlarının bir parçasıdır ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D ısplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="02de0-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="02de0-116">Veritabanını ayarlamanın en kolay yolu, Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) kullanmaktır ve `AdventureWorks.mdf` veritabanı dosyasını eklemektir.</span><span class="sxs-lookup"><span data-stu-id="02de0-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="02de0-117">Bu örnek için, SQL Server 2005 Express Sürüm örneğinin `SQLEXPRESS` ve Web sunucusuyla aynı makinede yer aldığı varsayılmaktadır; Bu, aynı zamanda varsayılan kurulumdır.</span><span class="sxs-lookup"><span data-stu-id="02de0-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="02de0-118">Kurulumlarınız farklıysa, veritabanının bağlantı bilgilerini uyarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="02de0-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="02de0-119">ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak `<form>` öğesi içinde):</span><span class="sxs-lookup"><span data-stu-id="02de0-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample1.aspx)]

<span data-ttu-id="02de0-120">Ardından, sayfaya bir veri kaynağı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="02de0-120">Then, add a data source to the page.</span></span> <span data-ttu-id="02de0-121">Sınırlı miktarda veri kullanmak için, AdventureWorks veritabanının satıcı tablosunda yalnızca ilk beş girişi seçersiniz.</span><span class="sxs-lookup"><span data-stu-id="02de0-121">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="02de0-122">Veri kaynağını oluşturmak için Visual Studio Yardımcısı 'nı kullanıyorsanız, geçerli sürümdeki bir hatanın `Purchasing`tablo adını (`Vendor`) ön eki olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="02de0-122">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="02de0-123">Aşağıdaki biçimlendirme doğru söz dizimini göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="02de0-123">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample2.aspx)]

<span data-ttu-id="02de0-124">Ardından, kalıcı açılan pencere olarak hizmet veren bir panel ekleyin:</span><span class="sxs-lookup"><span data-stu-id="02de0-124">Next, add a panel which serves as the modal popup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample3.aspx)]

<span data-ttu-id="02de0-125">Artık `HoverMenuExtender` Play 'e geliyor.</span><span class="sxs-lookup"><span data-stu-id="02de0-125">Now, the `HoverMenuExtender` comes into play.</span></span> <span data-ttu-id="02de0-126">Böylece veri kaynağındaki her öğe kendi açılan penceresini alır. Bu, Extender 'ın `<ItemTemplate>` bölümü içine alınmalıdır.</span><span class="sxs-lookup"><span data-stu-id="02de0-126">So that every element in the data source gets its own popup, the extender must be put within the repeater's `<ItemTemplate>` section.</span></span> <span data-ttu-id="02de0-127">Biçimlendirme şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="02de0-127">Here is the markup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample4.aspx)]

<span data-ttu-id="02de0-128">Artık veri kaynağındaki her öğe, 50 milisaniyelik (`PopDelay` özniteliği) gecikmeden sonra sağ tarafta (`PopupPosition` özniteliği) bir açılan pencere görüntüler.</span><span class="sxs-lookup"><span data-stu-id="02de0-128">Now every item in the data source displays a popup to the right (`PopupPosition` attribute) after a delay of 50 milliseconds (`PopDelay` attribute).</span></span>

<span data-ttu-id="02de0-129">[![Repeater 'daki her öğenin yanında bulunan vurgulu menü görüntülenir](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="02de0-129">[![The hover menu appears next to each item in the repeater](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="02de0-130">Yineleyici menü, Repeater 'daki her öğenin yanında görünür ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-hovermenu-with-a-repeater-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="02de0-130">The hover menu appears next to each item in the repeater ([Click to view full-size image](using-hovermenu-with-a-repeater-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="02de0-131">Next</span><span class="sxs-lookup"><span data-stu-id="02de0-131">Next</span></span>](using-hovermenu-with-a-repeater-control-vb.md)
