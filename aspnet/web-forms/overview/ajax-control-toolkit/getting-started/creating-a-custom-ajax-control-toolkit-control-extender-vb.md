---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
title: Özel AJAX denetim araç seti denetim Genişleticisi oluşturma (VB) | Microsoft Docs
author: microsoft
description: Özel genişleticiler, yeni sınıflar oluşturmaya gerek kalmadan ASP.NET denetimlerinin yeteneklerini özelleştirmenizi ve genişletmenizi sağlar.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 18b29834-c991-4e0c-b533-44d358fbfc9c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: 0849fa6c13679e0cd01bb20a4067a097acbce298
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578164"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-vb"></a>Özel AJAX Denetim Araç Seti Denetim Genişleticisi Oluşturma (VB)

[Microsoft](https://github.com/microsoft) tarafından

> Özel genişleticiler, yeni sınıflar oluşturmaya gerek kalmadan ASP.NET denetimlerinin yeteneklerini özelleştirmenizi ve genişletmenizi sağlar.

Bu öğreticide, özel bir AJAX denetim araç seti denetim genişletici oluşturmayı öğreneceksiniz. Bir metin kutusuna metin yazdığınızda bir düğmenin durumunu devre dışı iken etkin olarak değiştiren basit, ancak kullanışlı, yeni bir genişletici oluşturuyoruz. Bu öğreticiyi okuduktan sonra, ASP.NET AJAX araç takımını kendi denetim genişleticisiyle genişletebilirsiniz.

Visual Studio veya Visual Web Developer 'ı kullanarak özel denetim Genişleticileri oluşturabilirsiniz (Visual Web Developer 'ın en son sürümüne sahip olduğunuzdan emin olun).

## <a name="overview-of-the-disabledbutton-extender"></a>DisabledButton genişleticisini genel bakış

Yeni denetim genişleticimiz, DisabledButton genişletici olarak adlandırılmıştır. Bu genişletici 'in üç özelliği olacaktır:

- TargetControlID-denetimin genişlettiği metin kutusu.
- TargetButtonIID-devre dışı bırakılmış veya etkin olan düğme.
- DisabledText-düğme içinde başlangıçta görüntülenen metin. Yazmaya başladığınızda düğme metin özelliğinin değerini görüntüler.

DisabledButton genişleticisini bir TextBox ve Button denetimine kanca. Herhangi bir metin yazmadan önce, düğme devre dışı bırakılır ve metin kutusu ve düğme şuna benzer şekilde görünür:

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image1.png)

([Tam boyutlu görüntüyü görüntülemek Için tıklayın](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image3.png))

Metin yazmaya başladıktan sonra düğme etkinleştirilir ve metin kutusu ve düğme şuna benzer:

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image4.png)

([Tam boyutlu görüntüyü görüntülemek Için tıklayın](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image6.png))

Denetim genişleticimizi oluşturmak için aşağıdaki üç dosyayı oluşturmamız gerekir:

- DisabledButtonExtender. vb-bu dosya, Extender 'nizi oluşturmayı yönetecek ve tasarım zamanında özellikleri ayarlamanıza olanak tanıyan sunucu tarafı denetim sınıfıdır. Ayrıca, Extender 'ınızda ayarlanmakta olabilecek özellikleri de tanımlar. Bu özelliklere kod ve tasarım zamanı aracılığıyla erişilebilir ve DisableButtonBehavior. js dosyasında tanımlanan özellikler eşleşir.
- DisabledButtonBehavior. js--bu dosya, tüm istemci komut dosyası mantığınızı ekleyeceğiniz yerdir.
- DisabledButtonDesigner. vb-Bu sınıf tasarım zamanı işlevselliğine izin vermez. Denetim genişletici 'in Visual Studio/Visual Web Developer Designer ile düzgün çalışmasını istiyorsanız bu sınıfa ihtiyacınız vardır.

Bu nedenle, bir denetim genişletici sunucu tarafı denetiminden, istemci tarafı davranışından ve sunucu tarafı Tasarımcı sınıfından oluşur. Aşağıdaki bölümlerde bu dosyaların üçünü de nasıl oluşturacağınızı öğrenirsiniz.

