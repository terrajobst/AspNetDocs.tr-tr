---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
title: Özel HTML Yardımcıları oluşturma (VB) | Microsoft Docs
author: microsoft
description: Bu öğreticinin amacı, MVC görünümleriniz dahilinde kullanabileceğiniz özel HTML Yardımcıları oluşturmayı gösterir. HTML Yardımcısı 'ndan yararlanarak...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f96f4800-19ef-44c0-b457-55e777eb5de8
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: aaeadde258a2855343a5bfb1e5ee76000e04f6bd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600277"
---
# <a name="creating-custom-html-helpers-vb"></a>Özel HTML Yardımcıları Oluşturma (VB)

[Microsoft](https://github.com/microsoft) tarafından

[PDF 'YI indir](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_VB.pdf)

> Bu öğreticinin amacı, MVC görünümleriniz dahilinde kullanabileceğiniz özel HTML Yardımcıları oluşturmayı gösterir. HTML yardımcılarından yararlanarak, standart bir HTML sayfası oluşturmak için gerçekleştirmeniz gereken HTML etiketlerinin sıkıcı yazma miktarını azaltabilirsiniz.

Bu öğreticinin amacı, MVC görünümleriniz dahilinde kullanabileceğiniz özel HTML Yardımcıları oluşturmayı gösterir. HTML yardımcılarından yararlanarak, standart bir HTML sayfası oluşturmak için gerçekleştirmeniz gereken HTML etiketlerinin sıkıcı yazma miktarını azaltabilirsiniz.

Bu öğreticinin ilk bölümünde, ASP.NET MVC çerçevesine dahil olan mevcut HTML yardımcılarını anlatmaktadır. Sonra, özel HTML Yardımcıları oluşturmak için iki yöntem açıkladım: paylaşılan bir yöntem oluşturarak ve bir genişletme yöntemi oluşturarak özel HTML Yardımcıları oluşturmayı açıkladım.

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

Örneğin, liste 1 ' de formu göz önünde bulundurun. Bu form standart HTML yardımcılarını (bkz. Şekil 1) içeren yardım ile birlikte işlenir. Bu form `Html.BeginForm()` ve `Html.TextBox()` yardımcı yöntemlerini kullanır.

[HTML Yardımcıları ile işlenen ![sayfası](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)

**Şekil 01**: HTML Yardımcıları ile işlenen sayfa ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-custom-html-helpers-vb/_static/image3.png))

**Listeleme 1 – `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample1.aspx)]

`Html.BeginForm()` yardımcı yöntemi, açma ve kapatma HTML `<form>` etiketlerini oluşturmak için kullanılır. `Html.BeginForm()` yönteminin bir using ifadesinin içinde çağrıldığından emin olun. Using ifadesinde, using bloğunun sonunda `<form>` etiketinin kapalı olması güvence altına alınır.

Tercih ederseniz, bir using bloğu oluşturmak yerine, `<form>` etiketini kapatmak için HTML. EndForm () yardımcı yöntemini çağırabilirsiniz. Size çok sezgisel bir açma ve kapatma `<form>` etiketi oluşturmak için hangi yaklaşımı kullanın.

`Html.TextBox()` yardımcı yöntemleri, HTML `<input>` etiketlerini işlemek için 1. liste ' de kullanılır. Tarayıcınızda kaynağı görüntüle ' yi seçerseniz, liste 2 ' de HTML kaynağını görürsünüz. Kaynağın standart HTML etiketleri içerdiğini unutmayın.

> [!IMPORTANT]
> `Html.TextBox()`-HTML Yardımcısı 'nın `<% %>` etiketleri yerine `<%= %>` etiketleriyle işlendiğine dikkat edin. Eşittir işaretini eklemezseniz, hiçbir şey tarayıcıya işlenmez.

ASP.NET MVC çerçevesi küçük bir yardımcılar kümesi içerir. Büyük olasılıkla, MVC çerçevesini özel HTML yardımcılarını genişletmenize gerek duyarsınız. Bu öğreticinin geri kalanında, özel HTML Yardımcıları oluşturmak için iki yöntem öğrenirsiniz.

**Listeleme 2 – `Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-shared-methods"></a>Paylaşılan yöntemlerle HTML Yardımcıları oluşturma

Yeni bir HTML Yardımcısı oluşturmanın en kolay yolu, bir dize döndüren paylaşılan bir yöntem oluşturmaktır. Örneğin, bir HTML `<label>` etiketi oluşturan yeni bir HTML Yardımcısı oluşturmaya karar verdiğinizi düşünün. Bir `<label>`işlemek için liste 2 ' de sınıfını kullanabilirsiniz.

**Listeleme 2 – `Helpers\LabelHelper.vb`**

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample3.vb)]

