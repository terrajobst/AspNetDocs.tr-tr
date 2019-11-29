---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
title: Bir veritabanıyla basamaklı Dingdropdown kullanma (C#) | Microsoft Docs
author: wenz
description: AJAX denetim araç setinde bulunan Basamakarda açılan menü denetimi bir DropDownList denetimini genişleterek bir DropDownList içindeki değişikliklerin ilişkili değerleri anormal bir şekilde yükler...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 684f0c28-a490-4e5b-b5e5-5dfb77464b49
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
msc.type: authoredcontent
ms.openlocfilehash: bcf453170d17807b4e3b2d2a8b545cba43139f89
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599823"
---
# <a name="using-cascadingdropdown-with-a-database-c"></a>Veritabanı ile CascadingDropDown Kullanma (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)

> AJAX denetim araç setinde basamaklı Dingdropdown denetimi bir DropDownList denetimini genişleterek bir DropDownList içindeki değişikliklerin başka bir DropDownList içindeki ilişkili değerleri yükler. Bunun çalışması için özel bir Web hizmetinin oluşturulması gerekir.

## <a name="overview"></a>Genel bakış

AJAX denetim araç setinde basamaklı Dingdropdown denetimi bir DropDownList denetimini genişleterek bir DropDownList içindeki değişikliklerin başka bir DropDownList içindeki ilişkili değerleri yükler. (Örneğin, bir liste ABD durumlarının listesini sağlar ve sonraki liste o durumda büyük şehirlerle doldurulur.) Bunun çalışması için özel bir Web hizmetinin oluşturulması gerekir.

## <a name="steps"></a>Adımlar

Birincisi, bir veri kaynağı gereklidir. Bu örnek, AdventureWorks veritabanını ve Microsoft SQL Server 2005 Express sürümünü kullanır. Veritabanı, Visual Studio yüklemesinin (Express Edition dahil) isteğe bağlı bir parçasıdır ve [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)altında ayrı bir indirme olarak da kullanılabilir. AdventureWorks veritabanı SQL Server 2005 örnek ve örnek veritabanlarının bir parçasıdır ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D ısplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Veritabanını ayarlamanın en kolay yolu, Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) kullanmaktır ve `AdventureWorks.mdf` veritabanı dosyasını eklemektir.

Bu örnek için, SQL Server 2005 Express Sürüm örneğinin `SQLEXPRESS` ve Web sunucusuyla aynı makinede yer aldığı varsayılmaktadır; Bu, aynı zamanda varsayılan kurulumdır. Kurulumlarınız farklıysa, veritabanının bağlantı bilgilerini uyarlamanız gerekir.

ASP.NET AJAX ve Denetim araç seti işlevlerini etkinleştirmek için, `ScriptManager` denetimi sayfada herhangi bir yere yerleştirmeli (ancak &lt;`form`&gt; öğesi içinde):

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample1.aspx)]

Sonraki adımda iki DropDownList denetimi gereklidir. Bu örnekte, AdventureWorks 'ten satıcıyı ve iletişim bilgilerini kullanıyoruz, bu nedenle kullanılabilir satıcılar için bir liste ve kullanılabilir kişiler için bir liste oluşturacağız:

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample2.aspx)]

Daha sonra, sayfaya iki basamaklı Dingı açılan genişleticinin eklenmesi gerekir. Birincisi (satıcılar) listesini doldurur ve diğeri ikinci (kişiler) listesini doldurur. Aşağıdaki özniteliklerin ayarlanması gerekir:

- `ServicePath`: liste girdilerini sunan bir Web hizmetinin URL 'SI
- `ServiceMethod`: liste girdilerini teslim eden Web yöntemi
- `TargetControlID`: açılan listenin KIMLIĞI
- `Category`: çağrıldığında Web yöntemine gönderilen kategori bilgileri
- `PromptText`: sunucudan zaman uyumsuz olarak liste verileri yüklenirken görünen metin
- `ParentControlID`: (isteğe bağlı) geçerli listenin yüklenmesini tetikleyen üst açılan liste

