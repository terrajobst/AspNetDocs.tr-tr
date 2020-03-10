---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
title: AJAX denetim araç seti ile çalışmaya başlama (VB) | Microsoft Docs
author: microsoft
description: AJAX denetim araç setini kullanmaya başlamak için bilmeniz gereken her şey hakkında bilgi edinin.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 9f8fa166-49a2-402c-b236-20caef0c658f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
msc.type: authoredcontent
ms.openlocfilehash: ff614308555b31710b11f408e12e9a6fadbf98d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613486"
---
# <a name="get-started-with-the-ajax-control-toolkit-vb"></a>AJAX Denetim Araç Seti ile Çalışmaya Başlama (VB)

[Microsoft](https://github.com/microsoft) tarafından

> AJAX denetim araç setini kullanmaya başlamak için bilmeniz gereken her şey hakkında bilgi edinin.

AJAX denetim araç seti, ASP.NET uygulamalarınızda kullanabileceğiniz 30 ' dan fazla ücretsiz denetim içerir. Bu öğreticide, AJAX denetim araç setini indirme ve araç seti denetimlerini Visual Studio/Visual Web Developer Express araç kutusu 'na ekleme hakkında bilgi edineceksiniz.

## <a name="downloading-the-ajax-control-toolkit"></a>AJAX denetim araç seti indiriliyor

[AJAX denetim araç seti](http://devexpress.com/act) , ASP.net community ve ASP.net ekibinin üyeleri tarafından geliştirilen açık kaynaklı bir projem.

[AJAX denetim araç setini Indirmek ![](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)

**Şekil 01**: AJAX denetim araç seti indiriliyor ([tam boyutlu görüntüyü görüntülemek için tıklayın](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png))

Dosyayı indirdikten sonra dosyanın engellemesini kaldırmanız gerekir. Dosyaya sağ tıklayın, Özellikler ' i seçin ve **Engellemeyi kaldır** düğmesine tıklayın (bkz. Şekil 2).

[AJAX denetim araç seti ZIP dosyasının engellemesini kaldırma ![](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)

**Şekil 02**: AJAX denetim araç seti ZIP dosyasının engellemesini kaldırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png))

Dosyanın engellemesini kaldırdıktan sonra, dosyayı açabilir: dosyaya sağ tıklayıp **Tümünü Ayıkla** menü seçeneğini belirleyin. Şimdi, araç takımını Visual Studio/Visual Web Developer araç kutusu 'na eklemeye hazırız.

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a>Araç kutusuna AJAX denetim araç seti ekleme

AJAX denetim araç takımını kullanmanın en kolay yolu, araç takımını Visual Studio/Visual Web Developer araç kutusu 'na eklemektir (bkz. Şekil 3). Bu şekilde, yalnızca bir araç seti denetimini kullanmak istediğinizde bir sayfaya sürükleyebilirsiniz.

[Araç kutusu 'nda ![AJAX denetim araç seti görüntülenir](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)

**Şekil 03**: araç kutusu 'Nda AJAX denetim araç seti görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png))

İlk olarak, araç kutusu 'na bir AJAX denetim araç seti sekmesi eklemeniz gerekir. Şu adımları izleyin.

1. Yeni Web sitesi olan menü seçenek dosyasını seçerek yeni bir ASP.NET Web sitesi oluşturun. Dosyayı düzenleyicide açmak için Çözüm Gezgini penceresindeki default. aspx dosyasına çift tıklayın.
2. Genel sekmesinin altındaki araç kutusu ' na sağ tıklayın ve **Sekme Ekle** menü seçeneğini belirleyin (bkz. Şekil 4).
3. AJAX denetim araç seti adlı yeni bir sekme girin.

[Yeni sekme ekleme ![](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)

**Şekil 04**: yeni sekme ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png))

Ardından, AJAX denetim araç seti denetimlerini yeni sekmeye eklemeniz gerekir. şu adımları Izleyin:

- AJAX denetim araç seti sekmesinin altına sağ tıklayın ve öğe seçin menü seçeneğini belirleyin **(bkz. Şekil 5)** .
- AJAX denetim araç takımını sıkıştırmışın ve AjaxControlToolkit. dll derlemesini seçebileceğiniz konuma göz atın.

[araç kutusuna eklenecek öğeleri seçin ![](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)

**Şekil 05**: araç kutusuna eklenecek öğeleri seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png))

Bu adımları tamamladıktan sonra araç kutusu denetimleri araç kutusunda görünür.

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a>Araç setinin yeni bir sürümüne yükseltme

Araç setinin eski bir sürümünü kullanıyorsanız ve şu anda daha sonraki bir sürüme geçiş yapmanız gerekiyorsa önerilen adımlar şunlardır:

- İkili dosyalar-Web sitesi bin klasörünüzdeki AjaxControlToolkit. dll derlemesinin eski sürümünü silin.
- Araç kutusu öğeleri-AJAX denetim araç seti sekmesini silin ve aşağıdaki adımları izleyerek, bu sekmeyi, AjaxControlToolkit. dll derlemesinin yeni sürümü ile yeniden oluşturun.

> [!div class="step-by-step"]
> [Önceki](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
> [İleri](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)
