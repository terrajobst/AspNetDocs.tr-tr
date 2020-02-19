---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: Dinamik ve Türü kesin belirlenmiş görünümler | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 3e81c6381b1e280e3b74cb7eb6ea6e6c3224e655
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455691"
---
# <a name="dynamic-v-strongly-typed-views"></a>Dinamik ve Kesin Türü Belirtilmiş Görünümler

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

Bir denetleyiciden ASP.NET MVC 3 ' teki bir görünüme bilgi geçirmenin üç yolu vardır:

1. Türü kesin belirlenmiş bir model nesnesi.
2. Dinamik bir tür olarak (@model dinamik kullanarak)
3. ViewBag kullanma

Dinamik ve kesin belirlenmiş görünümleri karşılaştırmak ve karşılaştırmak için basit bir MVC 3 üst Blog uygulaması yazdım. Denetleyici basit bir blog listesi ile başlar:

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

Indexnotstonglytyped () metodunu sağ tıklatın ve bir Razor görünümü ekleyin.

[![8475. NotStronglyTypedView [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)

**Kesin belirlenmiş görünüm oluştur** kutusunun işaretli olmadığından emin olun. Elde edilen görünüm çok fazla içermez:

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

Kesin olarak belirlenmiş bir görünüm değil, dinamik olarak kullanılan bir görünüm kullandığından, IntelliSense bize yardımcı olmaz. Tamamlanan kod aşağıda gösterilmektedir:

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

[![6646. NotStronglyTypedView_5F00_IE [1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)

Artık türü kesin belirlenmiş bir görünüm ekleyeceğiz. Denetleyiciye aşağıdaki kodu ekleyin:

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]

Tam olarak aynı dönüş görünümüne (Topblogları) dikkat edin; kesin olmayan türsüz bir görünüm olarak çağırın. *Stonglytypedındex ()* içinde sağ tıklayın ve **Görünüm Ekle**' yi seçin. Bu kez **Blog** model sınıfını seçin ve Scaffold şablonu olarak **list** ' i seçin.

[![5658. StrongView [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)

Yeni görünüm şablonunun içinde IntelliSense desteği alırız.

[![7002. IntelliSense [1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)

C# projesi [buradan](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip)indirilebilir.
