---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-vb
title: ReorderList aracılığıyla sürükle ve bırak (VB) | Microsoft Docs
author: wenz
description: /data-access/tutorials/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 848e6bcf-4c3f-4d14-974d-e45b9444ab79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 3f7c5749053d8bf587467fb1939fca05ce2872a4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598699"
---
# <a name="drag-and-drop-via-reorderlist-vb"></a><span data-ttu-id="a345d-103">ReorderList Aracılığıyla Sürükle ve Bırak (VB)</span><span class="sxs-lookup"><span data-stu-id="a345d-103">Drag and Drop via ReorderList (VB)</span></span>

<span data-ttu-id="a345d-104">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="a345d-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a345d-105">[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="a345d-105">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5VB.pdf)</span></span>

> <span data-ttu-id="a345d-106">AJAX denetim araç setinde ReorderList denetimi, sürükleme ve bırakma yoluyla kullanıcı tarafından yeniden sıralanabilir bir liste sağlar.</span><span class="sxs-lookup"><span data-stu-id="a345d-106">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="a345d-107">Listenin geçerli sırası sunucuda kalıcı hale gelecektir.</span><span class="sxs-lookup"><span data-stu-id="a345d-107">The current order of the list shall be persisted on the server.</span></span>

## <a name="overview"></a><span data-ttu-id="a345d-108">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="a345d-108">Overview</span></span>

<span data-ttu-id="a345d-109">AJAX denetim araç setinde `ReorderList` denetimi, Kullanıcı tarafından sürükleme ve bırakma yoluyla yeniden sıralanabilir bir liste sağlar.</span><span class="sxs-lookup"><span data-stu-id="a345d-109">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="a345d-110">Listenin geçerli sırası sunucuda kalıcı hale gelecektir.</span><span class="sxs-lookup"><span data-stu-id="a345d-110">The current order of the list shall be persisted on the server.</span></span>

## <a name="steps"></a><span data-ttu-id="a345d-111">Adımlar</span><span class="sxs-lookup"><span data-stu-id="a345d-111">Steps</span></span>

<span data-ttu-id="a345d-112">`ReorderList` denetim, verileri bir veritabanından listeye bağlamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="a345d-112">The `ReorderList` control supports binding data from a database to the list.</span></span> <span data-ttu-id="a345d-113">Ayrıca, liste öğesinin sırasıyla veri deposuna geri değişiklikleri yazmayı de destekler.</span><span class="sxs-lookup"><span data-stu-id="a345d-113">Best of all, it also supports writing changes to the order of the list element back to the data store.</span></span>

<span data-ttu-id="a345d-114">Bu örnek, veri deposu olarak Microsoft SQL Server 2005 Express Edition kullanır.</span><span class="sxs-lookup"><span data-stu-id="a345d-114">This sample uses Microsoft SQL Server 2005 Express Edition as the data store.</span></span> <span data-ttu-id="a345d-115">Veritabanı, Express Edition da dahil olmak üzere Visual Studio yüklemesinin isteğe bağlı (ve ücretsiz) bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="a345d-115">The database is an optional (and free) part of a Visual Studio installation, including express edition.</span></span> <span data-ttu-id="a345d-116">Ayrıca, [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)altında ayrı bir indirme olarak da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a345d-116">It is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="a345d-117">Bu örnek için, SQL Server 2005 Express Sürüm örneğinin `SQLEXPRESS` ve Web sunucusuyla aynı makinede yer aldığı varsayılmaktadır; Bu, aynı zamanda varsayılan kurulumdır.</span><span class="sxs-lookup"><span data-stu-id="a345d-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="a345d-118">Kurulumlarınız farklıysa, veritabanının bağlantı bilgilerini uyarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a345d-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="a345d-119">Veritabanını ayarlamanın en kolay yolu, Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ) kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="a345d-119">The easiest way to set up the database is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span></span> <span data-ttu-id="a345d-120">Sunucuya bağlanın, `Databases` ' ye çift tıklayın ve yeni bir veritabanı oluşturun (sağ tıklayıp `New Database`' i seçin) `Tutorials`.</span><span class="sxs-lookup"><span data-stu-id="a345d-120">Connect to the server, double-click on `Databases` and create a new database (right-click and choose `New Database`) called `Tutorials`.</span></span>

