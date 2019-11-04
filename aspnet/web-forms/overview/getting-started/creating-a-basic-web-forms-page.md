---
uid: web-forms/overview/getting-started/creating-a-basic-web-forms-page
title: Temel ASP.NET 4,5 Web Forms sayfası oluşturmak için Visual Studio 2013 kullanma
author: Erikre
description: ''
ms.author: riande
ms.date: 03/03/2014
ms.assetid: a2f1c635-0817-4a9a-8c13-d5b5d29727c0
msc.legacyurl: /web-forms/overview/getting-started/creating-a-basic-web-forms-page
msc.type: authoredcontent
ms.openlocfilehash: 5d13a51128eecd92a82cfd06054448582a348e11
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445678"
---
# <a name="using-visual-studio-2013-to-create-a-basic-aspnet-45-web-forms-page"></a>Temel ASP.NET 4,5 Web Forms sayfası oluşturmak için Visual Studio 2013 kullanma

by [Erik Reitan](https://github.com/Erikre)

[!INCLUDE[](~/includes/rp.md)]

Bu izlenecek yol, [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) ' deki Web geliştirme ortamına ve [web için Microsoft Visual Studio Express 2013](https://www.microsoft.com/visualstudio/11/downloads#express-web)' e giriş yapmanızı sağlar. Bu izlenecek yol, basit bir ASP.NET Web Forms sayfası oluşturma sırasında size rehberlik eder ve yeni bir sayfa oluşturma, denetim ekleme ve kod yazma temel tekniklerini gösterir.

Bu izlenecek yolda gösterilen görevler şunlardır:

- Bir dosya sistemi Web Forms uygulaması projesi oluşturma.
- Visual Studio ile alıştırarak.
- ASP.NET sayfası oluşturma.
- Denetimler ekleme.
- Olay işleyicileri ekleme.
- Visual Studio 'dan bir sayfa çalıştırma ve test etme.

## <a name="prerequisites"></a>Prerequisites

Bu izlenecek yolu tamamlamak için şunlar gerekir:

- Web için [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) veya [Microsoft Visual Studio Express 2013](https://www.microsoft.com/visualstudio/11/downloads#express-web). .NET Framework otomatik olarak yüklenir. 

    > [!NOTE] 
    > 
    > Web için Microsoft Visual Studio 2013 ve Microsoft Visual Studio Express 2013, genellikle bu öğretici serisinin tamamında Visual Studio olarak adlandırılır.  
    >   
    > Visual Studio kullanıyorsanız, Bu izlenecek yol, Visual Studio 'Yu ilk kez başlattığınızda ayarların **Web geliştirme** koleksiyonunu seçtiğinizi varsayar. Daha fazla bilgi için bkz. [nasıl yapılır: Web geliştirme ortamı ayarlarını seçme](https://msdn.microsoft.com/library/ff521558.aspx).

## <a name="creating-a-web-application-project-and-a-page"></a>Web uygulaması projesi ve sayfa oluşturma

<a id="sectionToggle0"></a>

İzlenecek yolun bu bölümünde bir Web uygulaması projesi oluşturacak ve buna yeni bir sayfa ekleyeceksiniz. Ayrıca, HTML metni ekleyecek ve sayfayı tarayıcınızda çalıştıracaksınız.

### <a name="to-create-a-web-application-project"></a>Bir Web uygulaması projesi oluşturmak için

1. Microsoft Visual Studio açın.
2. **Dosya** menüsünde **Yeni proje**' yi seçin.  
    ![Dosya menüsü](creating-a-basic-web-forms-page/_static/image1.png)

    **Yeni proje** iletişim kutusu görüntülenir.
3. Soldaki -**Şablonlar** &gt; **Visual C#**  -&gt; **Web** şablonları grubunu seçin.
4. Orta sütundaki **ASP.NET Web uygulaması** şablonunu seçin.
5. Projeyi ***Basicwebapp*** olarak adlandırın ve **Tamam** düğmesine tıklayın.   
Yeni proje iletişim kutusunu ![](creating-a-basic-web-forms-page/_static/image2.png)
6. Sonra, **Web Forms** şablonunu seçin ve projeyi oluşturmak için **Tamam** düğmesine tıklayın.  
Yeni ASP.NET projesi iletişim kutusu ![](creating-a-basic-web-forms-page/_static/image3.png)  

    Visual Studio Web Forms şablonunu temel alan önceden oluşturulmuş işlevsellik içeren yeni bir proje oluşturur. Size yalnızca size bir *Home.* aspx sayfası, bir *About.* aspx sayfası, bir *Contact. aspx* sayfası ve ayrıca kullanıcıları kaydeden ve kimlik bilgilerini kaydederek Web sitenizde oturum açabilmeleri için üyelik işlevleri de içerir. Yeni bir sayfa oluşturulduğunda, varsayılan olarak Visual Studio, sayfanın HTML öğelerini görebileceğiniz **kaynak** görünümünde sayfayı görüntüler. Aşağıdaki çizimde, *Basicwebapp. aspx*adlı yeni bir Web sayfası oluşturduysanız **kaynak** görünümünde gördükleriniz gösterilmektedir.  
    ![kaynak görünümü](creating-a-basic-web-forms-page/_static/image4.png)

### <a name="a-tour-of-the-visual-studio-web-development-environment"></a>Visual Studio Web geliştirme ortamı turu

Sayfayı değiştirerek devam etmeden önce, Visual Studio geliştirme ortamı hakkında bilgi edinmek yararlı olur. Aşağıdaki çizimde, Visual Studio 'da kullanılabilen Windows ve araçlar ve Web için Visual Studio Express gösterilmektedir.

> [!NOTE] 
> 
> Bu diyagramda varsayılan pencereler ve pencere konumları gösterilmektedir. **Görünüm** menüsü, ek pencereleri görüntülemenize ve Windows 'u tercihlerinize uyacak şekilde yeniden düzenlemenize ve yeniden boyutlandırmanıza olanak sağlar. Pencere düzenlemede değişiklikler zaten yapılmışsa, gördükleriniz, çizimle eşleşmeyecektir.

 Visual Studio ortamı

![Visual Studio ortamı](creating-a-basic-web-forms-page/_static/image5.png)

### <a name="familiarize-yourself-with-the-web-designer"></a>Web tasarımcısı hakkında bilgi edinin

Yukarıdaki çizimi inceleyin ve metni, en yaygın kullanılan pencereleri ve araçları açıklayan aşağıdaki listeyle eşleştirin. (Gördüğünüz tüm pencereler ve araçlar burada listelenmemiştir ve yalnızca önceki çizimde işaretlenir.)

- Çubuklarındaki. Metin biçimlendirme, metin bulma ve benzeri komutları sağlar. Bazı araç çubukları yalnızca **Tasarım** görünümünde çalışırken kullanılabilir.
- **Çözüm Gezgini** pencere. Web uygulamanızdaki dosya ve klasörleri görüntüler.
- Belge penceresi. Sekmeli pencereler üzerinde çalışmakta olduğunuz belgeleri görüntüler. Sekmeler ' i tıklatarak belgeler arasında geçiş yapabilirsiniz.
- **Özellikler** penceresi. Sayfa, HTML öğeleri, denetimler ve diğer nesneler için ayarları değiştirmenize izin verir.
- Sekmeleri görüntüleyin. Size aynı belgenin farklı görünümlerini sunun. **Tasarım** görünümü, YAKLAŞıK bir WYSIWYG düzenlemesi yüzeyidir. **Kaynak** görünümü, sayfanın HTML düzenleyicisidir. **Bölünmüş** görünüm, belge Için hem **Tasarım** görünümünü hem de **kaynak** görünümünü görüntüler. Bu izlenecek yolda daha sonra **Tasarım** ve **kaynak** görünümleri ile çalışacaksınız. Web sayfalarını **Tasarım** görünümünde açmayı tercih ediyorsanız, **Araçlar** menüsünde **Seçenekler**' e tıklayın, **HTML Tasarımcısı** düğümünü seçin ve seçeneğinde **Başlangıç sayfaları** ' nı değiştirin.
- **Araç kutusu**. Sayfanız üzerine sürükleyebileceğiniz denetimler ve HTML öğeleri sağlar. **Araç kutusu** öğeleri ortak işleve göre gruplandırılır.
- S **nucu Gezgini**. Veritabanı bağlantılarını görüntüler. Sunucu Gezgini görünmüyorsa, Görünüm menüsünde Sunucu Gezgini ' a tıklayın.

### <a name="creating-a-new-aspnet-web-forms-page"></a>Yeni bir ASP.NET Web Forms sayfası oluşturma

**ASP.NET Web uygulaması** proje şablonunu kullanarak yeni bir Web Forms uygulaması oluşturduğunuzda, Visual Studio *varsayılan. aspx*adlı bir ASP.NET sayfası (Web Forms sayfası) ve diğer birçok dosya ve klasör ekler. Web uygulamanızın giriş sayfası olarak *default. aspx* sayfasını kullanabilirsiniz. Bununla birlikte, Bu anlatım için yeni bir sayfa oluşturacak ve bunlarla çalışacaksınız.

### <a name="to-add-a-page-to-the-web-application"></a>Web uygulamasına bir sayfa eklemek için

1. *Default. aspx* sayfasını kapatın. Bunu yapmak için, dosya adını görüntüleyen sekmeye tıklayın ve ardından Kapat seçeneğine tıklayın.
2. **Çözüm Gezgini**, Web uygulaması adına (Bu öğreticide, uygulama adı **basicwebsite**) sağ tıklayın ve ardından **Yeni öğe**&gt; -**Ekle** ' ye tıklayın.   
**Yeni öğe Ekle** iletişim kutusu görüntülenir.
3. Sol taraftaki **Visual C#**  -&gt; **Web** şablonları grubunu seçin. Ardından, ortadaki listeden **Web formu** ' nu seçin ve *firstweb sayfası. aspx*olarak adlandırın.   
    ![yeni öğe Ekle iletişim kutusu](creating-a-basic-web-forms-page/_static/image6.png)
4. Web sayfasını projenize eklemek için **Ekle** ' ye tıklayın.  
Visual Studio yeni sayfayı oluşturur ve açar.

### <a name="adding-html-to-the-page"></a>Sayfaya HTML ekleme

İzlenecek yolun bu bölümünde, sayfaya bazı statik metin ekleyeceksiniz.

### <a name="to-add-text-to-the-page"></a>Sayfaya metin eklemek için

1. Belge penceresinin en altında, **Tasarım görünümüne geçiş yapmak** için **Tasarım** sekmesine tıklayın.

    Tasarım görünümü geçerli sayfayı WYSıWYG benzeri bir şekilde görüntüler. Bu noktada, sayfada herhangi bir metin veya denetim yoktur, bu nedenle bir dikdörtgeni özetleyen kesikli çizgi dışında sayfa boştur. Bu dikdörtgen sayfadaki bir **div** öğesini temsil eder.
2. Kesik çizgi ile anahatlı dikdörtgen içerisine tıklayın.
3. **Visual Web Developer 'A hoş geldiniz** yazın ve **ENTER** tuşuna iki kez basın.

    Aşağıdaki çizimde, **Tasarım** görünümünde yazdığınız metin gösterilmektedir.

    ![Tasarım görünümü 'de hoş geldiniz metni](creating-a-basic-web-forms-page/_static/image7.png "Tasarım görünümü 'de hoş geldiniz metni")
4. **Kaynak** görünümüne geçin.

    **Tasarım** görünümü ' nde yazdığınızda oluşturduğunuz **kaynak** görünümünde HTML 'yi görebilirsiniz.  
    Statik metin](creating-a-basic-web-forms-page/_static/image8.png) ![Web sayfası

### <a name="running-the-page"></a>Sayfayı çalıştırma

Sayfaya denetimler ekleyerek devam etmeden önce, önce onu çalıştırabilirsiniz.

### <a name="to-run-the-page"></a>Sayfayı çalıştırmak için

1. **Çözüm Gezgini**, *firstweb sayfası. aspx* ' e sağ tıklayın ve **Başlangıç sayfası olarak ayarla**' yı seçin.
2. Sayfayı çalıştırmak için **CTRL + F5** tuşlarına basın.

    Sayfa tarayıcıda görüntülenir. Oluşturduğunuz sayfa *. aspx*dosya adı uzantısına sahip olsa da, şu anda HERHANGI bir HTML sayfası gibi çalışır.

    Tarayıcıda bir sayfa görüntülemek için **Çözüm Gezgini** sayfayı sağ tıklayıp **Tarayıcıda görüntüle**' yi seçebilirsiniz.
3. Web uygulamasını durdurmak için tarayıcıyı kapatın.

## <a name="adding-and-programming-controls"></a>Denetimleri ekleme ve programlama

<a id="sectionToggle1"></a>

Artık sayfaya sunucu denetimleri ekleyeceksiniz. Düğmeler, Etiketler, metin kutuları ve diğer tanıdık denetimler gibi sunucu denetimleri, Web Forms sayfalarınız için tipik form işleme özellikleri sağlar. Ancak, denetimleri istemci yerine sunucuda çalışan kodla programlayabilirsiniz.

Düğmeye bir [düğme](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) denetimi, [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) denetimi ve bir [etiket](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) denetimi ekleyecek ve [düğme](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) denetimi için [tıklama](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) olayını işlemek üzere kod yazacaksınız.

### <a name="to-add-controls-to-the-page"></a>Sayfaya denetim eklemek için

1. **Tasarım** görünümüne geçiş yapmak için **Tasarım** sekmesine tıklayın.
2. Ekleme noktasını, **Visual Web Developer 'A hoş geldiniz** metninin sonuna koyun ve **div** öğesi kutusunda biraz yer açmak için beş veya daha fazla kez **ENTER** tuşuna basın.
3. **Araç kutusunda**, zaten genişletilmemişse **Standart** grubu genişletin.  
Görüntülemek için sol taraftaki **araç kutusu** penceresini genişletmeniz gerekebileceğini unutmayın.
4. Bir [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) denetimini sayfaya sürükleyin ve bu kutuyu, Ilk satırda **Visual Web Developer 'a hoş geldiniz** **div** öğesinin ortasına bırakın.
5. Bir [düğme](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) denetimini sayfaya sürükleyin ve [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) denetiminin sağına bırakın.
6. Bir [etiket](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) denetimini sayfaya sürükleyin ve [düğme](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) denetiminin altındaki ayrı bir satıra bırakın.
7. Ekleme noktasını [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) denetiminin üzerine getirin ve ardından **adınızı girin:** .

    Bu statik HTML metni [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) denetiminin başlıktır. Statik HTML ve sunucu denetimlerini aynı sayfada karıştırabilirsiniz. Aşağıdaki çizimde, üç denetimin **Tasarım** görünümünde nasıl göründüğü gösterilmektedir.

    ![Tasarım görünümü üç denetim](creating-a-basic-web-forms-page/_static/image9.png "Tasarım görünümü üç denetim")

### <a name="setting-control-properties"></a>Denetim özelliklerini ayarlama

Visual Studio, sayfadaki denetimlerin özelliklerini ayarlamanıza yönelik çeşitli yollar sunar. İzlenecek yolun bu bölümünde, özellikleri hem **Tasarım** görünümü hem de **kaynak** görünümü içinde ayarlayacaksınız.

### <a name="to-set-control-properties"></a>Denetim özelliklerini ayarlamak için

1. İlk olarak, **Görünüm** menüsü '&gt; **diğer Windows** -&gt; **Özellikler penceresinden**seçerek **Özellikler** pencerelerini görüntüleyin. Alternatif olarak, **Özellikler** penceresini göstermek için **F4** ' i de seçebilirsiniz.
2. [Düğme](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) denetimini seçin ve ardından **Özellikler** penceresinde **metnin** değerini **görünen ad**olarak ayarlayın. Girdiğiniz metin, aşağıdaki çizimde gösterildiği gibi, tasarımcıda düğme üzerinde görünür.

    ![Düğme metnini ayarla](creating-a-basic-web-forms-page/_static/image10.png "Düğme metnini ayarla")
3. **Kaynak** görünümüne geçin.

    **Kaynak** görünümü, sayfa Için, Visual Studio 'nun sunucu denetimleri için oluşturduğu öğeler dahil olmak üzere HTML 'yi görüntüler. Denetimlerin **ASP:** önekini kullanması ve **runat =&quot;Server&quot;** özniteliğini IÇERMESI dışında, denetimler HTML benzeri sözdizimi kullanılarak bildirilmiştir.

    Denetim özellikleri öznitelik olarak bildirilmiştir. Örneğin, [düğme](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) denetiminin [metin](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.text.aspx) özelliğini ayarladığınızda, 1. adımda, aslında denetimin biçimlendirmesinde **metin** özniteliğini ayarlamıştı.

    > [!NOTE] 
    > 
    > Tüm denetimler, **runat =&quot;server&quot;** özniteliği de olan bir **form** öğesi içindedir. **Runat =&quot;server&quot;** özniteliği ve **ASP:** bir denetim etiketleri için önek, sayfa çalışırken sunucuda ASP.NET tarafından işlenmek üzere denetimleri işaretler. **&lt;&quot;form&quot;&gt;** ve **&lt;betiği runat =&quot;Server&quot;&gt;** öğelerinin dışındaki kod, tarayıcıya değiştirilmeden gönderilir, bu neden ASP.net kodunun bir öğe içinde olması gerekir açılış etiketi **runat =&quot;server&quot;** özniteliğini içeriyor.
4. Ardından, [etiket](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) denetimine ek bir özellik ekleyeceksiniz. **&lt;ASP: label&gt;** etiketindeki **ASP: Label** öğesinden hemen sonra ekleme noktasını yerleştirin ve ardından **boşluk**tuşuna basın.

    Bir [etiket](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) denetimi için ayarlayabileceğiniz kullanılabilir özelliklerin listesini görüntüleyen bir açılan liste görüntülenir. **IntelliSense**olarak anılan bu özellik, sayfadaki sunucu DENETIMLERININ, HTML öğelerinin ve diğer öğelerin sözdizimi ile **kaynak** görünümde size yardımcı olur. Aşağıdaki çizimde, [etiket](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) denetimi için **IntelliSense** açılan listesi gösterilmektedir.

    ![IntelliSense öznitelikleri](creating-a-basic-web-forms-page/_static/image11.png "IntelliSense öznitelikleri")
5. **ForeColor** öğesini seçin ve eşittir işareti yazın.

    IntelliSense, renklerin bir listesini görüntüler.

    > [!NOTE] 
    > 
    > Kod görüntülerken **CTRL + J** tuşlarına basarak dilediğiniz zaman bir **IntelliSense** açılan listesini görüntüleyebilirsiniz.
6. **[Etiket](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)** denetiminin metni için bir renk seçin. Beyaz bir arka planda okumak için yeterince karanlık bir renk seçtiğinizden emin olun.

    **ForeColor** özniteliği, kapanış tırnak işareti dahil olmak üzere seçtiğiniz renkle tamamlanır.

### <a name="programming-the-button-control"></a>Düğme denetimini programlama

Bu izlenecek yol için, kullanıcının metin kutusuna girdiği adı okuyan ve sonra da [etiket](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) denetimindeki adı görüntüleyen bir kod yazacaksınız.

### <a name="add-a-default-button-event-handler"></a>Varsayılan düğme olay işleyicisi ekleme

1. **Tasarım** görünümüne geçin.
2. [Düğme](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) denetimine çift tıklayın.

    Varsayılan olarak, Visual Studio bir arka plan kod dosyasına geçer ve [düğme](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) denetiminin varsayılan olayı olan [tıklama](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) olayı için bir iskelet olay işleyicisi oluşturur. Arka plan kod dosyası, (örneğin, HTML) Kullanıcı arabirimi biçiminizden sunucu kodınızdan (gibi C#) ayrılır.   
   İmleç bu olay işleyicisi için eklenen koda yerleştirildi.

    > [!NOTE] 
    > 
    > **Tasarım** görünümündeki bir denetime çift tıklamak, olay işleyicileri oluşturabileceğiniz birkaç yolla yalnızca biridir.
3. **Button1\_** olay işleyicisi ' ne tıklayın, ardından nokta ( **.** ) **Label1** yazın.

    Etiketin **kimliğinden** (**Label1**) sonraki noktayı yazdığınızda, Visual Studio aşağıdaki çizimde gösterildiği gibi, [etiket](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) denetimi için kullanılabilir üyelerin bir listesini görüntüler. Bir üyenin genellikle bir özelliği, yöntemi veya olayı.

    ![Kod görünümünde IntelliSense](creating-a-basic-web-forms-page/_static/image12.png "Kod görünümünde IntelliSense")
4. Aşağıdaki kod örneğinde gösterildiği gibi okuması için düğmenin **Click** olay işleyicisini sona erdirin.

    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample1.cs?highlight=3)]

    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample2.vb?highlight=2)]
