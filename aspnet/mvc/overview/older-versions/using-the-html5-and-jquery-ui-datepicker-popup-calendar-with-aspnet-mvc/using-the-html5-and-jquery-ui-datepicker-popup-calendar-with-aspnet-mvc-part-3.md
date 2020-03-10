---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
title: ASP.NET MVC ile HTML5 ve jQuery kullanıcı arabirimi DatePicker açılan takvimini kullanma-Bölüm 3 | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici, düzenleyici şablonları, görüntüleme şablonları ve jQuery UI DatePicker açılan takvimini bir ASP.NET MV içinde nasıl çalışabileceğiniz hakkında temel bilgileri öğretir...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 8f5f91ae-12d7-4cf3-ac09-4bb53d07ee60
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
msc.type: authoredcontent
ms.openlocfilehash: b3249397e54e64538c4dc78e5fe8b94656e8962b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538908"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-3"></a>ASP.NET MVC ile HTML5 ve jQuery kullanıcı arabirimi DatePicker açılan takvimini kullanma-Bölüm 3

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> Bu öğreticide, bir ASP.NET MVC web uygulamasında düzenleyici şablonları, görüntüleme şablonları ve jQuery UI DatePicker açılan takvim ile çalışma hakkında temel bilgiler verilir.

## <a name="working-with-complex-types"></a>Karmaşık türlerle çalışma

Bu bölümde bir adres sınıfı oluşturacak ve bunu göstermek için bir şablon oluşturmayı öğreneceksiniz.

*Modeller* klasöründe, *Person.cs* adlı yeni bir sınıf dosyası oluşturun; burada iki tür koyacaksınız: bir `Person` sınıfı ve bir `Address` sınıfı. `Person` sınıfı, `Address`olarak yazılmış bir özelliği içerir. `Address` türü karmaşık bir türdür, yani `int`, `string`veya `double`gibi yerleşik türlerden biri değildir. Bunun yerine, birkaç özelliği vardır. Yeni sınıfların kodu şöyle görünür:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample1.cs)]

`Movie` denetleyicisinde, bir kişi örneğini göstermek için aşağıdaki `PersonDetail` eylemini ekleyin:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample2.cs)]

Sonra, `Person` modelini bazı örnek verilerle doldurmak için `Movie` denetleyicisine aşağıdaki kodu ekleyin:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample3.cs)]

*Views\Movies\PersonDetail.cshtml* dosyasını açın ve `PersonDetail` görünümü için aşağıdaki biçimlendirmeyi ekleyin.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample4.cshtml)]

Uygulamayı çalıştırmak için CTRL + F5 tuşlarına basın ve *filmler/PersonDetail*' a gidin.

Bu ekran görüntüsünde görebileceğiniz gibi `PersonDetail` görünümü `Address` karmaşık türü içermez. (Hiçbir adres gösterilmez.)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image1.png)

`Address` modeli verileri, karmaşık bir tür olduğundan görüntülenmiyor. Adres bilgilerini göstermek için *Views\Movies\PersonDetail.cshtml* dosyasını yeniden açın ve aşağıdaki biçimlendirmeyi ekleyin.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample5.cshtml)]

Şimdi `PersonDetail` görünümü için biçimlendirmenin tamamı şöyle görünür:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample6.cshtml)]

Uygulamayı yeniden çalıştırın ve `PersonDetail` görünümünü görüntüleyin. Adres bilgileri artık görüntülenir:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image2.png)

### <a name="creating-a-template-for-a-complex-type"></a>Karmaşık bir tür için şablon oluşturma

Bu bölümde, `Address` karmaşık türünü işlemek için kullanılacak bir şablon oluşturacaksınız. `Address` türü için bir şablon oluşturduğunuzda, ASP.NET MVC uygulamayı uygulamanın herhangi bir yerinden bir adres modelini biçimlendirmek için otomatik olarak kullanabilir. Bu, `Address` türünün işlemeyi uygulamada tek bir yerden denetlemek için bir yol sağlar.

*Views\shared\displaytemplates* klasöründe, **Adres**adlı bir kesin türü belirtilmiş kısmi görünüm oluşturun:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image3.png)

**Ekle**' ye tıklayın ve ardından yeni *Views\shared\displaytemplates\address.cshtml* dosyasını açın. Yeni görünüm aşağıdaki oluşturulan biçimlendirmeyi içerir:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample7.cshtml)]

Uygulamayı çalıştırın ve `PersonDetail` görünümünü görüntüleyin. Bu kez, yeni oluşturduğunuz `Address` şablonu `Address` karmaşık türü göstermek için kullanılır; bu nedenle, ekran aşağıdaki gibi görünür:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image4.png)

### <a name="summary-ways-to-specify-the-model-display-format-and-template"></a>Özet: model görüntüleme biçimini ve şablonu belirtme yolları

Aşağıdaki yaklaşımlardan birini kullanarak bir model özelliğinin biçimini veya şablonunu belirtebilirsiniz:

- `DisplayFormat` özniteliği modeldeki bir özelliğe uygulanıyor. Örneğin, aşağıdaki kod, tarihin zaman olmadan görüntülenmesine neden olur:

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample8.cs)]
- Modeldeki bir özelliğe bir [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) özniteliği uygulama ve veri türünü belirtme. Örneğin, aşağıdaki kod, tarihin zaman olmadan görüntülenmesine neden olur.

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample9.cs)]

    Uygulama *Views\shared\displaytemplates* klasöründe veya *Views\Movies\DisplayTemplates* klasöründe *date. cshtml* şablonu içeriyorsa, bu şablon `DateTime` özelliğini işlemek için kullanılacaktır. Aksi halde, yerleşik ASP.NET şablon oluşturma sistemi, bir tarih olarak özelliği görüntüler.
- *Views\shared\displaytemplates* klasöründe veya adı biçimlendirmek istediğiniz veri türüyle eşleşen *Views\Movies\DisplayTemplates* klasöründe bir görüntüleme şablonu oluşturma. Örneğin, model için bir öznitelik eklemeden ve görünümlere herhangi bir biçimlendirme eklemeden, bir modeldeki `DateTime` özellikleri işlemek için *Views\shared\displaytemplates\datetime.exe* kullanıldığını gördünüz.
- Model özelliğinin görüntüleneceği şablonu belirtmek için modelde [Uııınt](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) özniteliği kullanılıyor.
- Görüntüleme şablonu adını, bir görünümdeki çağrı [Için HTML. displayto](https://msdn.microsoft.com/library/ee407420.aspx) 'a açıkça ekleme.

Kullandığınız yaklaşım, uygulamanızda ne yapmanız gerektiği konusunda farklılık gösterir. Tam olarak ihtiyacınız olan biçimlendirme türünü almak için bu yaklaşımların karıştığı yaygın olmayan bir durumdur.

Sonraki bölümde, bir bit olarak geçiş yapar ve verilerin nasıl girildiğini özelleştirmek için verilerin nasıl görüntülendiğini özelleştirirsiniz. Tarihleri belirtmek için bir yol yolu sağlamak üzere uygulamadaki düzenleme görünümlerine jQuery DatePicker ' i kullanacaksınız.

> [!div class="step-by-step"]
> [Önceki](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
> [İleri](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)
