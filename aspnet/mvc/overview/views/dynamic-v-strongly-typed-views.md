---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: Dinamik ve Kesin tür belirtilmiş görünümleri | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: bde40f609db25f590108bfc2396071c0033a1326
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/25/2019
ms.locfileid: "58423344"
---
<a name="dynamic-v-strongly-typed-views"></a>Dinamik ve Kesin Türü Belirtilmiş Görünümler
====================
Tarafından [Rick Anderson]((https://twitter.com/RickAndMSFT))

ASP.NET MVC 3'te bir görünüm için bir denetleyiciden bilgi geçirmek için üç yolu vardır:

1. Kesin olarak belirlenmiş model nesnesi.
2. Dinamik tür olarak (kullanarak @model dinamik)
3. Görünüm paketini kullanma

Ben karşılaştırın ve dinamik ve kesin türü belirtilmiş görünümleri için basit bir MVC 3 üst Blog uygulaması yazmamış. Denetleyici basit bir listesini blogları ile başlar:

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

IndexNotStonglyTyped() yönteminde sağ tıklayın ve bir Razor görünüm ekleyin.

[![8475.NotStronglyTypedView [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)

Emin **kesin türü belirtilmiş görünüm oluşturmak** kutunun işaretli değil. Ekranda çok içermiyor:

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

Dinamik ve bir kesin türü belirtilmiş görünüm kullandığımızdan, IntelliSense bize yardımcı olmaz. Tamamlanan kodu aşağıda gösterilmiştir:

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

[![6646.NotStronglyTypedView_5F00_IE [1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)

Kesin türü belirtilmiş görünüm şimdi ekleyeceğiz. Denetleyici için aşağıdaki kodu ekleyin:

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]


Tam olarak aynı dönüş View(topBlogs) olduğuna dikkat edin; kesin olmayan türü belirtilmiş görünüm çağırın. İçine sağ tıklayın *StonglyTypedIndex()* seçip **Görünüm Ekle**. Bu süre seçin **Blog** seçin ve Model sınıfı **listesi** İskele şablon olarak.

[![5658.StrongView [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)

Yeni Görünüm şablon içinde size IntelliSense desteği alın.

[![7002.IntelliSense[1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)

C# projesi indirilebilir [burada](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip).
