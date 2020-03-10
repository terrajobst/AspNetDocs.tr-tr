---
uid: web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
title: Mücadele botları (C#) | Microsoft Docs
author: wenz
description: Kullanıcı etkileşimi olmadan yorum formları göndererek, otomatik olarak Botte Web günlükleri ve diğer web siteleri. ASP.NET AJAX con içindeki NoBot denetimi...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0a1917e0-884a-4576-8e93-9ed660faae51
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
msc.type: authoredcontent
ms.openlocfilehash: fef55edf12a024e4dd66e2a18ea371ab4dac861f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627416"
---
# <a name="fighting-bots-c"></a>Mücadele Botları (C#)

[Hristia WENZ](https://github.com/wenz) tarafından

[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0CS.pdf)

> Kullanıcı etkileşimi olmadan yorum formları göndererek, otomatik olarak Botte Web günlükleri ve diğer web siteleri. ASP.NET AJAX denetim araç setinde NoBot denetimi, bu botların filifine yardımcı olabilir.

## <a name="overview"></a>Genel bakış

Kullanıcı etkileşimi olmadan yorum formları göndererek, otomatik olarak Botte Web günlükleri ve diğer web siteleri. ASP.NET AJAX denetim araç setinde NoBot denetimi, bu botların filifine yardımcı olabilir.

## <a name="steps"></a>Adımlar

En az bir yaygın yaklaşım, bilgisayarlara ve ınsanlara bilgi vermek için CAPTCHAs tamamen otomatikleştirilmiş ortak bir test olarak kullanılır. Bir BT testi başlangıçta, birisinin bir iletişim ortağının insan veya makine olduğunu belirlemek için ihtiyaç duyduğu bir sınamadır. Web 'de, bir CAPTCHA genellikle üzerinde bazı bozuk harfler içeren bir görüntüden oluşur. Fikir, görüntüdeki harfleri yalnızca bir insan okuyabileceğinden, OCR algoritmalarının başarısız olmasına neden olur.

Bu yaklaşımın çeşitli avantajları ve dezavantajları vardır ancak bunun bir tartışması, Bu öğreticinin kapsamının dışındadır. Ancak, ASP.NET AJAX denetim araç setinde benzer bir yaklaşım sağlayan bir denetim vardır: `NoBot`. Bir CAPTCHA 'dan daha kolay bir şekilde ele `NoBot` alınmıştır, ancak çok daha kolay olan Bloglar gibi web sitelerinde çok daha kolay bir şekilde çalışır.

`NoBot`, şu koşullardan en az biri karşılandığında geçerli ASP.NET Web formunun geri göndermasını karşılar:

- Tarayıcı bir JavaScript bulmaca 'yi çözemez (JavaScript devre dışı bırakıldığında örnek için)
- Kullanıcı formu hızlı bir şekilde gönderdi
- İstemci IP adresi, belirli bir süre içinde formu çok sık gönderdi.

Bu koşulları denetlemek için, `NoBot` denetimi bu öznitelikleri gerektirir (tümü isteğe bağlıdır):

- geri göndermeler arasındaki en az saniye miktarı `ResponseMinimumDelaySeconds`
- bir IP 'den gelen geri göndermeler ölçülere göre `CutoffWindowSeconds` zaman aralığının uzunluğu
- zaman aralığı başına en fazla saniye miktarı `CutoffMaximumInstances`

Aşağıdaki biçimlendirme, geri göndermeler arasında en az iki saniyelik bir gecikme süresi ve 30 saniyelik bir Aralık içinde yalnızca beş geri yükleme veya daha az yer olduğunu talep etmek için geçerlidir:

[!code-aspx[Main](fighting-bots-cs/samples/sample1.aspx)]

Her zamanki gibi, ASP.NET AJAX kitaplığının yüklenmesi ve Denetim araç seti kullanılabilmesi için `ScriptManager` sayfaya dahil ettiğinizden emin olun:

[!code-aspx[Main](fighting-bots-cs/samples/sample2.aspx)]

Çoğu denetim `NoBot` sunucu tarafında gerçekleşdiğinden, bu doğrulamaların sonucunu denetlemeniz gerekir. Bu, `NoBot``IsValid()` yöntemi çağırarak yapılabilir. `NoBotState`türünde olan bir bağımsız değişken (`out` parametresi/`ByRef` parametresi olarak) vardır. Dize temsili, denetimin başarısız olma nedenini içerir ve aksi takdirde `Valid`. Aşağıdaki kod `NoBot`sonucuna göre bir ileti verir:

[!code-aspx[Main](fighting-bots-cs/samples/sample3.aspx)]

Son olarak, göndermek için bir form ve ileti çıkarmak için bir etiket öğesi gerekir ve işiniz bitti!

[!code-aspx[Main](fighting-bots-cs/samples/sample4.aspx)]

Bu betiği çalıştırıp JavaScript 'ı devre dışı bıraktıktan veya ilk iki saniyede formu gönderdiğinizde ya da biçimi otuz saniye içinde yedi kez gönderdiğinizde bir hata iletisi alırsınız. Ancak, yalnızca% 90-95 ' un JavaScript 'in etkin olduğu için bu denetimi daha seyrek kullanın, bu nedenle kullanıcıların% 5-10 ' u `NoBot`test eder.

[Bu hata iletisine ![bir bot neden olmuş olabilir](fighting-bots-cs/_static/image2.png)](fighting-bots-cs/_static/image1.png)

Bu hata iletisi bir bot 'tan kaynaklanmış olabilir ([tam boyutlu görüntüyü görüntülemek Için tıklayın](fighting-bots-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Next](fighting-bots-vb.md)
