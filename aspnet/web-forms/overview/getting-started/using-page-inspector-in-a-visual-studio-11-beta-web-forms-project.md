---
uid: web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
title: ASP.NET Web Forms Visual Studio 2012 için sayfa denetçisi 'ni kullanma | Microsoft Docs
author: rick-anderson
description: Visual Studio 2012 için sayfa denetçisi, tümleşik bir tarayıcıyla bir Web geliştirme aracıdır. Tümleşik tarayıcıda ve sayfa denetçisinde herhangi bir öğe seçin...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 2ece0bf4-aae5-4ff4-8f62-28e0819d4f86
msc.legacyurl: /web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: c165bbea505b4cb8eae1312cdd587f4ed36541a0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78575924"
---
# <a name="using-page-inspector-for-visual-studio-2012-in-aspnet-web-forms"></a>ASP.NET Web Forms’da Visual Studio 2012 için Sayfa Denetçisini Kullanma

, Tim Ammann tarafından

> Visual Studio 2012 için sayfa denetçisi, tümleşik bir tarayıcıyla bir Web geliştirme aracıdır. Tümleşik tarayıcıda herhangi bir öğeyi seçin ve sayfa denetçisi öğenin kaynağını ve CSS 'sini anında vurgular. Uygulamanızdaki herhangi bir sayfaya gözatabilir, işlenmiş biçimlendirmenin kaynaklarını hızlıca bulabilir ve Visual Studio ortamında doğrudan tarayıcı araçları kullanabilirsiniz.
> 
> Bu öğreticide Inceleme modunun nasıl etkinleştirileceği ve ardından Web projenizdeki CSS kuralları ile metinlerin hızlı bir şekilde nasıl konumlandırmaları ve düzenlenmesi gösterilmektedir. Öğretici bir Web Forms uygulama projesi kullanır, ancak Web sitesi projeleri ve [MVC](https://go.microsoft.com/?linkid=9802002) uygulamaları Için sayfa denetçisi 'ni de kullanabilirsiniz.
> 
> Öğreticide aşağıdaki bölümler bulunur:
> 
> [Önkoşullar](#_1_prerequisites)
> 
> [Web uygulaması oluşturma](#_2_creating_a)
> 
> [Uygulamayı görüntülemek için sayfa denetçisini kullanma](#_3_using_page)
> 
> [Inceleme modunu etkinleştir](#_4_inspection_mode)
> 
> [Işaretlemede değişiklik yapmak için sayfa denetçisini kullanın](#_5_using_page)
> 
> [İnceleme modu ve HTML penceresi](#_6_inspection_mode)
> 
> [Stiller penceresinde CSS değişikliklerinin önizlemesi](#_7_previewing_css)
> 
> [CSS otomatik eşitleme](#css_auto_sync)
> 
> [CSS renk seçiciyi kullanma](#css_color_picker)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a>Önkoşullar

- Web için [Visual Studio 2012](https://www.microsoft.com/visualstudio/11) veya [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/downloads#express-web).

> [!NOTE]
> Sayfa denetçisinin en son sürümünü almak için, .NET 2,0 için Azure SDK 'yı yüklemek üzere [Web Platformu Yükleyicisi](https://go.microsoft.com/fwlink/?LinkId=255386) 'ni kullanın.

Sayfa denetçisi Microsoft Web Geliştirici Araçları ile paketlenmiştir. En son sürüm 1,3 ' dir. Sahip olduğunuz sürümü denetlemek için, Visual Studio 'Yu çalıştırın ve **Yardım** menüsünden **Microsoft Visual Studio hakkında** ' yı seçin.

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a>Web uygulaması oluşturma

İlk olarak, ile sayfa denetçisi kullanacağınız bir Web uygulaması oluşturacaksınız. Visual Studio 'da **dosya** &gt; **Yeni proje**' yi seçin. Sol tarafta, **görsel C#** ' i genişletin, **Web**' i seçin ve ardından **ASP.NET Web Forms uygulama**' yı seçin.

![Yeni Web Forms uygulaması](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image1.png)

**Tamam**’a tıklayın.

Uygulama **kaynak** görünümü ' nde açılır.

![Kaynak görünümünde yeni Web Forms uygulaması](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image2.png)

Artık birlikte çalışmak üzere bir uygulamanız olduğuna göre, sayfayı incelemek ve değiştirmek için sayfa denetçisi ' ni kullanabilirsiniz.

<a id="_starting_page_inspector"></a><a id="_3_starting_page"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-view-the-application"></a>Uygulamayı görüntülemek için sayfa denetçisini kullanma

Daha sonra, uygulamayı sayfa denetçisi ile birlikte görüntülenir. **Çözüm Gezgini**' de projeye sağ tıklayın ve ardından **sayfa denetçisinde görüntüle**' yi seçin.

![Sayfa denetçisinde görüntüle](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image3.png)

Varsayılan olarak, sayfa denetçisi ilk kez başlatıldığında, Visual Studio ortamının sol tarafında dar bir pencere olarak yerleştirilir. Sol tarafta bırakın ve bunu sizin için rahat olan bir genişliğe ayarlayın veya en üstteki, alttaki veya sağdaki araç alanlarından birine yerleştirin:

![Sayfa denetçisi yerleştirme konumları](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image4.png)

Sayfa denetçisi penceresini çıkardıysanız, Visual Studio 'Nun dışına veya varsa ikinci bir monitöre yerleştirebilirsiniz. Bununla birlikte, sayfa denetçisi penceresi yok edildiğinde, sayfa denetçisi ve Visual Studio arasında ALT + TAB 'a giderek, **araçlar** &gt; **seçenekler** &gt; **ortam** &gt; **Sekmeler ve pencereler**' e gidin ve **sekme kutusu**' nun altında, **kayan araç pencereleri ' nin her zaman ana pencerenin en üstünde yer alan**onay kutusunun işaretini kaldırın:

![Kayan araç Windows onay kutusunu Visual Studio ve yerleştirilmemiş sayfa denetçisi penceresi arasında ALT + TAB olarak temizleyin](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image5.png)

Sayfa denetçisi penceresinin üst bölmesi, geçerli sayfayı bir tarayıcı penceresinde gösterir. Alt bölmede, sol taraftaki HTML biçimlendirme sayfası ve sayfanın farklı yönlerini incelemenize olanak tanıyan bazı sekmeler gösterilir. Alt bölme, Internet Explorer 'daki [F12 geliştirici araçları](https://msdn.microsoft.com/ie/aa740478) benzerdir. (Ancak, Geliştirici araçlarının aksine, Visual Studio 'da doğrudan sayfa denetçisi kullanabilirsiniz.)

![Sayfa Denetçisi](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image6.png)

Bu öğreticide, hızlı bir şekilde gezinmenize ve uygulamada değişiklik yapmanıza yardımcı olması için sayfa denetçisi tarayıcı bölmesini ve **HTML** ve **Stiller** sekmelerini kullanacaksınız.

<a id="_4_inspection_mode"></a>
## <a name="enable-inspection-mode"></a>Inceleme modunu etkinleştir

Daha sonra, sayfa denetçisi Inceleme modunun nasıl çalıştığını görürsünüz. Sayfa denetçisi penceresinde, **Denetle** düğmesine tıklayın.

![Öğeyi İncele](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image7.png)

İnceleme modunu çalışırken görmek için farenizi sayfa denetçisi tarayıcı penceresi içinde sayfanın farklı bölümlerine taşıyın. Yaptığınız gibi fare işaretçisi büyük artı işaretine dönüşür ve alttaki öğe vurgulanır:

![Div üzerinde vurgulama. içerik-sarmalayıcı](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image8.png)

Fare işaretçisini taşırken,

- **Kaynak** görünümündeki içerikler, sayfadaki seçili öğeye karşılık gelen biçimlendirmeyi göstermek için değişir. İlgili biçimlendirme vurgulanır. Kaynak başka bir dosya ise, bu dosya kaynak görünümünde ilgili biçimlendirme vurgulanarak açılır.

- Sayfa denetçisindeki **HTML** sekmesinde görünen biçimlendirme Ayrıca sayfadaki seçili öğeye karşılık gelen şekilde değişir. **HTML** sekmesinde, ilgili biçimlendirme özetlenmiştir.

- **Stiller** sekmesi, geçerli SEÇIMLE ilgili CSS kurallarını gösterir.

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a>Işaretlemede değişiklik yapmak için sayfa denetçisini kullanın

Şimdi, konumu bulma ve biçimlendirme veya metin üzerinde değişiklik yapmak için sayfa denetçisini nasıl kullanabileceğinizi göreceksiniz.

Sayfa denetçisi ' ni Inceleme moduna alın ve ardından giriş sayfasının en altına kaydırın.

Alt bilgi alanını girdikten hemen sonra, sayfa denetçisi *site. Master* düzen dosyasını diğer sekmelerin sağındaki geçici bir sekmede açar ve seçtiğiniz ana sayfanın bölümünü vurgular. Bu, sayfa denetçisinin, gerçekten açtığınız farklı bir dosyadan gelmiş olabilecek bir sayfada içerik bulma ve görüntüleme şeklini gösterir.

![Inceleme modundaki alt bilgi vurguları](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image9.png)

Sayfa denetçisi tarayıcı penceresinde, fare işaretçinizi, telif hakkı <a id="a"> </a>bildiriminin bulunduğu çizginin üzerine getirin.

*Site. Master* sayfasında, karşılık gelen çizgi vurgulanır.

![Alt bilgi için telif hakkı satırı vurgulanmış](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image10.png)

*Site. Master* dosyasındaki satırın sonuna bir metin ekleyin.

&lt;p&gt;&amp;kopyalama; &lt;%: DateTime. Now. Year%&gt;-My ASP.NET Application rol!&lt;/p&gt;

Şimdi, sayfa denetçisi tarayıcı penceresinde sonuçları görmek için CTRL + ALT + ENTER tuşlarına basın veya güncelleştirme çubuğuna tıklayın.

![ASP.NET uygulamamın özellikleri!](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image11.png)

Altbilginin *default. aspx* sayfasında olduğunu, ancak ana düzen sayfasında olduğunu düşündük ve sayfa denetçisi sizin için buldu.

<a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a>İnceleme modu ve HTML penceresi

Daha sonra, HTML penceresine ve sizin için öğeleri nasıl eşlediği hakkında hızlı bir görünüme sahip olursunuz.

Sayfa denetçisini Inceleme moduna alın.

![Öğeyi İncele](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image12.png)

Sayfanın "buraya logonuzu" belirten üst kısmına tıklayın. Belirli bir öğeyi daha ayrıntılı bir şekilde inceleriz, bu nedenle fare işaretçisini taşırken tarayıcı penceresinde görüntüleme artık görünmez.

Şimdi, fare işaretçisini **HTML** penceresine taşıyın. Fare işaretçisini taşırken, sayfa denetçisi **HTML** penceresi içindeki öğeyi özetler ve tarayıcı penceresinde buna karşılık gelen öğeyi vurgular.

![HTML penceresi](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image13.png)

Daha önce olduğu gibi, sayfa denetçisi *site. Master* dosyasını sizin için geçici bir sekmede açar. site. Master sekmesine tıklayın ve ilgili biçimlendirme &lt;üst bilgi&gt; bölümünde vurgulanır:

![Vurgulanan işaretleme](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image14.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a>Stiller penceresinde CSS değişikliklerinin önizlemesi

Daha sonra, CSS değişikliklerini önizlemek için sayfa denetçisi **stilleri** penceresini nasıl kullanabileceğinizi göreceksiniz.

Inceleme moduna sayfa denetçisi koymak için **Denetle** düğmesine tıklayın.

Sayfa denetçisi tarayıcı penceresinde, **div. Content-Wrapper** etiketi görünene kadar fare Işaretçisini "giriş sayfası" bölümünün üzerine taşıyın.

![Öğelerin üzerine gelindiğinde](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image15.png)

Div. Content-Wrapper bölümünün içine bir kez tıklayın ve sonra fare işaretçisini **Stiller** penceresine taşıyın. . Öne çıkan. Content-sarmalayıcı sınıfı seçicisinin altında, arka plan rengi özelliği için onay kutusunu temizleyin ve seçin.

![Arka plan rengini temizle](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image16.png)

Sayfa denetçisi tarayıcı penceresinde değişikliğin anında nasıl önizlediğine dikkat edin.

Onay kutusunu yeniden seçin, sonra özellik değerini çift tıklatın ve `red`değiştirin. Değişiklik hemen görüntülenir:

![Kırmızı arka plan rengi](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image17.png)

**Stiller** penceresi, değişiklikleri stil sayfasına IŞLEMEDEN önce CSS değişikliklerinin test edilmesi ve önizlenmesi kolaylaştırır.

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a>CSS otomatik eşitleme

> [!NOTE]
> Bu özellik, sayfa denetçisinin 1,3 sürümünü gerektirir.

CSS otomatik eşitleme özelliği, bir CSS dosyasını doğrudan düzenlemenizi sağlar ve değişiklikleri sayfa denetçisi tarayıcısında hemen görebilirsiniz.

Inceleme moduna sayfa denetçisi koymak için **Denetle** ' ye tıklayın.

Sayfa denetçisi tarayıcısında, **div. Content-Wrapper** etiketi görünene kadar fare Işaretçisini "giriş sayfası" bölümünün üzerine taşıyın. Bu öğeyi seçmek için bir kez tıklayın.

**Stiller** penceresi, bu öğe IÇIN tüm CSS kurallarını gösterir. . Öne çıkan. Content-Wrapper sınıf seçiciyi bulmak için aşağı kaydırın. ". Öne çıkan. içerik-sarmalayıcı" seçeneğine tıklayın. Sayfa denetçisi, bu stili (site. css) tanımlayan CSS dosyasını açar ve ilgili CSS stilini vurgular.

![CSS dosyası](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image18.png)

Şimdi `background-color` değerini "Red" olarak değiştirin. Değişiklik, sayfa denetçisi tarayıcısında hemen görünür.

![Sayfa denetçisi tarayıcısı](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image19.png)

<a id="css_color_picker"></a>

## <a name="using-the-css-color-picker"></a>CSS renk seçiciyi kullanma

Daha sonra, varsayılan uygulamada Vurgulanan metin için CSS 'yi hızlı bir şekilde bulmak ve değiştirmek üzere sayfa denetçisi 'ni nasıl kullanacağınızı öğreneceksiniz. Bu örnekte, mavi vurgulamayı beğenmemenizi ve bunu başka bir renkle değiştirmek istediğinizi öğrendiniz.

**Denetle** düğmesine tıklayın.

![Öğeyi İncele](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image20.png)

Sayfa denetçisi tarayıcı penceresinde, CSS "Mark" etiketinin görünmesi için fare işaretçisini vurgulanan "videolar, öğreticiler ve örnekler" metninin üzerine taşıyın.

![Mark öğesinin üzerine gelindiğinde](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image21.png)

Seçmek için metne tıklayın. Karşılık gelen CSS işaret Seçicisi, **Stiller** penceresinin alt kısmında görünür.

![Stiller penceresinde işaret Seçicisi](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image22.png)

İşaret seçicisine tıklayın. Bu, Web uygulaması için *site. css* dosyasını açar. Site. css sekmesine tıklayın ve seçici için karşılık gelen CSS vurgulanır:

![stil sayfasında işaret Seçicisi](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image23.png)

Arka plan rengi özelliği ile satırı seçin ve kaldırın.

Şimdi **işaretle** arkaplan-Color özelliği için yeni bir renk seçmek üzere yeni Visual STUDIO 2012 CSS renk seçiciyi kullanacaksınız.

<a id="_using_the_visual"></a>

### <a name="using-the-visual-studio-2012-css-color-picker"></a>Visual Studio 2012 CSS renk seçiciyi kullanma

Visual Studio 2012 ' deki CSS Düzenleyicisi, renkleri seçip eklemeyi kolaylaştıran bir renk seçicisine sahiptir. Basit bir renk çubuğuna ve daha hassas denetim sağlayan bir "açılır" seçicisine sahiptir.

Renk Seçici standart bir renk paleti içerir, standart renk adlarını, karma kodları, RGB, RGBA, HSL ve HSLA renklerini destekler ve belgede en son kullandığınız renklerin bir listesini tutar.

Arka plan rengi özelliğinin olduğu satırda "BC" yazın ve aşağı oka bir kez basın.

Her sözcüğün ilk karakterini "Arkaplan-Color" gibi bir tire ayrılmış özellikte yazdığınızda, IntelliSense yalnızca eşleşen özellikleri göstermek için listeyi filtreler:

![IntelliSense filtrelenmiş değerler](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image24.png)

Şimdi bir iki nokta üst üste yazın. Bunu yaptığınızda, tam arka plan rengi Özellik adı eklenir. **#** veya **RGB yazın (** ve renk seçici çubuğu görünür:

![CSS Renk Seçici Çubuğu](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image25.png)

Renk seçici çubuğunun nasıl çalıştığını görmek için fare işaretçisi ile renklerini tıklatın veya aşağı ok tuşuna basın ve ardından sağ ve sağ ok tuşlarını kullanarak renkleri çapraz geçiş yapın. Bir rengi ziyaret ettiğinizde, arka plan rengi özelliği için karşılık gelen değer önizlenebilir:

![arka plan rengi Özellik değeri önizlenen](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image26.png)

Bu noktada, değeri seçmek için ENTER tuşuna basabilir ve sonra noktalı virgül (;) CSS girdisini doldurun. Şimdilik renk seçici açılır ekranının nasıl çalıştığını görebilmeniz için sonraki bölüme gidin.

#### <a name="using-the-color-picker-pop-down"></a>Renk Seçici açılır penceresini kullanma

Renk çubuğu Aradığınız renge sahip olmadığında renk seçici açılır penceresini kullanabilirsiniz.

Açmak için, renk çubuğunun sağ ucundaki çift köşeli çift ayraca tıklayın veya klavyede bir kez veya iki kez aşağı ok tuşuna basın.

![CSS Renk Seçici açılır menüsü](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image27.png)

Sağ taraftaki dikey çubuktan bir renge tıklayın. Bu, ana penceredeki bu renk için bir gradyan gösterir. ENTER tuşuna basarak doğrudan dikey çubuktan bir renk seçin veya ana penceredeki herhangi bir noktaya tıklayarak daha fazla duyarlık seçin.

Bilgisayar ekranınızda kullanmak istediğiniz bir renk varsa (Visual Studio Kullanıcı arabirimi içinde olması gerekmez), sağ alt köşedeki Damlalık aracını kullanarak değerini yakalayabilirsiniz.

Ayrıca renk seçicinin alt kısmına kaydırıcıyı taşıyarak bir rengin saydamlığını değiştirebilirsiniz. Bunun yapılması, RGBA biçimi geçirgenliği temsil ettiğinden, renk değerlerini RGBA değerlerine dönüştürür.

Bir renk seçtikten sonra, ENTER tuşuna basın ve ardından *site. css* dosyasındaki arka plan rengi girişini tamamlamaya yönelik bir noktalı virgül yazın.

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a>Sayfa denetçisi güncelleştirme çubuğu

Sayfa denetçisi, *site. css* dosyasındaki (veya uygulamadaki herhangi bir dosya) yapılan değişikliği hemen algılar ve bir güncelleştirme çubuğunda bir uyarı görüntüler.

![Güncelleştirme çubuğu](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image28.png)

Tüm dosyalarınızı kaydetmek ve sayfa denetçisi tarayıcısını yenilemek için CTRL + ALT + ENTER tuşlarına basın veya güncelleştirme çubuğuna tıklayın. Vurgu renginizdeki değişiklik tarayıcıda görünür:

![Vurgu rengi değişti](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image29.png)

<a id="_using_page_inspector_1"></a>Sayfa denetçisi tarayıcısını doğrudan Visual Studio ortamının içinden yenileyenizi görürsünüz. Dış tarayıcı yerine sayfa denetçisi kullanmak, Web uygulamalarınızı geliştirirken düzenleyicide kalmanızı sağlar.

## <a name="see-also"></a>Ayrıca Bkz.

[Sayfa denetçisi Ile tanışın](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector) (Channel 9 Videosu)

[Sayfa denetçisi hata iletileri](https://go.microsoft.com/?linkid=9813062) (MSDN)