5. **Çözüm Gezgini** ' de *firstweb sayfası. aspx* öğesine sağ tıklayıp **BIÇIMLENDIRMEYI görüntüle**' yi seçerek HTML biçimlemesinin **kaynak** görünümünü görüntülemek için geri dönün.
6. **&lt;ASP: Button&gt;** öğesine kaydırın. **&lt;ASP: Button&gt;** öğesinin şimdi **onclick =&quot;\_Button1** özniteliğine sahip olduğunu ve&quot;' a tıklayacağını unutmayın.

    Bu öznitelik, düğmenin [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) olayını önceki adımda kodlandığı işleyici yöntemine bağlar.

    Olay işleyicisi yöntemleri herhangi bir ada sahip olabilir; Gördüğünüz ad, Visual Studio tarafından oluşturulan varsayılan addır. Önemli nokta, HTML 'deki **OnClick** özniteliği için kullanılan adın, arka plan kodunda tanımlanan bir yöntemin adıyla eşleşmesi gerekir.

### <a name="running-the-page"></a>Sayfayı çalıştırma

Artık sayfadaki sunucu denetimlerini test edebilirsiniz.

### <a name="to-run-the-page"></a>Sayfayı çalıştırmak için

1. Sayfayı tarayıcıda çalıştırmak için **CTRL + F5** tuşlarına basın. Bir hata oluşursa yukarıdaki adımları yeniden denetleyin.
2. Metin kutusuna bir ad girin ve **görünen ad** düğmesine tıklayın.

    Girdiğiniz ad [etiket](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) denetiminde görüntülenir. Düğmeye tıkladığınızda, sayfanın Web sunucusuna nakledildiğini unutmayın. ASP.NET sonra sayfayı yeniden oluşturur, kodunuzu çalıştırır (Bu durumda, [düğme](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) denetiminin [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) olay işleyicisi çalıştırmaları) ve ardından yeni sayfayı tarayıcıya gönderir. Tarayıcıda durum çubuğunu izlerken, düğmeye her tıkladığınızda sayfanın Web sunucusuna gidiş dönüş yaptığını görebilirsiniz...
