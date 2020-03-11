---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
title: AJAX denetim araç seti denetimlerini ve denetim Genişleticilerini kullanma (C#) | Microsoft Docs
author: microsoft
description: ASP.NET sayfalarınıza AJAX denetim araç seti denetimleri ve Extender 'ların nasıl ekleneceğini öğrenin.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: c1e6b51c-3bc3-4bf7-9916-9991197af3dd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
msc.type: authoredcontent
ms.openlocfilehash: 1acafaadaf373b488b9e85b7ba31f08cd3b53e85
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78535415"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-c"></a>AJAX Denetim Araç Seti Denetimlerini ve Denetim Genişleticilerini Kullanma (C#)

[Microsoft](https://github.com/microsoft) tarafından

> ASP.NET sayfalarınıza AJAX denetim araç seti denetimleri ve Extender 'ların nasıl ekleneceğini öğrenin.

AJAX denetim araç seti bir denetimler kümesi ve denetim Genişleticileri içerir. Bu kısa öğreticide, bir ASP.NET sayfasına hem denetimleri hem de denetim Genişleticilerini nasıl ekleyeceğinizi öğreneceksiniz.

> [!NOTE] 
> 
> AJAX denetim araç setini yükleme ve AJAX denetim araç setini Visual Studio/Visual Web Developer araç kutusu 'na ekleme hakkında yönergeler için bkz. [AJAX denetim araç seti Ile çalışmaya başlama](get-started-with-the-ajax-control-toolkit-cs.md)öğreticisi.

## <a name="using-ajax-control-toolkit-controls"></a>AJAX denetim araç seti denetimlerini kullanma

AJAX denetim araç seti denetimi normal bir ASP.NET denetimi gibi çalışmaktadır. Denetimi araç kutusundan bir ASP.NET sayfasına sürükleyebilirsiniz. Denetimi sayfaya Tasarım görünümü veya kaynak görünümünde ekleyebilirsiniz.

AJAX denetim araç setinde denetimleri kullanırken bir özel gereksinim vardır. Sayfa bir ScriptManager denetimi içermelidir. ScriptManager Denetim araç seti denetimleri için gerekli tüm JavaScript 'ı dahil etmek için ScriptManager denetimi sorumludur.

Örneğin, AJAX denetim araç seti sekmesi, düzenleyici denetimi adında bir denetim içerir. Bu denetim zengin bir HTML Düzenleyicisi görüntüler. Bir sayfaya düzenleyici denetimi eklemek için aşağıdaki adımları izleyin:

1. Showweditor. aspx adlı yeni bir ASP.NET sayfası oluşturun
2. Araç kutusundaki AJAX Uzantıları sekmesinin altında bulunan ScriptManager denetimini seçin ve denetimi sayfaya sürükleyin.
3. Araç kutusundaki AJAX denetim araç seti sekmesinin altındaki düzenleyici denetimini seçin ve denetimi sayfaya sürükleyin (bkz. Şekil 1). Tasarımcı Şekil 2 gibi görünmelidir.
4. Web sitesini **Hata Ayıkla, hata ayıklamayı Başlat** veya F5 tuşuna basarak menü seçeneğini belirleyerek çalıştırın.
5. Şekil 3 ' te sayfayı görmeniz gerekir.

[HTML düzenleyici denetimini seçme ![](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)

**Şekil 01**: HTML düzenleyici denetimini seçme ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))

[Visual Studio Designer 'ı ScriptManager ve düzenleme denetimiyle ![](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)

**Şekil 02**: ScriptManager Ile Visual Studio Tasarımcısı ve düzenleme denetimi ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))

[DisplayEditor. aspx sayfasını ![](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)

**Şekil 03**: displayeditor. aspx sayfası ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))

## <a name="using-ajax-control-toolkit-control-extenders"></a>AJAX denetim araç seti denetim Genişleticilerini kullanma

AJAX denetim araç seti ayrıca denetim Genişleticilerini içerir. Adından da anlaşılacağı gibi, bir denetim genişletici var olan bir denetimin işlevselliğini genişletir. Örneğin, ConfirmButton denetim genişletici standart ASP.NET düğme denetimini genişletir. Genişletici düğme denetimi davranışını değiştirir, böylece düğme, düğmeye tıkladığınızda bir onay iletişim kutusu görüntüler.

AJAX denetim araç seti denetiminde olduğu gibi bir denetim Genişleticisi, ScriptManager denetimi gerektirir. Sayfada denetim Genişleticilerini kullanmaya başlamadan önce sayfaya bir ScriptManager denetimi eklemeniz gerekir.

ConfirmButton denetim genişletici 'i kullanmak için şu adımları izleyin:

1. ShowConfirmButton. aspx adlı yeni bir ASP.NET sayfası oluşturun
2. Denetimi, AJAX Uzantıları sekmesinin altındaki sayfaya sürükleyerek sayfaya bir ScriptManager denetimi ekleyin.
3. Araç kutusundaki Standart Sekmenin altındaki düğmeyi tasarımcı yüzeyine sürükleyerek sayfaya standart düğme denetimi ekleyin.
4. Genişletici görevi **Ekle** seçeneğine tıklayın (bkz. Şekil 4).
5. Genişletici Seç iletişim kutusunda ConfirmButtonExtender (Şekil 5 ' e bakın) öğesini seçin ve Tamam düğmesine tıklayın.
6. Tasarımcıda düğme denetimini seçin ve Özellikler penceresi Extender, Button1\_ConfirmButtonExtender düğümünü genişletin (bkz. Şekil 6). Değeri *gerçekten?* ConfirmText özelliğine atayın.
7. **Hata Ayıkla, hata ayıklamayı Başlat** veya F5 tuşuna basın menü seçeneğini belirleyerek sayfayı çalıştırın.

[Genişletici görevi Ekle seçeneği ![](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)

**Şekil 04**: Genişletici görevi Ekle seçeneği ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))

[ConfirmButton denetim genişletici ![seçme](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)

**Şekil 05**: ConfirmButton Control genişletici seçme ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))

[ConfirmButton özelliği ayarlama ![](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)

**Şekil 06**: ConfirmButton özelliğini ayarlama ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))

Sayfa açıldığında bir düğme görmeniz gerekir. Düğmeye tıkladığınızda, Şekil 7 ' de onay iletişim kutusunu alırsınız.

[onay iletişim kutusunu görüntüleme ![](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)

**Şekil 07**: onay iletişim kutusunu görüntüleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))

Normalde bir denetim genişleticisini bir sayfaya sürükleytiğine dikkat edin. Bunun yerine, bir sayfaya daha önce eklediğiniz bir denetime genişletici eklemek için **genişletici görevi Ekle** seçeneğini kullanın. Ayrıca, denetim Genişletici özelliklerini genişletmekte olan denetimin özellik sayfasını açarak ayarlayabildiğinize de dikkat edin.

Tek bir ASP.NET denetimi, birden çok denetim Genişleticileri tarafından genişletilebilir. Genişletilmekte olan denetimin özellik sayfası denetimle ilişkili tüm denetim Genişleticilerini listeler.

> [!div class="step-by-step"]
> [Önceki](get-started-with-the-ajax-control-toolkit-cs.md)
> [İleri](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