## <a name="creating-the-custom-extender-website-and-project"></a>Özel genişletici Web sitesi ve projesi oluşturma

İlk adım, Visual Studio/Visual Web Developer 'da bir sınıf kitaplığı projesi ve Web sitesi oluşturmaktır. Özel genişletici 'i sınıf kitaplığı projesinde oluşturacağız ve özel genişletici 'i Web sitesinde test eteceğiz.

Web sitesi ile başlayalım. Web sitesini oluşturmak için aşağıdaki adımları izleyin:

1. **Yeni Web sitesi**menü seçenek dosyasını seçin.
2. **ASP.NET Web sitesi** şablonunu seçin.
3. Yeni Web sitesini *websitesi1*olarak adlandırın.
4. **Tamam** düğmesine tıklayın.

Daha sonra, denetim genişleticisini içeren sınıf kitaplığı projesini oluşturuyoruz:

1. Menü seçenek **dosyası, Ekle, yeni proje '** yi seçin.
2. **Sınıf kitaplığı** şablonunu seçin.
3. Yeni sınıf kitaplığını **Customextenders**adıyla adlandırın.
4. **Tamam** düğmesine tıklayın.

Bu adımları tamamladıktan sonra, Çözüm Gezgini pencerenizin Şekil 1 gibi görünmesi gerekir.

[Web sitesi ve sınıf kitaplığı projesiyle ![çözüm](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image7.png)

**Şekil 01**: Web sitesi ve sınıf kitaplığı projesiyle çözüm ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image9.png))

Ardından, gerekli tüm derleme başvurularını sınıf kitaplığı projesine eklemeniz gerekir:

1. CustomExtenders projesine sağ tıklayın ve ardından **Başvuru Ekle**menü seçeneğini belirleyin.
2. .NET sekmesini seçin.
3. Aşağıdaki derlemelere başvurular ekleyin:

    1. System.Web.dll
    2. System. Web. Extensions. dll
    3. System. Design. dll
    4. System. Web. Extensions. Design. dll
4. Tarayıcı sekmesini seçin.
5. AjaxControlToolkit. dll derlemesine bir başvuru ekleyin. Bu derleme, AJAX denetim araç setini indirdiğiniz klasörde bulunur.

Projenize sağ tıklayıp Özellikler ' i seçip başvurular sekmesine tıklayarak tüm doğru başvuruları eklediğinizi doğrulayabilirsiniz (bkz. Şekil 2).

[![, gerekli başvuruların bulunduğu klasöre başvurur](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image10.png)

**Şekil 02**: gerekli başvuruları olan klasöre başvurur ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image12.png))

## <a name="creating-the-custom-control-extender"></a>Özel denetim genişletici oluşturma

Sınıf kitaplımuzu öğrendiğimiz için, Extender denetiimizi oluşturmaya başlayabiliriz. Özel bir genişletici denetim sınıfının tam kemikleri ile başlayalım (bkz. Listeleme 1).

**Listeleme 1-Mycustomexödeme. vb**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample1.vb)]

Liste 1 ' de denetim genişletici sınıfı hakkında fark ettiğiniz birkaç şey vardır. İlk olarak, sınıfın temel ExtenderControlBase sınıfından türediğine dikkat edin. Tüm AJAX denetim araç seti genişletici denetimleri bu temel sınıftan türetilir. Örneğin, temel sınıf her denetim genişletici 'in gerekli bir özelliği olan targetID özelliğini içerir.

Daha sonra, sınıfının istemci betiği ile ilgili aşağıdaki iki özniteliği içerdiğine dikkat edin:

- WebResource-bir dosyanın bir derlemeye gömülü kaynak olarak eklenmesine neden olur.
- ClientScriptResource-bir kod kaynağının bir derlemeden alınmasına neden olur.

WebResource özniteliği, özel genişletici derlendiğinde MyControlBehavior. js JavaScript dosyasını derlemeye eklemek için kullanılır. ClientScriptResource özniteliği, özel genişletici bir Web sayfasında kullanıldığında derlemeden MyControlBehavior. js betiğini almak için kullanılır.

WebResource ve ClientScriptResource özniteliklerinin çalışması için, JavaScript dosyasını gömülü bir kaynak olarak derlemeniz gerekir. Çözüm Gezgini penceresinde dosyayı seçin, özellik sayfasını açın ve **derleme eylemi** özelliğine *katıştırılmış kaynak* değerini atayın.