3. Tarayıcıda, çalıştırdığınız sayfanın kaynağını görüntülemek için sayfaya sağ tıklayıp **kaynağı görüntüle**' yi seçin.

    Sayfa kaynak kodunda, herhangi bir sunucu kodu olmadan HTML görürsünüz. Özellikle, **kaynak** görünümünde ile çalıştığınız **&lt;ASP:&gt;** öğelerini görmezsiniz. Sayfa çalıştığında, ASP.NET sunucu denetimlerini işler ve HTML öğelerini denetimi temsil eden işlevleri gerçekleştiren sayfada işler. Örneğin, **&lt;ASP: Button&gt;** Control, HTML **&lt;giriş türü =&quot;gönder&quot;&gt;** öğesi olarak işlenir.
4. Tarayıcıyı kapatın.

## <a name="working-with-additional-controls"></a>Ek denetimlerle çalışma

<a id="sectionToggle2"></a>

İzlenecek yolun bu bölümünde, [Takvim](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) denetimiyle birlikte çalışacaksınız. Bu, tarihleri ayda bir saat görüntüler. [Takvim](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) denetimi, çalıştığınız düğme, metin kutusu ve etiketten daha karmaşık bir denetimdir ve sunucu denetimlerinin bazı özelliklerini gösterir.

