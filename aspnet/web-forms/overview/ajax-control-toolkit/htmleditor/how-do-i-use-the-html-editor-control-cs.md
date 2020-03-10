---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
title: Nasıl yaparım? HTML düzenleyici denetimini mi kullanıyorsunuz? (C#) | Microsoft Docs
author: microsoft
description: Htmtaditor, bir araç çubuğundaki düğmeler aracılığıyla HTML içeriğini kolayca oluşturmanıza ve düzenlemenize olanak tanıyan bir ASP.NET AJAX denetimidir.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: f47e6224-c2e5-4472-b069-b6c7b6115200
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
msc.type: authoredcontent
ms.openlocfilehash: cb7d75b59b1361abeb6d3c38ad6e42e34d6e3f7b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78577863"
---
# <a name="how-do-i-use-the-html-editor-control-c"></a>Nasıl yaparım? HTML düzenleyici denetimini mi kullanıyorsunuz? (C#)

[Microsoft](https://github.com/microsoft) tarafından

> Htmtaditor, bir araç çubuğundaki düğmeler aracılığıyla HTML içeriğini kolayca oluşturmanıza ve düzenlemenize olanak tanıyan bir ASP.NET AJAX denetimidir.

Bu öğreticinin amacı, AJAX denetim araç seti 'ne dahil edilen HTML düzenleyici denetimine genel bir bakış sunmaktır. HTML Düzenleyicisi, yazı tipi boyutunu değiştirme, yazı tipi seçme, arka plan rengini değiştirme, ön plan rengini değiştirme, bağlantılar ekleme, görüntü ekleme, metin hizalamasını değiştirme ve kesme, kopyalama ve yapıştırma işlemleri gerçekleştirme seçeneklerini içerir (bkz. Şekil 1).

[HTML düzenleyicisini ![](how-do-i-use-the-html-editor-control-cs/_static/image1.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image1.png)

**Şekil 01**: HTML Düzenleyicisi ([tam boyutlu görüntüyü görüntülemek için tıklayın](how-do-i-use-the-html-editor-control-cs/_static/image2.png))

HTML Düzenleyicisi, Tasarım modunu kullanarak içerik girmenizi sağlar veya doğrudan HTML girebilirsiniz. Ayrıca, HTML içeriğinizi Önizleme seçeneği sunulur (bkz. Şekil 2).

[![tasarım, HTML ve önizleme düğmeleri](how-do-i-use-the-html-editor-control-cs/_static/image2.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image3.png)

**Şekil 02**: TASARıM, HTML ve önizleme düğmeleri ([tam boyutlu görüntüyü görüntülemek için tıklayın](how-do-i-use-the-html-editor-control-cs/_static/image4.png))

Bu öğreticide, HTML düzenleyicisini görüntülemeyi, HTML düzenleyicisinde görünen araç çubuğu düğmelerini özelleştirmeyi ve siteler arası betik saldırılarının nasıl önleneceğini öğreneceksiniz.

## <a name="displaying-the-html-editor"></a>HTML düzenleyicisini görüntüleme

HTML düzenleyicisini bir ASP.NET sayfasında kullanabilmeniz için önce sayfaya bir ScriptManager denetimi eklemeniz gerekir. ScriptManager denetimi, Visual Studio/Visual Web Developer Express araç kutusundaki AJAX Uzantıları sekmesinin altında bulunur.

Sayfadaki diğer denetimlerden önce, ScriptManager denetimini sayfanın en üstüne yerleştirmeniz gerekir. Örneğin, bunu açılan sunucu tarafı &lt;formu&gt; etiketinin hemen altına yerleştirebilirsiniz.

HTML Düzenleyicisi denetimi, geri kalan AJAX denetim araç seti denetimleriyle birlikte araç kutusunda bulunur. Düzenleyici denetimi olarak adlandırılır (bkz. Şekil 3).

[HTML Düzenleyicisi denetimini ![](how-do-i-use-the-html-editor-control-cs/_static/image3.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image5.png)

**Şekil 03**: HTML düzenleyici denetimi ([tam boyutlu görüntüyü görüntülemek için tıklayın](how-do-i-use-the-html-editor-control-cs/_static/image6.png))

HTML düzenleyicisini bir sayfaya sürükledikten sonra özellik sayfasında özelliklerini ayarlayabilirsiniz. Örneğin, normalde genişlik ve yükseklik özelliklerini ayarlamak istersiniz. Listeleme 1, HTML Düzenleyicisi içeren bir ASP.NET sayfasının kaynağını içerir.

**Listeleme 1-SimpleEditor. aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample1.aspx)]

Listeleme 1 ' deki sayfa bir HTML düzenleyici denetimi, bir düğme denetimi ve bir değişmez değer denetimi içerir. Düğmeye tıkladığınızda, HTML düzenleyicisinin içeriği değişmez denetimde görünür (bkz. Şekil 4).

[HTML Düzenleyicisi ile form gönderme ![](how-do-i-use-the-html-editor-control-cs/_static/image4.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image7.png)

**Şekil 04**: HTML düzenleyiciyle form gönderme ([tam boyutlu görüntüyü görüntülemek için tıklayın](how-do-i-use-the-html-editor-control-cs/_static/image8.png))

HTML düzenleyici Içerik özelliği, HTML düzenleyicisine girilen HTML içeriğini almak için kullanılır. Bu HTML içeriğinin JavaScript içeremeyeceğini unutmayın. Sonraki bölümde, JavaScript ekleme saldırılarını nasıl önleyebiliriz.

## <a name="customizing-the-html-editor-toolbar"></a>HTML Düzenleyici araç çubuğunu özelleştirme

Düzenleyicide görüntülenecek düğmeleri tam olarak özelleştirebilirsiniz. Örneğin, kullanıcıların HTML düzenleyicisini HTML moduna geçişini engellemek için HTML sekmesini kaldırmak isteyebilirsiniz. Ya da kullanıcıların bir forum iletisi gönderisini çok büyük metin oluşturmasını engellemek için yazı tipi boyutu açılır listesini kaldırmak isteyebilirsiniz (bkz. Şekil 5).

[özelleştirilmiş bir HTML Düzenleyicisi ![](how-do-i-use-the-html-editor-control-cs/_static/image5.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image9.png)

**Şekil 05**: ÖZELLEŞTIRILMIŞ bir HTML Düzenleyicisi ([tam boyutlu görüntüyü görüntülemek için tıklayın](how-do-i-use-the-html-editor-control-cs/_static/image10.png))

Araç çubuğu düğmelerini, temel düzenleyici sınıfından yeni bir HTML Düzenleyicisi türeterek özelleştirebilirsiniz. Örneğin, liste 2 ' deki özel düzenleyici yalnızca kalın ve italik için araç çubuğu düğmelerini içerir. Diğer tüm araç çubuğu düğmeleri kaldırılmıştır. Ayrıca, HTML sekmesi düzenleyicinin altından kaldırılmıştır (ancak tasarım ve önizleme sekmeleri hala orada bulunur).

**Listeleme 2-uygulama\_Code\CustomEditor.cs**

[!code-csharp[Main](how-do-i-use-the-html-editor-control-cs/samples/sample2.cs)]

Sınıfın otomatik olarak derlenmesi için liste 2 ' deki sınıfı App\_Code klasörünüze eklemeniz gerekir. Uygulama\_kodu klasörü Web sitenizde yoksa, klasörü eklemeniz yeterlidir.

Özel bir düzenleyici oluşturduktan sonra, normal HTML düzenleyicisini eklerken aynı şekilde bir ASP.NET sayfasına ekleyebilirsiniz (bkz. Listeleme 3).

**Listeleme 3-ShowCustomEditor. aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a>Siteler arası komut dosyası (XSS) saldırılarını önleme

Bir kullanıcıdan girişi kabul ettiğinizde ve bu girişi Web sitenizde yeniden görüntülerseniz, Web sitenizi siteler arası betik oluşturma (XSS) saldırılarına açık olarak açabilirsiniz. Teorik olarak, kötü niyetli bir korsan, giriş yeniden görüntülendiğinde yürütülen JavaScript kodunu gönderebilir. JavaScript, Kullanıcı parolalarını veya diğer gizli bilgileri çalmak için kullanılabilir.

Normalde, bir kullanıcıdan bir Web sayfasında görüntülemeden önce aldığınız herhangi bir girişi HTML kodlaması ile, XSS saldırılarını erteleyerek bu işlemi gerçekleştirebilirsiniz. Bununla birlikte, HTML düzenleyicisinin çıkışı yalnızca &lt;betiği&gt; etiketlerini kodlayıp, tüm HTML etiketlerini de kodlayacağından HTML kodlaması. Diğer bir deyişle, yazı tipi türü, yazı tipi boyutu ve arka plan rengi gibi tüm biçimlendirmeyi kaybedersiniz.

Kullanıcılarınızın gizli bilgilerini (parolalar, kredi kartı numaraları ve sosyal güvenlik numaraları gibi) topluyorsanız, bir kullanıcıdan HTML düzenleyiciyle aldığınız, kodlanmamış içeriği görüntülememelisiniz. HTML düzenleyicisini yalnızca, HTML içeriğini yeniden görüntülemediğiniz durumlarda veya HTML içeriğinin güvenilen bir taraf tarafından Web sitenize gönderilme durumunda kullanmanız gerekir.

Örneğin, bir blog uygulaması oluşturduğunuzu düşünün. Bu durumda, blog gönderilerini oluştururken HTML düzenleyicisini kullanmak mantıklı olur. Yalnızca bir blog gönderisi gönderen ve bu, kötü amaçlı JavaScript gönderebilme konusunda kendinize güvenmediğiniz tek bir Web siz olursunuz. Ancak, anonim kullanıcıların yorum gönderenlere izin verirken HTML düzenleyicisini kullanmak mantıklı değildir. Özellikle kullanıcıların parolalar gibi hassas bilgileri göndermesi durumunda dikkatli olmanız gerekir. Kötü niyetli bir Kullanıcı, bir parolayı çalmak için doğru JavaScript içeren bir yorum gönderebilir.

## <a name="summary"></a>Özet

Bu öğreticide, AJAX denetim araç seti 'ne dahil edilen HTML düzenleyici denetimine ilişkin kısa bir genel bakış sunulmaktadır. Bir kullanıcının zengin içeriğini kabul etmek ve içeriği sunucuya göndermek için HTML Düzenleyicisi 'ni nasıl kullanacağınızı öğrendiniz. Ayrıca, HTML Düzenleyicisi tarafından görüntülenen araç çubuğu düğmelerini nasıl özelleştirebileceğinizi de tartıştık. Son olarak, olası kötü amaçlı girişi kabul etmek için HTML düzenleyicisini kullanırken siteler arası betik saldırılarının nasıl önleneceğini öğrendiniz.

> [!div class="step-by-step"]
> [Next](how-do-i-use-the-html-editor-control-vb.md)
