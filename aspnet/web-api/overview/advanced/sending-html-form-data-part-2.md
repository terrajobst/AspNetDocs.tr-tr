---
uid: web-api/overview/advanced/sending-html-form-data-part-2
title: "ASP.NET Web API 'sinde HTML form verileri gönderme: dosya yükleme ve çok parçalı MIME-ASP.NET 4. x"
author: MikeWasson
description: Bu öğreticide, bir Web API 'sine dosya yükleme işleminin nasıl yapılacağı gösterilmektedir. Ayrıca, çok parçalı MIME verilerinin nasıl işlenmesi açıklanmaktadır.
ms.author: riande
ms.date: 06/21/2012
ms.custom: seoapril2019
ms.assetid: a7f3c1b5-69d9-4261-b082-19ffafa5f16a
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-2
msc.type: authoredcontent
ms.openlocfilehash: f5aaebb96f631dfb6b0da1fbca96cd93a6a7fe2d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557570"
---
# <a name="sending-html-form-data-in-aspnet-web-api-file-upload-and-multipart-mime"></a>ASP.NET Web API 'sinde HTML form verileri gönderme: dosya yükleme ve çok parçalı MIME

, [Mike te son](https://github.com/MikeWasson)

## <a name="part-2-file-upload-and-multipart-mime"></a>Bölüm 2: dosya yükleme ve çok parçalı MIME

Bu öğreticide, bir Web API 'sine dosya yükleme işleminin nasıl yapılacağı gösterilmektedir. Ayrıca, çok parçalı MIME verilerinin nasıl işlenmesi açıklanmaktadır.

> [!NOTE]
> [Tamamlanmış projeyi indirin](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d).

Bir dosyayı karşıya yüklemek için bir HTML formu örneği aşağıda verilmiştir:

[!code-html[Main](sending-html-form-data-part-2/samples/sample1.html)]

![](sending-html-form-data-part-2/_static/image1.png)

Bu form bir metin girişi denetimi ve bir dosya girişi denetimi içerir. Form bir dosya girişi denetimi içerdiğinde, **Enctype** özniteliği her zaman &quot;multipart/form-Data&quot;olmalıdır ve bu, formun çok PARÇALı bir MIME iletisi olarak gönderileceğini belirtir.

Bir çok parçalı MIME iletisinin biçimi, örnek bir isteğe bakarak anlaşılması en kolay yoldur:

[!code-console[Main](sending-html-form-data-part-2/samples/sample2.cmd)]

Bu ileti, her form denetimi için bir tane olmak üzere iki *parçaya*bölünür. Bölüm sınırları, tireler ile başlayan satırlar ile belirtilir.

> [!NOTE]
> Bölüm sınırı, sınır dizesinin yanlışlıkla bir ileti bölümü içinde görünmemesini sağlamak için rastgele bir bileşen (&quot;41184676334&quot;) içerir.

Her ileti parçası bir veya daha fazla üst bilgi içerir ve ardından bölüm içerikleri gelir.

- Content-Disposition üst bilgisi, denetimin adını içerir. Dosyalar için dosya adını da içerir.
- Content-Type üst bilgisi, bölümündeki verileri tanımlar. Bu üst bilgi atlanırsa, varsayılan metin/düz ' dır.

Önceki örnekte, Kullanıcı, Type Image/JPEG; içerik türü ile birlikte bir dosya olarak belirtilen bir dosyayı karşıya yükledi. ve metin girişinin değeri &quot;yaz tatili&quot;.

## <a name="file-upload"></a>Karşıya dosya yükleme

Şimdi çok parçalı bir MIME iletisinden dosyaları okuyan bir Web API denetleyicisine göz atalım. Denetleyici dosyaları zaman uyumsuz olarak okur. Web API 'SI, [görev tabanlı programlama modelini](https://msdn.microsoft.com/library/dd460693.aspx)kullanarak zaman uyumsuz eylemleri destekler. İlk olarak, **Async** ve **await** anahtar sözcüklerini destekleyen .NET Framework 4,5 ' i hedefliyorsanız, bu kod aşağıda verilmiştir.

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample3.cs)]

Denetleyici eyleminin hiçbir parametre almaz. Bunun nedeni, bir medya türü biçimlendirici çağırmadan, işlem içindeki istek gövdesini işletireceğiz.

**Imultipartcontent** yöntemi, isteğin çok PARÇALı bir MIME iletisi içerip içermediğini denetler. Aksi takdirde, denetleyici HTTP durum kodu 415 (desteklenmeyen medya türü) döndürür.

**Multipartformdatastreamprovider** sınıfı, karşıya yüklenen dosyalar için dosya akışlarını ayıran bir yardımcı nesnedir. Çok parçalı MIME iletisini okumak için, **Readasmultipartasync** yöntemini çağırın. Bu yöntem, tüm ileti parçalarını ayıklar ve bunları **Multipartformdatastreamprovider**tarafından sunulan akışlara yazar.

Yöntem tamamlandığında, **çok partfiledata** nesnelerinin bir koleksiyonu olan **Filedata** özelliğinden dosyalar hakkında bilgi alabilirsiniz.

- **Multipartfiledata. FileName** , sunucuda dosyanın kaydedildiği yerel dosya adıdır.
- **Multipartfiledata. Headers** , bölüm üst bilgisini (istek üst bilgisini*değil* ) içerir. Bunu, Içerik\_eğilimi ve Içerik türü üst bilgilerine erişmek için kullanabilirsiniz.

Adından da anlaşılacağı gibi, **Readasmultipartasync** zaman uyumsuz bir yöntemdir. Yöntem tamamlandıktan sonra iş gerçekleştirmek için bir [devamlılık görevi](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4,0) veya **await** anahtar sözcüğünü (.NET 4,5) kullanın.

Önceki kodun .NET Framework 4,0 sürümü aşağıda verilmiştir:

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample4.cs)]

## <a name="reading-form-control-data"></a>Form denetimi verilerini okuma

Daha önce gösterilen HTML formu metin girişi denetimine sahipti.

[!code-html[Main](sending-html-form-data-part-2/samples/sample5.html)]

**Multipartformdatastreamprovider**'ın **FormData** özelliğinden denetimin değerini alabilirsiniz.

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample6.cs?highlight=15)]

**FormData** , form denetimleri için ad/değer çiftlerini Içeren bir **NameValueCollection** . Koleksiyonda yinelenen anahtarlar bulunabilir. Şu formu göz önünde bulundurun:

[!code-html[Main](sending-html-form-data-part-2/samples/sample7.html)]

![](sending-html-form-data-part-2/_static/image2.png)

İstek gövdesi şöyle görünebilir:

[!code-console[Main](sending-html-form-data-part-2/samples/sample8.cmd)]

Bu durumda, **FormData** koleksiyonu aşağıdaki anahtar/değer çiftlerini içerir:

- seyahat: gidiş dönüş
- Seçenekler: nonstop
- Seçenekler: tarihler
- koltuk: pencere
