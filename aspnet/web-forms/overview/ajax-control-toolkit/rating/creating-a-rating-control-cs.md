---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
title: Derecelendirme denetimi oluşturma (C#) | Microsoft Docs
author: wenz
description: E-ticaretin topluluk sitelerine kadar birçok Web sitesi, kullanıcılarını makale veya öğe hızına sunmaya olanak sağlar. Bu genellikle bazı kodlama çabaları gerektirir, ancak...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 969fb28f-2bff-4fc4-b24a-27f5e2534a37
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
msc.type: authoredcontent
ms.openlocfilehash: c0bf793406e378321f54f0460031c526a0b41a02
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611559"
---
# <a name="creating-a-rating-control-c"></a>Derecelendirme Denetimi Oluşturma (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)

> E-ticaretin topluluk sitelerine kadar birçok Web sitesi, kullanıcılarını makale veya öğe hızına sunmaya olanak sağlar. Bu genellikle bazı kodlama çabaları gerektirir, ancak elden çıkarılmız için Denetim araç seti vardır.

## <a name="overview"></a>Genel bakış

E-ticaretin topluluk sitelerine kadar birçok Web sitesi, kullanıcılarını makale veya öğe hızına sunmaya olanak sağlar. Bu genellikle bazı kodlama çabaları gerektirir, ancak elden çıkarılmız için Denetim araç seti vardır.

## <a name="steps"></a>Adımlar

Birincisi, bir tanesi doldurulmuş bir derecelendirme öğesi ve diğeri de boş bir derecelendirme öğesi için (en az) iki tür görüntü gerekir. Bir derecelendirme öğesi genellikle bir yıldız veya gülümseme olur. Bu senaryo için, bu öğreticide kaynak kodu indirmelerinin bir parçası olarak gülümseme. png ve Empty. png ve Smiley-done. png olmak üzere üç dosya bulabilirsiniz.

Ardından, yeni bir ASP.NET dosyası oluşturun ve buna `ScriptManager` denetimi ekleyerek başlayın:

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample1.aspx)]

Sonra, ASP.NET AJAX denetim araç seti ' nden `Rating` denetimini ekleyin. Bu örnek için aşağıdaki özniteliklerin ayarlanması gerekir:

- kullanılacak ilk derecelendirmeyi `CurrentRating`
- maksimum derecelendirmeyi `MaxRating`
- bir derecelendirme öğesi (yıldız) boş olduğunda kullanılacak CSS sınıfını `EmptyStarCssClass`
- bir derecelendirme öğesi (yıldız) dolduğunda kullanılacak CSS sınıfını `FilledStarCssClass`
- görünür bir stat için kullanılacak CSS sınıfını `StarCssClass`
- bir yıldız derecelendirmesi sunucuya geri gönderildiğinde kullanılacak CSS sınıfını `WaitingStarCssClass`

Burada, başlangıçta hiçbirinin doldurulduğu beş öğe (Smileys) ile bir derecelendirme denetimi oluşturan biçimlendirme verilmiştir:

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample2.aspx)]

Şu anda başvurulan üç CSS sınıfı, CSS kullanılarak kolayca yapılacak uygun görüntü dosyalarını göstermeye gerek duyar:

[!code-css[Main](creating-a-rating-control-cs/samples/sample3.css)]

Üç görüntünün genişlik ve yüksekliğini sağladığınızdan emin olun, aksi takdirde ekran bir bit ileti olarak görünebilir.

Son olarak, derecelendirmenin sonucu kullanıcıya (veya en azından bir veritabanında kayıtlı) gösterilmelidir. Bu nedenle, derecelendirme formunu sunucuya göndermek için bir kısa mesaj ve Gönder düğmesinin çıktısı için bir etiket ekleyin:

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample4.aspx)]

Sunucu tarafı kodunda, derecelendirme denetimine `ID` aracılığıyla erişin ve sonra, örnek 0 ile 5 arasında bir değer olan seçili derecelendirme öğelerinin sayısı olan `CurrentRating` özelliğine erişin.

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample5.aspx)]

Sayfayı kaydedin ve tarayıcınıza yükleyin. (Başlangıçta boş) derecelendirme öğelerinin üzerine geldiğinizde bir JavaScript etkisi oluşur: derecelendirme değişir. Yıldız kümesine tıkladığınızda, geçerli derecelendirme korunur. Son olarak, formu gönderdiğinizde, sunucu tarafı kodu seçili derecelendirmeyi çıktı.

[en az kodla bir derecelendirme sistemi oluşturma ![](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)

Minimum kodla bir derecelendirme sistemi oluşturma ([tam boyutlu görüntüyü görüntülemek Için tıklayın](creating-a-rating-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Next](creating-a-rating-control-vb.md)