Denetim genişleticisini de bir TargetControlType özniteliği içerdiğine dikkat edin. Bu öznitelik, denetim Genişleticisi tarafından genişletilen denetimin türünü belirtmek için kullanılır. Liste 1 ' de, bir metin kutusunu genişletmek için denetim uzatması kullanılır.

Son olarak, özel genişleticin MyProperty adlı bir özellik içerdiğine dikkat edin. Özelliği ExtenderControlProperty özniteliğiyle işaretlenir. GetPropertyValue () ve SetPropertyValue () yöntemleri, özellik değerini sunucu tarafı denetim genişleticisini istemci tarafı davranışına geçirmek için kullanılır.

Şimdi çalışmaya devam edin ve DisabledButton genişlemizin için kodu uygulayın. Bu genişletici için kod, liste 2 ' de bulunabilir.

**Listeleme 2-DisabledButtonExtender. vb**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample2.vb)]

Liste 2 ' deki DisabledButton genişletici, Targetbuttonıd ve DisabledText adlı iki özelliğe sahiptir. Targetbuttonıd özelliğine uygulanan ıdreferenceproperty, bu özelliğe bir düğme denetimi KIMLIĞI dışında bir şey atamaktan izin vermez.

WebResource ve ClientScriptResource öznitelikleri, bu Genişletici ile DisabledButtonBehavior. js adlı bir dosyada bulunan bir istemci tarafı davranışını ilişkilendirir. Sonraki bölümde bu JavaScript dosyasını tartıştık.

## <a name="creating-the-custom-extender-behavior"></a>Özel genişletici davranışı oluşturma

Denetim genişleticinizin istemci tarafı bileşenine davranış denir. Düğmeyi devre dışı bırakma ve etkinleştirmenin gerçek mantığı, DisabledButton davranışının içindedir. Davranışın JavaScript kodu, Listeleme 3 ' te bulunur.

**Listeleme 3-DisabledButton. js**

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample3.js)]

Listeleme 3 ' teki JavaScript dosyası DisabledButtonBehavior adlı bir istemci tarafı sınıfı içerir. Sunucu tarafı ikizi gibi bu sınıf, Targetbuttonıd ve DisabledText adlı ve Get\_Targetbuttonıd/set\_Targetbuttonıd kullanarak erişebileceğiniz iki özellik içerir ve\_DisabledText/set\_DisabledText.

Initialize () yöntemi, davranış için bir KeyUp olay işleyicisini hedef öğe ile ilişkilendirir. Bu davranışla ilişkili TextBox 'a her bir harf yazdığınızda, KeyUp işleyicisi yürütülür. KeyUp işleyicisi, davranışla ilişkili TextBox 'ın herhangi bir metin içerip içermediğini bağlı olarak düğmeyi devre dışı bırakır veya devre dışı bırakır.

Kod 3 ' teki JavaScript dosyasını gömülü bir kaynak olarak derlemeniz gerektiğini unutmayın. Çözüm Gezgini penceresinde dosyayı seçin, özellik sayfasını açın ve **derleme eylemi** özelliğine *katıştırılmış kaynak* değerini atayın (bkz. Şekil 3). Bu seçenek hem Visual Studio hem de Visual Web Developer ' da kullanılabilir.

[bir JavaScript dosyasını katıştırılmış kaynak olarak ekleme ![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image13.png)

**Şekil 03**: bir JavaScript dosyasını katıştırılmış kaynak olarak ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image15.png))

## <a name="creating-the-custom-extender-designer"></a>Özel genişletici Tasarımcısı oluşturma

Extender 'imizi tamamlamaya yönelik oluşturması gereken bir son sınıf vardır. Kod 4 ' te tasarımcı sınıfını oluşturuyoruz. Bu sınıf, Extender 'ın Visual Studio/Visual Web Developer Designer ile düzgün çalışmasını sağlamak için gereklidir.

**Listeleme 4-DisabledButtonDesigner. vb**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample4.vb)]

