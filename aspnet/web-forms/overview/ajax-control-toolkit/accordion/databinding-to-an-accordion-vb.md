---
uid: web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
title: Bir Accordion 'a veri bağlama (VB) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde bulunan Accordion denetimi birden çok bölme sağlar ve kullanıcının her seferinde birini görüntülemesini sağlar. Panolar genellikle w olarak bildiriliyor...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b19f0875-7d3e-4ecf-baa1-a0c693c765b3
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
msc.type: authoredcontent
ms.openlocfilehash: bfb31940c0395c7ed1d5d471fb8fb686b66c59ad
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614522"
---
# <a name="databinding-to-an-accordion-vb"></a><span data-ttu-id="996b3-104">Bir Accordion’a Veri Bağlama (VB)</span><span class="sxs-lookup"><span data-stu-id="996b3-104">Databinding to an Accordion (VB)</span></span>

<span data-ttu-id="996b3-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="996b3-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="996b3-106">[Kodu indirin](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="996b3-106">[Download Code](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1VB.pdf)</span></span>

> <span data-ttu-id="996b3-107">AJAX denetim araç setinde bulunan Accordion denetimi birden çok bölme sağlar ve kullanıcının her seferinde birini görüntülemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="996b3-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="996b3-108">Panolar genellikle sayfanın kendisi içinde gösterilir, ancak bir veri kaynağına bağlama daha fazla esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="996b3-108">Panels are usually declared within the page itself, but binding to a data source offers more flexibility.</span></span>

## <a name="overview"></a><span data-ttu-id="996b3-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="996b3-109">Overview</span></span>

<span data-ttu-id="996b3-110">AJAX denetim araç setinde bulunan Accordion denetimi birden çok bölme sağlar ve kullanıcının her seferinde birini görüntülemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="996b3-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="996b3-111">Panolar genellikle sayfanın kendisi içinde gösterilir, ancak bir veri kaynağına bağlama daha fazla esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="996b3-111">Panels are usually declared within the page itself, but binding to a data source offers more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="996b3-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="996b3-112">Steps</span></span>

<span data-ttu-id="996b3-113">Birincisi, bir veri kaynağı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="996b3-113">First of all, a data source is required.</span></span> <span data-ttu-id="996b3-114">Bu örnek, AdventureWorks veritabanını ve Microsoft SQL Server 2005 Express sürümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="996b3-114">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="996b3-115">Veritabanı, Visual Studio yüklemesinin (Express Edition dahil) isteğe bağlı bir parçasıdır ve [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)altında ayrı bir indirme olarak da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="996b3-115">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="996b3-116">AdventureWorks veritabanı SQL Server 2005 örnek ve örnek veritabanlarının bir parçasıdır ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D ısplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="996b3-116">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="996b3-117">Veritabanını ayarlamanın en kolay yolu, Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) kullanmaktır ve `AdventureWorks.mdf` veritabanı dosyasını eklemektir.</span><span class="sxs-lookup"><span data-stu-id="996b3-117">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="996b3-118">Bu örnek için, SQL Server 2005 Express Sürüm örneğinin `SQLEXPRESS` ve Web sunucusuyla aynı makinede yer aldığı varsayılmaktadır; Bu, aynı zamanda varsayılan kurulumdır.</span><span class="sxs-lookup"><span data-stu-id="996b3-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="996b3-119">Kurulumlarınız farklıysa, veritabanının bağlantı bilgilerini uyarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="996b3-119">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="996b3-120">ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak `<form>` öğesi içinde):</span><span class="sxs-lookup"><span data-stu-id="996b3-120">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample1.aspx)]

