---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
title: ReorderList aracılığıyla sürükle ve bırak (C#) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde ReorderList denetimi, sürükleme ve bırakma yoluyla kullanıcı tarafından yeniden sıralanabilir bir liste sağlar. Listenin geçerli sırası olacaktır...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6350ee8e-11d6-4aff-b51c-942878014835
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: 2fc6d55a290cbb58bea36d8145d814e337bbd931
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78553832"
---
# <a name="drag-and-drop-via-reorderlist-c"></a><span data-ttu-id="1aefc-104">ReorderList Aracılığıyla Sürükle ve Bırak (C#)</span><span class="sxs-lookup"><span data-stu-id="1aefc-104">Drag and Drop via ReorderList (C#)</span></span>

<span data-ttu-id="1aefc-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="1aefc-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1aefc-106">[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="1aefc-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)</span></span>

> <span data-ttu-id="1aefc-107">AJAX denetim araç setinde ReorderList denetimi, sürükleme ve bırakma yoluyla kullanıcı tarafından yeniden sıralanabilir bir liste sağlar.</span><span class="sxs-lookup"><span data-stu-id="1aefc-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="1aefc-108">Listenin geçerli sırası sunucuda kalıcı hale gelecektir.</span><span class="sxs-lookup"><span data-stu-id="1aefc-108">The current order of the list shall be persisted on the server.</span></span>

## <a name="overview"></a><span data-ttu-id="1aefc-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="1aefc-109">Overview</span></span>

<span data-ttu-id="1aefc-110">AJAX denetim araç setinde `ReorderList` denetimi, Kullanıcı tarafından sürükleme ve bırakma yoluyla yeniden sıralanabilir bir liste sağlar.</span><span class="sxs-lookup"><span data-stu-id="1aefc-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="1aefc-111">Listenin geçerli sırası sunucuda kalıcı hale gelecektir.</span><span class="sxs-lookup"><span data-stu-id="1aefc-111">The current order of the list shall be persisted on the server.</span></span>

## <a name="steps"></a><span data-ttu-id="1aefc-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="1aefc-112">Steps</span></span>

<span data-ttu-id="1aefc-113">`ReorderList` denetim, verileri bir veritabanından listeye bağlamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="1aefc-113">The `ReorderList` control supports binding data from a database to the list.</span></span> <span data-ttu-id="1aefc-114">Ayrıca, liste öğesinin sırasıyla veri deposuna geri değişiklikleri yazmayı de destekler.</span><span class="sxs-lookup"><span data-stu-id="1aefc-114">Best of all, it also supports writing changes to the order of the list element back to the data store.</span></span>

<span data-ttu-id="1aefc-115">Bu örnek, veri deposu olarak Microsoft SQL Server 2005 Express Edition kullanır.</span><span class="sxs-lookup"><span data-stu-id="1aefc-115">This sample uses Microsoft SQL Server 2005 Express Edition as the data store.</span></span> <span data-ttu-id="1aefc-116">Veritabanı, Express Edition da dahil olmak üzere Visual Studio yüklemesinin isteğe bağlı (ve ücretsiz) bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="1aefc-116">The database is an optional (and free) part of a Visual Studio installation, including express edition.</span></span> <span data-ttu-id="1aefc-117">Ayrıca, [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)altında ayrı bir indirme olarak da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1aefc-117">It is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="1aefc-118">Bu örnek için, SQL Server 2005 Express Sürüm örneğinin `SQLEXPRESS` ve Web sunucusuyla aynı makinede yer aldığı varsayılmaktadır; Bu, aynı zamanda varsayılan kurulumdır.</span><span class="sxs-lookup"><span data-stu-id="1aefc-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="1aefc-119">Kurulumlarınız farklıysa, veritabanının bağlantı bilgilerini uyarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1aefc-119">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="1aefc-120">Veritabanını ayarlamanın en kolay yolu, Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ) kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="1aefc-120">The easiest way to set up the database is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span></span> <span data-ttu-id="1aefc-121">Sunucuya bağlanın, `Databases` ' ye çift tıklayın ve yeni bir veritabanı oluşturun (sağ tıklayıp `New Database`' i seçin) `Tutorials`.</span><span class="sxs-lookup"><span data-stu-id="1aefc-121">Connect to the server, double-click on `Databases` and create a new database (right-click and choose `New Database`) called `Tutorials`.</span></span>