Bu bölümde, sayfaya bir [System. Web. UI. WebControls. Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) denetimi ekleyecek ve bunu biçimlendirecaksınız.

### <a name="to-add-a-calendar-control"></a>Takvim denetimi eklemek için

1. Visual Studio 'da **Tasarım** görünümü ' ne geçin.
2. **Araç kutusunun** **Standart** bölümünde, bir [Takvim](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) denetimini sayfaya sürükleyin ve diğer denetimleri içeren **div** öğesinin altına bırakın.

    Takvimin akıllı etiket paneli görüntülenir. Panel, seçili denetim için en sık kullanılan görevleri gerçekleştirmenizi kolaylaştıran komutları görüntüler. Aşağıdaki çizimde, [Takvim](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) denetimi **Tasarım** görünümünde işlendiğinde gösterilmektedir.

    ![Tasarım görünümü Takvim denetimi](creating-a-basic-web-forms-page/_static/image13.png "Tasarım görünümü Takvim denetimi")
3. Akıllı etiket panelinde **otomatik biçim**' i seçin.

    **Otomatik biçimlendirme** iletişim kutusu görüntülenir ve bu, takvim için bir biçimlendirme şeması seçmenizi sağlar. Aşağıdaki çizimde, [Takvim](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) denetiminin **otomatik biçim** iletişim kutusu gösterilmektedir.

    ![Otomatik biçimlendirme iletişim kutusu (Takvim denetimi)](creating-a-basic-web-forms-page/_static/image14.png "Otomatik biçimlendirme iletişim kutusu (Takvim denetimi)")