<span data-ttu-id="a345d-121">Bu veritabanında aşağıdaki dört sütun ile `AJAX` adlı yeni bir tablo oluşturun:</span><span class="sxs-lookup"><span data-stu-id="a345d-121">In this database, create a new table called `AJAX` with the following four columns:</span></span>

- <span data-ttu-id="a345d-122">`id` (birincil anahtar, tamsayı, kimlik, NULL değil)</span><span class="sxs-lookup"><span data-stu-id="a345d-122">`id` (primary key, integer, identity, not NULL)</span></span>
- <span data-ttu-id="a345d-123">`char` (Char (1), NULL)</span><span class="sxs-lookup"><span data-stu-id="a345d-123">`char` (char(1), NULL)</span></span>
- <span data-ttu-id="a345d-124">`description` (varchar (50), NULL)</span><span class="sxs-lookup"><span data-stu-id="a345d-124">`description` (varchar(50), NULL)</span></span>
- <span data-ttu-id="a345d-125">`position` (int, NULL)</span><span class="sxs-lookup"><span data-stu-id="a345d-125">`position` (int, NULL)</span></span>

<span data-ttu-id="a345d-126">[AJAX tablosunun düzenine ![](drag-and-drop-via-reorderlist-vb/_static/image2.png)](drag-and-drop-via-reorderlist-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a345d-126">[![The layout of the AJAX table](drag-and-drop-via-reorderlist-vb/_static/image2.png)](drag-and-drop-via-reorderlist-vb/_static/image1.png)</span></span>

<span data-ttu-id="a345d-127">AJAX tablosunun düzeni ([tam boyutlu görüntüyü görüntülemek Için tıklayın](drag-and-drop-via-reorderlist-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="a345d-127">The layout of the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image3.png))</span></span>

<span data-ttu-id="a345d-128">Daha sonra, tabloyu birkaç değerle doldurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a345d-128">Next, fill the table with a couple of values.</span></span> <span data-ttu-id="a345d-129">`position` sütununun öğelerin sıralama düzenini bulundurduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a345d-129">Note that the `position` column holds the sort order of the elements.</span></span>

<span data-ttu-id="a345d-130">[AJAX tablosundaki ilk verileri ![](drag-and-drop-via-reorderlist-vb/_static/image5.png)](drag-and-drop-via-reorderlist-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="a345d-130">[![The initial data in the AJAX table](drag-and-drop-via-reorderlist-vb/_static/image5.png)](drag-and-drop-via-reorderlist-vb/_static/image4.png)</span></span>

<span data-ttu-id="a345d-131">AJAX tablosundaki ilk veriler ([tam boyutlu görüntüyü görüntülemek Için tıklayın](drag-and-drop-via-reorderlist-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="a345d-131">The initial data in the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image6.png))</span></span>

<span data-ttu-id="a345d-132">Sonraki adım, yeni veritabanıyla ve tablosuyla iletişim kurmak için bir `SqlDataSource` denetimi oluşturması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a345d-132">The next step requires to generate an `SqlDataSource` control to communicate with the new database and its table.</span></span> <span data-ttu-id="a345d-133">Veri kaynağı `SELECT` ve `UPDATE` SQL komutlarını desteklemelidir.</span><span class="sxs-lookup"><span data-stu-id="a345d-133">The data source must support the `SELECT` and `UPDATE` SQL commands.</span></span> <span data-ttu-id="a345d-134">Liste öğelerinin sıralaması daha sonra değiştirildiğinde, `ReorderList` denetimi otomatik olarak veri kaynağının `Update` komutuna iki değer gönderir: öğenin yeni konumu ve KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="a345d-134">When the order of the list elements is later changed, the `ReorderList` control automatically submits two values to the data source's `Update` command: the new position and the ID of the element.</span></span> <span data-ttu-id="a345d-135">Bu nedenle, veri kaynağı bu iki değer için bir `<UpdateParameters>` bölümüne ihtiyaç duyuyor:</span><span class="sxs-lookup"><span data-stu-id="a345d-135">Therefore, the data source needs an `<UpdateParameters>` section for these two values:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample1.aspx)]

<span data-ttu-id="a345d-136">`ReorderList` denetiminin aşağıdaki öznitelikleri ayarlaması gerekir:</span><span class="sxs-lookup"><span data-stu-id="a345d-136">The `ReorderList` control needs to set the following attributes:</span></span>

- <span data-ttu-id="a345d-137">`AllowReorder`: liste öğelerinin yeniden düzenlenmiş olup olmadığı</span><span class="sxs-lookup"><span data-stu-id="a345d-137">`AllowReorder`: Whether the list items may be rearranged</span></span>
- <span data-ttu-id="a345d-138">`DataSourceID`: veri kaynağının KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="a345d-138">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="a345d-139">`DataKeyField`: veri kaynağındaki birincil anahtar sütununun adı</span><span class="sxs-lookup"><span data-stu-id="a345d-139">`DataKeyField`: The name of the primary key column in the data source</span></span>
- <span data-ttu-id="a345d-140">`SortOrderField`: liste öğeleri için sıralama düzeni sağlayan veri kaynağı sütunu</span><span class="sxs-lookup"><span data-stu-id="a345d-140">`SortOrderField`: The data source column that provides the sort order for the list items</span></span>

<span data-ttu-id="a345d-141">`<DragHandleTemplate>` ve `<ItemTemplate>` bölümlerinde, listenin düzeni ince ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="a345d-141">In the `<DragHandleTemplate>` and `<ItemTemplate>` sections, the layout of the list can be fine-tuned.</span></span> <span data-ttu-id="a345d-142">Ayrıca, burada görüldüğü gibi `Eval()` yöntemi kullanılarak veri bağlama mümkündür:</span><span class="sxs-lookup"><span data-stu-id="a345d-142">Also, databinding is possible using the `Eval()` method, as seen here:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample2.aspx)]

