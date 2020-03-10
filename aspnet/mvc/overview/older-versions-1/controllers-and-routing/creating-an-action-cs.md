---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
title: Eylem oluşturma (C#) | Microsoft Docs
author: microsoft
description: Bir ASP.NET MVC denetleyicisine yeni bir eylem eklemeyi öğrenin. Bir yöntemin eylem olması için gereksinimler hakkında bilgi edinin.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: cb33b28c-3025-4bd1-a1fa-eaa3af7bb56f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
msc.type: authoredcontent
ms.openlocfilehash: ebba935383819935ad85c95245666f4eaf6a0dca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582056"
---
# <a name="creating-an-action-c"></a>Eylem Oluşturma (C#)

[Microsoft](https://github.com/microsoft) tarafından

> Bir ASP.NET MVC denetleyicisine yeni bir eylem eklemeyi öğrenin. Bir yöntemin eylem olması için gereksinimler hakkında bilgi edinin.

Bu öğreticinin amacı, yeni bir denetleyici eylemi oluşturmayı açıklamaktır. Bir eylem yönteminin gereksinimleri hakkında bilgi edinirsiniz. Ayrıca bir yöntemin eylem olarak gösterilmesini nasıl önleyeceğinizi öğreneceksiniz.

## <a name="adding-an-action-to-a-controller"></a>Denetleyiciye eylem ekleme

Denetleyiciye yeni bir yöntem ekleyerek denetleyiciye yeni bir eylem eklersiniz. Örneğin, liste 1 ' deki denetleyici dizin () adlı bir eylem ve SayHello () adlı bir eylem içerir. Her iki yöntem de eylem olarak sunulur.

**Listeleme 1-Controllers\HomeController.cs**

[!code-csharp[Main](creating-an-action-cs/samples/sample1.cs)]

Bir eylem olarak Universe sunulmak için bir yöntemin belirli gereksinimleri karşılaması gerekir:

- Yöntemin ortak olması gerekir.
- Metot statik bir yöntem olamaz.
- Yöntem bir genişletme yöntemi olamaz.
- Yöntem bir Oluşturucu, alıcı veya ayarlayıcı olamaz.
- Metodun açık genel türleri olamaz.
- Yöntemi, denetleyici temel sınıfının bir yöntemi değildir.
- Yöntem **ref** veya **Out** parametreleri içeremez.

Bir denetleyici eyleminin dönüş türü üzerinde hiçbir kısıtlama olmadığına dikkat edin. Bir denetleyici eylemi, bir dize, bir tarih saat, rastgele sınıfın bir örneği veya void döndürebilir. ASP.NET MVC Framework, bir eylem sonucu olmayan herhangi bir dönüş türünü bir dizeye dönüştürür ve dizeyi tarayıcıya işler.

Bu gereksinimleri ihlal etmediği herhangi bir yöntemi bir denetleyiciye eklediğinizde, yöntem bir denetleyici eylemi olarak sunulur. Burada dikkatli olun. Bir denetleyici eylemi, Internet 'e bağlı olan herkes tarafından çağrılabilir. Örneğin, bir Deletemde Web sitesi () denetleyici eylemi oluşturun.

## <a name="preventing-a-public-method-from-being-invoked"></a>Ortak yöntemin çağrılmasını önlemek

Denetleyici sınıfında ortak bir yöntem oluşturmanız gerekiyorsa ve yöntemi bir denetleyici eylemi olarak göstermek istemiyorsanız, yöntemin [Nonactıon] özniteliği kullanılarak çağrılmasını engelleyebilirsiniz. Örneğin, liste 2 ' deki denetleyici, [Nonactıon] özniteliğiyle donatılmış Companygizlilikler () adlı bir genel yöntem içerir.

**Listeleme 2-Controllers\WorkController.cs**

[!code-csharp[Main](creating-an-action-cs/samples/sample2.cs)]

Tarayıcınızın adres çubuğuna/Work/companygizlilikler yazarak Companygizlilikler () denetleyici eylemini çağırmaya çalışırsanız Şekil 1 ' de hata iletisini alırsınız.

[Eylem olmayan bir yöntemi çağırmak ![](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)

**Şekil 01**: eylem olmayan bir yöntem çağırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-an-action-cs/_static/image2.png))

> [!div class="step-by-step"]
> [Önceki](creating-a-controller-cs.md)
> [İleri](asp-net-mvc-routing-overview-vb.md)