4. **Bir düzen seçin** listesinden **basit** ' i seçin ve ardından **Tamam**' a tıklayın.
5. **Kaynak** görünümüne geçin.

    **&lt;ASP: Calendar&gt;** öğesini görebilirsiniz. Bu öğe, daha önce oluşturduğunuz basit denetimlerin öğelerinden çok daha uzun. Ayrıca, çeşitli biçimlendirme ayarlarını temsil eden **&lt;WeekEndDayStyle&gt;** gibi alt öğeler de içerir. Aşağıdaki çizimde, **kaynak** görünümündeki [Takvim](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) denetimi gösterilmektedir. ( **Kaynak** görünümünde gördüğünüz tam biçimlendirme, çizimden biraz farklı görünebilir.)

    ![Kaynak görünümünde Takvim denetimi](creating-a-basic-web-forms-page/_static/image15.png "Kaynak görünümünde Takvim denetimi")

### <a name="programming-the-calendar-control"></a>Takvim denetimini programlama

Bu bölümde, [Takvim](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) denetimini Şu anda seçili olan tarihi görüntüleyecek şekilde programlayabilirsiniz.

### <a name="to-program-the-calendar-control"></a>Takvim denetimini programlamak için

1. **Tasarım** görünümü ' nde [Takvim](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) denetimine çift tıklayın.

    Yeni bir olay işleyicisi oluşturulur ve *FirstWebPage.aspx.cs*adlı arka plan kod dosyasında görüntülenir.
