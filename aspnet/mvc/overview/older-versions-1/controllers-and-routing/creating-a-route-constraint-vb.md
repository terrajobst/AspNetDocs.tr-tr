---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-vb
title: Yol kısıtlaması oluşturma (VB) | Microsoft Docs
author: StephenWalther
description: Bu öğreticide, Stephen Walther, normal ifadelerle yol kısıtlamaları oluşturarak tarayıcı isteklerinin yollarla nasıl eşleştiğini nasıl denetleyebileceğinizi göstermektedir.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: b7cce113-c82c-45bf-b97b-357e5d9f7f56
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-vb
msc.type: authoredcontent
ms.openlocfilehash: 205742dd8f866c8828008c8aac7ab3f98b173ceb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601390"
---
# <a name="creating-a-route-constraint-vb"></a>Rota Kısıtlaması Oluşturma (VB)

ile [Stephen Walther](https://github.com/StephenWalther)

> Bu öğreticide, Stephen Walther, normal ifadelerle yol kısıtlamaları oluşturarak tarayıcı isteklerinin yollarla nasıl eşleştiğini nasıl denetleyebileceğinizi göstermektedir.

Belirli bir rota ile eşleşen Tarayıcı isteklerini kısıtlamak için yol kısıtlamalarını kullanırsınız. Bir yol kısıtlaması belirtmek için normal bir ifade kullanabilirsiniz.

Örneğin, yolu Global. asax dosyanızda liste 1 ' de tanımladığınızı düşünün.

**Listeleme 1-Global. asax. vb**

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample1.vb)]

Listeleme 1, ürün adlı bir rota içerir. Tarayıcı isteklerini, liste 2 ' de bulunan ProductController ile eşlemek için ürün yolunu kullanabilirsiniz.

**Listeleme 2-Controllers\productcontroller.exe**

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample2.vb)]

Ürün denetleyicisi tarafından açığa çıkarılan ayrıntılar () eyleminin ProductID adlı tek bir parametreyi kabul ettiğini unutmayın. Bu parametre bir tamsayı parametresidir.

Liste 1 ' de tanımlanan yol aşağıdaki URL 'Lerden hiçbiriyle eşleşir:

- /Product/23
- /Product/7

Ne yazık ki yol aşağıdaki URL 'Lerle aynı olacaktır:

- /Product/blah
- /Product/Apple

Ayrıntılar () eylemi bir tamsayı parametresi beklediği için, bir tamsayı değeri dışında bir istek içeren bir isteğin yapılması hataya neden olur. Örneğin, tarayıcınıza/Product/Apple URL 'sini yazarsanız Şekil 1 ' de hata sayfasını alırsınız.

[Yeni proje iletişim kutusunu ![](creating-a-route-constraint-vb/_static/image1.jpg)](creating-a-route-constraint-vb/_static/image1.png)

**Şekil 01**: bir sayfa açılımı görüntüleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-route-constraint-vb/_static/image2.png))

Gerçekten ne yapmak istiyorsunuz, yalnızca uygun bir ProductID tamsayı içeren URL 'Leri eşleştirin. Rota ile eşleşen URL 'Leri kısıtlamak için bir yol tanımlarken bir kısıtlama kullanabilirsiniz. Listeleme 3 ' teki değiştirilen ürün yolu, yalnızca tamsayılarla eşleşen bir normal ifade kısıtlaması içerir.

**Listeleme 3-Global. asax. vb**

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample3.vb)]

\D + normal ifadesi bir veya daha fazla tamsayılarla eşleşir. Bu kısıtlama, ürün yolunun aşağıdaki URL 'Lerle eşleşmesini sağlar:

- /Product/3
- /Product/8999

Şu URL 'Ler değil:

- /Product/Apple
- /Ürün

Bu tarayıcı istekleri başka bir yol tarafından işlenecek veya eşleşen yollar yoksa, *kaynak bulunamadı* hatası döndürülür.

> [!div class="step-by-step"]
> [Önceki](creating-custom-routes-vb.md)
> [İleri](creating-a-custom-route-constraint-vb.md)
