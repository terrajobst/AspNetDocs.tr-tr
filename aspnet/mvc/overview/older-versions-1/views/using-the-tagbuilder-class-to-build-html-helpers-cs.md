---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
title: HTML Yardımcıları oluşturmak için TagBuilder sınıfını kullanma (C#) | Microsoft Docs
author: StephenWalther
description: Stephen Walther, ASP.NET MVC çerçevesinde TagBuilder sınıfı adında yararlı bir yardımcı program sınıfı sağlar. TagBuilder sınıfını kolayca kullanabilirsiniz...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 3975a52f-bd15-4edd-8f3d-1df93672515b
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: c8eaea9932a30c744b9a69861619ce9458b5a23a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600032"
---
# <a name="using-the-tagbuilder-class-to-build-html-helpers-c"></a>HTML Yardımcıları oluşturmak için TagBuilder sınıfını kullanma (C#)

ile [Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther, ASP.NET MVC çerçevesinde TagBuilder sınıfı adında yararlı bir yardımcı program sınıfı sağlar. HTML etiketlerini kolayca oluşturmak için TagBuilder sınıfını kullanabilirsiniz.

ASP.NET MVC Framework, HTML Yardımcıları oluştururken kullanabileceğiniz TagBuilder sınıfı adında yararlı bir yardımcı program sınıfı içerir. Sınıf adı olarak TagBuilder sınıfı, HTML etiketlerini kolayca oluşturmanızı sağlar. Bu kısa öğreticide, TagBuilder sınıfına bir genel bakış sunulur ve HTML &lt;img&gt; etiketlerini işleyen basit bir HTML Yardımcısı oluştururken bu sınıfın nasıl kullanılacağını öğrenirsiniz.

## <a name="overview-of-the-tagbuilder-class"></a>TagBuilder sınıfına genel bakış

TagBuilder sınıfı System. Web. Mvc ad alanında yer alır. Beş yöntemi vardır:

- AddCssClass ()-etikete yeni bir *class = ""* özniteliği eklemenize olanak sağlar.
- GenerateId ()-bir etikete ID özniteliği eklemenize olanak sağlar. Bu yöntem, kimliğin içindeki dönemleri otomatik olarak değiştirir (varsayılan olarak, dönemler alt çizgi ile değiştirilir)
- MergeAttribute ()-bir etikete öznitelik eklemenize olanak sağlar. Bu yöntemin birden fazla aşırı yüklemesi var.
- SetInnerText ()-etiketin iç metnini ayarlamanıza olanak sağlar. İç metin otomatik olarak HTML kodlenmiştir.
- ToString ()-etiketi işlemenizi sağlar. Normal bir etiket, başlangıç etiketi, bitiş etiketi veya kendi kendine kapatma etiketi oluşturmak isteyip istemediğinizi belirtebilirsiniz.

TagBuilder sınıfı dört önemli özelliğe sahiptir:

- Öznitelikler-etiketin tüm özniteliklerini temsil eder.
- Idattributedotdeğişim-, dönemleri değiştirmek için generateId () yöntemi tarafından kullanılan karakteri temsil eder (varsayılan bir alt çizgi).
- InnerHtml-etiketin iç içeriğini temsil eder. Bu özelliğe bir dize atanması, dizeyi HTML olarak *Not etmez* .
- TagName-etiketin adını temsil eder.

Bu yöntemler ve özellikler, bir HTML etiketi oluşturmak için ihtiyacınız olan tüm temel yöntemleri ve özellikleri sağlar. TagBuilder sınıfını gerçekten kullanmanız gerekmez. Bunun yerine bir StringBuilder sınıfı kullanabilirsiniz. Ancak, TagBuilder sınıfı yaşamınızı biraz daha kolay hale getirir.

## <a name="creating-an-image-html-helper"></a>Görüntü HTML Yardımcısı oluşturma

TagBuilder sınıfının bir örneğini oluşturduğunuzda, TagBuilder oluşturucusuna derlemek istediğiniz etiketin adını geçirirsiniz. Daha sonra, etiketinin özniteliklerini değiştirmek için AddCssClass ve MergeAttribute () yöntemleri gibi yöntemleri çağırabilirsiniz. Son olarak, etiketini işlemek için ToString () yöntemini çağırın.

Örneğin, Listeleme 1 bir resim HTML Yardımcısı içerir. Görüntü Yardımcısı, bir HTML &lt;img&gt; etiketini temsil eden bir TagBuilder ile dahili olarak uygulanır.

**Listeleme 1-Helpers\ımagehelper.cs**

[!code-csharp[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample1.cs)]

Listeleme 1 ' deki sınıf, görüntü adlı iki statik aşırı yüklenmiş yöntem içerir. Image () yöntemini çağırdığınızda, bir HTML öznitelikleri kümesini temsil eden bir nesneyi geçirebilirsiniz.

TagBuilder. MergeAttribute () yönteminin, bir src özniteliği gibi ayrı ayrı öznitelikleri eklemek için nasıl kullanıldığına dikkat edin. Ayrıca, TagBuilder. MergeAttributes () yönteminin, TagBuilder 'a özniteliklerin bir koleksiyonunu eklemek için nasıl kullanıldığına dikkat edin. MergeAttributes () yöntemi bir sözlük&lt;dize, nesne&gt; parametresini kabul eder. Routevaluedicınary sınıfı, özniteliklerin koleksiyonunu temsil eden nesneyi&lt;dize, nesne&gt;olarak dönüştürmek için kullanılır.

Yansıma yardımcısını oluşturduktan sonra, ASP.NET MVC görünümlerinizin yardımcı öğesini diğer standart HTML yardımcılarını gibi kullanabilirsiniz. Liste 2 ' deki görünüm, aynı Xbox görüntüsünü iki kez görüntülemek için görüntü yardımcısını kullanır (bkz. Şekil 1). Image () yardımcısı hem hem de HTML öznitelik koleksiyonu olmadan çağrılır.

**Listeleme 2-Home\ındex.aspx**

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample2.aspx)]

[Yeni proje iletişim kutusunu ![](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.png)

**Şekil 01**: görüntü Yardımcısını kullanma ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image2.png))

Index. aspx görünümünün en üstündeki görüntü Yardımcısı ile ilişkili ad alanını içeri aktarmanız gerektiğini unutmayın. Yardımcı aşağıdaki yönergeyle içeri aktarılır:

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample3.aspx)]

> [!div class="step-by-step"]
> [Önceki](creating-custom-html-helpers-cs.md)
> [İleri](creating-page-layouts-with-view-master-pages-cs.md)