2. [SelectionChanged](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selectionchanged.aspx) olay işleyicisini aşağıdaki kodla sona erdirin.

    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample3.cs?highlight=3)]

    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample4.vb?highlight=2)]

    Yukarıdaki kod, etiket denetiminin metnini takvim denetiminin seçili tarihine ayarlar.

### <a name="running-the-page"></a>Sayfayı çalıştırma

Artık takvimi test edebilirsiniz.

### <a name="to-run-the-page"></a>Sayfayı çalıştırmak için

1. Sayfayı tarayıcıda çalıştırmak için **CTRL + F5** tuşlarına basın.
2. Takvimdeki bir tarihe tıklayın.

    Tıkladığınız Tarih [etiket](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) denetiminde görüntülenir.
3. Tarayıcıda, sayfanın kaynak kodunu görüntüleyin.

    [Takvim](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) denetiminin sayfada her gün bir **TD** öğesi olarak bir **tablo**olarak işlendiğine unutmayın.
4. Tarayıcıyı kapatın.

## <a name="next-steps"></a>Sonraki Adımlar

<a id="nextStepsToggle"></a>

Bu kılavuzda, Visual Studio sayfa Tasarımcısı 'nın temel özellikleri gösterilmektedir. Artık Visual Studio 'da bir Web Forms sayfası oluşturmayı ve düzenlemenizi anladığınıza göre, diğer özellikleri araştırmak isteyebilirsiniz. Örneğin, aşağıdakileri yapmak isteyebilirsiniz:

- [ASP.NET 4,5 Web Forms ve Visual Studio 2013 Ile çalışmaya](getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)başlama adım adım öğretici serisini izleyerek ASP.NET Web Forms hakkında daha fazla bilgi edinin.
- Geçişli stil sayfaları (CSS) hakkında daha fazla bilgi edinin. Ayrıntılar için bkz. [CSS Ile çalışma genel bakış](https://msdn.microsoft.com/library/bb398931.aspx).
