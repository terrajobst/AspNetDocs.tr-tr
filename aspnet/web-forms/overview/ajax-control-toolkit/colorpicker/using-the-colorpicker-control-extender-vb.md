---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
title: ColorPicker denetim genişletici 'i kullanma (VB) | Microsoft Docs
author: microsoft
description: ColorPicker, bir açılan denetimde UI ile istemci tarafı renk seçme işlevselliği sağlayan bir ASP.NET AJAX genişleticisi. Herhangi bir ASP.NET bağlanabilir...
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 577ae07b-a872-4818-a804-bca489b40ad0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: 77e2e3bc61a5e1498570959ca40acff83dc3fc82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554504"
---
# <a name="using-the-colorpicker-control-extender-vb"></a>ColorPicker denetim genişletici (VB) kullanma

[Microsoft](https://github.com/microsoft) tarafından

> ColorPicker, bir açılan denetimde UI ile istemci tarafı renk seçme işlevselliği sağlayan bir ASP.NET AJAX genişleticisi. Herhangi bir ASP.NET metin kutusu denetimine eklenebilir. İçerdiği.

Bu öğreticinin amacı, AJAX denetim araç seti ColorPicker denetim Genişletici ' i nasıl kullanabileceğinizi açıklamaktır. ColorPicker denetim genişletici bir renk seçmenizi sağlayan bir açılan pencere iletişim kutusu görüntüler. Kullanıcının bir renk seçmesini sağlayacak sezgisel bir kullanıcı arabirimi sağlamak istediğinizde ColorPicker yararlı olur.

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a>ColorPicker denetim Genişletici ile TextBox denetimini genişletme

Örneğin, ziyaretçilerin özelleştirilmiş iş kartları oluşturmalarına olanak tanıyan bir Web sitesi oluşturmak istediğinizi varsayalım. Ziyaretçiler bir iş kartının metnini girebilir ve rengi seçebilir. Liste 1 ' deki ASP.NET sayfası, txtCardText ve txtCardColor adlı iki TextBox denetimini içerir. Formu gönderdiğinizde, seçilen değerler görüntülenir (bkz. Şekil 1).

[iş kartı oluşturmaya yönelik basit form ![](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)

**Şekil 01**: iş kartı oluşturmaya yönelik basit form ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-the-colorpicker-control-extender-vb/_static/image2.png))

**Listeleme 1-CreateCard. aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample1.aspx)]

Listeleme 1 ' deki form işe yarar, ancak harika bir kullanıcı deneyimi sağlamıyor. Kullanıcı TextBox içine bir renk yazmak zorunda. Kullanıcı, özel bir renk isterse, örneğin, PEA 'nın yalnızca doğru tonu varsa, Kullanıcı HTML renk kodunu herhangi bir yardım olmadan saymalıdır.

Daha iyi bir kullanıcı deneyimi oluşturmak için ColorPicker denetim Genişletici ' i kullanabilirsiniz. Bir TextBox denetimine odak taşıdığınızda ColorPicker bir Color iletişim kutusu görüntüler (bkz. Şekil 2).

[ColorPicker denetim genişletici ![](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)

**Şekil 02**: ColorPicker denetim Genişleticisi ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-the-colorpicker-control-extender-vb/_static/image4.png))

ColorPicker denetim genişletici 'i liste 1 ' deki formla birlikte kullanmak için iki adımı tamamlamalısınız:

1. Sayfaya bir ScriptManager denetimi ekleyin
2. ColorPicker denetim genişletici 'i sayfaya ekleyin

ColorPicker 'ı kullanabilmeniz için, sayfanıza bir ScriptManager eklemeniz gerekir. Sağ taraftaki sunucu tarafı &lt;formu&gt; etiketinin altına ScriptManager eklemek için iyi bir yer vardır. Araç kutusu 'ndan ScriptManager 'ı sayfaya sürükleyebilirsiniz (ScriptManager, AJAX Uzantıları sekmesinin altında bulunur). Alternatif olarak, sunucu tarafı açma formu etiketinin altındaki kaynak görünümüne aşağıdaki etiketi yazabilirsiniz:

&lt;ASP: ScriptManager ID = "ScriptManager1" runat = "Server"/&gt;

