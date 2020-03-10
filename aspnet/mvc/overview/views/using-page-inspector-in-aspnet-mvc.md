---
uid: mvc/overview/views/using-page-inspector-in-aspnet-mvc
title: ASP.NET MVC 'de sayfa denetçisini kullanma | Microsoft Docs
author: rick-anderson
description: Visual Studio 2012 ' deki sayfa denetçisi tümleşik tarayıcıyla bir Web geliştirme aracıdır. Tümleşik tarayıcıda ve sayfa denetçisi ı ' nde herhangi bir öğe seçin...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: c7e4e1ab-4932-4614-9f53-aaf7c706d498
msc.legacyurl: /mvc/overview/views/using-page-inspector-in-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 5da3e142c52a770f59222c21d9f9a53cbbdbf498
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538019"
---
# <a name="using-page-inspector-in-aspnet-mvc"></a>ASP.NET MVC'de Sayfa Denetçisini Kullanma

, Tim Ammann tarafından

> Visual Studio 2012 ' deki sayfa denetçisi tümleşik tarayıcıyla bir Web geliştirme aracıdır. Tümleşik tarayıcıda herhangi bir öğeyi seçin ve sayfa denetçisi öğenin kaynağını ve CSS 'sini anında vurgular. Herhangi bir MVC görünümüne gözatabilir, işlenmiş biçimlendirmenin kaynaklarını hızlıca bulabilir ve Visual Studio ortamında doğrudan tarayıcı araçları kullanabilirsiniz.
> 
> [Videoyu izleyin](../../videos/mvc-4/using-page-inspector-in-aspnet-mvc.md)
> 
> Bu öğreticide Inceleme modunun nasıl etkinleştirileceği gösterilir ve sonra Web projenizde biçimlendirmeyi ve CSS 'yi hızlıca bulun ve düzenleyin. Öğretici bir MVC projesi kullanır, ancak [Web Forms](https://go.microsoft.com/?linkid=9802001) ve diğer ASP.NET uygulamaları Için sayfa denetçisi de kullanabilirsiniz.
> 
> Öğreticide aşağıdaki bölümler bulunur:
> 
> - [Önkoşullar](#_1_prerequisites)
> - [Web uygulaması oluşturma](#_2_creating_a)
> - [Bir görünüme gitmek için sayfa denetçisini kullanma](#_3_using_page)
> - [Inceleme modunu etkinleştir](#_4_inspection_mode)
> - [Işaretlemede değişiklik yapmak için sayfa denetçisini kullanın](#_5_using_page)
> - [İnceleme modu ve HTML penceresi](#_6_inspection_mode)
> - [Stiller penceresinde CSS değişikliklerinin önizlemesi](#_7_previewing_css)
> - [CSS otomatik eşitleme](#css_auto_sync)
> - [CSS renk seçiciyi kullanma](#css_color_picker)
> - [Dinamik sayfa öğelerini JavaScript 'e eşleme](#map_dynamic_elements)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a>Önkoşullar

- Web için [Visual Studio 2012](https://www.microsoft.com/visualstudio/11) veya [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/downloads#express-web).

> [!NOTE]
> Sayfa denetçisinin en son sürümünü almak için, .NET 2,0 için Microsoft Azure SDK 'sını yüklemek üzere [Web Platformu Yükleyicisi](https://go.microsoft.com/fwlink/?LinkId=255386) ' ni kullanın.

Sayfa denetçisi Microsoft Web Geliştirici Araçları ile paketlenmiştir. En son sürüm 1,3 ' dir. Sahip olduğunuz sürümü denetlemek için, Visual Studio 'Yu çalıştırın ve **Yardım** menüsünden **Microsoft Visual Studio hakkında** ' yı seçin.

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a>Web uygulaması oluşturma

İlk olarak, ile sayfa denetçisi kullanacağınız bir Web uygulaması oluşturun. Visual Studio 'da **dosya** &gt; **Yeni proje**' yi seçin. Sol tarafta, **C#görsel**' i genişletin, **Web**' i seçin ve **ASP.net MVC4 Web uygulaması**' nı seçin.

![Yeni ASP.NET MVC uygulaması](using-page-inspector-in-aspnet-mvc/_static/image2.png)

**Tamam**’a tıklayın.

**Yeni ASP.NET MVC 4 projesi** Iletişim kutusunda **Internet uygulaması**' nı seçin. **Razor** 'yi varsayılan görünüm altyapısı olarak bırakın.

![Yeni ASP.NET MVC projesi-Internet uygulaması](using-page-inspector-in-aspnet-mvc/_static/image4.png)

Uygulama **kaynak** görünümü ' nde açılır.

![Kaynak görünümünde yeni ASP.NET MVC uygulaması](using-page-inspector-in-aspnet-mvc/_static/image6.png)

Artık birlikte çalışmak üzere bir uygulamanız olduğuna göre, sayfayı incelemek ve değiştirmek için sayfa denetçisi ' ni kullanabilirsiniz.

<a id="_starting_page_inspector"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-browse-to-a-view"></a>Bir görünüme gitmek için sayfa denetçisini kullanma

Visual Studio 2012 ' de, projenizdeki herhangi bir görünüme sağ tıklayabilir, **sayfa denetçisinde görünüm**' ü seçtiğinizde, sayfa denetçisi bu yolu gösterir ve sayfayı görüntüler.

**Çözüm Gezgini**' de, **Görünümler** klasörünü ve ardından **giriş** klasörünü genişletin. Index. cshtml dosyasına sağ tıklayın ve **sayfa denetçisinde görüntüle**' yi seçin.

![Sayfa denetçisinde Index. cshtml 'yi görüntüle](using-page-inspector-in-aspnet-mvc/_static/image8.png)

Varsayılan olarak, sayfa denetçisi Visual Studio ortamının sol tarafında bir pencere olarak Yuvalandırılmış olur. İsterseniz, başka bir yere sabitleyebilir veya pencereyi serbest bırakabilirsiniz. Bkz. [nasıl yapılır: pencereleri düzenleme ve yerleştirme](https://msdn.microsoft.com/library/z4y0hsax.aspx).

Sayfa denetçisi penceresinin üst bölmesi, geçerli sayfayı bir tarayıcı penceresinde gösterir. Alt bölmede, sayfanın farklı yönlerini incelemenize olanak tanıyan bazı sekmeler ile birlikte HTML biçimlendirmesinde sayfa gösterilir. Alt bölme, Internet Explorer 'daki [F12 geliştirici araçları](https://msdn.microsoft.com/ie/aa740478) benzerdir.

![Sayfa denetçisinde ASP.NET MVC uygulaması](using-page-inspector-in-aspnet-mvc/_static/image10.png)

Bu öğreticide, hızlı gezinmek ve uygulamada değişiklikler yapmak için **HTML** ve **Stiller** sekmelerini kullanacaksınız.

<a id="_examining_(&quot;decomposing&quot;)_the"></a><a id="_inspection_mode_and"></a><a id="_4_inspection_mode"></a>

## <a name="enableinspection-mode"></a>Enableinceleme modu

Sayfa denetçisini Inceleme moduna almak için, **Denetle** düğmesine tıklayın. Denetleme modunda, fare işaretçisini işlenmiş sayfanın herhangi bir bölümünde tuttuğunuzda, karşılık gelen kaynak biçimlendirmesi veya kodu vurgulanır.

![Inceleme modunu değiştirme](using-page-inspector-in-aspnet-mvc/_static/image12.png)

Şimdi farenizi sayfa denetçisi içinde sayfanın farklı bölümlerine taşıyın. Yaptığınız gibi fare işaretçisi büyük artı işaretine dönüşür ve alttaki öğe vurgulanır:

![Div üzerinde vurgulama. içerik-sarmalayıcı](using-page-inspector-in-aspnet-mvc/_static/image14.png)

Fare işaretçisini taşırken, Visual Studio kaynak dosyada karşılık gelen Razor söz dizimi vurgular. HTML öğesi başka bir kaynak dosyasından geliyorsa, Visual Studio dosyayı otomatik olarak açar.

Sayfa denetçisinde, **HTML** sekmesi Razor söz DIZIMI oluşturulan HTML 'yi gösterir. Fare işaretçisini taşırken, HTML öğeleri vurgulanır. **Stiller** sekmesi Öğesı için CSS kurallarını gösterir.

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a>Işaretlemede değişiklik yapmak için sayfa denetçisini kullanın

Sayfa denetçisi, konumu açık olmayabilir olan biçimlendirmeyi bulmanızı sağlar. Ardından, biçimlendirmeyi değiştirebilir ve elde edilen değişiklikleri görebilirsiniz.

Bunu görmek için, **İncele** ' ye tıklayın ve ardından sayfa denetçisi penceresinde sayfanın en altına gidin.

Fare işaretçisini altbilgi alanına taşıdığınızda, sayfa denetçisi \_Layout. cshtml dosyasını açar ve seçtiğiniz düzen sayfasının bölümünü vurgular. Gördüğünüz gibi, alt bilgi, görünümün kendisi değil, düzen dosyasında tanımlanmıştır.

![Arasında](using-page-inspector-in-aspnet-mvc/_static/image16.png)

Artık fare işaretçinizi, telif hakkı <a id="a"> </a>bildiriminin bulunduğu çizginin üzerine taşıyın. \_Layout. cshtml sayfasında, karşılık gelen çizgi vurgulanır.

![Alt bilgi için telif hakkı satırı vurgulanmış](using-page-inspector-in-aspnet-mvc/_static/image18.png)

\_Layout. cshtml dosyasındaki satırın sonuna bir metin ekleyin.

&lt;p&gt;&amp;kopyalama; @DateTime.Now.Year-My ASP.NET MVC uygulaması Rolaları!&lt;/p&gt;

Şimdi, sayfa denetçisi tarayıcı penceresinde sonuçları görmek için CTRL + ALT + ENTER tuşlarına basın veya güncelleştirme çubuğuna tıklayın.

![ASP.NET uygulamamın özellikleri!](using-page-inspector-in-aspnet-mvc/_static/image20.png)

Alt bilginin Index. cshtml 'de tanımlandığını düşündük, ancak \_Layout. cshtml dosyasında olduğunu ve sayfa denetçisi sizin için bulmuştur.

<a id="_inspection_mode_and_1"></a><a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a>İnceleme modu ve HTML penceresi

Daha sonra, HTML penceresine ve sizin için öğeleri nasıl eşlediği hakkında hızlı bir görünüme sahip olursunuz.

Inceleme moduna sayfa denetçisi koymak için **Denetle** ' ye tıklayın.

Sayfanın "buraya logonuzu" belirten üst kısmına tıklayın. Belirli bir öğeyi daha ayrıntılı bir şekilde inceleriz, bu nedenle fare işaretçisini taşırken tarayıcı penceresinde görüntüleme artık görünmez.

Şimdi, fare işaretçisini **HTML** penceresine taşıyın. Fare işaretçisini taşırken, sayfa denetçisi **HTML** penceresi içindeki öğeyi özetler ve tarayıcı penceresinde buna karşılık gelen öğeyi vurgular.

![HTML penceresi](using-page-inspector-in-aspnet-mvc/_static/image22.png)

Daha önce olduğu gibi, sayfa denetçisi geçici bir sekmede sizin için \_Layout. cshtml dosyasını açar. \_Layout. cshtml geçici sekmesine tıklayın ve ilgili biçimlendirme, sizin için &lt;üst bilgi&gt; bölümünde vurgulanacaktır:

![Vurgulanan işaretleme](using-page-inspector-in-aspnet-mvc/_static/image24.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a>Stiller penceresinde CSS değişikliklerinin önizlemesi

Daha sonra, CSS değişikliklerini önizlemek için sayfa denetçisi **stilleri** penceresini kullanırsınız.

Inceleme moduna sayfa denetçisi koymak için **Denetle** ' ye tıklayın.

Sayfa denetçisi tarayıcı penceresinde, **div. Content-Wrapper** etiketi görünene kadar fare Işaretçisini "giriş sayfası" bölümünün üzerine taşıyın.

![Div üzerinde vurgulama. içerik-sarmalayıcı](using-page-inspector-in-aspnet-mvc/_static/image26.png)

Div. Content-Wrapper bölümünün içine bir kez tıklayın ve sonra fare işaretçisini **Stiller** penceresine taşıyın. **Stiller** penceresi, bu öğe IÇIN tüm CSS kurallarını gösterir. . Öne çıkan. Content-Wrapper sınıf seçiciyi bulmak için aşağı kaydırın. Şimdi arka plan rengi özelliği için onay kutusunu temizleyin.

![Arka plan rengini temizle](using-page-inspector-in-aspnet-mvc/_static/image28.png)

Sayfa denetçisi tarayıcı penceresinde değişikliğin anında nasıl önizlediğine dikkat edin.

Onay kutusunu yeniden seçin, sonra özellik değerine çift tıklayın ve kırmızı olarak değiştirin. Değişiklik hemen görüntülenir:

![Kırmızı arka plan rengi](using-page-inspector-in-aspnet-mvc/_static/image30.png)

**Stiller** penceresi, değişiklikleri stil sayfasına IŞLEMEDEN önce CSS değişikliklerinin test edilmesi ve önizlenmesi kolaylaştırır.

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a>CSS otomatik eşitleme

> [!NOTE]
> Bu özellik, sayfa denetçisinin 1,3 sürümünü gerektirir.

CSS otomatik eşitleme özelliği, bir CSS dosyasını doğrudan düzenlemenizi sağlar ve değişiklikleri sayfa denetçisi tarayıcısında hemen görebilirsiniz.

Inceleme moduna sayfa denetçisi koymak için **Denetle** ' ye tıklayın.

Sayfa denetçisi tarayıcısında, **div. Content-Wrapper** etiketi görünene kadar fare Işaretçisini "giriş sayfası" bölümünün üzerine taşıyın. Bu öğeyi seçmek için bir kez tıklayın.

**Stiller** penceresi, bu öğe IÇIN tüm CSS kurallarını gösterir. . Öne çıkan. Content-Wrapper sınıf seçiciyi bulmak için aşağı kaydırın. ". Öne çıkan. içerik-sarmalayıcı" seçeneğine tıklayın. Sayfa denetçisi, bu stili (site. css) tanımlayan CSS dosyasını açar ve ilgili CSS stilini vurgular.

![](using-page-inspector-in-aspnet-mvc/_static/image32.png)

Şimdi `background-color` değerini "Red" olarak değiştirin. Değişiklik, sayfa denetçisi tarayıcısında hemen görünür.

![](using-page-inspector-in-aspnet-mvc/_static/image34.png)

<a id="css_color_picker"></a>
## <a name="using-the-css-color-picker"></a>CSS renk seçiciyi kullanma

Visual Studio 2012 ' deki CSS Düzenleyicisi, renkleri seçip eklemeyi kolaylaştıran bir renk seçicisine sahiptir. Renk Seçici standart bir renk paleti içerir, standart renk adlarını, karma kodları, RGB, RGBA, HSL ve HSLA renklerini destekler ve belgede en son kullandığınız renklerin bir listesini tutar.

Önceki bölümde `background-color` özelliğinin değerini değiştirdiniz. Renk seçiciyi çağırmak için, ekleme noktasını özellik adından sonra yerleştirin ve **#** ya da **RGB (** ) yazın.

![CSS Renk Seçici Çubuğu](using-page-inspector-in-aspnet-mvc/_static/image36.png)

Seçmek için bir renge tıklayın veya aşağı ok tuşuna basın, sonra renkler arasında çapraz geçiş yapmak için sol ve sağ ok tuşlarını kullanın. Bir rengi ziyaret ettiğinizde, karşılık gelen onaltılı değer önizlenebilir:

![arka plan rengi Özellik değeri önizlenen](using-page-inspector-in-aspnet-mvc/_static/image38.png)

Renk çubuğu tam istediğiniz renge sahip değilse, renk seçici açılır penceresini kullanabilirsiniz. Açmak için, renk çubuğunun sağ ucundaki çift köşeli çift ayraca tıklayın veya klavyede bir kez veya iki kez aşağı ok tuşuna basın.

![CSS Renk Seçici açılır menüsü](using-page-inspector-in-aspnet-mvc/_static/image40.png)

Sağ taraftaki dikey çubuktan bir renge tıklayın. Bu, ana penceredeki bu renk için bir gradyan gösterir. ENTER tuşuna basarak doğrudan dikey çubuktan bir renk seçin veya ana penceredeki herhangi bir noktaya tıklayarak daha fazla duyarlık seçin.

Bilgisayar ekranınızda kullanmak istediğiniz bir renk varsa (Visual Studio Kullanıcı arabirimi içinde olması gerekmez), sağ alt köşedeki Damlalık aracını kullanarak değerini yakalayabilirsiniz.

Ayrıca renk seçicinin alt kısmına kaydırıcıyı taşıyarak bir rengin saydamlığını değiştirebilirsiniz. Bunun yapılması, RGBA biçimi geçirgenliği temsil ettiğinden, renk değerlerini RGBA değerlerine dönüştürür.

Bir renk seçtikten sonra, ENTER tuşuna basın ve ardından *site. css* dosyasındaki arka plan rengi girişini tamamlamaya yönelik bir noktalı virgül yazın.

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a>Sayfa denetçisi güncelleştirme çubuğu

Sayfa denetçisi, *site. css* dosyasındaki değişikliği hemen algılar ve bir güncelleştirme çubuğunda bir uyarı görüntüler.

![Güncelleştirme çubuğu](using-page-inspector-in-aspnet-mvc/_static/image42.png)

Tüm dosyalarınızı kaydetmek ve sayfa denetçisi tarayıcısını yenilemek için CTRL + ALT + ENTER tuşlarına basın veya güncelleştirme çubuğuna tıklayın. Vurgu renginizdeki değişiklik tarayıcıda görüntülenir.

<a id="map_dynamic_elements"></a>
## <a name="mapping-dynamic-page-elements-to-javascript"></a>Dinamik sayfa öğelerini JavaScript 'e eşleme

Modern Web uygulamalarında, sayfadaki öğeler genellikle JavaScript ile dinamik olarak oluşturulur. Bu, Bu sayfa öğelerine karşılık gelen statik biçimlendirme (HTML ya da Razor) olmadığı anlamına gelir.

Sürüm 1,3 ile, sayfa denetçisi artık sayfaya otomatik olarak eklenen öğeleri ilgili JavaScript koduna geri eşleyebilir. Bu özelliği göstermek için [tek sayfalı uygulama (Spa) şablonunu](../../../single-page-application/overview/introduction/knockoutjs-template.md)kullanacağız.

> [!NOTE]
> SPA şablonu [ASP.NET and Web Tools 2012,2](https://go.microsoft.com/fwlink/?LinkId=282650) güncelleştirmesini gerektirir.

Visual Studio 'da **dosya** &gt; **Yeni proje**' yi seçin. Sol tarafta, **C#görsel**' i genişletin, **Web**' i seçin ve **ASP.net MVC4 Web uygulaması**' nı seçin. **Tamam**’a tıklayın.

**Yeni ASP.NET MVC 4 proje** Iletişim kutusunda **tek sayfalı uygulama**' yı seçin.

Çözüm Gezgini ' de, **Görünümler** klasörünü ve ardından **giriş** klasörünü genişletin. Index. cshtml dosyasına sağ tıklayın ve **sayfa denetçisinde görüntüle**' yi seçin.

Sayfa denetçisi tarayıcısında görüntülenen ilk şey bir oturum açma sayfasıdır. "Kaydolun" a tıklayın ve bir Kullanıcı adı ve parola oluşturun. Kaydolduktan sonra uygulama oturumunuzu açar ve bazı örnek öğelerle bir yapılacaklar listesi oluşturur.

Inceleme moduna sayfa denetçisi koymak için **Denetle** ' ye tıklayın. Sayfa denetçisi tarayıcısında, yapılacaklar öğelerinden birine tıklayın. Mavi renkle vurgulanacak, öğe adının yanında "JS" ile Turuncu renkle vurgulandığına dikkat edin. Bu, öğesinin betik aracılığıyla dinamik olarak oluşturulduğunu belirtir.

![](using-page-inspector-in-aspnet-mvc/_static/image44.png)

Ayrıca, **çağrı yığını** sekmesinde turuncu bir alt çizgi görünür. Bu, **çağrı yığını** bölmesinin öğesi hakkında daha fazla bilgi olduğunu gösterir.

**Çağrı yığını** sekmesine tıklayın. **Çağrı yığını** bölmesi, öğesini oluşturan JavaScript çağrısının çağrı yığınını gösterir. JQuery gibi dış kitaplıklara yapılan çağrılar daraltılır, böylece uygulama betiğe yönelik çağrıları kolayca görebilirsiniz.

![](using-page-inspector-in-aspnet-mvc/_static/image46.png)

Dış kitaplıklara yapılan çağrılar dahil olmak üzere tam yığını görmek için, "dış kitaplıklar" etiketli düğümleri genişletebilirsiniz:

![](using-page-inspector-in-aspnet-mvc/_static/image48.png)

Çağrı yığınında bir öğeye tıklarsanız, Visual Studio kod dosyasını açar ve ilgili betiği vurgular.

![](using-page-inspector-in-aspnet-mvc/_static/image50.png)

## <a name="see-also"></a>Ayrıca Bkz.

[Visual Studio ile ASP.NET MVC 4 ' e giriş](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (ASP.NET Web sitesi)

[Sayfa denetçisi Ile tanışın](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/) (Channel 9 Videosu)

[Sayfa denetçisi hata iletileri](https://go.microsoft.com/?linkid=9813062) (MSDN)