Kullanılan programlama diline bağlı olarak, söz konusu Web hizmeti 'nin adı değişir ancak diğer tüm öznitelik değerleri aynıdır. İlk açılan liste için Basamakarda açılan öğe aşağıda verilmiştir:

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample3.aspx)]

İkinci liste için denetim genişleticilerinin `ParentControlID` özniteliği ayarlaması gerekir, böylece satıcılar listesinde bir girişi seçmek, kişiler listesinde ilişkili öğeleri yüklemeyi tetikler.

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample4.aspx)]

Fiili çalışma daha sonra Web hizmetinde yapılır, bu da aşağıdaki şekilde ayarlanmıştır. `[ScriptService]` özniteliğinin kullanıldığını unutmayın, aksi takdirde ASP.NET AJAX, istemci tarafı betik kodundan Web yöntemlerine erişmek için JavaScript proxy 'sini oluşturamaz.

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample5.aspx)]

Basamaklı Dingdropdown tarafından çağrılan Web yöntemlerinin imzası aşağıdaki gibidir:

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample6.cs)]

Bu nedenle, dönüş değeri denetim araç seti tarafından tanımlanan `CascadingDropDownNameValue` türünde bir dizi olmalıdır. `GetVendors()` yönteminin uygulanması oldukça kolaydır: kod AdventureWorks veritabanına bağlanır ve ilk 25 satıcıyı sorgular. `CascadingDropDownNameValue` oluşturucudaki ilk parametre, ikinci bir değer olan (HTML 'nin &lt;`option`&gt; öğesi) değeri olan liste girişinin başlık öğesidir. Kod şu şekildedir:

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample7.cs)]

Bir satıcı için ilişkili kişileri alma (Yöntem adı: `GetContactsForVendor()`), biraz karmaşık bir yöntemdir. İlki, ilk açılan listede seçilen satıcının belirlenmesi gerekir. Denetim araç seti, bu görev için bir yardımcı yöntemi tanımlar: `ParseKnownCategoryValuesString()` yöntemi, açılan verileri içeren bir `StringDictionary` öğesi döndürür:

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample8.cs)]

Güvenlik nedenleriyle, önce bu verilerin doğrulanması gerekir. Bu nedenle, bir satıcı girişi varsa (ilk basamaklı Dingdropdown öğesinin `Category` özelliği `"Vendor"`) olarak ayarlandığından, Seçili satıcının KIMLIĞI alınabilir:

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample9.cs)]

Yöntemin geri kalanı oldukça düz bir işlemdir ve sonra. Satıcının KIMLIĞI, söz konusu satıcının ilişkili tüm kişilerini alan bir SQL sorgusu için parametre olarak kullanılır. Bir kez daha, yöntem `CascadingDropDownNameValue`türünde bir dizi döndürür.

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample10.cs)]

ASP.NET sayfasını yükleyin ve kısa bir süre sonra satıcı listesi 25 girdi ile doldurulur. Bir giriş seçin ve ikinci açılan listenin verilerle nasıl doldurulduğuna dikkat edin.

[![ilk liste otomatik olarak doldurulur](using-cascadingdropdown-with-a-database-cs/_static/image2.png)](using-cascadingdropdown-with-a-database-cs/_static/image1.png)

İlk liste otomatik olarak doldurulur ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-cascadingdropdown-with-a-database-cs/_static/image3.png))

[![ikinci liste ilk listedeki seçime göre doldurulur](using-cascadingdropdown-with-a-database-cs/_static/image5.png)](using-cascadingdropdown-with-a-database-cs/_static/image4.png)

İkinci liste, ilk listedeki seçime göre doldurulur ([tam boyutlu görüntüyü görüntülemek Için tıklayın](using-cascadingdropdown-with-a-database-cs/_static/image6.png))

> [!div class="step-by-step"]
> [Önceki](filling-a-list-using-cascadingdropdown-cs.md)
> [İleri](presetting-list-entries-with-cascadingdropdown-cs.md)