ColorPicker denetim genişletici 'i sayfaya eklemenin en kolay yolu tasarım görünümüdür. Farenizi txtCardColor metin kutusunun üzerine getirdiğinizde, bir genişletici eklemenize olanak tanıyan bir akıllı görev seçeneği görüntülenir (bkz. Şekil 3). Bu seçeneği belirlerseniz, genişletici Sihirbazı görüntülenir (bkz. Şekil 4).

[Genişletici ekleme ![](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)

**Şekil 03**: Genişletici ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-the-colorpicker-control-extender-vb/_static/image6.png))

[Genişletici sihirbazıyla denetim genişletici 'i seçme ![](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)

**Şekil 04**: Genişletici sihirbazıyla bir denetim genişletici seçme ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-the-colorpicker-control-extender-vb/_static/image8.png))

Yok Cardcolor metin kutusunu ColorPicker Genişletici ile genişletmek için ColorPicker Genişletici ' i seçebilirsiniz. İletişim kutusunu kapatmak için Tamam ' ı tıklatın.

Bu değişiklikleri yaptıktan sonra, sayfanın kaynağı liste 2 gibi görünür.

**Listeleme 2-CreateCard. aspx (ColorPicker ile)**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample2.aspx)]

Sayfanın şimdi, txtCardColor metin kutusu denetiminin hemen altında görünen bir Colorpickergenişletici denetimi içerdiğine dikkat edin. Colorpickergenişletici denetimi, bir renk seçici iletişim kutusu görüntüleyecek şekilde txtCardColor denetimini genişletir.

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a>Renk seçici Iletişim kutusunu başlatmak için düğme kullanma

ColorPicker genişletici aşağıdaki özellikleri destekler:

- Popupbuttonıd-sayfadaki, Renk Seçici iletişim kutusunun görünmesine neden olan bir düğmenin KIMLIĞI.
- PopupPosition-Renk Seçici iletişim kutusunun hedef denetimine göre konumu. Olası değerler şunlardır. mutlak, orta, BottomLeft, BottomRight, TopLeft, Toprime, Right ve Left (varsayılan, BottomLeft).
- Samplecontrolıd-seçili rengi görüntüleyen bir denetimin KIMLIĞI.
- SelectedColor-ColorPicker tarafından seçilen başlangıç rengi.

Renk Seçici iletişim kutusunun nasıl görüntülendiğini ve seçilen rengin nasıl görüntülendiğini özelleştirmek için bu özellikleri kullanabilirsiniz. Kod 3 ' teki sayfa bu özelliklerden birkaçını nasıl kullanabileceğinizi gösterir.

**Listeleme 3-CreateCardButton. aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample3.aspx)]

Listeleme 3 ' teki sayfa bir renk seç düğmesi içerir (bkz. Şekil 5). Bu düğmeye tıkladığınızda, TextBox üzerinde renk seçici iletişim kutusu görüntülenir. İletişim kutusundan bir renk seçerseniz, seçilen renk lblSample etiket denetiminin arka plan rengi olarak görünür.

ColorPicker Popupbuttonıd özelliği, çekme rengi düğmesini ColorPicker Genişletici ile ilişkilendirmek için kullanılır. Popupbuttonıd özelliği için bir değer sağlarsanız, hedef denetim odağa sahip olduğunda Renk Seçici iletişim kutusu artık görünmez. İletişim kutusunu göstermek için düğmeye tıklamanız gerekir.

Samplecontrolıd özelliği, seçili renk ile ColorPicker ile görüntülenen bir denetimi ilişkilendirmek için kullanılır. ColorPicker, bu denetimin arka plan rengini Şu anda seçili renge değiştirir.

[Renk Seçici iletişim kutusunu bir düğmeyle görüntüleme ![](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)

**Şekil 05**: Renk Seçici iletişim kutusunu bir düğmeyle görüntüleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-the-colorpicker-control-extender-vb/_static/image10.png))

## <a name="summary"></a>Özet

Bu öğreticide, bir açılan Renk Seçici iletişim kutusunu göstermek için ColorPicker denetim genişletici 'in nasıl kullanılacağını öğrendiniz. İlk olarak, odak bir TextBox denetimine taşındığında iletişim kutusunu nasıl kullanabileceğinizi inceledik. Ardından, düğme tıklandığında Renk Seçici iletişim kutusunu görüntüleyen bir düğme oluşturmayı öğrendiniz.

> [!div class="step-by-step"]
> [Öncekini](using-the-colorpicker-control-extender-cs.md)