<span data-ttu-id="1aefc-122">Bu veritabanında aşağıdaki dört sütun ile `AJAX` adlı yeni bir tablo oluşturun:</span><span class="sxs-lookup"><span data-stu-id="1aefc-122">In this database, create a new table called `AJAX` with the following four columns:</span></span>

- <span data-ttu-id="1aefc-123">`id` (birincil anahtar, tamsayı, kimlik, NULL değil)</span><span class="sxs-lookup"><span data-stu-id="1aefc-123">`id` (primary key, integer, identity, not NULL)</span></span>
- <span data-ttu-id="1aefc-124">`char` (Char (1), NULL)</span><span class="sxs-lookup"><span data-stu-id="1aefc-124">`char` (char(1), NULL)</span></span>
- <span data-ttu-id="1aefc-125">`description` (varchar (50), NULL)</span><span class="sxs-lookup"><span data-stu-id="1aefc-125">`description` (varchar(50), NULL)</span></span>
- <span data-ttu-id="1aefc-126">`position` (int, NULL)</span><span class="sxs-lookup"><span data-stu-id="1aefc-126">`position` (int, NULL)</span></span>

<span data-ttu-id="1aefc-127">[AJAX tablosunun düzenine ![](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1aefc-127">[![The layout of the AJAX table](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)</span></span>

<span data-ttu-id="1aefc-128">AJAX tablosunun düzeni ([tam boyutlu görüntüyü görüntülemek Için tıklayın](drag-and-drop-via-reorderlist-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="1aefc-128">The layout of the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image3.png))</span></span>

<span data-ttu-id="1aefc-129">Daha sonra, tabloyu birkaç değerle doldurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1aefc-129">Next, fill the table with a couple of values.</span></span> <span data-ttu-id="1aefc-130">`position` sütununun öğelerin sıralama düzenini bulundurduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1aefc-130">Note that the `position` column holds the sort order of the elements.</span></span>

<span data-ttu-id="1aefc-131">[AJAX tablosundaki ilk verileri ![](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="1aefc-131">[![The initial data in the AJAX table](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)</span></span>

<span data-ttu-id="1aefc-132">AJAX tablosundaki ilk veriler ([tam boyutlu görüntüyü görüntülemek Için tıklayın](drag-and-drop-via-reorderlist-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="1aefc-132">The initial data in the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image6.png))</span></span>

<span data-ttu-id="1aefc-133">Sonraki adım, yeni veritabanıyla ve tablosuyla iletişim kurmak için bir `SqlDataSource` denetimi oluşturması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1aefc-133">The next step requires to generate an `SqlDataSource` control to communicate with the new database and its table.</span></span> <span data-ttu-id="1aefc-134">Veri kaynağı `SELECT` ve `UPDATE` SQL komutlarını desteklemelidir.</span><span class="sxs-lookup"><span data-stu-id="1aefc-134">The data source must support the `SELECT` and `UPDATE` SQL commands.</span></span> <span data-ttu-id="1aefc-135">Liste öğelerinin sıralaması daha sonra değiştirildiğinde, `ReorderList` denetimi otomatik olarak veri kaynağının `Update` komutuna iki değer gönderir: öğenin yeni konumu ve KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1aefc-135">When the order of the list elements is later changed, the `ReorderList` control automatically submits two values to the data source's `Update` command: the new position and the ID of the element.</span></span> <span data-ttu-id="1aefc-136">Bu nedenle, veri kaynağı bu iki değer için bir `<UpdateParameters>` bölümüne ihtiyaç duyuyor:</span><span class="sxs-lookup"><span data-stu-id="1aefc-136">Therefore, the data source needs an `<UpdateParameters>` section for these two values:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample1.aspx)]

<span data-ttu-id="1aefc-137">`ReorderList` denetiminin aşağıdaki öznitelikleri ayarlaması gerekir:</span><span class="sxs-lookup"><span data-stu-id="1aefc-137">The `ReorderList` control needs to set the following attributes:</span></span>

- <span data-ttu-id="1aefc-138">`AllowReorder`: liste öğelerinin yeniden düzenlenmiş olup olmadığı</span><span class="sxs-lookup"><span data-stu-id="1aefc-138">`AllowReorder`: Whether the list items may be rearranged</span></span>
- <span data-ttu-id="1aefc-139">`DataSourceID`: veri kaynağının KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="1aefc-139">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="1aefc-140">`DataKeyField`: veri kaynağındaki birincil anahtar sütununun adı</span><span class="sxs-lookup"><span data-stu-id="1aefc-140">`DataKeyField`: The name of the primary key column in the data source</span></span>
- <span data-ttu-id="1aefc-141">`SortOrderField`: liste öğeleri için sıralama düzeni sağlayan veri kaynağı sütunu</span><span class="sxs-lookup"><span data-stu-id="1aefc-141">`SortOrderField`: The data source column that provides the sort order for the list items</span></span>

<span data-ttu-id="1aefc-142">`<DragHandleTemplate>` ve `<ItemTemplate>` bölümlerinde, listenin düzeni ince ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="1aefc-142">In the `<DragHandleTemplate>` and `<ItemTemplate>` sections, the layout of the list can be fine-tuned.</span></span> <span data-ttu-id="1aefc-143">Ayrıca, burada görüldüğü gibi `Eval()` yöntemi kullanılarak veri bağlama mümkündür:</span><span class="sxs-lookup"><span data-stu-id="1aefc-143">Also, databinding is possible using the `Eval()` method, as seen here:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample2.aspx)]

<span data-ttu-id="1aefc-144">Aşağıdaki CSS stil bilgileri (`ReorderList` denetiminin `<DragHandleTemplate>` bölümünde başvurulur), fare işaretçisinin sürükleme tutamacının üzerine geldiğinde uygun şekilde değişmesini sağlar:</span><span class="sxs-lookup"><span data-stu-id="1aefc-144">The following CSS style information (referenced in the `<DragHandleTemplate>` section of the `ReorderList` control) makes sure that the mouse pointer changes appropriately when it hovers over the drag handle:</span></span>

[!code-css[Main](drag-and-drop-via-reorderlist-cs/samples/sample3.css)]

<span data-ttu-id="1aefc-145">Son olarak, `ScriptManager` bir denetim sayfa için ASP.NET AJAX 'ı başlatır:</span><span class="sxs-lookup"><span data-stu-id="1aefc-145">Finally, a `ScriptManager` control initializes ASP.NET AJAX for the page:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample4.aspx)]

<span data-ttu-id="1aefc-146">Bu örneği tarayıcıda çalıştırın ve liste öğelerini bir bit olarak yeniden düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="1aefc-146">Run this example in the browser and rearrange the list items a bit.</span></span> <span data-ttu-id="1aefc-147">Sonra, sayfayı yeniden yükleyin ve/veya veritabanına bakın.</span><span class="sxs-lookup"><span data-stu-id="1aefc-147">Then, reload the page and/or have a look at the database.</span></span> <span data-ttu-id="1aefc-148">Değiştirilen konumlar korunur ve ayrıca, yalnızca biçimlendirme kullanarak, veritabanındaki `position` sütununda ve tüm kodlar olmadan bu değerlere yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="1aefc-148">The altered positions have been maintained and are also reflected by the values in the `position` column in the database and that all without any code, just by using markup.</span></span>

<span data-ttu-id="1aefc-149">[veritabanındaki verileri yeni liste öğesi sırasına göre ![](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="1aefc-149">[![The data in the database changes according to the new list item order](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)</span></span>

<span data-ttu-id="1aefc-150">Veritabanındaki veriler yeni liste öğesi sırasına göre değişir ([tam boyutlu görüntüyü görüntülemek Için tıklayın](drag-and-drop-via-reorderlist-cs/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="1aefc-150">The data in the database changes according to the new list item order ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image9.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1aefc-151">[Önceki](using-postbacks-with-reorderlist-cs.md)
> [İleri](using-postbacks-with-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="1aefc-151">[Previous](using-postbacks-with-reorderlist-cs.md)
[Next](using-postbacks-with-reorderlist-vb.md)</span></span>
