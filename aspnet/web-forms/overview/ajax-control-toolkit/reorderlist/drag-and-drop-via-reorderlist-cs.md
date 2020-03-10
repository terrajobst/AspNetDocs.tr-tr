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
# <a name="drag-and-drop-via-reorderlist-c"></a>ReorderList Aracılığıyla Sürükle ve Bırak (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)

> AJAX denetim araç setinde ReorderList denetimi, sürükleme ve bırakma yoluyla kullanıcı tarafından yeniden sıralanabilir bir liste sağlar. Listenin geçerli sırası sunucuda kalıcı hale gelecektir.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde `ReorderList` denetimi, Kullanıcı tarafından sürükleme ve bırakma yoluyla yeniden sıralanabilir bir liste sağlar. Listenin geçerli sırası sunucuda kalıcı hale gelecektir.

## <a name="steps"></a>Adımlar

`ReorderList` denetim, verileri bir veritabanından listeye bağlamayı destekler. Ayrıca, liste öğesinin sırasıyla veri deposuna geri değişiklikleri yazmayı de destekler.

Bu örnek, veri deposu olarak Microsoft SQL Server 2005 Express Edition kullanır. Veritabanı, Express Edition da dahil olmak üzere Visual Studio yüklemesinin isteğe bağlı (ve ücretsiz) bir parçasıdır. Ayrıca, [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)altında ayrı bir indirme olarak da kullanılabilir. Bu örnek için, SQL Server 2005 Express Sürüm örneğinin `SQLEXPRESS` ve Web sunucusuyla aynı makinede yer aldığı varsayılmaktadır; Bu, aynı zamanda varsayılan kurulumdır. Kurulumlarınız farklıysa, veritabanının bağlantı bilgilerini uyarlamanız gerekir.

Veritabanını ayarlamanın en kolay yolu, Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ) kullanmaktır. Sunucuya bağlanın, `Databases` ' ye çift tıklayın ve yeni bir veritabanı oluşturun (sağ tıklayıp `New Database`' i seçin) `Tutorials`.

Bu veritabanında aşağıdaki dört sütun ile `AJAX` adlı yeni bir tablo oluşturun:

- `id` (birincil anahtar, tamsayı, kimlik, NULL değil)
- `char` (Char (1), NULL)
- `description` (varchar (50), NULL)
- `position` (int, NULL)

[AJAX tablosunun düzenine ![](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)

AJAX tablosunun düzeni ([tam boyutlu görüntüyü görüntülemek Için tıklayın](drag-and-drop-via-reorderlist-cs/_static/image3.png))

Daha sonra, tabloyu birkaç değerle doldurmanız gerekir. `position` sütununun öğelerin sıralama düzenini bulundurduğunu unutmayın.

[AJAX tablosundaki ilk verileri ![](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)

AJAX tablosundaki ilk veriler ([tam boyutlu görüntüyü görüntülemek Için tıklayın](drag-and-drop-via-reorderlist-cs/_static/image6.png))

Sonraki adım, yeni veritabanıyla ve tablosuyla iletişim kurmak için bir `SqlDataSource` denetimi oluşturması gerekir. Veri kaynağı `SELECT` ve `UPDATE` SQL komutlarını desteklemelidir. Liste öğelerinin sıralaması daha sonra değiştirildiğinde, `ReorderList` denetimi otomatik olarak veri kaynağının `Update` komutuna iki değer gönderir: öğenin yeni konumu ve KIMLIĞI. Bu nedenle, veri kaynağı bu iki değer için bir `<UpdateParameters>` bölümüne ihtiyaç duyuyor:

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample1.aspx)]

`ReorderList` denetiminin aşağıdaki öznitelikleri ayarlaması gerekir:

- `AllowReorder`: liste öğelerinin yeniden düzenlenmiş olup olmadığı
- `DataSourceID`: veri kaynağının KIMLIĞI
- `DataKeyField`: veri kaynağındaki birincil anahtar sütununun adı
- `SortOrderField`: liste öğeleri için sıralama düzeni sağlayan veri kaynağı sütunu

`<DragHandleTemplate>` ve `<ItemTemplate>` bölümlerinde, listenin düzeni ince ayarlanabilir. Ayrıca, burada görüldüğü gibi `Eval()` yöntemi kullanılarak veri bağlama mümkündür:

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample2.aspx)]

Aşağıdaki CSS stil bilgileri (`ReorderList` denetiminin `<DragHandleTemplate>` bölümünde başvurulur), fare işaretçisinin sürükleme tutamacının üzerine geldiğinde uygun şekilde değişmesini sağlar:

[!code-css[Main](drag-and-drop-via-reorderlist-cs/samples/sample3.css)]

Son olarak, `ScriptManager` bir denetim sayfa için ASP.NET AJAX 'ı başlatır:

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample4.aspx)]

Bu örneği tarayıcıda çalıştırın ve liste öğelerini bir bit olarak yeniden düzenleyin. Sonra, sayfayı yeniden yükleyin ve/veya veritabanına bakın. Değiştirilen konumlar korunur ve ayrıca, yalnızca biçimlendirme kullanarak, veritabanındaki `position` sütununda ve tüm kodlar olmadan bu değerlere yansıtılır.

[veritabanındaki verileri yeni liste öğesi sırasına göre ![](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)

Veritabanındaki veriler yeni liste öğesi sırasına göre değişir ([tam boyutlu görüntüyü görüntülemek Için tıklayın](drag-and-drop-via-reorderlist-cs/_static/image9.png))

> [!div class="step-by-step"]
> [Önceki](using-postbacks-with-reorderlist-cs.md)
> [İleri](using-postbacks-with-reorderlist-vb.md)