<span data-ttu-id="996b3-121">Ardından, sayfaya bir veri kaynağı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="996b3-121">Then, add a data source to the page.</span></span> <span data-ttu-id="996b3-122">Sınırlı miktarda veri kullanmak için, AdventureWorks veritabanının satıcı tablosunda yalnızca ilk beş girişi seçersiniz.</span><span class="sxs-lookup"><span data-stu-id="996b3-122">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="996b3-123">Veri kaynağını oluşturmak için Visual Studio Yardımcısı 'nı kullanıyorsanız, geçerli sürümdeki bir hatanın `Purchasing`tablo adını (`Vendor`) ön eki olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="996b3-123">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="996b3-124">Aşağıdaki biçimlendirme doğru söz dizimini göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="996b3-124">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample2.aspx)]

<span data-ttu-id="996b3-125">Veri kaynağının adını (ID) unutmayın.</span><span class="sxs-lookup"><span data-stu-id="996b3-125">Remember the name (ID) of the data source.</span></span> <span data-ttu-id="996b3-126">Bu çok tanımlayıcı daha sonra Accordion denetiminin `DataSourceID` özelliğinde kullanılmalıdır:</span><span class="sxs-lookup"><span data-stu-id="996b3-126">This very identification must then be used in the `DataSourceID` property of the Accordion control:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample3.aspx)]

<span data-ttu-id="996b3-127">Accordion denetimi içinde, üst bilgi (`<HeaderTemplate>`) ve içerik (`<ContentTemplate>`) dahil olmak üzere, denetimin çeşitli bölümlerine yönelik şablonlar sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="996b3-127">Within the Accordion control, you can provide templates for various parts of the control, including the header (`<HeaderTemplate>`) and the content (`<ContentTemplate>`).</span></span> <span data-ttu-id="996b3-128">Bu öğeler içinde, `DataBinder.Eval()` yöntemi kullanarak verileri veri kaynağından çıkış yapmanız yeterlidir:</span><span class="sxs-lookup"><span data-stu-id="996b3-128">Within these elements, just output the data from the data source, using the `DataBinder.Eval()` method:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample4.aspx)]

<span data-ttu-id="996b3-129">Sayfa yüklendiğinde, veri kaynağının bu sunucu tarafı koduyla Accordion 'e bağlanması gerekir:</span><span class="sxs-lookup"><span data-stu-id="996b3-129">When the page is loaded, the data source must be bound to the accordion with this server-side code:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample5.aspx)]

<span data-ttu-id="996b3-130">Bu örneği sonuçlandırma için, Accordion denetiminde (özelliklerinde `HeaderCssClass` ve `ContentCssClass`) başvurulan iki CSS sınıfını tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="996b3-130">To conclude this sample, you need to define the two CSS classes that are referenced in the Accordion control (in its properties `HeaderCssClass` and `ContentCssClass`).</span></span> <span data-ttu-id="996b3-131">Aşağıdaki biçimlendirmeyi sayfanın `<head>` bölümüne koyun:</span><span class="sxs-lookup"><span data-stu-id="996b3-131">Put the following markup in the `<head>` section of the page:</span></span>

[!code-css[Main](databinding-to-an-accordion-vb/samples/sample6.css)]

<span data-ttu-id="996b3-132">[Accordion içindeki verilerin ![doğrudan veri kaynağından gelir](databinding-to-an-accordion-vb/_static/image2.png)](databinding-to-an-accordion-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="996b3-132">[![The data in the accordion comes directly from the data source](databinding-to-an-accordion-vb/_static/image2.png)](databinding-to-an-accordion-vb/_static/image1.png)</span></span>

<span data-ttu-id="996b3-133">Accordion içindeki veriler doğrudan veri kaynağından gelir ([tam boyutlu görüntüyü görüntülemek Için tıklatın](databinding-to-an-accordion-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="996b3-133">The data in the accordion comes directly from the data source ([Click to view full-size image](databinding-to-an-accordion-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="996b3-134">[Önceki](dynamically-adding-an-accordion-pane-cs.md)
> [İleri](dynamically-adding-an-accordion-pane-vb.md)</span><span class="sxs-lookup"><span data-stu-id="996b3-134">[Previous](dynamically-adding-an-accordion-pane-cs.md)
[Next](dynamically-adding-an-accordion-pane-vb.md)</span></span>