<span data-ttu-id="a345d-143">Aşağıdaki CSS stil bilgileri (`ReorderList` denetiminin `<DragHandleTemplate>` bölümünde başvurulur), fare işaretçisinin sürükleme tutamacının üzerine geldiğinde uygun şekilde değişmesini sağlar:</span><span class="sxs-lookup"><span data-stu-id="a345d-143">The following CSS style information (referenced in the `<DragHandleTemplate>` section of the `ReorderList` control) makes sure that the mouse pointer changes appropriately when it hovers over the drag handle:</span></span>

[!code-css[Main](drag-and-drop-via-reorderlist-vb/samples/sample3.css)]

<span data-ttu-id="a345d-144">Son olarak, `ScriptManager` bir denetim sayfa için ASP.NET AJAX 'ı başlatır:</span><span class="sxs-lookup"><span data-stu-id="a345d-144">Finally, a `ScriptManager` control initializes ASP.NET AJAX for the page:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample4.aspx)]

<span data-ttu-id="a345d-145">Bu örneği tarayıcıda çalıştırın ve liste öğelerini bir bit olarak yeniden düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="a345d-145">Run this example in the browser and rearrange the list items a bit.</span></span> <span data-ttu-id="a345d-146">Sonra, sayfayı yeniden yükleyin ve/veya veritabanına bakın.</span><span class="sxs-lookup"><span data-stu-id="a345d-146">Then, reload the page and/or have a look at the database.</span></span> <span data-ttu-id="a345d-147">Değiştirilen konumlar korunur ve ayrıca, yalnızca biçimlendirme kullanarak, veritabanındaki `position` sütununda ve tüm kodlar olmadan bu değerlere yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="a345d-147">The altered positions have been maintained and are also reflected by the values in the `position` column in the database and that all without any code, just by using markup.</span></span>

<span data-ttu-id="a345d-148">[veritabanındaki verileri yeni liste öğesi sırasına göre ![](drag-and-drop-via-reorderlist-vb/_static/image8.png)](drag-and-drop-via-reorderlist-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="a345d-148">[![The data in the database changes according to the new list item order](drag-and-drop-via-reorderlist-vb/_static/image8.png)](drag-and-drop-via-reorderlist-vb/_static/image7.png)</span></span>

<span data-ttu-id="a345d-149">Veritabanındaki veriler yeni liste öğesi sırasına göre değişir ([tam boyutlu görüntüyü görüntülemek Için tıklayın](drag-and-drop-via-reorderlist-vb/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="a345d-149">The data in the database changes according to the new list item order ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image9.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a345d-150">Öncekini</span><span class="sxs-lookup"><span data-stu-id="a345d-150">Previous</span></span>](using-postbacks-with-reorderlist-vb.md)