Tasarımcı özniteliğiyle DisabledButton genişleticiyle kod 4 ' te tasarımcı ilişkilendirirsiniz. Tasarımcı özniteliğini aşağıdaki gibi DisabledButtonExtender sınıfına uygulamanız gerekir:

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample5.vb)]

## <a name="using-the-custom-extender"></a>Özel genişletici kullanma

DisabledButton denetim genişleticisini oluşturmayı tamamladığımıza göre, ASP.NET Web sitemizden kullanılması zaman vardır. İlk olarak, araç kutusu 'na özel genişletici eklememiz gerekiyor. Aşağıdaki adımları uygulayın:

1. Çözüm Gezgini penceresindeki sayfaya çift tıklayarak bir ASP.NET sayfasını açın.
2. Araç kutusuna sağ tıklayıp **öğe seç**menü seçeneğini belirleyin.
3. Araç kutusu öğelerini Seç iletişim kutusunda, CustomExtenders. dll derlemesine gidin.
4. İletişim kutusunu kapatmak için **Tamam** düğmesine tıklayın.

Bu adımları tamamladıktan sonra, DisabledButton denetim genişletici araç kutusunda görünmelidir (bkz. Şekil 4).

[Araç kutusunda DisabledButton ![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image16.png)

**Şekil 04**: araç kutusunda disabledbutton ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image18.png))

Sonra, yeni bir ASP.NET sayfası oluşturuyoruz. Aşağıdaki adımları uygulayın:

1. ShowDisabledButton. aspx adlı yeni bir ASP.NET sayfası oluşturun.
2. Bir ScriptManager 'ı sayfaya sürükleyin.
3. Sayfaya bir TextBox denetimi sürükleyin.
4. Sayfaya bir düğme denetimi sürükleyin.
5. Özellikler penceresi, düğme KIMLIĞI özelliğini <em>btnSave</em> değeri, Text özelliği ise *Save\** değerine değiştirin.

Standart ASP.NET metin kutusu ve düğme denetimi içeren bir sayfa oluşturduk.

Daha sonra, TextBox denetimini DisabledButton Genişletici ile genişletmemiz gerekir:

1. Genişletici Sihirbazı iletişim kutusunu açmak için **genişletici görevi Ekle** seçeneğini belirleyin (bkz. Şekil 5). İletişim kutusunda özel DisabledButton genişleticimizi içerdiğine dikkat edin.
2. DisabledButton Genişletici ' i seçin ve **Tamam** düğmesine tıklayın.

[Genişletici Sihirbazı iletişim kutusu ![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image19.png)

**Şekil 05**: Genişletici Sihirbazı iletişim kutusu ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image21.png))

Son olarak, DisabledButton Genişletici özelliklerini ayarlayabiliriz. TextBox denetiminin özelliklerini değiştirerek DisabledButton Extender 'ın özelliklerini değiştirebilirsiniz:

1. Tasarımcıda metin kutusunu seçin.
2. Özellikler penceresi, Extender düğümünü genişletin (bkz. Şekil 6).
3. Değeri DisabledText özelliğine ve *btnSave* değerini targetbuttonıd özelliğine atayın.

[![Genişletici özelliklerini ayarlama](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image22.png)

**Şekil 06**: Genişletici özelliklerini ayarlama ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image24.png))

Sayfayı çalıştırdığınızda (F5 tuşuna basarak) düğme denetimi başlangıçta devre dışıdır. Metin kutusuna metin girmeye başladığınızda düğme denetimi etkinleştirilir (bkz. Şekil 7).

[DisabledButton genişletici 'in eylemde ![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image25.png)

**Şekil 07**: disabledbutton genişletici eylemi ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image27.png))

## <a name="summary"></a>Özet

Bu öğreticinin amacı, AJAX denetim araç takımını özel genişletici denetimleriyle nasıl genişletebileceğinizi açıklamaktır. Bu öğreticide, basit bir DisabledButton Control genişletici oluşturduk. Bu genişletici, bir DisabledButtonExtender sınıfı, DisabledButtonBehavior JavaScript davranışı ve DisabledButtonDesigner sınıfı oluşturarak uyguladık. Özel bir denetim genişletici oluşturduğunuzda benzer bir adım kümesini takip edersiniz.

> [!div class="step-by-step"]
> [Öncekini](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)