Kod 2 ' de sınıf hakkında özel bir şey yoktur. `Label()` yöntemi yalnızca bir dize döndürür.

Listeleme 3 ' teki değiştirilen dizin görünümü HTML `<label>` etiketlerini işlemek için `LabelHelper` kullanır. Görünümün Application1. yardımcılar ad alanını içeri aktaran bir `<%@ imports %>` yönergesi içerdiğine dikkat edin.

**Listeleme 2 – `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a>Uzantı yöntemleriyle HTML Yardımcıları oluşturma

Yalnızca ASP.NET MVC çerçevesinin içerdiği standart HTML Yardımcıları gibi çalışan HTML Yardımcıları oluşturmak istiyorsanız, uzantı yöntemleri oluşturmanız gerekir. Uzantı yöntemleri varolan bir sınıfa yeni yöntemler eklemenizi sağlar. Bir HTML yardımcı yöntemi oluştururken, görünümün HTML özelliği tarafından temsil edilen `HtmlHelper` sınıfına yeni yöntemler eklersiniz.

Listeleme 3 ' teki Visual Basic modülü, `HtmlHelper` sınıfına `Label()` adlı bir uzantı yöntemi ekler. Bu modülle ilgili dikkat etmeniz gereken birkaç şey vardır. İlk olarak, modülün `<Extension()>` özniteliğiyle donatılmış olduğuna dikkat edin. Bu özniteliği kullanabilmeniz için `System.Runtime.CompilerServices` ad alanını içeri aktarmanız gerekir

İkincisi, `Label()` yönteminin ilk parametresinin `HtmlHelper` sınıfını temsil ettiğini unutmayın. Bir genişletme yönteminin ilk parametresi, genişletme yönteminin genişlettiği sınıfı gösterir.

**Listeleme 3 – `Helpers\LabelExtensions.vb`**

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample5.vb)]

Bir genişletme yöntemi oluşturup uygulamanızı başarılı bir şekilde oluşturduktan sonra, genişletme yöntemi bir sınıfın tüm diğer yöntemleri gibi Visual Studio IntelliSense 'de görünür (bkz. Şekil 2). Tek fark, genişletme yöntemlerinin bunların yanında özel bir simge (aşağı ok simgesi) ile görünme sayısıdır.

[HTML. Label () genişletme yöntemini kullanarak ![](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)

**Şekil 02**: HTML. Label () genişletme yöntemini kullanma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-custom-html-helpers-vb/_static/image6.png))

Liste 4 ' te değiştirilen dizin görünümü, tüm &lt;etiket&gt; etiketlerini işlemek için HTML. Label () genişletme yöntemini kullanır.

**Listeleme 4 – `Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample6.aspx)]

## <a name="summary"></a>Özet

Bu öğreticide, özel HTML Yardımcıları oluşturmak için iki yöntem öğrendiniz. İlk olarak, bir dize döndüren paylaşılan bir yöntem oluşturarak özel bir `Label()` HTML Yardımcısı oluşturmayı öğrendiniz. Daha sonra, `HtmlHelper` sınıfında bir genişletme yöntemi oluşturarak özel bir `Label()` HTML Yardımcısı yöntemi oluşturmayı öğrendiniz.

Bu öğreticide son derece basit bir HTML yardımcı yöntemi oluşturmaya odaklandım. Bir HTML Yardımcısı 'nın istediğiniz kadar karmaşık olduğunu fark edebilirsiniz. Ağaç görünümleri, menüler veya veritabanı verilerinin tabloları gibi zengin içerik işleyen HTML Yardımcıları oluşturabilirsiniz.

> [!div class="step-by-step"]
> [Önceki](asp-net-mvc-views-overview-vb.md)
> [İleri](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
