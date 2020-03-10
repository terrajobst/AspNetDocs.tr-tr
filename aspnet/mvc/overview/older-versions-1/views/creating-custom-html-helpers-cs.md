---
uid: aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: Özel HTML Yardımcıları oluşturma (C#) | Microsoft Docs
author: microsoft
description: Bu öğreticinin amacı, MVC görünümleriniz dahilinde kullanabileceğiniz özel HTML Yardımcıları oluşturmayı gösterir. HTML Yardımcısı 'ndan yararlanarak...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 264ff9850bad397826b45649d52fbfefafc53a01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600242"
---
# <a name="creating-custom-html-helpers-c"></a>Özel HTML Yardımcıları Oluşturma (C#)

[Microsoft](https://github.com/microsoft) tarafından

[PDF 'YI indir](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> Bu öğreticinin amacı, MVC görünümleriniz dahilinde kullanabileceğiniz özel HTML Yardımcıları oluşturmayı gösterir. HTML yardımcılarından yararlanarak, standart bir HTML sayfası oluşturmak için gerçekleştirmeniz gereken HTML etiketlerinin sıkıcı yazma miktarını azaltabilirsiniz.

Bu öğreticinin amacı, MVC görünümleriniz dahilinde kullanabileceğiniz özel HTML Yardımcıları oluşturmayı gösterir. HTML yardımcılarından yararlanarak, standart bir HTML sayfası oluşturmak için gerçekleştirmeniz gereken HTML etiketlerinin sıkıcı yazma miktarını azaltabilirsiniz.

Bu öğreticinin ilk bölümünde, ASP.NET MVC çerçevesine dahil olan mevcut HTML yardımcılarını anlatmaktadır. Sonra, özel HTML Yardımcıları oluşturmak için iki yöntem açıkladım: statik bir yöntem oluşturarak ve bir genişletme yöntemi oluşturarak özel HTML Yardımcıları oluşturmayı açıkladım.

## <a name="understanding-html-helpers"></a>HTML Yardımcıları anlama

HTML Yardımcısı yalnızca bir dize döndüren bir yöntemdir. Dize, istediğiniz herhangi bir içerik türünü temsil edebilir. Örneğin, HTML `<input>` ve `<img>` etiketleri gibi standart HTML etiketlerini işlemek için HTML Yardımcıları kullanabilirsiniz. Ayrıca, bir sekme şeridi veya bir HTML tablosu veritabanı verileri gibi karmaşık içerikleri işlemek için HTML Yardımcıları da kullanabilirsiniz.

ASP.NET MVC çerçevesi, aşağıdaki standart HTML Yardımcıları kümesini içerir (Bu bir liste değildir):

- HTML. ActionLink ()
- HTML. BeginForm ()
- Html.CheckBox()
- HTML. DropDownList ()
- Html.EndForm()
- HTML. Hidden ()
- Html.ListBox()
- HTML. Password ()
- Html.RadioButton()
- HTML. TextArea ()
- Html.TextBox()

Örneğin, liste 1 ' de formu göz önünde bulundurun. Bu form standart HTML yardımcılarını (bkz. Şekil 1) içeren yardım ile birlikte işlenir. Bu form basit bir HTML formu işlemek için `Html.BeginForm()` ve `Html.TextBox()` yardımcı yöntemlerini kullanır.

[HTML Yardımcıları ile işlenen ![sayfası](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)

**Şekil 01**: HTML Yardımcıları ile işlenen sayfa ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-custom-html-helpers-cs/_static/image3.png))

**Listeleme 1 – `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

HTML. BeginForm () yardımcı yöntemi, açma ve kapatma HTML `<form>` etiketlerini oluşturmak için kullanılır. `Html.BeginForm()` yönteminin bir using ifadesinin içinde çağrıldığından emin olun. Using ifadesinde, using bloğunun sonunda `<form>` etiketinin kapalı olması güvence altına alınır.

Tercih ederseniz, bir using bloğu oluşturmak yerine, `<form>` etiketini kapatmak için HTML. EndForm () yardımcı yöntemini çağırabilirsiniz. Size çok sezgisel bir açma ve kapatma `<form>` etiketi oluşturmak için hangi yaklaşımı kullanın.

`Html.TextBox()` yardımcı yöntemleri, HTML `<input>` etiketlerini işlemek için 1. liste ' de kullanılır. Tarayıcınızda kaynağı görüntüle ' yi seçerseniz, liste 2 ' de HTML kaynağını görürsünüz. Kaynağın standart HTML etiketleri içerdiğini unutmayın.

> [!IMPORTANT]
> `Html.TextBox()`-HTML Yardımcısı 'nın `<% %>` etiketleri yerine `<%= %>` etiketleriyle işlendiğine dikkat edin. Eşittir işaretini eklemezseniz, hiçbir şey tarayıcıya işlenmez.

ASP.NET MVC çerçevesi küçük bir yardımcılar kümesi içerir. Büyük olasılıkla, MVC çerçevesini özel HTML yardımcılarını genişletmenize gerek duyarsınız. Bu öğreticinin geri kalanında, özel HTML Yardımcıları oluşturmak için iki yöntem öğrenirsiniz.

**Listeleme 2 – `Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a>Statik yöntemlerle HTML Yardımcıları oluşturma

Yeni bir HTML Yardımcısı oluşturmanın en kolay yolu, bir dize döndüren statik bir yöntem oluşturmaktır. Örneğin, bir HTML `<label>` etiketi oluşturan yeni bir HTML Yardımcısı oluşturmaya karar verdiğinizi düşünün. Bir `<label>` işlemek için liste 2 ' de sınıfını kullanabilirsiniz.

**Listeleme 2 – `Helpers\LabelHelper.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

Kod 2 ' de sınıf hakkında özel bir şey yoktur. `Label()` yöntemi yalnızca bir dize döndürür.

Listeleme 3 ' teki değiştirilen dizin görünümü HTML `<label>` etiketlerini işlemek için `LabelHelper` kullanır. Görünümün, `Application1.Helpers` ad alanını içeri aktaran bir `<%@ imports %>` yönergesi içerdiğine dikkat edin.

**Listeleme 2 – `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a>Uzantı yöntemleriyle HTML Yardımcıları oluşturma

Yalnızca ASP.NET MVC çerçevesinin içerdiği standart HTML Yardımcıları gibi çalışan HTML Yardımcıları oluşturmak istiyorsanız, uzantı yöntemleri oluşturmanız gerekir. Uzantı yöntemleri varolan bir sınıfa yeni yöntemler eklemenizi sağlar. Bir HTML yardımcı yöntemi oluştururken, bir görünümün HTML özelliği tarafından temsil edilen HtmlHelper sınıfına yeni yöntemler eklersiniz.

Listeleme 3 ' teki sınıfı, `Label()`adlı `HtmlHelper` sınıfına bir genişletme yöntemi ekler. Bu sınıf hakkında dikkat etmeniz gereken birkaç nokta vardır. İlk olarak, sınıfın bir statik sınıf olduğunu fark edersiniz. Statik sınıfla bir genişletme yöntemi tanımlamanız gerekir.

İkincisi, `Label()` yönteminin ilk parametresinin önünde `this`anahtar sözcüğünün olduğuna dikkat edin. Bir genişletme yönteminin ilk parametresi, genişletme yönteminin genişlettiği sınıfı gösterir.

**Listeleme 3 – `Helpers\LabelExtensions.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

Bir genişletme yöntemi oluşturup uygulamanızı başarılı bir şekilde oluşturduktan sonra, genişletme yöntemi bir sınıfın tüm diğer yöntemleri gibi Visual Studio IntelliSense 'de görünür (bkz. Şekil 2). Tek fark, genişletme yöntemlerinin bunların yanında özel bir simge (aşağı ok simgesi) ile görünme sayısıdır.

[HTML. Label () genişletme yöntemini kullanarak ![](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)

**Şekil 02**: HTML. Label () genişletme yöntemini kullanma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-custom-html-helpers-cs/_static/image6.png))

Liste 4 ' te değiştirilen dizin görünümü, tüm `<label>` etiketlerini işlemek için HTML. Label () genişletme yöntemini kullanır.

**Listeleme 4 – `Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a>Özet

Bu öğreticide, özel HTML Yardımcıları oluşturmak için iki yöntem öğrendiniz. İlk olarak, bir dize döndüren statik bir yöntem oluşturarak özel bir `Label()` HTML Yardımcısı oluşturmayı öğrendiniz. Daha sonra, `HtmlHelper` sınıfında bir genişletme yöntemi oluşturarak özel bir `Label()` HTML Yardımcısı yöntemi oluşturmayı öğrendiniz.

Bu öğreticide son derece basit bir HTML yardımcı yöntemi oluşturmaya odaklandım. Bir HTML Yardımcısı 'nın istediğiniz kadar karmaşık olduğunu fark edebilirsiniz. Ağaç görünümleri, menüler veya veritabanı verilerinin tabloları gibi zengin içerik işleyen HTML Yardımcıları oluşturabilirsiniz.

> [!div class="step-by-step"]
> [Önceki](asp-net-mvc-views-overview-cs.md)
> [İleri](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
